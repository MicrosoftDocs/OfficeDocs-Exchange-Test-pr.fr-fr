---
title: "Activer l’aperçu de messag. vocale pour les utilisateurs: Exchange 2013 Help | Microsoft Docs"
TOCTitle: Activer l'aperçu de messagerie vocale pour les utilisateurs
ms:assetid: 206a5d2b-27c9-4e9b-a29a-6ddffaa07109
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ673514(v=EXCHG.150)
ms:contentKeyID: 51407169
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Activer l'aperçu de messagerie vocale pour les utilisateurs

 

_**Sapplique à :** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2013-02-21_

Vous pouvez activer la fonctionnalité Aperçu de messagerie vocale si elle a été désactivée pour les utilisateurs associés à une stratégie de boîte aux lettres de messagerie unifiée. L'activation de ce paramètre permet aux utilisateurs de recevoir le texte d'un message vocal dans le corps d'un message électronique ou d'un SMS. Le paramètre par défaut est Activé.

Pour les autres tâches de gestion relatives aux stratégies de boîte aux lettres de messagerie unifiée, consultez la rubrique [Procédures de stratégie de boîte aux lettres de messagerie unifiée](um-mailbox-policy-procedures-exchange-2013-help.md).

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : moins d'une minute.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l'entrée « Stratégies de boîte aux lettres de messagerie unifiée » dans la rubrique [Autorisations de messagerie unifiée](unified-messaging-permissions-exchange-2013-help.md).

  - Avant d'exécuter ces procédures, vérifiez qu'un plan de numérotation de messagerie unifiée a été créé. Pour obtenir la procédure détaillée, consultez la rubrique [Créer un plan de numérotation de messagerie unifiée](create-a-um-dial-plan-exchange-2013-help.md).

  - Avant d'effectuer ces procédures, vérifiez qu'une stratégie de boîte aux lettres de messagerie unifiée a été créée. Pour obtenir la procédure détaillée, consultez la rubrique [Créer une stratégie de boîte aux lettres de messagerie unifiée](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..


## Que souhaitez-vous faire ?

## Utiliser le Centre d'administration Exchange (CAE) pour activer l'Aperçu de messagerie vocale

1.  Dans le CAE, accédez à **Messagerie unifiée** \> **Plans de numérotation de messagerie unifiée**, sélectionnez le plan de numérotation de messagerie unifiée à modifier, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

2.  Dans la page **Plan de numérotation de messagerie unifiée**, sous **Stratégies de boîte aux lettres de messagerie unifiée**, sélectionnez la stratégie de boîte aux lettres de messagerie unifiée à gérer, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

3.  Dans la page **Stratégie de boîte aux lettres de messagerie unifiée** \> **Général**, cochez la case en regard de l'option **Autoriser l'aperçu de messagerie vocale**.

4.  Cliquez sur **Enregistrer**.

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour activer l'Aperçu de messagerie vocale

Cet exemple permet aux utilisateurs associés à la stratégie de boîte aux lettres de messagerie unifiée `MyUMMailboxPolicy` d'utiliser la fonctionnalité Aperçu de messagerie vocale.

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy - AllowVoiceMailPreview $true

