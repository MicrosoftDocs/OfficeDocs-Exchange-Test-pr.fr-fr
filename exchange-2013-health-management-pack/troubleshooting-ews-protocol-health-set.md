---
title: Dépannage de l'indicateur d'intégrité EWS.Protocol
TOCTitle: Dépannage de l'indicateur d'intégrité EWS.Protocol
ms:assetid: 826b2d5b-adbb-4bf5-94b6-0a8de2e3aac0
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/ms.exch.scom.ews.protocol(v=EXCHG.150)
ms:contentKeyID: 53276472
ms.date: 02/05/2016
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Dépannage de l'indicateur d'intégrité EWS.Protocol

 

_**Sapplique à :**Exchange Server 2013, Project Server 2013_

_**Dernière rubrique modifiée :**2015-03-09_

L'indicateur d'intégrité EWS.Protocol surveille le protocole de communication des services web Exchange (EWS) sur le serveur de boîtes aux lettres. L'indicateur d'intégrité EWS.Protocol est étroitement lié aux indicateurs d'intégrité suivants :

[Dépannage de l'indicateur d'intégrité EWS](troubleshooting-ews-health-set.md)

[Dépannage de l'indicateur d'intégrité EWS.Proxy](troubleshooting-ews-proxy-health-set.md)

Si vous recevez une alerte indiquant qu'EWS.Protocol présente un manque d'intégrité, cela signifie qu'un problème empêche probablement les utilisateurs d'accéder à Exchange.

## Explication

L'indicateur d'intégrité EWS.Protocol comprend les sondes suivantes :

1.  EwsSelfTestProbe

2.  EwsDeepTestProbe

La sonde EwsSelfTestProbe ne dépend pas de la Banque d'informations. Toutefois, la sonde EwsDeepTestProbe dépend de la Banque d'informations. Ces deux sondes effectuent des opérations EWS sur le serveur de boîtes aux lettres et utilisent la même méthode d'authentification que celle du serveur d'accès au client (CAS). EwsSeftTestProbe appelle la méthode **ConvertId** et EwsDeepTestProbe appelle la méthode **GetFolder**.


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
<td><p>EwsSelfTestProbe</p></td>
<td><p>EWS.Protocol</p></td>
<td><p>Active Directory</p></td>
<td><p>EWSSelfTestMonitor</p></td>
</tr>
<tr class="even">
<td><p>EwsDeepTestProbe</p></td>
<td><p>EWS.Protocol</p></td>
<td><p>Banque d'informations</p></td>
<td><p>EWSDeepTestMonitor</p></td>
</tr>
</tbody>
</table>


Pour plus d'informations sur les sondes et les moniteurs, consultez la rubrique [État et performances du serveur](https://technet.microsoft.com/fr-fr/library/jj150551\(v=exchg.150\)).

Quand vous recevez une alerte de ces informations d'intégrité, le message électronique contient les données suivantes :

1.  nom du serveur de boîtes aux lettres sur lequel l'alerte a été émise ;

2.  trace d'exception complète de la dernière erreur, notamment données de diagnostic et informations d'en-tête HTTP spécifiques ;

3.  heure de l'incident.

## Problèmes courants

Cette sonde peut échouer pour les raisons courantes suivantes :

  - Le pool d'applications EWS sur le serveur de boîtes aux lettres ne fonctionne pas correctement.

  - Les contrôleurs de domaine ne répondent pas ou ne peuvent pas communiquer avec le serveur de boîtes aux lettres.

  - La base de données de l’utilisateur n’est pas montée ou le service Banque d’informations n’est pas disponible pour une boîte aux lettres spécifique.

## Action de l'utilisateur

Il se peut que le service ait récupéré après avoir émis l'alerte. Par conséquent, quand vous recevez une alerte signalant que l'indicateur d'intégrité n'est pas intègre, vérifiez tout d'abord que le problème existe toujours. Si tel est le cas, exécutez les actions de récupération appropriées décrites dans les sections suivantes.

## Vérification de l'existence du problème

1.  Repérez les noms de l'indicateur d'intégrité et du serveur dans l'alerte.

2.  Les détails du message fournissent des informations sur la cause exacte de l'alerte. Le plus souvent, le message fournit des informations de dépannage suffisantes pour identifier la cause première. Si les détails du message ne sont pas clairs, procédez comme suit :
    
    1.  Ouvrez Environnement de ligne de commande Exchange Management Shell, puis exécutez la commande suivante pour récupérer les détails de l'indicateur d'intégrité qui a émis l'alerte :
        
            Get-ServerHealth <server name> | ?{$_.HealthSetName -eq "<health set name>"}
        
        Par exemple, pour récupérer les détails des informations d'intégrité d'EWS.Protocol à propos de server1.contoso.com, exécutez la commande suivante :
        
            Get-ServerHealth server1.contoso.com | ?{$_.HealthSetName -eq "EWS.Protocol"}
    
    2.  Consultez la sortie de la commande pour déterminer quel moniteur a signalé l'erreur. La valeur **AlertValue** du moniteur qui a émis l'alerte sera `Unhealthy`.
    
    3.  Réexécutez la sonde associée pour le moniteur dont l'état n'est pas intègre. Pour rechercher la sonde associée, reportez-vous au tableau figurant dans la section Explanation. Pour ce faire, exécutez la commande suivante :
        
            Invoke-MonitoringProbe <health set name>\<probe name> -Server <server name> | Format-List
        
        Par exemple, supposons que le moniteur défectueux soit **EWSSelfTestMonitor**. La sonde associée à ce moniteur est **EWSSelfTestProbe**. Pour exécuter cette sonde sur server1.contoso.com, exécutez la commande suivante :
        
            Invoke-MonitoringProbe EWS.Protocol\EWSSelfTestProbe -Server server1.contoso.com | Format-List
    
    4.  Dans la sortie de la commande, consultez la valeur **Result** de la sonde. Si elle indique **Succeeded**, le problème était une erreur passagère, qui n'existe plus. Autrement, reportez-vous aux étapes de récupération décrites dans les sections suivantes.

