---
title: 'Afficher les autorisations effectives: Exchange 2013 Help'
TOCTitle: Afficher les autorisations effectives
ms:assetid: ae6cb7cf-f998-44a6-a69a-02ad736c8260
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dd638167(v=EXCHG.150)
ms:contentKeyID: 50478867
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Afficher les autorisations effectives

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2012-10-09_

Dans Microsoft Exchange Server 2013, les autorisations sont accordées à l'aide de rôles de gestion attribués à des groupes de rôles de gestion, des stratégies d'attribution de rôle de gestion, des groupes de sécurité universels ou directement aux utilisateurs. Les utilisateurs reçoivent les autorisations s'ils sont membres des groupes de rôles ou des groupes de sécurité universels ou si des stratégies d'attribution de rôle leur sont attribuées.

La plupart des autorisations sont accordées en fonction de l'appartenance à un groupe de rôles ou de l'attribution des stratégies d'affectation aux utilisateurs finaux. Bien que l'utilisation de groupes de rôles et de stratégies d'affectation facilite l'octroi des autorisations à un grand nombre d'utilisateurs, vous ne savez pas nécessairement quels utilisateurs sont membres d'un groupe de rôles, ni quels utilisateurs disposent d'une stratégie d'affectation. C'est pourquoi le commutateur *GetEffectiveUsers* de la cmdlet **Get-ManagementRoleAssignment** est utile. Il indique quels utilisateurs ont reçu les autorisations accordées par un rôle de gestion via les groupes de rôles, les stratégies d'affectation et les groupes de sécurité universels qui leur ont été attribués.

Le commutateur *GetEffectiveUsers* est utilisé avec la cmdlet **Get-ManagementRoleAssignment** lorsque le paramètre *Role* est utilisé. En indiquant ce commutateur avec un rôle spécifique, la cmdlet **Get-ManagementRoleAssignment** examine tous les utilisateurs affectés au rôle, comme les groupes de rôles, les stratégies d'affectation et les groupes universels de sécurité, et répertorie les membres de chacun.

> [!NOTE]
> Le commutateur <em>GetEffectiveUser</em> ne répertorie pas les utilisateurs membres d'un groupe de rôles étranger lié. Si un groupe de rôles lié est trouvé, <strong>Tous les membres du groupe lié</strong> s'affichent à la place de la liste des utilisateurs. Pour plus d'informations sur les autorisations couvrant plusieurs forêts, voir <a href="understanding-multiple-forest-permissions-exchange-2013-help.md">Présentation des autorisations sur plusieurs forêts</a>.


