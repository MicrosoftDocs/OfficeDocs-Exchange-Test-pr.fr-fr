---
title: 'Utilis. la migr. par lots de doss. publics Exchange 2010 vers des groupes O365'
TOCTitle: Utilisation de la migration par lots pour migrer des dossiers publics Exchange 2010 vers Groupes Office 365
ms:assetid: d018558d-3075-4dd3-9ff7-91ce66b8d5fb
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Mt843875(v=EXCHG.150)
ms:contentKeyID: 74468756
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Utilisation de la migration par lots pour migrer des dossiers publics Exchange 2010 vers Groupes Office 365

 

_**Sapplique à :** Exchange Server 2010, Exchange Server 2013_

_**Dernière rubrique modifiée :** 2018-04-30_

**Résumé** : Comment déplacer vos dossiers publics Exchange 2010 vers des groupes Office 365.

Grâce à un processus appelé *migration par lots*, vous pouvez déplacer une partie ou la totalité de vos dossiers publics Exchange 2010 vers Groupes Office 365. La fonction Groupes est une nouvelle collaboration proposée par Microsoft, qui offre certains avantages par rapport aux dossiers publics. Consultez l’article [Migration de vos dossiers publics vers Groupes Office 365](https://docs.microsoft.com/fr-fr/exchange/collaboration-exo/public-folders/migrate-your-public-folders-to-office-365-groups) pour obtenir un aperçu des différences entre les dossiers publics et les groupes, et les raisons pour lesquelles passer aux groupes peut être utile ou non à votre organisation.

Cet article contient les procédures étape par étape pour effectuer la migration par lots effective de vos dossiers publics Exchange 2010.

## Ce qu’il faut savoir avant de commencer

Assurez-vous que toutes les conditions suivantes sont remplies avant de commencer la préparation de votre migration.

  - Le serveur Exchange 2010 doit exécuter **Exchange 2010 SP3 RU8** ou une version ultérieure.

  - Dans Exchange Online, vous devez être membre du groupe de rôles Gestion de l’organisation. Ce groupe de rôles diffère des autorisations qui vous sont attribuées quand vous vous abonnez à Office 365 ou à Exchange Online. Pour plus de détails sur l’activation du groupe de rôles Gestion de l’organisation, consultez la rubrique [Gérer des groupes de rôles](manage-role-groups-exchange-2013-help.md).

  - Dans Exchange 2010, vous devez être membre du groupe de rôles RBAC Gestion de l’organisation ou Gestion du serveur. Pour plus d’informations, consultez la rubrique [Ajouter des membres à un groupe de rôles](https://go.microsoft.com/fwlink/?linkid=299212).

  - Avant de migrer vos dossiers publics vers Groupes Office 365, nous vous recommandons de déplacer tout d’abord les boîtes aux lettres utilisateur vers Office 365 pour les utilisateurs ayant besoin d’accéder à Groupes Office 365 après la migration.

  - Outlook Anywhere doit être activé sur le serveur Exchange 2010 qui héberge vos bases de données de dossiers publics. Pour obtenir plus d’informations sur l’activation d’Outlook Anywhere sur des serveurs Exchange 2010, consultez la rubrique [Activer Outlook Anywhere](https://go.microsoft.com/fwlink/p/?linkid=187249).

  - Pour exécuter cette procédure, vous ne pouvez pas utiliser le Centre d’administration Exchange (CAE) ou la console de gestion Exchange (EMC). Sur les serveurs Exchange 2010, vous devez utiliser l’environnement de ligne de commande Exchange Management Shell. Pour Exchange Online, vous devez utiliser Exchange Online PowerShell. Pour obtenir plus d’informations, consultez la rubrique [Connexion à Exchange Online à l’aide de Remote PowerShell](https://technet.microsoft.com/library/jj984289\(v=exchg.150\).aspx).

  - À ce jour, seuls les dossiers publics de type courrier et calendrier peuvent être migrés vers Groupes Office 365 ; la migration des autres types de dossiers publics n’est pas prise en charge. En outre, les groupes cibles dans Office 365 devraient être créés avant la migration.

  - Le processus de migration par lots copie uniquement les messages et les éléments de calendrier provenant de dossiers publics pour la migration vers Groupes Office 365. Il ne copie aucune autre entité des dossiers publics comme les stratégies, les règles et les autorisations.

  - Le service Groupes Office 365 est fourni avec une boîte aux lettres de 50 Go. Vérifiez que la somme des données de dossiers publics à migrer est inférieure à 50 Go. De plus, conservez un espace de stockage pour le contenu supplémentaire à ajouter par vos utilisateurs à l’avenir, après la migration. Nous vous recommandons de ne pas migrer des dossiers publics dont la taille totale est supérieure à 25 Go.

  - Il ne s’agit pas d’une migration « tout ou rien ». Vous pouvez choisir les dossiers publics spécifiques à migrer ; seuls ces dossiers publics sont migrés. Si le dossier public migré contient des sous-dossiers, ces sous-dossiers ne seront pas automatiquement inclus dans la migration. Si vous avez besoin de les migrer, vous devez les inclure explicitement.

  - Les dossiers publics ne seront affectés en aucune façon par cette migration. Toutefois, une fois que vous utilisez notre script de verrouillage pour mettre les dossiers publics migrés en lecture seule, vos utilisateurs sont forcés d’utiliser Groupes Office 365 au lieu des dossiers publics.

  - Avant de commencer, nous vous recommandons de lire cet article dans son intégralité, car un temps d’arrêt est nécessaire pour certaines étapes.

## Étape 1 : Obtenir les scripts

La migration par lots vers Groupes Office 365 nécessite l’exécution d’un nombre de scripts à différents moments du processus de migration, comme décrit dans cet article. Téléchargez les scripts et les fichiers pris en charge [depuis cet emplacement](https://www.microsoft.com/en-us/download/details.aspx?id=55985). Une fois tous les scripts et les fichiers téléchargés, enregistrez-les dans le même emplacement, tel que `c:\PFtoGroups\Scripts`.

Avant de commencer, vérifiez que vous avez téléchargé et enregistré tous les scripts et fichiers suivants :

> [!NOTE]
> Veillez à enregistrer tous les scripts et fichiers au même emplacement.


  - **AddMembersToGroups.ps1**. Ce script ajoute des membres et des propriétaires à Groupes Office 365 en fonction des entrées d’autorisation des dossiers publics sources.

  - **AddMembersToGroups.strings.psd1**. Ce fichier de support est utilisé par le script `AddMembersToGroups.ps1`.

  - **LockAndSavePublicFolderProperties.ps1**. Ce script met les dossiers publics en lecture seule pour empêcher toute modification, et transfère les propriétés de messagerie des dossiers publics (à condition que les dossiers publics soient à extension messagerie) aux groupes cibles, qui redirigent les e-mails à partir de dossiers publics aux groupes cibles. Ce script sauvegarde également les entrées d’autorisation et les propriétés de messagerie avant de les modifier.

  - **LockAndSavePublicFolderProperties.strings.psd1:**  Ce fichier de support est utilisé par le script `LockAndSavePublicFolderProperties.ps1`.

  - **UnlockAndRestorePublicFolderProperties.ps1**. Ce script restaure les droits d’accès et les propriétés de messagerie des dossiers publics à l’aide de fichiers de sauvegarde créés par `LockandSavePublicFolderProperties.ps1`.

  - **UnlockAndRestorePublicFolderProperties.strings.psd1**. Ce fichier de support est utilisé par le script `UnlockAndRestorePublicFolderProperties.ps1`.

  - **WriteLog.ps1**. Ce script autorise les trois scripts précédents à écrire des journaux.

  - **RetryScriptBlock.ps1**. Ce script permet aux scripts `AddMembersToGroups`, `LockAndSavePublicFolderProperties` et `UnlockAndRestorePublicFolderProperties` de réessayer certaines actions en cas d’erreurs temporaires.

Pour obtenir plus d’informations sur les scripts `AddMembersToGroups.ps1`, `LockAndSavePublicFolderProperties.ps1` et `UnlockAndRestorePublicFolderProperties.ps1`, et sur les tâches qu’ils exécutent dans votre environnement, consultez la rubrique Scripts de migration plus loin dans cet article.

## Étape 2 : Préparer la migration

Les étapes suivantes sont nécessaires pour préparer votre organisation à la migration :

1.  Créer une liste de dossiers publics (types courrier et calendrier) à migrer vers Groupes Office 365.

2.  Tenir une liste des groupes cibles correspondants pour chaque dossier public migré. Vous pouvez créer un nouveau groupe dans Office 365 pour chaque dossier public ou utiliser un groupe existant. Si vous créez un nouveau groupe, consultez la rubrique [En savoir plus sur Groupes Office 365](https://go.microsoft.com/fwlink/p/?linkid=858521) pour comprendre les paramètres indispensables d’un groupe. Si l’ensemble d’autorisations par défaut d’un dossier public migré est défini sur **Auteur** ou sur un rôle supérieur, vous devez créer le groupe correspondant dans Office 365 avec le paramètre de confidentialité **Public**. Toutefois, pour que les utilisateurs puissent voir le groupe public sous le nœud **Groupes** dans Outlook, ils doivent quand même rejoindre le groupe.

3.  Renommez les dossiers publics qui contiennent une barre oblique inverse (**\\**) dans leur nom. Dans le cas contraire, il est possible que ces dossiers publics ne soient pas migrés correctement.

4.  La fonctionnalité de migration **PAW** doit être activée pour votre client Office 365. Pour vérifier si c’est le cas, exécutez la commande suivante dans Exchange Online PowerShell :
    
    ```powershell
    Get-MigrationConfig
    ```
    
    Si les résultats sous **Fonctionnalités** indiquent **PAW**, la fonctionnalité est activée et vous pouvez passer à l’*étape 3 : Créer le fichier .csv*.
    
    Si PAW n’est pas encore activé pour votre client, il se peut qu’il existe déjà des lots de migration, soit pour des dossiers publics, soit pour des utilisateurs. Ces lots peuvent avoir n’importe quel état, y compris Terminé. Si tel est le cas, terminez et supprimez des lots de migration existants jusqu’à ce que la commande `Get-MigrationBatch` ne renvoie plus aucun enregistrement. Une fois que tous les lots existants ont été supprimés, PAW doit normalement être activé de façon automatique. Notez que la modification n’apparaît pas immédiatement dans `Get-MigrationConfig`, ce qui est normal. Une fois que cette étape est terminée, vous pouvez continuer à créer de nouveaux lots dans le cas d’une migration d’utilisateurs.

## Étape 3 : Créer le fichier .csv

Créez un fichier .csv, qui fournira des entrées pour un des scripts de migration.

Le fichier .csv doit contenir les colonnes suivantes :

  - **FolderPath**. Chemin d’accès du dossier public à migrer.

  - **TargetGroupMailbox**. Adresse SMTP du groupe cible dans Office 365. Vous pouvez exécuter la commande suivante pour afficher l’adresse SMTP principale.
    
    ```powershell
    Get-UnifiedGroup <alias of the group> | Format-Table PrimarySmtpAddress
    ```

Exemple de fichier .csv :

```powershell
"FolderPath","TargetGroupMailbox"
"\Sales","sales@contoso.onmicrosoft.com"
"\Sales\EMEA","emeasales@contoso.onmicrosoft.com"
```

Notez qu’un dossier de courrier et un dossier de calendrier peuvent être fusionnés en un seul groupe dans Office 365. Toutefois, les autres scénarios de plusieurs dossiers publics fusionnant en un seul groupe ne sont pas pris en charge dans un lot de migration unique. Si vous n’avez pas besoin de mapper plusieurs dossiers publics au même groupe Office 365, vous pouvez le faire par lots de migration différents, qui doivent être exécutés consécutivement, l’un après l’autre. Chaque lot de migration peut contenir jusqu’à 500 entrées.

Un dossier public ne doit être migré qu’à un seul groupe dans un lot de migration.

## Étape 4 : Lancer la demande de migration

Dans cette étape, vous collectez les informations de votre environnement Exchange et vous utilisez ensuite ces informations dans Exchange Online PowerShell pour créer un lot de migration. Après cette étape, vous commencez la migration.

1.  Sur le serveur Exchange 2010, exécutez les commandes suivantes pour collecter les informations nécessaires à la création de votre lot de migration :
    
    1.  Recherchez le **LegacyExchangeDN** pour le compte d’un utilisateur qui est membre du rôle Administrateur de dossiers publics en saisissant la commande suivante. Notez qu’il s’agit du même utilisateur dont les informations d’identification vous sont utiles à l’étape 3 de cette procédure.
        
      ```powershell
      Get-Mailbox <PublicFolder_Administrator_Account> | Select-Object LegacyExchangeDN
      ```
    
    2.  Recherchez le LegacyExchangeDN de tout serveur de boîtes aux lettres disposant d’une base de données de dossiers publics en saisissant la commande suivante :
        
      ```powershell
      Get-ExchangeServer <public folder server> | Select-Object -Expand ExchangeLegacyDN
      ```
    
    3.  Recherchez le nom de domaine complet (FQDN) du nom d’hôte Outlook Anywhere. Il s’agit du nom d’hôte externe. Si vous avez plusieurs instances d’Outlook Anywhere, nous vous recommandons de sélectionner celle qui est la plus proche du point de terminaison de migration ou celle qui est la plus proche des réplicas de dossiers publics dans votre organisation Exchange Server 2010. La commande suivante recherche toutes les instances d’Outlook Anywhere :
        
      ```powershell
      Get-OutlookAnywhere | Format-Table Identity, ExternalHostName
      ```

2.  Dans Exchange Online PowerShell, utilisez les informations renvoyées ci-dessus dans l’étape 1 pour exécuter les commandes suivantes. Les variables dans ces commandes sont les valeurs de l’étape 1.
    
    1.  Transmettez les informations d’identification d’un utilisateur disposant d’autorisations d’administrateur dans l’environnement Exchange 2010 à la variable `$Source_Credential`. Lorsque vous exécutez enfin la demande de migration dans Exchange Online, utilisez ces informations d’identification pour accéder aux serveurs Exchange 2010 afin de copier le contenu dans Exchange Online.
        
      ```powershell
      $Source_Credential = Get-Credential
      <source_domain>\<PublicFolder_Administrator_Account>
      ```
    
    2.  Utilisez le ExchangeLegacyDN de l’utilisateur de migration sur le serveur Exchange hérité que vous avez trouvé à l’étape 1a susmentionnée, puis transmettez cette valeur à la variable `$Source_RemoteMailboxLegacyDN`.
        
      ```powershell
      $Source_RemoteMailboxLegacyDN = "<LegacyExchangeDN from step 1a>"
      ```
    
    3.  Utilisez le ExchangeLegacyDN du dossier public que vous avez trouvé à l’étape 1b susmentionnée, puis transmettez cette valeur à la variable `$Source_RemotePublicFolderServerLegacyDN`.
        
      ```powershell
      $Source_RemotePublicFolderServerLegacyDN = "<LegacyExchangeDN from step 1b>"
      ```
    
    4.  Utilisez le nom d’hôte externe d’Outlook Anywhere renvoyé à l’étape 1c, puis transmettez cette valeur à la variable `$Source_OutlookAnywhereExternalHostName`.
        
      ```powershell
      $Source_OutlookAnywhereExternalHostName = "<ExternalHostName from step 1c>"
      ```

3.  Dans Exchange Online PowerShell, exécutez la commande suivante pour créer un point de terminaison de migration :
    
  ```powershell
  $PfEndpoint = New-MigrationEndpoint -PublicFolderToUnifiedGroup -Name PFToGroupEndpoint -RPCProxyServer $Source_OutlookAnywhereExternalHostName -Credentials $Source_Credential -SourceMailboxLegacyDN $Source_RemoteMailboxLegacyDN -PublicFolderDatabaseServerLegacyDN $Source_RemotePublicFolderServerLegacyDN -Authentication Basic
  ```

4.  Exécutez la commande suivante pour créer un nouveau lot de migration de dossiers publics vers un groupe Office 365. Dans cette commande :
    
      - **CSVData** est le fichier .csv créé ci-dessus à l’*étape 3 : Créer le fichier .csv*. Veillez à bien indiquer le chemin d’accès complet vers ce fichier. Si le fichier a été déplacé pour une raison quelconque, veillez à vérifier et à utiliser le nouvel emplacement.
    
      - **NotificationEmails** est un paramètre facultatif qui peut être utilisé pour définir des adresses e-mail qui recevront des notifications concernant l’état et la progression de la migration.
    
      - **AutoStart** est un paramètre facultatif qui, lorsqu’il est utilisé, lance le lot de migration dès qu’il est créé.
    
      - **PublicFolderToUnifiedGroup** est le paramètre qui permet d’indiquer s’il s’agit d’un lot de migration de dossiers publics vers Groupes Office 365.
    
    <!-- end list -->
    
  ```powershell
  New-MigrationBatch -Name PublicFolderToGroupMigration -CSVData (Get-Content <path to .csv file> -Encoding Byte) -PublicFolderToUnifiedGroup -SourceEndpoint $PfEndpoint.Identity [-NotificationEmails <email addresses for migration notifications>] [-AutoStart]
  ```

5.  Lancez la migration en exécutant la commande suivante dans Exchange Online PowerShell. Notez que cette étape est nécessaire uniquement si le paramètre `-AutoStart` n’a pas été utilisé lors de la création du lot précédemment à l’étape 4.
    
  ```powershell
  Start-MigrationBatch PublicFolderToGroupMigration
  ```

Tandis que les migrations par lots doivent être créées à l’aide de la cmdlet `New-MigrationBatch` dans Exchange Online PowerShell, l’avancement de la migration peut être affiché et géré dans Centre d’administration Exchange. Vous pouvez également afficher la progression de la migration en exécutant les cmdlets [Get-MigrationBatch](https://technet.microsoft.com/fr-fr/library/jj219164\(v=exchg.150\)) et [Get-MigrationUser](https://technet.microsoft.com/fr-fr/library/jj218702\(v=exchg.150\)). La cmdlet `New-MigrationBatch` lance un utilisateur de migration pour chaque boîte aux lettres de groupe Office 365, et vous pouvez afficher l’état de ces requêtes à l’aide de la page de migration de boîtes aux lettres.

Pour accéder à la page de migration de boîte aux lettres, procédez comme suit :

1.  Dans Exchange Online, ouvrez Centre d’administration Exchange.

2.  Accédez à **Destinataires**, puis sélectionnez **Migration**.

3.  Sélectionnez la demande de migration qui vient d’être créée, puis, dans le volet **Détails**, cliquez sur **Afficher les détails**.

Lorsque l’état du lot est **Terminé**, vous pouvez passer à l’*étape 5 : Ajouter des membres aux groupes Office 365 à partir de dossiers publics*.

## Étape 5 : Ajouter des membres aux groupes Office 365 à partir de dossiers publics

Vous pouvez ajouter manuellement des membres au groupe cible dans Office 365 le cas échéant. Toutefois, pour ajouter des membres au groupe en fonction des entrées d’autorisation dans les dossiers publics, exécutez le script `AddMembersToGroups.ps1` sur le serveur Exchange 2010 comme indiqué dans la commande suivante. Les boîtes aux lettres utilisateur doivent être synchronisées avec Exchange Online pour être ajoutées en tant que membres d’un groupe Office 365. Pour connaître les autorisations à des dossiers publics pouvant être ajoutées en tant que membres d’un groupe dans Office 365, consultez la rubrique Scripts de migration plus loin dans cet article.

Dans la commande suivante :

  - **MappingCsv** est le fichier .csv généré dans l’*étape 3 : Créer le fichier .csv*. Veillez à bien indiquer le chemin d’accès complet à ce fichier. Si le fichier a été déplacé pour une raison quelconque, veillez à vérifier et à utiliser le nouvel emplacement.

  - **BackupDir** est le répertoire où sont enregistrés les fichiers journaux de migration.

  - **ArePublicFoldersOnPremises** est un paramètre qui permet d’indiquer si les dossiers publics sont situés en local ou dans Exchange Online.

  - **Credential** est le nom d’utilisateur et le mot de passe Exchange Online.

<!-- end list -->

```powershell
.\AddMembersToGroups.ps1 -MappingCsv <path to .csv file> -BackupDir <path to backup directory> -ArePublicFoldersOnPremises $true -Credential (Get-Credential)
```

Une fois que les utilisateurs ont été ajoutés à un groupe dans Office 365, ils peuvent commencer à l’utiliser.

## Étape 6 : Verrouiller les dossiers publics (temps d’arrêt obligatoire des dossiers publics)

Lorsque la majorité des données de vos dossiers publics a été migrée vers Groupes Office 365, vous pouvez exécuter le script `LockAndSavePublicFolderProperties.ps1` sur le serveur Exchange 2010 pour mettre les dossiers publics en lecture seule. Cette étape permet de s’assurer qu’aucune nouvelle donnée n’est ajoutée aux dossiers publics avant la fin de la migration.

> [!NOTE]
> S’il existe des dossiers publics à extension messagerie (MEPF) parmi les dossiers publics migrés, cette étape copie certaines propriétés des MEPF, telles que les adresses SMTP, dans le groupe correspondant dans Office 365, puis désactive la messagerie du dossier public. Étant donné que la messagerie des MEPF migrés est désactivée après l’exécution de ce script, vous commencez à voir des e-mails envoyés aux MEPF au lieu de les recevoir dans les groupes correspondants. Pour obtenir plus d’informations, consultez la rubrique Scripts de migration plus loin dans cet article.


Dans la commande suivante :

  - **MappingCsv** est le fichier .csv généré dans l’*étape 3 : Créer le fichier .csv*. Veillez à bien indiquer le chemin d’accès complet à ce fichier. Si le fichier a été déplacé pour une raison quelconque, veillez à vérifier et à utiliser le nouvel emplacement.

  - **BackupDir** est le répertoire où sont enregistrés les fichiers de sauvegarde pour les entrées d’autorisation, les propriétés des MEPF et les fichiers journaux de migration. Cette sauvegarde s’avère utile si vous devez restaurer les dossiers publics.

  - **ArePublicFoldersOnPremises** est un paramètre qui permet d’indiquer si les dossiers publics sont situés en local ou dans Exchange Online.

  - **Credential** est le nom d’utilisateur et le mot de passe Exchange Online.

<!-- end list -->

```powershell
.\LockAndSavePublicFolderProperties.ps1 -MappingCsv <path to .csv file> -BackupDir <path to backup directory> -ArePublicFoldersOnPremises $true -Credential (Get-Credential)
```

## Étape 7 : Finaliser la migration des dossiers publics vers Groupes Office 365

Après avoir mis vos dossiers publics en lecture seule, vous devrez recommencer la migration. Cela est nécessaire pour obtenir une copie finale incrémentielle de vos données. Avant de pouvoir exécuter à nouveau la migration, vous devrez supprimer le lot existant. Pour ce faire, exécutez la commande suivante :

```powershell
Remove-MigrationBatch <name of migration batch>
```

Ensuite, créez un nouveau lot avec le même fichier .csv en exécutant la commande suivante. Dans cette commande :

  - **CsvData** est le fichier .csv généré dans l’*étape 3 : Créer le fichier .csv*. Veillez à bien indiquer le chemin d’accès complet à ce fichier. Si le fichier a été déplacé pour une raison quelconque, veillez à vérifier et à utiliser le nouvel emplacement.

  - **NotificationEmails** est un paramètre facultatif qui peut être utilisé pour définir des adresses e-mail qui recevront des notifications concernant l’état et la progression de la migration.

  - **AutoStart** est un paramètre facultatif qui, lorsqu’il est utilisé, lance le lot de migration dès qu’il est créé.

<!-- end list -->

```powershell
New-MigrationBatch -Name PublicFolderToGroupMigration -CSVData (Get-Content <path to .csv file> -Encoding Byte) -PublicFolderToUnifiedGroup -SourceEndpoint $PfEndpoint.Identity [-NotificationEmails <email addresses for migration notifications>] [-AutoStart]
```

Une fois le nouveau lot créé, lancez la migration en exécutant la commande suivante dans Exchange Online PowerShell. Notez que cette étape est nécessaire uniquement si le paramètre `-AutoStart` n’a pas été utilisé dans la commande précédente.

```powershell
Start-MigrationBatch PublicFolderToGroupMigration
```

Une fois cette étape terminée (l’état du lot est **Terminé**), vérifiez que toutes les données ont été copiées dans Groupes Office 365. À ce stade, dès lors que vous êtes satisfait de l’expérience des groupes, vous pouvez commencer à supprimer les dossiers publics migrés à partir de votre environnement Exchange 2010.

> [!IMPORTANT]
> Bien qu’il existe des procédures prises en charge pour restaurer la migration et revenir aux dossiers publics, cela n’est pas possible quand les dossiers publics sources ont été supprimés. Consultez Comment puis-je restaurer les dossiers publics à partir de Groupes Office 365 ? pour obtenir plus d’informations.


## Problèmes connus

Les problèmes connus suivants peuvent survenir au cours d’une migration classique de dossiers publics vers Groupes Office 365.

  - Le script qui transfert l’adresse SMTP de dossiers publics à extension messagerie vers Groupes Office 365 ajoute uniquement les adresses comme adresses e-mail secondaires dans Exchange Online. Pour cette raison, si vous avez configuré Exchange Online Protection (EOP) ou le flux de messagerie centralisé dans votre environnement, des problèmes d’envoi d’e-mail aux groupes (aux adresses e-mail secondaires) surviennent après la migration.

  - Si le fichier de mappage .csv comporte une entrée dont le chemin d’accès de dossier public n’est pas valide, le lot de migration s’affiche sous la forme **Terminé** sans détecter d’erreur et aucune autre donnée n’est copiée.

## Scripts de migration

Pour votre information, cette section fournit des descriptions détaillées de trois des scripts de migration et les tâches qu’ils exécutent dans votre environnement Exchange. Tous les scripts et les fichiers pris en charge peuvent être [téléchargés depuis cet emplacement](https://www.microsoft.com/en-us/download/details.aspx?id=55985).

## AddMembersToGroups.ps1

Ce script lit les autorisations des dossiers publics migrés, puis ajoute des membres et des propriétaires à Groupes Office 365 comme suit :

  - Les utilisateurs associés aux rôles d’autorisation suivants sont ajoutés en tant que membres à un groupe dans Office 365. **Rôles d’autorisation** : Propriétaire, PublishingEditor, éditeur, PublishingAuthor, auteur

  - Par ailleurs, les utilisateurs disposant des droits d’accès minimum suivants sont également ajoutés en tant que membres à un groupe dans Office 365. **Droits d’accès** : ReadItems, CreateItems, FolderVisible, EditOwnedItems, DeleteOwnedItems

  - Les utilisateurs disposant du droit d’accès « propriétaire » sont ajoutés en tant que propriétaires à un groupe et les utilisateurs disposant d’autres droits d’accès admissibles sont ajoutés en tant que membres.

  - Les groupes de sécurité ne peuvent pas être ajoutés en tant que membres aux groupes dans Office 365. Par conséquent, ils sont développés, puis des utilisateurs individuels sont ajoutés comme membres ou propriétaires aux groupes en fonction des droits d’accès du groupe de sécurité.

  - Lorsque les utilisateurs de groupes de sécurité disposant des droits d’accès sur un dossier public ont eux-mêmes des autorisations explicites sur le même dossier public, les autorisations explicites sont prioritaires. Par exemple, prenons le cas d’un groupe de sécurité appelé « SG1 » qui comporte les membres User1 et User2. Les entrées d’autorisation du dossier public « PF1 » sont les suivantes :
    
    GS1 : Auteur de PF1
    
    User1 : Propriétaire de PF1
    
    Dans ce cas, User1 est ajouté comme propriétaire au groupe dans Office 365.

  - Lorsque l’autorisation par défaut d’un dossier public migré est définie sur « Auteur » ou sur un rôle supérieur, le script suggère de définir le paramètre de confidentialité du groupe correspondant sur « Public ».

Ce script peut être exécuté même après le verrouillage des dossiers publics, avec le paramètre `ArePublicFoldersLocked` défini sur ` $true`. Dans ce scénario, le script lit les autorisations d’accès en lecture à partir du fichier de sauvegarde créé au cours du verrouillage.

## LockAndSavePublicFolderProperties.ps1

Avec ce script, les dossiers publics sont migrés en lecture seule. Lorsque des dossiers publics à extension messagerie sont migrés, leur messagerie est d’abord désactivée et leurs adresses SMTP sont ajoutées aux groupes respectifs dans Office 365. Ensuite, les entrées d’autorisation sont modifiées pour être en lecture seule. Les propriétés de messagerie des dossiers publics à extension messagerie, ainsi que les entrées d’autorisation de tous les dossiers publics, sont sauvegardées en copie avant d’être modifiées.

S’il existe plusieurs lots de migration, un dossier de sauvegarde distinct doit être utilisé avec chaque fichier de mappage .csv.

Les propriétés de messagerie suivantes, ainsi que les dossiers publics respectifs à extension messagerie et les groupes Office 365 sont stockés :

  - PrimarySMTPAddress

  - EmailAddresses

  - ExternalEmailAddress

  - EmailAddressPolicyEnabled

  - GrantSendOnBehalfTo

  - Liste de clients approuvés SendAs

Les propriétés de messagerie susmentionnées sont stockées dans un fichier .csv, qui peut être utilisé lors du processus de restauration (si vous voulez revenir à l’utilisation des dossiers publics, consultez la rubrique Comment puis-je restaurer les dossiers publics à partir de Groupes Office 365 ? pour obtenir plus d’informations). Une capture instantanée des propriétés des dossiers publics à extension messagerie est également stockée dans un fichier appelé PfMailProperties.csv. Ce fichier n’est pas nécessaire pour le processus de restauration, mais peut tout de même être utilisé à titre informatif.

Les propriétés de messagerie suivantes sont migrées vers le groupe cible dans le cadre du verrouillage :

  - PrimarySMTPAddress

  - EmailAddresses

  - Liste de clients approuvés SendAs

  - GrantSendOnBehalfTo

Le script garantit l’ajout des propriétés PrimarySMTPAddress et EmailAddresses des dossiers publics à extension messagerie migrés en tant qu’adresses SMTP secondaires des groupes correspondants dans Office 365. En outre, les autorisations SendAs et SendOnBehalfTo des utilisateurs sur les dossiers publics à extension messagerie reçoivent une autorisation équivalente dans les groupes cibles correspondants.

**Droits d’accès accordés**

Seuls les droits d’accès suivants sont accordés afin que les utilisateurs s’assurent que les dossiers publics sont mis en lecture seule pour tous les utilisateurs.

  - ReadItems

  - CreateSubfolders

  - FolderContact

  - FolderVisible

Les entrées d’autorisation sont modifiées comme suit :

1.  ###  
    
    <table>
    <colgroup>
    <col style="width: 50%" />
    <col style="width: 50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>Avant le verrouillage</th>
    <th>Après le verrouillage</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p>Aucune</p></td>
    <td><p>Aucune</p></td>
    </tr>
    <tr class="even">
    <td><p>AvailabilityOnly</p></td>
    <td><p>AvailabilityOnly</p></td>
    </tr>
    <tr class="odd">
    <td><p>LimitedDetails</p></td>
    <td><p>LimitedDetails</p></td>
    </tr>
    <tr class="even">
    <td><p>Collaborateur</p></td>
    <td><p>FolderVisible</p></td>
    </tr>
    <tr class="odd">
    <td><p>Relecteur</p></td>
    <td><p>ReadItems, FolderVisible</p></td>
    </tr>
    <tr class="even">
    <td><p>NonEditingAuthor</p></td>
    <td><p>ReadItems, FolderVisible</p></td>
    </tr>
    <tr class="odd">
    <td><p>Auteur</p></td>
    <td><p>ReadItems, FolderVisible</p></td>
    </tr>
    <tr class="even">
    <td><p>Éditeur</p></td>
    <td><p>ReadItems, FolderVisible</p></td>
    </tr>
    <tr class="odd">
    <td><p>PublishingAuthor</p></td>
    <td><p>ReadItems, CreateSubfolders, FolderVisible</p></td>
    </tr>
    <tr class="even">
    <td><p>PublishingEditor</p></td>
    <td><p>ReadItems, CreateSubfolders, FolderVisible</p></td>
    </tr>
    <tr class="odd">
    <td><p>Propriétaire</p></td>
    <td><p>ReadItems, CreateSubfolders, FolderContact, FolderVisible</p></td>
    </tr>
    </tbody>
    </table>


2.  Les droits d’accès des utilisateurs sans autorisation d’accès en lecture restent intacts, et ils continuent d’être bloqués des droits de lecture.

3.  En ce qui concerne les utilisateurs associés à des rôles personnalisés, si les droits d’accès ne sont pas ReadItems, CreateSubfolders, FolderContact ou FolderVisible, ils sont supprimés. Dans le cas où les utilisateurs ne possèderaient aucun droit d’accès de la liste autorisée après le filtrage, le droit d’accès de ces utilisateurs est défini sur « Aucun ».

Il peut y avoir une interruption de l’envoi d’e-mails aux dossiers publics à extension messagerie entre la désactivation de la messagerie des dossiers et l’ajout de leurs adresses SMTP à Groupes Office 365.

## UnlockAndRestorePublicFolderProperties.ps1

Ce script réattribue des autorisations aux dossiers publics en fonction du fichier de sauvegarde pris pendant le verrouillage des dossiers publics. Ce script permet aussi d’activer la messagerie des dossiers publics qui a été désactivée, après avoir supprimé les adresses SMTP des dossiers à partir de leurs groupes respectifs dans Office 365. Un léger temps d’arrêt peut survenir au cours du processus.

## Comment puis-je restaurer les dossiers publics à partir de Groupes Office 365 ?

Si vous changez d’avis et souhaitez revenir à l’utilisation des dossiers publics après avoir utilisé Groupes Office 365, la commande répertoriée ci-dessous permet de restaurer votre environnement à l’état dans lequel il était avant la migration. Il est possible d’effectuer une restauration dans la mesure où les fichiers de sauvegarde existent et que vous n’avez pas supprimé les dossiers publics après la migration.

Sur votre serveur Exchange 2010, exécutez la commande suivante. Dans cette commande :

  - **BackupDir** est le répertoire où sont enregistrés les fichiers de sauvegarde pour les entrées d’autorisation, les propriétés des MEPF et les fichiers journaux de migration. Veillez à utiliser le même emplacement que celui indiqué à l’*étape 6 : Verrouiller les dossiers publics à basculer (temps d’arrêt obligatoire des dossiers publics)*.

  - **ArePublicFoldersOnPremises** est un paramètre qui permet d’indiquer si les dossiers publics sont situés en local ou dans Exchange Online.

  - **Credential** est le nom d’utilisateur et le mot de passe Exchange Online.

<!-- end list -->

```powershell
.\UnlockAndRestorePublicFolderProperties.ps1 -BackupDir <path to backup directory> -ArePublicFoldersOnPremises $true -Credential (Get-Credential)
```

N’oubliez pas qu’aucun des éléments ajoutés au groupe Office 365 ou des opérations de modification effectuées dans les groupes n’est copié dans vos dossiers publics. Par conséquent, il y aura une perte de données, en supposant que de nouvelles données ont été ajoutées alors que le dossier public était un groupe.

Notez également qu’il n’est pas possible de restaurer un sous-ensemble de dossiers publics, ce qui signifie que tous les dossiers publics migrés doivent être restaurés.

Les groupes correspondants dans Office 365 ne sont pas supprimés dans le cadre du processus de restauration. Vous devez nettoyer ou supprimer ces groupes manuellement.

