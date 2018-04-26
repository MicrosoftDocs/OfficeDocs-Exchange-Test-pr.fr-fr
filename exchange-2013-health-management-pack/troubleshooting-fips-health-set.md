---
title: Dépannage de l’indicateur d’intégrité FIPS
TOCTitle: Dépannage de l’indicateur d’intégrité FIPS
ms:assetid: 96e1b096-9cb5-426f-a84e-50d5599e4bbb
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/ms.exch.scom.fips(v=EXCHG.150)
ms:contentKeyID: 54652811
ms.date: 10/08/2015
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Dépannage de l’indicateur d’intégrité FIPS

 

_**Sapplique à :**Exchange Server 2013, Project Server 2013_

_**Dernière rubrique modifiée :**2015-03-09_

L’indicateur d’intégrité **FIPS** surveille l’intégrité globale des paramètres des normes FIPS (Federal Information Processing Standard) sur des serveurs Exchange. Pour plus d’informations sur les normes FIPS 140, consultez la rubrique [Validation des normes FIPS 140](http://go.microsoft.com/fwlink/p/?linkid=521913).

Une alerte vous informant que l’intégrité **FIPS** est défectueuse indique un problème qui peut empêcher votre serveur Exchange d’utiliser des processus et des composants conformes aux normes FIPS 140.

## Explication

Le service **FIPS** est surveillé à l’aide des sondes et moniteurs suivants :


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
<td><p>aucun (notification ou vérification)</p></td>
<td><p>FIPS</p></td>
<td><p>CrashEvent.scanningprocess</p></td>
</tr>
<tr class="even">
<td><p>aucun (notification ou vérification)</p></td>
<td><p>FIPS</p></td>
<td><p>MaintenanceFailureMonitor.FIPS</p></td>
</tr>
<tr class="odd">
<td><p>aucun (notification ou vérification)</p></td>
<td><p>FIPS</p></td>
<td><p>MaintenanceTimeoutMonitor.FIPS</p></td>
</tr>
<tr class="even">
<td><p>aucun (notification ou vérification)</p></td>
<td><p>FIPS</p></td>
<td><p>PrivateWorkingSetWarning.scanningprocess</p></td>
</tr>
<tr class="odd">
<td><p>aucun (notification ou vérification)</p></td>
<td><p>FIPS</p></td>
<td><p>PrivateWorkingSetError.scanningprocess</p></td>
</tr>
<tr class="even">
<td><p>aucun (notification ou vérification)</p></td>
<td><p>FIPS</p></td>
<td><p>ProcessProcessorTimeWarning.scanningprocess</p></td>
</tr>
<tr class="odd">
<td><p>aucun (notification ou vérification)</p></td>
<td><p>FIPS</p></td>
<td><p>ProcessProcessorTimeError.scanningprocess</p></td>
</tr>
</tbody>
</table>


Pour plus d’informations sur les sondes et les moniteurs, consultez la rubrique [État et performances du serveur](https://technet.microsoft.com/fr-fr/library/jj150551\(v=exchg.150\)).

## Action de l’utilisateur

Il se peut que le service ait récupéré après avoir émis l’alerte. Par conséquent, quand vous recevez une alerte signalant que l’indicateur d’intégrité **FIPS** est défectueux, vérifiez tout d’abord que le problème existe toujours. Si tel est le cas, exécutez les actions de récupération appropriées décrites dans la section suivante.

## Vérification du problème

1.  Repérez le nom de l’indicateur d’intégrité et celui du serveur dans l’alerte.

2.  Les détails du message fournissent des informations sur la cause exacte de l’alerte. Dans la plupart des cas, ils fournissent des informations de dépannage suffisantes pour identifier la cause première. Si les détails du message ne sont pas clairs, procédez comme suit :
    
    1.  Ouvrez Environnement de ligne de commande Exchange Management Shell, puis exécutez la commande suivante pour récupérer les détails de l’indicateur d’intégrité qui a émis l’alerte :
        
            Get-ServerHealth <server name> | ?{$_.HealthSetName -eq "<health set name>"}
        
        Par exemple, pour récupérer les détails de l’indicateur d’intégrité **FIPS** à propos de server1.contoso.com, exécutez la commande suivante :
        
            Get-ServerHealth server1.contoso.com | ?{$_.HealthSetName -eq "FIPS"}
    
    2.  Consultez la sortie de la commande pour déterminer le moniteur qui a signalé l’erreur. La valeur **AlertValue** du moniteur qui a émis l’alerte sera **Unhealthy**.

