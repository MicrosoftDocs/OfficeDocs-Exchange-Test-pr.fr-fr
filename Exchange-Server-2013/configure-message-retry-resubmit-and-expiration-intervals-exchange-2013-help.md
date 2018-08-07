---
title: 'Config. d’intervalles de nouvelle tentative, de renvoi et d’exp. des messages'
TOCTitle: Configuration d’intervalles de nouvelle tentative, de renvoi et d’expiration des messages
ms:assetid: 5420124f-aa4c-4702-b493-40a9a7edb786
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Aa998043(v=EXCHG.150)
ms:contentKeyID: 51407187
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configuration d’intervalles de nouvelle tentative, de renvoi et d’expiration des messages

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2014-12-16_

Microsoft Exchange Server 2013 vous permet de configurer les intervalles de nouvelle tentative, de renvoi et d'expiration des messages dans le service de transport sur des serveurs de boîtes aux lettres et de transport Edge. Pour obtenir des descriptions de ces paramètres, consultez la rubrique [Intervalles de nouvelle tentative, de renvoi et d’expiration des messages](message-retry-resubmit-and-expiration-intervals-exchange-2013-help.md).

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée de chaque procédure : 10 minutes

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrées « Service de transport » et « Serveur de transport Edge » dans la rubrique [Autorisations de flux de messagerie](mail-flow-permissions-exchange-2013-help.md).

  - Les paramètres par serveur personnalisés de vos fichiers de configuration d’application XML Exchange, par exemple les fichiers web.config sur les serveurs d’accès au client ou le fichier EdgeTransport.exe.config sur les serveurs de boîtes aux lettres, seront remplacés lors de l’installation d’une mise à jour cumulative Exchange. Veuillez enregistrer ces informations pour configurer à nouveau votre serveur après l’installation. Vous devez reconfigurer ces paramètres après avoir installé une mise à jour cumulative Exchange.

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.


## Que souhaitez-vous faire ?

## Utiliser EdgeTransport.exe.config pour configurer le nombre de tentatives suite à un problème de file d'attente, l'intervalle entre tentatives suite à un problème de file d'attente, l'intervalle entre tentatives de la file d'attente de remise de boîte aux lettres et la durée maximale d'inactivité avant renvoi

Pour configurer le nombre de tentatives suite à un problème de file d'attente, l'intervalle entre tentatives suite à un problème de file d'attente, l'intervalle entre tentatives de la file d'attente de remise de boîte aux lettres et la durée maximale d'inactivité avant renvoi, vous modifiez des clés dans le fichier XML de configuration de l'application %ExchangeInstallPath%Bin\\EdgeTransport.exe.config sur le serveur de boîtes aux lettres ou le serveur de transport Edge. Les modifications enregistrées dans ce fichier sont appliquées une fois que vous redémarrez le service de transport Microsoft Exchange. Quand vous redémarrez ce service, le flux de messagerie sur le serveur est temporairement interrompu.

1.  Dans une fenêtre d'invite de commandes sur le serveur de boîtes aux lettres ou le serveur de transport Edge, ouvrez le fichier EdgeTransport.exe.config dans Bloc-notes en exécutant la commande suivante :
    
        Notepad %ExchangeInstallPath%Bin\EdgeTransport.exe.config

2.  Recherchez les clés suivantes dans la section `<appSettings>`.
    
        <add key="QueueGlitchRetryCount" value="<Integer>" />
        <add key="QueueGlitchRetryInterval" value="<hh:mm:ss>" />
        <add key="MailboxDeliveryQueueRetryInterval" value="<hh:mm:ss>" />
        <add key="MaxIdleTimeBeforeResubmit" value="<hh:mm:ss>" />
    
    Ce exemple modifie le nombre de tentatives suite à un problème de file d'attente sur 6, l'intervalle entre tentatives suite à un problème de file d'attente sur 30 secondes, l'intervalle entre tentatives de la file d'attente de remise de boîte aux lettres sur 3 minutes et la durée maximale d'inactivité avant renvoi sur 6 heures.
    
        <add key="QueueGlitchRetryCount" value="6" />
        <add key="QueueGlitchRetryInterval" value="00:00:30" />
        <add key="MailboxDeliveryQueueRetryInterval" value="00:03:00" />
        <add key="MaxIdleTimeBeforeResubmit" value="6:00:00" />

