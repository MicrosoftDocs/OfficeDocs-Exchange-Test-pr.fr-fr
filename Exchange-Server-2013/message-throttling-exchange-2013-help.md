---
title: 'Limitation des messages: Exchange 2013 Help'
TOCTitle: Limitation des messages
ms:assetid: fba87902-2a79-42ac-b394-46a9016f667e
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb232205(v=EXCHG.150)
ms:contentKeyID: 50479612
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Limitation des messages

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2015-03-09_

La *limitation des messages* désigne un ensemble de limitations défini d'après le nombre de messages et de connexions qu'un ordinateur Microsoft Exchange Server 2013 peut traiter. Ces limites évitent l’épuisement accidentel ou intentionnel des ressources système sur le serveur Exchange.

**Contenu de cette rubrique**

Portée de la limitation des messages

Coût du message et limitation du débit de messagerie

Limitation des messages sur les serveurs

Limitation des messages sur les connecteurs d'envoi

Limitation des messages sur les connecteurs de réception

Stratégies de limitation des messages

## Portée de la limitation des messages

La limitation des messages implique diverses limites concernant la vitesse de traitement des messages, la vitesse de connexion SMTP et les délais d’expiration des sessions SMTP. Ces limites fonctionnent ensemble pour protéger un serveur Exchange contre une saturation de l'acceptation et de la remise de messages. Bien qu’il puisse y avoir un nombre important de messages et de connexions en souffrance, les limites de la limitation des messages permettent au serveur Exchange de traiter les messages et les connexions de façon ordonnée.

Outre la limitation des messages, vous pouvez également appliquer des limites de taille sur les composants individuels des messages, entre autres le nombre de destinataires, la taille de l’en-tête de message ou la taille des pièces jointes individuelles. Pour plus d’informations sur les tailles limites des messages, consultez la rubrique [Tailles limites des messages](message-size-limits-exchange-2013-help.md).

Une autre fonctionnalité permettant d’éviter la saturation des ressources système d’un serveur Exchange est la *régulation du flux*. Cette fonctionnalité analyse les ressources système pour le service de transport sur les serveurs de boîtes aux lettres et de transport Edge. Lorsqu’une ressource système analysée, telle que l’utilisation du disque dur ou de la mémoire, dépasse le seuil spécifié, le serveur diminue la vitesse à laquelle il accepte de nouvelles connexions et de nouveaux messages et se concentre sur la remise des messages existants. Lorsque les ressources système analysées reviennent à des niveaux d’utilisation normaux, le serveur augmente légèrement cette vitesse pour la ramener à un niveau normal.

Retour au début

## Coût du message et limitation du débit de messagerie

Pour garantir un débit cohérent des messages et une latence de remise des messages prévisible, Exchange 2013 établit un coût cumulé pour les messages. La fonction de qualité de service (QoS) a été ajoutée dans Microsoft Exchange Server 2010 SP1. Ce coût dépend des critères suivants :

  - Taille des messages

  - Nombre de destinataires

  - Fréquence de transmission

Les serveurs de transport Exchange 2013 suivent le coût de remise moyen pour les messages envoyés par des utilisateurs individuels. En tenant compte du coût des messages, Exchange 2013 fournit un groupe de paramètres qui permettent de contrôler l’incidence d’un utilisateur ou d’une connexion sur une organisation Exchange. Pour ce groupe de paramètres, on parle alors de *stratégie de limitation*. Lorsqu’un utilisateur transmet à maintes reprises des messages coûteux, notamment des messages à pièces jointes volumineuses ou des messages adressés à plusieurs destinataires, les serveurs de transport Exchange 2013 appliquent une stratégie de limitation pour attribuer une priorité moins élevée à des messages plus coûteux de l’utilisateur tout en poursuivant la remise des messages à plus faible coût. Ce nouveau paramètre procure un aspect « qualité de service » à la fonctionnalité de limitation des messages dans Exchange 2013.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>La limitation des messages n’affecte pas la priorité des messages du point de vue de l’utilisateur. Les messages conservent toujours la priorité définie à l’origine par l’utilisateur. Ils peuvent, par exemple, conserver un paramètre Important ou Urgent et ainsi de suite.</td>
</tr>
</tbody>
</table>


