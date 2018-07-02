---
title: 'Intervalles de nouvelle tentative, de renvoi et d’expiration des messages: Exchange 2013 Help'
TOCTitle: Intervalles de nouvelle tentative, de renvoi et d’expiration des messages
ms:assetid: 03020e6f-4c01-4c6e-ae47-fd74d4c4f96a
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ891103(v=EXCHG.150)
ms:contentKeyID: 51407150
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Intervalles de nouvelle tentative, de renvoi et d’expiration des messages

 

_**Sapplique à :**Exchange Server 2013_

_**Dernière rubrique modifiée :**2015-03-09_

Dans Microsoft Exchange Server 2013, les messages pour lesquels la remise échoue sont soumis à divers délais de nouvelle tentative, de renvoi et d'expiration, en fonction de la source et de la destination du message. Une *Nouvelle tentative* est une nouvelle tentative de connexion à la destination. Un *renvoi* est l'action qui consiste à renvoyer les messages à la file d'attente de soumission afin que le catégoriseur les traite une nouvelle fois. Le message *expire* une fois que toutes les tentatives de remise ont échoué au cours d’une période spécifiée. Après l'expiration d'un message, l'expéditeur est notifié de l'échec de la remise. Le message est alors supprimé de la file d'attente.

Dans toutes les situations de nouvelle tentative, de renvoi ou d'expiration, vous pouvez intervenir manuellement avant l'exécution des actions automatiques sur les messages.

Pour obtenir des recommandations sur la configuration de ces paramètres, consultez la rubrique [Configuration d’intervalles de nouvelle tentative, de renvoi et d’expiration des messages](configure-message-retry-resubmit-and-expiration-intervals-exchange-2013-help.md).

## Options de configuration pour les nouvelles tentatives de message

Quand un serveur de transport ne parvient pas à se connecter au saut suivant, l'état Nouvelle tentative est affecté à la file d'attente. Les tentatives de connexion se poursuivent jusqu'à ce que la file d'attente expire ou que la connexion soit établie.

## Options de configuration pour les nouvelles tentatives de message automatiques

Les options de configuration disponibles pour les intervalles de nouvelle tentative de message sont décrites dans le tableau suivant.

