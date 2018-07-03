---
title: "Réinitialisation à distance d'un téléphone mobile: Exchange 2013 Help"
TOCTitle: Réinitialisation à distance d'un téléphone mobile
ms:assetid: 67ba838e-031d-4a98-b277-170683b6f520
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Aa998614(v=EXCHG.150)
ms:contentKeyID: 52057093
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Réinitialisation à distance d'un téléphone mobile

 

_**Sapplique à :** Exchange Online, Exchange Server 2013_

_**Dernière rubrique modifiée :** 2013-02-06_

Vos utilisateurs transportent chaque jour des informations confidentielles dans leurs poches. Si l'un d'entre eux perd son téléphone mobile, vos données peuvent passer entre les mains d'une autre personne. Si le cas se présente, vous pouvez utiliser le Centre d'administration Exchange (CAE) ou l'environnement de ligne de commande Exchange Management Shell pour réinitialiser son téléphone et effacer toutes les données de l'utilisateur et de l'entreprise.

> [!NOTE]
> Cette rubrique contient également des instructions sur l'utilisation de MicrosoftOutlook Web App pour effectuer une réinitialisation à distance sur un téléphone. L'utilisateur doit être connecté à Outlook Web App pour effectuer un nettoyage à distance.


## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : 5 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l'entrée « Appareils mobiles » dans la rubrique [Autorisations des clients et des périphériques mobiles](clients-and-mobile-devices-permissions-exchange-2013-help.md).

  - Cette procédure permet d'effacer toutes les données présentes sur un téléphone mobile, y compris les applications installées, les photos et les informations personnelles.

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..


## Que souhaitez-vous faire ?

## Utiliser le Centre d'administration Exchange pour réinitialiser le téléphone d'un utilisateur

Vous pouvez utiliser le CAE pour réinitialiser le téléphone d'un utilisateur ou annuler une réinitialisation à distance qui n'est pas encore terminée.

1.  Dans le CAE, accédez à **Destinataires** \> **Boîtes aux lettres**.

2.  Sélectionnez l'utilisateur, puis sous **Appareils mobiles**, sélectionnez **Afficher les détails**.

3.  Dans la page **Paramètres de l'appareil mobile**, sélectionnez l'appareil mobile qui a été perdu, puis sélectionnez **Supprimer toutes les données**.

4.  Cliquez sur **Enregistrer**.

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour réinitialiser le téléphone d'un utilisateur

Vous pouvez utiliser la cmdlet **Clear-MobileDevice** dans l'environnement de ligne de commande Exchange Management Shell pour réinitialiser le téléphone d'un utilisateur.

La commande suivante réinitialise l'appareil nommé WM\_TonySmith et envoie un message de confirmation à admin@contoso.com.

    Clear-MobileDevice -Identity WM_TonySmith -NotificationEmailAddresses "admin@contoso.com"

## Utiliser Outlook Web App pour réinitialiser le téléphone d'un utilisateur

Vos utilisateurs peuvent réinitialiser leur téléphone à l'aide d'Outlook Web App.

1.  Dans Outlook Web App, sélectionnez **Paramètres \> Téléphone \> Appareils mobiles**.

2.  Sélectionnez le téléphone mobile.

3.  Cliquez ou appuyez sur l'icône **Réinitialiser l'appareil**.

## Comment savoir si cela a fonctionné ?

Différentes méthodes permettent de vérifier que la réinitialisation à distance a fonctionné.

  - Exécutez la cmdlet **Clear-MobileDevice** avec le paramètre *–NotificationEmailAddresses* configuré. Un message est envoyé à l'adresse de messagerie indiquée lorsque la réinitialisation à distance est terminée.

  - Dans le CAE, vérifiez l'état de l'appareil mobile. L'état doit changer de **Effacement en attente** à **Données supprimées**.

  - Dans Outlook Web App, vérifiez l'état de l'appareil mobile. L'état doit changer de **Effacement en attente** à **Données supprimées**.

