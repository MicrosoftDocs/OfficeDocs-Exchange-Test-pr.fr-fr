---
title: 'Gérer les paramètres de MU sur un serveur de BAL: Exchange 2013 Help'
TOCTitle: Gérer les paramètres de messagerie unifiée sur un serveur de boîtes aux lettres
ms:assetid: 6df4853d-21d2-473f-b0ca-ebc996d8794a
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Aa998815(v=EXCHG.150)
ms:contentKeyID: 50555407
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.Servers.UnifiedMessaging.UMServerPropertiesPropertyPage
ms.translationtype: MT
---

# Gérer les paramètres de messagerie unifiée sur un serveur de boîtes aux lettres

 

_**Sapplique à :** Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2013-02-11_

Après avoir installé un serveur de boîtes aux lettres exécutant le service de messagerie unifiée Microsoft Exchange, vous pouvez configurer plusieurs options, notamment le nombre d'appels simultanés, les ports d'écoute TCP et TLS (Transport Layer Security), l'état et le mode de démarrage de la messagerie unifiée.

> [!IMPORTANT]
> Il n'est pas nécessaire d'ajouter des serveurs de boîtes aux lettres à un plan de numérotation de messagerie unifiée avant qu'ils ne puissent traiter les appels pour la messagerie unifiée, sauf si vous intégrez la messagerie unifiée et Microsoft Office Communications Server 2007 R2 ou Microsoft Lync Server. Par défaut, tous les serveurs de boîtes aux lettres d'une organisation sont disponibles pour répondre aux appels entrants.


Pour d'autres tâches de gestion relatives aux serveurs de messagerie unifiée et de boîtes aux lettres, consultez la rubrique [Procédures de services de messagerie unifiée](um-services-procedures-exchange-2013-help.md).

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : 5 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l'entrée « Serveur de boîtes aux lettres (service de messagerie unifiée) » dans la rubrique [Autorisations de messagerie unifiée](unified-messaging-permissions-exchange-2013-help.md).

  - Vérifiez que le serveur de boîtes aux lettres est installé, sur le même ordinateur que le serveur d'accès au client ou sur un ordinateur distinct.

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..


## Que souhaitez-vous faire ?

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour configurer des propriétés de messagerie unifiée sur un serveur de boîtes aux lettres

Cet exemple illustre la suppression du serveur de boîtes aux lettres `MyMailboxServer` de tous les plans de numérotation SIP (Session Initiation Protocol).

    Set-UMService -Identity MyMailboxServer -DialPlans $null

Cet exemple illustre l'ajout du serveur de boîtes aux lettres `MyMailboxServer` au plan de numérotation SIP de messagerie unifiée `MySIPDialPlanName` et la définition du nombre maximal d'appels vocaux entrants.

    Set-UMService -Identity MyMailboxServer -DialPlans MySIPDialPlanName -MaxCalls 150 

Cet exemple illustre la définition du mode de démarrage double pour le serveur de boîtes aux lettres `MyUMServer`.

    Set-UMService -Identity MyMailboxServer -DialPlans MySIPDialPlanName -UMStartUpMode -Dual 

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour afficher les propriétés d'un serveur de boîtes aux lettres

Cet exemple illustre l'affichage d'une liste de tous les serveurs de boîtes aux lettres.

    Get-UMService

Cet exemple illustre l'affichage d'une liste de propriétés mise en forme pour le serveur de boîtes aux lettres `MyMailboxServer`.

    Get-UMService -Identity MyMailboxServer | Format-List

