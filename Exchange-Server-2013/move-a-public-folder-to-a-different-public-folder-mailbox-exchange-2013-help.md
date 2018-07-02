---
title: "Déplacement d'un dossier public vers une autre boîte aux lettres de dossiers publics: Exchange 2013 Help"
TOCTitle: Déplacement d'un dossier public vers une autre boîte aux lettres de dossiers publics
ms:assetid: b8744934-a3cb-443e-acce-a9a6ca5d88f6
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ906435(v=EXCHG.150)
ms:contentKeyID: 51407225
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Déplacement d'un dossier public vers une autre boîte aux lettres de dossiers publics

 

_**Sapplique à :**Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :**2016-11-16_

Si le contenu d'une boîte aux lettres de dossiers publics commence à dépasser vos quotas de boîte aux lettres, vous devrez peut-être déplacer des dossiers publics vers une autre boîte aux lettres de dossiers publics. Vous pouvez faire cela de deux manières. Pour déplacer un ou plusieurs dossiers publics qui ne contiennent pas de sous-dossiers, vous pouvez utiliser les cmdlets **PublicFolderMoveRequest**. Si vous devez déplacer une branche entière de dossier public (qui comprend le dossier public parent et tous les sous-dossiers), vous pouvez utiliser le script `Move-PublicFolderBranch.ps1` disponible lors de l'installation d'Exchange 2013.

Pour découvrir d'autres tâches de gestion associées aux dossiers publics, consultez la rubrique [Procédures relatives aux dossiers publics](public-folder-procedures-exchange-2013-help.md).

## Ce qu'il faut savoir avant de commencer

  - La durée d'exécution estimée de cette tâche dépend de la taille du dossier public.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l'entrée « Dossiers publics » dans la rubrique [Autorisations de partage et de collaboration](sharing-and-collaboration-permissions-exchange-2013-help.md).

  - Vous ne pouvez pas utiliser le Centre d'administration Exchange (CAE) pour effectuer ces procédures. Vous devez utiliser l'environnement de ligne de commande Exchange Management Shell.

  - Si le dossier à déplacer contient des sous-dossiers, ils ne seront pas déplacés par défaut. Si vous voulez déplacer un dossier public et ses sous-dossiers, utilisez le script **Move-PublicFolderBranch.ps1**.

  - Le déplacement de dossiers publics ne déplace que le contenu physique du dossier public. La hiérarchie logique reste inchangée.

  - En fonction de la taille du dossier public et de la quantité de contenu, le déplacement peut prendre plusieurs heures. Pendant ce temps, les utilisateurs pourront accéder aux dossiers publics. Ils ne pourront toutefois pas accéder aux dossiers publics publics pendant un court moment tant que le dossier se trouve dans l'état « Fin en cours ».

  - Vous ne pouvez effectuer qu'un déplacement de dossier public à la fois. Vous devez utiliser la cmdlet **Remove-PublicFolderMoveRequest** pour supprimer la demande une fois terminée.

  - Pour vérifier l'état d'une demande de déplacement de dossier public en cours, exécutez la cmdlet [Get-PublicFolderMoveRequest](https://technet.microsoft.com/fr-fr/library/jj878076\(v=exchg.150\)).

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

## Déplacer un seul dossier public

Cet exemple lance la demande de déplacement pour le dossier public \\CustomerEnagagements à partir de la boîte aux lettres de dossiers publics DeveloperReports to DeveloperReports01

    New-PublicFolderMoveRequest -Folders \DeveloperReports\CustomerEngagements -TargetMailbox DeveloperReports01

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>La boîte aux lettres de dossiers publics cible est verrouillée pendant que la demande de déplacement est active.</td>
</tr>
</tbody>
</table>


Pour obtenir des informations détaillées sur la syntaxe et les paramètres, consultez la rubrique [New-PublicFolderMoveRequest](https://technet.microsoft.com/fr-fr/library/jj878081\(v=exchg.150\)).

## Déplacer plusieurs dossiers publics

Cet exemple démarre la demande de déplacement des dossiers publics de la branche \\Dev vers la boîte aux lettres de dossiers publics cible DeveloperReports01. Cet exemple ne déplace pas le dossier public \\Dev.

    New-PublicFolderMoveRequest -Folders \Dev\CustomerEngagements,\Dev\RequestsforChange,\Dev\Usability -TargetMailbox DeveloperReports01

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>La boîte aux lettres de dossiers publics cible est verrouillée pendant que la demande de déplacement est active.</td>
</tr>
</tbody>
</table>


Pour obtenir des informations détaillées sur la syntaxe et les paramètres, consultez la rubrique [New-PublicFolderMoveRequest](https://technet.microsoft.com/fr-fr/library/jj878081\(v=exchg.150\)).

## Déplacer une branche de dossiers publics

Cet exemple utilise le script `Move-PublicFolderBranch.ps1` pour déplacer une branche de dossiers public. Cela lance la demande de déplacement du dossier public \\Dev et de tous ses sous-dossiers vers la boîte aux lettres de dossiers publics DeveloperReports01. Le script est situé dans le dossier des scripts et doit être exécuté à partir de cet emplacement.

    CD $env:ExchangeInstallPath\scripts
    
    .\Move-PublicFolderBranch.ps1 -FolderRoot \Dev -TargetPublicFolderMailbox DeveloperReports01

## Comment savoir si cela a fonctionné ?

Pour vérifier que la demande de déplacement de dossier public a bien été effectuée, exécutez la commande suivante :

    Get-PublicFolderMoveRequest | Format-List Status

L'état `Completed` indique que la demande de déplacement a réussi.

Si la demande de déplacement échoue, vous devrez peut-être restaurer le dossier public ou son contenu. Pour plus d'informations, consultez la rubrique [Restauration de dossiers publics et de boîtes aux lettres de dossiers publics à partir de déplacements ayant échoué](restore-public-folders-and-public-folder-mailboxes-from-failed-moves-exchange-2013-help.md).

