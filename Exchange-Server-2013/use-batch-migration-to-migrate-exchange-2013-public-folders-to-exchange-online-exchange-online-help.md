---
title: 'Migration par lot de dossiers publics Exchange 2013 vers Exchange Online'
TOCTitle: Utilisation de la migration par lot pour migrer des dossiers publics Exchange 2013 vers Exchange Online
ms:assetid: 25a5234c-dd2c-487b-8541-3655fbeb030a
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Mt798260(v=EXCHG.150)
ms:contentKeyID: 74432746
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Utilisation de la migration par lot pour migrer des dossiers publics Exchange 2013 vers Exchange Online

 

_**Dernière rubrique modifiée :** 2018-03-26_

**Résumé** : Cet article explique comment déplacer des dossiers publics modernes d’Exchange 2013 vers Office 365.

Migration de vos dossiers publics Exchange 2013 vers Exchange Online requiert Exchange Server 2013 CU15 ou version ultérieure dans votre environnement local.

> [!NOTE]
> Si votre organisation comporte à la fois des dossiers publics Exchange 2013 et Exchange 2016, et que vous voulez les déplacer vers Exchange Online, utilisez la <a href="https://go.microsoft.com/fwlink/p/?linkid=845314">version de cet article pour Exchange 2016</a> afin de planifier et d’exécuter la migration. La mise à jour cumulative CU15 ou une version ultérieure doit toujours être installée sur vos serveurs Exchange 2013.


