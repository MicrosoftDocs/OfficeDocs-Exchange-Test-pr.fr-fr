---
title: 'Configurer les propriétés des copies de la base de données de boîtes aux lettres: Exchange 2013 Help'
TOCTitle: Configurer les propriétés des copies de la base de données de boîtes aux lettres
ms:assetid: cf186561-ab2c-45c0-90f5-8d3ecfabeeac
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dd351151(v=EXCHG.150)
ms:contentKeyID: 50479199
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurer les propriétés des copies de la base de données de boîtes aux lettres

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2012-11-01_

Chaque copie de base de données de boîtes aux lettres possède ses propres propriétés que vous pouvez configurer. Celles-ci incluent le délai, le cas échéant, d’attente de relecture et de troncation, ainsi que le numéro de préférence d’activation. Pour plus d’informations sur le délai d’attente de relecture, le délai d’attente de troncation et le numéro de préférence d’activation, voir [Gestion des copies de base de données de boîtes aux lettres](managing-mailbox-database-copies-exchange-2013-help.md).

## Ce qu’il faut savoir avant de commencer ?

  - Durée d’exécution estimée de cette tâche : 1 minute

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultezEntrée « Copies de bases de données de boîtes aux lettres » dans la rubrique [Autorisations de haute disponibilité et de résilience des sites](high-availability-and-site-resilience-permissions-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..


## Que souhaitez-vous faire ?

## Utiliser le CAE pour configurer les propriétés de copie de la base de données de boîtes aux lettres

1.  Dans la CCE, accédez à **Serveurs** \> **Bases de données**.

2.  Sélectionnez la base de données à configurer.

3.  Dans le volet Détails, sous **Copies de base de données**, cliquez sur **Afficher les détails** pour la copie de base de données désirée, puis affichez ou configurez ce qui suit :
    
      - **Base de données**   Ce champ affiche le nom de la base de données sélectionnée.
    
      - **Serveur de boîtes aux lettres**   Ce champ affiche le nom du serveur de boîtes aux lettres qui héberge la copie de base de données sélectionnée.
    
      - **État de l’index de contenu** Ce champ affiche l’état actuel de l’index de contenu pour la copie de base de données sélectionnée.
    
      - **État**   Ce champ affiche l’état actuel de la copie de base de données sélectionnée.
    
      - **Longueur de la file d’attente de copie**   Ce champ indique le nombre de fichiers journaux en attente de copie dans la copie de base de données sélectionnée. Ce champ s’applique uniquement aux copies de base de données passives.
    
      - **Longueur de la file d’attente de relecture**   Ce champ indique le nombre de fichiers journaux en attente de relecture dans la copie de base de données sélectionnée. Ce champ s’applique uniquement aux copies de base de données passives.
    
      - **Messages d’erreurs**   Ce champ affiche les messages d’erreur concernant les copies de base de données dont l’état est `Failed` ou `Failed and Suspended`.
    
      - **Heure du dernier journal disponible**   Ce champ affiche la date et l’horodatage du dernier fichier journal généré sur la copie active de la base de données. Ce champ s’applique uniquement aux copies de base de données passives. Sur les copies de bases de données actives (répliquées et autonomes), ce champ affiche **jamais**.
    
      - **Heure du dernier journal inspecté**   Ce champ affiche la date et l’horodatage du dernier fichier journal inspecté par LogInspector sur la copie de base de données sélectionnée. Ce champ s’applique uniquement aux copies de base de données passives. Sur les copies de bases de données actives (répliquées et autonomes), ce champ affiche **jamais**.
    
      - **Heure du dernier journal copié**   Ce champ affiche la date et l’horodatage du dernier fichier journal copié par LogCopier sur la copie de base de données sélectionnée. Ce champ s’applique uniquement aux copies de base de données passives. Sur les copies de bases de données actives (répliquées et autonomes), ce champ affiche **jamais**.
    
      - **Heure du dernier journal relu**   Ce champ affiche la date et l’horodatage du dernier fichier journal relu par LogReplayer dans la copie de base de données sélectionnée. Ce champ s’applique uniquement aux copies de base de données passives. Sur les copies de bases de données actives (répliquées et autonomes), ce champ affiche **jamais**.
    
      - **Numéro de préférence d’activation**   Ce champ affiche le numéro de préférence d’activation. Il s’utilise dans le cadre du processus de sélection de la meilleure copie d’Active Manager et pour équilibrer le groupe de disponibilité de base de données (DAG) en redistribuant les bases de données de boîtes aux lettres actives dans tout le groupe de disponibilité de base de données lors de l’utilisation du script RedistributeActiveDatabases.ps1. La valeur de la préférence d’activation est un nombre supérieur ou égal à 1, où 1 correspond à l’ordre de préférence le plus élevé. Le nombre ne peut pas être supérieur au nombre de copies de la base de données de boîtes aux lettres.
    
      - **Retard de relecture (jours)**   Ce champ affiche le temps d’attente de la banque d’informations de Microsoft Exchange avant la relecture des fichiers journaux qui ont été copiés par le service de réplication Microsoft Exchange vers la copie de la base de données passive. La définition de ce paramètre sur une valeur supérieure à 0 crée une copie de la base de données retardée. Le paramètre par défaut pour cette valeur est 0 jour. La valeur maximale autorisée pour ce paramètre est 14 jours. La valeur minimale autorisée est 0 jour ; la définition de cette valeur sur 0 désactive le retard de relecture.

## Utiliser l’environnement de ligne de commande Exchange Management Shell pour configurer les propriétés de copie de la base de données de boîtes aux lettres

Cet exemple configure la copie d’une base de données de boîtes aux lettres dont le numéro de préférence d’activation est 3.

    Set-MailboxDatabaseCopy -Identity DB3\EX3 -ActivationPreference 3

Cet exemple illustre la configuration de la copie de la base de données DB1 hébergée sur Server1 avec un retard de relecture et un retard de troncation de 1 jour et un numéro de préférence d’activation de 2.

    Set-MailboxDatabaseCopy -Identity DB1\Server1 -ReplayLagTime 1.0:0:0 -TruncationLagTime 1.0:0:0 -ActivationPreference 2

## Comment savoir si cela a fonctionné ?

Pour vérifier que la configuration de la copie de base de données de boîtes aux lettres s’est bien effectuée, procédez de l’une des manières suivantes :

  - Dans le CAE, accédez à **Serveurs** \> **Bases de données**. Sélectionnez la base de données appropriée et, dans le volet Détails, cliquez sur **Afficher les détails** pour afficher les propriétés de la copie de base de données.

  - Dans l’environnement de ligne de commande Exchange Management Shell, exécutez la commande suivante pour afficher les informations de configuration pour une copie de base de données.
    
        Get-MailboxDatabaseCopyStatus <DatabaseCopyName> | Format-List

## Pour plus d’informations

[Set-MailboxDatabaseCopy](https://technet.microsoft.com/fr-fr/library/dd298104\(v=exchg.150\))

[Get-MailboxDatabaseCopyStatus](https://technet.microsoft.com/fr-fr/library/dd298044\(v=exchg.150\))

[Get-MailboxDatabase](https://technet.microsoft.com/fr-fr/library/bb124924\(v=exchg.150\))

