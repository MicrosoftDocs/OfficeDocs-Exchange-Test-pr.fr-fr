---
title: 'Créer un groupe de disponibilité de base de données: Exchange 2013 Help'
TOCTitle: Créer un groupe de disponibilité de base de données
ms:assetid: d6b98299-e203-488b-af73-50753fe152c8
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dd351172(v=EXCHG.150)
ms:contentKeyID: 50479330
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Créer un groupe de disponibilité de base de données

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2015-04-07_

Un groupe de disponibilité de base de données (DAG) est composé d’un maximum de 16 serveurs de boîtes aux lettres Microsoft Exchange Server 2013 qui permettent une récupération automatique au niveau de la base de données en cas de défaillance d’une base de données, d’un serveur ou du réseau. Lorsqu'un serveur de boîtes aux lettres est ajouté à un groupe de disponibilité de base de données, il fonctionne avec les autres serveurs du DAG pour assurer la récupération automatique des défaillances de la base de données, du serveur ou du réseau.

Souhaitez-vous rechercher les autres tâches de gestion relatives aux groupes de disponibilité de bases de données ? Consultez la rubrique [Gestion de groupes de disponibilité de base de données](managing-database-availability-groups-exchange-2013-help.md).

## Ce que vous devez savoir avant de commencer

  - Durée d’exécution estimée : 1 minute

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l’entrée « Groupes de disponibilité de la base de données » dans la rubrique [Autorisations de haute disponibilité et de résilience des sites](high-availability-and-site-resilience-permissions-exchange-2013-help.md).

  - Lors de la création d’un groupe de disponibilité de base de données (DAG) avec des serveurs de boîtes aux lettres qui exécutent Windows Server 2012, vous devez préconfigurer l’objet nom de cluster avant d’ajouter des membres au groupe de disponibilité de base de données (DAG). Si vous créez un DAG sans point d’accès administratif avec les serveurs de boîtes aux lettres exécutant Windows Server 2012 R2, vous n’avez pas besoin de prédéfinir un CNO pour le DAG. Pour obtenir la procédure détaillée, voir [Préinstallation de l’objet nom de cluster pour un groupe de disponibilité de base de données](pre-stage-the-cluster-name-object-for-a-database-availability-group-exchange-2013-help.md).

  - Lorsque vous créez un DAG, vous lui donnez un nom unique contenant 15 caractères au maximum. En plus d’attribuer un nom au DAG, vous devez y affecter une ou plusieurs adresses IP (soit IPv4 soit IPv4 et IPv6), sauf si vous créez un DAG Windows Server 2012 R2 sans point d’accès administratif et que vous n’affectez aucune adresse IP au DAG. Sinon, les adresses IP doivent figurer sur chaque sous-réseau destiné au réseau MAPI et être disponibles. Si vous spécifiez une ou plusieurs adresses IPv4 et que votre système est configuré pour utiliser IPv6, la tâche tentera également d’attribuer automatiquement une ou plusieurs adresses IPv6 au DAG.

  - Lors de la création d’un groupe de disponibilité de base de données (DAG), vous pouvez éventuellement spécifier un serveur témoin et un répertoire témoin. Si vous spécifiez un serveur témoin, nous recommandons d’utiliser un serveur d’accès au client dans lequel le rôle serveur de boîte aux lettres n’est pas installé. Cela permet à un administrateur Exchange de connaître la disponibilité du témoin et de s’assurer que toutes les autorisations de sécurité nécessaires pour utiliser le serveur témoin sont en place.
    
    Les combinaisons suivantes de comportements et d'options sont disponibles :
    
      - Vous pouvez n’attribuer un nom qu’au groupe de disponibilité de base de données et laisser les champs **Serveur témoin** et **Répertoire témoin** vides. Dans ce scénario, la tâche recherchera un serveur d’accès au client dans lequel le rôle serveur de boîte aux lettres n’est pas installé. Elle créera automatiquement le répertoire témoin et le partage par défaut sur le serveur d’accès au client et configurera le groupe de disponibilité de base de données pour utiliser ce serveur comme serveur témoin propre.
    
      - Vous pouvez donner un nom au groupe de disponibilité de base de données, au serveur témoin que vous souhaitez utiliser et au répertoire qui sera créé et partagé sur le serveur témoin.
    
      - Vous pouvez attribuer un nom au groupe de disponibilité de base de données et au serveur témoin que vous souhaitez utiliser, et laisser le champ **Répertoire témoin** vide. Dans ce scénario, la tâche créera le répertoire témoin par défaut sur le serveur témoin spécifié.
    
      - Vous pouvez attribuer un nom au groupe de disponibilité de base de données, laisser le champ **Serveur témoin** vide et spécifier le répertoire que vous voulez créer et partager sur le serveur témoin. Dans ce scénario, l’Assistant recherchera un serveur d’accès au client dans lequel le rôle serveur de boîte aux lettres n’est pas installé et créera automatiquement le répertoire témoin spécifié sur ce serveur, partagera le répertoire et configurera le groupe de disponibilité de base de données pour utiliser ce serveur d’accès au client comme son propre serveur témoin.
    
    > [!IMPORTANT]
	> Si le serveur témoin que vous spécifiez n’est pas un serveur Exchange 2013 ou Exchange 2010, vous devez ajouter le groupe de sécurité universel du sous-système approuvé Exchange au groupe Administrateurs local sur le serveur témoin. Ces autorisations de sécurité sont nécessaires pour garantir qu'Exchange peut créer un répertoire et un partage sur le serveur témoin si nécessaire. Si les autorisations appropriées ne sont pas configurées, l'erreur suivante est retournée :<br />
    > <code>Error: An error occurred during discovery of the database availability group topology. Error: An error occurred while attempting a cluster operation. Error: Cluster API &quot;AddClusterNode() (MaxPercentage=12) failed with 0x80070005. Error: Access is denied.&quot;</code>
    
  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..


