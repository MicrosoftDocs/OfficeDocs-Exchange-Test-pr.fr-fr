---
title: 'Présentation des stratégies d’attribution de rôle de gestion: Exchange 2013 Help'
TOCTitle: Présentation des stratégies d’attribution de rôle de gestion
ms:assetid: 25913e43-326a-4371-90b5-021a35f100fe
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dd638100(v=EXCHG.150)
ms:contentKeyID: 50477766
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Présentation des stratégies d’attribution de rôle de gestion

 

_**Sapplique à :** Exchange Online, Exchange Server 2013_

_**Dernière rubrique modifiée :** 2015-03-09_

Une *stratégie d’attributions de rôles de gestion* contient un ou plusieurs rôles de gestion des utilisateurs finals qui leur permettent de gérer leur propre boîte aux lettres Microsoft Exchange Server 2013 et la configuration du groupe de distribution. Les stratégies d’attributions de rôle, qui font partie du modèle d’autorisation du contrôle d’accès basé sur un rôle dans Exchange 2013 vous permettent de contrôler quels paramètres de configuration de groupe de distribution et de boîte aux lettres spécifique peuvent être modifiés par vos utilisateurs finals. Différents groupes d’utilisateurs peuvent bénéficier de stratégies d’attribution de rôle spécialisées.

> [!NOTE]
> Cette rubrique traite de la fonctionnalité RBAC avancée. Si vous souhaitez gérer des autorisations Exchange 2013 de base, comme l’utilisation du centre d’administration Exchange pour ajouter et supprimer des membres dans les groupes de rôles, créer et modifier des groupes de rôles ou créer et modifier des stratégies d’attribution de rôles, consultez la rubrique <a href="permissions-exchange-2013-help.md">Autorisations</a>.


