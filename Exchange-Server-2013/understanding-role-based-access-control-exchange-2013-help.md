---
title: "Présentation du contrôle d'accès basé sur un rôle: Exchange 2013 Help"
TOCTitle: Présentation du contrôle d'accès basé sur un rôle
ms:assetid: fd268867-2ae5-441b-8103-7a7583eb2bbe
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dd298183(v=EXCHG.150)
ms:contentKeyID: 50479629
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Présentation du contrôle d'accès basé sur un rôle

 

_**Sapplique à :**Exchange Online, Exchange Server 2013_

_**Dernière rubrique modifiée :**2018-01-31_

Le *Role Based Access Control* (RBAC) constitue le modèle d’autorisations dans Microsoft Exchange Server 2013. Grâce au contrôle d’accès basé sur un rôle, vous n’avez pas besoin de modifier et de gérer les listes de contrôle d’accès, ce qui était le cas dans Exchange Server 2007. Les listes de contrôle d’accès impliquaient plusieurs contraintes dans Exchange 2007, notamment de modifier les listes de contrôle d’accès sans effets involontaires, de gérer tous les changements apportés aux listes par le biais des mises à niveau et de résoudre les problèmes liés à une utilisation non standard de ces mêmes listes.

Le contrôle d’accès basé sur un rôle vous permet de contrôler ce que les administrateurs et les utilisateurs finaux peuvent réaliser, tant à des niveaux élargis que granulaires. Le contrôle d’accès basé sur un rôle vous permet d’aligner plus étroitement les rôles que vous attribuez aux utilisateurs et aux administrateurs avec les rôles réels dont ils sont dotés au sein de votre organisation. Dans Exchange 2007, le modèle d’autorisations serveur s’appliquait uniquement aux administrateurs qui géraient l’infrastructure Exchange 2007. Dans Exchange 2013, le contrôle d’accès basé sur un rôle gère à présent les tâches administratives qu’il est possible de réaliser et la portée avec laquelle les utilisateurs peuvent désormais administrer leur boîte aux lettres et leurs groupes de distribution personnels.

Le contrôle d’accès basé sur un rôle dispose de deux méthodes principales pour attribuer des autorisations aux utilisateurs de votre organisation, selon que l’utilisateur soit un administrateur, un spécialiste ou un utilisateur final : la gestion des groupes de rôles et les stratégies d’attribution de rôle de gestion. Chaque méthode associe des utilisateurs aux autorisations dont ils ont besoin pour effectuer leurs tâches. Une troisième méthode plus avancée, l’attribution de rôle d’utilisateur directe, peut également être adoptée. Les sections qui suivent dans cette rubrique explique le contrôle d’accès basé sur un rôle et fournissent des exemples de son utilisation.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Cette rubrique traite de la fonctionnalité RBAC avancée. Si vous souhaitez gérer des autorisations Exchange 2013 de base, comme l’utilisation du centre d’administration Exchange pour ajouter et supprimer des membres dans les groupes de rôles, créer et modifier des groupes de rôles ou créer et modifier des stratégies d’attribution de rôles, consultez la rubrique <a href="permissions-exchange-2013-help.md">Autorisations</a>.</td>
</tr>
</tbody>
</table>


**Contenu de cette rubrique**

Groupes de rôles de gestion

Stratégies d'attribution de rôle de gestion

Attribution de rôle d'utilisateur directe

Résumé et exemples

Pour plus d'informations

## Groupes de rôles de gestion

*Les groupes de rôles de gestion* associent les rôles de gestion à un groupe d’administrateurs ou d’utilisateurs spécialisés. Les administrateurs gèrent une vaste organisation Exchange ou une configuration étendue de destinataires. Les utilisateurs spécialisés gèrent les fonctionnalités spécifiques d’Exchange, telles que la conformité. Ils peuvent également disposer de compétences de gestion limitées, telles que celles de membres du support technique, mais pas de droits d’administration étendus. Les groupes de rôles associent généralement les rôles de gestion administrative à l’aide desquels les administrateurs et les utilisateurs spécialisés peuvent gérer la configuration de leur organisation et de leurs destinataires. Par exemple, la possibilité pour les administrateurs de gérer des destinataires ou d’exploiter les fonctionnalités de détection est contrôlée au moyen des groupes de rôles.

