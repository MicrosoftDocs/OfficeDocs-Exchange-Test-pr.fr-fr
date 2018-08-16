---
title: 'Stratégie de rétention par défaut dans Exchange Online et Exchange Server'
TOCTitle: Stratégie de rétention par défaut
ms:assetid: bcf31b2d-463b-4623-b488-c8ac40f14f62
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dn775046(v=EXCHG.150)
ms:contentKeyID: 62625971
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Stratégie de rétention par défaut dans Exchange Online et Exchange Server

 

_**Sapplique à :** Exchange Online, Exchange Server 2013_

_**Dernière rubrique modifiée :** 2015-03-09_

Exchange crée la stratégie de rétention appelée stratégie MRM par défaut dans votre organisation Exchange Online et dans votre organisation Exchange locale. La stratégie est appliquée automatiquement aux nouveaux utilisateurs dans Exchange Online. Dans les organisations locales, la stratégie est appliquée lorsque vous créez une archive pour la boîte aux lettres. Vous pouvez modifier la stratégie de rétention appliquée à un utilisateur à tout moment.

Vous pouvez modifier les balises incluses dans la stratégie MRM par défaut (par exemple, en modifiant l’âge ou les actions de rétention), désactiver une balise ou modifier la stratégie en ajoutant ou en supprimant des balises. La stratégie mise à jour est appliquée aux boîtes aux lettres lors du prochain traitement de ces dernières par l’Assistant Dossier géré.

## Balises de rétention liées à la stratégie MRM par défaut

Le tableau suivant dresse la liste des balises de rétention par défaut associées à la stratégie MRM par défaut.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Nom</th>
<th>Type</th>
<th>Âge de rétention (jours)</th>
<th>Action de rétention</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Déplacement vers l’archive après 2 ans - Par défaut</p></td>
<td><p>Balise de stratégie par défaut (DPT)</p></td>
<td><p>730</p></td>
<td><p>Déplacer vers l’archive</p></td>
</tr>
<tr class="even">
<td><p>Déplacement vers l’archive après 14 jours - Éléments récupérables</p></td>
<td><p>Dossier Éléments récupérables</p></td>
<td><p>14</p></td>
<td><p>Déplacer vers l’archive</p></td>
</tr>
<tr class="odd">
<td><p>Déplacement vers l’archive après 1 an - Personnel</p></td>
<td><p>Balise personnelle</p></td>
<td><p>365</p></td>
<td><p>Déplacer vers l’archive</p></td>
</tr>
<tr class="even">
<td><p>Déplacement vers l’archive après 5 ans - Personnel</p></td>
<td><p>Balise personnelle</p></td>
<td><p>1 825</p></td>
<td><p>Déplacer vers l’archive</p></td>
</tr>
<tr class="odd">
<td><p>Ne jamais déplacer vers l’archive - Personnel</p></td>
<td><p>Balise personnelle</p></td>
<td><p>Non applicable</p></td>
<td><p>Déplacer vers l’archive</p></td>
</tr>
<tr class="even">
<td><p>Suppression après 1 semaine</p></td>
<td><p>Balise personnelle</p></td>
<td><p>7</p></td>
<td><p>Supprimer et autoriser la récupération</p></td>
</tr>
<tr class="odd">
<td><p>Suppression après 1 mois</p></td>
<td><p>Balise personnelle</p></td>
<td><p>30</p></td>
<td><p>Supprimer et autoriser la récupération</p></td>
</tr>
<tr class="even">
<td><p>Suppression après 6 mois</p></td>
<td><p>Balise personnelle</p></td>
<td><p>180</p></td>
<td><p>Supprimer et autoriser la récupération</p></td>
</tr>
<tr class="odd">
<td><p>Suppression après 1 an</p></td>
<td><p>Balise personnelle</p></td>
<td><p>365</p></td>
<td><p>Supprimer et autoriser la récupération</p></td>
</tr>
<tr class="even">
<td><p>Suppression après 5 ans</p></td>
<td><p>Balise personnelle</p></td>
<td><p>1 825</p></td>
<td><p>Supprimer et autoriser la récupération</p></td>
</tr>
<tr class="odd">
<td><p>Ne jamais supprimer</p></td>
<td><p>Balise personnelle</p></td>
<td><p>Non applicable</p></td>
<td><p>Supprimer et autoriser la récupération</p></td>
</tr>
</tbody>
</table>


## Ce que vous pouvez faire avec la stratégie MRM par défaut


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Vous pouvez...</th>
<th>Dans Exchange Online...</th>
<th>Dans Exchange Server...</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Appliquer automatiquement la stratégie MRM par défaut aux nouveaux utilisateurs</p></td>
<td><p>Oui, appliquée par défaut. Aucune action n’est requise.</p></td>
<td><p>Oui, appliquée par défaut si vous créez également une archive pour le nouvel utilisateur.</p>
<p>Si vous créez une archive pour l’utilisateur ultérieurement, la stratégie n’est appliquée automatiquement que si l’utilisateur ne dispose pas d’une stratégie de rétention existante.</p></td>
</tr>
<tr class="even">
<td><p>Modifier l’âge de rétention ou l’action de rétention d’une balise de rétention liée à la stratégie</p></td>
<td><p>Oui</p></td>
<td><p>Oui</p></td>
</tr>
<tr class="odd">
<td><p>Désactiver une balise de rétention liée à la stratégie</p></td>
<td><p>Oui</p></td>
<td><p>Oui</p></td>
</tr>
<tr class="even">
<td><p>Ajouter une balise de rétention à la stratégie</p></td>
<td><p>Oui</p></td>
<td><p>Oui</p></td>
</tr>
<tr class="odd">
<td><p>Supprimer une balise de rétention de la stratégie</p></td>
<td><p>Oui</p></td>
<td><p>Oui</p></td>
</tr>
<tr class="even">
<td><p>Définir une autre stratégie en tant que stratégie de rétention par défaut à appliquer automatiquement aux nouveaux utilisateurs</p></td>
<td><p>Non</p></td>
<td><p>Non</p></td>
</tr>
</tbody>
</table>


## Plus d’informations

  - Une balise de rétention peut être liée à plus d’une stratégie de rétention. Pour plus d’informations sur la gestion de [Balises et stratégies de rétention](retention-tags-and-retention-policies-exchange-2013-help.md), voir [Procédures de gestion des enregistrements de messagerie](messaging-records-management-procedures-exchange-2013-help.md).

  - La stratégie MRM par défaut n’inclut pas de balise pour supprimer automatiquement des éléments (mais elle contient des balises personnelles avec l’action de rétention Supprimer que les utilisateurs peuvent appliquer aux éléments de boîte aux lettres). Si vous souhaitez supprimer automatiquement des éléments après une période spécifiée, vous pouvez créer une balise de stratégie par défaut (DPT) avec l’action de suppression requise et l’ajouter à la stratégie. Pour plus de détails, voir [Créer une stratégie de rétention](create-a-retention-policy-exchange-2013-help.md) et [Ajouter ou supprimer des balises de rétention à partir d’une stratégie de rétention](add-retention-tags-to-or-remove-retention-tags-from-a-retention-policy-exchange-2013-help.md).

  - Des stratégies de rétention sont appliquées aux utilisateurs de boîte aux lettres. La même stratégie s’applique à la boîte aux lettres et à l’archive de l’utilisateur.

