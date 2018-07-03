---
title: 'Gérer des groupes de rôles: Exchange 2013 Help'
TOCTitle: Gérer des groupes de rôles
ms:assetid: ab9b7a3b-bf67-4ba1-bde5-8e6ac174b82c
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ657480(v=EXCHG.150)
ms:contentKeyID: 50478857
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Gérer des groupes de rôles

 

_**Sapplique à :** Exchange Online, Exchange Server 2013_

_**Dernière rubrique modifiée :** 2012-10-08_

Cette rubrique vous explique comment ajouter, supprimer, copier et afficher des groupes de rôles de gestion dans Microsoft Exchange Server 2013. Elle vous indique également comment ajouter, supprimer et répertorier des rôles de gestion dans des groupes de rôles, et comment modifier des délégués et des étendues de gestion dans des groupes de rôles. Pour plus d’informations sur les groupes de rôles dans Exchange 2013, consultez la rubrique [Présentation des groupes de rôles de gestion](understanding-management-role-groups-exchange-2013-help.md).

Autres tâches de gestion relatives aux groupes de rôles, voir [Autorisations](permissions-exchange-2013-help.md).

## Ce qu’il faut savoir avant de commencer ?

  - Durée d’exécution estimée de chaque procédure : 5 à 10 minutes

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Groupes de rôles » dans la rubrique [Autorisations pour la gestion des rôles](role-management-permissions-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.


## Que souhaitez-vous faire ?

## Créer un groupe de rôles

Si vous souhaitez personnaliser les autorisations que vous pouvez attribuer à un groupe d’utilisateurs, créez un groupe de rôles de gestion personnalisé.

## Utiliser le CAE pour créer un groupe de rôles

1.  Dans le Centre d'administration Exchange (CAE), rendez-vous dans **Autorisations** \> **Rôles d'administrateur**, puis cliquez sur **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter").

2.  Dans la fenêtre **Nouveau groupe de rôles**, fournissez un nom pour le nouveau groupe de rôles.

3.  Vous pouvez sélectionner dès à présent les rôles à attribuer au groupe de rôles et les membres à ajouter au groupe de rôles, ou les sélectionner ultérieurement.

4.  Sélectionnez l'étendue d'écriture à appliquer au nouveau groupe de rôles.

5.  Cliquez sur **Enregistrer** pour créer le groupe de rôle.

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour créer un groupe de rôles

Pour créer un groupe de rôles, voir la section [Examples](https://technet.microsoft.com/fr-fr/dd638181\(exchg.150\)#examples) dans [New-RoleGroup](https://technet.microsoft.com/fr-fr/library/dd638181\(v=exchg.150\)).

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez bien créé un groupe de rôles, procédez comme suit :

1.  Dans le CAE, accédez à **Autorisations** \> **Rôles admin**.

2.  Vérifiez que le nouveau groupe de rôles apparaît dans la liste des groupes de rôles, puis sélectionnez-le.

3.  Vérifiez que les membres, les rôles attribués et l'étendue que vous avez indiqués dans le nouveau groupe de rôles sont répertoriés dans le volet des informations relatives au groupe de rôles.

## Copier un groupe de rôles

## Utiliser le CAE pour copier un groupe de rôles

Si vous disposez d’un groupe de rôles qui contient les autorisations que vous souhaitez octroyer aux utilisateurs, mais que vous voulez appliquer une autre étendue de gestion, ou supprimer ou ajouter un ou deux rôle(s) de gestion sans devoir ajouter tous les autres rôles manuellement, vous pouvez copier le groupe de rôles existant.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159813.important(EXCHG.150).gif" title="Important" alt="Important" />Important :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Vous ne pouvez pas utiliser le CAE pour copier un groupe de rôles si vous avez utilisé l'environnement de ligne de commande Exchange Management Shell pour configurer plusieurs étendues de rôle de gestion ou des étendues exclusives au niveau du groupe de rôles. Dans ce cas, vous devez utiliser les procédures d’environnement de ligne de commande décrites plus loin dans cette rubrique pour copier le groupe de rôles. Pour plus d’informations sur les étendues de rôle de gestion, consultez la rubrique <a href="understanding-management-role-scopes-exchange-2013-help.md">Présentation des portées du rôle de gestion</a>.</td>
</tr>
</tbody>
</table>


1.  Dans le CAE, accédez à **Autorisations** \> **Rôles admin**.

2.  Sélectionnez le groupe de rôles à copier, puis cliquez sur **Copier**![Icône Copier](images/JJ657480.ed7f7abf-39d8-4f43-a918-ccb3bff87ef5(EXCHG.150).gif "Icône Copier").

3.  Dans la fenêtre **Nouveau groupe de rôles**, fournissez un nom pour le nouveau groupe de rôles.

4.  Passez en revue les rôles qui ont été copiés dans le nouveau groupe de rôles. Ajoutez ou supprimez des rôles le cas échéant.

5.  Examinez l'étendue d'écriture et modifiez-la si nécessaire.

6.  Passez en revue les membres qui ont été copiés dans le nouveau groupe de rôles. Ajoutez ou supprimez des membres le cas échéant.

7.  Cliquez sur **Enregistrer** pour créer le groupe de rôle.

## Utiliser l’environnement de ligne de commande pour copier un groupe de rôles sans aucune portée

1.  Stockez le groupe de rôles que vous souhaitez copier dans une variable à l’aide de la commande suivante.
    
        $RoleGroup = Get-RoleGroup <name of role group to copy>

2.  Créez le groupe de rôles et ajoutez aussi des membres à ce groupe, puis indiquez les noms des utilisateurs pouvant déléguer le nouveau groupe de rôles à d'autres utilisateurs. Pour ce faire, utilisez la syntaxe suivante.
    
        New-RoleGroup <name of new role group> -Roles $RoleGroup.Roles -Members <member1, member2, member3...> -ManagedBy <user1, user2, user3...>

Par exemple, les commandes suivantes permettent de copier le groupe de rôles Organization Management, et de nommer le nouveau groupe de rôles « Limited Organization Management ». Les membres Isabelle, Carter et Lukas sont ajoutés et le groupe peut être délégué par Jenny et Katie.

    $RoleGroup = Get-RoleGroup "Organization Management"
    New-RoleGroup "Limited Organization Management" -Roles $RoleGroup.Roles -Members Isabelle, Carter, Lukas -ManagedBy Jenny, Katie

Une fois que le nouveau groupe de rôles est créé, vous pouvez ajouter ou supprimer des rôles, modifier la portée des affectations sur le rôle, et plus encore.

Pour des informations détaillées sur la syntaxe et les paramètres, consultez les rubriques [Get-RoleGroup](https://technet.microsoft.com/fr-fr/library/dd638115\(v=exchg.150\)) et [New-RoleGroup](https://technet.microsoft.com/fr-fr/library/dd638181\(v=exchg.150\)).

## Utiliser l’environnement de ligne de commande pour copier un groupe de rôles avec portée personnalisée

1.  Stockez le groupe de rôles que vous souhaitez copier dans une variable à l’aide de la commande suivante.
    
        $RoleGroup = Get-RoleGroup <name of role group to copy>

2.  Créez le nouveau groupe de rôles avec une portée personnalisée à l’aide de la syntaxe suivante.
    
        New-RoleGroup <name of new role group> -Roles $RoleGroup.Roles -CustomRecipientWriteScope <recipient scope name> -CustomConfigWriteScope <configuraiton scope name>

Par exemple, les commandes suivantes permettent de copier le groupe de rôles Organization Management et de créer un nouveau groupe appelé Vancouver Organization Management avec la portée du destinataire Vancouver Users et la portée de configuration Vancouver Servers.

    $RoleGroup = Get-RoleGroup "Organization Management"
    New-RoleGroup "Vancouver Organization Management" -Roles $RoleGroup.Roles -CustomRecipientWriteScope "Vancouver Users" -CustomConfigWriteScope "Vancouver Servers"

Vous pouvez également ajouter des membres au groupe de rôles que vous créez à l’aide du paramètre *Members* comme indiqué dans la section Utiliser l’environnement de ligne de commande pour copier un groupe de rôles sans aucune portée plus haut dans cette rubrique. Pour plus d’informations sur les étendues de gestion, voir [Présentation des portées du rôle de gestion](understanding-management-role-scopes-exchange-2013-help.md).

Une fois que le nouveau groupe de rôles est créé, vous pouvez ajouter ou supprimer des rôles et modifier la portée des affectations sur le rôle, entre autres tâches.

Pour des informations détaillées sur la syntaxe et les paramètres, consultez les rubriques [Get-RoleGroup](https://technet.microsoft.com/fr-fr/library/dd638115\(v=exchg.150\)) et [New-RoleGroup](https://technet.microsoft.com/fr-fr/library/dd638181\(v=exchg.150\)).

## Utiliser l’environnement de ligne de commande pour copier un groupe de rôles avec une portée d’unité d’organisation

1.  Stockez le groupe de rôles que vous souhaitez copier dans une variable à l’aide de la commande suivante.
    
        $RoleGroup = Get-RoleGroup <name of role group to copy>

2.  Créez le nouveau groupe de rôles avec une portée personnalisée à l’aide de la syntaxe suivante.
    
        New-RoleGroup <name of new role group> -Roles $RoleGroup.Roles -RecipientOrganizationalUnitScope <OU name>

Par exemple, les commandes suivantes permettent de copier le groupe de rôles Recipient Management et de créer un nouveau groupe appelé Toronto Recipient Management qui permet de gérer uniquement les utilisateurs de l’unité d’organisation Toronto Users.

    $RoleGroup = Get-RoleGroup "Recipient Management"
    New-RoleGroup "Toronto Recipient Management" -Roles $RoleGroup.Roles -RecipientOrganizationalUnitScope "contoso.com/Toronto Users"

Vous pouvez également ajouter des membres au groupe de rôles que vous créez à l’aide du paramètre *Members* comme indiqué dans la section Utiliser l’environnement de ligne de commande pour copier un groupe de rôles sans aucune portée plus haut dans cette rubrique. Pour plus d’informations sur les étendues de gestion, voir [Présentation des portées du rôle de gestion](understanding-management-role-scopes-exchange-2013-help.md).

Une fois que le nouveau groupe de rôles est créé, vous pouvez ajouter ou supprimer des rôles, modifier la portée des affectations sur le rôle, et plus encore.

Pour des informations détaillées sur la syntaxe et les paramètres, consultez les rubriques [Get-RoleGroup](https://technet.microsoft.com/fr-fr/library/dd638115\(v=exchg.150\)) et [New-RoleGroup](https://technet.microsoft.com/fr-fr/library/dd638181\(v=exchg.150\)).

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez bien copié un groupe de rôles, procédez comme suit :

1.  Dans le CAE, accédez à **Autorisations** \> **Rôles admin**.

2.  Vérifiez que le groupe de rôles copié apparaît dans la liste des groupes de rôles, puis sélectionnez-le.

3.  Vérifiez que les membres, les rôles attribués et l'étendue que vous avez indiqués dans le groupe de rôles copié sont répertoriés dans le volet des informations relatives au groupe de rôles.

## Supprimer un groupe de rôles

Si vous n’avez plus besoin du groupe de rôles que vous avez créé, vous pouvez le supprimer. Lorsque vous supprimez un groupe de rôles, les attributions de rôle de gestion entre le groupe de rôles et les rôles de gestion sont supprimées. Les rôles de gestion ne sont pas supprimés. Si un utilisateur dépendait du groupe de rôles pour accéder à une fonctionnalité, il n’y aura plus accès. Vous ne pouvez pas supprimer les rôles intégrés.

## Utiliser le CAE pour supprimer un groupe de rôles

1.  Dans le CAE, accédez à **Autorisations** \> **Rôles admin**.

2.  Sélectionnez le groupe de rôles à supprimer, puis cliquez sur **Supprimer**![Icône Supprimer](images/Dd979797.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "Icône Supprimer").

3.  Vérifiez que vous voulez effectivement supprimer le groupe de rôles sélectionné et, si tel est le cas, répondez **Oui** à l'avertissement.

## Utiliser l’environnement de ligne de commande Exchange Management Shell pour supprimer un groupe de rôles

Pour supprimer un groupe de rôles, voir la section [Examples](https://technet.microsoft.com/fr-fr/dd638141\(exchg.150\)#examples) dans [Remove-RoleGroup](https://technet.microsoft.com/fr-fr/library/dd638141\(v=exchg.150\)).

## Afficher des groupes de rôles

Vous pouvez afficher une liste de groupes de rôles ou des informations détaillées sur un groupe de rôles spécifique de votre organisation.

## Utiliser le CAE pour afficher une liste de groupes de rôles et les informations détaillées d'un groupe de rôles

1.  Dans CAE, accédez à **Autorisations** \> **Rôles admin**. Tous les groupes de rôles de votre organisation sont répertoriés ici.

2.  Sélectionnez un groupe de rôles pour en afficher les membres, les rôles attribués et l'étendue.

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour afficher une liste de groupes de rôles et les informations détaillées d'un groupe de rôles

Pour afficher une liste de groupes de rôles, voir la section [Examples](https://technet.microsoft.com/fr-fr/dd638115\(exchg.150\)#examples) dans [Get-RoleGroup](https://technet.microsoft.com/fr-fr/library/dd638115\(v=exchg.150\)).

## Ajouter un rôle à un groupe de rôles

L’ajout d’un rôle de gestion à un groupe de rôles est le moyen le plus efficace et le plus rapide d'octroyer des autorisations à un groupe d’administrateurs ou d'utilisateurs spécialistes. Si vous voulez permettre à des utilisateurs membres d’un groupe de rôles de gérer une fonctionnalité, vous devez ajouter le rôle de gestion qui gère cette fonctionnalité au groupe de rôles. Une fois que le rôle est ajouté, les membres du groupe de rôles se voient accorder les autorisations fournies par le rôle.

## Utiliser le CAE pour ajouter un rôle de gestion à un groupe de rôles

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159813.important(EXCHG.150).gif" title="Important" alt="Important" />Important :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Vous ne pouvez pas utiliser le Centre d'administration Exchange (CAE) pour ajouter des rôles à un groupe de rôles si vous avez utilisé l'environnement de ligne de commande Exchange Management Shell pour configurer plusieurs étendues de rôle de gestion ou des étendues exclusives au niveau du groupe de rôles. Si vous avez configuré plusieurs étendues ou étendues exclusives sur le groupe de rôles, vous devez utiliser les procédures de l’environnement de ligne de commande Exchange Management Shell ultérieurement dans cette rubrique pour ajouter des rôles au groupe de rôles. Pour plus d’informations sur les étendues de rôle de gestion, consultez la rubrique <a href="understanding-management-role-scopes-exchange-2013-help.md">Présentation des portées du rôle de gestion</a>.</td>
</tr>
</tbody>
</table>


1.  Dans CAE, accédez à **Autorisations** \> **Rôles admin**.

2.  Sélectionnez le groupe de rôles auquel ajouter un rôle, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

3.  Dans la section **Rôles**, sélectionnez les rôles à ajouter au groupe de rôles.

4.  Lorsque vous avez terminé l'ajout de rôles au groupe de rôles, cliquez sur **Enregistrer**.

## Utiliser l’environnement de ligne de commande Exchange Management Shell pour créer une attribution de rôle sans aucune portée

Vous pouvez créer une attribution de rôle sans aucune portée entre un rôle et un groupe de rôles. Lorsque vous effectuez cette opération, les étendues d’écriture implicite et de lecture implicite du rôle s’appliquent.

Utilisez la syntaxe suivante pour attribuer un rôle sans aucune portée à un groupe de rôles. Un nom d’attribution de rôle est créé automatiquement si vous n’en spécifiez pas un.

    New-ManagementRoleAssignment -SecurityGroup <role group name> -Role <role name>

Cet exemple attribue le rôle de gestion Transport Rules au groupe de rôles Seattle Compliance.

    New-ManagementRoleAssignment -SecurityGroup "Seattle Compliance" -Role "Transport Rules"

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [New-ManagementRoleAssignment](https://technet.microsoft.com/fr-fr/library/dd335193\(v=exchg.150\)).

## Utiliser l’environnement de ligne de commande Exchange Management Shell pour créer une attribution de rôle avec une portée prédéfinie

Si une portée prédéfinie correspond aux besoins de votre entreprise, vous pouvez l’appliquer à l’attribution de rôle plutôt que d’en créer une nouvelle. Pour obtenir une liste des étendues prédéfinies et leur description, consultez la rubrique [Présentation des portées du rôle de gestion](understanding-management-role-scopes-exchange-2013-help.md).

Pour plus d’informations sur les attributions de rôles, consultez la rubrique [Présentation des attributions de rôles de gestion](understanding-management-role-assignments-exchange-2013-help.md).

Utilisez la syntaxe suivante pour attribuer un rôle à un groupe de rôles avec une portée prédéfinie. Un nom d’attribution de rôle est créé automatiquement si vous n’en spécifiez pas un.

    New-ManagementRoleAssignment -SecurityGroup <role group name> -Role <role name> -RecipientRelativeWriteScope < MyGAL | MyDistributionGroups | Organization | Self >

Cet exemple attribue le rôle Message Tracking au groupe de rôles Enterprise Support et applique la portée prédéfinie Organization.

    New-ManagementRoleAssignment -SecurityGroup "Enterprise Support" -Role "Message Tracking" -RecipientRelativeWriteScope Organization

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [New-ManagementRoleAssignment](https://technet.microsoft.com/fr-fr/library/dd335193\(v=exchg.150\)).

## Utiliser l’environnement de ligne de commande Exchange Management Shell pour créer une attribution de rôle avec une portée de destinataire filtrée

Si vous avez créé une portée de destinataire filtrée, vous devez inclure cette portée dans la commande utilisée pour attribuer le rôle à un groupe de rôles à l’aide du paramètre *CustomRecipientWriteScope*.

Vous pouvez également inclure une portée d’écriture de configuration pour créer une attribution de rôle comportant une portée d’écriture de destinataire.

Pour plus d’informations sur les attributions de rôle et les étendues, voir les rubriques suivantes :

  - [Présentation des attributions de rôles de gestion](understanding-management-role-assignments-exchange-2013-help.md)

  - [Présentation des portées du rôle de gestion](understanding-management-role-scopes-exchange-2013-help.md)

Utilisez la syntaxe suivante pour attribuer un rôle à un groupe de rôles avec une portée de destinataire filtrée. Un nom d’attribution de rôle est créé automatiquement si vous n’en spécifiez pas un.

    New-ManagementRoleAssignment -SecurityGroup <role group name> -Role <role name> -CustomRecipientWriteScope <role scope name>

Cet exemple attribue le rôle Message Tracking au groupe de rôles Seattle Recipient Admins et applique la portée Seattle Recipients.

    New-ManagementRoleAssignment -SecurityGroup "Seattle Recipient Admins" -Role "Message Tracking" -CustomRecipientWriteScope "Seattle Recipients"

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [New-ManagementRoleAssignment](https://technet.microsoft.com/fr-fr/library/dd335193\(v=exchg.150\)).

## Utiliser l’environnement de ligne de commande Exchange Management Shell pour créer une attribution de rôle avec une étendue de configuration

Si vous avez créé un filtre de configuration de serveur ou de base de données ou une étendue basée sur une liste, vous devez inclure cette étendue dans la commande utilisée pour attribuer le rôle à un groupe de rôles à l’aide du paramètre *CustomConfigWriteScope*.

Vous pouvez également inclure une portée d’écriture de destinataire pour créer une attribution de rôle comportant une portée d’écriture de configuration.

Pour plus d’informations sur les attributions de rôle et les étendues de gestion, voir les rubriques suivantes :

  - [Présentation des attributions de rôles de gestion](understanding-management-role-assignments-exchange-2013-help.md)

  - [Présentation des portées du rôle de gestion](understanding-management-role-scopes-exchange-2013-help.md)

Utilisez la syntaxe suivante pour attribuer un rôle à un groupe de rôles avec une étendue de configuration. Un nom d’attribution de rôle est créé automatiquement si vous n’en spécifiez pas un.

    New-ManagementRoleAssignment -SecurityGroup <role group name> -Role <role name> -CustomConfigWriteScope <role scope name>

Cet exemple attribue le rôle Databases au groupe de rôles Seattle Server Admins et applique la portée Seattle Servers.

    New-ManagementRoleAssignment -SecurityGroup "Seattle Server Admins" -Role "Databases" -CustomConfigWriteScope "Seattle Servers"

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [New-ManagementRoleAssignment](https://technet.microsoft.com/fr-fr/library/dd335193\(v=exchg.150\)).

## Utiliser l’environnement de ligne de commande Exchange Shell pour créer une attribution de rôle avec une portée d’unité d’organisation

Si vous souhaitez appliquer l’étendue d’écriture d’un rôle à une unité d’organisation, spécifiez l’unité d’organisation directement dans le paramètre *RecipientOrganizationalUnitScope*.

Pour plus d’informations sur les attributions de rôle et les étendues de gestion, voir les rubriques suivantes :

  - [Présentation des attributions de rôles de gestion](understanding-management-role-assignments-exchange-2013-help.md)

  - [Présentation des portées du rôle de gestion](understanding-management-role-scopes-exchange-2013-help.md)

Utilisez la commande suivante pour attribuer un rôle à un groupe de rôles et réserver la portée d’écriture d’un rôle à une unité d’organisation spécifique. Un nom d’attribution de rôle est créé automatiquement si vous n’en spécifiez pas un.

    New-ManagementRoleAssignment -SecurityGroup <role group name> -Role <role name> -RecipientOrganizationalUnitScope <OU>

Cette exemple attribue le rôle Mail Recipients au groupe de rôles Seattle Recipient Admins et applique la portée de l’attribution à l’unité d’organisation Sales\\Users dans le domaine Contoso.com domain.

    New-ManagementRoleAssignment -SecurityGroup "Seattle Recipient Admins" -Role "Mail Recipients" -RecipientOrganizationalUnitScope contoso.com/sales/users

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [New-ManagementRoleAssignment](https://technet.microsoft.com/fr-fr/library/dd335193\(v=exchg.150\)).

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez bien ajouté des rôles à un groupe de rôles, procédez comme suit :

1.  Dans CAE, accédez à **Autorisations** \> **Rôles admin**.

2.  Sélectionnez le groupe de rôles auquel vous avez ajouté des rôles. Dans le volet des informations du groupe de rôles, vérifiez que les rôles ajoutés sont répertoriés.

## Supprimer un rôle d'un groupe de rôles

Le meilleur moyen pour révoquer des autorisations accordées à un groupe d'administrateurs ou d'utilisateurs spécialistes est de supprimer un rôle d'un groupe de rôles de gestion. Si vous ne souhaitez pas accorder à des administrateurs ou à des utilisateurs spécialistes l’autorisation de gérer une fonctionnalité, vous devez supprimer le rôle de gestion du groupe qui gère ces autorisations. Une fois le rôle supprimé, les membres du groupe de rôles ne seront plus autorisés à gérer la fonctionnalité.

> [!NOTE]
> Certains groupes de rôles (comme le groupe de rôles Gestion de l’organisation) limitent les rôles pouvant être supprimés. Pour plus d'informations, voir <a href="understanding-management-role-groups-exchange-2013-help.md">Présentation des groupes de rôles de gestion</a>.
> Si un administrateur est membre d’un autre groupe qui contient des rôles de gestion permettant à l’administrateur de gérer la fonctionnalité, vous devez soit supprimer l’administrateur des autres groupes de rôles, soit supprimer le rôle autorisant la gestion de la fonctionnalité des autres groupes de rôles.


## Utiliser le CAE pour supprimer un rôle de gestion dans un groupe de rôles

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159813.important(EXCHG.150).gif" title="Important" alt="Important" />Important :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Vous ne pouvez pas utiliser le Centre d'administration Exchange pour supprimer des rôles d'un groupe de rôles si vous avez utilisé l'environnement de ligne de commande Exchange Management Shell pour configurer plusieurs étendues ou des étendues exclusives au niveau du groupe de rôles. Si vous avez configuré des étendues multiples ou exclusives pour le groupe de rôles, vous devez supprimer les rôles du groupe de rôles en utilisant les procédures de l’environnement de ligne de commande Exchange Management Shell décrites ci-après. Pour plus d’informations sur les étendues de rôle de gestion, consultez la rubrique <a href="understanding-management-role-scopes-exchange-2013-help.md">Présentation des portées du rôle de gestion</a>.</td>
</tr>
</tbody>
</table>


1.  Dans le CAE, accédez à **Autorisations** \> **Rôles admin**.

2.  Sélectionnez le groupe de rôles duquel supprimer un rôle, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

3.  Dans la section **Rôles**, sélectionnez les rôles à supprimer du groupe de rôles.

4.  Lorsque vous avez terminé la suppression des rôles du groupe de rôles, cliquez sur **Enregistrer**.

## Utiliser l’environnement de ligne de commande Exchange Management Shell pour supprimer un rôle d’un groupe de rôles

Vous pouvez supprimer des rôles des groupes de rôles en récupérant l’attribution de rôle de gestion à l’aide de la cmdlet **Get-ManagementRoleAssignment**, puis en canalisant l’attribution de rôle renvoyée à la cmdlet **Remove-ManagementRoleAssignment**. À moins de vouloir supprimer simultanément les attributions de rôles de délégation et de rôles ordinaires, précisez le paramètre *Delegating* de manière à déterminer si vous voulez supprimer des attributions de rôles de délégation ou de rôles ordinaires.

Pour plus d’informations sur les attributions de rôles normales ou de délégation, voir [Présentation des attributions de rôles de gestion](understanding-management-role-assignments-exchange-2013-help.md).

Cette procédure utilise le traitement en pipeline. Pour plus d'informations sur le traitement en pipeline, voir [Traitement en pipeline](https://technet.microsoft.com/fr-fr/library/aa998260\(v=exchg.150\)).

Pour supprimer un rôle d’un groupe de rôles, utilisez la syntaxe suivante.

    Get-ManagementRoleAssignment -RoleAssignee <role group name> -Role <role name> -Delegating <$true | $false> | Remove-ManagementRoleAssignment

Cet exemple permet de supprimer le rôle Groupes de distribution du groupe de rôles des administrateurs des destinataires Seattle, qui autorise les administrateurs à gérer les groupes de distribution. Étant donné que nous souhaitons supprimer l’attribution de rôle qui autorise la gestion des groupes de distribution, le paramètre *Delegating* est configuré sur `$False`, ce qui permet de renvoyer uniquement des attributions de rôles ordinaires.

    Get-ManagementRoleAssignment -RoleAssignee "Seattle Recipient Administrators" -Role "Distribution Groups" -Delegating $false | Remove-ManagementRoleAssignment

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Remove-ManagementRoleAssignment](https://technet.microsoft.com/fr-fr/library/dd351205\(v=exchg.150\)).

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez bien supprimé des rôles d'un groupe de rôles, procédez comme suit :

1.  Dans le CAE, accédez à **Autorisations** \> **Rôles admin**.

2.  Sélectionnez le groupe de rôles duquel vous avez supprimé des rôles. Dans le volet des informations du groupe de rôles, vérifiez que les rôles supprimés ne sont plus répertoriés.

## Modifier l'étendue d'un groupe de rôles

Les attributions de rôles de gestion entre un groupe de rôles et un rôle contenant des étendues de gestion, qui déterminent les objets disponibles pour les membres de ce groupe de rôles. En modifiant l’étendue d’écriture sur un groupe de rôles, vous pouvez modifier des objets rendus disponibles aux membres du groupe de rôles pour les créer, les modifier ou les supprimer. Vous ne pouvez pas modifier l’étendue de lecture sur un groupe de rôles.

Exchange 2013 inclut des étendues qui sont appliquées par défaut à des attributions de rôles lorsqu’aucune étendue personnalisée n'est créée. Si vous souhaitez utiliser une étendue personnalisée avec une attribution de rôles sur un groupe de rôles, vous devez d’abord en créer une. Pour plus d’informations sur la création d’étendues personnalisées, qui est une tâche avancée, consultez la rubrique [Créer une étendue normale ou exclusive](create-a-regular-or-exclusive-scope-exchange-2013-help.md).

Pour plus d’informations sur les étendues de rôles de gestion et les attributions dans Exchange 2013, voir les rubriques suivantes :

  - [Présentation des portées du rôle de gestion](understanding-management-role-scopes-exchange-2013-help.md)

  - [Présentation des attributions de rôles de gestion](understanding-management-role-assignments-exchange-2013-help.md)

## Utiliser le CAE pour modifier l'étendue d'un groupe de rôles

Lorsque vous utilisez le Centre d'administration Exchange pour modifier l'étendue d'un groupe de rôles, vous modifiez en réalité l'étendue de toutes les attributions de rôles entre le groupe de rôles et chacun des rôles de gestion affectés au groupe de rôles. Si vous voulez modifier l'étendue des attributions de rôles spécifiques, vous devez utiliser les procédures de l’environnement de ligne de commande Exchange Management Shell décrites plus loin dans cette rubrique.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159813.important(EXCHG.150).gif" title="Important" alt="Important" />Important :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Vous ne pouvez pas utiliser le Centre d'administration Exchange pour gérer les étendues des attributions de rôles entre les rôles et un groupe de rôles si vous avez utilisé l'environnement de lignes de commande Exchange Management Shell pour configurer plusieurs étendues ou des étendues exclusives de ces attributions de rôles. Si vous avez configuré plusieurs étendues ou des étendues exclusives sur ces attributions de rôles, vous devez utiliser les procédures de l’environnement de ligne de commande Exchange Management Shell décrites plus loin dans cette rubrique pour gérer les étendues. Pour plus d’informations sur les étendues de rôle de gestion, consultez la rubrique <a href="understanding-management-role-scopes-exchange-2013-help.md">Présentation des portées du rôle de gestion</a>.</td>
</tr>
</tbody>
</table>


1.  Dans le CAE, accédez à **Autorisations** \> **Rôles admin**.

2.  Sélectionnez le groupe de rôles pour lequel vous voulez modifier l'étendue, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

3.  Sélectionnez une des deux options de **portée d’écriture** suivantes :
    
      - Une étendue d'écriture dans la zone déroulante, où vous pouvez sélectionner soit l'étendue d'écriture par défaut soit une étendue d'écriture personnalisée.
    
      - **Unité d’organisation**   Choisissez cette option et spécifiez une unité d’organisation pour lui associer ce groupe de rôles.

4.  Cliquez sur **Enregistrer** pour enregistrer les modifications apportées au groupe de rôles.

## Utiliser l’environnement de ligne de commande Exchange Management Shell pour modifier simultanément l’étendue de toutes les attributions de rôle sur un groupe de rôles

Les attributions de rôles entre le groupe de rôles et les rôles attribués peuvent utiliser l’étendue implicite obtenue des rôles, la même étendue personnalisée ou des étendues personnalisées différentes. Pour plus d’informations sur les attributions de rôles, consultez la rubrique [Présentation des attributions de rôles de gestion](understanding-management-role-assignments-exchange-2013-help.md).

Les étendues sur les attributions de rôles sont gérées à l’aide de la cmdlet **Set-ManagementRoleAssignment**. Vous ne pouvez pas gérer les étendues à l’aide de la cmdlet **Set-RoleGroup**.

Pour modifier simultanément l’étendue de toutes les attributions de rôle entre un groupe de rôles et un jeu de rôles de gestion, vous devez d’abord extraire les attributions de rôle du groupe de rôles, puis définir la nouvelle étendue sur chaque attribution. Pour ce faire, récupérez les attributions de rôle à l’aide de la cmdlet **Get-ManagementRoleAssignment**, puis transmettez-les à la cmdlet **Set-ManagementRoleAssignment**.

Cette procédure utilise les concepts de traitement en pipeline et le commutateur *WhatIf*. Pour plus d’informations, consultez les rubriques suivantes :

  - [Traitement en pipeline](https://technet.microsoft.com/fr-fr/library/aa998260\(v=exchg.150\))

  - [Commutateurs WhatIf, Confirm et ValidateOnly](whatif-confirm-and-validateonly-switches-exchange-2013-help.md)

Pour définir l’étendue de toutes les attributions de rôle sur un groupe de rôles simultanément, utilisez la syntaxe suivante.

    Get-ManagementRoleAssignment -RoleAssignee <name of role group> | Set-ManagementRoleAssignment -CustomRecipientWriteScope <recipient scope name> -CustomConfigWriteScope <configuration scope name> -RecipientRelativeScopeWriteScope < MyDistributionGroups | Organization | Self> -ExclusiveRecipientWriteScope <exclusive recipient scope name> -ExclusiveConfigWriteScope <exclusive configuration scope name> -RecipientOrganizationalUnitScope <organizational unit>

Vous utilisez uniquement les paramètres dont vous avez besoin pour configurer l’étendue que vous souhaitez utiliser. Par exemple, si vous souhaitez remplacer l’étendue du destinataire pour l’ensemble des attributions de rôle sur le groupe de rôles Gestion des destinataires Ventes par le groupe Employés du service des ventes directes, utilisez la commande suivante.

    Get-ManagementRoleAssignment -RoleAssignee "Sales Recipient Management" | Set-ManagementRoleAssignment -CustomRecipientWriteScope "Direct Sales Employees"

> [!NOTE]
> Le commutateur <em>WhatIf</em> vous permet de vérifier que seules les attributions de rôle devant être modifiées sont modifiées. Exécutez la commande précédente avec le commutateur <em>WhatIf</em> pour vérifier les résultats, puis supprimez le commutateur <em>WhatIf</em> pour appliquer les modifications.


Pour plus d’informations sur la modification des attributions des rôles de gestion, voir [Modifier une attribution de rôle](change-a-role-assignment-exchange-2013-help.md).

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Get-ManagementRoleAssignment](https://technet.microsoft.com/fr-fr/library/dd351024\(v=exchg.150\)).

## Utiliser l’environnement de ligne de commande pour modifier individuellement les attributions de rôle sur un groupe de rôles

Les attributions de rôles entre le groupe de rôles et les rôles attribués peuvent utiliser l’étendue implicite obtenue des rôles, la même étendue personnalisée ou des étendues personnalisées différentes. Pour plus d’informations sur les attributions de rôles, consultez la rubrique [Présentation des attributions de rôles de gestion](understanding-management-role-assignments-exchange-2013-help.md).

Les étendues sur les attributions de rôles sont gérées à l’aide de la cmdlet **Set-ManagementRoleAssignment**. Vous ne pouvez pas gérer les étendues à l’aide de la cmdlet **Set-RoleGroup**.

Cette procédure utilise les concepts de traitement en pipeline et la cmdlet **Format-List**. Pour plus d’informations, consultez les rubriques suivantes :

  - [Traitement en pipeline](https://technet.microsoft.com/fr-fr/library/aa998260\(v=exchg.150\))

  - [Utilisation de la sortie de la commande](working-with-command-output-exchange-2013-help.md)

Pour modifier l’étendue d’une attribution de rôle entre un groupe de rôles et un rôle de gestion, vous devez d’abord trouver le nom de l’attribution de rôle, puis définir l’étendue sur l’attribution.

1.  Pour rechercher les noms de toutes les attributions de rôle sur un groupe de rôles, utilisez la commande suivante. En transmettant les attributions de rôle de gestion à la cmdlet **Format-List**, vous pouvez afficher le nom complet de l’attribution.
    
        Get-ManagementRoleAssignment -RoleAssignee <role group name> | Format-List Name

2.  Recherchez le nom de l’attribution de rôle que vous souhaitez modifier. Utilisez le nom de l'attribution de rôle dans l'étape suivante.

3.  Pour définir l’étendue d’une attribution individuelle, utilisez la syntaxe suivante.
    
        Set-ManagementRoleAssignment <role assignment name> -CustomRecipientWriteScope <recipient scope name> -CustomConfigWriteScope <configuration scope name> -RecipientRelativeScopeWriteScope < MyDistributionGroups | Organization | Self> -ExclusiveRecipientWriteScope <exclusive recipient scope name> -ExclusiveConfigWriteScope <exclusive configuration scope name> -RecipientOrganizationalUnitScope <organizational unit>

Vous utilisez uniquement les paramètres dont vous avez besoin pour configurer l’étendue que vous souhaitez utiliser. Par exemple, si vous souhaitez remplacer l’étendue du destinataire de l’attribution de rôle Destinataires des messages\_Destinataires des Ventes par Tous les employés du service des ventes, utilisez la commande suivante.

    Set-ManagementRoleAssignment "Mail Recipients_Sales Recipient Management" -CustomRecipientWriteScope "All Sales Employees"

Pour plus d’informations sur la modification des attributions des rôles de gestion, voir [Modifier une attribution de rôle](change-a-role-assignment-exchange-2013-help.md).

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Set-ManagementRoleAssignment](https://technet.microsoft.com/fr-fr/library/dd335173\(v=exchg.150\)).

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez bien modifié l'étendue d'une attribution de rôle d'un groupe de rôles, procédez comme suit :

  - Si vous avez utilisé le CAE pour configurer l'étendue du groupe de rôles, procédez comme suit :
    
    1.  Dans le CAE, accédez à **Autorisations** \> **Rôles d'administrateur**. Tous les groupes de rôles de votre organisation sont répertoriés ici.
    
    2.  Sélectionnez un groupe de rôles pour afficher l'étendue qui est configurée pour ce groupe de rôles.

  - Si vous avez utilisé l'environnement de ligne de commande Exchange Management Shell pour configurer l'étendue du groupe de rôles, procédez comme suit :
    
    1.  Exécutez la commande suivante dans l’environnement de ligne de commande Exchange Management Shell.
        
            Get-ManagementRoleAssignment -RoleAssignee <role group name> | Format-Table *WriteScope
    
    2.  Vérifiez que l'étendue d'écriture des attributions de rôles a été remplacée par l'étendue que vous avez indiquée.

## Ajouter ou supprimer un délégué de groupe de rôles

Les délégués de groupe de rôles sont des utilisateurs ou des groupes universels de sécurité qui peuvent ajouter ou supprimer des membres dans un groupe de rôle ou encore modifier les propriétés d’un groupe de rôles. En ajoutant ou supprimant des délégués de groupe de rôles, vous pouvez contrôler quels sont ceux autorisés à gérer un groupe de rôles.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159813.important(EXCHG.150).gif" title="Important" alt="Important" />Important :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Après avoir ajouté un délégué à un groupe de rôles, ce dernier peut uniquement être géré par les délégués du groupe de rôles ou par les utilisateurs auxquels est affecté, directement ou indirectement le rôle de gestion Gestion des rôles.<br />
Si un utilisateur reçoit, directement ou indirectement, le rôle Gestion des rôles et qu’il n’est pas ajouté comme délégué du groupe de rôles, l’utilisateur doit utiliser le commutateur <em>BypassSecurityGroupManagerCheck</em> sur les cmdlets <strong>Add-RoleGroupMember</strong>, <strong>Remove-RoleGroupMember</strong>, <strong>Update-RoleGroupMember</strong> et <strong>Set-RoleGroup</strong> pour gérer un groupe de rôles.</td>
</tr>
</tbody>
</table>


> [!NOTE]
> Vous ne pouvez pas utiliser le CAE pour ajouter un délégué à un groupe de rôles.


## Utilisation du Shell pour ajouter un délégué à un groupe de rôles

Pour modifier la liste des délégués sur un groupe de rôles, vous utilisez le paramètre *ManagedBy* sur la cmdlet **Set-RoleGroup**. Le paramètre *ManagedBy* écrase toute la liste des délégués dans le groupe de rôles. Pour ajouter des délégués au groupe de rôles au lieu de remplacer toute la liste de délégués, suivez les étapes suivantes :

1.  Stockez le groupe de rôles dans une variable à l’aide de la commande suivante.
    
        $RoleGroup = Get-RoleGroup <role group name>

2.  Ajoutez le délégué au groupe de rôles stocké dans la variable à l’aide de la commande suivante.
    
        $RoleGroup.ManagedBy += (Get-User <user to add>).Identity
    
    > [!NOTE]
    > Utilisez la cmdlet <strong>Get-Group</strong> si vous souhaitez ajouter un groupe de sécurité universel.


3.  Répétez l’étape 2 pour chaque délégué que vous souhaitez ajouter.

4.  Appliquez la nouvelle liste de délégués au groupe de rôles réel à l’aide de la commande suivante.
    
        Set-RoleGroup <role group name> -ManagedBy $RoleGroup.ManagedBy

Cet exemple illustre l’ajout de l’utilisateur David Strome comme délégué du groupe de rôles Gestion de l’organisation.

    $RoleGroup = Get-RoleGroup "Organization Management"
    $RoleGroup.ManagedBy += (Get-User "David Strome").Identity
    Set-RoleGroup "Organization Management" -ManagedBy $RoleGroup.ManagedBy

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Set-RoleGroup](https://technet.microsoft.com/fr-fr/library/dd638182\(v=exchg.150\)).

## Utilisation du Shell pour supprimer un délégué d’un groupe de rôles

Pour modifier la liste des délégués sur un groupe de rôles, vous utilisez le paramètre *ManagedBy* sur la cmdlet **Set-RoleGroup**. Le paramètre *ManagedBy* écrase toute la liste des délégués dans le groupe de rôles. Pour supprimer des délégués d’un groupe de rôles au lieu de remplacer toute la liste de délégués, suivez les étapes suivantes :

1.  Stockez le groupe de rôles dans une variable à l’aide de la commande suivante.
    
        $RoleGroup = Get-RoleGroup <role group name>

2.  Supprimez le délégué du groupe de rôles stocké dans la variable à l’aide de la commande suivante.
    
        $RoleGroup.ManagedBy -= (Get-User <user to remove>).Identity
    
    > [!NOTE]
    > Utilisez la cmdlet <strong>Get-Group</strong> si vous souhaitez supprimer un groupe de sécurité universelle.


3.  Répétez l’étape 2 pour chaque délégué que vous souhaitez supprimer.

4.  Appliquez la nouvelle liste de délégués au groupe de rôles réel à l’aide de la commande suivante.
    
        Set-RoleGroup <role group name> -ManagedBy $RoleGroup.ManagedBy

Cet exemple illustre la suppression de l’utilisateur David Strome comme délégué du groupe de rôles Gestion de l’organisation.

    $RoleGroup = Get-RoleGroup "Organization Management"
    $RoleGroup.ManagedBy -= (Get-User "David Strome").Identity
    Set-RoleGroup "Organization Management" -ManagedBy $RoleGroup.ManagedBy

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Set-RoleGroup](https://technet.microsoft.com/fr-fr/library/dd638182\(v=exchg.150\)).

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez bien modifié la liste des délégués d'un groupe de rôles, procédez comme suit :

1.  Dans l’environnement de ligne de commande Exchange Management Shell, exécutez la commande suivante.
    
        Get-RoleGroup <role group name> | Format-List ManagedBy

2.  Vérifiez que les délégués répertoriés au niveau de la propriété *ManagedBy* incluent uniquement les délégués qui devraient être en mesure de gérer le groupe de rôles.

