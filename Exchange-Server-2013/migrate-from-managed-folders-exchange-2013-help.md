---
title: 'Migration à partir de dossiers gérés: Exchange 2013 Help'
TOCTitle: Migration à partir de dossiers gérés
ms:assetid: 6796a79d-501e-4216-9370-77965bc5835d
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dd298032(v=EXCHG.150)
ms:contentKeyID: 52062989
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Migration à partir de dossiers gérés

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2015-04-07_

Dans Microsoft Exchange Server 2013, la gestion des enregistrements de messagerie (MRM) s’effectue à l’aide de balises et de stratégies de rétention. Une stratégie de rétention est un groupe de balises de rétention applicables à une boîte aux lettres. Pour plus d’informations, consultez la rubrique [Balises et stratégies de rétention](https://docs.microsoft.com/fr-fr/exchange/security-and-compliance/messaging-records-management/retention-tags-and-policies). Les dossiers gérés, technologie de la fonctionnalité MRM introduite dans Exchange Server 2007, ne sont pas pris en charge.

Une boîte aux lettres à laquelle est appliquée une stratégie de boîte aux lettres de dossier géré peut être migrée pour utiliser une stratégie de rétention. Pour ce faire, vous devez créer des balises de rétention équivalentes aux dossiers gérés associés à la stratégie de boîte aux lettres de dossier géré de l'utilisateur.

> [!IMPORTANT]
> Avant de migrer des dossiers gérés vers des stratégies de rétention dans votre environnement de production, nous vous recommandons d'essayer le processus dans un environnement de test.


> [!TIP]
> Vous pouvez mettre des boîtes aux lettres en blocage de rétention afin d’arrêter le traitement des stratégies de rétention ou des stratégies de boîte aux lettres de dossier géré. La mise de boîtes aux lettres en blocage de rétention peut être utile dans des scénarios de migration pour éviter de supprimer des messages ou de déplacer des messages vers une archive tant que les paramètres de la nouvelle stratégie n’ont pas été vérifiés sur des boîtes aux lettres de test ou sur un petit nombre de boîtes aux lettres de production. Pour plus d’informations, consultez la rubrique <a href="https://docs.microsoft.com/fr-fr/exchange/security-and-compliance/messaging-records-management/mailbox-retention-hold">Placer une boîte aux lettres en blocage de rétention</a>.


Pour d’autres tâches de gestion associées à la fonctionnalité MRM, voir [Procédures de gestion des enregistrements de messagerie](messaging-records-management-procedures-exchange-2013-help.md).

## Comparaison entre les balises de rétention et les dossiers gérés

Contrairement aux dossiers gérés, qui exigent que les utilisateurs déplacent des éléments vers un dossier géré en fonction de paramètres de rétention, les balises de rétention peuvent être appliquées à un dossier ou à un élément dans la boîte aux lettres. Ce processus a un impact minimal sur les méthodes d’organisation du courrier électronique et du workflow de l’utilisateur. Lorsque des balises de rétention s'appliquent à un dossier, tous les éléments de ce dernier héritent des paramètres de rétention. Les utilisateurs peuvent spécifier des paramètres de rétention en appliquant différentes balises de rétention aux éléments de ce dossier.

Les dossiers gérés prennent en charge différents paramètres de contenu géré pour un dossier, chacun avec une classe de message différente (par exemple, élément de messagerie ou élément de calendrier). Les balises de rétention ne requièrent pas d'objet paramètres de contenu géré distinct, car les paramètres de rétention sont spécifiés dans les propriétés des balises. Il n’est pas possible de créer des balises de rétention pour des classes de messages particulières, à l’exception d’une balise de stratégie par défaut (DPT) pour les messages vocaux. Les balises de rétention ne permettent pas non plus d’utiliser la journalisation (effectuée par l’Assistant Dossier géré).

> [!NOTE]
> Les règles de journalisation utilisées pour envoyer des copies de messages avec un état de journal à une boîte aux lettres de journalisation sont appliquées dans le pipeline de transport par l’Agent de journalisation, et sont indépendantes de la fonctionnalité MRM. Pour plus d’informations, consultez la rubrique <a href="journaling-exchange-2013-help.md">Journalisation</a>.


Le tableau suivant compare la fonctionnalité MRM disponible lors de l'utilisation de balises de rétention ou de dossiers gérés.

### Balises de rétention et dossiers gérés

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Fonctionnalité</th>
<th>Balises de rétention</th>
<th>Dossiers gérés</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Spécifier des paramètres de rétention pour des dossiers par défaut (par exemple, la boîte de réception)</p></td>
<td><p>Utiliser les balises de stratégie de rétention (RPT)</p></td>
<td><p>Utiliser les dossiers gérés par défaut</p></td>
</tr>
<tr class="even">
<td><p>Spécifier des paramètres de rétention pour une boîte aux lettres entière</p></td>
<td><p>Utiliser une balise de stratégie par défaut (DPT)</p></td>
<td><p>Utiliser des dossiers gérés par défaut</p></td>
</tr>
<tr class="odd">
<td><p>Utiliser des paramètres de rétention pour des dossiers personnalisés</p></td>
<td><p>Utiliser des balises personnelles</p></td>
<td><p>Utiliser des dossiers personnalisés gérés</p></td>
</tr>
<tr class="even">
<td><p>Requérir des paramètres de contenu géré</p></td>
<td><p>Non (les paramètres de rétention sont inclus dans une balise de rétention)</p></td>
<td><p>Oui</p></td>
</tr>
<tr class="odd">
<td><p>Utiliser des paramètres de rétention pour différentes classes de messages (par exemple, messages électroniques, messages vocaux ou éléments de calendrier)</p></td>
<td><p>Non</p></td>
<td><p>Oui</p></td>
</tr>
<tr class="even">
<td><p>Prendre en charge l'action de déplacement vers une archive, qui déplace des éléments vers la boîte aux lettres d'archivage de l'utilisateur</p></td>
<td><p>Oui</p></td>
<td><p>Non</p></td>
</tr>
<tr class="odd">
<td><p>Prendre en charge l'action de déplacement vers un dossier géré</p></td>
<td><p>Non</p></td>
<td><p>Oui</p></td>
</tr>
<tr class="even">
<td><p>Autoriser la journalisation à l'aide de l'Assistant Dossier géré</p></td>
<td><p>Non</p></td>
<td><p>Oui</p></td>
</tr>
<tr class="odd">
<td><p>Stratégie appliquée à l'utilisateur</p></td>
<td><p>Stratégie de rétention</p></td>
<td><p>Stratégie de boîte aux lettres de dossier géré</p></td>
</tr>
<tr class="even">
<td><p>Nombre maximal de stratégies applicables à un utilisateur de boîte aux lettres</p></td>
<td><p>1</p></td>
<td><p>1</p></td>
</tr>
<tr class="odd">
<td><p>Traité par l'Assistant Dossier géré</p></td>
<td><p>Oui</p></td>
<td><p>Oui</p></td>
</tr>
<tr class="even">
<td><p>Prise en charge des clients</p></td>
<td><p>Microsoft Outlook 2010 et Office Outlook Web App</p></td>
<td><p>Outlook 2010, Office Outlook 2007 et Outlook Web App</p></td>
</tr>
</tbody>
</table>


## Ce qu’il faut savoir avant de commencer

  - Durée d’exécution estimée : 20 minutes.

  - Les procédures décrites dans cette rubrique requièrent des autorisations spécifiques. Consultez chaque procédure pour savoir quelles autorisations sont nécessaires.

  - Vous ne pouvez pas utiliser le Centre d’administration Exchange (CAE) pour créer des balises de rétention basées sur des stratégies de rétention.

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), et [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

## Migration d’utilisateurs de boîtes aux lettres à partir de dossiers gérés

Les étapes suivantes permettent de migrer des utilisateurs à partir de cette stratégie de boîte aux lettres de dossier géré vers une stratégie de rétention. Chaque étape est décrite ci-après dans cette rubrique :

1.  Recueillez des informations sur les stratégies de boîte aux lettres de dossier géré appliquées à toutes les boîtes aux lettres Exchange 2010 et Exchange 2007, sur les dossiers gérés dans chaque stratégie et sur les paramètres de contenu géré pour chaque dossier géré. Pour obtenir ces informations, vous pouvez utiliser la console de gestion Exchange ou l’environnement de ligne de commande sur un serveur Exchange 2010 ou Exchange 2007.

2.  Créez des balises de rétention pour la migration.

3.  Créez une stratégie de rétention et associez les balises de rétention nouvellement créées à cette stratégie.

4.  Supprimez la stratégie de boîte aux lettres de dossier géré, puis appliquez la stratégie de rétention aux boîtes aux lettres utilisateur.
    
    > [!IMPORTANT]
    > Une fois la stratégie de rétention appliquée à un utilisateur et l'Assistant Dossier géré lancé, les dossiers gérés de la boîte aux lettres utilisateur ne sont plus gérés.


Pour les procédures suivantes, les boîtes aux lettres Contoso se voient appliquer une stratégie de boîte aux lettres de dossier géré contenant les dossiers gérés suivants.

### Dossiers gérés pour Contoso

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>Dossier géré</th>
<th>Paramètres de contenu géré</th>
<th>Rétention activée</th>
<th>Âge de rétention</th>
<th>Action de rétention</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Corp-DeletedItems</p></td>
<td><p>CS-Corp-DeletedItems</p></td>
<td><p>Oui</p></td>
<td><p>30 jours</p></td>
<td><p>Supprimer et autoriser la récupération</p></td>
</tr>
<tr class="even">
<td><p>Corp-SentItems</p></td>
<td><p>CS-Corp-SentItems</p></td>
<td><p>Oui</p></td>
<td><p>1 825 jours</p></td>
<td><p>Déplacer vers les éléments supprimés</p></td>
</tr>
<tr class="odd">
<td><p>Corp-JunkMail</p></td>
<td><p>CS-Corp-JunkMail</p></td>
<td><p>Oui</p></td>
<td><p>30 jours</p></td>
<td><p>Supprimer définitivement</p></td>
</tr>
<tr class="even">
<td><p>Corp-EntireMailbox</p></td>
<td><p>CS-Corp-EntireMailbox</p></td>
<td><p>Oui</p></td>
<td><p>365 jours</p></td>
<td><p>Déplacer vers les éléments supprimés</p></td>
</tr>
<tr class="odd">
<td><p>30 jours</p></td>
<td><p>CS-30Days</p></td>
<td><p>Oui</p></td>
<td><p>30 jours</p></td>
<td><p>Déplacer vers les éléments supprimés</p></td>
</tr>
<tr class="even">
<td><p>5 ans</p></td>
<td><p>CS-5Years</p></td>
<td><p>Oui</p></td>
<td><p>1 825 jours</p></td>
<td><p>Déplacer vers les éléments supprimés</p></td>
</tr>
<tr class="odd">
<td><p>Ne jamais expirer</p></td>
<td><p>CS-NeverExpire</p></td>
<td><p>Non</p></td>
<td><p>365 jours</p></td>
<td><p>Non applicable</p></td>
</tr>
</tbody>
</table>


## Comment procéder ?

## Étape 1 : Création de balises de rétention pour la migration

Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l’entrée « Gestion des enregistrements de messagerie » dans la rubrique [Stratégie de messagerie et autorisations de conformité](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

Pour cette étape, vous pouvez utiliser deux méthodes :

  - **Créer des balises de rétention en fonction des dossiers gérés et des paramètres de contenu géré correspondants**   Avec cette méthode, vous utilisez la cmdlet **New-RetentionPolicyTag** avec le paramètre *ManagedFolderToUpgrade*. Lorsque vous spécifiez ce paramètre, la balise de rétention correspondante s'applique automatiquement au dossier géré.
    
    > [!IMPORTANT]
    > Si le dossier géré que vous souhaitez déplacer dispose de plusieurs paramètres de contenu géré pour différentes classes de messages, une seule balise de rétention est créée, et l’âge de rétention le plus long par rapport à tous les paramètres de contenu géré est utilisé comme âge de rétention pour la balise déplacée, quelle que soit la classe de message des paramètres de contenu géré.
    > Par exemple, examinez les paramètres de contenu géré suivants pour le dossier géré Corp-DeletedItems.


  - **Créer des balises de rétention en spécifiant manuellement des paramètres de rétention**   Avec cette méthode, vous utilisez la cmdlet **New-RetentionPolicyTag** sans le paramètre *ManagedFolderToUpgrade*. Si vous ne spécifiez pas ce paramètre, toute balise de stratégie de rétention ajoutée à la stratégie est appliquée aux dossiers par défaut, et la balise de stratégie par défaut est appliquée à la boîte aux lettres entière. Toutefois, toute balise personnelle ajoutée à la stratégie n'est pas automatiquement appliquée aux dossiers gérés.

> [!NOTE]
> Si vous êtes dans un environnement hybride comportant des serveurs Exchange 2013 et Exchange 2010, vous pouvez utiliser l’Assistant <strong>Transférer un dossier géré</strong> de la console de gestion Exchange sur un serveur Exchange 2010 pour déplacer un dossier géré et le paramètre de contenu géré correspondant vers des balises de rétention.


**Créer des balises de rétention en fonction des dossiers gérés**

Cet exemple montre comment créer des balises de rétention en fonction des paramètres de contenu géré correspondants affichés dans la stratégie de boîte aux lettres de dossier géré de Contoso.

```powershell
New-RetentionPolicyTag Corp-DeletedItems -ManagedFolderToUpgrade Corp-DeletedItems
New-RetentionPolicyTag Corp-SentItems -ManagedFolderToUpgrade Corp-SentItems
New-RetentionPolicyTag Corp-JunkMail -ManagedFolderToUpgrade Corp-JunkMail
New-RetentionPolicyTag Corp-EntireMailbox -ManagedFolderToUpgrade Corp-EntireMailbox
New-RetentionPolicyTag 30Days -ManagedFolderToUpgrade 30Days
New-RetentionPolicyTag 5Years -ManagedFolderToUpgrade 5Years
New-RetentionPolicyTag NeverExpire -ManagedFolderToUpgrade NeverExpire
```

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, consultez la rubrique [New-RetentionPolicyTag](https://technet.microsoft.com/fr-fr/library/dd335226\(v=exchg.150\)).

**Créer des balises de rétention manuellement**

> [!NOTE]
> Vous pouvez également utiliser le CAE pour créer des balises de rétention manuellement (non basées sur les paramètres définis dans les dossiers gérés). Pour plus d’informations, consultez la rubrique <a href="https://docs.microsoft.com/fr-fr/exchange/security-and-compliance/messaging-records-management/create-a-retention-policy">Créer une stratégie de rétention</a>.


Cet exemple montre comment créer des balises de rétention en fonction des dossiers gérés et des paramètres de contenu géré correspondants affichés dans la stratégie de boîte aux lettres de dossier géré de Contoso. Les paramètres de rétention sont spécifiés manuellement, sans l'aide du paramètre *ManagedFolderToUpgrade*.

```powershell
New-RetentionPolicyTag Corp-DeletedItems -Type DeletedItems -RetentionEnabled $true -AgeLimitForRetention 30 -RetentionAction DeleteAndAllowRecovery
New-RetentionPolicyTag Corp-SentItems -Type SentItems -RetentionEnabled $true -AgeLimitforRetention 1825 -RetentionAction MoveToDeletedItems
New-RetentionPolicyTag Corp-JunkMail -Type JunkMail -RetentionEnabled $true -AgeLimitforRetention 30 -RetentionAction PermanentlyDelete
New-RetentionPolicyTag Corp-EntireMailbox -Type All -RetentionEnabled $true -AgeLimitForRetention 365 -RetentionAction MoveToDeletedItems
New-RetentionPolicyTag 30Days -Type Personal -RetentionEnabled $true -AgeLimitForRetention 30 -RetentionAction MoveToDeletedItems
New-RetentionPolicyTag 5Years -Type Personal -RetentionEnabled $true -AgeLimitForRetention 1825 -RetentionAction MoveToDeletedItems
New-RetentionPolicyTag NeverExpire -Type Personal -RetentionEnabled $false
```

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, consultez la rubrique [New-RetentionPolicyTag](https://technet.microsoft.com/fr-fr/library/dd335226\(v=exchg.150\)).

## Étape 2 : Création d'une stratégie de rétention

Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez entrée « Gestion des enregistrements de messagerie » dans la rubrique [Stratégie de messagerie et autorisations de conformité](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

> [!NOTE]
> Vous pouvez également utiliser le CAE pour créer une stratégie de rétention et ajouter des balises de rétention à cette dernière. Pour plus d’informations, consultez la rubrique <a href="https://docs.microsoft.com/fr-fr/exchange/security-and-compliance/messaging-records-management/create-a-retention-policy">Créer une stratégie de rétention</a>.


Cet exemple montre comment créer la stratégie de rétention RP-Corp et associer les balises de rétention nouvellement créées à cette stratégie.

```powershell
New-RetentionPolicy RP-Corp -RetentionPolicyTagLinks Corp-DeletedItems,Corp-SentItems,Corp-JunkMail,Corp-EntireMailbox,30Days,NeverExpire
```

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, consultez la rubrique [New-RetentionPolicy](https://technet.microsoft.com/fr-fr/library/dd297970\(v=exchg.150\)).

## Étape 3 : Suppression de la stratégie de boîte aux lettres de dossier géré des boîtes aux lettres utilisateur

Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Application des stratégies de rétention » dans la rubrique [Stratégie de messagerie et autorisations de conformité](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

Cet exemple supprime la stratégie de boîte aux lettres de dossier géré et tous les dossiers gérés de la boîte aux lettres de Ken Kwok. Les dossiers gérés contenant des messages ne sont pas supprimés.

```powershell
Set-Mailbox -Identity Kwok -RemoveManagedFolderAndPolicy RP-Corp
```

## Étape 4 : Application de la stratégie de rétention aux boîtes aux lettres utilisateur

Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Application des stratégies de rétention » dans la rubrique [Stratégie de messagerie et autorisations de conformité](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

> [!NOTE]
> Vous pouvez également utiliser le CAE pour appliquer une stratégie de rétention à des utilisateurs. Pour plus d’informations, consultez la rubrique <a href="https://docs.microsoft.com/fr-fr/exchange/security-and-compliance/messaging-records-management/apply-retention-policy">Appliquer une stratégie de rétention aux boîtes aux lettres</a>.


Cet exemple montre comment appliquer la stratégie de rétention nouvellement créée RP-Corp à l'utilisateur de boîte aux lettres Ken Kwok.

```powershell
Set-Mailbox -Identity Kwok -RetentionPolicy RP-Corp
```

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, consultez la rubrique [Set-Mailbox](https://technet.microsoft.com/fr-fr/library/bb123981\(v=exchg.150\)).

## Comment savoir si cette tâche a fonctionné ?

Pour vérifier la réussite de la migration des dossiers gérés vers les stratégies de rétention, procédez comme suit :

  - Générez un rapport portant sur toutes les boîtes aux lettres utilisateur et sur les stratégies de rétention qui leur sont appliquées.
    
    Cette commande récupère la stratégie de rétention appliquée à toutes les boîtes aux lettres au sein d’une organisation, ainsi que leur état de blocage de rétention.
    
    ```powershell
    Get-Mailbox -ResultSize unlimited -Filter {Name -NotLike "DiscoverySearch*�?} | Format-Table Name,RetentionPolicy,RetentionHoldEnabled -Auto
    ```

  - Après que l’Assistant Dossier géré a traité la boîte aux lettres avec une stratégie de rétention, utilisez la cmdlet [Get-RetentionPolicyTag](https://technet.microsoft.com/fr-fr/library/dd298009\(v=exchg.150\)) pour extraire les balises de rétention configurées dans la boîte aux lettres utilisateur.
    
    Cette commande extrait les balises de rétention réellement appliquées à la boîte aux lettres d’April Stewart.
    
    ```powershell
    Get-RetentionPolicyTag -Mailbox astewart
    ```