3.  Quand vous avez terminé, enregistrez et fermez le fichier EdgeTransport.exe.config.

4.  Redémarrez le service de transport Microsoft Exchange en exécutant la commande suivante :
    
        net stop MSExchangeTransport && net start MSExchangeTransport

## Configurer les tentatives de relance après échec passager, l'intervalle de relance après échec passager et l'intervalle de relance après échec de la connexion sortante

Les tentatives de relance après un échec passager spécifient le nombre de tentatives de connexion effectuées après l'échec des tentatives de connexion contrôlées par les clés `QueueGlitchRetryCount` et `QueueGlitchRetryInterval`. La valeur par défaut du nombre de tentatives de relance après un échec passager est 6. La plage de valeurs valides pour ce paramètre s'étend de 0 à 15. Si vous définissez le nombre de tentatives de relance après un échec passager sur 0, la tentative de connexion suivante est contrôlée par l'*intervalle de relance après échec de la connexion sortante*.

L'intervalle de relance après un échec passager correspond à l'intervalle entre chaque tentative de connexion spécifiée par le nombre de tentatives de relance après un échec passager. Dans le service de transport sur un serveur de boîtes aux lettres, l'intervalle par défaut de relance après un échec passager est 5 minutes. Sur un serveur de transport Edge, l'intervalle par défaut de relance après un échec passager est 10 minutes.

L'intervalle de relance après échec de la connexion sortante correspond à l'intervalle de relance pour les tentatives de connexion sortante qui ont précédemment échoué. Les tentatives de connexion ayant échoué précédemment sont contrôlées par les tentatives de relance après échec passager et par l'intervalle de relance après échec passager. Dans le service de transport sur un serveur de boîtes aux lettres, la valeur par défaut de l'intervalle de relance après échec de la connexion sortante est 10 minutes. Sur un serveur de transport Edge, la valeur par défaut est 30 minutes.

## Utiliser le CAE pour configurer les tentatives de relance après échec passager, l'intervalle de relance après échec passager et l'intervalle de relance après échec de la connexion sortante

1.  Dans le Centre d'administration Exchange (CAE), cliquez sur **Serveurs**\>**Serveurs**, sélectionnez le serveur, cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier"), puis sur **Limites de transport**.

2.  Dans la section **Tentatives**, entrez une valeur dans les champs **Intervalle de relance après échec de la connexion sortante (secondes)**, **Intervalle de relance après échec passager (minutes)** ou **Tentatives de relance après échec passager**.

3.  Lorsque vous avez terminé, cliquez sur **Enregistrer**.

## Utiliser l'environnement de ligne de commande pour configurer les tentatives de relance après échec passager, l'intervalle de relance après échec passager et l'intervalle de relance après échec de la connexion sortante

Utilisez la syntaxe suivante pour configurer les tentatives de relance après échec passager, l'intervalle de relance après échec passager et l'intervalle de relance après échec de la connexion sortante dans le service de transport sur un serveur de boîtes aux lettres ou un serveur de transport Edge.

    Set-TransportService <ServerIdentity> -TransientFailureRetryCount <Integer> -TransientFailureRetryInterval <hh:mm:ss> -OutboundConnectionFailureRetryInterval <dd.hh:mm:ss>

Cet exemple montre comment modifier les valeurs suivantes sur le serveur de boîtes aux lettres nommé Mailbox01: sur le serveur de transport Edge Exchange01.

  - La nombre de tentatives de relance après échec passager est défini sur 8.

  - L'intervalle de relance après échec passager est défini sur 1 minute.

  - L'intervalle de relance après échec de la connexion sortante est défini sur 45 minutes.

