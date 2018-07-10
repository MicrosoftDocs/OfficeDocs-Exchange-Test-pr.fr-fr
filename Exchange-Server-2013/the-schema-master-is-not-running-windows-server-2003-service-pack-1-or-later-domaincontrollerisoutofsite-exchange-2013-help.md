---
title: 'Le contrôleur de schéma n’utilise pas Windows Server 2003 Service Pack 1 ou une version ultérieure_DomainControllerIsOutOfSite: Exchange 2013 Help'
TOCTitle: Le contrôleur de schéma n’utilise pas Windows Server 2003 Service Pack 1 ou une version ultérieure_DomainControllerIsOutOfSite
ms:assetid: 5edbe0b8-7610-4a52-aaaa-38c6a99e7e53
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/ms.exch.setupreadiness.domaincontrollerisoutofsite(v=EXCHG.150)
ms:contentKeyID: 50478203
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Le contrôleur de schéma n’utilise pas Windows Server 2003 Service Pack 1 ou une version ultérieure\_DomainControllerIsOutOfSite

 

_**Sapplique à :** Exchange Server_

_**Dernière rubrique modifiée :** 2016-12-09_

Le contenu de cette rubrique n'a pas été mis à jour pour Microsoft Exchange Server 2013. Bien qu'il n'ait pas été encore mis à jour, il peut toujours être applicable pour Exchange 2013. Si vous avez toujours besoin d'aide, consultez les ressources de communauté ci-dessous.

Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), et [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

Le programme d’installation de Microsoft Exchange Server 2007 ne peut pas poursuivre son exécution car le contrôleur de domaine attribué au rôle de contrôleur de schéma du service d’annuaire Active Directory, également baptisé FSMO (flexible single master operations, opérations à maître unique flottant), n’utilise pas Microsoft Windows Server™ 2003 Service Pack 1 (SP1) ou une version ultérieure.

Le programme d’installation d’Exchange 2007 nécessite que le contrôleur de domaine qui fait office de FSMO du schéma utilise Windows Server 2003 SP1 ou une version ultérieure.

Le FSMO contrôle toutes les mises à jour et les modifications du schéma Active Directory.

Pour résoudre ce problème, effectuez une ou plusieurs des opérations suivantes :

  - Mettez à niveau le contrôleur de domaine FSMO vers Windows Server 2003 SP1 ou une version ultérieure, puis recommencez l’installation de Microsoft Exchange.

  - Si un contrôleur de domaine FSMO exécute Microsoft Windows Server 2003 Service Pack 1 (SP1) ou version ultérieure dans l’organisation Exchange, exécutez le programme d’installation d’Exchange 2007 avec le paramètre /domaincontroller pointant sur ce contrôleur de domaine FSMO :
    
    \[*/DomainController* ou */dc\<FQDN of domain controller\>*\]
    
    Le paramètre  */DomainController* permet de spécifier le contrôleur de domaine à utiliser pour lire ou écrire dansActive Directory lors de l’installation. Vous pouvez utiliser NetBIOS ou le format de nom de domaine complet (FQDN).

Pour obtenir le dernier Service Pack de Windows Server 2003, visitez le site TechCenter de Windows Server ([https://go.microsoft.com/fwlink/?LinkId=45315](https://go.microsoft.com/fwlink/?linkid=45315)).

Pour plus d’informations sur les paramètres du programme d’installation d’Exchange Server 2007, consultez la rubrique « Procédure d’installation d’Exchange 2007 en mode sans assistance » ([https://go.microsoft.com/fwlink/?LinkId=86476](https://go.microsoft.com/fwlink/?linkid=86476)) in the Exchange Server 2007 product documentation.

