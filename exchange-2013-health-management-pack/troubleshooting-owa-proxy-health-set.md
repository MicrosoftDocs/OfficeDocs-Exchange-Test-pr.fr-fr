---
title: Dépannage de l'indicateur d'intégrité OWA.Proxy
TOCTitle: Dépannage de l'indicateur d'intégrité OWA.Proxy
ms:assetid: 1eaa26ad-b489-402a-ad2d-bfae3b083f42
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/ms.exch.scom.owa.proxy(v=EXCHG.150)
ms:contentKeyID: 53276462
ms.date: 02/05/2016
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Dépannage de l'indicateur d'intégrité OWA.Proxy

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2015-03-09_

L'indicateur d'intégrité OWA.Proxy surveille l'intégrité globale du service Outlook Web App.

Si vous recevez une alerte indiquant qu'OWA.Proxy présente un manque d'intégrité, cela signifie qu'un problème empêche probablement les utilisateurs d'utiliser le service Outlook Web App.

## Explication

Le service Outlook Web App est surveillé à l'aide des sondes et moniteurs suivants.


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
<td><p>OWAProxyTestProbe</p></td>
<td><p>OWA.Proxy</p></td>
<td><p>Active Directory</p></td>
<td><p>OWAProxyTestMonitor</p></td>
</tr>
<tr class="even">
<td><p>OWAanonymouscalendarProbe</p></td>
<td><p>OWA.Proxy</p></td>
<td><p>Active Directory</p></td>
<td><p>OWAProxyTestMonitor</p></td>
</tr>
</tbody>
</table>


Pour plus d'informations sur les sondes et les moniteurs, consultez la rubrique [État et performances du serveur](https://technet.microsoft.com/fr-fr/library/jj150551\(v=exchg.150\)).

## Problèmes courants

Cette sonde peut échouer pour les raisons courantes suivantes :

  - Le pool d’applications hébergé sur le serveur d’accès au client (CAS) contrôlé ne fonctionne pas correctement.

  - Les informations d'identification du compte assurant le contrôle sont incorrectes.

  - Les contrôleurs de domaine ne répondent pas.

## Action de l'utilisateur

Il se peut que le service ait récupéré après avoir émis l'alerte. Par conséquent, quand vous recevez une alerte signalant que l'indicateur d'intégrité n'est pas intègre, vérifiez tout d'abord que le problème existe toujours. Si tel est le cas, exécutez les actions de récupération appropriées décrites dans les sections suivantes.

## Vérification de l'existence du problème

1.  Repérez les noms de l'indicateur d'intégrité et du serveur dans l'alerte.

2.  Les détails du message fournissent des informations sur la cause exacte de l'alerte. Le plus souvent, le message fournit des informations de dépannage suffisantes pour identifier la cause première. Si les détails du message ne sont pas clairs, procédez comme suit :
    
    1.  Ouvrez Environnement de ligne de commande Exchange Management Shell, puis exécutez la commande suivante pour récupérer les détails de l'indicateur d'intégrité qui a émis l'alerte :
        
            Get-ServerHealth <server name> | ?{$_.HealthSetName -eq "<health set name>"}
        
        Par exemple, pour récupérer les détails de l'indicateur d'intégrité OWA.Proxy à propos de server1.contoso.com, exécutez la commande suivante :
        
            Get-ServerHealth server1.contoso.com | ?{$_.HealthSetName -eq "OWA.Proxy"}
    
    2.  Consultez la sortie de la commande pour déterminer quel moniteur a signalé l'erreur. La valeur **AlertValue** du moniteur qui a émis l'alerte sera `Unhealthy`.
    
    3.  Réexécutez la sonde associée pour le moniteur dont l’état d’intégrité est défectueux. Pour rechercher la sonde associée, reportez-vous au tableau figurant dans la section Explanation. Pour ce faire, exécutez la commande suivante :
        
            Invoke-MonitoringProbe <health set name>\<probe name> -Server <server name> | Format-List
        
        Par exemple, supposons que le moniteur défectueux soit **OWAProxyTestMonitor**. La sonde associée à ce moniteur est **OWAProxyTestProbe**. Pour exécuter cette sonde sur server1.contoso.com, exécutez la commande suivante :
        
            Invoke-MonitoringProbe OWA.Proxy\OWAProxyTestProbe -Server server1.contoso.com | Format-List
    
    4.  Dans la sortie de la commande, consultez la valeur **Result** de la sonde. Si elle indique **Succeeded**, le problème était une erreur passagère, qui n'existe plus. Autrement, reportez-vous aux étapes de récupération décrites dans les sections suivantes.

