---
title: Dépannage de l'indicateur d'intégrité POP
TOCTitle: Dépannage de l'indicateur d'intégrité POP
ms:assetid: 6114e9fe-d037-4cb9-a643-933eb5fabc45
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/ms.exch.scom.pop(v=EXCHG.150)
ms:contentKeyID: 53276470
ms.date: 02/05/2016
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Dépannage de l'indicateur d'intégrité POP

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2015-03-09_

L'indicateur d'intégrité POP vous permet de surveiller l'intégrité et la disponibilité globales du service Microsoft Exchange POP3 et de la connectivité au client POP3. L'indicateur d'intégrité POP est étroitement lié aux indicateurs d'intégrité suivants :

  - [Dépannage de l'indicateur d'intégrité POP.Protocol](troubleshooting-pop-protocol-health-set.md)

  - [Dépannage de l'indicateur d'intégrité POP.Proxy](troubleshooting-pop-proxy-health-set.md)

Si vous recevez une alerte indiquant que le service POP présente un manque d'intégrité, cela signifie qu'un problème empêche probablement les utilisateurs d'accéder à leur boîte aux lettres à l'aide de POP3 dans l'environnement Exchange.

## Explication

Le service POP est surveillé à l'aide des sondes et moniteurs suivants.


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
<td><p>PopCTPProbe</p></td>
<td><p>POP</p></td>
<td><p>Active Directory</p>
<p>Authentification</p>
<p>Authentification du serveur de boîtes aux lettres</p>
<p>Banque d'informations</p>
<p>Haute disponibilité</p>
<p>Réseau</p></td>
<td><p>PopCTPMonitor (indicateur d'intégrité POP)</p></td>
</tr>
<tr class="even">
<td><p>PopProxyTestProbe</p></td>
<td><p>POP.Proxy</p></td>
<td><p>Aucun</p></td>
<td><p>PopProxyTestMonitor (indicateur d'intégrité POP.Proxy)</p></td>
</tr>
<tr class="odd">
<td><p>PopDeepTestProbe</p></td>
<td><p>POP.Protocol</p></td>
<td><p>Active Directory</p>
<p>Authentification</p>
<p>Banque d'informations</p>
<p>Haute disponibilité</p></td>
<td><p>PopDeepTestMonitor (indicateur d'intégrité POP.Protocol)</p></td>
</tr>
<tr class="even">
<td><p>PopSelfTestProbe</p></td>
<td><p>POP.Protocol</p></td>
<td><p>Aucun</p></td>
<td><p>PopSelfTestMonitor (indicateur d'intégrité POP.Protocol)</p>
<p>AverageCommandProcessingTimeGt60sMonitor (indicateur d'intégrité POP)</p></td>
</tr>
</tbody>
</table>


## Action de l'utilisateur

Il se peut que le service ait récupéré après avoir émis l'alerte. Par conséquent, quand vous recevez une alerte signalant que l'indicateur d'intégrité n'est pas intègre, vérifiez tout d'abord que le problème existe toujours. Si tel est le cas, exécutez les actions de récupération appropriées décrites dans les sections suivantes.

## Vérification de l'existence du problème

1.  Repérez les noms de l'indicateur d'intégrité et du serveur dans l'alerte.

2.  Les détails du message fournissent des informations sur la cause exacte de l'alerte. Le plus souvent, le message fournit des informations de dépannage suffisantes pour identifier la cause première. Si les détails du message ne sont pas clairs, procédez comme suit :
    
    1.  Ouvrez Environnement de ligne de commande Exchange Management Shell, puis exécutez la commande suivante pour récupérer les détails de l'indicateur d'intégrité qui a émis l'alerte :
        
            Get-ServerHealth <server name> | ?{$_.HealthSetName -eq "<health set name>"}
        
        Par exemple, pour récupérer les détails de l'indicateur d'intégrité POP à propos de server1.contoso.com, exécutez la commande suivante :
        
            Get-ServerHealth server1.contoso.com | ?{$_.HealthSetName -eq "POP"}
    
    2.  Consultez la sortie de la commande pour déterminer quel moniteur a signalé l'erreur. La valeur **AlertValue** du moniteur qui a émis l'alerte sera `Unhealthy`.
    
    3.  Réexécutez la sonde associée pour le moniteur dont l’état d’intégrité est défectueux. Pour rechercher la sonde associée, reportez-vous au tableau figurant dans la section Explanation. Pour ce faire, exécutez la commande suivante :
        
            Invoke-MonitoringProbe <health set name>\<probe name> -Server <server name> | Format-List
        
        Par exemple, supposons que le moniteur défectueux soit **PopCTPMonitor**. La sonde associée à ce moniteur est **PopCTPProbe**. Pour exécuter cette sonde sur server1.contoso.com, exécutez la commande suivante :
        
            Invoke-MonitoringProbe POP\PopCTPProbe -Server server1.contoso.com | Format-List
    
    4.  Dans la sortie de la commande, consultez la valeur **Result** de la sonde. Si elle indique **Succeeded**, le problème était une erreur passagère, qui n'existe plus. Autrement, reportez-vous aux étapes de récupération décrites dans les sections suivantes.

## Actions de récupération PopTestDeepMonitor et PopSelfTestMonitor

Cette alerte de moniteur est généralement émise sur des serveurs de boîtes aux lettres.

1.  Redémarrez le service principal POP3. Pour plus d'informations, consultez la rubrique [Démarrage et arrêt des services POP3](https://technet.microsoft.com/fr-fr/library/aa997475\(v=exchg.150\)).

2.  Réexécutez la sonde associée en procédant de la manière décrite dans l'étape 2c de la section Verifying the issue still exists.

3.  Si la sonde échoue encore, basculez les bases de données hébergées sur le serveur de boîtes aux lettres à l'aide de la commande suivante :
    
        Set-MailboxServer -Identity <ServerName> -DatabaseCopyActivationDisabledAndMoveNow $true

4.  Après avoir supprimé toutes les bases de données du serveur de boîtes aux lettres, vous devez vérifier que les bases de données ont été correctement déplacées. Pour ce faire, exécutez la commande suivante :
    
        Get-MailboxDatabaseCopyStatus -Server <ServerName> | group status

5.  Assurez-vous que le serveur n'héberge aucune copie active de la base de données, puis redémarrez le serveur.

6.  Une fois le serveur redémarré, réexécutez la sonde associée de la manière décrite dans l'étape 2c de la section Verifying the issue still exists.

7.  Si la sonde réussit, basculez les bases de données en exécutant la commande suivante :
    
        Set-MailboxServer -Identity <ServerName> -DatabaseCopyActivationDisabledAndMoveNow $false

8.  En cas de nouvel échec de la sonde, il se peut que vous ayez besoin d'aide pour résoudre ce problème. Contactez un professionnel du Support Technique de Microsoft pour résoudre ce problème. Pour contacter un professionnel du Support Technique de Microsoft, consultez [Exchange Server Solutions Center](http://go.microsoft.com/fwlink/p/?linkid=180809). Dans le volet de navigation, cliquez sur **Ressources et options de support** et utilisez l'une des options indiquées sous **Obtenez du support technique** pour contacter un professionnel du support Microsoft. Étant donné que votre organisation peut avoir une procédure spécifique pour contacter directement les Services de Support Technique Microsoft, assurez-vous de connaître d'abord les instructions propres à votre organisation.

## Actions de récupération POPCTPMonitor

Cette alerte de moniteur est généralement émise sur des serveurs CAS.

1.  Redémarrez le service POP3 sur les serveurs exécutant le rôle serveur d'accès au client. Pour plus d'informations, consultez la rubrique [Démarrage et arrêt des services POP3](https://technet.microsoft.com/fr-fr/library/aa997475\(v=exchg.150\)).

2.  Réexécutez la sonde associée en procédant de la manière décrite dans l'étape 2c de la section Verifying the issue still exists.

3.  Si le problème persiste, exécutez les commandes suivantes dans Windows PowerShell :
    
    1.  ``` 
        Set-PopSettings -server <CAS server name> -ProtocolLoggingEnabled $true
        ```
    
    2.  Redémarrez le service POP3 sur les serveurs exécutant le rôle serveur d'accès au client.
    
    3.  Réexécutez la sonde associée en procédant de la manière décrite dans l'étape 2c de la section Verifying the issue still exists.
    
    4.  Exécutez la commande suivante, puis recherchez l'emplacement du fichier journal :
        
            Get-PopSettings -server <CAS server name>
    
    5.  Exécutez la commande suivante pour identifier la boîte aux lettres qui utilise cette commande en comparant les horodateurs avec la sonde :
        
            Get-ServerHealth <mailbox server name> | ?{ $_.HealthSetName -like "POP*"}
    
    6.  Si l'un de ces serveurs présente un manque d'intégrité, suivez les étapes décrites dans la section PopTestDeepMonitor and PopSelfTestMonitor Recovery Actions.

4.  Si le serveur de base de données est intègre, redémarrez le serveur d'accès au client.

5.  Une fois le serveur redémarré, réexécutez la sonde associée de la manière décrite dans l'étape 2c de la section Verifying the issue still exists.

6.  Désactivez l'enregistrement dans le journal de protocole en exécutant la commande suivante :
    
        Set-PopSettings -server <CAS server name> -ProtocolLoggingEnabled $false

7.  Redémarrez le service POP3 sur les serveurs exécutant le rôle serveur d'accès au client. Pour plus d'informations, consultez la rubrique [Démarrage et arrêt des services POP3](https://technet.microsoft.com/fr-fr/library/aa997475\(v=exchg.150\)).

8.  En cas de nouvel échec de la sonde, il se peut que vous ayez besoin d'aide pour résoudre ce problème. Contactez un professionnel du Support Technique de Microsoft pour résoudre ce problème. Pour contacter un professionnel du Support Technique de Microsoft, consultez [Exchange Server Solutions Center](http://go.microsoft.com/fwlink/p/?linkid=180809). Dans le volet de navigation, cliquez sur **Ressources et options de support** et utilisez l'une des options indiquées sous **Obtenez du support technique** pour contacter un professionnel du support Microsoft. Étant donné que votre organisation peut avoir une procédure spécifique pour contacter directement les Services de Support Technique Microsoft, assurez-vous de connaître d'abord les instructions propres à votre organisation.

## Actions de récupération PopProxyTestMonitor

1.  Redémarrez le service POP3 sur les serveurs exécutant le rôle serveur d'accès au client. Pour plus d'informations, consultez la rubrique [Démarrage et arrêt des services POP3](https://technet.microsoft.com/fr-fr/library/aa997475\(v=exchg.150\)).

2.  Réexécutez la sonde associée en procédant de la manière décrite dans l'étape 2c de la section Verifying the issue still exists.

3.  Si l'échec de la sonde persiste, redémarrez le serveur d'accès au client.

4.  Une fois le serveur redémarré, réexécutez la sonde associée de la manière décrite dans l'étape 2c de la section Verifying the issue still exists.

5.  En cas de nouvel échec de la sonde, il se peut que vous ayez besoin d'aide pour résoudre ce problème. Contactez un professionnel du Support Technique de Microsoft pour résoudre ce problème. Pour contacter un professionnel du Support Technique de Microsoft, consultez [Exchange Server Solutions Center](http://go.microsoft.com/fwlink/p/?linkid=180809). Dans le volet de navigation, cliquez sur **Ressources et options de support** et utilisez l'une des options indiquées sous **Obtenez du support technique** pour contacter un professionnel du support Microsoft. Étant donné que votre organisation peut avoir une procédure spécifique pour contacter directement les Services de Support Technique Microsoft, assurez-vous de connaître d'abord les instructions propres à votre organisation.

## Actions de récupération AverageCommandProcessingTimeGt60sMonitor

Cette alerte de moniteur est généralement émise sur des serveurs d'autorités de certification ou de boîtes aux lettres.

1.  Redémarrez le service POP3 sur les serveurs d'autorités de certification ou de boîtes aux lettres. Pour plus d'informations, consultez la rubrique [Démarrage et arrêt des services POP3](https://technet.microsoft.com/fr-fr/library/aa997475\(v=exchg.150\)).

2.  Patientez 10 minutes pour voir si le moniteur reste intègre. Après 10 minutes, exécutez la commande suivante (cet exemple utilise server1.contoso.com).
    
        Get-ServerHealth server1.contoso.com | ?{$_.HealthSetName -like "POP*"}

3.  Si le problème persiste, vous devez redémarrer le serveur. Si le serveur est un serveur d'accès au client, redémarrez simplement le serveur. Si le serveur est un serveur de boîtes aux lettres, vous devez basculer la base de données, puis vérifier les résultats. Pour ce faire, procédez comme suit :
    
    1.  Basculez les bases de données hébergées sur le serveur en exécutant la commande suivante :
        
            Set-MailboxServer -Identity <ServerName> -DatabaseCopyActivationDisabledAndMoveNow $true
        
        **Remarque**   Dans cet exemple de code et dans tous les exemples de codes suivants, remplacez *server1.contoso.com* par le nom réel du serveur.
    
    2.  Vérifiez que toutes les bases de données ont été déplacées hors du serveur qui signale le problème. Pour ce faire, exécutez la commande suivante :
        
            Get-MailboxDatabaseCopyStatus -Server <ServerName> | group status
        
        Si la sortie de la commande n'affiche aucune copie active sur le serveur, redémarrez ce dernier.

4.  Après le redémarrage du serveur, patientez 10 minutes, puis réexécutez la commande décrite dans l'étape 2 pour voir si le moniteur reste intègre.

5.  Si le moniteur est intègre et s'il s'agit d'un serveur de boîtes aux lettres, rebasculez les bases de données sur le serveur de boîtes aux lettres en exécutant la commande suivante :
    
        Set-MailboxServer -Identity <ServerName> -DatabaseCopyActivationDisabledAndMoveNow $false

6.  En cas de nouvel échec de la sonde, il se peut que vous ayez besoin d'aide pour résoudre ce problème. Contactez un professionnel du Support Technique de Microsoft pour résoudre ce problème. Pour contacter un professionnel du Support Technique de Microsoft, consultez [Exchange Server Solutions Center](http://go.microsoft.com/fwlink/p/?linkid=180809). Dans le volet de navigation, cliquez sur **Ressources et options de support** et utilisez l'une des options indiquées sous **Obtenez du support technique** pour contacter un professionnel du support Microsoft. Étant donné que votre organisation peut avoir une procédure spécifique pour contacter directement les Services de Support Technique Microsoft, assurez-vous de connaître d'abord les instructions propres à votre organisation.

## Pour plus d'informations

[Démarrage et arrêt des services POP3](https://technet.microsoft.com/fr-fr/library/aa997475\(v=exchg.150\))

[Test-PopConnectivity](https://technet.microsoft.com/fr-fr/library/bb738143\(v=exchg.150\))

