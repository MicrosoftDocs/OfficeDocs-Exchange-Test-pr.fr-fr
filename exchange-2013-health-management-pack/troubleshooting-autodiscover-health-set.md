---
title: Dépannage de l'indicateur d'intégrité Autodiscover
TOCTitle: Dépannage de l'indicateur d'intégrité Autodiscover
ms:assetid: bc933621-df73-4d1d-bdef-825b98be8e09
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/ms.exch.scom.autodiscover(v=EXCHG.150)
ms:contentKeyID: 53276482
ms.date: 02/05/2016
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Dépannage de l'indicateur d'intégrité Autodiscover

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2015-03-09_

L'indicateur d'intégrité Autodiscover surveille l'intégrité globale du service de découverte automatique pour les clients.

Si vous recevez une alerte indiquant qu'Autodiscover présente un manque d'intégrité, cela signifie qu'un problème empêche probablement les utilisateurs d'accéder à leur boîte aux lettres à l'aide du processus de découverte automatique.

## Explication

Le service de découverte automatique est surveillé à l'aide des sondes et moniteurs suivants.


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
<td><p>AutodiscoverCtpProbe</p></td>
<td><p>Découverte automatique</p></td>
<td><p>Active Directory</p></td>
<td><p>AutodiscoverCtpMonitor</p></td>
</tr>
</tbody>
</table>


Pour plus d'informations sur les sondes et les moniteurs, consultez la rubrique [État et performances du serveur](https://technet.microsoft.com/fr-fr/library/jj150551\(v=exchg.150\)).

## Problèmes courants

Cette sonde peut échouer pour les raisons courantes suivantes :

  - Le pool d'applications de découverte automatique (MSExchangeAutodiscoverAppPool) hébergé sur le serveur d'accès au client surveillé ne répond pas. Ou le pool d'applications de découverte automatique hébergé sur un ou plusieurs serveurs de boîtes aux lettres ne répond pas.

  - Le serveur d'accès au client rencontre des problèmes de réseau et ne peut pas se connecter au serveur de boîtes aux lettres ou au contrôleur de domaine.

  - Les informations d'identification du compte assurant le contrôle sont incorrectes.

  - Les contrôleurs de domaine ne répondent pas.

## Action de l'utilisateur

Il se peut que le service ait récupéré après avoir émis l’alerte. Par conséquent, quand vous recevez une alerte signalant que l'indicateur d'intégrité n'est pas intègre, vérifiez tout d'abord que le problème existe toujours. Si tel est le cas, exécutez les actions de récupération appropriées décrites dans les sections suivantes.

## Vérification de l'existence du problème

1.  Repérez les noms de l'indicateur d'intégrité et du serveur dans l'alerte.

2.  Les détails du message fournissent des informations sur la cause exacte de l'alerte. Le plus souvent, le message fournit des informations de dépannage suffisantes pour identifier la cause première. Si les détails du message ne sont pas clairs, procédez comme suit :
    
    1.  Ouvrez Environnement de ligne de commande Exchange Management Shell, puis exécutez la commande suivante pour récupérer les détails de l'indicateur d'intégrité qui a émis l'alerte :
        
            Get-ServerHealth <server name> | ?{$_.HealthSetName -eq "<health set name>"}
        
        Par exemple, pour récupérer les détails de l'indicateur d'intégrité Autodiscover à propos de server1.contoso.com, exécutez la commande suivante :
        
            Get-ServerHealth server1.contoso.com | ?{$_.HealthSetName -eq "Autodiscover"}
    
    2.  Consultez la sortie de la commande pour déterminer quel moniteur a signalé l'erreur. La valeur **AlertValue** du moniteur qui a émis l'alerte est `Unhealthy`.
    
    3.  Réexécutez la sonde associée pour le moniteur dont l’état d’intégrité est défectueux. Pour rechercher la sonde associée, reportez-vous au tableau figurant dans la section Explanation. Pour ce faire, exécutez la commande suivante :
        
            Invoke-MonitoringProbe <health set name>\<probe name> -Server <server name> | Format-List
        
        Par exemple, supposons que le moniteur défectueux soit **AutodiscoverCtpMonitor**. La sonde associée à ce moniteur est **AutodiscoverCtpProbe**. Pour exécuter cette sonde sur server1.contoso.com, exécutez la commande suivante :
        
            Invoke-MonitoringProbe Autodiscover\AutodiscoverCtpProbe -Server server1.contoso.com | Format-List
    
    4.  Dans la sortie de la commande, consultez la valeur **Result** de la sonde. Si elle indique **Succeeded**, le problème était une erreur passagère, qui n'existe plus. Autrement, reportez-vous aux étapes de récupération décrites dans les sections suivantes.

## Actions de récupération AutodiscoverCtpMonitor

Quand vous recevez une alerte de l'indicateur d'intégrité, le message électronique contient les informations suivantes :

  - nom du serveur ayant envoyé l'alerte ;

  - nom du serveur de boîtes aux lettres que la sonde surveillait ;

  - heure et date de l'alerte ;

  - mécanisme d'authentification utilisé et informations d'identification ;

  - trace d'exception complète de la dernière erreur, notamment données de diagnostic et informations d'en-tête HTTP spécifiques.