## Que souhaitez-vous faire ?

## Utiliser le CAE pour créer un groupe de disponibilité de base de données

1.  Dans le CAE, accédez à **Serveurs** \> **Groupes de disponibilité de la base de données**.

2.  Cliquez sur ![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter") pour créer un groupe de disponibilité de base de données.

3.  Sur la page **Nouveau groupe de disponibilité de base de données**, entrez les informations suivantes pour le groupe de disponibilité de base de données :
    
      - **Nom du groupe de disponibilité de la base de données**   Entrez un nom valide et unique de 15 caractères maximum pour le groupe de disponibilité de base de données. Ce nom est l’équivalent d’un nom d’ordinateur ; un objet réseau de cluster (CNO) correspondant sera créé dans Active Directory avec ce nom. Ce nom est le même pour le groupe de disponibilité de base de données et le cluster sous-jacent.
    
      - **Serveur témoin**   Spécifiez un serveur témoin pour le DAG. Si vous ne renseignez pas ce champ, le système tentera de sélectionner automatiquement un serveur d’accès au client du site Active Directory local installé sur un ordinateur qui n’est pas doté du rôle serveur de boîte aux lettres, pour l’utiliser comme serveur témoin.
        
        > [!NOTE]
        > Si vous spécifiez un serveur témoin, vous devez utiliser un nom d’hôte ou un nom de domaine complet. L'utilisation d'une adresse IP ou d'un nom contenant des caractères génériques n'est pas prise en charge. En outre, le serveur témoin ne peut pas être membre du groupe de disponibilité de base de données (DAG).
    
      - **Répertoire témoin**   Indiquez dans ce champ le chemin d’accès à un répertoire du serveur témoin qui sera utilisé pour stocker des données témoin. Si le répertoire n'existe pas, le système le crée pour vous sur le serveur témoin. Si vous ne renseignez pas ce champ, le répertoire par défaut (%SystemDrive%\\DAGFileShareWitnesses\\\<DAG FQDN\>) sera créé sur le serveur témoin.
    
      - **Adresses IP du groupe de disponibilité de base de données**   Attribuez une ou plusieurs adresses IPv4 statiques au groupe de disponibilité de base de données. Entrez une adresse IPv4, puis cliquez sur ![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter") pour l’ajouter. Laissez ce champ vide si vous voulez que le groupe de disponibilité de base de données (DAG) utilise le protocole DHCP pour obtenir les adresses IPv4 nécessaires. Éventuellement, entrez 255.255.255.255 pour créer un DAG sans adresse IP ni point d’accès administratif de cluster, qui s’applique uniquement aux DAG qui contiendront des serveurs de boîtes aux lettres exécutant Windows Server 2012 R2.

4.  Cliquez sur **Enregistrer** pour créer le DAG.

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour créer un groupe de disponibilité de base de données

Cet exemple illustre la création d’un groupe de disponibilité de base de données nommé DAG1 qui est configuré pour utiliser le serveur témoin FILESRV1 et le répertoire local C:\\DAG1. DAG1 est également configuré pour utiliser le protocole DHCP pour les adresses IP du groupe de disponibilité de base de données.

    New-DatabaseAvailabilityGroup -Name DAG1 -WitnessServer FILESRV1 -WitnessDirectory C:\DAG1

Cet exemple décrit la création du DAG DAG2. Le système sélectionne automatiquement un serveur d’accès au client dans le site Active Directory local qui ne contient pas le rôle serveur de boîte aux lettres en tant que serveur témoin du DAG. Une adresse IP statique unique est affectée à DAG2 car, dans cet exemple, tous les membres du DAG accèdent au réseau MAPI sur le même sous-réseau.

    New-DatabaseAvailabilityGroup -Name DAG2 -DatabaseAvailabilityGroupIPAddresses 10.0.0.8

Cet exemple crée le DAG DAG3. DAG3 est configuré pour utiliser le serveur témoin MBX2 et le répertoire local C:\\DAG3. Plusieurs adresses IP statiques sont attribuées à DAG3, car les membres du DAG sont sur des sous-réseaux différents du réseau MAPI.

    New-DatabaseAvailabilityGroup -Name DAG3 -WitnessServer MBX2 -WitnessDirectory C:\DAG3 -DatabaseAvailabilityGroupIPAddresses 10.0.0.8,192.168.0.8

Dans cet exemple, nous créons le groupe de disponibilité de base de données DAG4 configuré pour utiliser le protocole DHCP. En outre, le système sélectionne automatiquement le serveur témoin et le répertoire témoin par défaut est créé.

    New-DatabaseAvailabilityGroup -Name DAG4

Cet exemple crée le DAG DAG5, auquel aucun point d’accès administratif ne sera attribué (valable pour les DAG Windows Server 2012 R2 uniquement). En outre, MBX4 sera utilisé comme serveur témoin pour le DAG, et le répertoire témoin par défaut sera créé.

    New-DatabaseAvailabilityGroup -Name DAG5 -DatabaseAvailabilityGroupIPAddresses ([System.Net.IPAddress]::None) -WitnessServer MBX4

## Comment savoir si cela a fonctionné ?

Pour vérifier qu’un groupe de disponibilité de base de données a bien été créé, effectuez l’une des opérations suivantes :

  - Dans le CAE, accédez à **Serveurs** \> **Groupes de disponibilité de la base de données**. Le groupe de disponibilité de base de données créé s’affiche.

  - Dans l’environnement de ligne de commande Exchange Management Shell, exécutez la commande suivante pour vérifier que le DAG a bien été créé et pour afficher des informations sur ses propriétés.
    
        Get-DatabaseAvailabilityGroup <DAGName> | Format-List

## Pour plus d’informations

[Groupe de disponibilité de base de données (DAG)](database-availability-groups-dags-exchange-2013-help.md)

[Configuration des propriétés du groupe de disponibilité de base de données](configure-database-availability-group-properties-exchange-2013-help.md)

[Set-DatabaseAvailabilityGroup](https://technet.microsoft.com/fr-fr/library/dd297934\(v=exchg.150\))

[New-DatabaseAvailabilityGroup](https://technet.microsoft.com/fr-fr/library/dd351107\(v=exchg.150\))

[New-DatabaseAvailabilityGroupNetwork](https://technet.microsoft.com/fr-fr/library/dd335225\(v=exchg.150\))

[Add-DatabaseAvailabilityGroupServer](https://technet.microsoft.com/fr-fr/library/dd298049\(v=exchg.150\))

