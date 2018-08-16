---
title: 'Modifier une entrée sur un rôle supérieur non délimité: Exchange 2013 Help'
TOCTitle: Modifier une entrée de rôle sur un rôle de niveau supérieur non délimité
ms:assetid: 65c0bfb3-aafd-4c64-8429-7616c57adf1c
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dd876896(v=EXCHG.150)
ms:contentKeyID: 50478308
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Modifier une entrée de rôle sur un rôle de niveau supérieur non délimité

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2012-10-03_

Les entrées de rôle de gestion sur des rôles de haut niveau non délimités font référence aux scripts et cmdlets non-Exchange, ainsi qu’à leurs paramètres, que vous voulez rendre accessibles à ceux auxquels le rôle est attribué. En modifiant les paramètres disponibles sur une entrée de rôle, vous gérez ce que ceux auxquels le rôle est attribué peuvent faire avec le script ou la cmdlet non-Exchange. Pour plus d’informations sur les entrées des rôles non délimitées, voir [Présentation des rôles de gestion](understanding-management-roles-exchange-2013-help.md).

> [!NOTE]
> Si vous souhaitez modifier une entrée de rôle sur un rôle de gestion qui contient les cmdlets Exchange, voir <a href="change-a-role-entry-exchange-2013-help.md">Modifier une entrée de rôle</a>.


Souhaitez-vous rechercher les autres tâches de gestion relatives aux rôles ? Consultez la rubrique [Autorisations avancées](advanced-permissions-exchange-2013-help.md).

## Ce qu’il faut savoir avant de commencer ?

  - Durée d’exécution estimée de chaque procédure : 5 minutes

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l’entrée « Rôles de gestion » dans la rubrique [Autorisations pour la gestion des rôles](role-management-permissions-exchange-2013-help.md).

  - Vous devez utiliser l’environnement de ligne de commande Exchange Management Shell pour effectuer ces procédures.

  - La modification d’une entrée de rôle sur un rôle de haut niveau non délimité n’est inclus dans aucun groupe de rôles de gestion par défaut. Vous devez d’abord attribuer un rôle de gestion des rôles non délimités à un utilisateur, à un groupe de sécurité universel ou à un groupe de rôles auquel appartient l’utilisateur pour que celui-ci puisse ajouter ou modifier une entrée de rôle de haut niveau non délimité. Pour plus d’informations sur l’ajout d’un rôle à un utilisateur, un groupe de sécurité universelle ou un groupe de rôles, voir les rubriques suivantes :
    
      - [Gérer des groupes de rôles](manage-role-groups-exchange-2013-help.md)
    
      - [Ajouter un rôle à un utilisateur ou un groupe de sécurité universel](add-a-role-to-a-user-or-usg-exchange-2013-help.md)

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.


## Que souhaitez-vous faire ?

## Utiliser l’environnement de ligne de commande Exchange Management Shell pour ajouter un ou plusieurs paramètres à une entrée de rôle

Pour ajouter des paramètres à une entrée de rôle de haut niveau non délimité, vous devez procéder de la façon suivante :

  - Spécifiez les paramètres que vous souhaitez ajouter à l’aide du paramètre *Parameters*.

  - Spécifiez le paramètre *AddParameter* pour indiquer que vous souhaitez effectuer une opération d’ajout.

  - Spécifiez le paramètre *UnscopedTopLevel* pour indiquer que vous modifiez une entrée de rôle sur un rôle de haut niveau non délimité. Si vous ne spécifiez pas ce paramètre lorsque vous modifiez une entrée de rôle sur un rôle non délimité, une erreur se produit.

Pour ajouter des paramètres à une entrée de rôle, utilisez la syntaxe suivante.

    Set-ManagementRoleEntry <role name>\<script or non-Exchange cmdlet> -Parameters <parameter 1>, <parameter 2>, <parameter...> -AddParameter -UnscopedTopLevel