Pour la prise en charge de cette fonctionnalité, Exchange 2013 a recours aux mécanismes suivants :

  - **Agent de priorité interne** Cet agent est déclenché dans l’événement **OnResolvedMessage** et attribue une priorité plus faible à des messages du même expéditeur dont le coût cumulé est elévé. Ce coût est mesuré sur une période d’une minute et affecte les messages de plus de 500 destinataires ou de taille supérieure à un mégaoctet (Mo).

  - **Mise en file d’attente prioritaire selon des quotas pour la file d’attente de type MapiDelivery** Ce mécanisme oblige Exchange à envoyer des messages d’une file d’attente de priorité normale plus fréquemment que des messages d’une file d’attente à faible priorité. Par défaut, le ratio entre messages de priorité normale/faible est de 20:1. Cependant, les nouveaux messages placés dans une file d’attente à faible priorité ne sont jamais remis avant les nouveaux éléments d’une file d’attente de priorité plus élevée. Imaginons, par exemple, le scénario suivant :
    
    1.  Vingt messages de priorité normale sont remis. Par défaut, le prochain message remis est un message de plus faible priorité.
    
    2.  Le serveur de transport reçoit deux nouveaux messages : un message provenant d’une file d’attente à haute priorité, un autre issu d’une file d’attente de priorité plus faible.
    
    Dans ce scénario, le message de la file d’attente à haute priorité est remis en premier. Le message de la file d’attente à faible priorité est ensuite remis.

  - **Limitation des connexions simultanées selon l’intégrité de la base de données de messagerie (Messaging Database)** Ce mécanisme surveille l’intégrité de la base de données de messagerie Exchange (MDB) et limite les connexions simultanées aux serveurs de transport Exchange en fonction d’une valeur de mesure d’intégrité attribuée. La base de données (MDB) est surveillée par l’API du moniteur d’intégrité des ressources pour le service de transport sur le serveur de boîtes aux lettres et se voit attribuer une valeur d’intégrité de -1 à 100. Cette valeur est fondée sur les statistiques de performance RPC incluses avec chaque réponse RPC provenant du processus Store.exe dans le service de transport de boîtes aux lettres. Le mécanisme d’intégrité des ressources utilise à la fois le compteur de performances du taux de **demandes/seconde** et le compteur de performances **Latence moyenne RPC** pour calculer une valeur d’intégrité pour la base de données. Pour garantir une expérience d’utilisation interactive cohérente à l’utilisateur, Exchange réduit le nombre de connexions simultanées à mesure que la valeur d’intégrité diminue. Les plages de valeurs d’intégrité suivantes sont disponibles :
    
      - **-1** : cette valeur indique que l’état d’intégrité de la base de données MDB est inconnu. Elle est attribuée au démarrage de la base de données. Dans ce scénario, l’intégrité de la base de données est jugée satisfaisante.
    
      - **0** : cette valeur est attribuée si l’état d’intégrité de la base de données n’est pas bon. Dans cet état, la base de données ne devrait pas être contactée.
    
      - **1 à 99** : ces valeurs indiquent un état d’intégrité correct. Une valeur inférieure indique une base de données de moins bonne intégrité.
    
      - **100** : cette valeur indique une base de données intègre.

Le service de limitation Microsoft Exchange fournit le cadre de limitation des flux de messagerie. Le service de limitation Microsoft Exchange suit les paramètres de limitation de flux de messages pour un utilisateur en particulier et place en mémoire cache les informations de limitation. Les paramètres de limitation du flux de messages sont également désignés sous le nom de *budget*. Tout redémarrage du service de limitation Microsoft Exchange a pour effet de réinitialiser les budgets de limitation du flux de messages.

Vous pouvez utiliser les cmdlets de la stratégie de limitation disponibles dans Exchange 2013 pour configurer les paramètres de budget individuels d’une stratégie de limitation. Un budget désigne le degré d’accès dont dispose un utilisateur ou une application pour un paramètre spécifique. Il répresente le nombre de connexions dont peut bénéficier un utilisateur ou le nombre des activités qu’il est potentiellement autorisé à effectuer pour chaque période d’une minute. Par exemple, vous pouvez configurer un budget afin de définir le temps pendant lequel un utilisateur peut utiliser une fonctionnalité donnée dans Exchange, telle qu’ActiveSync, Outlook Web App ou les services Web Exchange. Ce seuil est stocké dans une stratégie de limitation et définit le budget.

Les paramètres de temps pour un budget sont définis sous la forme d’un pourcentage pour une minute. Un seuil de 100 % représente donc 60 secondes. Par exemple, imaginons que vous souhaitiez préciser les paramètres de stratégie Outlook Web App qui limitent le temps pendant lequel un utilisateur peut exécuter du code Outlook Web App sur un serveur d’accès au client, ainsi que le temps de communication avec ce dernier, à 600 millisecondes sur une période d’une minute. Pour cela, vous devez définir la valeur à 1 pour cent d’une minute (600 millisecondes) pour les deux paramètres suivants :

  - **OWAPercentTimeInCAS** : 1

  - **OWAPercentTimeInMailboxRPC** : 1

