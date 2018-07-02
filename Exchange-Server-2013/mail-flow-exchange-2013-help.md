---
title: 'Flux de messagerie: Exchange 2013 Help'
TOCTitle: Flux de messagerie
ms:assetid: 14df5e1a-a5f7-4b0d-ba97-f53b76f0e7e0
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Aa996349(v=EXCHG.150)
ms:contentKeyID: 50477551
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Flux de messagerie

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2015-03-09_

Dans Microsoft Exchange Server 2013, le flux de messagerie s'effectue par le pipeline de transport. Le *pipeline de transport* est un ensemble de services, de connexions, de composants et de files d'attente qui fonctionnent ensemble pour acheminer tous les messages vers le catégoriseur du service de transport d'un serveur de boîtes aux lettres dans une organisation.

Vous cherchez une liste de toutes les rubriques relatives aux flux de messagerie ? Voir Informations sur le flux de messagerie.

Pour plus d'informations sur la configuration des flux de messagerie dans une nouvelle organisation Exchange 2013, consultez la rubrique [Configuration du flux de messagerie et de l’accès au client](configure-mail-flow-and-client-access-exchange-2013-help.md).

**Contenu de cette rubrique**

Pipeline de transport

Service de transport sur les serveurs de boîtes aux lettres

Informations sur le flux de messagerie

## Pipeline de transport

Le pipeline de transport comprend les services suivants :

  - **Service de transport frontal sur les serveurs d’accès client**   Ce service agit comme un proxy sans état pour tout le trafic SMTP externe entrant et (en option) sortant pour l’organisation Exchange 2013. Le service de transport frontal n’inspecte pas le contenu des messages, ne communique pas avec le service de transport de boîtes aux lettres sur les serveurs de boîtes aux lettres et ne met pas les messages en file d’attente locale.

  - **Service de transport sur les serveurs de boîtes aux lettres**   Ce service est quasiment identique au rôle de serveur de transport Hub disponible dans les versions précédentes d’Exchange. Le service de transport gère le flux entier de messagerie SMTP pour l'organisation et procède à la catégorisation de messages, puis à l'inspection de leur contenu. Contrairement aux versions précédentes d'Exchange, le service de transport ne communique jamais directement avec les bases de données de boîtes aux lettres. Cette tâche est désormais gérée par le service de transport de boîtes aux lettres. Le service de transport achemine les messages entre le service de transport de boîtes aux lettres, le service de transport, le service de transport frontal et (selon votre configuration) le service de transport sur les serveurs de transport Edge. Le service de transport sur les serveurs de boîtes aux lettres est décrit de façon plus détaillée plus loin dans cette rubrique.

  - **Service de transport de boîtes aux lettres sur les serveurs de boîtes aux lettres**   Ce service est composé de deux services distincts : le service de dépôt de transport de boîte aux lettres et de remise de transport de boîte aux lettres. Le service de remise de transport de boîtes aux lettres reçoit les messages SMTP du service de transport sur le serveur de boîtes aux lettres local ou sur d'autres serveurs de boîtes aux lettres et se connecte à la base de données de boîtes aux lettres locale via un appel de procédure distant (RPC) Exchange pour remettre le message. Le service de dépôt de transport de boîtes aux lettres se connecte à la base de données de boîtes aux lettres locale par le biais du RPC pour récupérer les messages, puis soumet ces derniers, via SMTP, au service de transport sur le serveur de boîtes aux lettres local ou d'autres serveurs de boîtes aux lettres. Le service de dépôt de transport de boîtes aux lettres a accès aux mêmes informations de topologie de routage que le service de transport. Tout comme le service de transport frontal, le service de transport de boîtes aux lettres ne met pas les messages en file d'attente locale.

  - **Service de transport sur les serveurs de transport Edge**   Ce service est très semblable au service de transport sur les serveurs de boîtes aux lettres. Si un serveur de transport Edge est installé dans votre réseau de périmètre, tout le courrier provenant d’Internet ou dirigé vers Internet transite par le serveur de transport Edge du service de transport. Ce service est décrit en détail ci-après dans cette rubrique.

La figure suivante illustre les relations entre les composants du pipeline de transport Exchange 2013.

**Vue d'ensemble du pipeline de transport dans Exchange 2013.**

![Diagramme de synthèse du pipeline de transport](images/Aa996349.6f548b64-6ac2-4e98-9098-69ad6cd9f569(EXCHG.150).gif "Diagramme de synthèse du pipeline de transport")

## Messages provenant d’expéditeurs externes

Les messages ne provenant pas de l’organisation accèdent au pipeline de transport via un connecteur de réception du service de transport frontal du serveur d’accès au client et sont acheminés vers le service de transport d’un serveur de boîtes aux lettres.

