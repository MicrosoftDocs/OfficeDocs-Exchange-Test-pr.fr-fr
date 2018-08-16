---
title: 'Ajouter un rôle à un utlsr ou un grp de sécurité universel: Exchange 2013 Help'
TOCTitle: Ajouter un rôle à un utilisateur ou un groupe de sécurité universel
ms:assetid: ae5608de-a141-4714-8876-bce7d2a22cb5
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dd351056(v=EXCHG.150)
ms:contentKeyID: 50478992
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Ajouter un rôle à un utilisateur ou un groupe de sécurité universel

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2012-10-03_

L'attribution de rôles de gestion permet d'attribuer un rôle de gestion à un utilisateur ou à un groupe de sécurité universel. En attribuant un rôle à un utilisateur ou à un groupe de sécurité universel, vous autorisez ces utilisateurs à effectuer des tâches qui dépendent de cmdlets ou de scripts et permettez à leurs paramètres d'être définis sur le rôle de gestion.

Pour attribuer des rôles à un groupe de rôles de gestion ou à une stratégie d'attribution de rôles de gestion, voir les rubriques suivantes :

  - [Gérer des groupes de rôles](manage-role-groups-exchange-2013-help.md)

  - [Gérer les stratégies d’attribution des rôles](manage-role-assignment-policies-exchange-2013-help.md)

Pour ajouter des membres à un groupe de rôles ou affecter une stratégie d'attribution de rôle à un utilisateur final, voir les rubriques suivantes :

  - [Gérer les membres de groupes de rôles](manage-role-group-members-exchange-2013-help.md)

  - [Modifier la stratégie d’attribution sur une boîte aux lettres](change-the-assignment-policy-on-a-mailbox-exchange-2013-help.md)

Pour plus d'informations, voir [Présentation du contrôle d'accès basé sur un rôle](understanding-role-based-access-control-exchange-2013-help.md).

Souhaitez-vous rechercher les autres tâches de gestion relatives aux rôles ? Consultez la rubrique [Autorisations avancées](advanced-permissions-exchange-2013-help.md).

## Ce qu’il faut savoir avant de commencer ?

  - Durée d’exécution estimée de chaque procédure : 5 minutes

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Attribution des rôles » dans la rubrique [Autorisations pour la gestion des rôles](role-management-permissions-exchange-2013-help.md).

  - Vous devez utiliser l’environnement de ligne de commande Exchange Management Shell pour effectuer ces procédures.

  - Bien que vous puissiez attribuer des rôles directement aux utilisateurs et aux groupes de sécurité universels, la méthode recommandée pour accorder des autorisations aux administrateurs et aux utilisateurs finaux est d’utiliser les groupes de rôles de gestion et les stratégies d’attribution de rôle de gestion. Lorsque vous utilisez des groupes de rôles et des stratégies d’attribution, vous simplifiez votre modèle d’autorisations.

  - Les attributions de rôle sont cumulables. Cela signifie que tous les rôles sont évalués ensemble. Si deux rôles sont attribués à un utilisateur et si un rôle contient une cmdlet et l’autre non, la cmdlet de ce premier rôle sera disponible.
    
    Par défaut, les attributions de rôle n'offrent pas la possibilité d'attribuer des rôles aux autres utilisateurs. Pour permettre à un utilisateur d'attribuer des rôles à d'autres utilisateurs ou à des groupes de sécurité universels, voir [Déléguer les attributions de rôles](delegate-role-assignments-exchange-2013-help.md).

  - Si vous créez une attribution avec une étendue, celle-ci écrase l’étendue d’écriture implicite du rôle. Cependant, l’étendue de lecture implicite du rôle s’applique toujours. La nouvelle étendue ne peut pas renvoyer des objets en dehors de l’étendue de lecture implicite du rôle. Pour plus d'informations, voir [Présentation des portées du rôle de gestion](understanding-management-role-scopes-exchange-2013-help.md).

  - Toutes les procédures décrites dans cette rubrique utilisent le paramètre *SecurityGroup* pour affecter des rôles à un groupe de sécurité universel. Si vous souhaitez attribuer le rôle à un utilisateur spécifique, utilisez le paramètre *User* au lieu du paramètre *SecurityGroup*. Tous les autres éléments de la syntaxe sont identiques pour chaque commande.

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.


## Que souhaitez-vous faire ?

## Créer une attribution de rôle sans étendue

