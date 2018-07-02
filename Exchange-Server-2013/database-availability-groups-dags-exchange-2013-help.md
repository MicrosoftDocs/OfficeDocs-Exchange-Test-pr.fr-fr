---
title: 'Groupe de disponibilité de base de données (DAG): Exchange 2013 Help'
TOCTitle: Groupe de disponibilité de base de données (DAG)
ms:assetid: ab9b88ce-2f44-4334-96ad-a666b95888a0
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dd979799(v=EXCHG.150)
ms:contentKeyID: 50478988
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Groupe de disponibilité de base de données (DAG)

 

_**Sapplique à :**Exchange Server 2013_

_**Dernière rubrique modifiée :**2015-06-04_

Découvrez le DAG Exchange dans Exchange Server 2013. Cet article présente le cycle de vie du groupe de disponibilité de base de données (DAG), ainsi que l’utilisation d’un DAG pour la haute disponibilité et la résilience de site.

Un groupe de disponibilité de base de données (DAG) est le composant de base de la structure de résilience de site et de haute disponibilité de serveur de boîtes aux lettres intégré à Microsoft Exchange Server 2013. Un DAG est composé d'un maximum de 16 serveurs de boîtes aux lettres qui hébergent un ensemble de bases de données. Ces serveurs peuvent ainsi récupérer automatiquement des bases de données à la suite d'une panne d'un serveur ou lorsqu'une base de données n'est plus accessible.

Un DAG tient lieu de cadre pour la réplication de bases de données de boîtes aux lettres, le basculement et la permutation de bases de données et de serveurs et un composant interne appelé *Active Manager*. Active Manager, qui fonctionne sur tous les serveurs de boîtes aux lettres, gère les permutations et les basculements dans les DAG. Pour plus d'informations sur Active Manager, consultez la rubrique [Active Manager](active-manager-exchange-2013-help.md).

N'importe quel serveur d'un DAG peut héberger une copie d'une base de données de boîtes aux lettres se trouvant sur un autre serveur du DAG. Lorsqu’un serveur est ajouté à un DAG, il fonctionne avec les autres serveurs du DAG pour assurer la récupération automatique à la suite de défaillances affectant des bases de données de boîtes aux lettres, par exemple la défaillance d’un disque, d’un serveur ou d’un réseau.

**Contenu de cette rubrique**

Cycle de vie d’un groupe de disponibilité de base de données (DAG)

Utilisation d’un groupe de disponibilité de base de données (DAG) pour la haute disponibilité

Utilisation d’un groupe de disponibilité de base de données (DAG) pour la résilience de site

## Cycle de vie d’un groupe de disponibilité de base de données (DAG)

Les DAG exploitent le concept de *déploiement incrémentiel* qui vous permet de déployer la disponibilité de services et de données sur l'ensemble de vos serveurs de boîtes de lettres et de vos bases de données après l'installation d'Exchange. Après avoir déployé des serveurs de boîtes aux lettres Exchange 2013, vous pouvez créer un DAG, y ajouter des serveurs de boîtes aux lettres et répliquer des bases de données de boîtes aux lettres entre les membres de ce DAG.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Il est pris en charge pour créer un groupe de disponibilité de base de données (DAG) comprenant une combinaison de serveurs de boîtes aux lettres physiques et virtualisés, si les serveurs et les solutions répondent aux <a href="exchange-2013-system-requirements-exchange-2013-help.md">Configuration requise pour Exchange 2013</a> et aux conditions requises stipulées dans <a href="exchange-2013-virtualization-exchange-2013-help.md">Virtualisation d'Exchange 2013</a>. Comme pour toutes les configurations de haute disponibilité Exchange, vous devez vérifier que tous les serveurs de boîtes aux lettres dans le DAG sont correctement dimensionnés de façon à traiter la charge de travail nécessaire lors des interruptions programmées et non programmées.</td>
</tr>
</tbody>
</table>


