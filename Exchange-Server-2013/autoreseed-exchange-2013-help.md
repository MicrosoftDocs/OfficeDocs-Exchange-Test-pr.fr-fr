---
title: 'AutoReseed: Exchange 2013 Help'
TOCTitle: AutoReseed
ms:assetid: 61f9a8be-070e-4c62-b505-52644fcff0c5
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dn789209(v=EXCHG.150)
ms:contentKeyID: 62523885
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# AutoReseed

 

_**Sapplique à :**Exchange Server 2013 SP1_

_**Dernière rubrique modifiée :**2015-03-09_

La fonctionnalité de réamorçage automatique, AutoReseed, remplace une action généralement initiée par l’administrateur en cas de défaillance d’un disque, d’endommagement d’une base de données ou de tout autre problème nécessitant le réamorçage d’une copie de base de données. La fonctionnalité AutoReseed permet de restaurer automatiquement la redondance de base de données après une défaillance de disque par le biais de disques de rechange qui ont été configurés sur le système.

## Vue d’ensemble de la fonctionnalité AutoReseed

Dans une configuration AutoReseed, une structure de présentation du stockage standardisée est utilisée et l’administrateur choisit le point de départ. La fonctionnalité AutoReseed permet de restaurer la redondance dès que possible après une défaillance de disque. Il nécessite le pré-mappage d’un ensemble de volumes (dont des volumes de rechange) et de bases de données via des points de montage. En cas de défaillance de disque, si le disque n’est plus disponible pour le système d’exploitation, ou n’est plus accessible en écriture, un volume de rechange est alloué par le système et les copies de base de données concernées sont automatiquement réamorcées.

1.  Le service de réplication Microsoft Exchange recherche régulièrement les copies qui ont l’état FailedAndSuspended. Si toutes les copies de base de données sur un volume configuré pour AutoReseed sont dans un état FailedandSuspended pendant 15 minutes consécutives, le workflow AutoReseed est lancé.

2.  AutoReseed va tenter de reprendre les copies ayant échoué et celles suspendues jusqu’à trois fois, avec un intervalle de 5 minutes entre chaque tentative. Parfois, après la reprise d’une copie de base de données FailedandSuspended, cette dernière reste en état d’échec. Cela peut se produire pour toutes sortes de raisons. Cette étape est donc conçue pour traiter ces cas. AutoReseed suspend automatiquement une copie de base de données en échec depuis 10 minutes consécutives afin de maintenir l’exécution du workflow. Si les actions de suspension et de reprise n’aboutissent pas à une copie de base de données saine, le workflow continue.

3.  Lorsqu’il trouve une copie avec cet état, il effectue certaines vérifications préalables. Par exemple, il vérifie qu’un disque de rechange est disponible, que la base de données et ses fichiers journaux sont configurés sur le même volume et dans les emplacements adaptés correspondant aux conventions d’affectation de noms obligatoires.

4.  Si les vérifications préalables ont réussi, la fonctionnalité Disk Reclaimer du service de réplication Microsoft Exchange alloue, remappe et formate un disque de rechange. AutoReseed tentera d’attribuer un volume libre jusqu’à 5 fois, avec un intervalle d’une heure entre chaque tentative.

5.  Une fois qu’un volume libre a été attribué, AutoReseed effectuera une opération InPlaceSeed à l’aide du commutateur d’armorçage SafeDeleteExistingFiles. Toutes les bases de données qui se trouvaient sur le disque concerné sont réamorcées en utilisant la copie active de la base de données comme source d’amorçage.

6.  Une fois l’amorçage terminé, le service de réplication Microsoft Exchange vérifie que la copie nouvellement amorcée est intègre.

Une fois toutes les nouvelles tentatives épuisées, le workflow s’arrête. Après 3 jours, si la copie de base de données a toujours l’état FailedandSuspended, l’état du workflow est réinitialisé et celui-ci redémarre à l’étape 1. Ce comportement de réinitialisation/reprise est utile (et intentionnel), car le remplacement d’un disque ou d’un contrôleur défectueux peut prendre plusieurs jours.

À ce stade, si la défaillance provenait du disque, l’intervention manuelle d’un opérateur ou d’un administrateur était requise pour supprimer et remplacer le disque défectueux et reconfigurer le disque de remplacement en tant que disque de rechange.

Pour configurer la fonctionnalité AutoReseed, trois propriétés du DAG doivent être utilisées. Deux de ces propriétés font référence aux deux points de montage en cours d’utilisation. Exchange 2013 tire parti du fait que Windows Server autorise plusieurs points de montage par volume. La propriété *AutoDagVolumesRootFolderPath* fait référence au point de montage qui contient tous les volumes disponibles. Il s’agit de tous les volumes qui hébergent les bases de données et les volumes de rechange. La propriété *AutoDagDatabasesRootFolderPath* fait référence au point de montage qui contient les bases de données. Une troisième propriété de DAG, *AutoDagDatabaseCopiesPerVolume*, permet de configurer le nombre de copies de base de données par volume.

