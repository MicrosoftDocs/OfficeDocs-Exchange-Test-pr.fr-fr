---
title: 'Déplacement du chemin d’accès d’une copie de base de données de boîtes aux lettres: Exchange 2013 Help'
TOCTitle: Déplacement du chemin d’accès d’une copie de base de données de boîtes aux lettres
ms:assetid: 324f255c-d95d-4a8a-a134-c8cee5c5b9cb
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dd979782(v=EXCHG.150)
ms:contentKeyID: 50477846
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Déplacement du chemin d’accès d’une copie de base de données de boîtes aux lettres

 

_**Sapplique à :**Exchange Server 2013_

_**Dernière rubrique modifiée :**2014-05-07_

Une fois qu’une base de données de boîtes aux lettres est créée, vous pouvez la placer sur un autre volume, dossier, emplacement ou chemin à l’aide du CAE ou de l’environnement de ligne de commande Exchange Management Shell. Pour obtenir des instructions détaillées sur la procédure de déplacement du chemin d’une base de données pour une base de données de boîtes aux lettres non répliquée, consultez la rubrique [Move a mailbox database path](manage-mailbox-databases-in-exchange-2013-exchange-2013-help.md).

Si la base de données de boîtes aux lettres en cours de déplacement a une ou plusieurs copies, vous devez suivre la procédure de cette rubrique pour déplacer la base de données de boîtes aux lettres. Toutes les copies d’une base de données de boîtes aux lettres doivent être situées dans le même chemin sur chaque serveur qui héberge une copie. Par exemple, si la base de données DB1 est placée sous C:\\mountpoints\\DB1 sur le serveur EX1, les copies de DB1 sur les serveurs EX2, EX3, etc, doivent également se trouver sous C:\\mountpoints\\DB1.

Souhaitez-vous rechercher les autres tâches de gestion relatives aux copies de la base de données de boîtes aux lettres ? Consultez la rubrique [Gestion des copies de base de données de boîtes aux lettres](managing-mailbox-database-copies-exchange-2013-help.md).

