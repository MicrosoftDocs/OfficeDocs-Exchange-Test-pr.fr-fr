---
title: 'Modifier une attribution de rôle: Exchange 2013 Help'
TOCTitle: Modifier une attribution de rôle
ms:assetid: 0fa77efc-e393-461f-b3c0-232cc56cee85
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dd335096(v=EXCHG.150)
ms:contentKeyID: 50477510
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Modifier une attribution de rôle

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2012-10-03_

Les attributions du rôle de gestion affectent un rôle de gestion à l’utilisateur. La modification de l’attribution de rôle vous permet de contrôler les objets que peuvent modifier les utilisateurs auxquels un rôle a été attribué. Les étendues de rôle de gestion appliquées aux attributions de rôle remplacent l’étendue d’écriture implicite du rôle. Cependant, l’étendue de lecture implicite du rôle s’applique toujours. Les étendues que vous appliquez ne peuvent pas renvoyer d’objets en dehors de l’étendue de lecture implicite du rôle.

Pour plus d’informations sur les étendues de rôles de gestion et les attributions dans Microsoft Exchange Server 2013, voir les rubriques suivantes :

  - [Présentation des attributions de rôles de gestion](understanding-management-role-assignments-exchange-2013-help.md)

  - [Présentation des portées du rôle de gestion](understanding-management-role-scopes-exchange-2013-help.md)

Souhaitez-vous rechercher les autres tâches de gestion relatives aux attributions de rôles ? Voir [Autorisations avancées](advanced-permissions-exchange-2013-help.md).

## Ce qu’il faut savoir avant de commencer ?

  - Durée d’exécution estimée de chaque procédure : 5 minutes

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Attribution des rôles » dans la rubrique [Autorisations pour la gestion des rôles](role-management-permissions-exchange-2013-help.md).

  - Vous devez utiliser l’environnement de ligne de commande Exchange Management Shell pour effectuer ces procédures.

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.


## Que souhaitez-vous faire ?

## Utiliser l’environnement de ligne de commande Exchange Management Shell pour activer ou désactiver une attribution de rôles

Les attributions de rôles sont activées par défaut, impliquant que le rôle associé est appliqué à l’utilisateur du rôle auquel le rôle est attribué. Si une attribution de rôle est désactivée, le rôle associé n’est pas appliqué à l’utilisateur du rôle.

Pour activer une attribution de rôle, utilisez la syntaxe suivante.

```powershell
Set-ManagementRoleAssignment <role assignment> -Enabled $true
```

Pour désactiver une attribution de rôle, utilisez la syntaxe suivante.

```powershell
Set-ManagementRoleAssignment <role assignment> -Enabled $false
```

Cet exemple montre comment désactiver l’attribution de rôle Attribution Support technique.

