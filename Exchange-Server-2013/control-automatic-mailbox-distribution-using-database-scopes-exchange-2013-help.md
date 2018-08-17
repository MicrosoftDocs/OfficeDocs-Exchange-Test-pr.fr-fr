---
title: 'Contrôler la distribution automatique de BAL à l’aide d’étendues de BDD'
TOCTitle: Contrôler la distribution automatique de boîtes aux lettres à l’aide d’étendues de base de données
ms:assetid: 8eaff177-2251-4c8b-8570-c91a77d0a6fc
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Ff628332(v=EXCHG.150)
ms:contentKeyID: 50478676
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Contrôler la distribution automatique de boîtes aux lettres à l’aide d’étendues de base de données

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2015-04-07_

La distribution automatique des boîtes aux lettres est une fonctionnalité de Microsoft Exchange Server 2013 qui sélectionne de manière aléatoire une base de données de boîtes aux lettres afin de stocker une boîte aux lettres nouvelle ou déplacée lorsqu’aucune base de données n’est explicitement spécifiée. Cette fonctionnalité peut s’avérer utile lorsque vous souhaitez autoriser de jeunes administrateurs ou membres du service d’assistance à créer des boîtes aux lettres sans connaître les bases de données dans lesquelles les boîtes aux lettres doivent être créées.

Vous pouvez utiliser des étendues de gestion de bases de données pour déterminer les bases de données de boîtes aux lettres pouvant être sélectionnées par la distribution automatique de boîtes aux lettres. Lorsque vous appliquez des étendues de base de données à un administrateur, seules les bases de données correspondant à l’étendue de base de données définie sont accessibles à l’administrateur. La distribution automatique des boîtes aux lettres utilisant le contexte de l’utilisateur actuel, elle est également limitée par les étendues de base de données appliquées à l’administrateur.

Pour plus d’informations sur la distribution automatique de boîtes aux lettres, les étendues de base de données et les attributions de rôles, consultez les rubriques suivantes :

  - [Distribution automatique de boîtes aux lettres](automatic-mailbox-distribution-exchange-2013-help.md)

  - [Présentation des portées du rôle de gestion](understanding-management-role-scopes-exchange-2013-help.md)

  - [Présentation des attributions de rôles de gestion](understanding-management-role-assignments-exchange-2013-help.md)

Souhaitez-vous rechercher d’autres tâches de gestion relatives aux étendues ? Consultez la rubrique [Autorisations avancées](advanced-permissions-exchange-2013-help.md).

## Ce qu’il faut savoir avant de commencer ?

  - Durée estimée de la procédure : 10 minutes

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Étendues de gestion » dans la rubrique [Autorisations pour la gestion des rôles](role-management-permissions-exchange-2013-help.md).

  - Vous devez utiliser l’environnement de ligne de commande Exchange Management Shell pour effectuer ces procédures.

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.


## Comment procéder ?

## Étape 1 : Créer une étendue de base de données

Dans cette étape, déterminez les bases de données à inclure dans l’étendue de base de données. Indiquez également si vous souhaitez spécifier une liste statique de bases de données ou bien créer un filtre de base de données contenant uniquement les bases de données qui correspondent aux critères spécifiés.

> [!NOTE]
> Les attributions de rôle associées aux étendues de base de données s’appliquent uniquement aux utilisateurs qui se connectent à des serveurs dotés de Microsoft Exchange Server 2010 Service Pack 1 (SP1) ou version ultérieure ou d’Exchange 2013. Si un utilisateur auquel est appliquée une attribution de rôle associée à une étendue de base de données se connecte à une version de serveur antérieure à Exchange 2010 SP1, l’attribution de rôle n’est pas appliquée à cet utilisateur et celui-ci ne bénéficiera pas des autorisations octroyées dans le cadre de cette attribution.


## Utiliser une étendue de liste des bases de données

Utilisez une liste de bases de données pour définir une liste statique de bases de données de boîtes aux lettres à inclure dans cette étendue. Pour créer une étendue de liste de bases de données, utilisez la syntaxe suivante.

    New-ManagementScope -Name <scope name> -DatabaseList <database 1>, <database 2...>

Dans cet exemple, on crée une étendue qui s’applique uniquement aux bases de données Base de données 1, Base de données 2 et Base de données 3.

    New-ManagementScope -Name "Accounting databases" -DatabaseList "Database 1", "Database 2", "Database 3"

