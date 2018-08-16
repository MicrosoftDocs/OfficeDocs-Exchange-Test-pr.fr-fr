---
title: 'Copies de bases de données de boîtes aux lettres: Exchange 2013 Help'
TOCTitle: Copies de bases de données de boîtes aux lettres
ms:assetid: ce748bca-3e24-493b-b9e6-153157bffd6a
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dd979802(v=EXCHG.150)
ms:contentKeyID: 50479194
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Copies de bases de données de boîtes aux lettres

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2015-04-07_

Microsoft Exchange Server 2013 exploite le concept de mobilité des bases de données, c’est-à-dire la gestion par Exchange des basculements au niveau base de données. La mobilité de base de données permet de déconnecter des bases de données de leur serveur, de prendre en charge jusqu’à 16 copies d’une base de données individuelle et de fournir une expérience native pour l’ajout de copies de bases de données à une base de données.

## Principales caractéristiques

Les principales caractéristiques des copies de bases de données sont les suivantes :

  - Il est possible de créer jusqu’à 16 copies d’une base de données de boîtes aux lettres Exchange 2013 sur plusieurs serveurs de boîtes aux lettres, à condition que les serveurs soient réunis dans un groupe de disponibilité de base de données, qui représente une limite pour la réplication continue. Les bases de données de boîtes aux lettres Exchange 2013 ne peuvent être répliquées que sur d’autres serveurs de boîtes aux lettres Exchange 2013 appartenant au même groupe de disponibilité de base de données. Vous ne pouvez ni répliquer une base de données se trouvant en dehors d’un groupe de disponibilité de base de données ni répliquer une base de données de boîtes aux lettres Exchange 2013 sur un serveur exécutant Exchange 2010 ou une version antérieure. Pour obtenir des informations détaillées sur les groupes de disponibilité de base de données, voir [Groupe de disponibilité de base de données (DAG)](database-availability-groups-dags-exchange-2013-help.md).

  - Tous les serveurs de boîtes aux lettres d’un groupe de disponibilité de base de données doivent se trouver dans le même domaine Active Directory.

  - Les copies de bases de données de boîte aux lettres prennent en charge les concepts de délai d’attente de relecture et de délai d’attente de troncation. Une planification appropriée doit être effectuée avant d’activer ces fonctionnalités.

  - Toutes les copies de bases de données peuvent être sauvegardées à l’aide d’une application de sauvegarde basée sur un service de cliché instantané des volumes (VSS) qui reconnaît Exchange.

  - Les copies de bases de données peuvent être uniquement créées sur des serveurs de boîtes aux lettres qui n’hébergent pas la copie active d’une base de données. Vous ne pouvez pas non plus créer deux copies de la même base de données sur le même serveur.

  - Toutes les copies d’une base de données utilisent le même chemin sur chaque serveur hébergeant une copie. Le chemin de la base de données et celui du fichier journal d’une copie de base de données sur chaque serveur de boîtes aux lettres ne doivent pas entrer en conflit avec d’autres chemins de base de données.

  - Les copies de base de données peuvent être créées sur le même site Active Directory ou des sites différents et sur le même sous-réseau ou des sous-réseaux différents.

  - Les copies de bases de données ne sont pas prises en charge par les serveurs de boîtes aux lettres dont la latence du parcours circulaire du réseau est supérieure à 500 millisecondes (ms).

## Copies de bases de données de boîtes aux lettres

Vous pouvez créer une copie de base de données de boîtes aux lettres à tout moment. Les copies de bases de données de boîtes aux lettres peuvent être réparties sur des serveurs de boîtes aux lettres de manière souple et granulaire.

Vous pouvez créer une copie de base de données de boîtes aux lettres à l’aide de l’Assistant **Ajouter une copie de base de données de boîte aux lettres** dans le Centre d’administration Exchange ou à l’aide de la cmdlet **Add-MailboxDatabaseCopy** de l’environnement de ligne de commande Exchange Management Shell.

Lorsque vous créez une copie de base de données de boîtes aux lettres, spécifiez les paramètres suivants :

  - *Identity*   Ce paramètre spécifie le nom de la base de données en cours de copie. Les noms de base de données doivent être uniques au sein de l’organisation Exchange.

  - *MailboxServer*   Ce paramètre spécifie le nom du serveur de boîtes aux lettres qui hébergera la copie de la base de données. Ce serveur doit être membre du même groupe de disponibilité de base de données et ne doit pas déjà héberger de copie de base de données.

Vous pouvez également spécifier les paramètres suivants :

  - *ActivationPreference*    Ce paramètre spécifie le numéro de préférence d’activation, qui est utilisé dans le cadre du processus de sélection de la meilleure copie par le gestionnaire Active Manager. Ce numéro sert également à la redistribution des bases de données de boîtes aux lettres actives dans le DAG à l’aide du script RedistributeActiveDatabases.ps1. La valeur de la préférence d’activation est un nombre supérieur ou égal à 1, où 1 correspond à l’ordre de préférence le plus élevé. Le numéro de position ne peut pas être supérieur au nombre de copies de base de données de boîtes aux lettres.

  - *ReplayLagTime *  Ce paramètre spécifie le temps d’attente du Service de réplication Microsoft Exchange avant la relecture des fichiers journaux copiés dans la copie de la base de données. Le format de ce paramètre est (jours.heures:minutes:secondes). La valeur par défaut est 0 seconde. La valeur maximale autorisée est 14 jours. Le paramètre minimal autorisé est 0 seconde. Si la valeur du retard de relecture est configurée sur 0, le retard de relecture du journal est désactivé.

  - *TruncationLagTime*   Ce paramètre spécifie le temps d’attente du service de réplication Microsoft Exchange avant la troncation des fichiers journaux qui ont été relus dans une copie de la base de données. Le décompte commence une fois le dernier journal relu dans la copie de la base de données. Le format de ce paramètre est (jours.heures:minutes:secondes). La valeur par défaut est 0 seconde. La valeur maximale autorisée est 14 jours. Le paramètre minimal autorisé est 0 seconde. Si la valeur du retard de troncation est configurée sur 0, le retard de troncation du journal est désactivé.

  - *SeedingPostponed*    Ce paramètre spécifie que la tâche ne doit pas automatiquement amorcer la copie de la base de données sur le serveur de boîtes aux lettres spécifié. Cette option est en général utilisée lorsque vous avez l’intention d’amorcer une nouvelle copie de base de données de boîtes aux lettres à l’aide d’une copie passive existante d’une base de données (par exemple, si vous ajoutez une deuxième copie d’une base de données spécifique à un emplacement distant). Lorsque vous utilisez ce paramètre, vous devez manuellement amorcer la copie de la base de données à l’aide de la cmdlet [Update-MailboxDatabaseCopy](https://technet.microsoft.com/fr-fr/library/dd335201\(v=exchg.150\)).

Pour plus d’informations sur la création, l’utilisation et la gestion de copies de base de données, voir [Gestion des copies de base de données de boîtes aux lettres](managing-mailbox-database-copies-exchange-2013-help.md).

