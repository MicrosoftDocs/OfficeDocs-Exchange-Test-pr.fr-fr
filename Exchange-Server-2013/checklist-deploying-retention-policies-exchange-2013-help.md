---
title: 'Liste de contrôle : Déploiement de stratégies de rétention: Exchange 2013 Help'
TOCTitle: 'Liste de contrôle : Déploiement de stratégies de rétention'
ms:assetid: 59e299fd-b6a8-48f5-88ae-dc20dbe32e90
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Ee364743(v=EXCHG.150)
ms:contentKeyID: 50478259
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Liste de contrôle : Déploiement de stratégies de rétention

 

_**Sapplique à :** Exchange Online, Exchange Server 2013_

_**Dernière rubrique modifiée :** 2016-12-09_

Utilisez cette liste de vérification pour déployer des stratégies de rétention dans votre organisation Microsoft Exchange Server 2013. Avant de commencer avec cette liste de vérification, assurez-vous d’avoir bien assimilé les concepts présentés dans les rubriques suivantes :

  - [Gestion des enregistrements de messagerie](messaging-records-management-exchange-2013-help.md)

  - [Balises et stratégies de rétention](retention-tags-and-retention-policies-exchange-2013-help.md)

## Liste de vérification pour le déploiement de stratégies de rétention


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Terminé ?</th>
<th>Tâches</th>
<th>Ressources</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p> </p></td>
<td><p>Évaluer les exigences relatives à la gestion des enregistrements de messagerie (MRM) pour différents groupes d’utilisateurs.</p></td>
<td><p><a href="messaging-records-management-exchange-2013-help.md">Gestion des enregistrements de messagerie</a></p></td>
</tr>
<tr class="even">
<td><p><strong> </strong></p></td>
<td><p>Déterminer quelles versions du client Microsoft Outlook sont utilisées.</p></td>
<td><p>Analyser les fichiers journaux d’accès au client RPC dans <code>%ExchangeInstallPath%Logging\RPC Client Access</code>.</p></td>
</tr>
<tr class="odd">
<td><p> </p></td>
<td><p>Créer des balises de rétention.</p></td>
<td><p><a href="create-a-retention-policy-exchange-2013-help.md">Créer une stratégie de rétention</a></p></td>
</tr>
<tr class="even">
<td><p><strong> </strong></p></td>
<td><p>Créer des stratégies de rétention.</p></td>
<td><p><a href="create-a-retention-policy-exchange-2013-help.md">Créer une stratégie de rétention</a></p></td>
</tr>
<tr class="odd">
<td><p> </p></td>
<td><p>Ajouter des balises de rétention aux stratégies de rétention.</p></td>
<td><p><a href="add-retention-tags-to-or-remove-retention-tags-from-a-retention-policy-exchange-2013-help.md">Ajouter ou supprimer des balises de rétention à partir d’une stratégie de rétention</a></p></td>
</tr>
<tr class="even">
<td><p><strong> </strong></p></td>
<td><p>Activer le blocage de rétention des boîtes aux lettres.</p></td>
<td><p><a href="place-a-mailbox-on-retention-hold-exchange-2013-help.md">Placer une boîte aux lettres en blocage de rétention</a></p></td>
</tr>
<tr class="odd">
<td><p> </p></td>
<td><p>Appliquer une stratégie de rétention à une seule boîte aux lettres aux fins de test.</p></td>
<td><p><a href="apply-a-retention-policy-to-mailboxes-exchange-2013-help.md">Appliquer une stratégie de rétention aux boîtes aux lettres</a></p></td>
</tr>
<tr class="even">
<td><p><strong> </strong></p></td>
<td><p>Facultatif : Implémenter le blocage du client pour bloquer les clients hérités de Outlook.</p></td>
<td><p><a href="configure-outlook-client-blocking-exchange-2013-help.md">Configurez le blocage de clients Outlook pour la gestion des enregistrements de messagerie</a></p></td>
</tr>
<tr class="odd">
<td><p> </p></td>
<td><p>Commencer la communication auprès des utilisateurs et les activités de formation. Inclure une date d’échéance du traitement des stratégies de rétention et de déplacement ou suppression des éléments.</p></td>
<td><p>Non applicable</p></td>
</tr>
<tr class="even">
<td><p><strong> </strong></p></td>
<td><p>Appliquer la stratégie de rétention aux boîtes aux lettres supplémentaires.</p></td>
<td><p><a href="apply-a-retention-policy-to-mailboxes-exchange-2013-help.md">Appliquer une stratégie de rétention aux boîtes aux lettres</a></p></td>
</tr>
<tr class="odd">
<td><p> </p></td>
<td><p>Quelques jours avant, rappeler aux utilisateurs la date d’échéance.</p></td>
<td><p>Non applicable</p></td>
</tr>
<tr class="even">
<td><p><strong> </strong></p></td>
<td><p>À la date d’échéance, désactiver le blocage de rétention des boîtes aux lettres.</p></td>
<td><p><a href="place-a-mailbox-on-retention-hold-exchange-2013-help.md">Placer une boîte aux lettres en blocage de rétention</a></p></td>
</tr>
</tbody>
</table>

