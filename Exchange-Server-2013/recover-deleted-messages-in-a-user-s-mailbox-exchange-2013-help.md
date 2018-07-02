---
title: 'Récupérer des messages supprimés dans la boîte aux lettres d’un utilisateur: Exchange 2013 Help'
TOCTitle: Récupérer des messages supprimés dans la boîte aux lettres d’un utilisateur
ms:assetid: 9e0e34ce-efc5-454e-8d15-57b4da867f12
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Ff660637(v=EXCHG.150)
ms:contentKeyID: 50555452
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Récupérer des messages supprimés dans la boîte aux lettres d’un utilisateur

 

_**Sapplique à :**Exchange Online, Exchange Server 2013_

_**Dernière rubrique modifiée :**2016-12-09_

(Cette rubrique concerne les administrateurs Exchange.)

Les administrateurs peuvent rechercher et récupérer des messages électroniques supprimés dans la boîte aux lettres d’un utilisateur. Cela inclut les éléments qui sont supprimés définitivement (purgés) par une personne (à l’aide de la fonctionnalité Récupérer les éléments supprimés dans Outlook ou Outlook Web App) ou les éléments supprimés par un processus automatisé, tel que la stratégie de rétention attribuée à des boîtes aux lettres d’utilisateur. Dans ce cas, un utilisateur ne peut pas récupérer les éléments supprimés définitivement. Mais les administrateurs peuvent récupérer les messages supprimés définitivement si la période de rétention des éléments supprimés de l’élément n’a pas expiré.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Outre la recherche et la récupération d’éléments supprimés (transférés dans le dossier des éléments récupérables\purges si la récupération d’élément unique ou la mise en attente pour litige est activée), cette procédure permet de rechercher d’autres éléments résidant dans d’autres dossiers de la boîte aux lettres et d’en supprimer de la boîte aux lettres source (<em>recherche et destruction</em>).</td>
</tr>
</tbody>
</table>


