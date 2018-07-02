---
title: 'Désactiver un standard automatique de messagerie unifiée: Exchange 2013 Help'
TOCTitle: Désactiver un standard automatique de messagerie unifiée
ms:assetid: ad79f374-f68f-430b-8b9c-2c841e1c55ae
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb124228(v=EXCHG.150)
ms:contentKeyID: 50478861
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Désactiver un standard automatique de messagerie unifiée

 

_**Sapplique à :** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2012-11-05_

Par défaut, lorsqu'un standard automatique de messagerie unifiée est créé, il présente l'état Désactivé. Après avoir créé le standard automatique de messagerie unifiée, vous pouvez en modifier le statut pour contrôler s'il peut répondre à des appels entrants. Par exemple, vous pouvez désactiver le standard automatique de messagerie unifiée lorsque vous enregistrez ou réenregistrez des messages et des messages d'assistance vocaux personnalisés.

Pour les autres tâches de gestion relatives aux standards automatiques de messagerie unifiée, consultez la rubrique [Procédures relatives au standard automatique de messagerie unifiée](um-auto-attendant-procedures-exchange-2013-help.md).

## Ce qu’il faut savoir avant de commencer ?

  - Durée d'exécution estimée : Moins d’une minute.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Standards automatiques de messagerie unifiée » dans la rubrique [Autorisations de messagerie unifiée](unified-messaging-permissions-exchange-2013-help.md).

  - Avant d’exécuter ces procédures, vérifiez qu’un plan de numérotation de messagerie unifiée a été créé. Pour obtenir la procédure détaillée, consultez la rubrique [Créer un plan de numérotation de messagerie unifiée](create-a-um-dial-plan-exchange-2013-help.md).

  - Avant d’exécuter ces procédures, vérifiez qu’un standard automatique de messagerie unifiée a été créé. Pour obtenir la procédure détaillée, voir [Créer un standard automatique de messagerie unifiée](create-a-um-auto-attendant-exchange-2013-help.md). Confirmez également que le standard automatique de messagerie unifiée est activé.

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

## Utiliser le CAE pour désactiver un standard automatique de messagerie unifiée

1.  Dans le Centre d’administration Exchange, accédez à **Messagerie unifiée** \> **Plans de numérotation de messagerie unifiée**. Dans l'affichage liste, sélectionnez le plan de numérotation à modifier puis, dans la barre d’outils, cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

2.  Sur la page **Plan de numérotation de messagerie unifiée**, sous **Standards automatiques de messagerie unifiée**, sélectionnez le standard automatique de messagerie unifiée à désactiver. Dans la barre d'outils, cliquez sur **Flèche vers le bas**![Icône de flèche vers le bas](images/JJ150576.ef5ca57d-a033-457b-bd92-6361877c33d0(EXCHG.150).gif "Icône de flèche vers le bas")

3.  Sur la page **Avertissement**, cliquez sur **Oui**.

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour désactiver un standard automatique de messagerie unifiée

Cet exemple désactive un standard automatique de messagerie unifiée nommé `MyUMAutoAttendant`.

    Disable-UMAutoAttendant -Identity MyUMAutoAttendant

