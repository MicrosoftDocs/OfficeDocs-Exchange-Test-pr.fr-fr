---
title: 'Compteurs de performance pr gérer les enregist. de messag.: Exchange 2013 Help'
TOCTitle: Compteurs de performance pour la gestion des enregistrements de messagerie
ms:assetid: b59def6f-4249-4e0c-8057-8ae6eb7c5676
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb310790(v=EXCHG.150)
ms:contentKeyID: 51407216
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Compteurs de performance pour la gestion des enregistrements de messagerie

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2015-03-09_

Les compteurs de performances de cette rubrique contrôlent l'Assistant Dossier géré quand il implémente la gestion des enregistrements de messagerie (MRM) pour Microsoft Exchange Server 2010. Étant donné que l'exécution de l'Assistant Dossier géré est un processus consommant une quantité importante de ressources, vous devez l'exécuter uniquement lorsque votre serveur peut tolérer la charge supplémentaire. Nous vous recommandons également de contrôler les performances lors de l'exécution de l'Assistant Dossier géré. En plus des compteurs de performances répertoriés dans cette rubrique, vous pouvez également demander à contrôler les compteurs de performances supplémentaires qui analysent des éléments tels que les performances de disque et l'utilisation de l'UC.

Pour plus d'informations sur la surveillance d'ordinateurs exécutant la fonctionnalité de gestion des enregistrements de messagerie, consultez la rubrique [Gestion des enregistrements de messagerie de la surveillance](monitoring-https://docs.microsoft.com/fr-fr/exchange/security-and-compliance/messaging-records-management/messaging-records-management).

## Compteurs de performance pour la gestion des enregistrements de messagerie

Le tableau suivant décrit les compteurs de performance utilisés pour la gestion des enregistrements de messagerie.

### Compteurs de performance, objets de performance et description

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Compteur de performance</th>
<th>Objet de performance</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Durée moyenne du traitement des boîtes aux lettres en secondes</p></td>
<td><p>Assistants MSExchange</p></td>
<td><p>Comptabilise la durée de traitement moyenne des boîtes aux lettres pour les assistants basés sur l’heure.</p></td>
</tr>
<tr class="even">
<td><p>Boîtes aux lettres traitées</p></td>
<td><p>Assistants MSExchange</p></td>
<td><p>Comptabilise le nombre de boîtes aux lettres traitées par des assistants basés sur l’heure depuis le démarrage du service.</p></td>
</tr>
<tr class="odd">
<td><p>Boîtes aux lettres traitées/s</p></td>
<td><p>Assistants MSExchange</p></td>
<td><p>Détermine la fréquence de traitement des boîtes aux lettres par des assistants basés sur l’heure par seconde.</p></td>
</tr>
<tr class="even">
<td><p>Éléments supprimés mais récupérables</p></td>
<td><p>Assistant Dossier géré MSExchange</p></td>
<td><p>Comptabilise le nombre d'éléments supprimés par l'Assistant Dossier géré depuis le début de l'intervalle de planification le plus récent (Les éléments sont encore récupérables via le dossier Éléments récupérables). Ce nombre inclut des éléments des boîtes aux lettres dont le traitement a été planifié durant l'intervalle de planification et de toutes les boîtes aux lettres dont vous avez spécifié le traitement. Ce compteur est remis à zéro au début de chaque intervalle de planification.</p></td>
</tr>
<tr class="odd">
<td><p>Éléments journalisés</p></td>
<td><p>Assistant Dossier géré MSExchange</p></td>
<td><p>Compte le nombre d'éléments répertoriés par l'Assistant Dossier géré depuis le début de l'intervalle de planification le plus récent. Le nombre inclut des éléments des boîtes aux lettres planifiés pour traitement au cours du cycle de travail actuel et des éléments des boîtes aux lettres spécifiés pour traitement. Ce compteur est remis à zéro au début de chaque cycle de travail.</p></td>
</tr>
<tr class="even">
<td><p>Éléments marqués comme périmés</p></td>
<td><p>Assistant Dossier géré MSExchange</p></td>
<td><p>Comptabilise le nombre d'éléments marqués comme périmés par l'Assistant Dossier géré depuis le début de l'intervalle de planification le plus récent. Le nombre inclut des éléments des boîtes aux lettres planifiés pour traitement au cours de l'intervalle de planification et des éléments des boîtes aux lettres spécifiés pour traitement. Ce compteur est remis à zéro au début de chaque intervalle de planification.</p></td>
</tr>
<tr class="odd">
<td><p>Éléments déplacés</p></td>
<td><p>Assistant Dossier géré MSExchange</p></td>
<td><p>Comptabilise le nombre d'éléments déplacés par l'Assistant Dossier géré depuis le début de l'intervalle de planification le plus récent. Le nombre inclut des éléments des boîtes aux lettres planifiés pour traitement au cours de l'intervalle de planification et des éléments des boîtes aux lettres spécifiés pour traitement. Ce compteur est remis à zéro au début de chaque intervalle de planification.</p></td>
</tr>
<tr class="even">
<td><p>Éléments supprimés définitivement</p></td>
<td><p>Assistant Dossier géré MSExchange</p></td>
<td><p>Comptabilise le nombre d'éléments supprimés définitivement par l'Assistant Dossier géré depuis le début de l'intervalle de planification le plus récent. Le nombre inclut des éléments des boîtes aux lettres planifiés pour traitement au cours de l'intervalle de planification et des éléments des boîtes aux lettres spécifiés pour traitement. Ce compteur est remis à zéro au début de chaque intervalle de planification.</p></td>
</tr>
<tr class="odd">
<td><p>Éléments soumis à une stratégie de rétention</p></td>
<td><p>Assistant Dossier géré MSExchange</p></td>
<td><p>Comptabilise le nombre d'éléments soumis à une stratégie de rétention par l'Assistant Dossier géré depuis le début de l'intervalle de planification le plus récent. Le nombre inclut des éléments des boîtes aux lettres planifiés pour traitement au cours de l'intervalle de planification et des éléments des boîtes aux lettres spécifiés pour traitement. Ce compteur est remis à zéro au début de chaque intervalle de planification. Ce compteur indique la somme des quatre compteurs suivants liés à l'expiration :</p>
<ul>
<li><p>Éléments journalisés</p></li>
<li><p>Éléments marqués comme périmés</p></li>
<li><p>Éléments déplacés</p></li>
<li><p>Éléments supprimés définitivement</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>TotalSizeItemsExpired - Taille des éléments soumis à la stratégie de rétention (en octets)</p></td>
<td><p>Assistant Dossier géré MSExchange</p></td>
<td><p>Indique la taille totale des éléments expirés par l'Assistant Dossier géré (SoftDelete, HardDelete, MoveToArchive).</p>
<p>Les éléments suivants sont inclus :</p>
<ul>
<li><p>Messages faisant l'objet d'une suppression ou d'un déplacement vers un dossier personnalisé géré par une stratégie de boîte aux lettres de dossier géré</p></li>
<li><p>Messages faisant l'objet d'une suppression ou d'un déplacement en archive par la stratégie de rétention de l'utilisateur</p></li>
<li><p>Messages expirés par stratégie de benne</p></li>
<li><p>Messages nettoyés par balise System Cleanup</p></li>
</ul>
<p>Ce compteur est remis à zéro à chaque point de contrôle du cycle de travail de l'Assistant Dossier géré.</p></td>
</tr>
<tr class="odd">
<td><p>TotalSizeItemsSoftDeleted - Taille des éléments supprimés mais récupérables (en octets)</p></td>
<td><p>Assistant Dossier géré MSExchange</p></td>
<td><p>Indique la taille totale des éléments supprimés (récupérables) par l'Assistant Dossier géré.</p>
<p>Les éléments suivants sont inclus :</p>
<ul>
<li><p>Messages supprimés (récupérables) par une stratégie de boîte aux lettres de dossier géré</p></li>
<li><p>Messages supprimés (récupérables) par une stratégie de rétention</p></li>
</ul>
<p>Ce compteur est remis à zéro à chaque point de contrôle du cycle de travail de l'Assistant Dossier géré.</p></td>
</tr>
<tr class="even">
<td><p>TotalSizeItemsPermanentlyDeleted - Taille des éléments supprimés définitivement (en octets)</p></td>
<td><p>Assistant Dossier géré MSExchange</p></td>
<td><p>Indique la taille totale des éléments supprimés (récupérables) par l'Assistant Dossier géré.</p>
<p>Les éléments suivants sont inclus :</p>
<ul>
<li><p>Messages supprimés (irrécupérables) par une stratégie de boîte aux lettres de dossier géré</p></li>
<li><p>Messages supprimés (irrécupérables) par une stratégie de rétention</p></li>
<li><p>Messages supprimés (irrécupérables) par la stratégie d'éléments récupérables</p></li>
</ul>
<p>Ce compteur est remis à zéro à chaque point de contrôle du cycle de travail de l'Assistant Dossier géré.</p></td>
</tr>
<tr class="odd">
<td><p>TotalSizeItemsMoved - Taille des éléments déplacés en raison d'une balise de stratégie d'archivage (en octets)</p></td>
<td><p>Assistant Dossier géré MSExchange</p></td>
<td><p>Indique la taille totale des éléments déplacés dans un dossier ou une archive par l'Assistant Dossier géré.</p>
<p>Les éléments suivants sont inclus :</p>
<ul>
<li><p>Messages déplacés dans un dossier personnalisé géré par une stratégie de boîte aux lettres de dossier géré</p></li>
<li><p>Messages déplacés vers l'archive personnelle par une stratégie de rétention</p></li>
</ul>
<p>Ce compteur est remis à zéro à chaque point de contrôle du cycle de travail de l'Assistant Dossier géré.</p></td>
</tr>
<tr class="even">
<td><p>TotalItemsWithPersonalTag - Éléments marqués avec la balise personnelle (Expiry ou Archive)</p></td>
<td><p>Assistant Dossier géré MSExchange</p></td>
<td><p>Indique le nombre de fois qu'un utilisateur marque des éléments avec une balise personnelle.</p>
<p>Cela comprend les balises de suppression et d'archivage.</p>
<p>Par exemple :</p>
<ul>
<li><p>Un élément est balisé avec une balise personnelle.</p></li>
<li><p>Un élément avec une balise personnelle est marqué avec une autre balise personnelle.</p></li>
</ul>
<p>Si un dossier est marqué avec une balise personnelle, le compteur est incrémenté du nombre total d'éléments dans le dossier.</p></td>
</tr>
<tr class="odd">
<td><p>TotalItemsWithDefaultTag - Éléments marqués avec la balise par défaut (Expiry ou Archive)</p></td>
<td><p>Assistant Dossier géré MSExchange</p></td>
<td><p>Indique le nombre d'éléments auxquels est attribuée une balise de stratégie par défaut en fonction d'une action de l'utilisateur, par exemple lors de la sélection d'un message avec une balise personnelle puis de l'option <strong>Utiliser la stratégie de dossier</strong>.</p>
<p>Si un nouvel utilisateur se voit attribuer une stratégie de rétention avec une balise de stratégie par défaut, le compteur est incrémenté du nombre d'éléments qui seront attribués par la balise de stratégie par défaut en fonction de la stratégie de rétention.</p>

> [!NOTE]
> Si un utilisateur dispose d'une stratégie de rétention avec une balise de stratégie par défaut, les nouveaux messages qui arrivent par le protocole de transport reçoivent une balise par défaut. Cette action n'est pas suivie par ce compteur.

</td>
</tr>
<tr class="even">
<td><p>TotalItemsWithSystemCleanupTag - Éléments marqués avec la balise System Cleanup</p></td>
<td><p>Assistant Dossier géré MSExchange</p></td>
<td><p>Indique le nombre d'éléments marqués avec la balise System Cleanup. Cela inclut les éléments de métadonnées de boîte aux lettres qui ne sont pas visibles pour les utilisateurs.</p></td>
</tr>
<tr class="odd">
<td><p>TotalItemsExpiredByDefaultExpiryTag - Éléments expirés à cause d'une balise Expiry par défaut</p></td>
<td><p>Assistant Dossier géré MSExchange</p></td>
<td><p>Indique le nombre d'éléments expirés (supprimés de manière récupérable ou irrécupérable) par l'Assistant Dossier géré en raison d'une balise non personnelle (par défaut ou système) dans une stratégie de rétention.</p>
<p>Cela n'inclut pas les éléments expirés par nettoyage du dossier Éléments récupérables ou du système.</p></td>
</tr>
<tr class="even">
<td><p>TotalItemsExpiredByPersonalExpiryTag - Éléments expirés à cause d'une balise Expiry personnelle</p></td>
<td><p>Assistant Dossier géré MSExchange</p></td>
<td><p>Indique le nombre d'éléments expirés (supprimés de manière récupérable ou irrécupérable) par l'Assistant Dossier géré en raison d'une balise personnelle dans la stratégie de rétention.</p></td>
</tr>
<tr class="odd">
<td><p>TotalItemsMovedByDefaultArchiveTag - Éléments déplacés à cause d'une balise Archive par défaut</p></td>
<td><p>Assistant Dossier géré MSExchange</p></td>
<td><p>Indique le nombre d'éléments déplacés en archive par l'Assistant Dossier géré en raison d'une balise Archive non personnelle (par défaut ou système) dans une stratégie de rétention.</p>
<p>Cela n'inclut pas les éléments déplacés dans le dossier Éléments récupérables en archive par le nettoyage des éléments récupérables.</p></td>
</tr>
<tr class="even">
<td><p>TotalItemsMovedByPersonalArchiveTag - Éléments déplacés à cause d'une balise Archive</p></td>
<td><p>Assistant Dossier géré MSExchange</p></td>
<td><p>Indique le nombre d'éléments déplacés en archive par l'Assistant Dossier géré en raison d'une balise Archive personnelle dans une stratégie de rétention.</p></td>
</tr>
<tr class="odd">
<td><p>TotalMovedDumpsterItems - Éléments déplacés des conteneurs de boîtes aux lettres</p></td>
<td><p>Assistant Dossier géré MSExchange</p></td>
<td><p>Indique le nombre d'éléments déplacés dans le dossier Éléments récupérables en archive par le nettoyage des éléments récupérables.</p></td>
</tr>
</tbody>
</table>

