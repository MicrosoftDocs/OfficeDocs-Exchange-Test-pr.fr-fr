---
title: 'Informations d’identification d’abonnement Edge: Exchange 2013 Help'
TOCTitle: Informations d’identification d’abonnement Edge
ms:assetid: 1d291bc1-9c00-4d1b-8da0-cb81f63d8305
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb266959(v=EXCHG.150)
ms:contentKeyID: 61180531
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Informations d’identification d’abonnement Edge

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2015-03-09_

Cette rubrique explique la façon dont le processus d’abonnement Edge configure des informations d’identification utilisées pour aider à sécuriser le processus de synchronisation EdgeSync et la façon dont EdgeSync utilise ces informations d’identification pour établir une connexion LDAP sécurisée entre un serveur de boîtes aux lettres Exchange 2013 et un serveur de transport Edge. Pour plus d’informations sur le processus d’abonnement Edge, consultez la rubrique [Abonnements Edge](edge-subscriptions-exchange-2013-help.md).

**Contenu de cette rubrique**

Edge Subscription process

EdgeSync replication accounts

Authenticate initial replication

Authenticate scheduled synchronization sessions

Renew EdgeSync replication accounts

## Processus d’abonnement Edge

Le serveur de transport Edge est abonné à un site Active Directory pour établir une relation de synchronisation entre les serveurs de boîtes aux lettres dans un site Active Directory et le serveur de transport Edge abonné. Les informations d’identification configurées lors du processus d’abonnement Edge servent à renforcer la sécurité de la connexion LDAP entre un serveur de boîtes aux lettres et un serveur de transport Edge dans le réseau de périmètre.

Lorsque vous exécutez la cmdlet **New-EdgeSubscription** sur un serveur de transport Edge, les informations d’identification du compte de réplication d’amorçage EdgeSync (ESBRA) sont créées dans l’annuaire AD LDS (Active Directory Lightweight Directory Services) sur le serveur local, puis écrites dans le fichier d’abonnement Edge. Ces informations d’identification permettent uniquement d’établir la synchronisation initiale et expirent 24 heures après la création du fichier d’abonnement Edge. Si le processus d’abonnement Edge n’est pas terminé dans les 24 heures, vous devrez réexécuter la cmdlet **New-EdgeSubscription** pour créer un fichier d’abonnement Edge. Le fichier XML d’abonnement Edge stocke des données de configuration pour l’abonnement Edge.

Le fichier XML d’abonnement Edge contient les données affichées dans le tableau suivant.

### Contenu du fichier d’abonnement Edge

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Données d’abonnement</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>EdgeServerName</strong></p></td>
<td><p>Nom NetBIOS du serveur de transport Edge. Le nom Active Directory de l’abonnement Edge correspond à ce nom.</p></td>
</tr>
<tr class="even">
<td><p><strong>EdgeServerFQDN</strong></p></td>
<td><p>Nom de domaine complet (FQDN) du serveur de transport Edge. Les serveurs de boîtes aux lettres dans le site Active Directory abonné doivent pouvoir localiser le serveur de transport Edge via DNS pour résoudre le nom de domaine complet.</p></td>
</tr>
<tr class="odd">
<td><p><strong>EdgeCertificateBlob</strong></p></td>
<td><p>Clé publique du certificat auto-signé du serveur de transport Edge.</p></td>
</tr>
<tr class="even">
<td><p><strong>ESRAUsername</strong></p></td>
<td><p>Nom attribué au compte ESBRA. Le format du compte ESBRA est le suivant : ESRA.<em>Nom du serveur de transport Edge</em>. ESRA signifie compte de réplication EdgeSync. Vous remarquerez la différence entre ESBRA (compte de réplication d’amorçage initial) et ESRA.</p></td>
</tr>
<tr class="odd">
<td><p><strong>ESRAPassword</strong></p></td>
<td><p>Mot de passe attribué au compte ESBRA. Le mot de passe est créé via un générateur de nombres aléatoires et stocké dans le fichier d’abonnement Edge en texte clair.</p></td>
</tr>
<tr class="even">
<td><p><strong>DateEffet</strong></p></td>
<td><p>Date de création du fichier d’abonnement Edge.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Durée</strong></p></td>
<td><p>Durée de validité de ces informations d’identification avant leur expiration. Le compte ESBRA est uniquement valide pendant 24 heures.</p></td>
</tr>
<tr class="even">
<td><p><strong>AdamSslPort</strong></p></td>
<td><p>Port LDAP sécurisé auquel EdgeSync se lie lors de la synchronisation des données depuis Active Directory vers AD LDS. Par défaut, il s’agit du port TCP 50636.</p></td>
</tr>
<tr class="odd">
<td><p><strong>ProductID</strong></p></td>
<td><p>Informations de licence du serveur de transport Edge. Vous devez acquérir le serveur de transport Edge sous licence avant de créer l’abonnement Edge.</p></td>
</tr>
<tr class="even">
<td><p><strong>VersionNumber</strong></p></td>
<td><p>Numéro de version du fichier d’abonnement Edge.</p></td>
</tr>
<tr class="odd">
<td><p><strong>SerialNumber</strong></p></td>
<td><p>Version Exchange du serveur de transport Edge.</p></td>
</tr>
</tbody>
</table>


