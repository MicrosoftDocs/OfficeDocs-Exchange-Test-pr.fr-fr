---
title: 'Créer un rôle non délimité: Exchange 2013 Help'
TOCTitle: Créer un rôle non délimité
ms:assetid: 5a042ccf-4d5f-4609-a91b-21c20d1e6459
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dd876886(v=EXCHG.150)
ms:contentKeyID: 50478159
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Créer un rôle non délimité

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2014-06-09_

Un rôle de gestion non délimité peut être utilisé pour fournir aux administrateurs et aux utilisateurs spécialistes l’accès aux scripts Windows PowerShell et aux cmdlets non Exchange. Vous pouvez soit créer un rôle de niveau supérieur non délimité et ajouter des scripts ou des cmdlets non Exchange à ce rôle, ou bien créer un rôle basé sur un rôle de niveau supérieur existant non délimité. Après la création et la personnalisation d’un rôle non délimité, ce dernier peut être attribué à des groupes de rôles de gestion, des utilisateurs et des groupes universels de sécurité (USG). Les rôles non délimités ne peuvent pas être attribués à des stratégies d’attribution de rôle de gestion. Pour plus d’informations sur les rôles non délimités, voir [Présentation des rôles de gestion](understanding-management-roles-exchange-2013-help.md).

> [!CAUTION]
> Les rôles non délimités peuvent être puissants car, comme le sous-entend leur nom, aucune étendue de gestion ne leur est appliquée. Autrement dit, les scripts et les cmdlets non Exchange qu’ils contiennent peuvent être exécutés sur n’importe quel objet de votre organisation Exchange. Pensez à cela lorsque vous ajoutez des scripts ou des cmdlets non Exchange à un rôle non délimité et lorsque vous attribuez le rôle non délimité.


> [!NOTE]
> Si vous souhaitez créer un rôle qui contient des cmdlets Exchange, vous devez créer un rôle basé sur un rôle de gestion existant. Pour plus d'informations sur la création des rôles avec les cmdlets Exchange, consultez <a href="create-a-role-exchange-2013-help.md">Créer un rôle</a>.


Souhaitez-vous rechercher les autres tâches de gestion relatives aux rôles ? Voir [Autorisations avancées](advanced-permissions-exchange-2013-help.md).

## Ce qu’il faut savoir avant de commencer ?

  - Durée d’exécution estimée de chaque procédure : 5 minutes

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l’entrée « Rôles de gestion » dans la rubrique [Autorisations pour la gestion des rôles](role-management-permissions-exchange-2013-help.md).

  - Vous devez utiliser l’environnement de ligne de commande Exchange Management Shell pour effectuer ces procédures.

  - La possibilité de créer des rôles non délimités n’est incluse dans aucun groupe de rôles de gestion par défaut. Vous devez d’abord attribuer un rôle de gestion des rôles non délimités à un utilisateur, à un groupe universel de sécurité ou à un groupe de rôles auquel appartient l’utilisateur pour que celui-ci puisse créer un groupe de rôle. Pour plus d’informations sur l’ajout d’un rôle à un utilisateur, un groupe de sécurité universelle ou un groupe de rôles, voir les rubriques suivantes :
    
      - [Gérer des groupes de rôles](manage-role-groups-exchange-2013-help.md)
    
      - [Ajouter un rôle à un utilisateur ou un groupe de sécurité universel](add-a-role-to-a-user-or-usg-exchange-2013-help.md)

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.


## Que souhaitez-vous faire ?

## Créer un rôle de gestion de niveau supérieur non délimité

Si vous souhaitez mettre à disposition des utilisateurs ou des spécialistes de votre organisation des scripts personnalisés ou des cmdlets non Exchange, vous devez créer un rôle de niveau supérieur non délimité. Les scripts et les cmdlets non Exchange peuvent uniquement être ajoutés à un rôle non délimité créé sous forme de rôle de niveau supérieur, car le rôle non délimité initial n’hérite pas des autres rôles. Le nouveau rôle de niveau supérieur non délimité peut alors être parent d’autres rôles non délimités qui peuvent aussi utiliser les scripts et les cmdlets non Exchange ajoutés.

Voici les étapes à suivre pour créer un rôle de niveau supérieur non délimité :

## Étape 1 : Créer le rôle de niveau supérieur non délimité

Les rôles de niveau supérieur non délimités n’ont pas de rôle parent. Pour créer un rôle sans parent, vous devez spécifier le commutateur *UnscopedTopLevel*. Utilisez la syntaxe suivante pour créer le nouveau rôle.

    New-ManagementRole <name of new role> -UnscopedTopLevel

Cet exemple crée le rôle de niveau supérieur non délimité de scripts informatiques.

    New-ManagementRole "IT Scripts" -UnscopedTopLevel

