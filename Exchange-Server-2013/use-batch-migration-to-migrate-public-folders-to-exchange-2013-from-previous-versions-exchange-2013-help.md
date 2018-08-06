---
title: 'Utiliser migr. par lots de doss. publics vers Exchange 2013 à partir vrs préc. | Microsoft Docs'
TOCTitle: Utiliser la migration par lots pour migrer les dossiers publics vers Exchange 2013 à partir de versions antérieures
ms:assetid: da808e27-d2b7-4fbd-915c-a600751f526c
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dn912663(v=EXCHG.150)
ms:contentKeyID: 64129762
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Utiliser la migration par lots pour migrer les dossiers publics vers Exchange 2013 à partir de versions antérieures

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2018-03-26_

**Résumé** : Cet article explique comment déplacer des dossiers publics à partir d’Exchange 2007 ou Exchange 2010 vers Exchange 2013.

Cet article décrit comment migrer vos dossiers publics d’Exchange Server 2010 SP3 RU8 ou Exchange 2007 SP3 RU15 vers Microsoft Exchange Server 2013 CU7 ou une version ultérieure dans la même forêt.

Il est fait référence aux serveurs Exchange 2010 SP3 RU8 et Exchange 2007 SP3 RU15 en tant que *serveurs Exchange hérités*.

> [!NOTE]
> La méthode de migration par lots décrite dans cet article est la seule méthode prise en charge pour la migration des dossiers publics hérités vers Exchange 2013. L’ancienne méthode de migration de dossiers publics en série est déconseillée et n’est plus prise en charge par Microsoft.


Vous effectuerez la migration à l’aide des cmdlets **\*MigrationBatch** et des cmdlets **\*PublicFolderMigrationRequest** pour la résolution des problèmes. En outre, vous utiliserez les scripts PowerShell suivants :

  - `Export-PublicFolderStatistics.ps1`   Ce script crée le fichier de mappage du nom du dossier à la taille du dossier.

  - ` Export-PublicFolderStatistics.psd1` Ce fichier de support est utilisé par le script Export-PublicFolderStatistics.ps1 et doit être téléchargé au même emplacement.

  - `PublicFolderToMailboxMapGenerator.ps1`   Ce script crée le fichier de mappage du dossier public à la boîte aux lettres.

  - `PublicFolderToMailboxMapGenerator.strings.psd1` Ce fichier de support est utilisé par le script PublicFolderToMailboxMapGenerator.ps1 et doit être téléchargé au même emplacement.

  - `Create-PublicFolderMailboxesForMigration.ps1` Ce script crée les boîtes aux lettres de dossiers publics cibles pour la migration. En outre, ce script calcule le nombre de boîtes aux lettres nécessaires pour gérer la charge utilisateur estimée, en fonction des recommandations relatives au nombre de connexions utilisateurs par boîte aux lettres de dossier public données dans [Limites pour les dossiers publics](limits-for-public-folders-exchange-2013-help.md).

  - `Create-PublicFolderMailboxesForMigration.strings.psd1` Ce fichier de support est utilisé par le script Create-PublicFolderMailboxesForMigration.ps1 et doit être téléchargé au même emplacement.

L’Étape 1 : Téléchargez les scripts de migration fournit des détails sur l’emplacement de téléchargement de ces scripts. Assurez-vous que tous les scripts sont téléchargés au même emplacement.

Pour découvrir d’autres tâches de gestion associées aux dossiers publics, consultez la rubrique [Procédures relatives aux dossiers publics](public-folder-procedures-exchange-2013-help.md).

## Quelles versions d’Exchange sont prises en charge pour la migration des dossiers publics vers Exchange 2013 ?

Exchange prend en charge le déplacement de vos dossiers publics à partir des versions héritées suivantes d’Exchange Server :

  - Exchange 2010 SP3 RU8 ou version ultérieure

  - Exchange 2007 SP3 RU15 ou version ultérieure

