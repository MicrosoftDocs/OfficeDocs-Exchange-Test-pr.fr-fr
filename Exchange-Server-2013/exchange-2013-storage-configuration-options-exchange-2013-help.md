---
title: 'Options de configuration du stockage Exchange 2013: Exchange 2013 Help'
TOCTitle: Options de configuration du stockage Exchange 2013
ms:assetid: 37cdeacf-74f9-4399-9860-4d1dbec12bb1
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Ee832792(v=EXCHG.150)
ms:contentKeyID: 50477906
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Options de configuration du stockage Exchange 2013

 

_**Sapplique à :**Exchange Online, Exchange Server, Exchange Server 2013_

_**Dernière rubrique modifiée :**2016-12-09_

La compréhension des options et des besoins de stockage pour le rôle serveur de boîtes aux lettres dans Microsoft Exchange Server 2013 constitue un aspect vital de votre solution de conception de stockage de serveurs de boîtes aux lettres.

**Contenu de cette rubrique**

Architectures de stockage

Types de disques physiques

Meilleures pratiques pour les configurations de stockage prises en charge

## Architectures de stockage

Le tableau suivant décrit les architectures de stockage prises en charge indique la meilleure pratique pour chaque type d'architecture de stockage, lorsque nécessaire.

### Architectures de stockage prises en charge

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Architecture de stockage</th>
<th>Description</th>
<th>Meilleure pratique</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Solution DAS (Direct-Attached Storage)</p></td>
<td><p>La solution DAS correspond à un système de stockage numérique directement connecté à un serveur ou à un poste de travail, sans réseau de stockage entre les deux. Par exemple, les transports assurés par une solution DAS incluent les interfaces SAS (Serial Attached SCSI) et ATA (Serial Attached Advanced Technology Attachment).</p></td>
<td><p>Non disponible.</p></td>
</tr>
<tr class="even">
<td><p>Réseau SAN (Storage Area Network) : Internet Small Computer System Interface (iSCSI)</p></td>
<td><p>L'architecture SAN permet de relier des périphériques de stockage distants (tels que des bases de disques et des bibliothèques de bandes) à des serveurs de sorte que ces périphériques semblent être connectés en local au système d'exploitation (par exemple, mémoire de blocs). Les réseaux SAN iSCSI (Internet Small Computer System Interface) encapsulent les commandes SCSI dans des paquets IP et utilisent les infrastructures de réseau courantes comme interface de transport de stockage (par exemple, Ethernet).</p></td>
<td><p>Ne partagez pas les disques physiques opérant des sauvegardes de données Exchange avec d’autres applications.</p>
<p>Utilisez des réseaux de stockage dédiés.</p>
<p>Utilisez plusieurs chemins d'accès réseau pour les configurations autonomes.</p></td>
</tr>
<tr class="odd">
<td><p>Réseau SAN : Fibre Channel</p></td>
<td><p>Les réseaux SAN Fibre Channel encapsulent les commandes SCSI dans des paquets Fibre Channel et utilisent généralement des réseaux Fibre Channel spécialisés comme interface de transport de stockage.</p></td>
<td><p>Ne partagez pas les disques physiques opérant des sauvegardes de données Exchange avec d’autres applications.</p>
<p>Utilisez plusieurs chemins d'accès réseau Fibre Channel pour les configurations autonomes.</p>
<p>Appliquez les meilleures pratiques des fabricants de solutions de stockage pour régler les adaptateurs de bus hôte Fibre Channel (HBA), par exemple, Queue Depth et Queue Target.</p></td>
</tr>
</tbody>
</table>


Un boîtier NAS (network-attached storage) est un ordinateur autonome relié à un réseau et servant exclusivement à fournir des services de stockage de fichiers de données à d'autres périphériques du réseau. Le système d'exploitation et les autres logiciels du boîtier NAS fournissent les fonctionnalités nécessaires au stockage de données, aux systèmes de fichiers et d'accès aux fichiers ainsi que la gestion de ces fonctionnalités (par exemple, stockage de fichiers).