## Ce que vous devez savoir avant de commencer

  - Lorsque vous effectuez une mise à niveau vers Exchange Server 2013 CU15 ou version ultérieure, vous devez également préparer Active Directory, faute de quoi la migration de vos dossiers publics échouera. Cette préparation d’Active Directory permet de s’assurer que l’ensemble des cmdlets PowerShell et des paramètres requis sont disponibles pour la préparation et la migration. Pour plus d’informations, voir la rubrique [Préparation d’Active Directory et des domaines](prepare-active-directory-and-domains-exchange-2013-help.md).

  - Dans Exchange Online, vous devez être membre du groupe de rôles Gestion de l’organisation. Ce groupe de rôles diffère des autorisations qui vous sont attribuées quand vous vous abonnez à Office 365 ou à Exchange Online. Pour plus de détails sur l’activation du groupe de rôles Gestion de l’organisation, consultez la rubrique [Gérer des groupes de rôles](manage-role-groups-exchange-2013-help.md).

  - Dans Exchange Server 2013, vous devez être membre du groupe de rôles RBAC Gestion de l’organisation ou Gestion du serveur. Pour plus d’informations, consultez la rubrique [Ajouter des membres à un groupe de rôles](https://go.microsoft.com/fwlink/?linkid=299212).

  - Avant de commencer la migration des dossiers publics, si un dossier public de votre organisation est supérieur à 25 Go, nous vous recommandons d’en supprimer du contenu pour le rendre plus petit, ou de répartir ce contenu dans plusieurs dossiers publics plus petits. Notez que la limite de 25 Go mentionnée ici s’applique uniquement au dossier public et non aux dossiers enfant ou aux sous-dossiers du dossier en question. Si aucune de ces options n’est envisageable, nous vous recommandons de ne pas déplacer vos dossiers publics vers Exchange Online. Pour plus d’informations, reportez-vous à [Limites d’Exchange Online](http://go.microsoft.com/fwlink/p/?linkid=391188).
    
    > [!NOTE]
    > Si vos quotas actuels pour les dossiers publics dans Exchange Online sont inférieurs à 25 Go, vous pouvez utiliser la <a href="https://go.microsoft.com/fwlink/p/?linkid=844062">cmdlet Set-OrganizationConfig</a> pour les augmenter avec les paramètres DefaultPublicFolderIssueWarningQuota et DefaultPublicFolderProhibitPostQuota.


  - Dans Office 365 et Exchange Online, vous pouvez créer 1 000 boîtes aux lettres de dossier public au maximum.

  - Si vous avez l’intention de migrer des utilisateurs vers Office 365, vous devez effectuer la migration de vos utilisateurs avant de migrer vos dossiers publics. Pour plus d’informations, reportez-vous à [Méthodes de migration des comptes de messagerie vers Office 365](https://go.microsoft.com/fwlink/p/?linkid=842798).

  - Le proxy MRS doit être activé sur au moins un serveur Exchange, lequel doit également héberger les boîtes aux lettres de dossier public. Pour plus d’informations, voir [Activation du point de terminaison du proxy MRS pour les déplacements distants](enable-the-mrs-proxy-endpoint-for-remote-moves-exchange-2013-help.md).

  - Pour effectuer les procédures de migration décrites dans cet article, vous ne pouvez pas utiliser le centre d’administration Exchange. Vous devez utiliser l’environnement de ligne de commande Exchange Management Shell sur vos serveurs Exchange 2013. Dans Exchange Online, vous devez utiliser Exchange Online PowerShell. Pour plus d’informations, reportez-vous à [Connexion à Exchange Online](http://go.microsoft.com/fwlink/p/?linkid=842801).

  - La migration d’éléments et de dossiers supprimés d’Exchange 2013 vers Exchange Online est prise en charge. Avant de commencer la migration, nous vous recommandons de vérifier tous les dossiers et éléments de dossier supprimés, et de supprimer définitivement tout ce dont vous n’aurez pas besoin dans Exchange Online. Notez que les éléments supprimés définitivement ne peuvent pas être récupérés.
    
    Vous pouvez utiliser les commandes suivantes pour obtenir la liste des dossiers publics supprimés présents dans le conteneur de dépôt Exchange (dans votre environnement Exchange local) :
    
        Get-PublicFolder \NON_IPM_SUBTREE\DUMPSTER_ROOT -Recurse | ?{$_.FolderClass -ne "$null"} | ft name,foldersize
    
    Pour supprimer définitivement un dossier spécifique, utilisez la commande suivante (cet exemple utilise un dossier nommé « Calendar2 ») :
    
        Get-PublicFolder \NON_IPM_SUBTREE\DUMPSTER_ROOT -Recurse | ?{$_.FolderClass -ne "$null" -and $_.Name -eq "Calendar2"} | Remove-PublicFolder

  - Avant de commencer, lisez cet article dans son intégralité. Certaines étapes requièrent l’arrêt du système. Pendant ce temps d’arrêt, les dossiers publics ne seront accessibles par personne.

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.


## Étape 1 : Téléchargez les scripts de migration

1.  Téléchargez tous les scripts et les fichiers de support à partir des [scripts de migration de dossiers publics Exchange 2013/2016](https://go.microsoft.com/fwlink/p/?linkid=844893).

2.  Enregistrez les scripts sur l’ordinateur local sur lequel vous exécuterez PowerShell. Par exemple, C:\\PFScripts. Assurez-vous que tous les scripts sont enregistrés au même emplacement.

Les scripts et les fichiers que vous téléchargez sont les suivants :

  - `Sync-ModernMailPublicFolders.ps1`   Ce script synchronise les objets de dossier public à extension messagerie entre votre environnement Exchange local et Office 365. Vous exécuterez ce script sur un serveur Exchange 2013.

  - `SyncModernMailPublicFolders.strings.psd1` Ce fichier de support est utilisé par le script Sync-ModernMailPublicFolders.ps1 et doit être téléchargé au même emplacement.

  - `Export-ModernPublicFolderStatistics.ps1`   Ce script crée le fichier de mappage entre les noms de dossier et les tailles de dossier et d’élément supprimé. Vous exécuterez ce script sur le serveur Exchange 2013.

  - `Export-ModernPublicFolderStatistics.strings.psd1` Ce fichier de support est utilisé par le script Export-ModernPublicFolderStatistics.ps1 et doit être téléchargé au même emplacement.

  - `ModernPublicFolderToMailboxMapGenerator.ps1` Ce script crée le fichier de mappage dossier public-boîte aux lettres en utilisant les résultats du script Export-ModernPublicFolderStatistics.ps1. Vous exécuterez ce script sur un serveur Exchange 2013.

  - `ModernPublicFolderToMailboxMapGenerator.strings.psd1` Ce fichier de support est utilisé par le script ModernPublicFolderToMailboxMapGenerator.ps1 et doit être téléchargé au même emplacement.

  - `SetMailPublicFolderExternalAddress.ps1` Ce script met à jour la valeur `ExternalEmailAddress` des dossiers publics à extension messagerie de votre environnement local en la définissant sur celle de leurs équivalents Exchange Online. Cela garantit que, après la migration, les e-mails adressés aux dossiers publics à extension messagerie sont correctement acheminés vers Exchange Online. Vous devez exécuter ce script sur un serveur Exchange 2013.

  - `SetMailPublicFolderExternalAddress.strings.psd1` Ce fichier de support est utilisé par le script SetMailPublicFolderExternalAddress.ps1 et doit être téléchargé au même emplacement.

## Étape 2 : Préparez la migration

Effectuez toutes les opérations préliminaires décrites dans les sections suivantes avant de commencer la migration des dossiers publics.

**Étapes préalables générales**

Pour réussir votre migration, procédez comme suit :

  - Assurez-vous qu’il n’existe aucun objet de messagerie de dossier public orphelin dans Active Directory. Il s’agit des objets présents dans Active Directory qui n’ont pas d’objet correspondant dans Exchange.

  - Vérifiez que les adresses de messagerie SMTP configurées pour les dossiers publics dans Active Directory correspondent aux adresses de messagerie SMTP sur les objets Exchange.

  - Vérifiez qu’il n’existe aucun objet de dossier public en double dans Active Directory. Cette précaution est nécessaire pour éviter que deux objets Active Directory ou plus ne pointent vers le même dossier public à extension messagerie.

**Opérations préliminaires dans l’environnement de serveur Exchange 2013 local**

Dans l’environnement de ligne de commande Exchange Management Shell (en local) effectuez les opérations suivantes :

1.  Une fois votre migration terminée, les caches DNS sur Internet mettront un certain temps à diriger les messages adressés à vos dossiers publics à extension messagerie vers leur nouvel emplacement dans Exchange Online. Pour vous assurer que les dossiers publics à extension messagerie migrés reçoivent les messages pendant cette période de transition de DNS, vous pouvez créer un domaine accepté avec un nom connu. Pour ce faire, exécutez la commande suivante dans votre environnement Exchange local. Dans cet exemple, `target domain` est votre domaine Office 365 ou Exchange Online, pour lequel un connecteur d’envoi a déjà été configuré par l’assistant de configuration hybride.
    
        New-AcceptedDomain -Name PublicFolderDestination_78c0b207_5ad2_4fee_8cb9_f373175b3f99 -DomainName <target domain> -DomainType InternalRelay
    
    **Exemple** :
    
        New-AcceptedDomain -Name PublicFolderDestination_78c0b207_5ad2_4fee_8cb9_f373175b3f99 -DomainName "contoso.mail.onmicrosoft.com" -DomainType InternalRelay
    
    Si le domaine accepté existe déjà dans votre environnement local, renommez-le `PublicFolderDestination_78c0b207_5ad2_4fee_8cb9_f373175b3f99` et laissez les autres attributs intacts.
    
    Pour vérifier si le domaine accepté est déjà présent dans votre environnement local, procédez comme suit :
    
        Get-AcceptedDomain | Where { $_.DomainName -eq "<target domain>" }
    
    Pour renommer le domaine accepté `PublicFolderDestination_78c0b207_5ad2_4fee_8cb9_f373175b3f99`, exécutez la commande suivante :
    
        Get-AcceptedDomain | Where { $_.DomainName -eq "<target domain>" } | Set-AcceptedDomain -Name PublicFolderDestination_78c0b207_5ad2_4fee_8cb9_f373175b3f99
    
    > [!NOTE]
    > Si vous souhaitez que vos dossiers publics à extension messagerie dans Exchange Online reçoivent des messages électroniques externes à partir d’Internet, vous devez désactiver le blocage du périmètre basé sur l’annuaire (DBEB) dans Exchange Online et Exchange Online Protection (EOP). Pour plus d’informations, voir <a href="https://technet.microsoft.com/fr-fr/library/dn600322(v=exchg.150)">Utiliser le blocage du périmètre basé sur l’annuaire pour rejeter les messages envoyés à des destinataires non valides</a>.


2.  Si le nom d’un dossier public contient une barre oblique inverse **\\** ou une barre oblique **/**, il se peut que le dossier ne soit pas migré vers la boîte aux lettres désignée pendant la migration. Avant d’effectuer la migration, renommez ces dossiers pour supprimer ces caractères.
    
    1.  Pour rechercher les dossiers publics dont le nom inclut une barre oblique inverse, exécutez la commande suivante :
        
            Get-PublicFolder -Recurse -ResultSize Unlimited | Where {$_.Name -like "*\*" -or $_.Name -like "*/*"} | Format-List Name, Identity, EntryId
    
    2.  Si des dossiers publics sont renvoyés, vous pouvez les renommer en exécutant la commande suivante :
        
            Set-PublicFolder -Identity "<public folder EntryId>" -Name "<new public folder name>"

3.  Procédez comme suit pour vérifier qu’il n’y ait pas d’enregistrement d’une précédente migration réussie dans votre organisation. S’il en existe un, vous devez définir cette valeur sur `$false`.
    
    Avant de modifier les valeurs, vérifiez que la précédente tentative de migration peut être annulée afin de ne pas effectuer accidentellement une seconde migration.
    
    1.  Exécutez la commande suivante pour rechercher d’éventuelles migrations précédentes et en vérifier le statut :
        
            Get-OrganizationConfig | Format-List PublicFoldersLockedforMigration, PublicFolderMigrationComplete, PublicFolderMailboxesLockedForNewConnections, PublicFolderMailboxesMigrationComplete
        
        > [!NOTE]
        > Si le paramètre <code>PublicFoldersLockedforMigration</code> ou <code>PublicFolderMigrationComplete</code> est <code>$true</code>, cela signifie que vous avez déjà migré des dossiers publics hérités auparavant. Vérifiez que les bases de données de dossiers publics héritées ont été désactivées avant de passer à l’étape 3b.
    
    2.  Si l’un des éléments ci-dessus est renvoyé avec la valeur `$true`, définissez-le sur `$false` en exécutant la commande suivante :
        
            Set-OrganizationConfig -PublicFoldersLockedforMigration:$false -PublicFolderMigrationComplete:$false -PublicFolderMailboxesLockedForNewConnections:$false -PublicFolderMailboxesMigrationComplete:$false

4.  Afin de vérifier la réussite de la migration une fois qu’elle est terminée, nous vous recommandons d’exécuter les commandes suivantes sur tous les serveurs Exchange 2013 appropriés. Cette opération crée des instantanés de votre déploiement de dossiers publics actuel, lesquels peuvent ensuite être comparés à vos dossiers publics nouvellement migrés.
    
    > [!NOTE]
    > Selon la taille de votre organisation Exchange, l’exécution de ces commandes peut prendre du temps.
    
      - Exécutez la commande suivante pour prendre un instantané de la structure de dossiers publics d'origine :
        
            Get-PublicFolder -Recurse -ResultSize Unlimited | Export-CliXML OnPrem_PFStructure.xml
    
      - Pour prendre un instantané des statistiques de dossiers publics, telles que le nombre, la taille et le propriétaire d’éléments, exécutez la commande suivante :
        
            Get-PublicFolderStatistics -ResultSize Unlimited | Export-CliXML OnPrem_PFStatistics.xml
    
      - Exécutez la commande suivante pour prendre un instantané des autorisations de dossier public :
        
            Get-PublicFolder -Recurse -ResultSize Unlimited | Get-PublicFolderClientPermission | Select-Object Identity,User -ExpandProperty AccessRights | Export-CliXML OnPrem_PFPerms.xml
    
      - Exécutez la commande suivante pour créer un instantané de vos dossiers publics à extension messagerie :
        
            Get-MailPublicFolder -ResultSize Unlimited | Export-CliXML OnPrem_MEPF.xml
    
      - Enregistrez les fichiers générés par les commandes précédentes dans un emplacement sûr afin d’effectuer une comparaison à la fin de la migration.

5.  Si vous utilisez Microsoft Azure Active Directory se connecter (Connect de publicité Azure) pour synchroniser les répertoires locaux avec Azure Active Directory, vous devez prendre les mesures suivantes (si vous n’utilisez pas d’Azure Connect d’Active Directory, vous pouvez ignorer cette étape) :
    
    1.  Sur un ordinateur local, ouvrez Microsoft Azure Active Directory Connect, puis sélectionnez **Configurer**.
    
    2.  Sur l’écran **Tâches supplémentaires**, sélectionnez **Personnaliser les options de synchronisation**, puis cliquez sur **Suivant**.
    
    3.  Sur l’écran **Connexion à Azure AD**, entrez les informations d’identification, puis cliquez sur **Suivant**. Une fois connecté, continuez à cliquer sur **Suivant** jusqu’à ce que vous accédiez à l’écran **Fonctionnalités facultatives**.
    
    4.  Assurez-vous que **Les dossiers publics Exchange Mail** n’est pas activée. S’il n’est pas sélectionné, vous pouvez continuer à la section suivante, *condition préalable les étapes dans Exchange en ligne*. Si elle est activée, désactivez la case à cocher, puis cliquez sur **suivant**.
        
        > [!NOTE]
        > Si vous ne voyez le <strong>Courrier Exchange des dossiers publics</strong> en tant qu’option dans l’écran <strong>Composants facultatifs</strong>, vous pouvez quitter Microsoft Azure Active Directory se connecter et passez à la section suivante, <em>condition préalable les étapes dans Exchange en ligne</em>.
    
    5.  Une fois que vous avez décoché l’option **Dossiers publics de messagerie Exchange**, cliquez sur **Suivant** jusqu’à ce que vous accédiez à l’écran **Prêt pour la configuration**, puis cliquez sur **Configurer**.

**Opérations préliminaires dans Exchange Online**

Dans Exchange Online PowerShell, procédez comme suit :

1.  Assurez-vous qu’il n’existe aucune demande de migration de dossiers publics. S’il en existe, supprimez-les, sinon, votre propre demande de migration échouera. Cette étape est nécessaire uniquement si vous pensez qu’il peut y avoir une demande de migration existante dans le pipeline (ayant échoué ou que vous avez abandonnée).
    
    Une demande de migration existante peut être de deux types : migration par lots ou en série. Les commandes permettant de détecter et de supprimer des demandes de chaque type sont indiquées ci-dessous.
    
    L’exemple suivant permet de détecter les demandes de migration en série existantes :
    
        Get-PublicFolderMigrationRequest | Get-PublicFolderMigrationRequestStatistics 
    
    L’exemple suivant supprime toutes les demandes de migration en série de dossiers publics :
    
        Get-PublicFolderMigrationRequest | Remove-PublicFolderMigrationRequest
    
    L’exemple suivant permet de détecter toute demande de migration par lots :
    
        Get-MigrationBatch | ?{$_.MigrationType.ToString() -eq "PublicFolder"}
    
    L’exemple suivant supprime toutes les demandes de migration par lots de dossiers publics :
    
        Remove-MigrationBatch <name of migration batch> -Confirm:$false

2.  La fonctionnalité de migration **PAW** doit être activée pour votre client Office 365. Vous pouvez vérifier si c’est le cas en exécutant la commande suivante dans Exchange Online PowerShell :
    
        Get-MigrationConfig
    
    Si les résultats sous **Features** indiquent **PAW**, la fonctionnalité est activée et vous pouvez passer à l’étape suivante.
    
    Si PAW n’est pas encore activé pour votre client, il se peut qu’il existe déjà des lots de migration, soit pour des dossiers publics, soit pour des utilisateurs. Ces lots peuvent avoir n’importe quel état, y compris Terminé. Si tel est le cas, terminez et supprimez des lots de migration jusqu’à ce que la commande `Get-MigrationBatch` ne renvoie plus aucun enregistrement. Une fois que toutes les lots existants ont été supprimés, PAW doit normalement être activé de façon automatique. Notez que la modification n’apparaît pas immédiatement dans `Get-MigrationConfig`, ce qui est normal. Dans le cas d’une migration d’utilisateurs, vous pouvez continuer à créer de nouveaux lots une fois que cette étape est terminée.

3.  Vérifiez qu’il n’existe déjà aucun dossier public ou aucune boîte aux lettres de dossier public dans Exchange Online. Si vous voyez des dossiers publics dans Exchange Online, avant de supprimer le moindre dossier public et la moindre boîte aux lettres de dossier public, il est important de déterminer la raison de leur présence, ainsi que le membre de votre organisation qui a commencé à créer une hiérarchie de dossiers publics.
    
    1.  Dans Office 365 ou Exchange Online PowerShell, pour voir s’il existe des boîtes aux lettres de dossiers publics, exécutez la commande suivante.
        
            Get-Mailbox -PublicFolder
    
    2.  Si la commande ne renvoie pas de boîte aux lettres de dossier public, passez à l’étape 3 (Générez les fichiers .csv). Si la commande renvoie des boîtes aux lettres de dossier public, exécutez la commande suivante pour voir s’il existe des dossiers publics :
        
            Get-PublicFolder -Recurse
    
    3.  Si Office 365 ou Exchange Online contient effectivement des dossiers publics, exécutez la commande Exchange Online PowerShell suivante pour les supprimer (après vous être assuré qu’ils n’étaient pas nécessaires). Vérifiez que vous avez enregistré les informations de ces dossiers publics avant de les supprimer, car elles seront définitivement supprimées lorsque vous supprimerez les dossiers publics.
        
            Get-MailPublicFolder -ResultSize Unlimited | where {$_.EntryId -ne $null}| Disable-MailPublicFolder -Confirm:$false 
            Get-PublicFolder -GetChildren \ -ResultSize Unlimited | Remove-PublicFolder -Recurse -Confirm:$false
    
    4.  Une fois les dossiers publics supprimés, exécutez les commandes suivantes pour supprimer toutes les boîtes aux lettres de dossier public :
        
            $hierarchyMailboxGuid = $(Get-OrganizationConfig).RootPublicFolderMailbox.HierarchyMailboxGuid
            Get-Mailbox -PublicFolder | Where-Object {$_.ExchangeGuid -ne $hierarchyMailboxGuid} | Remove-Mailbox -PublicFolder -Confirm:$false -Force
            Get-Mailbox -PublicFolder | Where-Object {$_.ExchangeGuid -eq $hierarchyMailboxGuid} | Remove-Mailbox -PublicFolder -Confirm:$false -Force
            Get-Mailbox -PublicFolder -SoftDeletedMailbox | Remove-Mailbox -PublicFolder -PermanentlyDelete:$true 

## Étape 3 : Générez les fichiers .csv

Utilisez les scripts téléchargés précédemment pour générer les fichiers .csv qui seront utilisés lors de la migration.

1.  Dans l’environnement de ligne de commande Exchange Management Shell (en local), exécutez le script `Export-ModernPublicFolderStatistics.ps1` pour créer le fichier de mappage nom de dossier-taille de dossier. Vous devez disposer des autorisations d’administrateur local pour exécuter ce script. Le fichier obtenu contient trois colonnes : **FolderName**, **FolderSize** et **DeletedItemSize**. Les valeurs des colonnes **FolderSize** et **DeletedItemSize** sont affichées en octets. Par exemple, **\\PublicFolder01,10240, 100** signifie que le dossier public nommé PublicFolder01 dans la racine de votre hiérarchie a une taille de 10 240 octets ou 10,240 Mo, et qu’il contient 100 octets d’éléments récupérables.
    
        .\Export-ModernPublicFolderStatistics.ps1 <Folder-to-size map path>
    
    **Exemple** :
    
        .\Export-ModernPublicFolderStatistics.ps1 stats.csv

2.  Exécutez le script `ModernPublicFolderToMailboxMapGenerator.ps1` pour créer un fichier .csv qui mappe les dossiers publics source avec les boîtes aux lettres de dossier public dans votre destination Exchange Online. Ce fichier permet de calculer le nombre correct de boîtes aux lettres de dossier public dans Exchange Online.
    
    > [!NOTE]
    > Le fichier généré par <code>ModernPublicFolderToMailboxMapGenerator.ps1</code> ne contiendra pas le nom de chaque dossier public de votre organisation. Il contient des références aux dossiers parents de plus grandes arborescences de dossiers, ou les noms des dossiers lorsqu’ils sont suffisamment importants. Vous pouvez considérer ce fichier comme un fichier « exception » permet de vous assurer que certains des arborescences de dossiers et dossiers supérieures à placer dans la messagerie du dossier public spécifiqueboîtes. Il est normal pour ne pas voir tous un de vos dossiers publics dans ce fichier. Les dossiers enfants de n’importe quel dossier répertorié dans ce fichier de mappage aussi migrent vers la même boîte aux lettres de dossier public en tant que leur dossier parent (sauf si mentionné explicitement sur une autre ligne dans le fichier de mappage qui les dirige vers une boîte aux lettres de dossiers publics différente).
    
        .\ModernPublicFolderToMailboxMapGenerator.ps1 <Maximum mailbox size in bytes><Maximum mailbox recoverable item size in bytes><Folder-to-size map path><Folder-to-mailbox map path>
    
      - `Maximum mailbox size in bytes` est la quantité maximale de données que vous voulez migrer dans n’importe quel boîte aux lettres de dossier public dans Exchange Online. La taille maximale de ce champ est actuellement 50 Go, mais nous vous recommandons d’utiliser une taille plus petite, par exemple 50 % de la taille maximale, afin de permettre un développement ultérieur.
    
      - `Maximum mailbox recoverable items size in bytes` est le quota d’éléments récupérables sur vos boîtes aux lettres Exchange Online. La taille maximale des boîtes aux lettres de dossier public dans Exchange Online est actuellement de 50 Go. Nous vous recommandons de définir ` RecoverableItemsQuota` sur 15 Go ou moins.
    
      - `Folder-to-size map path` est le chemin d’accès au fichier .csv que vous avez créé lors de l’exécution du script `Export-ModernPublicFolderStatistics.ps1`.
    
      - `Folder-to-mailbox map path` est le chemin d’accès au fichier .csv de mappage dossier-boîte aux lettres que vous créez lors de cette étape. Si vous spécifiez uniquement le nom du fichier, ce dernier est généré dans le répertoire PowerShell actuel sur l’ordinateur local.

**Exemple** :

    .\ModernPublicFolderToMailboxMapGenerator.ps1 -MailboxSize 25GB -MailboxRecoverableItemSize 1GB -ImportFile .\stats.csv -ExportFile map.csv

> [!NOTE]
> Nous ne prend en charge de migration de dossiers publics vers Exchange Online si le nombre de boîtes aux lettres de dossier public dans Exchange Online est supérieur à 100.


## Étape 4 : Créez les boîtes aux lettres de dossiers publics dans Exchange Online

À présent, dans Exchange Online PowerShell, créez les boîtes aux lettres de dossier public cible qui contiendront les dossiers publics migrés.

1.  Exécutez le script suivant pour créer les boîtes aux lettres de dossier public cibles. Le script crée une boîte aux lettres cible pour chaque boîte aux lettres du fichier .csv que vous avez généré à l’*étape 3 (Générez les fichiers .csv)*, en exécutant le script `ModernPublicFoldertoMailboxMapGenerator.ps1`.
    
        $mappings = Import-Csv <Folder-to-mailbox map path>
        $primaryMailboxName = ($mappings | Where-Object FolderPath -eq "\" ).TargetMailbox
        New-Mailbox -HoldForMigration:$true -PublicFolder -IsExcludedFromServingHierarchy:$false $primaryMailboxName 
        ($mappings | Where-Object TargetMailbox -ne $primaryMailboxName).TargetMailbox | Sort-Object -unique | ForEach-Object { New-Mailbox -PublicFolder -IsExcludedFromServingHierarchy:$false $_ }
    
      - `Folder-to-mailbox map path` est le chemin d’accès au fichier .csv de mappage dossier-boîte aux lettres qui a été généré par le script `ModernPublicFoldertoMailboxMapGenerator.ps1` à l’*étape 3 (Générez les fichiers .csv)*.

## Étape 5 : Lancez la demande de migration

Vous devez maintenant exécuter un certain nombre de commandes dans votre environnement Exchange 2013 local et dans Exchange Online.

1.  À partir de l’un de vos serveurs Exchange 2013 qui hébergent des boîtes aux lettres de dossier public, exécutez le script suivant. Ce script synchronise les dossiers publics à extension messagerie de votre annuaire Active Directory local dans Exchange Online. Vous devez avoir téléchargé la dernière version de ce script et l’exécuter à partir de l’environnement de ligne de commande Exchange Management Shell.
    
        .\Sync-ModernMailPublicFolders.ps1 -Credential (Get-Credential) -CsvSummaryFile:sync_summary.csv
    
      - `Credential` est votre nom d’utilisateur d’administration et votre mot de passe Exchange Online.
    
      - `CsvSummaryFile` est le chemin d’accès à l’emplacement souhaité pour le fichier journal des opérations et des erreurs de synchronisation. Ce journal sera au format .csv.

2.  Sur le serveur Exchange 2013, recherchez le serveur de point de terminaison du proxy MRS et notez-le. Vous aurez besoin de ces informations pour exécuter la demande de migration. Conservez-les pour l’étape 3b ci-dessous.

3.  Dans Exchange Online PowerShell, exécutez les commandes suivantes pour transmettre les informations MRS et les informations d’identification obtenues à l’étape précédente aux variables de cmdlet qui seront utilisées dans la demande de migration.
    
    1.  Transmettez les informations d’identification d’un utilisateur disposant d’autorisations d’administrateur dans l’environnement Exchange 2013 local à la variable `$Source_Credential`. La demande de migration que vous exécutez dans Exchange Online utilise ces informations d’identification pour accéder aux serveurs Exchange 2013 locaux pour copier le contenu des dossiers publics dans Exchange Online.
        
            $Source_Credential = Get-Credential <source_domain>\<PublicFolder_Administrator_Account>
    
    2.  Reprenez les informations du serveur proxy MRS de l’environnement Exchange 2013, obtenues à l’étape 2 ci-dessus, et transmettez-les à la variable suivante :
        
            $Source_RemoteServer = "<paste the value here>"

4.  Dans Exchange Online PowerShell, exécutez les commandes suivantes pour créer le point de terminaison de la migration de dossiers publics et la demande de migration associée :
    
        $PfEndpoint = New-MigrationEndpoint -PublicFolder -Name PublicFolderEndpoint -RemoteServer $Source_RemoteServer -Credentials $Source_Credential
         
        [byte[]]$bytes = Get-Content -Encoding Byte <folder_mapping.csv>
        
        New-MigrationBatch -Name PublicFolderMigration -CSVData $bytes -SourceEndpoint $PfEndpoint.Identity -NotificationEmails <email addresses for migration notifications>
    
    > [!NOTE]
    > Séparez les adresses de messagerie par des virgules.
    
    Où `folder_mapping.csv` est le fichier de mappage qui a été généré dans *étape 3 : créer les fichiers .csv*. Veillez à fournir le chemin d’accès de fichier complet. Si pour une raison quelconque, le fichier de mappage a été déplacé, veillez à utiliser le nouvel emplacement.

5.  Enfin, lancez la migration à l’aide de la commande suivante dans Exchange Online PowerShell :
    
        Start-MigrationBatch PublicFolderMigration

Bien que la migration par lots doive être créée à l’aide de la cmdlet New-MigrationBatch dans Exchange Online PowerShell, la progression et l’achèvement de la migration peuvent être affichés et gérés dans le CAE ou en exécutant la cmdlet Get-MigrationBatch. La cmdlet New-MigrationBatch lance une demande de migration de boîte aux lettres pour chaque boîte aux lettres de dossier public et vous pouvez consulter l’état de ces demandes à l’aide de la page de migration de boîte aux lettres.

Pour accéder à la page de migration de boîte aux lettres, procédez comme suit :

1.  Connectez-vous à Exchange Online et ouvrez le CAE.

2.  Accédez à **Destinataires**, puis sélectionnez **Migration**.

3.  Sélectionnez la demande de migration qui vient d’être créée, puis, dans le volet **Détails**, cliquez sur **Afficher les détails**.

Avant de passer à l’*étape 6 (Verrouillez les dossiers publics sur le serveur Exchange 2013)*, vérifiez que toutes les données ont été copiées et que le processus de migration ne comporte aucune migration. Une fois que vous vous êtes assuré que le lot est passé à l’état **synchronisé**, exécutez les commandes mentionnées à l’*étape 2 (Préparez la migration)*, dans la dernière étape sous **Opérations préliminaires dans l’environnement de serveur Exchange 2013 local**, afin de créer un instantané des dossiers publics en local. Une fois que ces commandes ont été exécutées, vous pouvez passer à l’étape suivante. Notez que ces commandes peuvent prendre un certain temps en fonction du nombre de dossiers que vous avez.

## Étape 6 : Verrouillez les dossiers publics dans l’environnement Exchange 2013 pour la migration finale (inaccessibilité des dossiers publics requise)

Jusqu’à ce stade du processus de migration, les utilisateurs pouvaient accéder aux dossiers publics en local. Au cours des étapes suivantes, les utilisateurs seront déconnectés des dossiers publics Exchange 2013, puis ces dossiers seront verrouillés jusqu’à ce que la synchronisation finale de la migration soit terminée. Les utilisateurs ne pourront pas accéder aux dossiers publics pendant cette période et les messages électroniques envoyés à ces dossiers publics à extension messagerie seront mis en file d’attente et ne seront pas remis tant que la migration des dossiers publics ne sera pas terminée.

Avant d’exécuter la commande `PublicFolderMailboxesLockedForNewConnections` comme décrit ci-dessous, assurez-vous que tous les travaux sont dans l’état de la **synchroniser**. Vous pouvez le faire en exécutant la commande `Get-PublicFolderMailboxMigrationRequest` . Suivez cette étape uniquement après que vous avez vérifié que tous les travaux sont dans l’état de la **synchroniser**.

Dans votre environnement local, exécutez la commande suivante pour verrouiller les dossiers publics Exchange 2013 pour la finalisation.

    Set-OrganizationConfig -PublicFolderMailboxesLockedForNewConnections $true

> [!NOTE]
> Si vous n’êtes pas en mesure d’accéder au paramètre <code>-PublicFolderMailboxesLockedForNewConnections</code> , il peut s’agir, car Active Directory n’a pas été préparé au cours de la mise à niveau CU, comme nous a informé au-dessus de <em>ce que vous devez connaître avant de commencer ?</em> Consultez <a href="prepare-active-directory-and-domains-exchange-2013-help.md">Préparation d’Active Directory et des domaines</a> pour plus d’informations.
> Notez également que tous les utilisateurs qui ont besoin d’accéder aux dossiers publics doivent être migrés en premier, <strong>avant</strong> que vous ne migriez les dossiers publics.


Si votre organisation possède des boîtes aux lettres de dossier public sur plusieurs serveurs Exchange 2013, vous devez patienter jusqu’à ce que la réplication d’Active Directory soit terminée. Une fois celle-ci terminé, vous pouvez vérifier que toutes les boîtes aux lettres de dossier public présentent l’indicateur `PublicFolderMailboxesLockedForNewConnections` et que les modifications en attente récemment apportées par les utilisateurs à leurs dossiers publics ont convergé dans toute l’organisation. Tout cela peut prendre plusieurs heures.

## Étape 7 : Finalisez la migration des dossiers publics (inaccessibilité des dossiers publics requise)

Avant d’effectuer la migration de dossiers publics, vous devez confirmer qu’il n’y a aucune autre boîte aux lettres de dossier public se déplace ou dossiers publics passe allant dans votre environnement de Exchange sur site. Pour ce faire, utilisez les applets de commande de `Get-MoveRequest` et `Get-PublicFolderMoveRequest` à un dossier public existant de la liste se déplace. S’il existe des déplacements en cours ou dans l’état **terminé**, supprimez-les.

Ensuite, pour effectuer la migration de dossiers publics, exécutez la commande suivante dans Exchange Online PowerShell :

    Complete-MigrationBatch PublicFolderMigration

Lorsque vous exécutez cette commande, Exchange effectue une synchronisation finale entre votre organisation sur place de Exchange et Exchange Online. Au cours de cette période, le statut du lot de migration ne pourra **synchronisés** à la **fin**, puis enfin sur **terminé**. Si la dernière synchronisation est réussie, les dossiers publics dans Exchange Online seront déverrouillées.

Il est courant pour le lot de migration mettre quelques heures avant son état change **synchronisés** pour **fin**, stade auquel commence la synchronisation finale.

## Étape 8 : Testez et déverrouillez les dossiers publics dans Exchange Online

Une fois que la migration de dossier public est terminée, procédez comme suit pour tester le succès de la migration et vérifier qu’elle est officiellement terminée. Ces tâches finales vous permettent de tester la hiérarchie des dossiers publics migrés avant de transférer définitivement votre organisation vers les dossiers publics Exchange Online.

1.  Dans Exchange Online PowerShell, attribuez quelques boîtes aux lettres test afin d’utiliser l’une de vos boîtes aux lettres de dossier public récemment migrées comme boîte aux lettres de dossier public par défaut :
    
        Set-Mailbox -Identity <test user> -DefaultPublicFolderMailbox <public folder mailbox identity>
    
    Assurez-vous que les utilisateurs test disposent des autorisations nécessaires pour créer des dossiers publics.

2.  Ouvrez une session Outlook à l’utilisateur de test désigné dans l’étape précédente, puis effectuez les tests suivants de dossier public. Notez qu’il peut prendre de 15 à 30 minutes pour que les modifications soient prises en compte. Une fois qu’Outlook est informé de ces modifications, il peut vous inviter à redémarrer plusieurs fois.
    
    1.  Affichez la hiérarchie.
    
    2.  Vérifiez les autorisations.
    
    3.  Créez des dossiers publics et supprimez-les.
    
    4.  Publiez du contenu dans un dossier public ou effacez-en.
    
    Si vous rencontrez un problème et que vous déterminez que vous n’êtes pas prêt à basculer les dossiers publics de votre organisation entièrement à Exchange Online, reportez-vous à la section [Restauration d’une migration de dossiers publics à partir d’Exchange 2013 vers Exchange Online](https://docs.microsoft.com/fr-fr/exchange/collaboration-exo/public-folders/roll-back-exchange-2013-public-folder-migration).

3.  Exécutez la commande suivante dans Exchange Online PowerShell pour déverrouiller vos dossiers publics dans Exchange en ligne. Après avoir exécuté la commande, il peut prendre environ 15 à 30 minutes pour que les modifications soient prises en compte. Une fois qu’Outlook est informé de ces modifications, il peut demander aux utilisateurs de redémarrer le programme plusieurs fois.
    
        Set-OrganizationConfig -RemotePublicFolderMailboxes $Null -PublicFoldersEnabled Local

## Étape 9 : Finaliser la migration sur place

Pour activer les e-mails vers des dossiers publics à extension messagerie sur site, procédez comme suit :

1.  Dans votre environnement local, exécutez le script suivant pour vous assurer que tous les e-mails adressés aux dossiers publics à extension messagerie sont correctement acheminés vers Exchange Online. Le script appliquera l’empreinte `ExternalEmailAddress` sur les dossiers publics à extension messagerie pour les diriger vers leurs équivalents Exchange Online :
    
        .\SetMailPublicFolderExternalAddress.ps1 -ExecutionSummaryFile:mepf_summary.csv

2.  Si les tests sont concluants, dans votre environnement local, exécutez la commande suivante pour indiquer que la migration des dossiers publics est terminée :
    
        Set-OrganizationConfig -PublicFolderMailboxesMigrationComplete:$true -PublicFoldersEnabled Remote

## Comment savoir si cela a fonctionné ?

Dans Étape 2 : Préparez la migration, vous avez pris des instantanés de la structure, des statistiques et des autorisations des dossiers publics locaux. Les étapes suivantes vous permettent de vérifier que votre migration de dossiers publics s’est correctement déroulée en prenant les mêmes instantanés dans Exchange Online après la migration. Vous pouvez ensuite comparer les données des deux fichiers pour vérifier la réussite de l’opération.

1.  Dans Exchange Online PowerShell, exécutez la commande suivante pour prendre un instantané de la nouvelle structure de dossiers :
    
        Get-PublicFolder -Recurse -ResultSize Unlimited | Export-CliXML Cloud_PFStructure.xml

2.  Dans Exchange Online PowerShell, exécutez les commandes suivantes pour prendre un instantané des statistiques de dossiers publics, telles que le nombre, la taille et le propriétaire des éléments :
    
        Get-PublicFolder -Recurse -ResultSize Unlimited | Get-PublicFolderStatistics | Export-CliXML Cloud_PFStatistics.xml

3.  Dans Exchange Online PowerShell, exécutez la commande suivante pour prendre un instantané des autorisations :
    
        Get-PublicFolder -Recurse -ResultSize Unlimited | Get-PublicFolderClientPermission | Select-Object Identity,User, AccessRights | Export-CliXML Cloud_PFPerms.xml

4.  Dans Exchange Online PowerShell, exécutez la commande suivante pour prendre un instantané des dossiers publics à extension messagerie.
    
        Get-MailPublicFolder -ResultSize Unlimited | Export-CliXML Cloud_MEPF.xml

## Problèmes connus

Les éléments suivants sont communs problèmes de migration de dossiers publics que vous pouvez rencontrer dans votre organisation.

  - Nous ne prend en charge de migration de dossiers publics vers Exchange Online si le nombre de boîtes aux lettres de dossier public dans Exchange Online est supérieur à 100.

  - Les autorisations du dossier public racine et du dossier EFORMS REGISTRY ne seront pas migrées vers Exchange Online, et vous devrez les appliquer manuellement dans Exchange Online. Pour ce faire, exécutez la commande suivante dans Exchange Online PowerShell : Exécutez la commande, une fois pour chaque entrée d’autorisation qui est présente en local mais qui n’est pas dans Exchange Online :
    
        Add-PublicFolderClientPermission "\" -User <user> -AccessRights <access rights>
        Add-PublicFolderClientPermission "\NON_IPM_SUBTREE\EFORMS REGISTRY" -User <user> -AccessRights <access rights>

  - Migrations de certains dossiers publics va échouer si certaines boîtes aux lettres de dossier public ne traitent pas de la hiérarchie de dossiers publics. Cela signifie que le paramètre `IsExcludedFromServingHierarchy` sur une ou plusieurs boîtes aux lettres est défini à `$true`. Pour éviter cela, définir toutes boîtes aux lettres dans Exchange Online à la hiérarchie.

  - Les autorisations **Envoyer en tant que** et **Envoyer de la part de** ne sont pas migrées vers Exchange Online. Si c’est le cas, utilisez les commandes suivantes dans votre environnement local pour noter qui détient ces autorisations.
    
    Pour voir les dossiers publics qui possèdent des autorisations Envoyer en tant que en local :
    
        Get-MailPublicFolder | Get-ADPermission | ?{$_.ExtendedRights -like "*Send-As*"}
    
    Pour voir les dossiers publics qui possèdent des autorisations Envoyer de la part de en local :
    
        Get-MailPublicFolder | ?{$_.GrantSendOnBehalfTo -ne "$null"} | ft name,GrantSendOnBehalfTo
    
    Pour ajouter des autorisations Envoyer en tant que à un dossier public à extension messagerie dans Exchange Online, accédez à Exchange Online PowerShell et saisissez la commande suivante :
    
        Add-RecipientPermission -Identity <mail-enabled public folder primary SMTP address> -Trustee <name of user to be assigned permission> -AccessRights SendAs
    
    **Exemple** :
    
        Add-RecipientPermission -Identity send1 -Trustee Exo1 -AccessRights SendAs
    
    Pour ajouter des autorisations Envoyer de la part de à un dossier public à extension messagerie dans Exchange Online, accédez à Exchange Online PowerShell et saisissez la commande suivante :
    
        Set-MailPublicFolder -Identity <name of public folder> -GrantSendOnBehalfTo <user or comma-separated list of users>
    
    **Exemple** :
    
        Set-MailPublicFolder send2 -GrantSendOnBehalfTo exo1,exo2

  - Ayant plus de 10 000 dossiers sous le dossier « \\NON\_IPM\_SUBTREE\\DUMPSTER\_ROOT » risque de faire échouer. Par conséquent, vérifiez le dossier « \\NON\_IPM\_SUBTREE\\DUMPSTER\_ROOT » pour voir s’il y a plus de 10 000 dossiers directement en dessous (enfants immédiats). Vous pouvez utiliser la commande suivante pour rechercher le nombre de dossiers publics à cet emplacement :
    
        (Get-PublicFolder -GetChildren "\NON_IPM_SUBTREE\DUMPSTER_ROOT").Count 
    
    Exchange Online ne supporte pas plus de 10 000 sous-dossiers, c’est pourquoi les migrations de plus de 10 000 dossiers échoue. Nous développons actuellement un script pour débloquer ces configurations. En attendant, nous vous recommandons d’attendre avant de migrer vos dossiers publics.

  - Tâches de migration sont progresse pas ou sont bloquées. Cela peut se produire s’il y a trop de travaux en cours d’exécution en parallèle, à l’origine de travaux à échouer avec des erreurs intermittentes. Vous pouvez réduire le nombre de tâches simultanées en modifiant des `MaxConcurrentMigrations` et `MaxConcurrentIncrementalSyncs` à un nombre plus petit. L’exemple suivant permet de définir ces valeurs :
    
        Set-MigrationEndpoint <PublicFolderEndpoint> -MaxConcurrentMigrations 30 -MaxConcurrentIncrementalSyncs 20  -SkipVerification 

  - Tâches de migration échouent avec l’erreur « Erreur : benne du dossier dans la benne. » Si vous rencontrez cette erreur, il doit être résolu si vous arrêtez le traitement par lots, puis redémarrez.

  - Tâches de migration échouer et générer un « demande a été mis en quarantaine en raison de l’erreur suivante : la clé donnée n’était pas présente dans le dictionnaire » message d’erreur. Cela se produit lorsqu’un élément endommagé est présent dans le dossier tâches de migration ne peut pas copier. Pour contourner ce problème :
    
    1.  Arrêter le traitement par lots de la migration.
    
    2.  Identifiez le dossier contenant l’élément défectueux. Le rapport de migration doit inclure des références au dossier qui a été copiée lorsque l’erreur s’est produite.
    
    3.  Dans votre environnement local, déplacez le dossier affecté à la boîte aux lettres de dossier public principaux. Vous pouvez utiliser l’applet de commande `New-PublicFolderMoveRequest` pour déplacer des dossiers.
    
    4.  Attendez que le déplacement du dossier terminer. Une fois terminée, supprimez la demande de déplacement. Redémarrez ensuite le lot de migration.

## Supprimer des boîtes aux lettres de dossier public de votre environnement Exchange local

Une fois que la migration est terminée et que vous avez vérifié que vos dossiers publics dans Exchange Online fonctionnent comme prévu et contiennent toutes les données attendues, vous pouvez supprimer vos boîtes aux lettres de dossier public locales.

Sachez que cette étape est irréversible, car une fois les boîtes aux lettres de dossier public sont supprimés, ils ne peuvent pas être récupérés. Par conséquent, nous recommandons vivement, en plus de la vérification de la réussite de la migration, également surveiller vos dossiers publics Exchange en ligne pendant quelques semaines avant de supprimer les boîtes aux lettres des dossiers publics locaux.

