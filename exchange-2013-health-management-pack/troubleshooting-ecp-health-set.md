---
title: Dépannage de l'indicateur d'intégrité ECP
TOCTitle: Dépannage de l'indicateur d'intégrité ECP
ms:assetid: 0a1cfcd5-585c-4a0a-9d3c-28dc49e16a6c
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/ms.exch.scom.ecp(v=EXCHG.150)
ms:contentKeyID: 53276459
ms.date: 02/05/2016
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Dépannage de l'indicateur d'intégrité ECP

 

_**Sapplique à :**Exchange Server 2013, Project Server 2013_

_**Dernière rubrique modifiée :**2015-03-09_

L'indicateur d'intégrité du Panneau de configuration Exchange (ECP) surveille l'intégrité globale du Centre d'administration Exchange (CAE) et du service de paramètres utilisateur d'Outlook Web App (OWA). L'indicateur d'intégrité du Panneau de configuration Exchange est étroitement lié au suivant :

[Dépannage de l'indicateur d'intégrité ECP.Proxy](troubleshooting-ecp-proxy-health-set.md)

Si vous recevez une alerte signalant que l’indicateur d’intégrité du Panneau de configuration Exchange est défectueux, cela indique un problème qui peut empêcher les utilisateurs d’y accéder.

## Explication

Le service du CAE est surveillé à l'aide des sondes et moniteurs suivants.


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
<td><p>EacSelfTestProbe</p></td>
<td><p>ECP</p></td>
<td><p>Active Directory</p></td>
<td><p>EacSelfTestMonitor</p></td>
</tr>
<tr class="even">
<td><p>EacDeepTestProbe</p></td>
<td><p>ECP</p></td>
<td><p>Active Directory</p></td>
<td><p>EacDeepTestMonitor</p></td>
</tr>
</tbody>
</table>


Pour plus d'informations sur les sondes et les moniteurs, consultez la rubrique [État et performances du serveur](https://technet.microsoft.com/fr-fr/library/jj150551\(v=exchg.150\)).

## Action de l'utilisateur

Quand vous recevez une alerte de l'indicateur d'intégrité, le message électronique contient les informations suivantes :

  - nom du serveur ayant envoyé l'alerte ;

  - heure et date de l'alerte ;

  - informations d'authentification et d'identification ;

  - trace d’exception complète de la dernière erreur, notamment données de diagnostic et informations d’en-tête HTTP spécifiques
    
    **Remarque**   Vous pouvez utiliser les informations contenues dans la trace de l'exception complète pour résoudre le problème.

Il se peut que le service ait récupéré après avoir émis l'alerte. Par conséquent, quand vous recevez une alerte signalant que l'indicateur d'intégrité n'est pas intègre, vérifiez tout d'abord que le problème existe toujours. Si tel est le cas, exécutez les actions de récupération appropriées décrites dans les sections suivantes.

## Vérification de l'existence du problème

1.  Repérez les noms de l'indicateur d'intégrité et du serveur dans l'alerte.

2.  Les détails du message fournissent des informations sur la cause exacte de l'alerte. Le plus souvent, le message fournit des informations de dépannage suffisantes pour identifier la cause première. Si les détails du message ne sont pas clairs, procédez comme suit :
    
    1.  Ouvrez Environnement de ligne de commande Exchange Management Shell, puis exécutez la commande suivante pour récupérer les détails de l'indicateur d'intégrité qui a émis l'alerte :
        
            Get-ServerHealth -Identity <ServerName> -HealthSet <HealthSetName>
        
        Par exemple, pour récupérer les détails de l’indicateur d’intégrité concernant server1.contoso.com, exécutez la commande suivante :
        
            Get-ServerHealth -Identity server1.contoso.com -HealthSetName ECP
    
    2.  Consultez la sortie de la commande pour déterminer quel moniteur a signalé l'erreur. La valeur **AlertValue** du moniteur qui a émis l'alerte sera `Unhealthy`.
    
    3.  Réexécutez la sonde associée pour le moniteur dont l’état d’intégrité est défectueux. Pour rechercher la sonde associée, reportez-vous au tableau figurant dans la section Explanation. Pour ce faire, exécutez la commande suivante :
        
            Invoke-MonitoringProbe <HealthSetName>\<ProbeName> -Server <ServerName> | Format-List
        
        Par exemple, supposons que le moniteur défectueux soit **EacSelfTestMonitor**. La sonde associée à ce moniteur est **EacSelfTestProbe**. Pour exécuter cette sonde sur server1.contoso.com, exécutez la commande suivante :
        
            Invoke-MonitoringProbe ECP\EacSelfTestProbe -Server server1.contoso.com | Format-List
    
    4.  Dans la sortie de la commande, consultez la valeur **Result** de la sonde. Si elle indique **Succeeded**, le problème était une erreur passagère, qui n'existe plus. Autrement, reportez-vous aux étapes de récupération décrites dans les sections suivantes.

## Actions de récupération EacSelfTestMonitor et EacDeepTestMonitor

1.  Démarrez le Gestionnaire des services Internet et connectez-vous au serveur signalant le problème. Cliquez sur **Pools d’applications**, puis recyclez le pool d’applications de l’indicateur d’intégrité nommé **MSExchangeECPAppPool**.

2.  Réexécutez la sonde associée en procédant de la manière décrite dans l'étape 2c de la section Verifying the issue still exists.

3.  Si le problème persiste, recyclez la totalité du service IIS à l'aide de l'utilitaire IISReset.

4.  Réexécutez la sonde associée en procédant de la manière décrite dans l'étape 2c de la section Verifying the issue still exists.

5.  Si la sonde échoue, redémarrer le serveur.

6.  Une fois le serveur redémarré, réexécutez la sonde associée en procédant de la manière décrite dans l'étape 2c de la section Verifying the issue still exists.

7.  En cas de nouvel échec de la sonde, il se peut que vous ayez besoin d'aide pour résoudre ce problème. Contactez un professionnel du Support Technique de Microsoft pour résoudre ce problème. Pour contacter un professionnel du Support Technique de Microsoft, consultez [Exchange Server Solutions Center](http://go.microsoft.com/fwlink/p/?linkid=180809). Dans le volet de navigation, cliquez sur **Ressources et options de support** et utilisez l'une des options indiquées sous **Obtenez du support technique** pour contacter un professionnel du support Microsoft. Étant donné que votre organisation peut avoir une procédure spécifique pour contacter directement les Services de Support Technique Microsoft, assurez-vous de connaître d'abord les instructions propres à votre organisation.

## Pour plus d'informations

[Nouveautés d'Exchange 2013](https://technet.microsoft.com/fr-fr/library/jj150540\(v=exchg.150\))

[Cmdlets Exchange 2013](https://technet.microsoft.com/fr-fr/library/bb124413\(v=exchg.150\))

[Centre d’administration Exchange dans Exchange 2013](https://technet.microsoft.com/fr-fr/library/jj150562\(v=exchg.150\))

