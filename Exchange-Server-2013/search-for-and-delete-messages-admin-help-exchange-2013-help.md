---
title: 'Recherche et suppression de messages - Aide de l’administrateur: Exchange 2013 Help'
TOCTitle: Recherche et suppression de messages - Aide de l’administrateur
ms:assetid: 8c36bb03-e716-4fdd-9958-4aa7a2a1db42
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Ff459253(v=EXCHG.150)
ms:contentKeyID: 52057116
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Recherche et suppression de messages - Aide de l’administrateur

 

_**Sapplique à :**Exchange Online, Exchange Server 2013_

_**Dernière rubrique modifiée :**2017-12-20_

Les administrateurs peuvent utiliser la cmdlet **Search-Mailbox** pour faire une recherche dans des boîtes aux lettres utilisateur, puis supprimer des messages d’une boîte aux lettres.

Pour rechercher et supprimer des messages en une seule étape, exécutez la cmdlet **Search-Mailbox** avec le commutateur *DeleteContent*. Cependant, quand vous effectuez cette opération, vous ne pouvez ni afficher un aperçu des résultats ni générer un journal des messages qui seront renvoyés par la recherche, et vous pourriez supprimer des messages par inadvertance. Pour afficher un aperçu du journal des messages identifiés par la recherche avant qu'ils ne soient supprimés, exécutez la cmdlet **Search-Mailbox** avec le commutateur *LogOnly*.

