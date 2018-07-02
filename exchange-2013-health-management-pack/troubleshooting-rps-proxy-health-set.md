---
title: Dépannage de l'indicateur d'intégrité RPS.Proxy
TOCTitle: Dépannage de l'indicateur d'intégrité RPS.Proxy
ms:assetid: a5058323-5d86-438a-ad4a-fa4292310e98
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/ms.exch.scom.rps.proxy(v=EXCHG.150)
ms:contentKeyID: 53276476
ms.date: 02/05/2016
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Dépannage de l'indicateur d'intégrité RPS.Proxy

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2015-03-09_

L'indicateur d'intégrité RPS.Proxy sur veille l'intégrité globale du service Remote PowerShell.

Si vous recevez une alerte signalant que RPS.Proxy n'est pas intègre, cela indique l'existence d'un problème qui pourrait vous empêcher d'utiliser Remote PowerShell pour accéder à Exchange.

## Explication

Le service RPS est surveillé à l'aide des sondes et moniteurs suivants :


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
<td><p>RPSProxyTestProbe</p></td>
<td><p>RPS.Proxy</p></td>
<td><p>Active Directory</p></td>
<td><p>RPSProxyTestMonitor</p></td>
</tr>
</tbody>
</table>


Pour plus d'informations sur les sondes et les moniteurs, consultez la rubrique [État et performances du serveur](https://technet.microsoft.com/fr-fr/library/jj150551\(v=exchg.150\)).

## Problèmes courants

L'échec de cette sonde peut avoir plusieurs causes. Les problèmes les plus courants sont les suivants :

  - Le pool d'applications hébergé sur le serveur CAS contrôlé ne fonctionne pas correctement.

  - Les informations d'identification du compte assurant le contrôle sont incorrectes.

  - Les contrôleurs de domaine ne répondent pas.

## Action de l'utilisateur

Le service a peut-être pu récupérer après l'émission de l'alerte. Par conséquent, quand vous recevez une alerte signalant que l'indicateur d'intégrité n'est pas intègre, vérifiez que le problème existe toujours. Si tel est le cas, exécutez les actions de récupération appropriées décrites dans les sections suivantes.

## Vérification de l'existence du problème

1.  Repérez les noms de l'indicateur d'intégrité et du serveur dans l'alerte.

2.  Les détails du message fournissent des informations sur la cause précise de l'alerte. Dans la plupart des cas, ils fournissent des informations de dépannage suffisantes pour identifier la cause première. Si les détails du message ne sont pas clairs, procédez comme suit :
    
    1.  Ouvrez l'environnement de ligne de commande, puis exécutez la commande suivante pour récupérer les détails de l'indicateur d'intégrité qui a émis l'alerte :
        
            Get-ServerHealth <server name> | ?{$_.HealthSetName -eq "<health set name>"}
        
        Par exemple, pour récupérer les détails de l'indicateur d'intégrité RPS.Proxy à propos de server1.contoso.com, exécutez la commande suivante :
        
            Get-ServerHealth server1.contoso.com | ?{$_.HealthSetName -eq "RPS.Proxy"}
    
    2.  Consultez la sortie de la commande pour déterminer quel moniteur a signalé l'erreur. La valeur **AlertValue** du moniteur qui a émis l'alerte sera `Unhealthy`.
    
    3.  Réexécutez la sonde associée pour le moniteur dont l'état n'est pas intègre. Reportez-vous au tableau fourni dans la section Explanation pour rechercher la sonde associée. Pour ce faire, exécutez la commande suivante :
        
            Invoke-MonitoringProbe <health set name>\<probe name> -Server <server name> | Format-List
        
        Par exemple, supposons que le moniteur défectueux soit **RPSProxyTestMonitor**. La sonde associée à ce moniteur est **RPSProxyTestProbe**. Pour exécuter cette sonde sur le serveur server1.contoso.com, exécutez la commande suivante :
        
            Invoke-MonitoringProbe RPS.Proxy\RPSProxyTestProbe -Server server1.contoso.com | Format-List
    
    4.  Dans la sortie de la commande, consultez la valeur **Result** de la sonde. Si elle indique **Succeeded**, le problème était une erreur passagère, qui n'existe plus. Sinon, reportez-vous aux étapes de récupération décrites dans les sections suivantes.

## Actions de récupération RPSProxyTestMonitor

Quand vous recevez une alerte de l'indicateur d'intégrité, le message électronique contient les informations suivantes :

  - Le nom du serveur CAS qui a envoyé l'alerte.

  - La trace d'exception complète incluant les messages d'erreur, données de diagnostic et informations d'en-tête HTTP spécifiques. Les informations figurant dans la trace d'exception complète peuvent vous aider à dépanner le problème.

  - L'heure et la date de survenance du problème.

Pour résoudre ce problème, procédez comme suit :

1.  Examinez les journaux du protocole sur les serveurs CAS. Les journaux du protocole sont situés dans le dossier *\<répertoire d'installation d'Exchange Server\>*\\Logging\\HttpProxy*\\\<protocole\>* sur le serveur CAS.

2.  Créez un compte d'utilisateur test, puis utilisez-le pour vous connecter au serveur CAS, par exemple https:// *\<nom de serveur\>*/owa

3.  Démarrez le Gestionnaire des services Internet, connectez-vous au serveur signalant l'erreur, puis vérifiez que le pool d'applications MSExchangePowerShellFrontEndAppPool est en cours d'exécution sur le serveur CAS.

4.  Cliquez sur **Pools d'applications**, puis recyclez le pool d'applications **MSExchangePowerShellFrontEndAppPool** en exécutant la commande suivante à partir de l'environnement de ligne de commande Exchange Management Shell :
    
        %SystemRoot%\System32\inetsrv\Appcmd recycle MSExchangePowerShellFrontEndAppPool

5.  Réexécutez la sonde associée de la manière décrite dans l'étape 2c de la section Verifying the issue still exists.

6.  Si le problème persiste, recyclez le service IIS à l'aide de l'utilitaire IISReset.

7.  Réexécutez la sonde associée de la manière décrite dans l'étape 2c de la section Verifying the issue still exists.

8.  Si le problème persiste, redémarrez le serveur.

9.  Une fois le serveur redémarré, réexécutez la sonde associée de la manière décrite dans l'étape 2.c. de la section Verifying the issue still exists.

10. Si l'échec de la sonde persiste, vous avez peut-être besoin d'assistance pour résoudre le problème. Contactez un professionnel du Support Technique de Microsoft pour résoudre ce problème. Pour contacter un professionnel du Support Technique de Microsoft, consultez [Exchange Server Solutions Center](http://go.microsoft.com/fwlink/p/?linkid=180809). Dans le volet de navigation, cliquez sur **Ressources et options de support** et utilisez l'une des options indiquées sous **Obtenez du support technique** pour contacter un professionnel du support Microsoft. Étant donné que votre organisation peut avoir une procédure spécifique pour contacter directement les Services de Support Technique Microsoft, assurez-vous de connaître d'abord les instructions propres à votre organisation.

## Pour plus d'informations

[Nouveautés d'Exchange 2013](https://technet.microsoft.com/fr-fr/library/jj150540\(v=exchg.150\))

[Cmdlets Exchange 2013](https://technet.microsoft.com/fr-fr/library/bb124413\(v=exchg.150\))

