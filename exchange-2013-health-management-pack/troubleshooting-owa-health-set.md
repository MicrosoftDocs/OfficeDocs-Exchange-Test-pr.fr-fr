---
title: Dépannage de l'indicateur d'intégrité OWA
TOCTitle: Dépannage de l'indicateur d'intégrité OWA
ms:assetid: eae9dbd7-2ce6-43ce-b9a1-b114fd0c3ab4
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/ms.exch.scom.owa(v=EXCHG.150)
ms:contentKeyID: 53276485
ms.date: 02/05/2016
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Dépannage de l'indicateur d'intégrité OWA

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2015-03-09_

L'indicateur d'intégrité Outlook Web App (OWA) surveille l'intégrité globale du service Outlook Web App.

Si vous recevez une alerte indiquant qu'Outlook Web App présente un manque d'intégrité, cela signifie qu'un problème empêche probablement les utilisateurs d'accéder à leur boîte aux lettres à l'aide d'Outlook Web App.

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
<td><p>OwaCtpProbe</p></td>
<td><p>Outlook Web App</p></td>
<td><p>Active Directory</p>
<p>Banque d'informations</p></td>
<td><p>OwaCtpMonitor</p></td>
</tr>
</tbody>
</table>


Pour plus d'informations sur les sondes et les moniteurs, consultez la rubrique [État et performances du serveur](https://technet.microsoft.com/fr-fr/library/jj150551\(v=exchg.150\)).

## Problèmes courants

Cette sonde peut échouer pour diverses raisons. Les plus courantes sont les suivantes :

  - Le pool d’applications Outlook Web App qui est hébergé sur le serveur d’accès au client (CAS) contrôlé ne répond pas, ou le pool d’applications qui est hébergé sur le serveur de boîtes aux lettres ne répond pas.

  - Le CAS rencontre des problèmes de réseau, et il ne peut pas se connecter au serveur de boîtes aux lettres ni au contrôleur de domaine.

  - Les informations d'identification du compte assurant le contrôle sont incorrectes.

  - La base de données de l’utilisateur n’est pas montée, ou la banque d’informations est inaccessible pour cette boîte aux lettres.

  - La banque d'informations ne répond pas.

  - Les contrôleurs de domaine ne répondent pas.

## Action de l'utilisateur

Il se peut que le service ait récupéré après avoir émis l'alerte. Par conséquent, quand vous recevez une alerte signalant que l'indicateur d'intégrité n'est pas intègre, vérifiez tout d'abord que le problème existe toujours. Si tel est le cas, exécutez les actions de récupération appropriées décrites dans les sections suivantes.

## Vérification de l'existence du problème

1.  Repérez les noms de l'indicateur d'intégrité et du serveur dans l'alerte.

2.  Les détails du message fournissent des informations sur la cause exacte de l'alerte. Le plus souvent, le message fournit des informations de dépannage suffisantes pour identifier la cause première. Si les détails du message ne sont pas clairs, procédez comme suit :
    
    1.  Ouvrez Environnement de ligne de commande Exchange Management Shell, puis exécutez la commande suivante pour récupérer les détails de l'indicateur d'intégrité qui a généré l'alerte :
        
            Get-ServerHealth <server name> | ?{$_.HealthSetName -eq "<health set name>"}
        
        Pour obtenir les détails de l'indicateur d'intégrité Outlook Web App concernant server1.contoso.com, exécutez la commande suivante :
        
            Get-ServerHealth server1.contoso.com | ?{$_.HealthSetName -eq "OWA"}
    
    2.  Consultez la sortie de la commande pour déterminer quel moniteur a signalé l'erreur. La valeur **AlertValue** du moniteur qui a émis l'alerte est `Unhealthy`.
    
    3.  Réexécutez la sonde associée pour le moniteur dont l’état d’intégrité est défectueux. Pour rechercher la sonde associée, reportez-vous au tableau figurant dans la section Explanation. Pour ce faire, exécutez la commande suivante :
        
            Invoke-MonitoringProbe <health set name>\<probe name> -Server <server name> | Format-List
        
        Par exemple, pour créer une sonde de surveillance Exchange ActiveSync sur *server1.contoso.com*, exécutez la commande suivante :
        
            Invoke-MonitoringProbe -Identity ActiveSync.Protocol\ActiveSyncSelfTestProbe -Server server1.contoso.com
    
    4.  Dans la sortie de la commande, consultez la valeur **Result** de la sonde. Si elle indique **Succeeded**, le problème était une erreur passagère, qui n'existe plus. Autrement, reportez-vous aux étapes de récupération décrites dans les sections suivantes.

## Actions de récupération OwaCtpMonitor

