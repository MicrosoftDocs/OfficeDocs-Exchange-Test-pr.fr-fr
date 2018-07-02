---
title: Dépannage de l'indicateur d'intégrité SiteMailbox
TOCTitle: Dépannage de l'indicateur d'intégrité SiteMailbox
ms:assetid: ac00985c-c9a5-44bf-b152-4b99d8ae24ed
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/ms.exch.scom.sitemailbox(v=EXCHG.150)
ms:contentKeyID: 53276478
ms.date: 10/08/2015
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Dépannage de l'indicateur d'intégrité SiteMailbox

 

_**Sapplique à :** Exchange Server 2013, Project Server 2013_

_**Dernière rubrique modifiée :** 2013-02-11_

L'indicateur d'intégrité SiteMailbox surveille l'intégrité et l'accessibilité globales des boîtes aux lettres de site au sein de votre organisation.

Si vous recevez une alerte indiquant que SiteMailbox présente un manque d'intégrité, cela signifie que le contenu de la boîte aux lettres d'un utilisateur n'est pas synchronisé.

## Explication

Le système de surveillance de SiteMailbox reçoit des résultats de synchronisation passive du service de synchronisation en arrière-plan. Ce système n'utilise pas de sonde. Les résultats de synchronisation passive sont consignés dans le système de surveillance de SiteMailbox après chaque tentative de synchronisation. Des synchronisations sont également déclenchées lorsque les événements suivants se produisent :

  - Les utilisateurs accèdent à leurs boîtes aux lettres de site à l'aide d'Outlook ou d'Outlook Web App

  - Ils exécutent la commande **Update-SiteMailbox**.

  - Ils ouvrent la fenêtre d'options Outlook Web App, puis cliquent sur le bouton **Démarrer la synchronisation** dans la page **État de synchronisation** pour la boîte aux lettres de site sélectionnée.

Pour plus d'informations sur la cmdlet Update-SiteMailbox cmdlet, consultez la rubrique : [Update-SiteMailbox](https://technet.microsoft.com/fr-fr/library/jj218690\(v=exchg.150\))

Pour plus d'informations sur les sondes et les moniteurs, consultez la rubrique [État et performances du serveur](https://technet.microsoft.com/fr-fr/library/jj150551\(v=exchg.150\)).

## Problèmes courants

Le service de surveillance de la synchronisation déclenche généralement une alerte quand des problèmes de synchronisation se produisent dans le site. Aucune alerte n'est envoyée en cas d'échec d'une seule boîte aux lettres de site. Pour déterminer la cause d'une alerte de dépassement de seuil pour une boîte aux lettres de site unique, nous vous recommandons de consulter les fichiers journaux de synchronisation de cette boîte aux lettres.

## Action de l'utilisateur

Il se peut que le service ait récupéré après avoir émis l'alerte. Par conséquent, quand vous recevez une alerte signalant que l'indicateur d'intégrité n'est pas intègre, vérifiez tout d'abord que le problème existe toujours. Si tel est le cas, exécutez les actions de récupération appropriées décrites dans les sections suivantes.

## Vérification de l'existence du problème

1.  Repérez les noms de l'indicateur d'intégrité et du serveur dans l'alerte.

2.  Les détails du message fournissent des informations sur la cause exacte de l'alerte. Le plus souvent, le message fournit des informations de dépannage suffisantes pour identifier la cause première. Si les détails du message ne sont pas clairs, procédez comme suit :
    
    1.  Ouvrez Environnement de ligne de commande Exchange Management Shell, puis exécutez la commande suivante pour récupérer les détails de l'indicateur d'intégrité qui a émis l'alerte :
        
            Get-ServerHealth <server name> | ?{$_.HealthSetName -eq "<health set name>"}
        
        Par exemple, pour récupérer les détails de l'indicateur d'intégrité SiteMailbox à propos de server1.contoso.com, exécutez la commande suivante :
        
            Get-ServerHealth server1.contoso.com | ?{$_.HealthSetName -eq "SiteMailbox"}
    
    2.  Consultez la sortie de la commande pour déterminer quel moniteur a signalé l'erreur. La valeur **AlertValue** du moniteur qui a émis l'alerte sera `Unhealthy`.

## Étapes de dépannage

