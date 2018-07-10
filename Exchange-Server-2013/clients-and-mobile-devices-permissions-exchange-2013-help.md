---
title: 'Autorisations des clients et des périphériques mobiles: Exchange 2013 Help'
TOCTitle: Autorisations des clients et des périphériques mobiles
ms:assetid: 57eca42a-5a7f-4c65-89f0-7a84f2dbea19
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dd638131(v=EXCHG.150)
ms:contentKeyID: 50478248
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Autorisations des clients et des périphériques mobiles

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2015-11-10_

Les autorisations requises pour effectuer des tâches pour les clients et périphériques mobiles varient en fonction de la procédure effectuée ou de la cmdlet que vous voulez exécuter. Pour plus d’informations sur les fonctionnalités de clients et de périphériques mobiles, voir [Clients et mobilité](clients-and-mobile-exchange-2013-help.md).

Pour trouver les autorisations dont vous avez besoin pour effectuer la procédure ou exécuter la cmdlet, procédez comme suit :

1.  Dans le tableau suivant, recherchez la fonctionnalité la plus adaptée à la procédure que vous souhaitez effectuer ou à la cmdlet que vous souhaitez exécuter.

2.  Ensuite, examinez les autorisations requises pour la fonctionnalité. Un de ces groupes de rôles, un groupe de rôles personnalisé équivalent ou un rôle de gestion équivalent doit vous être attribué. Vous pouvez également cliquer sur un groupe de rôles pour visualiser ses rôles de gestion. Si une fonctionnalité affiche plusieurs groupes de rôles, seul l’un de ces groupes de rôles doit vous être attribué pour que vous puissiez exploiter cette même fonctionnalité. Pour plus d’informations sur les groupes de rôles et les rôles de gestion, consultez la rubrique [Présentation du contrôle d'accès basé sur un rôle](understanding-role-based-access-control-exchange-2013-help.md).

3.  Maintenant, exécutez la cmdlet **Get-ManagementRoleAssignment** pour vérifier si les groupes de rôles ou les rôles de gestion qui vous ont été attribués vous permettent de bénéficier des autorisations nécessaires pour gérer la fonctionnalité.
    
    > [!NOTE]
    > Le rôle de gestion de rôle doit vous être attribué pour exécuter la cmdlet <strong>Get-ManagementRoleAssignment</strong>. Si vous ne bénéficiez pas des autorisations pour exécuter la cmdlet <strong>Get-ManagementRoleAssignment</strong>, demandez à votre administrateur Exchange de récupérer les groupes de rôles ou les rôles de gestion qui vous sont attribués.


Si vous souhaitez déléguer la possibilité de gérer une fonctionnalité à un autre utilisateur, voir [Déléguer les attributions de rôles](delegate-role-assignments-exchange-2013-help.md).

> [!NOTE]
> Certaines fonctionnalités nécessitent peut-être des autorisations de type administrateur local sur le serveur que vous souhaitez gérer. Pour gérer ces fonctionnalités, vous devez être membre d’un groupe Administrateurs local sur ce serveur.


## Autorisations du serveur d’accès au client

Vous pouvez configurer les fonctionnalités suivantes pour le serveur d’accès au client.

Les utilisateurs auxquels est affecté le groupe de rôles de gestion de l’organisation en affichage seul peuvent visualiser la configuration des fonctionnalités dans le tableau suivant. Pour plus d’informations, consultez la rubrique Afficher uniquement la gestion de l’organisation[Gestion de l’organisation en affichage seul](view-only-organization-management-exchange-2013-help.md).


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Fonctionnalité</th>
<th>Autorisations requises</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Paramètres de tableau du serveur d’accès au client</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p>
<p><a href="server-management-exchange-2013-help.md">Gestion du serveur</a></p></td>
</tr>
<tr class="even">
<td><p>Paramètres du serveur d’accès au client</p></td>
<td><p><a href="server-management-exchange-2013-help.md">Gestion du serveur</a></p></td>
</tr>
<tr class="odd">
<td><p>Paramètres de canal de messagerie du service d’accès au client</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p>
<p><a href="server-management-exchange-2013-help.md">Gestion du serveur</a></p></td>
</tr>
<tr class="even">
<td><p>Paramètres utilisateur d’accès au client</p></td>
<td><p><a href="server-management-exchange-2013-help.md">Gestion du serveur</a></p></td>
</tr>
<tr class="odd">
<td><p>Paramètres de répertoire virtuel d’accès au client</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p>
<p><a href="server-management-exchange-2013-help.md">Gestion du serveur</a></p></td>
</tr>
<tr class="even">
<td><p>Paramètres d’accès au client RPC</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p>
<p><a href="server-management-exchange-2013-help.md">Gestion du serveur</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">Gestion de l’organisation en affichage seul</a></p></td>
</tr>
<tr class="odd">
<td><p>Paramètres de proxy de notification Push</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gestion des destinataires</a></p></td>
</tr>
<tr class="even">
<td><p>Paramètres de redirection de l’authentification OAuth</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p></td>
</tr>
</tbody>
</table>


## Exchange ActiveSync, autorisations

Vous pouvez configurer ce qui suit pour Exchange ActiveSync.

Les utilisateurs auxquels est affecté le groupe de rôles de gestion de l’organisation en affichage seul peuvent visualiser la configuration des fonctionnalités dans le tableau suivant. Pour plus d’informations, consultez la rubrique Afficher uniquement la gestion de l’organisation[Gestion de l’organisation en affichage seul](view-only-organization-management-exchange-2013-help.md).


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Fonctionnalité</th>
<th>Autorisations requises</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Exchange ActiveSyncParamètres AutoBlock</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p></td>
</tr>
<tr class="even">
<td><p>Paramètres de la stratégie de boîte aux lettres d’Exchange ActiveSync</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p>
<p><a href="server-management-exchange-2013-help.md">Gestion du serveur</a></p></td>
</tr>
<tr class="odd">
<td><p>Paramètres du serveur Exchange ActiveSync</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p>
<p><a href="server-management-exchange-2013-help.md">Gestion du serveur</a></p></td>
</tr>
<tr class="even">
<td><p>Paramètres Exchange ActiveSync</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p>
<p><a href="server-management-exchange-2013-help.md">Gestion du serveur</a></p></td>
</tr>
<tr class="odd">
<td><p>Paramètres utilisateur d’Exchange ActiveSync</p></td>
<td><p><a href="recipient-management-exchange-2013-help.md">Gestion des destinataires</a></p></td>
</tr>
<tr class="even">
<td><p>Paramètres du répertoire virtuel Exchange ActiveSync</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p>
<p><a href="server-management-exchange-2013-help.md">Gestion du serveur</a></p></td>
</tr>
<tr class="odd">
<td><p>Paramètres de stratégie de boîte aux lettres de périphérique mobile</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p>
<p><a href="server-management-exchange-2013-help.md">Gestion du serveur</a></p></td>
</tr>
<tr class="even">
<td><p>Paramètres utilisateur de périphérique mobile</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p>
<p><a href="server-management-exchange-2013-help.md">Gestion du serveur</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gestion des destinataires</a></p></td>
</tr>
</tbody>
</table>


## Autorisations de découverte automatique

Vous pouvez configurer ce qui suit pour le service de découverte automatique.

Les utilisateurs auxquels est affecté le groupe de rôles de gestion de l’organisation en affichage seul peuvent visualiser la configuration des fonctionnalités dans le tableau suivant. Pour plus d’informations, consultez la rubrique Afficher uniquement la gestion de l’organisation[Gestion de l’organisation en affichage seul](view-only-organization-management-exchange-2013-help.md).


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Fonctionnalité</th>
<th>Autorisations requises</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Paramètres de configuration du service de découverte automatique</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p>
<p><a href="server-management-exchange-2013-help.md">Gestion du serveur</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">Gestion de l’organisation en affichage seul</a></p>
<p><a href="delegated-setup-exchange-2013-help.md">Installation déléguée</a></p>
<p><a href="hygiene-management-exchange-2013-help.md">Gestion de l’hygiène</a></p></td>
</tr>
<tr class="even">
<td><p>Paramètres de répertoire virtuel de découverte automatique</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p>
<p><a href="server-management-exchange-2013-help.md">Gestion du serveur</a></p></td>
</tr>
</tbody>
</table>


## Autorisations du service de disponibilité

Vous pouvez configurer ce qui suit pour le service de disponibilité.

Les utilisateurs auxquels est affecté le groupe de rôles de gestion de l’organisation en affichage seul peuvent visualiser la configuration des fonctionnalités dans le tableau suivant. Pour plus d’informations, consultez la rubrique Afficher uniquement la gestion de l’organisation[Gestion de l’organisation en affichage seul](view-only-organization-management-exchange-2013-help.md).


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Fonctionnalité</th>
<th>Autorisations requises</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Paramètres d’espace d’adressage de service de disponibilité</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">Gestion de l’organisation en affichage seul</a></p></td>
</tr>
<tr class="even">
<td><p>Paramètres de configuration du service de disponibilité</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p>
<p><a href="server-management-exchange-2013-help.md">Gestion du serveur</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">Gestion de l’organisation en affichage seul</a></p></td>
</tr>
</tbody>
</table>


## Autorisations de limitation du client

Vous pouvez configurer ce qui suit pour la limitation de client.

Les utilisateurs auxquels est affecté le groupe de rôles de gestion de l’organisation en affichage seul peuvent visualiser la configuration des fonctionnalités dans le tableau suivant. Pour plus d’informations, consultez la rubrique Afficher uniquement la gestion de l’organisation[Gestion de l’organisation en affichage seul](view-only-organization-management-exchange-2013-help.md).


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Fonctionnalité</th>
<th>Autorisations requises</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Paramètres de limitation de client</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">Gestion de l’organisation en affichage seul</a></p></td>
</tr>
</tbody>
</table>


## Autorisations des services Web Exchange

Vous pouvez configurer ce qui suit pour les répertoires virtuels des services Web.

Les utilisateurs auxquels est affecté le groupe de rôles de gestion de l’organisation en affichage seul peuvent visualiser la configuration des fonctionnalités dans le tableau suivant. Pour plus d’informations, consultez la rubrique Afficher uniquement la gestion de l’organisation[Gestion de l’organisation en affichage seul](view-only-organization-management-exchange-2013-help.md).


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Fonctionnalité</th>
<th>Autorisations requises</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Paramètres de répertoire virtuel des services Web Exchange</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p>
<p><a href="server-management-exchange-2013-help.md">Gestion du serveur</a></p></td>
</tr>
<tr class="even">
<td><p>Tester les services Web Exchange</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p>
<p><a href="server-management-exchange-2013-help.md">Gestion du serveur</a></p></td>
</tr>
<tr class="odd">
<td><p>Tester les services Web Outlook</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p></td>
</tr>
</tbody>
</table>


## Autorisations Outlook Anywhere

Vous pouvez configurer et gérer les paramètres suivants pour Outlook Anywhere.

Les utilisateurs auxquels est affecté le groupe de rôles de gestion de l’organisation en affichage seul peuvent visualiser la configuration des fonctionnalités dans le tableau suivant. Pour plus d’informations, consultez la rubrique Afficher uniquement la gestion de l’organisation[Gestion de l’organisation en affichage seul](view-only-organization-management-exchange-2013-help.md).


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Fonctionnalité</th>
<th>Autorisations requises</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Configuration d’Outlook Anywhere (activer, désactiver, modifier et afficher)</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p>
<p><a href="server-management-exchange-2013-help.md">Gestion du serveur</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">Gestion de l’organisation en affichage seul</a></p>
<p><a href="delegated-setup-exchange-2013-help.md">Installation déléguée</a></p>
<p><a href="hygiene-management-exchange-2013-help.md">Gestion de l’hygiène</a></p></td>
</tr>
<tr class="even">
<td><p>Composant proxy RPC sur HTTP</p></td>
<td><p>Administrateur de serveur local</p></td>
</tr>
<tr class="odd">
<td><p>Tester la connectivité Outlook Anywhere</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">Gestion de l’organisation en affichage seul</a></p>
<p><a href="server-management-exchange-2013-help.md">Gestion du serveur</a></p></td>
</tr>
</tbody>
</table>


## Autorisations Outlook Web App

Vous pouvez utiliser les fonctionnalités suivantes pour afficher les paramètres Outlook Web App, contrôler la sécurité et l’accès utilisateur à Outlook Web App, et tester la connectivité d’Outlook Web App.

Les utilisateurs auxquels est affecté le groupe de rôles de gestion de l’organisation en affichage seul peuvent visualiser la configuration des fonctionnalités dans le tableau suivant. Pour plus d’informations, consultez la rubrique Afficher uniquement la gestion de l’organisation[Gestion de l’organisation en affichage seul](view-only-organization-management-exchange-2013-help.md).


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Fonctionnalité</th>
<th>Autorisations requises</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Éditeur de graphiques</p></td>
<td><p>Administrateur de serveur local</p></td>
</tr>
<tr class="even">
<td><p>Gestionnaire des services Internet (IIS)</p></td>
<td><p>Administrateur de serveur local</p></td>
</tr>
<tr class="odd">
<td><p>ISA Server 2006</p></td>
<td><p>Administrateur d’entreprise ISA Server</p></td>
</tr>
<tr class="even">
<td><p>Stratégies de boîte aux lettres Outlook Web App</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gestion des destinataires</a></p></td>
</tr>
<tr class="odd">
<td><p>Répertoires virtuels Outlook Web App</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p>
<p><a href="server-management-exchange-2013-help.md">Gestion du serveur</a></p></td>
</tr>
<tr class="even">
<td><p>Éditeur du Registre</p></td>
<td><p>Administrateur de serveur local</p></td>
</tr>
<tr class="odd">
<td><p>Configuration S/MIME</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p></td>
</tr>
<tr class="even">
<td><p>Éditeur de texte</p></td>
<td><p>Administrateur de serveur local</p></td>
</tr>
<tr class="odd">
<td><p>Afficher les stratégies de boîte aux lettres Outlook Web App</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gestion des destinataires</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">Gestion de l’organisation en affichage seul</a></p>
<p><a href="delegated-setup-exchange-2013-help.md">Installation déléguée</a></p>
<p><a href="hygiene-management-exchange-2013-help.md">Gestion de l’hygiène</a></p></td>
</tr>
</tbody>
</table>


## Autorisations POP3 et IMAP4

Vous pouvez configurer ce qui suit pour POP3 et IMAP4.

Les utilisateurs auxquels est affecté le groupe de rôles de gestion de l’organisation en affichage seul peuvent visualiser la configuration des fonctionnalités dans le tableau suivant. Pour plus d’informations, consultez la rubrique Afficher uniquement la gestion de l’organisation[Gestion de l’organisation en affichage seul](view-only-organization-management-exchange-2013-help.md).


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Fonctionnalité</th>
<th>Autorisations requises</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Paramètres IMAP4</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p>
<p><a href="server-management-exchange-2013-help.md">Gestion du serveur</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">Gestion de l’organisation en affichage seul</a></p></td>
</tr>
<tr class="even">
<td><p>Paramètres POP3</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p>
<p><a href="server-management-exchange-2013-help.md">Gestion du serveur</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">Gestion de l’organisation en affichage seul</a></p></td>
</tr>
<tr class="odd">
<td><p>Tester les paramètres IMAP4</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p>
<p><a href="server-management-exchange-2013-help.md">Gestion du serveur</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">Gestion de l’organisation en affichage seul</a></p></td>
</tr>
<tr class="even">
<td><p>Tester les paramètres POP3</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p>
<p><a href="server-management-exchange-2013-help.md">Gestion du serveur</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">Gestion de l’organisation en affichage seul</a></p></td>
</tr>
</tbody>
</table>


## Autorisations du répertoire virtuel Windows PowerShell

Vous pouvez configurer ce qui suit pour Windows PowerShell.

Les utilisateurs auxquels est affecté le groupe de rôles de gestion de l’organisation en affichage seul peuvent visualiser la configuration des fonctionnalités dans le tableau suivant. Pour plus d’informations, consultez la rubrique Afficher uniquement la gestion de l’organisation[Gestion de l’organisation en affichage seul](view-only-organization-management-exchange-2013-help.md).


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Fonctionnalité</th>
<th>Autorisations requises</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Tester Windows PowerShell</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p></td>
</tr>
<tr class="even">
<td><p>Paramètres de Windows PowerShell</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p></td>
</tr>
</tbody>
</table>


## Autorisations de messagerie texte

Vous pouvez configurer ce qui suit pour la messagerie texte.

Les utilisateurs auxquels est affecté le groupe de rôles de gestion de l’organisation en affichage seul peuvent visualiser la configuration des fonctionnalités dans le tableau suivant. Pour plus d’informations, consultez la rubrique Afficher uniquement la gestion de l’organisation[Gestion de l’organisation en affichage seul](view-only-organization-management-exchange-2013-help.md).


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Fonctionnalité</th>
<th>Autorisations requises</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Paramètres de notification de la messagerie texte</p></td>
<td><p><a href="recipient-management-exchange-2013-help.md">Gestion des destinataires</a></p></td>
</tr>
<tr class="even">
<td><p>Paramètres de la messagerie texte</p></td>
<td><p><a href="recipient-management-exchange-2013-help.md">Gestion des destinataires</a></p></td>
</tr>
<tr class="odd">
<td><p>Paramètres utilisateur de la messagerie texte</p></td>
<td><p><a href="mytextmessaging-role-exchange-2013-help.md">Rôle MyTextMessaging</a></p>
<p>Les utilisateurs peuvent configurer les paramètres de messagerie texte sur leur propre boîte aux lettres. Les administrateurs ne peuvent pas configurer les paramètres de messagerie texte sur la boîte aux lettres d’un autre utilisateur.</p></td>
</tr>
</tbody>
</table>

