﻿---
title: "Le compte actif n'est pas connecté à un domaine Active Directory: Exchange 2013 Help"
TOCTitle: Le compte actif n'est pas connecté à un domaine Active Directory
ms:assetid: 0e229d10-605a-420f-bf8b-58a7fcb5b259
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/ms.exch.setupreadiness.loggedontodomain(v=EXCHG.150)
ms:contentKeyID: 50477502
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Le compte actif n'est pas connecté à un domaine Active Directory

 

_**Sapplique à :**Exchange Server_

_**Dernière rubrique modifiée :**2014-12-02_

La configuration de Microsoft Exchange Server 2013 ne peut pas continuer, car le compte actuel n’est pas connecté à un domaine Active Directory. Vous devez vous connecter à l'aide d'un compte Active Directory ayant les autorisations requises pour installer Exchange Server 2013.

Le programme d’installation requiert que l’utilisateur connecté lors de l’installation d’Exchange 2013 ait l’autorisation de créer et modifier des objets dans Active Directory. Si vous exécutez le programme d’installation d’Exchange 2013 dans votre organisation pour la première fois, le compte que vous utilisez doit être membre des groupes Administrateurs du schéma et Administrateurs de l’entreprise. Ces autorisations sont requises car Active Directory est préparé pour Exchange 2013 lors de la première exécution du programme d’installation. Une fois Active Directory préparé, le compte que vous utilisez pour installer des serveurs Exchange 2013 supplémentaires doit être membre du groupe de rôle de gestion Gestion de l’organisation.

Pour résoudre ce problème, accordez à l’utilisateur connecté des autorisations appropriées ou ouvrez une session à l’aide d’un compte possédant ces autorisations, puis exécutez de nouveau le programme d’installation d’Exchange 2013.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159813.important(EXCHG.150).gif" title="Important" alt="Important" />Important :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>L’installation inter-forêts d’Exchange 2013 n’est pas prise en charge. Utilisez un compte membre de la forêt Active Directory dans laquelle vous installez Exchange 2013.</td>
</tr>
</tbody>
</table>


Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), et [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

Avez-vous trouvé ce que vous cherchez ? Veuillez prendre une minute pour [nous envoyer votre avis à l'adresse](mailto:exsetuphelpfeedback@microsoft.com?subject=exchange%202013%20setup%20help%20feedback) au sujet des informations que vous souhaitiez y trouver.

