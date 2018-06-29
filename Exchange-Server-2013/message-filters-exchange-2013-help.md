---
title: 'Filtres de messages: Exchange 2013 Help'
TOCTitle: Filtres de messages
ms:assetid: 8e6187c1-76f0-49da-bc24-2ab57cfb3c2c
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb123714(v=EXCHG.150)
ms:contentKeyID: 50478678
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Filtres de messages

 

_**Sapplique à :**Exchange Server 2013_

_**Dernière rubrique modifiée :**2015-03-09_

Le filtrage génère différentes vues des messages figurant dans les files d'attente. La spécification de critères de filtrage vous permet d'identifier rapidement des messages et d'agir sur ces derniers. Lors de l'envoi d'un message électronique à plusieurs destinataires, le message peut se trouver dans plusieurs files d'attente. Quand vous filtrez les messages en fonction de leurs propriétés, vous pouvez localiser des messages dans toutes les files d'attente. Les scénarios suivants illustrent la manière dont vous pouvez utiliser le filtrage des messages pour gérer le flux de messagerie :

  - La file d'attente de soumission sur le serveur de boîtes aux lettres ou le serveur de transport Edge qui reçoit des messages en provenance d'Internet contient un volume important de messages placés en file d'attente pour remise. De nombreux messages ont le même objet. C'est pourquoi vous pensez que du courrier indésirable est envoyé à votre organisation. Vous pouvez créer un filtre pour afficher tous les messages correspondant aux critères d'objet. Si vous constatez qu'il s'agit de courrier indésirable, vous pouvez sélectionner tous les messages et les supprimer de la file d'attente de remise sans envoyer de notification d'échec de remise.

  - Un utilisateur signale que le flux de messagerie est lent. Vous examinez les files d'attente et constatez que de nombreux messages dont les objets sont aléatoires semblent provenir d'un même domaine. Vous pouvez créer un filtre pour afficher tous les messages mis en file d'attente qui proviennent de ce domaine. Si vous constatez qu'il s'agit de courrier indésirable, vous pouvez sélectionner tous les messages et les supprimer des files d'attente sans envoyer de notification d'échec de remise.

## Utilisation des propriétés de message en tant que filtres

Vous pouvez utiliser des propriétés de message pour créer un filtre et identifier les messages répondant à des critères spécifiés. Vous pouvez créer des filtres dans l'Afficheur des files d'attente ou en utilisant le paramètre *Filter* sur les cmdlets de gestion des messages. Notez que les cmdlets de gestion des messages prennent en charge un plus grand nombre de propriétés filtrables que l'Afficheur des files d'attente. Le tableau suivant répertorie les propriétés de message à l'aide desquelles vous pouvez filtrer les messages, ainsi que les valeurs associées à ces propriétés.

