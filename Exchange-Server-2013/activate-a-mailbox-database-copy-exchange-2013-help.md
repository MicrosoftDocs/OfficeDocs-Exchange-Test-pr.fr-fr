---
title: 'Activer une copie de la base de données de boîtes aux lettres: Exchange 2013 Help'
TOCTitle: Activer une copie de la base de données de boîtes aux lettres
ms:assetid: d948269b-c902-4d8d-8c2b-269473359baa
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Ee364750(v=EXCHG.150)
ms:contentKeyID: 50479307
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Activer une copie de la base de données de boîtes aux lettres

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2012-11-01_

L'activation de la copie d'une base de données de boîtes aux lettres consiste à désigner une copie passive spécifique comme nouvelle copie active d'une base de données de boîtes aux lettres. Ce processus est parfois appelé *basculement de base de données*. Un basculement de base de données implique le démontage de la base de données actuellement active et le montage de la copie de la base de données sur le serveur spécifié en tant que nouvelle copie de base de données de boîtes aux lettres active. La copie de la base de données qui va devenir la base de données de boîtes aux lettres active doit être intègre et opérationnelle.

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

## Utilisation du Centre d’administration Exchange pour déplacer la base de données de boîtes aux lettres active

1.  Dans la CCE, accédez à **Serveurs** \> **Bases de données**.

2.  Sélectionnez la base de données dont vous souhaitez activer la copie.

3.  Dans le volet Détails, sous **Copies de base de données**, cliquez sur **Activer** sous la copie de base de données que vous souhaitez activer.

4.  Cliquez sur **oui** pour activer la copie de base de données.

## Utilisation de l’environnement de ligne de commande Exchange Management Shell pour déplacer la base de données de boîtes aux lettres active

Dans cet exemple, une copie de la base de données DB4 hébergée sur MBX3 est activée et montée en tant que nouvelle base de données de boîtes aux lettres active. Avec cette commande, DB4 devient la nouvelle base de données de boîtes aux lettres active et ne remplace pas les paramètres de numérotation de montage de base de données sur MBX3.

    Move-ActiveMailboxDatabase DB4 -ActivateOnServer MBX3 -MountDialOverride:None

Cet exemple exécute un basculement de la base de données DB2 vers le serveur de boîtes aux lettres MBX1. Lorsque la commande est terminée, MBX1 héberge la copie active de DB2. Étant donné que le paramètre *MountDialOverride* est défini sur `None`, MBX1 monte la base de données à l’aide de ses propres paramètres de montage automatique.

    Move-ActiveMailboxDatabase DB2 -ActivateOnServer MBX1 -MountDialOverride:None

Cet exemple exécute un basculement de la base de données DB1 vers le serveur de boîtes aux lettres MBX3. Lorsque la commande est terminée, MBX3 héberge la copie active de DB1. Étant donné que le paramètre *MountDialOverride* est spécifié avec la valeur `Good Availability`, MBX3 monte la base de données avec le paramètre de montage automatique *GoodAvailability*.

    Move-ActiveMailboxDatabase DB1 -ActivateOnServer MBX3 -MountDialOverride:GoodAvailability

Cet exemple exécute un basculement de la base de données DB3 vers le serveur de boîtes aux lettres MBX4. Lorsque la commande est terminée, MBX4 héberge la copie active de DB3. Étant donné que le paramètre *MountDialOverride* n'est pas spécifié, MBX4 monte la base de données avec le paramètre de montage automatique *Lossless*.

    Move-ActiveMailboxDatabase DB3 -ActivateOnServer MBX4

Cet exemple effectue un basculement de serveur pour le serveur de boîte aux lettres nommé MBX1. Toutes les copies de la base de données de boîtes aux lettres actives sur MBX1 seront activées sur un ou plusieurs autres serveurs de boîtes aux lettres en utilisant des copies intègres des bases de données actives sur MBX1.

    Move-ActiveMailboxDatabase -Server MBX1

Cet exemple exécute un basculement de la base de données DB4 vers le serveur de boîtes aux lettres MBX5. Dans cet exemple, la copie de la base de données sur MBX5 possède une file d'attente de relecture supérieure à 6. Il en résulte que le paramètre *SkipLagChecks* doit être spécifié pour que la copie de la base de données soit activée sur MBX5.

    Move-ActiveMailboxDatabase DB4 MBX5 -SkipLagChecks

Cet exemple exécute un basculement de la base de données DB5 vers le serveur de boîtes aux lettres MBX6. Dans cet exemple, la copie de la base de données sur MBX6 possède un paramètre *ContentIndexState* ayant échoué. Il en résulte que le paramètre *SkipClientExperienceChecks* doit être spécifié pour que la copie de la base de données soit activée sur MBX6.

    Move-ActiveMailboxDatabase DB5 MBX6 -SkipClientExperienceChecks

## Comment savoir si cela a fonctionné ?

Pour vérifier que l’activation de la copie de base de données de boîtes aux lettres s’est bien effectuée, procédez de l’une des manières suivantes :

  - Dans le CAE, accédez à **Serveurs** \> **Bases de données**. Sélectionnez la base de données appropriée et, dans le volet Détails, cliquez sur **Afficher les détails** pour afficher les propriétés de la copie de base de données.

  - Dans l’environnement de ligne de commande Exchange Management Shell, exécutez la commande suivante pour afficher les informations d’état pour une copie de base de données.
    
        Get-MailboxDatabaseCopyStatus <DatabaseCopyName> | Format-List

## Pour plus d'informations

[Copies de bases de données de boîtes aux lettres](mailbox-database-copies-exchange-2013-help.md)

[Configurer les propriétés des copies de la base de données de boîtes aux lettres](configure-mailbox-database-copy-properties-exchange-2013-help.md)