Après sa création, le rôle est vide jusqu’à ce que vous y ajoutiez des scripts ou des cmdlets non Exchange.

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [New-ManagementRole](https://technet.microsoft.com/fr-fr/library/dd298073\(v=exchg.150\)).

## Étape 2a : Ajouter des entrées de rôle de gestion de script

Si vous voulez ajouter un script au nouveau rôle non délimité, utilisez cette procédure. Si vous voulez ajouter une cmdlet non Exchange à un nouveau rôle non délimité, utilisez la procédure décrite en Step 2b.

Pour ajouter un script Windows PowerShell à un rôle de niveau supérieur non délimité, vous devez ajouter une entrée de rôle de gestion au rôle. L’entrée de rôle contient le nom du script et les paramètres sur le script que vous souhaitez rendre disponibles au rôle.

Le script doit résider dans le répertoire `RemoteScripts` du chemin d’installation Microsoft Exchange Server 2013 sur chaque serveur exécutant Exchange 2013 où les utilisateurs peuvent se connecter pour exécuter le script. Si un utilisateur a accès pour exécuter un script mais que celui-ci ne se trouve pas sur le serveur Exchange 2013 auquel l’utilisateur est connecté, une erreur se produit. Par défaut, le chemin d’accès au répertoire `RemoteScripts` est C:\\Program Files\\Microsoft\\Exchange Server\\V15\\RemoteScripts.

Après que vous ayez copié le script sur les serveurs Exchange 2013 appropriés et décidé quels paramètres de script devraient être utilisés, créez l’entrée de rôle à l’aide de la syntaxe suivante.

    Add-ManagementRoleEntry <unscoped top-level role name>\<script filename> -Parameters <parameter 1, parameter 2, parameter...> -Type Script -UnscopedTopLevel

Cet exemple décrit l’ajout du script BulkProvisionUsers.ps1 au rôle de scripts IT Scripts avec les paramètres *Name* et *Location*.

    Add-ManagementRoleEntry "IT Scripts\BulkProvisionUsers.ps1" -Parameters Name, Location -Type Script -UnscopedTopLevel

> [!NOTE]
> La cmdlet <strong>Add-ManagementRoleEntry</strong> effectue une validation simple pour vous assurer que vous ajoutez uniquement les paramètres qui existent dans le script. Cependant, aucune validation supplémentaire n’est faite après l’ajout de l’entrée de rôle. Si des paramètres sont ultérieurement ajoutés ou supprimés, vous devez manuellement mettre à jour les entrées de rôle qui contiennent le script.


## Étape 2b : Ajouter des entrées de rôle de cmdlet non Exchange

Si vous voulez ajouter une cmdlet non Exchange au nouveau rôle non délimité, utilisez cette procédure. Si vous voulez ajouter un script au nouveau rôle non délimité, utilisez la procédure décrite en Step 2a

Pour ajouter une cmdlet non Exchange à un rôle de niveau supérieur non délimité, vous devez ajouter une entrée de rôle de gestion au rôle. L’entrée de rôle contient le composant logiciel enfichable de la cmdlet, le nom de cmdlet et les paramètres sur la cmdlet que vous souhaitez rendre disponibles au rôle.

Si vous ajoutez des cmdlets non Exchange au nouveau rôle, les cmdlets doivent être installées sur chaque serveur Exchange 2013 où les utilisateurs peuvent se connecter pour exécuter les cmdlets. Pour apprendre à installer et enregistrer correctement les composants logiciels enfichables Windows qui contiennent les cmdlets que vous souhaitez utiliser, reportez-vous à la documentation de votre produit.

Après avoir installé le composant logiciel Windows PowerShell contenant les cmdlets pour les serveurs Exchange 2013 qui conviennent et avoir choisi les paramètres de cmdlet à utiliser, créez l’entrée de rôle utilisant la syntaxe suivante.

    Add-ManagementRoleEntry <unscoped top-level role name>\<cmdlet name> -PSSnapinName <snap-in name> -Parameters <parameter 1, parameter 2, parameter...> -Type Cmdlet -UnscopedTopLevel

Cet exemple vous indique comment ajouter la cmdlet **Set-WidgetConfiguration** dans le composant logiciel enfichable Contoso.Admin.Cmdlets au rôle Widget Cmdlets avec les paramètres *Database* et *Size*.

    Add-ManagementRoleEntry "Widget Cmdlets\Set-WidgetConfiguration" -PSSnapinName Contoso.Admin.Cmdlets -Parameters Database, Size -Type Cmdlet -UnscopedTopLevel

> [!NOTE]
> La cmdlet <strong>Add-ManagementRoleEntry</strong> effectue une validation simple pour vous assurer que vous ajoutez uniquement les paramètres qui existent dans la cmdlet. Cependant, aucune validation supplémentaire n’est faite après l’ajout de l’entrée de rôle. Si la cmdlet est modifiée ultérieurement et que des paramètres sont ajoutés ou supprimés, vous devez manuellement mettre à jour les entrées de rôle qui contiennent la cmdlet.


## Étape 3 : Attribuer le rôle de gestion

L’étape finale lorsque vous créez et configurez un rôle consiste à l’attribuer à un utilisateur.

> [!NOTE]
> Les étendues de gestion ne peuvent pas être configurées sur les attributions de rôles qui affectent un rôle non délimité. Lorsque vous choisissez de créer une attribution de rôle pour un groupe de rôles, un utilisateur ou un groupe de sécurité universel, vous devez choisir l’option pour créer une attribution de rôle sans étendue de gestion.


Vous pouvez attribuer le nouveau rôle à un groupe de rôles, un utilisateur ou à un groupe de sécurité universel. Pour plus d’informations, consultez les rubriques suivantes :

  - [Gérer des groupes de rôles](manage-role-groups-exchange-2013-help.md)

  - [Ajouter un rôle à un utilisateur ou un groupe de sécurité universel](add-a-role-to-a-user-or-usg-exchange-2013-help.md)

## Créer un rôle non délimité basé sur un autre rôle non délimité

S’il existe un rôle de niveau supérieur non délimité existant ou d’autres rôles non délimités sur lesquels vous souhaitez baser de nouveaux rôles non délimités, vous pouvez créer des rôles non délimités enfants. Les rôles enfants du rôle non délimité peuvent contenir un sous-ensemble des scripts et des cmdlets qui existent sur les rôles parents non délimités. Cela s’avère utile, par exemple, si vous souhaitez attribuer uniquement un sous-ensemble des scripts ou des cmdlets disponibles sur un rôle parent non délimité à un administrateur moins expérimenté.

Voici les étapes à suivre pour créer un rôle enfant non délimité :

## Étape 1 : Créer le rôle enfant non délimité

Les nouveaux rôles enfants non délimités peuvent être basés sur des rôles existants non délimités. Lorsque vous créez un rôle, un rôle existant et ses entrées de rôle de gestion sont copiés dans le nouveau rôle. Le rôle existant devient le parent du nouveau rôle enfant. Si vous créez un rôle non délimité basé sur un autre rôle non délimité, vous devez choisir un rôle contenant toutes les cmdlets et tous les paramètres dont vous avez besoin puis supprimer ceux que vous ne voulez pas. Les rôles enfants non délimités ne peuvent pas avoir d’entrées de rôle de gestion qui n’existent pas dans le rôle parent.

> [!NOTE]
> Si vous souhaitez créer un rôle non délimité contenant des scripts ou des cmdlets non Exchange qui n’existent dans aucun autre rôle délimité, créez un rôle de niveau supérieur non délimité. Pour plus d’informations, voir Create an unscoped top-level management role auparavant dans cette rubrique.


Utilisez la syntaxe suivante pour créer le nouveau rôle.

    New-ManagementRole -Parent <existing unscoped role to copy> -Name <name of new unscoped role>

Cet exemple copie le rôle Scripts informatiques globaux et ses entrées de rôle de gestion dans le rôle Scripts informatiques diagnostics.

    New-ManagementRole -Parent "IT Global Scripts" -Name "Diagnostic IT Scripts"

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [New-ManagementRole](https://technet.microsoft.com/fr-fr/library/dd298073\(v=exchg.150\)).

## Étape 2 : Modifier les entrées de rôle de gestion du rôle

Après avoir créé votre rôle, vous devez modifier les entrées de rôle. Vous pouvez supprimer l’intégralité d’une entrée de rôle, qui supprime entièrement l’accès au script ou à la cmdlet non Exchange associé. Ou vous pouvez supprimer les paramètres d’une entrée de rôle pour supprimer l’accès aux paramètres spécifiques du script ou de la cmdlet non Exchange associé.

Il est impossible d’ajouter des entrées de rôle ou des paramètres sur des entrées de rôle sauf s’ils existent dans le rôle parent. Puisque vous venez de créer un rôle à partir d’un rôle parent à l’étape 1, vous ne pouvez pas ajouter des paramètres ou des entrées de rôles supplémentaires sur les entrées de rôles car elles n’existent pas dans le rôle parent.

Lorsque vous modifiez une entrée sur un rôle, vous pouvez effectuer l’une des actions suivantes :

  - Supprimer une entrée de rôle entière et unique.

  - Supprimer des entrées de rôles entières multiples.

  - Supprimer des paramètres d’une entrée de rôle.

Pour supprimer des entrées de rôles de votre nouveau rôle, voir [Supprimer une entrée de rôle d'un rôle](remove-a-role-entry-from-a-role-exchange-2013-help.md).

## Étape 3 : Attribuer le rôle de gestion

L’étape finale lorsque vous créez et configurez un rôle consiste à l’attribuer à un utilisateur.

> [!NOTE]
> Les étendues de gestion ne peuvent pas être configurées sur les attributions de rôles qui affectent un rôle non délimité. Lorsque vous choisissez de créer une attribution de rôle pour un groupe de rôles, un utilisateur ou un groupe de sécurité universel, vous devez choisir l’option pour créer une attribution de rôle sans étendue de gestion.


Vous pouvez attribuer le nouveau rôle à un groupe de rôles, un utilisateur ou à un groupe de sécurité universel. Pour plus d’informations, consultez les rubriques suivantes :

  - [Gérer des groupes de rôles](manage-role-groups-exchange-2013-help.md)

  - [Ajouter un rôle à un utilisateur ou un groupe de sécurité universel](add-a-role-to-a-user-or-usg-exchange-2013-help.md)

