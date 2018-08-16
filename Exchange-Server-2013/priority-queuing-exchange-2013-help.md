---
title: 'priorité de mise en file d’attente ;: Exchange 2013 Help'
TOCTitle: priorité de mise en file d’attente ;
ms:assetid: 6edbd826-fe55-435b-9c63-48e6365c3d09
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb691107(v=EXCHG.150)
ms:contentKeyID: 51407203
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# priorité de mise en file d’attente ;

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2015-03-09_

La *priorité de mise en file d'attente* est une fonctionnalité de Microsoft Exchange Server 2013 qui permet au niveau de priorité d'un message défini par l'expéditeur d'influencer le traitement du message par le service de transport sur le serveur de boîtes aux lettres.

La priorité de message est attribuée par l'expéditeur dans Microsoft Outlook quand ce dernier crée et envoie le message. Le destinataire peut définir l'une des valeurs de priorité de message suivantes dans Outlook :

  - Importance faible

  - Importance normale

  - Importance haute

La priorité par défaut d'un message créé dans Outlook ou Outlook Web App est Normale. La priorité du message est stockée dans le champ d'en-tête `X-Priority` dans l'en-tête du message.

Chaque message échangé au sein d'une organisation Exchange 2013 doit être catégorisé dans le service de transport d'un serveur de boîtes aux lettres avant de pouvoir être acheminé et remis. Le catégoriseur du service de transport d'un serveur de boîtes aux lettres collecte un message à la fois dans la file d'attente de soumission et exécute la résolution des destinataires, la résolution du routage et la conversion de contenu du message avant de placer ce dernier dans une file d'attente de remise. Pour plus d'informations, consultez la rubrique [Flux de messagerie](mail-flow-exchange-2013-help.md).

Les files d'attente de remise sont créées dynamiquement en fonction de la destination d'un message. Pour plus d'informations, consultez la rubrique [Files d'attente](queues-exchange-2013-help.md).

Tous les messages avec la même destination sont placés dans la même file d'attente de remise. La priorité de mise en file d'attente a une incidence sur la transmission des messages d'une file d'attente de remise au serveur de messagerie de destination. Lorsque la priorité de mise en file d'attente est activée, les messages à priorité haute sont transmis à leurs destinations avant les messages à priorité normale, et les messages à priorité normale sont transmis avant les messages à priorité faible. La remise des messages en fonction de leur priorité peut vous aider à définir des exigences de contrat SLA spécifiques pour les heures de remise des messages.

## Options de configuration de la priorité de mise en file d'attente

La prise en charge de la priorité de mise en file d'attente est contrôlée par des clés dans le fichier XLML de configuration de l'application `%ExchangeInstallPath%bin\EdgeTransport.exe.config`. Pour obtenir des recommandations sur la configuration de la priorité de mise en file d'attente, consultez la rubrique [Activer et configurer la file d'attente prioritaire](enable-and-configure-priority-queuing-exchange-2013-help.md).

Le tableau suivant décrit chaque clé plus en détail.

### Clés de priorité de mise en file d'attente dans le fichier EdgeTransport.exe.config

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Clé</th>
<th>Valeur par défaut</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>PriorityQueuingEnabled</em></p></td>
<td><p><code>false</code></p></td>
<td><p>Cette clé active ou désactive la priorité de mise en file d'attente dans le service de transport du serveur de boîte aux lettres. L'entrée valide pour cette clé est <code>true</code> ou <code>false</code>.</p>
<p>Quand la valeur de cette clé est <code>false</code>, la priorité de mise en file d'attente est désactivée, toutes les limites de priorité de mise en file d'attente des messages du fichier EdgeTransport.exe.config sont ignorées.</p></td>
</tr>
<tr class="even">
<td><p><em>MaxHighPriorityMessageSize</em></p></td>
<td><p><code>250KB</code></p></td>
<td><p>Cette clé spécifie la taille maximale autorisée d'un message à priorité haute. Si la taille du message à priorité haute est supérieure à la valeur spécifiée par cette clé, le message est automatiquement rétrogradé de Priorité haute à Priorité normale.</p>
<p>La valeur de cette clé doit être sensiblement inférieure à la valeur du paramètre <em>MaxSendMessageSize</em> pour la cmdlet <strong>Set-TransportConfig</strong>. La valeur par défaut de ce paramètre est <code>10 MB</code>. La différence entre ces deux valeurs assure des heures de remise cohérentes et prévisibles pour les messages à priorité haute.</p>
<p>Lorsque vous entrez une valeur, qualifiez-la à l'aide de l'une des unités suivantes :</p>
<ul>
<li><p>Ko (kilo-octets)</p></li>
<li><p>Mo (mégaoctets)</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p><em>LowPriorityDelayNotificationTimeout</em></p>
<p><em>NormalPriorityDelayNotificationTimeout</em></p>
<p><em>HighPriorityDelayNotificationTimeout</em></p></td>
<td><p><strong>Faible</strong> <code>8:00:00</code> (8 heures)</p>
<p><strong>Normale</strong> <code>4:00:00</code> (4 heures)</p>
<p><strong>Haute</strong> <code>00:30:00</code> (30 minutes)</p></td>
<td><p>Ces clés spécifient l'intervalle du délai d'attente pour les messages de notification d'état de remise retardée en fonction de la priorité du message.</p>
<p>Après chaque échec de remise d'un message, le service de transport génère un message de notification d'état de remise retardée et le place en file d'attente pour remise à l'expéditeur du message non remis. Ce message de notification d'état de remise retardée est envoyé après un intervalle spécifié de délai de notification retardée et uniquement si le message ayant échoué n'a pas été remis avec succès entre temps. Cette durée évite l'envoi de messages inutiles de notification d'état de remise retardée pouvant être causée par des défaillances temporaires de transmission de messages.</p>
<p>Pour spécifier une valeur, entrez-la sous forme d’une période : jj.hh:mm:ss où j = jours, h = heures, m = minutes et s = secondes.</p></td>
</tr>
<tr class="even">
<td><p><em>LowPriorityMessageExpirationTimeout</em></p>
<p><em>NormalPriorityMessageExpirationTimeout</em></p>
<p><em>HighPriorityMessageExpirationTimeout</em></p></td>
<td><p><strong>Faible</strong> <code>2.00:00:00</code> (2 jours)</p>
<p><strong>Normale</strong> <code>2.00:00:00</code> (2 jours)</p>
<p><strong>Haute</strong> <code>8:00:00</code> (8 heures)</p></td>
<td><p>Ces clés spécifient la durée maximale pendant laquelle un service de transport tente de remettre un message ayant échoué. Si le message ne peut pas être remis avant la fin de l'intervalle du délai d'expiration, une notification d'échec de remise contenant le message d'origine ou les en-têtes de message est remise à l'expéditeur.</p>
<p>Pour spécifier une valeur, entrez-la sous forme d’une période : jj.hh:mm:ss où j = jours, h = heures, m = minutes et s = secondes.</p></td>
</tr>
<tr class="odd">
<td><p><em>MaxPerDomainLowPriorityConnections</em></p>
<p><em>MaxPerDomainNormalPriorityConnections</em></p>
<p><em>MaxPerDomainHighPriorityConnections</em></p></td>
<td><p><strong>Faible</strong>   2</p>
<p><strong>Normale</strong>   15</p>
<p><strong>Haute</strong>   3</p></td>
<td><p>Ces clés spécifient le nombre maximal de connexions qu'un service de transport peut ouvrir sur un seul domaine distant. Les connexions sortantes vers des domaines distants se produisent en utilisant les files d'attente de remise et les connecteurs d'envoi existant sur le serveur de boîtes aux lettres.</p>
<p>La somme de ces trois clés doit être inférieure ou égale à la valeur du paramètre <em>MaxPerDomainOutboundConnections</em> sur la cmdlet <strong>Set-TransportService</strong>. La valeur par défaut de ce paramètre est <code>20</code>.</p></td>
</tr>
</tbody>
</table>


