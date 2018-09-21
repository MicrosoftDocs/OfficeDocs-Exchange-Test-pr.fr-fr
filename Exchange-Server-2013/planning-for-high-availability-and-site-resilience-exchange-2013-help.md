---
title: 'Planification: haute disponibilité et résilience de site: Exchange 2013 Help'
TOCTitle: Planification d'une haute disponibilité et d'une résilience de site
ms:assetid: 29bb0358-fc8e-4437-8feb-d2959ed0f102
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dd638104(v=EXCHG.150)
ms:contentKeyID: 50477787
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Planification d'une haute disponibilité et d'une résilience de site

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2016-12-09_

Pendant la phase de planification, les architectes, administrateurs et autres intervenants sur le système doivent identifier les impératifs de l’entreprise et de l’architecture pour le déploiement, en particulier les exigences de haute disponibilité et de résilience de site.

Certaines configurations sont requises pour le déploiement de ces fonctionnalités. Les configurations de matériel, de logiciel, et de réseau doivent également être remplies.

**Contenu de cette rubrique**

Conditions requises générales

Configuration matérielle minimale requise

Contraintes de stockage

Configuration logicielle requise

Configuration réseau requise

Configuration requise pour le serveur témoin

Planification de résilience de site

## Conditions requises générales

Avant de déployer un groupe de disponibilité de base de données (DAG) et de créer des copies de base de données de boîtes aux lettres, assurez-vous que les recommandations suivantes à l’échelle du système sont prises en compte :

  - Un serveur DNS (Domain Name System) doit être exécuté. Idéalement, le serveur DNS doit accepter des mises à jour dynamiques. Si cela n’est pas possible, vous devez créer un enregistrement (A) d’hôte DNS pour chaque serveur Exchange. Dans le cas contraire, Exchange ne fonctionnera pas correctement.

  - Chaque serveur de boîtes aux lettres d’un groupe de disponibilité de base de données doit être un serveur membre du même domaine.

  - L’ajout d’un serveur de boîtes aux lettres Exchange 2013 qui est aussi un serveur de répertoires pour un groupe de disponibilité de base de données n’est pas pris en charge.

  - Le nom que vous attribuez au groupe de disponibilité de base de données doit être un nom d’ordinateur valide, disponible, unique et composé tout au plus de 15 caractères.

Conditions requises générales

## Configuration matérielle minimale requise

Il n’y a généralement pas de configuration requise concernant le matériel pour les groupes de disponibilité de base de données ou les copies de bases de données de boîtes aux lettres. Les serveurs utilisés doivent remplir toutes les conditions présentées dans les rubriques [Conditions préalables pour Exchange 2013](exchange-2013-prerequisites-exchange-2013-help.md) et [Configuration requise pour Exchange 2013](exchange-2013-system-requirements-exchange-2013-help.md).

Conditions requises générales

## Contraintes de stockage

Il n’y a généralement pas de contrainte de stockage requise pour les groupes de disponibilité de base de données ou les copies de bases de données de boîtes aux lettres. Les groupes de disponibilité de base de données ne nécessitent pas ou n’utilisent pas le stockage partagé géré par cluster. Le stockage partagé géré par cluster est pris en charge pour l’utilisation dans un groupe de disponibilité de base de données uniquement lorsque celui-ci est configuré pour utiliser une solution qui exploite l’API de réplication tierce intégrée à Exchange 2013.

Conditions requises générales

## Configuration logicielle requise

Les groupes de disponibilité de base de données sont fournis dans Exchange 2013 Standard et dans Exchange 2013 Entreprise. En outre, un groupe de disponibilité de base de données peut contenir une combinaison de serveurs exécutant Exchange 2013 Standard ou Exchange 2013 Entreprise.

Chaque membre d’un groupe de disponibilité de base de données doit aussi exécuter le même système d’exploitation. Exchange 2013 fonctionne sous Windows Server 2008 R2, Windows Server 2012 et Windows Server 2012 R2. Tous les membres d’un groupe de disponibilité de base de données doivent exécuter le même système d’exploitation. Windows Server 2012 R2 est uniquement pris en charge pour les membres de DAG qui exécutent Exchange 2013 Service Pack 1 ou version ultérieure.

En plus des conditions nécessaires à l’installation d’Exchange 2013, le système d’exploitation doit remplir des conditions spéciales. Les DAG utilisent la technologie de clustering avec basculement de Windows. Par conséquent, ils nécessitent la version Enterprise ou Datacenter de Windows Server 2008 R2, ou la version Standard ou Datacenter des systèmes d’exploitation Windows Server 2012 ou Windows Server 2012 R2.

