---
title: 'Modifier l’étendue d’un rôle: Exchange 2013 Help'
TOCTitle: Modifier l’étendue d’un rôle
ms:assetid: 9180e1e0-c352-4ccd-8da6-885a2e309867
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dd298145(v=EXCHG.150)
ms:contentKeyID: 50478718
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Modifier l’étendue d’un rôle

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2012-10-03_

Les étendues des rôles de gestion déterminent quels objets sont mis à la disposition de l’utilisateur pour que ceux-ci puissent être modifiés à l’aide des cmdlets et des paramètres qui lui sont attribués. En modifiant une étendue, vous pouvez modifier des objets rendus disponibles aux utilisateurs pour les créer, les modifier ou les supprimer.

Vous pouvez modifier une étendue de gestion personnalisée. Vous pouvez modifier les étendues exclusives ou normales. Si vous modifiez une étendue exclusive, la nouvelle étendue prend effet immédiatement. Si vous souhaitez modifier une attribution de rôle de gestion avec une étendue de gestion d’unité d’organisation ou prédéfinie, voir [Modifier une attribution de rôle](change-a-role-assignment-exchange-2013-help.md).

Pour plus d’informations sur les étendues de rôles de gestion et les attributions dans Microsoft Exchange Server 2013, voir les rubriques suivantes :

  - [Présentation des portées du rôle de gestion](understanding-management-role-scopes-exchange-2013-help.md)

  - [Présentation des attributions de rôles de gestion](understanding-management-role-assignments-exchange-2013-help.md)

Souhaitez-vous rechercher les autres tâches de gestion relatives aux étendues des rôles ? Consultez la rubrique [Autorisations avancées](advanced-permissions-exchange-2013-help.md).

## Ce qu’il faut savoir avant de commencer ?

  - Durée d’exécution estimée de chaque procédure : 5 minutes

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Étendues de gestion » dans la rubrique [Autorisations pour la gestion des rôles](role-management-permissions-exchange-2013-help.md).

  - Vous devez utiliser l’environnement de ligne de commande Exchange Management Shell pour effectuer ces procédures.

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.


## Que souhaitez-vous faire ?

## Modifier le nom d’une étendue

Pour modifier le nom d’une étendue, utilisez la syntaxe suivante.

    Set-ManagementScope <current scope name> -Name <new scope name>

