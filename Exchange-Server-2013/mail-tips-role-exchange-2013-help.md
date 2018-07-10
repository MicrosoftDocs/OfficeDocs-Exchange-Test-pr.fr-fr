---
title: 'Rôle des conseils de messagerie: Exchange 2013 Help'
TOCTitle: Rôle des conseils de messagerie
ms:assetid: 74495ded-6097-4f10-a829-c8ed81f5ba3e
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dd876909(v=EXCHG.150)
ms:contentKeyID: 50478463
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Rôle des conseils de messagerie

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2015-03-09_

Le rôle de gestion Infos-courrier permet aux administrateurs de gérer les conseils de messagerie dans une organisation.

Ce rôle de gestion est l’un des rôles intégrés dans le modèle des autorisations de contrôle d’accès en fonction du rôle (RBAC) dans Microsoft Exchange Server 2013. Les rôles de gestion, qui sont attribués à un ou plusieurs groupes de rôles de gestion, stratégies d’attribution de rôle de gestion, utilisateurs ou groupes de sécurité universels, agissent en tant que regroupement logique de cmdlets ou de scripts qui sont associés pour fournir un accès afin d’afficher ou de modifier la configuration des composants Exchange 2013, tels que des bases de données de boîtes aux lettres, des règles de transport et des destinataires. Si une cmdlet ou un script et ses paramètres, appelés « entrée de rôle de gestion », sont inclus dans un rôle, cette cmdlet ou ce script et ses paramètres peuvent être exécutés par les utilisateurs qui ont attribué le rôle. Pour plus d’informations sur les rôles de gestion et les entrées de rôles de gestion, consultez la rubrique [Présentation des rôles de gestion](understanding-management-roles-exchange-2013-help.md).