Pour plus d'informations sur les rôles de gestion, les groupes de rôles et stratégies d'affectation, voir [Présentation du contrôle d'accès basé sur un rôle](understanding-role-based-access-control-exchange-2013-help.md). Pour plus d'informations sur les attributions des rôles de gestion, voir [Présentation des attributions de rôles de gestion](understanding-management-role-assignments-exchange-2013-help.md).

Souhaitez-vous rechercher les autres tâches de gestion relatives à la gestion des autorisations ? Consultez la rubrique [Autorisations](permissions-exchange-2013-help.md).

## Ce qu’il faut savoir avant de commencer ?

  - Durée d’exécution estimée de chaque procédure : 5 minutes

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultezEntrée « Groupes de rôles » ou « Stratégie d'attribution de rôle » dans la rubrique [Autorisations pour la gestion des rôles](role-management-permissions-exchange-2013-help.md).

  - Les procédures décrites dans cette rubrique ne peuvent être effectuées dans l'environnement de ligne de commande Exchange Management Shell. Vous ne pouvez pas utiliser le Centre d'administration Exchange (CAE) pour afficher des autorisations effectives.

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.


## Utiliser l'environnement de ligne de commande Exchange Management Shell pour répertorier tous les utilisateurs

Pour dresser la liste de tous les utilisateurs qui bénéficient des autorisations fournies par un rôle de gestion, utilisez la syntaxe suivante.

```powershell
Get-ManagementRoleAssignment -Role <role name> -GetEffectiveUsers
```

Cet exemple répertorie tous les utilisateurs qui bénéficient des autorisations fournies par le rôle Mail Recipients.

```powershell
Get-ManagementRoleAssignment -Role "Mail Recipients" -GetEffectiveUsers
```

Pour modifier les propriétés qui sont renvoyées dans la liste ou pour exporter la liste dans un fichier de valeurs séparées par une virgule (.csv), voir Utiliser l'environnement de ligne de commande Exchange Management Shell pour personnaliser la sortie et l'afficher plus loin dans cette rubrique.

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Get-ManagementRoleAssignment](https://technet.microsoft.com/fr-fr/library/dd351024\(v=exchg.150\)).

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour rechercher un utilisateur spécifique sur un rôle

Pour trouver un utilisateur spécifique ayant reçu les autorisations fournies par un rôle de gestion, vous devez utiliser la cmdlet **Get-ManagementRoleAssignment** pour extraire la liste de tous les utilisateurs effectifs, puis transférer la sortie à la cmdlet **Where**. La cmdlet **Where** filtre la sortie et retourne uniquement l'utilisateur spécifié. Utilisez la syntaxe suivante.

    Get-ManagementRoleAssignment -Role <role name> -GetEffectiveUsers | Where { $_.EffectiveUserName -Eq "<name of user>" }

Cet exemple recherche l'utilisateur David Strome sur le rôle Journaling.

    Get-ManagementRoleAssignment -Role Journaling -GetEffectiveUsers | Where { $_.EffectiveUserName -Eq "David Strome" }

Pour modifier les propriétés qui sont renvoyées dans la liste ou exporter cette dernière dans un fichier .csv, voir Utiliser l'environnement de ligne de commande Exchange Management Shell pour personnaliser la sortie et l'afficher ultérieurement dans cette rubrique.

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Get-ManagementRoleAssignment](https://technet.microsoft.com/fr-fr/library/dd351024\(v=exchg.150\)).

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour rechercher un utilisateur spécifique sur tous les rôles

Pour connaître tous les rôles par lesquels un utilisateur reçoit des autorisations, vous devez utiliser la cmdlet **Get-ManagementRoleAssignment** pour extraire tous les utilisateurs effectifs sur tous les rôles de gestion, puis transférer la sortie à la cmdlet **Where**. La cmdlet **Where** filtre la sortie et retourne uniquement les attributions de rôle qui accordent les autorisations aux utilisateurs.

    Get-ManagementRoleAssignment -GetEffectiveUsers | Where { $_.EffectiveUserName -Eq "<name of user>" }

Cet exemple recherche toutes les attributions de rôle qui accordent des autorisations à l'utilisateur Kim Akers.

```powershell
Get-ManagementRoleAssignment -GetEffectiveUsers | Where {     Get-ManagementRoleAssignment -GetEffectiveUsers | Where { $_.EffectiveUserName -Eq "Kim Akers" }.EffectiveUserName -Eq "Kim Akers" }
```

Si vous souhaitez modifier les propriétés qui sont renvoyées dans la liste ou l’exporter dans un fichier CSV, voir Utiliser l'environnement de ligne de commande Exchange Management Shell pour personnaliser la sortie et l'afficher ultérieurement dans cette rubrique.

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Get-ManagementRoleAssignment](https://technet.microsoft.com/fr-fr/library/dd351024\(v=exchg.150\)).

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour personnaliser la sortie et l'afficher

Il se peut que la sortie par défaut de la cmdlet **Get-ManagementRoleAssignment** ne contiennent pas les informations qui vous intéressent. La sortie de la cmdlet contient beaucoup plus de propriétés auxquelles vous pouvez accéder. Voici quelques-unes des propriétés qui pourraient être utiles :

  - **EffectiveUserName**   Nom de l'utilisateur.

  - **Role**   Rôle qui accorde les autorisations.

  - **RoleAssigneeName**   Groupe de rôles, stratégie d'affectation ou groupe universel de sécurité attribué au rôle et contenant l'utilisateur dans la propriété `EffectiveUserName`.

  - **RoleAssigneeType**   Indique si l'attribution de rôle concerne un groupe de rôles, une stratégie d'affectation, un groupe universel de sécurité ou un utilisateur.

  - **AssignmentMethod**   Indique si l'attribution entre le rôle et l'utilisateur concerné est directe ou indirecte.

  - **CustomRecipientWriteScope**   Indique l'étendue d'écriture du destinataire personnalisée, le cas échéant, appliquée à l'attribution du rôle au moment de sa création. La portée spécifiée dans cette propriété remplace la portée d'écriture de destinataire implicite spécifiée dans la propriété `RecipientWriteScope`.

  - **CustomConfigWriteScope**   Indique l'étendue d'écriture de configuration personnalisée, le cas échéant, appliquée à l'attribution du rôle au moment de sa création. La portée spécifiée dans cette propriété remplace la portée d'écriture de configuration implicite spécifiée dans la propriété `ConfigWriteScope`.

  - **RecipientReadScope**   Indique l'étendue de lecture de destinataire implicite appliquée au rôle.

  - **RecipientWriteScope**   Indique l'étendue d'écriture de destinataire implicite appliquée au rôle.

  - **ConfigReadScope**   Indique l'étendue de lecture de configuration implicite appliquée au rôle.

  - **ConfigWriteScope**   Indique l'étendue d'écriture de configuration implicite appliquée au rôle.

Pour sélectionner les propriétés que vous voulez afficher dans votre liste, vous utilisez des commandes similaires à celles utilisées dans les sections Utiliser l'environnement de ligne de commande Exchange Management Shell pour répertorier tous les utilisateurs, Utiliser l'environnement de ligne de commande Exchange Management Shell pour rechercher un utilisateur spécifique sur un rôle et Utiliser l'environnement de ligne de commande Exchange Management Shell pour rechercher un utilisateur spécifique sur tous les rôles. La différence réside dans le fait que vous transmettez les résultats de ces commandes aux cmdlets **Format-Table** ou **Select-Object**. La cmdlet **Format-Table** est utile pour afficher la liste des résultats à l'écran. La cmdlet **Select-Object** permet d'afficher la liste des résultats dans un fichier .csv.

Ces deux cmdlets vous permettent de spécifier les propriétés qui vous intéressent ainsi que leur ordre d'affichage. La cmdlet **Format-Table** offre davantage d'options lorsque vous affichez les résultats à l'écran, alors que la cmdlet **Select-Object** ne modifie la sortie en aucun cas, ce qui est utile lorsque vous exportez la liste dans un fichier .csv.

Pour plus d'informations sur les cmdlets **Format-Table** et**Select-Object**, voir [Utilisation de la sortie de la commande](working-with-command-output-exchange-2013-help.md).

## Afficher une liste personnalisée à l'écran

1.  Sélectionnez les informations que vous souhaitez voir et recherchez la commande associée à partir de l’une des procédures suivantes :
    
      - Utiliser l'environnement de ligne de commande Exchange Management Shell pour répertorier tous les utilisateurs
    
      - Utiliser l'environnement de ligne de commande Exchange Management Shell pour rechercher un utilisateur spécifique sur un rôle
    
      - Utiliser l'environnement de ligne de commande Exchange Management Shell pour rechercher un utilisateur spécifique sur tous les rôles

2.  Sélectionnez les propriétés que vous souhaitez voir dans votre liste.

3.  Utilisez la syntaxe suivante pour afficher la liste.
    
        <command to retrieve list > | Format-Table <property 1>, <property 2>, <property ...>

Cet exemple recherche l’utilisateur Michel Cordani sur tous les rôles et affiche les propriétés `EffectiveUserName`, `Role`, `CustomRecipientWriteScope` et `CustomConfigWriteScope`.

    Get-ManagementRoleAssignment -GetEffectiveUsers | Where { $_.EffectiveUserName -Eq "David Strome" } | Format-Table EffectiveUserName, Role, CustomRecipientWriteScope, CustomConfigWriteScope

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Get-ManagementRoleAssignment](https://technet.microsoft.com/fr-fr/library/dd351024\(v=exchg.150\)).

## Afficher une liste personnalisée dans un fichier .csv

Pour exporter la liste au format .csv, vous devez transmettre les résultats de la commande **Get-ManagementRoleAssignment** issus de la procédure appropriée décrite précédemment à la cmdlet **Select-Object**. La sortie de la cmdlet **Select-Object** est ensuite transmise à la cmdlet **Export-CSV** qui enregistre le fichier .csv résultant sous le nom de fichier que vous indiquez.

1.  Sélectionnez les informations que vous souhaitez voir et recherchez la commande associée à partir de l’une des procédures suivantes :
    
      - Utiliser l'environnement de ligne de commande Exchange Management Shell pour répertorier tous les utilisateurs
    
      - Utiliser l'environnement de ligne de commande Exchange Management Shell pour rechercher un utilisateur spécifique sur un rôle
    
      - Utiliser l'environnement de ligne de commande Exchange Management Shell pour rechercher un utilisateur spécifique sur tous les rôles

2.  Sélectionnez les propriétés que vous souhaitez voir dans votre liste.

3.  Utilisez la syntaxe suivante pour exporter la liste dans un fichier .csv.
    
        <command to retrieve list > | Select-Object <property 1>, <property 2>, <property ...> | Export-CSV <filename>

Cet exemple recherche l’utilisateur Michel Cordani sur tous les rôles et affiche les propriétés `EffectiveUserName`, `Role`, `CustomRecipientWriteScope` et `CustomConfigWriteScope`.

    Get-ManagementRoleAssignment -GetEffectiveUsers | Where { $_.EffectiveUserName -Eq "David Strome" } | Select-Object EffectiveUserName, Role, CustomRecipientWriteScope, CustomConfigWriteScope | Export-CSV c:\output.csv

Vous pouvez maintenant visualiser le fichier .csv dans la visionneuse de votre choix.

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Get-ManagementRoleAssignment](https://technet.microsoft.com/fr-fr/library/dd351024\(v=exchg.150\)).