L’ajout ou la suppression d’utilisateurs dans ou à partir des groupes de rôles dépend de la manière dont vous attribuez le plus souvent des autorisations aux administrateurs ou aux utilisateurs spécialistes. Pour plus d’informations, voir [Présentation des groupes de rôles de gestion](understanding-management-role-groups-exchange-2013-help.md).

Les groupes de rôles comprennent les composants suivants qui définissent ce que les administrateurs et les utilisateurs spécialistes peuvent réaliser :

  - **Groupe de rôles de gestion**   Le *groupe de rôles de gestion* est un groupe de sécurité universel spécial qui comprend des boîtes aux lettres, des utilisateurs, des groupes de sécurité universels et d’autres groupes de rôles appartenant à ce groupe de rôles. C’est là que vous ajoutez et supprimez des membres et c’est aussi là où les rôles de gestion sont attribués. L’association de tous les rôles sur un groupe de rôles définit tout ce que les utilisateurs ajoutés à un groupe de rôles peuvent gérer dans l’organisation Exchange.

  - **Rôle de gestion**   Un *rôle de gestion* est un conteneur pour un groupe d’entrées de rôle de gestion. Les rôles sont utilisés pour définir des tâches spécifiques pouvant être effectuées par les membres d’un groupe de rôles qui est affecté au rôle. Une *entrée de rôle de gestion* est une applet de commande, un script ou une autorisation spéciale qui permet d’effectuer chaque tâche spécifique dans un rôle. Pour plus d’informations, voir [Présentation des rôles de gestion](understanding-management-roles-exchange-2013-help.md).

  - **Attribution de rôle de gestion**   Une *attribution de rôle de gestion* représente le lien entre un rôle et un groupe de rôles. L’attribution d’un rôle à un groupe de rôles permet aux membres du groupe d’utiliser des cmdlets et des paramètres définis dans le rôle. Les attributions de rôles peuvent utiliser des étendues de gestion pour contrôler les endroits où l’attribution peut être utilisée. Pour plus d’informations, voir [Présentation des attributions de rôles de gestion](understanding-management-role-assignments-exchange-2013-help.md).

  - **Étendue de rôle de gestion**   Une *étendue de rôle de gestion* représente l’étendue de l’influence ou de l’impact sur une attribution de rôle. Quand un rôle avec une étendue est attribué à un groupe de rôles, l’étendue de gestion vise spécifiquement les objets que l’attribution est autorisée à gérer. L’attribution et son étendue sont ensuite accordées aux membres du groupe de rôles et limitent ce que peuvent gérer ces membres. Une étendue peut être composée d’une liste de serveurs ou de bases de données, d’unités d’organisation ou de filtres sur des objets serveur, base de données ou destinataire. Pour plus d’informations, voir [Présentation des portées du rôle de gestion](understanding-management-role-scopes-exchange-2013-help.md).

Lorsque vous ajoutez un utilisateur à un groupe de rôle, cet utilisateur bénéficie de tous les rôles attribués au groupe de rôles. Si des étendues sont appliquées à l’une des attributions de rôles entre le groupe de rôles et les rôles, ces étendues déterminent la configuration serveur ou les destinataires que l’utilisateur peut gérer.

Si vous souhaitez redéfinir les rôles attribués aux groupes de rôles, vous devez modifier les attributions de rôles qui lient les groupes de rôles aux rôles. À moins que les attributions intégrées dans Exchange 2013 ne correspondent pas à vos besoins, vous n’aurez pas à modifier ces attributions. Pour plus d’informations, voir [Présentation des attributions de rôles de gestion](understanding-management-role-assignments-exchange-2013-help.md).

Pour plus d’informations sur les groupes de rôles, voir la rubrique [Présentation des groupes de rôles de gestion](understanding-management-role-groups-exchange-2013-help.md).

## Stratégie d’attribution des rôles de gestion

Les stratégies d’attribution des rôles de gestion associent les rôles de gestion d’utilisateur final aux utilisateurs. Les stratégies d’attribution des rôles déterminent les rôles chargés de contrôler ce qu’un utilisateur peut effectuer au moyen de sa boîte aux lettres ou de son groupe de distribution. Ces rôles ne gèrent pas les fonctionnalités qui ne sont pas directement associées à l’utilisateur. Lorsque vous créez une stratégie d’attribution de rôle, vous définissez tout ce qu’un utilisateur peut effectuer avec sa boîte aux lettres. Par exemple, une stratégie d’attribution de rôle peut permettre à un utilisateur d’afficher le nom complet, ainsi que de configurer la messagerie vocale et des règles de boîte de réception. Une autre stratégie d’attribution de rôle peut autoriser un utilisateur à modifier l’adresse, à utiliser des messages textuels et à configurer des groupes de distribution. Tous les utilisateurs munis d’une boîte aux lettres Exchange 2013, y compris les administrateurs, reçoivent une stratégie d’attribution de rôle par défaut. Vous pouvez décider de la stratégie d’attribution de rôle à attribuer par défaut, choisir les éléments que la stratégie d’attribution de rôle par défaut doit inclure, remplacer les valeurs par défaut pour certaines boîtes aux lettres ou choisir de n’attribuer aucune stratégie d’attribution de rôle par défaut.

