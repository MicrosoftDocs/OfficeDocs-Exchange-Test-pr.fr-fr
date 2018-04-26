---
title: Dépannage de l'indicateur d'intégrité IMAP
TOCTitle: Dépannage de l'indicateur d'intégrité IMAP
ms:assetid: 2a06e671-4cc2-4ce5-bf53-6243ea140f20
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/ms.exch.scom.imap(v=EXCHG.150)
ms:contentKeyID: 53276463
ms.date: 02/05/2016
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Dépannage de l'indicateur d'intégrité IMAP

 

_**Sapplique à :**Exchange Server 2013_

_**Dernière rubrique modifiée :**2015-03-09_

L'indicateur d'intégrité IMAP surveille la disponibilité de l'infrastructure proxy IMAP4 sur le serveur d'accès au client (CAS). L'indicateur d'intégrité IMAP est étroitement lié à l'indicateur d'intégrité suivant :

[Dépannage de l'indicateur d'intégrité IMAP.Protocol](troubleshooting-imap-protocol-health-set.md)

[Dépannage de l'indicateur d'intégrité IMAP.Proxy](troubleshooting-imap-proxy-health-set.md)

Si vous recevez une alerte indiquant qu'IMAP présente un manque d'intégrité, cela signifie qu'un problème empêche probablement les utilisateurs d'accéder à leur boîte aux lettres à l'aide d'IMAP.

## Explication

