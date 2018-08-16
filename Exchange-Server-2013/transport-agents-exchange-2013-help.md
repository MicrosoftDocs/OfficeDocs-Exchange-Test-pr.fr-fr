---
title: 'Agents de transport: Exchange 2013 Help'
TOCTitle: Agents de transport
ms:assetid: e7389d63-3172-40d5-bf53-0d7cd7e78340
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb125012(v=EXCHG.150)
ms:contentKeyID: 50479459
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Agents de transport

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2015-03-09_

Les agents de transport vous permettent d'installer des logiciels personnalisés créés par Microsoft, des fournisseurs tiers ou votre organisation sur un serveur Exchange Server. Ces logiciels peuvent ensuite traiter tous les messages électroniques qui transitent par un pipeline de transport. Dans Microsoft Exchange Server 2013, le pipeline de transport est composé des processus suivants :

  - Service de transport frontal sur les serveurs d’accès au client

  - Service de transport sur les serveurs de boîtes aux lettres

  - Service de transport de boîte aux lettres sur les serveurs de boîtes aux lettres

  - Service de transport sur les serveurs de transport Edge

Pour plus d’informations sur le pipeline de transport, voir [Flux de messagerie](mail-flow-exchange-2013-help.md).

Comme dans la version antérieure de Microsoft Exchange, le transport Exchange 2013 propose l'extensibilité via le SDK des agents de transport Microsoft Exchange Server 2013. La version d’Exchange 2013 dans le kit de développement logiciel (SDK) est basée sur la version 4.0 d’Microsoft.NET Framework et autorise les tiers à implémenter les classes prédéfinies suivantes :

  - **SmtpReceiveAgent**

  - **RoutingAgent**

  - **DeliveryAgent**

Suite à la vérification de leur conformité par rapport aux bibliothèques du SDK, les assemblies sont enregistrées avec Exchange 2013, qui charge les agents et fait appel à leurs gestionnaires d'événements pendant des étapes spécifiques des sessions SMTP ou de traitement des messages. Ces étapes ou événements font partie des définitions des agents. Les informations d'enregistrement des agents sont stockées dans un fichier de configuration XML.

La liste suivante explique les exigences relatives à l'utilisation des agents de transport dans Exchange 2013.

  - Le service de transport sur les serveurs de boîtes aux lettres et les serveurs de transport Edge prennent entièrement en charge toutes les classes prédéfinies dans le kit de développement logiciel (SDK). Par conséquent, tous les agents de transport tiers écrits pour les rôles serveur de transport Edge ou Hub dans Microsoft Exchange Server 2010 doivent fonctionner dans le service de transport d’Exchange 2013.

  - Le service de transport frontal prend uniquement en charge la classe **SmtpReceiveAgent** dans le SDK, et les agents tiers ne peuvent pas agir sur l'événement SMTP **OnEndOfData**.

  - Le service de transport de boîtes aux lettres ne prend pas intégralement en charge le SDK. Vous ne pouvez donc pas utiliser d'agents tiers dans ce service.

La prise en charge des anciens agents de transport basés sur les versions de .NET Framework antérieures à la version 4.0 n’est pas activée par défaut, mais vous pouvez l’activer. Pour plus d'informations, consultez la rubrique [Activer la prise en charge des agents de transport hérités](enable-support-for-legacy-transport-agents-exchange-2013-help.md).

**Contenu de cette rubrique**

Mises à jour de la gestion des agents de transport

Agents de transport et événements SMTP

Priorité des agents de transport

Agents de transport intégrés

Dépanner les agents de transport

## Mises à jour de la gestion des agents de transport

En raison des mises à jour du pipeline de transport Exchange 2013, les cmdlets de l’agent de transport doivent faire la distinction entre le service de transport et le service de transport frontal, surtout si le serveur d’accès au client et le serveur de boîtes aux lettres sont installés sur le même ordinateur. Pour plus d'informations, voir [Gérer les agents de transport](manage-transport-agents-exchange-2013-help.md).

Les cmdlets de gestion de l’agent de transport manipulent un fichier de configuration situé au niveau de `%ExchangeInstallPath%TransportRoles\Shared`. Pour le service de transport sur les serveurs de boîtes aux lettres et les serveurs de transport Edge, le fichier est `agents.config`. Pour le service de transport frontal sur les serveurs d’accès au client, le fichier est `fetagents.config`. Les deux fichiers utilisent le même format que dans Exchange 2010. Pour plus d’informations sur la gestion des agents de transport, voir [Gérer les agents de transport](manage-transport-agents-exchange-2013-help.md).

