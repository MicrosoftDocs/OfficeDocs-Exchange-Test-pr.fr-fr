---
title: 'Gérer les membres de groupes de rôles: Exchange 2013 Help'
TOCTitle: Gérer les membres de groupes de rôles
ms:assetid: c064729d-7cda-47fc-b105-acf4b300d430
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ657492(v=EXCHG.150)
ms:contentKeyID: 50479073
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Gérer les membres de groupes de rôles

 

_**Sapplique à :** Exchange Online, Exchange Server 2013_

_**Dernière rubrique modifiée :** 2012-10-08_

Cette rubrique vous explique comment ajouter, supprimer et afficher les membres d’un groupe de rôles de gestion dans Microsoft Exchange Server 2013. Pour plus d’informations sur les groupes de rôles dans Exchange 2013, consultez la rubrique [Présentation des groupes de rôles de gestion](understanding-management-role-groups-exchange-2013-help.md).

Autres tâches de gestion relatives aux groupes de rôles, voir [Autorisations](permissions-exchange-2013-help.md).

## Ce qu’il faut savoir avant de commencer ?

  - Durée d’exécution estimée de chaque procédure : 5 minutes

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Groupes de rôles » dans la rubrique [Autorisations pour la gestion des rôles](role-management-permissions-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.


## Que souhaitez-vous faire ?

## Ajouter des membres à un groupe de rôles

Pour accorder à un utilisateur des autorisations octroyées par un groupe de rôles, vous devez ajouter cet utilisateur (ou un groupe de sécurité universel ou un autre groupe de rôles auquel appartient l’utilisateur) comme membre du groupe de rôles.

## Utiliser le CAE pour ajouter des membres à un groupe de rôles

1.  Dans le Centre d’administration Exchange (CAE), accédez à **Autorisations** \> **Rôles admin**.

2.  Sélectionnez le groupe de rôles auquel vous souhaitez ajouter des membres, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

3.  Dans la section **Membres**, cliquez sur **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter").

4.  Sélectionnez les utilisateurs, les groupes de sécurité universels ou d’autres groupes de rôles que vous souhaitez ajouter au groupe de rôles, puis cliquez sur **Ajouter**, puis sur **OK**.

5.  Cliquez sur **Enregistrer** pour enregistrer les modifications apportées au groupe de rôles.

## Utiliser l’environnement de ligne de commande Exchange Management Shell pour ajouter des membres à un groupe de rôles

Exemples

Exemples

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez bien ajouté un ou plusieurs membres à un groupe de rôles, procédez comme suit :

1.  Dans le CAE, accédez à **Autorisations** \> **Rôles admin**.

2.  Sélectionnez le groupe de rôles auquel vous avez ajouté des membres.

3.  Dans le volet des informations du groupe de rôles, vérifiez que les membres ajoutés sont répertoriés.

## Supprimer des membres d’un groupe de rôles

Pour supprimer les autorisations octroyées par un groupe de rôles d’un utilisateur, vous devez supprimer l’utilisateur, ou le groupe de sécurité universel dont l’utilisateur est membre, de l’appartenance au groupe de rôles.

## Utiliser le CAE pour supprimer des membres d’un groupe de rôles

1.  Dans le CAE, accédez à **Autorisations** \> **Rôles admin**.

2.  Sélectionnez le groupe de rôles duquel vous souhaitez supprimer les membres, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

3.  Dans la section **Membres**, sélectionnez les membres à supprimer, puis cliquez sur **Supprimer**![Icône Suppression](images/Dd362328.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "Icône Suppression"), puis sur **Enregistrer**.

## Utiliser l’environnement de ligne de commande Exchange Management Shell pour supprimer des membres d’un groupe de rôles

Exemples

Exemples

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez bien supprimé un ou plusieurs membres d’un groupe de rôles, procédez comme suit :

1.  Dans le CAE, accédez à **Autorisations** \> **Rôles admin**.

2.  Sélectionnez le groupe de rôles duquel vous avez supprimé des membres.

3.  Dans le volet des informations du groupe de rôles, vérifiez que les membres supprimés ne sont plus répertoriés.

## Afficher les membres d’un groupe de rôles

Les membres d’un groupe de rôles reçoivent les autorisations fournies par les rôles de gestion attribués au groupe de rôles. Vous pouvez afficher les membres d’un groupe de rôles pour savoir quels utilisateurs, groupes de sécurité universels et autres groupes de rôles reçoivent les autorisations fournies par le groupe de rôles que vous spécifiez.

## Utiliser le CAE pour afficher les membres d’un groupe de rôles

1.  Dans le CAE, accédez à **Autorisations** \> **Rôles admin**.

2.  Sélectionnez le groupe de rôles pour lequel vous souhaitez afficher les membres.

3.  Dans le volet des informations du groupe de rôles, affichez les membres dans le panneau d’informations du groupe de rôles.

## Utiliser l’environnement de ligne de commande Exchange Management Shell pour afficher les membres d’un groupe de rôles

Exemples