La création d'un DAG s'effectue à l'aide de la cmdlet [New-DatabaseAvailabilityGroup](https://technet.microsoft.com/fr-fr/library/dd351107\(v=exchg.150\)). À sa création, le DAG est un objet vide dans Active Directory. Cet objet Active Directory permet de stocker les informations nécessaires ayant trait au DAG, telles que les informations d'appartenance aux serveurs et certains paramètres de configuration de DAG. Lorsque vous ajoutez le premier serveur au DAG, un cluster de basculement est automatiquement créé pour le DAG. Ce cluster de basculement est utilisé exclusivement par le DAG et doit lui être dédié. L'utilisation du cluster à d'autres fins n'est pas prise en charge.

Outre la création d'un cluster de basculement, l'infrastructure qui surveille les serveurs pour détecter les pannes du réseau ou de serveurs est exécutée. Le mécanisme de pulsation du cluster de basculement et la base de données du cluster sont alors utilisés pour effectuer le suivi des informations liées au DAG et les gérer. Ces informations, qui peuvent changer rapidement, sont notamment l'état de montage de la base de données, l'état de réplication et le dernier emplacement monté.

Lors de sa création, le DAG reçoit un nom unique et soit une ou plusieurs adresses IP statiques lui sont affectées, soit il est configuré pour utiliser le protocole DHCP, soit il est créé sans point d’accès administratif de cluster. Les DAG sans point d’accès administratif peuvent être créés uniquement sur les serveurs exécutant Exchange 2013 Service Pack 1 ou version ultérieure sur Windows Server 2012 R2 Standard ou Datacenter Edition. Les DAG sans point d’accès administratif de cluster présentent les caractéristiques suivantes :

  - Aucune adresse IP n’est attribuée au cluster/DAG, donc il n’y a aucune ressource d’adresse IP dans le groupe de ressources de base de cluster.

  - Aucun nom de réseau n’est attribué au cluster, donc il n’y a aucune ressource de nom de réseau dans le groupe de ressources de base de cluster.

  - Le nom du cluster/DAG n’est pas inscrit dans DNS, et il ne peut pas être résolu sur le réseau.

  - Aucun objet nom de cluster (CNO) n’est créé dans Active Directory.

  - Le cluster ne peut pas être géré à l’aide de l’outil de gestion du cluster de basculement. Il doit être géré à l’aide de Windows PowerShell, et les cmdlets PowerShell doivent être exécutées sur des membres individuels du cluster.

Cet exemple montre comment utiliser l’environnement de ligne de commande Exchange Management Shell pour créer un DAG sans point d’accès administratif de cluster qui aura trois serveurs. Deux serveurs (EX1 et EX2) sont sur le même sous-réseau (10.0.0.0) et le troisième (EX3) se trouve sur un autre sous-réseau (192.168.0.0).

    New-DatabaseAvailabilityGroup -Name DAG1 -WitnessServer EX4 -DatabaseAvailabilityGroupIPAddresses 10.0.0.5,192.168.0.5
    Add-DatabaseAvailabilityGroupServer -Identity DAG1 -MailboxServer EX1
    Add-DatabaseAvailabilityGroupServer -Identity DAG1 -MailboxServer EX2
    Add-DatabaseAvailabilityGroupServer -Identity DAG1 -MailboxServer EX3

Les commandes pour créer un DAG sans point d’accès administratif de cluster sont très similaires :

    New-DatabaseAvailabilityGroup -Name DAG1 -WitnessServer EX4 -DatabaseAvailabilityGroupIPAddresses ([System.Net.IPAddress])::None
    Add-DatabaseAvailabilityGroupServer -Identity DAG1 -MailboxServer EX1
    Add-DatabaseAvailabilityGroupServer -Identity DAG1 -MailboxServer EX2
    Add-DatabaseAvailabilityGroupServer -Identity DAG1 -MailboxServer EX3

