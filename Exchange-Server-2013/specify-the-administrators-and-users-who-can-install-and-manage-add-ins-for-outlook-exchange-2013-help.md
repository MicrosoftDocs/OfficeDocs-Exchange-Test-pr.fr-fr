---
title: 'Désigner les administrateurs et utilisateurs qui peuvent installer et gérer des compléments pour Outlook: Exchange 2013 Help'
TOCTitle: Désigner les administrateurs et utilisateurs qui peuvent installer et gérer des compléments pour Outlook
ms:assetid: 7ee4302d-b8bb-40a0-9810-10d3a0271bcb
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ943754(v=EXCHG.150)
ms:contentKeyID: 52062971
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Désigner les administrateurs et utilisateurs qui peuvent installer et gérer des compléments pour Outlook

 

_**Sapplique à :**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :**2017-02-08_

Vous pouvez spécifier les administrateurs de votre organisation qui disposent des autorisations pour installer et gérer les compléments Outlook. Vous pouvez également indiquer les utilisateurs au sein de votre organisation qui disposent des autorisations pour installer et gérer des compléments pour leur propre utilisation.

Pour cela, vous devez attribuer ou supprimer des rôles de gestion propres aux compléments. Il existe cinq rôles intégrés.

Rôles administratifs

  - **Org Marketplace Apps**   Autorise un administrateur à installer et à gérer les compléments disponibles dans l’Office Store pour son organisation.

  - **Org Custom Apps**   Autorise un administrateur à installer et à gérer des compléments personnalisés pour son organisation.

Rôles d'utilisateur

  - **My Marketplace Apps**   Autorise un utilisateur à installer et à gérer des compléments de l’Office Store pour son utilisation personnelle.

  - **My Custom Apps**   Autorise un utilisateur à installer et à gérer des compléments personnalisés pour sa propre utilisation.

  - **My ReadWriteMailbox Apps**   Autorise un utilisateur à installer et à gérer des compléments qui exigent le niveau d’autorisation ReadWriteMailbox dans leur manifeste.

Les rôles administratifs mentionnés ci-dessus sont activés par défaut pour tous les administrateurs ayant le groupe de rôles **Gestion de l’organisation**. Par ailleurs, les rôles d’utilisateur ci-dessus sont également activés par défaut pour les utilisateurs finaux.

Pour plus d’informations sur ces rôles, consultez les rubriques [Rôle Org Marketplace Apps](org-marketplace-apps-role-exchange-2013-help.md), [Rôle Org Custom Apps](org-custom-apps-role-exchange-2013-help.md), [Rôle My Marketplace Apps](my-marketplace-apps-role-exchange-2013-help.md), [Rôle My Custom Apps](my-custom-apps-role-exchange-2013-help.md) et [Rôle Mes applications ReadWriteMailbox](my-readwritemailbox-apps-role-exchange-2013-help.md).

Pour plus d’informations sur les compléments, consultez la rubrique [Applications pour Outlook](add-ins-for-outlook-exchange-2013-help.md).

## Ce qu’il faut savoir avant de commencer

  - Durée d'exécution estimée : 5 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette cmdlet. Bien que tous les paramètres de cette cmdlet soient répertoriés dans cette rubrique, il est possible que vous n’ayez pas accès à certains paramètres s’ils ne sont pas inclus dans les autorisations qui vous ont été attribuées. Pour voir les autorisations qui vous sont nécessaires, voir l’entrée « Attribution des rôles » dans la rubrique [Autorisations pour la gestion des rôles](role-management-permissions-exchange-2013-help.md).

  - L’accès à Office Store n’est pas pris en charge pour les boîtes aux lettres ou les organisations de certains pays. Si l’option **Ajouter à partir d’Office Store** n’apparaît pas dans le **Centre d’administration Exchange** sous **Organisation** \> **Compléments** \> ![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter"), vous pourrez peut-être installer un complément pour Outlook depuis un emplacement de fichier ou une URL. Pour plus d’informations, contactez votre fournisseur de services.

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

<table>
<thead>
<tr class="header">
<th><img src="images/Bb125224.tip(EXCHG.150).gif" title="Conseil" alt="Conseil" />Conseil :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..</td>
</tr>
</tbody>
</table>


## Que souhaitez-vous faire ?

## Attribuer aux administrateurs les autorisations requises pour installer et gérer des compléments pour votre organisation

## Utiliser le Centre d'administration Exchange (CAE) pour attribuer des autorisations aux administrateurs

À l’aide du Centre d’administration Exchange, vous pouvez attribuer aux administrateurs les autorisations requises pour installer et gérer des compléments disponibles dans l’Office Store pour votre organisation. Pour obtenir des informations détaillées sur la procédure à suivre, consultez la rubrique [Gérer des groupes de rôles](manage-role-groups-exchange-2013-help.md).

## Attribuer aux utilisateurs les autorisations requises pour installer et gérer des compléments pour leur utilisation personnelle

## Utiliser le Centre d'administration Exchange (CAE) pour attribuer des autorisations aux utilisateurs

À l’aide du Centre d’administration Exchange, vous pouvez attribuer aux utilisateurs les autorisations requises pour afficher et modifier des compléments personnalisés pour leur propre utilisation. Pour obtenir des informations détaillées sur la procédure à suivre, consultez la rubrique [Gérer des groupes de rôles](manage-role-groups-exchange-2013-help.md).

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez bien attribué des autorisations à un utilisateur, exécutez une commande de l’environnement de ligne de commande Exchange Management Shell en utilisant le format `Get-ManagementRoleAssignment -Role <Role Name> -GetEffectiveUsers`, où `Role Name` représente le rôle pour lequel vous voulez vérifier les autorisations attribuées.

Cet exemple vous montre comment vérifier à qui vous avez attribué des autorisations pour installer des compléments de l’Office Store pour l’organisation.

1.  Exécutez `Get-ManagementRoleAssignment -Role "Org Marketplace Apps" -GetEffectiveUsers`.

2.  Dans les résultats, consultez les entrées de la colonne **Utilisateurs effectifs**.

Pour plus d'informations sur la syntaxe et les paramètres, consultez la rubrique [Get-ManagementRoleAssignment](https://technet.microsoft.com/fr-fr/library/dd351024\(v=exchg.150\)).

