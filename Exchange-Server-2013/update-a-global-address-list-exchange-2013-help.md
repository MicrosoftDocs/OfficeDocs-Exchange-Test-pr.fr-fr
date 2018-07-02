---
title: 'Mise à jour d’une liste d’adresses globale: Exchange 2013 Help'
TOCTitle: Mise à jour d’une liste d’adresses globale
ms:assetid: 236e8530-62dd-4c43-8a5d-8465623252e6
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb266966(v=EXCHG.150)
ms:contentKeyID: 50477760
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Mise à jour d’une liste d’adresses globale

 

_**Sapplique à :**Exchange Server 2013_

_**Dernière rubrique modifiée :**2014-12-16_

Vous pouvez utiliser l'environnement de ligne de commande Exchange Management Shell pour mettre à jour une liste d'adresses globale (LAG). Une liste d'adresses globale (LAG) est un répertoire qui contient les entrées de chaque groupe, utilisateur et contact dans la mise en œuvre de MicrosoftExchange d'une organisation.

Pour les autres tâches de gestion relatives aux listes d'adresses, consultez la rubrique [Procédures des listes d'adresses](address-list-procedures-exchange-2013-help.md).

## Ce qu’il faut savoir avant de commencer ?

  - Durée d'exécution estimée de chaque procédure : 5 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l'entrée « Listes d'adresses » dans la rubrique [Autorisations pour configurer les adresses de messagerie et les carnets d’adresses](email-address-and-address-book-permissions-exchange-2013-help.md).

  - Par défaut dans Exchange Online, le rôle de liste d’adresses n’est affecté à aucun groupe de rôles. Pour utiliser les cmdlets nécessitant le rôle Liste d’adresses, vous devez ajouter ce dernier à un groupe de rôles. Pour plus d’informations, consultez la section « Ajouter un rôle à un groupe de rôles » de la rubrique [Gérer des groupes de rôles](manage-role-groups-exchange-2013-help.md).

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


## Utilisation de l'environnement de ligne de commande Exchange Management Shell pour mettre à jour une liste d'adresses globale

Cet exemple montre comment mettre à jour une liste d'adresses globale pour l'entreprise Fourth Coffee.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>L'exécution de cette commande démarre uniquement le processus de mise à jour. La mise à jour de la LAG peut prendre plusieurs heures.</td>
</tr>
</tbody>
</table>


    Update-GlobalAddressList -Identity "Fourth Coffee"

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, consultez la rubrique [Update-GlobalAddressList](https://technet.microsoft.com/fr-fr/library/aa998806\(v=exchg.150\)).

