---
title: 'Supprimer un groupement de postes de messagerie unifiée: Exchange 2013 Help'
TOCTitle: Supprimer un groupement de postes de messagerie unifiée
ms:assetid: 11ac102d-b58d-486c-85b6-e096428e556d
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Aa996318(v=EXCHG.150)
ms:contentKeyID: 50555348
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Supprimer un groupement de postes de messagerie unifiée

 

_**Sapplique à :**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :**2012-11-05_

Après avoir supprimé un groupement de postes de messagerie unifiée (MU), la passerelle IP de messagerie unifiée associée au groupe ne gère plus les appels entrants et n’y répond plus. Si la suppression du groupement de postes de messagerie unifiée laisse la passerelle IP de messagerie unifiée sans aucun groupement de postes configuré restant, la passerelle IP n’est plus en mesure de traiter les appels de la messagerie unifiée.

Pour d’autres tâches relatives aux groupements de postes de messagerie unifiée, consultez la rubrique [Procédures de groupe postes de messagerie unifiée](um-hunt-group-procedures-exchange-2013-help.md).

<table>
<thead>
<tr class="header">
<th><img src="images/Bb125224.warning(EXCHG.150).gif" title="Avertissement" alt="Avertissement" />Avertissement :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Si vous voulez modifier les paramètres du groupement de postes de messagerie unifiée, vous devez supprimer le groupement de postes, puis créer un autre groupement de postes doté des paramètres appropriés.</td>
</tr>
</tbody>
</table>


## Ce qu’il faut savoir avant de commencer ?

  - Durée d'exécution estimée : Moins d’une minute.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Groupements de postes de messagerie unifiée » dans la rubrique [Autorisations de messagerie unifiée](unified-messaging-permissions-exchange-2013-help.md).

  - Avant d’exécuter ces procédures, vérifiez qu’un plan de numérotation de messagerie unifiée a été créé. Pour obtenir la procédure détaillée, consultez la rubrique [Créer un plan de numérotation de messagerie unifiée](create-a-um-dial-plan-exchange-2013-help.md).

  - Avant d’exécuter ces procédures, vérifiez qu’une passerelle IP de messagerie unifiée a été créée. Pour obtenir la procédure détaillée, consultez la rubrique [Créer une passerelle IP de messagerie unifiée](create-a-um-ip-gateway-exchange-2013-help.md).

  - Avant d’effectuer ces procédures, vérifiez qu’un groupement de postes de messagerie unifiée a été créé. Pour obtenir la procédure détaillée, consultez la rubrique [Créer un groupement de postes de messagerie unifiée](create-a-um-hunt-group-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

<table>
<thead>
<tr class="header">
<th><img src="images/Bb125224.tip(EXCHG.150).gif" title="Conseil" alt="Conseil" />Conseil :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..</td>
</tr>
</tbody>
</table>


## Que souhaitez-vous faire ?

## Création d’un groupement de postes de messagerie unifiée à l’aide du Centre d’administration Exchange (CAE)

1.  Dans le Centre d’administration Exchange, accédez à **Messagerie unifiée** \> **Plans de numérotation de messagerie unifiée**. Dans la liste affichée, cliquez sur le plan de numérotation de messagerie unifiée à modifier, puis dans la barre d’outils, cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

2.  Sur la page **Plan de numérotation de messagerie unifiée**, sous **Groupements de postes de messagerie unifiée**, sélectionnez le groupement de postes à supprimer, puis dans la barre d’outils, cliquez sur **Supprimer**![Icône Supprimer](images/Dd979797.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "Icône Supprimer").

3.  Sur la page **Avertissement**, cliquez sur **Oui**.

## Suppression d’un groupement de postes de messagerie unifiée à l’aide de l’environnement de ligne de commande Exchange Management Shell

Cet exemple montre comment supprimer un groupe de recherche de la messagerie unifiée nommé `MyUMHuntGroup`.

    Remove-UMHuntGroup -identity MyUMHuntGroup