Conditions requises générales

## Configuration réseau requise

Chaque groupe de disponibilité de base de données et chacun de leurs membres doivent remplir certaines configurations réseau spécifiques. Chaque groupe de disponibilité de base de données doit contenir un *réseau MAPI* unique qu’un de ses membres utilise pour communiquer avec d’autres serveurs (par exemple, d’autres serveurs Exchange 2013 ou serveurs de répertoires) et zéro ou plusieurs *réseaux de réplication*, qui sont des réseaux dédiés à l’amorçage et à l’envoi de fichiers journaux.

Dans les versions précédentes d’Exchange, nous recommandions l’utilisation d’au moins deux réseaux (un réseau MAPI et un réseau de réplication) pour les groupes de disponibilité de bases de données. Exchange 2013 prend en charge plusieurs réseaux, mais cette recommandation dépend de la topologie physique réelle de votre réseau. Si les membres de votre groupe de disponibilité de base de données exploitent plusieurs réseaux physiques séparés physiquement les uns des autres, l’utilisation d’un réseau MAPI et d’un réseau de réplication distincts est redondante. Si vos différents réseaux sont partiellement séparés physiquement, mais qu’ils convergent vers un seul réseau physique (par exemple, un lien WAN unique), il est recommandé de n’utiliser qu’un seul réseau (de préférence de type 10 Gigabit Ethernet) pour le trafic MAPI et le trafic de réplication. Cette configuration sera plus simple non seulement pour le réseau, mais également pour le chemin d’accès réseau.

