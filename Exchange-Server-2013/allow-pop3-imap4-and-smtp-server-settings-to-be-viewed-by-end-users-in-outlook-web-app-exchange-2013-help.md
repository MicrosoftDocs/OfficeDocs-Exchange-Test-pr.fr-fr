---
title: 'Autor. les utlsr finals à visual. les param. de srv POP3, IMAP4 et SMTP ds OWA'
TOCTitle: Autoriser les utilisateurs finals à visualiser les paramètres de serveur POP3, IMAP4 et SMTP dans Outlook Web App
ms:assetid: bd22bf7e-3bf7-45e6-8790-919b780166f6
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Gg298947(v=EXCHG.150)
ms:contentKeyID: 50555474
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Autoriser les utilisateurs finals à visualiser les paramètres de serveur POP3, IMAP4 et SMTP dans Outlook Web App

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2012-11-28_

Si des utilisateurs se servent de POP3 ou IMAP4 pour se connecter à leurs boîtes aux lettres Microsoft Exchange Server 2013, ils doivent avoir connaissance des paramètres de serveurs appropriés pour effectuer la connexion. Après une installation par défaut d’Exchange 2013, vos utilisateurs ne peuvent pas consulter leurs propres paramètres de serveur POP3 ou IMAP4 entrants ou paramètres de serveur SMTP sortants. Cependant, vous pouvez configurer Exchange pour permettre à vos utilisateurs de consulter leurs propres paramètres à l’aide de MicrosoftOutlook Web App.

Après avoir exécuté ces procédures, vos utilisateurs peuvent consulter leurs paramètres de serveurs dans Outlook Web App, en procédant comme suit :

1.  Dans Outlook Web App, cliquez sur **Paramètres** \> **Options**.

2.  Dans **Options**, cliquez sur **Compte** \> **Mon compte** \> **Paramètres pour accès POP ou IMAP**.

Pour plus d’informations sur POP3 et IMAP4, voir [POP3 et IMAP4 dans Exchange Server 2013](pop3-and-imap4-in-exchange-server-2013-exchange-2013-help.md).

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : 5 minutes.

  - Les procédures décrites dans cette rubrique requièrent des autorisations spécifiques. Consultez chaque procédure pour savoir quelles autorisations sont nécessaires.

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..


## Que souhaitez-vous faire ?

## Utiliser l’environnement de ligne de commande Exchange Management Shell pour permettre aux utilisateurs POP3 et IMAP4 de consulter dans Outlook Web App, leurs paramètres POP3 et IMAP4 entrants

Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrées « Paramètres POP3 » et « Paramètres IMAP4 » de la rubrique [Autorisations des clients et des périphériques mobiles](clients-and-mobile-devices-permissions-exchange-2013-help.md).

Cet exemple autorise les paramètres de serveurs POP3 externes à être visualisés par les utilisateurs finaux.

```powershell
Set-PopSettings -ExternalConnectionSettings {Dublin01.Contoso.com:995:SSL}
```

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Set-PopSettings](https://technet.microsoft.com/fr-fr/library/aa997154\(v=exchg.150\)).

Cet exemple autorise les paramètres de serveurs IMAP4 externes à être visualisés par les utilisateurs finaux.

```powershell
Set-ImapSettings -ExternalConnectionSettings {Dublin01.Contoso.com:993:SSL}
```

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Set-ImapSettings](https://technet.microsoft.com/fr-fr/library/aa998252\(v=exchg.150\)).

Pour appliquer ces modifications, vous devez redémarrer les services Internet (IIS). Vous n’avez pas besoin de redémarrer les services POP3. Pour redémarrer les services Internet (IIS), dans l’invite de commandes, entrez les éléments suivants :

```powershell
iisreset
```

## Comment savoir si cela a fonctionné ?

Pour vérifier qu’Exchange a bien été configuré pour permettre à des utilisateurs de consulter leurs paramètres de serveur POP3, procédez comme suit :

1.  Exécutez la commande suivante dans l’environnement de ligne de commande Exchange Management Shell.
    
    ```powershell
    Get-PopSettings | format-list
    ```

2.  Vérifiez que la propriété *ExternalConnectionSettings* est définie.

Pour vérifier qu’Exchange a bien été configuré pour permettre à des utilisateurs de consulter leurs paramètres de serveur IMAP4, procédez comme suit :

1.  Exécutez la commande suivante dans l’environnement de ligne de commande Exchange Management Shell.
    
    ```powershell
    Get-ImapSettings | format-list
    ```

2.  Vérifiez que la propriété *ExternalConnectionSettings* est définie.

## Utiliser l’environnement de ligne de commande Exchange Management Shell pour permettre aux utilisateurs POP3 et IMAP4 de consulter dans Outlook Web App, leurs paramètres SMTP sortants

Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Connecteurs de réception » dans la rubrique [Autorisations de flux de messagerie](mail-flow-permissions-exchange-2013-help.md).

Dans cet exemple, nous autorisons les utilisateurs à consulter les paramètres de serveur SMTP internes et externes à l’aide de Outlook Web App.

```powershell
Get-ReceiveConnector "*Client Frontend*" | Set-ReceiveConnector -Fqdn Server.Contoso.com -AdvertiseClientSettings $true 
```

Pour des informations détaillées sur la syntaxe et les paramètres, voir [Set-ReceiveConnector](https://technet.microsoft.com/fr-fr/library/bb125140\(v=exchg.150\)).

## Comment savoir si cela a fonctionné ?

Pour vérifier qu’Exchange a bien été configuré pour permettre à des utilisateurs de consulter leurs paramètres de serveur SMTP, procédez comme suit :

1.  Exécutez la commande suivante dans l’environnement de ligne de commande Exchange Management Shell.
    
    ```powershell
    Get-ReceiveConnector | format-list
    ```

2.  Si la propriété *AdvertiseClientSettings* est définie à `true`, les utilisateurs peuvent afficher leurs paramètres de serveur SMTP dans Outlook Web App. Si *AdvertiseClientSettings* est défini(e) à `false`, les utilisateurs ne peuvent pas afficher leurs paramètres de serveur SMTP dans Outlook Web App.

## Pour plus d'informations

Après avoir rendu visibles les paramètres POP3, IMAP4 et SMTP aux utilisateurs finaux, vous pouvez également :

[Activer ou désactiver l’accès POP3 pour un utilisateur](enable-or-disable-pop3-access-for-a-user-exchange-2013-help.md)

[Activation ou désactivation de l'accès IMAP4 pour un utilisateur](enable-or-disable-imap4-access-for-a-user-exchange-2013-help.md)

