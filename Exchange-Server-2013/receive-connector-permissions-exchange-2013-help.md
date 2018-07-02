---
title: 'Autorisations du connecteur de réception: Exchange 2013 Help'
TOCTitle: Autorisations du connecteur de réception
ms:assetid: 31af7139-6823-411b-81b3-e42edd83ee6c
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ673053(v=EXCHG.150)
ms:contentKeyID: 50477833
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Autorisations du connecteur de réception

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2015-04-07_

Le tableau suivant répertorie les types d’autorisations et fournit une description pour chacun.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Autorisation du connecteur de réception</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>ms-Exch-SMTP-Submit</p></td>
<td><p>La session doit recevoir cette autorisation, sans quoi elle ne peut pas soumettre de messages à ce connecteur de réception. Si une session ne dispose pas de cette autorisation, les commandes MAIL FROM et AUTH échouent.</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-SMTP-Accept-Any-Recipient</p></td>
<td><p>Cette autorisation permet à la session de relayer des messages via ce connecteur. Si cette autorisation n’est pas octroyée, seuls les messages adressés à des destinataires dans des domaines acceptés sont réceptionnés par ce connecteur.</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-SMTP-Accept-Any-Sender</p></td>
<td><p>Cette autorisation permet à la session d’ignorer le contrôle d’usurpation d’adresse de l’expéditeur.</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-SMTP-Accept-Authoritative-Domain-Sender</p></td>
<td><p>Cette autorisation permet aux expéditeurs ayant des adresses de messagerie dans des domaines faisant autorité d’établir une session sur ce connecteur de réception.</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-SMTP-Accept-Authentication-Flag</p></td>
<td><p>Cette autorisation permet aux serveurs Exchange 2003 d’envoyer des messages d’expéditeurs internes. Exchange 2010 reconnaît les messages comme internes. L’expéditeur peut déclarer le message comme approuvé. Les messages qui parviennent à votre système Exchange au moyen de dépôts anonymes sont relayés dans votre organisation Exchange avec cet indicateur dans un état non approuvé.</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Accept-Headers-Routing</p></td>
<td><p>Cette autorisation permet à la session de soumettre un message dont tous les en-têtes de réception sont intacts. Si cette autorisation n’est pas octroyée, le serveur supprime tous les en-têtes reçus.</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Accept-Headers-Organization</p></td>
<td><p>Cette autorisation permet à la session de soumettre un message dont tous les en-têtes d’organisation sont intacts. Les en-têtes d’organisation commencent tous par <strong>X-MS-Exchange-Organization-</strong>. Si cette autorisation n’est pas octroyée, le serveur de réception supprime tous les en-têtes d’organisation.</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Accept-Headers-Forest</p></td>
<td><p>Cette autorisation permet à la session de soumettre un message dont tous les en-têtes de forêt sont intacts. Les en-têtes de forêt commencent tous par <strong>X-MS-Exchange-Forest-</strong>. Si cette autorisation n’est pas octroyée, le serveur de réception supprime tous les en-têtes de forêt.</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Accept-Exch50</p></td>
<td><p>Cette autorisation permet à la session de soumettre un message contenant la commande XEXCH50. Cette commande est nécessaire pour assurer l’interopérabilité avec Exchange 2003. La commande XEXCH50 contient des données, telles que le seuil de probabilité de courrier indésirable (SCL) d’un message.</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Bypass-Message-Size-Limit</p></td>
<td><p>Cette autorisation permet à la session de soumettre un message dont la taille dépasse la valeur de restriction de taille de message configurée pour le connecteur.</p></td>
</tr>
<tr class="odd">
<td><p>Ms-Exch-Bypass-Anti-Spam</p></td>
<td><p>Cette autorisation permet à la session d’ignorer le filtrage du courrier indésirable.</p></td>
</tr>
</tbody>
</table>