## Actions de récupération OWAProxyTestMonitor

Quand vous recevez une alerte de l'indicateur d'intégrité, le message électronique contient les informations suivantes :

  - nom du CAS ayant envoyé l'alerte ;

  - trace d'exception complète de la dernière erreur, notamment données de diagnostic et informations d'en-tête HTTP spécifiques ;  
    
    **Remarque**   Vous pouvez utiliser les informations contenues dans la trace de l'exception complète pour résoudre le problème.

  - heure et date du problème.

Pour résoudre ce problème, procédez comme suit :

1.  Examinez les journaux du protocole sur les serveurs d'accès au client. Les journaux du protocole sont situés dans le dossier *\<répertoire d'installation d'Exchange Server\>*\\Logging\\HttpProxy*\\\<protocole\>* sur le CAS.

2.  Créez un compte d'utilisateur test, puis connectez-vous au CAS en utilisant ce compte. Par exemple, connectez-vous en utilisant : https:// *\<nom de serveur\>*/owa.

3.  Démarrez le Gestionnaire des services Internet, puis connectez-vous au serveur signalant le problème afin de déterminer si les pools d’applications **MSExchangeServicesAppPools** sont en cours d’exécution sur le CAS.

4.  Cliquez sur **Pools d'applications**, puis recyclez les pools d'applications **MSExchangeOWAAppPool** et **MSExchangeOWACalendarAppPool** en exécutant la commande suivante à partir de l'environnement de ligne de commande Exchange Management Shell :
    
        %SystemRoot%\System32\inetsrv\Appcmd recycle APPPOOL MSExchangeOWAAppPool
    
        %SystemRoot%\System32\inetsrv\Appcmd recycle APPPOOL MSExchangeOWACalendarAppPool

5.  Réexécutez la sonde associée en procédant de la manière décrite dans l'étape 2c de la section Verifying the issue still exists.

6.  Si le problème persiste, recyclez le service IIS à l'aide de l'utilitaire IISReset.

7.  Réexécutez la sonde associée en procédant de la manière décrite dans l'étape 2c de la section Verifying the issue still exists.

8.  Si le problème persiste, redémarrez le serveur.

9.  Une fois le serveur redémarré, réexécutez la sonde associée en procédant de la manière décrite dans l'étape 2c de la section Verifying the issue still exists.

10. En cas de nouvel échec de la sonde, il se peut que vous ayez besoin d'aide pour résoudre ce problème. Contactez un professionnel du Support Technique de Microsoft pour résoudre ce problème. Pour contacter un professionnel du Support Technique de Microsoft, consultez [Exchange Server Solutions Center](http://go.microsoft.com/fwlink/p/?linkid=180809). Dans le volet de navigation, cliquez sur **Ressources et options de support** et utilisez l'une des options indiquées sous **Obtenez du support technique** pour contacter un professionnel du support Microsoft. Étant donné que votre organisation peut avoir une procédure spécifique pour contacter directement les Services de Support Technique Microsoft, assurez-vous de connaître d'abord les instructions propres à votre organisation.

## Pour plus d'informations

[Nouveautés d'Exchange 2013](https://technet.microsoft.com/fr-fr/library/jj150540\(v=exchg.150\))

[Cmdlets Exchange 2013](https://technet.microsoft.com/fr-fr/library/bb124413\(v=exchg.150\))

[Managing Outlook Web App](https://technet.microsoft.com/fr-fr/3814b665-01e8-4881-9a44-163f14789ee4\(exchg.150\)#managing)

