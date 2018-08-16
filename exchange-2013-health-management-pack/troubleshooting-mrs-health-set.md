---
title: Dépannage de l'indicateur d'intégrité MRS
TOCTitle: Dépannage de l'indicateur d'intégrité MRS
ms:assetid: 21947ed6-1584-4db9-9cd6-f6c1de22e352
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/ms.exch.scom.mrs(v=EXCHG.150)
ms:contentKeyID: 53276466
ms.date: 02/05/2016
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Dépannage de l'indicateur d'intégrité MRS

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2015-03-09_

L'indicateur d'intégrité du service de réplication de boîte aux lettres (MRS) surveille l'intégrité globale du service MRS.

## Explication

Le service MRS est surveillé à l'aide des sondes et moniteurs suivants.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Sonde</th>
<th>Indicateur d'intégrité</th>
<th>Dépendances</th>
<th>Moniteurs associés</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>MRSServiceCrashingProbe</p></td>
<td><p>MRS</p></td>
<td><p>Banque d'informations</p></td>
<td><p>MRSServiceCrashingMonitor</p></td>
</tr>
</tbody>
</table>


Pour plus d'informations sur les sondes et les moniteurs, consultez la rubrique [État et performances du serveur](https://technet.microsoft.com/fr-fr/library/jj150551\(v=exchg.150\)).

## Action de l'utilisateur

Il se peut que le service ait récupéré après avoir émis l'alerte. Par conséquent, quand vous recevez une alerte signalant que l'indicateur d'intégrité n'est pas intègre, vérifiez tout d'abord que le problème existe toujours. Si tel est le cas, exécutez les actions de récupération appropriées décrites dans les sections suivantes.

## Vérification de l'existence du problème

1.  Repérez les noms de l'indicateur d'intégrité et du serveur dans l'alerte.

2.  Les détails du message fournissent des informations sur la cause exacte de l'alerte. Le plus souvent, le message fournit des informations de dépannage suffisantes pour identifier la cause première. Si les détails du message ne sont pas clairs, procédez comme suit :
    
    1.  Ouvrez Environnement de ligne de commande Exchange Management Shell, puis exécutez la commande suivante pour récupérer les détails de l'indicateur d'intégrité qui a émis l'alerte :
        
            Get-ServerHealth <server name> | ?{$_.HealthSetName -eq "<health set name>"}
        
        Par exemple, pour récupérer les détails de l'indicateur d'intégrité MRS à propos de server1.contoso.com, exécutez la commande suivante :
        
            Get-ServerHealth server1.contoso.com | ?{$_.HealthSetName -eq "MRS"}
    
    2.  Consultez la sortie de la commande pour déterminer quel moniteur a signalé l'erreur. La valeur **AlertValue** du moniteur qui a émis l'alerte sera `Unhealthy`.
    
    3.  Réexécutez la sonde associée pour le moniteur dont l'état n'est pas intègre. Pour rechercher la sonde associée, reportez-vous au tableau figurant dans la section Explanation. Pour ce faire, exécutez la commande suivante :
        
            Invoke-MonitoringProbe <health set name>\<probe name> -Server <server name> | Format-List
        
        Par exemple, supposons que le moniteur défectueux soit **MRSServiceCrashingMonitor**. La sonde associée à ce moniteur est **MRSServiceCrashingProbe**. Pour exécuter cette sonde sur server1.contoso.com, exécutez la commande suivante :
        
            Invoke-MonitoringProbe MRS\MRSServiceCrashingProbe -Server server1.contoso.com | Format-List
    
    4.  Dans la sortie de la commande, consultez la valeur **Result** de la sonde. Si elle indique **Succeeded**, le problème était une erreur passagère, qui n'existe plus. Autrement, reportez-vous aux étapes de récupération décrites dans les sections suivantes.

## Problèmes courants

Quand vous recevez une alerte de l'indicateur d'intégrité, le message électronique contient les informations suivantes :

  - nom du serveur ayant envoyé l'alerte ;

  - heure et date de l'alerte ;

  - mécanisme d'authentification utilisé et informations d'identification ;

  - trace d'exception complète de la dernière erreur, notamment données de diagnostic et informations d'en-tête HTTP spécifiques
    
    Vous pouvez utiliser les informations contenues dans la trace de l'exception complète pour résoudre le problème. L'exception générée par la sonde contient un motif de l'échec qui décrit pourquoi la sonde a échoué.

