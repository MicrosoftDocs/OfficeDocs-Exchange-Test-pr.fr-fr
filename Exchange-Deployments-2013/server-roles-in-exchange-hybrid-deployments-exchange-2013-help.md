---
title: 'Rôles serveur dans les déploiements hybrides Exchange: Exchange 2013 Help'
TOCTitle: Rôles serveur dans les déploiements hybrides Exchange
ms:assetid: 7a7eaf17-d2b0-4d62-90a2-45a0d2faca54
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ659051(v=EXCHG.150)
ms:contentKeyID: 50479669
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Rôles serveur dans les déploiements hybrides Exchange

 

_**Sapplique à :**Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :**2016-12-09_

Vous pouvez configurer des déploiements hybrides basés sur Exchange 2013 et Exchange 2016. Les rôles qui doivent être configurés pour prendre en charge un déploiement hybride dépendent de la version de Exchange que vous utilisez.

## Déploiement hybride Exchange 2016

Lors de la configuration d’un déploiement hybride dans une organisation Exchange 2016, vous n’êtes pas obligé d’installer des serveurs Exchange supplémentaires dans votre organisation Exchange existante. Vos serveurs de boîtes aux lettres coordonnent les communications entre votre organisation Exchange 2016 existante et l’organisation Exchange Online. Cette communication englobe le transport des messages et les caractéristiques de messagerie entre l’organisation locale et l’organisation Exchange Online. Nous vous recommandons vivement d’installer plusieurs serveurs Exchange dans votre organisation locale pour renforcer la fiabilité et la disponibilité des fonctions de déploiement hybride.

Exchange 2016 comporte seulement un seul rôle serveur requis, le rôle de boîte aux lettres. Outre l’hébergement des boîtes aux lettres de destinataire locales, le rôle de boîte aux lettres effectue toutes les fonctions nécessaires à la prise en charge d’un déploiement hybride avec Exchange Online. Cela inclut la gestion de tous les messages électroniques sécurisés échangés entre l’organisation locale et l’organisation Exchange Online, ainsi que des règles de transport, des stratégies de journalisation et de la remise des messages aux boîtes aux lettres utilisateur dans un déploiement hybride. Toutes les caractéristiques des relations organisationnelles et de la connectivité client, telles que le partage de disponibilité, sont également gérées par le serveur de boîtes aux lettres.

