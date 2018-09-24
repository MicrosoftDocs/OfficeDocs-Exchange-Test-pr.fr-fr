---
title: 'Gérer des groupes de rôles liés: Exchange 2013 Help'
TOCTitle: Gérer des groupes de rôles liés
ms:assetid: e2a07395-90c2-4d62-b15d-ac3ff28fe786
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ657502(v=EXCHG.150)
ms:contentKeyID: 50479401
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Gérer des groupes de rôles liés

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2012-10-09_

Vous pouvez utiliser un groupe de rôles de gestion liés pour permettre aux membres d’un groupe de sécurité universel (USG) d’une forêt Active Directory étrangère de gérer une organisation Microsoft Exchange Server 2013 au sein d’une forêt Active Directory de ressources. En associant un USG dans une forêt étrangère à un groupe de rôles liés, les membres de cet USG reçoivent les autorisations octroyées par les rôles de gestion attribués au groupe de rôles liés. Pour plus d’informations sur les groupes de rôles liés, voir [Présentation des groupes de rôles de gestion](understanding-management-role-groups-exchange-2013-help.md).

Pour créer et configurer des groupes de rôles liés, vous devez utiliser les cmdlets **New-RoleGroup** et **Set-RoleGroup**. Pour obtenir des informations détaillées sur la syntaxe et les paramètres, consultez les rubriques suivantes :

  - [New-RoleGroup](https://technet.microsoft.com/fr-fr/library/dd638181\(v=exchg.150\))

  - [Set-RoleGroup](https://technet.microsoft.com/fr-fr/library/dd638182\(v=exchg.150\))

Autres tâches de gestion relatives aux groupes de rôles, voir [Autorisations](permissions-exchange-2013-help.md).

## Ce qu’il faut savoir avant de commencer ?

  - Durée d’exécution estimée de chaque procédure : 5 à 10 minutes

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Groupes de rôles » dans la rubrique [Autorisations pour la gestion des rôles](role-management-permissions-exchange-2013-help.md).

  - Vous ne pouvez pas utiliser le Centre d’administration Exchange (CAE) pour créer ou configurer des groupes de rôles liés. Vous devez utiliser l’environnement de ligne de commande Exchange Management Shell.

  - Au minimum, la configuration d’un groupe de rôles liés requiert l’établissement d’une approbation unidirectionnelle entre la forêt de ressources Active Directory où réside le groupe de rôles liés et la forêt étrangère Active Directory où se trouvent les utilisateurs ou les USG. La forêt de ressources doit faire confiance à la forêt étrangère.

  - Vous devez posséder les informations suivantes sur la forêt étrangère Active Directory :
    
      - **Informations d’identification**   Vous devez posséder un nom d’utilisateur et un mot de passe pour accéder à la forêt étrangère Active Directory. Ces informations sont utilisées avec le paramètre *LinkedCredential* sur le cmdlets **New-RoleGroup** et **Set-RoleGroup**.
    
      - **Contrôleur de domaine**   Vous devez bénéficier d’un nom de domaine complet (FQDN) d’un Active Directorycontrôleur de domaine dans la forêt étrangèreActive Directory. Ces informations sont utilisées avec le paramètre *LinkedDomainController* sur le cmdlets **New-RoleGroup** et **Set-RoleGroup**.
    
      - **Groupe de sécurité universelle étranger**   Vous devez posséder le nom entier d’un groupe de sécurité universelle dans la forêt Active Directory étrangère qui contient les membres que vous souhaitez associer avec le groupe de rôles liés. Ces informations sont utilisées avec le paramètre *LinkedForeignGroup* sur les cmdlets **New-RoleGroup** et **Set-RoleGroup**.

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.


## Que souhaitez-vous faire ?

## Créer un groupe de rôles liés

## Utilisation du Shell pour créer un groupe de rôles liés non délimité

Pour créer un groupe de rôles liés et lui attribuer des rôles de gestion, procédez comme suit :

1.  Stockez les informations d’identification de la forêt Active Directory étrangère dans une variable.
    
    ```powershell
    $ForeignCredential = Get-Credential
    ```

2.  Créez le groupe de rôles liés à l’aide de la syntaxe suivante.
    
    ```powershell
    New-RoleGroup <role group name> -LinkedForeignGroup <name of foreign USG> -LinkedDomainController <FQDN of foreign Active Directory domain controller> -LinkedCredential $ForeignCredential -Roles <role1, role2, role3...>
    ```

3.  Ajoutez ou supprimez les membres depuis ou vers le groupe de sécurité universelle étranger en utilisant les ordinateurs et les utilisateurs Active Directory sur un ordinateur dans la forêt Active Directory étrangère.

Cet exemple effectue les opérations suivantes :

  - Récupération des informations d’identification pour la forêt Active Directory étrangère users.contoso.com. Ces informations d’identification sont utilisées pour vous connecter au contrôleur de domaine DC01.users.contoso.com dans la forêt étrangère.

  - Crée un groupe de rôles liés nommé Groupe de rôles de conformité dans la forêt de ressources où est installé Exchange 2013.

  - Relie le nouveau groupe de rôles à l’USG Administrateurs de conformité dans la forêt users.contoso.com Active Directory.

  - Attribue les rôles Règles de transport et Gestion de la journalisation au nouveau groupe de rôles liés.

<!-- end list -->

```powershell
$ForeignCredential = Get-Credential
```
```powershell
New-RoleGroup "Compliance Role Group" -LinkedForeignGroup "Compliance Administrators" -LinkedDomainController DC01.users.contoso.com -LinkedCredential $ForeignCredential -Roles "Transport Rules", "Journaling"
```

## Utilisation du Shell pour créer un groupe de rôles liés avec une portée de gestion personnalisée

Vous pouvez créer des groupes de rôles liés avec des portées de gestion de destinataires personnalisées, des portées de gestion de configuration personnalisées ou avec les deux. Pour créer un groupe de rôles liés et lui attribuer des rôles de gestion avec des portées personnalisées, procédez comme suit :

1.  Stockez les informations d’identification de la forêt Active Directory étrangère dans une variable.
    
    ```powershell
    $ForeignCredential = Get-Credential
    ```

2.  Créez le groupe de rôles liés à l’aide de la syntaxe suivante.
    
    ```powershell
    New-RoleGroup <role group name> -LinkedForeignGroup <name of foreign USG> -LinkedDomainController <FQDN of foreign Active Directory domain controller> -CustomConfigWriteScope <name of configuration scope> -CustomRecipientWriteScope <name of recipient scope> -LinkedCredential $ForeignCredential -Roles <role1, role2, role3...>
    ```

3.  Ajoutez ou supprimez les membres depuis ou vers le groupe de sécurité universelle étranger en utilisant les ordinateurs et les utilisateurs Active Directory sur un ordinateur dans la forêt Active Directory étrangère.

Cet exemple effectue les opérations suivantes :

  - Récupération des informations d’identification pour la forêt Active Directory étrangère users.contoso.com. Ces informations d’identification sont utilisées pour vous connecter au contrôleur de domaine DC01.users.contoso.com dans la forêt étrangère.

  - Crée un groupe de rôles liés nommé Groupe de rôles de conformité Seattle dans la forêt de ressources où est installé Exchange 2013.

  - Relie le nouveau groupe de rôles à l’USG Administrateurs de conformité Seattle dans la forêt users.contoso.com Active Directory.

  - Attribue les rôles Règles de transport et Gestion de journalisation au nouveau groupe de rôles liés avec la portée de destinataires personnalisée Destinataires Seattle.

<!-- end list -->

```powershell
$ForeignCredential = Get-Credential
```
```powershell
New-RoleGroup "Seattle Compliance Role Group" -LinkedForeignGroup "Seattle Compliance Administrators" -LinkedDomainController DC01.users.contoso.com -LinkedCredential $ForeignCredential -CustomRecipientWriteScope "Seattle Recipients" -Roles "Transport Rules", "Journaling"
```

Pour plus d’informations sur les étendues de gestion, voir [Présentation des portées du rôle de gestion](understanding-management-role-scopes-exchange-2013-help.md).

## Utilisation du Shell pour créer un groupe de rôles liés avec une portée OU

Vous pouvez créer des groupes de rôles liés qui utilisent une portée de destinataires OU. Pour créer un groupe de rôles liés et lui attribuer des rôles de gestion avec une portée OU, procédez comme suit :

1.  Stockez les informations d’identification de la forêt Active Directory étrangère dans une variable.
    
    ```powershell
    $ForeignCredential = Get-Credential
    ```

2.  Créez le groupe de rôles liés à l’aide de la syntaxe suivante.
    
    ```powershell
    New-RoleGroup <role group name> -LinkedForeignGroup <name of foreign USG> -LinkedDomainController <FQDN of foreign Active Directory domain controller> -LinkedCredential $ForeignCredential -RecipientOrganizationalUnitScope <OU name> -Roles <role1, role2, role3...>
    ```

3.  Ajoutez ou supprimez les membres depuis ou vers le groupe de sécurité universelle étranger en utilisant les ordinateurs et les utilisateurs Active Directory sur un ordinateur dans la forêt Active Directory étrangère.

Cet exemple effectue les opérations suivantes :

  - Récupération des informations d’identification pour la forêt Active Directory étrangère users.contoso.com. Ces informations d’identification sont utilisées pour vous connecter au contrôleur de domaine DC01.users.contoso.com dans la forêt étrangère.

  - Crée un groupe de rôles liés nommé Groupe de rôles de conformité Cadres dans la forêt de ressources où est installé Exchange 2013.

  - Relie le nouveau groupe de rôles à l’USG Administrateurs de conformité Cadres dans la forêt users.contoso.com Active Directory.

  - Attribue les rôles Règles de transport et Gestion de journalisation au nouveau groupe de rôles liés avec la portée de destinataires OU Cadres OU.

<!-- end list -->

```powershell
$ForeignCredential = Get-Credential
New-RoleGroup "Executives Compliance Role Group" -LinkedForeignGroup "Executives Compliance Administrators" -LinkedDomainController DC01.users.contoso.com -LinkedCredential $ForeignCredential -RecipientOrganizationalUnitScope "Executives OU" -Roles "Transport Rules", "Journaling"
```

Pour plus d’informations sur les étendues de gestion, voir [Présentation des portées du rôle de gestion](understanding-management-role-scopes-exchange-2013-help.md).

## Changer l'USG étranger sur un groupe de rôles liés

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour modifier le groupe de sécurité universel étranger associé à un groupe de rôles lié

Pour modifier le groupe de sécurité universel étranger associé à un groupe de rôles lié, effectuez les opérations suivantes :

1.  Stockez les informations d’identification de la forêt Active Directory étrangère dans une variable.
    
    ```powershell
    $ForeignCredential = Get-Credential
    ```

2.  Utilisez la syntaxe suivante pour modifier l'USG étranger sur le groupe de rôles liés existant.
    
    ```powershell
    Set-RoleGroup <role group name> -LinkedForeignGroup <name of foreign USG> -LinkedDomainController <FQDN of foreign Active Directory domain controller> -LinkedCredential $ForeignCredential 
    ```

Cet exemple effectue les opérations suivantes :

  - Récupération des informations d’identification pour la forêt Active Directory étrangère users.contoso.com. Ces informations d’identification sont utilisées pour vous connecter au contrôleur de domaine DC01.users.contoso.com dans la forêt étrangère.

  - Modification du groupe de sécurité universel étranger associé au groupe de rôles « Compliance Role Group » en « Regulatory Compliance Officers ».

<!-- end list -->

```powershell
$ForeignCredential = Get-Credential
Set-RoleGroup "Compliance Role Group" -LinkedForeignGroup "Regulatory Compliance Officers" -LinkedDomainController DC01.users.contoso.com -LinkedCredential $ForeignCredential
```

