---
title: 'Démarrage du service de messagerie unifiée Microsoft Exchange: Exchange 2013 Help'
TOCTitle: Démarrage du service de messagerie unifiée Microsoft Exchange
ms:assetid: b54008e6-172e-4435-8516-57cff740e89c
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb124330(v=EXCHG.150)
ms:contentKeyID: 50555466
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Démarrage du service de messagerie unifiée Microsoft Exchange

 

_**Sapplique à :** Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2012-11-16_

Vous pouvez utiliser le composant logiciel enfichable Services de la console de gestion Microsoft (MMC) ou cmd.exe à l'invite de commandes pour démarrer le service de messagerie unifiée Microsoft Exchange sur un serveur de boîtes aux lettres. Par défaut, le service de messagerie unifiée MicrosoftExchange est lancé après l'installation d'un serveur de boîtes aux lettres. Cependant, dans certains cas, vous êtes amené à redémarrer le service de messagerie unifiée Microsoft Exchange manuellement, par exemple lorsque vous mettez le serveur de boîtes aux lettres hors connexion et que vous devez ensuite le remettre en ligne.

Lorsque le service de messagerie unifiée Microsoft Exchange est démarré sur un serveur de boîtes aux lettres, ce dernier est disponible pour répondre aux appels de messagerie unifiée entrants et les traiter.

Pour connaître les tâches de gestion supplémentaires relatives aux serveurs de boîtes aux lettres, consultez la rubrique [Procédures de services de messagerie unifiée](um-services-procedures-exchange-2013-help.md).

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : moins d'une minute.

  - Pour effectuer les procédures suivantes, vous devez vous connecter au serveur de boîtes aux lettres à l'aide d'un compte appartenant au groupe Administrateurs local de cet ordinateur.

  - Vérifiez que le serveur de boîtes aux lettres est installé, sur le même ordinateur que le serveur d'accès au client ou sur un ordinateur séparé.

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..


## Que souhaitez-vous faire ?

## Utiliser le composant logiciel enfichable MMC Services pour démarrer le service de messagerie unifiée Microsoft Exchange

1.  Cliquez sur **Démarrer**, puis sur **Panneau de configuration**.

2.  Dans le Panneau de configuration, double-cliquez sur **Outils d'administration**.

3.  Dans **Outils d'administration**, double-cliquez sur **Services**.

4.  Dans le volet d'informations **Services**, cliquez avec le bouton droit sur **Messagerie unifiée Microsoft Exchange**, puis cliquez sur **Démarrer**.

## Utiliser une invite de commandes pour démarrer le service de messagerie unifiée Microsoft Exchange

1.  Cliquez sur **Démarrer**, puis sur **Exécuter**.

2.  Dans la zone **Ouvrir**, entrez la commande suivante, puis appuyez sur Entrée.
    
        net start MSExchangeUM