Pour plus d’informations sur les rôles de gestion, les groupes de rôles de gestion et les autres composants de contrôle d’accès basé sur un rôle, voir [Présentation du contrôle d'accès basé sur un rôle](understanding-role-based-access-control-exchange-2013-help.md).

## Gestion des attributions de rôles

Pour que ce rôle puisse accorder des autorisations, il doit être attribué à la personne affectée au rôle, qui peut être un groupe de rôles, un utilisateur ou un groupe de sécurité universel (USG). Cette affectation s’effectue à l’aide des attributions de rôles de gestion. Les attributions de rôles lient les personnes affectées au rôle aux rôles. Si plusieurs rôles sont attribués à une personne affectée au rôle, celle-ci bénéficie de l’association de toutes les autorisations accordées par tous les rôles attribués.

En plus de la liaison des personnes affectées au rôle pour ces rôles, les attributions de rôles peuvent également être appliquées aux étendues de gestion intégrées ou personnalisées. Les étendues de gestion contrôlent quels objets de base de données, destinataire et serveur peuvent être modifiés par les personnes affectées au rôle. Si ce rôle est attribué à une personne affectée au rôle mais qu’une étendue de gestion autorise la personne affectée au rôle à gérer uniquement certains objets basés sur une étendue définie, cette personne peut uniquement utiliser les autorisations accordées par ce rôle sur ces objets spécifiques. Les autorisations fournies par ce rôle ne peuvent pas être appliquées aux objets hors de l’étendue définie sur l’attribution de rôle. Pour plus d’informations sur les attributions de rôle et les étendues, consultez les rubriques suivantes :

  - [Présentation des attributions de rôles de gestion](understanding-management-role-assignments-exchange-2013-help.md)

  - [Présentation des portées du rôle de gestion](understanding-management-role-scopes-exchange-2013-help.md)

Ce rôle est attribué à un ou plusieurs groupes de rôles par défaut. Pour plus d’informations, consultez la section « Attributions de rôles de gestion par défaut » plus loin dans cette rubrique.

Si vous souhaitez afficher une liste de groupes de rôles, d’utilisateurs ou de groupes de sécurité universels attribués à ce rôle, utilisez la commande suivante.

    Get-ManagementRoleAssignment -Role "<role name>"

## Attributions de rôles normales et de délégation

Ce rôle peut être attribué aux personnes affectées au rôle à l’aide d’attributions de rôles normales ou de délégation. Les attributions de rôles normales accordent des autorisations fournies par le rôle à la personne affectée au rôle. Les attributions de rôle de délégation accordent à la personne affectée au rôle la possibilité d’affecter le rôle aux autres personnes affectées au rôle. Pour plus d’information sur les attributions de rôle normales et la délégation d’attributions de rôle de gestion, consultez la rubrique Présentation des attributions de rôles de gestion[Présentation des attributions de rôles de gestion](understanding-management-role-assignments-exchange-2013-help.md).

## Ajout ou suppression des attributions de rôles

Vous pouvez attribuer ce rôle à une autre personne. En attribuant ce rôle à une autre personne, vous modifiez ses autorisations en les accordant au nouvel utilisateur. Vous pouvez attribuer ce rôle à d’autres groupes de rôles intégrés ou vous pouvez créer des groupes de rôles et leur attribuer ce rôle. Vous pouvez également attribuer ce rôle aux utilisateurs ou groupes de sécurité universels. Cependant, nous vous recommandons de limiter l’attribution de rôles aux utilisateurs et groupes de sécurité universels car de telles attributions risquent d’augmenter sensiblement la complexité de votre modèle d’autorisations.

Pour attribuer ce rôle à d’autres personnes, il doit être attribué à un groupe de rôles, dont vous faites partie, directement à vous ou à un groupe de sécurité universel dont vous êtes membre, en utilisant une attribution de rôle de délégation. Pour plus d’informations sur les attributions de rôle de délégation, consultez la section « Attributions de rôles normales et de délégation ».

Vous pouvez également supprimer ce rôle à partir des groupes de rôle intégrés, des groupes de rôles que vous créez, des utilisateurs et des groupes de sécurité universels. Cependant, il doit toujours y avoir au moins une attribution de rôle de délégation entre ce rôle et un groupe de rôles ou un groupe de sécurité universel. Vous ne pouvez pas supprimer la dernière attribution de rôle de délégation. Cette limitation permet d’empêcher de vous déconnecter du système.

> [!NOTE]
> Il doit toujours y avoir au moins une attribution de rôle de délégation entre ce rôle et un groupe de rôles ou un groupe de sécurité universel. Vous ne pouvez pas supprimer la dernière attribution de rôle de délégation associée à ce rôle si la dernière attribution est affectée à un utilisateur.


Pour plus d’informations sur la manière d’ajouter ou de supprimer des attributions entre ce rôle et les groupes de rôles, les utilisateurs et les groupes de sécurité universels, consultez les rubriques suivantes :

  - [Gérer des groupes de rôles](manage-role-groups-exchange-2013-help.md)

  - [Ajouter un rôle à un utilisateur ou un groupe de sécurité universel](add-a-role-to-a-user-or-usg-exchange-2013-help.md)

  - [Supprimer un rôle d’un utilisateur ou un groupe universel de sécurité](remove-a-role-from-a-user-or-usg-exchange-2013-help.md)

## Modification des étendues de gestions sur les attributions de rôles

Vous pouvez également modifier les étendues de gestion sur les attributions de rôles existantes entre ce rôle et les personnes affectées au rôle. En modifiant les étendues sur ces attributions de rôles, vous contrôlez les objets qui peuvent être gérés à l’aide des autorisations fournies par ce rôle. Vous pouvez modifier l’étendue sur une attribution de rôle de plusieurs manières. Vous pouvez utiliser l’une des méthodes suivantes :

  - Ajouter une étendue personnalisée à l’aide de la cmdlet **Set-ManagementRoleAssignment**. Pour plus d’informations, consultez les rubriques suivantes :
    
      - [Créer une étendue normale ou exclusive](create-a-regular-or-exclusive-scope-exchange-2013-help.md)
    
      - [Modifier une attribution de rôle](change-a-role-assignment-exchange-2013-help.md)

  - Ajouter ou modifier une étendue de l’unité d’organisation à l’aide de la cmdlet **Set-ManagementRoleAssignment**. Pour plus d’informations, consultez la rubrique [Modifier une attribution de rôle](change-a-role-assignment-exchange-2013-help.md).

  - Ajouter ou modifier une étendue prédéfinie à l’aide de la cmdlet **Set-ManagementRoleAssignment**. Pour plus d’informations, consultez la rubrique [Modifier une attribution de rôle](change-a-role-assignment-exchange-2013-help.md).

  - Modifier l’étendue d’un destinataire, d’un serveur ou d’une base de données sur une étendue personnalisée associée à une attribution de rôle à l’aide de la cmdlet **Set-ManagementScope**. Pour plus d’informations, consultez la rubrique [Modifier l’étendue d’un rôle](change-a-role-scope-exchange-2013-help.md).

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
<th>Groupe de rôles</th>
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
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
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

