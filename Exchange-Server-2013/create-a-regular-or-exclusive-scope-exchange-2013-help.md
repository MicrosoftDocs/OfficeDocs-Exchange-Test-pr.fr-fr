---
title: 'Créer une étendue normale ou exclusive: Exchange 2013 Help'
TOCTitle: Créer une étendue normale ou exclusive
ms:assetid: b97a5be3-15cc-4954-ba30-a824a95e21be
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dd351083(v=EXCHG.150)
ms:contentKeyID: 50478946
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Créer une étendue normale ou exclusive

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2015-04-07_

Les étendues des rôles de gestion déterminent quels objets sont mis à la disposition de l’utilisateur pour que ceux-ci puissent être modifiés à l’aide des cmdlets et des paramètres qui lui sont attribués. En ajoutant une étendue de gestion, vous pouvez configurer les attributions des rôles de gestion afin que les utilisateurs puissent administrer des serveurs, des bases de données, des destinataires et des objets spécifiques au sein de votre organisation, sans pouvoir modifier d’autres objets.

> [!IMPORTANT]
> Lorsque vous créez une étendue normale ou exclusive, vous replacez l'étendue d'écriture définie sur le rôle de gestion que vous attribuez. Vous ne pouvez pas remplacer l'étendue de lecture configurée sur le rôle de gestion.


Vous pouvez créer une étendue de gestion personnalisée et ajouter ou modifier une attribution de rôle de gestion. Pour créer une attribution de rôle de gestion avec une étendue de gestion pré-générée ou d'unité d'organisation, voir [Ajouter un rôle à un utilisateur ou un groupe de sécurité universel](add-a-role-to-a-user-or-usg-exchange-2013-help.md).

Pour plus d’informations sur les étendues de rôles de gestion et les attributions dans Microsoft Exchange Server 2013, voir les rubriques suivantes :

  - [Présentation des portées du rôle de gestion](understanding-management-role-scopes-exchange-2013-help.md)

  - [Présentation des attributions de rôles de gestion](understanding-management-role-assignments-exchange-2013-help.md)

Souhaitez-vous rechercher les autres tâches de gestion relatives aux étendues ? Consultez la rubrique [Autorisations avancées](advanced-permissions-exchange-2013-help.md).

## Ce qu’il faut savoir avant de commencer ?

  - Durée d’exécution estimée de chaque procédure : 5 minutes

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Étendues de gestion » dans la rubrique [Autorisations pour la gestion des rôles](role-management-permissions-exchange-2013-help.md).

  - Vous devez utiliser l’environnement de ligne de commande Exchange Management Shell pour effectuer ces procédures.

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.


## Comment procéder ?

## Étape 1 : Créer une étendue personnalisée

Pour créer une étendue personnalisée, choisissez l’un des types d’étendues ci-dessous.

## Étendue de filtre de destinataire

Les étendues basées sur le filtre destinataires sont créées à l'aide du paramètre *RecipientRestrictionFilter* de la cmdlet **New-ManagementScope**. Lorsque vous créez un filtre de destinataire, outre les propriétés du destinataire à filtrer, vous pouvez spécifier l’unité d’organisation dans laquelle la requête du filtre s’exécute. Lorsque vous indiquez une unité d'organisation de base, vous limitez encore davantage la portée d'écriture du rôle.

Pour plus d’informations sur les filtres d’étendue de gestion, voir [Présentation des filtres d’attribution du rôle de gestion](understanding-management-role-scope-filters-exchange-2013-help.md).

Utilisez la syntaxe suivante pour créer une étendue de filtre de restriction de domaine avec une unité d'organisation de base.

```powershell
New-ManagementScope -Name <scope name> -RecipientRestrictionFilter <filter query> [-RecipientRoot <OU>]
```

Cet exemple crée une étendue qui inclut toutes les boîtes aux lettres de l'unité d'organisation contoso.com/Sales.

```powershell
New-ManagementScope -Name "Mailboxes in Sales OU" -RecipientRestrictionFilter { RecipientType -eq 'UserMailbox' } -RecipientRoot "contoso.com/Sales OU"
```

> [!NOTE]
> Vous pouvez omettre le paramètre <em>RecipientRoot</em> si vous souhaitez que le filtre s'applique à toute l'étendue de lecture implicite du rôle de gestion et non simplement à une unité d'organisation spécifique.


