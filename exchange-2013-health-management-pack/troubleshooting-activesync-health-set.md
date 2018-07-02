---
title: Dépannage de l'indicateur d'intégrité ActiveSync
TOCTitle: Dépannage de l'indicateur d'intégrité ActiveSync
ms:assetid: 8a0b8b26-b4ef-41b8-8f71-8271c1735a69
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/ms.exch.scom.activesync(v=EXCHG.150)
ms:contentKeyID: 53276471
ms.date: 02/05/2016
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Dépannage de l'indicateur d'intégrité ActiveSync

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2015-03-09_

L'indicateur d'intégrité Exchange ActiveSync surveille l'intégrité globale du service ActiveSync pour les clients mobiles au sein de votre organisation. L'indicateur d'intégrité ActiveSync est étroitement lié aux indicateurs d'intégrité suivants :

[Dépannage de l'indicateur d'intégrité ActiveSync.Protocol](troubleshooting-activesync-protocol-health-set.md)

[Dépannage de l'indicateur d'intégrité ActiveSync.Proxy](troubleshooting-activesync-proxy-health-set.md)

Si vous recevez une alerte indiquant que l'indicateur d'intégrité ActiveSync présente un manque d'intégrité, cela signifie qu'un problème empêche probablement les utilisateurs d'accéder à leur boîte aux lettres à l'aide d'ActiveSync.

## Explication

