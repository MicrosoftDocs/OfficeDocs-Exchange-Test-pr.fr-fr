---
title: 'Placer une boîte aux lettres en blocage de rétention: Exchange 2013 Help'
TOCTitle: Placer une boîte aux lettres en blocage de rétention
ms:assetid: 2baac4a7-3402-4142-bfb3-1649a950e677
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dd335168(v=EXCHG.150)
ms:contentKeyID: 50477724
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Placer une boîte aux lettres en blocage de rétention

 

_**Sapplique à :** Exchange Online, Exchange Server 2013_

_**Dernière rubrique modifiée :** 2012-10-14_

L’activation du blocage de rétention pour une boîte de lettres suspend le traitement de la stratégie de rétention ou de la stratégie de boîte aux lettres de dossier géré sur cette boîte aux lettres. Le blocage de rétention est conçu pour les situations impliquant un utilisateur en vacances ou momentanément absent.

Lorsque le blocage de rétention est activé, les utilisateurs peuvent se connecter à leur boîte aux lettres et modifier ou supprimer des éléments. Lors d’une recherche de boîte aux lettres, les éléments supprimés, qui ont dépassé la durée de la période de rétention des éléments supprimés, ne seront pas contenus dans les résultats de la recherche. Pour vous assurer que les éléments modifiés ou supprimés par les utilisateurs sont conservés dans des scénarios de conservation légale, vous devez activer la conservation légale d’une boîte aux lettres. Pour plus d’informations, voir [Créer ou supprimer une conservation inaltérable](create-or-remove-an-in-place-hold-exchange-2013-help.md).

Vous pouvez également inclure des commentaires de rétention pour les boîtes aux lettres pour lesquelles le blocage de rétention a été activé. Les commentaires sont affichés dans les versions prises en charge de Microsoft Outlook.

Pour les autres tâches de gestion relatives à la gestion des enregistrements de messagerie (MRM), voir [Procédures de gestion des enregistrements de messagerie](messaging-records-management-procedures-exchange-2013-help.md).

## Ce qu’il faut savoir avant de commencer ?

  - Durée d'exécution estimée : 1 minute.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l'entrée « Gestion des enregistrements de messagerie » à la rubrique [Stratégie de messagerie et autorisations de conformité](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

  - Vous ne pouvez pas utiliser le Centre d’administration Exchange (CAE) pour activer le blocage de rétention d’une boîte aux lettres. Vous devez utiliser l'environnement de ligne de commande Exchange Management Shell.

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.


## Que souhaitez-vous faire ?

## Utilisation de l’environnement de ligne de commande Exchange Management Shell pour activer le blocage de rétention d’une boîte aux lettres

Cet exemple montre comment activer le blocage de rétention de la boîte aux lettres de Jean-Charles Colon.

    Set-Mailbox "Michael Allen" -RetentionHoldEnabled $true

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Set-Mailbox](https://technet.microsoft.com/fr-fr/library/bb123981\(v=exchg.150\)).

## Utilisation de l’environnement de ligne de commande Exchange Management Shell pour supprimer le blocage de rétention d’une boîte aux lettres

Cet exemple supprime le blocage de rétention de boîte aux lettres de Jean-Charles Colon.

    Set-Mailbox "Michael Allen" -RetentionHoldEnabled $false

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Set-Mailbox](https://technet.microsoft.com/fr-fr/library/bb123981\(v=exchg.150\)).

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez correctement activé le blocage de rétention d’une boîte aux lettres, utilisez la cmdlet [Get-Mailbox](https://technet.microsoft.com/fr-fr/library/bb123685\(v=exchg.150\)) pour récupérer la propriété *RetentionHoldEnabled* de la boîte aux lettres.

Cette commande récupère la propriété *RetentionHoldEnabled* de la boîte aux lettres de Michael Allen.

    Get-Mailbox "Michael Allen" | Select RetentionHoldEnabled

Cette commande récupère toutes les boîtes aux lettres dans l’organisation Exchange, filtre les boîtes aux lettres dont le blocage de rétention a été activé et en dresse la liste avec la stratégie de rétention appliquée à chacune.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159813.important(EXCHG.150).gif" title="Important" alt="Important" />Important :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Étant donné que <em>RetentionHoldEnabled</em> n’est pas une propriété filtrable dans Exchange 2013, vous ne pouvez pas utiliser le paramètre <em>Filter</em> avec la cmdlet <strong>Get-Mailbox</strong> pour filtrer les boîtes aux lettres dont le blocage de rétention a été activé côté serveur. Cette commande récupère une liste de toutes les boîtes aux lettres et tous les filtres sur le client exécutant la session de l’environnement de ligne de commande Exchange Management Shell. Dans de grands environnements comportant des milliers de boîtes aux lettres, cette commande peut prendre un certain temps à s’exécuter.</td>
</tr>
</tbody>
</table>


    Get-Mailbox -ResultSize unlimited | Where-Object {$_.RetentionHoldEnabled -eq $true} | Format-Table Name,RetentionPolicy,RetentionHoldEnabled -Auto

