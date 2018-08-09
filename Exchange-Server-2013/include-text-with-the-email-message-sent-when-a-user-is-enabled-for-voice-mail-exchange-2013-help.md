---
title: 'Inclure du txt ac le msg électr. envoyé si un utlsr est activé pr messag. voc.'
TOCTitle: Inclure du texte avec le message électronique envoyé lorsqu'un utilisateur est activé pour la messagerie vocale
ms:assetid: 3e8292fb-0cdb-445d-8048-a59af7c38d63
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb201679(v=EXCHG.150)
ms:contentKeyID: 51407175
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Inclure du texte avec le message électronique envoyé lorsqu'un utilisateur est activé pour la messagerie vocale

 

_**Sapplique à :** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2012-12-16_

Quand la boîte aux lettres d'un utilisateur est activée pour la messagerie vocale de messagerie unifiée, un message d'accueil sur la messagerie unifiée est envoyé à l'utilisateur. Ce message contient les informations de code confidentiel qui permettent à l'utilisateur d'accéder pour la première fois au système de messagerie vocale.

Vous pouvez personnaliser le texte envoyé dans le message d'accueil en ajoutant du texte dans la zone **Lors de l'activation de la messagerie unifiée pour un utilisateur** dans la stratégie de boîte aux lettres de messagerie unifiée. Cela permet d'inclure des informations telles que les numéros de téléphone du support technique de messagerie unifiée ou des numéros Outlook Voice Access supplémentaires. Une fois le texte ajouté, il est inclus dans chaque message envoyé lors de l'activation de la messagerie unifiée pour des utilisateurs associés à la stratégie de boîte aux lettres de messagerie unifiée.

> [!NOTE]
> Le texte personnalisé ajouté au message d'accueil est limité à 512 caractères et peut contenir du texte HTML simple.


Pour d'autres tâches de gestion relatives aux stratégies de boîte aux lettres de messagerie unifiée, consultez la rubrique [Procédures de stratégie de boîte aux lettres de messagerie unifiée](um-mailbox-policy-procedures-exchange-2013-help.md).

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : moins d'une minute.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l'entrée « Stratégies de boîte aux lettres de messagerie unifiée » dans la rubrique [Autorisations de messagerie unifiée](unified-messaging-permissions-exchange-2013-help.md).

  - Avant d'exécuter ces procédures, vérifiez qu'un plan de numérotation de messagerie unifiée a été créé. Pour obtenir la procédure détaillée, consultez la rubrique [Créer un plan de numérotation de messagerie unifiée](create-a-um-dial-plan-exchange-2013-help.md).

  - Avant d'effectuer ces procédures, vérifiez qu'une stratégie de boîte aux lettres de messagerie unifiée a été créée. Pour obtenir la procédure détaillée, consultez la rubrique [Créer une stratégie de boîte aux lettres de messagerie unifiée](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..


## Que souhaitez-vous faire ?

## Utiliser le CAE pour personnaliser le texte envoyé lors de l'activation d'une boîte aux lettres pour la messagerie unifiée

1.  Dans le CAE, accédez à **Messagerie unifiée** \> **Plans de numérotation de messagerie unifiée**. Dans l'affichage Liste, sélectionnez le plan de numérotation de messagerie unifiée à modifier puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

2.  Dans la page **Plan de numérotation de messagerie unifiée**, sous **Stratégies de boîte aux lettres de messagerie unifiée**, sélectionnez la stratégie de boîte aux lettres de messagerie unifiée à gérer, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

3.  Dans la page **Stratégie de boîte aux lettres de messagerie unifiée** \> **Texte du message**, dans la zone de texte **Lors de l'activation de la messagerie unifiée pour un utilisateur**, entrez le texte à inclure au message envoyé lors de l'activation de la messagerie vocale de messagerie unifiée pour les utilisateurs.

4.  Cliquez sur **Enregistrer**.

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour personnaliser le texte envoyé lors de l'activation de la messagerie unifiée pour une boîte aux lettres

Cet exemple permet aux utilisateurs à extension messagerie unifiée associés à une stratégie de boîte aux lettres de messagerie unifiée de recevoir des instructions supplémentaires sur la messagerie unifiée et le numéro Outlook Voice Access qu'ils peuvent utiliser pour accéder à leur boîte aux lettres par téléphone.

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -UMEnabledText "You've been enabled for Unified Messaging voice mail. To access your Exchange mailbox, call your internal telephone extension number. From outside your office, call 425-555-1234."