Vous pouvez créer une attribution de rôle sans étendue. Lorsque vous effectuez cette opération, les étendues d’écriture implicite et de lecture implicite du rôle s’appliquent.

Utilisez la syntaxe suivante pour attribuer un rôle à un groupe de sécurité universel sans étendue.

    New-ManagementRoleAssignment -Name <assignment name> -SecurityGroup <USG> -Role <role name>

Cet exemple attribue le rôle « Exchange Servers » (serveurs Exchange) au groupe de sécurité universel SeattleAdmins.

    New-ManagementRoleAssignment -Name "Exchange Servers_SeattleAdmins" -SecurityGroup SeattleAdmins -Role "Exchange Servers"

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, consultez la rubrique [New-ManagementRoleAssignment](https://technet.microsoft.com/fr-fr/library/dd335193\(v=exchg.150\)).

## Créer une attribution de rôle avec une étendue relative prédéfinie

Si une étendue relative prédéfinie correspond à vos besoins professionnels, vous pouvez appliquer cette étendue à l’attribution de rôle au lieu de créer une étendue personnalisée. Pour obtenir une liste des étendues prédéfinies et leur description, consultez la rubrique [Présentation des portées du rôle de gestion](understanding-management-role-scopes-exchange-2013-help.md).

Utilisez la syntaxe suivante pour attribuer un rôle à un groupe de sécurité universel avec une étendue prédéfinie.

    New-ManagementRoleAssignment -Name <assignment name> -SecurityGroup < USG> -Role <role name> -RecipientRelativeWriteScope < MyDistributionGroups | Organization | Self >

Cet exemple attribue le rôle « Exchange Servers » au groupe de sécurité universel SeattleAdmins et applique l’étendue prédéfinie Organization.

    New-ManagementRoleAssignment -Name "Exchange Servers_SeattleAdmins" -SecurityGroup SeattleAdmins -Role "Exchange Servers" -RecipientRelativeWriteScope Organization

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [New-ManagementRoleAssignment](https://technet.microsoft.com/fr-fr/library/dd335193\(v=exchg.150\)).

## Créer une attribution de rôle avec une étendue basée sur le filtre destinataire

Si vous avez créé une étendue de destinataire basée sur le filtre et que vous voulez l’utiliser avec une attribution de rôle, vous devez inclure l’étendue dans la commande utilisée pour attribuer le rôle à un groupe de sécurité universel à l’aide du paramètre *CustomRecipientWriteScope*. Si vous utilisez le paramètre *CustomRecipientWriteScope*, vous ne pouvez pas utiliser le paramètre *RecipientOrganizationalUnitScope*.

Avant de pouvoir ajouter une étendue pour une attribution de rôle, vous devez en créer une. Pour plus d'informations, voir [Créer une étendue normale ou exclusive](create-a-regular-or-exclusive-scope-exchange-2013-help.md).

Utilisez la syntaxe suivante pour attribuer un rôle à un groupe de sécurité universel avec une étendue de destinataire basée sur le filtre.

    New-ManagementRoleAssignment -Name <assignment name> -SecurityGroup < USG> -Role <role name> -CustomRecipientWriteScope <role scope name>

Cet exemple attribue le rôle Mail Recipients (Destinataires) au groupe de sécurité universel Seattle Recipient Admins (Administrateurs destinataires de Seattle) et applique l’étendue Seattle Recipients (Destinataires de Seattle).

    New-ManagementRoleAssignment -Name "Mail Recipients_Seattle Recipient Admins" -SecurityGroup "Seattle Recipient Admins" -Role "Mail Recipients" -CustomRecipientWriteScope "Seattle Recipients"

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [New-ManagementRoleAssignment](https://technet.microsoft.com/fr-fr/library/dd335193\(v=exchg.150\)).

## Créer une attribution de rôle avec un filtre de serveur ou de base de données ou une étendue de configuration basée sur une liste

Si vous avez créé un filtre de serveur ou de base de données ou une étendue de configuration basée sur une liste et que vous voulez l’utiliser avec une attribution de rôle, vous devez inclure l’étendue dans la commande utilisée pour attribuer le rôle à un groupe de sécurité universel à l’aide du paramètre *CustomConfigWriteScope*.

Avant de pouvoir ajouter une étendue pour une attribution de rôle, vous devez en créer une. Pour plus d'informations, voir [Créer une étendue normale ou exclusive](create-a-regular-or-exclusive-scope-exchange-2013-help.md).

Utilisez la syntaxe suivante pour attribuer un rôle à un groupe de sécurité universel avec une étendue de configuration.

    New-ManagementRoleAssignment -Name <assignment name> -SecurityGroup <USG> -Role <role name> -CustomConfigWriteScope <role scope name>

Cet exemple attribue le rôle « Exchange Servers » au groupe de sécurité universel MailboxAdmins et applique l’étendue Mailbox Servers.

    New-ManagementRoleAssignment -Name "Exchange Servers_MailboxAdmins" -SecurityGroup MailboxAdmins -Role "Exchange Servers" -CustomConfigWriteScope "Mailbox Servers"

L'exemple précédent montre comment ajouter une attribution de rôle avec une étendue de configuration de serveur. La syntaxe utilisée pour ajouter une étendue de configuration de base de données est la même. Vous devez préciser le nom d’une étendue de base de données au lieu d’une étendue de serveur.

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [New-ManagementRoleAssignment](https://technet.microsoft.com/fr-fr/library/dd335193\(v=exchg.150\)).

## Créer une attribution de rôle avec une étendue d'unité d'organisation

Si vous souhaitez affecter une étendue d'écriture de rôle à une unité d'organisation, vous pouvez indiquer l'unité d'organisation directement dans le paramètre *RecipientOrganizationalUnitScope*. Si vous utilisez le paramètre *RecipientOrganizationalUnitScope*, vous ne pouvez pas utiliser le paramètre *CustomRecipientWriteScope*.

Utilisez la syntaxe suivante pour attribuer un rôle à un groupe de sécurité universel et limiter l’éténdue d’écriture d’un rôle à une unité d’organisation spécifique.

    New-ManagementRoleAssignment -Name <assignment name> -SecurityGroup <USG> -Role <role name> -RecipientOrganizationalUnitScope <OU>

Cet exemple attribue le rôle Mail Recipients au groupe de sécurité universel SalesRecipientAdmins et définit l’étendue de l’attribution sur l’unité d’organisation « sales/users » dans le domaine contoso.com.

    New-ManagementRoleAssignment -Name "Mail Recipients_SalesRecipientAdmins" -SecurityGroup SalesRecipientAdmins -Role "Mail Recipients" -RecipientOrganizationalUnitScope contoso.com/sales/users

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [New-ManagementRoleAssignment](https://technet.microsoft.com/fr-fr/library/dd335193\(v=exchg.150\)).

## Créer une attribution de rôle avec une étendue de destinataire ou de configuration exclusive

Pour créer une attribution de rôle exclusive avec une étendue de destinataire ou de configuration exclusive, vous pouvez utiliser les procédures décrites dans les sections Créer une attribution de rôle avec une étendue basée sur le filtre destinataire et Créer une attribution de rôle avec un filtre de serveur ou de base de données ou une étendue de configuration basée sur une liste. Toutefois, lorsque vous créez une attribution de rôle avec une étendue exclusive, vous devez spécifier les paramètres exclusifs suivants selon que vous utilisez une étendue de destinataire exclusive ou un étendue de configuration exclusive :

  - **Étendues exclusives sur le destinataire**   Utilisez le paramètre *ExclusiveRecipientWriteScope* au lieu du paramètre *CustomRecipientWriteScope*.

  - **Étendues de configuration exclusives**   Utilisez le paramètre *ExclusiveConfigWriteScope* au lieu du paramètre *CustomConfigWriteScope*.

Lorsque vous exécutez cette procédure, les personnes auxquelles le rôle est attribué peuvent effectuer des actions sur les objets inclus dans l’étendue exclusive. Pour plus d'informations sur les étendues exclusives, voir [Présentation des étendues exclusives](understanding-exclusive-scopes-exchange-2013-help.md).

Vous ne pouvez pas créer d'attribution de rôle avec des étendues à la fois exclusives et normales.

Cet exemple attribue le rôle Mail Recipients au groupe de sécurité universel Protected User Admins et applique l’étendue exclusive Protected Users.

    New-ManagementRoleAssignment -Name "Mail Recipients_Protected User Admins" -SecurityGroup "Protected User Admins" -Role "Mail Recipients" -ExclusiveRecipientWriteScope "Protected Users"

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [New-ManagementRoleAssignment](https://technet.microsoft.com/fr-fr/library/dd335193\(v=exchg.150\)).