Retour au début

## Agents de transport et événements SMTP

Les agents de transport utilisent des événements SMTP. Ces événements sont déclenchés lors du déplacement de messages dans le pipeline de transport. Les événements SMTP permettent aux agents de transport d'accéder à des messages en des points spécifiques durant la conversation SMTP et durant le routage de messages dans l'organisation.

Notez qu’il existe de nouveaux événements de réception SMTP dans Exchange 2013. Ceux-ci sont surviennent dans le service de transport frontal sur les serveurs d’accès au client, dans le service de transport sur les serveurs de boîtes aux lettres et les serveurs de transport Edge, et dans le service de distribution de transport de boîtes aux lettres sur les serveurs de boîtes aux lettres. Le catégoriseur n’existe que dans le service de transport sur les serveurs de boîtes aux lettres et les serveurs de transport Edge. Pour plus d’informations sur les services de transport et le catégoriseur, voir [Routage du courrier](mail-routing-exchange-2013-help.md).

Le tableau suivant présente les événements SMTP qui donnent accès à des messages dans le pipeline de transport.

### Événements de réception SMTP

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Séquence</th>
<th>Événement SMTP</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>1</p></td>
<td><p><strong>OnConnectEvent</strong></p></td>
<td><p>Cet événement est déclenché par la connexion initiale à partir d’un hôte SMTP distant.</p></td>
</tr>
<tr class="even">
<td><p>2</p></td>
<td><p><strong>OnHeloCommand</strong></p></td>
<td><p>Cet événement est déclenché lors de l’émission de la commande <code>HELO</code> par l’hôte SMTP distant.</p></td>
</tr>
<tr class="odd">
<td><p>3</p></td>
<td><p><strong>OnEhloCommand</strong></p></td>
<td><p>Cet événement est déclenché lors de l’émission de la commande <code>EHLO</code> par l’hôte SMTP distant.</p></td>
</tr>
<tr class="even">
<td><p>4</p></td>
<td><p><strong>OnStartTlsCommand</strong></p></td>
<td><p>Cet événement est déclenché lors de l’émission de la commande <code>STARTTLS</code> par l’hôte SMTP distant.</p></td>
</tr>
<tr class="odd">
<td><p>5</p></td>
<td><p><strong>OnAuthCommand</strong></p></td>
<td><p>Cet événement est déclenché lors de l’émission de la commande <code>AUTH</code> par l’hôte SMTP distant.</p></td>
</tr>
<tr class="even">
<td><p>6</p></td>
<td><p><strong>OnProcessAuthentication</strong></p></td>
<td><p>Cet événement est déclenché lors du traitement de l’authentification avec l’hôte SMTP distant.</p></td>
</tr>
<tr class="odd">
<td><p>7</p></td>
<td><p><strong>OnEndOfAuthentication</strong></p></td>
<td><p>Cet événement est déclenché lorsque l'hôte SMTP distant a terminé l'authentification.</p></td>
</tr>
<tr class="even">
<td><p>8</p></td>
<td><p><strong>OnXSessionParamsCommand</strong></p></td>
<td><p>Cet événement est déclenché lors de l’émission de la commande <code>XSESSIONPARAMS</code> par l’hôte SMTP distant.</p></td>
</tr>
<tr class="odd">
<td><p>9</p></td>
<td><p><strong>OnMailCommand</strong></p></td>
<td><p>Cet événement est déclenché lors de l’émission de la commande <code>MAIL FROM</code> par l’hôte SMTP distant.</p></td>
</tr>
<tr class="even">
<td><p>10</p></td>
<td><p><strong>OnRcptToCommand</strong></p></td>
<td><p>Cet événement est déclenché lors de l’émission de la commande <code>RCPT TO</code> par l’hôte SMTP distant.</p></td>
</tr>
<tr class="odd">
<td><p>11</p></td>
<td><p><strong>OnDataCommand</strong></p></td>
<td><p>Cet événement est déclenché lorsque la commande <code>DATA</code> (texte) ou <code>BDAT</code> (données binaires) est émise par l’hôte SMTP distant.</p></td>
</tr>
<tr class="even">
<td><p>12</p></td>
<td><p><strong>OnEndOfHeaders</strong></p></td>
<td><p>Cet événement est déclenché lorsque l’hôte SMTP distant a terminé de soumettre les en-têtes de message électronique. Ceci est indiqué par une ligne vide (<code>&lt;CRLF&gt;</code>) séparant les en-têtes et le corps du message.</p></td>
</tr>
<tr class="odd">
<td><p>13</p></td>
<td><p><strong>OnProxyInboundMessage</strong></p></td>
<td><p>Cet événement est déclenché lorsqu’une session SMTP entrante est relayée ou <em>envoyée par proxy</em> par le service de transport frontal sur un serveur d’accès au client vers le service de transport sur un serveur de boîtes aux lettres.</p></td>
</tr>
<tr class="even">
<td><p>14</p></td>
<td><p><strong>OnEndOfData</strong></p></td>
<td><p>Cet événement est déclenché lorsque l’hôte SMTP distant émet une commande de fin des données. Pour les sessions de texte démarrées par la commande <code>DATA</code>, l’indicateur de fin des données est <code>&lt;CRLF&gt;.&lt;CRLF&gt;</code>. Pour les sessions binaires démarrées par la commande <code>BDAT</code>, l’indicateur de fin des données est <code>BDAT LAST</code>.</p></td>
</tr>
<tr class="odd">
<td><p>**</p></td>
<td><p><strong>OnHelpCommand</strong></p></td>
<td><p>Cet événement est déclenché si la commande <code>HELP</code> est émise par l’hôte SMTP distant.</p></td>
</tr>
<tr class="even">
<td><p>**</p></td>
<td><p><strong>OnNoopCommand</strong></p></td>
<td><p>Cet événement est déclenché si la commande <code>NOOP</code> est émise par l’hôte SMTP distant.</p></td>
</tr>
<tr class="odd">
<td><p>**</p></td>
<td><p><strong>OnReject</strong></p></td>
<td><p>Cet événement est déclenché si l’hôte SMTP de réception émet une notification d’état de remise temporaire ou permanente destinée à l’hôte SMTP d’envoi.</p></td>
</tr>
<tr class="even">
<td><p>**</p></td>
<td><p><strong>OnRsetCommand</strong></p></td>
<td><p>Cet événement est déclenché si la commande <code>RSET</code> est émise par l’hôte SMTP d’envoi.</p></td>
</tr>
<tr class="odd">
<td><p>15</p></td>
<td><p><strong>OnDisconnectEvent</strong></p></td>
<td><p>Cet événement est déclenché par la déconnexion de la conversation SMTP par l’hôte SMTP de réception ou d’envoi. En général, cela se produit lorsque la commande <code>QUIT</code> est émise par l’hôte SMTP distant.</p></td>
</tr>
</tbody>
</table>


