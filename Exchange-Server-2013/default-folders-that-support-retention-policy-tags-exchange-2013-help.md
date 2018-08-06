---
title: 'Dossiers p. déf. prenant en charge balises strat. rétention: Exchange 2013 Help| Microsoft Docs'
TOCTitle: Dossiers par défaut prenant en charge les balises de stratégie de rétention
ms:assetid: d2e2064f-4102-4018-b688-504d09da6d39
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dn783294(v=EXCHG.150)
ms:contentKeyID: 62835953
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Dossiers par défaut prenant en charge les balises de stratégie de rétention

 

_**Sapplique à :** Exchange Online, Exchange Server 2013_

_**Dernière rubrique modifiée :** 2017-04-20_

Vous pouvez utiliser des [Balises et stratégies de rétention](retention-tags-and-retention-policies-exchange-2013-help.md) pour gérer le cycle de vie des messages électroniques. Les stratégies de rétention contiennent des balises de rétention, qui sont des paramètres que vous pouvez utiliser pour spécifier quand un message doit automatiquement être déplacé vers l’archive ou quand il doit être supprimé.

Une balise de stratégie de rétention (RPT) est un type de balise de rétention que vous pouvez appliquer aux dossiers par défaut dans une boîte aux lettres, comme **Boîte de réception** et **Éléments supprimés**.

![Créer une balise de stratégie de rétention (RPT)](images/Dn783294.b59a96fd-94e1-4c9b-bff6-97a1bd98dfe7(EXCHG.150).png "Créer une balise de stratégie de rétention (RPT)")

## Dossiers par défaut pris en charge

Vous pouvez créer des balises de stratégie de rétention pour les dossiers par défaut indiqués dans le tableau suivant.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Nom du dossier</th>
<th>Détails</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Archive</p></td>
<td><p>Ce dossier est la destination par défaut des messages archivés à l’aide du bouton Archiver d’Outlook. La fonctionnalité d’archivage fournit aux utilisateurs un moyen rapide de retirer des messages de leur boîte de réception sans les supprimer.</p>
<p>Cette balise RPT est uniquement disponible dans Exchange Online.</p></td>
</tr>
<tr class="even">
<td><p>Calendrier</p></td>
<td><p>Ce dossier par défaut est utilisé pour stocker des réunions et des rendez-vous.</p></td>
</tr>
<tr class="odd">
<td><p>Courrier non trié</p></td>
<td><p>Ce dossier contient les messages électroniques qui sont de faible priorité. Il examine ce que vous avez fait dans le passé pour déterminer les messages que vous êtes le plus susceptible d’ignorer. Il déplace ensuite ces messages vers le dossier <strong>Courrier non trié</strong>.</p></td>
</tr>
<tr class="even">
<td><p>Historique des conversations</p></td>
<td><p>Ce dossier est créé par Microsoft Lync (auparavant Microsoft Office Communicator). Bien qu’il ne soit pas traité comme un dossier par défaut dans Outlook, il est considéré comme un dossier spécial par Exchange et des balises de stratégie de rétention peuvent lui être appliquées.</p></td>
</tr>
<tr class="odd">
<td><p>Éléments supprimés</p></td>
<td><p>Ce dossier par défaut est utilisé pour stocker des éléments supprimés d’autres dossiers de la boîte aux lettres. Les utilisateurs d’Outlook et d’Outlook Web App peuvent vider manuellement ce dossier. Ils peuvent également configurer Outlook pour vider le dossier lors de la fermeture d’Outlook.</p></td>
</tr>
<tr class="even">
<td><p>Brouillons</p></td>
<td><p>Ce dossier par défaut sert à stocker les messages brouillons qui n’ont pas été envoyés par l’utilisateur. Outlook Web App utilise également ce dossier pour enregistrer les messages qui ont été envoyés par l’utilisateur, mais qui n’ont pas été soumis au serveur de transport Hub.</p></td>
</tr>
<tr class="odd">
<td><p>Boîte de réception</p></td>
<td><p>Ce dossier par défaut est utilisé pour stocker les messages envoyés à une boîte aux lettres.</p></td>
</tr>
<tr class="even">
<td><p>Journal</p></td>
<td><p>Ce dossier par défaut contient les actions sélectionnées par l’utilisateur. Ces actions sont automatiquement enregistrées par Outlook et placées dans une vue chronologique.</p></td>
</tr>
<tr class="odd">
<td><p>Courrier indésirable</p></td>
<td><p>Ce dossier par défaut sert à enregistrer les messages marqués comme indésirables par le filtre de contenu sur un serveur Exchange ou par le filtre de blocage du courrier indésirable dans Outlook.</p></td>
</tr>
<tr class="even">
<td><p>Notes</p></td>
<td><p>Ce dossier contient les notes créées par les utilisateurs dans Outlook. Ces notes sont également visibles dans Outlook Web App.</p></td>
</tr>
<tr class="odd">
<td><p>Boîte d’envoi</p></td>
<td><p>Ce dossier par défaut est utilisé pour stocker temporairement les messages envoyés par l’utilisateur jusqu’à ce qu’ils soient envoyés à un serveur de transport Hub. Une copie des messages envoyés est enregistrée dans le dossier par défaut Éléments envoyés. Il n’est pas nécessaire de créer une balise de stratégie de rétention pour ce dossier parce que les messages sont généralement conservés peu de temps dans ce dossier.</p></td>
</tr>
<tr class="even">
<td><p>Flux RSS</p></td>
<td><p>Ce dossier par défaut contient des flux RSS.</p></td>
</tr>
<tr class="odd">
<td><p>Éléments récupérables</p></td>
<td><p>Il s’agit d’un dossier caché du dossier de la sous-arborescence non-IPM. Il comprend les sous-dossiers Suppressions, Versions, Purges, DiscoveryHolds et Audits. Les balises de rétention de ce dossier déplacent les éléments du dossier Éléments récupérables de la boîte aux lettres principale de l’utilisateur vers son dossier Éléments récupérables de la boîte aux lettres d’archivage. Vous pouvez ajouter l’action <strong>Déplacer vers l’archive</strong> uniquement aux balises de ce dossier. Pour en savoir plus, consultez la rubrique <a href="recoverable-items-folder-exchange-2013-help.md">Dossier Éléments récupérables</a>.</p></td>
</tr>
<tr class="even">
<td><p>Éléments envoyés</p></td>
<td><p>Ce dossier par défaut permet de stocker des messages qui ont été envoyés à un serveur de transport Hub.</p></td>
</tr>
<tr class="odd">
<td><p>Problèmes de synchronisation</p></td>
<td><p>Ce dossier contient des journaux de synchronisation. Pour en savoir plus, consultez la rubrique <a href="https://go.microsoft.com/fwlink/p/?linkid=198215">Dossiers d’erreur de synchronisation</a>.</p></td>
</tr>
<tr class="even">
<td><p>Tâches</p></td>
<td><p>Ce dossier par défaut est utilisé pour stocker des tâches. Pour créer une balise de stratégie de rétention pour le dossier Tâches, vous devez utiliser le Environnement de ligne de commande Exchange Management Shell. Pour plus d’informations, voir <a href="https://technet.microsoft.com/fr-fr/library/dd335226(v=exchg.150)">New-RetentionPolicyTag</a>. Une fois que la balise de stratégie de rétention est créée pour le dossier Tâches, vous pouvez la gérer à l’aide du Centre d’administration Exchange.</p></td>
</tr>
</tbody>
</table>


