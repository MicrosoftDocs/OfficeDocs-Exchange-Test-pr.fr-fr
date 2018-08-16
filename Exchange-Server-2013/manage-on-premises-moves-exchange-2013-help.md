---
title: 'Gestion des déplacements locaux: Exchange 2013 Help'
TOCTitle: Gestion des déplacements locaux
ms:assetid: 1691b658-f5af-49c6-9170-5c3cb66c7306
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ150487(v=EXCHG.150)
ms:contentKeyID: 50477580
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Gestion des déplacements locaux

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2013-02-25_

Une demande de déplacement désigne le processus de déplacement d'une boîte aux lettres d'une base de données de boîtes aux lettres à une autre. Une demande de déplacement local est un déplacement de boîte aux lettres qui se produit dans une seule forêt. Dans Microsoft Exchange Server 2013, les boîtes aux lettres et les boîtes aux lettres d'archivage personnel peuvent se trouver sur des bases de données distinctes. À l'aide de la fonctionnalité de demande de déplacement, vous pouvez déplacer la boîte aux lettres principale et l'archive qui y est associée sur la même base de données ou sur des bases de données séparées. Les procédures décrites dans cette rubrique vous aideront à effectuer des déplacements de boîtes aux lettres locales.

Les procédures suivantes vous permettent de déplacer des boîtes aux lettres dans votre organisation locale. Ces procédures utilisent l'environnement de ligne de commande Exchange Management Shell et le Centre d'administration Exchange (CAE).

Lorsque vous utilisez des demandes de déplacement pour déplacer des boîtes aux lettres, ces demandes sont traitées par les deux services suivants :

  - Service de réplication de boîte aux lettres Microsoft Exchange

  - Proxy de réplication de boîte aux lettres Microsoft Exchange

Pour plus d'informations sur le serveur et le proxy de réplication de boîte aux lettres, consultez la rubrique [En savoir plus sur le proxy MRS](https://technet.microsoft.com/fr-fr/library/jj156451\(v=exchg.150\)).

Pour plus d'informations sur le déplacement de boîtes aux lettres, consultez la rubrique [Déplacements de boîtes aux lettres dans Exchange 2013](mailbox-moves-in-exchange-2013-exchange-2013-help.md).

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée de chaque procédure : 20 minutes

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l'entrée « Autorisations de migration et de déplacement de boîtes aux lettres » dans la rubrique [Autorisations des destinataires](recipients-permissions-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.


## Que souhaitez-vous faire ?

## Test d'une boîte aux lettres pour savoir si elle peut être déplacée

Cet exemple utilise le commutateur *WhatIf* pour tester la boîte aux lettres de Tony Smith et savoir si elle est prête à être déplacée vers la nouvelle base de données DB01 et si la commande renvoie des erreurs. Lorsque vous utilisez le commutateur *WhatIf*, le système effectue des vérifications sur la boîte aux lettres. Si la boîte aux lettres n'est pas prête à être déplacée, vous recevez un message d'erreur.

    New-MoveRequest -Identity 'tony@alpineskihouse.com' -TargetDatabase DB01 -WhatIf