Cet exemple indique comment changer l’étendue de serveurs Seattle en serveurs Seattle Exchange.

    Set-ManagementScope "Seattle Servers" -Name "Seattle Exchange Servers"

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Set-ManagementScope](https://technet.microsoft.com/fr-fr/library/dd297996\(v=exchg.150\)).

## Modifier un filtre de destinataire sur une étendue

Pour modifier le filtre de destinataire sur une étendue, utilisez la syntaxe suivante.

    Set-ManagementScope <scope name> -RecipientRestrictionFilter { <new recipient filter> }

Cet exemple indique comment modifier le filtre de destinataire pour faire correspondre tous les objets destinataire où la propriété **Company** est définie sur contoso.

    Set-ManagementScope "Company Scope" -RecipientRestrictionFilter { Company -eq 'contoso' }

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Set-ManagementScope](https://technet.microsoft.com/fr-fr/library/dd297996\(v=exchg.150\)).

Pour en savoir plus sur les filtres de destinataire et afficher la liste des propriétés de destinataire filtrables, voir [Présentation des filtres d’attribution du rôle de gestion](understanding-management-role-scope-filters-exchange-2013-help.md).

## Modifier la racine de l’unité d’organisation sur une étendue

Pour modifier la racine de l’unité d’organisation sur une étendue, utilisez la syntaxe suivante.

    Set-ManagementScope <scope name> -RecipientRoot <OU>

Cet exemple modifie la racine de l’unité d’organisation pour les utilisateurs du service des ventes en Amérique du Nord sous le domaine contoso.com.

    Set-ManagementScope "Sales Users" -RecipientRoot "contoso.com/North America/Sales"

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Set-ManagementScope](https://technet.microsoft.com/fr-fr/library/dd297996\(v=exchg.150\)).

## Modifier un filtre de serveur dans une étendue

Pour modifier le filtre de serveur sur une étendue, utilisez la syntaxe suivante.

    Set-ManagementScope <scope name> -ServerRestrictionFilter { <new server filter> }

Dans cet exemple, nous modifions le filtre de serveur afin de correspondre à tous les objets serveur dans lesquels la propriété **ServerSite** est définie à 'CN=Redmond,CN=Sites,CN=Configuration,DC=contoso,DC=com'.

    Set-ManagementScope "Company Scope" -ServerRestrictionFilter { ServerSite -eq 'CN=Redmond,CN=Sites,CN=Configuration,DC=contoso,DC=com' }

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Set-ManagementScope](https://technet.microsoft.com/fr-fr/library/dd297996\(v=exchg.150\)).

Pour en savoir plus sur les filtres de serveur et afficher la liste des propriétés de serveur filtrables, voir [Présentation des filtres d’attribution du rôle de gestion](understanding-management-role-scope-filters-exchange-2013-help.md).

## Modifier la liste de serveurs sur une étendue

Vous ne pouvez pas modifier la liste des serveurs sur une étendue. Si vous avez besoin de modifier la liste des serveurs, vous devez procéder comme suit :

1.  Si nécessaire, récupérez la liste des serveurs en cours dans l’étendue à remplacer en utilisant la procédure « Afficher une étendue spécifique » dans la rubrique [Afficher les étendues des rôles](view-role-scopes-exchange-2013-help.md).

2.  Créez une étendue avec la nouvelle liste de serveurs en utilisant « Étape 1 : Créer une procédure d’étendue » personnalisée dans la rubrique [Créer une étendue normale ou exclusive](create-a-regular-or-exclusive-scope-exchange-2013-help.md).

3.  Modifiez toutes les attributions de rôle de gestion qui utilisent l’ancienne étendue pour utiliser la nouvelle à l’aide de la procédure « Utiliser l’environnement Shell pour modifier le filtre de serveur ou l’étendue de liste sur une attribution de rôle » dans la rubrique [Modifier une attribution de rôle](change-a-role-assignment-exchange-2013-help.md).

4.  Supprimez l’ancienne étendue à l’aide de la procédure dans la rubrique [Supprimer une étendue de rôle](remove-a-role-scope-exchange-2013-help.md).

## Modifier un filtre de base de données sur une étendue

Pour modifier le filtre de base de données sur une étendue, utilisez la syntaxe suivante.

    Set-ManagementScope <scope name> -DatabaseRestrictionFilter { <new database filter> }

Cet exemple indique comment modifier le filtre de base de données pour faire correspondre tous les objets base de données où la propriété **Name** contient la chaîne « Executive ».

    Set-ManagementScope "Database Executive Scope" -DatabaseRestrictionFilter { Name -Like "*Executive*" }

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Set-ManagementScope](https://technet.microsoft.com/fr-fr/library/dd297996\(v=exchg.150\)).

Pour en savoir plus sur les filtres de base de données et afficher la liste des propriétés de base de données filtrables, voir [Présentation des filtres d’attribution du rôle de gestion](understanding-management-role-scope-filters-exchange-2013-help.md).

## Modifier la liste de bases de données sur une étendue

Vous ne pouvez pas modifier la liste des bases de données sur une étendue. Si vous avez besoin de modifier la liste des bases de données, vous devez procéder comme suit :

1.  Si nécessaire, récupérez la liste des bases de données en cours dans l’étendue à remplacer en utilisant la procédure « Afficher une étendue spécifique » dans la rubrique [Afficher les étendues des rôles](view-role-scopes-exchange-2013-help.md).

2.  Créez une étendue avec la nouvelle liste de bases de données en utilisant « Étape 1 : Créer une procédure d’étendue » personnalisée dans la rubrique [Créer une étendue normale ou exclusive](create-a-regular-or-exclusive-scope-exchange-2013-help.md).

3.  Modifiez toutes les attributions de rôle de gestion qui utilisent l’ancienne étendue pour utiliser la nouvelle à l’aide de la procédure « Utiliser l’environnement Shell pour modifier le filtre de base de données ou l’étendue de liste sur une attribution de rôle » dans la rubrique [Modifier une attribution de rôle](change-a-role-assignment-exchange-2013-help.md).

4.  Supprimez l’ancienne étendue à l’aide de la procédure dans la rubrique [Supprimer une étendue de rôle](remove-a-role-scope-exchange-2013-help.md).