```powershell
Set-ManagementRoleAssignment "Help Desk Assignment" -Enabled $false
```

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Set-ManagementRoleAssignment](https://technet.microsoft.com/fr-fr/library/dd335173\(v=exchg.150\)).

## Utiliser l’environnement de ligne de commande Exchange Management Shell pour modifier le rôle de gestion ou l’utilisateur d’un rôle sur une attribution de rôle

Il n’est pas possible de modifier le rôle de gestion ou l’utilisateur du rôle spécifié sur une attribution de rôle. Si vous souhaitez associer une attribution de rôle à un autre rôle ou utilisateur de rôle, vous devez créer une nouvelle attribution de rôle puis supprimer l’ancienne attribution de rôle. Pour plus d’informations sur l’ajout et la suppression d’attributions de rôles, voir les rubriques suivantes :

  - [Ajouter un rôle à un utilisateur ou un groupe de sécurité universel](add-a-role-to-a-user-or-usg-exchange-2013-help.md)

  - [Supprimer un rôle d’un utilisateur ou un groupe universel de sécurité](remove-a-role-from-a-user-or-usg-exchange-2013-help.md)

Si vous avez créé des attributions directement sur un utilisateur ou un groupe universel de sécurité, nous vous recommandons d’envisager l’utilisation des groupes de rôles de gestion et des stratégies d’attribution des rôles de gestion. Les groupes de rôles et les stratégies d’attribution vous permettent de simplifier votre modèle d’autorisations et de réduire le nombre d’attributions de rôles que vous devez gérer. Pour plus d’informations, voir [Présentation du contrôle d'accès basé sur un rôle](understanding-role-based-access-control-exchange-2013-help.md).

## Utiliser l’environnement de ligne de commande Exchange Management Shell pour modifier l’étendue relative prédéfinie sur une attribution de rôle

Vous pouvez modifier ou ajouter une étendue relative prédéfinie sur une attribution de rôle. Si vous ajoutez ou modifiez une étendue prédéfinie, toutes les étendues de destinataire précédemment spécifiées sont supprimées de l’attribution des rôles. Pour obtenir une liste des étendues prédéfinies et leur description, voir [Présentation des portées du rôle de gestion](understanding-management-role-scopes-exchange-2013-help.md).

Pour modifier ou ajouter une étendue prédéfinie sur une attribution de rôle, utilisez la syntaxe suivante.

    Set-ManagementRoleAssignment <assignment name> -RecipientRelativeWriteScope < MyDistributionGroups | Organization | Self >

Cet exemple montre comment modifier l’étendue prédéfinie sur l’attribution du rôle de gestion Attribution de John sur MesGroupesDistribution.

```powershell
Set-ManagementRoleAssignment "John's Assignment" - RecipientRelativeWriteScope MyDistributionGroups
```

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Set-ManagementRoleAssignment](https://technet.microsoft.com/fr-fr/library/dd335173\(v=exchg.150\)).

## Utiliser l’environnement de ligne de commande Exchange Management Shell pour modifier l’étendue de filtrage des destinataires sur une attribution de rôle

Vous pouvez soit spécifier une nouvelle étendue de filtre de destinataire soit modifier l’étendue de filtre de destinataire qui est déjà appliquée à l’attribution de rôle. Si vous ajoutez une étendue de filtre de destinataire, toutes les étendues de destinataire précédemment définies sont supprimées de l’attribution de rôle.

Pour spécifier une nouvelle étendue de filtre de destinataire ou en remplacer une existante, utilisez la syntaxe suivante.

    Set-ManagementRoleAssignment <assignment name> -CustomRecipientWriteScope <role scope name>

Cet exemple ajoute ou modifie l’étendue de filtre de destinataire sur les destinataires de Redmond.

    Set-ManagementRoleAssignment "Redmond Recipient Administrators Assignment" -CustomRecipientWriteScope "Redmond Recipients"

Si vous souhaitez conserver la même étendue de filtre de destinataire qui est appliquée sur l’attribution de rôle mais que vous souhaitez modifier le filtre de destinataire servant à faire correspondre les objets destinataires, vous devez modifier le filtre destinataire sur l’étendue elle-même. Pour plus d’informations sur la manière de modifier les étendues, voir [Modifier l’étendue d’un rôle](change-a-role-scope-exchange-2013-help.md).

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Set-ManagementRoleAssignment](https://technet.microsoft.com/fr-fr/library/dd335173\(v=exchg.150\)).

## Utiliser l’environnement de ligne de commande Exchange Management Shell pour modifier l’étendue de configuration de liste ou de filtre de serveur sur une attribution de rôle

Vous pouvez soit spécifier une nouvelle étendue de configuration de filtre ou de liste de serveur soit modifier l’étendue qui est déjà appliquée à l’attribution de rôle. Si vous ajoutez ou modifiez une étendue de configuration, toutes les étendues de configuration précédemment spécifiées sont supprimées de l’attribution de rôle.

Pour spécifier une nouvelle étendue de configuration ou en remplacer une existante, utilisez la syntaxe suivante.

```powershell
Set-ManagementRoleAssignment <assignment name> -CustomConfigWriteScope <role scope name>
```

Cet exemple ajoute ou modifie l’étendue de configuration aux serveurs de Redmond.

    Set-ManagementRoleAssignment "Redmond Administrators Assignment" -CustomConfigWriteScope "Redmond Servers"

Si vous souhaitez conserver la même étendue de configuration qui est appliquée à l’attribution de rôle mais que vous souhaitez modifier le filtre de serveur ou la liste des serveurs sur l’étendue, vous devez modifier l’étendue de configuration elle-même. Pour plus d’informations sur la manière de modifier les étendues, voir [Modifier l’étendue d’un rôle](change-a-role-scope-exchange-2013-help.md).

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Set-ManagementRoleAssignment](https://technet.microsoft.com/fr-fr/library/dd335173\(v=exchg.150\)).

## Utiliser l’environnement de ligne de commande Exchange Management Shell pour modifier l’étendue de configuration de liste ou de filtre de base de données sur une attribution de rôle

Vous pouvez soit spécifier une nouvelle étendue de configuration de filtre ou de liste de base de données soit modifier l’étendue qui est déjà appliquée à l’attribution de rôle. Si vous ajoutez ou modifiez une étendue de configuration, toutes les étendues de configuration précédemment spécifiées sont supprimées de l’attribution de rôle.

Pour spécifier une nouvelle étendue de configuration ou en remplacer une existante, utilisez la syntaxe suivante.

```powershell
Set-ManagementRoleAssignment <assignment name> -CustomConfigWriteScope <role scope name>
```

Cet exemple ajoute ou modifie l’étendue de configuration aux bases de données de Redmond.

```powershell
Set-ManagementRoleAssignment "Redmond Database Admins" -CustomConfigWriteScope "Redmond Databases"
```

Si vous souhaitez conserver la même étendue de configuration qui est appliquée à l’attribution de rôle mais que vous souhaitez modifier le filtre de base de données ou la liste des bases de données sur l’étendue, vous devez modifier l’étendue de configuration elle-même. Pour plus d’informations sur la manière de modifier les étendues, voir [Modifier l’étendue d’un rôle](change-a-role-scope-exchange-2013-help.md).

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Set-ManagementRoleAssignment](https://technet.microsoft.com/fr-fr/library/dd335173\(v=exchg.150\)).

## Utiliser l’environnement de ligne de commande Exchange Management Shell pour modifier l’unité d’organisation sur une attribution de rôle

Vous pouvez soit ajouter une nouvelle unité d’organisation soit modifier une unité d’organisation qui est déjà appliquée à l’attribution de rôle. Si vous spécifiez une nouvelle unité d’organisation, toutes les étendues de destinataire précédemment spécifiées sont supprimées de l’attribution de rôle.

Pour modifier ou ajouter une nouvelle unité d’organisation sur une attribution de rôle, utilisez la syntaxe suivante.

```powershell
Set-ManagementRoleAssignment <assignment name> -RecipientOrganizationalUnitScope <OU>
```

Cet exemple ajoute l’unité d’organisation Engineering\\Users au domaine contoso.com sur l’attribution de rôle Support technique Engineering.

    Set-ManagementRoleAssignment "Engineering Help Desk" -RecipientOrganizationalUnitScope contoso.com/Engineering/Users

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Set-ManagementRoleAssignment](https://technet.microsoft.com/fr-fr/library/dd335173\(v=exchg.150\)).

## Utiliser l’environnement de ligne de commande Exchange Management Shell pour modifier une étendue de destinataire ou de configuration exclusive

Pour modifier des étendues de configuration ou de destinataire exclusives, vous pouvez utiliser les procédures fournies dans les sections précédentes de cette rubrique « Utiliser l’environnement de ligne de commande Exchange Management Shell pour modifier l’étendue de filtrage des destinataires sur une attribution de rôle », « Utiliser l’environnement de ligne de commande Exchange Management Shell pour modifier l’étendue de configuration de liste ou de filtre de serveur sur une attribution de rôle » et « Utiliser l’environnement de ligne de commande Exchange Management Shell pour modifier l’étendue de configuration de liste ou de filtre de base de données sur une attribution de rôle ». La seule différence, c’est que lorsque vous modifiez une étendue exclusive, vous devez spécifier les paramètres exclusifs suivants selon que vous modifiez une étendue de destinataire exclusive ou une étendue de configuration exclusive :

  - **Étendues exclusives sur le destinataire**   Utilisez le paramètre *ExclusiveRecipientWriteScope* au lieu du paramètre *CustomRecipientWriteScope*.

  - **Étendues de configuration exclusives serveur et base de données**   Utilisez le paramètre *ExclusiveConfigWriteScope* au lieu du paramètre *CustomConfigWriteScope*.

Tout comme avec les étendues de configuration et de destinataire normales, si vous ajoutez ou modifiez une étendue exclusive, toutes les étendues de destinataire ou de configuration précédemment définies sont remplacées.

Cet exemple montre comment modifier une étendue d’écriture de destinataire exclusif.

    Set-ManagementRoleAssignment "Exclusive Executive Users" -ExclusiveRecipientWriteScope "Exclusive Executives"

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Set-ManagementRoleAssignment](https://technet.microsoft.com/fr-fr/library/dd335173\(v=exchg.150\)).