Vous pouvez utiliser les informations contenues dans la trace de l'exception complète pour résoudre le problème. L'exception générée par la sonde contient un motif de l'échec qui décrit pourquoi la sonde a échoué. Par exemple, le motif de l'échec peut être l'un des suivants :

  - **X-FEServer**   Indique le CAS sur lequel la sonde a été exécutée

  - **X-CalculatedBETarget**   Indique le serveur de boîtes aux lettres vers lequel la demande est acheminée

  - **X-DiagInfo**   Indique le serveur de boîtes aux lettres qui a reçu la demande

Pour résoudre ce problème, procédez comme suit :

1.  Examinez les journaux du protocole sur les serveurs d'accès au client et de boîte aux lettres. Par défaut, les journaux de protocole sur le serveur d'accès au client sont situés dans le dossier ***\<répertoire d'installation d'Exchange Server\>*\\Logging\\HttpProxy\\Autodiscover**. Par défaut, les fichiers journaux du protocole sur le serveur de boîtes aux lettres sont situés dans le dossier ***\<répertoire d'installation d'Exchange Server\>*\\Logging\\Autodiscover**.

2.  Créez un compte d'utilisateur test, puis connectez-vous au CAS en utilisant ce compte. Par exemple, connectez-vous en utilisant : https://*\<nom de serveur\>*/autodiscover/autodiscover.xml
    
    Si le nom du compte d’utilisateur test réussit, il se peut qu’un problème existe le serveur de boîtes aux lettres qui héberge la boîte aux lettres surveillée.
    
    Essayez de répéter les étapes précédentes en utilisant un compte test sur le serveur de boîtes aux lettres. Si cette tentative échoue, essayez d'effectuer un test sur un autre serveur d'accès au client afin de vérifier que le problème se produit sur un serveur d'accès au client spécifique et non sur le serveur de boîtes aux lettres.

3.  Vérifiez la connectivité réseau entre les serveurs d'accès au client et de boîtes aux lettres. Utilisez ping.exe pour vérifier que tous les serveurs répondent.

4.  Recherchez dans l'indicateur d'intégrité Autodiscover.Proxy les alertes indiquant qu'un problème affecte un serveur de boîtes aux lettres spécifique. Pour plus d'informations, consultez la rubrique [Dépannage de l'indicateur d'intégrité Autodiscover.Proxy](troubleshooting-autodiscover-proxy-health-set.md).

5.  Recherchez dans l'indicateur d'intégrité Autodiscover.Protocol les alertes indiquant qu'un problème affecte des serveurs de boîtes aux lettres spécifiques. Pour plus d'informations, consultez la rubrique [Dépannage de l'indicateur d'intégrité Autodiscover.Protocol](troubleshooting-autodiscover-protocol-health-set.md).

6.  Démarrez le Gestionnaire des services Internet, puis connectez-vous au serveur qui signale le problème. Vérifiez que le pool d'applications **MSExchangeAutodiscoverAppPool** est exécuté sur les serveurs d'accès au client et de boîtes aux lettres.

7.  Dans le Gestionnaire des services Internet, cliquez sur **Pools d'applications**, puis recyclez le pool d'applications **MSExchangeAutodiscoverAppPool** en exécutant la commande suivante à partir de l'environnement de ligne de commande Exchange Management Shell :
    
        %SystemRoot%\System32\inetsrv\Appcmd recycle MSExchangeAutodiscoverAppPool

8.  Réexécutez la sonde associée en procédant de la manière décrite dans l'étape 2c de la section Verifying the issue still exists.

9.  Si le problème persiste, recyclez le service IIS à l'aide de l'utilitaire IISReset ou en exécutant la commande suivante :
    
        Iisreset /noforce

10. Réexécutez la sonde associée en procédant de la manière décrite dans l'étape 2c de la section Verifying the issue still exists.

11. Si le problème persiste, redémarrez le serveur.

12. Une fois le serveur redémarré, réexécutez la sonde associée en procédant de la manière décrite dans l'étape 2c de la section Verifying the issue still exists.

13. En cas de nouvel échec de la sonde, il se peut que vous ayez besoin d'aide pour résoudre ce problème. Contactez un professionnel du Support Technique de Microsoft pour résoudre ce problème. Pour contacter un professionnel du Support Technique de Microsoft, consultez [Exchange Server Solutions Center](http://go.microsoft.com/fwlink/p/?linkid=180809). Dans le volet de navigation, cliquez sur **Ressources et options de support** et utilisez l'une des options indiquées sous **Obtenez du support technique** pour contacter un professionnel du support Microsoft. Étant donné que votre organisation peut avoir une procédure spécifique pour contacter directement les Services de Support Technique Microsoft, assurez-vous de connaître d'abord les instructions propres à votre organisation.

## Pour plus d'informations

[Nouveautés d'Exchange 2013](https://technet.microsoft.com/fr-fr/library/jj150540\(v=exchg.150\))

[Cmdlets Exchange 2013](https://technet.microsoft.com/fr-fr/library/bb124413\(v=exchg.150\))

