---
title: 'Présentation des attributions de rôles de gestion: Exchange 2013 Help'
TOCTitle: Présentation des attributions de rôles de gestion
ms:assetid: 1dc33dd6-52fb-4852-a5ce-027bc73e1d8f
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dd335131(v=EXCHG.150)
ms:contentKeyID: 50477732
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Présentation des attributions de rôles de gestion

 

_**Sapplique à :** Exchange Online, Exchange Server 2013_

_**Dernière rubrique modifiée :** 2012-10-04_

Une *attribution de rôle de gestion*, qui fait partie du modèle d’autorisation du contrôle d’accès basé sur un rôle dans Microsoft Exchange Server 2013, est le lien existant entre un rôle de gestion et un utilisateur de rôle. Un *utilisateur de rôle* est un groupe de rôles, une stratégie d’attribution de rôles, un utilisateur ou un groupe universel de sécurité (USG). Un rôle doit être attribué à un utilisateur de rôle pour entrer en vigueur. Pour plus d'informations sur le contrôle d'accès basé sur un rôle, consultez la rubrique [Présentation du contrôle d'accès basé sur un rôle](understanding-role-based-access-control-exchange-2013-help.md).

> [!NOTE]
> Cette rubrique traite de la fonctionnalité RBAC avancée. Si vous souhaitez gérer des autorisations Exchange 2013 de base, comme l’utilisation du centre d’administration Exchange pour ajouter et supprimer des membres dans les groupes de rôles, créer et modifier des groupes de rôles ou créer et modifier des stratégies d’attribution de rôles, consultez la rubrique <a href="permissions-exchange-2013-help.md">Autorisations</a>.


Cette rubrique explique l’attribution de rôles aux groupes de rôles, les stratégies d’attribution de rôles et l’attribution de rôles directs aux utilisateurs et groupes universels de sécurité. Elle n’aborde pas l’attribution de groupes de rôles ou des stratégies d’attribution de rôles pour les utilisateurs. Pour plus d’informations sur les groupes de rôles et les stratégies d’attribution de rôles, méthode recommandée pour attribuer des autorisations aux utilisateurs, consultez les rubriques suivantes :

  - [Présentation des groupes de rôles de gestion](understanding-management-role-groups-exchange-2013-help.md)

  - [Présentation des stratégies d’attribution de rôle de gestion](understanding-management-role-assignment-policies-exchange-2013-help.md)

Vous pouvez créer les types d’attributions de rôles suivants, expliqués en détail plus loin dans cette rubrique :

  - Attributions de rôles normales et de délégation

  - Attributions de rôles exclusives

## Gestion des attributions de rôles

Lorsque vous modifiez des attributions de rôles, les changements que vous apportez seront probablement effectués entre les stratégies des groupes de rôles et les stratégies d’attribution de rôles. En ajoutant des attributions de rôles aux utilisateurs de rôles, en en supprimant ou en en modifiant, il est possible de contrôler les autorisations accordées à vos administrateurs et utilisateurs, par l’activation et la désactivation la gestion des fonctionnalités liées.

Vous voudrez peut-être attribuer directement des rôles à des utilisateurs ou à des groupes universels de sécurité. Il existe une tâche plus avancée qui vous permet de définir à un niveau détaillé les autorisations accordées à vos utilisateurs. Bien que cela vous apporte de la flexibilité, cela augmente aussi la complexité de votre modèle d’autorisations. Par exemple, si l’utilisateur change de fonction, vous devrez peut-être réattribuer manuellement à un autre utilisateur les rôles qui lui ont été attribués. C’est pourquoi nous vous recommandons d’utiliser des groupes de rôles et des stratégies d’attributions de rôles pour donner des autorisations à vos utilisateurs. Vous pouvez attribuer les rôles à un groupe de rôles ou à une stratégie d’attribution de rôles puis simplement ajouter ou supprimer des membres du groupe de rôles, ou bien modifier les stratégies d’attribution de rôles si nécessaire.

Vous pouvez ajouter, supprimer et activer des attributions de rôles, modifier l’étendue de gestion sur une attribution de rôle existante et transférer les attributions de rôles vers d’autres utilisateurs de rôles. Le processus d’attribution de rôles à des groupes de rôles, à des stratégies d’attribution de rôles, à des utilisateurs et à des groupes universels de sécurité est en grande partie identique pour chaque utilisateur de rôle. Les seules exceptions sont les suivantes :

  - Les stratégies d’attribution de rôles peuvent uniquement recevoir des rôles de gestion des utilisateurs finaux.

  - Les stratégies d’attribution de rôle ne peuvent pas recevoir des attributions de rôles de délégation.

  - Vous ne pouvez pas spécifier d’étendue de gestion lors de la création d’une attribution de rôles pour des stratégies d’attribution de rôles.

Pour plus d’informations sur la gestion des attributions de rôles, consultez les rubriques suivantes :

  - Groupes de rôles :
    
      - [Gérer des groupes de rôles](manage-role-groups-exchange-2013-help.md)

  - Stratégies d’attribution de rôles :
    
      - [Gérer les stratégies d’attribution des rôles](manage-role-assignment-policies-exchange-2013-help.md)
    
      - [Modifier une attribution de rôle](change-a-role-assignment-exchange-2013-help.md)

  - Utilisateurs et groupes universels de sécurité :
    
      - [Ajouter un rôle à un utilisateur ou un groupe de sécurité universel](add-a-role-to-a-user-or-usg-exchange-2013-help.md)
    
      - [Supprimer un rôle d’un utilisateur ou un groupe universel de sécurité](remove-a-role-from-a-user-or-usg-exchange-2013-help.md)
    
      - [Modifier une attribution de rôle](change-a-role-assignment-exchange-2013-help.md)
    
      - [Modifier l’étendue d’un rôle](change-a-role-scope-exchange-2013-help.md)
    
      - [Déléguer les attributions de rôles](delegate-role-assignments-exchange-2013-help.md)

## Attributions de rôles normales et de délégation

Les attributions de rôles normales permettent à l’utilisateur de rôles d’accéder aux entrées du rôle de gestion disponibles par le rôle de gestion associé. Si plusieurs rôles de gestion sont attribués à un utilisateur de rôle, les entrées du rôle de gestion de chaque rôle de gestion sont regroupées et appliquées. Autrement dit, si des rôles de règles de transport et de journalisation sont attribués à un utilisateur de rôle, les rôles sont associés et l’ensemble des entrées du rôle de gestion associé est attribué à l’utilisateur de rôle. Si l’utilisateur de rôle est un groupe de rôles ou une stratégie d’attribution de rôles, les autorisations fournies par les rôles sont ensuite accordées aux utilisateurs attribués au groupe de rôles ou à la stratégie d’attribution de rôles. Pour plus d’informations sur les rôles de gestion et les entrées des rôles, consultez la rubrique [Présentation des rôles de gestion](understanding-management-roles-exchange-2013-help.md).

Les attributions de rôles de délégation ne donnent pas accès à la gestion des fonctionnalités. Les attributions de rôles de délégation permettent à un utilisateur de rôle d’attribuer le rôle spécifié aux autres utilisateurs de rôle. Si l’utilisateur de rôle est un groupe de rôles, n’importe quel membre du groupe de rôles peut attribuer le rôle à un autre utilisateur de rôle. Par défaut, seul le groupe de rôles Gestion de l’organisation peut attribuer des rôles à d’autres utilisateurs de rôles. Seul l’utilisateur ayant installé Exchange 2013 est membre du groupe de rôles Gestion de l’organisation par défaut. Vous pouvez toutefois y ajouter d’autres utilisateurs si nécessaire, ou créer d’autres groupes de rôles et attribuer des attributions de rôles de délégation à ces groupes.

> [!NOTE]
> Les attributions de rôles de délégation permettent aux utilisateurs de rôles de déléguer des rôles de gestion à d’autres utilisateurs de rôles. Cela ne permet pas aux utilisateurs de déléguer des groupes de rôles. Pour plus d’informations sur la délégation des groupes de rôles, consultez la rubrique <a href="understanding-management-role-groups-exchange-2013-help.md">Présentation des groupes de rôles de gestion</a>.


Si vous désirez qu’un utilisateur puisse gérer une fonctionnalité et attribuer à d’autres utilisateurs le rôle qui lui donne l’autorisation d’utiliser la fonctionnalité, attribuez comme suit :

1.  Une attribution de rôle normale pour chaque rôle de gestion qui autorise l’accès aux fonctionnalités à gérer.

2.  Une attribution de rôle de délégation à chaque rôle de gestion dont vous autorisez l’attribution à d’autres utilisateurs de rôles.

Il n’est pas nécessaire que les attributions de rôles normales et de délégation soient identiques pour un utilisateur de rôle. Par exemple, un utilisateur est membre d’un groupe de rôles auquel a été attribué le rôle de règles de transport à l’aide d’une attribution de rôles normale. Cela permet à l’utilisateur de gérer la fonctionnalité des règles de transport. Cependant, l’utilisateur ne reçoit pas d’attribution de rôle de délégation pour le rôle règles de transport. L’utilisateur ne peut donc pas attribuer ce rôle aux autres utilisateurs. Toutefois, l’utilisateur est membre d’un groupe de rôles auquel a été attribué le rôle de gestion de journalisation à l’aide d’une attribution de rôles de délégation. Le groupe de rôles dont l’utilisateur est membre ne possède pas d’attribution de rôles normale pour le rôle de journalisation car il possède l’attribution de rôles de délégation. L’utilisateur peut attribuer le rôle à d’autres utilisateurs de rôle.

## Étendues de gestion

Lorsque vous créez une attribution de rôle de gestion normale ou de délégation, vous avez la possibilité de créer l’attribution avec une étendue de gestion pour limiter les objets pouvant être manipulés par l’utilisateur. Vous pouvez créer des étendues de destinataire ou de configuration. Les étendues de destinataire vous permettent de déterminer qui manipule les boîtes aux lettres, les utilisateurs de messagerie, les groupes de distribution, etc. Les étendues de configuration vous permettent de déterminer qui, des utilisateurs, peut manipuler les serveurs et les bases de données.

Les étendues de destinataire et de configuration vous permettent de segmenter la gestion des objets serveur, base de données ou destinataire dans votre organisation. Par exemple, une étendue de destinataire peut être ajoutée à une attribution de rôle de sorte que les administrateurs de Vancouver peuvent uniquement gérer les destinataires de la même succursale. Un étendue de configuration serveur peut être ajoutée à une attribution de rôle différente afin que les administrateurs de Sydney puissent uniquement gérer les serveurs de leur site Active Directory.

Les étendues permettent d’attribuer des autorisations à des groupes d’utilisateurs et vous permettent d’orienter les administrateurs vers les sites sur lesquels ils peuvent exercer leurs fonctions. Cela vous permet de créer un modèle d’autorisations qui correspond à vos frontières géographiques ou organisationnelles.

Vous pouvez créer une attribution avec une étendue prédéfinie ou vous pouvez ajouter une étendue personnalisée à l’attribution. Les étendues prédéfinies, comme la limitation d’un utilisateur à ses boîte aux lettres ou groupes de distribution uniquement, peuvent s’appliquer à l’aide des options disponibles sur l’attribution elle-même. Vous pouvez également créer une étendue de destinataire ou de configuration personnalisée, puis l’ajouter à l’attribution de rôle. Les étendues personnalisées vous offrent une plus grande précision sur les objets inclus.

Vous ne pouvez pas spécifier d’étendues prédéfinies et personnalisées sur la même attribution. De plus, vous ne pouvez pas mélanger des étendues exclusives et normales sur la même attribution.

Chaque attribution de rôle ne peut comporter qu’une seule étendue de destinataire et de configuration. Si vous souhaitez appliquer plusieurs étendues de destinataire ou de configuration à un utilisateur de rôle pour le même rôle de gestion, vous devez alors créer plusieurs attributions de rôles.

Les attributions de rôles ne sont pas limitées aux étendues de destinataire et de configuration qui sont définies sur le rôle proprement dit, que celles-ci soient personnalisées ou prédéfinies. Ces étendues sont qualifiées d’implicites. Toute attribution de rôle n’ayant aucune étendue prédéfinie ou personnalisée hérite des étendues implicites du rôle à laquelle elle est associée.

Pour plus d’informations sur les étendues, consultez la rubrique [Présentation des portées du rôle de gestion](understanding-management-role-scopes-exchange-2013-help.md).

## Attributions de rôles exclusives

Les attributions de rôles exclusives sont créées lorsque vous associez une étendue exclusive à une attribution de rôle. Les étendues exclusives fonctionnent comme des étendues normales et permettent aux utilisateurs de rôles de gérer les destinataires correspondant à l’étendue exclusive. Cependant, contrairement aux étendues normales, tous les autres utilisateurs de rôle ne peuvent gérer le destinataire, même si le destinataire correspond à des étendues appliquées à leurs attributions de rôles. Cela peut s’avérer particulièrement utile lorsque vous désirez limiter la gestion d’un destinataire auprès de quelques administrateurs. Seuls ces administrateurs-là peuvent gérer le destinataire et l’accès est refusé à l’ensemble des autres administrateurs.

Imaginons, par exemple, les cas de figure suivants :

  - John est cadre chez Contoso. Sa boîte aux lettres correspond à une étendue exclusive appelée Utilisateurs VIP associée à l’attribution exclusive Limité aux VIP.

  - La boîte aux lettres de John fait aussi partie d’une étendue normale appelée Utilisateurs de Redmond associée à l’attribution normale Administration de Redmond.

  - Bill est administrateur associé à l’attribution exclusive Limité aux VIP.

  - Chris est administrateur associé à l’attribution normale Administration de Redmond.

La boîte aux lettres de John correspondant à l’étendue exclusive Utilisateurs VIP, seul Bill peut gérer sa boîte aux lettres. Même si la boîte aux lettres de John fait aussi partie de l’étendue normale Utilisateurs de Redmond, Chris n’est pas associé à l’attribution exclusive Limité aux VIP. Par conséquent, Exchange refuse que Chris gère la boîte aux lettres de John. Pour que Chris gère la boîte aux lettres de John, Chris doit recevoir une attribution exclusive contenant une étendue exclusive correspondant à la boîte aux lettres de John.

Pour plus d’informations, consultez la rubrique [Présentation des étendues exclusives](understanding-exclusive-scopes-exchange-2013-help.md).

