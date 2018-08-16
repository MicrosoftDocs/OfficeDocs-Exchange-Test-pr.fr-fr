---
title: 'Filtres de file d’attente: Exchange 2013 Help'
TOCTitle: Filtres de file d’attente
ms:assetid: fbfbdcab-e0d2-4ed9-8f7f-e5fa2c87360d
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb125237(v=EXCHG.150)
ms:contentKeyID: 50479614
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Filtres de file d’attente

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2015-03-09_

Le filtrage génère différentes vues de files d'attente. Vous utilisez les propriétés de file d'attente comme options de filtrage. En spécifiant des critères de filtrage, vous pouvez localiser rapidement des files d'attente et agir sur ces dernières. Les scénarios suivants illustrent la manière dont vous pouvez utiliser le filtrage des files d'attente pour gérer le flux de messagerie :

  - Vous recevez un message de Microsoft System Center Operations Manager, indiquant que la longueur d'une file d'attente a dépassé le seuil défini. Vous chercher à savoir s'il existe un problème de flux de messagerie au niveau du serveur.
    
    Vous pouvez créer un filtre pour afficher toutes les files d'attente contenant un nombre de messages supérieur au seuil normal. Si un problème de flux de messagerie est signalé, vous pouvez sélectionner toutes les files d'attente dans les résultats du filtre, et les suspendre pendant que vous poursuivez votre investigation.

  - Vous suspendez plusieurs files d'attente pour rechercher la cause des problèmes de flux de messagerie. Vous déterminez que le problème était lié à la configuration incorrecte d'un connecteur et qu'il est désormais résolu.
    
    Vous pouvez créer un filtre pour afficher toutes les files d'attente présentant l'état Suspendu, puis les sélectionner dans les résultats du filtre et les reprendre.

## Propriétés de file d'attente à utiliser lors du filtrage de files d'attente