Pour plus de sécurité, vous pouvez d'abord copier les messages vers une autre boîte aux lettres à l'aide des paramètres *TargetMailbox* et *TargetFolder*. De cette manière, vous êtes assuré de conserver une copie des messages supprimés pour pouvoir y accéder ultérieurement.

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : 10 minutes. La durée réelle dépend de la taille de la boîte aux lettres et de la requête de recherche.

  - Vous ne pouvez pas utiliser le Centre d’administration Exchange (CAE) pour effectuer ces procédures. Vous devez utiliser l’environnement de ligne de commande Exchange Management Shell.

  - Vous devez disposer des deux rôles de gestion suivants pour rechercher et supprimer des messages dans les boîtes aux lettres des utilisateurs :
    
      - **Recherche de boîte aux lettres**   Ce rôle vous permet de rechercher des messages dans plusieurs boîtes aux lettres dans votre organisation. Ce rôle n’est pas attribué par défaut aux administrateurs. Pour vous attribuer vous-même ce rôle afin de pouvoir rechercher les boîtes aux lettres, ajoutez-vous en tant que membre du groupe de rôles Gestion de la découverte. Consultez la rubrique [Attribution d’autorisations eDiscovery dans Exchange](assign-ediscovery-permissions-in-exchange-exchange-2013-help.md).
    
      - **Importation/Exportation de boîte aux lettres**   Ce rôle vous autorise à supprimer des messages de la boîte aux lettres d’un utilisateur. Par défaut, ce rôle n’est attribué à aucun groupe de rôles. Pour supprimer des messages des boîtes aux lettres des utilisateurs, vous pouvez ajouter le rôle Importation/Exportation de boîte aux lettres au groupe de rôles Gestion de l’organisation. Pour plus d’informations, consultez la section relative à l’ajout d’un rôle à un groupe de rôles dans [Gérer des groupes de rôles](manage-role-groups-exchange-2013-help.md).

  - Si la fonctionnalité de récupération d'élément unique est activée pour la boîte aux lettres dont vous souhaitez supprimer des messages, vous devez d'abord la désactiver. Pour plus d’informations, voir [Activation de la récupération d’élément unique pour une boîte aux lettres](enable-or-disable-single-item-recovery-for-a-mailbox-exchange-2013-help.md).

  - Si la boîte aux lettres dont vous souhaitez supprimer des messages est mise en conservation, nous vous recommandons de vous informer préalablement auprès du service de gestion des enregistrements ou juridique avant de désactiver la mise en attente et de supprimer le contenu de la boîte aux lettres. Une fois l’autorisation obtenue, suivez les étapes décrites dans la rubrique [Nettoyer le dossier Éléments récupérables](clean-up-the-recoverable-items-folder-exchange-2013-help.md).

  - Vous pouvez faire une recherche dans 10 000 boîtes aux lettres au maximum à l’aide de la cmdlet **Search-Mailbox**. Si vous êtes une organisation Exchange Online et que vous disposez de plus de 10 000 boîtes aux lettres, vous pouvez utiliser la fonctionnalité de recherche de conformité (ou la cmdlet **New-ComplianceSearch** correspondante) pour réaliser une recherche dans un nombre illimité de boîtes aux lettres. Vous pouvez ensuite utiliser la cmdlet **New-ComplianceSearchAction** pour supprimer les messages renvoyés par la recherche de conformité. Pour plus d’informations, reportez-vous à la rubrique [Recherche et suppression de messages électroniques dans votre organisation Office 365](https://go.microsoft.com/fwlink/p/?linkid=786856).

  - Si vous incluez une requête de recherche (à l’aide du paramètre *SearchQuery*), la cmdlet **Search-Mailbox** renverra au maximum 10 000 éléments dans les résultats de recherche. Ainsi, si vous incluez une requête de recherche, vous devrez peut-être exécuter la commande **Search-Mailbox** plusieurs fois pour supprimer plus de 10 000 éléments.

  - Pour rechercher des boîtes aux lettres de l’utilisateur archive également lorsque vous exécutez l’applet de commande **Search-Mailbox** . De même, les éléments dans la boîte aux lettres d’archive principale seront supprimés lorsque vous utilisez l’applet de commande **Search-Mailbox** avec le commutateur *DeleteContent* . Pour éviter cela, vous pouvez inclure le commutateur *DoNotIncludeArchive* . En outre, nous vous recommandons que vous n’utilisez pas le commutateur *DeleteContent* pour supprimer les messages dans les boîtes aux lettres de Exchange Online ayant une extension auto d’archivage activé car la perte de données inattendues peut-être se produire.

## Rechercher des messages et enregistrer les résultats de la recherche

Cet exemple permet d'effectuer une recherche dans la boîte aux lettres d'April Stewart au niveau des messages dont le champ Objet contient l'expression « Your bank statement » (Votre relevé de compte) et de consigner les résultats de la recherche dans le dossier SearchAndDeleteLog de la boîte aux lettres de l'administrateur. Les messages ne sont ni copiés ni supprimés de la boîte aux lettres cible.

    Search-Mailbox -Identity "April Stewart" -SearchQuery 'Subject:"Your bank statement"' -TargetMailbox administrator -TargetFolder "SearchAndDeleteLog" -LogOnly -LogLevel Full

Cet exemple permet d’effectuer une recherche dans toutes les boîtes aux lettres de l’organisation au niveau des messages comprenant n’importe quel type de fichier joint qui contient le mot « Trojan » dans le nom de fichier et envoie un message de journal à la boîte aux lettres de l’administrateur.

    Get-Mailbox -ResultSize unlimited | Search-Mailbox -SearchQuery attachment:trojan* -TargetMailbox administrator -TargetFolder "SearchAndDeleteLog" -LogOnly -LogLevel Full

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, consultez la rubrique [Search-Mailbox](https://technet.microsoft.com/fr-fr/library/dd298173\(v=exchg.150\)).

Revenir en haut de la page

## Rechercher et supprimer des messages

Cet exemple permet d'effectuer une recherche dans la boîte aux lettres d'April Stewart au niveau des messages dont le champ Objet contient l'expression « Your bank statement » et de supprimer les messages de la boîte aux lettres source sans copier les résultats de la recherche dans un autre dossier. Comme expliqué précédemment, le rôle de gestion Importation/Exportation de boîte aux lettres doit vous avoir été attribué pour que vous puissiez supprimer des messages de la boîte aux lettres d’un utilisateur.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159813.important(EXCHG.150).gif" title="Important" alt="Important" />Important :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Quand vous utilisez la cmdlet <strong>Search-Mailbox</strong> avec le commutateur <em>DeleteContent</em>, les messages sont définitivement supprimés de la boîte aux lettres source. Avant de supprimer définitivement des messages, nous vous conseillons d'utiliser le commutateur <em>LogOnly</em> pour générer un journal des messages identifiés lors de la recherche avant qu'ils ne soient supprimés ou de copier les messages vers une autre boîte aux lettres avant leur suppression de la boîte aux lettres source.</td>
</tr>
</tbody>
</table>


    Search-Mailbox -Identity "April Stewart" -SearchQuery 'Subject:"Your bank statement"' -DeleteContent

Cet exemple permet d'effectuer une recherche dans la boîte aux lettres d'April Stewart au niveau des messages dont le champ Objet contient l'expression « Your bank statement », de copier les résultats de la recherche dans le dossier AprilStewart-DeletedMessages de la boîte aux lettres BackupMailbox et de supprimer les messages de la boîte aux lettres d'April.

    Search-Mailbox -Identity "April Stewart" -SearchQuery 'Subject:"Your bank statement"' -TargetMailbox "BackupMailbox" -TargetFolder "AprilStewart-DeletedMessages" -LogLevel Full -DeleteContent

Cet exemple permet d’effectuer une recherche dans toutes les boîtes aux lettres de l’organisation au niveau des messages ayant pour objet « Download this file » et les supprime définitivement.

    Get-Mailbox -ResultSize unlimited | Search-Mailbox -SearchQuery 'Subject:"Download this file"' -DeleteContent

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, consultez la rubrique [Search-Mailbox](https://technet.microsoft.com/fr-fr/library/dd298173\(v=exchg.150\)).

Revenir en haut de la page

## Utilisation du paramètre -LogLevel Full

Dans certains des exemples ci-dessus, le paramètre *LogLevel* avec la valeur `Full` est utilisé pour consigner des informations détaillées concernant les résultats renvoyés par la cmdlet **Search-Mailbox**. Lorsque vous incluez ce paramètre, un courrier électronique est créé et envoyé à la boîte aux lettres spécifiée par le paramètre *TargetMailbox*. Le fichier journal (au format CSV nommé Résultats recherche.csv) est joint au courrier électronique et est disponible dans le dossier indiqué par le paramètre *TargetFolder*. Le fichier journal comporte une ligne par message inclus dans les résultats de la recherche lorsque vous exécutez la cmdlet **Search-Mailbox**.

