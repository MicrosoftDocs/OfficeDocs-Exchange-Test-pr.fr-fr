---
title: 'Créer un rôle: Exchange 2013 Help'
TOCTitle: Créer un rôle
ms:assetid: e614ad8f-5946-4135-b130-89ea626afcd4
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dd351214(v=EXCHG.150)
ms:contentKeyID: 50479455
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Créer un rôle

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2012-10-17_

Vous pouvez créer un rôle de gestion, modifier des entrées de rôle de gestion, ajouter une portée si besoin et attribuer le rôle à un utilisateur. Les cas dans lesquels vous devrez effectuer cette procédure sont assez rares. Avant de devoir créer un rôle de gestion, vérifiez d'abord si un rôle de gestion intégré peut être utilisé. Pour obtenir une liste des rôles de gestion intégrés, voir [Rôles de gestion intégrés](built-in-management-roles-exchange-2013-help.md).

Pour plus d’informations sur les rôles de gestion dans Microsoft Exchange Server 2013, voir [Présentation des rôles de gestion](understanding-management-roles-exchange-2013-help.md).

> [!NOTE]
> Cette rubrique n'indique pas comment créer un rôle de gestion sans portée définie. Pour plus d'informations sur la création d'un rôle de gestion sans portée définie, voir <a href="create-an-unscoped-role-exchange-2013-help.md">Créer un rôle non délimité</a>.


Souhaitez-vous rechercher les autres tâches de gestion relatives aux rôles ? Consultez la rubrique [Autorisations avancées](advanced-permissions-exchange-2013-help.md).

## Ce qu’il faut savoir avant de commencer ?

  - Durée estimée de la procédure : 10 minutes

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez entrée «Rôles de gestion» dans la rubrique [Autorisations pour la gestion des rôles](role-management-permissions-exchange-2013-help.md).

  - Vous devez utiliser l’environnement de ligne de commande Exchange Management Shell pour effectuer ces procédures.

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.


## Comment procéder ?

## Étape 1 : créer le rôle de gestion

Les nouveaux rôles de gestion sont basés sur des rôles existants. Lorsque vous créez un rôle, un rôle existant et ses entrées de rôle de gestion sont copiés dans le nouveau rôle. Le rôle existant devient le parent du nouveau rôle enfant. Vous devez toujours choisir un rôle qui contient les cmdlets et les paramètres dont vous avez besoin ; supprimez ensuite les cmdlets et les paramètres dont vous n'avez pas besoin. Les rôles enfants ne peuvent pas avoir des entrées de rôle de gestion qui n'existent pas dans le rôle parent.

Utilisez la syntaxe suivante pour créer le nouveau rôle.

```powershell
New-ManagementRole -Parent <existing role to copy> -Name <name of new role>
```

Cet exemple copie le rôle Mail Recipients et ses entrées de rôle de gestion dans le rôle Seattle Mail Recipients.

```powershell
New-ManagementRole -Parent "Mail Recipients" -Name "Seattle Mail Recipients"
```

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [New-ManagementRole](https://technet.microsoft.com/fr-fr/library/dd298073\(v=exchg.150\)).

## Étape 2 : modifier les entrées de rôle de gestion du nouveau rôle

Après avoir créé votre rôle, vous devez modifier les entrées de rôle. Vous pouvez supprimer une entrée de rôle entière. Dans ce cas, l'accès à la cmdlet associée est également supprimé. Ou bien, vous pouvez supprimer des paramètres d'une entrée de rôle pour supprimer l'accès à certains paramètres sur la cmdlet associée.

Vous ne pouvez pas ajouter des entrées ou des paramètres de rôle sur des entrées de rôle sauf s'ils existent dans le rôle parent. Puisque vous venez de créer un rôle à partir d’un rôle parent à l’étape 1, vous ne pouvez pas ajouter des paramètres ou des entrées de rôles supplémentaires sur les entrées de rôles car elles n’existent pas dans le rôle parent.

Lorsque vous modifiez une entrée sur un rôle, vous pouvez effectuez l’une des actions suivantes :

  - Supprimer une entrée de rôle entière et unique.

  - Supprimer des entrées de rôles entières multiples.

  - Supprimer des paramètres d’une entrée de rôle.

Pour supprimer des entrées de rôles de votre nouveau rôle, voir [Supprimer une entrée de rôle d'un rôle](remove-a-role-entry-from-a-role-exchange-2013-help.md).

## Étape 3 : créer une portée de rôle de gestion personnalisée, si nécessaire

Les portées de rôle de gestion déterminent les objets que l'utilisateur peut utiliser pour afficher ou modifier les entrées de rôle configurées à l'étape 2. Les nouveaux rôles de gestion héritent des portées de lecture et d'écriture de leur rôle parent. Ces portées sont appelées *portées implicites*. Toutefois, dans certains cas vous devrez modifier la portée d'écriture des nouveaux rôles en fonction des besoins de votre entreprise. Lorsque vous créez une portée personnalisée pour un rôle, vous remplacez la portée d'écriture implicite de ce rôle. La portée de lecture implicite du rôle ne change pas. Pour plus d’informations sur les portées de rôle de gestion, voir [Présentation des portées du rôle de gestion](understanding-management-role-scopes-exchange-2013-help.md).

Vous pouvez créer une portée personnalisée et une portée exclusive, utiliser une portée prédéfinie ou appliquer une portée à une attribution pour une unité d'organisation. La nouvelle portée doit être dans la portée de lecture implicite du rôle. Pour utiliser une portée prédéfinie ou pour spécifier une unité d'organisation, passez à l'étape 4.

Pour ajouter une portée personnalisée à votre nouveau rôle, voir [Créer une étendue normale ou exclusive](create-a-regular-or-exclusive-scope-exchange-2013-help.md).

## Étape 4 : attribuer le nouveau rôle de gestion

L’étape finale lorsque vous créez et configurez un rôle consiste à l’attribuer à un utilisateur.

Lorsque vous créez une attribution de rôle, vous avez plusieurs possibilités :

  - Créer l'attribution de rôle sans aucune portée.

  - Créer l'attribution de rôle avec une portée prédéfinie.

  - Créer l'attribution de rôle avec une unité d'organisation sans filtre de restriction de domaine.

  - Créer l'attribution de rôle avec la portée exclusive ou personnalisée créée à l'étape 3.
    
    > [!NOTE]
    > Vous ne pouvez pas spécifier une portée lorsque vous créez une attribution entre un rôle et une stratégie d'attribution de rôle de gestion.


Vous pouvez attribuer le nouveau rôle à un groupe de rôles, une stratégie d'attribution de rôle, un utilisateur ou un groupe de sécurité universel. Pour plus d’informations, consultez les rubriques suivantes :

  - [Gérer des groupes de rôles](manage-role-groups-exchange-2013-help.md)

  - [Gérer les stratégies d’attribution des rôles](manage-role-assignment-policies-exchange-2013-help.md)

  - [Ajouter un rôle à un utilisateur ou un groupe de sécurité universel](add-a-role-to-a-user-or-usg-exchange-2013-help.md)