Vous trouverez ci-dessous un exemple de configuration de la fonctionnalité AutoReseed.

**Exemple de configuration de la fonctionnalité AutoReseed**

![Exemple de configuration de réamorçage automatique](images/Dn789209.e3af7306-f5b4-4ec4-9ccf-222ec452699b(EXCHG.150).gif "Exemple de configuration de réamorçage automatique")

Dans cet exemple, il y a trois volumes : deux contiendront des bases de données (VOL1 et VOL2) et l’autre est un volume de rechange vide formaté (VOL3).

Pour configurer la fonctionnalité AutoReseed :

1.  Les trois volumes sont montés sous un point de montage unique. Dans cet exemple, le point de montage C:\\ExchVols est utilisé. Il s’agit du répertoire utilisé pour le stockage des bases de données Exchange.

2.  Le répertoire racine des bases de données de boîtes aux lettres est monté comme autre point de montage. Dans cet exemple, le point de montage C:\\ExchDBs est utilisé. Ensuite, une structure de répertoires est mise en place afin de créer le répertoire parent de la base de données et, sous le répertoire parent, deux sous-répertoires sont établis : un pour le fichier de base de données et un autre pour les fichiers journaux.

3.  Des bases de données sont créées. L’exemple ci-dessus illustre une conception simple utilisant une seule base de données par volume. Ainsi, sur VOL1, il existe trois répertoires : le répertoire parent et deux sous-répertoires (un pour le fichier de base de données de MDB1 et un autre pour ses journaux). Même s’il n’est pas représenté dans l’illustration, VOL2 comporte également trois répertoires : le répertoire parent et, sous ce dernier, un répertoire pour le fichier de base de données de MDB2, et un autre pour ses fichiers journaux.

Dans cette configuration, si MDB1 ou MDB2 venaient à rencontrer une défaillance, une copie de la base de données défectueuse serait automatiquement réamorcée sur VOL3.

## Fonctionnalité Disk Reclaimer

Le composant AutoReseed qui alloue et formate les disques de rechange est appelé *Disk Reclaimer*. Le composant Disk Reclaimer formate automatiquement les disques de rechange en prévision du réamorçage automatique à différents intervalles, en fonction de l’état du disque. Pour que le composant Disk Reclaimer puisse formater un disque, certaines conditions doivent être remplies :

  - Le composant Disk Reclaimer doit être activé. Il est activé par défaut, mais il peut être désactivé à l’aide de la cmdlet [Set-DatabaseAvailabilityGroup](https://technet.microsoft.com/fr-fr/library/dd297934\(v=exchg.150\)).

  - Le volume doit disposer d’un point de montage dans le chemin d’accès aux volumes racine (par défaut, C:\\ExchangeVolumes).

  - Le volume ne doit disposer d’aucun point de montage dans le chemin d’accès aux volumes de base de données (par défaut, C:\\ExchangeDatabases).

  - Si le volume contient des fichiers, aucun de ces fichiers ne doit avoir été touché au cours des dernières 24 heures.

En plus des conditions ci-dessus, le composant Disk Reclaimer ne peut tenter de formater un volume donné qu’une seule fois par jour. Le tableau suivant décrit le comportement de formatage du composant Disk Reclaimer.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>État du disque et des copies de base de données</th>
<th>Intervalle de formatage</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Le disque n’est pas formaté, est formaté mais vide ou est formaté mais contient des fichiers qui n’ont pas été touchés pendant 24 heures et il existe des copies de bases de données actives et intègres dans le site Active Directory local qui peuvent être utilisées comme source d’amorçage.</p></td>
<td><p>1 jour</p></td>
</tr>
<tr class="even">
<td><p>Le disque n’est pas formaté, est formaté mais vide ou est formaté mais contient des fichiers qui n’ont pas été touchés pendant 24 heures mais il existe des copies de bases de données actives non intègres dans le site Active Directory local qui peuvent être utilisées comme source d’amorçage.</p></td>
<td><p>2 jours</p></td>
</tr>
<tr class="odd">
<td><p>Le disque n’est pas formaté, est formaté mais vide ou est formaté mais contient des fichiers qui n’ont pas été touchés pendant 24 heures et il existe des copies de bases de données actives et intègres dans le site Active Directory local qui peuvent être utilisées comme source d’amorçage, mais il existe des fichiers inconnus autres que le fichier de base de données (fichier EDB) et les fichiers journaux.</p></td>
<td><p>2 semaines</p></td>
</tr>
<tr class="even">
<td><p>Le disque n’est pas formaté, est formaté mais vide ou est formaté mais contient des fichiers qui n’ont pas été touchés pendant 24 heures et il existe des copies de bases de données actives et intègres dans le site Active Directory local qui peuvent être utilisées comme source d’amorçage, mais il existe également un ou plusieurs fichiers de base de données (fichiers EDB) pour les bases de données qui ne sont pas présentes dans Active Directory.</p></td>
<td><p>2 semaines</p></td>
</tr>
</tbody>
</table>