Vous pouvez utiliser les propriétés de file d'attente pour créer un filtre et identifier les files d'attente répondant à des critères spécifiés. Vous pouvez créer des filtres dans l'Afficheur des files d'attente ou en utilisant le paramètre *Filter* avec les cmdlets de gestion des files d'attente. Notez que les cmdlets de gestion des files d'attente prennent en charge un plus grand nombre de propriétés filtrables que l'Afficheur des files d'attente. Le tableau suivant répertorie les propriétés de file d'attente permettant de filtrer, ainsi que les valeurs valides pour ces propriétés.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Propriété de file d'attente dans l'Afficheur des files d'attente</th>
<th>Propriété de file d'attente dans l'environnement de ligne de commande</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>s/o</p></td>
<td><p><code>DeferredMessageCount</code></p></td>
<td><p>Cette propriété identifie le nombre de messages renvoyés à la file d'attente de soumission en raison d'erreurs temporaires rencontrées lors de la résolution du destinataire. Pour plus d'informations sur les messages différés, consultez la rubrique <a href="recipient-resolution-exchange-2013-help.md">Résolution des destinataires</a>.</p></td>
</tr>
<tr class="even">
<td><p><strong>Type de remise</strong></p></td>
<td><p><code>DeliveryType</code></p></td>
<td><p>Les valeurs valides pour le paramètre <strong>DeliveryType</strong> sont énoncées dans la section « NextHopSolutionKey » de la rubrique <a href="queues-exchange-2013-help.md">Files d'attente</a>.</p></td>
</tr>
<tr class="odd">
<td><p>s/o</p></td>
<td><p><code>Identity</code></p></td>
<td><p>Cette propriété est l'identité de la file d'attente sous la forme <em>&lt;serveur&gt;\&lt;file_attente&gt;</em>. Pour plus d'informations, consultez la section « Identité de file d'attente » de la rubrique <a href="queues-exchange-2013-help.md">Files d'attente</a>.</p></td>
</tr>
<tr class="even">
<td><p>s/o</p></td>
<td><p><code>IncomingRate</code></p></td>
<td><p>Cette propriété est un nombre calculé indiquant la vitesse à laquelle les messages entrent dans la file d'attente. Pour plus d'informations, consultez la section « IncomingRate, OutgoingRate et Velocity » de la rubrique <a href="queues-exchange-2013-help.md">Files d'attente</a>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Dernière erreur</strong></p></td>
<td><p><code>LastError</code></p></td>
<td><p>Cette valeur spécifie la chaîne de texte de la dernière erreur enregistrée pour la file d'attente.</p></td>
</tr>
<tr class="even">
<td><p><strong>Date de la dernière tentative</strong></p></td>
<td><p><code>LastRetryTime</code></p></td>
<td><p>Cette propriété spécifie les date et l'heure de la dernière tentative de connexion pour une file d'attente dont l'état est <code>Retry</code>.</p></td>
</tr>
<tr class="odd">
<td><p>s/o</p></td>
<td><p><code>LockedMessageCount</code></p></td>
<td><p>Cette propriété est réservée à un usage interne chez Microsoft, et n'est pas utilisée dans les organisations Exchange 2013 locales.</p></td>
</tr>
<tr class="even">
<td><p><strong>Nombre de messages</strong></p></td>
<td><p><code>MessageCount</code></p></td>
<td><p>Cette propriété Indique le nombre de messages dans la file d'attente.</p></td>
</tr>
<tr class="odd">
<td><p>s/o</p></td>
<td><p><code>NextHopCategory</code></p></td>
<td><p>Cette propriété indiquant le saut suivant de la file d'attente comme <code>Internal</code> ou <code>External</code> est basée sur la valeur de la propriété <strong>DeliveryType</strong> de la file d'attente. Pour plus d'informations, consultez la section « NextHopSolutionKey » de la rubrique <a href="queues-exchange-2013-help.md">Files d'attente</a>.</p></td>
</tr>
<tr class="even">
<td><p>s/o</p></td>
<td><p><code>NextHopConnector</code></p></td>
<td><p>Cette propriété indiquant le GUID du saut suivant est basée sur la valeur de la propriété <strong>DeliveryType</strong> de la file d'attente. Pour plus d'informations, consultez la section « NextHopSolutionKey » de la rubrique <a href="queues-exchange-2013-help.md">Files d'attente</a>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Domaine de saut suivant</strong></p></td>
<td><p><code>NextHopDomain</code></p></td>
<td><p>Cette propriété indiquant le nom du saut suivant est basée sur la valeur de la propriété <strong>DeliveryType</strong> de la file d'attente. Pour plus d'informations, consultez la section « NextHopSolutionKey » de la rubrique <a href="queues-exchange-2013-help.md">Files d'attente</a>.</p></td>
</tr>
<tr class="even">
<td><p><strong>Date de la prochaine tentative</strong></p></td>
<td><p><code>NextRetryTime</code></p></td>
<td><p>Cette propriété spécifie les date et l'heure de la prochaine tentative de connexion pour une file d'attente dont l'état est <code>Retry</code>.</p></td>
</tr>
<tr class="odd">
<td><p>s/o</p></td>
<td><p><code>OutgoingRate</code></p></td>
<td><p>Cette propriété est un nombre calculé indiquant la vitesse à laquelle les messages quittent la file d'attente. Pour plus d'informations, consultez la section « IncomingRate, OutgoingRate et Velocity » de la rubrique <a href="queues-exchange-2013-help.md">Files d'attente</a>.</p></td>
</tr>
<tr class="even">
<td><p>s/o</p></td>
<td><p><code>RiskLevel</code></p></td>
<td><p>Cette propriété est réservée à un usage interne chez Microsoft, et n'est pas utilisée dans les organisations Exchange 2013 locales.</p></td>
</tr>
<tr class="odd">
<td><p><strong>État</strong></p></td>
<td><p><code>Status</code></p></td>
<td><p>Cette propriété indique l'état actuel de la file d'attente. Une file d'attente peut avoir l'un des états suivants : Actif, Connexion, Aucun, Suspendu, Prêt ou Nouvelle tentative. Pour plus d'informations, consultez la section « État de file d'attente » de la rubrique <a href="queues-exchange-2013-help.md">Files d'attente</a>.</p></td>
</tr>
<tr class="even">
<td><p>s/o</p></td>
<td><p><code>TlsDomain</code></p></td>
<td><p>Cette propriété contient le nom de domaine complet (FQDN) du domaine de destination si ce dernier est configuré pour la sécurité du domaine.</p></td>
</tr>
<tr class="odd">
<td><p>s/o</p></td>
<td><p><code>Velocity</code></p></td>
<td><p>Cette propriété contient un nombre calculé indiquant l'efficacité du drainage de la file d'attente. Pour plus d'informations, consultez la section « IncomingRate, OutgoingRate et Velocity » de la rubrique <a href="queues-exchange-2013-help.md">Files d'attente</a>.</p></td>
</tr>
</tbody>
</table>