L’attribution d’un utilisateur à une stratégie d’attribution dépend de la manière dont vous gérez le plus souvent des autorisations pour permettre à des utilisateurs de gérer eux-mêmes leurs options de boîte aux lettres et de groupe de distribution. Pour plus d’informations, voir [Présentation des stratégies d’attribution de rôle de gestion](understanding-management-role-assignment-policies-exchange-2013-help.md).

Les stratégies d’attribution de rôle présentent les composants suivants. Ils déterminent ce que les utilisateurs peuvent réaliser avec leurs boîtes aux lettres personnelles. Notez que certains de ces mêmes composants s’appliquent également aux groupes de rôles. Lorsqu’ils sont utilisés dans le cadre des stratégies d’attribution de rôle, ces composants peuvent uniquement permettre aux utilisateurs de gérer leurs boîtes aux lettres personnelles :

  - **Stratégie d’attribution de rôle de gestion**   La *stratégie d’attribution de rôle de gestion* est un objet spécial dans Exchange 2013. La stratégie d’attribution de rôle est associée aux utilisateurs lorsque leur boîte aux lettres est créée ou si vous modifiez la stratégie d’attribution de rôle sur une boîte aux lettres. C’est également ce que vous attribuez pour les rôles de gestion des utilisateurs finaux. L’association de tous les rôles sur une stratégie d’attribution de rôle définit tout ce que l’utilisateur peut gérer dans sa boîte aux lettres ou ses groupes de distribution.

  - **Rôle de gestion**   Un *rôle de gestion* est un conteneur pour un groupe d’entrées de rôles de gestion. Les rôles sont utilisés pour définir les tâches spécifiques qu’un utilisateur peut effectuer avec sa boîte aux lettres ou les groupes de distribution. Une *entrée de rôle de gestion* est une cmdlet, un script ou une autorisation spéciale qui permet d’effectuer chaque tâche spécifique dans un rôle de gestion. Vous pouvez uniquement utiliser des rôles des utilisateurs finaux avec les stratégies d’attribution de rôle. Pour plus d’informations, voir [Présentation des rôles de gestion](understanding-management-roles-exchange-2013-help.md).

  - **Attribution de rôle de gestion**   Une *attribution de rôle de gestion* représente le lien entre un rôle et une stratégie d’attribution de rôle. L’attribution d’un rôle à une stratégie d’attribution de rôle permet l’utilisation des cmdlets et des paramètres définis dans le rôle. Lorsque vous créez une attribution de rôle entre une stratégie d’attribution de rôle et un rôle, vous ne pouvez spécifier aucune étendue. L’étendue appliquée par l’attribution est `Self` ou `MyGAL`. Toutes les attributions de rôles ont une étendue limitée à la boîte aux lettres ou aux groupes de distribution de l’utilisateur. Pour plus d’informations, voir [Présentation des attributions de rôles de gestion](understanding-management-role-assignments-exchange-2013-help.md).

Si vous souhaitez redéfinir les rôles attribués aux stratégies d’attribution de rôle, vous devez modifier les attributions de rôles qui lient les stratégies d’attribution de rôle aux rôles. À moins que les attributions intégrées dans Exchange 2013 ne correspondent pas à vos besoins, vous n’aurez pas à modifier ces attributions. Pour plus d’informations, voir [Présentation des attributions de rôles de gestion](understanding-management-role-assignments-exchange-2013-help.md).

Pour plus d’informations, voir [Présentation des stratégies d’attribution de rôle de gestion](understanding-management-role-assignment-policies-exchange-2013-help.md).

## Attribution de rôle d’utilisateur directe

