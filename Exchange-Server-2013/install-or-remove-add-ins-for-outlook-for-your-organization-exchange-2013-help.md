---
title: 'Installation ou suppression d’applications pour votre organisation'
TOCTitle: Installation ou suppression d’applications pour votre organisation
ms:assetid: 112f3ef7-9943-4a1e-8a42-e08e8e9f67f4
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ943752(v=EXCHG.150)
ms:contentKeyID: 52062939
ms.date: 04/27/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Installation ou suppression d’applications pour votre organisation

 

_**Sapplique à :** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2017-02-03_

Vous pouvez installer ou supprimer des compléments pour Outlook pour votre organisation à l’aide du Centre d’administration Exchange (CAE) ou de l’environnement de ligne de commande Exchange Management Shell.

> [!NOTE]
> Par défaut, après avoir installé un complément pour votre organisation, le complément devient disponible pour tous les utilisateurs de votre organisation. Après la phase d’installation, vous pouvez utiliser le CAE ou l’environnement de ligne de commande Exchange Management Shell afin de rendre le complément facultatif ou obligatoire pour les utilisateurs et pour indiquer si le complément doit être activé ou désactivé. Pour plus d’informations sur la modification des paramètres par défaut d’un complément, consultez la rubrique <a href="manage-user-access-to-add-ins-for-outlook-exchange-online-help.md">Gestion de l’accès des utilisateurs aux applications pour Outlook</a>. Pour limiter la mise à disposition de compléments à des utilisateurs spécifiques de votre organisation, vous devez utiliser l’environnement de ligne de commande Exchange Management Shell. Pour plus d’informations, consultez la rubrique <a href="manage-user-access-to-add-ins-for-outlook-exchange-online-help.md">Gestion de l’accès des utilisateurs aux applications pour Outlook</a>.


Pour des tâches de gestion supplémentaires, consultez la rubrique [Applications pour Outlook](add-ins-for-outlook-exchange-2013-help.md).

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : 5 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Applications pour Outlook » dans la rubrique [Autorisations des destinataires](recipients-permissions-exchange-2013-help.md).

  - Vous pouvez attribuer des autorisations d’administrateur afin d’installer et de gérer des compléments pour votre organisation. Vous pouvez également attribuer des autorisations d’administrateur à des personnes afin que ces dernières installent et gèrent des compléments pour leur propre utilisation. Pour plus d’informations, consultez la rubrique [Désigner les administrateurs et utilisateurs qui peuvent installer et gérer des compléments pour Outlook](specify-the-administrators-and-users-who-can-install-and-manage-add-ins-for-outlook-exchange-2013-help.md).

  - L’accès à Office Store n’est pas pris en charge pour les boîtes aux lettres ou les organisations de certains pays. Si l’option **Ajouter à partir d’Office Store** n’apparaît pas dans le **Centre d’administration Exchange** sous **Organisation** \> **Compléments** \> ![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter"), vous pourrez peut-être installer un complément pour Outlook depuis un emplacement de fichier ou une URL. Pour plus d’informations, contactez votre fournisseur de services.

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..


## Que souhaitez-vous faire ?

## Installer un complément pour Outlook

## Utiliser le CAE pour ajouter un complément

1.  Dans le CAE, accédez à **Organisation** \> **Compléments**.

2.  Cliquez sur **Nouveau**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter"), puis sélectionnez l’emplacement à partir duquel vous souhaitez installer le complément.
    
      - **Ajouter à partir d’Office Store**. Sur Office Store, sélectionnez l’application à installer, puis cliquez sur **Ajouter**. Les applications qui fonctionnent avec Outlook Web App sont répertoriées sous **Compléments pour Office et SharePoint** \> **Outlook**.
        
        > [!NOTE]
        > L’accès à Office Store n’est pas pris en charge pour les boîtes aux lettres ou les organisations de certains pays. Si l’option <strong>Ajouter à partir d’Office Store</strong> n’apparaît pas dans le <strong>Centre d’administration Exchange</strong> sous <strong>Organisation</strong> &gt; <strong>Compléments</strong> &gt; <img src="images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif" title="Icône Ajouter" alt="Icône Ajouter" />, vous pourrez peut-être installer un complément pour Outlook depuis un emplacement de fichier ou une URL. Pour plus d’informations, contactez votre fournisseur de services.
    
      - **Ajouter à partir d’une URL**. Dans **URL**, entrez l’URL complète du fichier manifeste du complément à installer.
    
      - **Ajouter à partir d’un fichier**. Sélectionnez **Parcourir**, puis accédez à l’emplacement du fichier manifeste du complément à installer.

3.  Cliquez sur **Enregistrer**.

## Utiliser l’environnement de ligne de commande Exchange Management Shell pour ajouter un complément

Cet exemple illustre l’ajout d’un complément à partir d’une URL.

    New-App -OrganizationApp -Url <URL location for add-in manifest file>

Cet exemple illustre l’ajout d’un complément à partir d’un fichier.

    New-App -OrganizationApp -FileData <File location for add-in manifest file>

> [!TIP]
> Quand vous utilisez l’environnement de ligne de commande Exchange Management Shell afin d’installer un complément pour votre organisation, vous pouvez installer le complément et configurer en même temps des paramètres pour ce dernier.


Pour obtenir la syntaxe et les paramètres, consultez la rubrique [New-App](https://technet.microsoft.com/fr-fr/library/jj218722\(v=exchg.150\)).

## Supprimer un complément pour Outlook

## Utiliser le CAE pour supprimer un complément

1.  Dans le CAE, accédez à **Organisation** \> **Compléments**.

2.  Dans l'affichage Liste, sélectionnez l'application à supprimer, puis cliquez sur **Supprimer**![Icône Supprimer](images/Dd979797.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "Icône Supprimer").

## Utiliser l’environnement de ligne de commande Exchange Management Shell pour supprimer un complément

Vous pouvez utiliser l’environnement de ligne de commande Exchange Management Shell pour supprimer un complément au sein de votre organisation.

> [!NOTE]
> Exécutez la commande suivante pour rechercher les noms complets et les ID de complément pour tous les compléments pour Outlook installés au sein de votre organisation.


    Get-App -OrganizationApp |FL DisplayName,AppID

Exécutez la commande suivante pour supprimer le complément personnalisé Finance Test de l’organisation.

    Remove-App -OrganizationApp -Identity <GUID for Finance Test Add-in>

Pour obtenir la syntaxe et les paramètres, consultez la rubrique [Remove-App](https://technet.microsoft.com/fr-fr/library/jj218709\(v=exchg.150\)).

## Comment savoir si cela a fonctionné ?

Pour afficher les compléments installés dans votre organisation, effectuez l’une des opérations suivantes :

  - Dans le CAE, accédez à **Organisation** \> **Compléments**, puis passez en revue la liste des compléments installés.

  - Dans l’environnement de ligne de commande Exchange Management Shell, exécutez `Get-App`, puis passez en revue la liste des compléments installés.