Un utilisateur auquel cette stratégie est appliquée dispose à la fois d’un budget OWAPercentTimeInCAS et OWAPercentageTimeInMailboxRPC de 600 millisecondes. Dans ce scénario, dès qu’il se connecte dans Outlook Web App, l’utilisateur peut exécuter le code d’accès au client pendant 600 millisecondes au maximum. Une fois la période de 600 millisecondes écoulée, la connexion est considérée hors budget et le serveur Exchange n’autorise plus aucune action de la part d’Outlook Web App avant que la limite du budget ne soit atteinte (une minute après). À l’issue du délai d’une minute, l’utilisateur peut exécuter le code d’accès au client Outlook Web App pour 600 millisecondes supplémentaires.

Retour au début

## Limitation des messages sur les serveurs

Vous pouvez définir les options de limitation des messages aux emplacements suivants :

  - Dans le service de transport

  - sur un connecteur d’envoi

  - sur un connecteur de réception

Avec l'environnement de ligne de commande Exchange Management, vous pouvez définir toutes les options de limitation des messages disponibles dans le service de transport sur ​​des serveurs de boîtes aux lettres, dans le service de transport de boîtes aux lettres sur les serveurs de boîtes aux lettres ou dans le service de transport frontal sur les serveurs d’accès au client. Vous pouvez également définir certaines options en configurant les propriétés du serveur de transport dans le Centre d'administration Exchange (CAE).

Le tableau suivant illustre les options de limitation des messages disponibles sur les serveurs de transport.

### Options de limitation des messages sur les serveurs de transport

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Source</th>
<th>Paramètre</th>
<th>Valeur par défaut</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Set-TransportService</strong></p>
<p><strong>Set-MailboxTransportService</strong></p></td>
<td><p><em>MaxConcurrentMailboxDeliveries</em></p></td>
<td><p>20</p></td>
<td><p>Ce paramètre spécifie le nombre maximal de threads de remise que le service de transport peut ouvrir simultanément pour remettre des messages à des boîtes aux lettres. La plage d’entrée valide pour ce paramètre est comprise entre 1 et 256. Nous vous recommandons de ne pas modifier cette valeur, sauf si le Support technique Microsoft préconise cette modification.</p></td>
</tr>
<tr class="even">
<td><p><strong>Set-TransportService</strong></p>
<p><strong>Set-MailboxTransportService</strong></p></td>
<td><p><em>MaxConcurrentMailboxSubmissions</em></p></td>
<td><p>20</p></td>
<td><p>Ce paramètre spécifie le nombre maximal de threads de dépôt que le service de transport peut ouvrir simultanément pour envoyer des messages à partir de boîtes aux lettres. La plage d’entrées valide pour ce paramètre s’étend de 1 à 256.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Set-TransportService</strong></p></td>
<td><p><em>MaxConnectionRatePerMinute</em></p></td>
<td><p>1200</p></td>
<td><p>Ce paramètre spécifie la vitesse maximale d’ouverture des connexions avec le service de transport. Si de nombreuses tentatives de connexion sont effectuées simultanément sur le service de transport, le paramètre <em>MaxConnectionRatePerMinute</em> limite la vitesse d'ouverture des connexions afin de ne pas saturer les ressources du serveur.</p></td>
</tr>
<tr class="even">
<td><p><strong>Set-TransportService</strong> or</p>
<p>propriétés du serveur de transport</p></td>
<td><p><em>MaxOutboundConnections</em></p></td>
<td><p>1000</p></td>
<td><p>Ce paramètre spécifie le nombre maximal de connexions sortantes qui peuvent être ouvertes simultanément. Si vous entrez la valeur <code>unlimited</code>, aucune limite n’est imposée quant au nombre de connexions sortantes. La valeur de ce paramètre doit être supérieure ou égale à la valeur du paramètre <em>MaxPerDomainOutboundConnections</em>.</p>
<p>Cette valeur peut également être configuré à l'aide du CAE à partir de <strong>Serveurs</strong>&gt;<strong>Serveurs</strong>&gt;<strong>Propriétés</strong>&gt;<strong>Limites de transport</strong>&gt;<strong>Restrictions de connexion sortante</strong>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Set-TransportService</strong> or</p>
<p>propriétés du serveur de transport</p></td>
<td><p><em>MaxPerDomainOutboundConnections</em></p></td>
<td><p>20</p></td>
<td><p>Ce paramètre spécifie le nombre maximal de connexions simultanées à un domaine. Si vous entrez la valeur <code>unlimited</code>, aucune limite n’est imposée quant au nombre de connexions sortantes par domaine. La valeur de ce paramètre doit être supérieure ou égale à la valeur du paramètre <em>MaxOutboundConnections</em>.</p>
<p>Cette valeur peut également être configuré à l'aide du CAE à partir de <strong>Serveurs</strong>&gt;<strong>Serveurs</strong>&gt;<strong>Propriétés</strong>&gt;<strong>Limites de transport</strong>&gt;<strong>Restrictions de connexion sortante</strong>.</p></td>
</tr>
<tr class="even">
<td><p><strong>Set-TransportService</strong></p></td>
<td><p><em>PickupDirectoryMaxMessagesPerMinute</em></p></td>
<td><p>100</p></td>
<td><p>Ce paramètre spécifie le nombre maximal de messages traités par minute par le répertoire de collecte et le répertoire de relecture. Chaque répertoire peut traiter de façon indépendante des fichiers de messages à la vitesse spécifiée par ce paramètre .</p></td>
</tr>
</tbody>
</table>