Le service IMAP4 est surveillé à l'aide des sondes et moniteurs suivants.


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
<td><p>ImapCTPProbe</p></td>
<td><p>IMAP</p></td>
<td><p>Active Directory</p>
<p>Authentification</p>
<p>Authentification du serveur de boîtes aux lettres</p>
<p>Haute disponibilité</p>
<p>Réseau</p></td>
<td><p>ImapCTPMonitor (indicateur d'intégrité IMAP)</p></td>
</tr>
<tr class="even">
<td><p>ImapProxyTestProbe</p></td>
<td><p>IMAP.Proxy</p></td>
<td><p>Active Directory</p>
<p>Authentification</p></td>
<td><p>ImapProxyTestMonitor (indicateur d'intégrité IMAP.Proxy)</p></td>
</tr>
<tr class="odd">
<td><p>ImapDeepTestProbe</p></td>
<td><p>IMAP.Protocol</p></td>
<td><p>Active Directory</p>
<p>Authentification</p>
<p>Banque d'informations</p>
<p>Haute disponibilité</p></td>
<td><p>IMAP.Protocol (indicateur d'intégrité IMAP.Protocol)</p></td>
</tr>
<tr class="even">
<td><p>ImapSelfTestProbe</p></td>
<td><p>IMAP.Protocol</p></td>
<td><p>Active Directory</p>
<p>Authentification</p></td>
<td><p>IMAP.Protocol (indicateur d'intégrité IMAP.Protocol)</p>
<p>AverageCommandProcessingTimeGt60sMonitor (indicateur d'intégrité IMAP)</p></td>
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
        
        Par exemple, pour récupérer les détails de l'indicateur d'intégrité d'IMAP à propos de server1.contoso.com, exécutez la commande suivante :
        
            Get-ServerHealth server1.contoso.com | ?{$_.HealthSetName -like "IMAP*"}
    
    2.  Consultez la sortie de la commande pour déterminer quel moniteur a signalé l'erreur. La valeur **AlertValue** du moniteur qui a émis l'alerte sera `Unhealthy`.
    
    3.  Réexécutez la sonde associée pour le moniteur dont l'état n'est pas intègre. Pour rechercher la sonde associée, reportez-vous au tableau figurant dans la section Explanation. Pour ce faire, exécutez la commande suivante :
        
            Invoke-MonitoringProbe <health set name>\<probe name> -Server <server name> | Format-List
        
        Par exemple, supposons que le moniteur défectueux soit **ImapCTPMonitor**. La sonde associée à ce moniteur est **ImapCTPProbe**. Pour exécuter cette sonde sur server1.contoso.com, exécutez la commande suivante :
        
            Invoke-MonitoringProbe IMAP\ImapCTPProbe -Server server1.contoso.com | Format-List
    
    4.  Dans la sortie de la commande, consultez la valeur **Result** de la sonde. Si elle indique **Succeeded**, le problème était une erreur passagère, qui n'existe plus. Autrement, reportez-vous aux étapes de récupération décrites dans les sections suivantes.

## Actions de récupération ImapTestDeepMonitor et ImapSelfTestMonitor

1.  Redémarrez le service IMAP4 d'Exchange sur le serveur principal. Pour plus d'informations sur le démarrage et l'arrêt du service IMAP4, consultez la rubrique [Démarrer et arrêter les services IMAP4](https://technet.microsoft.com/fr-fr/library/bb124022\(v=exchg.150\)).

2.  Réexécutez la sonde associée en procédant de la manière décrite dans l'étape 2c de la section Verifying the issue still exists.

3.  Si le problème existe toujours, vous devez basculer les bases de données hébergées sur le serveur de boîtes aux lettres à l'aide de la commande suivante :
    
        Set-MailboxServer -Identity <ServerName> -DatabaseCopyActivationDisabledAndMoveNow $true

4.  Vérifiez que toutes les bases de données ont été déplacées hors du serveur qui signale le problème. Pour ce faire, exécutez la commande suivante :
    
        Get-MailboxDatabaseCopyStatus -Server server1.contoso.com | Group Status
    
    Si la sortie de la commande n'affiche aucune copie active sur le serveur, redémarrez ce dernier.

5.  Réexécutez la sonde associée en procédant de la manière décrite dans l'étape 2c de la section Verifying the issue still exists.

6.  Si la sonde réussit, basculez les bases de données en exécutant la commande suivante :
    
        Set-MailboxServer server1.contoso.com -DatabaseCopyActivationDisabledAndMoveNow $false

7.  En cas de nouvel échec de la sonde, il se peut que vous ayez besoin d'aide pour résoudre ce problème. Contactez un professionnel du Support Technique de Microsoft pour résoudre ce problème. Pour contacter un professionnel du Support Technique de Microsoft, consultez [Exchange Server Solutions Center](http://go.microsoft.com/fwlink/p/?linkid=180809). Dans le volet de navigation, cliquez sur **Ressources et options de support** et utilisez l'une des options indiquées sous **Obtenez du support technique** pour contacter un professionnel du support Microsoft. Étant donné que votre organisation peut avoir une procédure spécifique pour contacter directement les Services de Support Technique Microsoft, assurez-vous de connaître d'abord les instructions propres à votre organisation.

## Actions de récupération ImapCTPMonitor

Cette alerte de moniteur est généralement émise sur des serveurs CAS.

1.  Redémarrez le service IMAP4 d'Exchange sur le serveur principal. Pour plus d'informations sur le démarrage et l'arrêt du service IMAP4, consultez la rubrique [Démarrer et arrêter les services IMAP4](https://technet.microsoft.com/fr-fr/library/bb124022\(v=exchg.150\)).

2.  Réexécutez la sonde associée de la manière décrite dans l'étape 2c de la section Verifying the issue still exists.

3.  Si le problème persiste, vous devez activer la journalisation du protocole IMAP afin d'aider à résoudre le problème. Pour ce faire, procédez comme suit :
    
    1.  Dans Windows PowerShell, exécutez la commande suivante :
        
            Set-ImapSettings -server <CAS server name> -ProtocolLoggingEnabled $true
    
    2.  Redémarrez le service IMAP4 d'Exchange sur le serveur principal. Pour plus d'informations sur le démarrage et l'arrêt du service IMAP4, consultez la rubrique [Démarrer et arrêter les services IMAP4](https://technet.microsoft.com/fr-fr/library/bb124022\(v=exchg.150\)).
    
    3.  Réexécutez la sonde associée en procédant de la manière décrite dans l'étape 2c de la section Verifying the issue still exists.
    
    4.  Exécutez la commande suivante, puis déterminez l'emplacement du fichier journal. Pour ce faire, exécutez la commande suivante :
        
            Get-ImapSettings -server <CAS server name>
    
    5.  Identifiez la boîte aux lettres qui utilise cette commande. Le nom du serveur de boîtes aux lettres est la valeur correspondant à `_Mbx:` dans le message d'erreur.
    
    6.  Exécutez la commande suivante :
        
            Get-ServerHealth mailbox1.contoso.com | ?{$_.HealtSetName -like "IMAP*"}
        
        **Remarque**   Dans cette commande, remplacez *mailbox1.contoso.com* par le nom réel du serveur de boîtes aux lettres.
    
    7.  Si des moniteurs répertoriés dans la sortie de la commande présentent un manque d'intégrité, vous devez d'abord résoudre les problèmes concernant ces moniteurs. Suivez les étapes de résolution des problèmes décrites dans la section ImapTestDeepMonitor and ImapSelfTestMonitor Recovery Actions.

4.  Si le serveur de base de données est intègre, redémarrez le serveur d'accès au client.

5.  Une fois le serveur redémarré, réexécutez la sonde associée en procédant de la manière décrite dans l'étape 2c de la section Verifying the issue still exists.

6.  Désactivez l'enregistrement dans le journal du protocole. Pour ce faire, exécutez la commande PowerShell Windows suivante :
    
        Set-ImapSettings -server <CAS server name> -ProtocolLoggingEnabled $false

7.  Redémarrez le service IMAP4.

8.  En cas de nouvel échec de la sonde, il se peut que vous ayez besoin d'aide pour résoudre ce problème. Contactez un professionnel du Support Technique de Microsoft pour résoudre ce problème. Pour contacter un professionnel du Support Technique de Microsoft, consultez [Exchange Server Solutions Center](http://go.microsoft.com/fwlink/p/?linkid=180809). Dans le volet de navigation, cliquez sur **Ressources et options de support** et utilisez l'une des options indiquées sous **Obtenez du support technique** pour contacter un professionnel du support Microsoft. Étant donné que votre organisation peut avoir une procédure spécifique pour contacter directement les Services de Support Technique Microsoft, assurez-vous de connaître d'abord les instructions propres à votre organisation.

## Actions de récupération ImapProxyTestMonitor

1.  Redémarrez le service IMAP4.

2.  Réexécutez la sonde associée en procédant de la manière décrite dans l'étape 2c de la section Verifying the issue still exists.

3.  Si la sonde échoue encore, redémarrez le serveur d'accès au client.

4.  Une fois le serveur redémarré, réexécutez la sonde associée en procédant de la manière décrite dans l'étape 2c de la section Verifying the issue still exists.

5.  En cas de nouvel échec de la sonde, il se peut que vous ayez besoin d'aide pour résoudre ce problème. Contactez un professionnel du Support Technique de Microsoft pour résoudre ce problème. Pour contacter un professionnel du Support Technique de Microsoft, consultez [Exchange Server Solutions Center](http://go.microsoft.com/fwlink/p/?linkid=180809). Dans le volet de navigation, cliquez sur **Ressources et options de support** et utilisez l'une des options indiquées sous **Obtenez du support technique** pour contacter un professionnel du support Microsoft. Étant donné que votre organisation peut avoir une procédure spécifique pour contacter directement les Services de Support Technique Microsoft, assurez-vous de connaître d'abord les instructions propres à votre organisation.

## Actions de récupération AverageCommandProcessingTimeGt60sMonitor RequestsQueuedGt500Monitor

Cette alerte de moniteur est généralement émise sur des serveurs d'autorités de certification et de boîtes aux lettres.

1.  Redémarrez le service IMAP4 d'Exchange sur le serveur principal ou sur le serveur d'accès au client. Pour plus d'informations sur le démarrage et l'arrêt du service IMAP4, consultez la rubrique [Démarrer et arrêter les services IMAP4](https://technet.microsoft.com/fr-fr/library/bb124022\(v=exchg.150\)).

2.  Patientez 10 minutes pour voir si le moniteur reste intègre. Après ce délai, exécutez la commande suivante :
    
        Get-ServerHealth server1.contoso.com | ?{$_.HealthSetName -like "IMAP*"}
    
    **Remarque**   Dans cette commande, remplacez *server1.contoso.com* par le nom réel du serveur.

3.  Patientez 10 minutes, puis réexécutez la commande décrite dans l'étape 2 pour voir si le moniteur reste intègre.

4.  Si le problème persiste, vous devez redémarrer le serveur. Si le serveur est un serveur d'accès au client, redémarrez simplement le serveur. Si le serveur est un serveur de boîtes aux lettres, procédez comme suit :
    
    1.  Basculez les bases de données hébergées sur le serveur. Pour ce faire, exécutez la commande suivante :
        
            Set-MailboxServer server1.contoso.com -DatabaseCopyActivationDisabledAndMoveNow $true
        
        **Remarque**   Dans cet exemple de code et dans tous les exemples de code suivants, remplacez *server1.contoso.com* par le nom réel du serveur.
    
    2.  Vérifiez que toutes les bases de données ont été déplacées hors du serveur qui signale le problème. Pour ce faire, exécutez la commande suivante :
        
            Get-MailboxDatabaseCopyStatus -Server server1.contoso.com | Group Status
        
        Si la sortie de la commande n'affiche aucune copie active sur le serveur, redémarrez ce dernier.

5.  Après le redémarrage du serveur, patientez 10 minutes, puis réexécutez la commande décrite dans l'étape 2 pour voir si le moniteur reste intègre.

6.  Si le moniteur reste intègre et s'il s'agit d'un serveur de boîtes aux lettres, basculez les bases de données en exécutant la commande suivante :
    
        Set-MailboxServer server1.contoso.com -DatabaseCopyActivationDisabledAndMoveNow $false

7.  En cas de nouvel échec de la sonde, il se peut que vous ayez besoin d'aide pour résoudre ce problème. Contactez un professionnel du Support Technique de Microsoft pour résoudre ce problème. Pour contacter un professionnel du Support Technique de Microsoft, consultez [Exchange Server Solutions Center](http://go.microsoft.com/fwlink/p/?linkid=180809). Dans le volet de navigation, cliquez sur **Ressources et options de support** et utilisez l'une des options indiquées sous **Obtenez du support technique** pour contacter un professionnel du support Microsoft. Étant donné que votre organisation peut avoir une procédure spécifique pour contacter directement les Services de Support Technique Microsoft, assurez-vous de connaître d'abord les instructions propres à votre organisation.

## Pour plus d'informations

[POP3 et IMAP4](https://technet.microsoft.com/fr-fr/library/jj657728\(v=exchg.150\))

[Activer IMAP4 dans Exchange 2013](https://technet.microsoft.com/fr-fr/library/bb124489\(v=exchg.150\))

[Test-ImapConnectivity](https://technet.microsoft.com/fr-fr/library/bb738126\(v=exchg.150\))

