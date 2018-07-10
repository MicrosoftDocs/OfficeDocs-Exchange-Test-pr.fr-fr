---
title: 'Méthode de calcul de l’âge de rétention: Exchange 2013 Help'
TOCTitle: Méthode de calcul de l’âge de rétention
ms:assetid: a7daf7aa-0411-4b26-a422-eefd1b113f9f
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb430780(v=EXCHG.150)
ms:contentKeyID: 50478958
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Méthode de calcul de l’âge de rétention

 

_**Sapplique à :** Exchange Online, Exchange Server 2013_

_**Dernière rubrique modifiée :** 2016-07-27_

L’Assistant Dossier géré est l’un des nombreux processus d’*Assistant de boîte aux lettres* exécuté sur des serveurs de boîtes aux lettres. Sa tâche consiste à traiter les boîtes aux lettres dotées d’une stratégie de rétention, à ajouter des balises de rétention incluses dans la stratégie à la boîte aux lettres et à traiter les éléments de la boîte aux lettres. Si les éléments disposent d’une balise de rétention, l’Assistant vérifie l’âge de ces éléments. Si un élément a dépassé son *âge de rétention*, il prend l’*action de rétention* indiquée. Les actions de rétention comprennent le déplacement d’un élément vers l’archive de l’utilisateur, la suppression de l’élément et sa récupération, ou la suppression définitive de l’élément.

Pour plus d’informations, consultez la rubrique [Balises et stratégies de rétention](retention-tags-and-retention-policies-exchange-2013-help.md).

## Détermination de l’âge des différents types d’éléments

La période de rétention d’éléments de boîte aux lettres est calculée à partir de la date de remise ou, dans le cas de brouillons qui ne sont pas remis mais créés par l’utilisateur, de la date de création d’un élément. Quand l’Assistant Dossier géré traite les éléments d’une boîte aux lettres, il appose une date de début et une date d’expiration pour tous les éléments présentant des balises de rétention avec l’action de rétention **Supprimer et autoriser la récupération** ou **Supprimer définitivement**. Une date de déplacement est aussi apposée sur les éléments possédant une balise de rétention.

Les éléments contenus dans le dossier Éléments supprimés et ceux comportant une date de début et de fin, tels que des éléments de calendrier (réunions et rendez-vous) et des tâches, sont traités différemment, comme indiqué dans ce tableau.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Si le type d’élément est...</th>
<th>Et si l’élément est...</th>
<th>L’âge de rétention est calculé en fonction de...</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><ul>
<li><p>Message électronique</p></li>
<li><p>Document</p></li>
<li><p>Télécopie</p></li>
<li><p>Élément Journal</p></li>
<li><p>Demande de réunion, réponse ou annulation</p></li>
<li><p>Appel manqué</p></li>
</ul></td>
<td><p>Pas dans le dossier Éléments supprimés</p></td>
<td><p>Date de remise ou date de création</p></td>
</tr>
<tr class="even">
<td><ul>
<li><p>Message électronique</p></li>
<li><p>Document</p></li>
<li><p>Télécopie</p></li>
<li><p>Élément Journal</p></li>
<li><p>Demande de réunion, réponse ou annulation</p></li>
<li><p>Appel manqué</p></li>
</ul></td>
<td><p>Dans le dossier Éléments supprimés.</p></td>
<td><ul>
<li><p>Date de remise ou de création, sauf si l’objet a été supprimé d’un dossier qui ne comporte pas de balise de rétention héritée ou implicite.</p></li>
<li><p>Si un élément se trouve dans un dossier auquel aucune balise de rétention héritée ou implicite n’est appliquée, l’élément n’est pas traité par l’Assistant Dossier géré et, par conséquent, ce dernier ne lui attribue aucune date de début. Lorsque l’utilisateur supprime un tel élément et que l’Assistant Dossier géré le traite pour la première fois dans le dossier Éléments supprimés, il appose la date du jour comme date de début.</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Calendrier</p></td>
<td><p>Pas dans le dossier Éléments supprimés</p></td>
<td><ul>
<li><p>Les éléments de calendrier non périodiques expirent en fonction de leur date de fin.</p></li>
<li><p>Les éléments de calendrier périodiques expirent en fonction de la date de fin de leur dernière occurrence. Les éléments de calendrier périodiques sans date de fin n’expirent pas.</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Calendrier</p></td>
<td><p>Dans le dossier Éléments supprimés.</p></td>
<td><ol>
<li><p>Un élément de calendrier expire en fonction de sa <code>message-received date</code>, si elle existe.</p></li>
<li><p>Si un élément de calendrier ne possède pas de <code>message-received date</code>, il expire en fonction de sa <code>message-creation date</code>.</p></li>
<li><p>Si un élément de calendrier ne possède pas de <code>message-received date</code>, ni de <code>message-creation date</code>, il n’expire pas.</p></li>
</ol></td>
</tr>
<tr class="odd">
<td><p>Tâche</p></td>
<td><p>Pas dans le dossier Éléments supprimés</p></td>
<td><ul>
<li><p>Tâches non périodiques :</p>
<ol>
<li><p>Une tâche non périodique expire en fonction de sa <code>message-received date</code>, si elle existe.</p></li>
<li><p>Si une tâche non périodique ne possède pas de <code>message-received date</code>, elle expire en fonction de sa <code>message-creation date</code>.</p></li>
<li><p>Si une tâche non périodique ne possède ni <code>message-received date</code> ni <code></code><code>message-creation date</code>, elle n’expire pas.</p></li>
</ol></li>
<li><p>Une tâche périodique expire en fonction de la <code>end date</code> de sa dernière occurrence. Si une tâche périodique ne possède pas de <code>end date</code>, elle n’expire pas.</p></li>
<li><p>Une tâche de régénération (c’est-à-dire une tâche périodique qui se régénère un certain temps après l’achèvement de l’instance précédente) n’expire pas.</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Tâche</p></td>
<td><p>Dans le dossier Éléments supprimés.</p></td>
<td><ol>
<li><p>Une tâche expire en fonction de sa <code>message-received date</code>, si elle existe.</p></li>
<li><p>Si une tâche ne possède pas de <code>message-received date</code>, elle expire en fonction de sa <code>message-creation date</code>.</p></li>
<li><p>Si une tâche ne possède pas de <code>message-received date</code>, ni de <code>message-creation date</code>, elle n’expire pas.</p></li>
</ol></td>
</tr>
<tr class="odd">
<td><p>Contact</p></td>
<td><p>Dans n’importe quel dossier</p></td>
<td><p>Les contacts ne sont pas marqués avec une date de début ou une date d’expiration, c’est pourquoi ils sont ignorés par l’Assistant Dossier géré et n’expirent pas.</p></td>
</tr>
<tr class="even">
<td><p>Endommagé</p></td>
<td><p>Dans n’importe quel dossier</p></td>
<td><p>Les éléments endommagés sont ignorés par l’Assistant Dossier géré et n’expirent pas.</p></td>
</tr>
</tbody>
</table>