L’*attribution de rôle d’utilisateur directe* est une méthode avancée qui permet d’attribuer des rôles de gestion directement à un utilisateur ou un groupe de sécurité universel sans passer par un groupe de rôles ou une stratégie d’attribution de rôle. Les attributions de rôles directes peuvent être utiles lorsque vous devez préciser un ensemble d’autorisations détaillées pour un seul et unique utilisateur (et personne d’autre). En revanche, l’utilisation d’attributions directes peut considérablement accroître la complexité de votre modèle d’autorisations. Si un utilisateur change de poste ou quitte la société, vous devez manuellement supprimer les attributions et les ajouter au nouvel employé. Nous vous recommandons d’utiliser des groupes de rôles pour attribuer des autorisations à des administrateurs et des utilisateurs spécialistes et des stratégies d’attribution de rôle pour attribuer des autorisations à des utilisateurs.

Pour plus d’informations sur l’attribution de rôle directe, voir [Présentation des attributions de rôles de gestion](understanding-management-role-assignments-exchange-2013-help.md).

## Résumé et exemples

La figure ci-dessous présente les composants du contrôle d’accès basé sur un rôle et la manière dont ils s’adaptent les uns aux autres :

  - Groupes de rôles :
    
      - Un ou plusieurs administrateurs peuvent être membres d’un groupe de rôles. Ils peuvent aussi être membres de plusieurs groupe de rôles.
    
      - Le groupe de rôles se voit attribuer un ou plusieurs rôles. Ces attributions de rôles lient le groupe de rôles à un ou plusieurs rôles administratifs qui définissent les tâches qu’il est possible de réaliser.
    
      - Les attributions de rôles peuvent contenir des étendues de gestion qui définissent la géographie dans laquelle les utilisateurs du groupe de rôles peuvent effectuer des opérations. Les étendues déterminent là où les utilisateurs du groupe de rôles peuvent modifier la configuration.

  - Stratégies d’attribution de rôles :
    
      - Un ou plusieurs utilisateurs peuvent être associés à une stratégie d’attribution de rôle.
    
      - La stratégie d’attribution de rôle se voit attribuer un ou plusieurs rôles. Ces attributions de rôles lient la stratégie d’attribution de rôle à un ou plusieurs rôles d’utilisateur final. Ces rôles d’utilisateur final définissent ce que l’utilisateur est autorisé à configurer dans sa boîte aux lettres.
    
      - Les attributions de rôles entre les stratégies d’attribution de rôle et les rôles sont munies d’étendues intégrées qui limitent l’étendue des attributions à la boîte aux lettres ou aux groupes de distribution personnels de l’utilisateur.

  - Attribution de rôle directe (méthode avancée) :
    
      - Une attribution de rôle peut être directement créée entre un utilisateur ou un groupe de sécurité universel et un ou plusieurs rôles. Le rôle définit les tâches que l’utilisateur ou le groupe de sécurité universel peut effectuer.
    
      - Les attributions de rôles peuvent contenir des étendues de gestion qui définissent la géographie dans laquelle l’utilisateur ou le groupe de sécurité universel peut effectuer des opérations. Les étendues déterminent à quel emplacement l’utilisateur ou le groupe de sécurité universel peut modifier la configuration.

**Vue d’ensemble du contrôle d’accès basé sur un rôle**

![Relations des composants RBAC](images/Dd298183.1dee60cc-1d58-4d36-b34e-639f091e7a56(EXCHG.150).jpg "Relations des composants RBAC")

Comme le démontre la figure ci-avant, de nombreux composants du contrôle d’accès basé sur un rôle sont liés entre eux. La manière dont chaque composant s’imbrique dans un autre définit les autorisations appliquées à chaque administrateur ou utilisateur. Les exemples ci-dessous offrent un contexte supplémentaire sur la façon dont les groupes de rôles et les stratégies d’attribution de rôle sont utilisées au sein d’une organisation.

## Sabine, l’administratrice

Sabine travaille en qualité d’administratrice au sein de la PME Contoso. Travaillant au bureau de Vancouver, elle est responsable de la gestion des destinataires de l’entreprise. Lorsque le modèle d’autorisations de la société Contoso a été élaboré, Sabine était membre du groupe de rôles personnalisé Gestion des destinataires - Vancouver. Le groupe de rôles personnalisé Gestion des destinataires - Vancouver est le groupe qui correspond le mieux aux responsabilités de son poste qui impliquent notamment la création et la suppression des destinataires (des boîtes aux lettres et des contacts, par exemple), la gestion des membres des groupes de distribution et des propriétés des boîtes aux lettres et bien d’autres tâches encore.

