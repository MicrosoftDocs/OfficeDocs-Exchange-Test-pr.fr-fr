---
title: 'Définir les limites de délai d’exp. de connexion d’IMAP4: Exchange 2013 Help | Microsoft Docs'
TOCTitle: Définir les limites de délai d’expiration de connexion pour IMAP4
ms:assetid: 6b6a5bd1-a878-4a70-8e21-14d5042a58f1
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Aa998665(v=EXCHG.150)
ms:contentKeyID: 50555423
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Définir les limites de délai d’expiration de connexion pour IMAP4

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2012-11-28_

Vous pouvez utiliser le Centre d’administration Exchange ou l’environnement de ligne de commande Exchange Management pour configurer les limites de délai de connexion pour les connexions IMAP4 inactives authentifiées et non authentifiées.

Pour de plus amples informations sur IMAP4, consultez la rubrique [POP3 et IMAP4 dans Exchange Server 2013](pop3-and-imap4-in-exchange-server-2013-exchange-2013-help.md).

## Ce qu’il faut savoir avant de commencer ?

  - Durée d'exécution estimée : 5 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Paramètres IMAP4 » dans la rubrique [Autorisations des clients et des périphériques mobiles](clients-and-mobile-devices-permissions-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..


## Que souhaitez-vous faire ?

## Définition des limites de délai de connexion pour IMAP4 à l’aide du Centre d’administration Exchange (CAE)

1.  Dans le Centre d’administration Exchange, rendez-vous sur **Serveurs** **\>** **Serveurs**.

2.  Dans la liste des serveurs, sélectionnez le serveur d’accès au client, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

3.  Sur la page des propriétés du serveur, cliquez sur **IMAP4**.

4.  Faites défiler vers le bas, puis cliquez sur **Plus d’options**.

5.  Sous **Paramètres de délai d’attente**, utilisez les paramètres suivants :
    
      - **Délai d’attente authentifié (secondes)**    Indique le délai d’attente avant la fermeture d’une connexion authentifiée inactive. La valeur par défaut est 1 800. Les valeurs possibles sont comprises entre 30 et 86 400.
    
      - **Délai d’accès non authentifié (secondes)**    Indique le délai d’attente avant la fermeture d’une connexion inactive non authentifiée. La valeur par défaut est 60. Les valeurs possibles sont comprises entre 30 et 3 600.

6.  Cliquez sur **Appliquer**, puis sur **OK** pour enregistrer les modifications.

Une fois que vous avez défini les limites de délai de connexion pour IMAP4, vous devez redémarrer les services IMAP4 pour que les paramètres prennent effet. Pour plus d’informations sur le redémarrage des services IMAP4, consultez la rubrique [Démarrer et arrêter les services IMAP4](start-and-stop-the-imap4-services-exchange-2013-help.md).

## Utiliser l’environnement de ligne de commande Exchange Management Shell pour définir des limites de délai d’expiration de connexion pour IMAP4

Cet exemple définit la limite de délai de connexion pour les connexions authentifiées inactives.

    Set -ImapSettings -Identity CAS01 -AuthenticatedConnectionTimeout TimeValue

Cet exemple définit la limite de délai de connexion pour les connexions non authentifiées inactives.

    Set -ImapSettings -Identity CAS01 -PreAuthenticatedConnectionTimeout TimeValue

Une fois que vous avez défini les limites de délai de connexion pour IMAP4, vous devez redémarrer les services IMAP4 pour que les paramètres prennent effet. Pour plus d’informations sur le redémarrage des services IMAP4, consultez la rubrique [Démarrer et arrêter les services IMAP4](start-and-stop-the-imap4-services-exchange-2013-help.md).

Pour plus d’informations sur la syntaxe et les paramètres, voir [Set-ImapSettings](https://technet.microsoft.com/fr-fr/library/aa998252\(v=exchg.150\)).

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez bien défini les limites de connexion, procédez de l’une des manières suivantes :

1.  Dans le Centre d’administration Exchange, rendez-vous sur **Serveurs** **\>** **Serveurs**.

2.  Dans la liste des serveurs, sélectionnez le serveur d’accès au client, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

3.  Sur la page des propriétés du serveur, cliquez sur **IMAP4**.

4.  Faites défiler vers le bas, puis cliquez sur **Plus d’options**.

5.  Sous **Paramètres de délai d’attente**, vérifiez que les paramètres de connexion sont corrects.

Ou

1.  Exécutez la commande suivante dans l’environnement de ligne de commande Exchange Management Shell.
    
        Get-ImapSettings | format-list

2.  Vérifiez que les paramètres de connexion sont corrects.

## Pour plus d'informations

Après avoir défini les limites de délai d’expiration d’authentification pour IMAP4, vous voudrez probablement :

[Activation d’IMAP4 dans Exchange 2016](enable-imap4-in-exchange-2013-exchange-2013-help.md)

[Définir les limites de connexion pour IMAP4](set-connection-limits-for-imap4-exchange-2013-help.md)

