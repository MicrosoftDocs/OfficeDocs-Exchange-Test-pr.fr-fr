---
title: Dépannage de l’indicateur d’intégrité de transport HUB
TOCTitle: Dépannage de l’indicateur d’intégrité de transport HUB
ms:assetid: e3932ce3-836c-4230-9f64-63af1b704d79
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/ms.exch.scom.hubtransport(v=EXCHG.150)
ms:contentKeyID: 54652820
ms.date: 02/05/2016
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Dépannage de l’indicateur d’intégrité de transport HUB

 

_**Sapplique à :**Exchange Server 2013_

_**Dernière rubrique modifiée :**2015-03-09_

Le jeu d’intégrité **HubTransport** surveille l’intégrité globale du pipeline de transport sur les serveurs de boîtes aux lettres responsable de l’acheminement des messages électroniques dans votre organisation. Pour plus d’informations, voir [Flux de messagerie](https://technet.microsoft.com/fr-fr/library/aa996349\(v=exchg.150\)).

Si vous recevez une alerte indiquant que le jeu d’intégrité **HubTransport** est défectueux, cela signifie qu’un problème peut empêcher un message d’être acheminé et distribué.

## Explication

Le service **HubTransport** est surveillé à l’aide des sondes et moniteurs suivants :


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
<td><p>ActiveQueueDrainFailureProbe</p></td>
<td><p>HubTransport</p></td>
<td><p>ActiveQueueDrainFailureMonitor</p></td>
</tr>
<tr class="even">
<td><p>DiagnosticsAggregationLocalSnapshotProbe</p></td>
<td><p>HubTransport</p></td>
<td><p>DiagnosticsAggregationLocalSnapshotMonitor</p></td>
</tr>
<tr class="odd">
<td><p>DiagnosticsAggregationWebServiceProbe</p></td>
<td><p>HubTransport</p></td>
<td><p>DiagnosticsAggregationWebServiceMonitor</p></td>
</tr>
<tr class="even">
<td><p>HubAvailabilityProbe</p></td>
<td><p>HubTransport</p></td>
<td><p>HubAvailabilityMonitor</p></td>
</tr>
<tr class="odd">
<td><p>HubTransportServiceRunning</p></td>
<td><p>HubTransport</p></td>
<td><p>HubTransportServiceRunningMonitor</p></td>
</tr>
<tr class="even">
<td><p>ShadowQueueDiscardDrainFailureProbe</p></td>
<td><p>HubTransport</p></td>
<td><p>ShadowQueueDiscardDrainFailureMonitor</p></td>
</tr>
<tr class="odd">
<td><p>ThrottlingServiceRunning</p></td>
<td><p>HubTransport</p></td>
<td><p>ThrottlingServiceRunningMonitor</p></td>
</tr>
<tr class="even">
<td><p>TransportEdgeSync.Service.Probe</p></td>
<td><p>HubTransport</p></td>
<td><p>TransportEdgeSync.Service.Monitor</p></td>
</tr>
<tr class="odd">
<td><p>TransportLogSearchRunningProbe</p></td>
<td><p>HubTransport</p></td>
<td><p>TransportLogSearchRunningMonitor</p></td>
</tr>
<tr class="even">
<td><p>aucun (notification ou vérification)</p></td>
<td><p>HubTransport</p></td>
<td><p>BootloaderOutstandingItemsTriggerMonitor</p></td>
</tr>
<tr class="odd">
<td><p>aucun (notification ou vérification)</p></td>
<td><p>HubTransport</p></td>
<td><p>CrashEvent.edgetransport</p></td>
</tr>
<tr class="even">
<td><p>aucun (notification ou vérification)</p></td>
<td><p>HubTransport</p></td>
<td><p>CrashEvent.msexchangethrottling</p></td>
</tr>
<tr class="odd">
<td><p>aucun (notification ou vérification)</p></td>
<td><p>HubTransport</p></td>
<td><p>CrashEvent.msexchangetransport</p></td>
</tr>
<tr class="even">
<td><p>aucun (notification ou vérification)</p></td>
<td><p>HubTransport</p></td>
<td><p>CrashEvent.msexchangetransportlogsearch</p></td>
</tr>
<tr class="odd">
<td><p>aucun (notification ou vérification)</p></td>
<td><p>HubTransport</p></td>
<td><p>EdgeTransportBackpressureSustainedTimeMonitor</p></td>
</tr>
<tr class="even">
<td><p>aucun (notification ou vérification)</p></td>
<td><p>HubTransport</p></td>
<td><p>FederatedDecryptionAgentFailedToXDecryptMonitor</p></td>
</tr>
<tr class="odd">
<td><p>aucun (notification ou vérification)</p></td>
<td><p>HubTransport</p></td>
<td><p>HubTransport.ServiceInconsistentState.Monitor</p></td>
</tr>
<tr class="even">
<td><p>aucun (notification ou vérification)</p></td>
<td><p>HubTransport</p></td>
<td><p>IsMemberOfResolverExpandedGroupsCacheSizeMonitor</p></td>
</tr>
<tr class="odd">
<td><p>aucun (notification ou vérification)</p></td>
<td><p>HubTransport</p></td>
<td><p>IsMemberOfResolverResolvedGroupsCacheSizeMonitor</p></td>
</tr>
<tr class="even">
<td><p>aucun (notification ou vérification)</p></td>
<td><p>HubTransport</p></td>
<td><p>Messages.failed.to.be.made.redundant.Monitor</p></td>
</tr>
<tr class="odd">
<td><p>aucun (notification ou vérification)</p></td>
<td><p>HubTransport</p></td>
<td><p>MessagesDeferredDuringCategorizationMonitor</p></td>
</tr>
<tr class="even">
<td><p>aucun (notification ou vérification)</p></td>
<td><p>HubTransport</p></td>
<td><p>MessageTrackingLogsDirQuotaMonitor</p></td>
</tr>
<tr class="odd">
<td><p>aucun (notification ou vérification)</p></td>
<td><p>HubTransport</p></td>
<td><p>PrivateWorkingSetError.edgetransport</p></td>
</tr>
<tr class="even">
<td><p>aucun (notification ou vérification)</p></td>
<td><p>HubTransport</p></td>
<td><p>PrivateWorkingSetError.msexchahangetransportlogsearch</p></td>
</tr>
<tr class="odd">
<td><p>aucun (notification ou vérification)</p></td>
<td><p>HubTransport</p></td>
<td><p>PrivateWorkingSetError.msexchangethrottling</p></td>
</tr>
<tr class="even">
<td><p>aucun (notification ou vérification)</p></td>
<td><p>HubTransport</p></td>
<td><p>PrivateWorkingSetError.msexchangetransport</p></td>
</tr>
<tr class="odd">
<td><p>aucun (notification ou vérification)</p></td>
<td><p>HubTransport</p></td>
<td><p>PrivateWorkingSetWarning.edgetransport</p></td>
</tr>
<tr class="even">
<td><p>aucun (notification ou vérification)</p></td>
<td><p>HubTransport</p></td>
<td><p>PrivateWorkingSetWarning.msexchangethrottling</p></td>
</tr>
<tr class="odd">
<td><p>aucun (notification ou vérification)</p></td>
<td><p>HubTransport</p></td>
<td><p>PrivateWorkingSetWarning.msexchangetransport</p></td>
</tr>
<tr class="even">
<td><p>aucun (notification ou vérification)</p></td>
<td><p>HubTransport</p></td>
<td><p>PrivateWorkingSetWarning.msexchangetransportlogsearch</p></td>
</tr>
<tr class="odd">
<td><p>aucun (notification ou vérification)</p></td>
<td><p>HubTransport</p></td>
<td><p>ProcessProcessorTimeError.edgetransport</p></td>
</tr>
<tr class="even">
<td><p>aucun (notification ou vérification)</p></td>
<td><p>HubTransport</p></td>
<td><p>ProcessProcessorTimeError.msexchangethrottling</p></td>
</tr>
<tr class="odd">
<td><p>aucun (notification ou vérification)</p></td>
<td><p>HubTransport</p></td>
<td><p>ProcessProcessorTimeError.msexchangetransport</p></td>
</tr>
<tr class="even">
<td><p>aucun (notification ou vérification)</p></td>
<td><p>HubTransport</p></td>
<td><p>ProcessProcessorTimeError.msexchangetransportlogsearch</p></td>
</tr>
<tr class="odd">
<td><p>aucun (notification ou vérification)</p></td>
<td><p>HubTransport</p></td>
<td><p>ProcessProcessorTimeWarning.edgetransport</p></td>
</tr>
<tr class="even">
<td><p>aucun (notification ou vérification)</p></td>
<td><p>HubTransport</p></td>
<td><p>ProcessProcessorTimeWarning.msexchangethrottling</p></td>
</tr>
<tr class="odd">
<td><p>aucun (notification ou vérification)</p></td>
<td><p>HubTransport</p></td>
<td><p>ProcessProcessorTimeWarning.msexchangetransport</p></td>
</tr>
<tr class="even">
<td><p>aucun (notification ou vérification)</p></td>
<td><p>HubTransport</p></td>
<td><p>ProcessProcessorTimeWarning.msexchangetransportlogsearch</p></td>
</tr>
<tr class="odd">
<td><p>aucun (notification ou vérification)</p></td>
<td><p>HubTransport</p></td>
<td><p>QueueExternalAggregateMonitor</p></td>
</tr>
<tr class="even">
<td><p>aucun (notification ou vérification)</p></td>
<td><p>HubTransport</p></td>
<td><p>QueueInternalAggregateMonitor</p></td>
</tr>
<tr class="odd">
<td><p>aucun (notification ou vérification)</p></td>
<td><p>HubTransport</p></td>
<td><p>QueueInternalAggregateNormalPriorityMonitor</p></td>
</tr>
<tr class="even">
<td><p>aucun (notification ou vérification)</p></td>
<td><p>HubTransport</p></td>
<td><p>QueueInternalHubRetryMonitor</p></td>
</tr>
<tr class="odd">
<td><p>aucun (notification ou vérification)</p></td>
<td><p>HubTransport</p></td>
<td><p>QueueInternalHubRetryNormalPriorityMonitor</p></td>
</tr>
<tr class="even">
<td><p>aucun (notification ou vérification)</p></td>
<td><p>HubTransport</p></td>
<td><p>QueueMailboxRetryMonitor</p></td>
</tr>
<tr class="odd">
<td><p>aucun (notification ou vérification)</p></td>
<td><p>HubTransport</p></td>
<td><p>QueueNonSMTPRetryMonitor</p></td>
</tr>
<tr class="even">
<td><p>aucun (notification ou vérification)</p></td>
<td><p>HubTransport</p></td>
<td><p>RuleEvaluationFailureEventLogMonitor</p></td>
</tr>
<tr class="odd">
<td><p>aucun (notification ou vérification)</p></td>
<td><p>HubTransport</p></td>
<td><p>RuleEvaluationIgnoredFailureEventLogMonitor</p></td>
</tr>
<tr class="even">
<td><p>aucun (notification ou vérification)</p></td>
<td><p>HubTransport</p></td>
<td><p>RuleEvaluationIgnoredFipsFailureEventLogMonitor</p></td>
</tr>
<tr class="odd">
<td><p>aucun (notification ou vérification)</p></td>
<td><p>HubTransport</p></td>
<td><p>RuleEvaluationSmallScaleFailureEventLogMonitor</p></td>
</tr>
<tr class="even">
<td><p>aucun (notification ou vérification)</p></td>
<td><p>HubTransport</p></td>
<td><p>RuleEvaluationSmallScaleFipsFailureEventLogMonitor</p></td>
</tr>
<tr class="odd">
<td><p>aucun (notification ou vérification)</p></td>
<td><p>HubTransport</p></td>
<td><p>RuleExcessiveForkingEventLogMonitor</p></td>
</tr>
<tr class="even">
<td><p>aucun (notification ou vérification)</p></td>
<td><p>HubTransport</p></td>
<td><p>RuleLoadFailureEventLogMonitor</p></td>
</tr>
<tr class="odd">
<td><p>aucun (notification ou vérification)</p></td>
<td><p>HubTransport</p></td>
<td><p>RuleLoadSmallScaleFailureEventLogMonitor</p></td>
</tr>
<tr class="even">
<td><p>aucun (notification ou vérification)</p></td>
<td><p>HubTransport</p></td>
<td><p>SmtpProxyEhloOptionsDoNotMatchContinueProxyingMonitor</p></td>
</tr>
<tr class="odd">
<td><p>aucun (notification ou vérification)</p></td>
<td><p>HubTransport</p></td>
<td><p>SubmissionQueueMonitor</p></td>
</tr>
<tr class="even">
<td><p>aucun (notification ou vérification)</p></td>
<td><p>HubTransport</p></td>
<td><p>TlsDomainClientCertificateSubjectMismatchMonitor</p></td>
</tr>
<tr class="odd">
<td><p>aucun (notification ou vérification)</p></td>
<td><p>HubTransport</p></td>
<td><p>Total.Shadow.Queue.Length.Above.Threshold.Monitor</p></td>
</tr>
<tr class="even">
<td><p>aucun (notification ou vérification)</p></td>
<td><p>HubTransport</p></td>
<td><p>TotalE2ELatencyHighForMSExchangeTransportMonitor</p></td>
</tr>
<tr class="odd">
<td><p>aucun (notification ou vérification)</p></td>
<td><p>HubTransport</p></td>
<td><p>TotalE2ELatencyLowForMSExchangeTransportMonitor</p></td>
</tr>
<tr class="even">
<td><p>aucun (notification ou vérification)</p></td>
<td><p>HubTransport</p></td>
<td><p>TotalE2ELatencyNormalForMSExchangeTransportMonitor</p></td>
</tr>
<tr class="odd">
<td><p>aucun (notification ou vérification)</p></td>
<td><p>HubTransport</p></td>
<td><p>Transport.CatExpiry.Monitor</p></td>
</tr>
<tr class="even">
<td><p>aucun (notification ou vérification)</p></td>
<td><p>HubTransport</p></td>
<td><p>Transport.Critical.Storage.Recovery.Failed.Monitor</p></td>
</tr>
<tr class="odd">
<td><p>aucun (notification ou vérification)</p></td>
<td><p>HubTransport</p></td>
<td><p>Transport.DatabaseMoved.Monitor</p></td>
</tr>
<tr class="even">
<td><p>aucun (notification ou vérification)</p></td>
<td><p>HubTransport</p></td>
<td><p>Transport.DomainSecureCert.Monitor</p></td>
</tr>
<tr class="odd">
<td><p>aucun (notification ou vérification)</p></td>
<td><p>HubTransport</p></td>
<td><p>Transport.DomainSecureCertAuth.Monitor</p></td>
</tr>
<tr class="even">
<td><p>aucun (notification ou vérification)</p></td>
<td><p>HubTransport</p></td>
<td><p>Transport.DomainSecureServerCertFailed.Monitor</p></td>
</tr>
<tr class="odd">
<td><p>aucun (notification ou vérification)</p></td>
<td><p>HubTransport</p></td>
<td><p>Transport.DomainSecureServerDomainCertFailed.Monitor</p></td>
</tr>
<tr class="even">
<td><p>aucun (notification ou vérification)</p></td>
<td><p>HubTransport</p></td>
<td><p>Transport.FailedToCreatePickupDirectory.Monitor</p></td>
</tr>
<tr class="odd">
<td><p>aucun (notification ou vérification)</p></td>
<td><p>HubTransport</p></td>
<td><p>Transport.InvalidAcceptedDomain.Monitor</p></td>
</tr>
<tr class="even">
<td><p>aucun (notification ou vérification)</p></td>
<td><p>HubTransport</p></td>
<td><p>Transport.LowDiskSpace.Monitor</p></td>
</tr>
<tr class="odd">
<td><p>aucun (notification ou vérification)</p></td>
<td><p>HubTransport</p></td>
<td><p>Transport.Messages.Completing.Categorization.Monitor</p></td>
</tr>
<tr class="even">
<td><p>aucun (notification ou vérification)</p></td>
<td><p>HubTransport</p></td>
<td><p>Transport.NDRForUnrestrictedLargeDL.Monitor</p></td>
</tr>
<tr class="odd">
<td><p>aucun (notification ou vérification)</p></td>
<td><p>HubTransport</p></td>
<td><p>Transport.PickupDelete.Monitor</p></td>
</tr>
<tr class="even">
<td><p>aucun (notification ou vérification)</p></td>
<td><p>HubTransport</p></td>
<td><p>Transport.PickupIsBadmailingFile.Monitor</p></td>
</tr>
<tr class="odd">
<td><p>aucun (notification ou vérification)</p></td>
<td><p>HubTransport</p></td>
<td><p>Transport.SendConn.AuthKerb.Monitor</p></td>
</tr>
<tr class="even">
<td><p>aucun (notification ou vérification)</p></td>
<td><p>HubTransport</p></td>
<td><p>Transport.SendConnAuth.Monitor</p></td>
</tr>
<tr class="odd">
<td><p>aucun (notification ou vérification)</p></td>
<td><p>HubTransport</p></td>
<td><p>Transport.SendConnTLS.Monitor</p></td>
</tr>
<tr class="even">
<td><p>aucun (notification ou vérification)</p></td>
<td><p>HubTransport</p></td>
<td><p>Transport.ServerCertExpireSoon.Monitor</p></td>
</tr>
<tr class="odd">
<td><p>aucun (notification ou vérification)</p></td>
<td><p>HubTransport</p></td>
<td><p>Transport.ServerCertMismatch.Monitor</p></td>
</tr>
<tr class="even">
<td><p>aucun (notification ou vérification)</p></td>
<td><p>HubTransport</p></td>
<td><p>Transport.ServiceStartError.Monitor</p></td>
</tr>
<tr class="odd">
<td><p>aucun (notification ou vérification)</p></td>
<td><p>HubTransport</p></td>
<td><p>Transport.SmtpSendDirectTrustFailed.Monitor</p></td>
</tr>
<tr class="even">
<td><p>aucun (notification ou vérification)</p></td>
<td><p>HubTransport</p></td>
<td><p>Transport.TemplateDoesNotExist.Monitor</p></td>
</tr>
<tr class="odd">
<td><p>aucun (notification ou vérification)</p></td>
<td><p>HubTransport</p></td>
<td><p>Transport.TLSValidate.Monitor</p></td>
</tr>
<tr class="even">
<td><p>aucun (notification ou vérification)</p></td>
<td><p>HubTransport</p></td>
<td><p>Transport.UnknownTemplateInPublishingLicense.Monitor</p></td>
</tr>
<tr class="odd">
<td><p>aucun (notification ou vérification)</p></td>
<td><p>HubTransport</p></td>
<td><p>TransportCategorizerJobAvailabilityMonitor</p></td>
</tr>
<tr class="even">
<td><p>aucun (notification ou vérification)</p></td>
<td><p>HubTransport</p></td>
<td><p>TransportDatabaseCorruptMonitor</p></td>
</tr>
<tr class="odd">
<td><p>aucun (notification ou vérification)</p></td>
<td><p>HubTransport</p></td>
<td><p>TransportDeliveryFailures544Monitor</p></td>
</tr>
<tr class="even">
<td><p>aucun (notification ou vérification)</p></td>
<td><p>HubTransport</p></td>
<td><p>TransportDeliveryFailuresDeliveryStoreDriver520Monitor</p></td>
</tr>
<tr class="odd">
<td><p>aucun (notification ou vérification)</p></td>
<td><p>HubTransport</p></td>
<td><p>TransportLogGenerationCheckpointDepthMonitor</p></td>
</tr>
<tr class="even">
<td><p>aucun (notification ou vérification)</p></td>
<td><p>HubTransport</p></td>
<td><p>TransportLogSearchLogPathInvalidMonitor</p></td>
</tr>
<tr class="odd">
<td><p>aucun (notification ou vérification)</p></td>
<td><p>HubTransport</p></td>
<td><p>TransportMaxLocalLoopCountMonitor</p></td>
</tr>
<tr class="even">
<td><p>aucun (notification ou vérification)</p></td>
<td><p>HubTransport</p></td>
<td><p>TransportPickupReadMonitor</p></td>
</tr>
<tr class="odd">
<td><p>aucun (notification ou vérification)</p></td>
<td><p>HubTransport</p></td>
<td><p>TransportPoisonMessageMonitor</p></td>
</tr>
<tr class="even">
<td><p>aucun (notification ou vérification)</p></td>
<td><p>HubTransport</p></td>
<td><p>TransportRejectingMessageSubmissionsMonitor</p></td>
</tr>
<tr class="odd">
<td><p>aucun (notification ou vérification)</p></td>
<td><p>HubTransport</p></td>
<td><p>TransportServerCertPersonalStoreMonitor</p></td>
</tr>
<tr class="even">
<td><p>aucun (notification ou vérification)</p></td>
<td><p>HubTransport</p></td>
<td><p>UnreachableQueueMonitor</p></td>
</tr>
<tr class="odd">
<td><p>aucun (notification ou vérification)</p></td>
<td><p>HubTransport</p></td>
<td><p>XProxyToTransientInvalidArgumentsMonitor</p></td>
</tr>
</tbody>
</table>


Pour plus d’informations sur les sondes et les moniteurs, consultez la rubrique [État et performances du serveur](https://technet.microsoft.com/fr-fr/library/jj150551\(v=exchg.150\)).

## Action de l’utilisateur

Il se peut que le service ait récupéré après avoir émis l’alerte. Par conséquent, quand vous recevez une alerte signalant que le jeu d’intégrité **HubTransport** n’est pas intègre, vérifiez tout d’abord que le problème existe toujours. Si tel est le cas, exécutez les actions de récupération appropriées décrites dans la section suivante.

## Vérification du problème

1.  Repérez le nom de l’indicateur d’intégrité et celui du serveur dans l’alerte.

2.  Les détails du message fournissent des informations sur la cause exacte de l’alerte. Dans la plupart des cas, ils fournissent des informations de dépannage suffisantes pour identifier la cause première. Si les détails du message ne sont pas clairs, procédez comme suit :
    
    1.  Ouvrez Environnement de ligne de commande Exchange Management Shell, puis exécutez la commande suivante pour récupérer les détails de l’indicateur d’intégrité qui a émis l’alerte :
        
            Get-ServerHealth <server name> | ?{$_.HealthSetName -eq "<health set name>"}
        
        Par exemple, pour extraire les détails du jeu d’intégrité **HubTransport** à propos de mailbox1.contoso.com, exécutez la commande suivante :
        
            Get-ServerHealth mailbox1.contoso.com | ?{$_.HealthSetName -eq "HubTransport"}
    
    2.  Consultez la sortie de la commande pour déterminer le moniteur qui a signalé l’erreur. La valeur **AlertValue** du moniteur qui a émis l’alerte sera **Unhealthy**.
    
    3.  Réexécutez la sonde associée pour le moniteur dont l’état d’intégrité est défectueux. Pour rechercher la sonde associée, reportez-vous au tableau figurant dans la section [Explanation](troubleshooting-activesync-health-set.md). Pour ce faire, exécutez la commande suivante :
        
            Invoke-MonitoringProbe <health set name>\<probe name> -Server <server name> | Format-List
        
        Par exemple, supposons que le moniteur défectueux soit **ActiveQueueDrainFailureMonitor**. La sonde associée à ce moniteur est **ActiveQueueDrainFailureProbe**. Pour exécuter cette sonde sur mailbox1.contoso.com, exécutez la commande suivante :
        
            Invoke-MonitoringProbe HubTransport\ActiveQueueDrainFailureProbe -Server mailbox1.contoso.com | Format-List
    
    4.  Dans la sortie de la commande, consultez la section « Result » de la sonde. Si elle indique **Succeeded**, le problème était une erreur passagère, qui n’existe plus.

