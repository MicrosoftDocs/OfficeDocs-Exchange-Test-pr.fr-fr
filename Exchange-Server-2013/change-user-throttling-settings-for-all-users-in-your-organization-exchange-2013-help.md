---
title: 'Modifier param. de limitation d’utlsr pr tous les utlsr de votre organisation'
TOCTitle: Modifier les paramètres de limitation d’utilisateurs pour tous les utilisateurs de votre organisation
ms:assetid: c45cacfc-768d-4605-9bb0-53e30273fe4d
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ863578(v=EXCHG.150)
ms:contentKeyID: 50555480
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Modifier les paramètres de limitation d’utilisateurs pour tous les utilisateurs de votre organisation

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2014-08-05_

Vous pouvez contrôler la façon dont les utilisateurs de votre organisation Exchange utilisent les ressources en modifiant les paramètres de limitation par défaut.

Il était déjà possible de contrôler la façon dont les ressources étaient consommées par des utilisateurs individuels dans Exchange Server 2010. Cette fonctionnalité a été développée pour Exchange Server 2013. La stratégie intitulée GlobalThrottlingPolicy définit les paramètres de limitation par défaut pour les utilisateurs nouveaux et existants de votre organisation, sauf si vous avez personnalisé les stratégies de limitation. Dans de nombreux scénarios classiques de déploiement Exchange, la stratégie GlobalThrottlingPolicy doit convenir pour gérer vos utilisateurs.

Pour personnaliser les paramètres de limitation qui s’appliquent à tous les utilisateurs de votre organisation, créez une nouvelle stratégie de limitation avec l’affectation de l’étendue Organisation. Seul l’environnement de ligne de commande Exchange Management Shell vous permet de modifier les paramètres de limitation par défaut.

## Ce qu’il faut savoir avant de commencer ?

  - Durée d'exécution estimée : 10 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Limitation de l'utilisateur » dans la rubrique [Autorisations sur l’intégrité et les performances du serveur](server-health-and-performance-permissions-exchange-2013-help.md).

  - Dans les nouvelles stratégies à étendue Organisation, vous ne devez définir que les paramètres de limitation qui sont différents de ceux de la stratégie GlobalThrottlingPolicy et de toute autre stratégie organisationnelle. En procédant de cette manière, le reste des paramètres de stratégie de la stratégie GlobalThrottlingPolicy doivent être hérités, ainsi que toutes les mises à jour de stratégies de limitation qui seront ajoutées dans les mises à jour futures d’Exchange. Nous recommandons de revoir la section « Gérer des stratégies de limitation à l’aide d’étendues » dans la rubrique [Gestion de la charge de travail Exchange](exchange-workload-management-exchange-2013-help.md) avant de poursuivre cette procédure.

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..


## Utiliser l’environnement de ligne de commande Exchange Management Shell pour modifier la manière dont les ressources peuvent être utilisées par tous les utilisateurs de toute votre organisation

Cet exemple illustre la création d’une stratégie de limitation applicable à tous les utilisateurs de votre organisation. Les paramètres que vous omettez héritent des valeurs de la stratégie de limitation par défaut (GlobalThrottlingPolicy).

    New-ThrottlingPolicy -Name AllUsersEWSPolicy EwsMaxConcurrency 4 -ThrottlingPolicyScope Organization

Pour plus d'informations sur la syntaxe et les paramètres, voir [New-ThrottlingPolicy](https://technet.microsoft.com/fr-fr/library/dd351045\(v=exchg.150\)).

## Comment savoir si cela a fonctionné ?

Pour vérifier que la stratégie de limitation Organisation a été correctement créée, procédez comme suit :

1.  Exécutez la commande suivante.
    
        Get-ThrottlingPolicy | Format-List

2.  Vérifiez que la stratégie de limitation Organisation que vous venez de créer est répertoriée dans la colonne qui affiche l’objet GlobalThrottlingPolicy.

3.  Exécutez la commande suivante.
    
        Get-ThrottlingPolicy | Format-List

4.  Vérifiez que les propriétés associées à la nouvelle stratégie Organisation correspondent à la valeur ou aux valeurs que vous avez configurées.

