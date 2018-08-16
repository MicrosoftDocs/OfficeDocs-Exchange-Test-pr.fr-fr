---
title: Dépannage de l'indicateur d'intégrité EWS
TOCTitle: Dépannage de l'indicateur d'intégrité EWS
ms:assetid: f5aaacdd-7f4a-4d63-8440-1c564e644dfc
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/ms.exch.scom.ews(v=EXCHG.150)
ms:contentKeyID: 53276487
ms.date: 02/05/2016
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Dépannage de l'indicateur d'intégrité EWS

 

_**Sapplique à :** Exchange Server 2013, Project Server 2013_

_**Dernière rubrique modifiée :** 2015-03-09_

L'indicateur d'intégrité des services web Exchange (EWS) surveille l'intégrité globale du service EWS. L'indicateur d'intégrité EWS est étroitement lié aux indicateurs d'intégrité suivants :

[Dépannage de l'indicateur d'intégrité EWS.Protocol](troubleshooting-ews-protocol-health-set.md)

[Dépannage de l'indicateur d'intégrité EWS.Proxy](troubleshooting-ews-proxy-health-set.md)

Si vous recevez une alerte indiquant qu'EWS présente un manque d'intégrité, cela signifie qu'un problème empêche probablement les utilisateurs de communiquer avec le serveur Exchange.

## Explication