> [!NOTE]
> Les informations d’identification du compte ESBRA sont écrites dans le fichier d’abonnement Edge en texte clair. Vous devez protéger ce fichier tout au long du processus d’abonnement. Après l’importation du fichier d’abonnement Edge sur votre organisation Exchange, vous devez immédiatement supprimer le fichier d’abonnement Edge du serveur de transport Edge, du partage réseau que vous avez utilisé pour importer le fichier dans votre organisation Exchange et des supports amovibles.


Retour au début

## Comptes de réplication EdgeSync

Les comptes de réplication EdgeSync (ESRA) constituent un élément important de la sécurité EdgeSync. L’authentification et l’autorisation du compte ESRA correspondent au mécanisme permettant de sécuriser la connexion entre un serveur de transport Edge et un serveur de boîtes aux lettres.

Le compte ESBRA contenu dans le fichier d’abonnement Edge permet d’établir une connexion LDAP sécurisée lors de la synchronisation initiale. Une fois le fichier d’abonnement Edge importé vers un serveur de boîtes aux lettres dans le site Active Directory auquel le serveur de transport Edge est abonné, des comptes ESRA supplémentaires sont créés dans Active Directory pour chaque paire serveur de boîtes aux lettres-serveur de transport Edge. Lors de la synchronisation initiale, les informations d’identification du compte ESRA nouvellement créées sont répliquées dans AD LDS. Ces informations d’identification du compte ESRA permettent de sécuriser les sessions de synchronisation ultérieures.

Les propriétés indiquées dans le tableau suivant sont affectées à chaque compte de réplication EdgeSync.

### Propriétés Ms-Exch-EdgeSyncCredential

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Nom de propriété</th>
<th>Type</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>TargetServerFQDN</strong></p></td>
<td><p>Chaîne</p></td>
<td><p>Serveur de transport Edge acceptant ces informations d’identification.</p></td>
</tr>
<tr class="even">
<td><p><strong>SourceServerFQDN</strong></p></td>
<td><p>Chaîne</p></td>
<td><p>Serveur de boîtes aux lettres présentant ces informations d’identification. Cette valeur est vide si les informations d’identification correspondent aux informations d’identification du compte d’amorçage.</p></td>
</tr>
<tr class="odd">
<td><p><strong>EffectiveTime</strong></p></td>
<td><p>DateTime (UTC)</p></td>
<td><p>Heure de début d’utilisation de ces informations d’identification.</p></td>
</tr>
<tr class="even">
<td><p><strong>ExpirationTime</strong></p></td>
<td><p>DateTime (UTC)</p></td>
<td><p>Heure d’expiration de ces informations d’identification.</p></td>
</tr>
<tr class="odd">
<td><p><strong>UserName</strong></p></td>
<td><p>Chaîne</p></td>
<td><p>Nom d’utilisateur utilisé pour l’authentification.</p></td>
</tr>
<tr class="even">
<td><p><strong>Password</strong></p></td>
<td><p>Octet</p></td>
<td><p>Mot de passe utilisé pour l’authentification. Le mot de passe est chiffré à l’aide de <strong>ms-Exch-EdgeSync-Certificate</strong>.</p></td>
</tr>
</tbody>
</table>


