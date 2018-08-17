---
title: 'Config. d’AutoReseed pr un groupe de disponibilité de BDD: Exchange 2013 Help'
TOCTitle: Configuration d’AutoReseed pour un groupe de disponibilité de base de données
ms:assetid: 4a8bd779-b52a-40ed-8040-4d76eabeb41e
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ619303(v=EXCHG.150)
ms:contentKeyID: 50478100
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configuration d’AutoReseed pour un groupe de disponibilité de base de données

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2013-04-15_

AutoReseed est une fonction qui permet de restaurer rapidement la redondance des bases de données après une erreur du disque. En cas de défaillance du disque, les copies de bases de données stockées sur le disque sont automatiquement réamorcées sur un disque de rechange préconfiguré sur le serveur de boîtes aux lettres. Suivez les étapes indiquées dans la présente rubrique pour configurer AutoReseed pour un groupe de disponibilité de base de données.

> [!CAUTION]
> La fonction AutoReseed n'effectue aucune tâche de configuration prérequise à votre place. L'installation correcte des disques, l'ajout des disques de réserve au système, le remplacement des disques incorrects et le formatage de nouveaux disques doivent être exécutés manuellement pas un administrateur.


Si vous souhaitez rechercher des tâches de gestion supplémentaires relatives aux groupes de disponibilité de base de données, consultez la rubrique [Gestion de groupes de disponibilité de base de données](managing-database-availability-groups-exchange-2013-help.md).

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée de cette tâche : 10 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l'entrée « Groupes de disponibilité de la base de données » dans la rubrique [Autorisations de haute disponibilité et de résilience des sites](high-availability-and-site-resilience-permissions-exchange-2013-help.md).

  - Un disque/une partition logique unique par disque physique doit être créé(e).

  - La structure spécifique de la base de données et du dossier journal décrite dans les étapes ci-dessous doit être utilisée.

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..


## Comment procéder ?

## Étape 1 : Configurer les chemins d'accès racine aux bases de données et aux volumes

La première étape exige la configuration des répertoires racine pour les bases de données (*AutoDagDatabasesRootFolderPath*) et les volumes (*AutoDagVolumesRootFolderPath*) utilisés par le groupe de disponibilité de base de données. Les valeurs par défaut sont C:\\ExchangeDatabases et C:\\ExchangeVolumes, respectivement. Vous pouvez ignorer cette étape si vous utilisez les chemins d'accès par défaut.

Cet exemple montre comment configurer le chemin d'accès racine pour les bases de données.

    Set-DatabaseAvailabilityGroup DAG1 -AutoDagDatabasesRootFolderPath "C:\ExchDbs"

Cet exemple montre comment configurer le chemin d'accès racine pour les volumes de stockage.

    Set-DatabaseAvailabilityGroup DAG1 -AutoDagVolumesRootFolderPath "C:\ExchVols"

## Comment savoir si cette étape a fonctionné ?

Pour vérifier que vous avez bien configuré les chemins d'accès racine pour les bases de données et les volumes, exécutez la commande suivante :

    Get-DatabaseAvailabilityGroup DAG1 | Format-List *auto*

Le résultat pour *AutoDagDatabasesRootFolderPath* et *AutoDagVolumesRootFolderPath* doit refléter les chemins configurés.

## Étape 2 : Configurer plusieurs bases de données par volume

Configurez ensuite le nombre de bases de données par volume (*AutoDagDatabaseCopiesPerVolume*) pour le groupe de disponibilité de base de données.

Cet exemple montre comment configurer ce paramètre AutoReseed pour un groupe de disponibilité de base de données configuré avec 4 bases de données par volume.

    Set-DatabaseAvailabilityGroup DAG1 -AutoDagDatabaseCopiesPerVolume 4

## Comment savoir si cette étape a fonctionné ?

Pour vérifier que vous avez bien configuré le nombre de bases de données par volume, exécutez la commande suivante :

    Get-DatabaseAvailabilityGroup DAG1 | Format-List *auto*

Le résultat pour *AutoDagDatabaseCopiesPerVolume* doit refléter la valeur configurée.

## Étape 3 : Créez les répertoires racine pour des bases de données et des volumes

Créez ensuite les répertoires correspondant aux répertoires racine configurés à l'étape 1. Cet exemple montre comment créer les répertoires par défaut à l'aide de l'invite de commandes.

    md C:\ExchangeDatabases
    md C:\ExchangeVolumes
   

## Comment savoir si cette étape a fonctionné ?

Pour vérifier que vous avez bien configuré les répertoires racine des bases de données et des volumes, exécutez la commande suivante :

    Dir C:\

Les répertoires créés devraient apparaître dans la liste des résultats.

## Étape 4 : Montez les dossiers de volume

Pour chaque volume utilisé pour les bases de données (y compris les volumes de réserve), utilisez l'application Gestionnaire de disques Windows (diskmgmt.msc) pour monter chaque volume dans un dossier monté sous C:\\ExchangeVolumes\\. Par exemple, s'il existe 2 volumes avec des bases de données et un volume de rechange, montez les volumes sur les dossiers montés suivants :

  - C:\\ExchangeVolumes\\Volume1

  - C:\\ExchangeVolumes\\Volume2

  - C:\\ExchangeVolumes\\Volume3

