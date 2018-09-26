---
title: 'Démarrer et arrêter les services IMAP4: Exchange 2013 Help'
TOCTitle: Démarrer et arrêter les services IMAP4
ms:assetid: a52db4bd-69a6-47b2-acf3-d9d8571c7a87
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb124022(v=EXCHG.150)
ms:contentKeyID: 50478942
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Démarrer et arrêter les services IMAP4

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2012-10-05_

Par défaut, les deux services IMAP4, Microsoft Exchange IMAP4 service et le service IMAP4 principal de Microsoft Exchange, ne sont pas démarrés sur les ordinateurs exécutant MicrosoftExchange Server 2013. Vous devez démarrer ces deux services pour permettre à vos clients de messagerie de se connecter à Exchange à l'aide d'IMAP4. Une fois que vous avez activé ces services, Exchange 2013 accepte les communications non sécurisées de clients IMAP4 sur le port 143 et sur le port 993 en utilisant Secure Sockets Layer (SSL).

Le service Microsoft Exchange IMAP4 s'exécute sur des ordinateurs Exchange 2013 qui exécutent le rôle de serveur d'accès au client. Le service de serveur principal Microsoft Exchange IMAP4 s'exécute sur des ordinateurs Exchange 2013 qui exécutent le rôle de serveur de boîte aux lettres. Dans des environnements dans lesquels les rôles d’accès au client et de boîtes aux lettres sont exécutés sur le même ordinateur, vous gérez les deux services sur le même ordinateur.

Pour plus d’informations sur POP3 et IMAP4, voir [POP3 et IMAP4 dans Exchange Server 2013](pop3-and-imap4-in-exchange-server-2013-exchange-2013-help.md).

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : 2 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez la section « Autorisations POP3 et IMAP4 » dans la rubrique [Autorisations des clients et des périphériques mobiles](clients-and-mobile-devices-permissions-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..


## Que souhaitez-vous faire ?

## Utiliser le composant logiciel enfichable des services la console de gestion Microsoft pour démarrer ou arrêter le service IMAP4

Pour démarrer les services IMAP4 :

1.  Sur l’ordinateur exécutant le rôle serveur d’accès au client, cliquez sur **Démarrer**, puis **Programmes**, **Outils d’administration** et **Services**. Cliquez avec le bouton droit sur **Microsoft Exchange IMAP4**, puis cliquez sur **Démarrer**.

2.  Sur l’ordinateur exécutant le rôle serveur de boîtes aux lettres, cliquez sur **Démarrer**, puis **Programmes**, **Outils d’administration** et **Services**. Cliquez avec le bouton droit sur **IMAP4 principal de Microsoft Exchange**, puis cliquez sur **Démarrer**.

Pour arrêter les services IMAP4 :

1.  Sur l’ordinateur exécutant le rôle serveur d’accès au client, cliquez sur **Démarrer**, puis **Programmes**, **Outils d’administration** et **Services**. Cliquez avec le bouton droit sur **Microsoft Exchange IMAP4**, puis cliquez sur **Arrêter**.

2.  Sur l’ordinateur exécutant le rôle serveur de boîtes aux lettres, cliquez sur **Démarrer**, puis **Programmes**, **Outils d’administration** et **Services**. Cliquez avec le bouton droit sur **IMAP4 principal de Microsoft Exchange**, puis cliquez sur **Arrêter**.

## Utiliser le Shell pour démarrer ou arrêter les services IMAP4

Pour démarrer les services IMAP4 :

1.  Sur l'ordinateur exécutant le rôle de serveur d'accès au client, à partir du Shell, exécutez la commande suivante pour démarrer le service Microsoft Exchange IMAP4.
    
    ```powershell
    Start-service msExchangeIMAP4
    ```

2.  Sur l'ordinateur exécutant le rôle de serveur de boîtes aux lettres, à partir du Shell, exécutez la commande suivante pour démarrer le service IMAP4 principal de Microsoft Exchange.
    
    ```powershell
    Start-service msExchangeIMAP4BE
    ```

Pour arrêter les services IMAP4 :

1.  Sur l'ordinateur exécutant le rôle de serveur d'accès au client, à partir du Shell, exécutez la commande suivante pour arrêter le service Microsoft Exchange IMAP4.
    
    ```powershell
    Stop-service msExchangeIMAP4
    ```

2.  Sur l'ordinateur exécutant le rôle de serveur de boîtes aux lettres, à partir du Shell, exécutez la commande suivante pour arrêter le service IMAP4 principal de Microsoft Exchange.
    
    ```powershell
    Stop-service msExchangeIMAP4BE
    ```

## Utiliser la commande net start pour démarrer ou arrêter les services IMAP4

Pour démarrer les services IMAP4 :

1.  Sur l'ordinateur exécutant le rôle de serveur d'accès au client, depuis l’invite de commandes, exécutez la commande suivante pour démarrer le service Microsoft Exchange IMAP4.
    
    ```powershell
    net start msExchangeIMAP4
    ```

2.  Sur l'ordinateur exécutant le rôle de serveur de boîtes aux lettres, depuis l’invite de commandes, exécutez la commande suivante pour démarrer le service IMAP4 principal de Microsoft Exchange.
    
    ```powershell
    net start msExchangeIMAP4BE
    ```

Pour arrêter les services IMAP4 :

1.  Sur l'ordinateur exécutant le rôle de serveur d'accès au client, depuis l’invite de commandes, exécutez la commande suivante pour arrêter le service Microsoft Exchange IMAP4.
    
    ```powershell
    Net Stop MSExchangeIMAP4
    ```

2.  Sur l'ordinateur exécutant le rôle de serveur de boîtes aux lettres, depuis l’invite de commandes, exécutez la commande suivante pour arrêter le service IMAP4 principal de Microsoft Exchange.
    
    ```powershell
    Net Stop MSExchangeIMAP4BE
    ```

## Comment savoir si cela a fonctionné ?

1.  Sur le serveur d’accès au client Exchange, ouvrez le gestionnaire des tâches de Windows. Dans l'onglet **Services**, l’état de **MSExchangeIMAP4** affiche **En cours d’exécution** si le service Microsoft Exchange IMAP4 est exécuté.

2.  Sur le serveur de boîtes aux lettres Exchange, ouvrez le gestionnaire des tâches de Windows. Dans l'onglet **Services**, l’état de **MSExchangeIMAP4BE** affiche **En cours d’exécution** si le service IMAP4 principal de Microsoft Exchange est exécuté.