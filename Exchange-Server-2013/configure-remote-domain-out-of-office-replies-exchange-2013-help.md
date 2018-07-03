---
title: 'Configurer des réponses d’absence du bureau de domaine distant: Exchange 2013 Help'
TOCTitle: Configurer des réponses d’absence du bureau de domaine distant
ms:assetid: 0c1e56be-7a29-4294-9762-600f9f788741
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ657713(v=EXCHG.150)
ms:contentKeyID: 50477492
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configurer des réponses d’absence du bureau de domaine distant

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2015-04-08_

Vous pouvez utiliser Exchange Management Shell pour configurer la façon dont les courriers électroniques sont envoyés et reçus via des domaines distants. La section suivante indique comment utiliser l’environnement de ligne de commande Exchange Management Shell pour configurer la gestion des réponses d’absence du bureau dans Exchange.

## Ce qu’il faut savoir avant de commencer ?

  - Durée d'exécution estimée : 10 minutes

  - Vous pouvez uniquement utiliser l'environnement de ligne de commande Exchange Management Shell pour effectuer cette tâche.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l’entrée « Domaines distants » dans la rubrique [Autorisations de flux de messagerie](mail-flow-permissions-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.


## Utiliser l’environnement de ligne de commande Shell pour configurer les réponses d’absence du bureau

Vous pouvez utiliser la cmdlet **Set-RemoteDomain** pour configurer les propriétés d’un domaine distant.

Cet exemple désactive les messages d’absence du bureau pour le domaine distant Contoso.

    Set-RemoteDomain Contoso -AllowedOOFType None

Il autorise uniquement les messages externes de notification d'absence du bureau.

    Set-RemoteDomain Contoso -AllowedOOFType External