Le cluster pour DAG1 est créé lorsqu'EX1 est ajouté au groupe de disponibilité de base de données. Au cours de la création du cluster, la cmdlet **Add-DatabaseAvailabilityGroupServer** récupère les adresses IP configurées pour le DAG et ignore celles qui ne correspondent à aucun des sous-réseaux trouvés sur EX1. Dans le premier exemple ci-dessus, le cluster pour DAG1 est créé avec l’adresse IP 10.0.0.5 et l’adresse 192.168.0.5 est ignorée. Dans le second exemple ci-dessus, la valeur du paramètre *DatabaseAvailabilityGroupIPAddresses* demande à la tâche de créer un cluster de basculement pour le DAG qui ne dispose pas de point d’accès administratif. Ainsi, le cluster est créé avec une ressource de nom de réseau ou d’adresse IP dans le groupe de ressources de base de cluster.

EX2 est ensuite ajouté et la cmdlet **Add-DatabaseAvailabilityGroupServer** récupère de nouveau les adresses IP configurées pour le DAG. Les adresses IP du cluster ne changent pas, car EX2 se trouve sur le même sous-réseau qu’EX1.

EX3 est ensuite ajouté et la cmdlet **Add-DatabaseAvailabilityGroupServer** récupère de nouveau les adresses IP configurées pour le DAG. Étant donné qu'un sous-réseau correspondant à l'adresse 192.168.0.5 est présent sur EX3, l'adresse 192.168.0.5 est ajoutée en tant que ressource d'adresse IP dans le groupe de clusters. En outre, une dépendance **OR** pour la ressource Nom du réseau de chaque ressource d'adresse IP est automatiquement configurée. L’adresse 192.168.0.5 sera utilisée par le cluster lorsque le groupe de ressources de base de cluster bascule vers EX3.

Pour les DAG avec point d’accès administratif de cluster, la fonctionnalité de clustering de basculement de Windows enregistre les adresses IP du cluster dans le DNS (Domain Name System) lorsque la ressource Nom du réseau est disponible en ligne. En outre, lorsqu’EX1 est ajouté au cluster, un objet nom de cluster (CNO) est créé dans Active Directory. Le nom de réseau, les adresses IP, et le CNO du cluster ne sont pas utilisés pour les fonctions DAG. Les administrateurs et les utilisateurs finals n’ont pas besoin de communiquer, pour une raison ou une autre, avec le nom du cluster/DAG ni avec l’adresse IP ou de s’y connecter. Certaines applications tierces se connectent au point d’accès administratif de cluster pour effectuer des tâches de gestion, telles que des tâches de sauvegarde ou de surveillance. Si vous n’utilisez pas des applications tierces qui nécessitent un point d’accès administratif de cluster, et que votre DAG exécute Exchange 2013 SP1 ou version ultérieure sur Windows Server 2012 R2, nous vous conseillons de créer un DAG sans point d’accès administratif. Ceci simplifie la configuration du DAG, élimine le besoin d’une ou plusieurs adresses IP, et permet de réduire la surface d’attaque d’un DAG.

Les DAG sont également configurés pour utiliser un serveur témoin et un répertoire témoin. Le serveur témoin et le répertoire témoin sont automatiquement configurés par le système, mais l'administrateur peut les configurer manuellement. Dans les exemples ci-dessus, EX4 (un serveur qui n’est pas et qui ne sera pas membre du DAG) est configuré manuellement en tant que serveur témoin du DAG.

