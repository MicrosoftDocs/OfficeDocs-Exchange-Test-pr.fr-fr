---
title: 'Activation ou désactivation des carnets d’adresses hiérarchiques: Exchange 2013 Help'
TOCTitle: Activation ou désactivation des carnets d’adresses hiérarchiques
ms:assetid: b4c3a175-ce5e-4bfb-a4a0-92d25f3644b3
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Ff607473(v=EXCHG.150)
ms:contentKeyID: 50479037
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Activation ou désactivation des carnets d’adresses hiérarchiques

 

_**Sapplique à :** Exchange Online, Exchange Server 2013_

_**Dernière rubrique modifiée :** 2016-12-09_

Vous pouvez configurer un carnet d’adresses hiérarchique, une fonctionnalité dont les utilisateurs disposent dans Microsoft Outlook 2010 ou versions ultérieures. Avec un carnet d’adresses hiérarchique, les utilisateurs peuvent rechercher des destinataires dans leur organisation Exchange en utilisant une hiérarchie d’organisation basée sur la structure hiérarchique ou d’ancienneté. Pour en savoir plus sur les carnets d’adresses hiérarchiques, consultez la rubrique [Carnets d’adresses hiérarchiques](hierarchical-address-books-exchange-2013-help.md).

## Ce qu’il faut savoir avant de commencer ?

  - Durée d'exécution estimée : 1 heure.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Groupes de distribution » dans la rubrique [Autorisations des destinataires](recipients-permissions-exchange-2013-help.md).

  - Vous ne pouvez pas utiliser le Centre d’administration Exchange (CAE) pour effectuer cette procédure. Vous devez utiliser l'environnement de ligne de commande Exchange Management Shell.

  - Avant de commencer, parcourez la rubrique [Carnets d’adresses hiérarchiques](hierarchical-address-books-exchange-2013-help.md). Vous devez savoir si un carnet d’adresses hiérarchique convient à votre organisation Exchange.

  - Assurez-vous que vous comprenez la manière dont les unités d’organisation, les groupes, les utilisateurs et les contacts sont actuellement configurés dans votre organisation Exchange.

  - Étudiez les cmdlets et les paramètres associés dans le tableau ci-dessous. Ces éléments sont indispensables à la configuration d’un carnet d’adresses hiérarchique.
    
    
    <table>
    <colgroup>
    <col style="width: 50%" />
    <col style="width: 50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>Cmdlet</th>
    <th>Paramètre</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p><a href="https://technet.microsoft.com/fr-fr/library/aa997443(v=exchg.150)">Set-OrganizationConfig</a></p></td>
    <td><p><em>HierarchicalAddressBookRoot</em></p></td>
    </tr>
    <tr class="even">
    <td><p><a href="https://technet.microsoft.com/fr-fr/library/bb123770(v=exchg.150)">Set-Group</a></p></td>
    <td><p><em>IsHierarchicalGroup</em></p>
    <p><em>SeniorityIndex</em></p>
    <p><em>PhoneticDisplayName</em></p></td>
    </tr>
    <tr class="odd">
    <td><p><a href="https://technet.microsoft.com/fr-fr/library/aa998221(v=exchg.150)">Set-User</a></p></td>
    <td><p><em>SeniorityIndex</em></p>
    <p><em>PhoneticDisplayName</em></p></td>
    </tr>
    <tr class="even">
    <td><p><a href="https://technet.microsoft.com/fr-fr/library/bb124535(v=exchg.150)">Set-Contact</a></p></td>
    <td><p><em>SeniorityIndex</em></p>
    <p><em>PhoneticDisplayName</em></p></td>
    </tr>
    </tbody>
    </table>


  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.


## Que souhaitez-vous faire ?

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour activer un carnet d'adresses hiérarchique

> [!NOTE]
> Bien qu'il soit impossible d'utiliser le CAE pour activer un carnet d'adresses hiérarchique, une fois ce dernier activé vous pouvez utiliser le CAE pour gérer l'appartenance des groupes au sein de la hiérarchie d'organisation.


Dans cet exemple, une unité d’organisation appelée « HAB » (carnet d’adresses hiérarchique) sera créée pour le carnet d’adresses hiérarchique. Le nom du domaine de l’organisation est « Contoso-dom » et « Contoso,Ltd » sera le nom de l’organisation de niveau supérieur de la hiérarchie (l’*organisation racine*). Les groupes subordonnés appelés « Corporate Office », « Product Support Organization» et « Sales & Marketing Organization » seront créés en tant qu’organisations enfants sous Contoso,Ltd. De plus, les groupes « Human Resources », « Accounting Group » et « Administration Group » seront créés en tant qu’organisations enfants sous Corporate Office.

Pour plus d’informations détaillées sur la création de groupes de distribution, consultez la rubrique [Création et gestion de groupes de distribution](create-and-manage-distribution-groups-exchange-2013-help.md).