Prenez en compte les informations suivantes lors de la conception de l’infrastructure réseau de votre groupe de disponibilité de base de données :

  - Chaque membre du groupe de disponibilité de base de données doit avoir au moins une carte réseau capable de communiquer avec tous les autres membres du groupe de disponibilité de base de données. Si vous disposez d’un chemin d’accès réseau unique, nous vous recommandons d’utiliser au minimum la technologie 1 Gigabit Ethernet, avec toutefois une préférence pour le 10 Gigabit Ethernet. En outre, lorsque vous utilisez une carte réseau unique dans chaque membre du groupe de disponibilité de base de données, nous vous recommandons de concevoir la solution générale tout en gardant à l’esprit la carte et le chemin d’accès réseau unique.

  - L’utilisation de deux cartes réseau dans chaque membre du groupe de disponibilité de base de données vous procure un réseau MAPI et un réseau de réplication, et entraîne une redondance du réseau de réplication, ainsi que les comportements de récupération suivants :
    
      - Un basculement de serveur aura lieu en cas de défaillance au niveau du réseau MAPI (s’il y a des copies de base de données de boîtes aux lettres en bon état qui peuvent être activées).
    
      - En cas de défaillance au niveau du réseau de réplication, si le réseau MAPI n’est pas affecté par la défaillance, l’envoi de fichiers journaux et les opérations d’amorçage passeront à nouveau par le réseau MAPI, même si la propriété *ReplicationEnabled* du réseau MAPI est définie sur False. Lorsque le réseau de réplication défaillant est à nouveau en bon état et prêt à poursuivre l’envoi de journaux et les opérations d’amorçage, vous devez passer manuellement au réseau de réplication. Pour passer de la réplication sur le réseau MAPI à un réseau de réplication restauré, vous pouvez soit interrompre et reprendre la réplication continue en utilisant les cmdlets **Suspend-MailboxDatabaseCopy** et **Resume-MailboxDatabaseCopy**, soit redémarrer le service de réplication Microsoft Exchange. Nous recommandons l’utilisation des opérations d’interruption et de reprise pour éviter la brève interruption provoquée par le redémarrage du service de réplication Microsoft Exchange.

  - Chaque membre du groupe de disponibilité de base de données doit posséder le même nombre de réseaux. Par exemple, si vous envisagez d’utiliser une carte réseau unique dans un membre du groupe de disponibilité de base de données, tous les membres de ce groupe doivent aussi utiliser une carte réseau unique.

  - Chaque groupe de disponibilité de base de données ne doit avoir qu’un seul réseau MAPI. Le réseau MAPI doit offrir une connectivité à d’autres serveurs et services Exchange, tels que Active Directory et DNS.

  - Des réseaux de réplication supplémentaires peuvent être ajoutés si nécessaire. Vous pouvez aussi empêcher les points de défaillance uniques d’une carte réseau unique en utilisant une collaboration de cartes réseau ou une technologie similaire. Cependant, même l’utilisation d’une collaboration de cartes réseau n’empêche pas le réseau lui-même d’être un point de défaillance unique. De plus, une collaboration de cartes réseau complique inutilement le DAG.

  - Chaque réseau sur chaque serveur membre du groupe de disponibilité de base de données doit se trouver sur son propre sous-réseau. Chaque serveur du groupe de disponibilité de base de données peut se trouver sur un autre sous-réseau, mais les réseaux MAPI et de réplication doivent pouvoir être routés et offrir une connectivité de manière à ce que :
    
      - Chaque réseau de chaque serveur membre du groupe de disponibilité de base de données soit sur son propre sous-réseau, séparé du sous-réseau utilisé par chacun des autres réseaux sur le serveur.
    
      - Chaque réseau MAPI de serveur membre du DAG puisse communiquer avec tout autre réseau MAPI membre du DAG.
    
      - Chaque réseau de réplication de serveur membre du DAG puisse communiquer avec tout autre réseau de réplication membre du DAG.
    
      - Aucun routage direct ne permet la transmission de signaux de pulsation du réseau de réplication d’un serveur membre du DAG vers le réseau MAPI d’un autre membre du DAG, ou l’inverse, ou entre plusieurs réseaux de réplication au sein du groupe de disponibilité de base de données.

  - Quel que soit son emplacement géographique par rapport à d’autres membres du groupe de disponibilité de base de données, chaque membre du groupe doit présenter une latence de réseau en boucle de 500 millisecondes maximum par rapport aux autres membres. Lorsque la latence en boucle entre deux serveurs de boîtes aux lettres hébergeant des copies d’une base de données augmente, le potentiel de réplication non actualisé augmente également. Quelle que soit la latence de la solution, les utilisateurs doivent vérifier que les réseaux entre tous les membres du groupe de disponibilité de base de données sont capables de satisfaire aux objectifs de protection et de disponibilité des données du déploiement. Les configurations présentant des valeurs de latence plus élevées peuvent exiger un réglage spécial des paramètres du groupe de disponibilité de base de données, de la réplication et du réseau (tel que l’augmentation du nombre de bases de données ou la réduction du nombre de boîtes aux lettres par base de données) pour atteindre les objectifs escomptés.

  - La configuration de latence en boucle peut ne pas être la configuration de bande passante et de latence réseau la plus stricte pour une configuration à centres de données multiples. Vous devez évaluer la charge totale du réseau, qui inclut l’accès au client, Active Directory, le transport, la réplication continue et autre trafic pour déterminer la configuration réseau nécessaire pour votre environnement.

  - Les réseaux de groupes de disponibilité de base de données prennent en charge les protocoles Internet IPv4 et IPv6. Le protocole IPv6 n’est pris en charge que lorsque le protocole IPv4 est aussi utilisé ; un environnement exclusivement IPv6 n’est pas pris en charge. L’utilisation d’adresses IPv6 et de plages d’adresses IP n’est prise en charge que si les protocoles IPv6 et IPv4 sont activés sur cet ordinateur et si le réseau prend en charge les deux versions d’adresse IP. En cas de déploiement d’Exchange 2013 dans cette configuration, tous les rôles serveur peuvent échanger des données avec des périphériques, des serveurs et des clients utilisant des adresses IPv6.

  - APIPA (Automatic Private IP Addressing) est une fonctionnalité d’Windows qui attribue automatiquement les adresses IP quand aucun serveur DHCP (Dynamic Host Configuration Protocol) n’est disponible sur le réseau. Les adresses APIPA (y compris les adresses attribuées manuellement à partir des plages d’adresses APIPA) ne sont pas prises en charge en vue d’une utilisation par des groupes de disponibilité de base de données ou par Exchange 2013.

## Conditions requises pour le nom et l’adresse IP des groupes de disponibilité de base de données

Lors de la création, chaque groupe de disponibilité de base de données reçoit un nom unique, et est soit affecté à une ou plusieurs adresses IP statiques soit configuré pour l’utilisation de DHCP. Que vous utilisiez des adresses statiques ou dynamiques, toute adresse IP affectée au groupe de disponibilité de base de données doit se trouver sur le réseau MAPI.

Chaque DAG exécuté sous Windows Server 2008 R2 ou Windows Server 2012 nécessite au minimum une adresse IP sur le réseau MAPI. Un groupe de disponibilité de base de données nécessite des adresses IP supplémentaires quand le réseau MAPI est étendu sur plusieurs sous-réseaux. Les groupes de disponibilité de base de données exécutés sur Windows Server 2012 R2 créés sans point d’accès administratif de cluster ne nécessitent pas d’adresse IP.

