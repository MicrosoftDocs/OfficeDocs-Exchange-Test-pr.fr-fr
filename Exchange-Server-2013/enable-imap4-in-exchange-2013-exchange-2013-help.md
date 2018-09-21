---
title: 'Activation d’IMAP4 dans Exchange 2016: Exchange 2013 Help'
TOCTitle: Activation d’IMAP4 dans Exchange 2016
ms:assetid: c1ae10dd-14da-4400-b38d-2aeafde8abe6
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb124489(v=EXCHG.150)
ms:contentKeyID: 50479136
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Activation d’IMAP4 dans Exchange 2016

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2016-06-02_

Découvrez comment activer la connectivité client IMAP4 dans Exchange 2016 à l’aide de Microsoft Management Console (MMC) ou d’Environnement de ligne de commande Exchange Management Shell (EMS).

Lorsque vous installez Exchange Server 2016, la connectivité client IMAP4 n’est pas activée. Pour l’activer, vous devez démarrer deux services IMAP, le service Microsoft Exchange IMAP4 et le service de serveur principal Microsoft Exchange IMAP4. Une fois que vous avez activé le service IMAP4, Exchange 2016 accepte les communications non sécurisées des clients IMAP4 sur le port 143 et sur le port 993 à l’aide du protocole SSL (Secure Sockets Layer).

Vous gérez les services IMAP4 et IMAP4 principal sur le même ordinateur Exchange 2016 exécutant le rôle de serveur de boîte aux lettres. Dans Exchange 2016, les services d’accès au client font partie du rôle de serveur de boîte aux lettres afin que vous n’ayez plus à gérer les services séparément.

Pour plus d’informations sur la configuration des services POP3 et IMAP4, reportez-vous à [POP3 et IMAP4 dans Exchange Server 2013](pop3-and-imap4-in-exchange-server-2013-exchange-2013-help.md).

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : 2 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez la section « Autorisations POP3 et IMAP4 » dans la rubrique [Autorisations des clients et des périphériques mobiles](clients-and-mobile-devices-permissions-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.


## Que souhaitez-vous faire ?

## Utiliser Microsoft Management Console (MMC) pour activer IMAP4

Sur l’ordinateur exécutant le rôle serveur de boîtes aux lettres :

1.  Dans le composant logiciel enfichable **Services**, dans l’arborescence de la console, cliquez sur **Services (Local)**.

2.  Dans le volet de résultats, cliquez avec le bouton droit de la souris sur **Microsoft Exchange IMAP4**, puis cliquez sur **Propriétés**.

3.  Dans le volet de résultats, cliquez avec le bouton droit de la souris sur **IMAP4 principal de Microsoft Exchange IMAP4**, puis cliquez sur **Propriétés**.

4.  Sous l’onglet **Général**, sous **Type de démarrage**, sélectionnez **Automatique**, puis cliquez sur **Appliquer**.

5.  Sous **État du service**, cliquez sur **Démarrer**, puis sur **OK**.

## Utiliser Environnement de ligne de commande Exchange Management Shell pour activer IMAP4

Sur l’ordinateur exécutant le rôle serveur de boîtes aux lettres :

1.  Définissez le service Microsoft Exchange IMAP4 pour qu’il démarre automatiquement.
    
    ```powershell
Set-service msExchangeIMAP4 -startuptype automatic
```

2.  Démarrez le service Microsoft Exchange IMAP4.
    
    ```powershell
Start-service msExchangeIMAP4
```

3.  Définissez le service du serveur principal de Microsoft Exchange IMAP4 pour qu’il démarre automatiquement.
    
    ```powershell
Set-service msExchangeIMAP4BE -startuptype automatic
```

4.  Démarrez le service du serveur principal Microsoft Exchange IMAP4.
    
    ```powershell
Start-service msExchangeIMAP4BE
```

## Comment savoir si cela a fonctionné ?

Sur le serveur de boîtes aux lettres Exchange 2016, ouvrez le gestionnaire des tâches de Windows. Dans l’onglet **Services**, l’état de **MSExchangeIMAP4** et de **MSExchangeIMAP4BE** sera **En cours d’exécution** si IMAP4 est activé.

