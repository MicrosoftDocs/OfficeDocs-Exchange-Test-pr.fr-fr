---
title: 'Désactiver les notif. d’appels manqués pour un utilisateur: Exchange 2013 Help'
TOCTitle: Désactiver les notifications d’appels manqués pour un utilisateur
ms:assetid: e54937d5-3074-454f-b561-e601fecfc6ad
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ673570(v=EXCHG.150)
ms:contentKeyID: 52057168
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Désactiver les notifications d’appels manqués pour un utilisateur

 

_**Sapplique à :** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2012-12-09_

Vous pouvez activer ou désactiver les notifications d'appels en absence pour une stratégie de boîte aux lettres de messagerie unifiée à l'aide de l'environnement de ligne de commande Exchange Management Shell ou du Centre d'administration Exchange (CAE). Une notification d'appel en absence est un message électronique envoyé à un utilisateur quand celui-ci ne répond pas à un appel entrant et que l'appelant ne laisse pas de message vocal. Ce message électronique diffère de celui qui contient le message vocal laissé pour un utilisateur.

Quand vous désactivez les notifications d'appels en absence sur une stratégie de boîte aux lettres de messagerie unifiée, tous les utilisateurs associés à cette stratégie ne reçoivent plus de message électronique lorsqu'ils ne répondent pas à un appel et que l'appelant ne laisse pas de message vocal. Par défaut, les notifications d'appels en absence sont activées pour chaque stratégie de boîte aux lettres de messagerie unifiée qui est créée. Par ailleurs, une stratégie de boîte aux lettres de messagerie unifiée est créée chaque fois que vous créez un plan de numérotation de messagerie unifiée.

> [!NOTE]
> Lors de l'intégration de la messagerie unifiée et de Microsoft Lync Server, les notifications d'appels en absence ne sont pas disponibles aux utilisateurs qui disposent d'une boîte aux lettres située sur un serveur de boîtes aux lettres Exchange 2007 ou Exchange 2010 lorsqu'un utilisateur se déconnecte avant l'envoi de l'appel vers un serveur de boîtes aux lettres exécutant le service de messagerie unifiée Microsoft Exchange.


Pour les autres tâches de gestion relatives aux stratégies de boîte aux lettres de messagerie unifiée, consultez la rubrique [Gérer une stratégie de boîte aux lettres de messagerie unifiée](manage-a-um-mailbox-policy-exchange-2013-help.md).

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : Moins d’une minute.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Stratégies de boîte aux lettres de messagerie unifiée » dans la rubrique [Autorisations de messagerie unifiée](unified-messaging-permissions-exchange-2013-help.md).

  - Avant d'exécuter ces procédures, vérifiez qu'un plan de numérotation de messagerie unifiée a été créé. Pour obtenir la procédure détaillée, consultez la rubrique [Créer un plan de numérotation de messagerie unifiée](create-a-um-dial-plan-exchange-2013-help.md).

  - Avant d'effectuer ces procédures, vérifiez qu'une stratégie de boîte aux lettres de messagerie unifiée a été créée. Pour obtenir la procédure détaillée, consultez la rubrique [Créer une stratégie de boîte aux lettres de messagerie unifiée](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..


## Que souhaitez-vous faire ?

## Utiliser le Centre d'administration Exchange (CAE) pour désactiver les notifications d'appels en absence sur une stratégie de boîte aux lettres de messagerie unifiée

1.  Dans le CAE, accédez à **Messagerie unifiée** \> **Plans de numérotation de messagerie unifiée**. Dans l'affichage Liste, sélectionnez le plan de numérotation de messagerie unifiée à modifier puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

2.  Dans la page **Plan de numérotation de messagerie unifiée**, sous **Stratégies de boîte aux lettres de messagerie unifiée**, sélectionnez la stratégie de boîte aux lettres de messagerie unifiée à gérer, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

3.  Dans la page **Stratégie de boîte aux lettres de messagerie unifiée** \> **Général**, décochez la case en regard de l'option **Autoriser les notifications d'appel en absence**.

4.  Cliquez sur **Enregistrer**.

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour désactiver les notifications d'appels en absence sur une stratégie de boîte aux lettres de messagerie unifiée

Cet exemple désactive les notifications d'appels en absence sur la stratégie de boîte aux lettres de messagerie unifiée `MyUMMailboxPolicy`.

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -AllowMissedCallNotifications $false