Tout l’espace de stockage utilisé par Exchange pour le stockage de données Exchange doit être un stockage au niveau du bloc, car Exchange 2013 ne prend pas en charge l’utilisation des volumes NAS (Network Attached Storage) autres que dans le scénario SMB 3.0 indiqué plus loin dans la rubrique [Virtualisation d'Exchange 2013](exchange-2013-virtualization-exchange-2013-help.md). En outre, dans un environnement virtualisé, le stockage NAS qui est présenté à l’invité en tant que stockage au niveau du bloc via l’hyperviseur n’est pas pris en charge.

L'utilisation de niveaux de stockage n'est pas recommandé, car ils peuvent affecter négativement les performances du système. Pour cette raison, n'autorisez pas le contrôleur de stockage à déplacer automatiquement les fichiers les plus utilisés vers le stockage « plus rapide ».

Architectures de stockage

## Types de disques physiques

Le tableau suivant fournit une liste de types de disque physique pris en charge et indique la meilleure pratique pour chaque type de disque physique quand cela est nécessaire.

### Types de disque physique pris en charge

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Type de disque physique</th>
<th>Description</th>
<th>Pris en charge ou meilleure pratique</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Serial ATA (SATA)</p></td>
<td><p>SATA est une interface série pour les disques ATA et IDE (Integrated Device Electronics). Les disques SATA sont disponibles avec des facteurs de forme, vitesses et capacités variés.</p>
<p>De manière générale, choisissez des disques SATA pour le stockage des boîtes aux lettres Exchange 2013 lorsque vos impératifs de conception sont les suivants :</p>
<ul>
<li><p>Grande capacité</p></li>
<li><p>Performances moyennes</p></li>
<li><p>Consommation d'énergie modérée</p></li>
</ul></td>
<td><p>Prise en charge : disques avec secteur de 512 octets pour Windows Server 2008 et Windows Server 2008 R2. En outre, les disques 512e sont pris en charge pour Windows Server 2008 R2 avec ce qui suit :</p>
<ul>
<li><p>Le correctif logiciel décrit dans l’<a href="https://go.microsoft.com/fwlink/p/?linkid=3052%26kbid=982018">article 982018 de la Base de connaissances Microsoft</a>, « Une mise à jour améliorant la compatibilité de Windows 7 et Windows Server 2008 R2 avec les disques au format avancé est disponible ».</p></li>
<li><p>Windows Server 2008 R2 avec Service Pack 1 (SP1) et Exchange Server 2010 SP1.</p></li>
</ul>
<p>Exchange 2013 et versions ultérieures prend en charge les disques avec secteur natifs de 4 kilo-octets (Ko) et les disques 512e. La prise en charge nécessite que toutes les copies d’une base de données résident sur le même type de disque physique. Par exemple, une configuration avec une copie d’une base de données sur un disque avec secteur de 512 octets et une autre copie de cette même base de données sur un disque 512e ou un disque 4K n’est pas prise en charge.</p>
<p>Meilleure pratique : Optez pour des disques SATA de type entreprise qui offrent généralement de meilleures caractéristiques de fiabilité et de résistance à la chaleur et aux vibrations.</p></td>
</tr>
<tr class="even">
<td><p>Serial Attached SCSI</p></td>
<td><p>Serial Attached SCSI est une interface série pour les disques SCSI. Les disques Serial Attached SCSI sont disponibles avec des facteurs de forme, vitesses et capacités variés.</p>
<p>De manière générale, choisissez des disques Serial Attached SCSI pour le stockage des boîtes aux lettres Exchange 2013 lorsque vos impératifs de conception sont les suivants :</p>
<ul>
<li><p>Moyenne capacité</p></li>
<li><p>Hautes performances</p></li>
<li><p>Consommation d'énergie modérée</p></li>
</ul></td>
<td><p>Prise en charge : disques avec secteur de 512 octets pour Windows Server 2008 et Windows Server 2008 R2. En outre, les disques 512e sont pris en charge pour Windows Server 2008 R2 avec ce qui suit :</p>
<ul>
<li><p>Le correctif logiciel décrit dans l’<a href="https://go.microsoft.com/fwlink/p/?linkid=3052%26kbid=982018">article 982018 de la Base de connaissances Microsoft</a>, « Une mise à jour améliorant la compatibilité de Windows 7 et Windows Server 2008 R2 avec les disques au format avancé est disponible ».</p></li>
<li><p>Windows Server 2008 R2 avec Service Pack 1 (SP1) et Exchange Server 2010 SP1.</p></li>
</ul>
<p>Exchange 2013 et versions ultérieures prend en charge les disques avec secteur natifs de 4 kilo-octets (Ko) et les disques 512e. La prise en charge nécessite que toutes les copies d’une base de données résident sur le même type de disque physique. Par exemple, une configuration avec une copie d’une base de données sur un disque avec secteur de 512 octets et une autre copie de cette même base de données sur un disque 512e ou un disque 4K n’est pas prise en charge.</p>
<p>Meilleure pratique : La mise en cache des écritures sur disque physique doit être désactivée en cas d'utilisation sans onduleur.</p></td>
</tr>
<tr class="odd">
<td><p>Fibre Channel</p></td>
<td><p>Fibre Channel est une interface électrique servant à connecter des réseaux SAN utilisant la technologie Fibre Channel. Les disques Fibre Channel sont disponibles dans un grand choix de capacités et vitesses.</p>
<p>De manière générale, choisissez des disques Fibre Channel pour le stockage des boîtes aux lettres Exchange 2013 lorsque vos impératifs de conception sont les suivants :</p>
<ul>
<li><p>Moyenne capacité</p></li>
<li><p>Hautes performances</p></li>
<li><p>Connectivité SAN</p></li>
</ul></td>
<td><p>Prise en charge : disques avec secteur de 512 octets pour Windows Server 2008 et Windows Server 2008 R2. En outre, les disques 512e sont pris en charge pour Windows Server 2008 R2 avec ce qui suit :</p>
<ul>
<li><p>Le correctif logiciel décrit dans l’<a href="https://go.microsoft.com/fwlink/p/?linkid=3052%26kbid=982018">article 982018 de la Base de connaissances Microsoft</a>, « Une mise à jour améliorant la compatibilité de Windows 7 et Windows Server 2008 R2 avec les disques au format avancé est disponible ».</p></li>
<li><p>Windows Server 2008 R2 avec Service Pack 1 (SP1) et Exchange Server 2010 SP1.</p></li>
</ul>
<p>Exchange 2013 et versions ultérieures prend en charge les disques avec secteur natifs de 4 kilo-octets (Ko) et les disques 512e. La prise en charge nécessite que toutes les copies d’une base de données résident sur le même type de disque physique. Par exemple, une configuration avec une copie d’une base de données sur un disque avec secteur de 512 octets et une autre copie de cette même base de données sur un disque 512e ou un disque 4K n’est pas prise en charge.</p>
<p>Meilleure pratique : La mise en cache des écritures sur disque physique doit être désactivée en cas d'utilisation sans onduleur.</p></td>
</tr>
<tr class="even">
<td><p>Lecteur à semi-conducteurs (SSD) (disque flash)</p></td>
<td><p>Un SSD est un périphérique de stockage des données qui utilise une mémoire à semi-conducteurs pour stocker les données persistantes. Un SSD émule une interface de lecteur de disque dur. Les disques SSD sont proposés dans une multitude de vitesses (diverses performances d'entrées/sorties) et de capacités.</p>
<p>De manière générale, choisissez des disques SSD pour le stockage des boîtes aux lettres Exchange 2013 lorsque vos impératifs de conception sont les suivants :</p>
<ul>
<li><p>Faible capacité</p></li>
<li><p>Performances très élevées</p></li>
</ul></td>
<td><p>Prise en charge : disques avec secteur de 512 octets pour Windows Server 2008 et Windows Server 2008 R2. En outre, les disques 512e sont pris en charge pour Windows Server 2008 R2 avec ce qui suit :</p>
<ul>
<li><p>Le correctif logiciel décrit dans l’<a href="https://go.microsoft.com/fwlink/p/?linkid=3052%26kbid=982018">article 982018 de la Base de connaissances Microsoft</a>, « Une mise à jour améliorant la compatibilité de Windows 7 et Windows Server 2008 R2 avec les disques au format avancé est disponible ».</p></li>
<li><p>Windows Server 2008 R2 avec Service Pack 1 (SP1) et Exchange Server 2010 SP1.</p></li>
</ul>
<p>Exchange 2013 et versions ultérieures prend en charge les disques avec secteur natifs de 4 kilo-octets (Ko) et les disques 512e. La prise en charge nécessite que toutes les copies d’une base de données résident sur le même type de disque physique. Par exemple, une configuration avec une copie d’une base de données sur un disque avec secteur de 512 octets et une autre copie de cette même base de données sur un disque 512e ou un disque 4K n’est pas prise en charge.</p>
<p>Meilleure pratique : La mise en cache des écritures sur disque physique doit être désactivée en cas d'utilisation sans onduleur.</p>
<p>En général, les serveurs de boîtes aux lettres Exchange 2013 n’exigent pas les caractéristiques de performances fournies par un stockage SSD.</p></td>
</tr>
</tbody>
</table>


## Facteurs à prendre en compte lors du choix des types de disques

Il existe plusieurs compromis lors du choix des types de disques pour le stockage Exchange 2013. Le bon disque est celui offrant le bon équilibre entre performance (séquentielle et aléatoire), capacité, fiabilité, consommation d'énergie et coût. Le tableau suivant récapitule les types de disque physique pris en charge et fournit des informations pour vous guider dans votre choix.

D'un point de vue des performances, l'utilisation de disques de grande taille, plus lents, pour le stockage Exchange est acceptable, à condition que les disques puissent maintenir une latence moyenne de lecture et d'écriture latence de 20 ms au maximum sous charge.

### Facteurs à prendre en compte pour choisir un type de disque

<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>Vitesse de disque (TPM)</th>
<th>Facteur de forme de disque</th>
<th>Interface ou transport</th>
<th>Capacité</th>
<th>Performances d'E/S aléatoires</th>
<th>Performances d'E/S séquentielles</th>
<th>Consommation d'énergie</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>5 400</p></td>
<td><p>2,5 pouces</p></td>
<td><p>SATA</p></td>
<td><p>Moyenne</p></td>
<td><p>Médiocre</p></td>
<td><p>Médiocre</p></td>
<td><p>Excellente</p></td>
</tr>
<tr class="even">
<td><p>5 400</p></td>
<td><p>3,5 pouces</p></td>
<td><p>SATA</p></td>
<td><p>Excellente</p></td>
<td><p>Médiocre</p></td>
<td><p>Médiocre</p></td>
<td><p>Au-dessus de la moyenne</p></td>
</tr>
<tr class="odd">
<td><p>7 200</p></td>
<td><p>2,5 pouces</p></td>
<td><p>SATA</p></td>
<td><p>Moyenne</p></td>
<td><p>Moyenne</p></td>
<td><p>Moyenne</p></td>
<td><p>Excellente</p></td>
</tr>
<tr class="even">
<td><p>7 200</p></td>
<td><p>2,5 pouces</p></td>
<td><p>Serial Attached SCSI</p></td>
<td><p>Moyenne</p></td>
<td><p>Moyenne</p></td>
<td><p>Au-dessus de la moyenne</p></td>
<td><p>Excellente</p></td>
</tr>
<tr class="odd">
<td><p>7 200</p></td>
<td><p>3,5 pouces</p></td>
<td><p>SATA</p></td>
<td><p>Excellente</p></td>
<td><p>Moyenne</p></td>
<td><p>Au-dessus de la moyenne</p></td>
<td><p>Au-dessus de la moyenne</p></td>
</tr>
<tr class="even">
<td><p>7 200</p></td>
<td><p>3,5 pouces</p></td>
<td><p>Serial Attached SCSI</p></td>
<td><p>Excellente</p></td>
<td><p>Moyenne</p></td>
<td><p>Au-dessus de la moyenne</p></td>
<td><p>Au-dessus de la moyenne</p></td>
</tr>
<tr class="odd">
<td><p>7 200</p></td>
<td><p>3,5 pouces</p></td>
<td><p>Fibre Channel</p></td>
<td><p>Excellente</p></td>
<td><p>Moyenne</p></td>
<td><p>Au-dessus de la moyenne</p></td>
<td><p>Moyenne</p></td>
</tr>
<tr class="even">
<td><p>10 000</p></td>
<td><p>2,5 pouces</p></td>
<td><p>Serial Attached SCSI</p></td>
<td><p>En dessous de la moyenne</p></td>
<td><p>Excellente</p></td>
<td><p>Au-dessus de la moyenne</p></td>
<td><p>Au-dessus de la moyenne</p></td>
</tr>
<tr class="odd">
<td><p>10 000</p></td>
<td><p>3,5 pouces</p></td>
<td><p>SATA</p></td>
<td><p>Moyenne</p></td>
<td><p>Moyenne</p></td>
<td><p>Au-dessus de la moyenne</p></td>
<td><p>Au-dessus de la moyenne</p></td>
</tr>
<tr class="even">
<td><p>10 000</p></td>
<td><p>3,5 pouces</p></td>
<td><p>Serial Attached SCSI</p></td>
<td><p>Moyenne</p></td>
<td><p>Au-dessus de la moyenne</p></td>
<td><p>Au-dessus de la moyenne</p></td>
<td><p>En dessous de la moyenne</p></td>
</tr>
<tr class="odd">
<td><p>10 000</p></td>
<td><p>3,5 pouces</p></td>
<td><p>Fibre Channel</p></td>
<td><p>Moyenne</p></td>
<td><p>Au-dessus de la moyenne</p></td>
<td><p>Au-dessus de la moyenne</p></td>
<td><p>En dessous de la moyenne</p></td>
</tr>
<tr class="even">
<td><p>15 000</p></td>
<td><p>2,5 pouces</p></td>
<td><p>Serial Attached SCSI</p></td>
<td><p>Médiocre</p></td>
<td><p>Excellente</p></td>
<td><p>Excellente</p></td>
<td><p>Moyenne</p></td>
</tr>
<tr class="odd">
<td><p>15 000</p></td>
<td><p>3,5 pouces</p></td>
<td><p>Serial Attached SCSI</p></td>
<td><p>Moyenne</p></td>
<td><p>Excellente</p></td>
<td><p>Excellente</p></td>
<td><p>En dessous de la moyenne</p></td>
</tr>
<tr class="even">
<td><p>15 000</p></td>
<td><p>3,5 pouces</p></td>
<td><p>Fibre Channel</p></td>
<td><p>Moyenne</p></td>
<td><p>Excellente</p></td>
<td><p>Excellente</p></td>
<td><p>Médiocre</p></td>
</tr>
<tr class="odd">
<td><p>SSD : de type entreprise</p></td>
<td><p>Non applicable</p></td>
<td><p>SATA, Serial Attached SCSI, Fibre Channel</p></td>
<td><p>Médiocre</p></td>
<td><p>Excellente</p></td>
<td><p>Excellente</p></td>
<td><p>Excellente</p></td>
</tr>
</tbody>
</table>


Architectures de stockage

## Meilleures pratiques pour les configurations de stockage prises en charge

Cette section présente les meilleures pratiques relatives aux configurations de disques et contrôleurs prises en charge.

La technologie RAID (Redundant Array of Independent Disks) est souvent utilisée pour améliorer à la fois les caractéristiques de performance des disques individuels (par l'agrégation des données entre les disques) et pour offrir une protection contre les défaillances des disques. En raison des avancées apportées à la haute disponibilité par Exchange 2013, les composants RAID ne sont pas indispensables à une création de stockage Exchange 2013. Cependant, les composants RAID sont toujours essentiels pour la création de stockage Exchange 2013 pour des serveurs autonomes ainsi que des solutions qui nécessitent une tolérance de panne de stockage.

**Système d’exploitation, système ou volume de fichiers d’échange**

La configuration recommandée pour un système d’exploitation, un système ou un volume de fichier d’échange consiste à utiliser la technologie RAID pour protéger ce type de données. La configuration RAID recommandée est RAID-1 ou RAID-1/0, mais tous les types RAID sont pris en charge.

**Volumes distincts de base de données de boîtes aux lettres et de fichiers journaux**

Si vous déployez une architecture de rôle serveur de boîtes aux lettres autonome, la technologie RAID est obligatoire pour les volumes de base de données de boîtes aux lettres et de fichiers journaux. La configuration RAID recommandée pour les volumes de boîte aux lettres est RAID-1/0 (surtout si vous utilisez des disques de 5,4 Ko ou 7,2 Ko), mais tous les types RAID sont pris en charge. Pour les volumes de fichiers journaux, la configuration RAID recommandée est RAID-1 ou RAID-1/0.

Lorsque vous utilisez les configurations RAID-5 ou RAID-6 pour le système d’exploitation, le fichier d’échange ou les volumes de données Exchange, tenez comptes des points suivants :

  - Les configurations RAID-5, y compris les variantes telles que RAID-50 et RAID-51, ne doivent pas comporter plus de 7 disques par groupe de baies. Les fonctions d’analyse de surface et de nettoyage haute priorité ne doivent pas être activées pour le contrôleur de baie.

  - Pour les configurations RAID-6, les fonctions d’analyse de surface et de nettoyage haute priorité doivent être activées pour le contrôleur de baie.

Bien que JBOD soit pris en charge dans les architectures de haute disponibilité comportant au moins 3 copies de base de données à haute disponibilité (les volumes de base de données de boîtes aux lettres et de fichiers journaux étant distincts), JBOD n’est pas recommandé.

**Colocalisation des volumes de base de données de boîtes aux lettres et de fichiers journaux**

La colocalisation des volumes de base de données de boîtes aux lettres et de fichiers journaux n’est pas recommandée dans les architectures autonomes. Il existe deux possibilités pour ce scénario dans les architectures de haute disponibilité :

1.  Base de données unique par volume

2.  Plusieurs bases de données par volume

**Base de données unique par volume**

Du point de vue d’Exchange, JBOD permet de stocker la base de données et les journaux correspondants sur un même disque. Pour un déploiement sur un système de stockage JBOD, vous devez déployer au moins trois copies de base de données à haute disponibilité. L’utilisation d’un seul disque est un point de défaillance unique, car en cas de défaillance du disque, la copie de base de données qui réside sur ce dernier est perdue. En prévoyant au moins trois copies de base de données, vous garantissez une meilleure tolérance aux pannes, car vous disposez de deux copies supplémentaires en cas de défaillance de la copie (ou du disque). Toutefois, l’emplacement de trois copies de base de données à haute disponibilité, ainsi que l’utilisation de copies de base de données retardées, peut avoir des conséquences sur la conception de stockage. Le tableau suivant résume les recommandations concernant les aspects de RAID ou de JDOB à prendre en compte.

### Aspects de RAID ou JBOD à prendre en compte

<table style="width:100%;">
<colgroup>
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
</colgroup>
<thead>
<tr class="header">
<th>Serveurs de centre de données</th>
<th>Deux copies hautement disponibles (total)</th>
<th>Trois copies hautement disponibles (total)</th>
<th>Au moins deux copies hautement disponibles par centre de données</th>
<th>Une copie retardée</th>
<th>Au moins deux copies retardées par centre de données</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Serveurs de centre de données principal</p></td>
<td><p>RAID</p></td>
<td><p>RAID ou JBOD (2 copies)</p></td>
<td><p>RAID ou JBOD</p></td>
<td><p>RAID</p></td>
<td><p>RAID ou JBOD</p></td>
</tr>
<tr class="even">
<td><p>Serveurs de centre de données secondaire</p></td>
<td><p>RAID</p></td>
<td><p>RAID (1 copie)</p></td>
<td><p>RAID ou JBOD</p></td>
<td><p>RAID</p></td>
<td><p>RAID ou JBOD</p></td>
</tr>
</tbody>
</table>


Pour un déploiement sur le système JDOB avec les serveurs du centre de données principal, le groupe de disponibilité de base de données doit inclure au moins trois copies de base de données à haute disponibilité. Si vous associez des copies retardées sur le même serveur hébergeant des copies de base de données à haute disponibilité (en n’utilisant pas de serveurs de copie de base de données retardée dédiés, par exemple), vous avez au moins besoin de deux copies de base de données retardées.

Pour que les serveurs du centre de données secondaire utilisent JDOB, le centre doit au moins compter deux copies de base de données à haute disponibilité. La perte d’une copie dans le centre de données secondaire ne vous obligera pas à effectuer un réamorçage sur le réseau étendu ou à avoir un point de défaillance unique en cas d’activation du centre de données secondaire. Si vous associez des copies de base de données retardées sur le même serveur hébergeant des copies de base de données à haute disponibilité (en n’utilisant pas de serveurs de copie de base de données retardée dédiés, par exemple), vous nécessitez au moins deux copies de base de données retardées.

Pour les serveurs de copie de base de données retardée dédiés, vous devez ajouter au moins deux copies de base de données retardées dans un centre de données pour pouvoir utiliser JDOB. Sinon, la perte du disque entraîne la perte de la copie de base de données retardée, ainsi que la perte du mécanisme de protection.

**Plusieurs bases de données par volume**

La configuration de plusieurs bases de données par volume est un nouveau scénario JBOD disponible dans Exchange 2013. Celui-ci permet de mélanger les copies actives et passives (y compris les copies retardées) sur un même disque, afin d’en optimiser l’utilisation. Toutefois, pour déployer des copies retardées de cette manière, l’exécution de la journalisation automatique des copies retardées doit être activée. Le tableau suivant indique les aspects de JBOD à prendre en compte avec plusieurs bases de données par volume.

### Aspects de JBOD à prendre en compte

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Serveurs de centre de données</th>
<th>Au moins 3 copies (total)</th>
<th>Au moins 2 copies par centre de données</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Serveurs de centre de données principal</p></td>
<td><p>JBOD</p></td>
<td><p>JBOD</p></td>
</tr>
<tr class="even">
<td><p>Serveurs de centre de données secondaire</p></td>
<td><p>N/A</p></td>
<td><p>JBOD</p></td>
</tr>
</tbody>
</table>


Le tableau suivant fournit des conseils sur les configurations de groupes de stockage pour Exchange 2013.

### Prise en charge des types RAID pour le rôle serveur de boîtes aux lettres d'Exchange 2013

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Type RAID</th>
<th>Description</th>
<th>Pris en charge ou meilleure pratique</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Baie RAID avec taille de bande (Ko)</p></td>
<td><p>La taille de bande est l'unité de distribution des données par disque au sein d'un ensemble RAID. On parle également de <em>taille de blocs</em>.</p></td>
<td><p>Meilleure pratique : 256 Ko ou supérieur. Respectez les meilleures pratiques du fournisseur de la solution de stockage.</p></td>
</tr>
<tr class="even">
<td><p>Paramètres du cache de la baie de stockage</p></td>
<td><p>Paramètres de cache fournis par un contrôleur de mise en cache avec batterie de secours.</p></td>
<td><p>Meilleure pratique : 100 % de mise en cache en écriture (cache avec Flash ou batterie de secours) pour les contrôleurs de stockage DAS dans une configuration RAID ou JBOD. 75 % de mise en cache en écriture, 25 % en lecture (cache avec Flash ou batterie de secours) pour d’autres types de solutions de stockage comme le SAN. Si votre fournisseur de SAN recommande d’autres meilleures pratiques pour la configuration du cache sur leur plateforme, suivez les instructions de votre fournisseur de SAN.</p></td>
</tr>
<tr class="odd">
<td><p>Mise en cache en écriture du disque physique</p></td>
<td><p>Les paramètres pour la mise en cache sont sur chaque disque individuel.</p></td>
<td><p>Pris en charge : La mise en cache des écritures sur disque physique doit être désactivée en cas d'utilisation sans onduleur.</p></td>
</tr>
</tbody>
</table>


Le tableau suivant fournit des conseils sur les choix de fichier de base de données/journal.

### Choix de fichier de base de données/journal pour le rôle serveur de boîtes aux lettres d'Exchange 2013

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Options de fichier de base de données/journal</th>
<th>Description</th>
<th>Autonome : Pris en charge ou meilleure pratique</th>
<th>Haute disponibilité : Pris en charge ou meilleure pratique</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Placement du fichier : Isolation de la base de données par journal</p></td>
<td><p>L'isolation de la base de données par journal correspond au placement du fichier de la base de données et des journaux appartenant à la même base de données de boîtes aux lettres sur différents volumes sauvegardés sur des disques physiques différents.</p></td>
<td><p>Meilleure pratique : Pour les récupérer, déplacez le fichier (.edb) de base de données et les journaux appartenant à la même base de données vers des volumes différents sauvegardés sur des disques physiques distincts.</p></td>
<td><p>Pris en charge : L'isolation des journaux et bases de données n'est pas obligatoire.</p></td>
</tr>
<tr class="even">
<td><p>Placement du fichier : Fichiers de base de données par volume</p></td>
<td><p>Cette expression désigne la manière dont vous distribuez les fichiers de la base de données dans un volume de disque ou entre des volumes de disques.</p></td>
<td><p>Meilleure pratique : Basée sur votre méthodologie de sauvegarde.</p></td>
<td><p>Pris en charge : si vous utilisez JBOD, créez un volume unique avec des répertoires séparés pour les bases de données et pour les fichiers journaux.</p></td>
</tr>
<tr class="odd">
<td><p>Placement du fichier : Flux de journaux par volume</p></td>
<td><p>Cette expression désigne la manière dont vous distribuez les fichiers journaux de la base de données dans un volume de disque ou entre des volumes de disques.</p></td>
<td><p>Meilleure pratique : Basée sur votre méthodologie de sauvegarde.</p></td>
<td><p>Pris en charge : si vous utilisez JBOD, créez un volume unique avec des répertoires séparés pour les bases de données et pour les fichiers journaux.</p>
<p>Meilleure pratique : si vous utilisez JBOD, profitez de plusieurs bases de données par volume.</p></td>
</tr>
<tr class="even">
<td><p>Taille de la base de données</p></td>
<td><p>Cette expression désigne la taille du fichier (.edb) de base de données de disques.</p></td>
<td><p>Pris en charge : Environ 16 téraoctets.</p>
<p>Meilleure pratique :</p>
<ul>
<li><p>200 gigaoctets (Go) maximum.</p></li>
<li><p>Provision pour 120 % de la taille maximale calculée de la base de données.</p></li>
</ul></td>
<td><p>Pris en charge : Environ 16 téraoctets.</p>
<p>Meilleure pratique :</p>
<ul>
<li><p>2 téraoctets maximum.</p></li>
<li><p>Provision pour 120 % de la taille maximale calculée de la base de données.</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Méthode de troncation de journal</p></td>
<td><p>Processus de troncation et de suppression des anciens fichiers journaux de la base de données. Il existe deux méthodes :</p>
<ul>
<li><p>l’enregistrement circulaire par lequel Exchange supprime les journaux.</p></li>
<li><p>la troncation de journal, laquelle se produit après la réalisation d'une sauvegarde complète ou incrémentielle implémentant le service VSS (Volume Shadow Copy Service).</p></li>
</ul></td>
<td><p>Meilleure pratique :</p>
<ul>
<li><p>Utiliser les sauvegardes de la troncation de journal (par exemple, enregistrement circulaire désactivé).</p></li>
<li><p>Provision pour trois jours de capacité de génération de journal.</p></li>
</ul></td>
<td><p>Meilleure pratique :</p>
<ul>
<li><p>activer l'enregistrement circulaire pour les déploiements qui utilisent les fonctionnalités natives de protection des données d'Exchange.</p></li>
<li><p>Provision pour trois jours après le délai de retard de relecture de la capacité de génération de journal.</p></li>
</ul></td>
</tr>
</tbody>
</table>


Le tableau suivant fournit des conseils à propos des types de disque Windows.

### Types de disque Windows pour le rôle serveur de boîtes aux lettres d'Exchange 2013

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Type de disque Windows</th>
<th>Description</th>
<th>Autonome : Pris en charge ou meilleure pratique</th>
<th>Haute disponibilité : Pris en charge ou meilleure pratique</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Disque de base</p></td>
<td><p>Un disque initialisé pour le stockage de base est appelé disque de base. Un disque de base contient des volumes de base (partitions principales, partitions étendues et lecteurs logiques).</p></td>
<td><p>Pris en charge.</p>
<p>Meilleure pratique : Utilisez des disques de base.</p></td>
<td><p>Pris en charge.</p>
<p>Meilleure pratique : Utilisez des disques de base.</p></td>
</tr>
<tr class="even">
<td><p>Disque dynamique</p></td>
<td><p>Un disque initialisé pour le stockage dynamique est appelé disque dynamique. Un disque dynamique contient des volumes dynamiques (volumes simples, volumes fractionnés, volumes agrégés par bandes, volumes en miroir et volumes RAID-5).</p></td>
<td><p>Pris en charge.</p></td>
<td><p>Pris en charge.</p></td>
</tr>
</tbody>
</table>


Le tableau suivant fournit des conseils sur les configurations de volume.

### Configurations de volume pour le rôle serveur de boîtes aux lettres d'Exchange 2013

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Configuration de volume</th>
<th>Description</th>
<th>Autonome : Pris en charge ou meilleure pratique</th>
<th>Haute disponibilité : Pris en charge ou meilleure pratique</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>table de partition GUID (GPT)</p></td>
<td><p>GPT est une architecture de disques qui s'appuie sur l'ancien schéma de partitionnement MBR (Master boot record). La taille maximale de la partition au format NTFS est de 256 téraoctets.</p></td>
<td><p>Pris en charge.</p>
<p>Meilleure pratique : Utiliser les partitions GPT.</p></td>
<td><p>Pris en charge.</p>
<p>Meilleure pratique : Utiliser les partitions GPT.</p></td>
</tr>
<tr class="even">
<td><p>MBR</p></td>
<td><p>Un MBR (ou secteur de partition) est le secteur d'amorçage de 512 octets qui constitue le premier secteur (LBA Secteur 0) d'un périphérique de stockage de données partitionné tel qu'un disque dur. La taille maximale de la partition au format NTFS est de 2 téraoctets.</p></td>
<td><p>Pris en charge.</p></td>
<td><p>Pris en charge.</p></td>
</tr>
<tr class="odd">
<td><p>Alignement des partitions</p></td>
<td><p>Ce terme fait référence à l'alignement des partitions sur des limites de secteur pour optimiser les performances.</p></td>
<td><p>Pris en charge : Pour Windows Server 2008 R2 et Windows Server 2012, la valeur par défaut est 1 mégaoctet (Mo).</p></td>
<td><p>Pris en charge : Pour Windows Server 2008 R2 et Windows Server 2012, la valeur par défaut est 1 Mo.</p></td>
</tr>
<tr class="even">
<td><p>Chemin d'accès du volume</p></td>
<td><p>Ce terme fait référence au mode d'accès à un volume.</p></td>
<td><p>Pris en charge : Lettre du lecteur ou point de montage.</p>
<p>Meilleure pratique : La fonction RAID doit être activée pour le volume hôte sur le point de montage.</p></td>
<td><p>Pris en charge : Lettre du lecteur ou point de montage.</p>
<p>Meilleure pratique : La fonction RAID doit être activée pour le volume hôte sur le point de montage.</p></td>
</tr>
<tr class="odd">
<td><p>Système de fichiers</p></td>
<td><p>Méthode permettant de stocker et d'organiser les fichiers d'un ordinateur et les données qu'il contient de manière à faciliter leur recherche et leur accès.</p></td>
<td><p>Pris en charge : NTFS et ReFS.</p></td>
<td><p>Pris en charge : NTFS et ReFS.</p></td>
</tr>
<tr class="even">
<td><p>Défragmentation NTFS</p></td>
<td><p>La défragmentation NTFS est un processus réduisant le volume de fragmentation dans les systèmes de fichiers Windows. Ce résultat est obtenu par une organisation physique du disque afin de ranger les pièces de chaque fichier les unes contre les autres.</p></td>
<td><p>Pris en charge.</p>
<p>Meilleure pratique : Ni obligatoire, ni recommandé. Sur Windows Server 2012, nous vous recommandons également de désactiver la fonctionnalité d’optimisation et de défragmentation automatique des disques.</p></td>
<td><p>Pris en charge.</p>
<p>Meilleure pratique : Ni obligatoire, ni recommandé. Sur Windows Server 2012, nous vous recommandons également de désactiver la fonctionnalité d’optimisation et de défragmentation automatique des disques.</p></td>
</tr>
<tr class="odd">
<td><p>Taille d'unité d'allocation NTFS</p></td>
<td><p>La taille d'unité d'allocation NTFS représente le plus petit volume d'espace disque allouable à un fichier.</p></td>
<td><p>Pris en charge : Toutes les tailles d'unité d'allocation.</p>
<p>Meilleure pratique : 64 Ko pour les volumes de fichiers .edb et journaux.</p></td>
<td><p>Pris en charge : Toutes les tailles d'unité d'allocation.</p>
<p>Meilleure pratique : 64 Ko pour les volumes de fichiers .edb et journaux.</p></td>
</tr>
<tr class="even">
<td><p>Compression NTFS</p></td>
<td><p>La compression NTFS est le processus permettant de réduire la taille réelle d'un fichier stocké sur le disque dur.</p></td>
<td><p>Pris en charge : Non pris en charge pour les fichiers base de données ou journaux Exchange.</p></td>
<td><p>Pris en charge : Non pris en charge pour les fichiers base de données ou journaux Exchange.</p></td>
</tr>
<tr class="odd">
<td><p>Système de fichiers de cryptage NTFS (EFS)</p></td>
<td><p>Le système EFS permet aux utilisateurs de crypter des fichiers, des dossiers ou la totalité des lecteurs de données. Comme le système EFS fournit un cryptage fort par des algorithmes normalisés et un chiffrement à clé publique, les fichiers chiffrés sont confidentiels même en cas de brèche de sécurité dans le système.</p></td>
<td><p>Pris en charge : Non pris en charge pour les fichiers base de données ou journaux Exchange.</p></td>
<td><p>Non pris en charge pour les fichiers base de données ou journaux Exchange.</p></td>
</tr>
<tr class="even">
<td><p>Windows BitLocker (chiffrement de volume)</p></td>
<td><p>Windows BitLocker est une fonctionnalité de protection des données disponible dans Windows Server 2008. BitLocker protège les utilisateurs contre le vol ou l'exposition des données sur des ordinateurs perdus ou volés, et permet une suppression plus sécurisée des données lors de la mise hors service des ordinateurs.</p></td>
<td><p>Pris en charge : Tous les fichiers de base de données et tous les fichiers journaux Exchange.</p></td>
<td><p>Pris en charge : Tous les fichiers de base de données et tous les fichiers journaux Exchange. Les clusters de basculement Windows requièrent Windows Server 2008 R2 ou Windows Server 2008 R2 SP1 ainsi que le correctif logiciel suivant : <a href="http://go.microsoft.com/fwlink/p/?linkid=3052%26kbid=2446607">Vous ne pouvez pas activer BitLocker sur un volume de disque dans Windows Server 2008 R2 si l’ordinateur est un nœud de cluster de basculement</a>. Les volumes Exchange avec Bitlocker activé ne sont pas pris en charge dans les clusters de basculement Windows exécutant des versions antérieures de Windows.</p>
<p>Pour plus d’informations sur le chiffrement BitLocker Windows 7, consultez la rubrique relative au <a href="https://go.microsoft.com/fwlink/p/?linkid=220898">chiffrement de lecteur BitLocker dans Windows 7 : Forum aux questions</a>.</p></td>
</tr>
<tr class="odd">
<td><p>Bloc de message serveur (SMB) 3.0</p></td>
<td><p>Le protocole SMB (Server Message Block) est un protocole de partage de fichiers réseau (par-dessus TCP/IP ou d'autres protocoles réseau) qui permet à des applications sur un ordinateur d'accéder à des fichiers et des ressources sur un serveur distant. Il permet également aux applications de communiquer avec n'importe quel programme serveur configuré pour recevoir une demande client SMB. Windows Server 2012 introduit la nouvelle version 3.0 du protocole SMB avec les fonctionnalités suivantes :</p>
<ul>
<li><p>Basculement transparent SMB</p></li>
<li><p>Montée en puissance parallèle SMB</p></li>
<li><p>SMB multicanal</p></li>
<li><p>SMB direct</p></li>
<li><p>Chiffrement SMB</p></li>
<li><p>VSS pour les partages de fichiers SMB</p></li>
<li><p>Location d'annuaire SMB</p></li>
<li><p>PowerShell SMB</p></li>
</ul></td>
<td><p>Prise en charge limitée. Le scénario pris en charge est un déploiement virtualisé matériel dans lequel les disques sont hébergés sur des disques durs virtuels sur un partage SMB 3.0. Ces disques durs virtuels sont présentés à l'hôte via un hyperviseur. Pour plus d’informations, voir <a href="exchange-2013-virtualization-exchange-2013-help.md">Virtualisation d'Exchange 2013</a>.</p></td>
<td><p>Prise en charge limitée. Le scénario pris en charge est un déploiement virtualisé matériel dans lequel les disques sont hébergés sur des disques durs virtuels sur un partage SMB 3.0. Ces disques durs virtuels sont présentés à l'hôte via un hyperviseur. Pour plus d’informations, voir <a href="exchange-2013-virtualization-exchange-2013-help.md">Virtualisation d'Exchange 2013</a>.</p></td>
</tr>
<tr class="even">
<td><p>Espaces de stockage</p></td>
<td><p>Les espaces de stockage constituent une nouvelle solution de stockage offrant des capacités de virtualisation pour Windows Server 2012. Ils vous permettent d’organiser les disques physiques en pools de stockage, qui peuvent être facilement étendus en ajoutant des disques. Ces disques peuvent être connectés via USB, SATA ou SAS. Cette fonctionnalité utilise également des disques (espaces) virtuels qui se comportent exactement comme des disques physiques. Ils sont dotés de puissantes capacités associées, telles que l’allocation dynamique, ainsi que d’une résilience aux défaillances des médias physiques sous-jacents. Pour plus d’informations sur les espaces de stockage, consultez la rubrique <a href="https://technet.microsoft.com/fr-fr/library/hh831739.aspx">Vue d’ensemble des espaces de stockage</a>.</p></td>
<td><p>Pris en charge. Les mêmes restrictions que pour les types de disques physiques décrits dans cette rubrique s'appliquent.</p></td>
<td><p>Pris en charge. Les mêmes restrictions que pour les types de disques physiques décrits dans cette rubrique s'appliquent.</p></td>
</tr>
<tr class="odd">
<td><p>Système de fichiers résilient (ReFS, Resilient File System)</p></td>
<td><p>ReFS est un système de fichiers inédit pour Windows Server 2012 créé sur la base des systèmes NTFS. ReFS reste largement compatible avec le système NTFS. Il offre en outre des techniques de vérification des données et de correction automatique améliorées, ainsi qu’une résilience de bout en bout à la corruption intégrée, notamment quand il est utilisé en association avec la fonctionnalité Espaces de stockage. Pour plus d’informations sur le système ReFS, consultez la rubrique <a href="https://technet.microsoft.com/fr-fr/library/hh831724.aspx">Vue d’ensemble du système de fichiers résilient</a></p></td>
<td><p>Pris en charge pour les volumes contenant des fichiers de base de données Exchange, des fichiers journaux et des fichiers d’indexation de contenu. En cas de déploiement sur Windows Server 2012, vérifiez que les correctifs logiciels suivants sont installés sur Windows Server 2012 :</p>
<ul>
<li><p><a href="https://go.microsoft.com/fwlink/p/?linkid=717874">Correctif cumulatif de mise à jour de Windows 8 et Windows Server 2012 : avril 2013</a></p></li>
<li><p><a href="https://go.microsoft.com/fwlink/p/?linkid=717877">VDS (Virtual Disk Service) ou applications qui utilisent le blocage ou le gel VDS dans Windows Server 2012</a></p></li>
<li><p><a href="https://go.microsoft.com/fwlink/p/?linkid=717879">Un ordinateur basé sur Windows 8 ou Windows Server 2012 se bloque lorsque vous exécutez la commande « dir » sur un volume ReFS</a></p></li>
</ul>
<p>ReFS n’est pas pris en charge pour les volumes de système d’exploitation.</p>
<p>Meilleure pratique : les fonctionnalités d’intégrité des données doivent être désactivées pour les fichiers de base de données Exchange (.edb) ou le volume qui les héberge.</p></td>
<td><p>Pris en charge pour les volumes contenant des fichiers de base de données Exchange, des fichiers journaux et des fichiers d’indexation de contenu. En cas de déploiement sur Windows Server 2012, vérifiez que les correctifs logiciels suivants sont installés sur Windows Server 2012 :</p>
<ul>
<li><p><a href="https://go.microsoft.com/fwlink/p/?linkid=717874">Correctif cumulatif de mise à jour de Windows 8 et Windows Server 2012 : avril 2013</a></p></li>
<li><p><a href="https://go.microsoft.com/fwlink/p/?linkid=717877">VDS (Virtual Disk Service) ou applications qui utilisent le blocage ou le gel VDS dans Windows Server 2012</a></p></li>
<li><p><a href="https://go.microsoft.com/fwlink/p/?linkid=717879">Un ordinateur basé sur Windows 8 ou Windows Server 2012 se bloque lorsque vous exécutez la commande « dir » sur un volume ReFS</a></p></li>
</ul>
<p>ReFS n’est pas pris en charge pour les volumes de système d’exploitation.</p>
<p>Meilleure pratique : les fonctionnalités d’intégrité des données doivent être désactivées pour les fichiers de base de données Exchange (.edb) ou le volume qui les héberge.</p></td>
</tr>
<tr class="even">
<td><p>Suppression des doublons</p></td>
<td><p>La déduplication des données constitue une nouvelle technique permettant d'optimiser l'utilisation du stockage pour Windows Server 2012. Il s'agit d'une méthode de recherche et de suppression des éléments dupliqués au sein de données qui ne compromet ni leur fidélité ni leur intégrité. L'objectif est de stocker plus de données dans un espace plus restreint en segmentant les fichiers en petits blocs de taille variable, en identifiant les blocs dupliqués et en conservant une copie unique de chacun. Les copies redondantes du bloc sont remplacées par une référence à cette copie unique. Les blocs sont organisés en fichiers conteneurs, et les conteneurs sont compressés pour optimiser l'espace.</p></td>
<td><p>Non pris en charge pour les fichiers de base de données Exchange Remarque : peut être utilisé pour les fichiers de base de données Exchange qui sont complètement déconnectés (utilisés comme sauvegardes ou archives).</p></td>
<td><p>Non pris en charge pour les fichiers de base de données Exchange Remarque : peut être utilisé pour les fichiers de base de données Exchange qui sont complètement déconnectés (utilisés comme sauvegardes ou archives).</p></td>
</tr>
</tbody>
</table>


Architectures de stockage

