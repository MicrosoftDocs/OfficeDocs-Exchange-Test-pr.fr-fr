---
title: 'Exportation et importation de balises de rétention: Exchange 2013 Help'
TOCTitle: Exportation et importation de balises de rétention
ms:assetid: 18405ea2-7ccc-475e-bd84-8b040e17bf44
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ907307(v=EXCHG.150)
ms:contentKeyID: 51407159
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Exportation et importation de balises de rétention

 

_**Sapplique à :** Exchange Online, Exchange Server 2013_

_**Dernière rubrique modifiée :** 2017-11-15_

Il existe plusieurs cas de figure dans lesquels vous pourriez être amené à exporter ou importer des balises de rétention, par exemple :

  - Appliquer les mêmes stratégies de rétention sur tous les serveurs dans une organisation à plusieurs forêts Exchange

  - Application des mêmes stratégies de rétention dans un déploiement hybride dans lequel certaines boîtes aux lettres résident dans votre organisation Exchange locale alors que d'autres résident dans Exchange Online.

  - Application de stratégies de rétention dans un scénario d’archivage Exchange, où les utilisateurs locaux Exchange 2010 ou des boîtes aux lettres ultérieure ont une archive en nuage.

Dans ces scénarios, l'Assistant Dossier géré peut traiter correctement un élément auquel une balise de rétention est appliquée après que l'élément ou la boîte aux lettres ait été déplacé vers une autre organisation.

> [!CAUTION]
> Pour conserver les balises de rétention et les stratégies de rétention synchronisées entre deux organisations, chaque fois que vous apportez des modifications à une balise ou une stratégie de rétention dans l'organisation source, vous devez exécuter cette procédure pour exporter les balises et les stratégies de rétention de l'organisation source et les importer dans l'organisation de destination.
> Vous ne pouvez pas sélectionner des balises ou des stratégies de rétention spécifiques en vue de les exporter. Le script Export-RetentionTags.ps1 exporte toutes les balises et stratégies de rétention d’une organisation.


Pour les autres tâches de gestion relatives à la gestion des enregistrements de messagerie, consultez la rubrique [Procédures de gestion des enregistrements de messagerie](messaging-records-management-procedures-exchange-2013-help.md).

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée de chaque procédure : 10 minutes

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l'entrée « Gestion des enregistrements de messagerie » dans la rubrique [Stratégie de messagerie et autorisations de conformité](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

  - Les procédures décrites dans cette rubrique dépendent de ces trois fichiers dans le dossier `%ExchangeInstallPath%Scripts` sur votre serveur deExchange:
    
      - Export-RetentionTags.ps1
    
      - Import-RetentionTags.ps1
    
      - MigrateRetentionTags.strings.psd1

  - Vous ne pouvez pas sélectionner des balises ou des stratégies de rétention spécifiques en vue de les exporter ou de les importer. Le script Export-RetentionTags.ps1 exporte toutes les balises et stratégies de rétention d'une organisation. Le script Import-RetentionTags.ps1 importe toutes les balises et stratégies de rétention dans le fichier XML importé, en remplaçant toutes les balises et stratégies de rétention d'une organisation Exchange.

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.


## Étape 1 : Exporter des balises de rétention à partir d’une organisation Exchange locale

1.  Exécutez cette commande Environnement de ligne de commande Exchange Management Shell pour changer de répertoire dans le sous-répertoire de **Scripts** dans votre chemin d’installation de Exchange.
    
        Cd $Env:ExchangeInstallPath\Scripts

2.  Exécutez le script Export-RetentionTags.ps1 pour exporter des balises de rétention dans un fichier XML.
    
    > [!NOTE]
    > Si vous importez ou exportez des balises de rétention et les règles de rétention à Exchange Online, vous devez vous connecter votre session Windows PowerShell à Exchange Online. Pour plus d’informations, consultez <a href="https://technet.microsoft.com/fr-fr/library/jj984289(v=exchg.150)">Connexion à Exchange Online à l'aide de Remote PowerShell</a>.
    
        .\Export-RetentionTags.ps1 "c:\docs\ExportedRetentionTags.xml"

## Comment savoir si cela a fonctionné ?

Pour vérifier que les balises et les stratégies de rétention ont bien été exportées, procédez comme suit :

1.  Accédez au chemin que vous avez spécifié dans la commande d'exportation et vérifiez que le fichier XML portant le nom que vous avez spécifié a été créé.

2.  Vous pouvez également ouvrir le fichier XML dans un éditeur de texte pour examiner son contenu.

## Étape 2 : Importer des balises de rétention dans une organisation Exchange

1.  Exécutez cette commande Environnement de ligne de commande Exchange Management Shell pour modifier le répertoire dans le sous-répertoire de **Scripts** dans votre chemin d’installation de Exchange.
    
        Cd $Env:ExchangeInstallPath\Scripts

2.  Exécutez le script Import-RetentionTags.ps1 pour importer les balises de rétention d'un fichier XML précédemment exporté.
    
    > [!NOTE]
    > Si vous importez ou exportez des balises de rétention et les règles de rétention à Exchange Online, vous devez vous connecter votre session Windows PowerShell à Exchange Online. Pour plus d’informations, consultez <a href="https://technet.microsoft.com/fr-fr/library/jj984289(v=exchg.150)">Connexion à Exchange Online à l'aide de Remote PowerShell</a>.
    
    > [!NOTE]
    > Lorsque vous exécutez ce script sur Exchange Online, vous pouvez être invité à confirmer que vous voulez exécuter le logiciel à partir d’un éditeur non approuvé. Vérifiez que le nom de l’éditeur s’affiche sous la forme <code>CN=Microsoft Corporation, OU=MOPR, O=Microsoft Corporation, L=Redmond, S=Washington, C=US</code>, puis cliquez sur <strong>R</strong> pour permettre le script à exécuter une seule fois ou <strong>A</strong> toujours exécuter.
    
        .\Import-RetentionTags.ps1 "c:\docs\ExportedRetentionTags.xml"

## Comment savoir si cela a fonctionné ?

Pour vérifier que les balises et les stratégies de rétention ont bien été importées, procédez comme suit :

1.  Dans le Centre d'administration Exchange (CAE), accédez à **Gestion de la conformité** \> **Balises de rétention**, puis vérifiez que les balises de rétention ont bien été importées. Accédez à **Gestion de la conformité** \> **Stratégies de rétention**, puis vérifiez que les stratégies de rétention ont bien été importées.

2.  Utilisez les cmdlets **Get-RetentionPolicy** et **Get-RetentionPolicyTag** pour vérifier que les balises et les stratégies ont été créées. Pour obtenir un exemple sur la récupération des balises et des stratégies de rétention, consultez la section Exemples dans les rubriques [Get-RetentionPolicyTag](https://technet.microsoft.com/fr-fr/library/dd298009\(v=exchg.150\)) et [Get-RetentionPolicy](https://technet.microsoft.com/fr-fr/library/dd298086\(v=exchg.150\)).

