---
title: 'Nettoyer le dossier Éléments récupérables: Exchange 2013 Help'
TOCTitle: Nettoyer le dossier Éléments récupérables
ms:assetid: 82c310f8-de2f-46f2-8e1a-edb6055d6e69
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Ff678798(v=EXCHG.150)
ms:contentKeyID: 50555422
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
f1_keywords:
- dépassement classé
- Dépassement de messages
- dépassement des messages classés
- nettoyage de dépassements classés
- nettoyage de dépassements de message
- nettoyage du dépassement des messages classés
- Rechercher et détruire
ms.translationtype: HT
---

# Nettoyer le dossier Éléments récupérables

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2015-09-30_

Le dossier Éléments récupérables (connu dans les versions antérieures d’Exchange sous le nom de *conteneur de dépôt*) existe pour assurer une protection en cas de suppressions accidentelles ou malveillantes et pour faciliter les tâches de détection couramment effectuées avant ou pendant un litige ou des recherches. Pour plus d’informations sur le dossier Éléments récupérables, voir [Dossier Éléments récupérables](recoverable-items-folder-exchange-2013-help.md).

La méthode de nettoyage du dossier Éléments récupérables de la boîte aux lettres varie si la boîte aux lettres est en conservation pour litige ou inaltérable, ou si la récupération d’élément unique a été activée :

  - Si une boîte aux lettres n’est pas placée en conservation pour litige ou inaltérable, ou si la récupération d’élément unique n’est pas activée, vous pouvez simplement supprimer les éléments du dossier Éléments récupérables. Après suppression, vous ne pouvez pas utiliser le paramètre de récupération d’élément unique pour retrouver les éléments.

  - Si la boîte aux lettres est placée en conservation pour litige ou inaltérable, ou si la récupération d’élément unique est activée, il est important de protéger les données de la boîte aux lettres jusqu’à la suppression de la conservation ou l’activation de la récupération d’élément unique. Dans ce cas, vous devez exécuter des étapes plus détaillées pour le nettoyage du dossier Éléments récupérables.

