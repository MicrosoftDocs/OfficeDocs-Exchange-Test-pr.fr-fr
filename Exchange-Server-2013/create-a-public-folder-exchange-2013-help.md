---
title: 'Créer un dossier public: Exchange 2013 Help'
TOCTitle: Créer un dossier public
ms:assetid: 6d252e60-c8d0-4efd-b9d7-ba5284a6f8ab
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb691104(v=EXCHG.150)
ms:contentKeyID: 50478392
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.PublicFolders.NewPublicFolderWizardForm.NewPublicFolderWizardPage
ms.translationtype: HT
---

# Créer un dossier public

 

_**Sapplique à :** Exchange Online, Exchange Server 2013_

_**Dernière rubrique modifiée :** 2014-02-24_

Les dossiers publics sont conçus pour assurer un accès partagé et offrir une manière simple et efficace de collecter, d'organiser et de partager des informations avec d'autres personnes dans votre groupe de travail ou votre organisation.

Par défaut, un dossier public hérite des paramètres de son dossier parent, y compris les paramètres d'autorisations.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Pour plus d’informations sur les limites et les quotas de stockage pour les dossiers publics, consultez les rubriques suivantes :
<ul>
<li><p>Pour les dossiers publics dans Office 365, voir <a href="https://go.microsoft.com/fwlink/?linkid=391188">Limites d’Exchange Online</a>.</p></li>
<li><p>Pour les dossiers publics dans Exchange Server 2013 sur site, voir <a href="limits-for-public-folders-exchange-2013-help.md">Limites pour les dossiers publics</a>.</p></li>
</ul></td>
</tr>
</tbody>
</table>


Pour d'autres tâches de gestion relatives à la gestion des dossiers publics, consultez la rubrique [Procédures relatives aux dossiers publics](public-folder-procedures-exchange-2013-help.md).

Pour découvrir d'autres tâches de gestion associées aux dossiers publics, consultez la rubrique [Procédures de dossiers publics dans Office 365 et Exchange Online](https://technet.microsoft.com/fr-fr/library/jj966272\(v=exchg.150\)).

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : 5 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Dossiers publics » dans la rubrique [Autorisations de partage et de collaboration](sharing-and-collaboration-permissions-exchange-2013-help.md).

  - Vous ne pouvez créer de dossier public que si vous avez d’abord créé une boîte aux lettres de dossiers publics. Pour plus d'informations sur la création d'une boîte aux lettres de dossiers publics, consultez la rubrique [Création d’une boîte aux lettres de dossiers publics](create-a-public-folder-mailbox-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

## Que souhaitez-vous faire ?

## Utiliser le Centre d'administration Exchange (CAE) pour créer un dossier public

Lorsque vous utilisez le Centre d’administration Exchange (CAE) pour créer un dossier public, vous pouvez seulement définir le nom et le chemin d’accès de ce dossier public. Pour configurer des paramètres supplémentaires, vous devrez modifier le dossier public après sa création.

1.  Accédez à **Dossiers publics**\>**Dossiers publics**.

2.  Si vous souhaitez créer ce dossier public en tant qu'enfant d'un dossier public existant, cliquez sur le dossier public existant dans l'affichage Liste. Si vous souhaitez créer un dossier public de niveau supérieur, ignorez cette étape.

3.  Cliquez sur **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter").

4.  Dans **Dossier public**, entrez le nom du dossier public.
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ159813.important(EXCHG.150).gif" title="Important" alt="Important" />Important :</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>N'utilisez pas de barre oblique inverse (\) dans le nom du dossier public créé.</td>
    </tr>
    </tbody>
    </table>


5.  Dans le champ **Chemin d'accès**, vérifiez le chemin d'accès au dossier public. S’il ne s’agit pas du chemin d’accès souhaité, cliquez sur **Annuler** et suivez l’étape 2 de cette procédure.

6.  Cliquez sur **Enregistrer**.

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour créer un dossier public

Cet exemple permet de créer un dossier public appelé Reports dans le chemin d'accès Marketing\\2013.

    New-PublicFolder -Name Reports -Path \Marketing\2013

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159813.important(EXCHG.150).gif" title="Important" alt="Important" />Important :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>N'utilisez pas de barre oblique inverse (\) dans le nom du dossier public créé.</td>
</tr>
</tbody>
</table>


Pour obtenir des informations détaillées sur la syntaxe et les paramètres, consultez la rubrique [New-PublicFolder](https://technet.microsoft.com/fr-fr/library/aa996405\(v=exchg.150\)).

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez correctement créé un dossier public, procédez comme suit :

  - Dans le Centre d'administration Exchange (CAE), cliquez sur **Actualiser** pour actualiser la liste des dossiers publics. Le nouveau dossier public doit apparaître dans la liste.

  - Dans l'environnement de ligne de commande Exchange Management Shell, exécutez l'une des commandes suivantes :
    
        Get-PublicFolder -Identity \Marketing\2013\Reports | Format-List
    
        Get-PublicFolder -Identity \Marketing\2013 -GetChildren
    
        Get-PublicFolder -Recurse

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

