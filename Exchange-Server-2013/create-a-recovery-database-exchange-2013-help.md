---
title: 'Créer une base de données de récupération: Exchange 2013 Help'
TOCTitle: Créer une base de données de récupération
ms:assetid: 34d87491-b7b7-44a9-8d69-e1a9c1fe5852
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Ee332321(v=EXCHG.150)
ms:contentKeyID: 50477883
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Créer une base de données de récupération

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2013-01-21_

Vous pouvez utiliser l’environnement de ligne de commande Exchange Management Shell pour créer une base de données de récupération, un type particulier de base de données de boîtes aux lettres qui sert à monter et à extraire des données à partir de la base de données restaurée dans le cadre d’une opération de récupération. Une fois que vous avez créé une base de données de récupération, vous pouvez déplacer une base de données de boîtes aux lettres récupérée ou restaurée dans la base de données de récupération puis en extraire des données à l’aide de la cmdlet [New-MailboxRestoreRequest](https://technet.microsoft.com/fr-fr/library/ff829875\(v=exchg.150\)). Après extraction, les données peuvent ensuite être exportées dans un dossier ou fusionnées dans une boîte aux lettres existante. Les bases de données de récupération vous permettent de récupérer des données à partir d’une sauvegarde ou d’une copie de base de données sans perturber l’accès des utilisateurs aux données actuelles.

Souhaitez-vous rechercher d’autres tâches de gestion liées aux bases de données de récupération ? Consultez la rubrique [Récupérer des bases de données](recovery-databases-exchange-2013-help.md).

## Ce qu’il faut savoir avant de commencer ?

  - Durée d’exécution estimée de cette tâche : 1 minute

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l’entrée « Récupération de boîte aux lettres » dans la rubrique [Autorisations des destinataires](recipients-permissions-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..


## Utiliser l’environnement de ligne de commande Exchange Management Shell pour créer une base de données de récupération

Cet exemple montre comment créer la base de données de récupération RDB1 sur le serveur de boîtes aux lettres MBX2.

```powershell
New-MailboxDatabase -Recovery -Name RDB1 -Server MBX2
```

Cet exemple montre comment créer la base de données de récupération RDB2 sur le serveur de boîtes aux lettres MBX1 à l’aide d’un chemin d’accès personnalisé au fichier de la base de données et au dossier du journal.

```powershell
New-MailboxDatabase -Recovery -Name RDB2 -Server MBX1 -EdbFilePath "C:\Recovery\RDB2\RDB2.EDB" -LogFolderPath "C:\Recovery\RDB2"
```

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, consultez la rubrique [New-MailboxDatabase](https://technet.microsoft.com/fr-fr/library/aa997976\(v=exchg.150\)).

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez bien créé une base de données de récupération, procédez comme suit :

  - Dans l’environnement de ligne de commande Exchange Management Shell, exécutez la commande suivante pour afficher les informations de configuration de la base de données de récupération :
    
    ```powershell
    Get-MailboxDatabase <RecoveryDatabaseName> | Format-List
    ```

## Autres tâches

Après avoir créé une base de données de récupération, vous pouvez également vouloir restaurer des données à l’aide d’une base de données de récupération. Pour obtenir la procédure détaillée, voir [Restaurer des données à l’aide d’une base de données de récupération](restore-data-using-a-recovery-database-exchange-2013-help.md).

