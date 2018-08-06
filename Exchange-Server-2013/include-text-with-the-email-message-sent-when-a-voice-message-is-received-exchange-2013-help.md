---
title: "Inclure du texte avec l’e-mail envoyé lors de la réception d’un message vocal | Microsoft Docs"
TOCTitle: Inclure du texte avec le message électronique envoyé lors de la réception d'un message vocal
ms:assetid: b2eec29c-e5eb-4263-80d8-0b9813dd56dc
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb201718(v=EXCHG.150)
ms:contentKeyID: 51407223
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Inclure du texte avec le message électronique envoyé lors de la réception d'un message vocal

 

_**Sapplique à :** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2012-12-16_

Vous pouvez inclure du texte supplémentaire dans le message électronique envoyé quand un utilisateur à extension messagerie vocale de messagerie unifiée reçoit un message vocal. Par défaut, le texte inclus dans un message vocal indique uniquement que l'appelant a reçu un message vocal. Vous pouvez toutefois créer un message personnalisé en ajoutant du texte dans la zone **Lorsqu'un utilisateur reçoit un message vocal** dans une stratégie de boîte aux lettres de messagerie unifiée. Par exemple, le texte peut inclure des informations sur les stratégies de sécurité système et décrire la façon correcte de traiter les messages vocaux dans votre organisation. Une fois le texte ajouté, il est inclus dans chaque message électronique envoyé lorsque les utilisateurs à messagerie unifiée associés à la stratégie de boîte aux lettres de messagerie unifiée reçoivent un message vocal.

> [!NOTE]
> Le texte personnalisé qui accompagne un message vocal est limité à 512 caractères et peut contenir du texte HTML simple.


Pour découvrir d'autres tâches de gestion relatives aux stratégies de boîte aux lettres de messagerie unifiée, consultez la rubrique [Procédures de stratégie de boîte aux lettres de messagerie unifiée](um-mailbox-policy-procedures-exchange-2013-help.md).

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : moins d'une minute.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l'entrée « Stratégies de boîte aux lettres de messagerie unifiée » dans la rubrique [Autorisations de messagerie unifiée](unified-messaging-permissions-exchange-2013-help.md).

  - Avant d'effectuer ces procédures, vérifiez qu'un plan de numérotation de messagerie unifiée a été créé. Pour obtenir la procédure détaillée, consultez la rubrique [Créer un plan de numérotation de messagerie unifiée](create-a-um-dial-plan-exchange-2013-help.md).

  - Avant d'effectuer ces procédures, vérifiez qu'une stratégie de boîte aux lettres de messagerie unifiée a été créée. Pour obtenir la procédure détaillée, consultez la rubrique [Créer une stratégie de boîte aux lettres de messagerie unifiée](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..


## Que souhaitez-vous faire ?

## Utiliser le Centre d'administration Exchange (CAE) pour modifier le texte inclus dans un message vocal

1.  Dans le CAE, accédez à **Messagerie unifiée** \> **Plans de numérotation de messagerie unifiée**. Dans l'affichage Liste, sélectionnez le plan de numérotation de messagerie unifiée à modifier puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

2.  Dans la page **Plan de numérotation de messagerie unifiée**, sous **Stratégies de boîte aux lettres de messagerie unifiée**, sélectionnez la stratégie de boîte aux lettres de messagerie unifiée à gérer, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

3.  Dans la page **Stratégie de boîte aux lettres de messagerie unifiée** \> **Texte du message**, dans la zone de texte **Lorsqu'un utilisateur reçoit un message vocal**, entrez le texte à inclure au message envoyé lors de la réception d'un message vocal.

4.  Cliquez sur **Enregistrer**.

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour modifier le texte inclus dans un message vocal

Cet exemple inclut le texte supplémentaire « Do not forward voice message to users outside this organization » (Ne transférez pas de messages vocaux aux utilisateurs extérieurs à cette organisation) dans les messages vocaux envoyés aux utilisateurs associés à la stratégie de boîte aux lettres de messagerie unifiée `MyUMMailboxPolicy`.

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -VoiceMailText "Do not forward voice messages to users outside this organization."