### Options de configuration disponibles pour les intervalles de nouvelle tentative de message

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Paramètre ou nom de clé</th>
<th>Valeur par défaut</th>
<th>Configuration</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>QueueGlitchRetryCount</em></p></td>
<td><p>4</p></td>
<td><p>EdgeTransport.exe.config</p></td>
<td><p>Cette clé spécifie le nombre de tentatives de connexion effectuées dès qu'un serveur de transport rencontre des problèmes lors de la connexion au serveur de destination. Ces problèmes de connexion sont généralement causés par des pannes de réseau.</p>
<p>L'entrée valide pour ce paramètre est un entier allant de 0 à 15.</p>
<p>En principe, il est inutile de modifier cette clé, sauf si le réseau n'est pas fiable et fait face à de nombreuses interruptions de connexion.</p></td>
</tr>
<tr class="even">
<td><p><em>QueueGlitchRetryInterval</em></p></td>
<td><p><code>00:01:00</code> ou 1 minute</p></td>
<td><p>EdgeTransport.exe.config</p></td>
<td><p>Cette clé détermine l'intervalle de connexion entre chaque tentative de connexion spécifiée par la clé <em>QueueGlitchRetryCount</em>.</p>
<p>En principe, il est inutile de modifier ce paramètre, sauf si le réseau n'est pas fiable et fait face à de nombreuses interruptions de connexion.</p></td>
</tr>
<tr class="odd">
<td><p><em>TransientFailureRetryCount</em></p></td>
<td><p>6</p></td>
<td><p>Cmdlet <strong>Set-TransportService</strong> ou propriétés du serveur dans le Centre d’administration Exchange (CAE)</p></td>
<td><p>Ce paramètre spécifie le nombre de tentatives de connexion effectuées après l'échec des tentatives de connexion spécifiées par les clés <em>QueueGlitchRetryCount</em> et <em>QueueGlitchRetryInterval</em>. Les problèmes de connexion épuisant les paramètres <em>QueueGlitchRetryCount</em> et <em>QueueGlitchRetryInterval</em> peuvent être causés par le redémarrage du serveur ou par des échecs de recherches DNS mises en cache.</p>
<p>Une entrée valide pour ce paramètre est un entier compris entre 0 et 15. Si vous définissez ce paramètre sur 0, la prochaine tentative de connexion est contrôlée par le paramètre <em>OutboundConnectionFailureRetryInterval</em>.</p></td>
</tr>
<tr class="even">
<td><p><em>TransientFailureRetryInterval</em></p></td>
<td><ul>
<li><p>Service de transport sur les serveurs de boîtes aux lettres <code>00:05:00</code> ou 5 minutes</p></li>
<li><p>Serveurs de transport Edge : <code>00:01:00</code> ou 10 minutes</p></li>
</ul></td>
<td><p>Cmdlet <strong>Set-TransportService</strong> ou propriétés du serveur dans le CAE</p></td>
<td><p>Ce paramètre détermine l'intervalle de connexion entre chaque tentative de connexion spécifiée par le paramètre <em>TransientFailureRetryCount</em>.</p>
<p>Pour spécifier une valeur, entrez-la sous forme d’une période : jj.hh:mm:ss où j = jours, h = heures, m = minutes et s = secondes.</p></td>
</tr>
<tr class="odd">
<td><p><em>OutboundConnectionFailureRetryInterval</em></p></td>
<td><ul>
<li><p>Service de transport sur les serveurs de boîtes aux lettres <code>00:10:00</code> ou 10 minutes</p></li>
<li><p>Serveurs de transport Edge : <code>00:30:00</code> ou 30 minutes</p></li>
</ul></td>
<td><p>Cmdlet <strong>Set-TransportService</strong> ou propriétés du serveur dans le CAE</p></td>
<td><p>Ce paramètre spécifie l'intervalle de nouvelle tentative pour les tentatives de connexion sortante ayant échoué précédemment. Les tentatives de connexion précédemment échouées sont contrôlées par les paramètres <em>TransientFailureRetryCount</em> et <em>TransientFailureRetryInterval</em>.</p>
<p>Pour spécifier une valeur, entrez-la sous forme d’une période : jj.hh:mm:ss où j = jours, h = heures, m = minutes et s = secondes.</p></td>
</tr>
<tr class="even">
<td><p><em>MessageRetryInterval</em></p></td>
<td><p><code>00:15:00</code> ou 15 minutes</p></td>
<td><p>Cmdlet <strong>Set-TransportService</strong></p></td>
<td><p>Ce paramètre spécifie l'intervalle de nouvelle tentative des messages présentant l'état Nouvelle tentative. Nous vous recommandons de ne pas modifier la valeur par défaut, sauf si le support technique Microsoft préconise de le faire.</p></td>
</tr>
<tr class="odd">
<td><p><em>MailboxDeliveryQueueRetryInterval</em></p></td>
<td><p><code>00:05:00</code> ou 5 minutes</p></td>
<td><p>EdgeTransport.exe.config</p></td>
<td><p>Cette clé détermine la fréquence à laquelle les files d'attente tentent de se connecter au service de remise de transport des boîtes aux lettres pour une base de données de boîte aux lettres de destination ne pouvant être atteinte.</p>
<p>Pour spécifier une valeur, entrez-la sous forme d’une période : jj.hh:mm:ss où j = jours, h = heures, m = minutes et s = secondes.</p>
<p>Une entrée valide pour cette clé se situe entre 00:00:01 et 1.00:00:00.</p></td>
</tr>
</tbody>
</table>


Retour au début

## Options de configuration pour les nouvelles tentatives de message

Quand une une file d'attente de remise présente l'état Nouvelle tentative, vous pouvez forcer manuellement une tentative de connexion immédiate à l'aide de l'Afficheur des files d'attente dans la boîte à outils Exchange ou à l'aide de la cmdlet **Retry-Queue** dans l'environnement de ligne de commande. La tentative manuelle remplace la prochaine tentative planifiée. Si la connexion échoue, le minuteur d'intervalle de nouvelle tentative est réinitialisé. Pour que cette action ait un effet, la file d'attente de remise doit présenter l'état Nouvelle tentative.

Pour plus d'informations, consultez la section « Files d'attente de nouvelles tentatives » dans la rubrique [Gestion des files d’attente](manage-queues-exchange-2013-help.md).