En plus du groupe de rôles personnalisé Gestion des destinataires - Vancouver, Sabine a également besoin d’une stratégie d’attribution de rôle pour gérer les paramètres de configuration de sa boîte aux lettres personnelle. Les administrateurs de l’organisation ont décidé que tous les utilisateurs, à l’exception de la direction, bénéficieront des mêmes autorisations pour la gestion de leurs boîtes aux lettres personnelles. Ils peuvent configurer leur messagerie vocale, configurer des stratégies de rétention et modifier les informations de leurs adresses. La stratégie d’attribution de rôle proposée par défaut dans Exchange 2013 reflète désormais ces besoins.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Vous avez peut-être remarqué que Sabine est membre du groupe de rôles personnalisé Gestion des destinataires - Vancouver, ce qui devrait lui conférer les autorisations nécessaires pour gérer sa boîte aux lettres. C’est bel et bien le cas ; cependant, le groupe de rôles ne fournit pas toutes les autorisations nécessaires pour gérer l’ensemble des fonctionnalités de sa boîte aux lettres. Les autorisations requises pour gérer les paramètres de la messagerie vocale et de la stratégie de rétention ne sont pas incluses dans son groupe de rôles. Elles sont disponibles uniquement par le biais de la stratégie d’attribution de rôle qui lui est attribuée par défaut.</td>
</tr>
</tbody>
</table>


Pour permettre cela, envisagez le recours au groupe de rôles qui confère à Sabine des autorisations administratives pour les destinataires de Vancouver :

1.  Un groupe de rôles personnalisé appelé Gestion des destinataires - Vancouver a été créé. Les événements survenus lors de sa création sont les suivants :
    
    1.  Tous les rôles de gestion également attribués au groupe de rôles intégré Gestion des destinataires étaient attribués au groupe de rôles. Les utilisateurs ajoutés au groupe de rôle personnalisé Gestion des destinataires - Vancouver disposent ainsi des mêmes autorisations que les utilisateurs ajoutés au groupe de rôles Gestion des destinataires. Toutefois, la procédure suivante limite le cadre d’application de ces autorisations.
    
    2.  Une étendue de gestion personnalisée pour les destinataires de Vancouver a été créée. Elle correspond uniquement aux destinataires qui travaillent sur ce site. Cette étendue permet de filtrer des informations portant sur la ville de l’utilisateur ou sur d’autres données uniques.
    
    3.  Le groupe de rôles a été créé avec l’étendue de gestion personnalisée des destinataires de Vancouver. Les administrateurs ajoutés au groupe de rôles personnalisé Gestion des destinataires - Vancouver disposent donc d’autorisations de gestion des destinataires complètes mais n’en bénéficient que pour les destinataires basés à Vancouver.
    
    Pour plus d’informations sur la création d’un groupe de rôles personnalisés, voir [Gérer des groupes de rôles](manage-role-groups-exchange-2013-help.md).

2.  Sabine est ensuite ajoutée en tant que membre du groupe de rôles personnalisé Gestion des destinataires - Vancouver.
    
    Pour plus d’informations sur l’ajout de membres d’un groupe de rôles, voir [Gérer les membres de groupes de rôles](manage-role-group-members-exchange-2013-help.md).

Pour donner à Sabine la possibilité de gérer les paramètres de sa boîte aux lettres personnelle, une stratégie d’attribution de rôle doit être configurée avec les autorisations requises. La stratégie d’attribution de rôle par défaut est utilisée pour fournir aux utilisateurs les autorisations qui leur sont nécessaires pour configurer leur propre boîte aux lettres. Tous les rôles d’utilisateur final sont supprimés de la stratégie d’attribution de rôles par défaut, à l’exception des rôles `MyBaseOptions`, `MyContactInformation`, `MyVoicemail` et `MyRetentionPolicies`. `MyBaseOptions` est inclus, car ce rôle de gestion fournit les fonctionnalités utilisateur de base dans Outlook Web App, telles que les règles boîte de réception, la configuration de calendrier et d’autres tâches.

Il ne reste rien d’autre à faire puisque la stratégie d’attribution de rôle par défaut a déjà été attribuée à Sabine. Ainsi donc, les modifications apportées à cette stratégie d’attribution de rôle sont appliquées immédiatement à sa boîte aux lettres et à toutes les autres boîtes aux lettres auxquelles la stratégie d’attribution de rôle par défaut a également été attribuée.

