﻿---
title: 'Rôle MyRetentionPolicies: Exchange 2013 Help'
TOCTitle: Rôle MyRetentionPolicies
ms:assetid: 65f49d19-cfb5-4142-8359-8368d5c48085
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dd876897(v=EXCHG.150)
ms:contentKeyID: 50478314
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Rôle MyRetentionPolicies

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2015-03-09_

Le rôle de gestion `MyRetentionPolicies` permet à chaque utilisateur d’afficher ses balises de rétention et d’afficher et de modifier les paramètres et valeurs par défaut de ces balises.

Ce rôle de gestion est l’un des rôles intégrés dans le modèle des autorisations de contrôle d’accès en fonction du rôle (RBAC) dans Microsoft Exchange Server 2013. Les rôles de gestion, qui sont attribués à un ou plusieurs groupes de rôles de gestion, stratégies d’attribution de rôle de gestion, utilisateurs ou groupes de sécurité universels, agissent en tant que regroupement logique de cmdlets ou de scripts qui sont associés pour fournir un accès afin d’afficher ou de modifier la configuration des composants Exchange 2013, tels que des bases de données de boîtes aux lettres, des règles de transport et des destinataires. Si une cmdlet ou un script et ses paramètres, appelés « entrée de rôle de gestion », sont inclus dans un rôle, cette cmdlet ou ce script et ses paramètres peuvent être exécutés par les utilisateurs qui ont attribué le rôle. Pour plus d’informations sur les rôles de gestion et les entrées de rôles de gestion, consultez la rubrique [Présentation des rôles de gestion](understanding-management-roles-exchange-2013-help.md).

