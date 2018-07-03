---
title: 'Configurer Exchange 2013 pour les autorisations partagées: Exchange 2013 Help'
TOCTitle: Configurer Exchange 2013 pour les autorisations partagées
ms:assetid: 7d119977-b420-4b66-acf0-0a978b188cdd
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dd638146(v=EXCHG.150)
ms:contentKeyID: 50478544
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configurer Exchange 2013 pour les autorisations partagées

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2015-04-07_

Les autorisations partagées vous permettent, en tant qu’administrateur de Microsoft Exchange Server 2013, de créer les principaux de sécurité Active Directory (les utilisateurs par exemple), puis de les configurer comme destinataires d’Exchange. À l’inverse des autorisations fractionnées, qui permettent de répartir les tâches de gestion entre les groupes d’administrateurs Exchange et d’administrateurs Active Directory, les autorisations partagées n’ont pas recours à la séparation des tâches.

Pour plus d’informations sur les autorisations de partage, voir [Présentation des autorisations fractionnées](understanding-split-permissions-exchange-2013-help.md).

Vous pouvez configurer les autorisations partagées dans votre organisation Exchange 2013 si les autorisations fractionnées ont été préalablement paramétrées. La procédure permettant d’activer les autorisations partagées varie selon que vous utilisez actuellement les autorisations de type RBAC (contrôle d’accès basé sur un rôle) ou les autorisations Active Directory. Choisissez la procédure ci-après qui s’applique à votre configuration actuelle. Si les conditions suivantes sont remplies, votre organisation utilise les autorisations partagées Active Directory :

  - L’unité d’organisation Groupes protégés de Microsoft Exchange existe.

  - Le groupe de sécurité Autorisations de Exchange Windows se trouve dans l’unité d’organisation Groupes protégés de Microsoft Exchange.

  - Le groupe de sécurité du sous-système approuvé Exchange est membre du groupe de sécurité Autorisations de Exchange Windows.

  - Il n’y a pas d’attributions de rôle de gestion ordinaire au rôle Création de destinataires de message ou au rôle Création et appartenance au groupe de sécurité.

Si vous n’avez jamais configuré les autorisations divisées pour votre organisation, vous n’avez pas besoin d’exécuter cette procédure. Exchange 2013 est configuré par défaut pour les autorisations partagées.

