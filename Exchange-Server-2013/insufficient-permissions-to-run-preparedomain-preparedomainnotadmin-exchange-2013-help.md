---
title: 'Autorisations insuffisantes pour exécuter /PrepareDomain'
TOCTitle: Autorisations insuffisantes pour exécuter /PrepareDomain_PrepareDomainNotAdmin
ms:assetid: c33a2bc0-5b07-49b8-a1c1-53baa4933d44
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/ms.exch.setupreadiness.preparedomainnotadmin(v=EXCHG.150)
ms:contentKeyID: 50479112
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Autorisations insuffisantes pour exécuter /PrepareDomain\_PrepareDomainNotAdmin

 

_**Sapplique à :** Exchange Server_

_**Dernière rubrique modifiée :** 2016-12-09_

Le contenu de cette rubrique n'a pas été mis à jour pour Microsoft Exchange Server 2013. Bien qu'il n'ait pas été encore mis à jour, il peut toujours être applicable pour Exchange 2013. Si vous avez toujours besoin d'aide, consultez les ressources de communauté ci-dessous.

Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), et [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

Le programme d'installation de Microsoft Exchange Server 2007 ne peut pas poursuivre son exécution car la tentative d'exécution du processus **/PrepareDomain** a échoué. L'utilisateur connecté ne possède pas les autorisations suffisantes pour réaliser le processus **/PrepareDomain**.

Le programme d'installation d'Exchange 2007 nécessite que l'utilisateur connecté lors de l'exécution du processus **/PrepareDomain** soit membre du groupe Administrateurs de domaine du domaine préparé, ainsi que du groupe Administrateurs d'entreprise.

Pour résoudre ce problème, accordez à l'utilisateur connecté des autorisations de niveau Administrateurs de domaine pour le domaine préparé et inscrivez-le dans le groupe Administrateurs d'entreprise ou ouvrez une session à l'aide d'un compte disposant des autorisations, puis réexécutez le programme d'installation d'Exchange 2007.

Pour plus d’informations sur les autorisations Active Directory nécessaires avec Microsoft Exchange, consultez la rubrique Utilisation des autorisations Active Directory dans Exchange Server ([https://go.microsoft.com/fwlink/?LinkId=47592](https://go.microsoft.com/fwlink/?linkid=47592)).