Quand vous recevez une alerte de l'indicateur d'intégrité, le message électronique contient les informations suivantes :

  - nom du serveur ayant envoyé l'alerte ;

  - heure et date de l'alerte ;

  - mécanisme d'authentification utilisé et informations d'identification ;

  - trace d'exception complète de la dernière erreur, notamment données de diagnostic et informations d'en-tête HTTP spécifiques.  
    
    **Remarque**   Vous pouvez utiliser les informations contenues dans la trace de l'exception complète pour résoudre le problème. L'exception générée par la sonde contient un motif de l'échec qui décrit pourquoi la sonde a échoué.

**Erreurs de synchronisation en arrière-plan**

En cas d'échec du processus de synchronisation en arrière-plan, il se peut que vous receviez une alerte ressemblant à ceci :

The Site Mailbox background sync is failing at least 25%: 41 failures out of 87 attempts.Sample sync result:

\[Message:The remote server returned an error: (401) Unauthorized.\]\[Type:System.Net.WebException\]

Cette alerte est déclenchée quand un pourcentage invariablement élevé d'échecs de synchronisation a été observé au cours des quatre dernières heures. Afin d'éviter les faux négatifs, une alerte est envoyée uniquement si les conditions suivantes ont été réunies pendant une période de 15 minutes au cours des quatre dernières heures :

  - Au moins 20 échecs se sont produits au cours d'une période de 15 minutes.

  - Le pourcentage d'échecs comparé au nombre total de tentatives est supérieur à 25 % au cours d'une période de 15 minutes.

Chaque boîte aux lettres de site dans Exchange est liée à un site SharePoint. Pour chacune des boîtes aux lettres de site sur un serveur Exchange donné hébergeant le rôle de boîte aux lettres, le serveur synchronise les informations relatives à la boîte aux lettres de site à partir de SharePoint.

Au cours de ce processus, deux types de synchronisations ont lieu : la synchronisation de l'appartenance et la synchronisation des documents. Les métadonnées de ces processus de synchronisation proviennent de différents services web. De plus, un serveur Exchange donné peut contenir des boîtes aux lettres de site liées à plusieurs serveurs ou batteries SharePoint. L'alerte peut donc provenir de plusieurs serveurs de boîtes aux lettres, en fonction des conditions suivantes :

1.  Distribution des boîtes aux lettres de site activement utilisées au sein de l'organisation

2.  Serveurs SharePoint auxquels les boîtes aux lettres de site activement utilisées sont liés

3.  Suffisance ou non du volume de synchronisation du serveur de boîtes aux lettres pour répondre aux seuils d'alerte

Pour résoudre ce problème, l'échantillon de résultat de synchronisation dans l'alerte peut vous aider à déterminer la cause de l'échec. Les détails relatifs à la réussite ou à l'échec de chaque tentative de synchronisation sont enregistrés dans le dossier *\<répertoire d'installation exExchangeSvrNoVersion\>*Logging\\TeamMailbox. Pour les échecs, consultez les fichiers Microsoft.Exchange.ServiceHost\_TeamMailboxSyncLog\* les plus récents en recherchant le terme **failed**. Les cmdlets **Test-OAuthConnectivity**, **Test-SiteMailbox** et **Get-SiteMailboxDiagnostics** permettent également de dépanner davantage.

**Le service MSExchangeServiceHost n'est pas en cours d'exécution**

Si le service MSExchangeServiceHost n'est pas en cours d'exécution, vous recevez une alerte ressemblant à ce qui suit :

The 'MSExchangeServiceHost' service is not running after the recovery attempts. The service may be disabled or in crash loop.

Pour résoudre ce problème, vérifiez que le service MSExchangeServiceHost est en cours d'exécution sur le serveur ayant envoyé l'alerte. Si le service est en cours d'exécution, consultez les journaux des événements Windows pour obtenir des indications sur la raison pour laquelle il ne fonctionnait peut-être pas précédemment, telle qu'un contrôle manuel ou des pannes récurrentes du service.

**Le service MSExchangeServiceHost est bloqué**

Si le service MSExchangeServiceHost est bloqué, vous recevez une alerte ressemblant à ce qui suit :

The MSExchangeServiceHost process has crashed at least 3 times in last 60 minutes.  
Watson Message:

\<*Message*\>

Pour résoudre ce problème, consultez le journal des événements d'applications Windows sur le serveur ayant envoyé l'alerte pour **4999** événements relatifs au service MSExchangeServiceHost. Le texte des détails peut fournir des informations sur la cause du problème.

## Pour plus d'informations

[Nouveautés d'Exchange 2013](https://technet.microsoft.com/fr-fr/library/jj150540\(v=exchg.150\))

[Cmdlets Exchange 2013](https://technet.microsoft.com/fr-fr/library/bb124413\(v=exchg.150\))