## Comment la priorité de mise en file d'attente affecte les autres limites de message sur les serveurs de boîtes aux lettres ?

Tous les messages transmis via un service de transport sont soumis à diverses limites de relance, de resoumission et d'expiration de message. Pour plus d'informations, consultez la rubrique [Tailles limites des messages](message-size-limits-exchange-2013-help.md).

Certaines limites de message disponibles pour la cmdlet **Set-TransportService** ont des limites correspondantes de priorité de mise en file d'attente des messages. Ces dernières sont disponibles dans le fichier de configuration de l'application EdgeTransport.exe.config. Le tableau suivant présente ces limites de message correspondantes.

### Limites de message de la cmdlet Set-TransportService correspondant aux limites de priorité de mise en file d'attente des messages du fichier EdgeTransport.exe.config

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Source</th>
<th>Paramètre ou clé</th>
<th>Valeur par défaut</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Set-TransportService</strong></p></td>
<td><p><em>DelayNotificationTimeOut</em></p></td>
<td><p><code>4:00:00</code> (4 heures)</p></td>
</tr>
<tr class="even">
<td><p>EdgeTransport.exe.config</p></td>
<td><p><em>NormalPriorityDelayNotificationTimeout</em></p></td>
<td><p><code>4:00:00</code> (4 heures)</p></td>
</tr>
<tr class="odd">
<td><p><strong>Set-TransportService</strong></p></td>
<td><p><em>MessageExpirationTimeOut</em></p></td>
<td><p><code>2.00:00:00</code> (2 jours)</p></td>
</tr>
<tr class="even">
<td><p>EdgeTransport.exe.config</p></td>
<td><p><em>NormalPriorityMessageExpirationTimeout</em></p></td>
<td><p><code>2.00:00:00</code> (2 jours)</p></td>
</tr>
</tbody>
</table>


Lorsque la priorité de mise en file d'attente est désactivée, toutes les limites de priorité de mise en file d'attente des messages du fichier de configuration EdgeTransport.exe.config sont ignorées. Toutes les limites de message de la cmdlet **Set-TransportService** s'appliquent à tous les messages transitant via le service de transport sur le serveur de boîtes aux lettres.

Quand la priorité de mise en file d'attente est activée, les limites de priorité de mise en file d'attente des messages du fichier de configuration EdgeTransport.exe.config remplace les limites de message correspondantes pour la cmdlet **Set-TransportService**. Toutes les autres limites de message de la cmdlet **Set-TransportService** continuent de s'appliquer aux messages à priorité faible, à priorité normale ou à priorité haute transitant via le service de transport sur le serveur de boîtes aux lettres.

## Paramètres d'utilisateur pour la priorité de mise en file d'attente

La cmdlet **Set-Mailbox** a le paramètre *DowngradeHighPriorityMessagesEnabled*. La valeur par défaut est `$false`. Si ce paramètre est défini sur `$true`, les messages à priorité haute qui sont envoyés à partir de la boîte aux lettres sont automatiquement rétrogradés à Priorité normale.

