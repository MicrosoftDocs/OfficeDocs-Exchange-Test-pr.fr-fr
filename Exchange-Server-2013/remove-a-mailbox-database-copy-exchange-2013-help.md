---
title: 'Supprimer une copie de base de données de boîtes aux lettres: Exchange 2013 Help'
TOCTitle: Supprimer une copie de base de données de boîtes aux lettres
ms:assetid: 99fecdde-b158-4dfc-9ca7-ff7c0ada7819
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dd298164(v=EXCHG.150)
ms:contentKeyID: 50478783
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Supprimer une copie de base de données de boîtes aux lettres

 

_**Sapplique à :**Exchange Server 2013_

_**Dernière rubrique modifiée :**2012-11-06_

Ces procédures vous montrent comment supprimer une copie d’une base de données de boîtes aux lettres. Vous ne pouvez pas utiliser ces procédures pour supprimer la dernière copie de la base de données de boîtes aux lettres. Pour obtenir des instructions détaillées sur la manière de supprimer la dernière copie d’une base de données de boîtes aux lettres, voir [Remove a mailbox database](manage-mailbox-databases-in-exchange-2013-exchange-2013-help.md) ou [Remove-MailboxDatabase](https://technet.microsoft.com/fr-fr/library/aa997931\(v=exchg.150\)).

Souhaitez-vous rechercher les autres tâches de gestion relatives aux copies de la base de données de boîtes aux lettres ? Consultez la rubrique [Gestion des copies de base de données de boîtes aux lettres](managing-mailbox-database-copies-exchange-2013-help.md).

## Ce qu’il faut savoir avant de commencer ?

  - Durée d’exécution estimée de cette tâche : 1 minute

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultezEntrée « Copies de bases de données de boîtes aux lettres » dans la rubrique [Autorisations de haute disponibilité et de résilience des sites](high-availability-and-site-resilience-permissions-exchange-2013-help.md).

  - Les copies de bases de données de boîtes aux lettres peuvent uniquement être supprimées d’un groupe de disponibilité de base de données sain. Si le groupe de disponibilité de base de données n’est pas sain (par exemple, le cluster sous-jacent du groupe de disponibilité de base de données n’est pas opérationnel car le quorum a été perdu), vous ne pourrez pas supprimer de copies de base de données de boîtes aux lettres.

  - Si vous supprimez la dernière copie passive de la base de données, la connexion circulaire à la réplication continue (CRCL) ne doit pas être activée pour la base de données de boîtes aux lettres spécifiée. S la CRCL est activée, vous devez d’abord la désactiver. La connexion circulaire pourra être activée après la suppression de la copie de la base de données de boîtes aux lettres. Une fois activée pour une base de données de boîtes aux lettres non répliquée, la connexion circulaire JET est utilisée à la place de la connexion CRCL. Si vous ne supprimez pas la dernière copie passive d’une base de données, la connexion CRCL peut rester activée.

  - Après suppression d’une copie de base de données, vous devez manuellement supprimer toute base de données et fichiers de journalisation de transaction du serveur à partir duquel la base de données est en cours de suppression.

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

<table>
<thead>
<tr class="header">
<th><img src="images/Bb125224.tip(EXCHG.150).gif" title="Conseil" alt="Conseil" />Conseil :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..</td>
</tr>
</tbody>
</table>


## Que souhaitez-vous faire ?

## Utiliser le Centre d'administration Exchange pour supprimer une copie de la base de données de boîtes aux lettres

1.  Dans la CCE, accédez à **Serveurs** \> **Bases de données**.

2.  Sélectionnez la base de données de boîtes aux lettres dont vous souhaitez supprimer la copie.

3.  Dans le volet d’informations, accédez à la copie passive à supprimer, puis cliquez sur **Supprimer**.

4.  Dans la boîte de dialogue Avertissement, confirmez la suppression en cliquant sur **Oui**.

5.  Cliquez sur **Ok** pour confirmer la suppression, après avoir examiné tous les messages.

6.  Supprimez manuellement tous les fichiers journaux de transactions et de base de données du serveur duquel la copie de la base de données est supprimée.

## Utiliser l’environnement de ligne de commande Exchange Management Shell pour supprimer une copie de base de données de boîtes aux lettres

Dans cet exemple, nous supprimons une copie de base de données de boîtes aux lettres DB1 dans le serveur de boîtes aux lettres MBX1.

    Remove-MailboxDatabaseCopy -Identity DB1\MBX1 -Confirm:$False

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez bien supprimé une copie de base de données de boîtes aux lettres, procédez de l’une des manières suivantes :

  - Dans le CAE, accédez à **Serveurs** \> **Bases de données**. Sélectionnez la base de données appropriée et, dans le volet d'informations, vérifiez que la copie passive supprimée n'apparaît plus.

  - Dans l’environnement de ligne de commande Exchange Management, exécutez la commande suivante pour vérifier la suppression de la copie.
    
        Get-MailboxDatabase <DatabaseName> | Format-List DatabaseCopies
    
    La copie passive supprimée n'est plus répertoriée.

