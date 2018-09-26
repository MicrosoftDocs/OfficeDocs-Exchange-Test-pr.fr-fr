---
title: 'Déploiement de haute dispo. et de résilience de site: Exchange 2013 Help'
TOCTitle: Déploiement de haute disponibilité et de résilience de site
ms:assetid: 4c4e00a4-1f57-4fdb-b9b2-2779abf381a9
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dd638129(v=EXCHG.150)
ms:contentKeyID: 50478134
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Déploiement de haute disponibilité et de résilience de site

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2015-03-09_

Microsoft Exchange Server 2013 utilise le concept de « *déploiement incrémentiel* » aussi bien pour la haute disponibilité que pour la résilience de site. Il vous suffit d’installer au moins deux serveurs de boîtes aux lettres Exchange 2013 en mode autonome. Ensuite, vous les configurez, ainsi que les bases de données de boîtes aux lettres, de manière incrémentielle pour obtenir une haute disponibilité et une résilience de site, selon les besoins.

## Présentation du processus de déploiement

Bien que la procédure puisse varier légèrement d’une organisation à l’autre, le processus global de déploiement d’Exchange 2013 dans une configuration présentant une haute disponibilité ou une résilience de site est généralement identique. Après avoir réalisé les tâches de planification et de conception nécessaires à l’établissement et au déploiement d’un groupe de disponibilité de base de données (DAG) et à la création de copies de bases de données de boîtes aux lettres, vous pouvez également effectuer les opérations suivantes :

1.  Créer un groupe de disponibilité de base de données. Pour obtenir la procédure détaillée, voir [Créer un groupe de disponibilité de base de données](create-a-database-availability-group-exchange-2013-help.md).

2.  Si nécessaire, préparer l’objet réseau de cluster (CNO). Une préparation de l’objet réseau de cluster est nécessaire lors du déploiement d’un groupe de disponibilité de base de données avec des serveurs de boîtes aux lettres exécutant Windows Server 2012. Si vous déployez un groupe de disponibilité de base de données sans point d’accès administratif à l’aide des serveurs de boîtes aux lettres exécutant Windows Server 2012 R2, il n’est pas nécessaire de préparer un objet réseau de cluster. La préparation est également obligatoire dans les environnements dans lesquels la création du compte d’ordinateur est restreinte ou lorsque les comptes d’ordinateur sont créés dans un conteneur autre que le conteneur d’ordinateurs par défaut. Pour obtenir la procédure détaillée, voir [Préinstallation de l’objet nom de cluster pour un groupe de disponibilité de base de données](pre-stage-the-cluster-name-object-for-a-database-availability-group-exchange-2013-help.md).

3.  Ajouter au moins deux serveurs de boîtes aux lettres au groupe de disponibilité de base de données. Pour obtenir la procédure détaillée, voir [Gérer l’appartenance au groupe de disponibilité de la base de données](manage-database-availability-group-membership-exchange-2013-help.md).

4.  Configurer les propriétés du groupe de disponibilité de base de données selon vos besoins :
    
    1.  Configurer éventuellement le chiffrement et la compression pour le groupe de disponibilité de base de données, la réplication de port, les adresses IP du groupe de disponibilité de base de données et d’autres propriétés relatives à ce groupe. Pour obtenir la procédure détaillée, voir [Configuration des propriétés du groupe de disponibilité de base de données](configure-database-availability-group-properties-exchange-2013-help.md).
    
    2.  Activer le mode de coordination de l’activation du centre de données (DAC) pour le groupe de disponibilité de base de données. Cela permet de protéger le groupe de disponibilité de base de données contre les conditions de Split-Brain au niveau de la base de données lors d’un switchback vers le centre de données principal après un basculement, et active l’utilisation des cmdlets intégrées de récupération de groupe de disponibilité de base de données. Pour plus d’informations, consultez la rubrique [Mode de coordination de l’activation du centre de données](datacenter-activation-coordination-mode-exchange-2013-help.md).

5.  Ajouter des copies de base de données de boîtes aux lettres entre les serveurs de boîtes aux lettres du groupe de disponibilité de base de données. Pour obtenir la procédure détaillée, voir [Ajout d’une copie de base de données de boîtes aux lettres](add-a-mailbox-database-copy-exchange-2013-help.md).

## Exemple de déploiement : Groupe de disponibilité de base de données à quatre membres dans deux centres de données

