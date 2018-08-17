---
title: 'Déléguer les attributions de rôles: Exchange 2013 Help'
TOCTitle: Déléguer les attributions de rôles
ms:assetid: ed2d00d9-90c9-49dc-ab8a-cd791569aeed
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dd351237(v=EXCHG.150)
ms:contentKeyID: 50479496
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Déléguer les attributions de rôles

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2012-10-02_

La délégation de rôles de gestion permet aux bénéficiaires d'un rôle d'attribuer un rôle de gestion spécifique à d'autres groupes de rôles de gestion, à des stratégies d'attribution de rôles de gestion, à des utilisateurs ou à des groupes de sécurité universels. Par défaut, seuls les membres du groupe de rôles de gestion Gestion de l'organisation peuvent déléguer des attributions de rôles. Lorsqu'une nouvelle installation de Microsoft Exchange Server 2013 est déployée, seul le compte d'utilisateur qui a servi à installer Exchange 2013 est membre du groupe de rôles Gestion de l'organisation.

Si vous déléguez une attribution de rôle de délégation à un groupe de rôles, les membres de ce groupe de rôles peuvent déléguer le rôle de gestion associé à d'autres utilisateurs.

> [!IMPORTANT]
> La délégation d'attributions de rôle n'accorde pas aux bénéficiaires d'un rôle les autorisations octroyées par ce rôle, elle leur permet uniquement d'attribuer le rôle à d'autres. Si vous souhaitez accorder les autorisations octroyées par le rôle au bénéficiaire de ce rôle, vous devez également créer une attribution de rôle normale. Pour créer une attribution de rôle normale, consultez les rubriques suivantes :
> <a href="manage-role-groups-exchange-2013-help.md">Gérer des groupes de rôles</a>
> <a href="manage-role-assignment-policies-exchange-2013-help.md">Gérer les stratégies d’attribution des rôles</a>
> <a href="add-a-role-to-a-user-or-usg-exchange-2013-help.md">Ajouter un rôle à un utilisateur ou un groupe de sécurité universel</a>


> [!NOTE]
> Cette rubrique décrit la délégation d'attribution de rôle de gestion. Si vous souhaitez déléguer une attribution de rôle permettant à son bénéficiaire d'ajouter des membres à des groupes de rôles et d'en supprimer, ce qui est la méthode recommandée de délégation, voir <a href="manage-role-groups-exchange-2013-help.md">Gérer des groupes de rôles</a>.


Pour plus d'information sur les attributions de rôle normales et la délégation d'attributions de rôle de gestion, voir [Présentation des attributions de rôles de gestion](understanding-management-role-assignments-exchange-2013-help.md).

Souhaitez-vous rechercher les autres tâches de gestion relatives à la gestion des autorisations ? Consultez la rubrique [Autorisations avancées](advanced-permissions-exchange-2013-help.md).

## Ce qu’il faut savoir avant de commencer ?

  - Durée estimée de la procédure : 5 minutes

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Attribution des rôles » dans la rubrique [Autorisations pour la gestion des rôles](role-management-permissions-exchange-2013-help.md).

  - Vous devez utiliser l’environnement de ligne de commande Exchange Management Shell pour effectuer ces procédures.

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.


## Utiliser l'environnement de ligne de commande Exchange Management Shell pour déléguer un rôle de gestion

Vous pouvez créer des attributions de rôle de délégation à l'aide des mêmes portées prédéfinies, portées de destinataire ou de serveur filtrées, portées de serveur basées sur une liste et portées d'unité d'organisation pouvant être utilisées pour créer des portées exclusives ou normales. La seule différence entre la création d'une attribution de rôle normale et celle d'une attribution de rôle de délégation est l'ajout du commutateur *Delegating* à la commande. Pour plus d'informations sur la création d'attributions de rôle, voir les rubriques suivantes :

  - [Gérer des groupes de rôles](manage-role-groups-exchange-2013-help.md)

  - [Ajouter un rôle à un utilisateur ou un groupe de sécurité universel](add-a-role-to-a-user-or-usg-exchange-2013-help.md)

> [!NOTE]
> Vous ne pouvez pas créer une attribution de rôle de délégation dans une stratégie d'attribution de rôle de gestion.


Cet exemple crée une attribution de rôle de délégation pour permettre aux membres du groupe de rôles Senior Admins d'attribuer le rôle Mail Recipients à un utilisateur dans l'organisation Exchange.

    New-ManagementRoleAssignment -Role "Mail Recipients" -SecurityGroup "Senior Admins" -Name "Mail Recipients_Senior Admin - Delegate" -Delegating

Cet exemple crée une attribution de rôle de délégation pour permettre aux membres du groupe de rôles Senior Admins d'attribuer le rôle Mail Recipients seulement aux utilisateurs de l'unité d'organisation Sales/Users dans le domaine contoso.com.

    New-ManagementRoleAssignment -Role "Mail Recipients" -SecurityGroup "Senior Admins" -Name "Mail Recipients_Senior Admins - Delegate" -RecipientOrganizationalUnitScope contoso.com/sales/users -Delegating

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [New-ManagementRoleAssignment](https://technet.microsoft.com/fr-fr/library/dd335193\(v=exchg.150\)).