Une alerte par courrier électronique en provenance de l'indicateur d'intégrité contient les données suivantes :

  - nom du serveur ayant envoyé l'alerte ;

  - trace d'exception complète de la dernière erreur, notamment données de diagnostic et informations d'en-tête HTTP spécifiques.  
    
    **Remarque**   Vous pouvez utiliser les informations contenues dans la trace de l'exception complète pour résoudre le problème. L'exception générée par la sonde contient un motif de l'échec qui décrit pourquoi la sonde a échoué. Par exemple, l'exception contient ce qui suit :
    
      - **MissingKeyword**   Un mot clé attendu ne figure pas dans la réponse du serveur. Dans ce cas, l'exception contient les mots clés attendus.
    
      - **NameResolution**   La résolution DNS ne parvient pas à résoudre un nom de serveur donné.
    
      - **NetworkConnection**   La sonde rencontre un échec de connexion réseau quand elle tente de se connecter au pool d'applications OWA sur CAFE.
    
      - **UnexpectedHttpResponseCode**   La réponse contenait un code HTTP inattendu. Par exemple, le serveur a renvoyé un code HTTP **503**.
    
      - **RequestTimeout**   Le serveur a mis trop de temps à répondre à une demande du client.
    
      - **ScenarioTimeout**   La sonde a fonctionné, mais son exécution a pris plus d'une minute. Cela indique généralement une surcharge du système.
    
      - **OwaErrorPage**Outlook Web App a renvoyé une page d'erreur. Le nom de l'erreur à l'origine de l'échec figure généralement dans le message d'exception.
    
      - **OwaMailboxErrorPage**Outlook Web App a renvoyé une page d'erreur signalant une erreur en relation avec la banque de boîtes aux lettres. Cela indique généralement que la banque de boîtes aux lettres est hors service ou que des boîtes aux lettres sont en cours de démontage.
    
    La trace de l'exception contient un champ important nommé **FailingComponent**. La sonde tente de déterminer la défaillance, comme dans l'exemple suivant :
    
      - **Boîte aux lettres**   La sonde peut atteindre Outlook Web App, mais elle ne peut pas se connecter à la banque de boîtes aux lettres. Dans ce cas, la sonde est défaillante ou la latence d'accès à la boîte aux lettres a entraîné l'échec de la sonde et généré une erreur **ScenarioTimeout**. Lorsque des échecs de ce type se produisent, vous devez contrôler l'intégrité des serveurs de boîtes aux lettres.
    
      - **Active Directory**   La sonde peut atteindre Outlook Web App, mais elle ne peut pas se connecter à Active Directory. Dans ce cas, soit la sonde est défaillante, soit les latences d'appel Active Directory ont entraîné un dépassement de son délai d'exécution. En présence d'échecs de ce type, vous devez vérifier l'intégrité des contrôleurs de domaine, ainsi que les connexions réseau entre le CAS, les serveurs de boîtes aux lettres et les contrôleurs de domaine.
    
      - **OWA**   Cela signifie généralement qu'une erreur s'est produite à l'intérieur de la couche Outlook Web App. En présence d'échecs de ce type, vous devez vérifier l'intégrité du processus Outlook Web App sur le CAS et les serveurs de boîtes aux lettres, ainsi que les connexions réseau.
    
    L'exception contient également la dernière requête HTTP et les informations de réponse reçues avant la défaillance de la sonde. Le corps de l'escalade contient le chemin d'accès aux journaux de la sonde. Ces informations vous permettent de déterminer l'ensemble des requêtes HTTP web et des réponses envoyées lors de l'échec de la sonde. Ce fichier contient des données concernant uniquement les sondes défaillantes, car seules les tentatives qui ont échoué sont journalisées. Vous pouvez utiliser ces informations pour mieux comprendre la cause de l'échec du test.

  - Importance de la chute de la métrique de disponibilité (x%).

  - Chemin d'accès complet au dossier contenant les traces de requête HTTP complètes associées à la sonde. Par défaut, ces informations figurent dans le dossier *\<ExchangeServer\>*\\Logging\\Monitoring\\OWA\\ClientAccessProbe.

  - Heure et date de l'alerte.

Pour résoudre ce problème, procédez comme suit :

1.  Créez un compte d'utilisateur test, puis connectez-vous au CAS en utilisant ce compte. Par exemple, connectez-vous en utilisant https:// *\<nom de serveur\>*/owa.
    
    En cas d'échec, testez en utilisant un autre CAS pour vérifier si le problème se produit sur un CAS spécifique et non sur le serveur de boîtes aux lettres.

2.  Vérifiez la connectivité entre le CAS et les serveurs de boîtes aux lettres. Utilisez ping.exe pour vérifier que tous les serveurs répondent.