Retour au début

## Options de configuration pour les messages de notification d'état de remise retardée

Après chaque échec de remise d'un message, le serveur de transport Edge ou le service de transport sur le serveur de boîtes aux lettres génère un message de notification d'état de remise retardée et le place en file d'attente pour remise à l'expéditeur du message non remis. Ce message de notification d'état de remise retardée est envoyé après un intervalle spécifié de délai de notification retardée et uniquement si le message ayant échoué n'a pas été correctement remis entre temps. Par défaut, l'intervalle de délai de notification de retard est 4 heures. Cette durée évite l'envoi de messages inutiles de notification d'état de remise retardée pouvant être causé par des défaillances temporaires de transmission de messages. L'envoi de messages de notification d'état de remise retardée peut être activé ou désactivé pour les messages provenant de l'organisation Exchange ou de l'extérieur.

Les options de configuration disponibles pour les messages de notification d'état de remise retardée sont décrites dans le tableau suivant.

### Options de configuration disponibles pour les messages de notification d'état de remise retardée

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Nom de paramètre</th>
<th>Default value</th>
<th>Emplacement</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>DelayNotificationTimeOut</em></p></td>
<td><p><code>4:00:00</code>4 heures</p></td>
<td><p>Cmdlet <strong>Set-TransportService</strong> ou propriétés du serveur dans le CAE</p></td>
<td><p>Ce paramètre spécifie le délai d'attente qu'observe le serveur avant d'envoyer un message de notification d'état de remise retardée à l'expéditeur du message. La valeur de ce paramètre doit toujours être supérieure à la valeur du paramètre <em>TransientFailureRetryCount</em> multipliée par la valeur du paramètre <em>TransientFailureRetryInterval</em>.</p>
<p>Pour spécifier une valeur, entrez-la sous forme d’une période : jj.hh:mm:ss où j = jours, h = heures, m = minutes et s = secondes.</p></td>
</tr>
<tr class="even">
<td><p><em>ExternalDelayDSNEnabled</em></p></td>
<td><p><code>$true</code></p></td>
<td><p><strong>Set-TransportConfig</strong></p></td>
<td><p>Ce paramètre spécifie si les messages de notification d'état de remise retardée peuvent être envoyés à des expéditeurs de messages externes à l'organisation Exchange.</p>
<p>L'entrée valide pour ce paramètre est <code>$true</code> ou <code>$false</code>.</p></td>
</tr>
<tr class="odd">
<td><p><em>InternalDelayDSNEnabled</em></p></td>
<td><p><code>$true</code></p></td>
<td><p><strong>Set-TransportConfig</strong></p></td>
<td><p>Ce paramètre spécifie si les messages de notification d'état de remise retardée peuvent être envoyés à des expéditeurs de messages internes à l'organisation Exchange.</p>
<p>L'entrée valide pour ce paramètre est <code>$true</code> ou <code>$false</code>.</p></td>
</tr>
</tbody>
</table>


<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Sur les serveurs de transport Hub Exchange 2007, tous les paramètres <em>ExternalDSN*</em> et <em>InternalDSN*</em> sont disponibles pour la cmdlet <strong>Set-TransportServer</strong>, et non pour la cmdlet <strong>Set-TransportConfig</strong>. Si votre organisation comporte des serveurs de transport Hub Exchange 2007, vous devez modifier ces valeurs à l'aide de la cmdlet <strong>Set-TransportServer</strong> sur chaque serveur de transport Hub Exchange 2007.</td>
</tr>
</tbody>
</table>


Retour au début

## Options de configuration pour les tentatives de nouvelle soumission de message

La nouvelle soumission de message renvoie les messages non remis à la file d'attente de soumission pour qu'ils soient de nouveau traités par le catégoriseur.

## Nouvelle soumission de message automatique

Les messages non remis sont automatiquement soumis de nouveau si la file d'attente de remise présente l'état Nouvelle tentative et n'a pas réussi à remettre des messages pendant une durée spécifiée. Ce laps de temps est déterminé par la clé *MaxIdleTimeBeforeResubmit* dans le fichier de configuration de l'application EdgeTransport.exe.config. Seuls les messages situés dans les files d'attente peuvent faire l'objet d'une nouvelle soumission automatique.

