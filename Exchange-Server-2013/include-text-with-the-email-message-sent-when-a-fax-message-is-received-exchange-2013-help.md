---
title: 'Inclure le texte avec le message électronique envoyé lors de la réception d’un message de télécopie: Exchange 2013 Help'
TOCTitle: Inclure le texte avec le message électronique envoyé lors de la réception d’un message de télécopie
ms:assetid: 48244e58-b7d6-4f0e-bbae-d22bf0fc11ff
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb201684(v=EXCHG.150)
ms:contentKeyID: 51407178
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Inclure le texte avec le message électronique envoyé lors de la réception d’un message de télécopie

 

_**Sapplique à :**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :**2016-12-09_

Vous pouvez ajouter du texte au message électronique envoyé lors de la réception d'un message de télécopie par un utilisateur pour qui la messagerie vocale de messagerie unifiée et la réception de télécopies sont activées, et lorsque la stratégie de boîte aux lettres de messagerie unifiée a été configurée correctement pour utiliser un fournisseur de télécopie. Par défaut, le texte inclus quand un utilisateur à extension messagerie unifiée reçoit un message de télécopie indique uniquement que l'utilisateur a reçu un message de télécopie. Vous pouvez toutefois créer un message personnalisé en ajoutant du texte dans la zone **Lorsqu'un utilisateur reçoit un message de télécopie** dans une stratégie de boîte aux lettres de messagerie unifiée. Par exemple, le texte peut inclure des informations sur les stratégies de sécurité système et décrire la façon correcte de traiter les messages de télécopie dans votre organisation. Une fois le texte ajouté, il est inclus dans chaque message électronique envoyé lorsque les utilisateurs à extension messagerie unifiée associés à la stratégie de boîte aux lettres de messagerie unifiée reçoivent un message de télécopie.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Le texte personnalisé qui accompagne un message de télécopie est limité à 512 caractères et peut contenir du texte HTML simple.</td>
</tr>
</tbody>
</table>


Pour plus d’informations sur les partenaires de télécopie, consultez [Microsoft PinPoint pour les partenaires de télécopie](https://go.microsoft.com/fwlink/?linkid=190238).

Pour découvrir d'autres tâches de gestion relatives à la télécopie, consultez la rubrique [Procédures d'envoi de télécopie](faxing-procedures-exchange-2013-help.md).

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : moins d'une minute.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Stratégies de boîte aux lettres de messagerie unifiée » dans la rubrique [Autorisations de messagerie unifiée](unified-messaging-permissions-exchange-2013-help.md).

  - Avant d'exécuter ces procédures, vérifiez qu'un plan de numérotation de messagerie unifiée a été créé. Pour obtenir la procédure détaillée, consultez la rubrique [Créer un plan de numérotation de messagerie unifiée](create-a-um-dial-plan-exchange-2013-help.md).

  - Avant d'effectuer ces procédures, vérifiez qu'une stratégie de boîte aux lettres de messagerie unifiée a été créée. Pour obtenir la procédure détaillée, consultez la rubrique [Créer une stratégie de boîte aux lettres de messagerie unifiée](create-a-um-mailbox-policy-exchange-2013-help.md).

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

## Utiliser le CAE pour modifier le texte inclus dans un message de télécopie

1.  Dans le CAE, accédez à **Messagerie unifiée** \> **Plans de numérotation de messagerie unifiée**. Dans l'affichage Liste, sélectionnez le plan de numérotation de messagerie unifiée à modifier puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

2.  Dans la page **Plan de numérotation de messagerie unifiée**, sous **Stratégies de boîte aux lettres de messagerie unifiée**, sélectionnez la stratégie de boîte aux lettres de messagerie unifiée à gérer, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

3.  Dans la page **Stratégie de boîte aux lettres de messagerie unifiée** \> **Texte du message**, dans la zone de texte **Lorsqu'un utilisateur reçoit un message de télécopie**, entrez le texte à inclure au message envoyé lors de la réception d'un message de télécopie dans leur boîte aux lettres.

4.  Cliquez sur **Enregistrer**.

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour modifier le texte inclus dans un message de télécopie

Cet exemple permet aux utilisateurs à extension messagerie unifiée associés à une stratégie de boîte aux lettres de messagerie unifiée de recevoir des instructions supplémentaires sur l'ouverture d'un message de télécopie reçu dans leur boîte aux lettres.

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -FaxMessageText "To open this fax message, double-click the file attachment."

