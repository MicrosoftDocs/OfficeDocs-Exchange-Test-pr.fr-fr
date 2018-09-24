---
title: "Activer et configurer la file d'attente prioritaire: Exchange 2013 Help"
TOCTitle: Activer et configurer la file d'attente prioritaire
ms:assetid: 1975d85d-2f1d-4852-8d19-e74ba4ba3853
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ891104(v=EXCHG.150)
ms:contentKeyID: 51407160
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Activer et configurer la file d'attente prioritaire

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2014-12-16_

La *priorité de mise en file d'attente* est une fonctionnalité de Microsoft Exchange Server 2013 qui permet au niveau de priorité d'un message configuré par l'expéditeur dans Microsoft Outlook ou Outlook Web Access d'influencer le traitement du message par le service de transport sur le serveur de boîtes aux lettres. Lorsque la priorité de mise en file d'attente est activée, les messages à priorité haute sont transmis à leurs destinations avant les messages à priorité normale, et les messages à priorité normale sont transmis avant les messages à priorité faible. Pour plus d'informations, consultez la rubrique [priorité de mise en file d’attente ;](priority-queuing-exchange-2013-help.md).

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : 15 minutes

  - Les autorisations Exchange ne s'appliquent pas aux procédures de cette rubrique. Ces procédures sont exécutées dans le système d'exploitation du serveur Exchange.

  - Les modifications que vous enregistrez dans le fichier de configuration de l'application EdgeTransport.exe.config sont appliquées après le redémarrage du service de transport de Microsoft Exchange.

  - Quand vous redémarrez le service de transport Microsoft Exchange, le flux de messagerie sur le serveur est temporairement interrompu.

  - Les paramètres par serveur personnalisés de vos fichiers de configuration d’application XML Exchange, par exemple les fichiers web.config sur les serveurs d’accès au client ou le fichier EdgeTransport.exe.config sur les serveurs de boîtes aux lettres, seront remplacés lors de l’installation d’une mise à jour cumulative Exchange. Veuillez enregistrer ces informations pour configurer à nouveau votre serveur après l’installation. Vous devez reconfigurer ces paramètres après avoir installé une mise à jour cumulative Exchange.

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.


## Utiliser l'invite de commandes pour activer et configurer la priorité de mise en file d'attente dans le fichier EdgeTransport.exe.config

1.  Dans une fenêtre d'invite de commandes, ouvrez le fichier de configuration de l'application EdgeTransport.exe.config dans le Bloc-notes en exécutant la commande suivante :
    
    ```powershell
    Notepad %ExchangeInstallPath%Bin\EdgeTransport.exe.config
    ```

2.  Recherchez les clés suivantes dans la section `<appSettings>`.
    
    ```powershell
    <add key="PriorityQueuingEnabled" value="false" />
    <add key="MaxPerDomainHighPriorityConnections" value="3" />
    <add key="MaxPerDomainNormalPriorityConnections" value="15" />
    <add key="MaxPerDomainLowPriorityConnections" value="2" />
    <add key="HighPriorityMessageExpirationTimeout" value="8:00:00" />
    <add key="NormalPriorityMessageExpirationTimeout" value="2.00:00:00" />
    <add key="LowPriorityMessageExpirationTimeout" value="2.00:00:00" />
    <add key="HighPriorityDelayNotificationTimeout" value="00:30:00" />
    <add key="NormalPriorityDelayNotificationTimeout" value="4:00:00" />
    <add key="LowPriorityDelayNotificationTimeout" value="8:00:00" />
    <add key="MaxHighPriorityMessageSize" value="250KB" />
    ```
    
    Pour activer la priorité de mise en file d'attente dans le service de transport sur le serveur de boîtes aux lettres, utilisez la valeur suivante :
    
    ```command line
    <add key="PriorityQueuingEnabled" value="true" />
    ```
    
    Configurez les valeurs de priorité de mise en file d'attente restantes ou conservez les valeurs par défaut.

3.  Quand vous avez terminé, enregistrez et fermez le fichier EdgeTransport.exe.config.

4.  Redémarrez le service de transport Microsoft Exchange en exécutant la commande suivante :
    
    ```powershell
    net stop MSExchangeTransport && net start MSExchangeTransport
    ```

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez correctement activé et configuré la priorité de mise en file d'attente, procédez comme suit :

1.  Vérifiez que la clé **PriorityQueueinEnabled** dans le fichier de EdgeTransport.exe.config a la valeur `"true"`.

2.  Utilisez Outlook pour créer un message de test à priorité haute dont la taille est supérieure à la valeur spécifiée par la clé **MaxHighPriorityMessageSize**, puis vérifiez que le message arrive en tant que message à priorité normale.

3.  Essayez de vérifier que les messages à priorité haute envoyés au même destinataire ou à la même destination arrivent avant les messages à priorité faible. Pour ce faire, vous pouvez utiliser plusieurs boîtes aux lettres afin d'envoyer simultanément plusieurs messages de test similaires possédant un niveau de priorité différent au même destinataire ou à la même destination.