Cet exemple explique en détail comment l’organisation appelée « Contoso, Ltd » configure et déploie un groupe de disponibilité de base de données à quatre membres qui couvrira deux emplacements physiques : Redmond (État de Washington) et Portland (État de l’Oregon).

## Infrastructure de base

Chaque emplacement contient les éléments d’infrastructure nécessaires à l’exploitation d’une infrastructure de messagerie Exchange 2013, à savoir :

  - Services d’annuaire (Active Directory ou services de domaine Active Directory (AD DS))

  - Résolution de noms DNS (Domain Name System)

  - Plusieurs serveurs d’accès au client Exchange 2013

  - Plusieurs serveurs de boîtes aux lettres Exchange 2013

La figure suivante illustre la configuration de l’organisation Contoso.

**Groupe de disponibilité de base de données couvrant deux sites**

![Groupe de disponibilité de base de données couvrant deux sites](images/Dd638129.1c326fd4-3c7b-4416-a63d-fbfdd0cc6b18(EXCHG.150).gif "Groupe de disponibilité de base de données couvrant deux sites")

## Configuration du réseau

Comme l’illustrait la figure précédente, la solution implique l’utilisation de plusieurs sous-réseaux et de plusieurs réseaux. Chaque serveur de boîtes aux lettres du groupe de disponibilité de base de données dispose de deux cartes réseau sur des sous-réseaux distincts. Dans chaque serveur de boîtes aux lettres, une carte réseau sera utilisée pour le réseau MAPI (192.168.*x*.*x*) et l’autre pour le réseau de réplication (10.0.*x*.*x*). Seul le réseau MAPI fournit la connectivité à Active Directory, aux services DNS et autres serveurs et clients Exchange. La carte utilisée pour le réseau de réplication de chaque membre fournit la connectivité uniquement aux cartes du réseau de réplication des autres membres du groupe de disponibilité de base de données.

Le tableau suivant présente en détail les paramètres de chaque carte réseau dans chacun des nœuds.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Nom</th>
<th>Adresse IPv4</th>
<th>Masque de sous-réseau</th>
<th>Passerelle par défaut</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>MBX1 (MAPI)</p></td>
<td><p>192.168.1.4</p></td>
<td><p>255.255.255.0</p></td>
<td><p>192.168.1.1</p></td>
</tr>
<tr class="even">
<td><p>MBX2 (MAPI)</p></td>
<td><p>192.168.1.5</p></td>
<td><p>255.255.255.0</p></td>
<td><p>192.168.1.1</p></td>
</tr>
<tr class="odd">
<td><p>MBX3 (MAPI)</p></td>
<td><p>192.168.2.4</p></td>
<td><p>255.255.255.0</p></td>
<td><p>192.168.2.1</p></td>
</tr>
<tr class="even">
<td><p>MBX4 (MAPI)</p></td>
<td><p>192.168.2.5</p></td>
<td><p>255.255.255.0</p></td>
<td><p>192.168.2.1</p></td>
</tr>
<tr class="odd">
<td><p>MBX1 (réplication)</p></td>
<td><p>10.0.1.4</p></td>
<td><p>255.255.0.0</p></td>
<td><p>Aucun</p></td>
</tr>
<tr class="even">
<td><p>MBX2 (réplication)</p></td>
<td><p>10.0.1.5</p></td>
<td><p>255.255.0.0</p></td>
<td><p>Aucun</p></td>
</tr>
<tr class="odd">
<td><p>MBX3 (réplication)</p></td>
<td><p>10.0.2.4</p></td>
<td><p>255.255.0.0</p></td>
<td><p>Aucun</p></td>
</tr>
<tr class="even">
<td><p>MBX4 (réplication)</p></td>
<td><p>10.0.2.5</p></td>
<td><p>255.255.0.0</p></td>
<td><p>Aucun</p></td>
</tr>
</tbody>
</table>


Comme le montrait le tableau précédent, les cartes des réseaux de réplication n’utilisent pas de passerelles par défaut. Pour assurer la connectivité réseau entre chacune des cartes de réseau de réplication, Contoso utilise des itinéraires statiques permanents, configurés au moyen de l’outil Netsh.exe.

Pour configurer le routage des cartes de réseau de réplication sur MBX1 et MBX2, la commande suivante a été exécutée sur chaque serveur.