**Boîte aux lettres verrouillée**

Si une boîte aux lettres est verrouillée, il se peut que vous receviez une alerte ressemblant à ceci :

*MailboxIdentity: namprd03.prod.outlook.com/Microsoft Exchange Hosted Organizations/example.com/User6 MailboxGuid: Primary (00000000-abcd-01234-5678-1234567890ab) RequestFlags: IntraOrg, Pull, Protected Database: exampledb-db089 Exception: MapiExceptionADUnavailable: Unable to prepopulate the cache for user…*

Cela indique qu'une boîte aux lettres est verrouillée. Pour la déverrouiller, exécutez la commande suivante :

    New-MailboxRepairRequest -CorruptionType LockedMoveTarget -Identity <mailboxIdentity> [-Archive]

**Remarque**   Dans cette commande, remplacez \<*mailboxIdentity*\> par le nom de la boîte aux lettres qui est fourni dans le message électronique en tant que **MailboxIdentity**. S'il s'agit d'une boîte aux lettres d'archivage, vous devez inclure l'indicateur **–Archive**. Vous pouvez déterminer s'il s'agit d'une boîte aux lettres principale ou d'archivage en consultant le champ **MailboxGuid** dans l'alerte.

**Tâche de migration endommagée**

Si une tâche de migration est endommagée, il se peut que vous receviez une alerte ressemblant à ceci :

*Notification thrown by MailboxMigration at 9/7/2012 9:08:32 PM. Details: Diagnostic Information: ProcessCacheEntry: First Organization :: /o=ExchangeLabs/ou=Exchange Administrative Group (FYDIBOHF23SPDLT)/cn=Recipients/cn=e80fc128879e452ebc882f6bca7007fa-Migration.8*

Un endommagement se produit quand les métadonnées de migration présentent des erreurs. En cas d'endommagement, Microsoft reçoit un rapport Dr Watson pour investigation. Pour corriger ce problème, vous devez supprimer le lot de migration, puis le recréer. Pour ce faire, procédez comme suit :

1.  Pour supprimer le lot endommagé, exécutez la commande suivante :
    
        Remove-MigrationBatch -Identity

2.  Pour recréer le lot, exécutez la commande suivante :
    
        New-MigrationBatch -Local -Name

Pour plus d'informations, consultez la rubrique [Cmdlets Exchange 2013](https://technet.microsoft.com/fr-fr/library/bb124413\(v=exchg.150\))

**MailboxMigration alert: CriticalError**

Si une erreur critique se produit durant une migration de courrier électronique, il se peut que vous receviez une alerte ressemblant à ceci :

*Notification thrown by MailboxMigration at 9/7/2012 9:08:32 PM. Details: Diagnostic Information: ProcessCacheEntry: First Organization :: /o=ExchangeLabs/ou=Exchange Administrative Group (FYDIBOHF23SPDLT)/cn=Recipients/cn=e80fc128879e452ebc882f6bca7007fa-Migration.8*

Pour résoudre ce problème vous pouvez réessayer d'effectuer la migration. À cette fin, exécutez la commande suivante ou appuyez sur le bouton **Démarrer** dans le Centre d'administration Exchange (CAE).

    Call start-migrationbatch -Identity batchName

Lorsque ce problème se produit, un message Dr Watson est envoyé à Microsoft pour investigation.

**The Migration Exchange Replication Service is not running**

Si ce motif d'erreur est mentionné, vous pouvez vérifier l'intégrité du service en exécutant la commande suivante :

    Test-MRSHealth <servername> -MonitoringContext:$true

Vous pouvez également tenter de démarrer le service en exécutant la commande suivante :

    Start-Service msexchangemailboxreplication

**MSExchangeMailboxReplication RCP Ping Failed**

Si ce motif d'erreur est mentionné, il se peut que vous receviez une alerte ressemblant à ceci :

*An issue with MRS was detected at 6/26/2012 6:08:47 AM. Details: MRS RPC Ping check for server \<Nom de serveur\> failed with the following error: The RPC endpoint for the Microsoft Exchange Mailbox Replication service couldn't respond:*

