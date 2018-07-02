---
title: 'Interruption ou reprise d’une copie de base de données de boîtes aux lettres: Exchange 2013 Help'
TOCTitle: Interruption ou reprise d’une copie de base de données de boîtes aux lettres
ms:assetid: 96aa1b82-3e15-4215-843e-3d583af9504b
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dd298159(v=EXCHG.150)
ms:contentKeyID: 50478768
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Interruption ou reprise d’une copie de base de données de boîtes aux lettres

 

_**Sapplique à :**Exchange Server 2013_

_**Dernière rubrique modifiée :**2012-11-02_

Il peut être nécessaire de suspendre ou de reprendre une copie de base de données pour différentes raisons, par exemple la maintenance du disque contenant la copie de la base de données, ou pour suspendre l’activation de la copie d’une base de données individuelle à des fins de récupération d’urgence.

Souhaitez-vous rechercher les autres tâches de gestion relatives aux copies de la base de données de boîtes aux lettres ? Consultez la rubrique [Gestion des copies de base de données de boîtes aux lettres](managing-mailbox-database-copies-exchange-2013-help.md).

## Ce qu’il faut savoir avant de commencer ?

  - Durée d’exécution estimée de cette tâche : 1 minute

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultezEntrée « Copies de bases de données de boîtes aux lettres » dans la rubrique [Autorisations de haute disponibilité et de résilience des sites](high-availability-and-site-resilience-permissions-exchange-2013-help.md).

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

## Utiliser le Centre d’administration Exchange (EAC) pour interrompre une copie de la base de données de boîtes aux lettres

1.  Dans l’EAC, accédez à **Serveurs** \> **Bases de données**.

2.  Sélectionnez la base de données dont vous voulez suspendre la copie.

3.  Dans le volet d’informations, sous **Copies de base de données**, cliquez sur **Suspendre** sous la copie de base de données que vous souhaitez suspendre.

4.  Dans le champ **Commentaires**, ajoutez un commentaire facultatif d’une longueur maximale de 512 caractères indiquant la raison de la suspension.

5.  Pour suspendre l’activation automatique de la copie de la base de données, activez la case à cocher **Cette copie peut uniquement être activée manuellement**.

6.  Cliquez sur **enregistrer** pour enregistrer la copie de base de données.

## Utiliser le Centre d’administration Exchange (EAC) pour reprendre la copie d’une base de données de boîtes aux lettres

1.  Dans l’EAC, accédez à **Serveurs** \> **Bases de données**.

2.  Sélectionnez la base de données dont vous souhaitez reprendre la copie.

3.  Dans le volet d’informations, sous **Copies de base de données**, cliquez sur **Reprendre** sous la copie de base de données que vous souhaitez reprendre.

4.  Cliquez sur **Oui** pour reprendre la copie de base de données.

## Utiliser l’environnement de ligne de commande pour interrompre une copie de base de données de boîtes aux lettres

Dans cet exemple, nous suspendons la réplication en continue pour la copie de la base de données DB1 hébergée sur le serveur MBX1. Un commentaire facultatif a également été spécifié.

    Suspend-MailboxDatabaseCopy -Identity DB1\MBX1 -SuspendComment "Maintenance on MBX1" -Confirm:$False

Dans cet exemple, nous suspendons l’activation pour la copie de la base de données DB2 hébergée sur le serveur MBX2.

    Suspend-MailboxDatabaseCopy -Identity DB2\MBX2 -ActivationOnly -Confirm:$False

## Utiliser l’environnement de ligne de commande pour reprendre une copie de base de données de boîtes aux lettres

Dans cet exemple, nous reprenons la copie de la base de données DB1 sur le serveur MBX1.

    Resume-MailboxDatabaseCopy -Identity DB1\MBX1

Dans cet exemple, nous reprenons la copie de la base de données DB2 sur le serveur MBX2 pour la réplication uniquement.

    Resume-MailboxDatabaseCopy -Identity DB2\MBX2 -ReplicationOnly

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez réussi à suspendre ou reprendre la copie d’une base de données de boîte aux lettres, effectuez l’une des actions suivantes :

  - Dans le CAE, accédez à **Serveurs** \> **Bases de données**. Sélectionnez la base de données appropriée et, dans le volet Détails, cliquez sur **Afficher les détails** pour afficher les propriétés de la copie de base de données.

  - Dans l’environnement de ligne de commande Exchange Management Shell, exécutez la commande suivante pour afficher les informations d’état pour une copie de base de données.
    
        Get-MailboxDatabaseCopyStatus <DatabaseCopyName> | Format-List

