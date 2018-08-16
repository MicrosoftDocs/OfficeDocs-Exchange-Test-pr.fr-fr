---
title: 'Gérer l’appartenance au groupe de disponibilité de la BDD: Exchange 2013 Help'
TOCTitle: Gérer l’appartenance au groupe de disponibilité de la base de données
ms:assetid: fb2ea15e-96d5-4045-b75b-b0aa5fc60479
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dd351278(v=EXCHG.150)
ms:contentKeyID: 50479608
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Gérer l’appartenance au groupe de disponibilité de la base de données

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2014-08-13_

Lorsque vous ajoutez un serveur à un groupe de disponibilité de base de données (DAG), il coopère avec les autres serveurs de ce groupe afin de fournir une récupération automatique au niveau de la base de données en cas de défaillance de base de données, de serveur ou du réseau. Si vous supprimez un serveur d’un groupe de disponibilité de base de données (DAG), il n’est plus automatiquement protégé contre les défaillances.

Souhaitez-vous rechercher les autres tâches de gestion relatives aux groupes de disponibilité de bases de données ? Consultez la rubrique [Gestion de groupes de disponibilité de base de données](managing-database-availability-groups-exchange-2013-help.md).

## Ce que vous devez savoir avant de commencer

  - Durée d’exécution estimée : 5 minutes par serveur

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l’entrée « Groupes de disponibilité de la base de données » dans la rubrique [Autorisations de haute disponibilité et de résilience des sites](high-availability-and-site-resilience-permissions-exchange-2013-help.md).

  - Les groupes de disponibilité de la base de données utilisent les technologies de clustering avec basculement Windows. Chaque serveur de boîte aux lettres membre d’un groupe de disponibilité de la base de données constitue également un nœud dans le cluster sous-jacent, utilisé par le groupe de disponibilité de la base de données. En conséquence, un serveur de boîte aux lettres ne peut être membre que d’un seul groupe de disponibilité de la base de données à la fois. Comme les groupes de disponibilité de base de données (DAG) utilisent la technologie WFC, tous les serveurs ajoutés à un groupe doivent exécuter le même système d’exploitation : Windows Server 2008 R2 édition Enterprise ou Datacenter, ou l’édition Standard ou Datacenter Edition de Windows Server 2012 ou de Windows Server 2012 R2.

  - Si vous ajoutez des serveurs de boîtes aux lettres qui exécutent Windows Server 2012, vous devez préconfigurer l’objet nom de cluster pour le groupe de disponibilité de base de données (DAG). Si vous ajoutez des serveurs de boîtes aux lettres exécutant Windows Server 2012 R2 et que votre DAG n’a pas de point d’accès administratif, vous n’avez pas besoin de préconfigurer de CNO, car les DAG sans point d’accès administratif n’en ont pas. Pour obtenir la procédure détaillée, voir [Préinstallation de l’objet nom de cluster pour un groupe de disponibilité de base de données](pre-stage-the-cluster-name-object-for-a-database-availability-group-exchange-2013-help.md).

  - Avant de pouvoir ajouter des membres à un groupe de disponibilité de base de données, vous devez d’abord créer ce groupe. Pour obtenir la procédure détaillée, voir [Créer un groupe de disponibilité de base de données](create-a-database-availability-group-exchange-2013-help.md).

  - Vous devez supprimer toutes les copies de bases de données répliquées du serveur avant de pouvoir les supprimer d'un groupe de disponibilité de la base de données.

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..


## Que souhaitez-vous faire ?

## Utiliser le CAE (Centre d’administration Exchange) pour gérer l’appartenance à un groupe de disponibilité de la base de données

1.  Dans le CAE, accédez à **Serveurs** \> **Groupes de disponibilité de la base de données**.

2.  Sélectionnez le groupe de disponibilité de base de données que vous souhaitez configurer, puis cliquez sur ![Gérer les membres DAG](images/Dd351278.d567ae56-d6cd-4edb-ab67-ad8f7c58f337(EXCHG.150).gif "Gérer les membres DAG").
    
      - Pour ajouter un ou plusieurs serveurs de boîtes aux lettres à un groupe de disponibilité de base de données (DAG), cliquez sur ![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter"), sélectionnez les serveurs dans la liste, puis cliquez sur **Ajouter** et ensuite sur **OK**.
    
      - Pour supprimer un ou plusieurs serveurs de boîtes aux lettres d’un groupe de disponibilité de base de données (DAG), sélectionnez le ou les serveurs, puis cliquez sur le signe moins (-).

3.  Cliquez sur **Enregistrer** pour enregistrer les modifications.

4.  Lorsque cette tâche est terminée, cliquez sur **Fermer**.

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour gérer l'appartenance à un groupe de disponibilité de la base de données

Cet exemple ajoute le serveur de boîte aux lettres MBX1 au DAG DAG1.

    Add-DatabaseAvailabilityGroupServer -Identity DAG1 -MailboxServer MBX1

Cet exemple supprime le serveur de boîte aux lettres MBX1 du groupe de disponibilité de base de données (DAG) DAG3. Avant d'exécuter cette commande, assurez-vous qu'il n'existe aucune base de données répliquée sur le serveur de boîtes aux lettres.

    Remove-DatabaseAvailabilityGroupServer -Identity DAG1 -MailboxServer MBX1

Cet exemple supprime les paramètres de configuration du serveur de boîte aux lettres nommé MBX4 à partir du DAG DAG2. MBX4 devrait être hors connexion pendant une période prolongée ; sa configuration est donc supprimée du groupe de disponibilité de base de données (DAG) pendant qu’il est hors connexion, afin d’établir le quorum avec les membres restants du groupe de disponibilité de base de données (DAG) qui sont en ligne.

    Remove-DatabaseAvailabilityGroupServer -Identity DAG2 -MailboxServer MBX4 -ConfigurationOnly

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez correctement géré l’appartenance à un groupe de disponibilité de base de données, procédez comme suit :

  - Dans le CAE, accédez à **Serveurs** \> **Groupes de disponibilité de la base de données**. L’appartenance actuelle au groupe de disponibilité de base de données est affichée dans la colonne **Serveurs membres**.

  - Dans l’environnement de ligne de commande Exchange Management Shell, exécutez la commande suivante pour afficher les informations d’appartenance au groupe de disponibilité de base de données (DAG) :
    
        Get-DatabaseAvailabilityGroup <DAGName> | Format-List Servers

## Pour plus d’informations

[Add-DatabaseAvailabilityGroupServer](https://technet.microsoft.com/fr-fr/library/dd298049\(v=exchg.150\))

[Remove-DatabaseAvailabilityGroupServer](https://technet.microsoft.com/fr-fr/library/dd297956\(v=exchg.150\))

