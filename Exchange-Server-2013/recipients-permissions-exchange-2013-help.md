---
title: 'Autorisations des destinataires: Exchange 2013 Help'
TOCTitle: Autorisations des destinataires
ms:assetid: 5b690bcb-c6df-4511-90e1-08ca91f43b37
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dd638132(v=EXCHG.150)
ms:contentKeyID: 50478271
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Autorisations des destinataires

 

_**Sapplique à :**Exchange Server 2013_

_**Dernière rubrique modifiée :**2015-03-09_

Les autorisations nécessaires pour effectuer les tâches de gestion des destinataires varient en fonction de la procédure exécutée ou de la cmdlet à exécuter.

Pour trouver les autorisations dont vous avez besoin pour effectuer la procédure ou exécuter la cmdlet, procédez comme suit :

1.  Dans le tableau suivant, recherchez la fonctionnalité la plus adaptée à la procédure que vous souhaitez effectuer ou à la cmdlet que vous souhaitez exécuter.

2.  Ensuite, examinez les autorisations requises pour la fonctionnalité. Un de ces groupes de rôles, un groupe de rôles personnalisé équivalent ou un rôle de gestion équivalent doit vous être attribué. Vous pouvez également cliquer sur un groupe de rôles pour visualiser ses rôles de gestion. Si une fonctionnalité affiche plusieurs groupes de rôles, seul l’un de ces groupes de rôles doit vous être attribué pour que vous puissiez exploiter cette même fonctionnalité. Pour plus d’informations sur les groupes de rôles et les rôles de gestion, consultez la rubrique [Présentation du contrôle d'accès basé sur un rôle](understanding-role-based-access-control-exchange-2013-help.md).

3.  Maintenant, exécutez la cmdlet **Get-ManagementRoleAssignment** pour vérifier si les groupes de rôles ou les rôles de gestion qui vous ont été attribués vous permettent de bénéficier des autorisations nécessaires pour gérer la fonctionnalité.
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Le rôle de gestion de rôle doit vous être attribué pour exécuter la cmdlet <strong>Get-ManagementRoleAssignment</strong>. Si vous ne bénéficiez pas des autorisations pour exécuter la cmdlet <strong>Get-ManagementRoleAssignment</strong>, demandez à votre administrateur Exchange de récupérer les groupes de rôles ou les rôles de gestion qui vous sont attribués.</td>
    </tr>
    </tbody>
    </table>


Si vous souhaitez déléguer la possibilité de gérer une fonctionnalité à un autre utilisateur, voir [Déléguer les attributions de rôles](delegate-role-assignments-exchange-2013-help.md).

## Autorisations du serveur de boîtes aux lettres

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
<td><p>Réparation du calendrier, configuration du serveur</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p>
<p><a href="server-management-exchange-2013-help.md">Gestion du serveur</a></p></td>
</tr>
<tr class="even">
<td><p>Délégation des serveurs de boîtes aux lettres</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p></td>
</tr>
<tr class="odd">
<td><p>Stratégies d'adresse de messagerie</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p>
<p><a href="server-management-exchange-2013-help.md">Gestion du serveur</a></p></td>
</tr>
<tr class="even">
<td><p>Recherche Exchange</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">Gestion de l’organisation en affichage seul</a></p>
<p><a href="server-management-exchange-2013-help.md">Gestion du serveur</a></p></td>
</tr>
<tr class="odd">
<td><p>Recherche Exchange – Diagnostics</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">Gestion de l’organisation en affichage seul</a></p>
<p>Prise en charge du rôle de diagnostics</p>
<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Le rôle de Diagnostics du support n'est pas affecté à un groupe de rôles. Pour plus d'informations, consultez la rubrique <a href="add-a-role-to-a-user-or-usg-exchange-2013-help.md">Ajouter un rôle à un utilisateur ou un groupe de sécurité universel</a>.</td>
</tr>
</tbody>
</table>

</td>
</tr>
<tr class="even">
<td><p>Mesures de groupe</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p>
<p><a href="server-management-exchange-2013-help.md">Gestion du serveur</a></p></td>
</tr>
<tr class="odd">
<td><p>Importer et exporter</p></td>
<td><p>Rôle d'importation et d'exportation de boîtes aux lettres</p>
<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Le rôle d'importation et d'exportation de boîte aux lettres n'est pas affecté à un groupe de rôles. Pour plus d'informations, consultez la rubrique <a href="mailbox-import-export-role-exchange-2013-help.md">Rôle d’importation et d’exportation de boîtes aux lettres</a>.</td>
</tr>
</tbody>
</table>

</td>
</tr>
<tr class="even">
<td><p>Assistants de boîte aux lettres</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p>
<p><a href="server-management-exchange-2013-help.md">Gestion du serveur</a></p></td>
</tr>
<tr class="odd">
<td><p>Déplacements de boîte aux lettres</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gestion des destinataires</a></p></td>
</tr>
<tr class="even">
<td><p>Récupération de boîte aux lettres</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p></td>
</tr>
<tr class="odd">
<td><p>Demande de réparation de boîtes aux lettres</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p>
<p><a href="server-management-exchange-2013-help.md">Gestion du serveur</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gestion des destinataires</a></p></td>
</tr>
<tr class="even">
<td><p>Demande de restauration de boîtes aux lettres</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p></td>
</tr>
<tr class="odd">
<td><p>Configuration du serveur de boîtes aux lettres</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p>
<p><a href="server-management-exchange-2013-help.md">Gestion du serveur</a></p></td>
</tr>
<tr class="even">
<td><p>Gestion du service Indexeur de recherche Exchange sur un serveur de boîtes aux lettres</p></td>
<td><p>Administrateur local sur le serveur de boîtes aux lettres</p></td>
</tr>
<tr class="odd">
<td><p>Connectivité MAPI</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p>
<p><a href="server-management-exchange-2013-help.md">Gestion du serveur</a></p></td>
</tr>
<tr class="even">
<td><p>Répertoires virtuels de carnet d'adresses en mode hors connexion</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p>
<p><a href="server-management-exchange-2013-help.md">Gestion du serveur</a></p></td>
</tr>
<tr class="odd">
<td><p>Supprimer la banque de boîtes aux lettres</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p>
<p><a href="server-management-exchange-2013-help.md">Gestion du serveur</a></p></td>
</tr>
</tbody>
</table>


## Autorisations de calendrier et de partage

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
<td><p>Configuration du calendrier</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gestion des destinataires</a></p>
<p><a href="help-desk-exchange-2013-help.md">Support technique</a></p></td>
</tr>
<tr class="even">
<td><p>Diagnostics de calendrier</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p>
<p><a href="records-management-exchange-2013-help.md">Gestion des enregistrements</a></p>
<p><a href="hygiene-management-exchange-2013-help.md">Gestion de l’hygiène</a></p>
<p><a href="compliance-management-exchange-2013-help.md">Gestion de la conformité</a></p>
<p><a href="help-desk-exchange-2013-help.md">Support technique</a></p></td>
</tr>
<tr class="odd">
<td><p>Traitement du calendrier</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gestion des destinataires</a></p>
<p><a href="help-desk-exchange-2013-help.md">Support technique</a></p></td>
</tr>
<tr class="even">
<td><p>Notifications</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gestion des destinataires</a></p></td>
</tr>
<tr class="odd">
<td><p>Relations des organisations</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p></td>
</tr>
<tr class="even">
<td><p>Stratégies de partage</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p></td>
</tr>
</tbody>
</table>


## Autorisations de configuration de boîtes aux lettres de ressources

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
<td><p>Stratégies de réservation</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gestion des destinataires</a></p>
<p><a href="help-desk-exchange-2013-help.md">Support technique</a></p></td>
</tr>
<tr class="even">
<td><p>Délégation</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gestion des destinataires</a></p></td>
</tr>
<tr class="odd">
<td><p>Configuration du schéma des boîtes aux lettres de ressources</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p></td>
</tr>
</tbody>
</table>


## Autorisations de base de données de boîtes aux lettres

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
<td><p>Bases de données de boîtes aux lettres</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p>
<p><a href="server-management-exchange-2013-help.md">Gestion du serveur</a></p></td>
</tr>
</tbody>
</table>


## Autorisations de configuration des destinataires

Ce tableau contient les différentes autorisations requises pour gérer les destinataires.

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
<td><p>Liste d'adresses, liste d'adresses globale</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p></td>
</tr>
<tr class="even">
<td><p>Anti-spam</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gestion des destinataires</a></p></td>
</tr>
<tr class="odd">
<td><p>Applications pour Outlook</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">Gestion de l’organisation en affichage seul</a></p>
<p><a href="help-desk-exchange-2013-help.md">Support technique</a></p></td>
</tr>
<tr class="even">
<td><p>Application de stratégies de partage</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gestion des destinataires</a></p></td>
</tr>
<tr class="odd">
<td><p>Arbitrage</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p></td>
</tr>
<tr class="even">
<td><p>Archivage de la connectivité</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">Gestion de l’organisation en affichage seul</a></p>
<p><a href="server-management-exchange-2013-help.md">Gestion du serveur</a></p></td>
</tr>
<tr class="odd">
<td><p>Affectation de carnets d'adresses en mode hors connexion</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gestion des destinataires</a></p></td>
</tr>
<tr class="even">
<td><p>Répondeur automatique</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gestion des destinataires</a></p>
<p><a href="help-desk-exchange-2013-help.md">Support technique</a></p></td>
</tr>
<tr class="odd">
<td><p>Configuration du calendrier</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gestion des destinataires</a></p></td>
</tr>
<tr class="even">
<td><p>Réparation du calendrier</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gestion des destinataires</a></p></td>
</tr>
<tr class="odd">
<td><p>Paramètres d'agrégation des contacts</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gestion des destinataires</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">Gestion de l’organisation en affichage seul</a></p></td>
</tr>
<tr class="even">
<td><p>Boîtes aux lettres déconnectées</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gestion des destinataires</a></p>
<p><a href="help-desk-exchange-2013-help.md">Support technique</a></p></td>
</tr>
<tr class="odd">
<td><p>Groupes de distribution</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gestion des destinataires</a></p></td>
</tr>
<tr class="even">
<td><p>Groupes de distribution dynamique</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gestion des destinataires</a></p></td>
</tr>
<tr class="odd">
<td><p>Adresses de messagerie</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gestion des destinataires</a></p>
<p><a href="um-management-exchange-2013-help.md">Gestion de messagerie unifiée</a></p></td>
</tr>
<tr class="even">
<td><p>Règles de la boîte de réception</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gestion des destinataires</a></p>
<p><a href="help-desk-exchange-2013-help.md">Support technique</a></p></td>
</tr>
<tr class="odd">
<td><p>Contacts de messagerie</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gestion des destinataires</a></p></td>
</tr>
<tr class="even">
<td><p>Infos-courrier</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gestion des destinataires</a></p></td>
</tr>
<tr class="odd">
<td><p>Utilisateur de messagerie</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gestion des destinataires</a></p></td>
</tr>
<tr class="even">
<td><p>Autorisations de dossiers de boîte aux lettres</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gestion des destinataires</a></p>
<p><a href="help-desk-exchange-2013-help.md">Support technique</a></p></td>
</tr>
<tr class="odd">
<td><p>Dossiers de boîtes aux lettres</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gestion des destinataires</a></p></td>
</tr>
<tr class="even">
<td><p>Connectivité MAPI</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p>
<p></p></td>
</tr>
<tr class="odd">
<td><p>Configuration des messages</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gestion des destinataires</a></p>
<p><a href="help-desk-exchange-2013-help.md">Support technique</a></p></td>
</tr>
<tr class="even">
<td><p>Quotas de message</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gestion des destinataires</a></p></td>
</tr>
<tr class="odd">
<td><p>Modération</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gestion des destinataires</a></p></td>
</tr>
<tr class="even">
<td><p>Autorisations et délégation</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p></td>
</tr>
<tr class="odd">
<td><p>Boîtes aux lettres d'archivage</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gestion des destinataires</a></p></td>
</tr>
<tr class="even">
<td><p>Propriétés des données du destinataire</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gestion des destinataires</a></p></td>
</tr>
<tr class="odd">
<td><p>Boîtes aux lettres distantes</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gestion des destinataires</a></p></td>
</tr>
<tr class="even">
<td><p>Rétention et conservation légale</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gestion des destinataires</a></p>
<p><a href="records-management-exchange-2013-help.md">Gestion des enregistrements</a></p></td>
</tr>
<tr class="odd">
<td><p>Envoyer en tant que</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gestion des destinataires</a></p></td>
</tr>
<tr class="even">
<td><p>Configuration de l'orthographe</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gestion des destinataires</a></p>
<p><a href="help-desk-exchange-2013-help.md">Support technique</a></p></td>
</tr>
<tr class="odd">
<td><p>Messagerie unifiée</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p>
<p><a href="um-management-exchange-2013-help.md">Gestion de messagerie unifiée</a></p></td>
</tr>
<tr class="even">
<td><p>Boîtes aux lettres d'utilisateur</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gestion des destinataires</a></p></td>
</tr>
<tr class="odd">
<td><p>Photos de l'utilisateur</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gestion des destinataires</a></p>
<p><a href="help-desk-exchange-2013-help.md">Support technique</a></p></td>
</tr>
</tbody>
</table>


## Autorisations de migration et de déplacement de boîtes aux lettres

Le tableau contient les autorisations nécessaires au déplacement de boîtes aux lettres locales vers des forêts ou des domaines différents et à la migration de boîtes aux lettres locales vers et à partir de votre organisation en nuage.


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
<td><p>Déplacements de boîtes aux lettres (en local ou inter-forêts)</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gestion des destinataires</a></p></td>
</tr>
<tr class="even">
<td><p>Déplacements de boîtes aux lettres (déploiement hybride)</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gestion des destinataires</a></p></td>
</tr>
<tr class="odd">
<td><p>Migration (embarquement et débarquement à partir du nuage)</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gestion des destinataires</a></p></td>
</tr>
</tbody>
</table>

