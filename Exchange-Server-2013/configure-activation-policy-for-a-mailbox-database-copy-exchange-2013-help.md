---
title: 'Configurer la stratégie d’activation pour une copie de base de données de boîte aux lettres: Exchange 2013 Help'
TOCTitle: Configurer la stratégie d’activation pour une copie de base de données de boîte aux lettres
ms:assetid: 6b37ed6e-2e36-4688-b485-8fdbb8193ec8
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dd298046(v=EXCHG.150)
ms:contentKeyID: 50478371
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configurer la stratégie d’activation pour une copie de base de données de boîte aux lettres

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2012-11-02_

L’*activation* est le processus de transformation d’une copie passive de la base de données de boîtes aux lettres en une copie active. L’activation est exécutée automatiquement par le système dans le cadre d’une opération de basculement de base de données ou de serveur, mais peut aussi être effectuée manuellement par un administrateur dans le cadre d'une opération de switchover de base de données ou de serveur. Le blocage d’une base de données empêche cette dernière de devenir la copie active lors d’un basculement de base de données ou de serveur.

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

## Utiliser le Centre d’administration Exchange (EAC) pour configurer la stratégie d’activation d’une copie de la base de données de boîtes aux lettres

1.  
    
    Dans la CCE, accédez à **Serveurs** \> **Bases de données**.

2.  Sélectionnez la base de données que vous souhaitez configurer.

3.  
    
    Dans le volet d’informations, sous **Copies de base de données**, recherchez la copie de base de données que vous souhaitez configurer, puis cliquez sur **Interrompre**.

4.  Vous pouvez également ajouter un commentaire et activer la case à cocher **Cette copie peut uniquement être activée manuellement**.

5.  Cliquez sur **Enregistrer** pour enregistrer les modifications apportées à la configuration de la copie de base de données de boîtes aux lettres.

## Utiliser l’environnement de ligne de commande Exchange Management Shell pour interrompre ou reprendre une copie de base de données pour activation

Cet exemple indique comment bloquer la copie de la base de données DB1 sur le serveur MBX2 dans le cadre du processus d’activation.

    Suspend-MailboxDatabaseCopy -Identity DB1\MBX2 -ActivationOnly

Cet exemple indique comment reprendre la copie de la base de données DB1 sur le serveur MBX2 dans le cadre du processus d’activation.

    Resume-MailboxDatabaseCopy -Identity DB1\MBX2

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Suspend-MailboxDatabaseCopy](https://technet.microsoft.com/fr-fr/library/dd351074\(v=exchg.150\)) et [Resume-MailboxDatabaseCopy](https://technet.microsoft.com/fr-fr/library/dd335220\(v=exchg.150\)).

## Utiliser l’environnement de ligne de commande Exchange Management Shell pour configurer la stratégie d’activation d’un serveur

Cet exemple configure les copies de base de données sur le serveur MBX2 afin qu’elles soient bloquées pour l’activation.

    Set-MailboxServer -Identity MBX2 -DatabaseCopyAutoActivationPolicy Blocked

Cet exemple configure les copies de base de données sur le serveur MBX3 afin qu’elles soient bloquées pour l’activation hors site.

    Set-MailboxServer -Identity MBX3 -DatabaseCopyAutoActivationPolicy IntrasiteOnly

Cet exemple configure les copies de base de données sur le serveur MBX4 afin qu’elles soient débloquées pour l’activation.

    Set-MailboxServer -Identity MBX4 -DatabaseCopyAutoActivationPolicy Unrestricted

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Suspend-MailboxDatabaseCopy](https://technet.microsoft.com/fr-fr/library/dd351074\(v=exchg.150\)), [Resume-MailboxDatabaseCopy](https://technet.microsoft.com/fr-fr/library/dd335220\(v=exchg.150\)) ou [Set-MailboxServer](https://technet.microsoft.com/fr-fr/library/aa998651\(v=exchg.150\)).

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez bien configuré la stratégie d’activation, procédez de l’une des manières suivantes :

  - Dans l’environnement de ligne de commande Exchange Management Shell, exécutez la commande suivante pour vérifier les paramètres d’activation d’une copie de base de données :
    
        Get-MailboxDatabaseCopyStatus <DatabaseCopyName> | Format-List ActivationSuspended

  - Dans l’environnement de ligne de commande Exchange Management Shell, exécutez la commande suivante pour vérifier les paramètres d’activation d’un membre du groupe de disponibilité de base de données :
    
        Get-MailboxServer <ServerName> | Format-List DatabaseCopyAutoActivationPolicy