Pour obtenir des informations détaillées sur la syntaxe et les paramètres, consultez la rubrique [New-ManagementScope](https://technet.microsoft.com/fr-fr/library/dd335137\(v=exchg.150\)).

## Étendue de configuration de filtre de serveur

Les étendues de configuration basées sur le filtre serveur sont créées à l'aide du paramètre *ServerRestrictionFilter* de la cmdlet **New-ManagementScope**. Un filtre serveur vous permet de créer une étendue qui s'applique uniquement aux serveurs correspondant au filtre que vous spécifiez.

Pour plus d’informations sur les filtres d’étendue de gestion et pour obtenir une liste des propriétés de serveur filtrables, consultez la rubrique [Présentation des filtres d’attribution du rôle de gestion](understanding-management-role-scope-filters-exchange-2013-help.md).

Utilisez la syntaxe suivante pour créer une étendue de filtre de serveur.

```powershell
New-ManagementScope -Name <scope name> -ServerRestrictionFilter <filter query>
```

Dans cet exemple, une étendue qui inclut tous les serveurs au sein du site AD (Active Directory) 'CN=Redmond,CN=Sites,CN=Configuration,DC=contoso,DC=com' est créée.

```powershell
New-ManagementScope -Name "Servers in Seattle AD site" -ServerRestrictionFilter { ServerSite -eq 'CN=Redmond,CN=Sites,CN=Configuration,DC=contoso,DC=com' }
```

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [New-ManagementScope](https://technet.microsoft.com/fr-fr/library/dd335137\(v=exchg.150\)).

## Étendue de configuration de liste de serveurs

Les étendues de configuration basées sur la liste de serveurs sont créées à l'aide du paramètre *ServerList* de la cmdlet **New-ManagementScope**. Une étendue de liste de serveurs vous permet de créer une étendue qui s’applique uniquement aux serveurs que vous spécifiez dans une liste.

Utilisez la syntaxe suivante pour créer une étendue basée sur une liste de serveurs.

```powershell
New-ManagementScope -Name <scope name> -ServerList <server 1>, <server 2...>
```

Cet exemple crée une étendue qui s'applique uniquement aux serveurs MBX1, MBX3 et MBX5.

```powershell
New-ManagementScope -Name "Mailbox servers" -ServerList MBX1,MBX3,MBX5
```

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [New-ManagementScope](https://technet.microsoft.com/fr-fr/library/dd335137\(v=exchg.150\)).

## Étendue de configuration de filtre de base de données

Les étendues de configuration basées sur un filtre de base de données sont créées à l’aide du paramètre *DatabaseRestrictionFilter* de la cmdlet **New-ManagementScope**. Un filtre de base de données vous permet de créer une étendue qui s’applique uniquement aux bases de données correspondant au filtre que vous spécifiez.

> [!IMPORTANT]
> Les attributions de rôle associées aux étendues de base de données s’appliquent uniquement aux utilisateurs qui se connectent à des serveurs dotés de Microsoft Exchange Server 2010 Service Pack 1 (SP1) ou version ultérieure ou d’Exchange 2013. Si un utilisateur auquel est appliquée une attribution de rôle associée à une étendue de base de données se connecte à une version de serveur antérieure à Exchange 2010 SP1, l’attribution de rôle n’est pas appliquée à cet utilisateur et celui-ci ne bénéficiera pas des autorisations octroyées dans le cadre de cette attribution.


Pour plus d’informations sur les filtres d’étendue de gestion et pour obtenir une liste des propriétés de base de données filtrables, consultez la rubrique [Présentation des filtres d’attribution du rôle de gestion](understanding-management-role-scope-filters-exchange-2013-help.md).

Utilisez la syntaxe suivante pour créer un filtre de restriction appliqué à la base de données.

```powershell
New-ManagementScope -Name <scope name> -DatabaseRestrictionFilter <filter query>
```

Cet exemple crée une étendue qui inclut toutes les bases de données contenant la chaîne « Executive » dans la propriété **Name** de la base de données.

```powershell
New-ManagementScope -Name "Executive Databases" -DatabaseRestrictionFilter { Name -Like '*Executive*' }
```

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [New-ManagementScope](https://technet.microsoft.com/fr-fr/library/dd335137\(v=exchg.150\)).

## Étendue de configuration de liste de bases de données

Les étendues de configuration basées sur une liste de bases de données sont créées à l’aide du paramètre *DatabaseList* de la cmdlet **New-ManagementScope**. Une étendue de liste de bases de données vous permet de créer une étendue qui s’applique uniquement aux bases de données que vous spécifiez dans une liste.

> [!IMPORTANT]
> Les attributions de rôle associées aux étendues de base de données s’appliquent uniquement aux utilisateurs qui se connectent à des serveurs dotés de Microsoft Exchange Server 2010 Service Pack 1 (SP1) ou version ultérieure ou d’Exchange 2013. Si un utilisateur auquel est appliquée une attribution de rôle associée à une étendue de base de données se connecte à une version de serveur antérieure à Exchange 2010 SP1, l’attribution de rôle n’est pas appliquée à cet utilisateur et celui-ci ne bénéficiera pas des autorisations octroyées dans le cadre de cette attribution.


Utilisez la syntaxe suivante pour créer une étendue de liste de bases de données.

```powershell
New-ManagementScope -Name <scope name> -DatabaseList <database 1>, <database 2...>
```

Cet exemple crée une étendue qui s'applique uniquement aux bases de données Database 1, Database 2 et Database 3.

```powershell
New-ManagementScope -Name "Primary databases" -DatabaseList "Database 1", "Database 2", "Database 3"
```

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [New-ManagementScope](https://technet.microsoft.com/fr-fr/library/dd335137\(v=exchg.150\)).

## Étendue exclusive

Toute étendue créée à l'aide de la cmdlet **New-ManagementScope** peut être définie comme étendue exclusive. Pour créer une étendue exclusive, vous utilisez les mêmes commandes que celles décrites dans les sections précédentes pour créer une étendue de filtre de destinataire, une étendue de filtre de serveur, une étendue de liste de serveurs, une étendue de filtre de base de données ou une étendue de liste de bases de données, puis vous ajoutez le commutateur *Exclusive* à la commande.

> [!CAUTION]
> Lorsque vous créez des étendues de gestion exclusives, seuls les utilisateurs auxquels ont été affectées des étendues exclusives contenant des objets à modifier peuvent accéder à ces objets. Seuls les administrateurs affectés d'un rôle ayant l'étendue exclusive peuvent accéder à ces objets exclusifs ou protégés.


Cet exemple crée une étendue exclusive basée sur un filtre destinataire qui correspond à tout utilisateur du département Executives.

```powershell
New-ManagementScope "Executive Users Exclusive Scope" -RecipientRestrictionFilter { Department -Eq "Executives" } -Exclusive
```

Par défaut, lorsque vous créez une étendue exclusive, vous devez reconnaître que vous avez créé une étendue exclusive et que vous êtes conscient de l’impact que peut avoir cette étendue exclusive sur des attributions de rôle non exclusives existantes. Si vous souhaitez supprimer l'avertissement, vous pouvez utiliser le commutateur *Force*. Cet exemple crée la même étendue que dans l'exemple précédent, mais sans avertissement.

```powershell
New-ManagementScope "Executive Users Exclusive Scope" -RecipientRestrictionFilter { Department -Eq "Executives" } -Exclusive -Force
```

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [New-ManagementScope](https://technet.microsoft.com/fr-fr/library/dd335137\(v=exchg.150\)).

## Étape 2 : Ajouter ou modifier une attribution de rôle de gestion

Après avoir créé l'étendue, vous devez l'ajouter à une attribution de rôle de gestion nouvelle ou existante.

Si vous créez une étendue de gestion et souhaitez l’ajouter à une nouvelle attribution de rôle de gestion que vous allez créer, consultez les rubriques suivantes :

  - [Gérer des groupes de rôles](manage-role-groups-exchange-2013-help.md)

  - [Ajouter un rôle à un utilisateur ou un groupe de sécurité universel](add-a-role-to-a-user-or-usg-exchange-2013-help.md)

Si vous créez une étendue de rôle de gestion que vous souhaitez ajouter à une attribution de rôle de gestion existante, consultez les rubriques suivantes :

  - [Gérer les stratégies d’attribution des rôles](manage-role-assignment-policies-exchange-2013-help.md)

  - [Modifier une attribution de rôle](change-a-role-assignment-exchange-2013-help.md)

