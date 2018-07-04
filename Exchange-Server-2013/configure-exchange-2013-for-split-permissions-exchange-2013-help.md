---
title: 'Configurer Exchange 2013 pour les autorisations divisées: Exchange 2013 Help'
TOCTitle: Configurer Exchange 2013 pour les autorisations divisées
ms:assetid: 8c74f893-a6f3-4869-8571-3bc0f662cc87
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dd638155(v=EXCHG.150)
ms:contentKeyID: 50478658
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configurer Exchange 2013 pour les autorisations divisées

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2015-04-07_

Les autorisations fractionnées activent deux groupes distincts, tels que les administrateurs Active Directory et les administrateurs Microsoft Exchange Server 2013, pour gérer leurs services, objets et attributs respectifs. Les administrateurs Active Directory gèrent les principaux de sécurité, tels que les utilisateurs, qui fournissent les autorisations permettant d’accéder à une forêt Active Directory. Les administrateurs Exchange gèrent les attributs relatifs à Exchange sur les objets Active Directory, ainsi que la création et la gestion d’objets spécifiques à Exchange.

Microsoft Exchange Server 2013 offre les types suivants de modèle d’autorisations fractionnées :

  - **Autorisations fractionnées RBAC**   Les autorisations permettant de créer les principaux de sécurité dans la partition du domaine Active Directory sont contrôlées via la méthode RBAC (contrôle d’accès basé sur les rôles). Seuls les membres des groupes de rôles appropriés peuvent créer des principaux de sécurité.

  - **autorisations fractionnées Active Directory**   Les autorisations pour créer des principaux de sécurité dans la partition du domaine Active Directory sont totalement supprimées de tout utilisateur, service ou serveur Exchange. Aucune option n’est fournie dans le contrôle RBAC pour créer des principaux de sécurité. Dans Active Directory, ces derniers doivent être créés à l’aide des outils de gestion Active Directory.
    
    > [!NOTE]
    > Les autorisations fractionnées Active Directory sont disponibles dans les organisations qui exécutent Microsoft Exchange Server 2010 Service Pack 1 (SP1) ou ultérieur, Exchange 2013, ou les deux versions d’Exchange.


Le modèle que vous choisissez va dépendre de la structure et des besoins de votre organisation. Choisissez la procédure ci-après qui s’applique au modèle que vous souhaitez configurer. Nous vous recommandons d’utiliser le modèle d’autorisations fractionnées RBAC. En effet, ce modèle s’avère sensiblement plus souple tout en assurant le même niveau de séparation de l’administration que les autorisations fractionnées Active Directory.

Pour plus d’informations sur les autorisations partagées et fractionnées, voir [Présentation des autorisations fractionnées](understanding-split-permissions-exchange-2013-help.md).

