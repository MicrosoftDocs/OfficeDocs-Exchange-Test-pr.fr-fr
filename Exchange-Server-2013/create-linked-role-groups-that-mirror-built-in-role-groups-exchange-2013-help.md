---
title: 'Créer des groupes de rôles lié qui reflètent les groupes de rôles intégrés: Exchange 2013 Help'
TOCTitle: Créer des groupes de rôles lié qui reflètent les groupes de rôles intégrés
ms:assetid: 89dfcbb3-0568-4bbf-a885-746b91ba307e
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dd876918(v=EXCHG.150)
ms:contentKeyID: 50478642
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Créer des groupes de rôles lié qui reflètent les groupes de rôles intégrés

 

_**Sapplique à :**Exchange Server 2013_

_**Dernière rubrique modifiée :**2012-10-03_

Par le biais des groupes de rôles de gestion liés dans Microsoft Exchange Server 2013, vous pouvez lier un groupe de rôles d’une forêt de ressources Exchange 2013 à un groupe de sécurité universel d’une forêt utilisateur étrangère. Ceci est utile lorsque vous voulez que les administrateurs disposant d’un compte dans la forêt utilisateur gèrent les serveurs exécutant Exchange dans la forêt de ressources. Pour plus d’informations sur les groupes de rôles liés, voir [Présentation des groupes de rôles de gestion](understanding-management-role-groups-exchange-2013-help.md).

Par défaut, Exchange 2013 inclut un certain nombre de groupes de rôles intégrés qui vous autorisent à gérer différentes fonctionnalités et fonctions de travail. Chaque groupe de rôles est conçu pour accorder les autorisations propres à chaque fonctionnalité et fonction de travail. Toutefois, ces groupes de rôles ne peuvent pas être liés aux groupes de sécurité universels dans une forêt étrangère. Ils peuvent contenir uniquement des utilisateurs et groupes de sécurité universels à partir de la forêt de ressources locales. Heureusement, il est possible de répliquer ces groupes de rôles intégrés à l’aide des groupes de rôles liés.

Vous pouvez recréer chaque groupe de rôles intégré en tant que groupe de rôles lié. Tous les rôles et toutes les étendues de gestion attribués à chaque groupe de rôles sont ajoutés au nouveau groupe de rôles lié. Pour plus d’informations sur les rôles et les étendues de gestion, voir les rubriques suivantes :

  - [Présentation des rôles de gestion](understanding-management-roles-exchange-2013-help.md)

  - [Présentation des portées du rôle de gestion](understanding-management-role-scopes-exchange-2013-help.md)

Souhaitez-vous rechercher les autres tâches de gestion relatives aux groupes des rôles ? Consultez la rubrique [Autorisations](permissions-exchange-2013-help.md).

## Ce qu’il faut savoir avant de commencer ?

  - Durée d’exécution estimée de chaque procédure : 10 minutes

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l’entrée « Groupes de rôles » dans la rubrique [Autorisations pour la gestion des rôles](role-management-permissions-exchange-2013-help.md).

  - Vous devez utiliser l’environnement de ligne de commande Exchange Management Shell pour effectuer ces procédures.

  - La configuration d’un groupe de rôles lié nécessite une approbation unilatérale entre la forêt Active Directory de ressources dans laquelle résidera le groupe de rôles lié et la forêt Active Directory étrangère où résideront les utilisateurs ou les groupes de sécurité universels. La forêt de ressources doit faire confiance à la forêt étrangère.

  - Vous devez posséder les informations suivantes sur la forêt étrangère Active Directory :
    
      - **Informations d’identification**   Vous devez posséder un nom d’utilisateur et un mot de passe pour accéder à la forêt étrangère Active Directory. Ces informations sont utilisées avec le paramètre *LinkedCredential* sur la cmdlet**New-RoleGroup**. Ces informations sont obtenues en exécutant la cmdlet **Get-Credential**. Le format du nom d’utilisateur est le suivant : *domaine*\\*nomutilisateur*.
    
      - **Contrôleur de domaine**   Vous devez bénéficier d’un nom de domaine complet (FQDN) d’un Active Directorycontrôleur de domaine dans la forêt étrangèreActive Directory. Ces informations sont utilisées avec le paramètre *LinkedDomainController* sur la cmdlet**New-RoleGroup**.
    
      - **Groupe de sécurité universelle étranger**   Vous devez posséder le nom entier d’un groupe de sécurité universelle dans la forêt Active Directory étrangère qui contient les membres que vous souhaitez associer avec le groupe de rôles liés. Ces informations sont utilisées avec le paramètre *LinkedForeignGroup* sur la cmdlet**New-RoleGroup**.

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