\*\* Ces événements peuvent survenir n’importe quand après **OnConnectEvent** mais avant **OnDisconnectEvent**.

### Événements du catégoriseur

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Séquence</th>
<th>Événement du catégoriseur</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>1</p></td>
<td><p><strong>OnSubmittedMessage</strong></p></td>
<td><p>Cet événement est déclenché quand un message arrive dans la file d’attente de soumission du service de transport sur le serveur de boîtes aux lettres de réception ou le serveur de transport Edge.</p></td>
</tr>
<tr class="even">
<td><p>2</p></td>
<td><p><strong>OnResolvedMessage</strong></p></td>
<td><p>Cet événement est déclenché lorsque tous les destinataires ont été résolus, mais avant que le saut suivant ait été déterminé pour chaque destinataire. L’événement de routage <strong>OnResolvedMessage</strong> permet que des événements ultérieurs remplacent le comportement de routage par défaut à l’aide de la méthode <strong>SetRoutingOverride</strong> par destinataire.</p></td>
</tr>
<tr class="odd">
<td><p>3</p></td>
<td><p><strong>OnRoutedMessage</strong></p></td>
<td><p>Cet événement est déclenché après la catégorisation des messages, l'extension des listes de distribution et la résolution des destinataires.</p></td>
</tr>
<tr class="even">
<td><p>4</p></td>
<td><p><strong>OnCategorizedMessage</strong></p></td>
<td><p>Cet événement est déclenché lorsque le catégoriseur termine le traitement du message.</p></td>
</tr>
</tbody>
</table>


Retour au début

## Priorité des agents de transport