Les sections suivantes de cette rubrique décrivent le mode de configuration et d’utilisation des informations d’identification ESRA lors du processus de synchronisation EdgeSync.

## Configuration du compte de réplication d’amorçage EdgeSync

Lorsque la cmdlet **New-EdgeSubscription** est exécutée sur le serveur de transport Edge, le compte ESBRA est configuré comme suit :

  - Un certificat auto-signé (Edge-Cert) est créé sur le serveur de transport Edge. La clé privée est stockée dans le magasin de l’ordinateur local et écrite dans le fichier d’abonnement Edge.

  - Le compte ESBRA est créé dans AD LDS et les informations d’identification y relatives sont écrites dans le fichier d’abonnement Edge.

  - Pour exporter le fichier d’abonnement Edge, copiez-le sur un support amovible (le serveur Edge n’étant pas dans votre Active Directory, vous ne pouvez pas utiliser de dossier partagé pour l’exportation du fichier). Le fichier peut désormais être importé sur un serveur de boîtes aux lettres.

## Configuration des comptes de réplication EdgeSync dans Active Directory

Lorsque le fichier d’abonnement Edge est importé sur un serveur de boîtes aux lettres, la création d’un enregistrement de l’abonnement Edge dans Active Directory et la configuration d’informations d’identification du compte ESRA supplémentaires sont effectuées selon les étapes suivantes :

1.  Un objet de configuration du serveur de transport Edge est créé dans Active Directory. Le certificat Edge-Cert est écrit sur cet objet en tant qu’attribut.

2.  Chaque serveur de boîtes aux lettres dans le site Active Directory abonné reçoit une notification Active Directory relative à l’enregistrement d’un nouvel abonnement Edge. À réception de la notification, chaque serveur de boîtes aux lettres récupère le compte ESRA.edge et chiffre le compte à l’aide de la clé publique Edge-Cert. Le compte ESRA.edge chiffré est écrit sur l’objet de configuration du serveur de transport Edge.

3.  Chaque serveur de boîtes aux lettres crée un certificat auto-signé (TransportService-Cert). La clé privée est stockée dans le magasin de l’ordinateur local et la clé publique est stockée dans l’objet de configuration du serveur de boîtes aux lettres dans Active Directory.

4.  Chaque serveur de boîtes aux lettres chiffre le compte ESRA.edge à l’aide de la clé publique de son propre certificat TransportService, puis le stocke dans son propre objet de configuration.

