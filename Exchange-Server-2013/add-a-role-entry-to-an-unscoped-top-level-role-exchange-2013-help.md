---
title: 'Ajouter une entrée de rôle à un rôle de niveau supérieur non délimité: Exchange 2013 Help'
TOCTitle: Ajouter une entrée de rôle à un rôle de niveau supérieur non délimité
ms:assetid: 52fd3f20-c348-49d5-9bdb-f2cbf780cf2d
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dd979789(v=EXCHG.150)
ms:contentKeyID: 50478193
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Ajouter une entrée de rôle à un rôle de niveau supérieur non délimité

 

_**Sapplique à :**Exchange Server 2013_

_**Dernière rubrique modifiée :**2012-10-03_

Vous pouvez ajouter des scripts et des cmdlets non-Exchange à des rôles de gestion de haut niveau non délimités si vous voulez que les nouveaux scripts ou les nouvelles cmdlets non-Exchange soient disponibles pour les rôles non délimités existants. Ces scripts et cmdlets non-Exchange sont ajoutés en tant qu’entrées de rôles de gestion à des rôles de gestion de haut niveau non délimités. Ils peuvent alors être ajoutés par ces entrées de rôles de haut niveau non délimités ou tout autre rôle non délimité dérivé des rôles de haut niveau. Pour plus d’informations sur les entrées des rôles non délimitées, voir [Présentation des rôles de gestion](understanding-management-roles-exchange-2013-help.md).

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Si vous souhaitez modifier une entrée de rôle sur un rôle de gestion qui contient les cmdlets Exchange, voir <a href="change-a-role-entry-exchange-2013-help.md">Modifier une entrée de rôle</a>.</td>
</tr>
</tbody>
</table>


Souhaitez-vous rechercher les autres tâches de gestion relatives aux rôles ? Consultez la rubrique [Autorisations avancées](advanced-permissions-exchange-2013-help.md).

## Ce qu’il faut savoir avant de commencer ?

  - Durée d’exécution estimée de chaque procédure : 5 minutes

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l’entrée « Rôles de gestion » dans la rubrique [Autorisations pour la gestion des rôles](role-management-permissions-exchange-2013-help.md).

  - Vous devez utiliser l’environnement de ligne de commande Exchange Management Shell pour effectuer ces procédures.

  - L’ajout d’une entrée de rôle à un rôle de haut niveau non délimité n’est inclus dans aucun groupe de rôles de gestion par défaut. Vous devez d’abord attribuer un rôle de gestion des rôles non délimités à un utilisateur, à un groupe de sécurité universel ou à un groupe de rôles auquel appartient l’utilisateur pour que celui-ci puisse ajouter une entrée de rôle de haut niveau non délimité. Pour plus d’informations sur l’ajout d’un rôle à un groupe de rôles, à un utilisateur ou à un groupe de sécurité universel, voir les rubriques suivantes :
    
      - [Gérer des groupes de rôles](manage-role-groups-exchange-2013-help.md)
    
      - [Ajouter un rôle à un utilisateur ou un groupe de sécurité universel](add-a-role-to-a-user-or-usg-exchange-2013-help.md)

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

<table>
<thead>
<tr class="header">
<th><img src="images/Bb125224.tip(EXCHG.150).gif" title="Conseil" alt="Conseil" />Conseil :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.</td>
</tr>
</tbody>
</table>


## Que souhaitez-vous faire ?

## Ajouter une entrée de rôle de script à un rôle de haut niveau non délimité

Si vous voulez ajouter un script à un rôle non délimité existant, utilisez cette procédure. Si vous voulez ajouter une cmdlet non-Exchange à un rôle non délimité existant, voir la section « Ajouter une entrée de rôle de cmdlet non-Exchange à un rôle de haut niveau non délimité » plus loin dans cette rubrique.

Pour ajouter un script Windows PowerShell à un rôle de niveau supérieur non délimité, vous devez ajouter une entrée de rôle de gestion au rôle. L’entrée de rôle contient le nom du script et les paramètres sur le script que vous souhaitez rendre disponibles au rôle.

Le script doit résider dans le répertoire Scripts du chemin d’installation Microsoft Exchange Server 2013 sur chaque serveur exécutant Exchange 2013 où les utilisateurs peuvent se connecter pour exécuter le script. Si un utilisateur a accès pour exécuter un script mais que celui-ci ne se trouve pas sur le serveur Exchange 2013 auquel l’utilisateur est connecté, une erreur se produit. Par défaut, le chemin d’accès au répertoire Scripts est C:\\Program Files\\Microsoft\\Exchange Server\\V15\\Scripts.