L’illustration suivante représente un groupe de disponibilité de base de données dans lequel tous les nœuds ont le réseau MAPI sur le même sous-réseau.

**Groupe de disponibilité de base de données avec réseau MAPI sur le même sous-réseau**

![Groupe de disponibilité de la base de données sur un sous-réseau unique](images/Dd638104.bcb7ef68-6d18-4516-a736-b936991c82cb(EXCHG.150).gif "Groupe de disponibilité de la base de données sur un sous-réseau unique")

Dans cet exemple, le réseau MAPI dans chaque membre du groupe de disponibilité de base de données est sur le sous-réseau 172.19.18.*x*. Par conséquent, le groupe de disponibilité de base de données exige une adresse IP unique sur ce sous-réseau.

L’illustration suivante représente un groupe de disponibilité de base de données dont le réseau MAPI s’étend sur deux sous-réseaux : 172.19.18.*x* et 172.19.19.*x*.

**Groupe de disponibilité de base de données avec réseau MAPI sur plusieurs sous-réseaux**

![Groupe de disponibilité de la base de données étendu à plusieurs sous-réseaux](images/Dd638104.ffb57c64-3cb1-435c-8148-1b7154d1575c(EXCHG.150).gif "Groupe de disponibilité de la base de données étendu à plusieurs sous-réseaux")

Dans cet exemple, le réseau MAPI de chaque membre du groupe de disponibilité de base de données se trouve sur un sous-réseau distinct. Par conséquent, le groupe de disponibilité de base de données exige deux adresses IP, une pour chaque sous-réseau sur le réseau MAPI.

À chaque fois que le réseau MAPI du groupe de disponibilité de base de données est étendu sur un sous-réseau supplémentaire, une adresse IP supplémentaire pour ce sous-réseau-là doit être configurée pour le groupe de disponibilité de base de données. Chaque adresse IP configurée pour le groupe de disponibilité de base de données est affectée au cluster de basculement sous-jacent du groupe de disponibilité de base de données et utilisée par celui-ci. Le nom du groupe de disponibilité de base de données est aussi utilisé comme nom pour le cluster de basculement sous-jacent.

À n’importe quel moment spécifique, le cluster du groupe de disponibilité de base de données n’utilisera qu’une des adresses IP affectées. La fonction de clustering avec basculement Windows enregistre cette adresse IP dans le DNS quand l’adresse IP du cluster et les ressources de nom du réseau sont mises en ligne. En plus de l’utilisation d’une adresse IP et d’un nom de réseau, un objet nom de cluster (CNO) est créé dans Active Directory. Le nom, l’adresse IP et le CNO du cluster sont utilisés en interne par le système pour sécuriser le groupe de disponibilité de base de données et à des fins de communication interne. Les administrateurs et les utilisateurs finaux n’ont pas besoin d’interface ni de connexion avec le nom du groupe de disponibilité de base de données ni avec l’adresse IP.

> [!NOTE]
> Bien que le nom de réseau et l’adresse IP du cluster soient utilisés en interne par le système, il n’y a pas de dépendance irréversible dans Exchange 2013 pour que ces ressources soient disponibles. Même si le point d’accès administratif du cluster sous-jacent (c’est-à-dire, les ressources d’adresse IP et de nom de réseau) est en mode hors connexion, la communication interne a quand même lieu dans le groupe de disponibilité de base de données à l’aide du nom des serveurs membres de ce groupe. Cependant, nous vous recommandons de contrôler périodiquement la disponibilité de ces ressources afin de vous assurer qu’elles ne sont pas hors ligne pendant plus de 30 jours. Si le cluster sous-jacent est hors ligne pendant plus de 30 jours, le compte de CNO peut être invalidé par le mécanisme de nettoyage de la mémoire dans Active Directory.


## Configuration de la carte réseau pour les groupes de disponibilité de base de données