Pour plus d’informations sur le contrôle d’accès basé sur un rôle, voir [Présentation du contrôle d'accès basé sur un rôle](understanding-role-based-access-control-exchange-2013-help.md).

**Table des matières**

Couches de stratégie d’attribution de rôle

Stratégies d’attribution de rôle explicite et par défaut

Utilisation de stratégies d’attribution de rôle

Gestion de stratégie d’attribution de rôle

## Couches de stratégie d’attribution de rôle

Les différentes couches qui permettent de créer le modèle de stratégie d’attribution de rôle sont décrites dans la liste suivante :

  - **Boîtes aux lettres** Une stratégie d’attribution de rôle unique est affectée aux boîtes aux lettres. Lorsqu’une stratégie d’attribution de rôle est affectée à une boîte aux lettres, les affectations entre les rôles de gestion et la stratégie d’attribution de rôle s’appliquent à la boîte aux lettres. Cette action permet d’accorder à la messagerie toutes les autorisations fournies par les rôles de gestion.

  - **Stratégie d’attribution de rôle de gestion**   La *stratégie d’attribution de rôle de gestion* est un objet spécial dans Exchange 2013. Une stratégie d’attribution de rôle est associée aux utilisateurs lorsque leur boîte aux lettres est créée ou si vous modifiez la stratégie d’attribution de rôle sur une boîte aux lettres. C’est également ce que vous attribuez pour les rôles de gestion des utilisateurs finals. L’association de tous les rôles sur une stratégie d’attribution de rôle définit tout ce que l’utilisateur peut gérer dans sa boîte aux lettres ou ses groupes de distribution.

  - **Attribution d’un rôle de gestion**   Une *attribution de rôle de gestion* représente le lien entre un rôle de gestion et une stratégie d’attribution de rôle. L’attribution d’un rôle de gestion à une stratégie d’attribution de rôle permet l’utilisation des cmdlets et des paramètres définis dans le rôle de gestion. Lorsque vous créez une attribution de rôle entre une stratégie d’attribution de rôle et un rôle de gestion, vous ne pouvez spécifier aucune étendue. L’étendue appliquée par l’attribution est basée sur le rôle de gestion et elle est `Self` ou `MyGAL`. Pour plus d’informations, voir [Présentation des attributions de rôles de gestion](understanding-management-role-assignments-exchange-2013-help.md).

  - **Rôle de gestion**   Un *rôle de gestion* est un conteneur pour un groupe d’entrées de rôles de gestion. Les rôles sont utilisés pour définir les tâches spécifiques qu’un utilisateur peut effectuer avec sa boîte aux lettres ou les groupes de distribution. Une *entrée de rôle de gestion* est une cmdlet, un script ou une autorisation spéciale qui permet d’effectuer chaque tâche spécifique dans un rôle de gestion. Vous pouvez uniquement utiliser des rôles de gestion des utilisateurs finals avec les stratégies d’attribution de rôle. Pour plus d’informations, voir [Présentation des rôles de gestion](understanding-management-roles-exchange-2013-help.md).

  - **Entrée de rôle de gestion**   Les entrées de rôle de gestion sont les entrées individuelles d’un rôle de gestion qui déterminent les cmdlets et paramètres disponibles pour le rôle de gestion et le groupe de rôles. Chaque entrée de rôle est constituée d’une cmdlet unique et des paramètres accessibles par le rôle de gestion.

La figure suivante affiche chacune des couches de stratégie de rôle dans la liste précédente et la manière dont les couches sont associées.

**Modèle de stratégie d’attribution de rôle de gestion**

![Relations des modèles d’attribution des rôles](images/Dd638100.7f7c11ca-0d61-464d-98a3-a9991ec811b5(EXCHG.150).jpg "Relations des modèles d’attribution des rôles")

Pour plus d’informations sur les rôles de gestion, les attributions de rôle et les étendues, voir [Présentation du contrôle d'accès basé sur un rôle](understanding-role-based-access-control-exchange-2013-help.md).

## Stratégies d’attribution de rôle explicite et par défaut

Les sections suivantes décrivent les deux types de stratégies d’attribution de rôle dans Exchange 2013.

## Stratégie d’attribution de rôles par défaut

Une stratégie d’attribution de rôle par défaut est une stratégie attribuée à une boîte aux lettres lorsque la boîte aux lettres est créée ou déplacée sur un serveur exécutant Exchange 2013, et qu’une stratégie d’attribution de rôle n’a pas été fournie à l’aide du paramètre *RoleAssignmentPolicy* sur les cmdlets **New-Mailbox** ou **Enable-Mailbox**.

Exchange 2013 inclut une stratégie d’attribution de rôle par défaut qui fournit aux utilisateurs finals les autorisations utilisées le plus souvent. Vous pouvez modifier les autorisations par défaut sur la stratégie d’attribution de rôle par défaut en ajoutant ou en supprimant des rôles de gestion dans cette stratégie ou à partir de cette dernière.

Si vous souhaitez remplacer la stratégie d’attribution de rôle intégrée par défaut par votre propre stratégie d’attribution de rôle par défaut, vous pouvez utiliser la cmdlet **Set-RoleAssignmentPolicy** pour sélectionner une nouvelle stratégie par défaut. Si vous n’indiquez pas spécifiquement une stratégie d’attribution de rôle lorsque vous effectuez cette opération, la stratégie d’attribution de rôle que vous avez spécifiée par défaut est affectée aux nouvelles boîtes aux lettres.

Lorsque vous modifiez la stratégie d’attribution de rôle par défaut, les boîtes aux lettres pour lesquelles la stratégie d’attribution de rôle est fournie par défaut ne recevront pas automatiquement l’obtention de la nouvelle stratégie d’attribution de rôle par défaut. Si vous souhaitez mettre à jour les boîtes aux lettres préalablement créées pour utiliser la stratégie d’attribution de rôle que vous avez définie par défaut, vous devez utiliser la cmdlet **Set-Mailbox**.

## Stratégie d’attribution de rôle explicite

Une stratégie d’attribution de rôle explicite est une stratégie que vous affectez manuellement à une boîte aux lettres en utilisant le paramètre *RoleAssignmentPolicy* sur la cmdlet **New-Mailbox**, **Set-Mailbox** ou **Enable-Mailbox**. Lorsque vous affectez une stratégie d’attribution de rôle explicite, la nouvelle stratégie prend effet immédiatement et remplace celle préalablement attribuée.

## Utilisation de stratégies d’attribution de rôle

Les stratégies d’attribution de rôle vous permettent d’adapter les autorisations en fonction des besoins métier que vos utilisateurs doivent configurer. Si la stratégie d’attribution de rôle par défaut répond à vos besoins, vous n’avez pas besoin d’effectuer une personnalisation. Cependant, si vous disposez de nombreux groupes d’utilisateurs avec des besoins spécialisés, vous pouvez créer des stratégies d’attribution de rôle pour chacune d’entre eux.

La stratégie d’attribution de rôle par défaut que vous utilisez devrait contenir les autorisations qui s’appliquent à votre groupe d’utilisateurs le plus large. Puis, créez des stratégies d’attribution de rôle pour chacun de vos groupes d’utilisateurs spécialisés et adaptez ces stratégies d’attribution de rôle pour accorder plus ou moins d’autorisations à ces groupes. Lorsque vous organisez vos stratégies d’attribution de rôle de cette manière, vous réduisez la complexité en attribuant explicitement des stratégies d’attribution de rôle uniquement aux utilisateurs spécialisés tandis que la majorité de vos utilisateurs reçoivent les autorisations utilisées le plus souvent par la stratégie d’attribution de rôle par défaut.

Une boîte aux lettres peut avoir uniquement une stratégie d’attribution de rôle. Une stratégie d’attribution de rôle est affectée à tous les utilisateurs, y compris les administrateurs et les utilisateurs spécialisés. Si vous souhaitez qu’un utilisateur bénéficie d’un ensemble d’autorisations différent, vous devez attribuer à la boîte aux lettres de cet utilisateur une autre stratégie d’attribution de rôle avec les autorisations requises.

## Gestion de stratégie d’attribution de rôle

Pour ajouter une stratégie d’attribution de rôle, vous devez d’abord en créer une et décider si elle deviendra la stratégie d’attribution de rôle par défaut. Après avoir créé une stratégie d’attribution de rôle, vous affectez des rôles de gestion à la stratégie d’attribution de rôle. Puis, vous affectez la stratégie d’attribution de rôle aux boîtes aux lettres. Vous pouvez ultérieurement choisir d’ajouter ou de supprimer des rôles de gestion ou choisir une stratégie d’attribution de rôle différente pour qu’elle devienne la stratégie par défaut.

Le tableau suivant répertorie la couche de stratégie d’attribution de rôle et les rubriques relatives à la procédure que vous pouvez utiliser pour gérer chaque couche.

### Rubriques de gestion de stratégie d’attribution de rôle

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Couche de modèle de stratégie d’attribution de rôle</th>
<th>Rubriques de gestion</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Boîte aux lettres</p></td>
<td><p><a href="manage-user-mailboxes-exchange-2013-help.md">Gestion des boîtes aux lettres utilisateur</a></p>
<p><a href="change-the-assignment-policy-on-a-mailbox-exchange-2013-help.md">Modifier la stratégie d’attribution sur une boîte aux lettres</a></p></td>
</tr>
<tr class="even">
<td><p>Stratégie d’attribution de rôle</p></td>
<td><p><a href="manage-role-assignment-policies-exchange-2013-help.md">Gérer les stratégies d’attribution des rôles</a></p>
<p></p></td>
</tr>
<tr class="odd">
<td><p>Rôles de gestion et attributions</p></td>
<td><p><a href="manage-role-assignment-policies-exchange-2013-help.md">Gérer les stratégies d’attribution des rôles</a></p>
<p></p></td>
</tr>
<tr class="even">
<td><p>Entrées de rôles de gestion</p></td>
<td><p><a href="add-a-role-entry-to-a-role-exchange-2013-help.md">Ajouter une entrée de rôle à un rôle</a></p>
<p><a href="change-a-role-entry-exchange-2013-help.md">Modifier une entrée de rôle</a></p>
<p><a href="remove-a-role-entry-from-a-role-exchange-2013-help.md">Supprimer une entrée de rôle d'un rôle</a></p>

> [!NOTE]  
> La modification des entrées de rôle de gestion dans les rôles de gestion d’une stratégie d’attribution de rôle est une tâche avancée et elle n’est généralement pas requise dans la plupart des cas. Vous pouvez à la place utiliser un rôle de gestion préexistant qui convienne à vos besoins. Pour plus d’informations, voir <a href="built-in-role-groups-exchange-2013-help.md">Groupes de rôles intégrés</a>.

</td>
</tr>
</tbody>
</table>

