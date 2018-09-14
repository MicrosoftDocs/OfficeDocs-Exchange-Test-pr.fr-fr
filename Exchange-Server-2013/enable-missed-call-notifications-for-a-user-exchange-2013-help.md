---
title: "Activation des notifications d'appels en absence: Exchange 2013 Help"
TOCTitle: Activation des notifications d'appels en absence
ms:assetid: aa0cbb60-5422-474f-af16-621aade31c1f
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb232159(v=EXCHG.150)
ms:contentKeyID: 52057133
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Activation des notifications d'appels en absence

 

_**Sapplique à :** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2012-12-09_

Vous pouvez activer ou désactiver les notifications d'appels en absence pour une stratégie de boîte aux lettres de messagerie unifiée à l'aide de l'environnement de ligne de commande Exchange Management Shell ou du Centre d'administration Exchange (CAE). Une notification d'appel en absence est un message électronique envoyé à un utilisateur quand celui-ci ne répond pas à un appel entrant et que l'appelant ne laisse pas de message vocal. Ce message électronique diffère de celui qui contient le message vocal laissé pour un utilisateur.

Quand vous désactivez les notifications d'appels en absence sur une stratégie de boîte aux lettres de messagerie unifiée, tous les utilisateurs associés à cette stratégie ne reçoivent plus de message électronique lorsqu'ils ne répondent pas à un appel et que l'appelant ne laisse pas de message vocal. Par défaut, les notifications d'appels en absence sont activées pour chaque stratégie de boîte aux lettres de messagerie unifiée qui est créée. Par ailleurs, une stratégie de boîte aux lettres de messagerie unifiée est créée chaque fois que vous créez un plan de numérotation de messagerie unifiée.

> [!NOTE]
> Lors de l'intégration de la messagerie unifiée et de Microsoft Lync Server, les notifications d'appels en absence ne sont pas disponibles aux utilisateurs qui disposent d'une boîte aux lettres située sur un serveur de boîtes aux lettres Exchange 2007 ou Exchange 2010 lorsqu'un utilisateur se déconnecte avant l'envoi de l'appel vers un serveur de boîtes aux lettres exécutant le service de messagerie unifiée Microsoft Exchange.


Pour les autres tâches de gestion relatives aux stratégies de boîte aux lettres de messagerie unifiée, consultez la rubrique [Gérer une stratégie de boîte aux lettres de messagerie unifiée](https://docs.microsoft.com/fr-fr/exchange/voice-mail-unified-messaging/set-up-voice-mail/manage-um-mailbox-policy).

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : moins d'une minute.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l'entrée « Stratégies de boîte aux lettres de messagerie unifiée » dans la rubrique [Autorisations de messagerie unifiée](unified-messaging-permissions-exchange-2013-help.md).

  - Avant d'effectuer ces procédures, vérifiez qu'un plan de numérotation de messagerie unifiée a été créé. Pour obtenir la procédure détaillée, consultez la rubrique [Créer un plan de numérotation de messagerie unifiée](https://docs.microsoft.com/fr-fr/exchange/voice-mail-unified-messaging/connect-voice-mail-system/create-um-dial-plan).

  - Avant d'effectuer ces procédures, vérifiez qu'une stratégie de boîte aux lettres de messagerie unifiée a été créée. Pour obtenir la procédure détaillée, consultez la rubrique [Créer une stratégie de boîte aux lettres de messagerie unifiée](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..


## Que souhaitez-vous faire ?

## Utiliser le Centre d'administration Exchange (CAE) pour activer les notifications d'appels en absence sur une stratégie de boîte aux lettres de messagerie unifiée

1.  Dans le CAE, accédez à **Messagerie unifiée** \> **Plans de numérotation de messagerie unifiée**. Dans l'affichage Liste, sélectionnez le plan de numérotation de messagerie unifiée à modifier puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

2.  Dans la page **Plan de numérotation de messagerie unifiée**, sous **Stratégies de boîte aux lettres de messagerie unifiée**, sélectionnez la stratégie de boîte aux lettres de messagerie unifiée à gérer, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

3.  Dans la page **Stratégie de boîte aux lettres de messagerie unifiée** \> **Général**, cochez la case en regard de l'option **Autoriser les notifications d'appel en absence**.

4.  Cliquez sur **Enregistrer**.

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour activer les notifications d'appels en absence sur une stratégie de boîte aux lettres de messagerie unifiée

Cet exemple active les notifications d'appels en absence sur la stratégie de boîte aux lettres de messagerie unifiée `MyUMMailboxPolicy`.

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -AllowMissedCallNotifications $true

