---
title: 'Suppression et recréation de la boîte aux lettres de découverte par défaut dans Exchange: Exchange 2013 Help'
TOCTitle: Suppression et recréation de la boîte aux lettres de découverte par défaut dans Exchange
ms:assetid: 4bde0b00-bdf7-44b4-ba64-aa062bc10ca2
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dn750894(v=EXCHG.150)
ms:contentKeyID: 62371333
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Suppression et recréation de la boîte aux lettres de découverte par défaut dans Exchange

 

_**Sapplique à :** Exchange Online, Exchange Server 2013_

_**Dernière rubrique modifiée :** 2016-05-04_

Vous pouvez utiliser l’environnement de ligne de commande Exchange Management Shell pour supprimer la boîte aux lettres de découverte par défaut, la recréer, puis lui attribuer des autorisations.

## Pourquoi effectuer cette opération ?

Dans Exchange Server 2013 et Exchange Online, la taille maximale de la boîte aux lettres de découverte par défaut est de 50 Go. Elle permet de stocker les résultats de la recherche de découverte électronique locale. Avant la modification de la limite de taille, les organisations pouvaient augmenter le quota de stockage au-delà de 50 Go. Par conséquent, les boîtes aux lettres de découverte pouvaient s’accroître au-delà de 50 Go. Une boîte aux lettres de découverte par défaut dépassant 50 Go pose les trois problèmes suivants :

  - Elle n’est pas prise en charge.

  - Elle ne peut pas être migrée vers Office 365.

  - S’il s’agit de la boîte aux lettres de découverte par défaut dans Exchange Server 2010, elle ne peut pas être mise à niveau vers Exchange Server 2013.

La résolution du problème dépend de votre volonté d’enregistrer les résultats de la recherche à partir d’une boîte aux lettres de découverte par défaut qui dépasse 50 GB.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Voulez-vous enregistrer les résultats de le recherche ?</th>
<th>Procédez comme suit</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Non</p></td>
<td><p>Suivez les étapes de cette rubrique pour supprimer, puis recréer la boîte aux lettres de découverte par défaut.</p></td>
</tr>
<tr class="even">
<td><p>Oui</p></td>
<td><p>Consultez les étapes décrites dans la rubrique <a href="reduce-the-size-of-a-discovery-mailbox-in-exchange-exchange-2013-help.md">Réduction de la taille d’une boîte aux lettres de découverte dans Exchange</a>.</p></td>
</tr>
</tbody>
</table>


## Utiliser l’Environnement de ligne de commande Exchange Management Shell pour supprimer et recréer la boîte aux lettres de découverte par défaut

> [!NOTE]
> Vous ne pouvez pas utiliser le Centre d’administration Exchange (CAE), car les boîtes aux lettres de découverte n’y sont pas affichées.


1.  Exécutez la commande suivante pour supprimer la boîte aux lettres de découverte par défaut.
    
        Remove-Mailbox "DiscoverySearchMailbox{D919BA05-46A6-415f-80AD-7E09334BB852}"

2.  Dans le message de confirmation de suppression de la boîte aux lettres et de l’objet utilisateur Active Directory correspondant, saisissez **Y**, puis appuyez sur Entrée.
    
    Un objet utilisateur est créé dans Active Directory lorsque vous créez la boîte aux lettres de découverte à l’étape suivante.

3.  Exécutez la commande suivante pour recréer la boîte aux lettres de découverte par défaut.
    
        New-Mailbox -Name "DiscoverySearchMailbox{D919BA05-46A6-415f-80AD-7E09334BB852}" -Alias "DiscoverySearchMailbox{D919BA05-46A6-415f-80AD-7E09334BB852}" -DisplayName "Discovery Search Mailbox" -Discovery

4.  Exécutez la commande suivante pour attribuer des autorisations de groupe de rôles de gestion de la découverte afin d’ouvrir la boîte aux lettres de découverte par défaut et d’afficher les résultats de la recherche.
    
        Add-MailboxPermission "DiscoverySearchMailbox{D919BA05-46A6-415f-80AD-7E09334BB852}" -User "Discovery Management" -AccessRights FullAccess -InheritanceType all

