---
title: 'Récupérer un serveur membre de groupe de dispo. de la BDD: Exchange 2013 Help'
TOCTitle: Récupérer un serveur membre de groupe de disponibilité de la base de données
ms:assetid: eccd8f61-9706-4bb7-a62a-ec7c166f8019
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dd638206(v=EXCHG.150)
ms:contentKeyID: 50479502
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Récupérer un serveur membre de groupe de disponibilité de la base de données

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2016-12-09_

Si un serveur de boîtes aux lettres membre d’un groupe de disponibilité de base de données est perdu ou tombe en panne, et s’il est irrécupérable et doit être remplacé, vous pouvez effectuer une opération de récupération de ce serveur. Le programme d’installation de Microsoft Exchange Server 2013 inclut le commutateur */m:RecoverServer* qui permet d’exécuter les opérations de récupération du serveur. Lorsque vous exécutez le programme d’installation avec le commutateur */m:RecoverServer*, il lit les informations de configuration à partir d’Active Directory pour un serveur ayant le même nom que celui à partir duquel vous exécutez l’installation. Une fois que les informations de configuration du serveur sont récupérées depuis Active Directory, les fichiers et les services d’origine d’Exchange sont installés sur le serveur et les rôles et les paramètres qui étaient stockés dans Active Directory lui sont appliqués.

Souhaitez-vous rechercher les autres tâches de gestion relatives aux groupes de disponibilité de base de données ? Consultez la rubrique [Gestion de groupes de disponibilité de base de données](managing-database-availability-groups-exchange-2013-help.md).

## Ce qu’il faut savoir avant de commencer ?

  - Durée d'exécution estimée : 30 minute

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultezEntrée « Copies de bases de données de boîtes aux lettres » dans la rubrique [Autorisations de haute disponibilité et de résilience des sites](high-availability-and-site-resilience-permissions-exchange-2013-help.md).

  - Si Exchange est installé à un emplacement autre que celui défini par défaut, vous devez utiliser le commutateur d’installation */TargetDir* pour préciser l’emplacement des fichiers programme d’Exchange. Si vous n’utilisez pas le commutateur */TargetDir*, les fichiers programme d’Exchange doivent être installés à l’emplacement par défaut (%programfiles%\\Microsoft\\Exchange Server\\V15).
    
    Pour déterminer l’emplacement d’installation, procédez comme suit :
    
    1.  Ouvrez ADSIEDIT.MSC ou LDP.EXE.
    
    2.  Accédez à l’emplacement suivant : **CN=ExServerName,CN=Servers,CN=First Administrative Group,CN=Administrative Groups,CN=ExOrg Name,CN=Microsoft Exchange,CN=Services,CN=Configuration,DC=DomainName,CN=Com**
    
    3.  Cliquez avec le bouton droit sur l’objet serveur Exchange, puis cliquez sur **Propriétés**.
    
    4.  Recherchez l’attribut **msExchInstallPath**. Cet attribut contient le chemin d’installation actuel.

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..


## Utiliser le programme d’installation avec le commutateur /m:RecoverServer pour récupérer un serveur

1.  Récupérez les paramètres du délai d’attente de relecture ou de troncation pour les copies de bases de données de boîtes aux lettres se trouvant sur le serveur en cours de récupération à l’aide de la cmdlet [Get-MailboxDatabase](https://technet.microsoft.com/fr-fr/library/bb124924\(v=exchg.150\)).
    
        Get-MailboxDatabase DB1 | Format-List *lag*

2.  Supprimez les copies de bases de données de boîtes aux lettres se trouvant sur le serveur en cours de récupération à l’aide de la cmdlet [Remove-MailboxDatabaseCopy](https://technet.microsoft.com/fr-fr/library/dd335119\(v=exchg.150\)).
    
    ```powershell
Remove-MailboxDatabaseCopy DB1\MBX1
```

3.  Supprimez la configuration du serveur en panne du groupe de disponibilité de base de données à l’aide de la cmdlet [Remove-DatabaseAvailabilityGroupServer](https://technet.microsoft.com/fr-fr/library/dd297956\(v=exchg.150\)).
    
    ```powershell
Remove-DatabaseAvailabilityGroupServer -Identity DAG1 -MailboxServer MBX1
```
    
    > [!NOTE]
    > Si le membre du groupe de disponibilité de base de données supprimé est hors connexion et s’il ne peut pas être mis en ligne, vous devez ajouter le paramètre <em>ConfigurationOnly</em> à la commande précédente. Si vous utilisez le commutateur <em>ConfigurationOnly</em>, vous devez également expulser manuellement le nœud du cluster.


4.  Réinitialisez le compte d’ordinateur du serveur dans Active Directory. Pour obtenir la procédure détaillée, voir [Réinitialiser un compte d’ordinateur](http://go.microsoft.com/fwlink/p/?linkid=167188).

5.  Ouvrez une fenêtre d’invite de commandes. À l’aide du support d’installation d’origine, exécutez la commande suivante :
    
    ```powershell
Setup /m:RecoverServer
```

6.  Lorsque le processus de récupération d’installation est terminé, ajoutez le serveur récupéré au groupe de disponibilité de base de données à l’aide de la cmdlet [Add-DatabaseAvailabilityGroupServer](https://technet.microsoft.com/fr-fr/library/dd298049\(v=exchg.150\)).
    
    ```powershell
Add-DatabaseAvailabilityGroupServer -Identity DAG1 -MailboxServer MBX1
```

7.  Une fois que le serveur est ajouté au groupe de disponibilité de base de données, reconfigurez les copies de bases de données de boîtes aux lettres à l’aide de la cmdlet [Add-MailboxDatabaseCopy](https://technet.microsoft.com/fr-fr/library/dd298105\(v=exchg.150\)). Si des copies de bases de données déjà ajoutées ont un délai d’attente de relecture ou de troncation supérieur à 0, utilisez les paramètres *ReplayLagTime* et *TruncationLagTime* de la cmdlet [Add-MailboxDatabaseCopy](https://technet.microsoft.com/fr-fr/library/dd298105\(v=exchg.150\)) pour reconfigurer ces paramètres.
    
        Add-MailboxDatabaseCopy -Identity DB1 -MailboxServer MBX1
        Add-MailboxDatabaseCopy -Identity DB2 -MailboxServer MBX1 -ReplayLagTime 3.00:00:00
        Add-MailboxDatabaseCopy -Identity DB3 -MailboxServer MBX1 -ReplayLagTime 3.00:00:00 -TruncationLagTime 3.00:00:00

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez bien récupéré le membre du groupe de disponibilité de base de données, procédez comme suit :

  - Dans l’environnement de ligne de commande Exchange Management Shell, exécutez la commande suivante pour vérifier l’intégrité et le statut du membre du groupe de disponibilité de base de données restauré.
    
       ```
       ```powershell
Test-ReplicationHealth <ServerName>
```
       ```

       ```   
       ```powershell
Get-MailboxDatabaseCopyStatus -Server <ServerName>
```
       ```   
    
    L'ensemble des tests d'intégrité de réplication doivent réussir et le statut des bases de données et leurs index de contenu doivent être intègres.