<!-- end list -->

    Set-TransportService Mailbox01 -TransientFailureRetryCount 8 -TransientFailureRetryInterval 00:01:00 -OutboundConnectionFailureRetryInterval 00:45:00

> [!NOTE]
> Les paramètres <em>TransientFailureRetryCount</em> et <em>TransientFailureRetryInterval</em> sont également disponibles avec la cmdlet <strong>Set-FrontEndTransportService</strong> pour le service de transport frontal sur des serveurs d'accès au client.


## Configurer les tentatives de relance après échec passager, l'intervalle de relance après échec passager et l'intervalle de relance après échec de la connexion sortante

## Utiliser le CAE pour configurer les tentatives de relance après échec passager, l'intervalle de relance après échec passager et l'intervalle de relance après échec de la connexion sortante

1.  Dans le CAE, cliquez sur **Serveurs**\>**Serveurs**, sélectionnez le serveur, cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier"), puis sur **Limites de transport**.

2.  Dans la section **Tentatives**, entrez une valeur dans les champs **Intervalle de relance après échec de la connexion sortante (secondes)**, **Intervalle de relance après échec passager (minutes)** ou **Tentatives de relance après échec passager**.

3.  Lorsque vous avez terminé, cliquez sur **Enregistrer**.

## Utiliser l'environnement de ligne de commande pour configurer les tentatives de relance après échec passager, l'intervalle de relance après échec passager et l'intervalle de relance après échec de la connexion sortante

Utilisez la syntaxe suivante pour configurer les tentatives de relance après échec passager, l'intervalle de relance après échec passager et l'intervalle de relance après échec de la connexion sortante dans le service de transport sur un serveur de boîtes aux lettres ou un serveur de transport Edge.

    Set-TransportService <ServerIdentity> -TransientFailureRetryCount <Integer> -TransientFailureRetryInterval <hh:mm:ss> -OutboundConnectionFailureRetryInterval <dd.hh:mm:ss>

Cet exemple montre comment modifier les valeurs suivantes sur le serveur de boîtes aux lettres nommé Mailbox01: sur le serveur de transport Edge Exchange01.

  - La nombre de tentatives de relance après échec passager est défini sur 8.

  - L'intervalle de relance après échec passager est défini sur 1 minute.

  - L'intervalle de relance après échec de la connexion sortante est défini sur 45 minutes.

<!-- end list -->

    Set-TransportService Mailbox01 -TransientFailureRetryCount 8 -TransientFailureRetryInterval 00:01:00 -OutboundConnectionFailureRetryInterval 00:45:00

> [!NOTE]
> Les paramètres <em>TransientFailureRetryCount</em> et <em>TransientFailureRetryInterval</em> sont également disponibles avec la cmdlet <strong>Set-FrontEndTransportService</strong> pour le service de transport frontal sur des serveurs d'accès au client.


## Utiliser l'environnement de ligne de commande Exchange Management Shell pour configurer l'intervalle de nouvelle tentative de message

Par défaut, l’intervalle avant nouvelle tentative de message est `00:15:00` ou 15 minutes. Nous vous recommandons de ne pas modifier la valeur par défaut, sauf si le Support Microsoft préconise de le faire.

Pour définir l'intervalle de nouvelle tentative de message, utilisez la syntaxe suivante.

    Set-TransportService <ServerIdentity> -MessageRetryInterval <dd.hh:mm:ss>

Cet exemple montre la procédure de modification de l’intervalle avant nouvelle tentative de message sur 20 minutes sur le serveur de boîtes aux lettres Mailbox01.

    Set-TransportService Mailbox01 -MessageRetryInterval 00:20:00

## Configurer les paramètres d'expiration de notification d'état de remise retardée

