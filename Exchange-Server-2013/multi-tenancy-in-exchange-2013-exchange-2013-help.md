---
title: 'Architecture mutualisée dans Exchange 2013: Exchange 2013 Help'
TOCTitle: Architecture mutualisée dans Exchange 2013
ms:assetid: df09257d-dd98-4f59-b830-1818cedda15c
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ862352(v=EXCHG.150)
ms:contentKeyID: 50555504
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Architecture mutualisée dans Exchange 2013

 

_**Sapplique à :** Exchange Online, Exchange Server, Exchange Server 2013_

_**Dernière rubrique modifiée :** 2016-12-09_

Un déploiement Exchange 2013 partagé au sein d'une architecture mutualisée (hébergée) se définit comme un déploiement dans lequel l'organisation Exchange a été configurée pour héberger plusieurs organisations ou divisions discrètes (les clients) qui d’ordinaire ne partagent pas de courriers électroniques, de données, d’utilisateurs, de listes d’adresses globales ni tout autre objet Exchange couramment utilisé. Ce partage en termes de matériels, de logiciels et de ressources (tout en maintenant une séparation logique entre des clients), permet à des organisations d’optimiser la simplicité d’un déploiement Exchange standard tout en fournissant des fonctionnalités et des services d’une architecture mutualisée pour répondre à leurs besoins d’hébergement.

## Architecture mutualisée dans les organisations Exchange 2013

Dans Exchange 2013, nous poursuivons la prise en charge de l’hébergement en utilisant une installation Exchange locale et standard similaire à l’approche utilisée dans Exchange 2010 Service Pack 2 (SP2). Nous abandonnons le commutateur de mode `/hosting` pour mettre l’accent sur l’utilisation des stratégies de carnets d’adresses (ABP) combinées à des solutions de gestion de l’hébergement et des outils d’automatisation de fournisseurs de logiciels indépendants agréés. Ces solutions sont fondées sur une infrastructure d’instructions et de pratiques de configuration approuvées par Microsoft et offrent aux organisations Exchange un moyen plus facile et plus robuste de fournir des services et des fonctions d’hébergement.

Exchange 2013 prend en charge l’architecture mutualisée en exploitant les principaux composants et fonctions suivants :

  - **Active Directory**   Au lieu d’avoir des conteneurs Active Directory *ExchangeOrganization* distincts pour chaque division dans une organisation Exchange partagée au sein d’une architecture mutualisée, l’architecture mutualisée Exchange 2013 est prise en charge via un conteneur Active Directory *ExchangeOrganization* unique. Ainsi une structure Active Directory plus simple est permise, avec diminution des risques de rencontrer des problèmes d’autorisation liés à Active Directory.
    
    Pour plus d’informations sur les modifications d’Active Directory dans Exchange 2013, consultez la rubrique [Active Directory](active-directory-exchange-2013-help.md).

  - **Stratégies de carnet d’adresses (ABP)**   Introduites dans Exchange 2010 SP2, les stratégies de carnet d’adresses (ABP) sont utilisées dans Exchange 2013 pour contrôler l’accès des utilisateurs à une liste d’adresses, à la liste d’adresses globale (GAL) et à des carnets d’adresses en mode hors connexion (OAB) dans l’organisation Exchange. Les stratégies de carnet d’adresses (ABP) regroupent ces différents objets Active Directory en un même objet virtuel qui peut être affecté à des utilisateurs individuels, et pour créer un regroupement logique de ces ressources en une structure organisationnelle partagée au sein d’une architecture mutualisée. Les fonctionnalités des stratégies de carnet d’adresses (ABP) dans Exchange 2013 sont similaires à ce qui existait dans Exchange 2010 SP2.
    
    Pour plus d’informations sur les stratégies de carnet d’adresses (ABP) dans Exchange 2013, consultez la rubrique [Stratégies de carnet d’adresses](address-book-policies-exchange-2013-help.md).

  - **Solutions de gestion de l’hébergement**   Certains administrateurs utilisant Exchange 2013 pour offrir une solution Exchange hébergée trouveront certains avantages à utiliser une approche de gestion d’hébergement personnalisée. En raison de certaines limitations dues au Centre d’administration Exchange (EAC), Microsoft fait appel à des fournisseurs tiers pour l’assister dans le développement de solutions de panneau de configuration et d’automatisation qui sont en conformité avec les instructions et l’infrastructure approuvée et destinées à des organisations Exchange 2013 hébergées. Nous recommandons aux organisations qui configurent une solution Exchange hébergée d’exploiter ces outils pour gérer leurs organisations hébergées là où les circonstances l’exigent.
    
    Pour plus d’informations sur les solutions de gestion d’hébergement, y compris les fournisseurs de solutions validées, voir [Solutions et guide d’hébergement et d’architecture mutualisée Exchange Server 2013](https://go.microsoft.com/fwlink/?linkid=275036)

