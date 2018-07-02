---
title: 'Attribution d’autorisations eDiscovery dans Exchange: Exchange 2013 Help'
TOCTitle: Attribution d’autorisations eDiscovery dans Exchange
ms:assetid: 729e09d8-614b-431f-ae04-ae41fb4c628e
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dd298059(v=EXCHG.150)
ms:contentKeyID: 50478443
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Attribution d’autorisations eDiscovery dans Exchange

 

_**Sapplique à :** Exchange Online, Exchange Server 2013_

_**Dernière rubrique modifiée :** 2014-10-02_

Si vous souhaitez que les utilisateurs puissent utiliser la découverte électronique sur place (In-Place eDiscovery) Microsoft Exchange Server 2013, vous devez d’abord les autoriser en les ajoutant au groupe de rôles Gestion de la découverte. Les membres du groupe de rôles Gestion de la découverte ont les autorisations de boîtes aux lettres Accès total pour la boîte aux lettres de découverte qui est créée par le programme d’installation Exchange.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ673034.Caution(EXCHG.150).gif" title="Attention" alt="Attention" />Attention :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Les membres du groupe de rôles Gestion de la découverte peuvent accéder au contenu des messages sensibles. Plus précisément, ces membres peuvent utiliser <a href="in-place-ediscovery-exchange-2013-help.md">Découverte électronique locale</a> pour effectuer des recherches dans toutes les boîtes aux lettres de votre organisation Exchange, prévisualiser les messages (et autres éléments de boîte aux lettre), les copier vers une boîte aux lettres de découverte et exporter les messages copiés vers un fichier .pst. Dans la plupart des organisations, cette autorisation est accordée au personnel des ressources humaines ou du service juridique et de mise en conformité.<br />
</td>
</tr>
</tbody>
</table>


Pour en savoir plus sur le groupe de rôles Gestion de la découverte, voir [Gestion de la détection](discovery-management-exchange-2013-help.md). Pour en savoir plus sur le contrôle d’accès basé sur les rôles (RBAC), voir [Présentation du contrôle d'accès basé sur un rôle](understanding-role-based-access-control-exchange-2013-help.md).

Intéressé par des scénarios où cette procédure est utilisée ? Consultez les rubriques suivantes :

  - [Créer une recherche de découverte électronique inaltérable](create-an-in-place-ediscovery-search-exchange-2013-help.md)

  - [Créer ou supprimer une conservation inaltérable](create-or-remove-an-in-place-hold-exchange-2013-help.md)

## Ce qu’il faut savoir avant de commencer ?

  - Durée d’exécution estimée : 1 minute.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Groupes de rôles » dans la rubrique [Autorisations pour la gestion des rôles](role-management-permissions-exchange-2013-help.md).

  - Par défaut, le groupe de rôles Gestion de la découverte ne contient aucun membre. Les administrateurs ayant le rôle Gestion de l’organisation ne peuvent également pas créer ni gérer les recherches de découverte s’ils ne sont pas ajoutés au groupe de rôles Gestion de la découverte.

  - Dans Exchange 2013, les membres du groupe de rôles Gestion de l’organisation peuvent créer un [Conservation inaltérable et conservation pour litige](in-place-hold-and-litigation-hold-exchange-2013-help.md) afin de bloquer tout le contenu des boîtes aux lettres. Cependant, pour créer un blocage sur place basé sur une requête, l’utilisateur doit être membre du groupe de rôles Gestion de la découverte ou se voir attribuer le rôle Recherche de boîte aux lettres.

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

## Utiliser le Centre d’administration Exchange (EAC) pour ajouter un utilisateur au groupe de rôles Gestion de la découverte

1.  Accédez à **Autorisations** \> **Rôles d’administrateur**.

2.  Dans la liste, sélectionnez **Gestion de la découverte**, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier")

3.  Dans **Groupe de rôles**, sous **Membres**, cliquez sur **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter").

4.  Dans **Sélectionner les membres**, sélectionnez un ou plusieurs utilisateurs, cliquez sur **Ajouter**, puis cliquez sur **OK**.

5.  Dans **Groupe de rôles**, cliquez sur **Enregistrer**.

## Utilisation de l’environnement de ligne de commande Exchange Management Shell pour ajouter un utilisateur au groupe de rôles Gestion de la découverte

Cet exemple ajoute l’utilisateur Bsuneja au groupe de rôles Gestion de la découverte.

    Add-RoleGroupMember -Identity "Discovery Management" -Member Bsuneja

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Add-RoleGroupMember](https://technet.microsoft.com/fr-fr/library/dd638207\(v=exchg.150\)).

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez ajouté l’utilisateur au groupe de rôles Gestion de la découverte, procédez comme suit :

1.  Dans le Centre d’administration Exchange, accédez à **Autorisations** \> **Rôles d’administrateur**.

2.  Dans la liste, sélectionnez **Gestion de la découverte**.

3.  Dans le volet d’informations, vérifiez que l’utilisateur est répertorié sous **Membres**.

Vous pouvez également exécuter cette commande pour répertorier les membres du groupe de rôles Gestion de la découverte.

    Get-RoleGroupMember -Identity "Discovery Management"

<table>
<thead>
<tr class="header">
<th><img src="images/Bb125224.tip(EXCHG.150).gif" title="Conseil" alt="Conseil" />Conseil :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.</td>
</tr>
</tbody>
</table>