Le nom des dossiers montés peut être n’importe quel nom de dossier, tant que les dossiers sont montés sous le chemin d’accès du volume racine.

## Comment savoir si cette étape a fonctionné ?

Pour vérifier que vous avez bien monté les dossiers de volume, exécutez la commande suivante :

    Dir C:\

Les dossiers montés devraient apparaître dans la liste des résultats.

## Étape 5 : Créer les dossiers de base de données

Ensuite, créez les répertoires de base de données sous le chemin d'accès racine C:\\ExchangeDatabases. Cet exemple montre comment créer des répertoires pour une configuration de stockage avec 4 bases de données sur chaque volume.
```
    md c:\ExchangeDatabases\db001
```
```
    md c:\ExchangeDatabases\db002
```
```
    md c:\ExchangeDatabases\db003
```
```
    md c:\ExchangeDatabases\db004
```

## Comment savoir si cette étape a fonctionné ?

Pour vérifier que vous avez bien monté les dossiers de base de données, exécutez la commande suivante :

    Dir C:\ExchangeDatabases

Les répertoires créés devraient apparaître dans la liste des résultats.

## Étape 6 : Créer les points de montage pour les bases de données

Créez les points de montage pour chaque base de données et reliez le point de montage au bon volume. Par exemple, le dossier monté pour db001 devra être sur C:\\ExchangeDatabases\\db001. Pour ce faire, vous pouvez utiliser diskmgmt.msc ou mountvol.exe. Cet exemple montre comment monter db001 sur C:\\ExchangeDatabases\\db001 à l'aide de mountvol.exe.

    Mountvol.exe c:\ExchangeDatabases\db001 \\?\Volume (GUID)

## Comment savoir si cette étape a fonctionné ?

Pour vérifier que vous avez bien créé les points de montage pour la base de données, exécutez la commande suivante :

    Mountvol.exe C:\ExchangeDatabases\db001 /L

Le volume monté doit apparaître dans la liste des points de montage.

## Étape 7 : Créez la structure de répertoires de base de données

Créez ensuite deux répertoires sous les dossiers créés à l'étape 5, un pour chaque base de données et un pour chaque flux de journal de la base de données qui sera stocké sur le même volume. Vous devez utiliser le format suivant pour votre structure de répertoires :

C:\\\< *DatabaseFolderName*\>\\*DatabaseName*\\\<*DatabaseName*\>.db

C:\\\< *DatabaseFolderName*\>\\*DatabaseName*\\\<*DatabaseName*\>.log

Cet exemple montre comment créer des répertoires pour 4 bases de données qui seront stockées sur le volume 1 :
```
    md c:\ExchangeDatabases\db001\db001.db
```
```
    md c:\ExchangeDatabases\db001\db001.log
```
```
    md c:\ExchangeDatabases\db002\db002.db
```
```
    md c:\ExchangeDatabases\db002\db002.log
```
```
    md c:\ExchangeDatabases\db003\db003.db
```
```
    md c:\ExchangeDatabases\db003\db003.log
```
```
    md c:\ExchangeDatabases\db004\db004.db
```
```
    md c:\ExchangeDatabases\db004\db004.log
```

Répétez les commandes précédentes pour les bases de données sur chaque volume.

## Comment savoir si cette étape a fonctionné ?

Pour vérifier que vous avez bien créé la structure de répertoires de base de données, exécutez la commande suivante :

    Dir C:\ExchangeDatabases /s

Les répertoires créés devraient apparaître dans la liste des résultats.

## Étape 8 : Créez des bases de données

Créez des bases de données avec les chemins d'accès de base de données et de journal configurés avec les dossiers appropriés. Cet exemple montre comment créer une base de données stockée dans le répertoire et la structure de points de montage nouvellement créés.

    New-MailboxDatabase -Name db001 -Server MBX1 -LogFolderPath C:\ExchangeDatabases\db001\db001.log -EdbFilePath C:\ExchangeDatabases\db001\db001.db\db001.edb

## Comment savoir si cette étape a fonctionné ?

Pour vérifier que vous avez bien créé les bases de données dans le dossier approprié, exécutez la commande suivante :

    Get-MailboxDatabase db001 | Format List *path*

Les propriétés de la base de données renvoyées doivent indiquer que le fichier de la base de données et les fichiers journaux sont stockés dans les fichiers susmentionnés.

## Comment savoir si cette tâche a fonctionné ?

Pour vérifier que vous avez bien configuré AutoReseed pour un groupe de disponibilité de base de données, procédez comme suit :

1.  Exécutez la commande suivante pour vérifier que le groupe de disponibilité de base de données est configuré correctement :
    
        Get-DatabaseAvailabilityGroup DAG1 | Format-List *auto*

2.  Exécutez la commande suivante pour vérifier que la structure de répertoires est configurée correctement (vous trouverez ci-dessous les chemins d'accès par défaut ; si nécessaire, remplacez les chemins d'accès par ceux que vous utilisez).
    ```
        Dir c:\ExchangeDatabases /s
    ```
    ```
        Dir c:\ExchangeVolumes /s
    ```    