Pour plus d’informations sur la personnalisation de la stratégie d’attribution de rôle par défaut, voir [Gérer les stratégies d’attribution des rôles](manage-role-assignment-policies-exchange-2013-help.md).

## Joe, le spécialiste

Comme Sabine, Joe travaille au sein de la société Contoso. Il est responsable des opérations de découverte légale, de la définition des stratégies de rétention et de la configuration des règles de transport et de la journalisation pour l’ensemble de l’organisation. Comme dans le cas de Sabine, lorsque le modèle d’autorisations de la société Contoso a été élaboré, Joe a été ajouté aux groupes de rôles conformes à ses responsabilités professionnelles. Le groupe de rôles Gestion des enregistrements apporte à Joe les autorisations qui lui sont nécessaires pour configurer les stratégies de rétention, la journalisation et les règles de transport. Le groupe de rôles Gestion de la découverte lui offre la possibilité d’effectuer des recherches dans des boîtes aux lettres.

Comme Jane, Joe a également besoin d’autorisations pour gérer sa propre boîte aux lettres. Il reçoit les mêmes autorisations que Jane : Il peut configurer sa messagerie vocale et ses stratégies de rétention et modifier ses données d’adresse.

Pour accorder à Joe les autorisations requises pour réaliser les tâches qui lui incombent, Joe est ajouté aux groupes de rôles Gestion des enregistrements et Gestion de la découverte. Les groupes de rôles n’ont en aucune manière besoin d’être modifiés puisqu’ils lui donnent déjà les autorisations dont il a besoin et les étendues de gestion qui s’y appliquent couvrent la totalité de l’organisation.

Pour plus d’informations sur l’ajout d’un utilisateur à un groupe de rôles, voir [Gérer les membres de groupes de rôles](manage-role-group-members-exchange-2013-help.md).

La même stratégie d’attribution de rôle par défaut appliquée à la boîte aux lettres de Sabine l’est également à la boîte aux lettres de Joe. Il dispose ainsi de toutes les autorisations nécessaires pour les fonctionnalités qu’il est autorisé à gérer au sein de sa boîte aux lettres.

## Isabelle, Vice-présidente

Isabelle est la vice-présidente de la branche Marketing de Contoso. En tant que membre de l’équipe dirigeante de Contoso, elle bénéficie d’un plus grand nombre d’autorisations que l’utilisateur moyen. Cela inclut les autorisations qui lui permettent de gérer sa boîte aux lettres à une exception près : Isabelle n’est pas autorisée à gérer les stratégies de rétention qui lui sont propres pour des raisons de conformité légale. Elle peut configurer sa messagerie vocale, modifier ses informations de contact, modifier les données de son profil, créer et gérer ses groupes de distribution et s’ajouter à ou se supprimer de groupes de distribution existants dont d’autres utilisateurs seraient détenteurs.

Par conséquent, Isabelle bénéficie d’autorisations différentes pour sa boîte aux lettres. La plupart des utilisateurs de Contoso se voient attribuer la stratégie d’attribution de rôle par défaut. Cependant, les membres de l’équipe dirigeante bénéficient de la stratégie d’attribution de rôle réservée à la direction. Les opérations réalisées pour créer la stratégie d’attribution de rôle personnalisée sont les suivantes :

1.  Une stratégie d’attribution de rôle appelée « Direction » est créée. Les rôles `MyBaseOptions`, `MyContactInformation`, `MyVoicemail`, `MyProfileInformation`, `MyDistributionGroupMembership` et ` MyDistributionGroups` sont attribués à la stratégie d’attribution de rôle. Le rôle `MyBaseOptions` est inclus, car il fournit les fonctionnalités utilisateur de base dans Outlook Web App, telles que les règles de boîte de réception, la configuration de calendrier et d’autres tâches.

2.  La stratégie d’attribution de rôle Direction est ensuite attribuée manuellement à Isabelle.

La boîte aux lettres d’Isabelle dispose à présent des autorisations accordées par la stratégie d’attribution de rôle Direction. Toutes les modifications apportées à cette stratégie d’attribution de rôle sont appliquées automatiquement à sa boîte aux lettres et à toutes les autres boîtes aux lettres auxquelles la même stratégie d’attribution de rôle est attribuée.

## Pour plus d’informations

[Gérer les stratégies d’attribution des rôles](manage-role-assignment-policies-exchange-2013-help.md)

[Modifier la stratégie d’attribution sur une boîte aux lettres](change-the-assignment-policy-on-a-mailbox-exchange-2013-help.md)

