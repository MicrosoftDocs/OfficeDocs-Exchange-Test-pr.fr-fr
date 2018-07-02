---
title: 'Présentation des autorisations sur plusieurs forêts: Exchange 2013 Help'
TOCTitle: Présentation des autorisations sur plusieurs forêts
ms:assetid: 8241033f-e201-4799-b17c-4f120c6e6445
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dd298099(v=EXCHG.150)
ms:contentKeyID: 50478584
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Présentation des autorisations sur plusieurs forêts

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2015-04-07_

De nombreuses entreprises déploient plusieurs forêts pour créer des limites de sécurité dans leurs organisations. L'utilisation de plusieurs forêts aide les administrateurs à définir ces limites de sécurité afin de mieux répondre aux exigences, qu'il s'agisse de garantir qu'un nombre restreint de personnes ait accès aux ressources ou de segmenter les services au sein d'une organisation.

Microsoft Exchange Server 2013 prend en charge deux types de topologies à forêts multiples :

  - **Inter-forêts**   Les topologies inter-forêts peuvent avoir plusieurs forêts, chacune avec leur propre installation d'Exchange.

  - **Forêt ressource**   Les topologies de forêt ressource comprennent une forêt Exchange et une ou plusieurs forêts de comptes.

Dans le cadre de cette rubrique, la forêt contenant les groupes de sécurité universels et les utilisateurs en dehors de la forêt où est installé Exchange 2013, qu'il s'agisse d'une forêt de comptes ou d'une autre forêt ressource, est appelée une forêt étrangère.

La configuration des autorisations dans une topologie à plusieurs forêts repose sur la bonne configuration de la synchronisation des approbations de forêt et de la liste d'adresses globale pour la création de boîtes aux lettres liées. La forêt Exchange 2013 doit approuver la forêt étrangère contenant les groupes de sécurité universels associés aux groupes et utilisateurs de rôles liés associés aux boîtes aux lettres liées.

