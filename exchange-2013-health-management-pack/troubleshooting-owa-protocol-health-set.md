---
title: Dépannage de l'indicateur d'intégrité OWA.Protocol
TOCTitle: Dépannage de l'indicateur d'intégrité OWA.Protocol
ms:assetid: fe172da8-65d3-43e0-ba62-d36a1b05fc11
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/ms.exch.scom.owa.protocol(v=EXCHG.150)
ms:contentKeyID: 53276488
ms.date: 02/05/2016
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Dépannage de l'indicateur d'intégrité OWA.Protocol

 

_**Sapplique à :**Exchange Server 2013_

_**Dernière rubrique modifiée :**2015-03-09_

L'indicateur d'intégrité OWA.Protocol surveille le protocole Outlook Web App sur le serveur de boîtes aux lettres.

Si vous recevez une alerte indiquant qu'OWA.Protocol présente un manque d'intégrité, cela signifie qu'un problème empêche probablement les utilisateurs d'accéder à leur boîte aux lettres à l'aide d'Outlook Web App.

## Explication

Le service OWA est contrôlé à l'aide des sondes et moniteurs suivants.


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
<td><p>OwaSelfTestProbe</p></td>
<td><p>OWA.Protocol</p></td>
<td><p>Aucun</p></td>
<td><p>OwaSelfTestMonitor</p></td>
</tr>
<tr class="even">
<td><p>OwaDeepTestProbe</p></td>
<td><p>OWA.Protocol</p></td>
<td><p>Active Directory</p>
<p>Banque d'informations</p></td>
<td><p>OwaDeepTestMonitor</p></td>
</tr>
</tbody>
</table>


La sonde **OwaSelfTestProbe** envoie une seule requête HTTP à l'adresse suivante : https://localhost:444/owa/exhealth.check. La sonde confirme que le pool d'applications répond en renvoyant le code d'état **200 OK**. Cette sonde ne dépend d'aucun autre composant Exchange.