Deux facteurs déterminent l’ordre dans lequel les agents de transport agissent sur les messages dans le pipeline de transport :

1.  L’événement SMTP où l’agent de transport est inscrit et le moment où cet événement SMTP détecte des messages.

2.  La valeur de priorité attribuée à l’agent de transport s’il y a plusieurs agents inscrits au même événement SMTP. La priorité la plus élevée est 1. Une valeur entière supérieure indique une priorité plus faible pour l’agent.

Par exemple, supposons que vous avez configuré les agents de transport suivants :

  - L’agent de transport A avec une priorité de 1 et l’agent de transport C avec une priorité de 2 sont inscrits à l’événement SMTP **OnEndOfHeaders**.

  - L’agent de transport B avec une priorité de 4 est inscrit à l’événement SMTP **OnMailCommand**.

L’agent de transport B est appliqué en premier aux messages car l’événement **OnMailCommand** détecte les messages avant l’événement **OnEndOfHeaders**. Lorsque les messages atteignent l’événement **OnEndOfHeaders**, l’agent de transport A est appliqué avant l’agent de transport C, car il est prioritaire (valeur entière plus faible).

## Agents de transport intégrés

Exchange 2013 comprend de nombreux agents de transport intégrés qui offrent des fonctionnalités telles que la protection anti-courrier indésirable, les règles de transport et la journalisation. La plupart des agents de transport intégrés sur les serveurs de boîtes aux lettres et les serveurs d’accès au client Exchange 2013 sont invisibles et non gérables via les cmdlets de gestion des agents de transport. La quasi-totalité des agents de transport intégrés qui sont visibles et gérables se trouvent dans le service de transport sur les serveurs de boîtes aux lettres et sur les serveurs de transport Edge.

Les agents de transport intégrés les plus intéressants sur les serveurs de boîtes aux lettres sont décrits dans le tableau suivant. Notez qu’un grand nombre d’agents de transport invisibles et non gérables a été omis.

### Agents de transport intégrés intéressants sur les serveurs de boîtes aux lettres

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Nom de l’agent</th>
<th>Gérable ?</th>
<th>Priorité</th>
<th>Événements SMTP ou du catégoriseur</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Agent de règles de transport</p></td>
<td><p>Oui</p></td>
<td><p>1</p></td>
<td><p><strong>OnResolvedMessage</strong></p></td>
</tr>
<tr class="even">
<td><p>Agent de programme malveillant</p></td>
<td><p>Oui</p></td>
<td><p>2</p></td>
<td><p><strong>OnSubmittedMessage</strong></p></td>
</tr>
<tr class="odd">
<td><p>Agent de routage de messagerie texte</p></td>
<td><p>Oui</p></td>
<td><p>3</p></td>
<td><p><strong>OnSubmittedMessage</strong></p></td>
</tr>
<tr class="even">
<td><p>Agent de remise de la messagerie texte</p></td>
<td><p>Oui</p></td>
<td><p>4</p></td>
<td><p>s/o</p></td>
</tr>
<tr class="odd">
<td><p>Agent de journalisation</p></td>
<td><p>Non</p></td>
<td><p>Non configurable</p></td>
<td><p><strong>OnRoutedMessage</strong></p></td>
</tr>
<tr class="even">
<td><p>Agent de déchiffrement du rapport de journal</p></td>
<td><p>Non</p></td>
<td><p>Non configurable</p></td>
<td><p><strong>OnCategorizedMessage</strong></p></td>
</tr>
<tr class="odd">
<td><p>Agent de déchiffrement RMS</p></td>
<td><p>Non</p></td>
<td><p>Non configurable</p></td>
<td><p><strong>OnSubmittedMessage</strong></p></td>
</tr>
<tr class="even">
<td><p>Agent de chiffrement RMS</p></td>
<td><p>Non</p></td>
<td><p>Non configurable</p></td>
<td><p><strong>OnSubmittedMessage</strong>, <strong>OnRoutedMessage</strong></p></td>
</tr>
<tr class="odd">
<td><p>Agent de déchiffrement de protocole RMS</p></td>
<td><p>Non</p></td>
<td><p>Non configurable</p></td>
<td><p><strong>OnEndOfData</strong></p></td>
</tr>
</tbody>
</table>


Sur les serveurs de transport Edge, la plupart des agents de transport intégrés sont visibles et gérables par les cmdlets de gestion des agents de transport ou par d’autres cmdlets propres à des fonctionnalités.

