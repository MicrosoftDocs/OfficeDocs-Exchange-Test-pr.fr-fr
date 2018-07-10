---
title: Dépannage de l'indicateur d'intégrité UM
TOCTitle: Dépannage de l'indicateur d'intégrité UM
ms:assetid: db947791-63ce-45dd-8634-1dfa5f55e2c2
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/ms.exch.scom.um(v=EXCHG.150)
ms:contentKeyID: 53276481
ms.date: 02/05/2016
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Dépannage de l'indicateur d'intégrité UM

 

_**Sapplique à :** Exchange Server 2013, Project Server 2013_

_**Dernière rubrique modifiée :** 2015-03-09_

L'indicateur d'intégrité de messagerie unifiée surveille l'intégrité globale du service de messagerie unifiée de votre organisation.

Si vous recevez une alerte indiquant que la messagerie unifiée présente un manque d'intégrité, cela signifie qu'un problème empêche probablement les utilisateurs d'utiliser le service de messagerie unifiée de votre organisation. L'indicateur d'intégrité de la messagerie unifiée est étroitement lié aux indicateurs d'intégrité suivants :

[Dépannage de l'indicateur d'intégrité UM.CallRouter](troubleshooting-um-callrouter-health-set.md)

[Dépannage de l'indicateur d'intégrité UM.Protocol](troubleshooting-um-protocol-health-set.md)

## Explication

Le service de messagerie unifiée est contrôlé à l'aide des sondes et moniteurs suivants.


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
<tr class="even">
<td><p>UMCallRouterTestProbe</p></td>
<td><p>UM.CallRouter</p></td>
<td><p>Services de domaine Active Directory (AD DS)</p></td>
<td><p>UMCallRouterTestMonitor</p></td>
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
    
    3.  Réexécutez la sonde associée pour le moniteur dont l'état n'est pas intègre. Pour rechercher la sonde associée, reportez-vous au tableau figurant dans la section Explanation. Pour ce faire, exécutez la commande suivante :
        
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

**Les options SIP vers le service de messagerie unifiée ont échoué**

Déterminez si le service de messagerie unifiée est désactivé. Si le service de messagerie unifiée n'est pas démarré ou est désactivé, redémarrez le service de messagerie unifiée.

**Plus de {0} % des appels entrants ont été rejetés par le service de messagerie unifiée au cours de la dernière heure**

Consultez les journaux d'événement sur le serveur d'accès au client afin de déterminer si les objets de messagerie unifiée, tels que **umipgateway** et **umhuntgroup**, sont configurés correctement.

Si les journaux d'événement ne contiennent pas assez d'informations, vous devez peut-être activer les journaux d'événements de messagerie unifiée au niveau Expert, puis consulter les fichiers journaux des traces de messagerie unifiée.

**Plus de {0} % des appels entrants ont été rejetés par le processus de travail de messagerie unifiée au cours de la dernière heure**

Consultez les journaux d'événement sur le serveur d'accès au client afin de déterminer si les objets de messagerie unifiée, tels que **umipgateway** et **umhuntgroup**, sont configurés correctement.

Si les journaux d'événement ne contiennent pas assez d'informations, vous devez peut-être activer les journaux d'événements de messagerie unifiée au niveau Expert, puis consulter les fichiers journaux des traces de messagerie unifiée.

**moins de {0} % des messages ont été correctement traités au cours de la dernière heure**

Consultez les journaux d'événement sur le serveur d'accès au client afin de déterminer si les objets de messagerie unifiée, tels que **umipgateway** et **umhuntgroup**, sont configurés correctement.

Si les journaux d'événement ne contiennent pas assez d'informations, vous devez peut-être activer les journaux d'événements de messagerie unifiée au niveau Expert, puis consulter les fichiers journaux des traces de messagerie unifiée.

**Le service de messagerie unifiée Microsoft Exchange a rejeté un appel car le pipeline de la messagerie unifiée est plein.**

Consultez les journaux d'événement sur le serveur d'accès au client afin de déterminer si les objets de messagerie unifiée, tels que **umipgateway** et **umhuntgroup**, sont configurés correctement.

Si les journaux d'événement ne contiennent pas assez d'informations, vous devez peut-être activer les journaux d'événements de messagerie unifiée au niveau Expert, puis consulter les fichiers journaux des traces de messagerie unifiée.

**Le service Edge A/V n'est pas configuré correctement ou n'est pas en cours d'exécution**

1.  Consultez les journaux d'événement sur le serveur de boîtes aux lettres pour tenter de déterminer pourquoi les appels du serveur Lync échouent. Ensuite, procédez comme suit :
    
      - Vérifiez que le pool Lync sélectionné par le service de messagerie unifiée est opérationnel.
    
      - Pour utiliser un serveur Lync particulier, exécutez la commande suivante :
        
            Set-UMServer ExchangeUMServer -SIPAccessService <ServerName>

**Le serveur de messagerie unifiée n'a pas pu obtenir les informations d'identification auprès du service Edge A/V Communications Server.**

Consultez les journaux d'événement pour identifier le pool Lync sélectionné et vérifier qu'il est opérationnel.

**Le serveur Edge Audio/Vidéo Communications Server n'a pas pu ouvrir un port ou allouer des ressources lors de la tentative d'établissement d'une session.**

Consultez les journaux d'événement pour identifier le pool Lync sélectionné et vérifier qu'il est opérationnel.

**La date d'expiration du certificat du service de messagerie unifiée Microsoft Exchange est proche.**

Renouvelez le certificat du service de messagerie unifiée sur le serveur de boîtes aux lettres.

**Étapes de résolution des problèmes supplémentaires :** 

1.  Démarrez le Gestionnaire des services Internet, puis connectez-vous au serveur signalant le problème afin de déterminer si le pool d’applications **MSExchangeServicesAppPool** est en cours d’exécution.

2.  Dans le Gestionnaire des services Internet, cliquez sur **Pools d'applications**, puis recyclez le pool d'applications **MSExchangeServicesAppPool**. Pour ce faire, exécutez la commande suivante à partir du Environnement de ligne de commande Exchange Management Shell :
    
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