Pour de plus amples informations sur la syntaxe et les paramètres, consultez la rubrique [New-ManagementScope](https://technet.microsoft.com/fr-fr/library/dd335137\(v=exchg.150\)).

## Utiliser une étendue de filtre de base de données

Utilisez un filtre de base de données pour créer une étendue de base de données dynamique qui inclut uniquement les bases de données correspondant aux critères spécifiés. Ce filtre peut être utile si vous ne souhaitez pas gérer l’étendue de base de données après l’avoir créée et après avoir défini pour votre organisation des valeurs standard capables d’identifier des ensembles spécifiques de bases de données de boîtes aux lettres.

Pour obtenir une liste des propriétés de base de données pouvant être filtrées, consultez la rubrique [Présentation des filtres d’attribution du rôle de gestion](understanding-management-role-scope-filters-exchange-2013-help.md).

Pour créer une étendue de filtre de base de données, utilisez la syntaxe suivante.

    New-ManagementScope -Name <scope name> -DatabaseRestrictionFilter <filter query>

Dans cet exemple, on crée une étendue qui inclut toutes les bases de données contenant la chaîne « ACCT » dans la propriété **Name** de la base de données.

    New-ManagementScope -Name "Accounting Databases" -DatabaseRestrictionFilter { Name -Like '*ACCT*' }

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [New-ManagementScope](https://technet.microsoft.com/fr-fr/library/dd335137\(v=exchg.150\)).

## Étape 2 : Ajouter l’étendue de base de données à une attribution de rôle de gestion

Après avoir créé l’étendue, vous devez l’ajouter à une attribution de rôle de gestion nouvelle ou existante. Il est conseillé d’utiliser des groupes de rôles de gestion pour contrôler les autorisations administratives. Les exemples illustrés dans cette étape utilisent donc un groupe de rôles appelé Administrateurs comptabilité. Pour plus d’informations sur la création d’un groupe de rôles, consultez la rubrique [Gérer des groupes de rôles](manage-role-groups-exchange-2013-help.md).

Après avoir attribué le rôle à un groupe de rôles dans l’étendue de base de données, les membres du groupe ne pourront créer et déplacer des boîtes aux lettres que dans les bases de données comprises dans l’étendue.

Pour obtenir une liste des rôles intégrés pouvant être attribués à des groupes de rôles, consultez la rubrique [Rôles de gestion intégrés](built-in-management-roles-exchange-2013-help.md).

## Ajouter une nouvelle attribution de rôle

Utilisez la procédure ci-dessous si vous venez de créer un groupe de rôles auquel vous souhaitez ajouter des rôles.

Pour créer une attribution de rôle entre le rôle de gestion à affecter et le nouveau groupe de rôles à l’aide de la nouvelle étendue de base de données, utilisez la syntaxe suivante.

    New-ManagementRoleAssignment -SecurityGroup <role group name> -Role <role name> -CustomConfigWriteScope <database scope name>

Dans cet exemple, on crée une attribution de rôle entre les rôles Destinataires de messagerie et Création de destinataires de messagerie et le groupe de rôles Administrateurs comptabilité, à l’aide de l’étendue de base de données Bases de données de comptabilité.

    New-ManagementRoleAssignment -SecurityGroup "Accounting Administrators" -Role "Mail Recipients" -CustomConfigWriteScope "Accounting Databases"
    New-ManagementRoleAssignment -SecurityGroup "Accounting Administrators" -Role "Mail Recipient Creation" -CustomConfigWriteScope "Accounting Databases"

Pour de plus amples informations sur la syntaxe et les paramètres, consultez la rubrique [New-ManagementRoleAssignment](https://technet.microsoft.com/fr-fr/library/dd335193\(v=exchg.150\)).

## Modifier une attribution de rôle existante

Utilisez la procédure ci-dessous si des rôles sont déjà attribués entre un groupe de rôles existant et ceux auxquels vous souhaitez appliquer la nouvelle étendue de base de données.

Cette procédure utilise le traitement en pipeline. Pour plus d’informations, consultez la rubrique [Traitement en pipeline](https://technet.microsoft.com/fr-fr/library/aa998260\(v=exchg.150\)).

Pour modifier une attribution de rôle entre le rôle de gestion auquel vous souhaitez appliquer l’étendue de base de données et un groupe de rôles existant, utilisez la syntaxe suivante.

    Get-ManagementRoleAssignment -RoleAssignee <role group name> -Role <role name> | Set-ManagementRoleAssignment -CustomConfigWriteScope <database scope name>

Dans cet exemple, on ajoute l’étendue de base de données Bases de données comptabilité aux rôles Destinataires de messagerie et Création de destinataires de messagerie affectés au groupe de rôles Administrateurs comptabilité.

    Get-ManagementRoleAssignment -RoleAssignee "Accounting Administrators" -Role "Mail Recipients" | Set-ManagementRoleAssignment -CustomConfigWriteScope "Accounting Databases"
    Get-ManagementRoleAssignment -RoleAssignee "Accounting Administrators" -Role "Mail Recipient Creation" | Set-ManagementRoleAssignment -CustomConfigWriteScope "Accounting Databases"

Pour plus d’informations sur la syntaxe et les paramètres, consultez la rubrique [Get-ManagementRoleAssignment](https://technet.microsoft.com/fr-fr/library/dd351024\(v=exchg.150\)) ou [Set-ManagementRoleAssignment](https://technet.microsoft.com/fr-fr/library/dd335173\(v=exchg.150\)).

## Étape 3 : Ajouter des membres à un groupe de rôles (le cas échéant)

Si vous souhaitez ajouter des membres à un groupe de rôles, consultez la rubrique [Gérer les membres de groupes de rôles](manage-role-group-members-exchange-2013-help.md).

> [!NOTE]
> Si vous ajoutez des membres à ce groupe de rôles pour limiter les bases de données dans lesquelles il est possible de créer des utilisateurs ou de déplacer des boîtes aux lettres, assurez-vous qu’ils n’appartiennent pas à d’autres groupes de rôles pouvant accorder des autorisations supplémentaires.


## Étape 4 : Supprimer des membres d’un groupe de rôles (le cas échéant)

Si vous avez ajouté des membres à un nouveau groupe de rôles qui limite les bases de données dans lesquelles ils peuvent créer ou déplacer des boîtes aux lettres, et s’ils appartiennent à un autre groupe de rôles disposant d’autorisations supplémentaires, supprimez-les de l’ancien groupe. Pour plus d’informations, consultez la rubrique [Gérer les membres de groupes de rôles](manage-role-group-members-exchange-2013-help.md).

