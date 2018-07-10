---
title: Dépannage de l’indicateur d’intégrité MailboxTransport
TOCTitle: Dépannage de l’indicateur d’intégrité MailboxTransport
ms:assetid: 02bfa4cf-6929-437e-bae5-079ea1b92373
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/ms.exch.scom.mailboxtransport(v=EXCHG.150)
ms:contentKeyID: 54652786
ms.date: 02/05/2016
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Dépannage de l’indicateur d’intégrité MailboxTransport

 

_**Sapplique à :** Exchange Server 2013, Project Server 2013_

_**Dernière rubrique modifiée :** 2015-03-09_

L’indicateur d’intégrité **MailboxTransport** surveille l’intégrité globale des services de dépôt de transport de boîtes aux lettres et de remise de transport de boîtes aux lettres sur les serveurs de boîtes aux lettres. Ces services sont chargés d’envoyer des messages en provenance et à destination de bases de données de boîtes aux lettres. Pour plus d’informations, voir [Flux de messagerie](https://technet.microsoft.com/fr-fr/library/aa996349\(v=exchg.150\)).

Si vous recevez une alerte indiquant que l’indicateur d’intégrité **MailboxTransport** est défectueux, cela signifie qu’un problème empêche peut-être l’envoi ou la réception de messages depuis des bases de données de boîtes aux lettres.

## Explication

Le service **MailboxTransport** est surveillé à l’aide des sondes et moniteurs suivants :


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Sonde</th>
<th>Indicateur d’intégrité</th>
<th>Moniteurs associés</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>MailboxDeliveryAvailability</p></td>
<td><p>MailboxTransport</p></td>
<td><p>MailboxDeliveryAvailabilityMonitor</p></td>
</tr>
<tr class="even">
<td><p>MailboxDeliveryAvailabilityAggregationProbe</p></td>
<td><p>MailboxTransport</p></td>
<td><p>MailboxDeliveryAvailabilityAggregationMonitor</p></td>
</tr>
<tr class="odd">
<td><p>MailboxDeliveryInstanceAvailabilityProbe</p></td>
<td><p>MailboxTransport</p></td>
<td><p>MailboxDeliveryInstanceAvailabilityMonitor</p></td>
</tr>
<tr class="even">
<td><p>MailboxTransportDeliveryServiceRunning</p></td>
<td><p>MailboxTransport</p></td>
<td><p>MailboxTransportDeliveryServiceRunningMonitor</p></td>
</tr>
<tr class="odd">
<td><p>MailboxTransportSubmissionServiceRunning</p></td>
<td><p>MailboxTransport</p></td>
<td><p>MailboxTransportSubmissionServiceRunningMonitor</p></td>
</tr>
<tr class="even">
<td><p>Mapi.Submit.Probe</p></td>
<td><p>MailboxTransport</p></td>
<td><p>Mapi.Submit.Monitor</p></td>
</tr>
<tr class="odd">
<td><p>aucun (notification ou vérification)</p></td>
<td><p>MailboxTransport</p></td>
<td><p>CrashEvent.msexchangedelivery</p></td>
</tr>
<tr class="even">
<td><p>aucun (notification ou vérification)</p></td>
<td><p>MailboxTransport</p></td>
<td><p>CrashEvent.msexchangesubmission</p></td>
</tr>
<tr class="odd">
<td><p>aucun (notification ou vérification)</p></td>
<td><p>MailboxTransport</p></td>
<td><p>DeliveryBackpressureSustainedTimeMonitor</p></td>
</tr>
<tr class="even">
<td><p>aucun (notification ou vérification)</p></td>
<td><p>MailboxTransport</p></td>
<td><p>DeliveryInterceptorStoreDriverAgentPctPermFailedMonitor</p></td>
</tr>
<tr class="odd">
<td><p>aucun (notification ou vérification)</p></td>
<td><p>MailboxTransport</p></td>
<td><p>MailboxTransportUserQuarantineMonitor</p></td>
</tr>
<tr class="even">
<td><p>aucun (notification ou vérification)</p></td>
<td><p>MailboxTransport</p></td>
<td><p>MBTSubmissionInterceptorSubmissionAgentMonitor</p></td>
</tr>
<tr class="odd">
<td><p>aucun (notification ou vérification)</p></td>
<td><p>MailboxTransport</p></td>
<td><p>MSExchangeAsstAvgEventProcessingTimeSubmissionMonitor50</p></td>
</tr>
<tr class="even">
<td><p>aucun (notification ou vérification)</p></td>
<td><p>MailboxTransport</p></td>
<td><p>MSExchangeAsstAvgEventProcessingTimeSubmissionMonitor70</p></td>
</tr>
<tr class="odd">
<td><p>aucun (notification ou vérification)</p></td>
<td><p>MailboxTransport</p></td>
<td><p>PrivateWorkingSetError.msexchangedelivery</p></td>
</tr>
<tr class="even">
<td><p>aucun (notification ou vérification)</p></td>
<td><p>MailboxTransport</p></td>
<td><p>PrivateWorkingSetError.msexchangesubmission</p></td>
</tr>
<tr class="odd">
<td><p>aucun (notification ou vérification)</p></td>
<td><p>MailboxTransport</p></td>
<td><p>PrivateWorkingSetWarning.msexchangedelivery</p></td>
</tr>
<tr class="even">
<td><p>aucun (notification ou vérification)</p></td>
<td><p>MailboxTransport</p></td>
<td><p>PrivateWorkingSetWarning.msexchangesubmission</p></td>
</tr>
<tr class="odd">
<td><p>aucun (notification ou vérification)</p></td>
<td><p>MailboxTransport</p></td>
<td><p>ProcessProcessorTimeError.msexchangedelivery</p></td>
</tr>
<tr class="even">
<td><p>aucun (notification ou vérification)</p></td>
<td><p>MailboxTransport</p></td>
<td><p>ProcessProcessorTimeError.msexchangesubmission</p></td>
</tr>
<tr class="odd">
<td><p>aucun (notification ou vérification)</p></td>
<td><p>MailboxTransport</p></td>
<td><p>ProcessProcessorTimeWarning.msexchangedelivery</p></td>
</tr>
<tr class="even">
<td><p>aucun (notification ou vérification)</p></td>
<td><p>MailboxTransport</p></td>
<td><p>ProcessProcessorTimeWarning.msexchangesubmission</p></td>
</tr>
<tr class="odd">
<td><p>aucun (notification ou vérification)</p></td>
<td><p>MailboxTransport</p></td>
<td><p>SubmissionBackpressureSustainedTimeMonitor</p></td>
</tr>
<tr class="even">
<td><p>aucun (notification ou vérification)</p></td>
<td><p>MailboxTransport</p></td>
<td><p>SubmissionInterceptorSubmissionAgentPctPermFailedMonitor</p></td>
</tr>
<tr class="odd">
<td><p>aucun (notification ou vérification)</p></td>
<td><p>MailboxTransport</p></td>
<td><p>TransportDeliveryFailuresDeliveryStoreDriver560Monitor</p></td>
</tr>
</tbody>
</table>


Pour plus d’informations sur les sondes et les moniteurs, consultez la rubrique [État et performances du serveur](https://technet.microsoft.com/fr-fr/library/jj150551\(v=exchg.150\)).

## Action de l’utilisateur

Il se peut que le service ait récupéré après avoir émis l’alerte. Par conséquent, lorsque vous recevez une alerte signalant que l’indicateur d’intégrité **MailboxTransport** est défectueux, vérifiez d’abord que le problème existe toujours. Si tel est le cas, exécutez les actions de récupération appropriées décrites dans la section suivante.

## Vérification du problème

1.  Repérez le nom de l’indicateur d’intégrité et celui du serveur dans l’alerte.

2.  Les détails du message fournissent des informations sur la cause exacte de l’alerte. Dans la plupart des cas, ils fournissent des informations de dépannage suffisantes pour identifier la cause première. Si les détails du message ne sont pas clairs, procédez comme suit :
    
    1.  Ouvrez Environnement de ligne de commande Exchange Management Shell, puis exécutez la commande suivante pour récupérer les détails de l’indicateur d’intégrité qui a émis l’alerte :
        
            Get-ServerHealth <server name> | ?{$_.HealthSetName -eq "<health set name>"}
        
        Par exemple, pour extraire les détails de l’indicateur d’intégrité **MailboxTransport** relatifs à mailbox1.contoso.com, exécutez la commande suivante :
        
            Get-ServerHealth mailbox1.contoso.com | ?{$_.HealthSetName -eq "MailboxTransport"}
    
    2.  Consultez la sortie de la commande pour déterminer le moniteur qui a signalé l’erreur. La valeur **AlertValue** du moniteur qui a émis l’alerte sera **Unhealthy**.
    
    3.  Réexécutez la sonde associée pour le moniteur dont l’état d’intégrité est défectueux. Pour rechercher la sonde associée, reportez-vous au tableau figurant dans la section [Explanation](troubleshooting-activesync-health-set.md). Pour ce faire, exécutez la commande suivante :
        
            Invoke-MonitoringProbe <health set name>\<probe name> -Server <server name> | Format-List
        
        Par exemple, supposons que le moniteur défectueux soit **MailboxDeliveryAvailabilityMonitor**. La sonde associée à ce moniteur est **MailboxDeliveryAvailability**. Pour exécuter cette sonde sur mailbox1.contoso.com, exécutez la commande suivante :
        
            Invoke-MonitoringProbe MailboxTransport\MailboxDeliveryAvailabilityMonitor -Server mailbox1.contoso.com | Format-List
    
    4.  Dans la sortie de la commande, consultez la section « Result » de la sonde. Si elle indique **Succeeded**, le problème était une erreur passagère, qui n’existe plus.