<table>
<thead>
<tr class="header">
<th><img src="images/Bb125224.tip(EXCHG.150).gif" title="Conseil" alt="Conseil" />Conseil :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.</td>
</tr>
</tbody>
</table>


## Utiliser l’environnement Shell pour créer les groupes de rôles liés qui répliquent les groupes de rôles intégrés

Chacune des sections suivantes vous montre comment recréer chaque groupe de rôles en tant que groupe de rôles lié. Complétez les procédures de chaque section pour recréer tous les groupes de rôles intégrés en tant que groupes de rôles liés.

## Créer le groupe de rôles lié Gestion de l’organisation

Pour recréer le groupe de rôles Gestion de l’organisation en tant que groupe de rôles lié, utilisez une procédure différente de celle utilisée pour recréer d’autres groupes de rôles intégrés. Ceci en raison du fait que le groupe de rôles Gestion de l’organisation a des attributions de rôles de délégation entre lui et tous les rôles de gestion. Une étape supplémentaire est nécessaire pour recréer les attributions de rôles de délégation.

1.  Créez un groupe de sécurité universel dans la forêt étrangère qui sera lié au groupe de rôles Gestion de l’organisation.

2.  Stockez les informations d’identification de la forêt Active Directory étrangère dans une variable.
    
        $ForeignCredential = Get-Credential

3.  Enregistrez tous les rôles attribués au groupe de rôles Gestion de l’organisation dans une variable.
    
        $OrgMgmt  = Get-RoleGroup "Organization Management"

4.  Créez le groupe de rôles lié Gestion de l’organisation et ajoutez les rôles attribués au groupe de rôles intégré Gestion de l’organisation.
    
        New-RoleGroup "Organization Management - Linked" -LinkedForeignGroup <name of foreign USG> -LinkedDomainController <FQDN of foreign Active Directory domain controller> -LinkedCredential $ForeignCredential -Roles $OrgMgmt.Roles

5.  Supprimez toutes les attributions normales entre le nouveau groupe de rôles lié Gestion de l’organisation et les rôles d’utilisateur final My\*.
    
        Get-ManagementRoleAssignment -RoleAssignee "Organization Management - Linked" -Role My* | Remove-ManagementRoleAssignment

6.  Ajoutez les attributions de rôles de délégation entre le nouveau groupe de rôles lié Gestion de l’organisation et tous les rôles de gestion.
    
        Get-ManagementRole | New-ManagementRoleAssignment -SecurityGroup "Organization Management - Linked" -Delegating

Cet exemple part du principe que les valeurs suivantes sont utilisées pour chaque paramètre :

  - **LinkedForeignGroup** `Organization Management Administrators`

  - **LinkedDomainController** `DC01.users.contoso.com`