Pour des informations détaillées sur la syntaxe et les paramètres, consultez les rubriques [New-MigrationBatch](https://technet.microsoft.com/fr-fr/library/jj219166\(v=exchg.150\)) et [New-MoveRequest](https://technet.microsoft.com/fr-fr/library/dd351123\(v=exchg.150\)).

## Créer une demande de déplacement local

## Utiliser le Centre d'administration Exchange (CAE) pour créer une demande de déplacement local

Pour créer une demande de déplacement local, connectez-vous au CAE et procédez comme suit :

1.  Dans le CAE, accédez à **Destinataires** \> **Migration**, puis, cliquez sur **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter").

2.  Dans l'Assistant **Nouveau déplacement de boîte aux lettres locale**, sélectionnez l'utilisateur à déplacer, cliquez sur **OK**, puis cliquez sur **Suivant**.

3.  Dans la page **Déplacer la configuration**, spécifiez le nom du nouveau lot. Sélectionnez les options choisies pour la boîte aux lettres d'archive et l'emplacement de la base de données de la boîte aux lettres, puis cliquez sur **Nouveau**.

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour créer une demande de déplacement locale

L'exemple 2 de la rubrique [New-MoveRequest](https://technet.microsoft.com/fr-fr/library/dd351123\(v=exchg.150\)) illustre la création d'une demande de déplacement local.

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez terminé avec succès la migration, procédez comme suit :

  - Dans le CAE, accédez à **Destinataires** \> **Migration**.

  - Vérifiez que vos déplacements sont exécutés avec succès dans le CAE en cliquant sur **État de tous les lots**.

  - À partir du Shell, exécutez la commande suivante pour récupérer les informations de déplacement des boîtes aux lettres.
    
        Get-MigrationUserStatistics -Identity BatchName -Status | Format-List

Pour plus d'informations, consultez la rubrique [Get-MigrationUserStatistics](https://technet.microsoft.com/fr-fr/library/jj218695\(v=exchg.150\)).

## Créer une demande de déplacement en lot

## Utiliser le Centre d'administration Exchange (CAE) pour créer une demande de déplacement par lot

Connectez-vous au CAE et effectuez les opérations suivantes :

1.  Dans le CAE, accédez à **Destinataires** \> **Migration**, puis, cliquez sur **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter").

2.  Dans l'Assistant **Nouveau déplacement de boîte aux lettres locale**, sélectionnez les utilisateurs à déplacer, cliquez sur **OK**, puis cliquez sur **Suivant**.

3.  Dans la page **Déplacer la configuration**, spécifiez le nom du nouveau lot. Sélectionnez les options choisies pour la boîte aux lettres d'archive et l'emplacement de la base de données de la boîte aux lettres, puis cliquez sur **Nouveau**.

> [!WARNING]
> Veillez à ne pas définir la limite d'éléments incorrects sur une valeur supérieure à 50, car le déplacement risquerait d'échouer. Si vous définissez la limite d'éléments incorrects sur une valeur supérieure à 50, vous devez utiliser l'environnement de ligne de commande Exchange Management Shell et définir le paramètre –<em>AcceptLargeDataLoss</em> sur True.


## Utiliser l'environnement de ligne de commande Exchange Management Shell pour créer une demande de déplacement par lot

Cet exemple crée un lot de migration pour un déplacement local, dans lequel les boîtes aux lettres du fichier .csv spécifié sont déplacées vers une base de données de boîtes aux lettres différente. Ce fichier .csv affiche une seule colonne qui contient l'adresse de messagerie de chaque boîte aux lettres à déplacer. L'en-tête de cette colonne doit être nommé **EmailAddress**. Dans cet exemple, le lot de migration doit être démarré manuellement via la cmdlet **Start-MigrationBatch** ou dans le CAE. Sinon, vous pouvez utiliser le paramètre *AutoStart* pour démarrer le lot de migration automatiquement.
```
    New-MigrationBatch -Local -Name LocalMove1 -CSVData ([System.IO.File]::ReadAllBytes("C:\Users\Administrator\Desktop\LocalMove1.csv")) -TargetDatabases MBXDB2 -TimeZone "Pacific Standard Time"
```
```
    Start-MigrationBatch -Identity LocalMove1
```

Pour des informations détaillées sur la syntaxe et les paramètres, consultez les rubriques [New-MigrationBatch](https://technet.microsoft.com/fr-fr/library/jj219166\(v=exchg.150\)) et [Start-MigrationBatch](https://technet.microsoft.com/fr-fr/library/jj219165\(v=exchg.150\)).

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez terminé avec succès la migration, procédez comme suit :

  - Vérifiez que vos déplacements sont exécutés avec succès dans le CAE en cliquant sur **État de tous les lots**.

  - À partir du Shell, exécutez la commande suivante pour récupérer les informations de déplacement des boîtes aux lettres.
    
        Get-MigrationUserStatistics -Identity BatchName -Status | Format-List

Pour plus d'informations, consultez la rubrique [Get-MigrationUserStatistics](https://technet.microsoft.com/fr-fr/library/jj218695\(v=exchg.150\)).

## Afficher les lots de migration

Pour obtenir un exemple d'utilisation de l'environnement de ligne de commande Exchange Management Shell pour afficher un lot de migration, reportez-vous à l'exemple 2 de la rubrique [Get-MigrationBatch](https://technet.microsoft.com/fr-fr/library/jj219164\(v=exchg.150\)).

## Déplacer uniquement la boîte aux lettres principale d'un utilisateur

## Utiliser le Centre d'administration Exchange (CAE) pour ne déplacer que la boîte aux lettres principale d'un utilisateur

1.  Dans le CAE, accédez à **Destinataires** \> **Migration**, puis, cliquez sur **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter").

2.  Dans l'Assistant **Nouveau déplacement de boîte aux lettres locale**, sélectionnez l'utilisateur dont vous souhaitez déplacer la boîte aux lettres principale, cliquez sur **OK**, puis sur **Suivant**.

3.  Dans la page **Déplacer la configuration**, spécifiez le nom du nouveau lot. Sélectionnez **Déplacer uniquement la boîte aux lettres principale**, puis les options de votre choix concernant l'emplacement de la base de données de boîtes aux lettres et cliquez sur **Nouveau**.

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour déplacer uniquement la boîte aux lettres principale d'un utilisateur

Cet exemple déplace uniquement la boîte aux lettres principale de Tony Smith vers la base de données DB01. L'archive n'est pas déplacée.

    New-MoveRequest -Identity 'tony@alpineskihouse.com' -PrimaryOnly -TargetDatabase "DB01"

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, consultez la rubrique [New-MoveRequest](https://technet.microsoft.com/fr-fr/library/dd351123\(v=exchg.150\)).

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez terminé avec succès la migration, procédez comme suit :

  - Dans le CAE, cliquez sur **État de tous les lots**.

  - À partir du Shell, exécutez la commande suivante pour récupérer les informations de déplacement des boîtes aux lettres.
    
        Get-MigrationUserStatistics -Identity BatchName -Status | Format-List

Pour plus d'informations, consultez la rubrique [Get-MigrationUserStatistics](https://technet.microsoft.com/fr-fr/library/jj218695\(v=exchg.150\)).

## Créer un déplacement inter-forêts à l'aide d'un fichier de lot .csv

Cet exemple permet de configurer le point de terminaison de migration, puis de créer un déplacement par lot inter-forêts de la forêt source à la forêt cible, à l'aide d'un fichier .csv.
```
    New-MigrationEndpoint -Name Fabrikam -ExchangeRemote -Autodiscover -EmailAddress tonysmith@fabrikam.com -Credentials (Get-Credential fabrikam\tonysmith) 
    
    $csvData=[System.IO.File]::ReadAllBytes("C:\Users\Administrator\Desktop\batch.csv")
    New-MigrationBatch -CSVData $csvData -Timezone "Pacific Standard Time" -Name FabrikamMerger -SourceEndpoint Fabrikam -TargetDeliveryDomain "mail.contoso.com"
```
Pour plus d'informations sur la préparation de votre forêt pour des déplacements inter-forêts, consultez les rubriques suivantes :

  - [Préparer les boîtes aux lettres pour les demandes de déplacement inter-forêts](prepare-mailboxes-for-cross-forest-move-requests-exchange-2013-help.md)

  - [Préparer les boîtes aux lettres pour les déplacements inter-forêts à l’aide d’un exemple de code](prepare-mailboxes-for-cross-forest-moves-using-sample-code-exchange-2013-help.md)

  - [Préparer des boîtes aux lettres pour des déplacements inter-forêts à l’aide du script Prepare-MoveRequest.ps1 dans l’environnement de ligne de commande Exchange Management Shell](prepare-mailboxes-for-cross-forest-moves-using-the-prepare-moverequest-ps1-script-in-the-shell-exchange-2013-help.md)

Pour des informations détaillées sur la syntaxe et les paramètres, consultez les rubriques [New-MigrationBatch](https://technet.microsoft.com/fr-fr/library/jj219166\(v=exchg.150\)) et [New-MoveRequest](https://technet.microsoft.com/fr-fr/library/dd351123\(v=exchg.150\)).

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez terminé avec succès la migration, procédez comme suit :

  - À partir du Shell, exécutez la commande suivante pour récupérer les informations de déplacement des boîtes aux lettres.
    
        Get-MigrationUserStatistics -Identity BatchName -Status | Format-List

Pour plus d'informations, consultez la rubrique [Get-MigrationUserStatistics](https://technet.microsoft.com/fr-fr/library/jj218695\(v=exchg.150\)).

## Déplacer uniquement une boîte aux lettres d'archivage

## Utiliser le Centre d'administration Exchange (CAE) pour ne déplacer qu'une boîte aux lettres d'archivage

1.  Dans le CAE, accédez à **Destinataires** \> **Migration**, puis, cliquez sur **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter").

2.  Dans l'Assistant **Nouveau déplacement de boîte aux lettres locale**, sélectionnez l'utilisateur dont vous souhaitez déplacer la boîte aux lettres d'archivage, cliquez sur **OK**, puis sur **Suivant**.

3.  Dans la page **Déplacer la configuration**, spécifiez le nom du nouveau lot. Sélectionnez **Déplacer uniquement la boîte aux lettres d'archivage**, puis les options de votre choix concernant l'emplacement de la base de données de boîtes aux lettres, puis cliquez sur **Nouveau**.

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour déplacer uniquement une boîte aux lettres d'archivage

Cet exemple déplace uniquement la boîte aux lettres d'archivage de Tony Smith vers la base de données DB03. La boîte aux lettres principale n'est pas déplacée.

    New-MoveRequest -Identity 'tony@alpineskihouse.com' -ArchiveOnly -ArchiveTargetDatabase "DB03"

Pour des informations détaillées sur la syntaxe et les paramètres, consultez les rubriques [New-MigrationBatch](https://technet.microsoft.com/fr-fr/library/jj219166\(v=exchg.150\)) et [New-MoveRequest](https://technet.microsoft.com/fr-fr/library/dd351123\(v=exchg.150\)).

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez terminé avec succès la migration, procédez comme suit :

  - À partir du Shell, exécutez la commande suivante pour récupérer les informations de déplacement des boîtes aux lettres.
    
        Get-MigrationUserStatistics -Identity BatchName -Status | Format-List

Pour plus d'informations, consultez la rubrique [Get-MigrationUserStatistics](https://technet.microsoft.com/fr-fr/library/jj218695\(v=exchg.150\)).

## Déplacer la boîte aux lettres principale et la boîte aux lettres d'archivage de l'utilisateur vers des bases de données distinctes

Cet exemple déplace la boîte aux lettres principale et l'archive d'Ayla vers des bases de données distinctes. La boîte aux lettres principale est déplacée vers la base de données DB01 et l'archive vers la base de données DB03.

    New-MoveRequest -Identity 'ayla@humongousinsurance.com' -TargetDatabase DB01 -ArchiveTargetDatabase -DB03

Pour des informations détaillées sur la syntaxe et les paramètres, consultez les rubriques [New-MigrationBatch](https://technet.microsoft.com/fr-fr/library/jj219166\(v=exchg.150\)) et [New-MoveRequest](https://technet.microsoft.com/fr-fr/library/dd351123\(v=exchg.150\)).

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez terminé avec succès la migration, procédez comme suit :

  - À partir du Shell, exécutez la commande suivante pour récupérer les informations de déplacement des boîtes aux lettres.
    
        Get-MigrationUserStatistics -Identity BatchName -Status | Format-List

Pour plus d'informations, consultez la rubrique [Get-MigrationUserStatistics](https://technet.microsoft.com/fr-fr/library/jj218695\(v=exchg.150\)).

## Déplacer la boîte aux lettres principale d'un utilisateur et autoriser une limite élevée d'éléments incorrects

## Utiliser le Centre d'administration Exchange (CAE) pour déplacer la boîte aux lettres principale d'un utilisateur et autoriser une limite élevée d'éléments incorrects

1.  Dans le CAE, accédez à **Destinataires** \> **Migration**, puis, cliquez sur **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter").

2.  Dans l'Assistant **Nouveau déplacement de boîte aux lettres locale**, sélectionnez l'utilisateur dont vous souhaitez déplacer la boîte aux lettres principale, cliquez sur **OK**, puis sur **Suivant**.

3.  Dans la page **Déplacer la configuration**, spécifiez le nom du nouveau lot. Sélectionnez **Déplacer uniquement la boîte aux lettres principale**, puis les options de votre choix concernant l'emplacement de la base de données de boîtes aux lettres.

4.  Cliquez sur **Autres options**![Icône Options supplémentaires](images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif "Icône Options supplémentaires"), indiquez la limite d'éléments incorrects, puis cliquez sur **OK**.

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour déplacer la boîte aux lettres principale d'un utilisateur et autoriser une limite élevée d'éléments incorrects

Cet exemple déplace la boîte aux lettres principale de Lisa vers la base de données de boîtes aux lettres DB01 et définit la limite d'éléments incorrects sur `100`. Pour définir une limite élevée d'éléments incorrects, vous devez utiliser le paramètre *AcceptLargeDataLoss*.

    New-MoveRequest -Identity 'Lisa' -PrimaryOnly -TargetDatabase "DB01" -BadItemLimit 100 -AcceptLargeDataLoss

Pour des informations détaillées sur la syntaxe et les paramètres, consultez les rubriques [New-MigrationBatch](https://technet.microsoft.com/fr-fr/library/jj219166\(v=exchg.150\)) et [New-MoveRequest](https://technet.microsoft.com/fr-fr/library/dd351123\(v=exchg.150\)).

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez terminé avec succès la migration, procédez comme suit :

  - À partir du Shell, exécutez la commande suivante pour récupérer les informations de déplacement des boîtes aux lettres.
    
        Get-MigrationUserStatistics -Identity BatchName -Status | Format-List

Pour plus d'informations, consultez la rubrique [Get-MigrationUserStatistics](https://technet.microsoft.com/fr-fr/library/jj218695\(v=exchg.150\)).