Si un serveur de transport Edge Exchange 2013 est installé dans votre réseau de périmètre, les messages provenant de l’extérieur de l’organisation entrent dans le pipeline de transport au moyen d’un connecteur de réception dans le service de transport sur le serveur de transport Edge. L’endroit où sont ensuite acheminés vos messages dépend de la configuration de vos serveurs Exchange internes.

  - **Serveur de boîtes aux lettres et serveur d’accès au client installés sur le même ordinateur**   Dans cette configuration, le serveur d’accès au client est utilisé pour le flux de messagerie entrant. Le courrier qui arrive sur le service de transport sur le serveur de transport Edge est acheminé vers le service de transport frontal sur le serveur d’accès au client, puis vers le service de transport sur le serveur de boîtes aux lettres.

  - **Serveur de boîtes aux lettres et serveur d’accès au client installés sur des ordinateurs distincts**   Dans cette configuration, le flux de messagerie entrant contourne le serveur d’accès au client. Le courrier est acheminé du service de transport sur le serveur de transport Edge vers le service de transport sur le serveur de boîtes aux lettres.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Si un serveur de transport Edge Exchange 2010 ou Exchange 2007 est installé sur votre réseau de périmètre, le flux de messagerie se produit directement entre le serveur de transport Edge et le service de transport sur le serveur de boîtes aux lettres. Pour plus d'informations, consultez la rubrique <a href="use-an-exchange-2010-or-2007-edge-transport-server-in-exchange-2013-exchange-2013-help.md">Utilisation d’un serveur de transport Edge Exchange 2010 ou 2007 dans Exchange 2013</a>.</td>
</tr>
</tbody>
</table>


## Messages provenant d’expéditeurs internes

Les messages SMTP provenant de l’intérieur de l’organisation accèdent au pipeline de transport via le service de transport d’un serveur de boîtes aux lettres de l’une des manières suivantes :

  - via un connecteur de réception ;

  - à partir du répertoire de collecte ou du répertoire de relecture ;

  - à partir du service de transport de boîtes aux lettres ;

  - par le dépôt d'un agent.

Le message est acheminé en fonction de la destination de routage ou du groupe de remise. Pour plus d’informations, consultez la rubrique [Routage du courrier](mail-routing-exchange-2013-help.md).

Si le message possède des destinataires externes, il est acheminé à partir du service de transport sur le serveur de boîtes aux lettres vers Internet ou à partir du serveur de boîtes aux lettres vers le service de transport frontal sur un serveur d’accès au client, puis vers Internet si le connecteur d’envoi est configuré pour rediriger via proxy les connexions sortantes par le biais du serveur d’accès au client. Pour plus d’informations, consultez la rubrique [Créer un connecteur d’envoi pour les messages électroniques envoyés vers Internet](create-a-send-connector-for-email-sent-to-the-internet-exchange-2013-help.md).

Si un serveur de transport Edge est installé dans votre réseau de périmètre, les messages ayant des destinataires externes ne sont jamais transmis par le service de transport frontal sur un serveur d’accès au client. Le message est acheminé à partir du service de transport sur un serveur de boîtes aux lettres vers le service de transport sur le serveur de transport Edge.

## Service de transport sur les serveurs de boîtes aux lettres

Chaque message échangé au sein d'une organisation Exchange 2013 doit être catégorisé dans le service de transport d'un serveur de boîtes aux lettres avant de pouvoir être acheminé et remis. Quand un message a été catégorisé, il est placé dans une file d'attente de remise dans la base de données de boîtes aux lettres de destination, le groupe de disponibilité de base de données de destination (DAG), le site Active Directory, la forêt Active Directory ou le domaine de destination en dehors de l'organisation.