Cet exemple montre comment ajouter les paramètres *EmailAddress* et *City* au script **CreateUsers.ps1** sur le rôle non délimité Administrateurs des destinataires.

    Set-ManagementRoleEntry "Recipient Administrators\CreateUsers.ps1" -Parameters EmailAddress, City -AddParameter -UnscopedTopLevel

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Set-ManagementRoleEntry](https://technet.microsoft.com/fr-fr/library/dd351162\(v=exchg.150\)).

## Utiliser l’environnement de ligne de commande Exchange Management Shell pour supprimer un ou plusieurs paramètres d’une entrée de rôle

Pour supprimer des paramètres d’une entrée de rôle, vous devez procéder de la façon suivante :

  - Spécifiez les paramètres que vous souhaitez supprimer à l’aide du paramètre *Parameters*.

  - Spécifiez le paramètre *RemoveParameter* pour indiquer que vous souhaitez effectuer une opération de suppression.

  - Spécifiez le paramètre *UnscopedTopLevel* pour indiquer que vous modifiez une entrée de rôle sur un rôle de haut niveau non délimité. Si vous ne spécifiez pas ce paramètre lorsque vous modifiez une entrée de rôle sur un rôle non délimité, une erreur se produit.

> [!CAUTION]
> Vous ne pouvez pas annuler la suppression de ces opérations. Si vous supprimez par erreur un paramètre d’une entrée de rôle, vous devez l’ajouter à nouveau manuellement.


Pour supprimer des paramètres d’une entrée de rôle, utilisez la syntaxe suivante.

    Set-ManagementRoleEntry <role name>\<script or non-Exchange cmdlet> -Parameters <parameter 1>, <parameter 2>, <parameter...> -RemoveParameter -UnscopedTopLevel

Cet exemple montre comment supprimer les paramètres *Delay*, *Force* et *Credential* de la cmdlet **Start-Widget** non-Exchange sur le rôle Administrateurs de serveurs de niveau 1.

    Set-ManagementRoleEntry "Tier 1 Server Administrators\Start-Widget" -Parameters Delay, Force, Credential -RemoveParameter -UnscopedTopLevel

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Set-ManagementRoleEntry](https://technet.microsoft.com/fr-fr/library/dd351162\(v=exchg.150\)).

## Utiliser l’environnement de ligne de commande Exchange Management Shell pour supprimer tous les paramètres d’une entrée de rôle

Pour supprimer tous les paramètres d’une entrée de rôle, vous devez procéder de la façon suivante :

  - Spécifiez la valeur `$Null` sur le paramètre *Parameters*. Vous n’avez pas à utiliser le paramètre *RemoveParameter*.

  - Spécifiez le paramètre *UnscopedTopLevel* pour indiquer que vous modifiez une entrée de rôle sur un rôle de haut niveau non délimité. Si vous ne spécifiez pas ce paramètre lorsque vous modifiez une entrée de rôle sur un rôle non délimité, une erreur se produit.

La suppression de tous les paramètres d’une entrée de rôle est particulièrement utile lorsque vous voulez que quelques paramètres seulement soient disponibles sur un script ou une cmdlet non-Exchange et que vous souhaitez exclure tous les autres paramètres.

Si vous ne voulez pas qu’un rôle ait accès à un script ou à une cmdlet non-Exchange, supprimez complètement du rôle l’entrée de rôle associée au lieu de supprimer simplement les paramètres. Pour plus d’informations sur la suppression d’une entrée de rôle, voir [Supprimer une entrée de rôle d'un rôle](remove-a-role-entry-from-a-role-exchange-2013-help.md).

> [!CAUTION]
> Vous ne pouvez pas annuler la suppression de ces opérations. Si vous supprimez par erreur tous les paramètres d’une entrée de rôle, vous devez les ajouter à nouveau manuellement.


Pour supprimer des paramètres d’une entrée de rôle, utilisez la syntaxe suivante.

    Set-ManagementRoleEntry <role name>\<script or non-Exchange cmdlet> -Parameters $Null -UnscopedTopLevel

Cet exemple montre comment supprimer tous les paramètres du script FindMailboxesOverQuota.ps1 sur le rôle Administrateurs des destinataires.

    Set-ManagementRoleEntry "Recipient Administrators\FindMailboxesOverQuota.ps1" -Parameters $Null -UnscopedTopLevel

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Set-ManagementRoleEntry](https://technet.microsoft.com/fr-fr/library/dd351162\(v=exchg.150\)).

## Utiliser l’environnement de ligne de commande Exchange Management Shell pour appliquer un ensemble spécifique de paramètres

Si vous ne souhaitez inclure qu’un ensemble spécifique de paramètres dans une entrée de rôle, vous devez procéder de la façon suivante :

  - Spécifiez uniquement le paramètre *Parameters*. N’incluez pas les paramètres *AddParameter* ou *RemoveParameter*.

  - Spécifiez le paramètre *UnscopedTopLevel* pour indiquer que vous modifiez une entrée de rôle sur un rôle non délimité. Si vous ne spécifiez pas ce paramètre lorsque vous modifiez une entrée de rôle sur un rôle de haut niveau non délimité, une erreur se produit.

> [!CAUTION]
> Lorsque vous spécifiez uniquement le paramètre _Parameters_, uniquement les paramètres que vous spécifiez dans la commande sont inclus sur l’entrée de rôle. Tous les autres paramètres sont supprimés.


Pour spécifier un ensemble spécifique de paramètres, utilisez la syntaxe suivante.

    Set-ManagementRoleEntry <role name>\<script or non-Exchange cmdlet> -Parameters <parameter 1>, <parameter 2>, <parameter...> -UnscopedTopLevel

Cet exemple montre comment inclure uniquement les paramètres *Alias*, *DisplayName*, *WidgetConfig* et *Enabled* sur la cmdlet **Set-Widget** sur le rôle Administrateurs de destinataires de messages de Seattle.

    Set-ManagementRoleEntry "Seattle Mail Recipient Admins\Set-UMMailbox" -Parameters Alias, DisplayName, WidgetConfig, Enabled -UnscopedTopLevel

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Set-ManagementRoleEntry](https://technet.microsoft.com/fr-fr/library/dd351162\(v=exchg.150\)).

## Autres tâches

Après avoir modifié une entrée de rôle sur un rôle de haut niveau non délimité, vous souhaiterez probablement :

[Ajouter une entrée de rôle à un rôle](add-a-role-entry-to-a-role-exchange-2013-help.md)

[Gérer des groupes de rôles](manage-role-groups-exchange-2013-help.md)

[Gérer les membres de groupes de rôles](manage-role-group-members-exchange-2013-help.md)

[Ajouter un rôle à un utilisateur ou un groupe de sécurité universel](add-a-role-to-a-user-or-usg-exchange-2013-help.md)

[Supprimer un rôle d’un utilisateur ou un groupe universel de sécurité](remove-a-role-from-a-user-or-usg-exchange-2013-help.md)