Le service ActiveSync est surveillé à l'aide des sondes et moniteurs suivants.


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
<td><p>ActiveSyncCTPProbe</p></td>
<td><p>ActiveSync</p></td>
<td><p>Active Directory</p>
<p>Authentification</p>
<p>Authentification du serveur de boîtes aux lettres</p>
<p>Banque d'informations</p>
<p>Haute disponibilité</p>
<p>Réseau</p></td>
<td><p>ActiveSyncCTPMonitor (indicateur d'intégrité ActiveSync)</p></td>
</tr>
<tr class="even">
<td><p>ActiveSyncProxyTestProbe</p></td>
<td><p>ActiveSync.Proxy</p></td>
<td><p>-</p></td>
<td><p>ActiveSyncProxyTestMonitor (indicateur d'intégrité ActiveSync.Proxy)</p></td>
</tr>
<tr class="odd">
<td><p>ActiveSyncDeepTestProbe</p></td>
<td><p>ActiveSync.Protocol</p></td>
<td><p>Active Directory</p>
<p>Authentification</p>
<p>Banque d'informations</p>
<p>Haute disponibilité</p></td>
<td><p>ActiveSyncDeepTestMonitor (indicateur d'intégrité ActiveSync)</p></td>
</tr>
<tr class="even">
<td><p>ActiveSyncSelfTestProbe</p></td>
<td><p>ActiveSync.Protocol</p></td>
<td><p>Active Directory</p>
<p>Authentification</p></td>
<td><p>ActiveSyncSelfTestMonitor (indicateur d'intégrité ActiveSync.Protocol)</p>
<p>RequestsQueuedGt500Monitor (indicateur d'intégrité ActiveSync)</p></td>
</tr>
</tbody>
</table>


Pour plus d'informations sur les sondes et les moniteurs, consultez la rubrique [État et performances du serveur](https://technet.microsoft.com/fr-fr/library/jj150551\(v=exchg.150\)).

## Action de l'utilisateur

Il se peut que le service ait récupéré après avoir émis l'alerte. Par conséquent, quand vous recevez une alerte indiquant que l'indicateur d'intégrité ActiveSync présente un manque d'intégrité, vérifiez tout d'abord que le problème existe toujours. Si tel est le cas, exécutez les actions de récupération appropriées décrites dans les sections suivantes.

## Vérification du problème

1.  Repérez le nom de l’indicateur d’intégrité et celui du serveur dans l’alerte.

2.  Les détails du message fournissent des informations sur la cause exacte de l’alerte. Dans la plupart des cas, ils fournissent des informations de dépannage suffisantes pour identifier la cause première. Si les détails du message ne sont pas clairs, procédez comme suit :
    
    1.  Ouvrez Environnement de ligne de commande Exchange Management Shell, puis exécutez la commande suivante pour récupérer les détails de l'indicateur d'intégrité qui a émis l'alerte :
        
            Get-ServerHealth <server name> | ?{$_.HealthSetName -eq "<health set name>"}
        
        Par exemple, pour récupérer les détails de l'indicateur d'intégrité ActiveSync à propos de server1.contoso.com, exécutez la commande suivante :
        
            Get-ServerHealth server1.contoso.com | ?{$_.HealthSetName -eq "ActiveSync"}
    
    2.  Consultez la sortie de la commande pour déterminer quel moniteur a signalé l'erreur. La valeur **AlertValue** du moniteur qui a émis l'alerte sera **Défectueux**.
    
    3.  Réexécutez la sonde associée pour le moniteur dont l’état d’intégrité est défectueux. Pour rechercher la sonde associée, reportez-vous au tableau figurant dans la section Explanation. Pour ce faire, exécutez la commande suivante :
        
            Invoke-MonitoringProbe <health set name>\<probe name> -Server <server name> | Format-List
        
        Par exemple, supposons que le moniteur défectueux soit **ActiveSyncCTPMonitor**. La sonde associée à ce moniteur est **ActiveSyncCTPProbe**. Pour exécuter cette sonde sur server1.contoso.com, exécutez la commande suivante :
        
            Invoke-MonitoringProbe ActiveSync\ActiveSyncCTPProbe -Server server1.contoso.com | Format-List
    
    4.  Dans la sortie de la commande, consultez la section « Result » de la sonde. Si elle indique **Succeeded**, le problème était une erreur passagère, qui n'existe plus. Autrement, reportez-vous aux étapes de récupération décrites dans les sections suivantes.

## Actions de récupération ActiveSyncDeepTestMonitor et ActiveSyncSelfTestMonitor

Cette alerte de moniteur est généralement émise sur des serveurs de boîtes aux lettres. Pour exécuter les actions de récupération, procédez comme suit :

1.  Démarrez le Gestionnaire des services Internet, puis connectez-vous au serveur qui signale le problème. Cliquez sur **Pools d’applications**, puis recyclez le pool d’applications ActiveSync nommé **MSExchangeSyncAppPool**.

2.  Réexécutez la sonde associée en procédant de la manière décrite dans l'étape 2c de la section Verifying the issue.

3.  Si le problème persiste, recyclez la totalité du service IIS à l'aide de l'utilitaire IISReset.

4.  Réexécutez la sonde associée en procédant de la manière décrite dans l'étape 2c de la section Verifying the issue.

5.  Si le problème persiste, redémarrez le serveur. Pour ce faire, basculez d'abord les bases de données hébergées sur le serveur à l'aide de la commande suivante :
    
        Set-MailboxServer server1.contoso.com -DatabaseCopyActivationDisabledAndMoveNow $true
    
    Dans cet exemple de code et dans tous les exemples de code suivants, remplacez *server1.contoso.com* par le nom réel du serveur.

6.  Ensuite, vérifiez que toutes les bases de données ont été déplacées hors du serveur qui signale le problème. Pour ce faire, exécutez la commande suivante :
    
        Get-MailboxDatabaseCopyStatus -Server server1.contoso.com | Group Status

7.  Si la sortie de la commande exécutée à l'étape 6 n'affiche aucune copie active sur le serveur, redémarrez ce dernier. Si la sortie ne montre pas de copie active, réexécutez les étapes 5 et 6.

8.  Une fois le serveur redémarré, réexécutez la sonde associée en procédant de la manière décrite dans l'étape 2c de la section Verifying the issue.

9.  Si la sonde réussit, basculez les bases de données en exécutant la commande suivante :
    
        Set-MailboxServer server1.contoso.com -DatabaseCopyActivationDisabledAndMoveNow $false

10. Si l'échec de la sonde persiste, vous avez peut-être besoin d'assistance pour résoudre le problème. Contactez un professionnel du Support Technique de Microsoft pour résoudre ce problème. Pour contacter un professionnel du Support Technique de Microsoft, consultez [Exchange Server Solutions Center](http://go.microsoft.com/fwlink/p/?linkid=180809). Dans le volet de navigation, cliquez sur **Ressources et options de support** et utilisez l'une des options indiquées sous **Obtenez du support technique** pour contacter un professionnel du support Microsoft. Étant donné que votre organisation peut avoir une procédure spécifique pour contacter directement les Services de Support Technique Microsoft, assurez-vous de connaître d'abord les instructions propres à votre organisation.

## Actions de récupération ActiveSyncCTPMonitor

Cette alerte de moniteur est généralement émise sur des serveurs CAS.

1.  Démarrez le Gestionnaire des services Internet, puis connectez-vous au serveur qui signale le problème. Cliquez sur **Pools d'applications**, puis recyclez le pool d'applications ActiveSync nommé **MSExchangeSyncAppPool**.

2.  Réexécutez la sonde associée en procédant de la manière décrite dans l'étape 2c de la section Verifying the issue.

3.  Si le problème persiste, recyclez la totalité du service IIS à l'aide de l'utilitaire IISReset.

4.  Réexécutez la sonde associée en procédant de la manière décrite dans l'étape 2c de la section Verifying the issue.

5.  Si le problème persiste, vous devez vérifier l'état d'intégrité sur le serveur de boîtes aux lettres correspondant. Le nom du serveur de boîtes aux lettres est la valeur `_Mbx:` indiquée dans le message d’erreur.
    
    1.  Exécutez la commande suivante pour le serveur de boîtes aux lettres approprié. Par exemple, exécutez la commande suivante pour un serveur de boîtes aux lettres nommé mailbox1.contoso.com :
        
            Get-ServerHealth mailbox1.contoso.com | ?{$_.HealtSetName -like "ActiveSync*"}
    
    2.  Si des moniteurs répertoriés dans la sortie de la commande présentent des problèmes d'intégrité, vous devez d'abord résoudre ces derniers. Pour ce faire, suivez les étapes de dépannage décrites dans la section ActiveSyncDeepTestMonitor and ActiveSyncSelfTestMonitor Recovery Actions.

6.  Si tous les moniteurs sur le serveur de boîtes aux lettres sont intègres, redémarrez le CAS.

7.  Une fois le serveur redémarré, réexécutez la sonde associée en procédant de la manière décrite dans l'étape 2c de la section Verifying the issue.

8.  Si l'échec de la sonde persiste, vous avez peut-être besoin d'assistance pour résoudre le problème. Contactez un professionnel du Support Technique de Microsoft pour résoudre ce problème. Pour contacter un professionnel du Support Technique de Microsoft, consultez [Exchange Server Solutions Center](http://go.microsoft.com/fwlink/p/?linkid=180809). Dans le volet de navigation, cliquez sur **Ressources et options de support** et utilisez l'une des options indiquées sous **Obtenez du support technique** pour contacter un professionnel du support Microsoft. Étant donné que votre organisation peut avoir une procédure spécifique pour contacter directement les Services de Support Technique Microsoft, assurez-vous de connaître d'abord les instructions propres à votre organisation.

## Actions de récupération RequestsQueuedGt500Monitor

Cette alerte de moniteur est généralement émise sur des serveurs CAS.

1.  Démarrez le Gestionnaire des services Internet, puis connectez-vous au serveur qui signale le problème. Cliquez sur **Pools d'applications**, puis recyclez le pool d'applications ActiveSync nommé **MSExchangeSyncAppPool**.

2.  Patientez 10 minutes pour voir si le moniteur reste intègre. Après 10 minutes, exécutez la commande suivante pour le serveur approprié. Par exemple, exécutez la commande suivante pour server1.contoso.com :
    
        Get-ServerHealth server1.contoso.com | ?{$_.HealthSetName -like "ActiveSync*"}

3.  Si le problème persiste, recyclez la totalité du service IIS à l'aide de l'utilitaire IISReset.

4.  Patientez 10 minutes, puis réexécutez la commande décrite dans l'étape 2 pour voir si le moniteur reste intègre.

5.  Si le problème persiste, redémarrez le serveur. Si le serveur est un serveur d'accès au client, redémarrez simplement le serveur. Si le serveur est un serveur de boîtes aux lettres, procédez comme suit :
    
    1.  Basculez les bases de données hébergées sur le serveur. Pour ce faire, exécutez la commande suivante :
        
            Set-MailboxServer server1.contoso.com -DatabaseCopyActivationDisabledAndMoveNow $true
        
        **Remarque**   Dans cet exemple de code et dans tous les exemples de codes suivants, remplacez *server1.contoso.com* par le nom réel du serveur.
    
    2.  Vérifiez que toutes les bases de données ont été déplacées hors du serveur qui signale le problème. Pour ce faire, exécutez la commande suivante :
        
            Get-MailboxDatabaseCopyStatus -Server server1.contoso.com | Group Status
        
        Si la sortie de la commande n'affiche aucune copie active sur le serveur, redémarrez ce dernier.

6.  Après le redémarrage du serveur, patientez 10 minutes, puis réexécutez la commande décrite dans l'étape 2 pour voir si le moniteur reste intègre.

7.  Si le moniteur reste intègre et s'il s'agit d'un serveur de boîtes aux lettres, basculez les bases de données en exécutant la commande suivante :
    
        Set-MailboxServer server1.contoso.com -DatabaseCopyActivationDisabledAndMoveNow $false

8.  Si l'échec de la sonde persiste, vous avez peut-être besoin d'assistance pour résoudre le problème. Contactez un professionnel du Support Technique de Microsoft pour résoudre ce problème. Pour contacter un professionnel du Support Technique de Microsoft, consultez [Exchange Server Solutions Center](http://go.microsoft.com/fwlink/p/?linkid=180809). Dans le volet de navigation, cliquez sur **Ressources et options de support** et utilisez l'une des options indiquées sous **Obtenez du support technique** pour contacter un professionnel du support Microsoft. Étant donné que votre organisation peut avoir une procédure spécifique pour contacter directement les Services de Support Technique Microsoft, assurez-vous de connaître d'abord les instructions propres à votre organisation.

## Pour plus d'informations

[Exchange ActiveSync](https://technet.microsoft.com/fr-fr/library/aa998357\(v=exchg.150\))

[Appareils mobiles](https://technet.microsoft.com/fr-fr/library/bb232129\(v=exchg.150\))

[Tâches de gestion des répertoires virtuels Exchange ActiveSync](https://technet.microsoft.com/fr-fr/library/bb125170\(v=exchg.150\))