Le service de transport du serveur de boîtes aux lettres comprend les composants et processus suivants :

  - **Réception SMTP**   Lorsque le service de transport reçoit des messages, leur contenu est inspecté, des règles de transport sont appliquées et des opérations d'inspection anti-spam et anti-programme malveillant sont exécutées si elles sont activées. La session SMTP présente une série d'événements qui fonctionnent ensemble dans un ordre spécifique pour valider le contenu d'un message avant de l'accepter. Quand un message a franchi le processus de réception SMTP sans être rejeté par des événements de réception ou un agent anti-spam et anti-programme malveillant, il est placé dans la file d'attente de dépôt.

  - **Dépôt**   Le dépôt est le processus consistant à placer des messages dans la file d'attente de dépôt. Le catégoriseur sélectionne un message à la fois pour la catégorisation. Voici les trois modes de dépôt :
    
      - À partir de la réception SMTP via un connecteur de réception.
    
      - Via le répertoire de collecte ou le répertoire de relecture. Ces répertoires existent sur les serveurs de boîtes aux lettres et les serveurs de transport Edge. Les fichiers de message correctement mis en forme qui sont copiés dans le répertoire de collecte ou le répertoire de relecture sont placés directement dans la file d'attente de dépôt.
    
      - Via un agent de transport.

  - **Catégoriseur**   Le catégoriseur collecte un message à la fois dans la file d'attente de dépôt. Le catégoriseur exécute les étapes suivantes :
    
      - résolution du destinataire, qui inclut un adressage, une extension et une bifurcation de niveau supérieur ;
    
      - résolution de routage ;
    
      - conversion de contenu.
    
    En outre, les règles de flux de messagerie définies par l'organisation sont appliquées. Une fois les messages catégorisés, ils sont placés dans une file d'attente de remise qui varie selon la destination du message. Les messages sont placés dans une file d'attente par la base de données de la boîte aux lettres de destination, le groupe de disponibilité de base de données, le site Active Directory, le domaine externe ou la forêt Active Directory.

  - **Envoi SMTP**   L'acheminement des messages à partir du service de transport varie selon l'emplacement des destinataires des messages par rapport au serveur de boîtes aux lettres sur lequel a lieu la catégorisation. Le message peut être acheminé vers l’un des emplacements suivants :
    
      - Vers le service de transport de boîtes aux lettres sur le même serveur de boîtes aux lettres.
    
      - Vers le service de transport de boîtes aux lettres sur un serveur de boîtes aux lettres distinct qui fait partie du même groupe de disponibilité de base de données (DAG).
    
      - Vers le service de transport sur un serveur de boîtes aux lettres dans un autre DAG, un site Active Directory ou une forêt Active Directory.
    
      - Pour une remise sur Internet par un connecteur d’envoi sur le même serveur de boîtes aux lettres, par le service de transport sur un serveur de boîtes aux lettres distinct, par le service de transport frontal sur un serveur d’accès au client ou par le service de transport sur un serveur de transport Edge dans le réseau de périmètre.

## Service de transport sur les serveurs de transport Edge

Les composants du service de transport sur les serveurs de transport Edge sont identiques aux composants du service de transport sur les serveurs de boîtes aux lettres. Cependant, ce qui se passe réellement au cours de chaque étape du traitement sur les serveurs de transport Edge est différent. Les différences sont décrites dans la liste suivante.

  - **Réception SMTP**   Quand un serveur de transport Edge est abonné à un site Active Directory interne, le connecteur de réception par défaut est automatiquement configuré pour accepter le courrier provenant de serveurs de boîtes aux lettres internes et d’Internet. Lorsque des messages Internet arrivent sur le serveur de transport Edge, les agents de blocage du courrier indésirable filtrent les connexions et le contenu du message, et aident à identifier l’expéditeur et le destinataire lors de l’acceptation du message dans l’organisation. Les agents de blocage du courrier indésirable sont installés et activés par défaut. Des fonctionnalités supplémentaires de filtrage des connexions et des pièces jointes sont disponibles, mais le filtrage intégré des programmes malveillants ne l’est pas. En outre, les règles de transport sont contrôlées par l’agent d’application de règles de transport Edge. Par rapport à l’agent de règles de transport sur les serveurs de boîtes aux lettres, seulement un petit sous-ensemble de conditions de règle de transport sont disponibles sur les serveurs de transport Edge. Toutefois, il existe des actions de règles de transport uniques associées aux connexions SMTP qui ne sont disponibles que sur les serveurs de transport Edge.

  - **Soumission**   Sur un serveur de transport Edge, les messages entrent généralement dans la file d’attente de soumission par le biais d’un connecteur de réception. Toutefois, le répertoire de collecte et le répertoire de relecture sont également disponibles.

  - **Catégoriseur**   Sur un serveur de transport Edge, la catégorisation est un court processus au cours duquel le message est directement placé dans une file d’attente de remise pour être remis aux destinataires internes ou externes.

  - **Envoi SMTP**   Quand un serveur de transport Edge est abonné à un site Active Directory interne, deux connecteurs d’envoi sont automatiquement créés et configurés. L’un est chargé d’envoyer le courrier sortant aux destinataires Internet, l’autre est chargé de l’envoi du courrier entrant provenant d’Internet aux destinataires internes. Le courrier entrant est envoyé au service de transport sur un serveur de boîtes aux lettres disponible dans le site Active Directory abonné.

## Informations sur le flux de messagerie

