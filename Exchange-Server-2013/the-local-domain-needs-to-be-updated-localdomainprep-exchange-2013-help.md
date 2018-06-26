---
title: 'Le domaine local doit être mis à jour_LocalDomainPrep: Exchange 2013 Help'
TOCTitle: Le domaine local doit être mis à jour_LocalDomainPrep
ms:assetid: f33e6785-e85a-495e-a124-ebcb2b763e75
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/ms.exch.setupreadiness.localdomainprep(v=EXCHG.150)
ms:contentKeyID: 50479522
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Le domaine local doit être mis à jour\_LocalDomainPrep

 

_**Sapplique à :**Exchange Server_

_**Dernière rubrique modifiée :**2016-12-09_

Le contenu de cette rubrique n'a pas été mis à jour pour Microsoft Exchange Server 2013. Bien qu'il n'ait pas été encore mis à jour, il peut toujours être applicable pour Exchange 2013. Si vous avez toujours besoin d'aide, consultez les ressources de communauté ci-dessous.

Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), et [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

Le programme d'installation de Microsoft Exchange Server 2007 ne peut pas poursuivre son exécution car l'utilisateur connecté ne possède pas les autorisations nécessaires pour la préparation de domaine.

Le programme d'installation d'Exchange nécessite que l'utilisateur connecté lors de l'exécution de **Setup /PrepareDomain** soit un membre des groupes Administrateurs de domaine et Administrateurs d'organisation Exchange ou du groupe Administrateurs de l'entreprise.

Pour résoudre ce problème, accordez à l'utilisateur connecté des autorisations de niveau Admins du domaine et Administrateurs d'organisation Exchange ou inscrivez-le dans le groupe Administrateurs de l'entreprise ou ouvrez une session à l'aide d'un compte disposant des autorisations, puis recommencez l'installation d'Exchange 2007.

Pour plus d’informations sur les autorisations Active Directory nécessaires avec Microsoft Exchange, consultez la rubrique Utilisation des autorisations Active Directory dans Exchange Server ([https://go.microsoft.com/fwlink/?LinkId=47592](https://go.microsoft.com/fwlink/?linkid=47592)).