3.  Recherchez dans l'indicateur d'intégrité OWA.Protocol des alertes indiquant qu'un problème affecte un serveur de boîtes aux lettres spécifique. Pour plus d'informations, consultez la rubrique [Dépannage de l'indicateur d'intégrité OWA.Protocol](troubleshooting-owa-protocol-health-set.md).

4.  Démarrez le Gestionnaire des services Internet, puis connectez-vous au serveur signalant le problème afin de vérifier que le pool d’applications MSExchangeOwaAppPool est exécuté sur le CAS.

5.  Dans le Gestionnaire des services Internet, vérifiez si le site web par défaut est opérationnel.

6.  Identifiez la base de données de boîtes aux lettres à l'origine de l'échec de la sonde, puis vérifiez que la base de données de boîtes aux lettres est active sur le serveur de boîtes aux lettres, et que la banque de boîtes aux lettres est intègre. Pour identifier les informations de GUID de la base de données défaillante, consultez les informations de la trace de l'exception. Chaque échec doit être associé à une entrée ressemblant à ceci :
    
    Starting Owa probe with Target: https://localhost/owa/, Username: *HealthMailboxdf8b87828ab0427cb91e985bbdfcec62@yourdomain.com*

7.  Copiez le GUID HealthMailbox, puis exécutez la commande suivante dans l'environnement de ligne de commande :
    
        Get-Mailbox -Monitoring -Identity <username>
    
    Par exemple, exécutez la commande suivante :
    
        Get-Mailbox -Monitoring -Identity HealthMailboxdf8b87828ab0427cb91e985bbdfcec62@yourdomain.com
    
    Dans l’objet renvoyé, vous pouvez localiser le nom de la base de données de l’utilisateur, et vous pouvez également déterminer où réside la base de données actuellement active.

8.  Si vous avez configuré une redirection entre sites, il se peut que vous voyiez des sondes en échec et générant une erreur MissingKeyword. Cela se produit parce que, par défaut, les sondes CAS s'exécutent sur les comptes pour tout emplacement, et parce que la probe ne tente pas de tester un CAS sur un autre site quand elle utilise une redirection. Pour résoudre ce problème, vérifiez que les serveurs sur chaque se trouvent dans MonitoringGroups. Les CAS d'un groupe d'analyse donné effectuent le test uniquement avec des serveurs de boîtes aux lettres figurant dans le même groupe.
    
    Pour déterminer les groupes d'analyse pour vos serveurs, exécutez la commande suivante :
    
        Get-ExchangeServer | ft MonitoringGroup
    
    Pour modifier le groupe d'analyse sur un serveur, utilisez la cmdlet **Set-ExchangeServer** avec le paramètre *MonitoringGroup*. Par exemple, exécutez la commande suivante :
    
        Set-ExchangeServer -Identity "ServerName" -MonitoringGroup "Primary"

9.  Dans le Gestionnaire des services Internet, cliquez sur **Pools d'applications**, puis recyclez le pool d'applications **MSExchangeOWAAppPool** en exécutant la commande suivante à partir de l'Environnement de ligne de commande Exchange Management Shell :
    
        %SystemRoot%\System32\inetsrv\Appcmd recycle MSExchangeOWAAppPool

10. Réexécutez la sonde associée de la manière décrite dans l'étape 2c de la section Verifying the issue still exists.

11. Si le problème persiste, recyclez le service IIS à l'aide de l'utilitaire IISReset ou en exécutant la commande suivante :
    
        Iisreset /noforce

12. Réexécutez la sonde associée de la manière décrite dans l'étape 2c de la section Verifying the issue still exists.

13. Si le problème persiste, redémarrez le serveur.

14. Une fois le serveur redémarré, réexécutez la sonde associée de la manière décrite dans l'étape 2c de la section Verifying the issue still exists.

15. Si l'échec de la sonde persiste, vous avez peut-être besoin d'assistance pour résoudre le problème. Contactez un professionnel du Support Technique de Microsoft pour résoudre ce problème. Pour contacter un professionnel du Support Technique de Microsoft, consultez [Exchange Server Solutions Center](http://go.microsoft.com/fwlink/p/?linkid=180809). Dans le volet de navigation, cliquez sur **Ressources et options de support** et utilisez l'une des options indiquées sous **Obtenez du support technique** pour contacter un professionnel du support Microsoft. Étant donné que votre organisation peut avoir une procédure spécifique pour contacter directement les Services de Support Technique Microsoft, assurez-vous de connaître d'abord les instructions propres à votre organisation.

## Pour plus d'informations

[Nouveautés d'Exchange 2013](https://technet.microsoft.com/fr-fr/library/jj150540\(v=exchg.150\))

[Cmdlets Exchange 2013](https://technet.microsoft.com/fr-fr/library/bb124413\(v=exchg.150\))

