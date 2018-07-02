---
title: 'Démarrage et arrêt des services POP3: Exchange 2013 Help'
TOCTitle: Démarrage et arrêt des services POP3
ms:assetid: 3d543921-d8c9-4d4b-99a1-82446b585ceb
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Aa997475(v=EXCHG.150)
ms:contentKeyID: 50477965
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Démarrage et arrêt des services POP3

 

_**Sapplique à :**Exchange Server 2013_

_**Dernière rubrique modifiée :**2013-03-13_

Par défaut, les deux services POP3 (service Microsoft Exchange POP3 et service de serveur principal Microsoft Exchange POP3) ne sont pas démarrés sur les ordinateurs exécutant MicrosoftExchange Server 2013. Vous devez démarrer ces deux services pour permettre à vos clients de messagerie de se connecter à Exchange à l'aide de POP3. Une fois ces services démarrés, Exchange 2013 accepte les communications non sécurisées des clients POP3 sur le port 110 et sur le port 995 utilisant SSL (Secure Sockets Layer).

Le service Microsoft Exchange POP3 s'exécute sur des ordinateurs Exchange 2013 qui exécutent le rôle serveur d'accès au client. Le service de serveur principal Microsoft Exchange POP3 s'exécute sur l'ordinateur Exchange 2013 qui exécute le rôle serveur de boîtes aux lettres. Dans des environnements dans lesquels les rôles d'accès au client et de boîtes aux lettres sont exécutés sur le même ordinateur, vous gérez les deux services sur le même ordinateur.

Pour plus d'informations sur POP3 et IMAP4, consultez la rubrique [POP3 et IMAP4 dans Exchange Server 2013](pop3-and-imap4-in-exchange-server-2013-exchange-2013-help.md).

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : 2 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez la section « Autorisations POP3 et IMAP4 » dans la rubrique [Autorisations des clients et des périphériques mobiles](clients-and-mobile-devices-permissions-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

<table>
<thead>
<tr class="header">
<th><img src="images/Bb125224.tip(EXCHG.150).gif" title="Conseil" alt="Conseil" />Conseil :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..</td>
</tr>
</tbody>
</table>


## Que souhaitez-vous faire ?

## Utiliser le composant logiciel enfichable des services la console de gestion Microsoft pour démarrer et arrêter les services POP3

Pour démarrer les services POP3 :

1.  Sur l'ordinateur exécutant le rôle serveur d'accès au client, cliquez sur **Démarrer**, puis **Programmes**, **Outils d'administration** et **Services**. Cliquez avec le bouton droit sur **Microsoft Exchange POP3**, puis cliquez sur **Démarrer**.

2.  Sur l'ordinateur exécutant le rôle serveur de boîtes aux lettres, cliquez sur **Démarrer**, puis **Programmes**, **Outils d'administration** et **Services**. Dans le volet de résultats, cliquez avec le bouton droit sur **Serveur principal Microsoft Exchange POP3**, puis cliquez sur **Démarrer**.

Pour arrêter les services POP3 :

1.  Sur l'ordinateur exécutant le rôle serveur d'accès au client, cliquez sur **Démarrer**, puis **Programmes**, **Outils d'administration** et **Services**. Cliquez avec le bouton droit sur **Microsoft Exchange POP3**, puis cliquez sur **Arrêter**.

2.  Sur l'ordinateur exécutant le rôle serveur de boîtes aux lettres, cliquez sur **Démarrer**, puis **Programmes**, **Outils d'administration** et **Services**. Cliquez avec le bouton droit sur **Serveur principal Microsoft Exchange POP3**, puis cliquez sur **Arrêter**.

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour démarrer ou arrêter les services POP3

Pour démarrer les services POP3 :

1.  Sur l'ordinateur qui exécute le rôle serveur d'accès au client, à partir de l'environnement de ligne de commande Exchange Management Shell, exécutez la commande suivante pour démarrer le service Microsoft Exchange POP3.
    
        Start-service MSExchangePOP3

2.  Sur l'ordinateur qui exécute le rôle serveur de boîtes aux lettres, à partir de l'environnement de ligne de commande Exchange Management Shell, exécutez la commande suivante pour démarrer le service de serveur principal Microsoft Exchange POP3.
    
        Start-service MSExchangePOP3BE

Pour arrêter les services POP3 :

1.  Sur l'ordinateur qui exécute le rôle serveur d'accès au client, à partir de l'environnement de ligne de commande Exchange Management Shell, exécutez la commande suivante pour arrêter le service Microsoft Exchange POP3.
    
        Stop-service MSExchangePOP3

2.  Sur l'ordinateur qui exécute le rôle serveur de boîtes aux lettres, à partir de l'environnement de ligne de commande Exchange Management Shell, exécutez la commande suivante pour arrêter le service de serveur principal Microsoft Exchange POP3.
    
        Stop-service MSExchangePOP3BE

## Utiliser la commande net start pour démarrer ou arrêter les services POP3

Pour démarrer les services POP3 :

1.  Sur l'ordinateur qui exécute le rôle serveur d'accès au client, depuis l'invite de commandes, exécutez la commande suivante pour démarrer le service Microsoft Exchange POP3.
    
        Net Start msExchangePOP3

2.  Sur l'ordinateur qui exécute le rôle serveur de boîtes aux lettres, depuis l'invite de commandes, exécutez la commande suivante pour démarrer le service de serveur principal Microsoft Exchange POP3.
    
        Net Start msExchangePOP3BE

Pour arrêter les services POP3 :

1.  Sur l'ordinateur qui exécute le rôle serveur d'accès au client, depuis l'invite de commandes, exécutez la commande suivante pour arrêter le service Microsoft Exchange POP3.
    
        Net Stop MSExchangePOP3

2.  Sur l'ordinateur qui exécute le rôle serveur de boîtes aux lettres, depuis l'invite de commandes, exécutez la commande suivante pour arrêter le service de serveur principal Microsoft Exchange POP3.
    
        Net Stop MSExchangePOP3BE

## Comment savoir si cela a fonctionné ?

1.  Sur le serveur d'accès au client Exchange, ouvrez le gestionnaire des tâches de Windows. Dans l'onglet **Services**, l'état de **MSExchangePOP3** affiche **En cours d'exécution** si le service Microsoft Exchange POP3 est exécuté.

2.  Sur le serveur de boîtes aux lettres Exchange, ouvrez le gestionnaire des tâches de Windows. Dans l'onglet **Services**, l'état de **MSExchangePOP3BE** affiche **En cours d'exécution** si le service de serveur principal Microsoft Exchange POP3 est exécuté.

