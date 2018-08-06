---
title: 'Déployer des topologies à plsr forêts pour Exchange 2013: Exchange 2013 Help | Microsoft Docs'
TOCTitle: Déploiement de topologies à plusieurs forêts pour Exchange 2013
ms:assetid: d51f2b7d-9045-40cf-8b9f-43787a6fff6d
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb124734(v=EXCHG.150)
ms:contentKeyID: 51407246
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Déploiement de topologies à plusieurs forêts pour Exchange 2013

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2016-12-09_

Cette rubrique offre une vue d'ensemble du déploiement de Microsoft Exchange Server 2013 dans des topologies à forêts multiples. Vous trouverez des informations sur les sujets suivants :

  - **Topologies de forêts multiples prises en charge**   Exchange 2013 prend en charge deux types de topologies de forêts multiples : inter-forêts et forêt de ressources.

  - **Synchronisation de la liste d'adresses globale**   Si vous travaillez dans un environnement inter-forêts, vous devez vous assurer que la liste d'adresses globale (LAG) d'une forêt donnée contient des destinataires d'autres forêts.

  - **Déplacement des boîtes aux lettres entre des forêts**   Les cmdlets **New-MoveRequest** et **New-MigrationBatch** de l'environnement de ligne de commande Exchange Management Shell peuvent aider au déplacement de boîtes aux lettres d'une forêt à une autre.

  - **Présentation de l'administration de plusieurs forêts**   Découvrez le modèle d'autorisations qui vous permettra de configurer et de gérer les autorisations entre vos forêts.

## Topologies de forêts multiples prises en charge

Exchange 2013 prend en charge les types de topologies de forêts multiples suivants :

  - **Inter-forêts**   Une topologie inter-forêt compte plusieurs forêts Exchange. Voici un aperçu des actions à effectuer pour déployer Exchange 2013 dans une topologie avec des forêts multiples :
    
    1.  Vous devez d'abord installer Exchange 2013 dans chaque forêt. Pour plus d'informations, consultez la rubrique [Déployer une nouvelle installation d’Exchange 2013](deploy-a-new-installation-of-exchange-2013-exchange-2013-help.md).
    
    2.  Vous devez ensuite synchroniser les destinataires dans chacune des forêts, de sorte que la liste d'adresses globale de chaque forêt contienne les utilisateurs de toutes les forêts synchronisées. Pour plus d'informations, consultez la section « Synchronisation de la liste d'adresses globale » ci-dessous.
    
    3.  Enfin, vous devez configurer le service de disponibilité de façon à ce que les utilisateurs opérant dans une forêt puissent voir des données de disponibilité sur des utilisateurs opérant dans une autre forêt. Pour plus d'informations, consultez la rubrique [Configuration du service de disponibilité pour des topologies inter-forêts](configure-the-availability-service-for-cross-forest-topologies-exchange-2013-help.md).
    
    Pour plus de détails sur le déploiement d'Exchange 2013 dans une topologie inter-forêts, consultez la rubrique [Déploiement d’Exchange 2013 dans une topologie inter-forêts](deploy-exchange-2013-in-a-cross-forest-topology-exchange-2013-help.md).

  - **Forêt de ressources**   Une topologie de forêt de ressources compte une forêt Exchange et une ou plusieurs forêts de compte d'utilisateur. Voici un aperçu des actions à effectuer pour déployer Exchange 2013 dans une topologie avec une forêt de ressources :
    
    1.  Exchange doit être installé dans une forêt. Dans la forêt Exchange, les comptes d'utilisateurs qui ont des boîtes aux lettres Exchange doivent être désactivés.
    
    2.  Vous devez disposer d'au moins une forêt contenant des comptes d'utilisateurs. Exchange ne doit *pas* être installé dans cette forêt.
    
    3.  Vous devez ensuite associer les comptes d'utilisateurs désactivés dans la forêt Exchange avec les comptes d'utilisateurs figurant dans la forêt des comptes.
    
    Pour en savoir plus sur le déploiement d'Exchange 2013 dans une topologie de forêt de ressources, consultez la rubrique [Déploiement d’Exchange 2013 dans une topologie de forêt ressource Exchange](deploy-exchange-2013-in-an-exchange-resource-forest-topology-exchange-2013-help.md).

## Synchronisation de la liste d'adresses globale

