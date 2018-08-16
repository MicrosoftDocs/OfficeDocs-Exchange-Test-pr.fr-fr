---
title: 'Activ. ou désactiv. l’accès IMAP4 pr un utilisateur: Exchange 2013 Help'
TOCTitle: Activation ou désactivation de l'accès IMAP4 pour un utilisateur
ms:assetid: a685fae4-b6f1-42fe-8bdc-5f99f9617799
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb676481(v=EXCHG.150)
ms:contentKeyID: 50478828
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Activation ou désactivation de l'accès IMAP4 pour un utilisateur

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2013-01-18_

Vous pouvez activer ou désactiver IMAP4 pour un utilisateur.

> [!NOTE]
> Après avoir activé ou désactivé IMAP4 pour un utilisateur, vous devez redémarrer le service Microsoft Exchange IMAP4 et le service Microsoft Exchange IMAP4 Backend. Pour plus d'informations sur le redémarrage du service IMAP4, consultez la rubrique <a href="start-and-stop-the-imap4-services-exchange-2013-help.md">Démarrer et arrêter les services IMAP4</a>.


Pour plus d'informations sur la gestion des boîtes aux lettres utilisateur, reportez-vous à la rubrique [Gestion des boîtes aux lettres utilisateur](manage-user-mailboxes-exchange-2013-help.md).

Pour plus d'informations sur POP3 et IMAP4, consultez la rubrique [POP3 et IMAP4 dans Exchange Server 2013](pop3-and-imap4-in-exchange-server-2013-exchange-2013-help.md).

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : 2 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez la section « Autorisations de configuration des destinataires » dans la rubrique [Autorisations des destinataires](recipients-permissions-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..


## Que souhaitez-vous faire ?

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour activer ou désactiver IMAP4 pour un utilisateur

1.  Dans le CAE, accédez à **Destinataires**  \> **Boîtes aux lettres**.

2.  Dans le volet Résultats, sélectionnez l'utilisateur pour lequel vous souhaitez activer ou désactiver IMAP4, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

3.  Dans la boîte de dialogue **Boîte aux lettres utilisateur**, dans l'arborescence de la console, cliquez sur **Fonctionnalités de boîte aux lettres**.
    
    Dans le volet Résultats, sous **Connectivité de messagerie**, effectuez l'une des opérations suivantes :
    
      - Pour désactiver IMAP4 pour l'utilisateur, sous **IMAP4 : Activé**, cliquez sur **Désactiver**.
    
      - Pour activer IMAP4 pour l'utilisateur, sous **IMAP4 : Désactivé**, cliquez sur **Activer**.

4.  Cliquez sur **Enregistrer**.

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour activer ou désactiver IMAP4 pour un utilisateur

Cet exemple active IMAP4 pour l'utilisateur John Smith.

    Set-CASMailbox -Identity "John Smith" -IMAPEnabled $true

Cet exemple désactive IMAP4 pour l'utilisateur John Smith.

    Set-CASMailbox -Identity "John Smith" -IMAPEnabled $false

## Comment savoir si cela a fonctionné ?

1.  Dans le CAE, accédez à **Destinataires**  \> **Boîtes aux lettres**.

2.  Dans le volet Résultats, sélectionnez l'utilisateur pour lequel vous souhaitez activer ou désactiver IMAP4, puis cliquez sur **Modifier**.

3.  Dans la boîte de dialogue **Boîte aux lettres utilisateur**, dans l'arborescence de la console, cliquez sur **Fonctionnalités de boîte aux lettres**.
    
    Dans le volet Résultats, examinez le champ **Connectivité de messagerie**.
    
      - Si IMAP4 est activé pour l'utilisateur, vous verrez **IMAP4 : Activé**.
    
      - Si IMAP4 n'est pas activé pour l'utilisateur, vous verrez **IMAP4 : Désactivé**.

4.  Cliquez sur **Enregistrer**.