Si vous devez déplacer vos dossiers publics vers Exchange 2013, mais que vos serveurs locaux n’exécutent pas les versions de support minimum d’Exchange 2010 ou d’Exchange 2007, consultez la rubrique [Migrer les dossiers publics vers Exchange 2013 à partir de versions antérieures](https://technet.microsoft.com/fr-fr/library/jj150486\(v=exchg.150\)). Bien que la migration en série soit une possibilité, nous vous recommandons vivement de mettre à niveau vos serveurs locaux et d’utiliser la migration par lots. La migration par lots est bien plus rapide et offre une bien meilleure fiabilité.

Vous ne pouvez pas migrer des dossiers publics directement à partir d’Exchange 2003. Si vous exécutez Exchange 2003 dans votre organisation, vous devez déplacer toutes les bases de données de dossiers publics et les réplicas vers Exchange 2010 SP3 RU8 ou une version ultérieure, ou vers Exchange 2007 SP3 RU15 ou une version ultérieure. Aucun réplica de dossier public ne peut rester sur Exchange 2003. En outre, les messages électroniques destinés à un dossier public Exchange 2013 ne peuvent pas être acheminés via un serveur Exchange 2003.

## Ce qu’il faut savoir avant de commencer

  - Avant de commencer, nous vous recommandons de lire cette rubrique dans son intégralité, car un temps mort est nécessaire pour certaines étapes.

  - Le serveur Exchange 2010 doit exécuter Exchange 2010 SP3 RU8 ou une version ultérieure.

  - Le serveur Exchange 2007 doit exécuter Exchange 2007 SP3 RU15 ou une version ultérieure.

  - Le nombre maximal de dossiers publics pouvant être migrés vers Exchange 2013 au sein d’une seule migration est de 500 000.

  - Dans Exchange 2013, vous devez être membre du groupe de rôles Gestion de l’organisation. Pour plus de détails sur l’activation du groupe de rôles Gestion de l’organisation, consultez la rubrique [Gérer des groupes de rôles](manage-role-groups-exchange-2013-help.md).

  - Dans Exchange 2010, vous devez être membre du groupe de rôles RBAC Gestion de l’organisation ou Gestion du serveur. Pour plus d’informations, consultez la rubrique [Ajouter des membres à un groupe de rôles](https://go.microsoft.com/fwlink/?linkid=299212).

  - Dans Exchange 2007, le rôle Administrateur d’organisation Exchange ou Administrateur d’Exchange Server doit vous être attribué. Le rôle Administrateur de dossiers publics et le groupe Administrateurs local doivent également vous être attribués pour le serveur cible. Pour plus d’informations, consultez la rubrique [Procédure d’ajout d’un utilisateur ou d’un groupe à un rôle d’administrateur](https://go.microsoft.com/fwlink/p/?linkid=81779).

  - Sur le serveur Exchange 2007, effectuez une mise à niveau vers [Windows PowerShell 2.0 et WinRM 2.0 pour Windows Server 2008 x64 Edition](http://go.microsoft.com/fwlink/p/?linkid=3052&kbid=968930).

  - Avant de procéder à la migration, n’oubliez pas de prendre en compte les [Limites pour les dossiers publics](limits-for-public-folders-exchange-2013-help.md).

  - Avant de migrer, déplacez toutes les boîtes aux lettres d’utilisateur vers Exchange 2013, car les utilisateurs avec des boîtes aux lettres Exchange 2007 ou Exchange 2010 n’auront pas accès aux dossiers publics sur Exchange 2013. Pour plus d’informations, consultez la rubrique [Déplacements de boîtes aux lettres dans Exchange 2013](mailbox-moves-in-exchange-2013-exchange-2013-help.md).

  - Dans un environnement à plusieurs domaines, les dossiers publics à extension messagerie fonctionnent plus après la migration vers Exchange 2013 si Exchange s’exécute dans un domaine enfant. C’est parce que dans Exchange 2013, les objets de dossier public à extension messagerie sont requis pour être sous le domaine racine. Pour résoudre ce problème, vous devez désactiver la messagerie vos dossiers publics à extension messagerie et puis activer la messagerie pour les à nouveau, qui vous permet de les déplacer vers l’emplacement de domaine correct.

  - Une fois la migration effectuée, si vous souhaitez que les expéditeurs externes puissent envoyer des messages vers les dossiers publics migrés à extension messagerie, l’utilisateur **Anonyme** doit au moins disposer de l’autorisation **Création d’éléments**. Dans le cas contraire, les expéditeurs externes recevront une notification d’échec de remise et les messages ne seront pas transmis au dossier public migré à extension messagerie. Pour en savoir plus sur la définition d’autorisations pour l’utilisateur Anonyme, reportez-vous à la rubrique [Activation ou désactivation de la messagerie pour un dossier public](mail-enable-or-mail-disable-a-public-folder-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.


## Comment procéder ?

## Étape 1 : Téléchargez les scripts de migration

1.  Téléchargez tous les scripts et les fichiers de support à partir des [scripts de migration de dossiers publics](https://go.microsoft.com/fwlink/?linkid=299838).

2.  Enregistrez les scripts sur l’ordinateur local sur lequel vous exécuterez PowerShell. Par exemple, C:\\PFScripts. Assurez-vous que tous les scripts sont enregistrés au même emplacement.

## Étape 2 : Préparez la migration

Avant de commencer la migration, exécutez les étapes préalables suivantes.

**Étapes préalables sur le serveur Exchange hérité**

1.  À des fins de vérification à la fin de la migration, nous vous recommandons d’exécuter d’abord les commandes suivantes sur le serveur Exchange hérité pour prendre des instantanés de votre déploiement de dossiers publics actuel :
    
      - Exécutez la commande suivante pour prendre un instantané de la structure du dossier source d’origine :
        
            Get-PublicFolder -Recurse | Export-CliXML C:\PFMigration\Legacy_PFStructure.xml
    
      - Exécutez la commande suivante pour prendre un instantané des statistiques du dossier public (nombre d’éléments, taille, et propriétaire) :
        
            Get-PublicFolderStatistics | Export-CliXML C:\PFMigration\Legacy_PFStatistics.xml
    
      - Exécutez la commande suivante pour prendre un instantané des autorisations :
        
            Get-PublicFolder -Recurse | Get-PublicFolderClientPermission | Select-Object Identity,User -ExpandProperty AccessRights | Export-CliXML C:\PFMigration\Legacy_PFPerms.xml
    
    Enregistrez les informations des commandes précédentes à des fins de comparaison une fois la migration terminée.

2.  Si le nom d’un dossier public contient une barre oblique inverse **\\**, les dossiers publics seront créés dans le dossier public parent lors de la migration. Avant de procéder à la migration, il est recommandé de renommer les dossiers publics dont le nom inclut une barre oblique inverse.
    
    1.  Dans Exchange 2010, pour rechercher les dossiers publics dont le nom inclut une barre oblique inverse, exécutez la commande suivante :
        
            Get-PublicFolderStatistics -ResultSize Unlimited | Where {($_.Name -like "*\*") -or ($_.Name -like "*/*") } | Format-List Name, Identity
    
    2.  Dans Exchange 2007, pour rechercher les dossiers publics dont le nom inclut une barre oblique inverse, exécutez la commande suivante :
        
            Get-PublicFolderDatabase | ForEach {Get-PublicFolderStatistics -Server $_.Server | Where {$_.Name -like "*\*"}}
    
    3.  Si des dossiers publics sont renvoyés, vous pouvez les renommer en exécutant la commande suivante :
        
            Set-PublicFolder -Identity <public folder identity> -Name <new public folder name>

3.  Vérifiez qu’il n’existe aucun autre enregistrement d’une migration réussie.
    
    1.  L’exemple suivant vérifie l’état de la migration des dossiers publics.
        
            Get-OrganizationConfig | Format-List PublicFoldersLockedforMigration, PublicFolderMigrationComplete
        
        S’il y a eu une migration précédente, la valeur des propriétés *PublicFoldersLockedforMigration* ou *PublicFolderMigrationComplete* est `$true`. Utilisez la commande de l’étape 3b pour définir la valeur sur `$false`. Si la valeur est définie sur `$true`, votre demande de migration échoue.
    
    2.  Si l’état de la propriété *PublicFoldersLockedforMigration* ou *PublicFolderMigrationComplete* a la valeur `$true`, exécutez la commande suivante pour définir la valeur sur `$false` :
        
            Set-OrganizationConfig -PublicFoldersLockedforMigration:$false -PublicFolderMigrationComplete:$false
    
    > [!WARNING]
    > Après avoir redéfini ces propriétés, attendez qu’Exchange détecte les nouveaux paramètres. Cela peut prendre jusqu’à deux heures.


Pour plus d’informations sur la syntaxe et les paramètres, consultez les rubriques suivantes :

  - [Get-PublicFolder](https://technet.microsoft.com/fr-fr/library/aa997615\(v=exchg.150\))

  - [Get-PublicFolderDatabase](https://technet.microsoft.com/fr-fr/library/jj733416\(v=exchg.150\))

  - [Set-PublicFolder](https://technet.microsoft.com/fr-fr/library/aa998596\(v=exchg.150\))

  - [Get-PublicFolderStatistics](https://technet.microsoft.com/fr-fr/library/aa998663\(v=exchg.150\))

  - [Get-PublicFolderClientPermission](https://technet.microsoft.com/fr-fr/library/bb124365\(v=exchg.150\))

  - [Get-OrganizationConfig](https://go.microsoft.com/fwlink/p/?linkid=183212)

  - [Set-OrganizationConfig](https://go.microsoft.com/fwlink/p/?linkid=183213)

**Étapes préalables sur le serveur Exchange 2013**

1.  Assurez-vous qu’il n’existe aucune demande de migration de dossiers publics. S’il en existe, supprimez-les, sinon, votre propre demande de migration échouera. Cette étape n’est pas obligatoire dans tous les cas. Elle est nécessaire uniquement si vous pensez qu’il peut y avoir une demande de migration existante dans le pipeline.
    
    Une demande de migration existante peut être de deux types : migration par lots ou en série. Les commandes permettant de détecter les demandes pour chaque type et de supprimer des demandes de chaque type sont les suivantes :
    
    > [!NOTE]
    > Avant de supprimer une demande de migration, il est important de comprendre la raison de son existence. L’exécution des commandes suivantes déterminera le moment de la création de la demande précédente et vous permettra de diagnostiquer les problèmes qui ont pu se produire. Pour déterminer la raison du changement, il se peut que vous deviez communiquer avec d’autres administrateurs de votre organisation.
    
    L’exemple suivant permet de détecter les demandes de migration en série existantes.
    
        Get-PublicFolderMigrationRequest | Get-PublicFolderMigrationRequestStatistics -IncludeReport | Format-List
    
    L’exemple suivant supprime toutes les demandes de migration en série de dossiers publics.
    
        Get-PublicFolderMigrationRequest | Remove-PublicFolderMigrationRequest
    
    L’exemple suivant permet de détecter toute demande de migration par lots.
    
        $batch = Get-MigrationBatch | ?{$_.MigrationType.ToString() -eq "PublicFolder"}
    
    L’exemple suivant supprime toutes les demandes de migration par lots de dossiers publics.
    
        $batch | Remove-MigrationBatch -Confirm:$false

2.  Vérifiez qu’aucun dossier public ou boîte aux lettres de dossiers publics n’existe sur les serveurs Exchange 2013.
    
    1.  Exécutez la commande suivante pour déterminer s’il existe des boîtes aux lettres de dossiers publics.
        
            Get-Mailbox -PublicFolder 
    
    2.  Si la commande n’a pas renvoyé de boîte aux lettres de dossiers publics, passez à l’Step 3: Generate the CSV files. Si la commande a renvoyé des dossiers publics, exécutez la commande suivante pour voir s’il existe des dossiers publics :
        
            Get-PublicFolder
    
    3.  Si vous avez des dossiers publics, exécutez les commandes PowerShell suivantes pour les supprimer. Assurez-vous que vous avez enregistré les informations présentes dans les dossiers publics.
        
        > [!NOTE]
        > Toutes les informations contenues dans les dossiers publics sont définitivement effacées lorsque vous les supprimez.
        ```
            Get-Mailbox -PublicFolder | Where{$_.IsRootPublicFolderMailbox -eq $false} | Remove-Mailbox -PublicFolder -Force -Confirm:$false
        ```
        ```
            Get-Mailbox -PublicFolder | Remove-Mailbox -PublicFolder -Force -Confirm:$false
        ```
Pour plus d’informations sur la syntaxe et les paramètres, consultez les rubriques suivantes :

  - [Get-MigrationBatch](https://technet.microsoft.com/fr-fr/library/jj219164\(v=exchg.150\))

  - [Get-PublicFolderMigrationRequest](https://technet.microsoft.com/fr-fr/library/jj218718\(v=exchg.150\))

  - [Remove-PublicFolderMigrationRequest](https://technet.microsoft.com/fr-fr/library/jj218625\(v=exchg.150\))

  - [Get-Mailbox](https://technet.microsoft.com/fr-fr/library/bb123685\(v=exchg.150\))

  - [Get-PublicFolder](https://technet.microsoft.com/fr-fr/library/aa997615\(v=exchg.150\))

  - [Get-MailPublicFolder](https://technet.microsoft.com/fr-fr/library/bb124772\(v=exchg.150\))

  - [Disable-MailPublicFolder](https://technet.microsoft.com/fr-fr/library/bb123781\(v=exchg.150\))

  - [Remove-PublicFolder](https://technet.microsoft.com/fr-fr/library/bb124894\(v=exchg.150\))

  - [Remove-Mailbox](https://technet.microsoft.com/fr-fr/library/aa995948\(v=exchg.150\))

## Étape 3 : Générez les fichiers .csv

1.  Sur le serveur Exchange hérité, exécutez le script `Export-PublicFolderStatistics.ps1` pour créer le fichier de mappage de nom de dossier à taille de dossier. Ce script doit être exécuté par un administrateur local. Le fichier contient deux colonnes : **FolderName** et **FolderSize**. Les valeurs de la colonne **FolderSize** s’affichent en octets. Par exemple, **\\PublicFolder01,10000**.
    
        .\Export-PublicFolderStatistics.ps1  <Folder to size map path> <FQDN of source server>
    
      - *FQDN of source server* correspond au nom de domaine complet du serveur de boîtes aux lettres hébergeant la hiérarchie de dossiers publics.
    
      - *Folder to size map path* correspond au nom de fichier et au chemin d’accès d’un dossier partagé sur le réseau où vous souhaitez enregistrer le fichier .csv. Plus loin dans cette rubrique, vous devez accéder à ce fichier à partir du serveur Exchange 2013. Si vous spécifiez uniquement le nom du fichier, ce dernier est généré dans le répertoire PowerShell actuel sur l’ordinateur local.

2.  Pour créer le fichier de mappage de dossier public à boîte aux lettres, exécutez le script `PublicFolderToMailboxMapGenerator.ps1`. Ce fichier est utilisé pour calculer le nombre correct de boîtes aux lettres de dossiers publics sur le serveur de boîte aux lettres Exchange 2013.
    
    > [!NOTE]
    > Si le nom d’un dossier public contient une barre oblique inverse <strong>\</strong>, les dossiers publics seront créés dans le dossier public parent. Nous vous recommandons d’examiner le fichier .csv et de modifier les noms contenant une barre oblique inverse.
    
        .\PublicFolderToMailboxMapGenerator.ps1 <Maximum mailbox size in bytes> <Folder to size map path> <Folder to mailbox map path>
    
      - *Maximum mailbox size in bytes* correspond à la taille maximale que vous souhaitez définir pour les nouvelles boîtes aux lettres de dossiers publics. Lors de la définition de ce paramètre, veillez à permettre le développement de la boîte aux lettres de dossiers publics en faisant en sorte qu’elle ait suffisamment d’espace pour augmenter en taille.
    
      - *Folder to size map path* correspond au chemin d’accès au fichier .csv que vous avez créé lors de l’exécution du script `Export-PublicFolderStatistics.ps1`.
    
      - *Folder to mailbox map path* correspond au nom de fichier et au chemin d’accès au fichier .csv de mappage du dossier à la boîte aux lettres que vous allez créer lors de cette étape. Si vous spécifiez uniquement le nom du fichier, ce dernier est généré dans le répertoire PowerShell actuel sur l’ordinateur local.

## Étape 4 : Créez des boîtes aux lettres de dossiers publics dans Exchange 2013

1.  Exécutez la commande suivante pour créer les boîtes aux lettres de dossier public cible. Le script crée une boîte aux lettres cible pour chaque boîte aux lettres dans le fichier .csv que vous avez généré à l’étape 3, en exécutant le script PublicFoldertoMailboxMapGenerator.ps1.
    
        .\Create-PublicFolderMailboxesForMigration.ps1 -FolderMappingCsv Mapping.csv -EstimatedNumberOfConcurrentUsers:<estimate>
    
    *Mapping.csv* est le fichier généré par le script PublicFoldertoMailboxMapGenerator.ps1 à l’étape 3. Le nombre estimé de connexions utilisateur simultanées parcourant une hiérarchie de dossiers publics est généralement inférieur au nombre total d’utilisateurs dans une organisation.

## Étape 5 : Lancez la demande de migration

Les étapes de migration des dossiers publics Exchange 2007 sont différentes de celles associées à la migration des dossiers publics Exchange 2010.

> [!TIP]
> Que la migration soit effectuée d’Exchange 2007 ou d’Exchange 2010, une fois que les demandes de migration par lots sont créées avec la cmdlet appropriée, vous pouvez afficher les demandes et les gérer dans le CAE.


**Migration des dossiers publics Exchange 2007**

1.  Les dossiers publics système hérités comme OWAScratchPad et la sous-arborescence du dossier racine du schéma dans Exchange 2007 ne seront pas reconnus par Exchange 2013 et seront donc traités comme des éléments « incorrects ». Cela entraînera l’échec de la migration. Dans le cadre de la demande de migration, vous devez spécifier une valeur pour le paramètre `BadItemLimit`. Celle-ci dépend du nombre de bases de données de dossiers publics que vous possédez. Les commandes suivantes déterminent le nombre de bases de données de dossiers publics que vous possédez et calculent la limite `BadItemLimit` pour la demande de migration.
    
        $PublicFolderDatabasesInOrg = @(Get-PublicFolderDatabase)
    
        $BadItemLimitCount = 5 + ($PublicFolderDatabasesInOrg.Count -1)

2.  Sur le serveur Exchange 2013, exécutez la commande suivante :
    
        New-MigrationBatch -Name PFMigration -SourcePublicFolderDatabase (Get-PublicFolderDatabase -Server <Source server name>) -CSVData (Get-Content <Folder to mailbox map path> -Encoding Byte) -NotificationEmails <email addresses for migration notifications> -BadItemLimit $BadItemLimitCount 

3.  Lancez la migration à l’aide de la commande suivante :
    
        Start-MigrationBatch PFMigration

**Migration des dossiers publics Exchange 2010**

1.  Sur le serveur Exchange 2013, exécutez la commande suivante.
    
        New-MigrationBatch -Name PFMigration -SourcePublicFolderDatabase (Get-PublicFolderDatabase -Server <Source server name>) -CSVData (Get-Content <Folder to mailbox map path> -Encoding Byte) -NotificationEmails <email addresses for migration notifications> 
    
    Le paramètre `NotificationEmails` est facultatif.

2.  Lancez la migration à l’aide de la commande suivante :
    
        Start-MigrationBatch PFMigration
    
    Ou :
    
    Vous pouvez démarrer la migration dans le CAE.
    
    1.  Connectez-vous à Exchange Online et ouvrez le CAE.
    
    2.  Accédez à **Destinataires**\>**Migration**.
    
    3.  Sélectionnez le lot de migration que vous venez de créer, puis cliquez sur le bouton Démarrer.

La colonne **Statut** indique le statut du lot initial comme **Créé**. Le statut devient **Synchronisation** pendant la migration. Lorsque la demande de migration est terminée, le statut sera **Synchronisé**. Vous pouvez double-cliquer sur un lot pour afficher le statut de boîtes aux lettres individuelles dans le lot. Les tâches de boîte aux lettres commencent par le statut **En file d’attente**. Lorsque la tâche commence, le statut est **Synchronisation** et, une fois que la `InitialSync` est terminée, le statut affichera **Synchronisé**.

La progression et l’achèvement de la migration peuvent être affichés et gérés dans le CAE. Étant donné que la cmdlet **New-MigrationBatch** lance une demande de migration de boîte aux lettres pour chaque boîte aux lettres de dossiers publics, vous pouvez consulter l’état de ces demandes à l’aide de la page de migration de boîte aux lettres. Pour accéder à cette page et créer des rapports de migration qui peuvent vous être envoyés par courrier électronique, procédez comme suit :

1.  Connectez-vous à Exchange Online et ouvrez le CAE.

2.  Accédez à **Boîte aux lettres** \> **Migration**.

3.  Sélectionnez la demande de migration qui vient d’être créée, puis cliquez sur **Afficher les détails** dans le volet **Détails**.

Pour plus d’informations sur la syntaxe et les paramètres, consultez les rubriques suivantes :

  - [New-PublicFolderMigrationRequest](https://technet.microsoft.com/fr-fr/library/jj218636\(v=exchg.150\))

  - [Get-PublicFolderDatabase](https://technet.microsoft.com/fr-fr/library/jj733416\(v=exchg.150\))

  - [Get-PublicFolderMigrationRequest](https://technet.microsoft.com/fr-fr/library/jj218718\(v=exchg.150\))

  - [Get-PublicFolderMigrationRequestStatistics](https://technet.microsoft.com/fr-fr/library/jj218697\(v=exchg.150\))

## Étape 6 : Verrouillez les dossiers publics sur le serveur Exchange hérité pour la migration finale (temps mort requis)

Jusqu’à ce stade de la migration, les utilisateurs pouvaient accéder aux dossiers publics. Au cours des étapes suivantes, les utilisateurs seront déconnectés des dossiers publics hérités, et les dossiers seront verrouillés jusqu’à ce que la synchronisation finale de la migration soit terminée. Les utilisateurs ne pourront pas accéder aux dossiers publics durant cette procédure. En outre, les messages électroniques envoyés aux dossiers publics à extension messagerie seront mis en file d’attente et ne seront pas remis tant que la migration des dossiers publics ne sera pas terminée.

Avant d’exécuter la commande `PublicFoldersLockedForMigration` comme décrit ci-dessous, assurez-vous que tous les travaux sont dans l’état **Synchronisé**. Pour cela, exécutez la commande `Get-PublicFolderMailboxMigrationRequest`. Passez à cette étape uniquement une fois que vous avez vérifié que tous les travaux sont dans l’état **Synchronisé**.

Sur le serveur Exchange hérité, exécutez la commande suivante pour verrouiller les dossiers publics hérités le temps que la migration s’achève.

    Set-OrganizationConfig -PublicFoldersLockedForMigration:$true

> [!NOTE]
> Si, pour une raison quelconque, le fichier de commandes de migration n’est pas finalisé (<strong>PublicFolderMigrationComplete</strong> affiche <strong>False</strong>), redémarrez la banque d’informations (IS) sur le serveur hérité.


Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Set-OrganizationConfig](https://technet.microsoft.com/fr-fr/library/aa997443\(v=exchg.150\)).

Si votre organisation possède plusieurs bases de données de dossiers publics, vous devrez attendre la fin de la réplication des dossiers publics pour confirmer que toutes les bases de données de dossiers publics présentent l’indicateur `PublicFoldersLockedForMigration` et que les modifications en attente que les utilisateurs ont récemment apportées aux dossiers se sont répercutées dans l’ensemble de l’organisation. Cela peut prendre plusieurs heures.

## Étape 7 : Finaliser la migration des dossiers publics (temps d’arrêt requis)

Commencez par exécuter la cmdlet suivante pour remplacer le type de déploiement Exchange 2013 par **Remote** :

    Set-OrganizationConfig -PublicFoldersEnabled Remote

Vous pouvez ensuite effectuer la migration de dossier public en exécutant la commande suivante :

    Complete-MigrationBatch PublicFolderMigration

Ou, dans le CAE, vous pouvez effectuer la migration en cliquant sur **Terminer ce lot de migration**.

Lors de la migration, Exchange effectue une synchronisation finale entre le serveur Exchange hérité et Exchange 2013. Si la synchronisation finale fonctionne, les dossiers publics présents sur le serveur Exchange 2013 sont déverrouillés et le statut du lot de migration passe à **Finalisation en cours** puis à **Terminé**. Le statut du lot de migration met généralement quelques heures à passer de **Synchronisé** à **Finalisation en cours**, moment auquel la synchronisation commence.

## Étape 8 : Testez et déverrouillez la migration des dossiers publics

Une fois la migration des dossiers publics finalisée, vous devez exécuter le test suivant pour vous assurer de sa réussite. Cette opération vous permet de tester la hiérarchie de dossiers publics migrée avant d’utiliser les dossiers publics Exchange 2013.

1.  Dans PowerShell, exécutez la commande suivante pour attribuer des boîtes aux lettres de test et utiliser une boîte aux lettres de dossiers publics récemment migrée comme boîte aux lettres de dossiers publics par défaut.
    
        Set-Mailbox -Identity <Test User> -DefaultPublicFolderMailbox <Public Folder Mailbox Identity>

2.  Connectez-vous à Outlook 2007 (ou version ultérieure) avec l’utilisateur test identifié à l’étape précédente, puis exécutez les tests de dossiers publics suivants :
    
      - Affichez la hiérarchie.
    
      - Vérifiez les autorisations.
    
      - Créez et supprimez des dossiers publics.
    
      - Publiez ou effacez du contenu dans un dossier public.

3.  Si vous rencontrez des problèmes, consultez la section Roll back the migration plus loin dans cette rubrique. Si le contenu et la hiérarchie des dossiers publics sont acceptables et fonctionnent comme prévu, exécutez la commande suivante pour déverrouiller les dossiers publics pour l’ensemble des autres utilisateurs.
    
        Get-Mailbox -PublicFolder | Set-Mailbox -PublicFolder -IsExcludedFromServingHierarchy $false
    
    > [!NOTE]
    > N’utilisez pas le paramètre <em>IsExcludedFromServingHierarchy</em> après la validation de la migration initiale, car ce paramètre est utilisé par le service de gestion automatisée du stockage pour Exchange Online.


4.  Sur le serveur Exchange hérité, exécutez la commande suivante pour indiquer que la migration de dossiers publics est terminée :
    
        Set-OrganizationConfig -PublicFolderMigrationComplete:$true

5.  Une fois que vous avez vérifié que la migration est terminée, exécutez la commande suivante :
    
        Set-OrganizationConfig -PublicFoldersEnabled Local

6.  Enfin, si vous souhaitez que les expéditeurs externes puissent envoyer des messages vers des dossiers publics migrés à extension messagerie, l’utilisateur **Anonyme** doit disposer au moins de l’autorisation **Création d’éléments**. Dans le cas contraire, les expéditeurs externes recevront une notification d’échec de remise et les messages ne seront pas transmis au dossier public migré à extension messagerie.
    
    Vous pouvez utiliser l’environnement de ligne de commande Exchange Management Shell ou Outlook pour définir les autorisations de l’utilisateur Anonyme. Pour en savoir plus sur la définition des autorisations de l’utilisateur Anonyme, consultez la rubrique [Activation ou désactivation de la messagerie pour un dossier public](mail-enable-or-mail-disable-a-public-folder-exchange-2013-help.md).

## Comment savoir si cela a fonctionné ?

À l’Step 2: Prepare for the migration, il vous a été demandé de prendre des instantanés de la structure, des statistiques et des autorisations des dossiers publics avant de lancer la migration. Les étapes suivantes vous permettent de vérifier que votre migration de dossiers publics s’est correctement déroulée en prenant les mêmes instantanés à la fin de la migration. Vous pouvez ensuite comparer les données des deux fichiers pour vérifier la réussite de l’opération.

1.  Exécutez la commande suivante pour prendre un instantané de la nouvelle structure de dossiers.
    
        Get-PublicFolder -Recurse | Export-CliXML C:\PFMigration\Cloud_PFStructure.xml

2.  Exécutez la commande suivante pour prendre un instantané des statistiques de dossiers publics, telles que le nombre d’éléments, la taille et le propriétaire :
    
        Get-PublicFolderStatistics -ResultSize Unlimited | Export-CliXML C:\PFMigration\Cloud_PFStatistics.xml

3.  Pour prendre un instantané des autorisations, exécutez la commande suivante :
    
        Get-PublicFolder -Recurse | Get-PublicFolderClientPermission | Select-Object Identity,User -ExpandProperty AccessRights | Export-CliXML  C:\PFMigration\Cloud_PFPerms.xml

## Suppression des bases de données de dossiers publics des serveurs Exchange hérités

À la fin de la migration, lorsque vous avez vérifié que les dossiers publics Exchange 2013 fonctionnent comme prévu, vous devez supprimer les bases de données de dossiers publics sur les serveurs Exchange hérités.

  - Pour plus d’informations sur la suppression des bases de données de dossiers publics des serveurs Exchange 2007, consultez la rubrique [Suppression de bases de données de dossiers publics](https://go.microsoft.com/fwlink/?linkid=123678).

  - Pour plus d’informations sur la suppression des bases de données de dossiers publics des serveurs Exchange 2010, consultez la rubrique [Supprimer des bases de données de dossiers publics](https://go.microsoft.com/fwlink/?linkid=81409).

## Annulation de la migration

Si vous rencontrez des problèmes en relation avec la migration et devez réactiver vos dossiers publics Exchange hérités, procédez comme suit :

> [!WARNING]
> Si vous annulez votre migration vers les serveurs Exchange hérités, vous perdrez les courriers électroniques envoyés aux dossiers publics à extension messagerie ou le contenu publié dans des dossiers publics dans Exchange 2013 après la migration. Pour sauvegarder ce contenu, exportez le contenu des dossiers publics dans un fichier .pst, puis importez-le dans les dossiers publics hérités une fois la restauration terminée.


1.  Sur le serveur Exchange hérité, exécutez la commande suivante pour déverrouiller les dossiers publics Exchange hérités. Ce processus peut prendre plusieurs heures.
    
        Set-OrganizationConfig -PublicFoldersLockedForMigration:$False

2.  Sur le serveur Exchange 2013, exécutez les commandes suivantes pour supprimer les boîtes aux lettres de dossiers publics.
    
        Get-Mailbox -PublicFolder | Where{$_.IsRootPublicFolderMailbox -eq $false} | Remove-Mailbox -PublicFolder -Force -Confirm:$false
        
        Get-Mailbox -PublicFolder | Remove-Mailbox -PublicFolder -Force -Confirm:$false

3.  Sur le serveur Exchange hérité, exécutez la commande suivante pour régler l’indicateur `PublicFolderMigrationComplete` sur `$false`.
    
        Set-OrganizationConfig -PublicFolderMigrationComplete:$False

