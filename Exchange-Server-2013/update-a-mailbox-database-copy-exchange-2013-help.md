---
title: "Mise à jour d'une copie de base de données de boîtes aux lettres: Exchange 2013 Help"
TOCTitle: Mise à jour d'une copie de base de données de boîtes aux lettres
ms:assetid: bead3cc5-7d50-446f-95b7-e432bcb7968e
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dd351100(v=EXCHG.150)
ms:contentKeyID: 50479095
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Mise à jour d'une copie de base de données de boîtes aux lettres

 

_**Sapplique à :**Exchange Server 2013_

_**Dernière rubrique modifiée :**2012-11-02_

La mise à jour, également appelée *amorçage*, est un processus au cours duquel une copie de base de données de boîtes aux lettres est ajoutée à un autre serveur de boîtes aux lettres dans un groupe de disponibilité de base de données. La copie ajoutée devient la base de données de référence pour la copie passive dans laquelle les fichiers journaux copiés à partir de la copie active sont relus. L'amorçage est nécessaire dans les cas suivants :

  - lorsqu'une nouvelle copie passive d'une base de données est créée. L’amorçage peut être différé pour une nouvelle copie de la base de données de boîtes aux lettres, mais chaque copie passive de la base de données doit être amorcée pour fonctionner comme copie redondante de la base de données.

  - après un basculement au cours duquel des données sont perdues car la copie passive de la base de données est différente et irrécupérable.

  - Lorsque le système détecte un fichier journal endommagé qui ne peut pas être relu dans la copie passive de la base de données.

  - après une défragmentation hors connexion d'une copie de la base de données.

  - après la réinitialisation sur 1 d'une séquence de génération de journaux pour la base de données.