Retour au début

## Limitation des messages sur les connecteurs d'envoi

Le tableau suivant illustre l'option de limitation des messages disponible sur les connecteurs d'envoi. Vous devez utiliser l'environnement de ligne de commande Exchange Management pour configurer cette option.

### Option de limitation des messages disponibles sur les connecteurs d’envoi

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Source</th>
<th>Paramètre</th>
<th>Valeur par défaut</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Set-SendConnector</strong></p></td>
<td><p><em>ConnectionInactivityTimeOut</em></p></td>
<td><p>10 minutes</p></td>
<td><p>Ce paramètre spécifie la durée maximale pendant laquelle une connexion SMTP ouverte avec un serveur de messagerie de destination peut rester inactive avant d’être interrompue.</p></td>
</tr>
</tbody>
</table>


Retour au début

## Limitation des messages sur les connecteurs de réception

Le tableau qui suit affiche les options de limitation des messages disponibles sur les connecteurs de réception configurés sur un serveur de transport Hub ou un serveur de transport Edge. Vous devez utiliser l'environnement de ligne de commande Exchange Management pour configurer ces options.

### Option de limitation des messages disponibles sur les connecteurs de réception

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Source</th>
<th>Paramètre</th>
<th>Valeur par défaut</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Set-ReceiveConnector</strong></p></td>
<td><p><em>ConnectionInactivityTimeOut</em></p></td>
<td><p>5 minutes dans le service de Transport sur les serveurs de boîtes aux lettres</p>
<p>5 minutes pour une application frontale sur un serveur d'accès au client.</p>
<p>1 minute sur les serveurs de transport Edge.</p></td>
<td><p>Ce paramètre spécifie la durée maximale pendant laquelle une connexion SMTP ouverte avec un serveur de messagerie source peut rester inactive avant d’être interrompue. La valeur de ce paramètre doit être inférieure à la valeur spécifiée par le paramètre <em>ConnectionTimeout</em>.</p></td>
</tr>
<tr class="even">
<td><p><strong>Set-ReceiveConnector</strong></p></td>
<td><p><em>ConnectionTimeOut</em></p></td>
<td><p>10 minutes dans le service de Transport sur les serveurs de boîtes aux lettres</p>
<p>10 minutes pour une application frontale sur un serveur d'accès au client.</p>
<p>5 minutes sur les serveurs de transport Edge.</p></td>
<td><p>Ce paramètre spécifie la durée maximale pendant laquelle une connexion SMTP avec un serveur de messagerie source peut rester ouverte, même si le serveur de messagerie source transmet des données. La valeur de ce paramètre doit être supérieure à la valeur spécifiée par le paramètre <em>ConnectionInactivityTimeout</em>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Set-ReceiveConnector</strong></p></td>
<td><p><em>MaxInboundConnection</em></p></td>
<td><p>5000</p></td>
<td><p>Ce paramètre spécifie le nombre maximal de connexions SMTP entrantes que ce connecteur de réception autorise simultanément.</p></td>
</tr>
<tr class="even">
<td><p><strong>Set-ReceiveConnector</strong></p></td>
<td><p><em>MaxInboundConnectionPercentagePerSource</em></p></td>
<td><p>100 % sur le connecteur de réception par défaut dans le service de transport sur un serveur de boîtes aux lettres</p>
<p>2 % sur les autres connecteurs de réception dans le service de transport sur les serveurs de boîtes aux lettres et dans le service de transport frontal sur les serveurs d’accès au client.</p></td>
<td><p>Ce paramètre spécifie le nombre maximal de connexions SMTP qu’un connecteur de réception autorise simultanément depuis un serveur de messagerie source. La valeur est exprimée comme pourcentage de connexions restantes disponibles sur un connecteur de réception. Le nombre maximal de connexions autorisées par le connecteur de réception est défini par le paramètre <em>MaxInboundConnection</em>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Set-ReceiveConnector</strong></p></td>
<td><p><em>MaxInboundConnectionPerSource</em></p></td>
<td><p>unlimited sur le connecteur de réception par défaut dans le service de transport sur un serveur de boîtes aux lettres</p>
<p>20 sur les autres connecteurs de réception dans le service de transport sur les serveurs de boîtes aux lettres et dans le service de transport frontal sur les serveurs d’accès au client.</p></td>
<td><p>Ce paramètre spécifie le nombre maximal de connexions SMTP qu’un connecteur de réception autorise simultanément depuis un serveur de messagerie source.</p></td>
</tr>
<tr class="even">
<td><p><strong>Set-ReceiveConnector</strong></p></td>
<td><p><em>MaxProtocolErrors</em></p></td>
<td><p>5</p></td>
<td><p>Ce paramètre spécifie le nombre maximal d’erreurs de protocole SMTP qu’un connecteur de réception autorise avant que le connecteur de réception ne ferme la connexion au serveur de messagerie source.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Set-ReceiveConnector</strong></p></td>
<td><p><em>TarpitInterval</em></p></td>
<td><p>5 secondes</p></td>
<td><p>Ce paramètre spécifie l’intervalle de <em>répulsion des courriers indésirables</em>. La répulsion des courriers indésirables (tarpitting) est la pratique consistant à retarder de façon artificielle les réponses SMTP pour des profils de communication SMTP spécifiques qui indiquent des attaques DHA (Directory Harvest Attack) ou d’autres messages indésirables. Une <em>attaque DHA (Directory Harvest Attack)</em> est une tentative de collecte d’adresses électroniques valides d’une organisation spécifique à utiliser comme cible pour l’envoi de messages électroniques commerciaux non sollicités.</p>
<p>L’intervalle spécifié par le paramètre <em>TarpitInterval</em> s’applique uniquement aux connexions anonymes.</p></td>
</tr>
</tbody>
</table>


