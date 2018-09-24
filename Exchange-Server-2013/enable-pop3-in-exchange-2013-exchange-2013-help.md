---
title: 'Activation de POP3 dans Exchange 2013: Exchange 2013 Help'
TOCTitle: Activer POP3
ms:assetid: e226a5f1-429d-4046-b925-da6cc151709e
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb124934(v=EXCHG.150)
ms:contentKeyID: 50479399
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Activation de POP3 dans Exchange 2013

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2017-03-28_

Découvrez comment activer la connectivité client POP3 dans Exchange 2016 à l’aide de Microsoft Management Console (MMC) ou d’Environnement de ligne de commande Exchange Management Shell (EMS).

Lorsque vous installez Exchange Server 2016, la connectivité du client POP3 n'est pas activée. Pour activer la connectivité du client POP3, vous devez démarrer deux services POP3 (le service Microsoft Exchange POP3 et le service de serveur principal Microsoft Exchange POP3). Une fois le service POP3 activé, Exchange 2016 accepte, sur les ports 110 et 995, des communications non sécurisées avec le client POP3 utilisant SSL (Secure Sockets Layer).

Vous gérez les services POP3 et POP3 principal sur le même ordinateur Exchange 2016 exécutant le rôle de serveur de boîte aux lettres. Dans Exchange 2016, les services d’accès au client font partie du rôle de serveur de boîte aux lettres afin que vous n’ayez plus à gérer les services séparément.

Pour plus d’informations sur la configuration des services POP3 et IMAP4, reportez-vous à [POP3 et IMAP4 dans Exchange Server 2013](pop3-and-imap4-in-exchange-server-2013-exchange-2013-help.md).

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : 2 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez la section « Autorisations POP3 et IMAP4 » dans la rubrique [Autorisations des clients et des périphériques mobiles](clients-and-mobile-devices-permissions-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.


## Que souhaitez-vous faire ?

## Utiliser Microsoft Management Console (MMC) pour activer POP3

Sur l’ordinateur exécutant le rôle serveur de boîtes aux lettres :

1.  Dans le composant logiciel enfichable **Services**, dans l'arborescence de la console, cliquez sur **Services (Local)**.

2.  Dans le volet de résultats, cliquez avec le bouton droit sur **Microsoft Exchange POP3**, puis cliquez sur **Propriétés**.

3.  Dans le volet de résultats, cliquez avec le bouton droit sur **Serveur principal Microsoft Exchange POP3**, puis cliquez sur **Propriétés**.

4.  Sous l'onglet **Général**, sous **Type de démarrage**, sélectionnez **Automatique**, puis cliquez sur **Appliquer**.

5.  Sous **État du service**, cliquez sur **Démarrer**, puis sur **OK**.

## Utiliser Environnement de ligne de commande Exchange Management Shell pour activer POP3

Sur l’ordinateur exécutant le rôle serveur de boîtes aux lettres :

1.  Paramétrez le service Microsoft Exchange POP3 de sorte qu'il démarre automatiquement.
    
    ```powershell
    Set-service msExchangePOP3 -startuptype automatic
    ```

2.  Démarrez le service Microsoft Exchange POP3.
    
    ```powershell
    Start-service msExchangePOP3
    ```

3.  Paramétrez le service Serveur principal Microsoft Exchange POP3 de sorte qu'il démarre automatiquement.
    
    ```powershell
    Set-service msExchangePOP3BE -startuptype automatic
    ```

4.  Démarrez le service Serveur principal Microsoft Exchange POP3.
    
    ```powershell
    Start-service msExchangePOP3BE
    ```

## Comment savoir si cela a fonctionné ?

Sur le serveur de boîtes aux lettres Exchange 2016, ouvrez le gestionnaire des tâches de Windows. Sous l'onglet **Services**, l'état de **MSExchangePOP3** et de **MSExchangePOP3BE** sera **En cours d'exécution** si POP3 est activé.

