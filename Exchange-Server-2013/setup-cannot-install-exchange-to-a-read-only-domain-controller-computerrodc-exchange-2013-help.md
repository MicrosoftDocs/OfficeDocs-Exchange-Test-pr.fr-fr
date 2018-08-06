---
title: 'Impossible d’installer Exchange dans un contrôleur de domaine en lecture seule | Microsoft Docs'
TOCTitle: Le programme d’installation ne peut pas installer Exchange dans un contrôleur de domaine en lecture seule_ComputerRODC
ms:assetid: 4934d755-65be-47e2-86b0-6ea1ab148a96
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/ms.exch.setupreadiness.computerrodc(v=EXCHG.150)
ms:contentKeyID: 50478033
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Le programme d’installation ne peut pas installer Exchange dans un contrôleur de domaine en lecture seule\_ComputerRODC

 

_**Sapplique à :** Exchange Server_

_**Dernière rubrique modifiée :** 2012-06-05_

Le contenu de cette rubrique n'a pas été mis à jour pour Microsoft Exchange Server 2013. Bien qu'il n'ait pas été encore mis à jour, il peut toujours être applicable pour Exchange 2013. Si vous avez toujours besoin d'aide, consultez les ressources de communauté ci-dessous.

Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), et [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

Le programme d’installation de Microsoft Exchange Server 2007 ne peut pas poursuivre l’installation car l’ordinateur cible est un contrôleur de domaine en lecture seule (RODC).

Les contrôleurs de domaine en lecture seule sont une fonctionnalité de Windows Server 2008 Active Directory. Il s’agit d’un type d’option d’installation de contrôleur de domaine qui peut être installée sur des sites distants dont les niveaux de sécurité physiques peuvent être plus faibles.

Le programme d’installation Exchange nécessite un accès en écriture à l’ordinateur d’installation cible.

Pour résoudre ce problème, sélectionnez un ordinateur d’installation cible qui n’est pas désigné comme contrôleur de domaine en lecture seule, puis réexécutez le programme d’installation.