Exchange 2013 utilise un modèle d’autorisations de contrôle d’accès basé sur un rôle (RBAC). Les groupes de rôles de gestion dont les administrateurs sont membres et les stratégies d'attribution de rôles de gestion affectées aux utilisateurs finaux déterminent les actions que peuvent entreprendre chaque administrateur et utilisateur final. Pour comprendre les autorisations sur plusieurs forêts, vous devez connaître le contrôle d'accès basé sur un rôle. Pour plus d'informations sur le contrôle d'accès basé sur un rôle, les groupes de rôles et les stratégies d'attribution de rôles, consultez les rubriques suivantes :

  - [Présentation du contrôle d'accès basé sur un rôle](understanding-role-based-access-control-exchange-2013-help.md)

  - [Présentation des groupes de rôles de gestion](understanding-management-role-groups-exchange-2013-help.md)

  - [Présentation des stratégies d’attribution de rôle de gestion](understanding-management-role-assignment-policies-exchange-2013-help.md)

Souhaitez-vous rechercher les tâches de gestion liées aux autorisations de gestion ? Consultez la rubrique [Autorisations](permissions-exchange-2013-help.md).

**Contenu de cette rubrique**

Autorisations dans une topologie à plusieurs forêts

Autorisations inter-limites

Configurer des autorisations inter-limites

## Autorisations dans une topologie à plusieurs forêts

Le contrôle d'accès basé sur un rôle applique les autorisations à tous les objets Exchange dans une forêt unique, la configuration du contrôle d'accès basé sur un rôle dans chaque forêt étant configurée indépendamment de toutes les autres forêts. Quand vous créez un groupe de rôles dans une forêt, ce dernier n'existe dans aucune autre forêt et les autorisations qu'il accorde s'appliquent uniquement à la forêt dans laquelle il a été créé. Par exemple, un membre d'un groupe de rôles qui accorde des autorisations pour créer une boîte aux lettres peut créer uniquement cette dernière dans la forêt contenant ce groupe de rôles.

Si vous disposez de plusieurs forêts Exchange et souhaitez configurer des autorisations à l’identique dans chacune des forêts, vous devez appliquer la même configuration dans chaque forêt de manière explicite. Par exemple, vous avez deux forêts Exchange 2013 et souhaitez créer un groupe de rôles Gestion de la conformité pour gérer les autorisations de votre service juridique, procédez comme suit :

  - Dans chaque forêt, créez un groupe de rôles nommé Gestion de la conformité. Si vos administrateurs se trouvent dans une forêt étrangère distincte de l'une ou l'autre forêt Exchange, créez les deux groupes de rôles en tant que groupes de rôles liés. Pour plus d'informations sur les groupes de rôles, voir la section Autorisations inter-limites.

  - Dans chaque forêt, créez des attributions de rôles entre les nouveaux groupes de rôles et les rôles que vous voulez utiliser.

  - Dans le cadre des nouvelles attributions de rôles, vous pouvez également ajouter des étendues de gestion qui englobent les objets serveur et destinataire dans chaque forêt.

  - Si vous avez créé les groupes de rôles en tant que groupes de rôles liés, ajoutez des membres au groupe de sécurité universel associé dans la forêt étrangère.

La figure suivante montre comment les groupes de rôles configurés dans les forêts Exchange 2013 sont liés à leurs forêts respectives. Le groupe de rôles Gestion de l'organisation dans la forêt Exchange 2013 A accorde des autorisations uniquement pour gérer les boîtes aux lettres et serveurs qui se trouvent dans cette forêt. De même, les groupes de rôles dans la forêt Exchange 2013 B accordent des autorisations uniquement aux boîtes aux lettres et serveurs qui se trouvent dans cette forêt.

La figure montre également que le groupe de rôles personnalisé A est créé dans chaque forêt. Même s'ils sont été créés avec le même nom, chacun d'entre eux représente sa propre entité distincte. En fait, comme l'illustre la figure, chacun peut se voir attribuer des rôles de gestion différents dans leurs forêts respectives. Le groupe de rôles personnalisé A dans la forêt Exchange 2013 A se voit attribuer les rôles Recherche de boîte aux lettres et Suivi de message, tandis que le groupe de rôles personnalisé A dans la forêt Exchange 2013 B se voit attribuer les rôles Recherche de boîte aux lettres et Gestion de la rétention.

En outre, les étendues de gestion créées dans chaque forêt sont également liées par la forêt. Les étendues de serveur créées dans chaque forêt peut uniquement contenir les serveurs membres de cette forêt. Les étendues A et B du serveur peuvent uniquement contenir les serveurs de la forêt Exchange 2013 A et de la forêt Exchange 2013 B, respectivement. De même, l'étendue du destinataire dans la forêt Exchange 2013 B peut uniquement contenir les boîtes aux lettres qui se trouvent dans la forêt Exchange 2013 B.

**Relation de portée entre les contrôles d'accès basés sur un rôle et les limites de la forêt**

![Relations de portée entre les contrôles d’accès basés sur un rôle et les limites de la forêt](images/Dd298099.220da7c3-cbb8-42ac-9d58-084d996bf837(EXCHG.150).gif "Relations de portée entre les contrôles d’accès basés sur un rôle et les limites de la forêt")

## Autorisations inter-limites

Les autorisations accordées par les contrôles d'accès basés sur un rôle autorisent seulement les utilisateurs à afficher ou modifier les objets Exchange d'une forêt spécifique. Vous pouvez cependant octroyer des autorisations pour afficher et modifier les objets Exchange d'une forêt aux utilisateurs se trouvant en dehors de cette forêt. En utilisant les autorisations inter-limites, vous pouvez centraliser les comptes de gestion Exchange dans une forêt unique au lieu de devoir vous réauthentifier sur chaque forêt individuelle pour exécuter des tâches.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Les autorisations accordées à un utilisateur en dehors d'une forêt Exchange s'appliquent toujours seulement à cette forêt Exchange spécifique. Par exemple, si un utilisateur dans une forêt étrangère est membre du groupe de rôles lié Gestion de l'organisation situé dans ForêtA, il peut gérer uniquement les objets Exchange contenus dans ForêtA. Un utilisateur doit être membre des groupes de rôles liés dans chaque forêt Exchange pour se voir octroyer des autorisations pour gérer chaque forêt.</td>
</tr>
</tbody>
</table>


Les autorisations inter-limites vous permettent également d’appliquer des stratégies d’attribution de rôle aux boîtes aux lettres des utilisateurs dont les boîtes aux lettres se trouvent dans une forêt Exchange, mais dont les comptes utilisateur se trouvent dans une forêt de comptes. Exchange 2013 prend en charge l’autorisation inter-limites en utilisant des groupes de rôles liés et des boîtes aux lettres liées, faisant l’objet d'une présentation dans les sections suivantes.

## Autorisations administratives

Les autorisations administratives sont octroyées dans les limites de la forêt en utilisant des groupes de rôles liés et des boîtes aux lettres liées.

Un groupe de rôles lié est créé dans l'organisation Exchange 2013 et lié à un groupe de sécurité universel dans les limites de la forêt dans la forêt étrangère. Le groupe de sécurité universel sur lequel est lié le groupe de rôles lié peut être :

  - Un groupe universel de sécurité dédié utilisé spécifiquement par le groupe de rôles lié

  - Un groupe universel de sécurité lié par des groupes de rôles liés dans plusieurs forêts Exchange 2013

  - Un groupe de sécurité universel d'un groupe de rôles dans une autre forêt Exchange 2013

  - Un groupe de sécurité universel associé à un rôle administratif Exchange Server 2007 ou un groupe de rôles Exchange 2010

Le groupe de sécurité universel sur lequel est lié le groupe de rôles doit se trouver dans une autre forêt. Vous ne pouvez pas lier un groupe de rôles à un groupe de sécurité universel dans la même forêt.

La figure suivante montre que les groupes de sécurité universels dans une forêt de comptes peuvent être associés à des groupes de rôles dans une ou plusieurs forêts ressource Exchange 2013. Les membres des groupes de sécurité universels dans la forêt de comptes deviennent en réalité membres des groupes de rôles par le biais des groupes de sécurité universels.

**Groupes de rôles liés associés aux groupes de sécurité universels dans une forêt distincte**

![Groupe de rôles lié et relations du groupe de sécurité universel](images/Dd298099.23f245e8-b80f-4082-8628-ee6701259be6(EXCHG.150).gif "Groupe de rôles lié et relations du groupe de sécurité universel")

Quand vous créez un groupe de rôles lié, vous attribuez des rôles au groupe de rôles lié dans la forêt Exchange 2013. Les attributions qui associent les rôles au groupe de rôles lié peuvent si nécessaire inclure des portées de gestion. Ces portées sont limitées à la forêt dans laquelle est créé le groupe de rôles lié.

L'appartenance du groupe de rôles lié est gérée en ajoutant et en supprimant des membres depuis et vers le groupe de sécurité universel dans la forêt étrangère. Lorsque vous ajoutez des membres à ce groupe de sécurité universel, les autorisations attribuées au groupe de rôles lié dans la forêt Exchange 2013 leur sont accordées. Si vous avez lié plusieurs groupes de rôles liés au même groupe de sécurité universel, les membres de ce groupe de sécurité universel se voient octroyer les autorisations attribuées à chaque groupe de rôles lié dans chaque forêt Exchange 2013.

Vous ne pouvez pas gérer l'appartenance d'un groupe de rôles lié à partir de la forêt Exchange 2013.

Une seconde méthode d'attribution des autorisations administratives dans les limites de la forêt consiste à utiliser des boîtes aux lettres liées. Pour que les utilisateurs d'une forêt de comptes utilisent un déploiement Exchange 2013 dans un forêt ressource Exchange 2013 distincte, vous devez configurer des boîtes aux lettres liées pour chaque utilisateur. Les boîtes aux lettres liées peuvent être ajoutées en tant que membres aux groupes de rôles dans la forêt Exchange 2013. Quand une boîte aux lettres liée devient membre d'un groupe de rôles, elle se voit accorder, ainsi que l'utilisateur dans la forêt de comptes associée à la boîte aux lettres liée, les autorisations fournies par le groupe de rôles.

La figure suivante montre la relation entre les utilisateurs dans une forêt de comptes, les boîtes aux lettres liées leur étant associées et les groupes de rôles dont ils sont membres.

**Utilisateurs dans une forêt de comptes associés à des boîtes aux lettres liées membres de groupes de rôles**

![Relations entre le groupe de rôles et la boîte aux lettres liée](images/Dd298099.e59242f6-5c63-4114-90f7-6b6c2478570c(EXCHG.150).gif "Relations entre le groupe de rôles et la boîte aux lettres liée")

Les groupes de rôles liés et les boîtes aux lettres liées comportent tous deux des avantages et des inconvénients lorsqu'ils sont utilisés pour attribuer une autorisation administrative dans les limites de la forêt. Le tableau suivant décrit certains d'entre eux.

### Avantages et inconvénients du groupe de rôle lié et de la boîte aux lettres liée

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Groupes de rôles liés ou boîtes aux lettres liées</th>
<th>Avantage</th>
<th>Inconvénient</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Groupes de rôles liés</p></td>
<td><p>Vous pouvez associer plusieurs groupes de rôles liés provenant de plusieurs forêts Exchange 2013 sur un groupe de sécurité universel unique dans une forêt de comptes ou une autre forêt ressource Exchange. Cela vous permet d'administrer des topologies de forêt Exchange complexes par le biais d'un petit ensemble de groupes de sécurité universels dans une forêt unique.</p></td>
<td><p>Il est impossible de convertir un groupe de rôles ordinaire en groupe de rôles lié. Vous devez créer manuellement les groupes de rôles liés pour remplacer chaque groupe de rôle ordinaire disposant des autorisations que vous souhaitez octroyer dans la limite de la forêt. Pour plus d'informations, consultez la rubrique Configurer des autorisations inter-limites.</p></td>
</tr>
<tr class="even">
<td><p>Boîtes aux lettres liées</p></td>
<td><p>Les boîtes aux lettres liées vous permettent d'utiliser les groupes de rôles existants dans la forêt Exchange. Les boîtes aux lettres liées sont ajoutées en tant que membres aux groupes de rôles existants, comme n'importe quelle boîte aux lettres ordinaire, groupe de sécurité universel et utilisateur dans la même forêt Exchange.</p></td>
<td><p>Si vous octroyez des autorisations dans plusieurs forêts Exchange 2013 à l'aide de boîtes aux lettres liées à un utilisateur unique dans une forêt de comptes, vous devez modifier l'appartenance du groupe de rôles dans chaque forêt Exchange 2013 si vous souhaitez modifier les autorisations accordées à l'utilisateur.</p></td>
</tr>
</tbody>
</table>


Il est conseillé d'utiliser les groupes de rôles liés pour octroyer l'autorisation dans les limites de la forêt si vous envisagez d'avoir plusieurs forêts ressource Exchange.

## Autorisations de l’utilisateur final

Les autorisations de l'utilisateur final sont attribuées à des boîtes aux lettres individuelles à l'aide de stratégies d'affectation de rôle. Quand Exchange 2013 est installé dans une forêt ressource, des boîtes aux lettres liées sont créées dans la forêt ressource et associées aux comptes d'utilisateurs dans la forêt de comptes.

Quand une boîte aux lettres liée est créée, une stratégie d'affectation de rôles lui est attribuée par défaut comme pour n'importe quelle boîte aux lettres ordinaire. La stratégie d'affectation de rôles détermine les autorisations de l'utilisateur final qui sont octroyées à la boîte aux lettres. Ces autorisations permettent aux utilisateurs d'afficher et de modifier les paramètres associés aux fonctionnalités suivantes :

  - Informations de profil de l'utilisateur final

  - Messagerie vocale de l'utilisateur final

  - Appartenance et propriété de distribution de l'utilisateur final

Lorsqu'une stratégie d'affectation de rôles est attribuée à une boîte aux lettres liée, l'utilisateur dans la forêt de comptes associée à la boîte aux lettres liée se voit accorder les autorisations de gestion des fonctionnalités disponibles pour cet utilisateur. Les autorisations s'appliquent uniquement aux ressources dans la forêt Exchange sur laquelle se trouve la boîte aux lettres liée. La figure suivante montre la relation entre l'utilisateur final dans une forêt de comptes, les boîtes aux lettres liées leur étant associées et la stratégie d'affectation de rôles attribuée à la boîte aux lettres liée. De plus, une boîte aux lettres liée associée à un utilisateur administratif dans la forêt de comptes peut être associée à plusieurs groupes de rôles en plus de la stratégie d'affectation de rôles.

**Utilisateurs dans une forêt de comptes associés à des boîtes aux lettres liées pour lesquelles une stratégie d'affectation de rôles est attribuée**

![Relations entre le groupe de rôles et la stratégie d’attribution](images/Dd298099.785b9b35-4292-43ce-917b-117d0174742e(EXCHG.150).gif "Relations entre le groupe de rôles et la stratégie d’attribution")

Retour au début

## Configurer des autorisations inter-limites

Pour configurer les autorisations inter-limites dans une topologie à plusieurs forêts, vous devez créer des groupes de rôles liés pour chaque groupe de rôles que vous voulez lier aux groupes de sécurité universels dans une forêt étrangère. Cela signifie que vous devez créer un groupe de rôles lié pour chaque groupe de rôles intégré. Vous devez :

1.  Créer un groupe de sécurité universel dans la forêt étrangère pour chaque groupe de rôles lié à créer. Ajoutez des membres à ce groupe de sécurité universel auquel vous souhaitez accorder des autorisations.

2.  Créer un groupe de rôles lié pour chaque groupe de rôle intégré. Les événements suivants se produisent lors de la création du groupe de rôles lié :
    
      - Les mêmes rôles que ceux affectés au groupe de rôles intégré sont attribués au nouveau groupe de rôles lié.
    
      - Le groupe de rôles lié est associé au groupe de sécurité universel dans la forêt étrangère.

3.  Créer des groupes de rôle liés pour tous les groupes de rôles personnalisés que vous avez créés.

4.  Vous pouvez également affecter des étendues personnalisées aux nouveaux groupes de rôles liés.

Pour plus d'informations sur l'exécution de cette procédure, consultez les rubriques suivantes :

  - [Créer des groupes de rôles lié qui reflètent les groupes de rôles intégrés](create-linked-role-groups-that-mirror-built-in-role-groups-exchange-2013-help.md)

  - [Gérer des groupes de rôles liés](manage-linked-role-groups-exchange-2013-help.md)

  - [Gérer des groupes de rôles](manage-role-groups-exchange-2013-help.md)

Si vous devez modifier le groupe de sécurité universel auquel un groupe de rôles lié est associé, consultez la rubrique [Gérer des groupes de rôles liés](manage-linked-role-groups-exchange-2013-help.md).

Quand une boîte aux lettres liée est créée, une stratégie d'affectation de rôles lui est automatiquement attribuée. Vous pouvez modifier la stratégie d'affectation de rôles attribuée à la boîte aux lettres liée, ou modifier la stratégie d'affectation de rôles attribuée aux boîtes aux lettres par défaut lors de leur création. Pour plus d’informations, consultez les rubriques suivantes :

  - [Modifier la stratégie d’attribution sur une boîte aux lettres](change-the-assignment-policy-on-a-mailbox-exchange-2013-help.md)

  - [Gérer les stratégies d’attribution des rôles](manage-role-assignment-policies-exchange-2013-help.md)

