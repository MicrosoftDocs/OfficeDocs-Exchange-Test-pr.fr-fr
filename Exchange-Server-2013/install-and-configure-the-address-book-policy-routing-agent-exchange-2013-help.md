---
title: "installation et configuration de l'agent de routage des stratégies de carnet d'adresses: Exchange 2013 Help"
TOCTitle: installation et configuration de l'agent de routage des stratégies de carnet d'adresses
ms:assetid: 20e8a43d-4508-4388-a2c9-aa3073593cc2
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ907308(v=EXCHG.150)
ms:contentKeyID: 51407164
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# installation et configuration de l'agent de routage des stratégies de carnet d'adresses

 

_**Sapplique à :** Exchange Online, Exchange Server 2013_

_**Dernière rubrique modifiée :** 2014-01-09_

L'agent de routage des stratégies de carnet d'adresses est un agent de transport exécuté sur le serveur de boîtes aux lettres qui contrôle la manière dont les destinataires sont résolus dans votre organisation. Quand l’agent de routage des stratégies de carnet d’adresses est installé et configuré, les utilisateurs affectés à plusieurs LAG apparaissent en tant que destinataires externes, dans le sens où ils ne peuvent pas afficher les cartes de visite de destinataires externes.

Pour les autres tâches de gestion relatives aux stratégies de carnet d'adresses, consultez la rubrique [Procédures des stratégies de carnet d’adresses](address-book-policy-procedures-exchange-2013-help.md).

Vous recherchez la version Exchange Online de cette rubrique ? Consultez la rubrique [Activation du routage des stratégies de carnet d’adresses](https://technet.microsoft.com/fr-fr/library/jj891095\(v=exchg.150\)).

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée de cette tâche : 15 minutes.

  - Après avoir installé et configuré l'agent de routage des stratégies de carnet d'adresses, l'évaluation des messages électroniques de l'organisation par un agent peut prendre jusqu'à 30 minutes.

  - Vous ne pouvez pas utiliser le Centre d’administration Exchange pour effectuer cette procédure. Vous devez utiliser l'environnement de ligne de commande Exchange Management Shell.

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.


## Comment procéder ?

## Étape 1 : installation de l'agent de routage des stratégies de carnet d'adresses

Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l'entrée « Agents de transport » dans la rubrique [Autorisations de flux de messagerie](mail-flow-permissions-exchange-2013-help.md).

Installez l'agent de routage des stratégies de carnet d'adresses en exécutant la commande suivante. Il s’agit de la commande et de la syntaxe exactes que vous devez utiliser.

    Install-TransportAgent -Name "ABP Routing Agent" -TransportAgentFactory "Microsoft.Exchange.Transport.Agent.AddressBookPolicyRoutingAgent.AddressBookPolicyRoutingAgentFactory" -AssemblyPath $env:ExchangeInstallPath\TransportRoles\agents\AddressBookPolicyRoutingAgent\Microsoft.Exchange.Transport.Agent.AddressBookPolicyRoutingAgent.dll

Vous recevrez un avertissement indiquant que le service de transport doit être redémarré pour que vos modifications soient appliquées, mais auparavant, effectuez l’étape 2 de manière à ne redémarrer le service de transport qu’une seule fois.

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, consultez la rubrique [Install-TransportAgent](https://technet.microsoft.com/fr-fr/library/aa997998\(v=exchg.150\)).

## Étape 2 : activation de l'agent de routage de transport

Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l'entrée « Agents de transport » dans la rubrique [Autorisations de flux de messagerie](mail-flow-permissions-exchange-2013-help.md).

Après avoir installé l'agent de routage des stratégies de carnet d'adresses, vous devez l'activer en exécutant la commande suivante :

    Enable-TransportAgent "ABP Routing Agent"

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, consultez la rubrique [Enable-TransportAgent](https://technet.microsoft.com/fr-fr/library/bb124921\(v=exchg.150\)).

## Étape 3 : redémarrage du service de transport et vérification de l'installation et de l'activation de l'agent de routage des stratégies de carnet d'adresses

Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l'entrée « Agents de transport » dans la rubrique [Autorisations de flux de messagerie](mail-flow-permissions-exchange-2013-help.md).

1.  Redémarrez le service de transport en exécutant la commande suivante.
    
        Restart-Service MSExchangeTransport

2.  Après le redémarrage du service, vérifiez que l'agent de routage des stratégies de carnet d'adresses est installé et activé en exécutant la cmdlet suivante.
    
        Get-TransportAgent
    
    Si l'agent de routage des stratégies de carnet d'adresses figure dans la liste, cela signifie qu'il a bien été installé.

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, consultez la rubrique [Get-TransportAgent](https://technet.microsoft.com/fr-fr/library/bb123536\(v=exchg.150\)).

## Étape 4 : activation de l'agent de routage des stratégies de carnet d'adresses

Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l'entrée « Configuration du transport » dans la rubrique [Autorisations de flux de messagerie](mail-flow-permissions-exchange-2013-help.md).

La dernière étape de ce processus consiste à activer le routage des stratégies de carnet d'adresses pour l'organisation. Exécutez la commande suivante.

    Set-TransportConfig -AddressBookPolicyRoutingEnabled $true

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, consultez la rubrique [Set-TransportConfig](https://technet.microsoft.com/fr-fr/library/bb124151\(v=exchg.150\)).