Si ce problème se produit, vous pouvez vérifier l'intégrité du service en exécutant la commande suivante :

    Test-MRSHealth <servername> -MonitoringContext:$true

Vous pouvez également tenter de redémarrer le service en exécutant la commande suivante :

    Restart-Service msexchangemailboxreplication

**MSExchangeMailboxReplication Service is repeatedly crashing**

Si le service MSExchangeMailboxReplication se bloque ou cesse de répondre, il se peut que vous receviez une alerte ressemblant à ceci :

*The MRS process has crashed at least 3 times in last 01:00:00. \<b\>Watson Message:\</b\> Watson report about to be sent for process id: 41432, with parameters: E12, \<Nom de serveur\>, 15.00.0516.024, MSExchangeMailboxReplication, M.Exchange.MailboxReplicationService, M.E.M.BaseJob.BeginJob, System.ApplicationException, 7ec9, 15.00.0516.024. ErrorReportingEnabled: True.*

Si ce problème se produit, vous pouvez vérifier l'intégrité du service en exécutant la commande suivante :

    Test-MRSHealth <servername> -MonitoringContext:$true

Vous pouvez également tenter de redémarrer le service en exécutant la commande suivante :

    Restart-Service msexchangemailboxreplication

**MSExchangeMailboxReplication is not scanning MDB queues**

Si le service MSExchangeMailboxReplication ne parvient pas à analyser les files d'attente, il se peut que vous receviez une alerte ressemblant à ceci :

*An issue with MRS was detected at 6/26/2012 6:20:44 AM. Details: MRS queue scan check for server \<Nom de serveur\> failed with the following error: The Microsoft Exchange Mailbox Replication Service isn't scanning mailbox database queues for jobs. Last scan age: 04:38:02.1959439..*

Si ce problème se produit, vous pouvez vérifier l'intégrité du service en exécutant la commande suivante :

    Test-MRSHealth <servername> -MonitoringContext:$true

Vous pouvez également tenter de redémarrer le service en exécutant la commande suivante :

    Restart-Service msexchangemailboxreplication

**Étapes de dépannage supplémentaires :** 

1.  Démarrez le Gestionnaire des services Internet, puis connectez-vous au serveur signalant le problème afin de déterminer si le pool d'applications **MSExchangeServicesAppPool** est en cours d'exécution.

2.  Dans le Gestionnaire des services Internet, cliquez sur **Pools d'applications**, puis recyclez le pool d'applications **MSExchangeServicesAppPool** en exécutant la commande suivante à partir de l'environnement de ligne de commande :
    
        %SystemRoot%\System32\inetsrv\Appcmd recycle MSExchangeServicesAppPool

3.  Réexécutez la sonde associée en procédant de la manière décrite dans l'étape 2c de la section Verifying the issue still exists.

4.  Si le problème persiste, recyclez le service IIS à l'aide de l'utilitaire IISReset ou en exécutant la commande suivante :
    
        Iisreset /noforce

5.  Réexécutez la sonde associée en procédant de la manière décrite dans l'étape 2c de la section Verifying the issue still exists.

6.  Si le problème persiste, redémarrez le serveur.

7.  Une fois le serveur redémarré, réexécutez la sonde associée en procédant de la manière décrite dans l'étape 2c de la section Verifying the issue still exists.

8.  En cas de nouvel échec de la sonde, il se peut que vous ayez besoin d'aide pour résoudre ce problème. Contactez un professionnel du Support Technique de Microsoft pour résoudre ce problème. Pour contacter un professionnel du Support Technique de Microsoft, consultez [Exchange Server Solutions Center](http://go.microsoft.com/fwlink/p/?linkid=180809). Dans le volet de navigation, cliquez sur **Ressources et options de support** et utilisez l'une des options indiquées sous **Obtenez du support technique** pour contacter un professionnel du support Microsoft. Étant donné que votre organisation peut avoir une procédure spécifique pour contacter directement les Services de Support Technique Microsoft, assurez-vous de connaître d'abord les instructions propres à votre organisation.

## Pour plus d'informations

[Nouveautés d'Exchange 2013](https://technet.microsoft.com/fr-fr/library/jj150540\(v=exchg.150\))

[Cmdlets Exchange 2013](https://technet.microsoft.com/fr-fr/library/bb124413\(v=exchg.150\))