Par défaut, un DAG est conçu pour utiliser la fonctionnalité de réplication continue intégrée pour répliquer des bases de données de boîtes aux lettres entre les serveurs qui en sont membres. Si vous utilisez la réplication de données tierce avec l'API de réplication tierce dans Exchange 2013, vous devez créer le DAG en mode réplication tierce à l'aide de la cmdlet [New-DatabaseAvailabilityGroup](https://technet.microsoft.com/fr-fr/library/dd351107\(v=exchg.150\)) avec le paramètre *ThirdPartyReplication*. Une fois que ce mode est activé, il ne peut pas être désactivé.

Une fois le DAG créé, des serveurs de boîtes aux lettres peuvent y être ajoutés. Lorsque le premier serveur est ajouté au DAG, un cluster qui sera utilisé par ce dernier est créé. Les DAG utilisent la technologie de clustering de basculement de Windows ; il peut s'agir notamment de la pulsation de clusters, de réseaux de clusters et d'une base de données de clusters (pour stocker les données qui changent, par exemple lorsque l'état d'une base de données passe d'actif à passif et inversement ou de montée à démontée et inversement). Lorsqu'un serveur est ajouté au DAG, il est ajouté au cluster sous-jacent. Le modèle de quorum du cluster est automatiquement ajusté par Exchange et le serveur est ajouté à l'objet du DAG dans Active Directory.

Après l'ajout de serveurs de boîtes aux lettres à un DAG, vous pouvez configurer plusieurs propriétés, comme l'utilisation du chiffrement ou de la compression réseau pour la réplication des bases de données au sein du DAG. Vous pouvez également configurer des réseaux de DAG et en créer.

Une fois que vous avez ajouté des membres à un DAG et configuré celui-ci, vous pouvez répliquer les bases de données de boîtes aux lettres actives se trouvant sur chaque serveur sur les autres membres du DAG. Vous pouvez ensuite surveiller l'intégrité et l'état des copies de ces bases de données à l'aide de différents outils de surveillance intégrés. Vous pouvez également effectuer des permutations de serveurs et de bases de données.

Pour plus d'informations sur la création d'un DAG, la gestion des serveurs membres d'un DAG, la configuration des propriétés d'un DAG, la création de copies de bases de données de boîtes aux lettres et leur surveillance et sur les permutations de serveurs et de bases de données, consultez la rubrique [Gestion de la haute disponibilité et de la résilience de site](managing-high-availability-and-site-resilience-exchange-2013-help.md).

## Modèles de quorum d’un groupe de disponibilité de base de données (DAG)

Un cluster de basculement de Windows se trouve sous chaque DAG. Les clusters de basculement utilisent le concept de quorum, qui utilise lui-même un consensus de votants pour assurer que seul un sous-ensemble des membres du cluster (ce qui pourrait signifier tous les membres ou une majorité des membres) fonctionne à la fois. Le quorum n'est pas un nouveau concept pour Exchange 2013. Les serveurs de boîtes aux lettres à haut niveau de disponibilité dans les versions précédentes d'Exchange utilisent aussi les clusters de basculement et le concept du quorum. Le quorum représente une vue partagée des membres et des ressources, et le terme quorum est également utilisé pour décrire les données physiques représentant la configuration au sein du cluster partagé entre plusieurs membres du cluster. Les clusters de basculement de tous les groupes de disponibilité de base de données doivent donc avoir un quorum. Si le cluster perd son quorum, toutes les opérations du DAG se terminent et toutes les bases de données montées qui sont hébergées dans le DAG sont démontées. Dans ce cas, une intervention de l'administrateur est nécessaire pour corriger le problème du quorum et restaurer les opérations du DAG.

Le quorum est important pour assurer la cohérence, départager pour éviter le partitionnement, et réduire le temps de réponse des clusters :

  - **Assurer la cohérence**   Une exigence cruciale pour un cluster de basculement de Windows est que chacun des membres garde toujours une vue du cluster qui est cohérente avec celle des autres membres. La ruche de cluster agit comme le référentiel définitif pour toutes les informations de configuration relatives au cluster. Si la ruche de cluster ne peut pas être chargée localement sur un membre DAG, le service de cluster ne démarre pas car il n'est pas en mesure de garantir que le membre satisfait à l'exigence d'avoir une vue du cluster qui est cohérente avec celle des autres membres.

  - **Départager**   Une ressource de témoin de quorum est utilisée dans les DAG avec un nombre pair de membres afin d'éviter les scénarios de Split-Brain Syndrome et pour s'assurer qu'un seul ensemble de membres de la DAG est considéré comme étant officiel. Quand le serveur témoin devient nécessaire pour le quorum, tout membre du DAG qui peut communiquer avec le serveur témoin peut placer un SMB (Server Message Block) dans le fichier witness.log du serveur témoin. Le membre du DAG qui verrouille le serveur témoin (appelé le *nœud de verrouillage*) conserve un vote supplémentaire pour le quorum. Les membres du DAG en contact avec le nœud de verrouillage sont majoritaires et conservent le quorum. Les membres du DAG qui ne peuvent pas communiquer avec le nœud de verrouillage sont minoritaires et perdent ainsi le quorum.

  - **Réduire le temps de réponse**   Pour assurer la réactivité, le modèle de quorum vérifie que, chaque fois que le cluster s'exécute, un nombre suffisant de membres du système distribué sont opérationnels et aptes à communiquer, et qu'au moins une réplique de l'état actuel du cluster peut être garantie. Aucun délai supplémentaire n'est nécessaire pour que les membres entrent en communication ou pour déterminer si une réplique spécifique est garantie.

Les DAG comportant un nombre pair de membres utilisent le mode de quorum de nœuds et de partage de fichiers majoritaire du cluster de basculement. Ce mode fait appel à un serveur témoin externe pour départager. Dans ce mode de quorum, chaque membre du DAG obtient un vote. En outre, le serveur témoin est utilisé pour donner à un membre du DAG un vote pondéré (il obtient, par exemple, deux votes au lieu d'un). Les données du quorum du cluster sont stockées par défaut sur le disque système de chaque membre du DAG et leur cohérence est maintenue sur l'ensemble de ces disques. Toutefois, aucune copie des données du quorum n'est stockée sur le serveur témoin. Un fichier sur le serveur témoin est utilisé pour surveiller quel membre a la copie la plus récente des données, mais le serveur témoin ne possède pas de copie des données du quorum du cluster. Dans ce mode, une majorité des votants (les membres du DAG plus le serveur témoin) doivent être opérationnels et aptes à communiquer les uns avec les autres pour conserver le quorum. Si une majorité des votants ne peuvent pas communiquer entre eux, le cluster sous-jacent du DAG perd le quorum et le DAG nécessitera une intervention de l'administrateur pour redevenir opérationnel.

Les DAG comportant un nombre impair de membres utilisent le mode de quorum Nœud majoritaire du cluster de basculement. Dans ce mode, chaque membre obtient un vote et le disque système local de chaque membre est utilisé pour stocker les données du quorum du cluster. Si la configuration du DAG change, cette modification est apportée sur les différents disques. La modification est considérée comme validée ou rendue permanente uniquement si elle est apportée sur les disques de la moitié des membres (arrondis à la valeur inférieure) plus un. Par exemple, dans un DAG composé de cinq membres, la modification doit être effectuée sur deux membres plus un, ou un total de trois membres.

Le quorum requiert qu'une majorité des votants soient aptes à communiquer les uns avec les autres. Prenons un DAG constitué de quatre membres. Du fait que ce DAG possède un nombre pair de membres, un serveur témoin externe est utilisé pour accorder à l'un des membres du cluster un cinquième vote de départage. Pour conserver une majorité des votants (et donc le quorum), trois votants minimum doivent être aptes à communiquer les uns avec les autres. À tout moment, jusqu'à deux votants peuvent être déconnectés sans perturber les services et l'accès aux données. Si trois votants ou plus sont déconnectés, le DAG perd le quorum, et le service et l'accès aux données sont interrompus tant que vous n'aurez pas résolu le problème.

Retour au début

## Utilisation d’un groupe de disponibilité de base de données (DAG) pour la haute disponibilité

Pour montrer de quelle manière un DAG permet d'assurer un haut niveau de disponibilité des bases de données de boîtes aux lettres, prenons l'exemple suivant, dans lequel un DAG comporte cinq membres. L'illustration suivante représente ce DAG.

**DAG comportant cinq membres**

![Groupe de disponibilité de base de données (DAG)](images/Dd979799.21fcbf7b-cb10-49c0-8e32-bdf3c03f825d(EXCHG.150).gif "Groupe de disponibilité de base de données (DAG)")

Dans l'illustration précédente, les bases de données vertes sont des copies de bases de données de boîtes aux lettres actives et les bases de données bleues sont des copies de bases de données de boîtes aux lettres passives. Dans cet exemple, les copies de bases de données ne sont pas répliquées de manière identique sur chaque serveur, elles sont réparties sur plusieurs serveurs. Ainsi, deux serveurs ne comportent pas le même ensemble de copies de bases de données, ce qui rend le DAG plus résilient aux pannes, notamment les pannes qui se produisent lorsque d'autres composants sont indisponibles pour des raisons de maintenance.

Examinons le scénario suivant, basé sur l'exemple précédent, qui illustre la résilience à plusieurs pannes de base de données et de serveur.

Au départ, tous les serveurs et bases de données sont en bon état de fonctionnement. Comme vous devez installer certaines mises à jour de système d'exploitation sur EX2, vous mettez le serveur en mode maintenance. Cela entraîne une permutation de serveur, qui active la copie de DB4 sur un autre serveur de boîtes aux lettres. Une permutation de serveur fait passer toutes les copies des bases de données de boîtes aux lettres d'un serveur vers d'autres serveurs de boîtes aux lettres du DAG en vue d'une mise hors service programmée de ce serveur. Dans cet exemple, une seule base de données de boîtes aux lettres est active sur EX2 (DB4), par conséquent, une seule copie de base de données active est déplacée.

**DAG avec un serveur déconnecté pour des raisons de maintenance**

![Groupe de disponibilité de base de données (DAG) avec un serveur hors ligne](images/Dd979799.f48f0e77-80e1-4f14-8c36-112393895bdc(EXCHG.150).gif "Groupe de disponibilité de base de données (DAG) avec un serveur hors ligne")

Lorsque vous procédez à la maintenance du serveur EX2, EX3 subit une panne matérielle catastrophique et est déconnecté. Avant d'être déconnecté, le serveur EX3 hébergeait la copie active de DB2. Pour récupérer la base de données DB2 à la suite de la panne, le système active automatiquement la copie de DB2 qui est hébergée sur EX1 dans un délai de 30 secondes. Cela est montré dans l'illustration suivante.

**DAG avec un serveur hors ligne pour des raisons de maintenance et un serveur défaillant**

![Groupe de disponibilité de la base de données avec un serveur hors ligne et un serveur défaillant](images/Dd979799.9bbfd9e7-3881-4957-ae8d-32318cbc208b(EXCHG.150).gif "Groupe de disponibilité de la base de données avec un serveur hors ligne et un serveur défaillant")

Une fois la maintenance programmée menée à bien pour EX2, vous mettez le serveur en ligne et le retirez du mode maintenance. Dès qu'EX2 est disponible, les autres membres du DAG en sont notifiés et les copies de DB1, DB4 et DB5 qui sont hébergées sur EX2 sont automatiquement synchronisées avec la copie active de chaque base de données. Cela est montré dans l'illustration suivante.

**DAG avec un serveur restauré synchronisant ses copies de bases de données**

![Groupe de disponibilité de la base de données avec bases de données de resynchronisation de serveurs restaurées](images/Dd979799.58601531-e078-41d3-9287-e8e470ef7f41(EXCHG.150).gif "Groupe de disponibilité de la base de données avec bases de données de resynchronisation de serveurs restaurées")

Une fois que le composant matériel tombé en panne dans EX3 a été remplacé par un nouveau composant, EX3 est mis en ligne. Dès qu'EX3 est disponible, les autres membres du DAG en sont notifiés et les copies de DB2, DB3 et DB4 qui sont hébergées sur EX3 sont automatiquement synchronisées avec la copie active de chaque base de données. Cela est montré dans l'illustration suivante.

**DAG avec un serveur réparé synchronisant ses copies de bases de données**

![Groupe de disponibilité de la base de données avec copies de bases de données de resynchronisation membres](images/Dd979799.56259671-e840-4cf0-9ea2-3657dc36c035(EXCHG.150).gif "Groupe de disponibilité de la base de données avec copies de bases de données de resynchronisation membres")

Retour au début

## Utilisation d’un groupe de disponibilité de base de données (DAG) pour la résilience de site

En plus d'assurer un haut niveau de disponibilité dans un centre de données, un DAG peut également être étendu à d'autres centres de données dans une configuration qui en garantit la résilience de site. Dans les illustrations des exemples précédents, le DAG est situé dans un seul centre de données et un seul site Active Directory. Le déploiement incrémentiel peut être utilisé pour étendre ce DAG à un second centre de données (et un second site Active Directory) en déployant un serveur de boîtes aux lettres et les ressources nécessaires (un ou plusieurs serveurs Active Directory, ainsi que des services DNS). Le serveur de boîte aux lettres est ensuite ajouté au DAG, comme illustré dans la figure suivante.

**Groupe de disponibilité de la base de données étendu à deux sites Active Directory**

![Groupe de disponibilité de la base de données étendu à deux sites Active Directory](images/Dd979799.28e96e9d-d7d6-451a-b7b8-c06122c81dc9(EXCHG.150).gif "Groupe de disponibilité de la base de données étendu à deux sites Active Directory")

Dans cet exemple, une copie passive de chaque base de données active du centre de données de Redmond est configurée sur EX6 dans le centre de données de Dublin. Toutefois, de nombreux autres exemples de configurations DAG fournissent une résilience de site. Par exemple :

  - Au lieu d'héberger seulement des copies de base de données passives, EX6 pourrait héberger toutes les copies actives, ou il pourrait héberger un mélange de copies actives et passives.

  - En plus d'EX6, plusieurs membres de DAG pourraient être déployés dans le centre de données de Dublin pour assurer la protection contre les défaillances supplémentaires. Cette configuration fournit également une capacité supplémentaire, de sorte que si le centre de données de Redmond tombe en panne, celui de Dublin peut prendre en charge une population d'utilisateurs beaucoup plus importante.

## Utilisation de plusieurs groupes de disponibilité de base de données (DAG) pour la résilience de site

Dans l'exemple précédent, un seul DAG s'étend sur plusieurs centres de données, offrant la résilience de site pour l'un des centres de données ou les deux à la fois. Quand on utilise un seul DAG afin de fournir la résilience de site dans un environnement où chaque centre de données auquel vous étendez le DAG a une population d'utilisateurs actifs, il y a un point unique de défaillance dans la connexion de réseau étendu (WAN). Ceci est dû au fait que le quorum requiert qu'une majorité des votants soient aptes à communiquer les uns avec les autres.

Dans l'exemple précédent, la majorité des votants sont situés dans le centre de données de Redmond. Si le centre de données de Dublin héberge des bases de données de boîtes aux lettres actives et s'il a une population d'utilisateurs locaux, une panne du réseau étendu entraînerait l'interruption du service de messagerie pour les utilisateurs de Dublin. Lorsque la connectivité du réseau étendu est rompue, seuls les membres du DAG dans le centre de données de Redmond conservent le quorum et continuent d'offrir le service de messagerie.

Pour résoudre le problème du réseau étendu comme seul point de défaillance lorsque vous devez fournir la résilience de site pour plusieurs centres de données ayant chacun une population d'utilisateurs actifs, vous devez déployer plusieurs DAG dont chacune possède une majorité de votants dans un centre de données distinct. Lorsqu'une panne du réseau étendu survient, la réplication est bloquée jusqu'à ce que la connectivité soit restaurée. Les utilisateurs disposent du service de messagerie car chaque DAG continue de servir sa population d'utilisateurs locaux.

Retour au début

