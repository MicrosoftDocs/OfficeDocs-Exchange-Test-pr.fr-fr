---
title: 'Supprimer un dossier public: Exchange 2013 Help'
TOCTitle: Supprimer un dossier public
ms:assetid: 334b831d-e372-4d85-a407-5c8a5d0e78de
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Aa997202(v=EXCHG.150)
ms:contentKeyID: 50477866
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Supprimer un dossier public

 

_**Sapplique à :** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2016-11-16_

Vous devrez peut-être supprimer des dossiers publics qui ne sont plus utilisés dans votre organisation. Pour vous aider à choisir les dossiers publics à supprimer, consultez la rubrique [Affichage des statistiques des dossiers publics et des éléments des dossiers publics](view-statistics-for-public-folders-and-public-folder-items-exchange-2013-help.md).

Pour d'autres tâches de gestion relatives à la gestion des dossiers publics, consultez la rubrique [Procédures relatives aux dossiers publics](public-folder-procedures-exchange-2013-help.md).

Pour découvrir d'autres tâches de gestion associées aux dossiers publics, consultez la rubrique [Procédures de dossiers publics dans Office 365 et Exchange Online](https://technet.microsoft.com/fr-fr/library/jj966272\(v=exchg.150\)).

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : 5 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l'entrée « Dossiers publics » dans la rubrique [Autorisations de partage et de collaboration](sharing-and-collaboration-permissions-exchange-2013-help.md).

  - Vous ne pouvez pas supprimer un dossier public à extension messagerie. Vous devez d'abord désactiver la messagerie pour le dossier public avant de pouvoir le supprimer. Pour plus d'informations, consultez la rubrique [Activation ou désactivation de la messagerie pour un dossier public](mail-enable-or-mail-disable-a-public-folder-exchange-2013-help.md).

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


## Que souhaitez-vous faire ?

## Utiliser le Centre d'administration Exchange (CAE) pour supprimer un dossier public

1.  Accédez à **Dossiers publics** \> **Dossiers publics**.

2.  Dans l'affichage Liste, sélectionnez le dossier public à supprimer. Le fait de cliquer sur le nom du dossier permet d’afficher les sous-dossiers contenus dans ce dernier, le cas échéant. À ce stade, vous pouvez cliquer pour sélectionner un sous-dossier spécifique à supprimer.
    
    Pour supprimer un dossier ou un sous-dossier, cliquez n’importe où sur la ligne du dossier, sauf sur son nom souligné, puis cliquez sur **Supprimer**![Icône Supprimer](images/Dd979797.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "Icône Supprimer"). Si vous cliquez sur le nom souligné du dossier, l’option **Supprimer** ne sera pas disponible pour la sélection.
    
    ![Sélection d’un dossier public à supprimer](images/Aa997202.8666290d-3f19-4c70-afe3-45569762718b(EXCHG.150).png "Sélection d’un dossier public à supprimer")  

3.  Un message d'avertissement vous demande de confirmer la suppression du dossier public. Cliquez sur **Oui** pour continuer.

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour créer un dossier public

Cet exemple supprime le dossier public Help Desk\\Resolved. Cette commande suppose que le dossier public Resolved ne comporte pas de sous-dossiers.

    Remove-PublicFolder -Identity "\Help Desk\Resolved"

Cet exemple teste la commande précédente sans apporter de modifications.

    Remove-PublicFolder -Identity "\HelpDesk\Resolved" -WhatIf

Cet exemple supprime le dossier public Marketing et tous ses sous-dossiers, car la commande s'exécute de manière récurrente.

    Remove-PublicFolder -Identity "\Marketing" -Recurse:$True

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, consultez les rubriques [Remove-PublicFolder](https://technet.microsoft.com/fr-fr/library/bb124894\(v=exchg.150\)).