À l’aide des valeurs précédentes, cet exemple montre comment recréer le groupe de rôles Gestion de l’organisation en tant que groupe de rôles lié.

    $ForeignCredential = Get-Credential
    $OrgMgmt  = Get-RoleGroup "Organization Management"
    New-RoleGroup "Organization Management - Linked" -LinkedForeignGroup "Organization Management Administrators" -LinkedDomainController DC01.users.contoso.com -LinkedCredential $ForeignCredential -Roles $OrgMgmt.Roles
    Get-ManagementRoleAssignment -RoleAssignee "Organization Management - Linked" -Role My* | Remove-ManagementRoleAssignment
    Get-ManagementRole | New-ManagementRoleAssignment -SecurityGroup "Organization Management - Linked" -Delegating

## Créer tous les autres groupes de rôles liés

Pour recréer les groupes de rôles intégrés (autres que le groupe de rôles Gestion de l’organisation) en tant que groupes de rôles liés, utilisez la procédure suivante pour chaque groupe.

1.  Créez un groupe de sécurité universel dans la forêt étrangère pour chaque groupe de rôles qui sera lié à chaque nouveau groupe de rôles.

2.  Stockez les informations d’identification de la forêt Active Directory étrangère dans une variable. Vous ne devez effectuer cette opération qu’une seule fois.
    
        $ForeignCredential = Get-Credential

3.  Récupérez une liste de groupes de rôles à l’aide de la cmdlet suivante.
    
        Get-RoleGroup

4.  Pour chaque groupe de rôles, autre que le groupe de rôles Gestion de l’organisation, procédez de la façon suivante.
    
        $RoleGroup = Get-RoleGroup <name of role group to re-create>
        New-RoleGroup "<role group name> - Linked" -LinkedForeignGroup <name of foreign USG> -LinkedDomainController <FQDN of foreign Active Directory domain controller> -LinkedCredential $ForeignCredential -Roles $RoleGroup.Roles

5.  Répétez l’étape précédente pour chaque groupe de rôles intégré à recréer en tant que groupe de rôles lié.

Cet exemple part du principe que les valeurs suivantes sont utilisées pour chaque paramètre :

  - **LinkedDomainController** `DC01.users.contoso.com`

  - **Groupes de rôles intégrés à recréer en tant que groupes de rôles liés** `Recipient Management, Server Management`

  - **Groupe étranger pour le groupe de rôles lié Gestion des destinataires** `Recipient Management Administrators`

  - **Groupe étranger pour le groupe de rôles lié Gestion des serveurs** `Server Management Administrators`

À l’aide des valeurs précédentes, cet exemple montre comment recréer les groupes de rôles Gestion des serveurs et Gestion des destinataires en tant que groupes de rôles liés.

    $ForeignCredential = Get-Credential
    Get-RoleGroup
    $RoleGroup = Get-RoleGroup "Recipient Management"
    New-RoleGroup "Recipient Management - Linked" -LinkedForeignGroup "Recipient Management Administrators" -LinkedDomainController DC01.users.contoso.com -LinkedCredential $ForeignCredential -Roles $RoleGroup.Roles
    $RoleGroup = Get-RoleGroup "Server Management"
    New-RoleGroup "Server Management - Linked" -LinkedForeignGroup "Server Management Administrators" -LinkedDomainController DC01.users.contoso.com -LinkedCredential $ForeignCredential -Roles $RoleGroup.Roles

## Autres tâches

Après avoir créé des groupes de rôles liés, vous souhaiterez probablement :

ajouter des membres aux groupes de sécurité universels étrangers à l’aide des utilisateurs et ordinateurs Active Directory dans la forêt étrangère.

supprimer des membres des groupes de rôles intégrés. Pour plus d’informations, consultez la rubrique [Gérer les membres de groupes de rôles](manage-role-group-members-exchange-2013-help.md).

Ajouter, supprimer ou modifier l’étendue des rôles sur les groupes de rôles liés. Pour plus d’informations, consultez la rubrique [Gérer des groupes de rôles](manage-role-groups-exchange-2013-help.md).

Créez des groupes de rôles liés supplémentaires. Pour plus d’informations, consultez la rubrique [Gérer des groupes de rôles liés](manage-linked-role-groups-exchange-2013-help.md).

