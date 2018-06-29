---
title: 'Mettre à jour un carnet d’adresses en mode hors connexion: Exchange 2013 Help'
TOCTitle: Mettre à jour un carnet d’adresses en mode hors connexion
ms:assetid: 448a207e-41b4-4cef-9fe9-a68b81e2ec4e
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Aa997684(v=EXCHG.150)
ms:contentKeyID: 50478043
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Mettre à jour un carnet d’adresses en mode hors connexion

 

_**Sapplique à :**Exchange Server 2013_

_**Dernière rubrique modifiée :**2013-11-15_

Après la création d’un carnet d’adresses en mode hors connexion ou la modification de ses paramètres, les modifications ne sont accessibles aux utilisateurs qu’une fois le processus de génération de carnet d’adresses en mode hors connexion (OABGen) terminé.

Pour les autres tâches de gestion relatives aux carnets d’adresses en mode hors connexion, voir [Procédures des carnets d’adresses en mode hors connexion](offline-address-book-procedures-exchange-2013-help.md).

## Ce qu’il faut savoir avant de commencer ?

  - Durée d’exécution estimée de chaque procédure : 5 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Carnets d’adresses en mode hors connexion » dans la rubrique [Autorisations pour configurer les adresses de messagerie et les carnets d’adresses](email-address-and-address-book-permissions-exchange-2013-help.md).

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


## Utiliser l’environnement de ligne de commande Exchange Management Shell pour mettre à jour le carnet d’adresses en mode hors connexion

Cet exemple montre comment mettre à jour le carnet d’adresses en mode hors connexion appelé Mon carnet d’adresses en mode hors connexion.

    Update-OfflineAddressBook -Identity "My OAB"

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Update-OfflineAddressBook](https://technet.microsoft.com/fr-fr/library/aa995979\(v=exchg.150\)).

