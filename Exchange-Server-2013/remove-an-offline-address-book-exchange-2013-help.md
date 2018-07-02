---
title: "Suppression d'un carnet d'adresses en mode hors connexion: Exchange 2013 Help"
TOCTitle: Suppression d'un carnet d'adresses en mode hors connexion
ms:assetid: d69f1e8a-b3cb-4739-90cd-85ea450d06f3
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb124744(v=EXCHG.150)
ms:contentKeyID: 50479286
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Suppression d'un carnet d'adresses en mode hors connexion

 

_**Sapplique à :**Exchange Online, Exchange Server 2013_

_**Dernière rubrique modifiée :**2014-12-16_

Cette rubrique explique comment supprimer un carnet d'adresses en mode hors connexion (OAB).

Pour les autres tâches de gestion relatives aux carnets d'adresses en mode hors connexion, consultez la rubrique [Procédures des carnets d’adresses en mode hors connexion](offline-address-book-procedures-exchange-2013-help.md).

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée de chaque procédure : 5 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l'entrée « Carnets d'adresses en mode hors connexion » dans la rubrique [Autorisations pour configurer les adresses de messagerie et les carnets d’adresses](email-address-and-address-book-permissions-exchange-2013-help.md).

  - Par défaut dans Exchange Online, le rôle de liste d’adresses n’est affecté à aucun groupe de rôles. Pour utiliser les cmdlets nécessitant le rôle Liste d’adresses, vous devez ajouter ce dernier à un groupe de rôles. Pour plus d’informations, consultez la section « Ajouter un rôle à un groupe de rôles » de la rubrique [Gérer des groupes de rôles](manage-role-groups-exchange-2013-help.md).

  - Une fois que vous avez supprimé un carnet d'adresses en mode hors connexion associé à un utilisateur ou à une base de données de boîtes aux lettres, le destinataire devra télécharger le carnet d'adresses en mode hors connexion par défaut tant que vous n'aurez pas affecté un nouveau carnet d'adresses en mode hors connexion à cet utilisateur. Si vous supprimez le carnet d'adresses en mode hors connexion, vous devez affecter un autre carnet d'adresses en mode hors connexion par défaut. Pour obtenir des instructions sur la modification du carnet d'adresses en mode hors connexion par défaut, consultez la rubrique [Modifiication du carnet d'adresses en mode hors connexion par défaut](change-the-default-offline-address-book-exchange-2013-help.md).

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


## Utiliser l'environnement de ligne de commande Exchange Management Shell pour supprimer un carnet d'adresses en mode hors connexion

Cet exemple montre comment supprimer un carnet d'adresses en mode hors connexion nommé mon carnet d'adresses en mode hors connexion.

    Remove-OfflineAddressBook -Identity "My OAB"

Tapez **Y** pour confirmer la suppression du carnet d'adresses en mode hors connexion, puis appuyez sur ENTRÉE.

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, consultez la rubrique [Remove-OfflineAddressBook](https://technet.microsoft.com/fr-fr/library/bb123594\(v=exchg.150\)).

