---
title: Dépannage de l'indicateur d'intégrité UM.CallRouter
TOCTitle: Dépannage de l'indicateur d'intégrité UM.CallRouter
ms:assetid: 444a9038-0952-4823-98fb-99fa59f4a378
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/ms.exch.scom.um.callrouter(v=EXCHG.150)
ms:contentKeyID: 53276464
ms.date: 02/05/2016
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Dépannage de l'indicateur d'intégrité UM.CallRouter

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2015-03-09_

L'indicateur d'intégrité du routeur d'appels de messagerie unifiée Microsoft Exchange contrôle l'intégrité globale du service de routeur d'appels de messagerie unifiée.

Si vous recevez une alerte indiquant que la messagerie unifiée présente un manque d'intégrité, cela signifie qu'un problème empêche probablement les utilisateurs d'utiliser le service de messagerie unifiée de votre organisation. L'indicateur d'intégrité de la messagerie unifiée est étroitement lié aux indicateurs d'intégrité suivants :

[Dépannage de l'indicateur d'intégrité UM](troubleshooting-um-health-set.md)

[Dépannage de l'indicateur d'intégrité UM.Protocol](troubleshooting-um-protocol-health-set.md)

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
        
        Par exemple, pour récupérer les détails de l'indicateur d'intégrité UM.CallRouter à propos de server1.contoso.com, exécutez la commande suivante :
        
            Get-ServerHealth server1.contoso.com | ?{$_.HealthSetName -eq "UM.CallRouter"}
    
    2.  Consultez la sortie de la commande pour déterminer quel moniteur a signalé l'erreur. La valeur **AlertValue** du moniteur qui a émis l'alerte sera `Unhealthy`.
    
    3.  Réexécutez la sonde associée pour le moniteur dont l'état n'est pas intègre. Pour rechercher la sonde associée, reportez-vous au tableau figurant dans la section Explanation. Pour ce faire, exécutez la commande suivante :
        
            Invoke-MonitoringProbe <health set name>\<probe name> -Server <server name> | Format-List
        
        Par exemple, supposons que le moniteur défectueux soit **UMCallRouterTestMonitor**. La sonde associée à ce moniteur est **UMCallRouterTestProbe**. Pour exécuter cette sonde sur server1.contoso.com, exécutez la commande suivante :
        
            Invoke-MonitoringProbe UM.CallRouter\UMCallRouterTestMonitor -Server server1.contoso.com | Format-List
    
    4.  Dans la sortie de la commande, consultez la valeur **Result** de la sonde. Si elle indique **Succeeded**, le problème était une erreur passagère, qui n'existe plus. Autrement, reportez-vous aux étapes de récupération décrites dans les sections suivantes.

## Étapes de résolution des problèmes

Quand vous recevez une alerte de l'indicateur d'intégrité, le message électronique contient les informations suivantes :

  - nom du serveur ayant envoyé l'alerte ;

  - heure et date de l'alerte ;

  - mécanisme d'authentification utilisé et informations d'identification ;

  - trace d'exception complète de la dernière erreur, notamment données de diagnostic et informations d'en-tête HTTP spécifiques.
    
    **Remarque**   Vous pouvez utiliser les informations contenues dans la trace de l'exception complète pour résoudre le problème. L'exception générée par la sonde contient un motif de l'échec qui décrit pourquoi la sonde a échoué.

**Les options SIP vers le service routeur d'appels de messagerie unifiée ont échoué**

Déterminez si le service routeur d'appels de messagerie unifiée est désactivé. Si le service routeur d'appels de messagerie unifiée n'est pas démarré ou activé, redémarrez le service de messagerie unifiée.

**Plus de 50 % des appels entrants ont été rejetés par le routeur d'appels de messagerie unifiée au cours de la dernière heure**

Consultez les journaux d'événement sur le serveur d'accès au client afin de déterminer si les objets de messagerie unifiée, tels que **umipgateway** et **umhuntgroup**, sont configurés correctement.

Si les journaux d'événement ne contiennent pas assez d'informations, vous devez peut-être activer les journaux d'événements de messagerie unifiée au niveau Expert, puis consulter les fichiers journaux des traces de messagerie unifiée.

**Plus de {0} % du proxy de notification d'appel en absence ont échoué sur le routeur d'appels de messagerie unifiée au cours de la dernière heure**

Consultez les journaux d'événement sur le serveur d'accès au client afin de déterminer si les objets de messagerie unifiée, tels que **umipgateway** et **umhuntgroup**, sont configurés correctement.

Si les journaux d'événement ne contiennent pas assez d'informations, vous devez peut-être activer les journaux d'événements de messagerie unifiée au niveau Expert, puis consulter les fichiers journaux des traces de messagerie unifiée.

**La date d'expiration du certificat du routeur d'appels de messagerie unifiée Microsoft Exchange est proche.**

Renouvelez le certificat du service routeur d'appels de messagerie unifiée sur le serveur d'accès au client.

**Étapes de résolution des problèmes supplémentaires :** 

1.  Démarrez le Gestionnaire des services Internet, puis connectez-vous au serveur signalant le problème afin de déterminer si le pool d’applications **MSExchangeServicesAppPool** est en cours d’exécution.

2.  Dans le Gestionnaire des services Internet, cliquez sur **Pools d'applications**, puis recyclez le pool d'applications **MSExchangeServicesAppPool** en exécutant la commande suivante à partir de l'environnement de ligne de commande Exchange Management Shell :
    
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

