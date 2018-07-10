---
title: Dépannage de l'indicateur d'intégrité UM.Protocol
TOCTitle: Dépannage de l'indicateur d'intégrité UM.Protocol
ms:assetid: 8dd9a16f-77a1-4a8d-aea4-5e96ab922dd4
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/ms.exch.scom.um.protocol(v=EXCHG.150)
ms:contentKeyID: 53276473
ms.date: 02/05/2016
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Dépannage de l'indicateur d'intégrité UM.Protocol

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2015-03-09_

L'indicateur d'intégrité UM.Protocol surveille le protocole de messagerie unifiée sur le serveur de boîtes aux lettres.

Si vous recevez une alerte indiquant qu'UM.Protocol présente un manque d'intégrité, cela signifie qu'un problème empêche probablement les utilisateurs d'utiliser le service de messagerie unifiée de votre organisation. L'indicateur d'intégrité UM.Protocol est étroitement lié aux indicateurs d'intégrité suivants :

[Dépannage de l'indicateur d'intégrité UM](troubleshooting-um-health-set.md)

[Dépannage de l'indicateur d'intégrité UM.CallRouter](troubleshooting-um-callrouter-health-set.md)

## Explication

Le service de protocole de messagerie unifiée est surveillé à l'aide des sondes et moniteurs suivants.


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
<td><p>UMSelfTestProbe</p></td>
<td><p>UM.Protocol</p></td>
<td><p>Services de domaine Active Directory (AD DS)</p></td>
<td><p>UMSelfTestMonitor</p></td>
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
        
        Par exemple, pour récupérer les détails de l'ensemble d'intégrité d'UM.Protocol à propos de server1.contoso.com, exécutez la commande suivante :
        
            Get-ServerHealth server1.contoso.com | ?{$_.HealthSetName -eq "UM.Protocol"}
    
    2.  Consultez la sortie de la commande pour déterminer quel moniteur a signalé l'erreur. La valeur **AlertValue** du moniteur qui a émis l'alerte sera `Unhealthy`.
    
    3.  Réexécutez la sonde associée pour le moniteur dont l’état d’intégrité est défectueux. Pour rechercher la sonde associée, reportez-vous au tableau figurant dans la section Explanation. Pour ce faire, exécutez la commande suivante :
        
            Invoke-MonitoringProbe <health set name>\<probe name> -Server <server name> | Format-List
        
        Par exemple, supposons que le moniteur défectueux soit **UMSelfTestMonitor**. La sonde associée à ce moniteur est **UMSelfTestProbe**. Pour exécuter cette sonde sur server1.contoso.com, exécutez la commande suivante :
        
            Invoke-MonitoringProbe UM.Protocol\UMSelfTestMonitor -Server server1.contoso.com | Format-List
    
    4.  Dans la sortie de la commande, consultez la valeur **Result** de la sonde. Si elle indique **Succeeded**, le problème était une erreur passagère, qui n'existe plus. Autrement, reportez-vous aux étapes de récupération décrites dans les sections suivantes.

## Étapes de résolution des problèmes

Quand vous recevez une alerte de l'indicateur d'intégrité, le message électronique contient les informations suivantes :

  - nom du serveur ayant envoyé l'alerte ;

  - heure et date de l'alerte ;

  - mécanisme d'authentification utilisé et informations d'identification ;

  - trace d'exception complète de la dernière erreur, notamment données de diagnostic et informations d'en-tête HTTP spécifiques.
    
    **Remarque**   Vous pouvez utiliser les informations contenues dans la trace de l'exception complète pour résoudre le problème. L'exception générée par la sonde contient un motif de l'échec qui décrit pourquoi la sonde a échoué.

Pour plus d'informations sur la résolution des problèmes liés aux messages d'alerte de la messagerie unifiée, consultez la rubrique [Dépannage de l'indicateur d'intégrité UM](troubleshooting-um-health-set.md).

## Pour plus d'informations

[Nouveautés d'Exchange 2013](https://technet.microsoft.com/fr-fr/library/jj150540\(v=exchg.150\))

[Cmdlets Exchange 2013](https://technet.microsoft.com/fr-fr/library/bb124413\(v=exchg.150\))