Retour au début

## Stratégies de limitation des messages

Dans Exchange 2013, chaque boîte aux lettres contient un paramètre *ThrottlingPolicy*. La valeur par défaut de ce paramètre est vide (`$null`). Vous pouvez utiliser le paramètre *ThrottlingPolicy* dans la cmdlet **Set-Mailbox** pour configurer la stratégie de limitation d’une boîte aux lettres.

Par défaut, il existe une stratégie de limitation qui offre une configuration par défaut avec un budget précis pour les utilisateurs qui se connectent à Exchange. Pour configurer des paramètres de budget personnalisés pour un ou plusieurs utilisateurs, créez une nouvelle stratégie de limitation. Appliquez ensuite la stratégie à l’utilisateur ou au groupe approprié.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159813.important(EXCHG.150).gif" title="Important" alt="Important" />Important :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Nous vous recommandons de ne pas modifier la stratégie de limitation par défaut.</td>
</tr>
</tbody>
</table>


Vous pouvez définir toutes les options de limitation des messages disponibles sur les serveurs de boîtes aux lettres dans l’environnement de ligne de commande Exchange Management. Les cmdlets suivantes sont disponibles pour gérer les stratégies de limitation :

  - **Get-ThrottlingPolicy**

  - **Remove-ThrottlingPolicy**

  - **New-ThrottlingPolicy**

  - **Set-ThrottlingPolicy**

Vous pouvez utiliser les cmdlets **New-ThrottlingPolicy** et **Set-ThrottlingPolicy** pour configurer le volume des activités que peut effectuer un utilisateur dans Exchange sur une connexion ou une période donnée. Ces paramètres forment le budget de l’utilisateur. Vous pouvez établir des stratégies de limitation pour contrôler l’accès aux fonctionnalités Exchange suivantes :

  - Exchange ActiveSync

  - Services Web Exchange

  - Outlook Web App

  - Messagerie unifiée

  - IMAP4

  - POP3

  - Connexions client Outlook (connexions MAPI ou RPC)

  - Paramètres de flux de messages

  - Commandes PowerShell

  - Utilisations de l’UC

Retour au début

