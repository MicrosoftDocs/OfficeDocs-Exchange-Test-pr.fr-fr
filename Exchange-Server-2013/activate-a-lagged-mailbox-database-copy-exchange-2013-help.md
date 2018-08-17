---
title: 'Activation d’une copie de la base de données de boîtes aux lettres retardée: Exchange 2013 Help'
TOCTitle: Activation d’une copie de la base de données de boîtes aux lettres retardée
ms:assetid: 493d9c40-644d-49d6-9291-949acbcfdcb6
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dd979786(v=EXCHG.150)
ms:contentKeyID: 50478087
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Activation d’une copie de la base de données de boîtes aux lettres retardée

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2014-01-28_

Une copie de base de données de boîte aux lettres retardée est configurée avec un délai d'attente de relecture supérieur à 0. L'activation et la récupération d'une copie de base de données de boîte aux lettres retardée constitue un processus simple si vous souhaitez que la base de données relise tous les fichiers journaux et active la copie de base de données. Si vous souhaitez relire les fichiers journaux jusqu'à un moment spécifique dans le temps, l'opération se complique car il vous faut manipuler manuellement les fichiers journaux et exécuter Eseutil.

Vous recherchez des informations supplémentaires sur les copies retardées de base de données de boîtes aux lettres ? Consultez la rubrique [Gestion des copies de base de données de boîtes aux lettres](managing-mailbox-database-copies-exchange-2013-help.md).

> [!NOTE]
> Le délai nécessaire à l'activation d'une copie de base de données de boîte aux lettres retardée dépend directement du nombre de fichiers journaux devant être relus ainsi que de la vitesse de lecture permise par le matériel. Vous pouvez voir, au minimum, une fréquence de relecture d’au moins deux journaux par seconde et par base de données.


## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée de cette tâche : 1 minute, plus la durée nécessaire à la duplication de la copie retardée, la relecture des fichiers journaux requis et l'extraction des données ou le montage de la base de données pour l'activité du client.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l'entrée « Copies de bases de données de boîtes aux lettres » dans la rubrique [Autorisations de haute disponibilité et de résilience des sites](high-availability-and-site-resilience-permissions-exchange-2013-help.md).

  - La copie de base de données de boîte aux lettres en cours d'activation doit être configurée avec un délai d'attente de relecture supérieur à 0.

  - La copie de base de données de boîte aux lettres en cours d'activation doit disposer de tous les fichiers journaux émis jusqu'au moment où vous souhaitez la récupérer. Gardez à l'esprit que les transactions de base de données peuvent englober plusieurs fichiers journaux lorsque vous déterminez le moment jusqu'auquel vous souhaitez effectuer la récupération.

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..


## Que souhaitez-vous faire ?

## Utilisation du Shell pour activer une copie de base de données de boîte aux lettres retardée à un moment spécifique

> [!NOTE]
> Vous ne pouvez pas utiliser le Centre d'administration Exchange (CAE) pour activer une copie de base de données de boîtes aux lettres retardée à un point spécifique dans le temps. Vous exécutez à la place une série d'étapes au moyen du Shell et de la ligne de commande.