Chaque carte réseau doit être correctement configurée selon l’usage prévu. La configuration d’une carte réseau destinée à un réseau MAPI n’est pas la même que celle d’une carte réseau destinée à un réseau de réplication. Pour configurer correctement chaque carte réseau, vous devez configurer l’ordre de connexion au réseau dans Windows de manière à ce que le réseau MAPI se connecte en premier. Pour savoir comment modifier l’ordre de connexion au réseau, consultez la rubrique relative à la [modification de l’ordre des liaisons du protocole](https://go.microsoft.com/fwlink/p/?linkid=179138).

## Configuration de la carte du réseau MAPI

Une carte réseau destinée à l’utilisation par un réseau MAPI doit être configurée comme décrit dans le tableau suivant.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Fonctionnalités de mise en réseau</th>
<th>Paramètres</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Client pour les réseaux Microsoft</p></td>
<td><p>Activé</p></td>
</tr>
<tr class="even">
<td><p>Planificateur de paquets QoS</p></td>
<td><p>Éventuellement activé</p></td>
</tr>
<tr class="odd">
<td><p>Partage de fichiers et d’imprimantes pour les réseaux Microsoft</p></td>
<td><p>Activé</p></td>
</tr>
<tr class="even">
<td><p>Internet Protocol Version 6 (TCP/IP v6)</p></td>
<td><p>Activé</p></td>
</tr>
<tr class="odd">
<td><p>Internet Protocol Version 4 (TCP/IP v4)</p></td>
<td><p>Activé</p></td>
</tr>
<tr class="even">
<td><p>Pilote E/S Mappage de découverte de couche liaison</p></td>
<td><p>Activé</p></td>
</tr>
<tr class="odd">
<td><p>Répondeur de découverte de couche de liaison</p></td>
<td><p>Activé</p></td>
</tr>
</tbody>
</table>


Les propriétés TCP/IP v4 d’une carte de réseau MAPI sont configurées de la manière suivante :

  - L’adresse IP du réseau MAPI d’un membre du groupe de disponibilité de base de données peut être affectée ou configurée manuellement pour utiliser le protocole DHCP. Dans ce cas, nous vous recommandons d’utiliser les réservations persistantes pour l’adresse IP du serveur.

  - Le réseau MAPI utilise généralement une passerelle par défaut, bien que ce ne soit pas obligatoire.

  - Au moins une adresse de serveur DNS doit être configurée. Pour la redondance, il est recommandé d’utiliser plusieurs serveurs DNS.

  - La case **Enregistrer les adresses de cette connexion dans le serveur DNS** doit être cochée.

## Configuration de la carte du réseau de réplication

Une carte réseau destinée à l’utilisation par un réseau de réplication doit être configurée comme décrit dans le tableau suivant.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Fonctionnalités de mise en réseau</th>
<th>Paramètres</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Client pour les réseaux Microsoft</p></td>
<td><p>Désactivé</p></td>
</tr>
<tr class="even">
<td><p>Planificateur de paquets QoS</p></td>
<td><p>Éventuellement activé</p></td>
</tr>
<tr class="odd">
<td><p>Partage de fichiers et d’imprimantes pour les réseaux Microsoft</p></td>
<td><p>Désactivé</p></td>
</tr>
<tr class="even">
<td><p>Internet Protocol Version 6 (TCP/IP v6)</p></td>
<td><p>Activé</p></td>
</tr>
<tr class="odd">
<td><p>Internet Protocol Version 4 (TCP/IP v4)</p></td>
<td><p>Activé</p></td>
</tr>
<tr class="even">
<td><p>Pilote E/S Mappage de découverte de couche liaison</p></td>
<td><p>Activé</p></td>
</tr>
<tr class="odd">
<td><p>Répondeur de découverte de couche de liaison</p></td>
<td><p>Activé</p></td>
</tr>
</tbody>
</table>


Les propriétés TCP/IP v4 d’une carte de réseau de réplication sont configurées de la manière suivante :

  - L’adresse IP du réseau de réplication d’un membre du groupe de disponibilité de base de données peut être affectée ou configurée manuellement pour utiliser le protocole DHCP. Dans ce cas, nous vous recommandons d’utiliser les réservations persistantes pour l’adresse IP du serveur.

  - Les réseaux de réplication n’ont généralement pas de passerelle par défaut et, si le réseau MAPI en a une, aucun autre réseau ne doit avoir de passerelle par défaut. Le routage du trafic réseau sur un réseau de réplication peut être configuré à l’aide de routes persistantes et statiques au réseau correspondant sur d’autres membres du groupe de disponibilité de base de données utilisant des adresses de passerelle qui peuvent effectuer le routage entre les réseaux de réplication. Tout autre trafic ne correspondant pas à cette route sera traité par la passerelle par défaut configurée sur la carte du réseau MAPI.

  - Les adresses de serveur DNS ne doivent pas être configurées.

  - La case à cocher **Enregistrer les adresses de cette connexion dans le serveur DNS** ne doit pas être activée.

Conditions requises générales

## Configuration requise pour le serveur témoin

Un *serveur témoin* est un serveur extérieur au groupe de disponibilité de base de données qui sert à obtenir et maintenir le quorum quand le groupe de disponibilité de base de données a un nombre de membres pair. Les groupes de disponibilité de base de données ayant un nombre de membres impair n’utilisent pas de serveur témoin. Tout groupe de disponibilité de base de données ayant un nombre de membres pair doit utiliser un serveur témoin. Le serveur témoin peut être n’importe quel ordinateur exécutant Windows Server. Il n’est pas nécessaire que la version du système d’exploitation Windows Server du serveur témoin corresponde au système d’exploitation utilisé par les membres du groupe de disponibilité de base de données.

Le quorum est géré au niveau du cluster, sous le groupe de disponibilité de base de données. Un groupe de disponibilité de base de données a le quorum quand la majorité de ses membres sont connectés et peuvent communiquer les uns avec les autres. Cette notion de quorum est un aspect du concept de quorum dans le clustering de basculement Windows. Parmi les aspects liés et nécessaires au quorum dans les clusters de basculement se trouve la *ressource quorum*. La ressource quorum est une ressource située dans un cluster de basculement, fournissant un moyen d’arbitrage conduisant à l’état de cluster et aux décisions d’appartenance. La ressource quorum fournit également un stockage permanent pour le stockage des informations de configuration. La ressource de quorum est accompagnée du *journal de quorum* qui est une base de données de configuration pour le cluster. Il contient des informations telles que les serveurs membres du cluster, les ressources installées dans le cluster et l’état de ces ressources (par exemple, en ligne ou hors connexion).

Il est fondamental que chaque membre du groupe de disponibilité de base de données ait une vue cohérente de la configuration du cluster sous-jacent du groupe. Le quorum agit comme le référentiel définitif pour toutes les informations de configuration relatives au cluster. Le quorum est utilisé pour départager les nœuds afin d’éviter le syndrome *Split-Brain*. Le syndrome Split-Brain est une situation qui se produit lorsque les membres du groupe de disponibilité de base de données ne peuvent pas communiquer entre eux bien qu’ils soient opérationnels. Ce syndrome est évité en exigeant toujours qu’une majorité des membres du groupe de disponibilité de base de données (et dans le cas des groupes de disponibilité de base de données ayant un nombre de membres pair, le serveur témoin du groupe de disponibilité de base de données) soient disponibles et en interaction pour que le groupe de disponibilité de base de données soit opérationnel.

Conditions requises générales

## Planification de résilience de site

Chaque jour, un nombre croissant d’entreprises reconnaît que l’accès à un système de messagerie fiable et disponible est essentiel à leur réussite. Pour de nombreuses organisations, le système de messagerie fait partie des plans de continuité d’activité et la résilience du site doit être conçue dans leur déploiement de service de messagerie. Fondamentalement, de nombreuses solutions de résilience de site impliquent le déploiement de matériel dans un deuxième centre de données.

En définitive, la conception générale d’un groupe de disponibilité de base de données, y compris le nombre de membres du groupe de disponibilité de base de données et le nombre de copies de base de données de boîtes aux lettres, dépendra des accords de niveau du service de récupération (SLA) de chaque organisation pour traiter divers scénarios d’échec. Pendant la phase de planification, les architectes et administrateurs du système identifient les besoins du déploiement, y compris les exigences de résilience de site. Ils déterminent les emplacements à utiliser et les cibles SLA requises pour la récupération. L’accord SLA déterminera les deux éléments spécifiques qui doivent être la base de la conception d’une solution de haute disponibilité et de résilience de site : l’objectif de temps de récupération et l’objectif de point de récupération. Ces deux valeurs sont mesurées en minutes. L’objectif de temps de récupération correspond au temps nécessaire à la restauration du service. L’objectif de point de récupération correspond à l’actualité des données après l’opération de récupération. Un accord SLA peut aussi être défini pour restaurer le centre de données principal pour qu’il fonctionne complètement une fois les problèmes résolus.

Les architectes et administrateurs de la solution identifieront aussi les ensembles d’utilisateurs qui requièrent une protection de résilience de site et détermineront si la solution multi-site doit être une configuration actif/passif ou actif/actif. Dans une configuration actif/passif, aucun utilisateur n’est normalement hébergé dans le centre de données de secours. Dans une configuration actif/actif, les utilisateurs sont hébergés aux deux emplacements, et un certain pourcentage du nombre total de bases de données dans le cadre de cette solution a un emplacement actif préféré dans un deuxième centre de données. Quand le service est défaillant pour les utilisateurs d’un centre de données, ces utilisateurs sont activés dans l’autre centre de données.

L’élaboration des contrats de niveau de service appropriés requiert souvent de répondre aux questions de base suivantes :

  - Quel niveau de service est requis suite à un échec du centre de données principal ?

  - Les utilisateurs ont-ils besoin de leurs données ou uniquement des services de messagerie ?

  - À quelle fréquence les données sont-elles requises ?

  - Combien d’utilisateurs doivent être pris en charge ?

  - Comment les utilisateurs accèderont-ils à leurs données ?

  - Qu’est-ce que le SLA d’activation de centre de données en mode veille ?

  - Comment le service est-il ramené vers le centre de données principal ?

  - Les ressources sont-elles dédiées à la solution de résilience de site ?

En répondant à ces questions, vous commencez à donner forme à une conception de résilience de site pour votre solution de messagerie. Une exigence clé en relation avec la récupération suite à une défaillance de site consiste à créer une solution permettant de récupérer les données nécessaires dans un centre de données de sauvegarde hébergeant le service de messagerie de sauvegarde.

## Planification de certificat

Il n’y a pas de considération de conception spéciale ou unique pour les certificats lors du déploiement d’un groupe de disponibilité de base de données dans un centre de données unique. Toutefois, lorsque vous étendez un groupe de disponibilité de base de données sur plusieurs centres de données dans une configuration de résilience de site, il y a quelques considérations spécifiques en matière de certificats. Généralement, votre conception de certificat dépend des clients utilisés, ainsi que des conditions des autres applications utilisant des certificats. Certaines recommandations et meilleures pratiques doivent être observées en ce qui concerne le type et le nombre de certificats.

Il est recommandé de réduire le nombre de certificats que vous utilisez pour vos serveurs Exchange et d’inverser les serveurs proxy. Il est recommandé d’utiliser un certificat unique pour tous ces points finaux de service dans chaque centre de données. Cette approche minimise le nombre de certificats nécessaires, ce qui réduit à la fois le coût et la complexité de la solution.

Pour les clients Outlook Anywhere, il est recommandé d’utiliser un seul certificat SAN (autre nom d’objet) par centre de données, en incluant plusieurs noms d’hôtes dans le certificat. Pour assurer la connectivité d’Outlook Anywhere après un basculement de base de données, de serveur ou de centre de données, vous devez utiliser le même nom de principal pour chaque certificat et paramétrer l’objet configuration de fournisseur OutlookActive Directory avec le même nom de principal dans le formulaire Microsoft-Standard (msstd). Par exemple, si vous utilisez le nom de principal de certificat mail.contoso.com, vous configurez les attributs de la manière suivante :

```powershell
Set-OutlookProvider EXPR -CertPrincipalName "msstd:mail.contoso.com"
```

Quelques applications qui s’intègrent à Exchange présentent des conditions spéciales de certificat qui peuvent nécessiter l’utilisation de certificats supplémentaires. Exchange 2013 peut coexister avec Office Communications Server (OCS). OCS requiert des certificats 1024 bits ou des certificats plus importants qui utilisent le nom de serveur OCS comme nom principal du certificat. Utiliser le nom de serveur OCS comme nom principal de certificat empêcherait Outlook Anywhere de fonctionner correctement. Il vous faut donc utiliser un certificat supplémentaire séparé pour l’environnement OCS.

## Planification de réseau

En plus des conditions spécifiques de mise en réseau nécessaires pour chaque groupe de disponibilité de base de données ainsi que pour chaque serveur membre d’un groupe de disponibilité de base de données, il existe d’autres conditions et recommandations spécifiques aux configurations de résilience de site. Comme avec tous les groupes de disponibilité de base de données, que les membres soient déployés dans un seul ou plusieurs sites, la latence en boucle du réseau entre les membres du groupe de disponibilité de base de données ne doit pas dépasser 500 millisecondes. En outre, certains paramètres spécifiques de configuration sont recommandés pour les groupes de disponibilité de base de données étendus sur plusieurs sites :

  - **Les réseaux MAPI doivent être isolés des réseaux de réplication** Les stratégies de réseau Windows, les stratégies de pare-feu Windows ou les listes de contrôle d’accès routeur (ACL) doivent être utilisées pour bloquer le trafic entre le réseau MAPI et les réseaux de réplication. Cette configuration est nécessaire pour empêcher la pulsation de réseau inter-conversation.

  - **Les enregistrements DNS côté client doivent avoir une valeur de durée de vie (TTL, Time to Live) de 5 minutes.** Le temps d’indisponibilité vécu par les clients dépend non seulement de la rapidité du basculement, mais aussi de la vitesse à laquelle la réplication DNS se produit et à laquelle les clients demandent les informations DNS mises à jour. Les enregistrements DNS pour tous les services clients Exchange, y compris Microsoft Office Outlook Web App, Microsoft Exchange ActiveSync, les services web Exchange, Outlook Anywhere, les protocoles SMTP, POP3 et IMAP4 dans les serveurs DNS internes et externes doivent être paramétrés avec une durée de vie de 5 minutes.

  - **Utilisation d’un routage statique pour configurer la connectivité sur les réseaux de réplication** Utilisez un routage permanent statique pour fournir la connectivité réseau entre les cartes du réseau de réplication. Ce processus consiste en une configuration rapide et unique, effectuée sur chaque membre du groupe de disponibilité de base de données lors de l’utilisation d’adresses IP statiques. Si vous utilisez un protocole DHCP pour obtenir des adresses IP pour vos réseaux de réplication, vous pouvez aussi vous en servir pour affecter des routages statiques à la réplication et ainsi simplifier le processus de configuration.

## Planification générale de résilience de site

En plus des conditions répertoriées ci-dessus pour la haute disponibilité, il existe d’autres recommandations pour le déploiement d’Exchange 2013 dans une configuration de résilience de site (par exemple, l’extension d’un groupe de disponibilité de base de données sur plusieurs centres de données). Ce que vous faites pendant la phase de planification conditionnera directement la réussite de votre solution de résilience de site. Par exemple, une conception d’espace de noms médiocre peut entraîner des complications avec les certificats et une configuration de certificat incorrecte peut empêcher les utilisateurs d’accéder aux services.

Afin de minimiser le temps que prend l’activation d’un deuxième centre de données et de permettre à celui-ci d’héberger des points finaux de service d’un centre de données défaillant, il faut effectuer la planification de façon appropriée. Voici quelques exemples :

  - Vos objectifs SLA pour la solution de résilience de site doivent être bien compris et bien documentés.

  - Les serveurs du deuxième centre de données doivent disposer d’une capacité suffisante pour héberger la population d’utilisateurs des deux centres de données.

  - Tous les services fournis dans le centre de données principal doivent être activés dans le deuxième centre de données (à moins que le service ne soit pas inclus dans le cadre de l’accord SLA de résilience de site). Les services sont les suivants : Active Directory, infrastructure de réseau (par exemple, DNS, TCP/IP, etc.), services de téléphonie (si la messagerie unifiée est utilisée) et infrastructure de site (par exemple, alimentation ou refroidissement).

  - Pour que certains services puissent fonctionner à partir du centre de données défaillant, les certificats de serveur appropriés doivent être configurés. Certains services ne permettent pas l’instanciation (par exemple, POP3 et IMAP4) et ne permettent l’utilisation que d’un seul certificat. Dans ces cas, soit il doit s’agir d’un certificat SAN (autre nom d’objet) incluant plusieurs noms, soit les différents noms doivent être suffisamment similaires pour permettre le recours à un certificat générique (à condition que les stratégies de sécurité de l’organisation autorisent l’utilisation de certificats génériques).

  - Les services nécessaires doivent être définis dans le deuxième centre de données. Par exemple, si le premier centre de données a trois URL SMTP différentes sur plusieurs serveurs de transport, la configuration appropriée doit être définie dans le deuxième centre de données afin d’activer au moins un (si ce n’est les trois) serveur(s) de transport pour héberger la charge de travail.

  - La configuration de réseau nécessaire doit être en place pour prendre en charge le basculement de centre de données. Cela peut impliquer de veiller à ce que les configurations d’équilibrage de charge soient en place, que le serveur DNS général soit configuré et que la connexion Internet soit activée avec la configuration de routage appropriée.

  - La stratégie d’activation des changements du DNS nécessaires au basculement de centre de données doit être comprise. Les changements DNS spécifiques, dont leurs paramètres de durée de vie, doivent être définis et documentés pour prendre en charge le SLA en vigueur.

  - Une stratégie de test de la solution doit aussi être établie et prise en compte dans l’accord SLA. La validation périodique du déploiement représente la seule manière de garantir que la qualité et la viabilité du déploiement ne se dégradent pas avec le temps. Après la validation du déploiement, nous vous recommandons de documenter explicitement la partie de la configuration affectant directement la réussite de la solution. En outre, nous vous recommandons aussi d’améliorer vos processus de gestion des changements liés à ces segments du déploiement.

Conditions requises générales