Vous pouvez utiliser le CAE ou l'environnement de ligne de commande pour configurer l'intervalle d'expiration de notification d'état de remise retardée. Ce paramètre s'applique uniquement au serveur de transport local. Pour activer ou désactiver l'envoi de messages de notification d'état de remise retardée à des expéditeurs internes et externes, vous pouvez utiliser uniquement l'environnement de ligne de commande. Ces paramètres s'appliquent à tous les serveurs de transport au sein de votre organisation.

> [!NOTE]
> Sur les serveurs de transport Hub Exchange 2007, tous les paramètres <em>ExternalDSN*</em> et <em>InternalDSN*</em> sont disponibles pour la cmdlet <strong>Set-TransportServer</strong>, et non pour la cmdlet <strong>Set-TransportConfig</strong>. Si votre organisation comporte des serveurs de transport Hub Exchange 2007, vous devez modifier ces valeurs à l'aide de la cmdlet <strong>Set-TransportServer</strong> sur chaque serveur de transport Hub Exchange 2007.


## Utiliser le CAE pour configurer le délai d'attente avant l'envoi d'un message de notification d'état de remise retardée

1.  Dans le CAE, cliquez sur **Serveurs**\>**Serveurs**, sélectionnez le serveur, cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier"), puis sur **Limites de transport**.

2.  Dans la section **Notifications**, entrez une valeur pour **Avertir l'expéditeur lorsque le message est différé après (heures)**.

3.  Lorsque vous avez terminé, cliquez sur **Enregistrer**.

## Utiliser l'environnement de ligne de commande pour configurer le délai d'attente avant l'envoi d'un message de notification d'état de remise retardée

Pour définir l'intervalle de nouvelle tentative de message, utilisez la syntaxe suivante.

    Set-TransportService <ServerIdentity> -DelayNotificationTimeout <dd.hh:mm:ss>

Cet exemple montre comment modifier le délai d'attente avant l'envoi d'un message de notification d'état de remise retardée sur 6 heures sur le serveur de boîtes aux lettres nommé Mailbox01.

    Set-TransportService Mailbox01 -DelayNotificationTimeout 06:00:00

## Utiliser l'environnement de ligne de commande pour activer ou désactiver l'envoi de messages de notification d'état de remise retardée à des expéditeurs de messages internes et externes

Pour configurer les paramètres de notification DSN retardée, utilisez la syntaxe suivante.

    Set-TransportConfig -ExternalDelayDSNEnabled <$true | $false> -InternalDelayDSNEnabled <$true |$false>

Cet exemple montre comment empêcher l'envoi de messages de notification d'état de remise retardée à des expéditeurs externes.

    Set-TransportConfig -ExternalDelayDSNEnabled $false

Cet exemple montre comment empêcher l'envoi de messages de notification d'état de remise retardée à des expéditeurs internes.

    Set-TransportConfig -InternalDelayDSNEnabled $false

## Configurer le délai d'expiration des messages

## Utiliser le CAE pour configurer le délai d'expiration des messages

1.  Dans le CAE, cliquez sur **Serveurs**\>**Serveurs**, sélectionnez le serveur, cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier"), puis sur **Limites de transport**.

2.  Dans la section **Expiration du message**, entrez une valeur pour **Durée maximale depuis le dépôt (jours)**.

3.  Lorsque vous avez terminé, cliquez sur **Enregistrer**.

## Utiliser l'environnement de ligne de commande pour configurer le délai d'expiration des messages

Pour configurer le délai d'expiration des messages, utilisez la syntaxe suivante.

    Set-TransportService <ServerIdentity> -MessageExpirationTimeout <dd.hh:mm:ss>

Cet exemple montre comment modifier le délai d'expiration des messages sur 4 jours sur un serveur Exchange nommé Mailbox01.

    Set-TransportService Mailbox01 -MessageExpirationTimeout 4.00:00:00

