---
title: 'Configuration des propriétés du groupe de disponibilité de base de données: Exchange 2013 Help'
TOCTitle: Configuration des propriétés du groupe de disponibilité de base de données
ms:assetid: 50daeac5-a16f-4362-a325-19e0fe25d59d
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dd297985(v=EXCHG.150)
ms:contentKeyID: 50478181
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configuration des propriétés du groupe de disponibilité de base de données

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2014-06-24_

Vous pouvez utiliser le Centre d’administration Exchange (CAE) ou l’environnement de ligne de commande Exchange Management Shell pour configurer les propriétés du groupe de disponibilité de base de données (DAG), y compris l’adresse IP du DAG, ainsi que le serveur et répertoire témoins utilisés par le groupe de disponibilité de base de données. L’environnement de ligne de commande Exchange Management Shell vous permet de configurer les propriétés du DAG qui ne sont pas accessibles dans le CAE, telles que les informations relatives au serveur et répertoire témoins de remplacement, le port TCP utilisé pour la réplication et le mode de coordination de l’activation du centre de données (DAC).

## Ce qu’il faut savoir avant de commencer ?

  - Durée d’exécution estimée : 1 minute

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Groupes de disponibilité de la base de données » dans la rubrique [Autorisations de haute disponibilité et de résilience des sites](high-availability-and-site-resilience-permissions-exchange-2013-help.md).

  - Les valeurs des propriétés du DAG sont stockées dans Active Directory et dans la base de données de clusters. Toutefois, certaines propriétés sont enregistrées uniquement dans la base de données de clusters. Par conséquent, le cluster sous-jacent du groupe de disponibilité de base de données doit être en cours d’exécution et avoir atteint le quorum afin de définir les propriétés des éléments suivants :
    
      - ReplicationPort
    
      - NetworkCompression
    
      - NetworkEncryption
    
      - DiscoverNetworks

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..


## Que souhaitez-vous faire ?

## Utiliser l’EAC pour configurer les propriétés du groupe de disponibilité de base de données

1.  Dans le CAE, accédez à **Serveurs** \> **Groupes de disponibilité de base de données**.