Pour plus d’informations sur les rôles de gestion, les groupes de rôles de gestion et les autres composants de contrôle d’accès basé sur un rôle, voir [Présentation du contrôle d'accès basé sur un rôle](understanding-role-based-access-control-exchange-2013-help.md).

## Gestion des attributions de rôles

Pour que ce rôle puisse accorder des autorisations, il doit être attribué à un utilisateur de rôle, telle qu’une stratégie d’attribution de rôle. Cette affectation s’effectue à l’aide des attributions de rôles de gestion. Les attributions de rôles lient les personnes affectées au rôle aux rôles. Si plusieurs rôles sont attribués à une personne affectée au rôle, celle-ci bénéficie de l’association de toutes les autorisations accordées par tous les rôles attribués.

> [!NOTE]
> Vous pouvez aussi attribuer ce rôle de gestion à un groupe de rôles, un groupe de sécurité universelle ou directement à un utilisateur. Toutefois, les rôles centrés sur l’utilisateur sont plus efficaces lors d’une utilisation avec des stratégies d’attribution de rôle.


Ce rôle centré sur l’utilisateur a des étendues implicites qui ne peuvent pas être modifiées. Par conséquent, vous ne devez pas ajouter d’étendues personnalisées à des attributions de rôle qui affectent ce rôle à des stratégies d’attribution de rôles, des groupes de rôles, des groupes de sécurité universelle ou des utilisateurs.

Pour plus d’informations sur les attributions de rôle et les étendues, consultez les rubriques suivantes :

  - [Présentation des attributions de rôles de gestion](understanding-management-role-assignments-exchange-2013-help.md)

  - [Présentation des portées du rôle de gestion](understanding-management-role-scopes-exchange-2013-help.md)

Ce rôle peut être attribué à une ou plusieurs stratégies d’attribution de rôles par défaut. Pour plus d’informations, consultez la section « Attributions de rôles de gestion par défaut ».

Si vous souhaitez afficher une liste de groupes de rôles, d’utilisateurs ou de groupes de sécurité universels attribués à ce rôle, utilisez la commande suivante.

    Get-ManagementRoleAssignment -Role "<role name>"

## Attributions de rôles normales et de délégation

Ce rôle peut être attribué aux personnes affectées au rôle à l’aide d’attributions de rôles normales ou de délégation. Les attributions de rôles normales accordent des autorisations fournies par le rôle à la personne affectée au rôle. Les attributions de rôle de délégation accordent à la personne affectée au rôle la possibilité d’affecter le rôle aux autres personnes affectées au rôle. Pour plus d’information sur les attributions de rôle normales et la délégation d’attributions de rôle de gestion, consultez la rubrique Présentation des attributions de rôles de gestion[Présentation des attributions de rôles de gestion](understanding-management-role-assignments-exchange-2013-help.md).

## Ajout ou suppression des attributions de rôles

Vous pouvez attribuer ce rôle à une autre personne. En attribuant ce rôle à une autre personne, vous modifiez ses autorisations en les accordant au nouvel utilisateur. Vous pouvez affecter ce rôle à d’autres stratégies d’attribution de rôles intégrées ou vous pouvez créer des stratégies d’attribution de rôles et leur attribuer ce rôle.

Pour attribuer ce rôle à d’autres personnes, il doit être attribué à un groupe de rôles, dont vous faites partie, directement à vous ou à un groupe de sécurité universel dont vous êtes membre, en utilisant une attribution de rôle de délégation. Pour plus d’informations sur les attributions de rôle de délégation, consultez la section « Attributions de rôles normales et de délégation ».

Vous pouvez également supprimer ce rôle de la stratégie d’attribution de rôle par défaut, des stratégies d’attribution de rôle et des groupes de rôles que vous créez, des utilisateurs et des groupes de sécurité universels. Cependant, il doit toujours y avoir au moins une attribution de rôle de délégation entre ce rôle et un groupe de rôles ou un groupe de sécurité universel. Vous ne pouvez pas supprimer la dernière attribution de rôle de délégation.

Pour plus d’informations sur la manière d’ajouter ou de supprimer des attributions entre ce rôle et les groupes de rôles, les utilisateurs et les groupes de sécurité universels, consultez les rubriques suivantes :

  - Section « Ajouter ou supprimer un rôle dans un groupe de rôles » dans [Gérer des groupes de rôles](manage-role-groups-exchange-2013-help.md)

  - [Ajouter un rôle à un utilisateur ou un groupe de sécurité universel](add-a-role-to-a-user-or-usg-exchange-2013-help.md)

  - [Supprimer un rôle d’un utilisateur ou un groupe universel de sécurité](remove-a-role-from-a-user-or-usg-exchange-2013-help.md)

## Activation ou désactivation des attributions de rôles

En activant ou en désactivant une attribution de rôle, vous contrôlez si cette attribution est effective ou non. Si une attribution de rôle est désactivée, les autorisations accordées par le rôle associé ne sont pas appliquées à la personne affectée au rôle. C’est commode si vous souhaitez temporairement supprimer des autorisations sans supprimer une attribution de rôle. Pour plus d’informations, consultez la rubrique Modifier une attribution de rôle[Modifier une attribution de rôle](change-a-role-assignment-exchange-2013-help.md).

## Gestion par défaut des attributions de rôles

Ce rôle a des attributions de rôle pour une ou plusieurs personnes affectées au rôle. Le tableau suivant indique si l’attribution de rôle est normale ou déléguée. Il indique également les étendues de gestion appliquées à chaque attribution. La liste suivante décrit chaque colonne :

  - **Attribution normale**   Les attributions de rôle normales permettent à la personne affectée au rôle d’accéder aux autorisations fournies par les entrées de rôle de gestion pour ce dernier.

  - **Attribution de délégation**   Les attributions de rôle de délégation donnent à la personne affectée au rôle la possibilité de l’attribuer aux groupes de rôle, aux utilisateurs ou aux groupes de sécurité universels.

  - **Étendue de lecture du destinataire**   L’étendue de lecture du destinataire détermine les objets destinataire que la personne affectée au rôle est autorisée à lire à partir de Active Directory.

  - **Étendue d’écriture du destinataire**   L’étendue d’écriture du destinataire détermine les objets destinataire que la personne affectée au rôle est autorisée à modifier dans Active Directory.

  - **Étendue de lecture de configuration**   L’étendue de lecture de configuration détermine les objets serveur et de configuration que la personne affectée au rôle est autorisée à lire à partir de Active Directory.

  - **Étendue d’écriture de configuration**   L’étendue d’écriture de configuration détermine les objets serveur et d’organisation que la personne affectée au rôle est autorisée à modifier dans Active Directory.

### Attributions de rôles de gestion par défaut pour ce rôle

<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>Groupe de rôles ou stratégie d’attribution</th>
<th>Attribution normale</th>
<th>Délégation d’une attribution</th>
<th>Étendue de lecture du destinataire</th>
<th>Étendue d’écriture du destinataire</th>
<th>Étendue de lecture de configuration</th>
<th>Configuration de l’étendue d’écriture</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
</tbody>
</table>


## Gestion de la personnalisation des rôles

Ce rôle a été configuré pour fournir à une personne affectée au rôle toutes les cmdlets nécessaires, ainsi que les paramètres, pour gérer les fonctionnalités et les composants répertoriés au début de cette rubrique. D’autres rôles ont également été fournis pour activer la gestion d’autres fonctionnalités. En ajoutant et en supprimant des rôles dans des groupes de rôles, vous pouvez créer un modèle d’autorisations personnalisé sans personnaliser des rôles de gestion individuels. Pour obtenir une liste complète de rôles, consultez la rubrique [Rôles de gestion intégrés](built-in-management-roles-exchange-2013-help.md). Pour plus d’informations sur la personnalisation des groupes de rôles, consultez la rubrique [Gérer des groupes de rôles](manage-role-groups-exchange-2013-help.md).

Si vous décidez que vous avez besoin de créer une version personnalisée de ce rôle, vous devez créer un rôle enfant et personnaliser le nouveau rôle.

> [!CAUTION]
> Les informations suivantes vous permettent d’effectuer la gestion avancée d’autorisations. La personnalisation des rôles de gestion peut augmenter considérablement la complexité de votre modèle d’autorisations. Vous risquez d’interrompre le fonctionnement de certaines fonctions si vous remplacez le rôle de gestion intégré par un rôle personnalisé et configuré de manière incorrecte.


Les étapes suivantes sont celles les plus courantes pour créer un rôle personnalisé et l’attribuer à une personne affectée au rôle :

1.  Créez une copie de ce rôle. Pour plus d’informations, consultez la rubrique [Créer un rôle](create-a-role-exchange-2013-help.md).

2.  Modifiez ou supprimez les entrées de rôle sur le nouveau rôle à l’aide des cmdlets **Set-ManagementRoleEntry** et **Remove-ManagementRoleEntry**. Vous ne pouvez pas ajouter d’entrées de rôles au nouveau rôle car il ne peut contenir que les entrées de rôle sur le rôle intégré parent. Pour plus d’informations, consultez les rubriques suivantes :
    
      - [Modifier une entrée de rôle](change-a-role-entry-exchange-2013-help.md)
    
      - [Supprimer une entrée de rôle d'un rôle](remove-a-role-entry-from-a-role-exchange-2013-help.md)

3.  Si vous souhaitez remplacer le rôle intégré par le nouveau rôle personnalisé, supprimez toute attribution de rôle associée au rôle intégré. Pour plus d’informations, consultez les rubriques suivantes :
    
      - Section « Ajouter ou supprimer un rôle dans un groupe de rôles » dans [Gérer des groupes de rôles](manage-role-groups-exchange-2013-help.md)
    
      - [Supprimer un rôle d’un utilisateur ou un groupe universel de sécurité](remove-a-role-from-a-user-or-usg-exchange-2013-help.md)

4.  Affectez le nouveau rôle personnalisé aux personnes requises. Pour plus d’informations, consultez les rubriques suivantes :
    
      - Section « Ajouter ou supprimer un rôle dans un groupe de rôles » dans [Gérer des groupes de rôles](manage-role-groups-exchange-2013-help.md)
    
      - [Ajouter un rôle à un utilisateur ou un groupe de sécurité universel](add-a-role-to-a-user-or-usg-exchange-2013-help.md)
        
        > [!NOTE]
        > Si vous souhaitez que les autres utilisateurs, en plus de l’utilisateur qui a créé le rôle, puissent attribuer le nouveau rôle personnalisé, assurez-vous d’ajouter une attribution de rôle de délégation à au moins une personne affectée au rôle. Pour plus d’informations, consultez la rubrique <a href="delegate-role-assignments-exchange-2013-help.md">Déléguer les attributions de rôles</a>.