EWS est surveillé à l'aide des sondes et moniteurs suivants.


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
<td><p>EwsCtpProbe</p></td>
<td><p>EWS</p></td>
<td><p>Banque d'informations</p>
<p>Services de domaine Active Directory (AD DS)</p></td>
<td><p>EwsCtpMonitor (indicateur d'intégrité EWS)</p></td>
</tr>
<tr class="even">
<td><p>EwsSelfTestProbe</p></td>
<td><p>EWS.Protocol</p></td>
<td><p>Services de domaine Active Directory (AD DS)</p></td>
<td><p>EWSSelfTestMonitor</p></td>
</tr>
<tr class="odd">
<td><p>EwsDeepTestProbe</p></td>
<td><p>EWS.Protocol</p></td>
<td><p>Banque d'informations</p></td>
<td><p>EWSDeepTestMonitor</p></td>
</tr>
</tbody>
</table>


Cette sonde établit une connexion EWS complète à partir du serveur d'accès au client (CAS) à un serveur de boîtes aux lettres à l'aide d'un compte de surveillance. Cette sonde appelle la méthode **GetFolder** sur EWS. Pour plus d'informations sur les sondes et les moniteurs, consultez la rubrique [État et performances du serveur](https://technet.microsoft.com/fr-fr/library/jj150551\(v=exchg.150\)).

## Problèmes courants

Cette sonde peut échouer pour les raisons courantes suivantes :

  - Il existe une discordance entre le mécanisme d'authentification utilisé par la sonde et celui utilisé sur le répertoire virtuel du CAS.

  - Le pool d’applications EWS dans le CAS surveillé ne répond pas.

  - Le CAS rencontre des problèmes de réseau quand il se connecte au serveur de boîtes aux lettres.

  - Le CAS rencontre des problèmes de communication quand il se connecte aux contrôleurs de domaine.

  - Les contrôleurs de domaine ne répondent pas.

  - Le pool d'applications EWS résidant sur un ou plusieurs serveurs de boîtes aux lettres ne répond pas.

  - La base de données de l’utilisateur n’est pas montée ou le service Banque d’informations n’est pas disponible pour une boîte aux lettres spécifique.

  - Le service Banque d'Informations sur un ou plusieurs services de boîtes aux lettres rencontre des problèmes.

## Action de l'utilisateur

Il se peut que le service ait récupéré après avoir émis l'alerte. Par conséquent, quand vous recevez une alerte signalant que l'indicateur d'intégrité n'est pas intègre, vérifiez tout d'abord que le problème existe toujours. Si tel est le cas, exécutez les actions de récupération appropriées décrites dans les sections suivantes.

## Vérification de l'existence du problème

1.  Repérez les noms de l'indicateur d'intégrité et du serveur dans l'alerte.
    
    Quand vous recevez une alerte en provenance de cet indicateur d'intégrité, le message électronique contient les données suivantes :
    
    1.  nom du CAS qui a émis l'alerte ;
    
    2.  nom du serveur de boîtes aux lettres que la sonde surveillait en tant que ressource cible ;
    
    3.  trace d'exception complète de la dernière erreur, notamment données de diagnostic et informations d'en-tête HTTP spécifiques ;
    
    4.  heure de l'incident ;
    
    5.  mécanisme d'authentification utilisé et informations d'identification.
    
    Les informations sur la trace d'exception constituent l'indication la plus importante concernant la cause de l'échec de la sonde. Le message d'escalade contient également les en-têtes HTTP suivants :
    
    1.  **X-FEServer**   Indique le CAS sur lequel la sonde a été exécutée
    
    2.  **X-TargetBEServer**   Indique le serveur MBX vers lequel la demande a été routée
    
    3.  **X-DiagInfo**   Indique le serveur MBX qui a reçu la demande

2.  Les détails du message fournissent des informations sur la cause exacte de l'alerte. Le plus souvent, le message fournit des informations de dépannage suffisantes pour identifier la cause première. Si les détails du message ne sont pas clairs, procédez comme suit :
    
    1.  Ouvrez Environnement de ligne de commande Exchange Management Shell, puis exécutez la commande suivante pour récupérer les détails de l'indicateur d'intégrité qui a émis l'alerte :
        
            Get-ServerHealth <server name> | ?{$_.HealthSetName -eq "<health set name>"}
        
        Par exemple, pour récupérer les détails de l'indicateur d'intégrité EWS à propos de server1.contoso.com, exécutez la commande suivante :
        
            Get-ServerHealth server1.contoso.com | ?{$_.HealthSetName -eq "EWS"}
    
    2.  Consultez la sortie de la commande pour déterminer quel moniteur a signalé l'erreur. La valeur **AlertValue** du moniteur qui a émis l'alerte sera `Unhealthy`.
    
    3.  Réexécutez la sonde associée pour le moniteur dont l'état d'intégrité est douteux. Pour rechercher la sonde associée, reportez-vous au tableau figurant dans la section Explanation. Pour ce faire, exécutez la commande suivante :
        
            Invoke-MonitoringProbe <health set name>\<probe name> -Server <server name> | Format-List
        
        Pour l'indicateur d'intégrité EWS, supposons que le moniteur défaillant est **EWSCtpMonitor**. La sonde associée à ce moniteur est **EWSCtpProbe**. Pour exécuter cette sonde sur server1.contoso.com, exécutez la commande suivante :
        
            Invoke-MonitoringProbe EWS\EWSCtpProbe -Server server1.contoso.com | Format-List
    
    4.  Dans la sortie de la commande, consultez la valeur **Result** de la sonde. Si elle indique **Succeeded**, le problème était une erreur passagère, qui n'existe plus. Autrement, reportez-vous aux étapes de récupération décrites dans les sections suivantes.

## Actions de récupération EwsCtpMonitor

1.  Démarrez le Gestionnaire des services Internet, puis connectez-vous au serveur signalant le problème afin de déterminer si le pool d’applications **MSExchangeServicesAppPool** est en cours d’exécution sur le CAS et sur le serveur de boîtes aux lettres.

2.  Identifiez la MailboxDatabase à l'origine de l'échec des sondes. Ensuite, vérifiez que la base de données de boîtes aux lettres est active pour le serveur de boîtes aux lettres, et que la Banque d'informations est intègre.

3.  Cliquez sur **Pools d'applications**, puis recyclez le pool d'applications **MSExchangeServicesAppPool** en exécutant la commande suivante à partir de l'environnement de ligne de commande Exchange Management Shell :
    
        %SystemRoot%\System32\inetsrv\Appcmd recycle MSExchangeServicesAppPool

4.  Réexécutez la sonde associée en procédant de la manière décrite dans l'étape 2c de la section Verifying the issue still exists.

5.  Si le problème persiste, recyclez la totalité du service IIS à l'aide de l'utilitaire IISReset.

6.  Réexécutez la sonde associée en procédant de la manière décrite dans l'étape 2c de la section Verifying the issue still exists.

7.  Si le problème persiste, consultez les fichiers journaux de protocole sur le CAS et le serveur de boîtes aux lettres. Les journaux du protocole pour le CAS résident dans le dossier *\<répertoire d'installation du serveur Exchange\>\\Logging\\HttpProxy\\Ews*. Sur le serveur de boîtes aux lettres, les journaux résident dans le dossier *\<répertoire d'installation du serveur Exchange\>\\Logging\\Ews*.

8.  Créez un compte d'utilisateur test, puis connectez-vous au CAS en utilisant ce compte. Par exemple, connectez-vous en utilisant : https:// \<nom de serveur\>/ews/exchange.asmx. Si le problème persiste, essayez un autre CAS pour déterminer si le problème s'étend à ce CAS et non au serveur de boîtes aux lettres. Si le nom d'utilisateur test passe, il se peut qu'un problème affecte la base de données de boîtes aux lettres concernée ou le serveur de boîtes aux lettres sur lequel se trouve la boîte aux lettres de surveillance. Essayez de répéter cette étape en utilisant un compte test existant dans la base de données de boîtes aux lettres.

9.  Vérifiez la connectivité réseau entre le CAS et le serveur de boîtes aux lettres.

10. Recherchez dans l'indicateur d'intégrité EWS.Proxy les alertes indiquant qu'un problème affecte un CAS spécifique.

11. Recherchez dans l'indicateur d'intégrité EWS.Protocol les alertes indiquant qu'un problème affecte un serveur de boîtes aux lettres spécifique.

12. Si le problème persiste, redémarrez le serveur. Pour ce faire, commencez par basculer les bases de données hébergées sur le serveur. Pour ce faire, exécutez la commande suivante :
    
        Set-MailboxServer server1.contoso.com -DatabaseCopyActivationDisabledAndMoveNow $true
    
    **Remarque**   Dans cet exemple de code et dans tous les exemples de codes suivants, remplacez *server1.contoso.com* par le nom réel du serveur.

13. Vérifiez que toutes les bases de données ont été déplacées hors du serveur qui signale le problème. Pour ce faire, exécutez la commande suivante :
    
        Get-MailboxDatabaseCopyStatus -Server server1.contoso.com | Group Status
    
    Si la sortie de la commande n'affiche aucune copie active sur le serveur, redémarrez ce dernier.

14. Une fois le serveur redémarré, réexécutez la sonde associée en procédant de la manière décrite dans l'étape 2c de la section Verifying the issue still exists.

15. Si la sonde réussit, basculez de nouveau les bases de données vers le serveur de boîtes aux lettres en exécutant la commande suivante :
    
        Set-MailboxServer server1.contoso.com -DatabaseCopyActivationDisabledAndMoveNow $false

16. Si l'échec de la sonde persiste, vous avez peut-être besoin d'assistance pour résoudre le problème. Contactez un professionnel du Support Technique de Microsoft pour résoudre ce problème. Pour contacter un professionnel du Support Technique de Microsoft, consultez [Exchange Server Solutions Center](http://go.microsoft.com/fwlink/p/?linkid=180809). Dans le volet de navigation, cliquez sur **Ressources et options de support** et utilisez l'une des options indiquées sous **Obtenez du support technique** pour contacter un professionnel du support Microsoft. Étant donné que votre organisation peut avoir une procédure spécifique pour contacter directement les Services de Support Technique Microsoft, assurez-vous de connaître d'abord les instructions propres à votre organisation.

## Pour plus d'informations

[Cmdlets Exchange 2013](https://technet.microsoft.com/fr-fr/library/bb124413\(v=exchg.150\))

[Nouveautés d'Exchange 2013](https://technet.microsoft.com/fr-fr/library/jj150540\(v=exchg.150\))

