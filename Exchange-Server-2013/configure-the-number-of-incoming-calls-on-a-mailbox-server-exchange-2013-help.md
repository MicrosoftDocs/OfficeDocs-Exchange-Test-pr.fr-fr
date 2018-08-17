---
title: 'Configurer le nombre d’appels entrants sur un srv de BAL: Exchange 2013 Help'
TOCTitle: Configurer le nombre d'appels entrants sur un serveur de boîtes aux lettres
ms:assetid: 419e1de9-2bf8-48a8-824d-2a536b0a6d90
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Aa997637(v=EXCHG.150)
ms:contentKeyID: 50555376
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurer le nombre d'appels entrants sur un serveur de boîtes aux lettres

 

_**Sapplique à :** Exchange Server, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2013-02-23_

Vous pouvez configurer le nombre de connexions entrantes simultanées qu'un serveur de boîtes aux lettres qui exécute le service de messagerie unifiée Microsoft Exchange acceptera. Cela inclut tous les appels entrants, y compris Outlook Voice Access, répondre aux appels, les standards automatiques et les appels de télécopie. Lorsque vous augmentez le nombre de connexions simultanées sur un serveur de boîtes aux lettres, davantage de ressources système est requises que si vous réduisez le nombre d'appels simultanés. Réduction du nombre d'appels simultanés est particulièrement important sur les ordinateurs plus lents sur lequel sont installés les services de messagerie unifiée. La plage pour le nombre d'appels vocaux simultanés est 0 à 200. Le paramètre par défaut est 100.

Pour d'autres tâches relatives aux serveurs de messagerie unifiée et de boîtes aux lettres, consultez la rubrique [Procédures de services de messagerie unifiée](um-services-procedures-exchange-2013-help.md).

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : moins d'une minute.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l'entrée « Serveur de boîtes aux lettres (service de messagerie unifiée) » dans la rubrique [Autorisations de messagerie unifiée](unified-messaging-permissions-exchange-2013-help.md).

  - Vérifiez que vous avez correctement installé les serveurs d'accès au Client et boîte aux lettres.

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..


## Que souhaitez-vous faire ?

## Utiliser le CAE pour configurer le nombre d'appels entrants sur un serveur de boîtes aux lettres

1.  Dans le CAE, accédez à **Serveurs** \> **Serveurs**.

2.  Dans l'affichage Liste, sélectionnez le serveur Exchange à modifier, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

3.  Dans la page **Exchange Server**, cliquez sur **Messagerie unifiée**.

4.  Sous **Paramètres du service de messagerie unifiée**, sous l'élément **Nombre maximal d'appels autorisés**, entrez un nombre compris entre 0 et 200, puis cliquez sur **Enregistrer**.

## Utiliser l'environnement de ligne de commande pour configurer le nombre d'appels entrants sur un serveur de boîtes aux lettres

Cet exemple définit le nombre d'appels vocaux, Outlook Voice Access et de télécopie entrants qui peuvent être acceptés par un serveur de boîtes aux lettres nommé `MyMailboxServer1` sur 50.

    Set-UMService -Identity MyMailboxServer1 -MaxCallsAllowed 50

