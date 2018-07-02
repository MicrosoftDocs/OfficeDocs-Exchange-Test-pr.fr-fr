---
title: 'Mise à jour de la hiérarchie de dossiers publics: Exchange 2013 Help'
TOCTitle: Mise à jour de la hiérarchie de dossiers publics
ms:assetid: a7b2fb51-0207-4d7d-938d-466ae110bb90
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ945055(v=EXCHG.150)
ms:contentKeyID: 52057150
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Mise à jour de la hiérarchie de dossiers publics

 

_**Sapplique à :** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2014-04-03_

Vous devez uniquement mettre à jour la hiérarchie de dossiers publics si vous souhaitez appeler manuellement le synchronisateur de hiérarchie et l’Assistant Boîte aux lettres. Ceux-ci doivent être appelés ensemble au moins une fois chaque 24 heures pour chaque boîte aux lettres de dossiers publics dans l'organisation. Le synchronisateur de hiérarchie est appelé toutes les 15 minutes dès qu'un utilisateur se connecte à une boîte aux lettres secondaire avec Microsoft Outlook ou un client des services web de Microsoft Exchange.

Pour découvrir d'autres tâches de gestion associées aux dossiers publics dans Exchange Online, consultez la rubrique [Procédures de dossiers publics dans Office 365 et Exchange Online](https://technet.microsoft.com/fr-fr/library/jj966272\(v=exchg.150\)).

Pour découvrir d'autres tâches de gestion associées aux dossiers publics dans Exchange Server 2013, consultez la rubrique [Procédures relatives aux dossiers publics](public-folder-procedures-exchange-2013-help.md).

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : 5 minutes

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l'entrée « Dossiers publics » dans la rubrique [Autorisations de partage et de collaboration](sharing-and-collaboration-permissions-exchange-2013-help.md).

  - Vous ne pouvez pas effectuer cette procédure dans le CAE. Vous devez utiliser l'environnement de ligne de commande Exchange Management Shell.

  - Nous vous recommandons d'utiliser le paramètre *SuppressStatus* lorsque vous exécutez cette commande avec paramètre *InvokeSynchronizer*. Si vous n'utilisez pas ce paramètre dans la commande, la sortie affiche des messages d'état toutes les 3 secondes à une minute. Tant que la minute n'est pas écoulée, vous ne pouvez pas utiliser cette instance de l'environnement de ligne de commande Exchange Management Shell.

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


## Mise à jour de la hiérarchie de dossiers publics

Cet exemple met à jour la hiérarchie de dossiers publics sur la boîte aux lettres des dossiers publics PF\_marketing et supprime la sortie de la commande.

    Update-PublicFolderMailbox -Identity PF_marketing -InvokeSynchronizer -SuppressStatus

Cet exemple met à jour toutes les boîtes aux lettres de dossiers publics et supprime la sortie de la commande.

    Get-Mailbox -PublicFolder | Update-PublicFolderMailbox InvokeSynchronizer -SuppressStatus