1.  Créez une unité d’organisation portant le nom HAB dans l’organisation Contoso. Vous pouvez utiliser l’outil Utilisateurs et ordinateurs Active Directory ou bien taper ce qui suit à l’invite de commandes.
    
    > [!NOTE]
    > Vous pouvez également utiliser une unité d’organisation existante dans votre forêt Exchange.
    
        dsadd ou "OU=HAB,DC=Contoso-dom,DC=Contoso,DC=com"
    
    > [!NOTE]
    > Pour plus de détails, consultez la rubrique <a href="https://go.microsoft.com/fwlink/p/?linkid=198986">Créer une nouvelle unité d’organisation</a>.


2.  Créez le groupe de distribution racine Contoso,Ltd pour l’unité d’organisation HAB (carnet d’adresses hiérarchique).
    
    > [!NOTE]
    > Pour les besoins de cette rubrique, l’exemple présenté ici utilise l’environnement de ligne de commande Exchange Management Shell. Il est cependant possible de créer un groupe de distribution via le CAE. Pour plus de détails, consultez la rubrique <a href="create-and-manage-distribution-groups-exchange-2013-help.md">Création et gestion de groupes de distribution</a>.
    
        New-DistributionGroup -Name "Contoso,Ltd" -DisplayName "Contoso,Ltd" -Alias "ContosoRoot" -OrganizationalUnit "Contoso-dom.Contoso.com/HAB" -SamAccountName "ContosoRoot" -Type "Distribution"

3.  Désignez Contoso,Ltd comme l’organisation racine du carnet d’adresses hiérarchique.
    
        Set-OrganizationConfig -HierarchicalAddressBookRoot "Contoso,Ltd"

4.  Créez des groupes de distribution pour les autres niveaux dans le carnet d’adresses hiérarchique. Pour cet exemple, il vous faudrait créer les groupes suivants : Corporate Office, Product Support Organization, Sales & Marketing Organization, Human Resources, Accounting Group et Administration Group. Cet exemple crée le groupe de distribution Corporate Office.
    
    > [!NOTE]
    > Pour les besoins de cette rubrique, l’exemple présenté ici utilise l’environnement de ligne de commande Exchange Management Shell. Il est cependant possible de créer des groupes de distribution via le CAE. Pour plus d’informations, consultez la rubrique <a href="create-and-manage-distribution-groups-exchange-2013-help.md">Création et gestion de groupes de distribution</a>.
    
        New-DistributionGroup -Name "Corporate Office" -DisplayName "Corporate Office" -Alias "CorporateOffice" -OrganizationalUnit "Contoso-dom.Contoso.com/HAB" -SamAccountName "CorporateOffice" -Type "Distribution"

5.  Désignez chacun des groupes comme membres du carnet d’adresses hiérarchique. Pour cet exemple, il vous faudrait désigner les groupes suivants en tant que groupes hiérarchiques : Contoso,Ltd, Corporate Office, Product Support Organization, Sales & Marketing Organization, Human Resources, Accounting Group et Administration Group. Cet exemple désigne le groupe de distribution Contoso,Ltd comme membre du carnet d’adresses hiérarchique.
    
        Set-Group -Identity "Contoso,Ltd" -IsHierarchicalGroup $true

6.  Ajoutez chacun des groupes subordonnés en tant que membres de l’organisation racine. Dans cet exemple, les groupes de distribution Corporate Office, Product Support Organization et Sales & Marketing Organization sont ajoutés en tant que membres de l’organisation racine Contoso,Ltd dans le carnet d’adresses hiérarchique. Cet exemple ajoute le groupe de distribution Corporate Office comme membre du groupe de distribution racine Contoso,Ltd.
    
    > [!NOTE]
    > Cet exemple utilise l’alias des groupes de distribution.
    
        Add-DistributionGroupMember -Identity "ContosoRoot" -Member "CorporateOffice"

7.  Ajoutez chacun des groupes subordonnés du groupe de distribution Corporate Office en tant que membres de ce groupe. Dans cet exemple, les groupes de distribution Human Resources, Accounting Group et Administration Group sont ajoutés en tant que membres du groupe de distribution Corporate Office. Cet exemple ajoute le groupe de distribution Human Resources comme membre du groupe de distribution Corporate Office.
    
    > [!NOTE]
    > Cet exemple utilise l’alias des groupes de distribution et suppose que l’alias du groupe de distribution Human Resources est HumanResources.
    
        Add-DistributionGroupMember -Identity "CorporateOffice" -Member "HumanResources"

8.  Ajoutez des utilisateurs aux groupes dans le carnet d’adresses hiérarchique. Dans cet exemple, David Hamilton (adresse SMTP : DHamilton@contoso.com) est un utilisateur existant dans l’unité d’organisation Contoso-dom.Contoso.com/Users et sera ajouté au groupe Corporate Office. Répétez cette étape pour ajouter d’autres utilisateurs aux groupes du carnet d’adresses hiérarchique.
    
        Add-DistributionGroupMember -Identity "CorporateOffice" -Member "DHamilton"

