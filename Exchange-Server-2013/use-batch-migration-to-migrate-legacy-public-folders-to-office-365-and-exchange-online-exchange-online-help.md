---
title: 'Utilisation de la migration par lot pour migrer des dossiers publics vers Office 365 et Exchange Online: Exchange 2013 Help'
TOCTitle: Utilisation de la migration par lot pour migrer des dossiers publics vers Office 365 et Exchange Online
ms:assetid: e8ab9309-7d12-4f02-bfc4-14e61a373958
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dn874017(v=EXCHG.150)
ms:contentKeyID: 63892224
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Utilisation de la migration par lot pour migrer des dossiers publics vers Office 365 et Exchange Online

 

_**Sapplique à :** Exchange Online, Exchange Server, Exchange Server 2013_

_**Dernière rubrique modifiée :** 2018-03-26_

**Résumé** : Utilisez ces procédures pour déplacer vos dossiers publics Exchange 2007 et Exchange 2010 vers Office 365.

Cette rubrique décrit la migration intermédiaire ou à basculement de vos dossiers publics à partir du correctif cumulatif 8 (RU8) pour Exchange Server 2010 Service Pack 3 (SP3) ou du correctif cumulatif 15 (RU15) pour Exchange 2007 SP3 vers Office 365 ou Exchange Online.

Cette rubrique fait référence aux serveurs Exchange 2010 SP3 RU8 et Exchange 2007 SP3 RU15 en tant que *serveurs Exchange hérités*. En outre, les étapes de cette rubrique s’appliquent à la fois à Exchange Online et à Office 365. Les termes peuvent être utilisés de manière interchangeable dans cette rubrique.

> [!NOTE]
> La méthode de migration par lots décrite dans cet article est la seule méthode prise en charge pour la migration des dossiers publics hérités vers Office 365 et Exchange Online. L’ancienne méthode de migration de dossiers publics en série est déconseillée et n’est plus prise en charge par Microsoft.


Nous vous recommandons de ne pas utiliser la fonctionnalité d’exportation PST d’Outlook pour migrer des dossiers publics vers Office 365 ou Exchange Online. La croissance de la boîte aux lettres de dossiers publics Office 365 et Exchange Online est gérée avec une fonctionnalité de fractionnement automatique qui divise la boîte aux lettres de dossiers publics quand celle-ci dépasse les quotas de taille. La fonctionnalité de fractionnement automatique ne peut pas gérer une croissance soudaine des boîtes aux lettres de dossiers publics lorsque vous utilisez l’exportation PST pour migrer vos dossiers publics. De plus, le déplacement des données à partir de la boîte aux lettres principale avec le fractionnement automatique pourrait prendre jusqu’à deux semaines. Nous vous recommandons d’utiliser les instructions basées sur la cmdlet et contenues dans ce document pour migrer des dossiers publics vers Office 365 et Exchange Online. Toutefois, si vous choisissez de migrer les dossiers publics à l’aide d’une exportation PST, consultez la section Migrer des dossiers publics vers Office 365 avec l’exportation PST d’Outlook plus loin dans cette rubrique.

Vous procéderez à la migration en utilisant les cmdlets **\*-MigrationBatch**, en plus des scripts PowerShell suivants :

  - `Export-PublicFolderStatistics.ps1`   Ce script crée le fichier de mappage du nom du dossier à la taille du dossier. Vous allez exécuter ce script sur le serveur Exchange hérité.

  - `Export-PublicFolderStatistics.psd1`   Le script `Export-PublicFolderStatistics.ps1` utilise ce fichier de support qui doit être téléchargé au même emplacement.

  - `PublicFolderToMailboxMapGenerator.ps1`   Ce script crée le fichier de mappage du dossier public à la boîte aux lettres à l’aide de la sortie du script `Export-PublicFolderStatistics.ps1`. Vous allez exécuter ce script sur le serveur Exchange hérité.

  - `PublicFolderToMailboxMapGenerator.strings.psd1`   Le script `PublicFolderToMailboxMapGenerator.ps1` utilise ce fichier de support qui doit être téléchargé au même emplacement.

  - `Create-PublicFolderMailboxesForMigration.ps1` Ce script crée les boîtes aux lettres de dossiers publics cibles pour la migration. En outre, ce script calcule le nombre de boîtes aux lettres nécessaires pour gérer la charge utilisateur estimée, en fonction des recommandations relatives au nombre de connexions utilisateurs par boîte aux lettres de dossier public données dans [Limites pour les dossiers publics](limits-for-public-folders-exchange-2013-help.md).

  - `Create-PublicFolderMailboxesForMigration.strings.psd1` Ce fichier de support est utilisé par le script Create-PublicFolderMailboxesForMigration.ps1 et doit être téléchargé au même emplacement.

  - `Sync-MailPublicFolders.ps1`   Ce script synchronise les objets de dossier public à extension messagerie entre votre déploiement local d’Exchange et Office 365. Vous l’exécuterez sur le serveur Exchange hérité.

  - `SyncMailPublicFolders.strings.psd1`   Il s’agit d’un fichier de support utilisé par le script `Sync-MailPublicFolders.ps1`. Il doit être copié dans le même emplacement que les scripts précédents.

L’Étape 1 : Téléchargez les scripts de migration fournit des détails sur l’emplacement de téléchargement de ces scripts. Assurez-vous que tous les scripts sont téléchargés au même emplacement.

Pour découvrir d'autres tâches de gestion associées aux dossiers publics, consultez la rubrique [Procédures relatives aux dossiers publics](public-folder-procedures-exchange-2013-help.md).

## Quelles versions d’Exchange sont prises en charge pour la migration de dossiers publics vers Office 365 et Exchange Online ?

Exchange prend en charge le déplacement de vos dossiers publics vers Office 365 et Exchange Online à partir des versions héritées suivantes d’Exchange Server :

  - Exchange 2010 SP3 RU8 ou version ultérieure

  - Exchange 2007 SP3 RU15 ou version ultérieure

Si vous devez déplacer vos dossiers publics vers Exchange Online, mais que vos serveurs locaux n’utilisent pas les versions minimales requises pour Exchange 2010 ou Exchange 2007, nous vous recommandons de mettre à niveau vos serveurs locaux et d’utiliser la migration par lots, qui est la seule méthode de migration de dossiers publics prise en charge.

