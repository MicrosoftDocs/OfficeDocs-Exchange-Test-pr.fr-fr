---
title: "Déf. du port d’écoute TLS sur un serveur d’accès au client: Exchange 2013 Help | Microsoft Docs"
TOCTitle: Définissez le port d'écoute TLS sur un serveur d'accès au Client
ms:assetid: f4401923-61fa-4dc5-95f8-c0d2f515b2ea
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ673576(v=EXCHG.150)
ms:contentKeyID: 50555520
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Définissez le port d'écoute TLS sur un serveur d'accès au Client

 

_**Sapplique à :** Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2013-02-17_

Vous pouvez configurer le port de Transport Layer Security (TLS) qui est utilisé pour écouter les requêtes SIP sur un serveur d'accès au Client qui exécute le service Microsoft Exchange Unified Messaging routeur d'appels. Par défaut, lorsque vous installez un serveur d'accès au Client, le numéro de port d'écoute TLS SIP est défini à 5061.

Le port d'écoute TLS doit être configuré sur 5061 pour :

  - Définir le paramètre de sécurité VoIP d'un plan de numérotation de messagerie unifiée sur Sécurisé SIP.

  - Définir le paramètre de sécurité VoIP d'un plan de numérotation de messagerie unifiée sur Sécurisé.

  - Intégrer à MicrosoftOffice Communications Server 2007 R2 ou Microsoft Lync Server.

  - Utiliser l'authentification TLS (Transport Layer Security) mutuelle pour chiffrer des données réseau entre des serveurs d'accès au client, des serveurs de boîtes aux lettres qui exécutent le service de messagerie unifiée Microsoft Exchange, et des passerelles VoIP, des PBX (Private Branch eXchanges) compatibles SIP (Session Initiation Protocol), des PBX IP ou des contrôleurs de limite de session (SBC).

Si vous souhaitez utiliser l'authentification mutual TLS entre une passerelle IP de messagerie unifiée et un plan de numérotation fonctionnant en mode sécurisé SIP ou sécurisé, lorsque vous créez la passerelle IP de messagerie unifiée, vous devez le configurer avec un nom de domaine complet (FQDN) et ensuite configurer la passerelle IP de messagerie unifiée pour écouter sur le port TLS 5061. Vous devez également vérifier que les passerelles VoIP, PBX activé pour SIP, PBX IP, ou SBC ont également été configurés pour écouter les requêtes TLS mutuelles sur le port 5061.

Vous pouvez uniquement configurer les ports TCP et TLS du serveur d'accès au client. Vous ne pouvez pas configurer les ports d'un serveur de boîtes aux lettres Exchange 2013. Toutefois, vous pouvez utiliser la cmdlet **Set-UMService** pour configurer les ports d'écoute TCP et TLS pour des serveurs de messagerie unifiée Exchange 2010.

Pour découvrir des tâches supplémentaires relatives à la messagerie unifiée et aux serveurs d'accès au client, consultez la rubrique [Procédures de services de messagerie unifiée](um-services-procedures-exchange-2013-help.md).

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : moins d'une minute.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l'entrée « Serveur d'accès au client (service de routeur d'appel de messagerie unifiée) » dans la rubrique [Autorisations de messagerie unifiée](unified-messaging-permissions-exchange-2013-help.md).

  - Vérifiez que vous avez correctement installé les serveurs d'accès au client et de boîtes aux lettres.

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..


## Que souhaitez-vous faire ?

## Utiliser le Centre d'administration Exchange (CAE) pour configurer le port d'écoute TLS sur un serveur d'accès au client

1.  Dans le CAE, accédez à **Serveurs** \> **Serveurs**.

2.  Dans l'affichage Liste, sélectionnez le serveur Exchange à modifier, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

3.  Dans la page **Exchange Server**, cliquez sur **Messagerie unifiée**.

4.  Sous **Paramètres du service de messagerie unifiée**, sous **Port d'écoute TLS**, entrez le numéro du port TLS, puis cliquez sur **Enregistrer**.

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour configurer le port d'écoute TLS sur un serveur d'accès au client

Cet exemple définit le port d'écoute TLS du serveur d'accès au client `MyClientAccessServer` sur 5561.

    Set-UMCallRouterSettings -Server MyClientAccessServer -SipTlsListeningPort 5561