5.  Chaque serveur de boîtes aux lettres génère un compte ESRA pour chaque objet de configuration du serveur de transport Edge existant dans Active Directory (ESRA.edge.*Mailboxname.\#*).
    
    Exemple : ESRA.edge.Example.0
    
    Le mot de passe ESRA.edge est créé par un générateur de nombres aléatoires et chiffré à l’aide de la clé publique du certificat TransportService-Cert. Le mot de passe généré a la longueur maximale autorisée pour Windows Server.

6.  Chaque compte ESRA.edge *Mailboxname.\#* est chiffré à l’aide de la clé publique du certificat Edge-Cert et stocké sur l’objet de configuration du serveur de transport Edge dans Active Directory.

Les sections suivantes expliquent l’utilisation de ces comptes lors de la synchronisation EdgeSync.

Retour au début

## Authentification de la réplication initiale

Le compte ESBRA initial est utilisé uniquement lors de l’établissement de la synchronisation initiale. Lors de la première synchronisation EdgeSync, les comptes ESRA supplémentaires, ESRA.edge*Mailboxname.\#*, sont répliqués vers AD LDS. Ces comptes permettent d’identifier ultérieurement les sessions de synchronisation EdgeSync.

Le serveur de boîtes aux lettres chargé d’effectuer la réplication initiale est sélectionné de manière aléatoire. Le premier serveur de boîtes aux lettres dans Active Directory qui effectue une analyse de la topologie et découvre le nouvel abonnement Edge effectue la réplication initiale. Comme cette découverte est basée sur la durée de l’analyse de la topologie, n’importe quel serveur de boîtes aux lettres du site peut effectuer la réplication initiale.

EdgeSync démarre une session LDAP sécurisée du serveur de boîtes aux lettres vers le serveur de transport Edge. Le serveur de transport Edge présente son certificat auto-signé et le serveur de boîtes aux lettres vérifie que le certificat correspond au certificat stocké dans l’objet de configuration du serveur de transport Edge dans Active Directory. Une fois l’identité du serveur de transport Edge vérifiée, le serveur de boîtes aux lettres fournit les informations d’identification du compte ESRA.edge *Mailboxname.\#* au serveur de transport Edge. Le serveur de transport Edge vérifie que les informations d’identification correspondent à celles du compte stocké dans AD LDS.

Le service EdgeSync sur le serveur de boîtes aux lettres transfère ensuite les données de configuration, de topologie et de destinataire d’Active Directory vers AD LDS. La modification de l’objet de configuration du serveur de transport Edge dans Active Directory est répliquée dans AD LDS. AD LDS reçoit les entrées ESRA.edge.*Mailboxname.\#* nouvellement ajoutées et le service d’informations d’identification Microsoft Exchange crée le compte AD LDS correspondant. Ces comptes sont désormais disponibles pour authentifier les sessions de synchronisation EdgeSync planifiées ultérieurement.

## Service d’identification Microsoft Exchange

Le service d’informations d’identification Microsoft Exchange fait partie du processus d’abonnement Edge. Il s’exécute uniquement sur le serveur de transport Edge. Ce service crée les comptes ESRA réciproques dans AD LDS de sorte qu’un serveur de boîtes aux lettres peut s’authentifier auprès d’un serveur de transport Edge pour effectuer la synchronisation EdgeSync. Le service EdgeSync ne communique pas directement avec le service d’informations d’identification Microsoft Exchange. Le service d’informations d’identification Microsoft Exchange communique avec AD LDS et installe les informations d’identification du compte ESRA lorsque le serveur de boîtes aux lettres les met à jour.

Retour au début

## Authentification des sessions de synchronisation planifiées

Une fois la synchronisation EdgeSync initiale terminée, la planification de la synchronisation EdgeSync est établie et les données modifiées dans Active Directory sont régulièrement mises à jour dans AD LDS. Un serveur de boîtes aux lettres démarre une session LDAP sécurisée avec l’instance AD LDS sur le serveur de transport Edge. AD LDS prouve son identité auprès de ce serveur de boîtes aux lettres en présentant son certificat auto-signé. Le serveur de boîtes aux lettres présente ses informations d’identification ESRA.edge à AD LDS. Le mot de passe ESRA.edge est chiffré à l’aide de la clé publique du certificat auto-signé du serveur de boîtes aux lettres. Ces informations d’identification peuvent uniquement être utilisées par ce serveur de boîtes aux lettres spécifique pour s’authentifier auprès d’AD LDS.

Retour au début

## Renouvellement des comptes de réplication EdgeSync

Le mot de passe du compte ESRA doit être conforme à la stratégie de mot de passe du serveur local. Pour empêcher le processus de renouvellement du mot de passe de provoquer un échec d’authentification temporaire, un deuxième compte ESRA.edge est créé sept jours avant l’expiration du premier compte ESRA.edge avec une date effective trois jours avant la date d’expiration du premier compte ESRA. Dès que le deuxième compte ESRA.edge devient effectif, le service EdgeSync cesse d’utiliser le premier compte et commence à utiliser le deuxième compte. Lorsque le délai d’expiration du premier compte est atteint, ces informations d’identification du compte ESRA sont supprimées. Ce processus de renouvellement se poursuit jusqu’à la suppression de l’abonnement Edge.

Retour au début