Pour plus d’informations sur les groupes de rôle de gestion, les rôles de gestion et la délégation des attributions de rôles de gestion, voir les rubriques suivantes :

  - [Présentation du contrôle d'accès basé sur un rôle](understanding-role-based-access-control-exchange-2013-help.md)

  - [Présentation des groupes de rôles de gestion](understanding-management-role-groups-exchange-2013-help.md)

  - [Présentation des rôles de gestion](understanding-management-roles-exchange-2013-help.md)

  - [Présentation des attributions de rôles de gestion](understanding-management-role-assignments-exchange-2013-help.md)

Souhaitez-vous rechercher les autres tâches de gestion relatives aux autorisations ? Consultez la rubrique [Autorisations avancées](advanced-permissions-exchange-2013-help.md).

## Ce qu’il faut savoir avant de commencer ?

  - Durée d’exécution estimée de chaque procédure : 5 minutes

  - Les procédures décrites dans cette rubrique requièrent des autorisations spécifiques. Consultez chaque procédure pour savoir quelles autorisations sont nécessaires.

  - Vous devez utiliser Windows PowerShell, l'interface de commande Windows ou les deux pour exécuter ces procédures. Pour plus d’informations, voir chaque procédure.

  - L’organisation Exchange 2013 doit être configurée pour accepter les autorisations fractionnées Active Directory ou RBAC.

  - Si votre organisation dispose de serveurs Microsoft Exchange Server 2010, le modèle d’autorisations que vous sélectionnez doit s’appliquer à ces serveurs.

  - Vous devez disposer des autorisations appropriées pour déléguer les rôles de gestion Création du destinataire de messagerie et Création du groupe de sécurité et appartenance au groupe de rôles de gestion Gestion de l’organisation ou à un autre groupe de rôles auquel est attribué le rôle Destinataires de message.

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.


## Que souhaitez-vous faire ?

## Passer des autorisations fractionnées RBAC aux autorisations partagées

Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l’entrée « Groupes de rôles » dans la rubrique [Autorisations pour la gestion des rôles](role-management-permissions-exchange-2013-help.md).

Pour passer des autorisations fractionnées RBAC aux autorisations partagées Exchange 2013, vous devez attribuer le rôle Création du destinataire de messagerie et le rôle Création du groupe de sécurité et appartenance à un groupe de rôles auquel est également attribué le rôle Destinataires de message et qui possède comme membres les administrateurs Exchange 2013. Dans la configuration des autorisations partagées par défaut, le groupe de rôles Gestion de l’organisation contient chacun de ces rôles. De ce fait, le groupe de rôles Gestion de l’organisation figure dans cette procédure.

## Configurer les autorisations partagées

Pour configurer les autorisations partagées dans le groupe de rôles Gestion de l’organisation, effectuez la procédure suivante en utilisant un compte doté des autorisations nécessaires pour déléguer les attributions de rôle du rôle Création du destinataire de messagerie et du rôle Création du groupe de sécurité et appartenance :

1.  Ajoutez les attributions de rôle de délégation des rôles Création du destinataire de messagerie et Création du groupe de sécurité et appartenance au groupe de rôles Gestion de l’organisation en exécutant les commandes suivantes.
    
        New-ManagementRoleAssignment -Role "Mail Recipient Creation" -SecurityGroup "Organization Management" -Delegating
        New-ManagementRoleAssignment -Role "Security Group Creation and Membership" -SecurityGroup "Organization Management" -Delegating
    
    > [!NOTE]
    > Le rôle de gestion des rôles doit être attribué au groupe de rôles (dans cette procédure, le groupe de rôle des administrateurs Active Directory) qui dispose des attributions de rôle de délégation pour les rôles Création du destinataire de messagerie et Création du groupe de sécurité et appartenance au groupe de rôles pour qu’il puisse exécuter la cmdlet <strong>New-ManagementRoleAssignment</strong>. L’utilisateur de rôle autorisé à déléguer le rôle de gestion des rôles doit attribuer ce rôle au groupe de rôles des administrateurs Active Directory.


2.  Ajoutez les attributions de rôle ordinaire du rôle Création du destinataire de messagerie aux groupes de rôles Gestion de l’organisation et Gestion des destinataires en exécutant les commandes suivantes.
    
        New-ManagementRoleAssignment -Role "Mail Recipient Creation" -SecurityGroup "Organization Management"
        New-ManagementRoleAssignment -Role "Security Group Creation and Membership" -SecurityGroup "Recipient Management"

3.  Ajoutez une attribution de rôle ordinaire du rôle Création du groupe de sécurité et appartenance au groupe de rôles Gestion de l’organisation en exécutant la commande suivante.
    
        New-ManagementRoleAssignment -Role "Security Group Creation and Membership" -SecurityGroup "Organization Management"

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [New-ManagementRoleAssignment](https://technet.microsoft.com/fr-fr/library/dd335193\(v=exchg.150\)).

## Supprimer les autorisations via les administrateurs d’Active Directory (facultatif)

Vous pouvez éventuellement supprimer les autorisations octroyées aux administrateurs Active Directory si vous ne souhaitez plus créer ou gérer des objets Active Directory via les outils de gestion Exchange. Pour supprimer les autorisations dont disposent les administrateurs Active Directory, effectuez cette procédure.

> [!NOTE]
> Même s’il vous est possible de supprimer les autorisations des administrateurs Active Directory de gérer des objets Active Directory via les outils de gestion Exchange, Active Directory les administrateurs peuvent continuer à gérer les objets Active Directory au moyen des outils de gestion Active Directory si leurs autorisations Active Directory le leur permettent. Cependant, ils ne sont pas en mesure de gérer les attributs spécifiques à Exchange dans les objets Active Directory. Pour plus d’informations, voir <a href="understanding-split-permissions-exchange-2013-help.md">Présentation des autorisations fractionnées</a>.


Pour supprimer les autorisations fractionnées liées à Exchange des administrateurs Active Directory, procédez comme suit :

1.  Au moyen de la commande suivante, supprimez les attributions de rôle ordinaire et de rôle de délégation qui attribuent le rôle Création du destinataire de messagerie au groupe de rôles ou au groupe de sécurité universelle qui contient comme membres les administrateurs Active Directory. Cette commande utilise le groupe de rôles des administrateurs Active Directory à titre d’exemple. Le commutateur *WhatIf* vous permet d’afficher les attributions de rôles qui seront supprimées. Supprimez le commutateur *WhatIf*, puis réexécutez la commande pour supprimer les attributions de rôles.
    
        Get-ManagementRoleAssignment -Role "Mail Recipient Creation" | Where { $_.RoleAssigneeName -EQ "Active Directory Administrators" } | Remove-ManagementRoleAssignment -WhatIf

2.  A l’aide de la commande suivante, supprimez les attributions de rôle ordinaire et de rôle de délégation qui attribuent le rôle Création du groupe de sécurité et appartenance au groupe de rôles ou au groupe de sécurité universelle qui contient comme membres les administrateurs Active Directory. Cette commande utilise le groupe de rôles des administrateurs Active Directory à titre d’exemple. Le commutateur *WhatIf* vous permet d’afficher les attributions de rôles qui seront supprimées. Supprimez le commutateur *WhatIf*, puis réexécutez la commande pour supprimer les attributions de rôles.
    
        Get-ManagementRoleAssignment -Role "Security Group Creation and Membership" | Where { $_.RoleAssigneeName -EQ "Active Directory Administrators" } | Remove-ManagementRoleAssignment -WhatIf

3.  Facultatif. Pour supprimer l’ensemble des autorisations Exchange associées aux administrateurs Active Directory, vous pouvez supprimer le groupe de rôles ou le groupe de sécurité universelle dont ils sont membres. Pour plus d’informations sur la suppression d’un groupe de rôles, voir [Gérer des groupes de rôles](manage-role-groups-exchange-2013-help.md).

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Get-ManagementRoleAssignment](https://technet.microsoft.com/fr-fr/library/dd351024\(v=exchg.150\)) et [Remove-ManagementRoleAssignment](https://technet.microsoft.com/fr-fr/library/dd351205\(v=exchg.150\)).

## Passer des autorisations fractionnées Active Directory aux autorisations partagées

Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l’entrée « Autorisations fractionnées Active Directory » de la rubrique [Autorisations pour la gestion des rôles](role-management-permissions-exchange-2013-help.md).

Pour passer des autorisations fractionnées Active Directory aux autorisations partagées Exchange 2013, vous devez réexécuter le programme d’installation d’Exchange afin de désactiver les autorisations fractionnées Active Directory dans l’organisation Exchange, puis créer des attributions de rôles entre un groupe de rôles et les rôles Création du destinataire de messagerie et Création du groupe de sécurité et appartenance. Dans la configuration des autorisations partagées par défaut, le groupe de rôles Gestion de l’organisation contient chacun de ces rôles. De ce fait, le groupe de rôles Gestion de l’organisation figure dans cette procédure.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159813.important(EXCHG.150).gif" title="Important" alt="Important" />Important :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>La commande setup.com dans cette procédure modifie Active Directory. Pour l’utiliser, vous devez utiliser un compte doté des autorisations requises. Ce compte peut être différent de celui disposant des autorisations pour créer les attributions de rôles via la cmdlet <strong>New-ManagementRoleAssignment</strong>. Utilisez le ou les comptes dotés des autorisations permettant d’exécuter chaque étape de la procédure.</td>
</tr>
</tbody>
</table>


Pour passer des autorisations fractionnées Active Directory aux autorisations partagées, procédez comme suit :

1.  Dans une invite de commandes Windows, exécutez la commande suivante du support d’installation d’Exchange 2013 pour désactiver les autorisations fractionnées Active Directory.
    
        setup.exe /PrepareAD /ActiveDirectorySplitPermissions:false

2.  Depuis l’environnement de ligne de commande Exchange Management Shell, exécutez les commandes suivantes pour ajouter des attributions de rôles ordinaires entre les rôles Création du destinataire de messagerie et Création du groupe de sécurité et gestion et les groupes de rôles Gestion de l’organisation et Gestion des destinataires.
    
        New-ManagementRoleAssignment "Mail Recipient Creation_Organization Management" -Role "Mail Recipient Creation" -SecurityGroup "Organization Management"
        New-ManagementRoleAssignment "Security Group Creation and Membership_Org Management" -Role "Security Group Creation and Membership" -SecurityGroup "Organization Management"
        New-ManagementRoleAssignment "Mail Recipient Creation_Recipient Management" -Role "Mail Recipient Creation" -SecurityGroup "Recipient Management"

3.  Redémarrez les serveurs Exchange 2013 dans votre organisation.
    
    > [!NOTE]
    > Si votre organisation comporte des serveurs Exchange 2010, vous devez aussi les redémarrer.


Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [New-ManagementRoleAssignment](https://technet.microsoft.com/fr-fr/library/dd335193\(v=exchg.150\)).