1.  Cet exemple interrompt la réplication de la copie retardée en cours d'activation à l'aide de la cmdlet [Suspend-MailboxDatabaseCopy](https://technet.microsoft.com/fr-fr/library/dd351074\(v=exchg.150\)).
    
        Suspend-MailboxDatabaseCopy DB1\EX3 -SuspendComment "Activate lagged copy of DB1 on Server EX3" -Confirm:$false

2.  De manière facultative (afin de conserver une copie retardée), effectuez une copie de la copie de la base de données et de ses fichiers journaux.
    
    > [!NOTE]
    > À ce stade, la poursuite de cette procédure sur le volume existant pénaliserait les performances d'écriture de la copie. Si cette conséquence n'est pas souhaitée, vous pouvez copier la base de données et les fichiers journaux sur un autre volume pour effectuer la récupération.


3.  Déterminez les fichiers journaux à relire impérativement dans la base de données afin de satisfaire à vos exigences temporelles concernant cette récupération (en vous basant sur l'heure et la date des fichiers journaux, comme présenté dans Windows Explorer). Tous les fichiers journaux créés suite à ce moment doivent être déplacés vers un autre répertoire jusqu'à ce que le processus de récupération prenne fin et que les fichiers journaux ne soient plus nécessaires.

4.  Supprimez le fichier point de contrôle (.chk) de la base de données.

5.  Cet exemple utilise la commande Eseutil pour effectuer l'opération de récupération.
    
        Eseutil.exe /r eXX /a
    
    > [!NOTE]
    > Dans l'exemple précédent, e<em>XX</em> est le préfixe de génération du journal pour la base de données (par exemple, E00, E01, E02, etc.).
    
    > [!IMPORTANT]
    > Cette étape peut demander beaucoup de temps et plusieurs facteurs influent, tels que la longueur du temps d'attente de relecture, le nombre de fichiers journaux générés au cours de cette période et la vitesse à laquelle votre matériel est en mesure de relire ces journaux dans la base de données en cours de récupération.


6.  Une fois la relecture des journaux terminée, la base de données se trouve dans un état d'arrêt correct et peut être copiée, puis utilisée dans le cadre d'une récupération.

7.  Suite au processus de récupération, cet exemple reprend la réplication de la base de données qui a été utilisée dans le cadre de l'opération de récupération.
    
        Resume-MailboxDatabaseCopy DB1\EX3

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, consultez les rubriques [Suspend-MailboxDatabaseCopy](https://technet.microsoft.com/fr-fr/library/dd351074\(v=exchg.150\)) et [Resume-MailboxDatabaseCopy](https://technet.microsoft.com/fr-fr/library/dd335220\(v=exchg.150\)).

## Utilisez le Shell pour activer une copie de base de données de boîtes aux lettres retardée en relisant tous les fichiers journaux non validé

1.  De manière facultative (afin de conserver une copie retardée), effectuez une copie de la copie de la base de données et de ses fichiers journaux.
    
    1.  Cet exemple interrompt la réplication de la copie retardée en cours d'activation à l'aide de la cmdlet [Suspend-MailboxDatabaseCopy](https://technet.microsoft.com/fr-fr/library/dd351074\(v=exchg.150\)).
        
            Suspend-MailboxDatabaseCopy DB1\EX3 -SuspendComment "Activate lagged copy of DB1 on Server EX3" -Confirm:$false
    
    2.  De manière facultative (afin de conserver une copie retardée), effectuez une copie de la copie de la base de données et de ses fichiers journaux.
        
        > [!NOTE]
        > À ce stade, la poursuite de cette procédure sur le volume existant pénaliserait les performances d'écriture de la copie. Si cette conséquence n'est pas souhaitée, vous pouvez copier la base de données et les fichiers journaux sur un autre volume pour effectuer la récupération.


2.  Cet exemple active la copie de base de données de boîtes aux lettres retardée en utilisant la cmdlet [Move-ActiveMailboxDatabase](https://technet.microsoft.com/fr-fr/library/dd298068\(v=exchg.150\)) avec le paramètre *SkipLagChecks*.
    
        Move-ActiveMailboxDatabase DB1 -ActivateOnServer EX3 -SkipLagChecks

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour activer une copie de base de données de boîtes aux lettres retardée à l'aide de la fonctionnalité de récupération SafetyNet

1.  De manière facultative, (afin d'éviter une copie retardée), prenez un instantané VSS basé sur un système de fichiers (non compatible avec Exchange) des volumes contenant la copie de base de données et ses fichiers journaux.
    
    1.  Cet exemple interrompt la réplication de la copie retardée en cours d'activation à l'aide de la cmdlet [Suspend-MailboxDatabaseCopy](https://technet.microsoft.com/fr-fr/library/dd351074\(v=exchg.150\)).
        
            Suspend-MailboxDatabaseCopy DB1\EX3 -SuspendComment "Activate lagged copy of DB1 on Server EX3" -Confirm:$false
    
    2.  De manière facultative (afin de conserver une copie retardée), effectuez une copie de la copie de la base de données et de ses fichiers journaux.
        
        > [!NOTE]
        > À ce stade, la poursuite de cette procédure sur le volume existant pénaliserait les performances d'écriture de la copie. Si cette conséquence n'est pas souhaitée, vous pouvez copier la base de données et les fichiers journaux sur un autre volume pour effectuer la récupération.


2.  Déterminez les journaux requis pour la copie de base de données retardée en recherchant la valeur « Log required: » (Journal requis) dans la sortie de l'en-tête de base de données ESEUTIL
    
        Eseutil /mh <DBPath> | findstr /c:"Log Required"
    
    Notez les numéros hexadécimaux entre parenthèses. Le premier numéro correspond à la génération requise la plus faible (désignée par LowGeneration) et le deuxième numéro à la génération requise la plus élevée (désignée par HighGeneration). Déplacez tous les fichiers de génération de journaux dont la séquence de génération est supérieure à HighGeneration vers un autre emplacement, afin qu'ils ne soient pas relus dans la base de données.

3.  Sur le serveur hébergeant la copie active de la base de données, supprimez les fichiers journaux pour la copie retardée en cours d'activation de la copie active, ou arrêtez le service de réplication Microsoft Exchange.

4.  Effectuez un basculement de base de données et activez la copie retardée. Cet exemple active la base de données à l'aide de la cmdlet [Move-ActiveMailboxDatabase](https://technet.microsoft.com/fr-fr/library/dd298068\(v=exchg.150\)) avec différents paramètres.
    
        Move-ActiveMailboxDatabase DB1 -ActivateOnServer EX3 -MountDialOverride BestEffort -SkipActiveCopyChecks -SkipClientExperienceChecks -SkipHealthChecks -SkipLagChecks

5.  À ce stade, la base de données est automatiquement montée et demande une nouvelle remise des messages manquants à partir de SafetyNet.

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez bien activé une copie de base de données de boîtes aux lettres retardée, procédez de l'une des manières suivantes :

  - Dans le CAE, accédez à **Serveurs** \> **Bases de données**. Sélectionnez la base de données appropriée et, dans le volet Détails, cliquez sur **Afficher les détails** pour afficher les propriétés de la copie de base de données.

  - Dans l’environnement de ligne de commande Exchange Management Shell, exécutez la commande suivante pour afficher les informations d’état pour une copie de base de données.
    
        Get-MailboxDatabaseCopyStatus <DatabaseCopyName> | Format-List