Les agents de transport intégrés les plus intéressants sur les serveurs transport Edge sont décrits dans le tableau suivant. Notez que les agents de transport invisibles et non gérables a été omis.

### Agents de transport intégrés intéressants sur les serveurs de Transport Edge

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Nom de l’agent</th>
<th>Gérable ?</th>
<th>Priorité</th>
<th>Événements SMTP ou du catégoriseur</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Agent de filtrage des connexions</p></td>
<td><p>Oui</p></td>
<td><p>1</p></td>
<td><p><strong>OnConnectEvent</strong>, <strong>OnMailCommand</strong>, <strong>OnRcptComand</strong> et <strong>OnEndOfHeaders</strong></p></td>
</tr>
<tr class="even">
<td><p>Agent de réécriture d’adresses pour les messages entrants</p></td>
<td><p>Oui</p></td>
<td><p>2</p></td>
<td><p><strong>OnRcptCommand</strong>, <strong>OnEndOfHeaders</strong></p></td>
</tr>
<tr class="odd">
<td><p>Agent d’application de règles de transport Edge</p></td>
<td><p>Oui</p></td>
<td><p>3</p></td>
<td><p><strong>OnEndOfData</strong></p></td>
</tr>
<tr class="even">
<td><p>Agent de filtrage du contenu*</p></td>
<td><p>Oui</p></td>
<td><p>4</p></td>
<td><p><strong>OnEndOfData</strong></p></td>
</tr>
<tr class="odd">
<td><p>Agent d’ID de l’expéditeur*</p></td>
<td><p>Oui</p></td>
<td><p>5</p></td>
<td><p><strong>OnEndOfHeaders</strong></p></td>
</tr>
<tr class="even">
<td><p>Agent de filtrage des expéditeurs*</p></td>
<td><p>Oui</p></td>
<td><p>6</p></td>
<td><p><strong>OnMailCommand</strong>, <strong>OnEndOfHeaders</strong></p></td>
</tr>
<tr class="odd">
<td><p>Agent de filtrage des destinataires</p></td>
<td><p>Oui</p></td>
<td><p>7</p></td>
<td><p><strong>OnRcptCommand</strong></p></td>
</tr>
<tr class="even">
<td><p>Agent d’analyse de protocole*</p></td>
<td><p>Oui</p></td>
<td><p>8</p></td>
<td><p><strong>OnConnectEvent</strong>, <strong>OnEndOfHeaders</strong>, <strong>OnEndOfData</strong>, <strong>OnReject</strong>, <strong>OnRsetCommand</strong> et <strong>OnDisconnectEvent</strong></p></td>
</tr>
<tr class="odd">
<td><p>Agent de filtrage des pièces jointes</p></td>
<td><p>Oui</p></td>
<td><p>9</p></td>
<td><p><strong>OnEndOfData</strong></p></td>
</tr>
<tr class="even">
<td><p>Agent de réécriture d’adresses pour les messages sortants</p></td>
<td><p>Oui</p></td>
<td><p>10</p></td>
<td><p><strong>OnSubmittedMessage</strong>, <strong>OnRoutedMessage</strong></p></td>
</tr>
</tbody>
</table>


\* Vous pouvez également installer et configurer ces agents anti-courrier indésirable sur les serveurs de boîtes aux lettres. Pour plus d’informations, voir [Activer la fonctionnalité de blocage du courrier indésirable sur un serveur de boîtes aux lettres](enable-anti-spam-functionality-on-mailbox-servers-exchange-2013-help.md).

Retour au début

## Dépanner les agents de transport

Pour résoudre les problèmes liés aux agents de transport, vous pouvez utiliser les fonctionnalités suivantes :

  - **Get-TransportPipeline** : cette cmdlet affiche les événements SMTP et les agents de transport correspondants qui détectent des messages sur le serveur Exchange. Pour plus d’informations, voir [Afficher les agents de transport dans le pipeline de transport](view-transport-agents-in-the-transport-pipeline-exchange-2013-help.md).

  - **Suivi du pipeline** : le suivi du pipeline génère une capture instantanée exacte d’un message avant et après sa rencontre avec chaque agent de transport. Cela vous permet de rechercher un agent de transport qui fournit des résultats inattendus. Pour plus d’informations, voir [Suivi du pipeline](pipeline-tracing-exchange-2013-help.md).

Retour au début

