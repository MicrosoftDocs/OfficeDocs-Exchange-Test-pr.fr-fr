---
title: 'Désactivation du chiffrement TLS entre des sites Active Directory: Exchange 2013 Help'
TOCTitle: Désactivation du chiffrement TLS entre des sites Active Directory
ms:assetid: 1e1a0acf-24e7-4f94-9b33-603a4e0a812c
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dd876856(v=EXCHG.150)
ms:contentKeyID: 52062943
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Désactivation du chiffrement TLS entre des sites Active Directory

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2013-02-19_

Microsoft Exchange Server 2013 prend en charge la désactivation de l'authentification TLS pour la communication SMTP entre serveurs de boîtes aux lettres dans certaines topologies où des contrôleurs d'optimisation de réseau étendu (WOC) compressent le trafic SMTP.

Cette rubrique explique pas à pas comment configurer le service de transport dans vos serveurs de boîtes aux lettres concernés pour désactiver l'authentification TLS, et veiller à ce que votre topologie de routage Active Directory soit configurée pour router les messages correctement. Pour plus d'informations sur ce scénario, consultez la rubrique [Scénario : configuration d'Exchange pour prendre en charge les contrôleurs d'optimisation de réseau étendu](scenario-configure-exchange-to-support-wan-optimization-controllers-exchange-2013-help.md).

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée de cette tâche : 60 minutes.

  - Pour pouvoir effectuer toutes les tâches de ce scénario de bout en bout, votre compte doit être membre du groupe de rôles Gestion de l'organisation, même si certaines étapes de configuration peuvent être effectuées avec moins de droits.

  - Veillez à désactivez l'authentification TLS uniquement pour les connexions transitant par des périphériques WOC.

  - Cette procédure requiert que Exchange 2013 soit déployé sur plusieurs sites Active Directory, un site étant connecté aux autres via une liaison réseau étendu.

  - Cette procédure requiert que les périphériques WOC soient déployés pour compresser le trafic SMTP sur la liaison réseau étendu.

  - Cette procédure requiert un chemin d'accès logique au flux de messagerie pour Exchange, passant par la liaison réseau étendu sur laquelle les périphériques WOC sont déployés.

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.


## Que souhaitez-vous faire ?

## Étape 1 : Utiliser l'environnement de ligne de commande pour configurer le serveur de boîtes aux lettres afin d'utiliser l'authentification rétrogradée d'Exchange Server

Pour configurer le service de transport sur un serveur de boîtes aux lettres afin d'utiliser l'authentification rétrogradée d'Exchange Server, exécutez la commande suivante :

    Set-TransportService <ServerIdentity> -UseDowngradedExchangeServerAuth $true

Cet exemple montre comment modifier cette configuration sur le serveur nommé Mailbox01.

    Set-TransportService Mailbox01 -UseDowngradedExchangeServerAuth $true

## Étape 2 : Créer un connecteur de réception dédié sur le serveur de boîtes aux lettres pour le site Active Directory cible

## Utiliser le CAE pour créer le connecteur de réception

1.  Dans le Centre d'administration Exchange (CAE), accédez à **Flux de messagerie** \> **Connecteurs d'envoi**, puis cliquez sur **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter").

2.  Dans la première page de l'Assistant **Nouveau connecteur de réception**, entrez les valeurs suivantes.
    
      - **Nom**   Entrez une valeur descriptive.
    
      - **Type**   Interne
    
    Lorsque vous avez terminé, cliquez sur **Suivant**.

3.  Dans la deuxième page de l'Assistant **Nouveau connecteur de réception**, dans la section **Paramètres distant**, entrez les adresses ou plages d'adresses IP pour le site Active Directory cible. Lorsque vous avez fini, cliquez sur **Terminer**.

## Utiliser l'environnement de ligne de commande pour créer le connecteur de réception

Pour créer un connecteur de réception sur le serveur de boîtes aux lettres, exécutez la commande suivante :

    New-ReceiveConnector -Name <Name> -Server <ServerIdentity> -RemoteIPRanges <IPAddressRange> -Internal

Cet exemple montre comment créer le connecteur de réception nommé WAN sur un serveur nommé Mailbox01 avec les paramètres suivants :

  - Le paramètre *RemoteIPRanges* est défini sur 10.0.2.0/24. Cette plage d'adresses IP doit correspondre au site distant Active Directory où ce connecteur de réception recevra les connexions non chiffrées. Si le site distant comporte plusieurs sous-réseaux IP, vous pouvez les entrer en les séparant par des virgules.

  - Le type d'utilisation est défini sur Interne.

<!-- end list -->

    New-ReceiveConnector -Name WAN -Server Hub01 -RemoteIPRanges 10.0.2.0/24 -Internal

## Étape 3 : Utiliser l'environnement de ligne de commande pour désactiver l'authentification TLS sur le connecteur de réception dédié

Pour désactiver l'authentification TLS sur le connecteur de réception, exécutez la commande suivante :

    Set-ReceiveConnector <ReceiveConnectorIdentity> -SuppressXAnonymousTLS $true

Cet exemple montre comment désactiver l'authentification TLS sur le connecteur de réception nommé WAN sur le serveur de boîtes aux lettres nommé Mailbox01.

    Set-ReceiveConnector Mailbox01\WAN -SuppressXAnonymousTLS $true

## Étape 4 : Utiliser l'environnement de ligne de commande pour désigner les sites Active Directory comme sites hub

Pour désigner un site Active Directory en tant que site hub, exécutez la commande suivante :

    Set-AdSite <ADSiteIdentity> -HubSiteEnabled $true

Vous devez effectuer cette procédure une fois dans chaque site Active Directory incluant des serveurs de boîtes aux lettres participant à un trafic non-chiffré.

Cet exemple montre comment configurer le site Active Directory nommé Central Office Site 1 comme site hub.

    Set-AdSite "Central Office Site 1" -HubSiteEnabled $true

## Étape 5 : Utiliser l'environnement de ligne de commande pour configurer l'itinéraire de routage le moins coûteux via la connexion WAN

Selon la configuration des coûts du lien de sites IP dans Active Directory, cette étape n'est peut-être pas nécessaire. Vous devez vérifier que la liaison réseau avec les périphériques WOC se trouve dans l'itinéraire de routage le moins coûteux. Pour afficher les coûts de lien de sites Active Directory et les coûts de lien de sites spécifiques d'Exchange, exécutez la commande suivante :

    Get-AdSiteLink

Si la liaison réseau avec les périphériques WOC déployés ne figure pas sur l'itinéraire de routage le moins coûteux, vous devez attribuer un coût spécifique d'Exchange au lien de sites IP concerné pour être certain que les messages soient routés correctement. Pour plus d'informations sur ce problème particulier, consultez la section « Configuration des coûts de lien de sites Active Directory spécifiques d'Exchange » de la rubrique [Scénario : configuration d'Exchange pour prendre en charge les contrôleurs d'optimisation de réseau étendu](scenario-configure-exchange-to-support-wan-optimization-controllers-exchange-2013-help.md).

Cet exemple montre comment configurer un coût 15 spécifique d'Exchange pour le lien de sites IP nommé Branch Office 2-Branch Office 1.

    Set-AdSiteLink "Branch Office 2-Branch Office 1" -ExchangeCost 15

