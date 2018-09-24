---
title: 'Démarrage du service routeur d’appels de messagerie unifiée Microsoft Exchange'
TOCTitle: Démarrage du service routeur d'appels de messagerie unifiée Microsoft Exchange
ms:assetid: 8b7e1a4c-87b3-4477-a95f-6b41cf2d38f0
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ673542(v=EXCHG.150)
ms:contentKeyID: 50555442
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Démarrage du service routeur d'appels de messagerie unifiée Microsoft Exchange

 

_**Sapplique à :** Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2012-11-16_

Le composant logiciel enfichable Services de la console de gestion (MMC) Microsoft ou cmd.exe à l'invite de commandes vous permet de démarrer le service routeur des appels de messagerie unifiée MicrosoftExchange sur un serveur d'accès au client. Par défaut, le service routeur des appels de messagerie unifiée MicrosoftExchange démarre après l'installation d'un serveur d'accès au client. Cependant, il est parfois nécessaire de redémarrer ou d'arrêter le service routeur des appels de messagerie unifiée MicrosoftExchange manuellement, par exemple, si après avoir mis le serveur d'accès au client hors connexion, vous devez le remettre en ligne.

Lorsque le service routeur des appels de messagerie unifiée MicrosoftExchange démarre sur un serveur d'accès au client, ce dernier est disponible pour répondre et traiter les appels de messagerie unifiée entrants.

Pour les tâches de gestion supplémentaires relatives aux serveurs d'accès au client, consultez la rubrique [Procédures de services de messagerie unifiée](um-services-procedures-exchange-2013-help.md).

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : moins d'une minute.

  - Pour exécuter les procédures suivantes, vous devez vous connecter au serveur d'accès au client à l'aide d'un compte appartenant au groupe Administrateurs local.

  - Vérifiez que le serveur d'accès au client est installé, soit sur le même ordinateur que le serveur de boîtes aux lettres, soit sur un ordinateur distinct.

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..


## Que souhaitez-vous faire ?

## Utiliser le composant logiciel enfichable Services de la console de gestion (MMC) pour démarrer le service routeur des appels de messagerie unifiée Microsoft Exchange

1.  Cliquez sur **Démarrer**, puis sur **Panneau de configuration**.

2.  Dans le Panneau de configuration, double-cliquez sur **Outils d'administration**.

3.  Dans **Outils d'administration**, double-cliquez sur **Services**.

4.  Dans le volet d'informations **Services**, cliquez avec le bouton droit sur **Routeur des appels de messagerie unifiée Microsoft Exchange**, puis cliquez sur **Démarrer**.

## Utiliser une invite de commandes pour démarrer le service routeur des appels de messagerie unifiée Microsoft Exchange

1.  Cliquez sur **Démarrer**, puis sur **Exécuter**.

2.  Dans la zone **Ouvrir**, entrez la commande suivante, puis appuyez sur Entrée.
    
    ```powershell
    net start MSExchangeUMCR
    ```