Vous ne pouvez pas migrer les dossiers publics directement à partir de Exchange 2003. Si vous exécutez cette version d’Exchange dans votre organisation, vous devez déplacer l’ensemble des bases de données et réplicas de dossiers publics vers Exchange 2010 SP3 RU8 ou une version ultérieure, ou vers Exchange 2007 SP3 RU10 ou une version ultérieure. Aucun réplica de dossier public ne peut rester sur Exchange 2003. En outre, les messages électroniques destinés à un dossier public Exchange 2013 ne peuvent pas être acheminés via un serveur Exchange 2003.

## Ce qu’il faut savoir avant de commencer

  - Le serveur Exchange 2010 doit exécuter Exchange 2010 SP3 RU8 ou une version ultérieure.

  - Le serveur Exchange 2007 doit exécuter Exchange 2007 SP3 RU15 ou une version ultérieure.

  - Dans Office 365 et Exchange Online, vous devez être membre du groupe de rôles Gestion de l’organisation. Ce groupe de rôles diffère des autorisations qui vous sont attribuées quand vous vous abonnez à Office 365 ou Exchange Online. Pour plus de détails sur l’activation du groupe de rôles Gestion de l’organisation, consultez la rubrique [Gérer des groupes de rôles](manage-role-groups-exchange-2013-help.md).

  - Dans Exchange 2010, vous devez être membre du groupe de rôles RBAC Gestion de l’organisation ou Gestion du serveur. Pour plus d’informations, consultez la rubrique [Ajouter des membres à un groupe de rôles](https://go.microsoft.com/fwlink/?linkid=299212).

  - Dans Exchange 2007, le rôle Administrateur d’organisation Exchange ou Administrateur d’Exchange Server doit vous être attribué. Le rôle Administrateur de dossiers publics et le groupe Administrateurs local doivent également vous être attribués pour le serveur cible. Pour plus d’informations, consultez la rubrique [Procédure d’ajout d’un utilisateur ou d’un groupe à un rôle d’administrateur](https://go.microsoft.com/fwlink/p/?linkid=81779).

  - Sur le serveur Exchange 2007, effectuez une mise à niveau vers [Windows PowerShell 2.0 et WinRM 2.0 pour Windows Server 2008 x64 Edition](http://go.microsoft.com/fwlink/p/?linkid=3052&kbid=968930).

  - Avant la migration, si un dossier public au sein de votre organisation a une taille supérieure à 2 Go, nous vous recommandons soit d’en supprimer le contenu, soit de le fractionner en plusieurs dossiers publics. Si aucune de ces options n’est envisageable, nous vous recommandons de ne pas déplacer vos dossiers publics vers Office 365 et Exchange Online.

  - Dans Office 365 et Exchange Online, vous pouvez créer 1 000 boîtes aux lettres de dossiers publics au maximum.

  - Avant de migrer vos dossiers publics, nous vous recommandons de déplacer toutes les boîtes aux lettres d’utilisateurs vers Office 365 et Exchange Online. Pour plus d’informations, voir [Méthodes de migration des comptes de messagerie vers Office 365](https://go.microsoft.com/fwlink/p/?linkid=524030).

  - Outlook Anywhere doit être activé sur le serveur Exchange hérité. Pour plus d’informations sur l’activation d’Outlook Anywhere sur des serveurs Exchange 2010, consultez la rubrique [Activer Outlook Anywhere](https://go.microsoft.com/fwlink/p/?linkid=187249). Pour plus d’informations sur l’activation d’Outlook Anywhere sur des serveurs Exchange 2007, consultez la rubrique [Procédure d’activation d’Outlook Anywhere](https://go.microsoft.com/fwlink/p/?linkid=167210).

  - Pour exécuter cette procédure, vous ne pouvez pas utiliser le Centre d’administration Exchange (CAE) ou la console de gestion Exchange (EMC). Sur les serveurs Exchange hérités, vous devez utiliser l’Environnement de ligne de commande Exchange Management Shell. Pour Exchange Online, vous devez utiliser Exchange Online PowerShell. Pour plus d’informations, voir [Connexion à Exchange Online à l'aide de Remote PowerShell](https://technet.microsoft.com/fr-fr/library/jj984289\(v=exchg.150\)).

  - Avant de commencer, nous vous recommandons de lire cette rubrique dans son intégralité, car un temps mort est nécessaire pour certaines étapes.

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.


## Comment procéder ?

## Étape 1 : Téléchargez les scripts de migration

1.  Téléchargez tous les scripts et les fichiers de support à partir des [scripts de migration de dossiers publics](https://go.microsoft.com/fwlink/?linkid=299838).

2.  Enregistrez les scripts sur l’ordinateur local sur lequel vous exécuterez PowerShell. Par exemple, C:\\PFScripts. Assurez-vous que tous les scripts sont enregistrés au même emplacement.

3.  Téléchargez les fichiers suivants à partir des [dossiers publics à extension messagerie - script de synchronisation d’annuaire](https://go.microsoft.com/fwlink/p/?linkid=532376) :
    
    1.  `Sync-MailPublicFolders.ps1`
    
    2.  `SyncMailPublicFolders.strings.psd1`

4.  Enregistrez les scripts au même emplacement qu’à l’étape 2. Par exemple, C:\\PFScripts.

## Étape 2 : Préparez la migration

Avant de commencer la migration, exécutez les étapes préalables suivantes.

**Étapes préalables générales**

  - Assurez-vous qu’il n’existe aucun objet de messagerie de dossier public orphelin dans Active Directory, c’est-à-dire aucun objet présent dans Active Directory sans objet Exchange correspondant.

  - Vérifiez que l’adresse de messagerie SMTP configurée pour les dossiers publics dans Active Directory corresponde aux adresses de messagerie SMTP sur les objets Exchange.

  - Vérifiez qu’il n’existe aucun objet de dossier public en double dans Active Directory, afin d’éviter que deux objets Active Directory ou plus pointent vers le même dossier public à extension messagerie.

**Étapes préalables sur le serveur Exchange hérité**

1.  Sur le serveur Exchange hérité, assurez-vous que le routage vers les dossiers publics à extension messagerie qui existeront dans Office 365 ou Exchange Online continue de fonctionner jusqu’à ce que tous les caches DNS sur Internet soient mis à jour pour pointer vers le DNS d’Office 365 ou d’Exchange Online où votre organisation réside maintenant. Pour ce faire, exécutez la commande suivante pour configurer un domaine accepté avec un nom bien connu qui routera correctement les messages électroniques vers le domaine Office 365 ou Exchange Online.
    
        New-AcceptedDomain -Name "PublicFolderDestination_78c0b207_5ad2_4fee_8cb9_f373175b3f99" -DomainName contoso.onmicrosoft.com -DomainType InternalRelay 

2.  Si le nom d’un dossier public contient une barre oblique inverse **\\**, les dossiers publics seront créés dans le dossier public parent lors de la migration. Avant de procéder à la migration, il est recommandé de renommer les dossiers publics dont le nom inclut une barre oblique inverse.
    
    1.  Dans Exchange 2010, pour rechercher les dossiers publics dont le nom inclut une barre oblique inverse, exécutez la commande suivante :
        
            Get-PublicFolderStatistics -ResultSize Unlimited | Where {($_.Name -like "*\*") -or ($_.Name -like "*/*") } | Format-List Name, Identity
    
    2.  Dans Exchange 2007, pour rechercher les dossiers publics dont le nom inclut une barre oblique inverse, exécutez la commande suivante :
        
            Get-PublicFolderDatabase | ForEach {Get-PublicFolderStatistics -Server $_.Server | Where {$_.Name -like "*\*"}}
    
    3.  Si des dossiers publics sont renvoyés, vous pouvez les renommer en exécutant la commande suivante :
        
            Set-PublicFolder -Identity <public folder identity> -Name <new public folder name>

3.  Vérifiez qu’il n’existe aucun autre enregistrement d’une migration réussie. S’il en existe un, vous devrez paramétrer cette valeur sur `$false`. Si la valeur est définie sur `$true`, la demande de migration échouera.
    
    1.  L’exemple suivant vérifie l’état de la migration des dossiers publics.
        
            Get-OrganizationConfig | Format-List PublicFoldersLockedforMigration, PublicFolderMigrationComplete
    
    2.  Si l’état de la propriété *PublicFoldersLockedforMigration* ou *PublicFolderMigrationComplete* a la valeur `$true`, exécutez la commande suivante pour définir la valeur sur `$false` :
        
            Set-OrganizationConfig -PublicFoldersLockedforMigration:$false -PublicFolderMigrationComplete:$false
    
    > [!WARNING]
    > Après avoir redéfini ces propriétés, attendez qu’Exchange détecte les nouveaux paramètres. Cela peut prendre jusqu’à deux heures.


4.  À des fins de vérification à la fin de la migration, nous vous recommandons d’exécuter d’abord les commandes Environnement de ligne de commande Exchange Management Shell suivantes sur le serveur Exchange hérité pour prendre des instantanés de votre déploiement de dossiers publics actuel.
    
    1.  Exécutez la commande suivante pour prendre un instantané de la structure de dossiers publics d'origine :
        
            Get-PublicFolder -Recurse | Export-CliXML C:\PFMigration\Legacy_PFStructure.xml
    
    2.  Pour prendre un instantané des statistiques de dossiers publics, telles que le nombre, la taille et le propriétaire d’éléments, exécutez la commande suivante :
        
            Get-PublicFolderStatistics -ResultSize Unlimited | Export-CliXML C:\PFMigration\Legacy_PFStatistics.xml
    
    3.  Pour prendre un instantané des autorisations, exécutez la commande suivante :
        
            Get-PublicFolder -Recurse | Get-PublicFolderClientPermission | Select-Object Identity,User -ExpandProperty AccessRights | Export-CliXML C:\PFMigration\Legacy_PFPerms.xml
    
    Enregistrez les informations résultant de l'exécution des commandes précédentes pour effectuer une comparaison à l'issue de la migration.

5.  Si vous utilisez Microsoft Azure Active Directory Connect (Azure AD Connect) pour synchroniser vos répertoires locaux avec Azure Active Directory, vous devez procéder comme suit (si vous n’utilisez pas Azure AD Connect, vous pouvez ignorer cette étape) :
    
    1.  Sur un ordinateur local, ouvrez Microsoft Azure Active Directory Connect, puis sélectionnez **Configurer**.
    
    2.  Sur l’écran **Tâches supplémentaires**, sélectionnez **Personnaliser les options de synchronisation**, puis cliquez sur **Suivant**.
    
    3.  Sur l’écran **Connexion à Azure AD**, entrez les informations d’identification, puis cliquez sur **Suivant**. Une fois connecté, continuez à cliquer sur **Suivant** jusqu’à ce que vous accédiez à l’écran **Fonctionnalités facultatives**.
    
    4.  Vérifiez que l’option **Dossiers publics de messagerie Exchange** n’est pas sélectionnée. Si elle n’est pas sélectionnée, vous pouvez continuer jusqu’à la section suivante, *Étapes préalables dans Office 365 ou Exchange Online*. Si elle est sélectionnée, décochez la case, puis cliquez sur **Suivant**.
        
        > [!NOTE]
        > Si <strong>Dossiers publics de messagerie Exchange</strong> n’apparaît pas comme une option sur l’écran <strong>Fonctionnalités facultatives</strong>, vous pouvez quitter Microsoft Azure Active Directory Connect, puis passer à la section suivante <em>Étapes préalables dans Office 365 ou Exchange Online</em>.
    
    5.  Une fois que vous avez décoché l’option **Dossiers publics de messagerie Exchange**, cliquez sur **Suivant** jusqu’à ce que vous accédiez à l’écran **Prêt pour la configuration**, puis cliquez sur **Configurer**.

Pour plus d’informations sur la syntaxe et les paramètres, consultez les rubriques suivantes :

  - [New-AcceptedDomain](https://technet.microsoft.com/fr-fr/library/aa995975\(v=exchg.150\))

  - [Get-PublicFolder](https://technet.microsoft.com/fr-fr/library/aa997615\(v=exchg.150\))

  - [Get-PublicFolderDatabase](https://technet.microsoft.com/fr-fr/library/jj733416\(v=exchg.150\))

  - [Set-PublicFolder](https://technet.microsoft.com/fr-fr/library/aa998596\(v=exchg.150\))

  - [Get-PublicFolderStatistics](https://technet.microsoft.com/fr-fr/library/aa998663\(v=exchg.150\))

  - [Get-PublicFolderClientPermission](https://technet.microsoft.com/fr-fr/library/bb124365\(v=exchg.150\))

  - [Get-OrganizationConfig](https://go.microsoft.com/fwlink/p/?linkid=183212)

  - [Set-OrganizationConfig](https://go.microsoft.com/fwlink/p/?linkid=183213)

**Étapes préalables dans Office 365 ou Exchange Online**

1.  Assurez-vous qu’il n’existe aucune demande de migration de dossiers publics. S’il en existe, supprimez-les, sinon, votre propre demande de migration échouera. Cette étape n’est pas obligatoire dans tous les cas. Elle est nécessaire uniquement si vous pensez qu’il peut y avoir une demande de migration existante dans le pipeline.
    
    Une demande de migration existante peut être de deux types : migration par lots ou en série. Les commandes permettant de détecter les demandes pour chaque type et de supprimer des demandes de chaque type sont les suivantes :
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ159813.important(EXCHG.150).gif" title="Important" alt="Important" />Important :</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Avant de supprimer une demande de migration, il est important de comprendre la raison de son existence. L’exécution des commandes suivantes déterminera le moment de la création de la demande précédente et vous permettra de diagnostiquer les problèmes qui ont pu se produire. Pour déterminer la raison du changement, il se peut que vous deviez communiquer avec d’autres administrateurs de votre organisation.</td>
    </tr>
    </tbody>
    </table>
    
    L’exemple suivant permet de détecter les demandes de migration en série existantes.
    
        Get-PublicFolderMigrationRequest | Get-PublicFolderMigrationRequestStatistics -IncludeReport | Format-List
    
    L’exemple suivant supprime toutes les demandes de migration en série de dossiers publics.
    
        Get-PublicFolderMigrationRequest | Remove-PublicFolderMigrationRequest
    
    L’exemple suivant permet de détecter toute demande de migration par lots.
    
        $batch = Get-MigrationBatch | ?{$_.MigrationType.ToString() -eq "PublicFolder"}
    
    L’exemple suivant supprime toutes les demandes de migration par lots de dossiers publics.
    
        $batch | Remove-MigrationBatch -Confirm:$false

2.  Assurez-vous qu’il n’existe aucun dossier public ni aucune boîte aux lettres de dossiers publics dans Office 365.
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ159813.important(EXCHG.150).gif" title="Important" alt="Important" />Important :</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Si vous voyez des dossiers publics dans Office 365 ou Exchange Online, il est important de déterminer la raison de leur présence et la personne qui, au sein de votre organisation, a commencé à créer une hiérarchie de dossiers publics avant de supprimer les dossiers publics et boîtes aux lettres de dossiers publics.</td>
    </tr>
    </tbody>
    </table>
    
    1.  Dans Office 365 ou Exchange Online PowerShell, pour voir s’il existe des boîtes aux lettres de dossiers publics, exécutez la commande suivante.
        
            Get-Mailbox -PublicFolder 
    
    2.  Si la commande n’a pas renvoyé de boîte aux lettres de dossiers publics, passez à l’Étape 3 : génération des fichiers .csv. Si la commande renvoie une ou plusieurs boîtes aux lettres de dossiers publics, exécutez la commande suivante pour voir s’il existe un dossier public:
        
            Get-PublicFolder
    
    3.  Si Office 365 ou Exchange Online contient des dossiers publics, exécutez la commande Exchange Online PowerShell suivante pour les supprimer. Assurez-vous que vous avez enregistré les informations présentes dans les dossiers publics dans Office 365. Toutes les informations contenues dans les dossiers publics seront définitivement supprimées lorsque vous supprimerez les dossiers publics.
        
            Get-MailPublicFolder | where {$_.EntryId -ne $null}| Disable-MailPublicFolder -Confirm:$false 
            
            
            Get-PublicFolder -GetChildren \ | Remove-PublicFolder -Recurse -Confirm:$false
    
    4.  Une fois les dossiers publics supprimés, exécutez les commandes suivantes pour supprimer toutes les boîtes aux lettres de dossiers publics.
        
            $hierarchyMailboxGuid = $(Get-OrganizationConfig).RootPublicFolderMailbox.HierarchyMailboxGuid
            
            Get-Mailbox -PublicFolder:$true | Where-Object {$_.ExchangeGuid -ne $hierarchyMailboxGuid} | Remove-Mailbox -PublicFolder -Confirm:$false
            
            Get-Mailbox -PublicFolder:$true | Where-Object {$_.ExchangeGuid -eq $hierarchyMailboxGuid} | Remove-Mailbox -PublicFolder -Confirm:$false

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

## Étape 3 : génération des fichiers .csv

1.  Sur le serveur Exchange hérité, exécutez le script `Export-PublicFolderStatistics.ps1` pour créer le fichier de mappage de nom de dossier à taille de dossier. Ce script doit toujours être exécuté par un administrateur local. Le fichier contient deux colonnes : **FolderName** et **FolderSize**. Les valeurs de la colonne **FolderSize** s’affichent en octets. Par exemple, **\\PublicFolder01,10000**.
    
        .\Export-PublicFolderStatistics.ps1  <Folder to size map path> <FQDN of source server>
    
      - *FQDN of source server* est égal au nom de domaine complet du serveur de boîtes aux lettres hébergeant la hiérarchie de dossiers publics.
    
      - *Folder to size map path* est égal au nom de fichier et au chemin d’accès d’un dossier partagé sur le réseau où vous souhaitez enregistrer le fichier .csv. Plus loin dans cette rubrique, vous devrez utiliser Exchange Online PowerShell pour accéder à ce fichier. Si vous spécifiez uniquement le nom du fichier, ce dernier est généré dans le répertoire PowerShell actuel sur l’ordinateur local.
    
      - Si nécessaire, supprimez tous les dossiers système à extension messagerie de la sortie générée par le script avant de continuer.

2.  Pour créer le fichier de mappage de dossier public à boîte aux lettres, exécutez le script `PublicFolderToMailboxMapGenerator.ps1`. Ce fichier permet de calculer le nombre correct de boîtes aux lettres de dossiers publics dans Exchange Online.
    
        .\PublicFolderToMailboxMapGenerator.ps1 <Maximum mailbox size in bytes> <Folder to size map path> <Folder to mailbox map path>
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ159813.important(EXCHG.150).gif" title="Important" alt="Important" />Important :</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Le fichier de mappage du dossier public à la boîte aux lettres ne doit pas dépasser 1 000 lignes. Si ce fichier dépasse 1 000 lignes, votre structure de dossiers publics doit être simplifiée. Il est déconseillé d’utiliser un fichier de plus de 1 000 lignes sous peine de provoquer des erreurs de migration.</td>
    </tr>
    </tbody>
    </table>
    
      - Avant d’exécuter le script, utilisez la cmdlet suivante pour vérifier les limites du dossier public actuel de votre locataire Exchange Online. Ensuite, notez les valeurs de quota à jour pour les dossiers publics. `Get-OrganizationConfig | fl *quota*`
        
        Dans Exchange Online, la valeur par défaut est de 1,7 Go pour **DefaultPublicFolderIssueWarningQuota** et de 2 Go pour **DefaultPublicFolderProhibitPostQuota**.
    
      - *Maximum mailbox size in bytes* est égal à la taille maximale que vous souhaitez définir pour les nouvelles boîtes aux lettres de dossiers publics. Dans Exchange Online, la taille maximale des boîtes aux lettres de dossiers publics est de 100 Go. Nous vous recommandons d’utiliser un paramètre de 15 Go afin que chaque boîte aux lettres de dossier public ait suffisamment d’espace pour augmenter en taille. Exchange Online a un quota de dossier public par défaut « interdire la publication » de 2 Go. Si vous avez des dossiers publics individuels supérieurs à 2 Go, vous pouvez utiliser l’une des options suivantes pour résoudre ce problème :
        
          - Avant de lancer le lot de migration, augmentez le quota de dossier public par défaut « interdire la publication » en exécutant la cmdlet suivante :
            
            `Set-OrganizationConfig -DefaultPublicFolderProhibitPostQuota <size value> -DefaultPublicFolderIssueWarningQuota <size value>`
        
          - Avant de lancer le lot de migration, supprimez le contenu du dossier public pour réduire sa taille à 2 Go au maximum.
        
          - Avant de lancer le lot de migration, fractionnez le dossier public en plusieurs dossiers publics d’une taille de 2 Go maximum chacun.
        
        > [!NOTE]
        > Si la taille d’un dossier public est supérieure à 30 Go et si la suppression de contenu ou le fractionnement en plusieurs dossiers publics est impossible, nous vous recommandons de ne pas déplacer vos dossiers publics vers Exchange Online.
    
      - *Folder to size map path* est le chemin d’accès au fichier .csv que vous avez créé lors de l’exécution du script `Export-PublicFolderStatistics.ps1`.
    
      - *Folder to mailbox map path* est égal au nom de fichier et au chemin d’accès au fichier .csv de mappage du dossier à la boîte aux lettres que vous créez lors de cette étape. Si vous spécifiez uniquement le nom du fichier, ce dernier est généré dans le répertoire PowerShell actuel sur l’ordinateur local.

> [!NOTE]
> Une fois que les scripts sont exécutés et les fichiers .csv générés, les nouveaux dossiers publics ou les mises à jour des dossiers publics existants ne seront pas collectés.


## Étape 4 : Créez les boîtes aux lettres de dossiers publics dans Exchange Online

1.  Exécutez la commande suivante pour créer les boîtes aux lettres de dossier public cible. Le script crée une boîte aux lettres cible pour chaque boîte aux lettres dans le fichier .csv que vous avez généré à l’étape 3, en exécutant le script PublicFoldertoMailboxMapGenerator.ps1.
    
        .\Create-PublicFolderMailboxesForMigration.ps1 -FolderMappingCsv Mapping.csv -EstimatedNumberOfConcurrentUsers:<estimate>
    
    *Mapping.csv* est le fichier généré par le script PublicFoldertoMailboxMapGenerator.ps1 à l’étape 3. Le nombre estimé de connexions utilisateur simultanées parcourant une hiérarchie de dossiers publics est généralement inférieur au nombre total d’utilisateurs dans une organisation.

## Étape 5 : Lancez la demande de migration

1.  Sur le serveur Exchange hérité, exécutez la commande suivante pour synchroniser les dossiers publics à extension messagerie à partir de votre annuaire Active Directory local vers Exchange Online.
    
        Sync-MailPublicFolders.ps1 -Credential (Get-Credential) -CsvSummaryFile:sync_summary.csv
    
    `Credential` est votre nom d’utilisateur et votre mot de passe Office 365. `CsvSummaryFile` est le chemin d’accès de l’emplacement où vous voulez journaliser les opérations et les erreurs de synchronisation au format .CSV.
    
    > [!NOTE]
    > Nous vous recommandons de commencer par simuler les actions du script avant de l’exécuter réellement. Pour ce faire, exécutez le script avec un paramètre <code>-WhatIf</code>.


2.  Sur le serveur Exchange hérité, recueillez les informations suivantes, nécessaires pour l’exécution de la demande de migration :
    
    1.  Recherchez le `LegacyExchangeDN` du compte de l’utilisateur membre du rôle Administrateur de dossiers publics. Il s’agit de l’utilisateur dont les informations d’identification vous seront utiles à l’étape 3 de cette procédure.
        
            Get-Mailbox <PublicFolder_Administrator_Account> | Select-Object LegacyExchangeDN
    
    2.  Recherchez le `LegacyExchangeDN` de tout serveur de boîtes aux lettres disposant d’une base de données de dossiers publics.
        
            Get-ExchangeServer <public folder server> | Select-Object -Expand ExchangeLegacyDN
    
    3.  Recherchez le nom de domaine complet (FQDN) du nom d’hôte Outlook Anywhere. Si vous avez plusieurs instances d’Outlook Anywhere, nous vous recommandons de sélectionner celle qui est la plus proche du point de terminaison de migration ou celle qui est la plus proche des réplicas de dossiers publics dans l’organisation Exchange héritée. La commande suivante recherche toutes les instances d’Outlook Anywhere :
        
            Get-OutlookAnywhere | Format-Table Identity,ExternalHostName

3.  Dans Office 365 PowerShell, exécutez les commandes suivantes pour transmettre les informations recueillies à l’étape précédente aux variables qui seront utilisées dans la demande de migration.
    
    1.  Transmettez les informations d’identification d’un utilisateur disposant d’autorisations administratives sur le serveur Exchange hérité dans la variable `$Source_Credential`. La demande de migration exécutée dans Exchange Online utilisera ces informations d’identification pour accéder à vos serveurs Exchange hérités afin d’en copier le contenu.
        
            $Source_Credential = Get-Credential <source_domain\PublicFolder_Administrator_Account>
    
    2.  Utilisez le `ExchangeLegacyDN` de l’utilisateur de migration sur le serveur Exchange hérité que vous avez trouvé à l’étape 2a, et transmettez-le à la variable `$Source_RemoteMailboxLegacyDN`.
        
            $Source_RemoteMailboxLegacyDN = "<paste the value here>"
    
    3.  Utilisez le `ExchangeLegacyDN` du serveur de dossiers publics que vous avez trouvé à l’étape 2b ci-dessus, et transmettez-le à la variable `$Source_RemotePublicFolderServerLegacyDN`.
        
            $Source_RemotePublicFolderServerLegacyDN = "<paste the value here>"
    
    4.  Utilisez le nom d’hôte externe d’Outlook Anywhere que vous avez trouvé à l’état 2c, et transmettez-le à la variable `$Source_OutlookAnywhereExternalHostName`.
        
            $Source_OutlookAnywhereExternalHostName = "<paste the value here>"

4.  Enfin, dans Exchange Online PowerShell, exécutez les commandes suivantes pour créer la demande de migration.
    
    > [!NOTE]
    > La méthode d’authentification dans l’exemple de Environnement de ligne de commande Exchange Management Shell suivant doit correspondre à vos paramètres Outlook Anywhere, sinon la commande échouera.
    
        $PfEndpoint = New-MigrationEndpoint -PublicFolder -Name PublicFolderEndpoint -RPCProxyServer $Source_OutlookAnywhereExternalHostName -Credentials $Source_Credential -SourceMailboxLegacyDN $Source_RemoteMailboxLegacyDN -PublicFolderDatabaseServerLegacyDN $Source_RemotePublicFolderServerLegacyDN -Authentication Basic
        
        [byte[]]$bytes = Get-Content -Encoding Byte <folder_mapping.csv>
        
        New-MigrationBatch -Name PublicFolderMigration -CSVData $bytes -SourceEndpoint $PfEndpoint.Identity -NotificationEmails <email addresses for migration notifications>
    
    Où le fichier \<*folder\_mapping.csv*\> est le fichier généré à l’Étape 3 : génération des fichiers .csv.

5.  Lancez la migration à l’aide de la commande suivante :
    
        Start-MigrationBatch PublicFolderMigration

Alors que la migration par lots doit être créée à l’aide de la cmdlet **New-MigrationBatch** dans l’Environnement de ligne de commande Exchange Management Shell, la progression et l’achèvement de la migration peuvent être affichés et gérés dans le CAE. Étant donné que la cmdlet **New-MigrationBatch** lance une demande de migration de boîte aux lettres pour chaque boîte aux lettres de dossiers publics, vous pouvez consulter l’état de ces demandes à l’aide de la page de migration de boîte aux lettres. Pour accéder à cette page et créer des rapports de migration qui peuvent vous être envoyés par courrier électronique, procédez comme suit :

1.  Connectez-vous à Exchange Online et ouvrez l’EAC.

2.  Accédez à **Boîte aux lettres** \> **Migration**.

3.  Sélectionnez la demande de migration qui vient d’être créée, puis cliquez sur **Afficher les détails** dans le volet **Détails**.

Pour plus d’informations sur la syntaxe et les paramètres, consultez les rubriques suivantes :

  - [Get-Mailbox](https://technet.microsoft.com/fr-fr/library/bb123685\(v=exchg.150\))

  - [Get-ExchangeServer](https://technet.microsoft.com/fr-fr/library/bb123873\(v=exchg.150\))

  - [Get-OutlookAnywhere](https://technet.microsoft.com/fr-fr/library/bb124263\(v=exchg.150\))

  - [New-PublicFolderMigrationRequest](https://technet.microsoft.com/fr-fr/library/jj218636\(v=exchg.150\))

  - [Get-PublicFolderDatabase](https://technet.microsoft.com/fr-fr/library/jj733416\(v=exchg.150\))

  - [Get-PublicFolderMigrationRequest](https://technet.microsoft.com/fr-fr/library/jj218718\(v=exchg.150\))

  - [Get-PublicFolderMigrationRequestStatistics](https://technet.microsoft.com/fr-fr/library/jj218697\(v=exchg.150\))

## Étape 6 : verrouillage des dossiers publics du serveur Exchange hérité pour une migration finale (temps d'interruption requis)

Jusqu’à ce stade du processus de migration, les utilisateurs pouvaient accéder aux dossiers publics. Au cours des étapes suivantes, les utilisateurs seront déconnectés des dossiers publics hérités, et les dossiers seront verrouillés jusqu’à ce que la synchronisation finale de la migration soit terminée. Les utilisateurs ne pourront pas accéder aux dossiers publics durant ce processus. En outre, les messages électroniques envoyés aux dossiers publics à extension messagerie seront mis en file d’attente et ne seront pas remis tant que la migration des dossiers publics ne sera pas terminée.

Avant d’exécuter la commande `PublicFoldersLockedForMigration` comme décrit ci-dessous, assurez-vous que tous les travaux sont dans l’état **Synchronisé**. Pour cela, exécutez la commande `Get-PublicFolderMailboxMigrationRequest`. Passez à cette étape uniquement une fois que vous avez vérifié que tous les travaux sont dans l’état **Synchronisé**.

Sur le serveur Exchange hérité, exécutez la commande suivante pour verrouiller les dossiers publics hérités le temps que la migration s’achève.

    Set-OrganizationConfig -PublicFoldersLockedForMigration:$true

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Set-OrganizationConfig](https://technet.microsoft.com/fr-fr/library/aa997443\(v=exchg.150\)).

Si votre organisation possède plusieurs bases de données de dossiers publics, vous devrez attendre la fin de la réplication des dossiers publics pour confirmer que toutes les bases de données de dossiers publics présentent l’indicateur `PublicFoldersLockedForMigration` et que les modifications en attente que les utilisateurs ont récemment apportées aux dossiers se sont répercutées dans l’ensemble de l’organisation. Cela peut prendre plusieurs heures.

## Étape 7 : Finalisez la migration des dossiers publics (temps mort requis)

Pour terminer la migration de dossiers publics, exécutez la commande suivante :

    Complete-MigrationBatch PublicFolderMigration

Durant la migration, Exchange effectue une synchronisation finale entre le serveur Exchange hérité et Exchange Online. Si la synchronisation finale fonctionne, les dossiers publics présents sur le serveur Exchange Online sont déverrouillés et le statut du lot de migration affichera **Terminé**. Le statut du lot de migration met généralement quelques heures à passer de **Synchronisé** à **Finalisation en cours**, étape à laquelle la synchronisation commence.

Si vous avez configuré un déploiement hybride entre vos serveurs Exchange locaux et Office 365, vous devez exécuter la commande suivante dans Exchange Online PowerShell une fois la migration terminée :

    Set-OrganizationConfig -RemotePublicFolderMailboxes $Null -PublicFoldersEnabled Local

## Étape 8 : Testez et déverrouillez la migration des dossiers publics

Une fois la migration des dossiers publics finalisée, vous devez exécuter le test suivant pour vous assurer de sa réussite. Cela vous permet de tester la hiérarchie de dossiers publics migrée avant d’utiliser les dossiers publics Office 365 ou Exchange Online.

1.  Dans Office 365 ou Exchange Online PowerShell, attribuez quelques boîtes aux lettres test afin d’utiliser une boîte aux lettres de dossiers publics récemment migrée comme boîte aux lettres de dossiers publics par défaut.
    
        Set-Mailbox -Identity <Test User> -DefaultPublicFolderMailbox <Public Folder Mailbox Identity>

2.  Connectez-vous à Outlook 2007 (ou version ultérieure) avec l’utilisateur test identifié à l’étape précédente, puis exécutez les tests de dossiers publics suivants :
    
      - Affichez la hiérarchie.
    
      - Vérifiez les autorisations.
    
      - Créez et supprimez des dossiers publics.
    
      - Publiez ou effacez du contenu dans un dossier public.

3.  Si vous rencontrez des problèmes, consultez la section Annulation de la migration plus loin dans cette rubrique. Si le contenu et la hiérarchie des dossiers publics sont acceptables et fonctionnent comme prévu, passez à l’étape suivante.

4.  Sur le serveur Exchange hérité, exécutez la commande suivante pour indiquer que la migration de dossiers publics est terminée :
    
        Set-OrganizationConfig -PublicFolderMigrationComplete:$true

5.  Après avoir vérifié que la migration est terminée, exécutez la commande suivante dans Exchange Online PowerShell pour vous assurer que le paramètre *PublicFoldersEnabled* sur **Set-OrganizationConfig** est défini sur `Local` :
    
        Set-OrganizationConfig -PublicFoldersEnabled Local

Pour plus d’informations sur la syntaxe et les paramètres, consultez les rubriques suivantes :

[Set-Mailbox](https://technet.microsoft.com/fr-fr/library/bb123981\(v=exchg.150\))

[Get-Mailbox](https://technet.microsoft.com/fr-fr/library/bb123685\(v=exchg.150\))

[Set-OrganizationConfig](https://technet.microsoft.com/fr-fr/library/aa997443\(v=exchg.150\))

## Comment savoir si cela a fonctionné ?

À l’Étape 2 : Préparez la migration, il vous a été demandé de prendre des instantanés de la structure, des statistiques et des autorisations des dossiers publics avant de lancer la migration. Les étapes suivantes vous permettent de vérifier que votre migration de dossiers publics s’est correctement déroulée en prenant les mêmes instantanés à la fin de la migration. Vous pouvez ensuite comparer les données des deux fichiers pour vérifier la réussite de l’opération.

1.  Dans Exchange Online PowerShell, exécutez la commande suivante pour prendre un instantané de la nouvelle structure de dossiers.
    
        Get-PublicFolder -Recurse | Export-CliXML C:\PFMigration\Cloud_PFStructure.xml

2.  Dans Exchange Online PowerShell, exécutez les commandes suivantes pour prendre un instantané des statistiques de dossiers publics, telles que le nombre, la taille et le propriétaire d’éléments :
    
        Get-PublicFolderStatistics -ResultSize Unlimited | Export-CliXML C:\PFMigration\Cloud_PFStatistics.xml

3.  Dans Exchange Online PowerShell, exécutez la commande suivante pour prendre un instantané des autorisations.
    
        Get-PublicFolder -Recurse | Get-PublicFolderClientPermission | Select-Object Identity,User -ExpandProperty AccessRights | Export-CliXML  C:\PFMigration\Cloud_PFPerms.xml

## Suppression des bases de données de dossiers publics des serveurs Exchange hérités

Une fois la migration terminée, après avoir vérifié que vos dossiers publics Exchange Online fonctionnent comme prévu, vous devez supprimer les bases de données de dossiers publics sur les serveurs Exchange hérités.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159813.important(EXCHG.150).gif" title="Important" alt="Important" />Important :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Dans la mesure où toutes vos boîtes aux lettres ont été migrées vers Office 365 avant la migration du dossier public, nous vous recommandons vivement d’acheminer le trafic via Office 365 (flux de messagerie décentralisé) à la place du flux de messagerie centralisé via votre environnement local. Si vous choisissez de conserver le flux de messagerie centralisé, cela peut entraîner des problèmes de remise à vos dossiers publics, étant donné que vous avez supprimé les bases de données de boîtes aux lettres de dossier public de votre organisation locale.</td>
</tr>
</tbody>
</table>


  - Pour plus d’informations sur la suppression des bases de données de dossiers publics des serveurs Exchange 2007, consultez la rubrique [Suppression de bases de données de dossiers publics](https://go.microsoft.com/fwlink/?linkid=123678).

  - Pour plus d’informations sur la suppression des bases de données de dossiers publics des serveurs Exchange 2010, consultez la rubrique [Supprimer des bases de données de dossiers publics](https://go.microsoft.com/fwlink/?linkid=81409).

## Annulation de la migration

Si vous rencontrez des problèmes en relation avec la migration et devez réactiver vos dossiers publics Exchange hérités, procédez comme suit :

> [!WARNING]
> Si vous annulez votre migration en restaurant les serveurs Exchange hérités, vous perdez tous les messages électroniques envoyés aux dossier publics à extension messagerie ainsi que tout contenu publié dans les dossiers publics après la migration. Pour sauvegarder ce contenu, exportez le contenu des dossiers publics dans un fichier .pst, puis importez-le dans les dossiers publics hérités une fois la restauration terminée.


1.  Sur le serveur Exchange hérité, exécutez la commande suivante pour déverrouiller les dossiers publics Exchange hérités. Ce processus peut prendre plusieurs heures.
    
        Set-OrganizationConfig -PublicFoldersLockedForMigration:$False

2.  Dans Exchange Online PowerShell, exécutez les commandes suivantes pour supprimer tous les dossiers publics Exchange Online.
    
        $hierarchyMailboxGuid = $(Get-OrganizationConfig).RootPublicFolderMailbox.HierarchyMailboxGuid
        
        Get-Mailbox -PublicFolder:$true | Where-Object {$_.ExchangeGuid -ne $hierarchyMailboxGuid} | Remove-Mailbox -PublicFolder -Confirm:$false -Force
        
        Get-Mailbox -PublicFolder:$true | Where-Object {$_.ExchangeGuid -eq $hierarchyMailboxGuid} | Remove-Mailbox -PublicFolder -Confirm:$false -Force

3.  Sur le serveur Exchange hérité, exécutez la commande suivante pour régler l'indicateur `PublicFolderMigrationComplete` sur `$false`.
    
        Set-OrganizationConfig -PublicFolderMigrationComplete:$False

## Migrer des dossiers publics vers Office 365 avec l’exportation PST d’Outlook

Nous vous recommandons de ne pas utiliser la fonctionnalité d’exportation PST d’Outlook pour migrer des dossiers publics vers Office 365 ou Exchange Online si la taille de votre hiérarchie de dossiers publics locale est supérieure à 30 Go. La croissance de la boîte aux lettres de dossiers publics en ligne Office 365 est gérée avec une fonctionnalité de fractionnement automatique qui divise la boîte aux lettres de dossiers publics quand celle-ci dépasse les quotas de taille. La fonctionnalité de fractionnement automatique ne peut pas gérer une croissance soudaine des boîtes aux lettres de dossiers publics lorsque vous utilisez l’exportation PST pour migrer vos dossiers publics. De plus, le déplacement des données à partir de la boîte aux lettres principale avec le fractionnement automatique pourrait prendre jusqu’à deux semaines. En outre, prenez en compte les points suivants avant d’utiliser la fonctionnalité PST d’Outlook pour exporter des dossiers publics vers Office 365 ou Exchange Online :

  - Les autorisations de dossiers publics seront perdues lors de ce processus. Capturez les autorisations actuelles avant la migration et ajoutez-les manuellement de nouveau une fois la migration terminée.

  - Si vous utilisez des autorisations complexes ou si vous avez un grand nombre de dossiers à migrer, nous vous recommandons d’utiliser la méthode de la cmdlet pour la migration.

  - Toute modification d’élément ou de dossier apportée aux dossiers publics sources lors de la migration d’exportation PST sera perdue. Par conséquent, nous vous recommandons d’utiliser la méthode de la cmdlet si ce processus d’exportation et d’importation risque de durer longtemps.

Si vous voulez tout de même migrer vos dossiers publics avec les fichiers PST, procédez comme suit pour assurer une migration réussie.

1.  Suivez les instructions de Étape 1 : Téléchargez les scripts de migration pour télécharger les scripts de migration. Il vous suffit de télécharger le fichier `PublicFolderToMailboxMapGenerator.ps1`.

2.  Suivez l’étape 2 de Étape 3 : génération des fichiers .csv pour créer le fichier de mappage du dossier public à la boîte aux lettres. Ce fichier permet de calculer le nombre correct de boîtes aux lettres de dossiers publics dans Exchange Online.

3.  Créez les boîtes aux lettres de dossiers publics dont vous aurez besoin à partir du fichier de mappage. Pour plus d’informations, voir [Création d’une boîte aux lettres de dossiers publics](create-a-public-folder-mailbox-exchange-2013-help.md).

4.  Utilisez la cmdlet New-PublicFolder pour créer le dossier public de plus haut niveau dans chacune des boîtes aux lettres de dossiers publics, avec le paramètre *Mailbox*.

5.  Exportez et importez les fichiers PST avec Outlook.

6.  Définissez les autorisations sur les dossiers publics avec le CAE. Pour plus d’informations, suivez [Step 3: Assign permissions to the public folder](set-up-public-folders-in-a-new-organization-exchange-2013-help.md) dans la rubrique [Configuration des dossiers publics dans une nouvelle organisation](set-up-public-folders-in-a-new-organization-exchange-2013-help.md).

> [!WARNING]
> Si vous avez déjà commencé une migration PST et que vous avez rencontré un problème lorsque la boîte aux lettres principale est pleine, vous avez deux options pour la récupération de la migration PST :
> <ol>
> <li><p>Attendez que la fonctionnalité de fractionnement automatique ait déplacé les données de la boîte aux lettres principale. Cela peut prendre jusqu’à deux semaines. Toutefois, tous les dossiers publics d’une boîte aux lettres de dossiers publics complètement pleine ne seront pas en mesure de recevoir de nouveaux contenus tant que le fractionnement automatique n’est pas terminé.</p></li>
> <li><p><a href="create-a-public-folder-mailbox-exchange-2013-help.md">Création d’une boîte aux lettres de dossiers publics</a> puis utilisez la cmdlet <strong>New-PublicFolder</strong> avec le paramètre <em>Mailbox</em> pour créer les dossiers publics qui restent dans la boîte aux lettres de dossiers publics secondaire. Cet exemple crée un dossier public nommé PF201 dans la boîte aux lettres de dossiers publics secondaire.</p>
> <pre><code>New-PublicFolder -Name PF201 -Mailbox SecondaryPFMbx</code></pre></li></ol>

## Vous débutez avec Office 365 ?


<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><img src="images/Bb123521.eac8a413-9498-4220-8544-1e37d1aaea13(EXCHG.150).png" title="Icône rapide pour LinkedIn Learning" alt="Icône rapide pour LinkedIn Learning" /> <strong>Vous débutez avec Office 365 ?</strong><br />
Découvrez les cours vidéo gratuits pour <a href="https://support.office.com/fr-fr/article/office-365-admin-and-it-pro-courses-68cc9b95-0bdc-491e-a81f-ee70b3ec63c5">Office 365 admins and IT pros</a> proposés par LinkedIn Learning.</p></td>
</tr>
</tbody>
</table>

