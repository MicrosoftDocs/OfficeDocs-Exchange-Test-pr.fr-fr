---
title: 'Afficher les agents de transp. dans le pipeline de transp.: Exchange 2013 Help | Microsoft Docs'
TOCTitle: Afficher les agents de transport dans le pipeline de transport
ms:assetid: bd715d8e-7b21-48de-8f68-d425d8506e4c
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb124395(v=EXCHG.150)
ms:contentKeyID: 51407230
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Afficher les agents de transport dans le pipeline de transport

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2015-04-08_

Vous pouvez utiliser l'environnement de ligne de commande Exchange Management Shell pour afficher une liste d'agents de transport dans le pipeline de transport sur des serveurs de boîtes aux lettres et d'accès au client Microsoft Exchange Server 2013. Plus particulièrement, la cmdlet **Get-TransportPipeline** affiche des informations sur les types d'agents de transport suivants dans le pipeline de transport :

  - Agents basés sur les classes **SmtpReceiveAgent**, **RoutingAgent**, **DeliveryAgent** et **StorageAgent** dans le service de transport sur les serveurs de boîtes aux lettres.

  - Agents basés sur la classe **SmtpReceiveAgentClass** dans le service de remise du transport de boîte au lettres sur des serveurs de boîtes aux lettres.

  - Agents basés sur la classe **SmtpReceiveAgentClass** dans le service de transport frontal sur des serveurs d'accès au client.

Vous pouvez afficher la liste de tous les agents de transport activés qui ont rencontré des messages dans le pipeline de transport et les événements SMTP sur lesquels ils sont enregistrés. Pour plus d'informations sur les agents de transport, consultez les rubriques [Agents de transport](transport-agents-exchange-2013-help.md).

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : 5 minutes

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l'entrée « Agents de transport » dans la rubrique [Autorisations de flux de messagerie](mail-flow-permissions-exchange-2013-help.md).

  - Vous pouvez uniquement utiliser l'environnement de ligne de commande Exchange Management Shell pour effectuer cette tâche.

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.


## Utiliser l'environnement de ligne de commande Exchange Management Shell pour afficher la liste des agents de transport dans le pipeline de transport

Pour utiliser l'environnement de ligne de commande pour afficher une liste d'agents de transport dans le pipeline de transport sur un serveur Exchange, exécutez la commande suivante :

    Get-TransportPipeline | Format-List

Pour exporter les résultats vers un fichier texte nommé C:\\My Documents\\Transport Agents.txt, exécutez la commande suivante :

    Get-TransportPipeline | Format-List > "C:\My Documents\Transport Agents.txt"

## Comment savoir si cela a fonctionné ?

Seuls les agents de transport ayant rencontré des messages dans le pipeline de transport entre le démarrage du service de transport et l'exécution de la cmdlet **Get-TransportPipeline** sont affichés par la cmdlet. Un agent de transport n'ayant pas rencontré de message dans le pipeline de transport n'apparaît pas dans les résultats affichés par la cmdlet **Get-TransportPipeline**, même si cet agent de transport est activé.