### Propriétés de message à utiliser lors du filtrage de messages

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Propriété de message dans l'Afficheur des files d'attente</th>
<th>Propriété de message dans l'environnement de ligne de commande Exchange Management Shell</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Date de réception</strong></p></td>
<td><p><code>DateReceived</code></p></td>
<td><p>Date et heure de mise en file d'attente du message.</p></td>
</tr>
<tr class="even">
<td><p>N/A</p></td>
<td><p><code>DeferReason</code></p></td>
<td><p>Cette propriété indique pourquoi le message a été différé. Si le message n'a pas été différé, cette propriété a la valeur <code>None</code>. Un message différé est renvoyé à la file d'attente de soumission en raison d'erreurs temporaires rencontrées lors de la résolution du destinataire. Pour plus d'informations sur les messages différés, consultez la rubrique <a href="recipient-resolution-exchange-2013-help.md">Résolution des destinataires</a>. Les valeurs possibles sont les suivantes :</p>
<p><code>AD Transient Failure During Content Conversion</code></p>
<p><code>AD Transient Failure During Resolve</code></p>
<p><code>Agent</code></p>
<p><code>Ambiguous Recipient</code></p>
<p><code>Loop Detected</code></p>
<p><code>Marked As Retry Delivery If Rejected</code></p>
<p><code>Rerouted By Store Driver</code></p>
<p><code>Storage Transient Failure During Content Conversion</code></p>
<p><code>Transient Failure</code></p>
<p><code>Target Site Inbound Mail Disabled</code></p>
<p><code>Recipient Thread Limit Exceeded</code></p>
<p><code>Transient Attribution Failure</code></p>
<p><code>Transient Accepted Domains Load Failure</code></p></td>
</tr>
<tr class="odd">
<td><p><strong>Heure d'expiration</strong></p></td>
<td><p><code>ExpirationTime</code></p></td>
<td><p>Cette propriété contient la date et l'heure d'expiration du message et de sa suppression de la file d'attente s'il ne peut pas être remis.</p></td>
</tr>
<tr class="even">
<td><p><strong>Adresse de l'expéditeur</strong></p></td>
<td><p><code>FromAddress</code></p></td>
<td><p>Cette propriété contient l'adresse SMTP de l'expéditeur.</p></td>
</tr>
<tr class="odd">
<td><p>N/A</p></td>
<td><p><code>Identity</code></p></td>
<td><p>Cette propriété est l'identité du message sous la forme <em>&lt;serveur&gt;\&lt;file_attente&gt;\&lt;MessageInteger&gt;</em>. Pour plus d'informations, consultez la section « Identité de message » de la rubrique <a href="queues-exchange-2013-help.md">Files d'attente</a>.</p></td>
</tr>
<tr class="even">
<td><p><strong>Identificateur du message Internet</strong></p></td>
<td><p><code>InternetMessageId</code></p></td>
<td><p>Cette propriété contient la valeur du champ d'en-tête <code>Message-ID:</code> situé dans l'en-tête du message. La valeur est exprimée sous la forme d'une adresse de messagerie contenant un GUID et le nom de domaine complet du serveur SMTP d'envoi. Par exemple :</p>
<p><code>&lt;67D754D6103DC4FB3BA6BC7205DACABA61231@mailbox01.contoso.com&gt;</code></p></td>
</tr>
<tr class="odd">
<td><p><strong>Dernière erreur</strong></p></td>
<td><p><code>LastError</code></p></td>
<td><p>Cette propriété contient le texte de la dernière erreur enregistrée pour un message. Par exemple, <code>A matching connector cannot be found to route the external recipient</code>.</p></td>
</tr>
<tr class="even">
<td><p>N/A</p></td>
<td><p><code>MessageLatency</code></p></td>
<td><p>Cette propriété contient la durée écoulée entre la première entrée du message dans la file d'attente de soumission sur le serveur et le moment où celui-ci a été placé dans la file d'attente. La valeur utilise la syntaxe <em>hh:mm:ss.ff</em>, où <em>hh</em> = heure, <em>mm</em> = minute, <em>ss</em> = seconde et <em>ff</em> = fractions d'une seconde.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Nom de la source du message</strong></p></td>
<td><p><code>MessageSourceName</code></p></td>
<td><p>Cette propriété contient une chaîne de caractères qui indique le nom du composant de transport ayant envoyé ce message à la file d'attente. Par exemple, si le message est arrivé par un connecteur de réception, la valeur est : <code>SMTP:</code><em>&lt;nom_connecteur&gt;</em>. Si le message est une notification d'état de remise, la valeur est <code>DSN</code>.</p></td>
</tr>
<tr class="even">
<td><p>N/A</p></td>
<td><p><code>Priority</code></p></td>
<td><p>Cette propriété contient la priorité du message attribuée par l'utilisateur dans Outlook ou Outlook Web App. Les valeurs possibles sont <code>Low</code>, <code>Normal</code> et <code>High</code>. Pour plus d'informations, consultez la rubrique <a href="priority-queuing-exchange-2013-help.md">priorité de mise en file d’attente ;</a>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Identificateur de file d'attente</strong></p></td>
<td><p><code>Queue</code></p></td>
<td><p>Cette propriété est l'identité de la file d'attente dans laquelle figure le message. L'identité de la file d'attente utilise la syntaxe <em>&lt;serveur&gt;\&lt;file_attente&gt;</em>. Pour plus d'informations, consultez la section « Identité de file d'attente » de la rubrique <a href="queues-exchange-2013-help.md">Files d'attente</a>.</p></td>
</tr>
<tr class="even">
<td><p>N/A</p></td>
<td><p><code>RetryCount</code></p></td>
<td><p>Cette propriété identifie le nombre de tentatives d'envoi automatiques ou manuelles du message à la destination.</p></td>
</tr>
<tr class="odd">
<td><p><strong>SCL</strong></p></td>
<td><p><code>SCL</code></p></td>
<td><p>La valeur de la propriété SCL spécifie le seuil de probabilité de courrier indésirable (SCL) du message. Les entrées de seuil de probabilité de courrier indésirable admises sont des entiers compris entre 0 et 9. Si la valeur de la propriété SCL n'est pas indiquée, cela signifie que le message n'a pas été traité par l'agent de filtrage du contenu.</p>
<p>Cette propriété contient la valeur de seuil de probabilité de courrier indésirable du message. Les entrées de seuil de probabilité de courrier indésirable admises sont des entiers compris entre 0 et 9 et -1. Pour plus d'informations, consultez la rubrique <a href="spam-confidence-level-threshold-exchange-2013-help.md">Niveau de confiance du courrier indésirable</a>.</p></td>
</tr>
<tr class="even">
<td><p><strong>Taille (Ko)</strong></p></td>
<td><p><code>Size</code></p></td>
<td><p>Cette propriété indique la taille du message.</p></td>
</tr>
<tr class="odd">
<td><p><strong>IP source</strong></p></td>
<td><p><code>SourceIP</code></p></td>
<td><p>Cette propriété contient l'adresse IP du serveur ayant envoyé le message au serveur Exchange qui contient la file d'attente dans laquelle figure le message. L'adresse peut prendre la forme de l'adresse IP d'un serveur SMTP distant ou de l'adresse IP du serveur Exchange local.</p></td>
</tr>
<tr class="even">
<td><p><strong>État</strong></p></td>
<td><p><code>Status</code></p></td>
<td><p>Cette propriété indique l'état actuel du message. Les valeurs d'état d'un message peuvent être les suivantes :</p>
<p><code>Active</code></p>
<p><code>Locked</code></p>
<p><code>None</code></p>
<p><code>Pending Remove</code></p>
<p><code>Pending Suspend</code></p>
<p><code>Ready</code></p>
<p><code>Retry</code></p>
<p><code>Suspended</code></p>
<p>Pour plus d'informations, consultez la section « Propriétés de message » de la rubrique <a href="queues-exchange-2013-help.md">Files d'attente</a>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Objet</strong></p></td>
<td><p><code>Subject</code></p></td>
<td><p>Cette propriété spécifie l'objet d'un message se trouvant dans le champ d'en-tête <code>Subject:</code> de l'en-tête du message.</p></td>
</tr>
</tbody>
</table>