```powershell
netsh interface ipv4 add route 10.0.2.0/24 <NetworkName> 10.0.1.254
```

Pour configurer le routage des cartes de réseau de réplication sur MBX3 et MBX4, la commande suivante a été exécutée sur chaque serveur.

```powershell
netsh interface ipv4 add route 10.0.1.0/24 <NetworkName> 10.0.2.254
```

Les paramètres réseau supplémentaires suivants ont également été configurés :

  - La case **Enregistrer les adresses de cette connexion dans le système DNS** est cochée pour la carte réseau de chaque membre du groupe de disponibilité de base de données et désactivée pour chaque carte de réseau de réplication.

  - Au moins une adresse de serveur DNS est configurée pour la carte de réseau MAPI de chaque membre de groupe de disponibilité de base de données ; aucune adresse n’est configurée pour les cartes de réseau de réplication. À des fins de redondance, Contoso utilise plusieurs adresses de serveur DNS pour leurs cartes de réseau MAPI.

  - Contoso n’utilise pas le Pare-feu Windows et l’a désactivé sur ses serveurs.

Lorsque les cartes réseau ont été configurées, Contoso est prêt à créer un groupe de disponibilité de base de données et à y ajouter les serveurs de boîtes aux lettres.

## Création et configuration du groupe de disponibilité de base de données