## Actions de récupération pour EWSSelfTestMonitor et EWSDeepTestMonitor

Cette alerte de moniteur est généralement émise pour des serveurs de boîtes aux lettres.

1.  Démarrez le Gestionnaire des services Internet, puis connectez-vous au serveur signalant le problème afin de déterminer si le pool d’applications MSExchangeServicesAppPool est en cours d’exécution sur le CAS et le serveur de boîte aux lettres.

2.  Identifiez la MailboxDatabase à l'origine de l'échec des sondes, puis vérifiez que la MailboxDatabase est active sur le MailboxServer, et que la Banque d'informations est intègre.

3.  Cliquez sur **Pools d'applications**, puis recyclez le pool d'applications **MSExchangeServicesAppPool** en exécutant la commande suivante à partir de l'environnement de ligne de commande Exchange Management Shell :
    
        %SystemRoot%\System32\inetsrv\Appcmd recycle MSExchangeServicesAppPool

4.  Réexécutez la sonde associée en procédant de la manière décrite dans l'étape 2c de la section Verifying the issue still exists.

5.  Si le problème persiste, redémarrez le service IIS à l'aide de l'utilitaire IISReset.

6.  Réexécutez la sonde associée en procédant de la manière décrite dans l'étape 2c de la section Verifying the issue still exists.

7.  Si le problème persiste, consultez les fichiers journaux de protocole sur le serveur de boîtes aux lettres. Sur le serveur de boîtes aux lettres, les journaux sont situés dans le dossier *\<répertoire d'installation d'Exchange Server\>*\\Logging\\Ews.

8.  Créez un compte d'utilisateur test, puis connectez-vous en utilisant ce compte sur le serveur de boîtes aux lettres donné sur le port 444 https://*\<nom\_serveur\>*:444/ews/exchange.asmx. Si le test réussit, un problème peut affecter la base de données de boîtes aux lettres ou le serveur de boîtes aux lettres sur lequel se trouve la boîte aux lettres de surveillance. Essayez de répéter cette étape en utilisant un compte test sur cette base de données.

9.  Recherchez dans les informations d'intégrité d'EWS.Protocol les alertes indiquant qu'un problème affecte le serveur de boîtes aux lettres.

10. Si le problème persiste, redémarrez le serveur. Pour ce faire, basculez d'abord les bases de données hébergées sur le serveur à l'aide de la commande suivante :
    
        Set-MailboxServer server1.contoso.com -DatabaseCopyActivationDisabledAndMoveNow $true
    
    Dans cet exemple de code et dans tous les exemples de code suivants, remplacez *server1.contoso.com* par le nom réel du serveur.

11. Vérifiez que toutes les bases de données ont été déplacées hors du serveur qui signale le problème. Pour ce faire, exécutez la commande suivante :
    
        Get-MailboxDatabaseCopyStatus -Server server1.contoso.com | Group Status
    
    Si la sortie de la commande n'affiche aucune copie active sur le serveur, redémarrez ce dernier. Redémarrez le serveur.

12. Une fois le serveur redémarré, réexécutez la sonde associée en procédant de la manière décrite dans l'étape 2c de la section Verifying the issue still exists.

13. Si la sonde réussit, basculez les bases de données en exécutant la commande suivante :
    
        Set-MailboxServer server1.contoso.com -DatabaseCopyActivationDisabledAndMoveNow $false

14. Si l'échec de la sonde persiste, vous avez peut-être besoin d'assistance pour résoudre le problème. Contactez un professionnel du Support Technique de Microsoft pour résoudre ce problème. Pour contacter un professionnel du Support Technique de Microsoft, consultez [Exchange Server Solutions Center](http://go.microsoft.com/fwlink/p/?linkid=180809). Dans le volet de navigation, cliquez sur **Ressources et options de support** et utilisez l'une des options indiquées sous **Obtenez du support technique** pour contacter un professionnel du support Microsoft. Étant donné que votre organisation peut avoir une procédure spécifique pour contacter directement les Services de Support Technique Microsoft, assurez-vous de connaître d'abord les instructions propres à votre organisation.

## Pour plus d'informations

[Nouveautés d'Exchange 2013](https://technet.microsoft.com/fr-fr/library/jj150540\(v=exchg.150\))