9.  Définissez le paramètre *SeniorityIndex* pour les groupes au sein du carnet d’adresses hiérarchique. Dans cet exemple, le groupe Corporate Office contient trois groupes enfants : Human Resources, Accounting Group et Administration Group. Plutôt que d’afficher les groupes dans un ordre alphabétique croissant (soit la valeur par défaut), le mode de tri choisi de préférence sera Human Resources (*SeniorityIndex* = 100), Accounting Group (*SeniorityIndex* = 50), puis Administration Group (*SeniorityIndex* = 25). Cet exemple définit sur 100 le paramètre *SeniorityIndex* pour le groupe Human Resources.
    
        Set-Group -Identity "Human Resources" -SeniorityIndex 100
    
    > [!NOTE]
    > Le paramètre <em>SeniorityIndex</em> est une valeur numérique utilisée pour trier des groupes ou des utilisateurs dans un ordre numérique décroissant dans un carnet d’adresses hiérarchique. Si le paramètre <em>SeniorityIndex</em> n’est pas défini ou équivaut à deux ou plusieurs utilisateurs, le mode de tri dans le carnet d’adresses hiérarchique utilise le paramètre <em>PhoneticDisplayName</em> pour répertorier les utilisateurs dans l’ordre alphabétique croissant. Si le paramètre <em>PhoneticDisplayName</em> n’est pas défini, l’ordre de tri dans le carnet d’adresses hiérarchique est défini par défaut avec la valeur <em>DisplayName</em> et affiche les utilisateurs par ordre alphabétique croissant.


10. Définissez le paramètre *SeniorityIndex* pour les utilisateurs au sein des groupes du carnet d’adresses hiérarchique. Dans cet exemple, le groupe Corporate Office contient trois utilisateurs : Amy Alberts, David Hamilton et Rajesh M. Patel. Plutôt que d’afficher les utilisateurs dans un ordre alphabétique croissant (valeur par défaut), le mode de tri choisi de préférence sera David Hamilton (*SeniorityIndex* = 100), Rajesh M. Patel (*SeniorityIndex* = 50), puis Amy Alberts (*SeniorityIndex* = 25). Cet exemple définit sur 100 le paramètre *SeniorityIndex* pour l’utilisateur David Hamilton.
    
        Set-User -Identity "DHamilton@contoso.com" -SeniorityIndex 100

Une fois les étapes ci-avant terminées, le carnet d’adresses hiérarchique est visible dans Outlook. Pour le consulter, ouvrez Outlook, puis cliquez sur **Carnet d’adresses**. Le carnet d’adresses hiérarchique apparaît dans l’onglet **Organisation** comme dans la figure ci-après.

**Exemple de carnet d’adresses hiérarchique pour Contoso,Ltd**

![Boîte de dialogue Carnet d’adresses hiérarchique](images/Ff607473.d8cc782f-61cd-44c4-9c74-432ebea0c3db(EXCHG.150).gif "Boîte de dialogue Carnet d’adresses hiérarchique")

Une fois le carnet d’adresses hiérarchique créé, vous pouvez recourir au CAE pour gérer l’appartenance des groupes au sein de la hiérarchie d’organisation. Vous devrez en revanche faire appel à l’environnement de ligne de commande Exchange Management Shell pour modifier le paramètre *SeniorityIndex* pour tous les nouveaux groupes ou utilisateurs.

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, consultez les rubriques suivantes :

  - [New-DistributionGroup](https://technet.microsoft.com/fr-fr/library/aa998856\(v=exchg.150\))

  - [Set-OrganizationConfig](https://technet.microsoft.com/fr-fr/library/aa997443\(v=exchg.150\))

  - [Set-Group](https://technet.microsoft.com/fr-fr/library/bb123770\(v=exchg.150\))

  - [Add-DistributionGroupMember](https://technet.microsoft.com/fr-fr/library/bb124340\(v=exchg.150\))

  - [Set-User](https://technet.microsoft.com/fr-fr/library/aa998221\(v=exchg.150\))

## Utiliser l’environnement de ligne de commande Exchange Management Shell pour désactiver un carnet d’adresses hiérarchique

Cet exemple désactive l’organisation racine utilisée pour le carnet d’adresses hiérarchique.

    Set-OrganizationConfig -HierarchicalAddressBookRoot $null

> [!NOTE]
> Cette commande ne supprime pas l’organisation racine ni les groupes enfants employés dans la structure du carnet d’adresses hiérarchique ou elle ne réinitialise pas les valeurs <em>SeniorityIndex</em> des groupes ou des utilisateurs. Elle empêche uniquement l’affichage du carnet d’adresses hiérarchique dans Outlook. Pour activer de nouveau le carnet d’adresses hiérarchique avec les mêmes paramètres de configuration, vous avez simplement besoin de réactiver l’organisation racine.


Pour obtenir des informations détaillées sur la syntaxe et les paramètres, consultez la rubrique [Set-OrganizationConfig](https://technet.microsoft.com/fr-fr/library/aa997443\(v=exchg.150\)).

