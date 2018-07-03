---
title: 'Activer ou désactiver Outlook Web App pour une boîte aux lettres: Exchange 2013 Help'
TOCTitle: Activer ou désactiver Outlook Web App pour une boîte aux lettres
ms:assetid: abc19646-6211-4f18-a060-e347452dcc53
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb124124(v=EXCHG.150)
ms:contentKeyID: 50555471
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Activer ou désactiver Outlook Web App pour une boîte aux lettres

 

_**Sapplique à :** Exchange Online, Exchange Server 2013_

_**Dernière rubrique modifiée :** 2012-11-14_

Le Centre d’administration Exchange (EAC) ou l’environnement de ligne de commande Exchange Management Shell vous permet d’activer ou de désactiver Outlook Web App pour une boîte aux lettres utilisateur. Si Outlook Web App est activé, un utilisateur peut utiliser Outlook Web App pour envoyer et recevoir un message électronique. Si Outlook Web App est désactivé, la boîte aux lettres continue de recevoir des messages électroniques et un utilisateur peut y accéder pour envoyer et recevoir des messages électroniques via un client MAPI comme Microsoft Outlook ou un client de messagerie électronique POP ou IMAP, en supposant que la boîte aux lettres soit activée pour accepter un accès de ces clients.

> [!NOTE]
> La prise en charge pour Outlook Web App et pour les clients de messagerie électronique MAPI, POP3 et IMAP4 est activée par défaut lors de la création d’une boîte aux lettres utilisateur.


Pour les tâches supplémentaires de gestion relatives à la gestion de l’accès aux clients de messagerie, consultez les rubriques suivantes :

  - [Activer ou désactiver MAPI pour une boîte aux lettres](enable-or-disable-mapi-for-a-mailbox-exchange-online-help.md)

  - [Activation ou désactivation de l'accès IMAP4 pour un utilisateur](enable-or-disable-imap4-access-for-a-user-exchange-2013-help.md)

  - [Activer ou désactiver l’accès POP3 pour un utilisateur](enable-or-disable-pop3-access-for-a-user-exchange-2013-help.md)

## Ce qu’il faut savoir avant de commencer ?

  - Durée d'exécution estimée : 2 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Paramètres utilisateur d’accès au client » dans la rubrique [Autorisations des clients et des périphériques mobiles](clients-and-mobile-devices-permissions-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..


## Que souhaitez-vous faire ?

## Utiliser le Centre d’administration Exchange (EAC) pour activer ou désactiver Outlook Web App

1.  Dans le CAE, accédez à **Destinataires**  \> **Boîtes aux lettres**.

2.  Dans la liste des boîtes aux lettres utilisateur, cliquez sur la boîte aux lettres pour laquelle vous souhaitez activer ou désactiver Outlook Web App, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

3.  Dans la page de propriétés de boîte aux lettres, cliquez sur **Fonctionnalités de boîte aux lettres**.

4.  Sous **Connectivité de messages électroniques**, sélectionnez l’une des options suivantes :
    
      - Pour désactiver Outlook Web App, sous **Outlook Web App : Activé**, cliquez sur **Désactiver**.
        
        Un message d’avertissement s’affiche pour vous demander de confirmer la désactivation de Outlook Web App. Cliquez sur **Oui**.
    
      - Pour activer Outlook Web App, sous **Outlook Web App : Désactivé**, cliquez sur **Activer**.

5.  Cliquez sur **Enregistrer** pour enregistrer votre modification.

> [!NOTE]
> Vous pouvez activer ou désactiver Outlook Web App pour plusieurs boîtes aux lettres utilisateur à l’aide de la fonction de modification en bloc du Centre d’administration Exchange (EAC). Pour plus d’informations sur comment procéder, consultez la section « Modifier en bloc des boîtes aux lettres utilisateur » dans <a href="manage-user-mailboxes-exchange-2013-help.md">Gestion des boîtes aux lettres utilisateur</a>.


## Utiliser l’environnement de ligne de commande Exchange Management Shell pour activer ou désactiver Outlook Web App

Dans cet exemple, nous désactivons Outlook Web App pour la boîte aux lettres de Yan Li.

    Set-CASMailbox -Identity "Yan Li" -OWAEnabled $false

Dans cet exemple, nous activons Outlook Web App pour la boîte aux lettres d’Elly Nkya.

    Set-CASMailbox -Identity Ellyn@contoso.com -OWAEnabled $true

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Set-CASMailbox](https://technet.microsoft.com/fr-fr/library/bb125264\(v=exchg.150\)).

## Comment savoir si cela a fonctionné ?

Pour vérifier que l’opération d’activation ou de désactivation de Outlook Web App s’est effectuée correctement pour une boîte aux lettres utilisateur, exécutez l’une des actions suivantes :

  - Dans le Centre d’administration Exchange (EAC), accédez à **Destinataires** \> **Boîtes aux lettres**, cliquez sur la boîte aux lettres, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

  - Dans la page de propriétés de boîte aux lettres, cliquez sur **Fonctionnalités de boîte aux lettres**.

  - Sous **Connectivité de messages électroniques**, vérifiez si Outlook Web App est activé ou désactivé.

Ou

  - Exécutez la commande suivante dans l’environnement de ligne de commande Exchange Management Shell.
    
        Get-CASMailbox <identity>
    
    Si Outlook Web App est activé, la valeur pour la propriété *OWAEnabled* est `True`. Si Outlook Web App est désactivé, la valeur est `False`.

