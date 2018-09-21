---
title: 'Création d’un réseau de groupe de disponibilité de la BDD: Exchange 2013 Help'
TOCTitle: Création d’un réseau de groupe de disponibilité de la base de données
ms:assetid: 6caec7be-788a-4058-87a7-f31c575b870c
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dd298051(v=EXCHG.150)
ms:contentKeyID: 50478386
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Création d’un réseau de groupe de disponibilité de la base de données

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2012-11-02_

Si nécessaire, vous pouvez créer des réseaux supplémentaires en vue de les utiliser dans un groupe de disponibilité de base de données (DAG). Vous pouvez utiliser le Centre d’administration Exchange (CAE) ou l’environnement de ligne de commande Exchange Management pour créer un groupe de disponibilité de base de données.

Souhaitez-vous rechercher les autres tâches de gestion relatives aux groupes de disponibilité de bases de données ? Consultez la rubrique [Gestion de groupes de disponibilité de base de données](managing-database-availability-groups-exchange-2013-help.md).

## Ce que vous devez savoir avant de commencer

  - Durée d’exécution estimée : 1 minute

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Groupes de disponibilité de la base de données » dans la rubrique [Autorisations de haute disponibilité et de résilience des sites](high-availability-and-site-resilience-permissions-exchange-2013-help.md).

  - Vous pouvez créer un réseau DAG uniquement si la configuration automatique du réseau a été activée pour un DAG. Pour obtenir la procédure détaillée de désactivation d’une configuration de réseau automatique pour un DAG, consultez la rubrique [Configuration des propriétés du groupe de disponibilité de base de données](configure-database-availability-group-properties-exchange-2013-help.md).

  - Lors de la création d’un réseau DAG, vous devez attribuer des sous-réseaux uniques qui ne sont pas utilisés par un autre réseau DAG. Si vous utilisez des sous-réseaux qui sont attribués à un réseau DAG existant, ils seront supprimés de ce réseau DAG et ajoutés au réseau DAG nouvellement créé.

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]  
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..


## Que souhaitez-vous faire ?

## Utiliser le Centre d’administration Exchange (EAC) pour créer un réseau de groupe de disponibilité de base de données

1.  Dans le CAE, accédez à **Serveurs** \> **Groupes de disponibilité de base de données**.

2.  Sélectionnez le groupe de disponibilité de base de données que vous souhaitez configurer, puis cliquez sur ![Ajouter un réseau DAG](images/Dd298051.befcdc4e-7f7a-451d-a0a8-608c79f5d186(EXCHG.150).gif "Ajouter un réseau DAG").

3.  Sur la page **Nouveau réseau de groupe de disponibilité de la base de données**, fournissez les informations suivantes :
    
      - **Nom du réseau du groupe de disponibilité de base de données**   Entrez dans ce champ un nom de réseau unique dans le groupe de disponibilité de base de données.
    
      - **Description**   Utilisez ce champ pour fournir une description textuelle du réseau DAG.
    
      - **Sous-réseaux**   Utilisez ce champ pour associer un ou plusieurs sous-réseaux au réseau DAG. Cliquez sur ![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter") pour ajouter un sous-réseau, cliquez sur ![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier") pour modifier un sous-réseau et cliquez sur le signe moins (-) pour supprimer un sous-réseau.

4.  Cliquez sur **Enregistrer** pour créer le réseau DAG.

## Utiliser le shell pour créer un réseau dans un groupe de disponibilité de base de données

Cet exemple montre comment créer le réseau ReplicationDagNetwork02 avec le sous-réseau 10.0.0.0 et le masque de bits 8 dans le groupe de disponibilité de base de données DAG1. La réplication est activée pour le réseau et une description optionnelle du réseau est également ajoutée.

    New-DatabaseAvailabilityGroupNetwork -DatabaseAvailabilityGroup DAG1 -Name ReplicationDagNetwork02 -Description "Replication network 2" -Subnets 10.0.0.0/8 -ReplicationEnabled:$True

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez bien créé un réseau de groupe de disponibilité de base de données, procédez de l’une des manières suivantes :

  - Dans le CAE, accédez à **Serveurs** \> **Groupes de disponibilité de la base de données**. Sélectionnez le DAG approprié. Le réseau DAG nouvellement créé s’affiche alors dans le volet d’informations.

  - Dans l’environnement de ligne de commande Exchange Management Shell, exécutez la commande suivante pour vérifier que le réseau DAG a bien été créé et pour afficher les informations de configuration du réseau DAG :
    
    ```powershell
Get-DatabaseAvailabilityGroupNetwork <DAGNetworkName> | Format-List
```

## Pour plus d'informations

[Set-DatabaseAvailabilityGroupNetwork](https://technet.microsoft.com/fr-fr/library/dd298008\(v=exchg.150\))

[Get-DatabaseAvailabilityGroupNetwork](https://technet.microsoft.com/fr-fr/library/dd297938\(v=exchg.150\))

[New-DatabaseAvailabilityGroupNetwork](https://technet.microsoft.com/fr-fr/library/dd335225\(v=exchg.150\))

[Remove-DatabaseAvailabilityGroupNetwork](https://technet.microsoft.com/fr-fr/library/dd298131\(v=exchg.150\))