## Ce qu’il faut savoir avant de commencer ?

  - Durée d’exécution estimée de cette tâche : 2 minutes sont nécessaires, plus le temps nécessaire au déplacement des données, qui varie selon une multitude de facteurs, tels que la taille de la base de données, la vitesse, la bande passante disponible et le temps de réponse du réseau ainsi que les vitesses de stockage.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultezEntrée « Copies de bases de données de boîtes aux lettres » dans la rubrique [Autorisations de haute disponibilité et de résilience des sites](high-availability-and-site-resilience-permissions-exchange-2013-help.md).

  - Pour exécuter l’opération de déplacement, la base de données doit être démontée de façon temporaire, ce qui la rend inaccessible à tous les utilisateurs. Si la base de données est actuellement démontée, elle n’est pas remontée au terme du processus.

  - Pour exécuter l’opération de déplacement, la réplication de la base de données doit être désactivée pour toutes les copies. La suspension de la réplication n’est pas suffisante ; vous devez la désactiver par le biais de la cmdlet [Remove-MailboxDatabaseCopy](https://technet.microsoft.com/fr-fr/library/dd335119\(v=exchg.150\)) pour supprimer les copies de la base de données.

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

<table>
<thead>
<tr class="header">
<th><img src="images/Bb125224.tip(EXCHG.150).gif" title="Conseil" alt="Conseil" />Conseil :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..</td>
</tr>
</tbody>
</table>


## Utilisation de l’environnement de ligne de commande Exchange Management Shell pour placer une base de données de boîtes aux lettres répliquée sous un nouveau chemin

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Vous ne pouvez pas utiliser le CAE pour placer une base de données de boîtes aux lettres répliquée sous un nouveau chemin.</td>
</tr>
</tbody>
</table>


1.  Notez les paramètres d’attente de relecture et de troncation de toutes les copies de la base de données de boîtes aux lettres en cours de déplacement. Vous pouvez obtenir ces informations par le biais de la cmdlet [Get-MailboxDatabase](https://technet.microsoft.com/fr-fr/library/bb124924\(v=exchg.150\)), comme illustré dans l’exemple suivant.
    
        Get-MailboxDatabase DB1 | Format-List *lag*

2.  Si l’enregistrement circulaire est activé pour la base de données, il doit être désactivé avant de poursuivre. Vous pouvez désactiver l’enregistrement circulaire pour une base de données de boîtes aux lettres à l’aide de la cmdlet [Set-MailboxDatabase](https://technet.microsoft.com/fr-fr/library/bb123971\(v=exchg.150\)), comme illustré dans l’exemple suivant.
    
        Set-MailboxDatabase DB1 -CircularLoggingEnabled $false

3.  Supprimez toutes les copies de la base de données en cours de déplacement. Pour obtenir la procédure détaillée, voir [Supprimer une copie de base de données de boîtes aux lettres](remove-a-mailbox-database-copy-exchange-2013-help.md). Une fois toutes les copies supprimées, conservez la base de données et les fichiers journaux des transactions de chaque serveur duquel la copie de la base de données a été supprimée en les déplaçant. Ces fichiers sont conservés de façon que les copies de la base de données ne nécessitent aucun réamorçage après leur rajout.

4.  Placez la base de données de boîtes aux lettres dans le nouvel emplacement. Pour obtenir la procédure détaillée, consultez la rubrique [Move a mailbox database path](manage-mailbox-databases-in-exchange-2013-exchange-2013-help.md).
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ159813.important(EXCHG.150).gif" title="Important" alt="Important" />Important :</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Pendant l’opération de déplacement, la base de données déplacée doit être démontée. Tant que le déplacement n’est pas terminé, il y a une interruption de service et un blocage système pour tous les utilisateurs dont les boîtes aux lettres sont contenues dans la base de données en cours de déplacement. Une fois l’opération de déplacement terminée, la base de données est montée automatiquement.</td>
    </tr>
    </tbody>
    </table>


5.  Créez la structure de dossiers nécessaire sur chaque serveur de boîtes aux lettres qui contenait déjà une copie passive de la base de données de boîtes aux lettres déplacée. Par exemple, si vous avez placé la base de données sous C:\\mountpoints\\DB1, vous devez créer le même chemin d’accès sur chaque serveur de boîtes aux lettres qui doit héberger une copie de la base de données de boîtes aux lettres.

6.  Une fois la structure de dossiers créée, placez la copie passive de la base de données de boîtes aux lettres et ses flux de journaux dans le nouvel emplacement. Voici les fichiers conservés après l’étape 3. Répétez ce processus pour chaque copie de base de données supprimée à l’étape 3.

7.  Ajoutez toutes les copies de base de données supprimées à l’étape 3. Pour obtenir des instructions détaillées, voir [Ajout d’une copie de base de données de boîtes aux lettres](add-a-mailbox-database-copy-exchange-2013-help.md).

8.  Sur chaque serveur qui contient une copie de la base de données de boîtes aux lettres en cours de déplacement, exécutez les commandes suivantes pour arrêter et redémarrer les services d’indexation du contenu.
    
        Net stop MSExchangeFastSearch
        Net start MSExchangeFastSearch

9.  Vous pouvez éventuellement activer l’enregistrement circulaire à l’aide de la cmdlet [Set-MailboxDatabase](https://technet.microsoft.com/fr-fr/library/bb123971\(v=exchg.150\)), comme illustré dans l’exemple suivant.
    
        Set-MailboxDatabase DB1 -CircularLoggingEnabled $true

10. Reconfigurez toutes les valeurs déjà définies pour le délai d’attente de relecture et le délai d’attente de troncation par le biais de la cmdlet [Set-MailboxDatabaseCopy](https://technet.microsoft.com/fr-fr/library/dd298104\(v=exchg.150\)), comme illustré dans l’exemple suivant.
    
        Set-MailboxDatabaseCopy DB1\MBX2 -ReplayLagTime 00:15:00

11. Comme chaque copie doit être ajoutée, il est conseillé de vérifier l’intégrité et l’état d’une copie avant d’ajouter la copie suivante. Vous pouvez vérifier l’intégrité et l’état en :
    
    1.  examinant le journal des événements signalant des erreurs ou des avertissements concernant la base de données ou sa copie.
    
    2.  utilisant la cmdlet [Get-MailboxDatabaseCopyStatus](https://technet.microsoft.com/fr-fr/library/dd298044\(v=exchg.150\)) pour vérifier l’intégrité et l’état de la réplication continue de la copie de base de données.
    
    3.  utilisant la cmdlet [Test-ReplicationHealth](https://technet.microsoft.com/fr-fr/library/bb691314\(v=exchg.150\)) pour vérifier l’intégrité et l’état du groupe de disponibilité de base de données et de la réplication continue.

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, consultez les rubriques suivantes :

  - [Get-MailboxDatabase](https://technet.microsoft.com/fr-fr/library/bb124924\(v=exchg.150\))

  - [Set-MailboxDatabase](https://technet.microsoft.com/fr-fr/library/bb123971\(v=exchg.150\))

  - [Set-MailboxDatabaseCopy](https://technet.microsoft.com/fr-fr/library/dd298104\(v=exchg.150\))

  - [Get-MailboxDatabaseCopyStatus](https://technet.microsoft.com/fr-fr/library/dd298044\(v=exchg.150\))

  - [Test-ReplicationHealth](https://technet.microsoft.com/fr-fr/library/bb691314\(v=exchg.150\))

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez bien déplacé le chemin d’accès d’une copie de base de données de boîtes aux lettres, procédez de l’une des manières suivantes :

  - Dans le CAE, accédez à **Serveurs** \> **Bases de données**. Sélectionnez la base de données qui a été copiée. Dans le volet Détails, l'état de la copie de la base de données et son index de contenu sont affichés avec la longueur de la file d'attente de copie actuelle. Vérifiez que l’état est Intègre.

  - Dans l’environnement de ligne de commande Exchange Management Shell, exécutez la commande suivante pour vérifier que la base de données de boîtes aux lettres a bien été créée et qu’elle est intègre :
    
        Get-MailboxDatabaseCopyStatus <DatabaseCopyName>
    
    Le statut et l'état de l'index de contenu doivent être sains.

