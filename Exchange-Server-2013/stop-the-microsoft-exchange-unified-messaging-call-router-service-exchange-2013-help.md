---
title: "Arrêtez le service Microsoft Exchange Unified Messaging routeur d'appels: Exchange 2013 Help"
TOCTitle: Arrêtez le service Microsoft Exchange Unified Messaging routeur d'appels
ms:assetid: 79935528-1a8c-4f22-826c-8f9a60f4f6f4
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ673535(v=EXCHG.150)
ms:contentKeyID: 50555416
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Arrêtez le service Microsoft Exchange Unified Messaging routeur d'appels

 

_**Sapplique à :** Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2012-11-16_

Le composant logiciel enfichable Services de la console de gestion (MMC) Microsoft ou cmd.exe à l'invite de commandes vous permet d'arrêter le service routeur des appels de messagerie unifiée MicrosoftExchange sur un serveur d'accès au client. Dans certaines circonstances, vous êtes amené à arrêter ce service, par exemple, si vous devez mettre le serveur d'accès au client hors connexion. Lorsque vous arrêtez le service routeur des appels de messagerie unifiée MicrosoftExchange, le serveur d'accès au client n'est pas en mesure d'accepter ni de traiter des appels entrants.

Pour les tâches de gestion supplémentaires relatives aux serveurs d'accès au client, consultez la rubrique [Procédures de services de messagerie unifiée](um-services-procedures-exchange-2013-help.md).

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : moins d'une minute.

  - Pour exécuter les procédures suivantes, vous devez vous connecter au serveur d'accès au client à l'aide d'un compte appartenant au groupe Administrateurs local.

  - Vérifiez que le serveur d'accès au client est installé, sur le même ordinateur que le serveur de boîtes aux lettres ou sur un ordinateur distinct.

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..


## Que souhaitez-vous faire ?

## Utiliser le composant logiciel enfichable Services de la console de gestion (MMC) pour arrêter le service routeur des appels de messagerie unifiée Microsoft Exchange

1.  Cliquez sur **Démarrer**, puis sur **Panneau de configuration**.

2.  Dans le Panneau de configuration, double-cliquez sur **Outils d'administration**.

3.  Dans **Outils d'administration**, double-cliquez sur **Services**.

4.  Dans le volet d'informations **Services**, cliquez avec le bouton droit sur **Routeur d'appels de messagerie unifiée Microsoft Exchange**, puis cliquez sur **Arrêter**.

## Utiliser une invite de commandes pour arrêter le service routeur des appels de messagerie unifiée Microsoft Exchange

1.  Cliquez sur **Démarrer**, puis sur **Exécuter**.

2.  Dans la zone **Ouvrir**, entrez la commande suivante, puis appuyez sur Entrée.
    
        net stop MSExchangeUMCR