## Plus d’informations

  - Les balises de stratégie de rétention sont des balises de rétention pour les dossiers par défaut. Vous pouvez sélectionner uniquement une action de suppression pour les balises de stratégie de rétention, soit **supprimer et autoriser la récupération**, soit **supprimer définitivement**.

  - Vous ne pouvez pas créer une balise de stratégie de rétention pour déplacer des messages vers l’archive. Pour déplacer d’anciens éléments à archiver, vous pouvez créer une *balise de stratégie par défaut* (DPT), qui s’applique à l’ensemble de la boîte aux lettres, ou des *balises personnelles*, qui sont affichées dans Outlook et Outlook Web App (OWA) comme des stratégies d’archivage. Vos utilisateurs peuvent les appliquer à des dossiers ou des messages individuels.

  - Il n’est pas possible d’appliquer des balises de stratégie de rétention au dossier Contacts.

  - Vous ne pouvez ajouter qu’une balise de stratégie de rétention pour un dossier par défaut particulier à une stratégie de rétention. Par exemple, si une stratégie de rétention comporte une balise pour Boîte de réception, vous ne pouvez pas ajouter une autre balise de stratégie de rétention de type Boîte de réception à cette stratégie de rétention.

  - Pour découvrir comment créer des balises de stratégie de rétention ou d’autres types de balises de rétention et les ajouter à une stratégie de rétention, consultez la rubrique [Créer une stratégie de rétention](create-a-retention-policy-exchange-2013-help.md).

  - Dans Exchange 2013 et Exchange Online, une balise de stratégie par défaut est également appliquée aux dossiers par défaut **Calendrier** et **Tâches**. Cela peut entraîner la suppression ou le déplacement d’éléments vers l’archive locale, selon les paramètres des balises de stratégie par défaut. Pour empêcher que les paramètres des balises de stratégie par défaut n’entraînent la suppression d’éléments de ces dossiers, créez des balises de stratégie de rétention en désactivant les paramètres de rétention. Pour éviter que les paramètres des balises de stratégie par défaut n’entraînent le déplacement d’éléments dans un dossier par défaut, vous pouvez créer une balise personnelle désactivée avec l’action Déplacer vers l’archive, l’ajouter à la stratégie de rétention et demander aux utilisateurs de l’appliquer au dossier par défaut. Pour plus de détails, consultez la rubrique [Empêcher l’archivage d’éléments dans un dossier par défaut dans Exchange 2010](https://go.microsoft.com/fwlink/?linkid=511071).