L’administrateur a décidé de créer un script d’interface de ligne de commande Windows PowerShell qui effectue plusieurs tâches :

  - Il utilise la cmdlet [New-DatabaseAvailabilityGroup](https://technet.microsoft.com/fr-fr/library/dd351107\(v=exchg.150\)) pour créer le groupe de disponibilité de base de données. Comme Redmond est considéré comme le centre de données principal, Contoso a choisi d’utiliser un serveur témoin dans le même centre de données : CAS1.

  - Il utilise la cmdlet [Set-DatabaseAvailabilityGroup](https://technet.microsoft.com/fr-fr/library/dd297934\(v=exchg.150\)) pour préconfigurer un serveur témoin et un répertoire témoin de remplacement si un basculement de centre de données s’avérait nécessaire.

  - Il utilise la cmdlet [Add-DatabaseAvailabilityGroupServer](https://technet.microsoft.com/fr-fr/library/dd298049\(v=exchg.150\)) pour ajouter chacun des quatre serveurs de boîtes aux lettres au groupe de disponibilité de base de données.

  - Il utilise la cmdlet [Set-DatabaseAvailabilityGroup](https://technet.microsoft.com/fr-fr/library/dd297934\(v=exchg.150\)) pour configurer le groupe de disponibilité de base de données en mode DAC. Pour plus d’informations sur le mode DAC, voir [Mode de coordination de l’activation du centre de données](datacenter-activation-coordination-mode-exchange-2013-help.md).

Les commandes utilisées dans le script sont les suivantes :

```powershell
New-DatabaseAvailabilityGroup -Name DAG1 -WitnessServer CAS1 -WitnessDirectory C:\DAGWitness\DAG1.contoso.com -DatabaseAvailabilityGroupIPAddresses 192.168.1.8,192.168.2.8
```

La commande précédente crée le groupe de disponibilité de base de données DAG1, configure CAS1 comme serveur témoin, configure un répertoire témoin spécifique (C:\\DAGWitness\\DAG1.contoso.com), puis définit deux adresses IP pour le groupe de disponibilité de base de données (une pour chaque sous-réseau du réseau MAPI).

```powershell
Set-DatabaseAvailabilityGroup -Identity DAG1 -AlternateWitnessDirectory C:\DAGWitness\DAG1.contoso.com -AlternateWitnessServer CAS4
```

La commande précédente configure DAG1 pour qu’il utilise un serveur témoin de remplacement de CAS4, ainsi qu’un répertoire témoin de remplacement sur CAS4 qui utilise le même chemin d’accès que celui configuré sur CAS1.

> [!NOTE]
> L’utilisation d’un chemin d’accès identique n’est pas obligatoire. Contoso a choisi cette option pour standardiser la configuration de son organisation.


```powershell
Add-DatabaseAvailabilityGroupServer -Identity DAG1 -MailboxServer MBX1
Add-DatabaseAvailabilityGroupServer -Identity DAG1 -MailboxServer MBX3
Add-DatabaseAvailabilityGroupServer -Identity DAG1 -MailboxServer MBX2
Add-DatabaseAvailabilityGroupServer -Identity DAG1 -MailboxServer MBX4
```

Les commandes précédentes ajoutent chaque serveur de boîtes aux lettres au groupe de disponibilité de base de données, un par un. Elles installent également le composant Clustering avec basculement Windows sur chaque serveur de boîtes aux lettres (s’il n’est pas encore installé), créent un cluster de basculement et rattachent chaque serveur de boîtes aux lettres au nouveau cluster.

```powershell
Set-DatabaseAvailabilityGroup -Identity DAG1 -DatacenterActivationMode DagOnly
```

La commande précédente active le mode DAC pour le groupe de disponibilité de base de données.

## Bases de données de boîtes aux lettres et copies de bases de données de boîtes aux lettres

Lorsque le groupe de disponibilité de base de données a été créé et que les serveurs de boîtes aux lettres ont été ajoutés à ce groupe, Contoso prépare la création des bases de données de boîtes aux lettres et de leurs copies. Pour répondre aux critères de tolérance aux pannes, Contoso prévoit de configurer chaque base de données de boîtes aux lettres avec trois copies non retardées et une copie retardée. La copie retardée sera configurée avec un délai de réexécution de journal de trois jours.

Cette configuration fournit au total quatre copies de chaque base de données (une active, deux passives non retardées et une passive retardée). Contoso prévoit d’avoir quatre bases de données actives par serveur. Avec quatre bases de données actives par serveur et trois copies passives de chaque base de données, la solution Contoso contient en tout 16 copies de base de données.

Comme l’illustre la figure suivante, Contoso adopte une approche équilibrée pour l’agencement de ses bases de données.

**Agencement des copies de bases de données pour Contoso, Ltd**

![Disposition de la copie de la base de données pour Contoso, Ltd](images/Dd638129.41d0c78e-ccaf-4b67-8bab-6fb344668ead(EXCHG.150).gif "Disposition de la copie de la base de données pour Contoso, Ltd")

Chaque serveur de boîtes aux lettres héberge une copie active de base de données de boîtes aux lettres, deux copies passives non retardées et une copie passive retardée. La copie retardée de chaque base de données de boîtes aux lettres active est hébergée sur un serveur de boîtes aux lettres dans l’autre site.

Pour créer cette configuration, l’administrateur exécute plusieurs commandes.

Sur MBX1, exécutez les commandes suivantes :

```powershell
Add-MailboxDatabaseCopy -Identity DB1 -MailboxServer MBX2
Add-MailboxDatabaseCopy -Identity DB1 -MailboxServer MBX4
Add-MailboxDatabaseCopy -Identity DB1 -MailboxServer MBX3 -ReplayLagTime 3.00:00:00 -SeedingPostponed
Suspend-MailboxDatabaseCopy -Identity DB1\MBX3 -SuspendComment "Seed from MBX4" -Confirm:$False
Update-MailboxDatabaseCopy -Identity DB1\MBX3 -SourceServer MBX4
Suspend-MailboxDatabaseCopy -Identity DB1\MBX3 -ActivationOnly
```

Sur MBX2, exécutez les commandes suivantes :

```powershell
Add-MailboxDatabaseCopy -Identity DB2 -MailboxServer MBX1
Add-MailboxDatabaseCopy -Identity DB2 -MailboxServer MBX3
Add-MailboxDatabaseCopy -Identity DB2 -MailboxServer MBX4 -ReplayLagTime 3.00:00:00 -SeedingPostponed
Suspend-MailboxDatabaseCopy -Identity DB2\MBX4 -SuspendComment "Seed from MBX3" -Confirm:$False
Update-MailboxDatabaseCopy -Identity DB2\MBX4 -SourceServer MBX3
Suspend-MailboxDatabaseCopy -Identity DB2\MBX4 -ActivationOnly
```

Sur MBX3, exécutez les commandes suivantes :

```powershell
Add-MailboxDatabaseCopy -Identity DB3 -MailboxServer MBX4
Add-MailboxDatabaseCopy -Identity DB3 -MailboxServer MBX2
Add-MailboxDatabaseCopy -Identity DB3 -MailboxServer MBX1 -ReplayLagTime 3.00:00:00 -SeedingPostponed
Suspend-MailboxDatabaseCopy -Identity DB3\MBX1 -SuspendComment "Seed from MBX2" -Confirm:$False
Update-MailboxDatabaseCopy -Identity DB3\MBX1 -SourceServer MBX2
Suspend-MailboxDatabaseCopy -Identity DB3\MBX1 -ActivationOnly
```

Sur MBX4, exécutez les commandes suivantes :

```powershell
Add-MailboxDatabaseCopy -Identity DB4 -MailboxServer MBX3
Add-MailboxDatabaseCopy -Identity DB4 -MailboxServer MBX1
Add-MailboxDatabaseCopy -Identity DB4 -MailboxServer MBX2 -ReplayLagTime 3.00:00:00 -SeedingPostponed
Suspend-MailboxDatabaseCopy -Identity DB4\MBX2 -SuspendComment "Seed from MBX1" -Confirm:$False
Update-MailboxDatabaseCopy -Identity DB4\MBX2 -SourceServer MBX1
Suspend-MailboxDatabaseCopy -Identity DB4\MBX2 -ActivationOnly
```

Dans les exemples précédents de la cmdlet **Add-MailboxDatabaseCopy**, le paramètre *ActivationPreference* n’était pas spécifié. La tâche incrémente automatiquement le numéro de préférences d’activation à chaque copie ajoutée. Le numéro de préférence 1 est toujours attribué à la base de données d’origine. Le numéro de préférence 2 est attribué automatiquement à la première copie ajoutée par la cmdlet **Add-MailboxDatabaseCopy**. Si aucune copie n’est supprimée, le numéro de préférence 3 est automatiquement attribué à la prochaine copie ajoutée, et ainsi de suite. Dans les exemples précédents, le numéro de préférence 2 est donc attribué à la copie passive dans le même centre de données que la copie active ; le numéro de préférence 3 est attribué à la copie passive non retardée dans le centre de données distant et le numéro de préférence 4 est attribué à la copie passive retardée dans le centre de données distant.

Bien qu’il existe deux copies de chaque base de données active sur le réseau étendu de l’autre emplacement, l’amorçage sur le réseau étendu n’a été réalisé qu’une seule fois. Cela est dû au fait que Contoso exploite la capacité d’Exchange 2013 d’utiliser une copie passive de la base de données comme source d’amorçage. Le fait d’utiliser la cmdlet [Add-MailboxDatabaseCopy](https://technet.microsoft.com/fr-fr/library/dd298105\(v=exchg.150\)) avec le paramètre *SeedingPostponed* évite l’amorçage automatique de la copie de base de données en cours de création. L’administrateur peut ensuite suspendre la copie non amorcée et, à l’aide de la cmdlet [Update-MailboxDatabaseCopy](https://technet.microsoft.com/fr-fr/library/dd335201\(v=exchg.150\)) avec le paramètre *SourceServer*, il peut désigner la copie locale de la base de données comme source de l’opération d’amorçage. Il en résulte que l’amorçage de la deuxième copie de base de données ajoutée à chaque emplacement se déroule au niveau local et non sur le réseau étendu.

> [!NOTE]
> Dans l’exemple précédent, la copie de base de données non retardée est amorcée sur le réseau étendu, puis elle sert à amorcer la copie retardée de la base de données située dans le même centre de données que la copie non retardée.


Contoso a configuré une des copies passives de chaque base de données de boîtes aux lettres en tant que copie retardée pour qu’elle serve de protection dans l’éventualité, rare mais catastrophique, d’une corruption logique de la base de données. Par conséquent, l’administrateur utilise la cmdlet [Suspend-MailboxDatabaseCopy](https://technet.microsoft.com/fr-fr/library/dd351074\(v=exchg.150\)) et le paramètre *ActivationOnly* pour configurer les copies retardées comme étant bloquées pour l’activation. Ceci garantit que les copies de bases de données retardées ne seront pas activées si un basculement de base de données ou de serveur devait se produire.

## Validation de la solution

Une fois la solution déployée et configurée, l’administrateur effectue plusieurs tâches validant l’état de préparation de la solution avant de déplacer les boîtes aux lettres de production vers les bases de données du groupe de disponibilité de base de données. La solution doit être soumise à des tests et à des inspections, en faisant appel à plusieurs méthodes et notamment des simulations de défaillance. Pour valider la solution, l’administrateur effectue plusieurs tâches.

Pour vérifier l’intégrité globale du groupe de disponibilité de base de données, l’administrateur exécute la cmdlet [Test-ReplicationHealth](https://technet.microsoft.com/fr-fr/library/bb691314\(v=exchg.150\)). Cette cmdlet vérifie plusieurs aspects de l’état de réplication et de réexécution pour fournir des informations sur chaque serveur de boîtes aux lettres et chaque copie de base de données du groupe de disponibilité de base de données.

Pour vérifier l’activité de réplication et de réexécution, l’administrateur exécute la cmdlet [Get-MailboxDatabaseCopyStatus](https://technet.microsoft.com/fr-fr/library/dd298044\(v=exchg.150\)). Cette cmdlet peut fournir des informations en temps réel sur l’état d’une copie spécifique de base de données de boîtes aux lettres ou sur l’ensemble des copies de bases de données de boîtes aux lettres sur un serveur précis. Pour plus d’informations sur la surveillance de l’intégrité et l’état des bases de données répliquées dans un groupe de disponibilité de base de données, voir [Surveillance des groupes de disponibilité des bases de données](monitoring-database-availability-groups-exchange-2013-help.md).

Pour vérifier que les basculements fonctionnent comme prévu, l’administrateur utilise la cmdlet [Move-ActiveMailboxDatabase](https://technet.microsoft.com/fr-fr/library/dd298068\(v=exchg.150\)) pour exécuter une série de basculements de bases de données et de serveurs. Une fois ces tâches réalisées, il utilise la même cmdlet pour déplacer les copies actives de bases de données vers leur emplacement d’origine.

Pour vérifier les comportements attendus dans divers scénarios de défaillance, l’administrateur effectue plusieurs tâches destinées à simuler une défaillance ou à provoquer une véritable défaillance. Par exemple :

  - Débrancher le cordon d’alimentation sur MBX1, déclenchant ainsi un basculement de serveur. L’administrateur vérifie alors que la base de données DB1 s’active sur un autre serveur (de préférence MBX2, sur la base des numéros de préférence d’activation).

  - Débrancher le câble réseau de la carte réseau MAPI sur MBX2, déclenchant ainsi un basculement de serveur. L’administrateur vérifie alors que la base de données DB2 s’active sur un autre serveur (de préférence MBX1, sur la base des numéros de préférence d’activation).

  - Mettre hors connexion le disque utilisé par la copie active de la base de données (DB3), déclenchant ainsi un basculement de base de données. L’administrateur vérifie alors que la base de données DB3 s’active sur un autre serveur (de préférence MBX4, sur la base des numéros de préférence d’activation).

Une organisation peut aussi tester d’autres scénarios de défaillance en fonction de ses besoins. À la suite de la simulation d’une seule défaillance (par exemple, débrancher le cordon d’alimentation) et de l’observation de la capacité de récupération de la solution, l’administrateur peut opter pour un retour à la configuration d’origine. Dans certains cas, la solution peut être testée pour résister à plusieurs défaillances simultanées. En fin de compte, votre plan de tests vous indiquera s’il faut rétablir la configuration d’origine de la solution après avoir réalisé chaque simulation de défaillance.

En outre, un administrateur peut décider de débrancher la connexion réseau entre deux centres de données pour simuler une défaillance de site. La réalisation d’un basculement de centre de données est une opération plus complexe exigeant une plus grande coordination, mais elle est recommandée si la solution en cours de déploiement doit apporter la résilience de site aux services et données de messagerie.

## Transition vers le mode d’exploitation

Une fois la solution déployée, son extension peut être poursuivie au moyen du déploiement incrémentiel. À ce stade, la gestion de la solution doit se tourner vers des processus d’exploitation impliquant l’exécution des tâches suivantes :

  - Surveiller l’intégrité et l’état des groupes de disponibilité de base de données et des copies de bases de données de boîtes aux lettres. Pour plus d’informations, consultez la rubrique [Surveillance des groupes de disponibilité des bases de données](monitoring-database-availability-groups-exchange-2013-help.md).

  - Effectuer les basculements de base de données si cela est nécessaire. Pour connaître la procédure détaillée d’exécution d’un basculement de base de données, voir [Activer une copie de la base de données de boîtes aux lettres](activate-a-mailbox-database-copy-exchange-2013-help.md).

Pour plus d’informations sur la gestion de la solution, voir [Gestion de la haute disponibilité et de la résilience de site](managing-high-availability-and-site-resilience-exchange-2013-help.md).