Après que vous ayez copié le script sur les serveurs Exchange 2013 appropriés et décidé quels paramètres de script devraient être utilisés, créez l’entrée de rôle à l’aide de la syntaxe suivante.

    Add-ManagementRoleEntry <unscoped top-level role name>\<script filename> -Parameters <parameter 1, parameter 2, parameter...> -Type Script -UnscopedTopLevel

Cet exemple décrit l’ajout du script BulkProvisionUsers.ps1 au rôle de scripts IT Scripts avec les paramètres *Name* et *Location*.

    Add-ManagementRoleEntry "IT Scripts\BulkProvisionUsers.ps1" -Parameters Name, Location -Type Script -UnscopedTopLevel

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>La cmdlet <strong>Add-ManagementRoleEntry</strong> effectue une validation simple pour vous assurer que vous ajoutez uniquement les paramètres qui existent dans le script. Cependant, aucune validation supplémentaire n’est faite après l’ajout de l’entrée de rôle. Si des paramètres sont ultérieurement ajoutés ou supprimés, vous devez manuellement mettre à jour les entrées de rôle qui contiennent le script.</td>
</tr>
</tbody>
</table>


## Ajouter une entrée de rôle de cmdlet non-Exchange à un rôle de haut niveau non délimité

Si vous voulez ajouter une cmdlet non-Exchange à un rôle non délimité existant, utilisez cette procédure. Si vous voulez ajouter un script à un rôle non délimité existant, voir la section « Ajouter une entrée de rôle de script à un rôle de haut niveau non délimité » plus haut dans cette rubrique.

Pour ajouter une cmdlet non Exchange à un rôle de niveau supérieur non délimité, vous devez ajouter une entrée de rôle de gestion au rôle. L’entrée de rôle contient le composant logiciel enfichable de la cmdlet, le nom de cmdlet et les paramètres sur la cmdlet que vous souhaitez rendre disponibles au rôle.

Si vous ajoutez des cmdlets non Exchange au nouveau rôle, les cmdlets doivent être installées sur chaque serveur Exchange 2013 où les utilisateurs peuvent se connecter pour exécuter les cmdlets. Pour apprendre à installer et enregistrer correctement les composants logiciels enfichables Windows qui contiennent les cmdlets que vous souhaitez utiliser, reportez-vous à la documentation de votre produit.

Après avoir installé le composant logiciel Windows PowerShell contenant les cmdlets pour les serveurs Exchange 2013 qui conviennent et avoir choisi les paramètres de cmdlet à utiliser, créez l’entrée de rôle utilisant la syntaxe suivante.

    Add-ManagementRoleEntry <unscoped top-level role name>\<cmdlet name> -PSSnapinName <snap-in name> -Parameters <parameter 1, parameter 2, parameter...> -Type Cmdlet -UnscopedTopLevel

Cet exemple vous indique comment ajouter la cmdlet **Set-WidgetConfiguration** dans le composant logiciel enfichable Contoso.Admin.Cmdlets au rôle Widget Cmdlets avec les paramètres *Database* et *Size*.

    Add-ManagementRoleEntry "Widget Cmdlets\Set-WidgetConfiguration" -PSSnapinName Contoso.Admin.Cmdlets -Parameters Database, Size -Type Cmdlet -UnscopedTopLevel

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>La cmdlet <strong>Add-ManagementRoleEntry</strong> effectue une validation simple pour vous assurer que vous ajoutez uniquement les paramètres qui existent dans la cmdlet. Cependant, aucune validation supplémentaire n’est faite après l’ajout de l’entrée de rôle. Si la cmdlet est modifiée ultérieurement et que des paramètres sont ajoutés ou supprimés, vous devez manuellement mettre à jour les entrées de rôle qui contiennent la cmdlet.</td>
</tr>
</tbody>
</table>


## Autres tâches

Après avoir ajouté une entrée de rôle à un rôle de haut niveau non délimité, vous souhaiterez probablement :

[Ajouter une entrée de rôle à un rôle](add-a-role-entry-to-a-role-exchange-2013-help.md)

[Gérer des groupes de rôles](manage-role-groups-exchange-2013-help.md)

[Gérer les membres de groupes de rôles](manage-role-group-members-exchange-2013-help.md)

[Ajouter un rôle à un utilisateur ou un groupe de sécurité universel](add-a-role-to-a-user-or-usg-exchange-2013-help.md)

[Supprimer un rôle d’un utilisateur ou un groupe universel de sécurité](remove-a-role-from-a-user-or-usg-exchange-2013-help.md)

