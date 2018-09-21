---
title: 'Surveiller les groupes de dispo. des bases de données: Exchange 2013 Help'
TOCTitle: Surveillance des groupes de disponibilité des bases de données
ms:assetid: f5bdfd6e-e93c-4d96-8bc2-548750d51930
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dd351258(v=EXCHG.150)
ms:contentKeyID: 50479562
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Surveillance des groupes de disponibilité des bases de données

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2015-03-09_

Vous pouvez utiliser les informations de cette rubrique afin de surveiller l’intégrité et l’état des copies de base de données de boîtes aux lettres pour les groupes de disponibilité de base de données (DAG), pour recueillir des informations de diagnostic et pour configurer le seuil de surveillance d’espace disque faible.

## Cmdlet Get-MailboxDatabaseCopyStatus

Vous pouvez utiliser la cmdlet [Get-MailboxDatabaseCopyStatus](https://technet.microsoft.com/fr-fr/library/dd298044\(v=exchg.150\)) pour afficher des informations sur l’état des copies de la base de données de boîtes aux lettres. Cette cmdlet vous permet de consulter des informations sur toutes les copies d’une base de données spécifique, des informations sur une copie spécifique d’une base de données installée sur un serveur donné ou des informations sur toutes les copies de base de données installées sur un serveur. Le tableau suivant décrit les valeurs possibles de l’état d’une copie de base de données de boîtes aux lettres.

### État de copie de la base de données

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>État de copie de la base de données</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Failed</p></td>
<td><p>La copie de la base de données de boîtes aux lettres possède l’état Échec car elle n’est pas suspendue et n’est pas capable de copier ou de relire les fichiers journaux. Lorsque la copie est définie sur l’état Échec et qu’elle n’est pas suspendue, le système vérifie régulièrement si le problème à l’origine de cet état a été résolu. Si le système détecte que le problème est résolu, et à condition qu’il n’y ait aucune autre difficulté, l’état de copie passe automatiquement à Sain.</p></td>
</tr>
<tr class="even">
<td><p>Seeding</p></td>
<td><p>La copie de la base de données de boîtes aux lettres ou l’index de contenu est en cours d’amorçage, ou tous deux le sont. Après l’exécution réussie de l’amorçage, l’état de la copie doit passer à Initialisation en cours.</p></td>
</tr>
<tr class="odd">
<td><p>SeedingSource</p></td>
<td><p>La copie de la base de données de boîtes aux lettres est utilisée comme élément source pour une opération d’amorçage de copie de base de données.</p></td>
</tr>
<tr class="even">
<td><p>Suspended</p></td>
<td><p>La copie de la base de données de boîtes aux lettres possède l’état Suspendu car un administrateur a manuellement suspendu la copie de la base de données en exécutant la cmdlet <strong>Suspend-MailboxDatabaseCopy</strong>.</p></td>
</tr>
<tr class="odd">
<td><p>Healthy</p></td>
<td><p>La copie de la base de données de boîtes aux lettres est en train de copier et de relire les fichiers journaux ou a déjà effectué cette opération.</p></td>
</tr>
<tr class="even">
<td><p>ServiceDown</p></td>
<td><p>Le service de réplication Microsoft Exchange n’est pas disponible ou est en cours d’exécution sur le serveur qui héberge la copie de la base de données de boîtes aux lettres.</p></td>
</tr>
<tr class="odd">
<td><p>Initializing</p></td>
<td><p>L’état de la copie de la base de données de boîtes aux lettres est « Initialisation en cours » si une copie de base de données a été créée, lorsque le service de réplication d’Microsoft Exchange est en cours de démarrage ou vient juste de démarrer, et pendant le passage de l’état Suspendu, ServiceDown, Échec, Amorçage ou SinglePageRestore à un autre état. Lorsqu’elle est définie sur l’état d’initialisation, le système vérifie que la base de données et l’état du flux de journal sont cohérents. Dans la plupart des cas, l’état de la copie est défini sur Initialisation en cours pendant environ 15 secondes, mais dans tous les cas, il ne doit pas rester défini sur cet état pendant plus de 30 secondes.</p></td>
</tr>
<tr class="even">
<td><p>Resynchronizing</p></td>
<td><p>La copie de la base de données de boîtes aux lettres et ses fichiers journaux sont comparés avec la copie active de la base de données pour vous permettre de rechercher d’éventuelles divergences entre les deux copies. L’état de la copie reste tel quel tant que les divergences trouvées n’ont pas été résolues.</p></td>
</tr>
<tr class="odd">
<td><p>Mounted</p></td>
<td><p>La copie active est en ligne et accepte les connexions des clients. Seule la copie active de la base de données de boîtes aux lettres peut posséder l’état Monté.</p></td>
</tr>
<tr class="even">
<td><p>Dismounted</p></td>
<td><p>La copie active est hors ligne et n’accepte pas les connexions des clients. Seule la copie active de la base de données de boîtes aux lettres peut être définie sur Démontée.</p></td>
</tr>
<tr class="odd">
<td><p>Mounting</p></td>
<td><p>La copie active va être en ligne mais n’accepte pas encore les connexions des clients. Seule la copie active de la base de données de boîtes aux lettres peut posséder l’état Montage.</p></td>
</tr>
<tr class="even">
<td><p>Dismounting</p></td>
<td><p>La copie active va passer en mode hors connexion et met fin aux connexions des clients. Seule la copie active de la base de données de boîtes aux lettres peut posséder l’état Démontage.</p></td>
</tr>
<tr class="odd">
<td><p>DisconnectedAndHealthy</p></td>
<td><p>La copie de la base de données de boîtes aux lettres n’est plus connectée à la copie active de la base de données et possédait l’état Sain lorsque la perte de connexion s’est produite. Cet état représente la copie de la base de données par rapport à la connectivité de sa copie de base de données source. Il peut être signalé lors des défaillances réseau d’un groupe de disponibilité de base de données entre la copie source et la copie cible.</p></td>
</tr>
<tr class="even">
<td><p>DisconnectedAndResynchronizing</p></td>
<td><p>La copie de la base de données de boîtes aux lettres n’est plus connectée à la copie active de la base de données et possédait l’état Resynchronisation lorsque la perte de connexion s’est produite. Cet état représente la copie de la base de données par rapport à la connectivité de sa copie de base de données source. Il peut être signalé lors des défaillances réseau d’un groupe de disponibilité de base de données entre la copie source et la copie cible.</p></td>
</tr>
<tr class="odd">
<td><p>FailedAndSuspended</p></td>
<td><p>Les états Échec et Suspendu ont été définis simultanément par le système en raison de la détection d’une défaillance et parce que sa résolution nécessite l’intervention d’un administrateur. Cela se produit, par exemple, lorsque le système détecte une divergence irrécupérable entre la base de données de boîtes aux lettres active et une copie de la base de données. Contrairement à l’état Échec, le système ne vérifie pas régulièrement si le problème a été résolu et si une récupération automatique a lieu. L’intervention d’un administrateur est indispensable pour corriger la cause sous-jacente de la défaillance afin que la copie de la base de données puisse passer à un état sain.</p></td>
</tr>
<tr class="even">
<td><p>SinglePageRestore</p></td>
<td><p>Cet état indique qu’une opération de restauration en page unique a lieu sur la copie de la base de données de boîtes aux lettres.</p></td>
</tr>
</tbody>
</table>


La cmdlet **Get-MailboxDatabaseCopyStatus** renvoie également des informations sur les réseaux de réplication en cours d’utilisation, y compris *IncomingLogCopyingNetwork*, qui est renvoyé pour des copies de bases de données passives et *OutgoingConnections*, qui est renvoyé pour les bases de données actives comportant plus d’une copie, ainsi que toute copie de base de données utilisée en tant que source pour une opération d’amorçage de base de données. Des informations de connexion sortante sont fournies pour les copies de base de données qui se trouvent dans la réplication en mode fichier. Des informations de connexion sortante sont fournies pour les copies de base de données qui se trouvent dans la réplication en mode blocage.

## Get-MailboxDatabaseCopyStatus - Exemples

Les exemples suivants utilisent la cmdlet **Get-MailboxDatabaseCopyStatus**. Chaque exemple transfère les résultats à la cmdlet **Format-List** afin qu’ils soient affichés sous la forme d’une liste.

Cet exemple renvoie les informations relatives à l’état de toutes les copies de la base de données nommée DB2.

```powershell
Get-MailboxDatabaseCopyStatus -Identity DB2 | Format-List
```

Cet exemple renvoie l’état de toutes les copies de base de données sur le serveur de boîtes aux lettres nommé MBX2.

```powershell
Get-MailboxDatabaseCopyStatus -Server MBX2 | Format-List
```

Cet exemple renvoie l’état de toutes les copies de base de données sur le serveur de boîtes aux lettres local.

```powershell
Get-MailboxDatabaseCopyStatus -Local | Format-List
```

Pour plus d’informations sur l’utilisation de la cmdlet **Get-MailboxDatabaseCopyStatus**, voir [Get-MailboxDatabaseCopyStatus](https://technet.microsoft.com/fr-fr/library/dd298044\(v=exchg.150\)).

## Cmdlet Test-ReplicationHealth

Vous pouvez utiliser la cmdlet [Test-ReplicationHealth](https://technet.microsoft.com/fr-fr/library/bb691314\(v=exchg.150\)) pour afficher des informations sur l’état de réplication continue des copies de la base de données de boîtes aux lettres. Cette cmdlet permet de vérifier tous les aspects de l’état de réplication et de relecture afin d’offrir une vue d’ensemble complète d’un serveur de boîtes aux lettres spécifique dans un groupe de disponibilité de base de données.

La cmdlet **Test-ReplicationHealth** a été conçue pour l’analyse proactive de la réplication continue et du pipeline de la réplication continue, la disponibilité d’Active Manager, l’état du service de cluster sous-jacent, le quorum et les composants réseau. Elle peut être exécutée localement ou à distance sur n’importe quel serveur de boîtes aux lettres dans un groupe de disponibilité de base de données. La cmdlet **Test-ReplicationHealth** exécute les tests répertoriés dans le tableau suivant.

### Tests de la cmdlet Test-ReplicationHealth

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Nom du test</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>ClusterService</p></td>
<td><p>Vérifie que le service de cluster est en cours d’exécution et accessible sur le membre du DAG spécifié ou, si aucun membre de DAG n’est indiqué, sur le serveur local.</p></td>
</tr>
<tr class="even">
<td><p>ReplayService</p></td>
<td><p>Vérifie que le service de réplication Microsoft Exchange est en cours d’exécution et accessible sur le membre du DAG spécifié ou, si aucun membre de DAG n’est indiqué, sur le serveur local.</p></td>
</tr>
<tr class="odd">
<td><p>ActiveManager</p></td>
<td><p>Vérifie que le rôle de l’instance d’Active Manager en cours d’exécution sur le membre du groupe de disponibilité de base de données (DAG) spécifié, ou si aucun membre de groupe de disponibilité de base de données (DAG) n’a été spécifié, le serveur local, est valide (principal, secondaire ou autonome).</p></td>
</tr>
<tr class="even">
<td><p>TasksRpcListener</p></td>
<td><p>Vérifie que le serveur d’appel de procédure distante (RPC) des tâches est en cours d’exécution et accessible sur le membre du DAG spécifié ou, si aucun membre de DAG n’est indiqué, sur le serveur local.</p></td>
</tr>
<tr class="odd">
<td><p>TcpListener</p></td>
<td><p>Vérifie que le port d’écoute TCP de copie du journal est en cours d’exécution et accessible sur le membre du DAG spécifié ou, si aucun membre de DAG n’est indiqué, sur le serveur local.</p></td>
</tr>
<tr class="even">
<td><p>ServerLocatorService</p></td>
<td><p>Vérifie les processus client/serveur Active Manager sur les membres du DAG et sur le serveur d’accès au client qui effectuent des recherches dans Active Directory et Active Manager afin de déterminer où la base de données de boîtes aux lettres d’un utilisateur est active.</p></td>
</tr>
<tr class="odd">
<td><p>DagMembersUp</p></td>
<td><p>Vérifie que tous les membres du DAG sont disponibles, en cours d’exécution et accessibles.</p></td>
</tr>
<tr class="even">
<td><p>ClusterNetwork</p></td>
<td><p>Vérifie que tous les réseaux gérés par des clusters sur le membre du groupe de disponibilité de base de données (DAG) spécifié, ou si aucun membre du groupe de disponibilité de base de données (DAG) n’est spécifié, le serveur local, sont disponibles.</p></td>
</tr>
<tr class="odd">
<td><p>QuorumGroup</p></td>
<td><p>Vérifie que le groupe de clusters par défaut (groupe quorum) est sain et en ligne.</p></td>
</tr>
<tr class="even">
<td><p>FileShareQuorum</p></td>
<td><p>Vérifie que le serveur témoin, le répertoire témoin et le partage configurés pour le DAG sont accessibles.</p></td>
</tr>
<tr class="odd">
<td><p>DatabaseRedundancy</p></td>
<td><p>Vérifie l’existence d’au moins une copie saine disponible des bases de données sur le membre du DAG spécifié ou, si aucun membre de DAG n’est indiqué, sur le serveur local.</p></td>
</tr>
<tr class="even">
<td><p>DatabaseAvailability</p></td>
<td><p>Vérifie que la disponibilité des bases de données est suffisante sur le membre du DAG spécifié ou, si aucun membre de DAG n’est indiqué, sur le serveur local.</p></td>
</tr>
<tr class="odd">
<td><p>DBCopySuspended</p></td>
<td><p>Vérifie si des copies de la base de données de boîtes aux lettres ont l’état Suspendu sur le membre de DAG spécifié ou, si aucun membre de DAG n’est indiqué, sur le serveur local.</p></td>
</tr>
<tr class="even">
<td><p>DBCopyFailed</p></td>
<td><p>Vérifie si des copies de la base de données de boîtes aux lettres ont l’état Échec sur le membre de DAG spécifié ou, si aucun membre de DAG n’est indiqué, sur le serveur local.</p></td>
</tr>
<tr class="odd">
<td><p>DBInitializing</p></td>
<td><p>Vérifie si des copies de la base de données de boîtes aux lettres ont l’état Initialisation en cours sur le membre de DAG spécifié ou, si aucun membre de DAG n’est indiqué, sur le serveur local.</p></td>
</tr>
<tr class="even">
<td><p>DBDisconnected</p></td>
<td><p>Vérifie si des copies de la base de données de boîtes aux lettres ont l’état Déconnecté sur le membre de DAG spécifié ou, si aucun membre de DAG n’est indiqué, sur le serveur local.</p></td>
</tr>
<tr class="odd">
<td><p>DBLogCopyKeepingUp</p></td>
<td><p>Vérifie que la copie du journal et l’inspection par les copies passives des bases de données sur le membre du groupe de disponibilité de base de données (DAG) spécifié, ou si aucun membre du groupe de disponibilité de base de données (DAG) n’est spécifié, sur le serveur local, sont en mesure de suivre la cadence de l’activité de génération du journal sur la copie active.</p></td>
</tr>
<tr class="even">
<td><p>DBLogReplayKeepingUp</p></td>
<td><p>Vérifie que l’activité de relecture pour les copies passives de bases de données sur le membre du groupe de disponibilité de base de données (DAG) spécifié, ou si aucun membre du groupe de disponibilité de base de données (DAG) n’est spécifié, sur le serveur local, est en mesure de suivre la cadence de l’activité de copie du journal et d’inspection.</p></td>
</tr>
</tbody>
</table>


## Test-ReplicationHealth - Exemple

Cet exemple utilise la cmdlet **Test-ReplicationHealth** pour tester l’intégrité de la réplication pour le serveur de boîtes aux lettres MBX1.

```powershell
Test-ReplicationHealth -Identity MBX1
```

## Journalisation des événements du canal Crimson

Windows comprend deux catégories de journaux d’événements : les journaux Windows et les journaux des applications et des services. La catégorie de journaux Windows inclut les journaux d’événements disponibles dans les versions précédentes de Windows : les journaux des événements d’application, de sécurité et système. Elle inclut également deux nouveaux journaux : le journal d’installation et le journal des événements transmis (ForwardedEvents). Les journaux Windows sont conçus pour le stockage d’événements appartenant à des applications héritées et d’événements qui s’appliquent à la totalité du système.

Les journaux des applications et des services sont une nouvelle catégorie de journaux d’événements. Ces journaux stockent les événements d’une application ou d’un composant unique au lieu des événements qui concernent le système entier. Cette nouvelle catégorie de journaux d’événements est désignée par les termes « canal crimson d’une application ».

La catégorie de journaux des applications et services inclut quatre sous-types : les journaux d’administration, opérationnels, d’analyse et de débogage. Les événements des journaux d’administration sont particulièrement utiles si vous utilisez des enregistrements du journal d’événements pour résoudre les problèmes. Les événements contenus dans le journal d’administration doivent vous indiquer comment répondre aux événements. Les événements du journal opérationnel sont eux aussi utiles, mais ils nécessitent une interprétation plus détaillée. Les journaux d’administration et de débogage ne sont pas aussi conviviaux. Les journaux d’analyse (masqués et désactivés par défaut) stockent des événements qui effectuent le suivi d’un problème. Ils contiennent généralement un grand nombre d’événements. Les journaux de débogage sont utilisés par les développeurs lors du débogage d’applications.

Exchange 2013 enregistre les événements dans les canaux crimson, dans la zone des journaux des applications et services. Vous pouvez afficher ces canaux en procédant comme suit :

1.  Ouvrez l’Observateur d’événements.

2.  Dans l’arborescence de la console, accédez à **Journaux des applications et des services** \> **Microsoft** \> **Exchange**.

3.  Sous **Exchange**, sélectionnez un canal pourpre, comme **HighAvailability** ou **MailboxDatabaseFailureItems**, pour afficher les événements liés aux groupes de disponibilité de base de données ou à la copie de base de données. Vous pouvez également choisir **ActiveMontoring** ou **ManagedAvailability** pour afficher les événements liés à la disponibilité gérée.

Le canal HighAvailability contient des événements liés au démarrage et à la fermeture du service de réplication Microsoft Exchange ainsi que les divers composants qui s’exécutent au sein de ce service Microsoft Exchange, comme Active Manager, l’API de réplication synchrone tiers, le serveur de tâches RPC, le port d’écoute TCP et l’enregistreur VSS (Service de cliché instantané de volumes). Le canal HighAvailability permet également à Active Manager de journaliser les événements associés aux événements d’analyse de rôle et d’action de base de données Active Manager, comme le montage de la base de données et la troncation du journal, et d’enregistrer des événements associés au cluster sous-jacent du DAG.

Le canal MailboxDatabaseFailureItems sert à journaliser les événements associés aux défaillances qui affectent une base de données de boîte aux lettres répliquées.

Le canal ActiveMonitoring contient les événements de définition et de résultat des sondes, moniteurs et répondeurs de disponibilité gérée.

Le canal ManagedAvailability contient les journaux des actions de récupération, ainsi que les résultats et les événements associés.

## Moniteur d’espace disque faible

La fonction de disponibilité gérée Exchange 2013 surveille des centaines de mesures système et de composants chaque minute, y compris la quantité d’espace disque libre sur les volumes utilisés par le rôle serveur de boîtes aux lettres. Avant Exchange 2013 Service Pack 1 (SP1), Exchange surveillait l’espace disponible sur tous les volumes locaux, y compris ceux qui ne contenaient pas de bases de données ou de fichiers journaux. Dans SP1 et les versions supérieures, seuls les volumes qui contiennent des bases de données Exchange et des fichiers journaux sont surveillés. Dans SP1, le seuil par défaut pour le moniteur d’espace de volume faible volume est de 200 Go. Dans la mise à jour cumulative 6 d’Exchange 2013 et les versions ultérieures, le seuil par défaut est de 180 Go. Dans SP1 et les versions ultérieures, vous pouvez configurer le seuil en ajoutant la valeur de registre DWORD suivante (en Mo) sur chaque serveur de boîtes aux lettres que vous souhaitez personnaliser :

Chemin : **HKEY\_LOCAL\_MACHINE\\Software\\Microsoft\\ExchangeServer\\v15\\Replay\\Parameters**

Valeur : *SpaceMonitorLowSpaceThresholdInMB*

Par exemple, pour configurer le seuil sur 100 Go, vous devez configurer la valeur de registre suivante :

**REG\_DWORD 186a0 (100000)**

Après avoir configuré ou modifié la valeur de registre ci-dessus, vous devez redémarrer le service de gestion des groupes de disponibilité de base de données (DAG) Microsoft Exchange pour que les modifications soient prises en compte.

## Script CollectOverMetrics.ps1

Exchange 2013 comprend un script appelé CollectOverMetrics.ps1 disponible dans le dossier Scripts. CollectOverMetrics.ps1 lit les journaux des événements relatifs aux membres du DAG pour rassembler des informations sur les opérations relatives aux bases de données (telles que montages, déplacements et basculements de bases de données) sur une période donnée. Pour chaque opération, le script enregistre les informations suivantes :

  - Identité de la base de données

  - Heure de début et de fin de l’opération

  - Serveurs sur lesquels la base de données a été montée au début et à la fin de l’opération

  - Raison de l’opération

  - Si l’opération est un succès et si l’opération est un échec, les détails de l’erreur

Le script consigne ces informations dans des fichiers .csv avec une opération par ligne. Il crée un fichier .csv pour chaque DAG.

Ce script prend en charge des paramètres qui vous permettent de personnaliser son comportement et ses résultats. Par exemple, les résultats peuvent être limités à un sous-ensemble spécifique à l’aide des paramètres *Database* et *ReportFilter*. Seules les opérations correspondant à ces filtres seront consignées dans le rapport récapitulatif au format HTML. Les paramètres disponibles sont répertoriés dans le tableau suivant.

### Paramètres du script CollectOverMetrics.ps1

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Paramètre</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>DatabaseAvailabilityGroup</em></p></td>
<td><p>Spécifie le nom du DAG à partir duquel vous voulez collecter des mesures. Si ce paramètre est omis, le DAG auquel le serveur local appartient sera utilisé. Des caractères génériques peuvent être utilisés pour collecter des informations à partir de plusieurs DAG et créer des rapports.</p></td>
</tr>
<tr class="even">
<td><p><em>Database</em></p></td>
<td><p>Fournit la liste des bases de données pour lesquelles le rapport doit être généré. Les caractères génériques sont pris en charge, par exemple, <code>-Database:&quot;DB1&quot;,&quot;DB2&quot;</code> ou <code>-Database:&quot;DB*&quot;</code>.</p></td>
</tr>
<tr class="odd">
<td><p><em>StartTime</em></p></td>
<td><p>Spécifie la durée de la période à analyser. Le script analyse uniquement les événements consignés au cours de cette période. Par conséquent, le script peut sélectionner des enregistrements d’opération partiels (par exemple, seulement la fin d’une opération au début de la période ou inversement). Si ni le paramètre <em>StartTime</em>, ni le paramètre <em>EndTime</em> n’est spécifié, le script analyse par défaut les dernières 24 heures. Si un seul des deux paramètres est spécifié, l’analyse du script commencera ou se terminera à l’heure spécifiée pour une période de 24 heures.</p></td>
</tr>
<tr class="even">
<td><p><em>EndTime</em></p></td>
<td><p>Spécifie la durée de la période à analyser. Le script analyse uniquement les événements consignés au cours de cette période. Par conséquent, le script peut sélectionner des enregistrements d’opération partiels (par exemple, seulement la fin d’une opération au début de la période ou inversement). Si ni le paramètre <em>StartTime</em>, ni le paramètre <em>EndTime</em> n’est spécifié, le script analyse par défaut les dernières 24 heures. Si un seul des deux paramètres est spécifié, l’analyse du script commencera ou se terminera à l’heure spécifiée pour une période de 24 heures.</p></td>
</tr>
<tr class="odd">
<td><p><em>ReportPath</em></p></td>
<td><p>Spécifie le dossier utilisé pour stocker les résultats du traitement des événements. Si ce paramètre est omis, le dossier Scripts sera utilisé. Si le paramètre est spécifié, le script génère une liste de fichiers .csv et utilise ces derniers comme données source pour créer un rapport récapitulatif au format HTML. Ce rapport est le même que celui qui est généré avec l’option -GenerateHtmlReport. Les fichiers peuvent être générés sur plusieurs groupes de disponibilité de base de données (DAG) à différents moments ou simultanément et le script fusionne ensuite toutes leurs données.</p></td>
</tr>
<tr class="even">
<td><p><em>GenerateHtmlReport</em></p></td>
<td><p>Indique au script de rassembler toutes les informations qu’il a enregistrées, de les regrouper ensuite par type d’opération et de générer un fichier HTML comprenant des statistiques pour chacun de ces groupes. Le rapport indique le nombre total d’opérations dans chaque groupe ainsi que le nombre d’opérations ayant échoué et fournit des statistiques sur la durée des opérations dans chaque groupe. Le rapport indique également le type des erreurs qui ont entraîné l’échec des opérations.</p></td>
</tr>
<tr class="odd">
<td><p><em>ShowHtmlReport</em></p></td>
<td><p>Indique que le rapport HTML doit être affiché dans un navigateur Web après avoir été généré.</p></td>
</tr>
<tr class="even">
<td><p><em>SummariseCsvFiles</em></p></td>
<td><p>Indique au script de lire les données des fichiers .csv qu’il a générés. Ces données sont ensuite utilisées pour générer un rapport récapitulatif similaire au rapport généré par le paramètre <em>GenerateHtmlReport</em>.</p></td>
</tr>
<tr class="odd">
<td><p><em>ActionType</em></p></td>
<td><p>Indique le type des actions opérationnelles que le script doit collecter. Les valeurs de ce paramètre sont <code>Move</code>, <code>Mount</code>, <code>Dismount</code> et <code>Remount</code>. La valeur <code>Move</code> indique quand la base de données change de serveur, par déplacement contrôlé ou par basculement. Les valeurs <code>Mount</code>, <code>Dismount</code> et <code>Remount</code> indiquent quand la base de données change d’état de montage sans être transférée sur un autre ordinateur.</p></td>
</tr>
<tr class="even">
<td><p><em>ActionTrigger</em></p></td>
<td><p>Indique quelles opérations administratives doivent être collectées par le script. Les valeurs de ce paramètre sont <code>Admin</code> et <code>Automatic</code>. Les actions automatiques sont des actions effectuées automatiquement par le système (par exemple, un basculement lorsqu’un serveur n’est plus disponible en ligne). Les actions administratives sont des actions effectuées par un administrateur à l’aide de l’environnement de ligne de commande Exchange Management Shell ou du Centre d'administration Exchange.</p></td>
</tr>
<tr class="odd">
<td><p><em>RawOutput</em></p></td>
<td><p>Indique au script de consigner les résultats directement dans le flux de sortie, comme c’est le cas dans un scénario d’écriture de sortie (write-output), au lieu de les consigner dans des fichiers .csv. Ces informations peuvent ensuite être transmises à d’autres commandes.</p></td>
</tr>
<tr class="even">
<td><p><em>IncludedExtendedEvents</em></p></td>
<td><p>Indique au script de collecter les événements qui fournissent des informations de diagnostic sur le temps consacré au montage des bases de données. Cette étape peut prendre du temps si le journal des événements relatifs aux applications est volumineux.</p></td>
</tr>
<tr class="odd">
<td><p><em>MergeCSVFiles</em></p></td>
<td><p>Indique au script de récupérer tous les fichiers .csv contenant des données sur chaque opération et de les fusionner en un seul fichier .csv.</p></td>
</tr>
<tr class="even">
<td><p><em>ReportFilter</em></p></td>
<td><p>Indique d’appliquer un filtre aux opérations à partir des champs des fichiers .csv. Ce paramètre utilise le même format qu’une opération <code>Where</code>, chaque élément étant défini sur <code>$_</code> et retournant une valeur booléenne. Par exemple : <code>{$_DatabaseName -notlike &quot;Mailbox Database*&quot;}</code> peut être utilisé pour exclure les bases de données par défaut du rapport.</p></td>
</tr>
</tbody>
</table>


## CollectOverMetrics.ps1 - Exemples

L’exemple suivant illustre la collecte de mesures pour toutes les bases de données correspondant à DB\* (avec un caractère générique inclus) dans le groupe de disponibilité de base de données nommé DAG1. Une fois les mesures recueillies, un rapport HTML est généré et affiché.

    CollectOverMetrics.ps1 -DatabaseAvailabilityGroup DAG1 -Database:"DB*" -GenerateHTMLReport -ShowHTMLReport

Les exemples suivants montrent différentes manières de filtrer un rapport récapitulatif HTML. Le premier exemple utilise le paramètre *Database* qui récupère une liste de noms de base de données. Le rapport récapitulatif contient alors uniquement des données sur ces bases de données. Les deux exemples suivants utilisent l’option *ReportFilter*. Le dernier exemple filtre toutes les bases de données par défaut.

    CollectOverMetrics.ps1 -SummariseCsvFiles (dir *.csv) -Database MailboxDatabase123,MailboxDatabase456
    CollectOverMetrics.ps1 -SummariseCsvFiles (dir *.csv) -ReportFilter { $_.DatabaseName -notlike "Mailbox Database*" }
    CollectOverMetrics.ps1 -SummariseCsvFiles (dir *.csv) -ReportFilter { ($_.ActiveOnStart -like "ServerXYZ*") -and ($_.ActiveOnEnd -notlike "ServerXYZ*") }

## Script CollectReplicationMetrics.ps1

Le script d’évaluation de l’intégrité CollectReplicationMetrics.ps1 est lui aussi inclus dans Exchange 2013. Il fournit une forme active d’analyse, car il collecte des mesures en temps réel, pendant son exécution. CollectReplicationMetrics.ps1 collecte des données à partir des compteurs de performance liés à la réplication des bases de données. Le script rassemble des données de compteur provenant de plusieurs serveurs de boîtes aux lettres, consigne ces données de chaque serveur dans un fichier .csv, puis établit un rapport des différentes statistiques sur la base de l’ensemble de ces données (par exemple, le temps pendant lequel chaque copie était en échec ou suspendue, la longueur moyenne de la file d’attente de copie ou de relecture ou le temps pendant lequel les copies ne correspondaient plus aux critères de basculement).

Vous pouvez spécifier les serveurs individuellement ou vous pouvez spécifier des DAG entiers. Vous pouvez exécuter le script pour commencer par collecter des données et générer ensuite le rapport, ou vous pouvez l’exécuter pour collecter uniquement des données ou pour établir un rapport à partir des données déjà collectées. Vous pouvez spécifier la fréquence à laquelle les données doivent être collectées et la durée totale de la collecte.

Les données collectées sur chaque serveur sont consignées dans un fichier nommé **CounterData.\<Nom\_serveur\>.\<horodatage\>.csv**. Le rapport récapitulatif est enregistré dans un fichier nommé **HaReplPerfReport.\<Nom\_DAG\>.\<horodatage\>.csv** ou **HaReplPerfReport.\<horodatage\>.csv** si vous n’avez pas exécuté le script avec le paramètre *DagName*.

Le script lance des tâches Windows PowerShell pour collecter les données de chaque serveur. Ces tâches sont exécutées pour toute la durée de la collecte des données. Si vous spécifiez un grand nombre de serveurs, ce processus peut consommer une quantité considérable de mémoire. L’étape finale du processus, lorsqu’un rapport récapitulatif est établi à partir des données, peut également prendre beaucoup de temps pour de grands volumes de données. Il est possible d’exécuter l’étape de collecte sur un ordinateur, puis de copier les données ailleurs pour les traiter.

Le script CollectReplicationMetrics.ps1 prend en charge des paramètres qui vous permettent de personnaliser son comportement et ses résultats. Les paramètres disponibles sont répertoriés dans le tableau suivant.

### Paramètres du script CollectReplicationMetrics.ps1

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Paramètre</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>DagName</em></p></td>
<td><p>Spécifie le nom du DAG à partir duquel vous voulez collecter des mesures. Si ce paramètre est omis, le DAG auquel le serveur local appartient sera utilisé.</p></td>
</tr>
<tr class="even">
<td><p><em>DatabaseNames</em></p></td>
<td><p>Fournit la liste des bases de données pour lesquelles le rapport doit être généré. Les caractères génériques sont pris en charge, par exemple, <code>-DatabaseNames:&quot;DB1&quot;,&quot;DB2&quot;</code> ou <code>-DatabaseNames:&quot;DB*&quot;</code>.</p></td>
</tr>
<tr class="odd">
<td><p><em>ReportPath</em></p></td>
<td><p>Spécifie le dossier utilisé pour stocker les résultats du traitement des événements. Si ce paramètre est omis, le dossier Scripts sera utilisé.</p></td>
</tr>
<tr class="even">
<td><p><em>Duration</em></p></td>
<td><p>Spécifie la durée pendant laquelle que le processus de collecte doit s’exécuter. Il s’agit en général de valeurs comprises entre une et trois heures. Des durées plus longues doivent être utilisées uniquement pour des intervalles plus importants entre chaque collecte ou pour une série de tâches plus courtes exécutées par des tâches planifiées.</p></td>
</tr>
<tr class="odd">
<td><p><em>Frequency</em></p></td>
<td><p>Spécifie la fréquence à laquelle les mesures de données sont collectées. En général, les valeurs sont 30 secondes, une minute ou cinq minutes. Dans des circonstances normales, des intervalles plus courts que ces valeurs ne montrent pas des changements importants entre chaque collecte.</p></td>
</tr>
<tr class="even">
<td><p><em>Servers</em></p></td>
<td><p>Indique l’identité des serveurs sur lesquels des statistiques seront collectées. Vous pouvez spécifier n’importe quelle valeur, y compris des caractères génériques ou des GUID.</p></td>
</tr>
<tr class="odd">
<td><p><em>SummariseFiles</em></p></td>
<td><p>Spécifie une liste de fichiers .csv pour générer un rapport récapitulatif. Ces fichiers sont nommés <strong>CounterData.&lt;Données_compteur&gt;*</strong> et sont générés par le script CollectReplicationMetrics.ps1.</p></td>
</tr>
<tr class="even">
<td><p><em>Mode</em></p></td>
<td><p>Spécifie les étapes de traitement que le script exécute. Vous pouvez utiliser les valeurs suivantes :</p>
<ul>
<li><p><code>CollectAndReport</code>   Il s’agit de la valeur par défaut. Cette valeur signifie que le script doit collecter les données des serveurs et les traiter pour produire le rapport récapitulatif.</p></li>
<li><p><code>CollectOnly</code>   Cette valeur signifie que le script doit uniquement collecter les données et ne pas produire de rapport.</p></li>
<li><p><code>ProcessOnly</code>   Cette valeur signifie que le script doit importer les données d’un ensemble de fichiers .csv et les traiter pour produire le rapport récapitulatif. Le paramètre <em>SummariseFiles</em> est utilisé pour fournir au script la liste de fichiers à traiter.</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p><em>MoveFilestoArchive</em></p></td>
<td><p>Spécifie que le script doit placer les fichiers dans un dossier compressé une fois qu’ils sont traités.</p></td>
</tr>
<tr class="even">
<td><p><em>LoadExchangeSnapin</em></p></td>
<td><p>Spécifie que le script doit charger les commandes de l’environnement de ligne de commande Exchange Management Shell. Ce paramètre est utile s’il faut exécuter le script en dehors de l’environnement de ligne de commande Exchange Management Shell, à l’instar d’une tâche planifiée.</p></td>
</tr>
</tbody>
</table>


## CollectReplicationMetrics.ps1 - Exemple

L’exemple suivant illustre la collecte des données sur une période d’une heure, et à des intervalles d’une minute, à partir de tous les serveurs du groupe de disponibilité de base de données DAG1, puis génère un rapport récapitulatif. Le paramètre *ReportPath* est également utilisé pour que le script place tous les fichiers dans le répertoire actuel.

```powershell
CollectReplicationMetrics.ps1 -DagName DAG1 -Duration "01:00:00" -Frequency "00:01:00" -ReportPath
```

L’exemple suivant illustre la lecture des données de tous les fichiers correspondant à CounterData\*, puis génère un rapport récapitulatif.

    CollectReplicationMetrics.ps1 -SummariseFiles (dir CounterData*) -Mode ProcessOnly -ReportPath