2.  Sélectionnez le DAG que vous voulez configurer, puis cliquez sur ![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

3.  
    
    Utilisez la page **Général** pour afficher l'appartenance au groupe de disponibilité de base de données et l'état opérationnel et pour configurer le serveur témoin du groupe de disponibilité de base de données, le répertoire témoin et la configuration du réseau automatique :
    
      - **Serveur témoin**   Nom d’hôte ou nom de domaine complet du serveur témoin pour ce groupe de disponibilité de base de données. Bien qu’il s’agisse d’une propriété obligatoire pour tous les groupes de disponibilité de base de données, le serveur témoin est utilisé lorsqu’il y a un nombre pair de membres du DAG et que le modèle de quorum utilisé par le cluster est Nœud et partage de fichiers majoritaires.
    
      - **Répertoire témoin**   Le chemin entier du répertoire utilisé pour stocker le fichier témoin .log sur le serveur témoin. Bien qu’il s’agisse d’une propriété obligatoire pour tous les groupes de disponibilité de base de données, le répertoire témoin n’est utilisé que lorsque le serveur témoin du groupe de disponibilité de base de données est utilisé.
    
      - **Serveurs opérationnels**   Champ en lecture seule qui affiche une liste de membres du groupe de disponibilité de base de données et leur état opérationnel actuel.
    
      - **Configurer le réseau des groupes de base de données manuellement**   Case à cocher que vous activez lorsque vous souhaitez configurer tous les réseaux DAG manuellement. Si vous n’activez pas cette case à cocher, le système configure les réseaux DAG automatiquement selon la configuration de l’interface réseau. Si cette case à cocher est activée, les cmdlets **Set-DatabaseAvailabilityGroupNetwork** et **New-DatabaseAvailabilityGroupNetwork** sont désactivées pour une utilisation administrative dans le groupe de disponibilité de base de données.

4.  
    
    Utilisez la page **Adresse IP** pour afficher et modifier les adresses IP assignées au groupe de disponibilité de base de données :
    
      - Sélectionnez une adresse IP existante et cliquez sur ![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier") pour la modifier.
    
      - Sélectionnez une adresse IP existante et cliquez sur l'icone moins (supprimer) pour la supprimer.
    
      - Entrez une adresse IP et cliquez sur ![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter") pour l'ajouter au DAG.

5.  
    
    Cliquez sur **Enregistrer** pour enregistrer les modifications apportées.

## Utiliser l’environnement de ligne de commande Exchange Management Shell pour configurer les propriétés du groupe de disponibilité de base de données

Cet exemple définit le répertoire témoin sur C:\\DAG1DIR pour un groupe de disponibilité de base de données appelé DAG1.

    Set-DatabaseAvailabilityGroup -Identity DAG1 -WitnessDirectory C:\DAG1DIR

Cet exemple préconfigure un autre serveur témoin de CAS3 et un autre répertoire témoin de C:\\DAGFileShareWitnesses\\DAG1.contoso.com pour le DAG DAG1.

    Set-DatabaseAvailabilityGroup -Identity DAG1 -AlternateWitnessDirectory C:\DAGFileShareWitnesses\DAG1.contoso.com -AlternateWitnessServer CAS3

Cet exemple montre comment configurer le groupe de disponibilité de base de données DAG1 afin d’utiliser DHCP pour obtenir une adresse IP.

    Set-DatabaseAvailabilityGroup -Identity DAG1 -DatabaseAvailabilityGroupIPAddresses 0.0.0.0

Cet exemple configure un groupe de disponibilité de base de données appelé DAG1 qui utilise une adresse IP statique de 10.0.0.8.

    Set-DatabaseAvailabilityGroup -Identity DAG1 -DatabaseAvailabilityGroupIPAddresses 10.0.0.8

Cet exemple configure le groupe de disponibilité de base de données de sous-réseaux multiples appelé DAG1 avec plusieurs adresses IP statiques.

    Set-DatabaseAvailabilityGroup -Identity DAG1 -DatabaseAvailabilityGroupIPAddresses 10.0.0.8,10.0.1.8

Cet exemple configure le groupe de disponibilité de base de données DAG1 pour son utilisation en mode d’activation du centre de données.

    Set-DatabaseAvailabilityGroup -Identity DAG1 -DatacenterActivationMode DagOnly

Cet exemple montre comment configurer le port de réplication 63132 pour le groupe de disponibilité de base de données DAG1.

    Set-DatabaseAvailabilityGroup -Identity DAG1 -ReplicationPort 63132

> [!NOTE]
> Après avoir modifié le port de réplication par défaut d’un DAG, vous devez modifier manuellement les exceptions de pare-feu sur chaque membre du DAG pour autoriser la communication sur le port spécifié.


## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez bien configuré le groupe de disponibilité de base de données, procédez comme suit :

  - Dans l’environnement de ligne de commande Exchange Management Shell, exécutez la commande suivante pour afficher les paramètres de configuration du groupe de disponibilité de base de données et vérifier la bonne configuration du DAG :
    
        Get-DatabaseAvailabilityGroup <DAGName> | Format-List

## Pour plus d'informations

[Créer un groupe de disponibilité de base de données](create-a-database-availability-group-exchange-2013-help.md)

[Supprimer un groupe de disponibilité de la base de données](remove-a-database-availability-group-exchange-2013-help.md)

[Création d’un réseau de groupe de disponibilité de la base de données](create-a-database-availability-group-network-exchange-2013-help.md)

[Gérer l’appartenance au groupe de disponibilité de la base de données](manage-database-availability-group-membership-exchange-2013-help.md)

[Get-DatabaseAvailabilityGroup](https://technet.microsoft.com/fr-fr/library/dd351226\(v=exchg.150\))

[Set-DatabaseAvailabilityGroup](https://technet.microsoft.com/fr-fr/library/dd297934\(v=exchg.150\))