Pour spécifier une valeur, entrez-la sous forme d’une période : jj.hh:mm:ss où j = jours, h = heures, m = minutes et s = secondes.

Par défaut, la valeur est `12:00:00` (soit 12 heures).

## Nouvelle soumission de message manuelle

Vous pouvez soumettre à nouveau manuellement les messages présentant l’état suivant dans le service de transport sur un serveur de boîte aux lettres ou un serveur de transport Edge :

  - Files d'attente de remise dont l'état est Nouvelle tentative. Les messages dans les files d'attente ne doivent pas présenter l'état Suspendu ;

  - les messages dans la file d'attente inaccessible qui ne présentent pas l'état Suspendu ;

  - les messages dans la file d'attente de messages incohérents.

Pour plus d'informations sur la file d'attente de messages incohérents et la file d'attente inaccessible, consultez la section « Informations sur la file d'attente de messages incohérents et la file d'attente inaccessible » dans la rubrique [Files d'attente](queues-exchange-2013-help.md).

Si vous voulez resoumettre manuellement les messages qui se trouvent dans les files d'attente de remise ou la file d'attente inaccessible sans attendre le délai spécifié par le paramètre *MaxIdleTimeBeforeResubmit*, vous devez utiliser la cmdlet **Retry-Queue** avec le paramètre *Resubmit*. Pour resoumettre manuellement les messages figurant dans la file d'attente de messages incohérents, vous devez utiliser l'Afficheur des files d'attente ou la cmdlet **Resume-Message**. Pour plus d'informations, consultez la section « Resoumettre les messages en file d'attente » dans la rubrique [Gestion des files d’attente](manage-queues-exchange-2013-help.md).

Pour resoumettre manuellement les messages, il existe une autre méthode qui consiste à suspendre les messages, à les exporter vers des fichiers texte dotés d'une extension de nom de fichier .eml, puis à copier les fichiers .eml dans le répertoire de relecture de n'importe quel serveur de boîtes aux lettres ou de transport Edge. Cette méthode fonctionne pour les messages se trouvant dans les files d'attente de remise ou la file d'attente inaccessible. Les messages situés dans la file d'attente de messages incohérents présentent déjà l'état Suspendu. Il est impossible de suspendre ou d'exporter les messages situés dans la file d'attente de soumission.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Lorsque vous exportez des messages à partir d'une file d'attente, vous ne supprimez pas les messages de la file d'attente. Une fois les messages exportés et soumis de nouveau à l'aide du répertoire de relecture, vous devez supprimer les messages suspendus pour éviter de remettre des messages en double.</td>
</tr>
</tbody>
</table>


Pour plus d'informations, consultez la rubrique [Exportation de messages de files d'attente](export-messages-from-queues-exchange-2013-help.md).

Retour au début

## Options de configuration pour l'expiration des messages

Le *délai d’expiration des messages* spécifie la durée maximale pendant laquelle un serveur de transport Edge ou le service de transport sur un serveur de boîte aux lettres tente de remettre un message qui n’a pas pu être remis. S'il ne parvient pas à remettre le message avant la fin de ce délai, une notification d'échec de remise contenant le message d'origine ou les en-têtes du message est remise à l'expéditeur.

## Expiration de message automatique

Le délai d'expiration des messages est spécifié par le paramètre *MessageExpirationTimeOut* pour la cmdlet **Set-TransportService**, ou dans les propriétés du serveur de transport dans le CAE.

Pour spécifier une valeur, entrez-la sous forme d’une période : jj.hh:mm:ss où j = jours, h = heures, m = minutes et s = secondes.

Par défaut, la valeur est `2.00:00:00` (soit 2 jours). La plage d'entrées valide pour ce paramètre s'étend de `00:00:05` à `90.00:00:00`.

## Expiration de message manuelle

Bien qu'il soit impossible de forcer manuellement l'expiration des messages, il est possible de les supprimer manuellement d'une file d'attente, à l'exception de la file d'attente de soumission, avec ou sans notification d'échec de remise.

Pour plus d'informations, consultez la section « Supprimer les messages des files d'attente » dans la rubrique [Gestion des messages dans les files d'attente](manage-messages-in-queues-exchange-2013-help.md).

Retour au début