Par défaut, une liste d'adresses globale contient les destinataires de messagerie d'une seule forêt. Si vous travaillez dans un environnement inter-forêts, nous vous recommandons d'utiliser Microsoft Identity Lifecycle Manager (ILM) 2007 Feature Pack 1 (FP1) pour vous assurer que la liste d'adresses globale dans une forêt donnée contient tous les destinataires de messagerie d'autres forêts. ILM 2007 FP1 crée des utilisateurs de messagerie qui représentent des destinataires d'autres forêts, ce qui permet aux utilisateurs de les afficher dans la liste d'adresses globale et d'envoyer du courrier. Par exemple, les utilisateurs de la forêt A apparaissent en tant qu'utilisateur de messagerie dans la forêt B et inversement. Les utilisateurs de la forêt cible peuvent alors sélectionner l'objet utilisateur de messagerie qui représente un destinataire d'une autre forêt et lui envoyer du courrier.

Pour activer la synchronisation de la liste d'adresses globale, vous créez des agents de gestion qui importent les groupes, contacts et utilisateurs à extension messagerie à partir des services Active Directory indiqués vers un métarépertoire centralisé. Dans le métarépertoire, les objets à extension messagerie sont représentés en tant qu'utilisateurs de messagerie. Les groupes sont représentés en tant que contacts sans aucun membre associé. Les agents de gestion exportent alors ces utilisateurs de messagerie vers une unité d'organisation dans la forêt cible spécifiée.

Pour plus d'informations sur Forefront Identity Manager (FIM), consultez la rubrique [Forefront Identity Manager 2010](https://go.microsoft.com/fwlink/p/?linkid=279864).

## Déplacement de boîtes aux lettres entre forêts

Dans une topologie inter-forêts, vous pouvez déplacer des boîtes aux lettres entre des forêts. Pour cela, vous devez utiliser la cmdlet **New-MoveRequest** ou **New-MigrationBatch** dans l'environnement de ligne de commande Exchange Management Shell. Pour plus d'informations sur le déplacement de boîtes aux lettres d'une forêt vers une autre, consultez les rubriques suivantes :

  - [Préparer les boîtes aux lettres pour les demandes de déplacement inter-forêts](prepare-mailboxes-for-cross-forest-move-requests-exchange-2013-help.md)

  - [Préparer des boîtes aux lettres pour des déplacements inter-forêts à l’aide du script Prepare-MoveRequest.ps1 dans l’environnement de ligne de commande Exchange Management Shell](prepare-mailboxes-for-cross-forest-moves-using-the-prepare-moverequest-ps1-script-in-the-shell-exchange-2013-help.md)

  - [Préparer les boîtes aux lettres pour les déplacements inter-forêts à l’aide d’un exemple de code](prepare-mailboxes-for-cross-forest-moves-using-sample-code-exchange-2013-help.md)

## Présentation de l'administration de plusieurs forêts

Exchange 2013 utilise la nouvelle fonctionnalité d'autorisations pour gérer vos environnements de forêts multiples.

Exchange 2013 utilise un modèle d'autorisations de contrôle d'accès basé sur un rôle (RBAC). Les groupes de rôles de gestion dont les administrateurs sont membres et les stratégies d'attribution de rôles de gestion affectées aux utilisateurs finaux déterminent les actions que peuvent entreprendre chaque administrateur et utilisateur final. Pour comprendre les autorisations dans plusieurs forêts, vous devez être familiarisé avec la fonctionnalité de contrôle d'accès basé sur un rôle (RBAC). Pour plus d'informations sur le contrôle d'accès basé sur un rôle (RBAC), les groupes de rôles et les stratégies d'attribution de rôles en particulier, consultez la rubrique [Présentation du contrôle d'accès basé sur un rôle](understanding-role-based-access-control-exchange-2013-help.md).

Vous pouvez recourir au modèle d'autorisations RBAC pour configurer et gérer les autorisations entre vos forêts. Pour plus d'informations sur les autorisations dans plusieurs forêts, consultez les rubriques suivantes :

  - [Présentation des autorisations sur plusieurs forêts](understanding-multiple-forest-permissions-exchange-2013-help.md)

  - [Gérer des groupes de rôles liés](manage-linked-role-groups-exchange-2013-help.md)

  - [Créer des groupes de rôles lié qui reflètent les groupes de rôles intégrés](create-linked-role-groups-that-mirror-built-in-role-groups-exchange-2013-help.md)

