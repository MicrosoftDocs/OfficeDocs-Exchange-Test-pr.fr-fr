---
title: 'Référence d’autorisations pour le déploiement d’Exchange 2013: Exchange 2013 Help'
TOCTitle: Référence d’autorisations pour le déploiement d’Exchange 2013
ms:assetid: b13412d0-0cc4-4c1d-bf31-cae3d3e211a9
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Ee681663(v=EXCHG.150)
ms:contentKeyID: 59634344
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Référence d’autorisations pour le déploiement d’Exchange 2013

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2016-12-09_

Cette rubrique décrit les autorisations nécessaires pour configurer une organisation Microsoft Exchange Server 2013. Les groupes de sécurité universels qui sont associés aux groupes de rôles de gestion, et autres groupes et principaux de sécurité Windows sont ajoutés aux listes de contrôle d'accès (ACL) de divers objets Active Directory. Les listes de contrôle d'accès déterminent les opérations qui peuvent être réalisées sur chaque objet. En comprenant les autorisations accordées à chaque groupe de rôles, groupe de sécurité ou principal de sécurité, vous pouvez déterminer les autorisations minimales requises pour installer Exchange 2013.

Dans certains cas, la liste de contrôle d'accès n'est pas appliquée à la propriété habituelle, **ntSecurityDescriptor**, mais à une autre telle que **msExchMailboxSecurityDescriptor**. Le service d'annuaire ne peut pas appliquer une sécurité non spécifiée dans le descripteur de sécurité de Windows. Dans la plupart des cas, ces listes de contrôle d'accès sont répliquées par le service de banque d'informations pour les stocker sur des objets appropriés. Cependant, il n'existe aucun outil permettant d'afficher ces listes de contrôle d'accès autrement que sous la forme de données binaires brutes.

Les colonnes d'un tableau d'autorisations contiennent les informations suivantes :

  - **Compte**   Principal de sécurité auquel les autorisations sont accordées ou refusées

  - **Type d'ACE**   Type d'entrée de contrôle d'accès (ACE)
    
      - **ACE Autoriser**   Une entrée de contrôle d'accès autoriser permet à l'utilisateur ou au groupe qui y est associé d'accéder à un élément.
    
      - **ACE Refuser**   Une entrée de contrôle d'accès refuser empêche l'utilisateur ou le groupe qui y est associé d'accéder à un élément.

  - **Héritage**   Type d'héritage utilisé pour les objets enfants.
    
      - **Tous** Indique que les autorisations s'appliquent à l'objet et tous les sous-objets.
    
      - **Desc** Indique que les autorisations s’appliquent à la classe d’objets indiquée dans la ligne Sur propriété/S’applique à.
    
      - **Aucun** Indique que ces autorisations ne s'appliquent qu'à l'objet.

  - **Autorisations**   Autorisations octroyées au compte.

  - **Sur propriété/S'applique à**   Dans certains cas, les autorisations s'appliquent uniquement à une propriété, un jeu de propriétés ou une classe d'objets donnés. Ces autorisations limitées sont spécifiées ici.

  - **Commentaires**   Le cas échéant, cette colonne explique pourquoi des autorisations sont requises ou fournit d'autres informations sur les autorisations.

Les autorisations sont généralement répertoriées dans le tableau selon les noms utilisés dans la page de propriétés **Sécurité** d'ADSI (Active Directory Service Interfaces) Edit (AdsiEdit.msc), vue **Avancé** sous l'onglet **Afficher/Modifier**. La page des propriétés **Sécurité** d'ADSI Edit offre une vue beaucoup plus condensée des autorisations. L'outil LDP (Ldp.exe) affiche le masque d'accès directement sous la forme d'une valeur numérique. Le code d'installation se réfère aux autorisations par constantes prédéfinies.

