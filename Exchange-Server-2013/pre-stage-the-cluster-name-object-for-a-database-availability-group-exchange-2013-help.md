---
title: 'Préinstallation de l’objet nom de cluster pr un groupe de dispo. de BDD'
TOCTitle: Préinstallation de l’objet nom de cluster pour un groupe de disponibilité de base de données
ms:assetid: 51ebf2f6-8a02-44ef-a489-ca361cb0f63a
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Ff367878(v=EXCHG.150)
ms:contentKeyID: 50478114
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Préinstallation de l’objet nom de cluster pour un groupe de disponibilité de base de données

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2014-08-14_

Dans des environnements où la création d’un compte d’ordinateur est limitée ou des comptes d’ordinateurs sont créés dans un conteneur autre que le conteneur d’ordinateurs par défaut, vous pouvez préinstaller l’objet nom de cluster (CNO), puis le configurer en lui affectant des autorisations. La préparation du CNO est également nécessaire pour les membres du DAG Windows Server 2012 ou Windows Server 2012 R2 en raison des modifications apportées aux autorisations dans Windows pour les objets Ordinateur. Lors du déploiement d’un groupe de disponibilité de base de données (DAG) à l’aide des serveurs de boîtes aux lettres qui exécutent Windows Server 2012 ou Windows Server 2012 R2, vous devez préinstaller et configurer le CNO, sauf si vous déployez un DAG sans point d’accès d’administration du cluster. Les DAG sans points d’accès d’administration du cluster n’utilisent pas de CNO ; la préinstallation n’est pas nécessaire pour ces DAG.

Vous pouvez créer et désactiver un compte d’ordinateur pour l’objet réseau de cluster, puis vous pouvez :

  - attribuer le contrôle total du compte d’ordinateur au compte d’ordinateur du premier serveur de boîte aux lettres ajoutée au groupe de disponibilité de base de données.

  - attribuer le contrôle total du compte d’ordinateur au groupe de sécurité universel du sous-système approuvé Exchange.

## Ce qu’il faut savoir avant de commencer ?

  - Durée d'exécution estimée : 1 minute

  - Vous devez utiliser un compte disposant des autorisations pour créer des objets ordinateur dans Active Directory.

  - Une fois les étapes suivantes terminées, attendez que la réplication d’Active Directory se produise. Après réplication de l’objet, vous pouvez ajouter le premier membre au groupe de disponibilité de base de données.

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..


## Que souhaitez-vous faire ?

## Préconfigurer l’objet réseau de cluster

1.  Ouvrez Utilisateurs et ordinateurs Active Directory.

2.  Développez le nœud de la forêt.

3.  Cliquez avec le bouton droit sur l’unité d’organisation dans laquelle vous souhaitez créer le nouveau compte, sélectionnez **Nouveau**, puis sélectionnez **Ordinateur**.

4.  Dans **Nouvel objet - Ordinateur**, tapez le nom du compte de l’ordinateur pour l’objet réseau de cluster dans la zone **Nom de l’ordinateur**. Il s’agit du nom que vous utiliserez pour le groupe de disponibilité de base de données. Cliquez sur **OK** pour créer le compte.

5.  Cliquez avec le bouton droit sur le nouveau compte d’ordinateur, puis cliquez sur **Désactiver le compte**. Cliquez sur **Oui** pour confirmer la désactivation, puis cliquez sur **OK**.

## Affecter des autorisations à l’objet réseau de cluster

1.  Ouvrez Utilisateurs et ordinateurs Active Directory.

2.  Si les fonctionnalités avancées ne sont pas activées, activez-les en cliquant sur **Affichage**, puis en cliquant sur **Fonctionnalités avancées**.

3.  Cliquez avec le bouton droit sur le nouveau compte d’utilisateur, puis cliquez sur **Propriétés**.

4.  Sous **\<Nom de l’ordinateur\> Propriétés**, sur l’onglet **Sécurité**, cliquez sur **Ajouter** pour ajouter le compte d’ordinateur pour le premier nœud à ajouter au groupe de disponibilité de base de données ou pour ajouter le groupe de sécurité universel du sous-système approuvé Exchange :
    
      - Pour ajouter le sous-système approuvé Exchange, tapez **Exchange Trusted Subsystem** dans le champ **Entrez les noms des objets à sélectionner**. Cliquez sur **OK** pour ajouter le groupe de sécurité universel. Sélectionnez le groupe de sécurité universel du sous-système approuvé Exchange et dans le champ **Autorisations pour le sous-système approuvé Exchange**, sélectionnez **Contrôle total** dans la colonne **Autoriser**. Cliquez sur **OK** pour enregistrer les paramètres d’autorisation.
    
      - Pour ajouter le compte d’ordinateur au premier nœud à ajouter au groupe de disponibilité de base de données, cliquez sur **Types d’objets**. Dans la boîte de dialogue **Types d’objets**, désactivez les cases à cocher **Principaux de sécurité intégrés**, **Groupes** et **Utilisateurs**. Activez la case à cocher **Ordinateurs**, puis cliquez sur **OK**. Dans le champ **Entrez les noms des objets à sélectionner**, tapez le nom du premier serveur de boîte aux lettres à ajouter au groupe de disponibilité de base de données, puis cliquez sur **OK**. Sélectionnez le premier compte d’ordinateur du nœud, puis dans le champ **Autorisations pour \<NodeName\>**, sélectionnez **Contrôle total** dans la colonne **Autoriser**. Cliquez sur **OK** pour enregistrer les paramètres d’autorisation.

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez bien configuré l’objet réseau de cluster, procédez comme suit :

1.  Ouvrez Utilisateurs et ordinateurs Active Directory.

2.  Développez le nœud de la forêt.

3.  Ouvrez l’unité d’organisation dans laquelle vous avez créé le compte, puis vérifiez que le compte est référencé.