## Ce qu’il faut savoir avant de commencer ?

  - Durée d'exécution estimée : 15 à 30 minutes.

  - Les procédures décrites dans cette rubrique requièrent des autorisations spécifiques. Consultez chaque procédure pour savoir quelles autorisations sont nécessaires.

  - La récupération d’élément unique doit être activée pour une boîte aux lettres avant la suppression de l’élément que vous souhaitez récupérer. Dans Exchange Online, la récupération d’élément unique est activée par défaut lors de la création d’une boîte aux lettres. Dans Exchange 2013, la récupération d’élément unique est désactivée lors de la création d’une boîte aux lettres. Pour plus d'informations, consultez la rubrique [Activation de la récupération d’élément unique pour une boîte aux lettres](enable-or-disable-single-item-recovery-for-a-mailbox-exchange-2013-help.md).

  - Pour rechercher et récupérer des éléments, vous devez disposer des informations suivantes :
    
      - **Boîte aux lettres source**   Il s’agit de la boîte aux lettres qui fait l’objet de la recherche.
    
      - **Boîte aux lettres cible**   Il s’agit de la boîte aux lettres de découverte qui contiendra les messages récupérés. Le programme d’installation d’Exchange crée une boîte aux lettres de découverte par défaut. Dans Exchange Online, une boîte aux lettres de découverte est également créée par défaut. Si nécessaire, vous pouvez en créer d’autres. Pour plus d’informations, voir [Créer une boîte aux lettres de découverte](create-a-discovery-mailbox-exchange-2013-help.md).
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>Avec la cmdlet <strong>Search-Mailbox</strong>, il est aussi possible de spécifier une boîte aux lettres cible qui n’est pas une boîte de découverte. Il est en revanche impossible que la même boîte aux lettres soit à la fois source et cible.</td>
        </tr>
        </tbody>
        </table>
    
      - **Critères de recherche**   Nom de l’expéditeur, du destinataire, ou mots-clés (termes ou expressions) dans le message.

  - Cette rubrique porte sur l’utilisation de PowerShell pour récupérer les éléments supprimés dans la boîte aux lettres d’un utilisateur. Vous pouvez également utiliser l’outil eDiscovery inaltérable basé sur l’interface utilisateur pour rechercher et exporter des éléments supprimés dans un fichier PST. L’utilisateur utilise ce fichier PST pour restaurer les messages supprimés dans sa boîte aux lettres. Pour obtenir des instructions détaillées, consultez la page relative à la [récupération d’éléments supprimés dans la boîte aux lettres d’un utilisateur](https://go.microsoft.com/fwlink/p/?linkid=722928).

## Étape 1 (facultatif) : Connexion à Exchange Online à l’aide de Remote PowerShell

Vous devez uniquement effectuer cette étape si vous possédez une organisation Exchange Online ou Office 365. Si vous possédez une organisation Exchange 2013, passez à l’étape suivante et exécutez la commande dans Environnement de ligne de commande Exchange Management Shell.

1.  Sur votre ordinateur local, ouvrez Windows PowerShell et exécutez la commande suivante.
    
        $UserCredential = Get-Credential
    
    Dans la boîte de dialogue **Demande d’informations d’identification Windows PowerShell**, saisissez le nom d’utilisateur et le mot de passe d’un compte d’administrateur global Office 365, puis cliquez sur **OK**.

2.  Exécutez la commande suivante.
    
        $Session = New-PSSession -ConfigurationName Microsoft.Exchange -ConnectionUri https://outlook.office365.com/powershell-liveid/ -Credential $UserCredential -Authentication Basic -AllowRedirection

3.  Exécutez la commande suivante.
    
        Import-PSSession $Session

4.  Pour vérifier que vous êtes connecté à votre organisation Exchange Online, exécutez la commande suivante pour obtenir la liste de toutes les boîtes aux lettres de votre organisation.
    
        Get-Mailbox

Pour plus d’informations ou si vous rencontrez des problèmes pour vous connecter à votre organisation Exchange Online, consultez la rubrique [Connexion à Exchange Online à l’aide de Remote PowerShell](https://go.microsoft.com/fwlink/p/?linkid=517283).

## Étape 2 : Rechercher et récupérer les éléments manquants

Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez entrée « In-Place eDiscovery » dans la rubrique [Stratégie de messagerie et autorisations de conformité](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Vous pouvez utiliser la découverte électronique inaltérable dans le Centre d’administration Exchange (CAE) pour rechercher des éléments manquants. Cependant, lorsque vous utilisez le Centre d’administration Exchange (EAC), vous ne pouvez pas restreindre la recherche au dossier Éléments récupérables. Les messages correspondant à vos paramètres de recherche seront renvoyés même s’ils n’ont pas été supprimés. Après les avoir récupérés dans la boîte aux lettres de découverte spécifiée, il est peut-être nécessaire de revoir les résultats de la recherche et de supprimer des messages inutiles avant de récupérer les messages restants dans la boîte aux lettres de l’utilisateur ou de les exporter dans un fichier .pst.<br />
Pour plus d’informations sur l’utilisation du Centre d’administration Exchange (EAC) pour effectuer une recherche de découverte électronique sur place (In-Place eDiscovery), voir <a href="create-an-in-place-ediscovery-search-exchange-2013-help.md">Créer une recherche de découverte électronique inaltérable</a>.</td>
</tr>
</tbody>
</table>


La première étape du processus de récupération consiste à rechercher des messages dans la boîte aux lettres source. Pour effectuer une recherche dans la boîte aux lettres d’un utilisateur et copier les messages dans une boîte aux lettres de découverte, utilisez l’une des deux méthodes ci-après.

Dans l’exemple ci-après, la recherche porte sur les messages dans la boîte aux lettres d’April Stewart qui répondent aux critères suivants :

  - Expéditeur : Ken Kwok

  - Mot clé : Seattle

<!-- end list -->

    Search-Mailbox "April Stewart" -SearchQuery "from:'Ken Kwok' AND seattle" -TargetMailbox "Discovery Search Mailbox" -TargetFolder "April Stewart Recovery" -LogLevel Full

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Associé à la cmdlet <strong>Search-Mailbox</strong>, le paramètre <em>SearchQuery</em> permet de cibler l’étendue de la recherche en spécifiant une requête formatée à l’aide du langage KQL (Keyword Query Language). Vous pouvez également utiliser le commutateur <em>SearchDumpsterOnly</em> pour ne rechercher que des éléments dans le dossier Éléments récupérables.</td>
</tr>
</tbody>
</table>


Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Search-Mailbox](https://technet.microsoft.com/fr-fr/library/dd298173\(v=exchg.150\)).

**Comment savoir si cela a fonctionné ?**

Pour vérifier que la recherche des messages à récupérer s’est correctement effectuée, connectez-vous à la boîte aux lettres que vous avez sélectionnée comme boîte aux lettres cible, puis examinez les résultats de la recherche.

## Étape 3 : Restaurer les éléments récupérés

Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez entrée « In-Place eDiscovery » dans la rubrique [Stratégie de messagerie et autorisations de conformité](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Vous ne pouvez pas utiliser le CAE pour restaurer des éléments récupérés.</td>
</tr>
</tbody>
</table>


Une fois que les messages ont été récupérés dans une boîte aux lettres de découverte, restaurez-les dans la boîte aux lettres de l’utilisateur via la cmdlet **Search-Mailbox**. Dans Exchange 2013, vous pouvez également utiliser les cmdlets **New-MailboxExportRequest** et **New-MailboxImportRequest** pour exporter ou importer les messages à partir d’un fichier .pst.

## Utiliser l’environnement de ligne de commande pour restaurer les messages

Dans l’exemple suivant, les messages sont restaurés dans la boîte aux lettres d’April Stewart et supprimés de la boîte aux lettres de détection.

    Search-Mailbox "Discovery Search Mailbox" -SearchQuery "from:'Ken Kwok' AND seattle" -TargetMailbox "April Stewart" -TargetFolder "Recovered Messages" -LogLevel Full -DeleteContent

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Search-Mailbox](https://technet.microsoft.com/fr-fr/library/dd298173\(v=exchg.150\)).

**Comment savoir si cela a fonctionné ?**

Pour vérifier que les messages ont été correctement récupérés dans la boîte aux lettres de l’utilisateur, demandez à l’utilisateur d’examiner les messages du dossier cible spécifié par vos soins dans la commande ci-dessus.

## (Exchange 2013) Utiliser l’environnement de ligne de commande Exchange Management Shell pour exporter et importer des messages à partir d’un fichier .pst

Dans Exchange 2013, vous pouvez exporter le contenu d’une boîte aux lettres vers un fichier .pst et importer le contenu d’un fichier .pst vers une boîte aux lettres. Pour plus d’informations sur l’importation et l’exportation de données de boîtes aux lettres, consultez la rubrique [Demandes d’exportation et d’importation de boîtes aux lettres](mailbox-import-and-export-requests-exchange-2013-help.md). Vous ne pouvez pas effectuer cette tâche dans Exchange Online.

Dans l’exemple ci-après, les paramètres suivants sont utilisés pour exporter des messages à partir du dossier April Stewart Recovery de la boîte aux lettres de découverte vers un fichier .pst :

  - **Boîte aux lettres**   Discovery Search Mailbox

  - **Dossier source**   April Stewart Recovery

  - **Filtrage du contenu**   Prévisions de déplacements pour avril

  - **Chemin d’accès au fichier PST**   \\\\MYSERVER\\HelpDeskPst\\AprilStewartRecovery.pst

<!-- end list -->

    New-MailboxExportRequest -Mailbox "Discovery Search Mailbox" -SourceRootFolder "April Stewart Recovery" -ContentFilter {Subject -eq "April travel plans"} -FilePath \\MYSERVER\HelpDeskPst\AprilStewartRecovery.pst

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [New-MailboxExportRequest](https://technet.microsoft.com/fr-fr/library/ff607299\(v=exchg.150\)).

Dans l’exemple ci-après, les paramètres suivants sont utilisés pour importer des messages, à partir d’un fichier .pst, dans le dossier Recovered By Helpdesk de la boîte aux lettres d’April Stewart :

  - **Boîte aux lettres**   April Stewart

  - **Dossier cible**   Recovered By Helpdesk

  - **Chemin d’accès au fichier PST**   \\\\MYSERVER\\HelpDeskPst\\AprilStewartRecovery.pst

<!-- end list -->

    New-MailboxImportRequest -Mailbox "April Stewart" -TargetRootFolder "Recovered By Helpdesk" -FilePath \\MYSERVER\HelpDeskPst\AprilStewartRecovery.pst 

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [New-MailboxImportRequest](https://technet.microsoft.com/fr-fr/library/ff607310\(v=exchg.150\)).

**Comment savoir si cela a fonctionné ?**

Pour vérifier que les messages ont été correctement exportés dans un fichier .pst, utilisez Outlook pour ouvrir le fichier .pst et inspectez son contenu. Pour vérifier que les messages ont été correctement importés à partir du fichier .pst, demandez à l’utilisateur d’inspecter le contenu du dossier cible spécifié par vos soins dans la commande ci-dessus.

## Plus d’informations

  - La possibilité de récupérer des éléments supprimés est activée par la *récupération d’élément unique*, qui permet à un administrateur de récupérer un message ayant été supprimé définitivement par un utilisateur ou par une stratégie de rétention tant que la période de rétention de l’élément supprimé n’a pas expiré pour cet élément. Pour en savoir plus sur la fonctionnalité de récupération d’élément unique, consultez la rubrique [Dossier Éléments récupérables](recoverable-items-folder-exchange-2013-help.md).

  - Une boîte aux lettres Exchange Online est configurée pour conserver les éléments supprimés pendant 14 jours, par défaut. Vous pouvez augmenter la valeur de ce paramètre jusqu’à 30 jours au maximum. Dans Exchange 2013, une base de données de boîtes aux lettres est configurée pour conserver les éléments supprimés pendant 14 jours, par défaut. Vous pouvez configurer les paramètres de rétention des éléments supprimés pour une boîte aux lettres ou une base de données de boîtes aux lettres. Pour plus d’informations, consultez les rubriques suivantes :
    
      - [Modifier la durée de conservation des éléments supprimés définitivement pour une boîte aux lettres Exchange Online](https://technet.microsoft.com/fr-fr/library/dn163584\(v=exchg.150\))
    
      - [Configurer la rétention des éléments supprimés et les quotas d’éléments récupérables](configure-deleted-item-retention-and-recoverable-items-quotas-exchange-2013-help.md)

  - Comme expliqué précédemment, vous pouvez également utiliser l’outil eDiscovery inaltérable pour rechercher et exporter des éléments supprimés dans un fichier PST. L’utilisateur utilise ce fichier PST pour restaurer les messages supprimés dans sa boîte aux lettres. Pour obtenir des instructions détaillées, consultez la page relative à la [récupération d’éléments supprimés dans la boîte aux lettres d’un utilisateur](https://go.microsoft.com/fwlink/p/?linkid=722928).

  - Les utilisateurs peuvent récupérer un élément supprimé s’il n’a pas été supprimé définitivement et si la période de rétention de l’élément supprimé de cet élément n’a pas expiré. Si les utilisateurs souhaitent récupérer des éléments supprimés du dossier Éléments récupérables, dirigez-les vers les rubriques suivantes :
    
      - [Restaurer les éléments supprimés dans Outlook 2010](https://go.microsoft.com/fwlink/p/?linkid=524923)
    
      - [Restaurer les éléments supprimés dans Outlook 2013](https://go.microsoft.com/fwlink/p/?linkid=624829)
    
      - [Récupérer des éléments ou des messages supprimés dans Outlook Web App](https://go.microsoft.com/fwlink/p/?linkid=524924)

  - Cette rubrique explique comment utiliser la cmdlet **Search-Mailbox** pour rechercher et récupérer des éléments manquants. Cette cmdlet ne permet d’explorer qu’une boîte aux lettres à la fois. Si vous souhaitez effectuer une recherche dans plusieurs boîtes aux lettres simultanément, vous pouvez utiliser [Découverte électronique locale](in-place-ediscovery-exchange-2013-help.md) dans le Centre d’administration Exchange (CAE) ou la cmdlet [New-MailboxSearch](https://technet.microsoft.com/fr-fr/library/dd298064\(v=exchg.150\)) dans Windows PowerShell.

  - Outre l’utilisation de cette procédure pour rechercher et récupérer des éléments supprimés, vous pouvez également utiliser une procédure similaire pour rechercher des éléments dans des boîtes aux lettres d’utilisateur, puis supprimer ces éléments de la boîte aux lettres source. Pour plus d’informations, consultez la rubrique [Recherche et suppression de messages - Aide de l’administrateur](search-for-and-delete-messages-admin-help-exchange-2013-help.md).

