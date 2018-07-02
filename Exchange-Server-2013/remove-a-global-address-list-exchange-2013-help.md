---
title: "Suppression d'une liste d'adresses globale: Exchange 2013 Help"
TOCTitle: Suppression d'une liste d'adresses globale
ms:assetid: 65d75b69-641b-4a37-a63c-47cf018f5f22
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb232077(v=EXCHG.150)
ms:contentKeyID: 50478310
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Suppression d'une liste d'adresses globale

 

_**Sapplique à :**Exchange Online, Exchange Server 2013_

_**Dernière rubrique modifiée :**2014-12-16_

La liste d'adresses globale (LAG) est un répertoire qui contient les entrées de chaque groupe, utilisateur et contact au sein d'une organisation Exchange.

Pour les autres tâches de gestion relatives aux listes d'adresses, consultez la rubrique [Procédures des listes d'adresses](address-list-procedures-exchange-2013-help.md).

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée de chaque procédure : 5 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l'entrée « Listes d'adresses » dans la rubrique [Autorisations pour configurer les adresses de messagerie et les carnets d’adresses](email-address-and-address-book-permissions-exchange-2013-help.md).

  - Par défaut dans Exchange Online, le rôle de liste d’adresses n’est affecté à aucun groupe de rôles. Pour utiliser les cmdlets nécessitant le rôle Liste d’adresses, vous devez ajouter ce dernier à un groupe de rôles. Pour plus d’informations, consultez la section « Ajouter un rôle à un groupe de rôles » de la rubrique [Gérer des groupes de rôles](manage-role-groups-exchange-2013-help.md).

  - Il est impossible de supprimer la liste d'adresses globale par défaut.

  - Vous ne pouvez pas utiliser le Centre d’administration Exchange (CAE) pour effectuer cette procédure. Vous devez utiliser l'environnement de ligne de commande Exchange Management Shell.

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

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


## Utilisation de l'environnement de ligne de commande Exchange Management Shell pour supprimer une liste d'adresses globale

Cet exemple montre comment supprimer le quatrième café de la liste d'adresses globale du contrôleur de domaine ad-server.fourthcoffee.com.

    Remove-GlobalAddressList -Identity "Fourth Coffee" -DomainController ad-server.fourthcoffee.com

Tapez **Y** pour confirmer la suppression de la LAG, puis appuyez sur ENTRÉE.

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, consultez la rubrique [Remove-GlobalAddressList](https://technet.microsoft.com/fr-fr/library/bb124368\(v=exchg.150\)).

