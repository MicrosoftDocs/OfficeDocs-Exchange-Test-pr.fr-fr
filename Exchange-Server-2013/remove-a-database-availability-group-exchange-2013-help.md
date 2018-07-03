---
title: 'Supprimer un groupe de disponibilité de la base de données: Exchange 2013 Help'
TOCTitle: Supprimer un groupe de disponibilité de la base de données
ms:assetid: 071296e9-31b0-40f4-9a02-177d97486ebd
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dd335069(v=EXCHG.150)
ms:contentKeyID: 50477464
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Supprimer un groupe de disponibilité de la base de données

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2012-11-16_

Vous pouvez supprimer rapidement et facilement un groupe de disponibilité de base de données (DAG). Vous pouvez utiliser le Centre d'administration Exchange (CAE) ou l’environnement de ligne de commande Exchange Management pour supprimer un groupe de disponibilité de base de données.

Souhaitez-vous rechercher les autres tâches de gestion relatives aux groupes de disponibilité de bases de données ? Consultez la rubrique [Gestion de groupes de disponibilité de base de données](managing-database-availability-groups-exchange-2013-help.md).

## Ce que vous devez savoir avant de commencer

  - Durée d’exécution estimée : 1 minute

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Groupes de disponibilité de la base de données » dans la rubrique [Autorisations de haute disponibilité et de résilience des sites](high-availability-and-site-resilience-permissions-exchange-2013-help.md).

  - Pour pouvoir être supprimé, un DAG doit être vide. Si le DAG que vous voulez supprimer contient des serveurs de boîtes aux lettres, vous devez tout d'abord supprimer les serveurs du DAG. Pour connaître la procédure détaillée de suppression d'un serveur de boîtes aux lettres d'un DAG, voir [Gérer l’appartenance au groupe de disponibilité de la base de données](manage-database-availability-group-membership-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..


## Que souhaitez-vous faire ?

## Utiliser le Centre d’administration Exchange pour supprimer un groupe de disponibilité de base de données

1.  Accédez à **Serveurs** \> **Groupes de disponibilité de la base de données**.

2.  Sélectionnez le DAG à supprimer et cliquez sur **Supprimer**![Icône Supprimer](images/Dd979797.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "Icône Supprimer").

3.  Cliquez sur **Oui** pour confirmer que vous avez lu le message d’avertissement et supprimer le DAG.

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour supprimer un groupe de disponibilité de base de données

Cet exemple montre comment supprimer le groupe de disponibilité de base de données DAG1.

    Remove-DatabaseAvailabilityGroup -Identity DAG1

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez bien supprimé le groupe de disponibilité de base de données, procédez de l’une des manières suivantes :

  - Dans le Centre d’administration Exchange, accédez à **Serveurs** \> **Groupes de disponibilité de base de données** et vérifiez si le groupe de disponibilité de base de données est toujours affiché.

  - Dans l’environnement de ligne de commande Exchange Management Shell, exécutez la commande suivante pour voir si le DAG existe toujours :
    
        Get-DatabaseAvailabilityGroup <DAGName>
    
    Si le DAG a été correctement supprimé, un message d’erreur indiquant que l’objet est introuvable s’affiche lorsque vous exécutez la commande précédente.