Pour plus d’informations sur les groupes de rôle de gestion, les rôles de gestion et les attributions de rôles de gestion de délégation, voir les rubriques suivantes :

  - [Présentation du contrôle d'accès basé sur un rôle](understanding-role-based-access-control-exchange-2013-help.md)

  - [Présentation des groupes de rôles de gestion](understanding-management-role-groups-exchange-2013-help.md)

  - [Présentation des rôles de gestion](understanding-management-roles-exchange-2013-help.md)

  - [Présentation des attributions de rôles de gestion](understanding-management-role-assignments-exchange-2013-help.md)

Souhaitez-vous rechercher les autres tâches de gestion relatives aux autorisations ? Consultez la rubrique [Autorisations avancées](advanced-permissions-exchange-2013-help.md).

## Ce qu’il faut savoir avant de commencer ?

  - Durée d’exécution estimée de chaque procédure : 5 minutes

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l’entrée « Autorisations fractionnées Active Directory » de la rubrique [Autorisations pour la gestion des rôles](role-management-permissions-exchange-2013-help.md).

  - Vous devez utiliser Windows PowerShell, l'interface de commande Windows ou les deux pour exécuter ces procédures. Pour plus d’informations, voir chaque procédure.

  - Si votre organisation dispose de serveurs Exchange 2010, le modèle d’autorisations que vous sélectionnez doit s’appliquer à ces serveurs.

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.


## Que souhaitez-vous faire ?

## Passer aux autorisations fractionnées RBAC

Vous pouvez configurer votre organisation Exchange 2013 pour les autorisations fractionnées RBAC. Une fois terminé, seuls les administrateurs Active Directory pourront créer les entités de sécurité Active Directory. Cela signifie que les administrateurs Exchange ne pourront pas utiliser les cmdlets suivantes :

  - **New-Mailbox**

  - **New-MailContact**

  - **New-MailUser**

  - **New-RemoteMailbox**

  - **Remove-Mailbox**

  - **Remove-MailContact**

  - **Remove-MailUser**

  - **Remove-RemoteMailbox**

Les administrateurs Exchange pourront uniquement gérer les attributs Exchange sur les entités de sécurité Active Directory existants. Toutefois, ils pourront gérer des objets spécifiques à Exchange, tels que les règles de transport et les groupes de distribution. Pour plus d’informations, consultez la section relative aux autorisations fractionnées RBAC dans la rubrique [Présentation des autorisations fractionnées](understanding-split-permissions-exchange-2013-help.md).

Pour configurer les autorisations fractionnées dans Exchange 2013, vous devez attribuer le rôle Création du destinataire de messagerie et le rôle Création du groupe de sécurité et appartenance à un groupe de rôles contenant des membres qui sont administrateurs d’Active Directory. Vous devez ensuite supprimer les attributions entre ces rôles et tout groupe de rôles ou groupe de sécurité universelle qui contient les administrateurs d’Exchange.

Pour configurer les autorisations fractionnées RBAC, procédez comme suit :

1.  Si les autorisations fractionnées Active Directory sont actuellement configurées pour votre organisation, procédez comme suit à l’invite de commandes de l’environnement de ligne de commande Windows.
    
    1.  Désactivez les autorisations fractionnées Active Directory en exécutant la commande suivante à partir du support d’installation d’Exchange 2013.
        
            setup.exe /PrepareAD /ActiveDirectorySplitPermissions:false
    
    2.  Redémarrez les serveurs Exchange 2013 de l’entreprise ou attendez que le jeton d’accès Active Directory soit répliqué sur tous vos serveurs Exchange 2013.
        
        > [!NOTE]
        > Si votre organisation comporte des serveurs Exchange 2010, vous devez aussi les redémarrer.


2.  À partir de l’environnement de ligne de commande ExchangeManagement Shell, procédez comme suit :
    
    1.  Créez un groupe de rôles pour les administrateurs Active Directory. Non seulement la commande crée le groupe de rôles, mais elle crée aussi des attributions de rôle ordinaire entre le nouveau groupe de rôles et les rôles Création du destinataire de messagerie et Création du groupe de sécurité et appartenance.
        
            New-RoleGroup "Active Directory Administrators" -Roles "Mail Recipient Creation", "Security Group Creation and Membership"
        
        > [!NOTE]
        > Pour que les membres de ce groupe de rôles puissent créer des attributions de rôle, ajoutez le rôle de gestion des rôles. Vous n’avez pas à vous en occuper à ce stade. Toutefois, si vous souhaitez toujours attribuer le rôle Création du destinataire de messagerie ou le rôle Création du groupe de sécurité et appartenance à d’autres utilisateurs de rôle, le rôle de gestion des rôles doit être attribué à ce nouveau groupe de rôles. La procédure ci-après permet de configurer le groupe de rôles des administrateurs Active Directory en tant que seul groupe de rôles habilité à déléguer ces rôles.
    
    2.  Créez les attributions de rôle de délégation entre le nouveau groupe de rôles et les rôles Création du destinataire de messagerie et Création du groupe de sécurité et appartenance en exécutant les commandes suivantes.
        
            New-ManagementRoleAssignment -Role "Mail Recipient Creation" -SecurityGroup "Active Directory Administrators" -Delegating
            New-ManagementRoleAssignment -Role "Security Group Creation and Membership" -SecurityGroup "Active Directory Administrators" -Delegating
    
    3.  Ajoutez des membres au nouveau groupe de rôles à l’aide de la commande suivante.
        
            Add-RoleGroupMember "Active Directory Administrators" -Member <user to add>
    
    4.  Remplacez la liste des délégués dans le nouveau groupe de rôles, de sorte que seuls les membres du groupe de rôles peuvent ajouter ou supprimer des membres.
        
            Set-RoleGroup "Active Directory Administrators" -ManagedBy "Active Directory Administrators"
        
        > [!NOTE]
        > Les membres du groupe de rôles Gestion de l’organisation, ou ceux auxquels est attribué le rôle de gestion des rôles, soit directement soit via un autre groupe de rôles ou groupe de sécurité universelle, peuvent ignorer ce contrôle de sécurité des délégués. Si vous souhaitez empêcher tout administrateur Exchange de s’ajouter au nouveau groupe de rôles, vous devez supprimer l’attribution de rôle entre le rôle de gestion des rôles et les administrateurs Exchange, puis l’attribuer à un autre groupe.
    
    5.  Recherchez toutes les attributions de rôle ordinaire et de délégation concernant le rôle Création du destinataire de messagerie à l’aide de la commande suivante. La commande affiche uniquement le nom (**Name**), le rôle (**Role**) et les propriétés **RoleAssigneeName**.
        
            Get-ManagementRoleAssignment -Role "Mail Recipient Creation" | Format-Table Name, Role, RoleAssigneeName -Auto
    
    6.  À l’aide de la commande suivante, supprimez toutes les attributions de rôle ordinaire et de délégation concernant le rôle Création du destinataire de messagerie qui ne sont pas associées au nouveau groupe de rôle ou à tout autre groupe de rôle, groupe de sécurité universelle ou attribution directe que vous souhaitez conserver.
        
            Remove-ManagementRoleAssignment <Mail Recipient Creation role assignment to remove>
        
        > [!NOTE]
        > Pour supprimer l’ensemble des attributions de rôle ordinaire et de délégation du rôle Création du destinataire de messagerie dont dispose un utilisateur de rôle autre que le groupe des administrateurs Active Directory, exécutez la commande suivante. Le commutateur <em>WhatIf</em> vous permet d’afficher les attributions de rôles qui seront supprimées. Supprimez le commutateur <em>WhatIf</em> et réexécutez la commande pour supprimer les attributions de rôles.
        
            Get-ManagementRoleAssignment -Role "Mail Recipient Creation" | Where { $_.RoleAssigneeName -NE "Active Directory Administrators" } | Remove-ManagementRoleAssignment -WhatIf
    
    7.  Recherchez toutes les attributions de rôle ordinaire et de délégation concernant le rôle Création du groupe de sécurité et appartenance à l’aide de la commande suivante. La commande affiche uniquement le nom (**Name**), le rôle (**Role**) et les propriétés **RoleAssigneeName**.
        
            Get-ManagementRoleAssignment -Role "Security Group Creation and Membership" | Format-Table Name, Role, RoleAssigneeName -Auto
    
    8.  À l’aide de la commande suivante, supprimez toutes les attributions de rôle ordinaire et de délégation concernant le rôle Création du groupe de sécurité et appartenance qui ne sont pas associées au nouveau groupe de rôle ou à tout autre groupe de rôle, groupe de sécurité universelle ou attribution directe que vous souhaitez conserver.
        
            Remove-ManagementRoleAssignment <Security Group Creation and Membership role assignment to remove>
        
        > [!NOTE]
        > Vous pouvez utiliser la commande présentée dans la remarque précédente pour supprimer toutes les attributions de rôle ordinaire et de délégation concernant le rôle de création du groupe de sécurité et appartenance associées à tout utilisateur de rôle autre que le groupe de rôle des administrateurs Active Directory, comme indiqué dans l’exemple ci-après.
        
            Get-ManagementRoleAssignment -Role "Security Group Creation and Membership" | Where { $_.RoleAssigneeName -NE "Active Directory Administrators" } | Remove-ManagementRoleAssignment -WhatIf

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, consultez les rubriques suivantes :

  - [New-RoleGroup](https://technet.microsoft.com/fr-fr/library/dd638181\(v=exchg.150\))

  - [New-ManagementRoleAssignment](https://technet.microsoft.com/fr-fr/library/dd335193\(v=exchg.150\))

  - [Add-RoleGroupMember](https://technet.microsoft.com/fr-fr/library/dd638207\(v=exchg.150\))

  - [Set-RoleGroup](https://technet.microsoft.com/fr-fr/library/dd638182\(v=exchg.150\))

  - [Get-ManagementRoleAssignment](https://technet.microsoft.com/fr-fr/library/dd351024\(v=exchg.150\))

  - [Remove-ManagementRoleAssignment](https://technet.microsoft.com/fr-fr/library/dd351205\(v=exchg.150\))

## Passer aux autorisations fractionnées Active Directory

Vous pouvez configurer votre organisation Exchange 2013 pour les autorisations fractionnées Active Directory. Les autorisations fractionnées Active Directory suppriment totalement les autorisations permettant aux administrateurs et serveurs Exchange de créer des principaux de sécurité Active Directory ou de modifier des attributs non-Exchange sur ces objets. Une fois cette opération terminée, seuls les administrateurs Active Directory pourront créer les principaux de sécurité Active Directory. Cela signifie que les administrateurs Exchange ne pourront pas utiliser les cmdlets suivantes :

  - **Add-DistributionGroupMember**

  - **New-DistributionGroup**

  - **New-Mailbox**

  - **New-MailContact**

  - **New-MailUser**

  - **New-RemoteMailbox**

  - **Remove-DistributionGroup**

  - **Remove-DistributionGroupMember**

  - **Remove-Mailbox**

  - **Remove-MailContact**

  - **Remove-MailUser**

  - **Remove-RemoteMailbox**

  - **Update-DistributionGroupMember**

Les administrateurs et les serveurs Exchange pourront uniquement gérer les attributs Exchange sur les principaux de sécurité Active Directory existants. Cependant, ils seront en mesure de créer et de gérer des objets spécifiques d’Exchange, comme des règles de transport et des plans de numérotation de messagerie unifiée.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ673034.Caution(EXCHG.150).gif" title="Attention" alt="Attention" />Attention :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Une fois que vous activé les autorisations fractionnées Active Directory, les administrateurs et les serveurs Exchange ne peuvent plus créer de principaux de sécurité dans Active Directory ni gérer l’appartenance au groupe de distribution. Pour effectuer ces tâches, utilisez les outils de gestion Active Directory en vous assurant de bénéficier des autorisations Active Directory nécessaires. Avant de procéder à ces modifications, assurez-vous de bien en connaître les conséquences sur vos processus administratifs et les applications intégrées à Exchange 2013 ainsi que le modèle d’autorisation RBAC.<br />
Pour plus d’informations, consultez la section relative aux autorisations fractionnées Active Directory dans la rubrique <a href="understanding-split-permissions-exchange-2013-help.md">Présentation des autorisations fractionnées</a>.</td>
</tr>
</tbody>
</table>


Pour basculer des autorisations partagées ou fractionnées RBAC vers les autorisations fractionnées Active Directory, procédez comme suit :

1.  Dans une invite de commandes Windows, exécutez la commande suivante du support d’installation d’Exchange 2013 pour activer les autorisations fractionnées Active Directory.
    
        setup.exe /PrepareAD /ActiveDirectorySplitPermissions:true

2.  Si votre organisation dispose de plusieurs domaines Active Directory, vous devez exécuter `setup.exe /PrepareDomain` dans chacun des domaines enfant contenant des serveurs ou des objets Exchange ou exécuter `setup.exe /PrepareAllDomains` à partir d’un site disposant d’un serveur Active Directory pour chacun des domaines.

3.  Redémarrez les serveurs Exchange 2013 de l’entreprise ou attendez que le jeton d’accès Active Directory soit répliqué sur tous vos serveurs Exchange 2013.
    
    > [!NOTE]
    > Si votre organisation comporte des serveurs Exchange 2010, vous devez aussi les redémarrer.