Le tableau suivant contient des liens vers des rubriques qui vous aideront à découvrir et à gérer le flux de messagerie dans Exchange 2013.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Rubrique</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="mail-routing-exchange-2013-help.md">Routage du courrier</a></p></td>
<td><p>Le routage de messagerie décrit comment les messages sont transmis entre des serveurs de messagerie.</p></td>
</tr>
<tr class="even">
<td><p><a href="connectors-exchange-2013-help.md">Connecteurs</a></p></td>
<td><p>Les connecteurs déterminent où et comment les messages sont transmis à destination et en provenance de serveurs Exchange.</p></td>
</tr>
<tr class="odd">
<td><p><a href="domains-exchange-2013-help.md">Domaines</a></p></td>
<td><p>Les domaines acceptés définissent les espaces d'adressage SMTP utilisés dans l'organisation Exchange. Les domaines distants configurent le formatage des messages et les paramètres de codage des messages envoyés à des domaines externes.</p></td>
</tr>
<tr class="even">
<td><p><a href="transport-agents-exchange-2013-help.md">Agents de transport</a></p></td>
<td><p>Les agents de transport agissent sur les messages pendant leur acheminement via le pipeline de transport Exchange.</p></td>
</tr>
<tr class="odd">
<td><p><a href="transport-high-availability-exchange-2013-help.md">Haute disponibilité du transport</a></p></td>
<td><p>La haute disponibilité du transport explique comment Exchange 2013 conserve des copies redondantes des messages pendant le transit et après leur remise.</p></td>
</tr>
<tr class="even">
<td><p><a href="transport-logs-exchange-2013-help.md">Journaux de transport</a></p></td>
<td><p>Les journaux de transport enregistrent le parcours des messages lorsqu'ils sont acheminés via le pipeline de transport.</p></td>
</tr>
<tr class="odd">
<td><p><a href="manage-message-approval-exchange-2013-help.md">Gérer l’approbation des messages</a></p></td>
<td><p>Le transport modéré nécessite l'approbation de messages envoyés à des destinataires spécifiques.</p></td>
</tr>
<tr class="even">
<td><p><a href="content-conversion-exchange-2013-help.md">conversion de contenu.</a></p></td>
<td><p>La conversion de contenu vérifie les options de conversion des messages au format TNEF (Transport Neutral encoding format) pour les destinataires externes, ainsi que les options de conversion MAPI pour les destinataires internes.</p></td>
</tr>
<tr class="odd">
<td><p><a href="dsns-and-ndrs-in-exchange-2013-exchange-2013-help.md">Notifications d’état de remise et notifications d’échec de remise dans Exchange 2013</a></p></td>
<td><p>Les notifications d'état de remise (DSN) sont des messages système envoyés aux expéditeurs des messages, tels que des notifications d'échec de remise.</p></td>
</tr>
<tr class="even">
<td><p><a href="track-messages-with-delivery-reports-exchange-2013-help.md">Suivre les messages avec des rapports de remise</a></p></td>
<td><p>La fonctionnalité Rapports de remise est un outil de suivi des messages qui permet d'obtenir l'état de remise des messages électroniques qui ont été envoyés ou reçus par des utilisateurs inclus dans le carnet d'adresses de votre organisation et qui présentent un objet donné. Vous pouvez suivre les informations de remise des messages envoyés ou reçus par une boîte aux lettres spécifique dans votre organisation.</p></td>
</tr>
<tr class="odd">
<td><p><a href="message-size-limits-exchange-2013-help.md">Tailles limites des messages</a></p></td>
<td><p>Cette rubrique décrit les limites de taille et de composants individuels qui sont imposées à des messages.</p></td>
</tr>
<tr class="even">
<td><p><a href="queue-viewer-exchange-2013-help.md">Afficheur des files d’attente</a></p></td>
<td><p>Utilisez l'Afficheur des files d'attente dans la boîte à outils Exchange pour afficher et agir sur les files d'attente et les messages qu'elles contiennent.</p></td>
</tr>
<tr class="odd">
<td><p><a href="pickup-directory-and-replay-directory-exchange-2013-help.md">Répertoire de collecte et répertoire de relecture</a></p></td>
<td><p>Les répertoires de collecte et de relecture permettent d'insérer des fichiers de message dans le pipeline de transport.</p></td>
</tr>
<tr class="even">
<td><p><a href="use-an-exchange-2010-or-2007-edge-transport-server-in-exchange-2013-exchange-2013-help.md">Utilisation d’un serveur de transport Edge Exchange 2010 ou 2007 dans Exchange 2013</a></p></td>
<td><p>Cette rubrique décrit les points importants liés à l'utilisation d'un serveur de transport Edge de versions précédentes d'Exchange dans Exchange 2013.</p></td>
</tr>
</tbody>
</table>