Le tableau suivant présente les relations entres ces valeurs.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Page Résumé d'ADSI Edit</th>
<th>Vue Avancée d'ADSI Edit, onglet Afficher/Modifier</th>
<th>Entrées de liste de contrôle d'accès appliquées à un objet donné</th>
<th>Valeur binaire (masque d'accès dans LDP)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Contrôle total</p></td>
<td><p>Contrôle total</p></td>
<td><p><code>WRITE_OWNER | WRITE_DAC | READ_CONTROL | DELETE | ACTRL_DS_CONTROL_ACCESS | ACTRL_DS_LIST_OBJECT | ACTRL_DS_DELETE_TREE | ACTRL_DS_WRITE_PROP | ACTRL_DS_READ_PROP | ACTRL_DS_SELF | ACTRL_DS_LIST | ACTRL_DS_DELETE_CHILD | ACTRL_DS_CREATE_CHILD</code></p></td>
<td><p><code>0x000F01FF</code></p></td>
</tr>
<tr class="even">
<td><p>Lecture</p></td>
<td><p>Contenu de la liste + Lire toutes les propriétés + Autorisations de lecture</p></td>
<td><p><code>ACTRL_DS_LIST | ACTRL_DS_READ_PROP | READ_CONTROL</code></p></td>
<td><p><code>0x00020014</code></p></td>
</tr>
<tr class="odd">
<td><p>Écriture</p></td>
<td><p>Écrire toutes les propriétés + Toutes les écritures validées</p></td>
<td><p><code>ACTRL_DS_WRITE_PROP | ACTRL_DS_SELF</code></p></td>
<td><p><code>0x00000028</code></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Contenu de la liste</p></td>
<td><p><code>ACTRL_DS_LIST</code></p></td>
<td><p><code>0x00000004</code></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>Lire toutes les propriétés</p></td>
<td><p><code>ACTRL_DS_READ_PROP</code></p></td>
<td><p><code>0x00000010</code></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Écrire toutes les propriétés</p></td>
<td><p><code>ACTRL_DS_WRITE_PROP</code></p></td>
<td><p><code>0x00000020</code></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>Suppression</p></td>
<td><p><code>DELETE</code></p></td>
<td><p><code>0x00010000</code></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Supprimer sous-arborescence</p></td>
<td><p><code>ACTRL_DS_DELETE_TREE</code></p></td>
<td><p><code>0x00000040</code></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>Autorisations de lecture</p></td>
<td><p><code>READ_CONTROL</code></p></td>
<td><p><code>0x00020000</code></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Modifier autorisations</p></td>
<td><p><code>WRITE_DAC</code></p></td>
<td><p><code>0x00040000</code></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>Modifier propriétaire</p></td>
<td><p><code>WRITE_OWNER</code></p></td>
<td><p><code>0x00080000</code></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Toutes les écritures validées</p></td>
<td><p><code>ACTRL_DS_SELF</code></p></td>
<td><p><code>0x00000008</code></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>Tous les droits étendus</p></td>
<td><p><code>ACTRL_DS_CONTROL_ACCESS</code></p></td>
<td><p><code>0x00000100</code></p></td>
</tr>
<tr class="even">
<td><p>Créer tous les objets enfants</p></td>
<td><p>Créer tous les objets enfants</p></td>
<td><p><code>ACTRL_DS_CREATE_CHILD</code></p></td>
<td><p><code>0x00000001</code></p></td>
</tr>
<tr class="odd">
<td><p>Supprimer tous les objets enfants</p></td>
<td><p>Supprimer tous les objets enfants</p></td>
<td><p><code>ACTRL_DS_DELETE_CHILD</code></p></td>
<td><p><code>0x00000002</code></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p></p></td>
<td><p><code>ACTRL_DS_LIST_OBJECT</code></p></td>
<td><p><code>0x00000080</code></p></td>
</tr>
</tbody>
</table>


Les droits étendus sont des droits personnalisés définis par des applications individuelles. Ils sont spécifiés dans la liste de contrôle d'accès. Toutefois, ils n'ont pas de signification pour Active Directory. L’application spécifique applique tous les droits étendus. « Créer un dossier public » ou « Créer des propriétés nommées dans la banque d'informations » sont des exemples de droits Exchange étendus.

Pour plus d’informations sur les autorisations définies durant une installation de Microsoft Exchange Server 2010, voir la rubrique [Référence d’autorisations de déploiement d’Exchange 2010](https://go.microsoft.com/fwlink/p/?linkid=402924).

## Préparation des autorisations Active Directory

Les tableaux d'autorisations contenus dans cette section répertorient les autorisations qui sont définies lors de l'exécution de la commande `Setup /PrepareAD`.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Les autorisations décrites dans cette section sont les autorisations par défaut qui sont configurées lorsque vous déployez Exchange 2013 avec le modèle d’autorisations partagées. Si vous avez déployé Exchange 2013 avec le modèle d’autorisations divisées Active Directory, les autorisations par défaut sont différentes. Pour plus d’informations sur les modifications apportées aux autorisations par défaut lors de l’utilisation des autorisations divisées Active Directory et des modèles d’autorisations divisées et partagées en général, voir <a href="understanding-split-permissions-exchange-2013-help.md">Active Directory split permissions</a> dans <a href="understanding-split-permissions-exchange-2013-help.md">Présentation des autorisations fractionnées</a>. Si vous choisissez de ne pas utiliser les autorisations divisées Active Directory lorsque vous installez Exchange, Exchange utilisera les autorisations partagées.</td>
</tr>
</tbody>
</table>


## Autorisations du conteneur Microsoft Exchange

Le tableau suivant présente les autorisations définies sur le conteneur Microsoft Exchange dans la partition de configuration.

### Nom unique de l’objet : CN=Microsoft Exchange,CN=Services,CN=Configuration,DC=\<domaine\>

<table style="width:100%;">
<colgroup>
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
</colgroup>
<thead>
<tr class="header">
<th>Compte</th>
<th>Type d’ACE</th>
<th>Héritage</th>
<th>Autorisations</th>
<th>Sur propriété/S’applique à</th>
<th>Commentaires</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Compte d'installation</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Contrôle total</p></td>
<td><p></p></td>
<td><p>Ce compte est utilisé pour exécuter <code>/PrepareAD</code>.</p></td>
</tr>
<tr class="even">
<td><p>Gestion de l'organisation</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Contrôle total</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Sous-système approuvé Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Contrôle total</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Serveurs Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Lecture</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Utilisateurs authentifiés</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Aucun</p></td>
<td><p>Propriété de lecture</p>
<p>Contenu de la liste</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Sous-système approuvé Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Modifier les autorisations</p></td>
<td><p>msExchSmtpRceiveConnector</p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Gestion des dossiers publics</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Lecture</p>
<p>Objet de liste</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Installation déléguée</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Lecture</p>
<p>Objet de liste</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


## Autorisations du conteneur du service Microsoft Exchange Autodiscover

Le tableau suivant répertorie les autorisations qui sont définies sur le conteneur de découverte automatique de Microsoft Exchange dans la partition de configuration.

### Nom unique de l’objet : CN=Microsoft Exchange Autodiscover,CN=Services,CN=Configuration,DC=\<domaine\>

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>Compte</th>
<th>Type d’ACE</th>
<th>Héritage</th>
<th>Autorisations</th>
<th>Sur propriété/S’applique à</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Serveurs Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Lecture</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


## Autorisations du conteneur d'organisation Microsoft Exchange

Les tableaux d’autorisations contenus dans cette section répertorient les autorisations qui sont définies sur l’organisation Microsoft Exchange et les sous-conteneurs dans la partition de configuration.

### Nom unique de l’objet : CN=\<organisation\>,CN=Microsoft Exchange,CN=Services,CN=Configuration,DC=\<domaine\>

<table style="width:100%;">
<colgroup>
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
</colgroup>
<thead>
<tr class="header">
<th>Compte(s)</th>
<th>Type d’ACE</th>
<th>Héritage</th>
<th>Autorisations</th>
<th>Sur propriété/S’applique à</th>
<th>Commentaires</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Administrateurs d'entreprise</p>
<p>Administrateurs de domaine racine</p>
<p>Compte d’installation</p>
<p>Gestion de l’organisation</p></td>
<td><p>ACE Refuser</p></td>
<td><p>Tout</p></td>
<td><p>Envoyer en tant que</p>
<p>Recevoir en tant que</p></td>
<td><p></p></td>
<td><p>Les administrateurs Windows ne sont pas autorisés à ouvrir les boîtes aux lettres.</p></td>
</tr>
<tr class="even">
<td><p>Administrateurs d’entreprise</p>
<p>Administrateurs de schéma</p>
<p>Administrateurs de domaine racine</p>
<p>Compte d’installation</p>
<p>Gestion de l’organisation</p></td>
<td><p>ACE Refuser</p></td>
<td><p>Tout</p></td>
<td><p>Emprunt d’identité des services Web Exchange</p>
<p>Sérialisation de jeton de services Web Exchange</p></td>
<td><p></p></td>
<td><p>Droit étendu</p></td>
</tr>
<tr class="odd">
<td><p>Administrateurs d’entreprise</p>
<p>Administrateurs de schéma</p>
<p>Administrateurs de domaine racine</p>
<p>Compte d’installation</p></td>
<td><p>ACE Refuser</p></td>
<td><p>Tout</p></td>
<td><p>Stockage d’accès de transport</p>
<p>Stockage de délégation contrainte</p>
<p>Stockage d'accès en lecture</p>
<p>Stockage d'accès en lecture/écriture</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Système local</p></td>
<td><p>Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Tous les droits étendus</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Utilisateurs authentifiés</p></td>
<td><p>ACE Refuser</p></td>
<td><p>Desc</p></td>
<td><p>Propriété de lecture</p></td>
<td><p><code>msExchAvailabilityUserPassword / msExchAvailabilityAddressSpace</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Utilisateurs authentifiés</p></td>
<td><p>Autoriser</p></td>
<td><p>Aucun</p></td>
<td><p>Lecture</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Gestion de l’organisation</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Autorisations de lecture</p>
<p>Contenu de la liste</p>
<p>Propriété de lecture</p>
<p>Objet de liste</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Gestion des dossiers publics</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Autorisations de lecture</p>
<p>Contenu de la liste</p>
<p>Propriété de lecture</p>
<p>Objet de liste</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Autorité NT\Service réseau</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Lecture</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Serveurs de disponibilité gérés</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Autorisations de lecture</p>
<p>Contenu de la liste</p>
<p>Propriété de lecture</p>
<p>Objet de liste</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Serveurs Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Tous les droits étendus</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Serveurs Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Propriété d’écriture</p></td>
<td><p><code>groupType</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Serveurs Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Propriété d’écriture</p></td>
<td><p><code>msExchOwningServer</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Serveurs Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Propriété d’écriture</p></td>
<td><p><code>msExchMailboxSecurityDescriptor</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Serveurs Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Propriété d’écriture</p></td>
<td><p><code>msExchUMServerWritableFlags</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Serveurs Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Propriété d’écriture</p></td>
<td><p><code>msExchDatabaseCreated</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Serveurs Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Propriété d’écriture</p></td>
<td><p><code>msExchUserCulture</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Serveurs Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Propriété d’écriture</p></td>
<td><p><code>msExchMobileMailboxFlags</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Serveurs Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Propriété d’écriture</p></td>
<td><p><code>siteFolderGUID</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Serveurs Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Propriété d’écriture</p></td>
<td><p><code>siteFolderServer</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Serveurs Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Propriété d’écriture</p></td>
<td><p><code>msExchEDBOffline</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Serveurs Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Propriété d’écriture</p></td>
<td><p><code>userCertificate</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Serveurs Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Propriété d’écriture</p></td>
<td><p><code>msExchUMDtmfMap</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Serveurs Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Propriété d’écriture</p></td>
<td><p><code>msExchBlockedSendersHash</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Serveurs Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Propriété d’écriture</p></td>
<td><p><code>Personal Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Serveurs Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Propriété d’écriture</p></td>
<td><p><code>Public Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Serveurs Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Propriété d’écriture</p></td>
<td><p><code>Exchange Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Serveurs Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Propriété d’écriture</p></td>
<td><p><code>msExchPatchMDB</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Serveurs Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Propriété d’écriture</p></td>
<td><p><code>publicDelegates</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Serveurs Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Propriété d’écriture</p></td>
<td><p><code>msExchUMSpokenName</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Serveurs Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Propriété d’écriture</p></td>
<td><p><code>msExchUMPinChecksum</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Serveurs Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Propriété d’écriture</p></td>
<td><p><code>legacyExchangeDN</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Serveurs Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Propriété d’écriture</p></td>
<td><p><code>msExchSafeSendersHash</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Serveurs Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Propriété d’écriture</p></td>
<td><p><code>thumbnailPhoto</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Gestion de l’organisation</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Créer un dossier public de niveau supérieur</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Gestion des dossiers publics</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Créer un dossier public de niveau supérieur</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Gestion de l’organisation</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Afficher l’état de la banque d’informations</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Gestion des dossiers publics</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Afficher l’état de la banque d’informations</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Gestion de l’organisation</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Administrer la banque d’informations</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Gestion des dossiers publics</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Administrer la banque d’informations</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Gestion de l’organisation</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Créer des propriétés nommées dans la banque d’informations</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Gestion des dossiers publics</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Créer des propriétés nommées dans la banque d’informations</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Gestion de l’organisation</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Modifier la liste de contrôle d’accès des dossiers publics</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Gestion des dossiers publics</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Modifier la liste de contrôle d’accès des dossiers publics</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Gestion de l’organisation</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Modifier les quotas de dossiers publics</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Gestion des dossiers publics</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Modifier les quotas de dossiers publics</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Gestion de l’organisation</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Modifier la liste de contrôle d’accès d’administration des dossiers publics</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Gestion des dossiers publics</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Modifier la liste de contrôle d’accès d’administration des dossiers publics</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Gestion de l’organisation</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Modifier l’expiration des dossiers publics</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Gestion des dossiers publics</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Modifier l’expiration des dossiers publics</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Gestion de l’organisation</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Modifier la liste de réplicas des dossiers publics</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Gestion des dossiers publics</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Modifier la liste de réplicas des dossiers publics</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Gestion de l’organisation</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Modifier la rétention des éléments supprimés des dossiers publics</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Gestion des dossiers publics</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Modifier la rétention des éléments supprimés des dossiers publics</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Gestion de l’organisation</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Créer un dossier public</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Gestion des dossiers publics</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Créer un dossier public</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Gestion des dossiers publics</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Dossier public à extension messagerie</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Tout le monde</p>
<p>Autorité NT\Connexion anonyme</p>
<p></p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Créer des propriétés nommées dans la banque d’informations</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Tout le monde</p>
<p>Autorité NT\Connexion anonyme</p>
<p></p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Créer un dossier public</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Tout le monde</p>
<p>Autorité NT\Connexion anonyme</p>
<p></p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Desc</p></td>
<td><p>Autorisations de lecture</p>
<p>Contenu de la liste</p>
<p>Propriété de lecture</p>
<p>Objet de liste</p></td>
<td><p><code>/ msExchPrivateMDB</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Tout le monde</p>
<p>Autorité NT\Connexion anonyme</p>
<p></p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Desc</p></td>
<td><p>Autorisations de lecture</p>
<p>Contenu de la liste</p>
<p>Propriété de lecture</p>
<p>Objet de liste</p></td>
<td><p><code>/ msExchPublicMDB</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Serveurs Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Desc</p></td>
<td><p>Autorisations de lecture</p>
<p>Contenu de la liste</p>
<p>Propriété de lecture</p>
<p>Objet de liste</p></td>
<td><p><code>/ siteAddressing</code></p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


### Nom unique de l’objet : CN=Toutes les listes d’adresses,CN=Conteneur de listes d’adresses,CN=\<organisation\>

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>Compte</th>
<th>Type d’ACE</th>
<th>Héritage</th>
<th>Autorisations</th>
<th>Sur propriété/S’applique à</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Utilisateurs authentifiés</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Contenu de la liste</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Gestion de l’organisation</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Propriété d’écriture</p></td>
<td><p><code>msExchLastAppliedRecipientFilter</code></p>
<p><code>msExchRecipientFilterFlags</code></p></td>
</tr>
<tr class="odd">
<td><p>Gestion des dossiers publics</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Propriété d’écriture</p></td>
<td><p><code>msExchLastAppliedRecipientFilter</code></p>
<p><code>msExchRecipientFilterFlags</code></p></td>
</tr>
</tbody>
</table>


### Nom unique de l’objet : CN=Listes d’adresses en mode hors connexion,CN=Conteneur de liste d’adresses, CN=\<organisation\>

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>Compte</th>
<th>Type d’ACE</th>
<th>Héritage</th>
<th>Autorisations</th>
<th>Sur propriété/S’applique à</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Utilisateurs authentifiés</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Téléchargement du carnet d'adresses en mode hors connexion</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


### Nom unique de l’objet : CN=Adressage,CN=\<organisation\>

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>Compte</th>
<th>Type d’ACE</th>
<th>Héritage</th>
<th>Autorisations</th>
<th>Sur propriété/S’applique à</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Utilisateurs authentifiés</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Lecture</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


### Nom unique de l’objet : CN=Stratégies de destinataire,CN=\<organisation\>

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>Compte</th>
<th>Type d’ACE</th>
<th>Héritage</th>
<th>Autorisations</th>
<th>Sur propriété/S’applique à</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Gestion de l’organisation</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Propriété d’écriture</p></td>
<td><p><code>msExchLastAppliedRecipientFilter</code></p>
<p><code>msExchRecipientFilterFlags</code></p></td>
</tr>
<tr class="even">
<td><p>Gestion des dossiers publics</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Propriété d’écriture</p></td>
<td><p><code>msExchLastAppliedRecipientFilter</code></p>
<p><code>msExchRecipientFilterFlags</code></p></td>
</tr>
</tbody>
</table>


## Autorisations du conteneur de partition de configuration

Les tableaux d'autorisations contenus dans cette section répertorient les autorisations qui sont définies par la commande `Setup /PrepareAD` sur plusieurs sous-conteneurs de la partition de configuration.

### Nom unique de l’objet : CN=Sites,CN=Configuration,DC=\<domaine\>

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>Compte</th>
<th>Type d’ACE</th>
<th>Héritage</th>
<th>Autorisations</th>
<th>Sur propriété/S’applique à</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Gestion de l’organisation</p>
<p>Sous-système approuvé Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Propriété d’écriture</p></td>
<td><p><code>msExchVersion / site</code></p></td>
</tr>
<tr class="even">
<td><p>Gestion de l’organisation</p>
<p>Sous-système approuvé Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Propriété d’écriture</p></td>
<td><p><code>msExchVersion / site-link</code></p></td>
</tr>
<tr class="odd">
<td><p>Gestion de l’organisation</p>
<p>Sous-système approuvé Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Propriété d’écriture</p></td>
<td><p><code>msExchPartnerId / site</code></p></td>
</tr>
<tr class="even">
<td><p>Gestion de l’organisation</p>
<p>Sous-système approuvé Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Propriété d’écriture</p></td>
<td><p><code>msExchMinorPartnerId / site</code></p></td>
</tr>
<tr class="odd">
<td><p>Gestion de l’organisation</p>
<p>Sous-système approuvé Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Propriété d’écriture</p></td>
<td><p><code>msExchResponsibleforSites / site</code></p></td>
</tr>
<tr class="even">
<td><p>Gestion de l’organisation</p>
<p>Sous-système approuvé Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p></p></td>
<td><p>Propriété d’écriture</p></td>
<td><p><code>msExchTransportSiteFlags / site</code></p></td>
</tr>
<tr class="odd">
<td><p>Gestion de l’organisation</p>
<p>Sous-système approuvé Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Propriété d’écriture</p></td>
<td><p><code>msExchCost / site-link</code></p></td>
</tr>
<tr class="even">
<td><p>Gestion de l’organisation</p>
<p>Sous-système approuvé Exchange</p>
<p>Système local</p>
<p>Serveurs Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Desc</p></td>
<td><p>Autorisations de lecture</p>
<p>Contenu de la liste</p>
<p>Propriété de lecture</p>
<p>Objet de liste</p></td>
<td><p><code>/ msExchEdgeSyncEHFConnector</code></p></td>
</tr>
<tr class="odd">
<td><p>Gestion de l’organisation</p>
<p>Sous-système approuvé Exchange</p>
<p>Système local</p>
<p>Serveurs Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Desc</p></td>
<td><p>Autorisations de lecture</p>
<p>Contenu de la liste</p>
<p>Propriété de lecture</p>
<p>Objet de liste</p></td>
<td><p><code>/ msExchEdgeSyncMservConnector</code></p></td>
</tr>
<tr class="even">
<td><p>Gestion de l’organisation</p>
<p>Sous-système approuvé Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Enfants</p></td>
<td><p>Créer un enfant</p>
<p>Supprimer l’enfant</p>
<p>Supprimer l’arborescence</p></td>
<td><p><code>msExchEdgeSyncServiceConfig / site</code></p></td>
</tr>
<tr class="odd">
<td><p>Gestion de l’organisation</p>
<p>Sous-système approuvé Exchange</p>
<p>Système local</p>
<p>Serveurs Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Desc</p></td>
<td><p>Autorisations de lecture</p>
<p>Contenu de la liste</p>
<p>Propriété de lecture</p>
<p>Objet de liste</p></td>
<td><p><code>/ msExchEdgeSyncServiceConfig</code></p></td>
</tr>
<tr class="even">
<td><p>Gestion de l’organisation</p>
<p>Sous-système approuvé Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Enfants</p></td>
<td><p>Créer un enfant</p>
<p>Supprimer l’enfant</p>
<p>Supprimer l’arborescence</p></td>
<td><p><code>msExchEdgeSyncMservConnector / msExchEdgeSyncServiceConfig</code></p></td>
</tr>
<tr class="odd">
<td><p>Gestion de l’organisation</p>
<p>Sous-système approuvé Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Enfants</p></td>
<td><p>Créer un enfant</p>
<p>Supprimer l’enfant</p>
<p>Supprimer l’arborescence</p></td>
<td><p><code>msExchEdgeSyncEHFConnector / msExchEdgeSyncServiceConfig</code></p></td>
</tr>
</tbody>
</table>


### Nom unique de l’objet : CN=Objets supprimés,CN=Configuration,DC=\<domaine\>

<table style="width:100%;">
<colgroup>
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
</colgroup>
<thead>
<tr class="header">
<th>Compte</th>
<th>Type d’ACE</th>
<th>Héritage</th>
<th>Autorisations</th>
<th>Sur propriété/S’applique à</th>
<th>Commentaires</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Serveurs Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Contenu de la liste</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Administration de l'organisation</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Lecture</p>
<p>Objet de liste</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Compte d’installation</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Autorisation de lecture</p>
<p>Autorisation d'écriture</p>
<p>Contenu de la liste</p>
<p>Propriété de lecture</p>
<p>Objet de liste</p></td>
<td><p></p></td>
<td><p>Ce compte est utilisé pour exécuter <code>/PrepareAD</code>.</p></td>
</tr>
<tr class="even">
<td><p>Sous-système approuvé Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Lecture</p>
<p>Objet de liste</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Service réseau</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Contenu de la liste</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


## Autorisations du groupe d'administration Exchange

La commande `Setup /PrepareAD` configure également les autorisations suivantes pour les groupes d'administration au sein de l'organisation.

### Nom unique de l’objet : CN=\<groupe d’administration\>,CN=Groupes d’administration,CN=\<organisation\>

<table style="width:100%;">
<colgroup>
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
</colgroup>
<thead>
<tr class="header">
<th>Compte</th>
<th>Type d’ACE</th>
<th>Héritage</th>
<th>Autorisations</th>
<th>Sur propriété/S’applique à</th>
<th>Commentaires</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Gestion de l’organisation</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Desc</p></td>
<td><p>Service de mise à jour de destinataire d’accès</p></td>
<td><p><code>msExchExchangeServer</code></p></td>
<td><p>Autorise les administrateurs des destinataires Exchange à marquer des destinataires à l’aide d’informations sur l’adresse proxy.</p></td>
</tr>
<tr class="even">
<td><p>Système local</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Desc</p></td>
<td><p>Service de mise à jour de destinataire d’accès</p></td>
<td><p><code>msExchExchangeServer</code></p></td>
<td><p>Autorise les serveurs à marquer des destinataires à l'aide d'informations sur l'adresse proxy.</p></td>
</tr>
<tr class="odd">
<td><p>Gestion des dossiers publics</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Desc</p></td>
<td><p>Service de mise à jour de destinataire d’accès</p></td>
<td><p><code>msExchExchangeServer</code></p></td>
<td><p>Autorise les administrateurs de dossiers publics Exchange à marquer des destinataires à l’aide d’informations sur l’adresse proxy.</p></td>
</tr>
</tbody>
</table>


### Nom unique de l’objet : CN=Paramètres de sécurité avancés,CN=\<groupe d’administration\>,CN=Groupes d’administration,CN=\<organisation\>

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>Compte</th>
<th>Type d’ACE</th>
<th>Héritage</th>
<th>Autorisations</th>
<th>Sur propriété/S’applique à</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Utilisateurs authentifiés</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Aucun</p></td>
<td><p>Contenu de la liste</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


### Nom unique de l’objet : CN=Chiffrement,CN=Paramètres de sécurité avancés,CN=\<groupe d’administration\>,CN=Groupes d’administration,CN=\<organisation\>

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>Compte</th>
<th>Type d’ACE</th>
<th>Héritage</th>
<th>Autorisations</th>
<th>Sur propriété/S’applique à</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Utilisateurs authentifiés</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Aucun</p></td>
<td><p>Propriété de lecture</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


### Nom unique de l’objet : CN=Baies,CN=\<groupe d’administration\>,CN=Groupes d’administration,CN=\<organisation\>

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>Compte</th>
<th>Type d’ACE</th>
<th>Héritage</th>
<th>Autorisations</th>
<th>Sur propriété/S’applique à</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Utilisateurs authentifiés</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Aucun</p></td>
<td><p>Contenu de la liste</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


### Nom unique de l’objet : CN=Groupes de disponibilité de base de données,CN=\<groupe d’administration\>,CN=Groupes d’administration,CN=\<organisation\>

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>Compte</th>
<th>Type d’ACE</th>
<th>Héritage</th>
<th>Autorisations</th>
<th>Sur propriété/S’applique à</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Utilisateurs authentifiés</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Aucun</p></td>
<td><p>Contenu de la liste</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


### Nom unique de l’objet : CN=Bases de données,CN=\<groupe d’administration\>,CN=Groupes d’administration,CN=\<organisation\>

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>Compte</th>
<th>Type d’ACE</th>
<th>Héritage</th>
<th>Autorisations</th>
<th>Sur propriété/S’applique à</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Utilisateurs authentifiés</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Aucun</p></td>
<td><p>Contenu de la liste</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


### Nom unique de l’objet : CN=Serveurs,CN=\<groupe d’administration\>,CN=Groupes d’administration,CN=\<organisation\>

<table style="width:100%;">
<colgroup>
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
</colgroup>
<thead>
<tr class="header">
<th>Compte</th>
<th>Type d’ACE</th>
<th>Héritage</th>
<th>Autorisations</th>
<th>Sur propriété/S’applique à</th>
<th>Commentaires</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Serveurs Exchange</p></td>
<td><p>ACE Refuser</p></td>
<td><p>Tout</p></td>
<td><p>Recevoir en tant que</p></td>
<td><p></p></td>
<td><p>Les serveurs Exchange ne sont pas autorisés à ouvrir les boîtes aux lettres.</p></td>
</tr>
<tr class="even">
<td><p>Utilisateurs authentifiés</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Aucun</p></td>
<td><p>Contenu de la liste</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


## Autorisations du conteneur de groupes de sécurité Microsoft Exchange

Les tableaux d’autorisations contenus dans cette section répertorient les autorisations qui sont définies pour le conteneur de groupes de sécurité Microsoft Exchange dans la partition du domaine racine.

### Nom unique de l’objet : OU=Groupes de sécurité Microsoft Exchange,DC=\<domaine racine\>

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>Compte</th>
<th>Type d’ACE</th>
<th>Héritage</th>
<th>Autorisations</th>
<th>Sur propriété/S’applique à</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Gestion de l’organisation</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Contrôle total</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Sous-système approuvé Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Créer un enfant</p></td>
<td><p><code>/ Group</code></p></td>
</tr>
<tr class="odd">
<td><p>Sous-système approuvé Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Desc</p></td>
<td><p>Supprimer</p></td>
<td><p><code>/ group</code></p></td>
</tr>
<tr class="even">
<td><p>Sous-système approuvé Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Desc</p></td>
<td><p>Propriété d’écriture</p></td>
<td><p><code>Member / group</code></p></td>
</tr>
</tbody>
</table>


### Nom unique de l’objet : CN=Gestion de l’organisation,OU=Groupes de sécurité Microsoft Exchange,DC=\<domaine racine\>

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>Compte</th>
<th>Type d’ACE</th>
<th>Héritage</th>
<th>Autorisations</th>
<th>Sur propriété/S’applique à</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Gestion de l’organisation</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Contrôle total</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


### Nom unique de l’objet : CN=Gestion de dossiers publics, OU=Groupes de sécurité de Microsoft Exchange, DC=\<domaine racine\>

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>Compte</th>
<th>Type d’ACE</th>
<th>Héritage</th>
<th>Autorisations</th>
<th>Sur propriété/S’applique à</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Gestion de l’organisation</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Contrôle total</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


### Nom unique de l’objet : CN=ExchangeLegacyInterop,OU=Groupes de sécurité Microsoft Exchange,DC=\<domaine racine\>

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>Compte</th>
<th>Type d’ACE</th>
<th>Héritage</th>
<th>Autorisations</th>
<th>Sur propriété/S’applique à</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Gestion de l’organisation</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Contrôle total</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


### Nom unique de l’objet : CN=Serveurs Exchange,OU=Groupes de sécurité Microsoft Exchange,DC=\<domaine racine\>

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>Compte</th>
<th>Type d’ACE</th>
<th>Héritage</th>
<th>Autorisations</th>
<th>Sur propriété/S’applique à</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Gestion de l’organisation</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Contrôle total</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Administrateurs de domaine racine</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Membres autorisés à lire</p>
<p>Membres autorisés à écrire</p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Administrateurs de domaine enfant</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Membres autorisés à lire</p>
<p>Membres autorisés à écrire</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


## Préparation du domaine

Les tableaux suivants répertorient les autorisations qui sont définies lors de l'exécution de la commande `Setup /PrepareDomain`.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Les autorisations décrites dans cette section sont les autorisations par défaut qui sont configurées lorsque vous déployez Exchange 2013 avec le modèle d’autorisations partagées. Si vous avez déployé Exchange 2013 avec le modèle d’autorisations divisées Active Directory, les autorisations par défaut sont différentes. Pour plus d’informations sur les modifications apportées aux autorisations par défaut lors de l’utilisation des autorisations divisées Active Directory et des modèles d’autorisations divisées et partagées en général, voir <a href="understanding-split-permissions-exchange-2013-help.md">Active Directory split permissions</a> dans <a href="understanding-split-permissions-exchange-2013-help.md">Présentation des autorisations fractionnées</a>. Si vous choisissez de ne pas utiliser les autorisations divisées Active Directory lorsque vous installez Exchange, Exchange utilisera les autorisations partagées.</td>
</tr>
</tbody>
</table>


### Nom unique de l’objet : DC=\<domaine\>

<table style="width:100%;">
<colgroup>
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
</colgroup>
<thead>
<tr class="header">
<th>Compte</th>
<th>Type d’ACE</th>
<th>Héritage</th>
<th>Autorisations</th>
<th>Sur propriété/S’applique à</th>
<th>Commentaires</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Utilisateurs authentifiés</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Propriété de lecture</p></td>
<td><p><code>Exchange Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>AUTORITÉ NT\RÉSEAU</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Propriété de lecture</p></td>
<td><p><code>Exchange Personal Information</code></p></td>
<td><p>Accorde des autorisations de lecture du service de transport.</p></td>
</tr>
<tr class="odd">
<td><p>Serveurs Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Propriété d’écriture</p></td>
<td><p><code>groupType</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Serveurs Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Propriété d’écriture</p></td>
<td><p><code>msExchMailboxSecurityDescriptor</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Serveurs Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Propriété d’écriture</p></td>
<td><p><code>msExchUMServerWritableFlags</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Serveurs Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Propriété de lecture</p></td>
<td><p><code>Exchange Personal Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Serveurs Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Propriété de lecture</p></td>
<td><p><code>Exchange Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Serveurs Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Propriété d’écriture</p></td>
<td><p><code>msExchUserCultulre</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Serveurs Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Propriété de lecture</p></td>
<td><p><code>memberOf</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Serveurs Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Propriété de lecture</p></td>
<td><p><code>garbageCollPeriod</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Serveurs Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Propriété de lecture</p></td>
<td><p><code>userAccountControl</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Serveurs Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Propriété de lecture</p></td>
<td><p><code>canonicalName</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Serveurs Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Synchronisation de la réplication</p></td>
<td><p></p></td>
<td><p>Droit étendu</p></td>
</tr>
<tr class="even">
<td><p>Serveurs Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Créer un enfant</p>
<p>Supprimer l’enfant</p>
<p>Répertorier les enfants</p></td>
<td><p><code>msExchActiveSyncDevices / User</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Serveurs Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Créer un enfant</p>
<p>Supprimer l’enfant</p>
<p>Répertorier les enfants</p></td>
<td><p><code>msExchActiveSyncDevices / inetOrgPerson</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Serveurs Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Propriété d’écriture</p></td>
<td><p><code>msExchSafeSendersHash</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Serveurs Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Propriété d’écriture</p></td>
<td><p><code>msExchPublicDelegates</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Serveurs Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Propriété d’écriture</p></td>
<td><p><code>msExchMobileMailboxFlags</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Serveurs Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Propriété d’écriture</p></td>
<td><p><code>msExchSafeRecipientsHash</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Serveurs Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Propriété d’écriture</p></td>
<td><p><code>userCertificate</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Serveurs Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Propriété d’écriture</p></td>
<td><p><code>msExchUMDtmfMap</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Serveurs Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Propriété d’écriture</p></td>
<td><p><code>msExchBlockedSendersHash</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Serveurs Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Propriété d’écriture</p></td>
<td><p><code>msExchUMSpokenName</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Serveurs Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Propriété d’écriture</p></td>
<td><p><code>msExchUMPinChecksum</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Serveurs Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Propriété d’écriture</p></td>
<td><p><code>thumbnailPhoto</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Gestion de l’organisation</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Lecture</p>
<p>Objet de liste</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Gestion de l’organisation</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Propriété d’écriture</p></td>
<td><p><code>Exchange Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Gestion de l’organisation</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Propriété d’écriture</p></td>
<td><p><code>garbageCollPeriod</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Gestion de l’organisation</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Propriété d’écriture</p></td>
<td><p><code>legacyExchangeDN</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Gestion de l’organisation</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Propriété d’écriture</p></td>
<td><p><code>msExchPublicDelegates</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Gestion de l’organisation</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Propriété d’écriture</p></td>
<td><p><code>textEncodedORAddress</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Gestion de l’organisation</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Propriété d’écriture</p></td>
<td><p><code>proxyAddresses</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Gestion de l’organisation</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Propriété d’écriture</p></td>
<td><p><code>mail</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Gestion de l’organisation</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Propriété d’écriture</p></td>
<td><p><code>displayNamePrintable</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Gestion de l’organisation</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Propriété d’écriture</p></td>
<td><p><code>showInAddressBook</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Gestion de l’organisation</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Propriété d’écriture</p></td>
<td><p><code>Exchange Personal Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Gestion de l’organisation</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Contrôle total</p></td>
<td><p><code>/ msExchDynamicDistributionList</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Gestion de l’organisation</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Propriété d’écriture</p></td>
<td><p><code>adminDisplayName</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Gestion de l’organisation</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Propriété d’écriture</p></td>
<td><p><code>displayName</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Sous-système approuvé Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Lecture</p>
<p>Objet de liste</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Sous-système approuvé Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Propriété d’écriture</p></td>
<td><p><code>displayName</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Sous-système approuvé Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Propriété d’écriture</p></td>
<td><p><code>Public Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Sous-système approuvé Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Propriété d’écriture</p></td>
<td><p><code>msExchPublicDelegates</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Sous-système approuvé Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Propriété d’écriture</p></td>
<td><p><code>adminDisplayName</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Sous-système approuvé Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Contrôle total</p></td>
<td><p><code>/ msExchDynamicDistributionList</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Sous-système approuvé Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Propriété d’écriture</p></td>
<td><p><code>Exchange Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Sous-système approuvé Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Propriété d’écriture</p></td>
<td><p><code>Exchange Personal Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Sous-système approuvé Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Propriété d’écriture</p></td>
<td><p><code>garbageCollPeriod</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Sous-système approuvé Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Propriété d’écriture</p></td>
<td><p><code>textEncodedORAddress</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Sous-système approuvé Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Propriété d’écriture</p></td>
<td><p><code>showInAddressBook</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Sous-système approuvé Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Propriété d’écriture</p></td>
<td><p><code>legacyExchangeDN</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Sous-système approuvé Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Propriété d’écriture</p></td>
<td><p><code>Personal Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Sous-système approuvé Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Propriété d’écriture</p></td>
<td><p><code>proxyAddresses</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Sous-système approuvé Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Propriété d’écriture</p></td>
<td><p><code>displayNamePrintable</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Sous-système approuvé Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Propriété d’écriture</p></td>
<td><p><code>mail</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Autorisations Windows Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Propriété d’écriture</p></td>
<td><p><code>pwdLastSet</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Autorisations Windows Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>DACL d’écriture</p></td>
<td><p><code>/ user</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Autorisations Windows Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>DACL d’écriture</p>
<p></p></td>
<td><p><code>/ inetOrgPerson</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Autorisations Windows Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Supprimer l’arborescence</p></td>
<td><p><code>/ user</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Autorisations Windows Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Supprimer l’arborescence</p>
<p></p></td>
<td><p><code>/ inetOrgPerson</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Autorisations Windows Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Propriété d’écriture</p></td>
<td><p><code>sAMAccountName</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Autorisations Windows Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Créer un enfant</p>
<p>Supprimer</p></td>
<td><p><code>/ contact</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Autorisations Windows Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Créer un enfant</p>
<p>Supprimer</p></td>
<td><p><code>/ inetOrgPerson</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Autorisations Windows Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Créer un enfant</p>
<p>Supprimer</p></td>
<td><p><code>/ user</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Autorisations Windows Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Créer un enfant</p>
<p>Supprimer</p></td>
<td><p><code>/ organizationUnit</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Autorisations Windows Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Créer un enfant</p>
<p>Supprimer</p></td>
<td><p><code>/ group</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Autorisations Windows Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Créer un enfant</p>
<p>Supprimer l’enfant</p></td>
<td><p><code>/ computer</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Autorisations Windows Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Propriété d’écriture</p></td>
<td><p><code>Member</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Autorisations Windows Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Propriété d’écriture</p></td>
<td><p><code>wwwHomePage</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Autorisations Windows Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Propriété d’écriture</p></td>
<td><p><code>countryCode</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Autorisations Windows Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Propriété d’écriture</p></td>
<td><p><code>userAccountControl</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Autorisations Windows Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Propriété d’écriture</p></td>
<td><p><code>managedBy</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Autorisations Windows Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Réinitialiser le mot de passe à la prochaine connexion</p></td>
<td><p></p></td>
<td><p>Droit étendu</p></td>
</tr>
<tr class="even">
<td><p>Autorisations Windows Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Changer le mot de passe</p></td>
<td><p><code> / user</code></p></td>
<td><p>Droit étendu</p></td>
</tr>
<tr class="odd">
<td><p>Installation déléguée</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Propriété de lecture</p></td>
<td><p><code>User Account Restrictions</code></p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


### Nom unique de l’objet : CN=AdminSDHolder,CN=Système,DC=\<domaine\>

<table style="width:100%;">
<colgroup>
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
</colgroup>
<thead>
<tr class="header">
<th>Compte</th>
<th>Type d’ACE</th>
<th>Héritage</th>
<th>Autorisations</th>
<th>Sur propriété/S’applique à</th>
<th>Commentaires</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Utilisateurs authentifiés</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Propriété de lecture</p></td>
<td><p><code>Exchange Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>AUTORITÉ NT\RÉSEAU</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Propriété de lecture</p></td>
<td><p><code>Exchange Personal Information</code></p></td>
<td><p>Accorde des autorisations de lecture du service de transport.</p></td>
</tr>
<tr class="odd">
<td><p>Serveurs Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Propriété d’écriture</p></td>
<td><p><code>groupType</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Serveurs Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Propriété d’écriture</p></td>
<td><p><code>msExchMailboxSecurityDescriptor</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Serveurs Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Propriété d’écriture</p></td>
<td><p><code>msExchUMServerWritableFlags</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Serveurs Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Propriété de lecture</p></td>
<td><p><code>Exchange Personal Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Serveurs Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Propriété de lecture</p></td>
<td><p><code>Exchange Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Serveurs Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Propriété d’écriture</p></td>
<td><p><code>msExchUserCultulre</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Serveurs Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Propriété de lecture</p></td>
<td><p><code>memberOf</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Serveurs Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Propriété de lecture</p></td>
<td><p><code>garbageCollPeriod</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Serveurs Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Propriété de lecture</p></td>
<td><p><code>userAccountControl</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Serveurs Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Propriété de lecture</p></td>
<td><p><code>canonicalName</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Serveurs Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Synchronisation de la réplication</p></td>
<td><p></p></td>
<td><p>Droit étendu</p></td>
</tr>
<tr class="even">
<td><p>Serveurs Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Créer un enfant</p>
<p>Supprimer l’enfant</p>
<p>Répertorier les enfants</p></td>
<td><p><code>msExchActiveSyncDevices / User</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Serveurs Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Créer un enfant</p>
<p>Supprimer l’enfant</p>
<p>Répertorier les enfants</p></td>
<td><p><code>msExchActiveSyncDevices / inetOrgPerson</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Serveurs Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Propriété d’écriture</p></td>
<td><p><code>msExchSafeSendersHash</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Serveurs Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Propriété d’écriture</p></td>
<td><p><code>msExchPublicDelegates</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Serveurs Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Propriété d’écriture</p></td>
<td><p><code>msExchMobileMailboxFlags</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Serveurs Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Propriété d’écriture</p></td>
<td><p><code>msExchSafeRecipientsHash</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Serveurs Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Propriété d’écriture</p></td>
<td><p><code>userCertificate</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Serveurs Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Propriété d’écriture</p></td>
<td><p><code>msExchUMDtmfMap</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Serveurs Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Propriété d’écriture</p></td>
<td><p><code>msExchBlockedSendersHash</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Serveurs Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Propriété d’écriture</p></td>
<td><p><code>msExchUMSpokenName</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Serveurs Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Propriété d’écriture</p></td>
<td><p><code>msExchUMPinChecksum</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Serveurs Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Propriété d’écriture</p></td>
<td><p><code>thumbnailPhoto</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Gestion de l’organisation</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Lecture</p>
<p>Objet de liste</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Gestion de l’organisation</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Propriété d’écriture</p></td>
<td><p><code>Exchange Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Gestion de l’organisation</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Propriété d’écriture</p></td>
<td><p><code>garbageCollPeriod</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Gestion de l’organisation</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Propriété d’écriture</p></td>
<td><p><code>legacyExchangeDN</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Gestion de l’organisation</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Propriété d’écriture</p></td>
<td><p><code>msExchPublicDelegates</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Gestion de l’organisation</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Propriété d’écriture</p></td>
<td><p><code>textEncodedORAddress</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Gestion de l’organisation</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Propriété d’écriture</p></td>
<td><p><code>proxyAddresses</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Gestion de l’organisation</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Propriété d’écriture</p></td>
<td><p><code>mail</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Gestion de l’organisation</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Propriété d’écriture</p></td>
<td><p><code>displayNamePrintable</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Gestion de l’organisation</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Propriété d’écriture</p></td>
<td><p><code>showInAddressBook</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Gestion de l’organisation</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Propriété d’écriture</p></td>
<td><p><code>Exchange Personal Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Gestion de l’organisation</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Contrôle total</p></td>
<td><p><code>/ msExchDynamicDistributionList</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Gestion de l’organisation</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Propriété d’écriture</p></td>
<td><p><code>adminDisplayName</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Gestion de l’organisation</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Propriété d’écriture</p></td>
<td><p><code>displayName</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Sous-système approuvé Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Lecture</p>
<p>Objet de liste</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Sous-système approuvé Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Propriété d’écriture</p></td>
<td><p><code>displayName</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Sous-système approuvé Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Propriété d’écriture</p></td>
<td><p><code>Public Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Sous-système approuvé Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Propriété d’écriture</p></td>
<td><p><code>msExchPublicDelegates</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Sous-système approuvé Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Propriété d’écriture</p></td>
<td><p><code>adminDisplayName</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Sous-système approuvé Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Contrôle total</p></td>
<td><p><code>/ msExchDynamicDistributionList</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Sous-système approuvé Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Propriété d’écriture</p></td>
<td><p><code>Exchange Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Sous-système approuvé Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Propriété d’écriture</p></td>
<td><p><code>Exchange Personal Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Sous-système approuvé Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Propriété d’écriture</p></td>
<td><p><code>garbageCollPeriod</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Sous-système approuvé Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Propriété d’écriture</p></td>
<td><p><code>textEncodedORAddress</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Sous-système approuvé Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Propriété d’écriture</p></td>
<td><p><code>showInAddressBook</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Sous-système approuvé Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Propriété d’écriture</p></td>
<td><p><code>legacyExchangeDN</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Sous-système approuvé Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Propriété d’écriture</p></td>
<td><p><code>Personal Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Sous-système approuvé Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Propriété d’écriture</p></td>
<td><p><code>proxyAddresses</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Sous-système approuvé Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Propriété d’écriture</p></td>
<td><p><code>displayNamePrintable</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Sous-système approuvé Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Propriété d’écriture</p></td>
<td><p><code>mail</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Autorisations Windows Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Propriété d’écriture</p></td>
<td><p><code>pwdLastSet</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Autorisations Windows Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Propriété d’écriture</p></td>
<td><p><code>sAMAccountName</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Autorisations Windows Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Propriété d’écriture</p></td>
<td><p><code>Member</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Autorisations Windows Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Propriété d’écriture</p></td>
<td><p><code>wwwHomePage</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Autorisations Windows Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Propriété d’écriture</p></td>
<td><p><code>countryCode</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Autorisations Windows Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Propriété d’écriture</p></td>
<td><p><code>userAccountControl</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Autorisations Windows Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Propriété d’écriture</p></td>
<td><p><code>managedBy</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Installation déléguée</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Propriété de lecture</p></td>
<td><p><code>User Account Restrictions</code></p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


### Nom unique de l’objet : CN=Objets supprimés,DC=\<domaine\>

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>Compte</th>
<th>Type d’ACE</th>
<th>Héritage</th>
<th>Autorisations</th>
<th>Sur propriété/S’applique à</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Serveurs Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Contenu de la liste</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


### Nom unique de l’objet : CN=Objets système Microsoft Exchange,DC=\<domaine\>

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>Compte</th>
<th>Type d’ACE</th>
<th>Héritage</th>
<th>Autorisations</th>
<th>Sur propriété/S’applique à</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>AUTORITÉ NT\RÉSEAU</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Propriété de lecture</p>
<p>Contenu de la liste</p>
<p>Autorisations de lecture</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Utilisateurs authentifiés</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Autorisations de lecture</p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Utilisateurs authentifiés</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Propriété de lecture</p></td>
<td><p><code>garbageCollPeriod</code></p></td>
</tr>
<tr class="even">
<td><p>Utilisateurs authentifiés</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Propriété de lecture</p></td>
<td><p><code>adminDisplayName</code></p></td>
</tr>
<tr class="odd">
<td><p>Utilisateurs authentifiés</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Propriété de lecture</p></td>
<td><p><code>modifyTimeStamp</code></p></td>
</tr>
<tr class="even">
<td><p>Serveurs Exchange</p></td>
<td><p>ACE Refuser</p></td>
<td><p>Tout</p></td>
<td><p>Supprimer l’arborescence</p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Serveurs Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Autorisations de lecture</p>
<p>Contenu de la liste</p>
<p>Propriété de lectureSupprimer l’arborescence</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Serveurs Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Créer un enfant</p>
<p></p></td>
<td><p><code>/ msExchSystemMailbox</code></p></td>
</tr>
<tr class="odd">
<td><p>Serveurs Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Créer un enfant</p>
<p>Supprimer l’enfant</p></td>
<td><p><code>/ publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>Serveurs Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Créer un enfant</p>
<p></p></td>
<td><p><code>/ user</code></p></td>
</tr>
<tr class="odd">
<td><p>Serveurs Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Supprimer l’enfant</p>
<p></p></td>
<td><p><code>/ msExchSystemMailbox</code></p></td>
</tr>
<tr class="even">
<td><p>Serveurs Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Supprimer l’enfant</p>
<p></p></td>
<td><p><code>/ user</code></p></td>
</tr>
<tr class="odd">
<td><p>Serveurs Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Desc</p></td>
<td><p>Propriété d’écriture</p></td>
<td><p><code>/ publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>Serveurs Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Desc</p></td>
<td><p>Propriété d’écriture</p></td>
<td><p><code>/ msExchSystemMailbox</code></p></td>
</tr>
<tr class="odd">
<td><p>Serveurs Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Desc</p></td>
<td><p>Propriété d’écriture</p></td>
<td><p><code>/ user</code></p></td>
</tr>
<tr class="even">
<td><p>Serveurs Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Desc</p></td>
<td><p>Changer le mot de passe</p>
<p>Réinitialiser le mot de passe à la prochaine connexion</p></td>
<td><p><code>/ user</code></p></td>
</tr>
<tr class="odd">
<td><p>Gestion de l’organisation</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Autorisations de lecture</p>
<p>Contenu de la liste</p>
<p>Propriété de lecture</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Gestion de l’organisation</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Desc</p></td>
<td><p>Propriété d’écriture</p></td>
<td><p><code>/ msExchSystemMailbox</code></p></td>
</tr>
<tr class="odd">
<td><p>Gestion de l’organisation</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Créer un enfant</p>
<p>Supprimer l’enfant</p></td>
<td><p><code>/ msExchSystemMailbox</code></p></td>
</tr>
<tr class="even">
<td><p>Gestion de l’organisation</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Desc</p></td>
<td><p>Propriété d’écriture</p></td>
<td><p><code>/ user</code></p></td>
</tr>
<tr class="odd">
<td><p>Gestion de l’organisation</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Créer un enfant</p>
<p>Supprimer l’enfant</p></td>
<td><p><code>/ user</code></p></td>
</tr>
<tr class="even">
<td><p>Gestion de l’organisation</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Desc</p></td>
<td><p>Propriété de lecture</p>
<p>Propriété d’écriture</p></td>
<td><p><code>mail / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>Gestion de l’organisation</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Desc</p></td>
<td><p>Propriété de lecture</p>
<p>Propriété d’écriture</p></td>
<td><p><code>displayNamePrintable / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>Gestion de l’organisation</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Desc</p></td>
<td><p>Propriété de lecture</p>
<p>Propriété d’écriture</p></td>
<td><p><code>displayName / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>Gestion de l’organisation</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Desc</p></td>
<td><p>Propriété de lecture</p>
<p>Propriété d’écriture</p></td>
<td><p><code>textEncodedORAddress / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>Gestion de l’organisation</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Desc</p></td>
<td><p>Propriété de lecture</p>
<p>Propriété d’écriture</p></td>
<td><p><code>proxyAddresses / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>Gestion de l’organisation</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Desc</p></td>
<td><p>Propriété de lecture</p>
<p>Propriété d’écriture</p></td>
<td><p><code>cn / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>Gestion de l’organisation</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Desc</p></td>
<td><p>Propriété de lecture</p>
<p>Propriété d’écriture</p></td>
<td><p><code>showInAddressBook / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>Gestion de l’organisation</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Desc</p></td>
<td><p>Propriété de lecture</p>
<p>Propriété d’écriture</p></td>
<td><p><code>Exchange Information / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>Gestion de l’organisation</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Desc</p></td>
<td><p>Propriété de lecture</p>
<p>Propriété d’écriture</p></td>
<td><p>legacyExchangeDN / publicFolder</p></td>
</tr>
<tr class="odd">
<td><p>Gestion de l’organisation</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Desc</p></td>
<td><p>Propriété de lecture</p>
<p>Propriété d’écriture</p></td>
<td><p><code>Exchange Personal Information / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>Gestion de l’organisation</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Desc</p></td>
<td><p>Propriété de lecture</p>
<p>Propriété d’écriture</p></td>
<td><p><code>msDSPhoneticDisplayName / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>Gestion de l’organisation</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Desc</p></td>
<td><p>Propriété de lecture</p>
<p>Propriété d’écriture</p></td>
<td><p><code>msExchPFContacts / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>Gestion de l’organisation</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Desc</p></td>
<td><p>Propriété de lecture</p>
<p>Propriété d’écriture</p></td>
<td><p><code>garbageCollPeriod / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>Gestion de l’organisation</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Desc</p></td>
<td><p>Propriété de lecture</p>
<p>Propriété d’écriture</p></td>
<td><p><code>name / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>Gestion de l’organisation</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Desc</p></td>
<td><p>Propriété de lecture</p>
<p>Propriété d’écriture</p></td>
<td><p><code>msExchPublicDelegates / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>Gestion des dossiers publics</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Autorisations de lecture</p>
<p>Contenu de la liste</p>
<p>Propriété de lecture</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Gestion des dossiers publics</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Desc</p></td>
<td><p>Propriété de lecture</p>
<p>Propriété d’écriture</p></td>
<td><p><code>mail / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>Gestion des dossiers publics</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Desc</p></td>
<td><p>Propriété de lecture</p>
<p>Propriété d’écriture</p></td>
<td><p><code>displayNamePrintable / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>Gestion des dossiers publics</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Desc</p></td>
<td><p>Propriété de lecture</p>
<p>Propriété d’écriture</p></td>
<td><p><code>displayName / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>Gestion des dossiers publics</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Desc</p></td>
<td><p>Propriété de lecture</p>
<p>Propriété d’écriture</p></td>
<td><p><code>textEncodedORAddress / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>Gestion des dossiers publics</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Desc</p></td>
<td><p>Propriété de lecture</p>
<p>Propriété d’écriture</p></td>
<td><p><code>proxyAddresses / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>Gestion des dossiers publics</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Desc</p></td>
<td><p>Propriété de lecture</p>
<p>Propriété d’écriture</p></td>
<td><p><code>cn / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>Gestion des dossiers publics</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Desc</p></td>
<td><p>Propriété de lecture</p>
<p>Propriété d’écriture</p></td>
<td><p><code>showInAddressBook / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>Gestion des dossiers publics</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Desc</p></td>
<td><p>Propriété de lecture</p>
<p>Propriété d’écriture</p></td>
<td><p><code>Exchange Information / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>Gestion des dossiers publics</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Desc</p></td>
<td><p>Propriété de lecture</p>
<p>Propriété d’écriture</p></td>
<td><p><code>legacyExchangeDN / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>Gestion des dossiers publics</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Desc</p></td>
<td><p>Propriété de lecture</p>
<p>Propriété d’écriture</p></td>
<td><p><code>Exchange Personal Information / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>Gestion des dossiers publics</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Desc</p></td>
<td><p>Propriété de lecture</p>
<p>Propriété d’écriture</p></td>
<td><p><code>msDSPhoneticDisplayName / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>Gestion des dossiers publics</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Desc</p></td>
<td><p>Propriété de lecture</p>
<p>Propriété d’écriture</p></td>
<td><p><code>msExchPFContacts / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>Gestion des dossiers publics</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Desc</p></td>
<td><p>Propriété de lecture</p>
<p>Propriété d’écriture</p></td>
<td><p><code>garbageCollPeriod / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>Gestion des dossiers publics</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Desc</p></td>
<td><p>Propriété de lecture</p>
<p>Propriété d’écriture</p></td>
<td><p><code>name / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>Gestion des dossiers publics</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Desc</p></td>
<td><p>Propriété de lecture</p>
<p>Propriété d’écriture</p></td>
<td><p><code>msExchPublicDelegates / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>Sous-système approuvé Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Autorisations de lecture</p>
<p>Contenu de la liste</p>
<p>Propriété de lecture</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Sous-système approuvé Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Desc</p></td>
<td><p>Propriété de lecture</p>
<p>Propriété d’écriture</p></td>
<td><p><code>mail / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>Sous-système approuvé Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Desc</p></td>
<td><p>Propriété de lecture</p>
<p>Propriété d’écriture</p></td>
<td><p><code>displayNamePrintable / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>Sous-système approuvé Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Desc</p></td>
<td><p>Propriété de lecture</p>
<p>Propriété d’écriture</p></td>
<td><p><code>displayName / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>Sous-système approuvé Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Desc</p></td>
<td><p>Propriété de lecture</p>
<p>Propriété d’écriture</p></td>
<td><p><code>textEncodedORAddress / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>Sous-système approuvé Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Desc</p></td>
<td><p>Propriété de lecture</p>
<p>Propriété d’écriture</p></td>
<td><p><code>proxyAddresses / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>Sous-système approuvé Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Desc</p></td>
<td><p>Propriété de lecture</p>
<p>Propriété d’écriture</p></td>
<td><p><code>cn / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>Sous-système approuvé Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Desc</p></td>
<td><p>Propriété de lecture</p>
<p>Propriété d’écriture</p></td>
<td><p><code>showInAddressBook / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>Sous-système approuvé Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Desc</p></td>
<td><p>Propriété de lecture</p>
<p>Propriété d’écriture</p></td>
<td><p><code>Exchange Information / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>Sous-système approuvé Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Desc</p></td>
<td><p>Propriété de lecture</p>
<p>Propriété d’écriture</p></td>
<td><p><code>legacyExchangeDN / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>Sous-système approuvé Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Desc</p></td>
<td><p>Propriété de lecture</p>
<p>Propriété d’écriture</p></td>
<td><p><code>Exchange Personal Information / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>Sous-système approuvé Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Desc</p></td>
<td><p>Propriété de lecture</p>
<p>Propriété d’écriture</p></td>
<td><p><code>msDSPhoneticDisplayName / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>Sous-système approuvé Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Desc</p></td>
<td><p>Propriété de lecture</p>
<p>Propriété d’écriture</p></td>
<td><p><code>msExchPFContacts / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>Sous-système approuvé Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Desc</p></td>
<td><p>Propriété de lecture</p>
<p>Propriété d’écriture</p></td>
<td><p><code>garbageCollPeriod / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>Sous-système approuvé Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Desc</p></td>
<td><p>Propriété de lecture</p>
<p>Propriété d’écriture</p></td>
<td><p><code>name / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>Sous-système approuvé Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Desc</p></td>
<td><p>Propriété de lecture</p>
<p>Propriété d’écriture</p></td>
<td><p><code>msExchPublicDelegates / publicFolder</code></p></td>
</tr>
</tbody>
</table>


### Nom unique de l’objet : CN=Serveurs de domaine d’installation Exchange,CN=Objets système Microsoft Exchange,DC=\<domaine\>

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>Compte</th>
<th>Type d’ACE</th>
<th>Héritage</th>
<th>Autorisations</th>
<th>Sur propriété/S’applique à</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Gestion de l’organisation</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Contrôle total</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


## Installation du rôle de serveur

Durant l’installation des rôles serveur de boîtes aux lettres et d’accès au client, le programme d’installation ajoute le groupe universel de sécurité Gestion de l’organisation au groupe de sécurité des administrateurs sur l’ordinateur local de façon à ce que des membres du groupe de rôles de gestion nommé Gestion de l’organisation puissent gérer le serveur.

Le tableau d’autorisations suivant présente les autorisations qui sont définies lorsque vous installez les rôles serveur de boîtes aux lettres ou d’accès au client.

### Nom unique de l’objet : CN=\<serveur\>,CN=Serveurs,CN=\<groupe d’administration\>,CN=Groupes d’administration,CN=\<organisation\>

<table style="width:100%;">
<colgroup>
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
</colgroup>
<thead>
<tr class="header">
<th>Compte</th>
<th>Type d’ACE</th>
<th>Héritage</th>
<th>Autorisations</th>
<th>Sur propriété/S’applique à</th>
<th>Commentaires</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>MACHINE$</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Autorisations de lecture</p>
<p>Contenu de la liste</p>
<p>Propriété de lecture</p>
<p>Objet de liste</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>MACHINE$</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Aucun</p></td>
<td><p>Propriété d’écriture</p></td>
<td><p><code>msExchServerSite</code></p>
<p><code>msExchEdgeSyncCredential</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Serveurs Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Stockage d’accès de transport</p>
<p>Stockage de délégation contrainte</p>
<p>Stockage d'accès en lecture seule</p>
<p>Stockage d'accès en lecture/écriture</p></td>
<td><p></p></td>
<td><p>Droits étendus</p></td>
</tr>
<tr class="even">
<td><p>AUTORITÉ NT\RÉSEAU</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Sérialisation de jeton de services Web Exchange</p></td>
<td><p></p></td>
<td><p>Droit étendu</p>
<p>Accordé uniquement sur les objets de rôle serveur de boîtes aux lettres.</p></td>
</tr>
<tr class="odd">
<td><p>AUTORITÉ NT\RÉSEAU</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Autorisations de lecture</p>
<p>Contenu de la liste</p>
<p>Propriété de lecture</p>
<p>Objet de liste</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Système local</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Autorisations de lecture</p>
<p>Contenu de la liste</p>
<p>Propriété de lecture</p>
<p>Objet de liste</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Installation déléguée</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Contrôle total</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Installation déléguée</p></td>
<td><p>ACE Refuser</p></td>
<td><p>Tout</p></td>
<td><p>Créer un enfant</p>
<p>Supprimer l’enfant</p></td>
<td><p><code>/ msExchPublicMDB</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Utilisateurs authentifiés</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Propriété de lecture</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Installation déléguée</p></td>
<td><p>ACE Refuser</p></td>
<td><p>Tout</p></td>
<td><p>Recevoir en tant que</p>
<p>Envoyer en tant que</p></td>
<td><p></p></td>
<td><p>Droit étendu</p></td>
</tr>
</tbody>
</table>


## Groupes de disponibilité de base de données

Les tableaux d'autorisations contenus dans cette section répertorient les autorisations qui sont définies pour les groupes de disponibilité de base de données et ses membres.

### Nom unique de l’objet : CN=\<NomDAG\>,CN=Groupes de disponibilité de base de données,CN=\<groupe d’administration\>,CN=Groupes d’administration,CN=\<organisation\>

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>Compte</th>
<th>Type d’ACE</th>
<th>Héritage</th>
<th>Autorisations</th>
<th>Sur propriété/S’applique à</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Utilisateurs authentifiés</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Aucun</p></td>
<td><p>Propriété de lecture</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


## Transport Edge

Si vous installez un serveur de transport Edge et établissez un abonnement Edge avec l'organisation Exchange, les autorisations répertoriées dans le tableau d'autorisations suivant sont définies lors de l'instanciation du serveur de transport Edge dans l'organisation.

### Nom unique de l’objet : CN=\<serveur\>,CN=Serveurs,CN=\<groupe d’administration\>,CN=Groupes d’administration,CN=\<organisation\>

<table style="width:100%;">
<colgroup>
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
</colgroup>
<thead>
<tr class="header">
<th>Compte</th>
<th>Type d’ACE</th>
<th>Héritage</th>
<th>Autorisations</th>
<th>Sur propriété/S’applique à</th>
<th>Commentaires</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Serveurs Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Propriété d’écriture</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Utilisateurs authentifiés</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Aucun</p></td>
<td><p>Propriétés de lecture</p></td>
<td><p></p></td>
<td><p>L’entrée de contrôle d’accès est définie dans le schéma pour les objets de classe <code>msExchExchangeServer</code><code>defaultSecurityDescriptor</code>.</p></td>
</tr>
</tbody>
</table>


## Installation du serveur de boîtes aux lettres

Lors de l’installation du premier serveur de boîtes aux lettres, les conteneurs suivants sont créés, s’ils n’existent pas déjà. Le tableau des autorisations suivant présente les autorisations appliquées.

### Nom unique de l’objet : CN=Configuration de disponibilité,CN=\<organisation\>

<table style="width:100%;">
<colgroup>
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
</colgroup>
<thead>
<tr class="header">
<th>Compte</th>
<th>Type d’ACE</th>
<th>Héritage</th>
<th>Autorisations</th>
<th>Sur propriété/S’applique à</th>
<th>Commentaires</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Serveurs Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Desc</p></td>
<td><p>Propriété de lecture</p></td>
<td><p><code>msExchAvailabilityUserPassword / msExchAvailabilityAddressSpaceObjects</code></p></td>
<td><p>Droit étendu</p></td>
</tr>
</tbody>
</table>


### Nom unique de l’objet : CN=Par défaut\<Serveur\>,CN=Connecteurs de réception SMTP,CN=Protocoles,CN=\<Serveur\>,CN=Serveurs,CN=\<groupe d’administration\>,CN=\<organisation\>

<table style="width:100%;">
<colgroup>
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
</colgroup>
<thead>
<tr class="header">
<th>Compte</th>
<th>Type d’ACE</th>
<th>Héritage</th>
<th>Autorisations</th>
<th>Sur propriété/S’applique à</th>
<th>Commentaires</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>ExchangeLegacyInterop</p></td>
<td><p>ACE Refuser</p></td>
<td><p>Tout</p></td>
<td><p>Accepter les en-têtes de forêt</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>ExchangeLegacyInterop</p></td>
<td><p>ACE Refuser</p></td>
<td><p>Tout</p></td>
<td><p>Accepter les en-têtes d’organisation</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Serveurs Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Accepter tous les expéditeurs</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>ExchangeLegacyInterop</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Accepter tous les expéditeurs</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Accepter tous les expéditeurs</p></td>
<td><p></p></td>
<td><p>Il s’agit du SID (identificateur de sécurité) connu pour les serveurs de boîtes aux lettres.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Accepter tous les expéditeurs</p></td>
<td><p></p></td>
<td><p>Il s’agit du SID connu pour les serveurs de transport Edge.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Accepter tous les expéditeurs</p></td>
<td><p></p></td>
<td><p>Il s’agit du SID connu pour les serveurs sécurisés en externe.</p></td>
</tr>
<tr class="even">
<td><p>Serveurs Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Accepter EXCH50</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>ExchangeLegacyInterop</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Accepter EXCH50</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Accepter EXCH50</p></td>
<td><p></p></td>
<td><p>Il s’agit du SID connu pour les serveurs de boîtes aux lettres.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Accepter EXCH50</p></td>
<td><p></p></td>
<td><p>Il s’agit du SID connu pour les serveurs de transport Edge.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Accepter EXCH50</p></td>
<td><p></p></td>
<td><p>Il s’agit du SID connu pour les serveurs sécurisés en externe.</p></td>
</tr>
<tr class="odd">
<td><p>Serveurs Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Envoyer des messages à n’importe quel destinataire</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>ExchangeLegacyInterop</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Envoyer des messages à n’importe quel destinataire</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Envoyer des messages à n’importe quel destinataire</p></td>
<td><p></p></td>
<td><p>Il s’agit du SID connu pour les serveurs de boîtes aux lettres.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Envoyer des messages à n’importe quel destinataire</p></td>
<td><p></p></td>
<td><p>Il s’agit du SID connu pour les serveurs de transport Edge.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Envoyer des messages à n’importe quel destinataire</p></td>
<td><p></p></td>
<td><p>Il s’agit du SID connu pour les serveurs sécurisés en externe.</p></td>
</tr>
<tr class="even">
<td><p>Serveurs Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Accepter XShadow</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Accepter XShadow</p></td>
<td><p></p></td>
<td><p>Il s’agit du SID connu pour les serveurs de transport Edge.</p></td>
</tr>
<tr class="even">
<td><p>Serveurs Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Accepter les en-têtes de routage</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>ExchangeLegacyInterop</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Accepter les en-têtes de routage</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Accepter les en-têtes de routage</p></td>
<td><p></p></td>
<td><p>Il s’agit du SID connu pour les serveurs de boîtes aux lettres.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Accepter les en-têtes de routage</p></td>
<td><p></p></td>
<td><p>Il s’agit du SID connu pour les serveurs de transport Edge.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Accepter les en-têtes de routage</p></td>
<td><p></p></td>
<td><p>Il s’agit du SID connu pour les serveurs sécurisés en externe.</p></td>
</tr>
<tr class="odd">
<td><p>Serveurs Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Accepter XSessionParams</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Accepter XSessionParams</p></td>
<td><p></p></td>
<td><p>Il s’agit du SID connu pour les serveurs de boîtes aux lettres.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Accepter XSessionParams</p></td>
<td><p></p></td>
<td><p>Il s’agit du SID connu pour les serveurs de boîtes aux lettres.</p></td>
</tr>
<tr class="even">
<td><p>Serveurs Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Accepter les en-têtes de forêt</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Accepter les en-têtes de forêt</p></td>
<td><p></p></td>
<td><p>Il s’agit du SID connu pour les serveurs de boîtes aux lettres.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Accepter les en-têtes de forêt</p></td>
<td><p></p></td>
<td><p>Il s’agit du SID connu pour les serveurs de transport Edge.</p></td>
</tr>
<tr class="odd">
<td><p>Serveurs Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Accepter xAttr</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Accepter xAttr</p></td>
<td><p></p></td>
<td><p>Il s’agit du SID connu pour les serveurs de boîtes aux lettres.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Accepter xAttr</p></td>
<td><p></p></td>
<td><p>Il s’agit du SID connu pour les serveurs de transport Edge.</p></td>
</tr>
<tr class="even">
<td><p>Serveurs Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Accepter XProxyFrom</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Accepter XProxyFrom de forêt</p></td>
<td><p></p></td>
<td><p>Il s’agit du SID connu pour les serveurs de boîtes aux lettres.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Accepter XProxyFrom de forêt</p></td>
<td><p></p></td>
<td><p>Il s’agit du SID connu pour les serveurs de transport Edge.</p></td>
</tr>
<tr class="odd">
<td><p>Serveurs Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Accepter XSysProbe</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Accepter XSysProbe de forêt</p></td>
<td><p></p></td>
<td><p>Il s’agit du SID connu pour les serveurs de boîtes aux lettres.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Accepter XSysProbe de forêt</p></td>
<td><p></p></td>
<td><p>Il s’agit du SID connu pour les serveurs de transport Edge.</p></td>
</tr>
<tr class="even">
<td><p>Serveurs Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Envoyer les propriétés étendues XMessageContext</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Envoyer les propriétés étendues XMessageContext</p></td>
<td><p></p></td>
<td><p>Il s’agit du SID connu pour les serveurs de boîtes aux lettres.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Envoyer les propriétés étendues XMessageContext</p></td>
<td><p></p></td>
<td><p>Il s’agit du SID connu pour les serveurs de transport Edge.</p></td>
</tr>
<tr class="odd">
<td><p>Serveurs Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Envoyer un index FAST XMessageContext</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Envoyer un index FAST XMessageContext</p></td>
<td><p></p></td>
<td><p>Il s’agit du SID connu pour les serveurs de boîtes aux lettres.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Envoyer un index FAST XMessageContext</p></td>
<td><p></p></td>
<td><p>Il s’agit du SID connu pour les serveurs de transport Edge.</p></td>
</tr>
<tr class="even">
<td><p>Serveurs Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Envoyer le cache de destinataires AD XMessageContext</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Envoyer le cache de destinataires AD XMessageContext</p></td>
<td><p></p></td>
<td><p>Il s’agit du SID connu pour les serveurs de boîtes aux lettres.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Envoyer le cache de destinataires AD XMessageContext</p></td>
<td><p></p></td>
<td><p>Il s’agit du SID connu pour les serveurs de transport Edge.</p></td>
</tr>
<tr class="odd">
<td><p>Serveurs Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Accepter l’indicateur d’authentification</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>ExchangeLegacyInterop</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Accepter l’indicateur d’authentification</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Accepter l’indicateur d’authentification</p></td>
<td><p></p></td>
<td><p>Il s’agit du SID connu pour les serveurs de boîtes aux lettres.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Accepter l’indicateur d’authentification</p></td>
<td><p></p></td>
<td><p>Il s’agit du SID connu pour les serveurs de transport Edge.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Accepter l’indicateur d’authentification</p></td>
<td><p></p></td>
<td><p>Il s’agit du SID connu pour les serveurs sécurisés en externe.</p></td>
</tr>
<tr class="even">
<td><p>Serveurs Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Ignorer le blocage du courrier indésirable</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>ExchangeLegacyInterop</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Ignorer le blocage du courrier indésirable</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Ignorer le blocage du courrier indésirable</p></td>
<td><p></p></td>
<td><p>Il s’agit du SID connu pour les serveurs de boîtes aux lettres.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Ignorer le blocage du courrier indésirable</p></td>
<td><p></p></td>
<td><p>Il s’agit du SID connu pour les serveurs de transport Edge.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Ignorer le blocage du courrier indésirable</p></td>
<td><p></p></td>
<td><p>Il s’agit du SID connu pour les serveurs sécurisés en externe.</p></td>
</tr>
<tr class="odd">
<td><p>Serveurs Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Ignorer la limite de taille du message</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>ExchangeLegacyInterop</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Ignorer la limite de taille du message</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Ignorer la limite de taille du message</p></td>
<td><p></p></td>
<td><p>Il s’agit du SID connu pour les serveurs de boîtes aux lettres.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Ignorer la limite de taille du message</p></td>
<td><p></p></td>
<td><p>Il s’agit du SID connu pour les serveurs de transport Edge.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Ignorer la limite de taille du message</p></td>
<td><p></p></td>
<td><p>Il s’agit du SID connu pour les serveurs sécurisés en externe.</p></td>
</tr>
<tr class="even">
<td><p>Serveurs Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Accepter les en-têtes d’organisation</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Accepter les en-têtes d’organisation</p></td>
<td><p></p></td>
<td><p>Il s’agit du SID connu pour les serveurs de boîtes aux lettres.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Accepter les en-têtes d’organisation</p></td>
<td><p></p></td>
<td><p>Il s’agit du SID connu pour les serveurs de transport Edge.</p></td>
</tr>
<tr class="odd">
<td><p>Serveurs Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Envoyer des messages au serveur</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>ExchangeLegacyInterop</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Envoyer des messages au serveur</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Envoyer des messages au serveur</p></td>
<td><p></p></td>
<td><p>Il s’agit du SID connu pour les serveurs de boîtes aux lettres.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Envoyer des messages au serveur</p></td>
<td><p></p></td>
<td><p>Il s’agit du SID connu pour les serveurs de transport Edge.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Envoyer des messages au serveur</p></td>
<td><p></p></td>
<td><p>Il s’agit du SID connu pour les serveurs sécurisés en externe.</p></td>
</tr>
<tr class="even">
<td><p>Serveurs Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Accepter un expéditeur de domaine faisant autorité</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>ExchangeLegacyInterop</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Accepter un expéditeur de domaine faisant autorité</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Accepter un expéditeur de domaine faisant autorité</p></td>
<td><p></p></td>
<td><p>Il s’agit du SID connu pour les serveurs de boîtes aux lettres.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Accepter un expéditeur de domaine faisant autorité</p></td>
<td><p></p></td>
<td><p>Il s’agit du SID connu pour les serveurs de transport Edge.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Accepter un expéditeur de domaine faisant autorité</p></td>
<td><p></p></td>
<td><p>Il s’agit du SID connu pour les serveurs sécurisés en externe.</p></td>
</tr>
<tr class="odd">
<td><p>Utilisateurs authentifiés</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Envoyer des messages à n’importe quel destinataire</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Utilisateurs authentifiés</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Accepter les en-têtes de routage</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Utilisateurs authentifiés</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Ignorer le blocage du courrier indésirable</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Utilisateurs authentifiés</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Envoyer des messages au serveur</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


### Nom unique de l’objet : CN=Client \<Serveur\>,CN=Connecteurs de réception SMTP,CN=Protocoles,CN=\<Serveur\>,CN=Serveurs,CN=\<groupe d’administration\>,CN=\<organisation\>

<table style="width:100%;">
<colgroup>
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
</colgroup>
<thead>
<tr class="header">
<th>Compte</th>
<th>Type d’ACE</th>
<th>Héritage</th>
<th>Autorisations</th>
<th>Sur propriété/S’applique à</th>
<th>Commentaires</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Utilisateurs authentifiés</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Envoyer des messages à n’importe quel destinataire</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Utilisateurs authentifiés</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Accepter les en-têtes de routage</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Utilisateurs authentifiés</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Ignorer le blocage du courrier indésirable</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Utilisateurs authentifiés</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Envoyer des messages au serveur</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Serveurs Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Accepter XSessionParams</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Accepter XSessionParams</p></td>
<td><p></p></td>
<td><p>Il s’agit du SID connu pour les serveurs de boîtes aux lettres.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Accepter XSessionParams</p></td>
<td><p></p></td>
<td><p>Il s’agit du SID connu pour les serveurs de boîtes aux lettres.</p></td>
</tr>
<tr class="even">
<td><p>Serveurs Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Accepter tous les expéditeurs</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Accepter tous les expéditeurs</p></td>
<td><p></p></td>
<td><p>Il s’agit du SID (identificateur de sécurité) connu pour les serveurs de boîtes aux lettres.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Accepter tous les expéditeurs</p></td>
<td><p></p></td>
<td><p>Il s’agit du SID connu pour les serveurs de transport Edge.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Accepter tous les expéditeurs</p></td>
<td><p></p></td>
<td><p>Il s’agit du SID connu pour les serveurs sécurisés en externe.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Accepter Exch50</p></td>
<td><p></p></td>
<td><p>Il s’agit du SID connu pour les serveurs de boîtes aux lettres.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Accepter Exch50</p></td>
<td><p></p></td>
<td><p>Il s’agit du SID connu pour les serveurs de transport Edge.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Accepter Exch50</p></td>
<td><p></p></td>
<td><p>Il s’agit du SID connu pour les serveurs sécurisés en externe.</p></td>
</tr>
<tr class="odd">
<td><p>Serveurs Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Accepter Exch50</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Serveurs Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Envoyer des messages à n’importe quel destinataire</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>ExchangeLegacyInterop</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Envoyer des messages à n’importe quel destinataire</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Envoyer des messages à n’importe quel destinataire</p></td>
<td><p></p></td>
<td><p>Il s’agit du SID connu pour les serveurs de boîtes aux lettres.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Envoyer des messages à n’importe quel destinataire</p></td>
<td><p></p></td>
<td><p>Il s’agit du SID connu pour les serveurs de transport Edge.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Envoyer des messages à n’importe quel destinataire</p></td>
<td><p></p></td>
<td><p>Il s’agit du SID connu pour les serveurs sécurisés en externe.</p></td>
</tr>
<tr class="odd">
<td><p>Serveurs Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Accepter XShadow</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Accepter XShadow</p></td>
<td><p></p></td>
<td><p>Il s’agit du SID connu pour les serveurs de transport Edge.</p></td>
</tr>
<tr class="odd">
<td><p>Serveurs Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Accepter les en-têtes de routage</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>ExchangeLegacyInterop</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Accepter les en-têtes de routage</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Accepter les en-têtes de routage</p></td>
<td><p></p></td>
<td><p>Il s’agit du SID connu pour les serveurs de boîtes aux lettres.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Accepter les en-têtes de routage</p></td>
<td><p></p></td>
<td><p>Il s’agit du SID connu pour les serveurs de transport Edge.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Accepter les en-têtes de routage</p></td>
<td><p></p></td>
<td><p>Il s’agit du SID connu pour les serveurs sécurisés en externe.</p></td>
</tr>
<tr class="even">
<td><p>Serveurs Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Accepter les en-têtes de forêt</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Accepter les en-têtes de forêt</p></td>
<td><p></p></td>
<td><p>Il s’agit du SID connu pour les serveurs de boîtes aux lettres.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Accepter les en-têtes de forêt</p></td>
<td><p></p></td>
<td><p>Il s’agit du SID connu pour les serveurs de transport Edge.</p></td>
</tr>
<tr class="odd">
<td><p>Serveurs Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Accepter xAttr</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Accepter xAttr</p></td>
<td><p></p></td>
<td><p>Il s’agit du SID connu pour les serveurs de boîtes aux lettres.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Accepter xAttr</p></td>
<td><p></p></td>
<td><p>Il s’agit du SID connu pour les serveurs de transport Edge.</p></td>
</tr>
<tr class="even">
<td><p>Serveurs Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Accepter XProxyFrom</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Accepter XProxyFrom de forêt</p></td>
<td><p></p></td>
<td><p>Il s’agit du SID connu pour les serveurs de boîtes aux lettres.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Accepter XProxyFrom de forêt</p></td>
<td><p></p></td>
<td><p>Il s’agit du SID connu pour les serveurs de transport Edge.</p></td>
</tr>
<tr class="odd">
<td><p>Serveurs Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Accepter l’indicateur d’authentification</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Accepter l’indicateur d’authentification</p></td>
<td><p></p></td>
<td><p>Il s’agit du SID connu pour les serveurs de boîtes aux lettres.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Accepter l’indicateur d’authentification</p></td>
<td><p></p></td>
<td><p>Il s’agit du SID connu pour les serveurs de transport Edge.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Accepter l’indicateur d’authentification</p></td>
<td><p></p></td>
<td><p>Il s’agit du SID connu pour les serveurs sécurisés en externe.</p></td>
</tr>
<tr class="odd">
<td><p>Serveurs Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Accepter XSysProbe</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Accepter XSysProbe de forêt</p></td>
<td><p></p></td>
<td><p>Il s’agit du SID connu pour les serveurs de boîtes aux lettres.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Accepter XSysProbe de forêt</p></td>
<td><p></p></td>
<td><p>Il s’agit du SID connu pour les serveurs de transport Edge.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Accepter l’indicateur d’authentification</p></td>
<td><p></p></td>
<td><p>Il s’agit du SID connu pour les serveurs sécurisés en externe.</p></td>
</tr>
<tr class="odd">
<td><p>Serveurs Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Ignorer le blocage du courrier indésirable</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Ignorer le blocage du courrier indésirable</p></td>
<td><p></p></td>
<td><p>Il s’agit du SID connu pour les serveurs de boîtes aux lettres.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Ignorer le blocage du courrier indésirable</p></td>
<td><p></p></td>
<td><p>Il s’agit du SID connu pour les serveurs de transport Edge.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Ignorer le blocage du courrier indésirable</p></td>
<td><p></p></td>
<td><p>Il s’agit du SID connu pour les serveurs sécurisés en externe.</p></td>
</tr>
<tr class="odd">
<td><p>Serveurs Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Envoyer les propriétés étendues XMessageContext</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Envoyer les propriétés étendues XMessageContext</p></td>
<td><p></p></td>
<td><p>Il s’agit du SID connu pour les serveurs de boîtes aux lettres.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Envoyer les propriétés étendues XMessageContext</p></td>
<td><p></p></td>
<td><p>Il s’agit du SID connu pour les serveurs de transport Edge.</p></td>
</tr>
<tr class="even">
<td><p>Serveurs Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Envoyer un index FAST XMessageContext</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Envoyer un index FAST XMessageContext</p></td>
<td><p></p></td>
<td><p>Il s’agit du SID connu pour les serveurs de boîtes aux lettres.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Envoyer un index FAST XMessageContext</p></td>
<td><p></p></td>
<td><p>Il s’agit du SID connu pour les serveurs de transport Edge.</p></td>
</tr>
<tr class="odd">
<td><p>Serveurs Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Ignorer la limite de taille du message</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Ignorer la limite de taille du message</p></td>
<td><p></p></td>
<td><p>Il s’agit du SID connu pour les serveurs de boîtes aux lettres.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Ignorer la limite de taille du message</p></td>
<td><p></p></td>
<td><p>Il s’agit du SID connu pour les serveurs de transport Edge.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Ignorer la limite de taille du message</p></td>
<td><p></p></td>
<td><p>Il s’agit du SID connu pour les serveurs sécurisés en externe.</p></td>
</tr>
<tr class="odd">
<td><p>Serveurs Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Accepter les en-têtes d’organisation</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Accepter les en-têtes d’organisation</p></td>
<td><p></p></td>
<td><p>Il s’agit du SID connu pour les serveurs de boîtes aux lettres.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Accepter les en-têtes d’organisation</p></td>
<td><p></p></td>
<td><p>Il s’agit du SID connu pour les serveurs de transport Edge.</p></td>
</tr>
<tr class="even">
<td><p>Serveurs Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Envoyer le cache de destinataires AD XMessageContext</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Envoyer le cache de destinataires AD XMessageContext</p></td>
<td><p></p></td>
<td><p>Il s’agit du SID connu pour les serveurs de boîtes aux lettres.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Envoyer le cache de destinataires AD XMessageContext</p></td>
<td><p></p></td>
<td><p>Il s’agit du SID connu pour les serveurs de transport Edge.</p></td>
</tr>
<tr class="odd">
<td><p>Serveurs Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Envoyer des messages au serveur</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Envoyer des messages au serveur</p></td>
<td><p></p></td>
<td><p>Il s’agit du SID connu pour les serveurs de boîtes aux lettres.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Envoyer des messages au serveur</p></td>
<td><p></p></td>
<td><p>Il s’agit du SID connu pour les serveurs de transport Edge.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Envoyer des messages au serveur</p></td>
<td><p></p></td>
<td><p>Il s’agit du SID connu pour les serveurs sécurisés en externe.</p></td>
</tr>
<tr class="odd">
<td><p>Serveurs Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Accepter un expéditeur de domaine faisant autorité</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Accepter un expéditeur de domaine faisant autorité</p></td>
<td><p></p></td>
<td><p>Il s’agit du SID connu pour les serveurs de boîtes aux lettres.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Accepter un expéditeur de domaine faisant autorité</p></td>
<td><p></p></td>
<td><p>Il s’agit du SID connu pour les serveurs de transport Edge.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Accepter un expéditeur de domaine faisant autorité</p></td>
<td><p></p></td>
<td><p>Il s’agit du SID connu pour les serveurs sécurisés en externe.</p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p></p></td>
<td><p></p></td>
<td><p></p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


## Création de connecteurs d'envoi SMTP

Le tableau suivant répertorie les autorisations qui sont définies lorsque vous créez des connecteurs d'envoi.

### Nom unique de l’objet : CN=\<Nom du connecteur\>,CN=Connexions,CN=\<groupe de routage\>,CN=Groupes de routage, CN=\<groupe d’administration\>,CN=\<organisation\>

<table style="width:100%;">
<colgroup>
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
</colgroup>
<thead>
<tr class="header">
<th>Compte</th>
<th>Type d’ACE</th>
<th>Héritage</th>
<th>Autorisations</th>
<th>Sur propriété/S’applique à</th>
<th>Commentaires</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>AUTORITÉ NT\CONNEXION ANONYME</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Envoyer les en-têtes de routage</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Serveurs Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Envoyer les en-têtes d’organisation</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Envoyer les en-têtes d’organisation</p></td>
<td><p></p></td>
<td><p>Il s’agit du SID connu pour les serveurs de boîtes aux lettres.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Envoyer les en-têtes d’organisation</p></td>
<td><p></p></td>
<td><p>Il s’agit du SID connu pour les serveurs de transport Edge.</p></td>
</tr>
<tr class="odd">
<td><p>Serveurs Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Envoyer les en-têtes de forêt</p></td>
<td><p></p></td>
<td><p>Il s’agit du SID connu pour les serveurs de boîtes aux lettres.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Envoyer les en-têtes de forêt</p></td>
<td><p></p></td>
<td><p>Il s’agit du SID connu pour les serveurs de boîtes aux lettres.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Envoyer les en-têtes de forêt</p></td>
<td><p></p></td>
<td><p>Il s’agit du SID connu pour les serveurs de transport Edge.</p></td>
</tr>
<tr class="even">
<td><p>Serveurs Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Envoyer XShadow</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Envoyer XShadow</p></td>
<td><p></p></td>
<td><p>Il s’agit du SID connu pour les serveurs de boîtes aux lettres.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Envoyer XShadow</p></td>
<td><p></p></td>
<td><p>Il s’agit du SID connu pour les serveurs de transport Edge.</p></td>
</tr>
<tr class="odd">
<td><p>Serveurs Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Envoyer les en-têtes de routage</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-10</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Envoyer les en-têtes de routage</p></td>
<td><p></p></td>
<td><p>Il s'agit du SID connu pour les serveurs partenaires.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Envoyer les en-têtes de routage</p></td>
<td><p></p></td>
<td><p>Il s’agit du SID connu pour les serveurs de boîtes aux lettres.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Envoyer les en-têtes de routage</p></td>
<td><p></p></td>
<td><p>Il s’agit du SID connu pour les serveurs de transport Edge.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Envoyer les en-têtes de routage</p></td>
<td><p></p></td>
<td><p>Il s’agit du SID connu pour les serveurs sécurisés en externe.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-24</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Envoyer les en-têtes de routage</p></td>
<td><p></p></td>
<td><p>Il s’agit du SID connu pour les serveurs Exchange hérités.</p></td>
</tr>
<tr class="odd">
<td><p>Serveurs Exchange</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Envoyer Exch50</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Envoyer Exch50</p></td>
<td><p></p></td>
<td><p>Il s’agit du SID connu pour les serveurs de boîtes aux lettres.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Envoyer Exch50</p></td>
<td><p></p></td>
<td><p>Il s’agit du SID connu pour les serveurs de transport Edge.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Envoyer Exch50</p></td>
<td><p></p></td>
<td><p>Il s’agit du SID connu pour les serveurs sécurisés en externe.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-24</p></td>
<td><p>ACE Autoriser</p></td>
<td><p>Tout</p></td>
<td><p>Envoyer Exch50</p></td>
<td><p></p></td>
<td><p>Il s’agit du SID connu pour les serveurs Exchange hérités.</p></td>
</tr>
</tbody>
</table>