## Exemples


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Si l’utilisateur...</th>
<th>Les balises de rétention sur le dossier...</th>
<th>L’Assistant Dossier géré...</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><ol>
<li><p>Reçoit un message dans la boîte de réception le 26/01/2013.</p></li>
<li><p>Supprime le message le 27/02/2013.</p></li>
</ol>
<p></p></td>
<td><ul>
<li><p>Boîte de réception : Supprimer dans 365 jours</p></li>
<li><p>Éléments supprimés : Supprimer dans 30 jours</p></li>
</ul>
<p></p></td>
<td><ol>
<li><p>Traite le message dans la boîte de réception le 26/01/2013, indique sa <em>date de début</em> (le 26/01/2013) et sa <em>date d’expiration</em> (le 26/01/2014).</p></li>
<li><p>Traite à nouveau le message dans le dossier Éléments supprimés le 27/02/2013. Il recalcule la date d’expiration en fonction de la même date de début (26/01/2013).</p></li>
<li><p>Comme l’élément a plus de 30 jours, il expire immédiatement.</p></li>
</ol></td>
</tr>
<tr class="even">
<td><ol>
<li><p>Reçoit un message dans la boîte de réception le 26/01/2013.</p></li>
<li><p>Supprime le message le 27/02/2013.</p></li>
</ol></td>
<td><ul>
<li><p>Boîte de réception : Aucune (héritée ou implicite)</p></li>
<li><p>Éléments supprimés : Supprimer dans 30 jours</p></li>
</ul></td>
<td><ol>
<li><p>Traite le message dans le dossier Éléments supprimés le 27/02/2013 et détermine que l’élément n’a pas de date de début. Il appose la date actuelle comme date de début, et le 27/03/13 comme date d’expiration.</p></li>
<li><p>L’élément expire le 27/03/13, soit 30 jours après sa suppression ou son déplacement dans le dossier Éléments supprimés par l’utilisateur.</p></li>
</ol></td>
</tr>
</tbody>
</table>


## Plus d’informations

  - Dans Exchange Online, l’Assistant Dossier géré traite une boîte aux lettres une fois tous les sept jours. Cela peut entraîner l’expiration d’éléments jusqu’à 7 jours suivant la date d’expiration indiquée sur l’élément.

  - Les éléments de boîtes aux lettres placées en blocage de rétention ne sont traités par l’Assistant Dossier géré qu’une fois le blocage de rétention enlevé.

  - Si les fonctionnalités Conservation inaltérable ou Conservation pour litige sont activées sur des boîtes aux lettres, les éléments qui expirent sont supprimés de la boîte de réception, mais conservés dans le dossier Éléments supprimés jusqu’à ce que la [Conservation inaltérable et conservation pour litige](in-place-hold-and-litigation-hold-exchange-2013-help.md) soit supprimée de la boîte aux lettres.

  - Dans les déploiements hybrides, les mêmes balises et stratégies de rétention doivent exister dans vos organisations sur site et Exchange Online afin de déplacer et de faire expirer de façon cohérente des éléments dans les deux organisations. Pour plus d’informations, consultez la rubrique [Exportation et importation de balises de rétention](export-and-import-retention-tags-exchange-2013-help.md).

