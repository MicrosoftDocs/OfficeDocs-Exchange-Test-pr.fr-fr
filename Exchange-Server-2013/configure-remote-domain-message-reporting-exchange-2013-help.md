---
title: 'Configuration du rapport de message de domaine distant: Exchange 2013 Help'
TOCTitle: Configuration du rapport de message de domaine distant
ms:assetid: 73dc686a-e7a3-44c7-b82f-f52ff9273199
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ649325(v=EXCHG.150)
ms:contentKeyID: 50478455
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configuration du rapport de message de domaine distant

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2015-04-08_

Vous pouvez utiliser Exchange Management Shell pour configurer la façon dont les courriers électroniques sont envoyés et reçus via des domaines distants. Lisez les informations ci-dessous pour savoir comment utiliser Exchange Management Shell afin de configurer la façon dont Exchange gère les rapports de remise et de non-remise.

## Ce qu’il faut savoir avant de commencer ?

  - Durée d’exécution estimée : 10 minutes

  - Vous pouvez uniquement utiliser l'environnement de ligne de commande Exchange Management Shell pour effectuer cette tâche.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l’entrée « Domaines distants » dans la rubrique [Autorisations de flux de messagerie](mail-flow-permissions-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.


## Utiliser l’environnement de ligne de commande Exchange Management Shell pour configurer la génération des rapports de message

Vous pouvez utiliser la cmdlet **Set-RemoteDomain** pour configurer les propriétés d’un domaine distant.

Cet exemple désactive les rapports de remise dans le domaine distant appelé Contoso. Ce paramètre est activé par défaut.

```powershell
Set-RemoteDomain Contoso -DeliveryReportEnabled $false
```

Dans cet exemple la notification d’échec de remise au domaine distant est désactivée. Ce paramètre est activé par défaut.

```powershell
Set-RemoteDomain Contoso -NDREnabled $false
```