Vous pouvez utiliser les méthodes suivantes pour effectuer un amorçage :

  - **Amorçage automatique**   Un amorçage automatique produit une copie passive de la base de données active sur le serveur de boîtes aux lettres cible. L’amorçage automatique se produit lors de la création d’une base de données.

  - **Amorçage à l’aide de la cmdlet Update-MailboxDatabaseCopy**   La cmdlet [Update-MailboxDatabaseCopy](https://technet.microsoft.com/fr-fr/library/dd335201\(v=exchg.150\)) de l’environnement de ligne de commande Management Shell vous permet d’amorcer une copie de base de données à tout moment.

  - **Amorçage à l’aide de l’Assistant Mettre à jour la copie de base de données**   L’Assistant Mettre à jour la copie de base de données du Centre d’administration Exchange (EAC) vous permet d’amorcer une copie de base de données à tout moment.

  - **Copie manuelle de la base de données en mode hors connexion**   Vous pouvez démonter la copie active de la base de données et copier le fichier de base de données au même emplacement sur un autre serveur de boîtes aux lettres appartenant au même groupe de disponibilité de base de données. Si vous utilisez cette méthode, le service est interrompu, car le processus requiert le démontage de la base de données.

La mise à jour d’une copie de base de données peut prendre du temps, notamment si la base de données à copier est volumineuse ou si la latence du réseau est élevée ou que le débit du réseau est faible. Une fois que le processus d’amorçage a démarré, ne fermez pas le Centre d’administration Exchange (EAC) ou l’environnement de ligne de commande Exchange Management Shell avant la fin de l’opération. Si vous le faites, l'opération d'amorçage sera interrompue.

Vous pouvez amorcer une copie de base de données en utilisant la copie active ou une copie passive à jour comme source de l'amorçage. Lorsque vous effectuez l'amorçage à partir d'une copie passive, sachez que l'opération d'amorçage est interrompue, et génère une erreur de communication réseau, dans les circonstances suivantes :

  - si l'état de la copie de source d'amorçage passe de Failed à FailedAndSuspended.

  - si la base de données bascule sur une autre copie.

Il est possible d'amorcer plusieurs copies d'une base de données en même temps. Cependant, lorsque vous procédez à un amorçage simultané de plusieurs copies, vous devez amorcer uniquement le fichier de base de données et omettre le catalogue d'indexation de contenu. Pour ce faire, utilisez le paramètre *DatabaseOnly* avec la cmdlet [Update-MailboxDatabaseCopy](https://technet.microsoft.com/fr-fr/library/dd335201\(v=exchg.150\)).

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Si vous n’utilisez pas le paramètre <em>DatabaseOnly</em> lors de l’amorçage de plusieurs cibles à partir de la même source, la tâche doit échouer avec l’erreur SeedInProgressException FE1C6491.</td>
</tr>
</tbody>
</table>


Souhaitez-vous rechercher les autres tâches de gestion relatives aux copies de la base de données de boîtes aux lettres ? Consultez la rubrique [Gestion des copies de base de données de boîtes aux lettres](managing-mailbox-database-copies-exchange-2013-help.md).

## Ce qu’il faut savoir avant de commencer ?

  - Durée d’exécution estimée de cette tâche : 2 minutes sont nécessaires, plus le temps d'amorçage de la copie de base de données, en fonction d'une grande variété de facteurs, tels que la taille de la base de données, la vitesse, la bande passante disponible et le temps de réponse du réseau ainsi que les vitesses de stockage.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultezEntrée « Copies de bases de données de boîtes aux lettres » dans la rubrique [Autorisations de haute disponibilité et de résilience des sites](high-availability-and-site-resilience-permissions-exchange-2013-help.md).

  - La copie de base de données de boîte aux lettres doit être suspendue. Pour connaître la procédure détaillée, voir [Interruption ou reprise d’une copie de base de données de boîtes aux lettres](suspend-or-resume-a-mailbox-database-copy-exchange-2013-help.md).

  - Le service Accès à distance au Registre doit être exécuté sur le serveur hébergeant la copie de base de données passive que vous mettez à jour.

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


## Que souhaitez-vous faire ?

## Utiliser le CAE pour mettre à jour une copie de la base de données de boîtes aux lettres

1.  Dans la CCE, accédez à **Serveurs** \> **Bases de données**.

2.  Sélectionnez la base de données de boîtes aux lettres dont vous voulez mettre à jour la copie passive.

3.  Dans le volet d’informations, sous **Copies de base de données**, cliquez sur **Interrompre** sous la copie passive de la base de données à amorcer. Fournissez des commentaires facultatifs le cas échéant, puis cliquez sur **Enregistrer**.

4.  Dans le volet d’informations, sous **Copies de base de données**, cliquez sur **Mettre à jour** sous la copie passive de la base de données à amorcer.

5.  
    
    Par défaut, la copie active de la base de données est utilisée comme base de données source pour l'amorçage. Si vous préférez utiliser une copie passive de la base de données pour l’amorçage, cliquez sur **Parcourir…** pour sélectionner le serveur contenant la copie passive de la base de données à utiliser pour la source.

6.  Cliquez sur **Enregistrer** pour mettre à jour la copie passive de la base de données.

## Utilisation de l’environnement de ligne de commande Exchange Management Shell pour mettre à jour une copie de la base de données de boîtes aux lettres

Dans cet exemple, nous montrons comment amorcer une copie de la base de données DB1 sur MBX1.

    Update-MailboxDatabaseCopy -Identity DB1\MBX1

Dans cet exemple, nous montrons comment amorcer une copie de la base de données DB1 sur MBX1 avec MBX2 comme serveur de boîtes aux lettres source pour l’amorçage.

    Update-MailboxDatabaseCopy -Identity DB1\MBX1 -SourceServer MBX2

Dans cet exemple, nous montrons comment amorcer une copie de la base de données DB1 sur MBX1 sans amorçage du catalogue d’indexation de contenu.

    Update-MailboxDatabaseCopy -Identity DB1\MBX1 -DatabaseOnly

Dans cet exemple, nous montrons comment amorcer le catalogue d’indexation de contenu pour la copie de la base de données DB1 sur MBX1 sans amorcer le fichier de base de données.

    Update-MailboxDatabaseCopy -Identity DB1\MBX1 -CatalogOnly

## Copier manuellement une base de données hors connexion

1.  Si l'enregistrement circulaire est activé pour la base de données, il doit être désactivé avant de poursuivre. Vous pouvez désactiver l'enregistrement circulaire pour une base de données de boîtes aux lettres à l'aide de la cmdlet [Set-MailboxDatabase](https://technet.microsoft.com/fr-fr/library/bb123971\(v=exchg.150\)), comme illustré dans l'exemple suivant.
    
        Set-MailboxDatabase DB1 -CircularLoggingEnabled $false

2.  Démontez la base de données. Vous pouvez utiliser la cmdlet [Dismount-Database](https://technet.microsoft.com/fr-fr/library/bb124936\(v=exchg.150\)), comme illustré dans cet exemple.
    
        Dismount-Database DB1 -Confirm $false

3.  Copier manuellement les fichiers de base de données (le fichier de base de données et tous les fichiers journaux) sur un autre emplacement, tel qu'un lecteur de disque externe ou un partage réseau.

4.  Montez la base de données. Vous pouvez utiliser la cmdlet [Mount-Database](https://technet.microsoft.com/fr-fr/library/aa998871\(v=exchg.150\)), comme illustré dans cet exemple.
    
        Mount-Database DB1

5.  Sur le serveur qui hébergera la copie, copiez les fichiers de base de données à partir du lecteur externe ou du partage réseau vers le même chemin d'accès que la copie de la base de données active. Par exemple, si le chemin d’accès à la copie de la base de données active est D:\\BDD1\\BDD1.edb et que le chemin d’accès aux fichiers journaux est D:\\BDD1, vous devrez alors copier les fichiers de base de données sur D:\\BDD1 sur le serveur qui doit héberger la copie.

6.  Ajoutez la copie de la base de données de boîtes aux lettres à l'aide de la cmdlet [Add-MailboxDatabaseCopy](https://technet.microsoft.com/fr-fr/library/dd298105\(v=exchg.150\)) avec le paramètre *SeedingPostponed*, comme illustré dans l'exemple suivant.
    
        Add-MailboxDatabaseCopy -Identity DB1 -MailboxServer MBX3 -SeedingPostponed

7.  Si l'enregistrement circulaire est activé pour la base de données, réactivez-le à l'aide de la cmdlet [Set-MailboxDatabase](https://technet.microsoft.com/fr-fr/library/bb123971\(v=exchg.150\)), comme illustré dans l'exemple suivant.
    
        Set-MailboxDatabase DB1 -CircularLoggingEnabled $true

## Comment savoir si cela a fonctionné ?

Pour vérifier que l’amorçage de la copie de base de données de boîtes aux lettres s’est bien effectué, procédez de l’une des manières suivantes :

  - Dans le CAE, accédez à **Serveurs** \> **Bases de données**. Sélectionnez la base de données qui a été amorcée. Dans le volet Détails, l'état de la copie de la base de données et son index de contenu sont affichés avec la longueur de la file d'attente de copie actuelle.

  - Dans l’environnement de ligne de commande Exchange Management Shell, exécutez la commande suivante pour vérifier que la copie de la base de données de boîtes aux lettres a bien été amorcée et est saine.
    
        Get-MailboxDatabaseCopyStatus <DatabaseCopyName>
    
    Le statut et l'état de l'index de contenu doivent être sains.

