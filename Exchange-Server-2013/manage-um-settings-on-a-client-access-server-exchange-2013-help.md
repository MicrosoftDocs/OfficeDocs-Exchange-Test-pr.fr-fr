---
title: 'Gestion des param. de MU sur un serveur d’accès au client: Exchange 2013 Help'
TOCTitle: Gestion des paramètres de messagerie unifiée sur un serveur d’accès au client
ms:assetid: 08667911-fa86-404e-84b1-65cedd94d579
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ673507(v=EXCHG.150)
ms:contentKeyID: 50555342
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Gestion des paramètres de messagerie unifiée sur un serveur d’accès au client

 

_**Sapplique à :** Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2013-04-09_

Après avoir installé un serveur d'accès au client exécuté sur le service routeur d'appels de messagerie unifiée Microsoft Exchange, vous pouvez configurer plusieurs options, notamment le nombre d'appels simultanés, les ports d'écoute TCP et TLS (Transport Layer Security), l'état et le mode de démarrage.

> [!NOTE]
> Il n'est pas nécessaire d'ajouter des serveurs d'accès au client à un plan de numérotation de messagerie unifiée avant qu'ils ne puissent traiter les appels pour la messagerie unifiée, sauf si vous intégrez la messagerie unifiée et Microsoft Office Communications Server 2007 R2 ou Microsoft Lync Server. Par défaut, tous les serveurs d'accès au client d'une organisation sont disponibles pour répondre aux appels entrants.


Pour découvrir des tâches supplémentaires relatives à la messagerie unifiée et aux serveurs d'accès au client, consultez la rubrique [Procédures de services de messagerie unifiée](um-services-procedures-exchange-2013-help.md).

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : 5 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l'entrée « Serveur d'accès au client (service de routeur d'appel de messagerie unifiée) » dans la rubrique [Autorisations de messagerie unifiée](unified-messaging-permissions-exchange-2013-help.md).

  - Vérifiez que le serveur d'accès au client est installé, soit sur le même ordinateur que le serveur de boîtes aux lettres, soit sur un ordinateur distinct.

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..


## Que souhaitez-vous faire ?

## Configuration des propriétés de messagerie unifiée sur un serveur d'accès au client à l'aide de l'environnement de ligne de commande Exchange Management Shell

Cet exemple supprime un serveur d'accès au client nommé `MyClientAccessServer` de tous les plans de numérotation SIP (Session Initiation Protocol).

    Set-UMCallRouterSettings -DialPlans $null - Server MyClientAccessServer

Cet exemple ajoute un serveur d'accès au client nommé `MyClientAccessServer` à un plan de numérotation SIP nommé `MySIPDialPlan` et définit le nombre maximal d'appels vocaux entrants.

    Set-UMCallRouterSettings -DialPlans MySIPDialPlan -MaxCalls 150 -Server MyClientAccessServer

Cet exemple définit le port d'écoute TCP SIP sur 5077 et le mode de démarrage Double sur un serveur d'accès au client nommé `MyClientAccessServer`.

    Set-UMCallRouterSettings  -Server MyClientAccessServer-SipTCPListeningPort 5077 -UMStartUpMode -Dual 

## Affichage des propriétés du serveur d'accès au client à l'aide de l'environnement de ligne de commande Exchange Management Shell

Cet exemple montre comment afficher une liste de tous les serveurs d'accès au client.

    Get-UMCallRouterSettings

Cet exemple montre comment afficher une liste formatée des propriétés pour le serveur d'accès au client.

    Get-UMCallRouterSettings | Format-List