Pour en savoir plus sur la planification de la capacité Exchange 2016, consultez l’article relatif au [dimensionnement des déploiements Exchange 2016](http://go.microsoft.com/fwlink/p/?linkid=301990).

## Déploiement hybride Exchange 2013

Lors de la configuration d'un déploiement hybride dans une organisation Exchange 2013, vous n'êtes pas obligé d'installer des serveurs Exchange supplémentaires dans votre organisation Exchange existante. Vos serveurs d'accès au client et de messagerie coordonnent les communications entre votre organisation Exchange 2013 existante et l'organisation Exchange Online. Cette communication englobe le transport des messages et les caractéristiques de messagerie entre l'organisation locale et l'organisation Exchange Online. Nous vous recommandons vivement d'installer plusieurs serveurs Exchange dans votre organisation locale pour renforcer la fiabilité et la disponibilité des fonctions de déploiement hybride.

Voici un rapide résumé des rôles serveur Exchange 2013 dans un déploiement hybride :

  - **Rôle serveur d'accès au client**   Le rôle serveur d'accès au client continue à proposer la même fonctionnalité que celle généralement fournie par les autres serveurs d'accès au client de votre organisation Exchange 2013, avec quelques ajouts nécessaires à la prise en charge d'un déploiement hybride. Le serveur d'accès au client assure également la gestion de tous les messages électroniques sécurisés échangés entre l'organisation locale et l'organisation Exchange Online, ainsi que des règles de transport, des stratégies de journalisation et de la remise des messages aux boîtes aux lettres utilisateur dans un déploiement hybride. Par défaut, un connecteur de réception dédié est configuré sur le serveur d'accès au client pour gérer le transport de courrier hybride sécurisé. L'ensemble des connexions au client, y compris l'accès au client Outlook, Outlook Web App et Outlook Anywhere, passe par le rôle serveur d'accès au client. Les fonctions des relations des organisations locale et Exchange Online, telles que le partage de disponibilité, sont également gérées par le rôle serveur d'accès au client.
    
    Pour plus d'informations, consultez la rubrique [Serveur d’accès au client](https://technet.microsoft.com/fr-fr/library/dd298114\(v=exchg.150\)).

  - **Rôle serveur de boîte aux lettres**   Le rôle serveur de boîte aux lettres héberge les boîtes aux lettres de destinataires locaux et communique avec l'organisation Exchange Online par proxy via le serveur d'accès au client local. Par défaut, un connecteur d'envoi dédié est configuré sur le rôle serveur de boîte aux lettres pour gérer le transport de courrier hybride sécurisé.
    
    Pour plus d'informations, consultez la rubrique [Serveur de boîtes aux lettres](https://technet.microsoft.com/fr-fr/library/jj150491\(v=exchg.150\)).

Selon la configuration de déploiement hybride souhaitée, un serveur Exchange 2013 requiert l'installation de l'un des deux rôles serveur ou des deux :

  - **Serveur Exchange unique**   Si vous décidez d’installer un serveur Exchange unique dans votre organisation sur site, vous devrez installer les deux rôles serveur d’accès au client et de boîte aux lettres sur ce serveur.

  - **Plusieurs serveurs Exchange**   Si vous décidez d'installer plusieurs serveurs Exchange dans votre organisation locale, vous pouvez installer les rôles serveur sur des serveurs distincts dans votre organisation locale. Par exemple, vous pouvez installer un serveur Exchange doté de rôles de boîte aux lettres et d'accès au client, et installer un autre serveur Exchange possédant uniquement le rôle serveur d'accès au client. Toutefois, la meilleure configuration de serveur recommandée consiste à installer les deux rôles serveur d'accès au client et de boîte aux lettres sur *chaque* serveur déployé dans votre organisation locale.

Pour en savoir plus sur la planification de la capacité d'Exchange 2013, consultez la page [Présentation des configurations de rôles de serveur multiples dans la planification de la capacité](http://go.microsoft.com/fwlink/?linkid=266576).

## Fonctionnalités Exchange Server dans des déploiements hybrides

Les serveurs Exchange permettent de doter votre organisation locale de plusieurs fonctions importantes au sein d'un déploiement hybride :

  - **Fédération**   Les serveurs Exchange vous permettent de créer une approbation de fédération pour votre organisation locale à l’aide de Microsoft Federation Gateway. Microsoft Federation Gateway est un service en nuage gratuit proposé par Microsoft qui agit comme un courtier d’approbation entre votre organisation locale et l’organisation Office 365. La fonction de fédération est un élément nécessaire à la création d’une relation d’organisation entre l’organisation locale et l’organisation Exchange Online.
    
    Pour plus d'informations, consultez la rubrique [Fédération](https://technet.microsoft.com/fr-fr/library/dd335047\(v=exchg.150\)).

  - **Relations organisationnelles**   Les serveurs Exchange 2013 dotés du rôle d’accès au client et les serveurs Exchange 2016 permettent de créer des relations organisationnelles entre les organisations locale et Exchange Online. Les relations organisationnelles sont nécessaires pour de nombreux autres services dans un déploiement hybride, tels que le partage des informations de disponibilité du calendrier, le suivi des messages et les déplacements de boîtes aux lettres entre l’organisation locale et l’organisation Exchange Online.
    
    Pour plus d'informations, consultez la rubrique [Partage](https://technet.microsoft.com/fr-fr/library/dd638083\(v=exchg.150\)).

  - **Transport de messages**   Les serveurs Exchange dotés des rôles serveur d'accès au client et de boîte aux lettres sont chargés d'assurer le transport des messages dans un déploiement hybride. À l'aide des connecteurs d'envoi et de réception, ils servent de points de terminaison de connexion pour les messages externes entrants et assurent également la remise des messages sortants sur Internet et dans l'organisation Exchange Online.
    
    Pour plus d'informations, consultez la rubrique [Options de transport dans les déploiements hybrides Exchange](transport-options-in-exchange-hybrid-deployments-exchange-2013-help.md).

  - **Sécurité du transport des messages**   Les serveurs Exchange dotés des rôles serveur d'accès au client et de boîte aux lettres contribuent à la sécurisation des messages échangés entre l'organisation locale et l'organisation Exchange Online à l'aide de la fonctionnalité Sécurité du domaine d'Exchange. La sécurité peut être renforcée par l'authentification TLS (Transport Layer Security) mutuelle et le chiffrement des messages échangés.
    
    Pour plus d'informations, consultez la rubrique [Présentation de la sécurité de domaine](http://go.microsoft.com/fwlink/p/?linkid=266581).

  - **Outlook sur le web (appelé Outlook Web App dans Exchange 2013)**   Les serveurs Exchange 2013 dotés du rôle d’accès au client et les serveurs Exchange 2016 dotés du rôle de boîte aux lettres prennent en charge la configuration d’un point de terminaison URL unique pour les connexions externes aux boîtes aux lettres locales et Exchange Online. Pour les boîtes aux lettres locales, les serveurs Exchange sont configurés pour traiter des demandes Outlook sur le web. Pour les boîtes aux lettres de l’organisation Exchange Online, les serveurs Exchange sont configurés pour afficher automatiquement un lien vers le point de terminaison Outlook sur le web dans l’organisation Exchange Online.
    
    Pour plus d'informations, consultez la rubrique [Outlook Web App](https://technet.microsoft.com/fr-fr/library/jj657718\(v=exchg.150\)).

