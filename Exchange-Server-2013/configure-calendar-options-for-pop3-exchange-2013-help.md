---
title: 'Configurer les options de calendrier pour POP3: Exchange 2013 Help'
TOCTitle: Configurer les options de calendrier pour POP3
ms:assetid: ac3d60a0-8697-4c06-9e93-f8d2c4b157b6
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb124133(v=EXCHG.150)
ms:contentKeyID: 50555473
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configurer les options de calendrier pour POP3

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2012-11-27_

L’environnement de ligne de commande Exchange Management Shell vous permet de configurer des paramètres d’accès au calendrier pour vos utilisateurs qui se connectent à leurs boîtes aux lettres via des connexions POP3. Les paramètres que vous spécifiez déterminent la manière dont vos utilisateurs POP3 peuvent accéder à leur calendrier et échanger des informations de calendrier (par exemple, organiser ou répondre à une demande de réunion) avec d’autres utilisateurs.

Pour plus d’informations sur POP3, voir [POP3 et IMAP4 dans Exchange Server 2013](pop3-and-imap4-in-exchange-server-2013-exchange-2013-help.md).

## Ce qu’il faut savoir avant de commencer ?

  - Durée d'exécution estimée : 5 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Paramètres POP3 » dans la rubrique [Autorisations des clients et des périphériques mobiles](clients-and-mobile-devices-permissions-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..


## Utiliser l'environnement de ligne de commande Exchange Management shell pour définir les options de calendrier pour POP3

Dans cet exemple, nous permettons à des utilisateurs POP3 d’utiliser la norme iCalendar, il s’agit d’une norme dédiée à l’échange d’informations de calendrier.

```powershell
Set-PopSettings -Identity CAS01 -CalendarItemRetrievalOption iCalendar
```

Dans cet exemple, nous permettons à des utilisateurs POP3 d’accéder aux informations de calendrier à partir d’un serveur interne.

    Set-PopSettings -Identity CAS01 -CalendarItemRetrievalOption IntranetUrl 

Cet exemple permet aux utilisateurs POP3 d'accéder aux informations de calendrier à partir d'Internet sur un serveur externe.

```powershell
Set-PopSettings -CalendarItemRetrievalOption InternetUrl
```

Dans cet exemple, nous permettons à des utilisateurs POP3 d’accéder aux informations de calendrier à l’aide d’une adresse URL Outlook Web App directe. Si vous utilisez `Custom`, vous devez spécifier une adresse URL Outlook Web App à l’aide du paramètre *OWAServerUrl*.

```powershell
Set-PopSettings -CalendarItemRetrievalOption Custom -OwaServerUrl "https://OwaServer01"
```

Une fois les options de calendrier spécifiées pour POP3, vous devez redémarrer les services POP3. Pour plus d’informations sur le redémarrage des services POP3, consultez la rubrique [Démarrage et arrêt des services POP3](start-and-stop-the-pop3-services-exchange-2013-help.md).

Pour plus d'informations sur la syntaxe et les paramètres, voir [Set-PopSettings](https://technet.microsoft.com/fr-fr/library/aa997154\(v=exchg.150\)).

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez correctement défini des options de calendrier, procédez comme suit :

Exécutez la commande suivante dans l’environnement de ligne de commande Exchange Management Shell.

```powershell
Get-PopSettings | format-list
```

Vérifiez que les paramètres de calendrier sont correctes.

## Pour plus d'informations

Une fois que vous avez défini les options de calendrier pour POP3, vous pouvez également :

[Configurer les options de format d’extraction de message POP3 et IMAP4](configure-pop3-and-imap4-message-retrieval-format-options-exchange-2013-help.md)

[Définir les limites de délai d’expiration de connexion pour POP3](set-connection-time-out-limits-for-pop3-exchange-2013-help.md)