Pour en savoir plus sur la conservation pour litige ou inaltérable, voir [Conservation inaltérable et conservation pour litige](https://docs.microsoft.com/fr-fr/exchange/security-and-compliance/in-place-and-litigation-holds). Pour plus d’informations sur la récupération d’élément unique, voir la rubrique « Récupération d’élément unique » dans [Dossier Éléments récupérables](recoverable-items-folder-exchange-2013-help.md).

Pour plus d’informations sur le dossier Éléments récupérables, voir [Dossier Éléments récupérables](recoverable-items-folder-exchange-2013-help.md).

## Ce qu’il faut savoir avant de commencer ?

  - Durée estimée de la procédure : 30 minutes. Cela peut varier selon la taille du dossier Éléments récupérables

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Suppression du contenu de la boîte aux lettres » dans la rubrique [Stratégie de messagerie et autorisations de conformité](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

  - Étant donné que le mauvais nettoyage du dossier Éléments récupérables peut entraîner la perte de données, il est important de savoir ce que contient le contenu du dossier Éléments récupérables et l’impact sur le retrait de son contenu. Avant d’exécuter cette procédure, nous vous recommandons de consulter les informations dans [Dossier Éléments récupérables](recoverable-items-folder-exchange-2013-help.md).

  - Vous ne pouvez pas utiliser le Centre d’administration Exchange (CAE) pour effectuer ces procédures. Vous devez utiliser l'environnement de ligne de commande Exchange Management Shell.

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), et [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

## Utiliser l’environnement de ligne de commande Exchange Management Shell afin de supprimer des éléments du dossier Éléments récupérables pour les boîtes aux lettres qui ne sont pas placées en conservation ou pour lesquelles la récupération d’élément unique n’est pas activée

Cet exemple supprime de manière permanente les éléments du dossier Éléments récupérables de Gurinder Singh et copie également les éléments dans le dossier GurinderSingh-RecoverableItems de la boîte aux lettres de détection (créée par le programme d’installation Exchange).

```powershell
Search-Mailbox -Identity "Gurinder Singh" -SearchDumpsterOnly -TargetMailbox "Discovery Search Mailbox" -TargetFolder "GurinderSingh-RecoverableItems" -DeleteContent
```

> [!NOTE]
> Pour supprimer les éléments de la boîte aux lettres sans les copier vers une autre boîte aux lettres, utilisez la commande précédente sans les paramètres <em>TargetMailbox</em> et <em>TargetFolder</em>.


Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Search-Mailbox](https://technet.microsoft.com/fr-fr/library/dd298173\(v=exchg.150\)).

## Utiliser l’environnement de ligne de commande Exchange Management Shell afin de nettoyer le dossier Éléments récupérables pour les boîtes aux lettres qui sont placées en conservation ou pour lesquelles la récupération d’élément unique est activée

Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Suppression du contenu de la boîte aux lettres » dans la rubrique [Stratégie de messagerie et autorisations de conformité](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

Si une boîte aux lettres atteint son quota d’éléments récupérables, nous vous recommandons d’augmenter le quota et de ne pas supprimer les éléments du dossier. Vous pouvez également surveiller les événements dans le journal des applications relatif au quota d’avertissement des éléments récupérables et entreprendre les actions nécessaires (telles que l’augmentation du quota ou la recherche de croissance du dossier Éléments récupérables pour les boîtes aux lettres qui atteignent le quota d’avertissement).

Si des contraintes de stockage ou des problèmes similaires vous empêchent d’augmenter le quota d’éléments récupérables et si vous devez supprimer des messages du dossier Éléments récupérables d’une boîte aux lettres placée en conservation pour litige ou inaltérable, ou pour laquelle la récupération d’élément unique a été activée, nous vous recommandons de commencer par copier les données du dossier Éléments récupérables de l’utilisateur dans une autre boîte aux lettres. Si vous supprimez les éléments en raison de contraintes de stockage sur un volume, vous pouvez copier les éléments sur une boîte aux lettres située sur un volume qui dispose d’un stockage adéquat.

Cette procédure copie les éléments du dossier Éléments récupérables de Gurinder Singh dans le dossier GurinderSingh-RecoverableItems dans la boîte aux lettres de détection. Avant de copier et de supprimer les éléments du dossier Éléments récupérables, vous devez d’abord effectuer plusieurs étapes pour vous assurer que les éléments ne sont pas supprimés du dossier Éléments récupérables. Après avoir copié les éléments dans une boîte aux lettres de recherche ou de sauvegarde et avoir nettoyé le dossier, vous pouvez revenir aux paramètres précédents de la boîte aux lettres.

1.  Récupérez les paramètres de quota suivants. Assurez-vous de noter les valeurs afin de pouvoir récupérer ces paramètres après nettoyage du dossier Éléments récupérables :
    
      - *RecoverableItemsQuota*
    
      - *RecoverableItemsWarningQuota*
    
      - *ProhibitSendQuota*
    
      - *ProhibitSendReceiveQuota*
    
      - *UseDatabaseQuotaDefaults*
    
      - *RetainDeletedItemsFor*
    
      - *UseDatabaseRetentionDefaults*
    
    > [!NOTE]
    > Si le paramètre <em>UseDatabaseQuotaDefaults</em> est défini à <code>$true</code>, les paramètres de quota précédents ne sont pas appliqués. Les paramètres de quota correspondants et configurés sur la base de données de boîte aux lettres sont appliqués, même si des paramètres de boîte aux lettres individuels sont renseignés.
    
    ```powershell
    Get-Mailbox "Gurinder Singh" | Format-List RecoverableItemsQuota, RecoverableItemsWarningQuota, ProhibitSendQuota, ProhibitSendReceiveQuota, UseDatabaseQuotaDefaults, RetainDeletedItemsFor, UseDatabaseRetentionDefaults
    ```

2.  Récupérez les paramètres d’accès de boîte aux lettres relatifs à cette dernière. Assurez-vous de noter ces paramètres pour une utilisation ultérieure.
    
    ```powershell
    Get-CASMailbox "Gurinder Singh" | Format-List EwsEnabled, ActiveSyncEnabled, MAPIEnabled, OWAEnabled, ImapEnabled, PopEnabled
    ```

3.  Récupérez la taille actuelle du dossier Éléments récupérables. Notez la taille afin de pouvoir augmenter les quotas à l’étape 6.
    
    ```powershell
    Get-MailboxFolderStatistics "Gurinder Singh" -FolderScope RecoverableItems | Format-List Name,FolderAndSubfolderSize
    ```

4.  Récupérez la configuration de cycle de fonctionnement de l’Assistant Dossier géré actuel. Assurez-vous de noter ces paramètres pour une utilisation ultérieure.
    
    ```powershell
    Get-MailboxServer "My Mailbox Server" | Format-List Name,ManagedFolderWorkCycle
    ```

5.  Désactivez l’accès du client à la boîte aux lettres pour vous assurer qu’aucune modification ne peut être effectuée sur les données de boîte aux lettres pour la durée de cette procédure.
    
    ```powershell
    Set-CASMailbox "Gurinder Singh" -EwsEnabled $false -ActiveSyncEnabled $false -MAPIEnabled $false -OWAEnabled $false -ImapEnabled $false -PopEnabled $false
    ```

6.  Pour vous assurer qu’aucun élément n’est supprimé du dossier Éléments récupérables, augmentez le quota d’éléments récupérables, augmentez le quota d’avertissement d’éléments récupérables et définissez la période de rétention des éléments supprimés à une valeur supérieure à la taille actuelle du dossier Éléments récupérables de l’utilisateur. Ceci est particulièrement important pour la conservation de messages de boîtes aux lettres qui sont en conservation pour litige ou inaltérable. Nous vous recommandons d’augmenter ces paramètres en multipliant par deux la taille actuelle.
    
    ```powershell
    Set-Mailbox "Gurinder Singh" -RecoverableItemsQuota 50Gb -RecoverableItemsWarningQuota 50Gb -RetainDeletedItemsFor 3650 -ProhibitSendQuota 50Gb -ProhibitSendRecieveQuota 50Gb -UseDatabaseQuotaDefaults $false -UseDatabaseRetentionDefaults $false
    ```

7.  Désactivez l’Assistant Dossier géré sur le serveur de boîte aux lettres.
    
    ```powershell
    Set-MailboxServer MyMailboxServer -ManagedFolderWorkCycle $null
    ```
    
    > [!IMPORTANT]
    > Si la boîte aux lettres se trouve sur une base de données de boîtes aux lettres dans un groupe de disponibilité de base de données, vous devez désactiver l’Assistant Dossier géré sur chaque membre du groupe de disponibilité de base de données qui héberge une copie de la base de données. Si la base de données échoue sur un autre serveur, cela empêche l’Assistant Dossier géré sur ce serveur de supprimer les données de la boîte aux lettres.


8.  Désactivez la récupération d’élément unique et supprimez la conservation pour litige de la boîte aux lettres.
    
    ```powershell
    Set-Mailbox "Gurinder Singh" -SingleItemRecoveryEnabled $false -LitigationHoldEnabled $false
    ```
    
    > [!IMPORTANT]
    > Après exécution de cette commande, il faut parfois une heure pour désactiver la récupération d’élément unique ou la conservation pour litige. Nous vous recommandons d’effectuer la prochaine étape uniquement après écoulement de cette période.


9.  Copiez les éléments du dossier Éléments récupérables vers un dossier qui se trouve dans la boîte aux lettres de détection et supprimez le contenu de la boîte aux lettres source.
    
    ```powershell
    Search-Mailbox -Identity "Gurinder Singh" -SearchDumpsterOnly -TargetMailbox "Discovery Search Mailbox" -TargetFolder "GurinderSingh-RecoverableItems" -DeleteContent
    ```
    
    Si vous avez besoin de supprimer uniquement les messages qui correspondent aux conditions spécifiées, utilisez le paramètre *SearchQuery* pour spécifier les conditions. Cet exemple supprime les messages qui disposent de la chaîne « Votre relevé de compte » dans le champ **Objet**.
    
    ```powershell
    Search-Mailbox -Identity "Gurinder Singh" -SearchQuery "Subject:'Your bank statement'" -SearchDumpsterOnly -TargetMailbox "Discovery Search Mailbox" -TargetFolder "GurinderSingh-RecoverableItems" -DeleteContent
    ```
    
    > [!NOTE]
    > Il n’est pas nécessaire de copier les éléments dans la boîte aux lettres de détection. Vous pouvez copier des messages dans toute boîte aux lettres. Cependant, pour empêcher l’accès aux données de boîtes aux lettres éventuellement sensibles, nous vous recommandons de copier les messages dans une boîte aux lettres dont l’accès est limité aux responsables d’enregistrements autorisés. Par défaut, l’accès à la boîte aux lettres de détection par défaut est limité aux membres du groupe de rôles Gestion de la découverte. Pour plus d’informations, consultez la rubrique <a href="https://docs.microsoft.com/fr-fr/exchange/security-and-compliance/in-place-ediscovery/in-place-ediscovery">Découverte électronique locale</a>.


10. Si la boîte aux lettres a été placée en conservation pour litige ou si la récupération d’élément unique a été préalablement activée, activez à nouveau ces fonctionnalités.
    
    ```powershell
    Set-Mailbox "Gurinder Singh" -SingleItemRecoveryEnabled $true -LitigationHoldEnabled $true
    ```
    
    > [!IMPORTANT]
    > Après exécution de cette commande, il faut parfois une heure pour activer la récupération d’élément unique ou la conservation pour litige. Nous vous recommandons d’activer l’Assistant Dossier géré et d’autoriser l’accès au client (étapes 11 et 12) uniquement après écoulement de cette période.


11. Reparamétrez les quotas suivants aux valeurs notées à l’étape 1 :
    
      - *RecoverableItemsQuota*
    
      - *RecoverableItemsWarningQuota*
    
      - *ProhibitSendQuota*
    
      - *ProhibitSendReceiveQuota*
    
      - *UseDatabaseQuotaDefaults*
    
      - *RetainDeletedItemsFor*
    
      - *UseDatabaseRetentionDefaults*
    
    Dans cet exemple, la boîte aux lettres est supprimée du blocage de rétention, la période de rétention de l’élément supprimé est redéfinie à la valeur par défaut de 14 jours et le quota d’éléments récupérables est configuré pour utiliser la même valeur que pour la base de données de boîte aux lettres. Si les valeurs que vous avez notées à l’étape 1 sont différentes, vous devez utiliser les paramètres précédents pour spécifier chaque valeur et définir le paramètre *UseDatabaseQuotaDefaults* à `$false`. Si les paramètres *RetainDeletedItemsForand UseDatabaseRetentionDefaults* ont été préalablement définis à une valeur différente, vous devez également les rétablir aux valeurs indiquées à l’étape 1.
    
    ```powershell
    Set-Mailbox "Gurinder Singh" -RetentionHoldEnabled $false -RetainDeletedItemsFor 14 -RecoverableItemsQuota unlimited -UseDatabaseQuotaDefaults $true
    ```

12. Activez l’Assistant Dossier géré en redéfinissant le cycle de travail à la valeur indiquée à l’étape 4. Cet exemple définit le cycle de travail à un jour.
    
    ```powershell
    Set-MailboxServer MyMailboxServer -ManagedFolderWorkCycle 1
    ```

13. Activez l’accès au client.
    
    ```powershell
    Set-CASMailbox -ActiveSyncEnabled $true -EwsEnabled $true -MAPIEnabled $true -OWAEnabled $true -ImapEnabled $true -PopEnabled $true
    ```

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, consultez les rubriques suivantes :

  - [Get-Mailbox](https://technet.microsoft.com/fr-fr/library/bb123685\(v=exchg.150\))

  - [Get-CASMailbox](https://technet.microsoft.com/fr-fr/library/bb124754\(v=exchg.150\))

  - [Get-MailboxFolderStatistics](https://technet.microsoft.com/fr-fr/library/aa996762\(v=exchg.150\))

  - [Get-MailboxServer](https://technet.microsoft.com/fr-fr/library/bb123539\(v=exchg.150\))

  - [Set-CASMailbox](https://technet.microsoft.com/fr-fr/library/bb125264\(v=exchg.150\))

  - [Set-Mailbox](https://technet.microsoft.com/fr-fr/library/bb123981\(v=exchg.150\))

  - [Set-MailboxServer](https://technet.microsoft.com/fr-fr/library/aa998651\(v=exchg.150\))

  - [Search-Mailbox](https://technet.microsoft.com/fr-fr/library/dd298173\(v=exchg.150\))

## Comment savoir si cela a fonctionné ?

Pour vérifier que le nettoyage du dossier Éléments récupérables d’une boîte aux lettres s’est correctement effectué, utilisez la cmdlet [Get-MailboxFolderStatistics](https://technet.microsoft.com/fr-fr/library/aa996762\(v=exchg.150\)) pour contrôler la taille du dossier Éléments récupérables.

Dans cet exemple, nous récupérons la taille du dossier Éléments récupérables et de ses sous-dossiers ainsi qu’un comptage des éléments du dossier et de chacun des sous-dossiers.

```powershell
Get-MailboxFolderStatistics -Identity "Gurinder Singh" -FolderScope RecoverableItems | Format-Table Name,FolderAndSubfolderSize,ItemsInFolderAndSubfolders -Auto
```

