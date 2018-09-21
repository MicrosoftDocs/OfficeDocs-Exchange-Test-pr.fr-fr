---
title: 'Arrêt du service de messagerie unifiée Microsoft Exchange: Exchange 2013 Help'
TOCTitle: Arrêt du service de messagerie unifiée Microsoft Exchange
ms:assetid: 64fa5535-8150-45c6-82e6-d2346892a031
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Aa998595(v=EXCHG.150)
ms:contentKeyID: 50555402
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Arrêt du service de messagerie unifiée Microsoft Exchange

 

_**Sapplique à :** Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2012-11-16_

Vous pouvez utiliser le composant logiciel enfichable Services de Microsoft Management Console (MMC) ou cmd.exe à l'invite de commandes pour arrêter le service de messagerie unifiée MicrosoftExchange sur un serveur de boîtes aux lettres. Dans certaines circonstances, vous serez amené à interrompre ce service, par exemple, quand le serveur de boîtes aux lettres doit être mis hors connexion. Quand vous arrêtez le service de messagerie unifiée Microsoft Exchange, le serveur de boîtes aux lettres ne peut ni accepter, ni traiter les appels entrants.

Pour d'autres tâches de gestion relatives aux serveurs de boîtes aux lettres, consultez la rubrique [Procédures de services de messagerie unifiée](um-services-procedures-exchange-2013-help.md).

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : moins d'une minute.

  - Pour exécuter les procédures suivantes, vous devez vous connecter au serveur de boîtes aux lettres à l'aide d'un compte appartenant au groupe Administrateurs local de cet ordinateur.

  - Vérifiez que le serveur de boîtes aux lettres est installé, sur le même ordinateur que le serveur d'accès au client ou sur un ordinateur distinct.

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..


## Que souhaitez-vous faire ?

## Utiliser le composant logiciel enfichable des services MMC pour arrêter le service de messagerie unifiée Microsoft Exchange

1.  Cliquez sur **Démarrer**, puis sur **Panneau de configuration**.

2.  Dans le Panneau de configuration, double-cliquez sur **Outils d'administration**.

3.  Dans **Outils d'administration**, double-cliquez sur **Services**.

4.  Dans le volet d'informations **Services**, cliquez avec le bouton droit sur **Messagerie unifiée Microsoft Exchange**, puis cliquez sur **Arrêter**.

## Utiliser une invite de commandes pour arrêter le service de messagerie unifiée Microsoft Exchange

1.  Cliquez sur **Démarrer**, puis sur **Exécuter**.

2.  Dans la zone **Ouvrir**, entrez la commande suivante, puis appuyez sur Entrée.
    
    ```powershell
net stop MSExchangeUM
```

