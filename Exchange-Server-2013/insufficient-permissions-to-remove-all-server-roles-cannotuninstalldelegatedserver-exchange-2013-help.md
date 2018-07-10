---
title: 'Autorisations insuffisantes pour supprimer tous les rôles serveur_CannotUninstallDelegatedServer: Exchange 2013 Help'
TOCTitle: Autorisations insuffisantes pour supprimer tous les rôles serveur_CannotUninstallDelegatedServer
ms:assetid: 214ae6f3-15e7-4337-99e8-40f9547c8e0c
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/ms.exch.setupreadiness.cannotuninstalldelegatedserver(v=EXCHG.150)
ms:contentKeyID: 50477634
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Autorisations insuffisantes pour supprimer tous les rôles serveur\_CannotUninstallDelegatedServer

 

_**Sapplique à :** Exchange Server_

_**Dernière rubrique modifiée :** 2016-12-09_

Le contenu de cette rubrique n'a pas été mis à jour pour Microsoft Exchange Server 2013. Bien qu'il n'ait pas été encore mis à jour, il peut toujours être applicable pour Exchange 2013. Si vous avez toujours besoin d'aide, consultez les ressources de communauté ci-dessous.

Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), et [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

Le programme d’installation de Microsoft Exchange Server 2007 ne peut pas poursuivre son exécution car la tentative de désinstaller tous les rôles serveurs a échoué.

Le programme d’installation d’Exchange 2007 nécessite que l’utilisateur connecté lors de la désinstallation de tous les rôles serveurs soit membre des groupes Administrateurs d’organisation Exchange ou du groupe Administrateurs de l’entreprise.

Pour résoudre ce problème, accordez à l’utilisateur connecté des autorisations de niveau Organisation Exchange ou inscrivez-le dans le groupe Administrateurs de l’entreprise ou ouvrez une session à l’aide d’un compte disposant des autorisations, puis recommencez l’installation d’Exchange 2007.

Pour plus d’informations sur les autorisations Active Directory nécessaires avec Microsoft Exchange, reportez-vous à la section « Travailler avec Active Directory des autorisations dans Exchange Server » ([https://go.microsoft.com/fwlink/?LinkId=47592](https://go.microsoft.com/fwlink/?linkid=47592)).