La sonde **OwaDeepTestProbe** est exécutée sur chaque base de données de boîtes aux lettres à l'aide de copies sur le serveur actuel. La sonde permet d'établir qu'une ouverture de session complète est possible sur ce serveur. Pour ce faire, elle simule le type de trafic généré par un serveur d’accès au client (CAS) sur ce serveur spécifique. La sonde dépend des services de domaine Active Directory (AD DS) pour l'authentification, et de la banque de boîtes aux lettres pour l'accès aux boîtes aux lettres. Pour plus d'informations sur les sondes et les moniteurs, consultez la rubrique [État et performances du serveur](https://technet.microsoft.com/fr-fr/library/jj150551\(v=exchg.150\)).

## Problèmes courants

Cette sonde peut échouer pour les raisons courantes suivantes :

  - Le pool d’applications OWA hébergé sur le CAS contrôlé ne répond pas, ou le pool d’applications qui est hébergé sur le serveur de boîtes aux lettres ne répond pas.

  - Le serveur de boîtes aux lettres ou le CAS rencontre des problèmes de réseau, et il ne peut pas se connecter à l’autre serveur ou à un contrôleur de domaine.

  - Les informations d'identification du compte assurant le contrôle sont incorrectes.

  - La base de données de l’utilisateur n’est pas montée, ou la banque d’informations est inaccessible pour cette boîte aux lettres.

  - La banque d'informations ne répond pas.

  - Les contrôleurs de domaine ne répondent pas.

## Action de l'utilisateur

Il se peut que le service ait récupéré après avoir émis l'alerte. Par conséquent, quand vous recevez une alerte signalant que l'indicateur d'intégrité n'est pas intègre, vérifiez tout d'abord que le problème existe toujours. Si tel est le cas, exécutez les actions de récupération appropriées décrites dans les sections suivantes.

## Vérification de l'existence du problème

1.  Repérez les noms de l'indicateur d'intégrité et du serveur dans l'alerte.

2.  Les détails du message fournissent des informations sur la cause exacte de l'alerte. Le plus souvent, le message fournit des informations de dépannage suffisantes pour identifier la cause première. Si les détails du message ne sont pas clairs, procédez comme suit :
    
    1.  Ouvrez Environnement de ligne de commande Exchange Management Shell, puis exécutez la commande suivante pour récupérer les détails de l'indicateur d'intégrité qui a émis l'alerte :
        
            Get-ServerHealth <server name> | ?{$_.HealthSetName -eq "<health set name>"}
        
        Par exemple, pour récupérer les détails de l'indicateur d'intégrité OWA.Protocol à propos de server1.contoso.com, exécutez la commande suivante :
        
            Get-ServerHealth server1.contoso.com | ?{$_.HealthSetName -eq "OWA.Protocol"}
    
    2.  Consultez la sortie de la commande pour déterminer quel moniteur a signalé l'erreur. La valeur **AlertValue** du moniteur qui a émis l'alerte sera `Unhealthy`.
    
    3.  Réexécutez la sonde associée pour le moniteur dont l’état d’intégrité est défectueux. Pour rechercher la sonde associée, reportez-vous au tableau figurant dans la section Explanation. Pour ce faire, exécutez la commande suivante :
        
            Invoke-MonitoringProbe <health set name>\<probe name> -Server <server name> | Format-List
        
        Par exemple, supposons que le moniteur défectueux soit **OwaSelfTestMonitor**. La sonde associée à ce moniteur est **OwaSelfTestProbe**. Pour exécuter cette sonde sur server1.contoso.com, exécutez la commande suivante :
        
            Invoke-MonitoringProbe OWA.Protocol\OwaSelfTestProbe -Server server1.contoso.com | Format-List
    
    4.  Dans la sortie de la commande, consultez la valeur **Result** de la sonde. Si elle indique **Succeeded**, le problème était une erreur passagère, qui n'existe plus. Autrement, reportez-vous aux étapes de récupération décrites dans les sections suivantes.

Quand vous recevez une alerte de l'indicateur d'intégrité, le message électronique contient les informations suivantes :

  - nom du serveur ayant envoyé l'alerte ;

  - type de sonde défaillante (SelfTest ou DeepTest) ;

  - heure et date de l'alerte ;

  - chemin d'accès au dossier dans lequel figurent les traces de requête HTTP complètes associées à la sonde ;
    
      
    Par défaut les fichiers de trace se trouvent dans les dossiers suivants :
    
      - SelfTestProbe : \<*ExchangeServer*\>\\Logging\\Monitoring\\OWA\\ProtocolProbe
    
      - DeepTestProbe : \<*ExchangeServer*\>\\Logging\\Monitoring\\OWA\\MailboxProbe

  - trace d'exception complète de la dernière erreur, notamment données de diagnostic et informations d'en-tête HTTP spécifiques.  
    
    **Remarque**   Vous pouvez utiliser les informations contenues dans la trace de l'exception complète pour résoudre le problème. L'exception générée par la sonde contient un motif de l'échec décrivant pourquoi la sonde a échoué. Le motif de l'échec peut être l'un des problèmes suivants :
    
      - **MissingKeyword**   Un mot clé attendu ne figure pas dans la réponse du serveur. Dans ce cas, l'exception contient les mots clés attendus.
    
      - **NameResolution**   La résolution DNS ne parvient pas à résoudre un nom de serveur donné.
    
      - **NetworkConnection**   La sonde rencontre un échec de connexion réseau quand elle tente de se connecter au pool d'applications OWA sur CAFE.
    
      - **UnexpectedHttpResponseCode**   La réponse contient un code HTTP inattendu. Par exemple, le serveur a renvoyé un code HTTP **503**.
    
      - **RequestTimeout**   Le serveur a mis trop de temps à répondre à une demande du client.
    
      - **UnexpectedHttpResponseCode**   La réponse a renvoyé un code HTTP inattendu. Par exemple, le serveur a renvoyé un code HTTP **503**.
    
      - **ScenarioTimeout**   La sonde a fonctionné, mais son exécution a pris plus d'une minute. Ceci indique généralement un système qui est surchargé.
    
      - **OwaErrorPage**   OWA a renvoyé une page d'erreur. Le nom de l'erreur à l'origine de l'échec figure généralement dans le message d'exception.
    
      - **OwaMailboxErrorPage**   OWA a renvoyé une page d'erreur signalant une erreur en relation avec la banque de boîtes aux lettres. Cela indique généralement des problèmes tels qu'un arrêt de la banque de boîtes aux lettres, ou des boîtes aux lettres en cours de démontage.
    
    La trace de l'exception contient un champ important nommé **FailingComponent**, dans lequel la sonde s'efforce de déterminer et de catégoriser l'échec. Par exemple, la sonde peut renvoyer l'une des valeurs suivantes :
    
      - **Boîte aux lettres**   La sonde peut atteindre OWA, mais elle ne peut pas se connecter à la banque de boîtes aux lettres. Dans ce cas, la sonde est défaillante ou la latence d'accès à la boîte aux lettres a entraîné l'échec de la sonde et généré une erreur **ScenarioTimeout**. Lorsque des échecs de ce type se produisent, vous devez contrôler l'intégrité des serveurs de boîtes aux lettres.
    
      - **Active Directory**   La sonde peut atteindre OWA, mais elle ne peut pas se connecter à AD DS. Dans ce cas, soit la sonde est défaillante, soit les latences d'appel AD DS ont entraîné un dépassement de son délai d'exécution. En présence d'échecs de ce type, vous devez vérifier l'intégrité des contrôleurs de domaine, ainsi que les connexions réseau entre le CAS, les serveurs de boîtes aux lettres et les contrôleurs de domaine.
    
      - **OWA**   Cela signifie généralement qu'une erreur s'est produite à l'intérieur de la couche OWA. En présence d'échecs de ce type, vous devez vérifier l'intégrité du processus OWA sur le CAS et le serveur de boîtes aux lettres, ainsi que les connexions réseau.
    
    L'exception contient également la dernière requête HTTP et les informations de réponse reçues avant la défaillance de la sonde.  
      
    Le corps de l'escalade contient le chemin d'accès aux journaux de la sonde qui peuvent être utilisés pour vérifier l'ensemble des requêtes HTTP web et des réponses envoyées lors de l'échec de la sonde. Ce fichier contient des données concernant uniquement les sondes défaillantes, car seules les tentatives qui ont échoué sont journalisées. Vous pouvez utiliser ces informations pour mieux comprendre la cause de l'échec du test.

## Actions de récupération OwaSelfTestProbe

Cette sonde ayant très peu de dépendances, des défaillances se produisent généralement quand le traitement du pool d'applications OWA ne répond pas.

Pour résoudre ce problème, procédez comme suit :

1.  Pour vérifier la présence de nouveaux échecs, cliquez sur l'URL du journal des traces de la sonde dans le corps du message électronique d'alerte.

2.  Créez un compte d'utilisateur test sur le serveur sur lequel la boîte aux lettres est montée. Tentez d'ouvrir une session pour déterminer si le problème peut être reproduit.

3.  Recherchez dans l'indicateur d'intégrité OWA des alertes indiquant qu'un problème affecte un serveur de boîtes aux lettres spécifique. Pour plus d'informations, consultez la rubrique [Dépannage de l'indicateur d'intégrité OWA](troubleshooting-owa-health-set.md).

4.  Démarrez le Gestionnaire des services Internet, puis connectez-vous au serveur signalant le problème afin de déterminer si le pool d’applications **MSExchangeOwaAppPool** est en cours d’exécution sur le CAS.

5.  Dans le Gestionnaire des services Internet, vérifiez si le site web par défaut est opérationnel.

6.  Dans le Gestionnaire des services Internet, cliquez sur **Pools d'applications**, puis recyclez le pool d'applications **MSExchangeOWAAppPool** en exécutant la commande suivante à partir de l'Environnement de ligne de commande Exchange Management Shell :
    
        %SystemRoot%\System32\inetsrv\Appcmd recycle MSExchangeOWAAppPool

7.  Réexécutez la sonde associée en procédant de la manière décrite dans l'étape 2c de la section Verifying the issue still exists.

8.  Si le problème persiste, recyclez le service IIS à l'aide de l'utilitaire IISReset ou en exécutant la commande suivante :
    
        Iisreset /noforce

9.  Réexécutez la sonde associée en procédant de la manière décrite dans l'étape 2c de la section Verifying the issue still exists.

10. Si le problème persiste, redémarrez le serveur.

11. Une fois le serveur redémarré, réexécutez la sonde associée en procédant de la manière décrite dans l'étape 2c de la section Verifying the issue still exists.

12. En cas de nouvel échec de la sonde, il se peut que vous ayez besoin d'aide pour résoudre ce problème. Contactez un professionnel du Support Technique de Microsoft pour résoudre ce problème. Pour contacter un professionnel du Support Technique de Microsoft, consultez [Exchange Server Solutions Center](http://go.microsoft.com/fwlink/p/?linkid=180809). Dans le volet de navigation, cliquez sur **Ressources et options de support** et utilisez l'une des options indiquées sous **Obtenez du support technique** pour contacter un professionnel du support Microsoft. Étant donné que votre organisation peut avoir une procédure spécifique pour contacter directement les Services de Support Technique Microsoft, assurez-vous de connaître d'abord les instructions propres à votre organisation.

## Actions de récupération OwaDeepTestProbe

1.  Pour déterminer si le problème persiste, créez un compte d'utilisateur test sur le serveur sur lequel la boîte aux lettres est montée, puis essayez de vous connecter à OWA. Par exemple, essayez de vous connecter en utilisant : https:// *\<nom de serveur\>*/owa.

2.  Recherchez dans l'indicateur d'intégrité OWA des alertes indiquant qu'un problème affecte un serveur de boîtes aux lettres spécifique. Pour plus d'informations, consultez la rubrique [Dépannage de l'indicateur d'intégrité OWA](troubleshooting-owa-health-set.md).

3.  Démarrez le Gestionnaire des services Internet, puis connectez-vous au serveur signalant le problème afin de déterminer si le pool d'applications **MSExchangeOwaAppPool** est en cours d'exécution sur le CAS.

4.  Dans le Gestionnaire des services Internet, vérifiez si le site web par défaut est opérationnel.

5.  Identifiez la base de données de boîtes aux lettres à l'origine de l'échec de la sonde, puis vérifiez que la base de données de boîtes aux lettres est active sur le serveur de boîtes aux lettres, et que la banque de boîtes aux lettres est intègre. Pour identifier les informations de GUID de la base de données défaillante, consultez les informations de la trace de l'exception. Chaque échec doit être associé à une entrée ressemblant à ceci :
    
    `Starting Owa probe with Target: https://localhost/owa/, Username:  HealthMailboxdf8b87828ab0427cb91e985bbdfcec62@yourdomain.com`

6.  Copiez le GUID HealthMailbox, puis exécutez la commande suivante dans l'environnement de ligne de commande :
    
        Get-Mailbox -Monitoring -Identity <username>
    
    Par exemple, exécutez la commande suivante :
    
        Get-Mailbox -Monitoring -Identity HealthMailboxdf8b87828ab0427cb91e985bbdfcec62@yourdomain.com
    
    Dans l’objet renvoyé, vous pouvez localiser le nom de la base de données de l’utilisateur, et vous pouvez également déterminer où réside la base de données actuellement active.

7.  Dans le Gestionnaire des services Internet, cliquez sur **Pools d'applications**, puis recyclez le pool d'applications **MSExchangeOWAAppPool** en exécutant la commande suivante à partir de l'environnement de ligne de commande :
    
        %SystemRoot%\System32\inetsrv\Appcmd recycle MSExchangeOWAAppPool

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

