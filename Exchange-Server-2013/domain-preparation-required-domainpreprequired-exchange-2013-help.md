---
title: 'Préparation de domaine requise_DomainPrepRequired: Exchange 2013 Help'
TOCTitle: Préparation de domaine requise_DomainPrepRequired
ms:assetid: f6feae6f-7404-4b1f-887f-ed63c26a6bcd
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/ms.exch.setupreadiness.domainpreprequired(v=EXCHG.150)
ms:contentKeyID: 50479575
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Préparation de domaine requise\_DomainPrepRequired

 

_**Sapplique à :**Exchange Server_

_**Dernière rubrique modifiée :**2016-12-09_

Le contenu de cette rubrique n'a pas été mis à jour pour Microsoft Exchange Server 2013. Bien qu'il n'ait pas été encore mis à jour, il peut toujours être applicable pour Exchange 2013. Si vous avez toujours besoin d'aide, consultez les ressources de communauté ci-dessous.

Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), et [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

Le programme d'installation de Microsoft Exchange Server 2007 ne peut pas poursuivre son exécution car la tentative d'installer le rôle serveur a échoué.

Le programme d'installation de Microsoft Exchange nécessite que le domaine local soit préparé pour Exchange Server 2007 avant de pouvoir installer certains rôles serveurs.

La préparation du domaine pour Exchange Server 2007 est la procédure suivante :

  - définition d'autorisations sur le conteneur de domaine pour les serveurs Exchange, les administrateurs d'organisation Exchange, les utilisateurs authentifiés et les administrateurs de boîtes aux lettres Exchange ;

  - création du conteneur Objets système Microsoft Exchange s'il n'existe pas et définition des autorisations sur ce conteneur pour les serveurs Exchange, les administrateurs d'organisation Exchange et les utilisateurs authentifiés ;

  - création d'un groupe global de domaines dans le domaine actuel, nommé Serveurs de domaine Exchange.

  - Ajout du groupe Serveurs de domaine Exchange au groupe de sécurité universel Serveurs Exchange dans le domaine racine.

Pour résoudre ce problème, exécutez **setup /PrepareDomain** pour préparer le domaine local et réessayez l'installation du rôle serveur.

Pour plus d’informations sur la réalisation du processus PrepareDomain, consultez la rubrique Procédure de préparation d’Active Directory et de domaines ([https://go.microsoft.com/fwlink/?LinkId=78453](https://go.microsoft.com/fwlink/?linkid=78453)).

