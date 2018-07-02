---
title: 'Afficher des membres d’un groupe de distribution dynamique: Exchange 2013 Help'
TOCTitle: Afficher des membres d’un groupe de distribution dynamique
ms:assetid: 40b100c6-864e-4c82-9f98-08dd5c83e378
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb232019(v=EXCHG.150)
ms:contentKeyID: 50477278
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Afficher des membres d’un groupe de distribution dynamique

 

_**Sapplique à :**Exchange Online, Exchange Server 2013_

_**Dernière rubrique modifiée :**2018-03-02_

Les groupes de distribution dynamique sont des groupes de distribution dont l’appartenance se base sur des filtres de destinataires spécifiques plutôt que sur un ensemble de destinataires défini. MicrosoftExchange intègre des filtres prédéfinis qui facilitent la création des filtres de destinataires pour les groupes de distribution dynamique. Un *filtre prédéfini* est un filtre couramment utilisé qui permet de répondre à de nombreux critères de filtrage des destinataires. Vous pouvez spécifier les types de destinataire que vous voulez inclure dans un groupe de distribution dynamique. En outre, vous pouvez également spécifier la liste des conditions que les destinataires doivent satisfaire. Vous pouvez utiliser l’environnement de ligne de commande Exchange Management Shell pour afficher la liste des destinataires d’un groupe de distribution dynamique qui utilise des filtres prédéfinis.

## Ce qu'il faut savoir avant de commencer ?

  - Durée d'exécution estimée : 2 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Groupes de distribution dynamique » dans la rubrique [Autorisations des destinataires](recipients-permissions-exchange-2013-help.md).

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

## Utilisation de l’environnement de ligne de commande Exchange Management Shell pour afficher la liste des membres d’un groupe de distribution dynamique

Cet exemple renvoie la liste des membres du groupe de distribution dynamique nommé employés à plein temps. La première commande enregistre l’objet de groupe de distribution dynamique dans la variable `$FTE`. La deuxième commande utilise l’applet de commande **Get-Recipient** pour répertorier les destinataires qui correspondent aux critères définis pour le groupe de distribution dynamique.

    $FTE = Get-DynamicDistributionGroup "Full Time Employees"

    Get-Recipient -RecipientPreviewFilter $FTE.RecipientFilter -OrganizationalUnit $FTE.RecipientContainer

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, consultez la rubrique [Get-DynamicDistributionGroup](https://technet.microsoft.com/fr-fr/library/bb124762\(v=exchg.150\)) et [Get-Recipient](https://technet.microsoft.com/fr-fr/library/aa996921\(v=exchg.150\)).

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Vous ne pouvez pas afficher les membres d’un groupe de distribution dynamique à l’aide de l’estimation à l’achèvement.</td>
</tr>
</tbody>
</table>


## Comment savoir si cela a fonctionné ?

Pour vérifier que vous l’avez vu avec succès les membres d’un groupe de distribution dynamique, effectuez le des opérations suivantes :

  - Dans l’environnement de ligne de commande Exchange Management Shell, une liste des membres est retournée suite à votre exécution de la commande précédente pour obtenir un aperçu de la liste des membres du groupe de distribution dynamique. Par exemple, si vous avez créé une boîte aux lettres de nouvel utilisateur avec des propriétés qui correspondent au filtre des destinataires pour le groupe de distribution dynamique, ce nouvel utilisateur devrait apparaître dans la liste des membres du groupe.

