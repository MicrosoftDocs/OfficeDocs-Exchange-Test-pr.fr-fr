---
title: 'Restaurer des données à l’aide d’une base de données de récupération: Exchange 2013 Help'
TOCTitle: Restaurer des données à l’aide d’une base de données de récupération
ms:assetid: d64c18e7-16af-4bd8-a5c5-01206984d4d1
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Ee332351(v=EXCHG.150)
ms:contentKeyID: 50479277
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Restaurer des données à l’aide d’une base de données de récupération

 

_**Sapplique à :**Exchange Server 2013_

_**Dernière rubrique modifiée :**2014-10-01_

Une base de données de récupération constitue un type de base de données de boîtes aux lettres spécial, qui vous permet de monter une base de données de boîtes aux lettres restaurée et d’en extraire les données, dans le cadre d’une opération de récupération. Un groupe de stockage de récupération vous permet de récupérer des données à partir d'une sauvegarde ou d'une copie de base de données sans interrompre l'accès des utilisateurs aux données actuelles.

Une fois la base de données de récupération créée, vous pouvez restaurer une base de données de boîtes aux lettres dans la base de données de récupération à l’aide d’une application de sauvegarde ou en copiant une base de données et ses fichiers journaux dans la structure de dossiers de la base de données de récupération. Vous pouvez ensuite utiliser la cmdlet [New-MailboxRestoreRequest](https://technet.microsoft.com/fr-fr/library/ff829875\(v=exchg.150\)) pour extraire des données depuis la base de données récupérée. Après extraction, les données peuvent être exportées dans un dossier ou fusionnées dans une boîte aux lettres existante.

Si vous souhaitez rechercher des tâches de gestion supplémentaires relatives aux bases de données de récupération, consultez la rubrique [Récupérer des bases de données](recovery-databases-exchange-2013-help.md).

## Ce qu’il faut savoir avant de commencer ?

  - Durée d’exécution estimée de cette tâche : 1 minute, plus le temps nécessaire pour mettre la base de données dans un état d’arrêt correct et extraire les données.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez entrée « Récupération de boîtes aux lettres » dans la rubrique [Autorisations des destinataires](recipients-permissions-exchange-2013-help.md).

  - Certaines applications offrent la possibilité de restaurer des données Exchange directement vers une base de données de récupération. La fonction Sauvegarde Windows Server peut restaurer uniquement des sauvegardes de niveau de fichier vers une base de données de récupération. Elle ne peut pas être utilisée pour restaurer des sauvegardes de niveau d’application vers une base de données de récupération.

  - La base de données et les fichiers journaux contenant les données récupérées doivent être restaurés ou copiés dans la structure de dossiers de la base de données de récupération.

  - La base de données doit être dans un état d'arrêt correct. Comme une base de données de récupération constitue un autre emplacement de restauration pour toutes les bases de données, toutes les bases de données restaurées seront dans un état d'arrêt incorrect. Vous pouvez utiliser **Eseutil /R** pour mettre les bases de données restaurées dans un état d’arrêt correct.

## Utilisez le shell pour récupérer des données à l'aide d'une base de données de récupération

1.  Copiez une base de données récupérée et ses fichiers journaux, ou restaurez une base de données et ses fichiers journaux, à l’emplacement que vous allez utiliser pour votre base de données de récupération.

2.  Utilisez Eseutil pour mettre cette base de données dans un état d’arrêt correct. Dans l’exemple précédent, EXX est le préfixe de génération de journal (par exemple E00, E01, E02, etc.).
    
        Eseutil /R EXX /l <RDBLogFilePath> /d <RDBEdbFolder>
    
    L’exemple suivant illustre le préfixe de génération de journal E01, la base de données de récupération et le chemin d’accès aux fichiers journaux E:\\Databases\\RDB1 :
    
        Eseutil /R E01 /l E:\Databases\RDB1 /d E:\Databases\RDB1

3.  Créer une base de données de récupération. Attribuez un nom unique à la base de données de récupération, mais utilisez le nom et le chemin d’accès du fichier de base de données pour le paramètre EdbFilePath, et l’emplacement des fichiers journaux récupérés pour le paramètre LogFolderPath.
    
        New-MailboxDatabase -Recovery -Name <RDBName> -Server <ServerName> -EdbFilePath <RDBPathandFileName> -LogFolderPath <LogFilePath>
    
    L’exemple suivant illustre la création d’une base de données de récupération qui sera utilisée pour récupérer DB1.edb et ses fichiers journaux, qui se trouvent dans E:\\Databases\\RDB1.
    
        New-MailboxDatabase -Recovery -Name <RDBName> -Server <ServerName> -EdbFilePath "E:\Databases\RDB1\DB1.EDB" -LogFolderPath "E:\Databases\RDB1"

4.  Redémarrez le service de banque d’informations Microsoft Exchange :
    
        Restart-Service MSExchangeIS

5.  Montez la base de données de récupération :
    
        Mount-database <RDBName>

6.  Vérifiez que la base de données montée contient les boîtes aux lettres que vous voulez restaurer :
    
        Get-MailboxStatistics -Database <RDBName> | ft -auto

7.  Utilisez la cmdlet New-MailboxRestoreRequest pour restaurer une boîte aux lettres ou des éléments de la base de données de récupération vers une boîte aux lettres de production.
    
    L’exemple qui suit illustre la restauration de la boîte aux lettres source, dont la valeur MailboxGUID est 1d20855f-fd54-4681-98e6-e249f7326ddd sur la base de données de boîtes aux lettres DB1, vers la boîte aux lettres cible dont l’alias est Morris.
    
        New-MailboxRestoreRequest -SourceDatabase DB1 -SourceStoreMailbox 1d20855f-fd54-4681-98e6-e249f7326ddd -TargetMailbox Morris
    
    L’exemple qui suit illustre la restauration du contenu de la boîte aux lettres source dont le nom complet est Morris Cornejo sur la base de données de boîtes aux lettres DB1, vers la boîte aux lettres d’archivage Morris@contoso.com.
    
        New-MaiboxRestoreRequest -SourceDatabase DB1 -SourceStoreMailbox "Morris Cornejo" -TargetMailbox Morris@contoso.com -TargetIsArchive

8.  Vérifiez régulièrement l’état de la demande de restauration de boîte aux lettres à l’aide de la cmdlet [Get-MailboxRestoreRequest](https://technet.microsoft.com/fr-fr/library/ff829907\(v=exchg.150\)).
    
    Lorsque l’état de la restauration est Terminé, supprimez la demande de restauration à l’aide de la cmdlet [Remove-MailboxRestoreRequest](https://technet.microsoft.com/fr-fr/library/ff829910\(v=exchg.150\)). Par exemple :
    
        Get-MailboxRestoreRequest -Status Completed | Remove-MailboxRestoreRequest

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez bien récupéré les données de la boîte aux lettres, ouvrez la boîte aux lettres cible à l’aide d’Outlook ou d’Outlook Web App et vérifiez que les données récupérées sont présentes.

<table>
<thead>
<tr class="header">
<th><img src="images/Bb125224.tip(EXCHG.150).gif" title="Conseil" alt="Conseil" />Conseil :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.</td>
</tr>
</tbody>
</table>

