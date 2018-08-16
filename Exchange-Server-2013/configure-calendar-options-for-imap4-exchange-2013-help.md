---
title: 'Configurer les options de calendrier pour IMAP4: Exchange 2013 Help'
TOCTitle: Configurer les options de calendrier pour IMAP4
ms:assetid: 6679c8b2-3f0f-449a-a17c-a7b30001538c
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Aa998606(v=EXCHG.150)
ms:contentKeyID: 50555421
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configurer les options de calendrier pour IMAP4

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2012-11-27_

Vous pouvez utiliser l’environnement de ligne de commande Exchange Management Shell pour configurer les paramètres d’accès au calendrier des utilisateurs qui se connectent à leurs boîtes aux lettres à l’aide de connexions IMAP4. Les paramètres que vous spécifiez déterminent la manière dont vos utilisateurs IMAP4 peuvent accéder à leur calendrier et échangent des informations de calendrier (par exemple, envoyer ou répondre à une demande de réunion) avec d’autres utilisateurs.

Pour de plus amples informations sur IMAP4, consultez la rubrique [POP3 et IMAP4 dans Exchange Server 2013](pop3-and-imap4-in-exchange-server-2013-exchange-2013-help.md).

## Ce qu’il faut savoir avant de commencer ?

  - Durée d'exécution estimée : 5 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Paramètres IMAP4 » dans la rubrique [Autorisations des clients et des périphériques mobiles](clients-and-mobile-devices-permissions-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..


## Utilisation du Shell pour définir les options de calendrier pour IMAP4

Cet exemple permet aux utilisateurs IMAP4 d’utiliser la norme iCalendar, une norme d’échange d’informations de calendrier.

    Set-ImapSettings -Identity CAS01 -CalendarItemRetrievalOption iCalendar

Cet exemple permet aux utilisateurs IMAP4 d’accéder aux informations de calendrier à partir d’un serveur interne.

    Set-ImapSettings -Identity CAS01 -CalendarItemRetrievalOption IntranetUrl 

Cet exemple montre comment permettre aux utilisateurs IMAP4 d’accéder aux informations de calendrier à partir d’Internet sur un serveur externe.

    Set-ImapSettings -CalendarItemRetrievalOption InternetUrl

Cet exemple permet aux utilisateurs IMAP4 d’accéder aux informations de calendrier à l’aide d’une URL Outlook Web App directe. Si vous utilisez `Custom`, vous devez spécifier une URL Outlook Web App à l’aide du paramètre *OWAServerUrl*.

    Set-Imap4Settings -CalendarItemRetrievalOption Custom -OwaServerUrl "https://OwaServer01"

Une fois les options de calendrier spécifiées pour IMAP4, vous devez redémarrer les services IMAP4. Pour plus d’informations sur le redémarrage des services IMAP4, consultez la rubrique [Démarrer et arrêter les services IMAP4](start-and-stop-the-imap4-services-exchange-2013-help.md).

Pour plus d'informations sur la syntaxe et les paramètres, voir [Set-ImapSettings](https://technet.microsoft.com/fr-fr/library/aa998252\(v=exchg.150\)).

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez bien défini les options de calendrier, procédez comme suit :

Exécutez la commande suivante dans l’environnement de ligne de commande Exchange Management Shell.

    Get-ImapSettings | format-list

Vérifiez que les paramètres du calendrier sont corrects.

## Pour plus d'informations

Une fois que vous avez défini les options de calendrier pour IMAP4, vous pouvez également :

[Configurer les options de format d’extraction de message POP3 et IMAP4](configure-pop3-and-imap4-message-retrieval-format-options-exchange-2013-help.md)

[Définir les limites de délai d’expiration de connexion pour IMAP4](set-connection-time-out-limits-for-imap4-exchange-2013-help.md)

