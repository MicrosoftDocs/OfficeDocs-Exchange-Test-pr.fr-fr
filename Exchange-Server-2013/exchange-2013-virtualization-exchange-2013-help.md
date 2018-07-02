---
title: "Virtualisation d'Exchange 2013: Exchange 2013 Help"
TOCTitle: Virtualisation d'Exchange 2013
ms:assetid: 36184b2f-4cd9-48f8-b100-867fe4c6b579
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ619301(v=EXCHG.150)
ms:contentKeyID: 50477893
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Virtualisation d'Exchange 2013

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2017-08-08_

Vous pouvez déployer Microsoft Exchange Server 2013 dans un environnement virtualisé. Cette rubrique propose une vue d’ensemble des scénarios pris en charge pour le déploiement d’Exchange 2013 sur un logiciel de virtualisation de matériel.

**Contenu de cette rubrique**

Exigences en matière de virtualisation de matériel

Exigences de stockage des ordinateurs hôtes

Exigences de stockage Exchange

Exigences et recommandations relatives à la mémoire Exchange

Clustering de basculement basé sur l’hôte et migration d’Exchange

Les termes suivants sont utilisés au sujet de la virtualisation d’Exchange :

  - **Démarrage à froid**   L’action consistant à démarrer le système d’exploitation d’un système mis hors tension s’appelle un *démarrage à froid*. L’état du système d’exploitation n’a pas perduré dans ce cas.

  - **État enregistré**   Lorsqu’une machine virtuelle est éteinte, les hyperviseurs ont généralement la possibilité d’enregistrer l’état de la machine virtuelle. Ainsi, lorsque la machine est remise en marche, elle revient à l’*état enregistré* plutôt que de passer par un démarrage à froid.

  - **Migrations planifiées**   Lorsqu’un administrateur système décide de déplacer une machine virtuelle d’un hôte hyperviseur à un autre, l’action est définie comme une *migration planifiée*. Il peut s’agir d’une migration unique, ou bien un administrateur système peut configurer l’automatisation pour déplacer la machine virtuelle de manière échelonnée. Une migration planifiée peut également être le résultat d’un autre événement sur le système, qui n’est pas une panne matérielle ou logicielle. L’aspect essentiel est que la machine virtuelle Exchange fonctionne normalement et doit être déplacée pour une raison quelconque. Ce déplacement peut se faire via un outil technologique, comme Live Migration ou vMotion. Cependant, si la machine virtuelle Exchange ou l’hôte hyperviseur sur lequel se trouve la machine virtuelle subit une panne quelconque, le résultat n’est pas défini comme une migration planifiée.

## Exigences en matière de virtualisation de matériel

Microsoft prend en charge Exchange 2013 en production sur un logiciel de virtualisation de matériel si toutes les conditions suivantes sont remplies :

  - Le logiciel de virtualisation de matériel exécute l’une des applications suivantes :
    
      - N’importe quelle version de Windows Server dotée de la technologie Hyper-V ou de Microsoft Hyper-V Server
    
      - Tout hyperviseur tiers validé dans le cadre du [programme Windows SVVP (Server Virtualization Validation Program)](https://go.microsoft.com/fwlink/p/?linkid=125375).
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Le déploiement d’Exchange 2013 sur des fournisseurs IaaS (Infrastructure-as-a-Service) est pris en charge si toutes les conditions de prise en charge sont remplies. Si des fournisseurs sont chargés de l’approvisionnement de machines virtuelles, ces conditions consistent notamment à s’assurer que l’hyperviseur utilisé pour les machines virtuelles Exchange est entièrement pris en charge et que l’infrastructure qu’utilisera Exchange répond aux exigences de performances qui ont été déterminées au cours du processus de dimensionnement. Le déploiement de machines virtuelles Microsoft Azure est pris en charge si tous les volumes de stockage utilisés pour les bases de données Exchange et les journaux de transactions de base de données (y compris les bases de données de transport) sont configurés pour le stockage Azure Premium.</td>
    </tr>
    </tbody>
    </table>


  - L'ordinateur virtuel invité d’Exchange remplit les conditions suivantes :
    
      - Il exécute Exchange 2013.
    
      - Il est déployé sur Windows Server 2008 R2 SP1 (ou versions ultérieures), sur Windows Server 2012 ou sur Windows Server 2012 R2.

Pour les déploiements de Exchange 2013 :

  - Tous les rôles serveur d’Exchange 2013 sont pris en charge dans une machine virtuelle.

  - Il est possible de combiner les machines virtuelles d’un serveur Exchange (y compris les machines virtuelles d’une boîte aux lettres Exchange appartenant à un groupe de disponibilité de base de données ou DAG) à la technologie de migration et de clustering de basculement basée sur un hôte, à condition qu’elles n’enregistrent et ne restaurent pas l’état sur le disque lorsqu’elles sont déplacées ou déconnectées. Toute activité de basculement survenant au niveau de l’hyperviseur doit se terminer par un démarrage à froid lorsque la machine virtuelle est activée sur le nœud cible. Les migrations planifiées doivent se terminer par l’arrêt du système et un démarrage à froid ou par une migration en ligne faisant appel à une technologie de migration dynamique Hyper-V, par exemple. La migration de machines virtuelles basée sur un hyperviseur est prise en charge par le fournisseur de l’hyperviseur. Vous devez donc vous assurer qu’il prend en charge la migration des machines virtuelles Exchange et qu’il l’a testée. Microsoft prend en charge la migration dynamique Hyper-V de ces machines virtuelles.

  - Seuls les logiciels de gestion (par exemple, logiciel antivirus, logiciel de sauvegarde, logiciel de gestion des ordinateurs virtuels) peuvent être déployés sur l’ordinateur hôte physique. Aucune autre application serveur (par exemple, Exchange, SQL Server, Active Directory ou SAP) ne doit être installée sur l’ordinateur hôte. Les serveurs hôtes doivent être dédiés à l’exécution des ordinateurs virtuels invités.

  - Certains hyperviseurs intègrent des fonctionnalités de génération de captures instantanées des ordinateurs virtuels. qui capturent l’état d’un ordinateur virtuel pendant son exécution. Cette fonctionnalité permet de générer plusieurs captures instantanées d’un ordinateur virtuel, puis de restaurer celui-ci dans un état précédent via l’application d’une capture instantanée à l’ordinateur virtuel. Les captures instantanées d’ordinateur virtuel ne sont toutefois pas compatibles avec les applications. Leur utilisation peut avoir des conséquences non souhaitées et inattendues pour une application serveur chargée de conserver les données d’état, telle qu’Exchange. Aussi, la génération de captures instantanées d’un ordinateur virtuel Exchange n’est-elle pas prise en charge.

  - De nombreux produits de virtualisation de matériel permettent de spécifier le nombre de processeurs virtuels à allouer à chaque ordinateur virtuel invité. Les processeurs virtuels de l’ordinateur virtuel invité partagent un nombre fixe de cœurs de processeurs physiques dans le système physique. Exchange ne peut pas prendre en charge plus de 2 processeurs virtuels pour 1 processeur physique (nous vous recommandons d’utiliser 1 processeur virtuel pour 1 processeur physique). Par exemple, pour un système biprocesseur utilisant des processeurs quadri-cœur, le système hôte comporte 8 cœurs de processeurs physiques. Dans un système présentant une telle configuration, vous ne devez pas allouer plus de 16 processeurs virtuels à l’ensemble des ordinateurs virtuels invités.

  - Le calcul du nombre total de processeurs virtuels requis pour l’ordinateur hôte doit également tenir compte des configurations de système d’exploitation et d’E/S. Dans la plupart des cas, deux processeurs virtuels sont requis dans le système d’exploitation hôte pour un système hébergeant des ordinateurs virtuels Exchange. Cette valeur doit être utilisée comme base pour le processeur virtuel du système d’exploitation hôte lors du calcul du ratio global cœurs physiques/processeurs virtuels. Si le contrôle des performances du système d’exploitation hôte indique que vous consommez davantage d’utilisation processeur que l’équivalent de deux processeurs, vous devez réduire le nombre de processeurs virtuels affectés aux ordinateurs virtuels invités en conséquence et vérifier que le ratio global processeur virtuel/cœurs physiques ne dépasse pas 2/1.

  - Le système d’exploitation d’un ordinateur invité Exchange doit utiliser un disque avec une taille minimale de 15 gigaoctets (Go) plus la taille de la mémoire virtuelle allouée à l’ordinateur invité. Cette exigence est nécessaire pour tenir compte de la configuration requise du disque pour le système d’exploitation et le fichier de pagination. Par exemple, si 16 Go de mémoire sont affectés à l’ordinateur invité, un minimum de 31 Go d’espace disque est requis pour le disque du système d’exploitation.
    
    Par ailleurs, il se peut que la communication directe entre les ordinateurs virtuels invités et les adaptateurs de bus hôte SCSI ou Fibre Channel installés sur l’ordinateur hôte soit empêchée. Dans ce cas, vous devez configurer les adaptateurs dans le système d’exploitation de l’ordinateur hôte et présenter les numéros d’unité logique aux ordinateurs virtuels invités comme disque virtuel ou disque amovible.

  - La seule méthode prise en charge pour envoyer des courriers électroniques vers des domaines externes à partir de ressources de calcul Azure consiste à utiliser un relais SMTP (également appelé « hôte actif SMTP »). La ressource de calcul Azure envoie le courrier électronique vers le relais SMTP, puis le fournisseur du relais SMTP transmet le courrier électronique au domaine externe. Microsoft Exchange Online Protection est l’un des fournisseurs de relais SMTP, mais il existe également de nombreux autres fournisseurs tiers. Pour plus d’informations, consultez le billet du blog de l’équipe du support technique Microsoft Azure concernant l’[envoi de courriers électroniques à partir d’une ressource de calcul Azure vers des domaines externes](https://go.microsoft.com/fwlink/p/?linkid=799723).

Exigences en matière de virtualisation de matériel

## Exigences de stockage des ordinateurs hôtes

Les exigences d’espace disque minimal pour chaque ordinateur hôte sont les suivantes :

  - Les ordinateurs hôtes dans certaines applications de virtualisation matérielle requièrent de l’espace de stockage pour un système d’exploitation et ses composants. Par exemple, lors de l’exécution de Windows Server 2008 R2 avec Hyper-V, il vous faudra un minimum de 10 Go pour répondre aux exigences de Windows Server 2008. Pour plus de détails, voir [Configuration système requise pour Windows Server 2008 R2](https://go.microsoft.com/fwlink/p/?linkid=125378). Un espace de stockage supplémentaire est également nécessaire pour prendre en charge le fichier de pagination, les logiciels de gestion et les fichiers de récupération sur incident (vidage) du système d’exploitation.

  - Certains hyperviseurs conservent sur l’ordinateur hôte des fichiers qui sont uniques à chaque ordinateur virtuel invité. Par exemple, dans un environnement Hyper-V, un fichier de stockage de mémoire temporaire (fichier BIN) est créé et conservé pour chaque ordinateur invité. La taille de chaque fichier BIN correspond au volume de mémoire alloué à l’ordinateur invité. D’autres fichiers peuvent également être créés et conservés sur l’ordinateur hôte pour chaque ordinateur invité.

  - Si votre ordinateur hôte exécute Windows Server 2012 Hyper-V ou Hyper-V 2012 et que vous configurez un cluster de basculement basé sur l’hôte qui hébergera des serveurs de boîtes aux lettres Exchange dans un groupe de disponibilité de base de données, nous vous recommandons de suivre les instructions de l’article 2872325 de la base de connaissances Microsoft sur les [nœuds de cluster invité dans Hyper-V qui ne peuvent pas être créés ou joints](https://support.microsoft.com/kb/2872325).

Exigences en matière de virtualisation de matériel

## Exigences de stockage Exchange

Les exigences pour un stockage connecté à un serveur Exchange virtualisé sont les suivantes :

  - À chaque ordinateur invité Exchange doit être alloué un espace de stockage suffisant sur l’ordinateur hôte pour le disque fixe contenant le système d’exploitation de l’ordinateur invité, les fichiers de stockage de mémoire temporaire utilisés et les fichiers des ordinateurs virtuels hébergés sur l’ordinateur hôte. Pour chaque ordinateur invité d’Exchange, vous devez également allouer un stockage suffisant pour les files d’attente des messages et pour les bases de données et fichiers journaux sur les serveurs de boîtes aux lettres.

  - Le stockage utilisé par l’ordinateur invité Exchange pour le stockage de données Exchange (par exemple, les bases de données de boîtes aux lettres et les files d’attente de transport) peut être un stockage virtuel de taille fixe (par exemple, des disques durs virtuels fixes (VHD ou VHDX) dans un environnement Hyper-V), stockage virtuel dynamique lors de l’utilisation de fichiers VHDX avec Hyper-V, stockage pass through SCSI ou stockage SCSI Internet (iSCSI). Le stockage direct est un stockage configuré au niveau de l’hôte et dédié à un seul ordinateur invité. Tout l’espace de stockage utilisé par un ordinateur invité Exchange pour le stockage de données Exchange doit être un stockage au niveau du bloc, car Exchange 2013 ne prend pas en charge l’utilisation des volumes NAS (Network Attached Storage) autres que dans le scénario SMB 3.0 indiqué plus loin dans cette rubrique. En outre, le stockage NAS qui est présenté à l’invité en tant que stockage au niveau du bloc via l’hyperviseur n’est pas pris en charge.

  - Des disques virtuels fixes ou dynamiques peuvent être stockés sur un partage de fichiers SMB 3.0 appuyé par un stockage au niveau du bloc si l’ordinateur invité est exécuté sur Windows Server 2012 Hyper-V (ou une version ultérieure de d’Hyper-V). La seule utilisation prise en charge des partages de fichiers SMB 3.0 est pour le stockage de disques virtuels fixes ou dynamiques. Ces partages de fichiers ne peut pas servir pour le stockage direct des données Exchange. Lors de l’utilisation des partages de fichiers SMB 3.0 pour stocker des disques virtuels fixes ou dynamiques, la sauvegarde du stockage du partage de fichiers doit être configurée pour une haute disponibilité afin de garantir la meilleure disponibilité possible du service Exchange.

  - Le stockage utilisé par Exchange doit être hébergé en piles de disque distinctes du stockage hébergeant le système d’exploitation de l’ordinateur virtuel invité.

  - La configuration du stockage iSCSI pour l’utilisation d’un initiateur iSCSI sur un ordinateur virtuel invité Exchange est prise en charge. Cette configuration présente toutefois des performances réduites car la pile de mise en réseau d’un ordinateur virtuel inclut moins de fonctionnalités (par exemple, toutes les piles de mise en réseau virtuel ne prennent pas en charge les trames Jumbo).

Exigences en matière de virtualisation de matériel

## Exigences et recommandations relatives à la mémoire Exchange

Certains hyperviseurs offrent la possibilité de sursolliciter ou d’ajuster de façon dynamique la quantité de mémoire disponible sur un ordinateur invité spécifique en fonction de l’utilisation visible de la mémoire sur ce dernier par rapport aux besoins d’autres ordinateurs invités gérés par le même hyperviseur. Cette technologie est justifiée dans le cas de charges de travail exigeant une certaine quantité de mémoire sur de courtes périodes, à l’issue desquelles elle peut être renvoyée à d’autres utilisations. Cependant, elle n’a aucun intérêt dans le cas de charges de travail conçues pour solliciter en permanence de la mémoire. Tout comme de nombreuses applications serveur optimisées pour les performances en faisant appel à la mise en cache des données en mémoire, Exchange est en proie à un ralentissement des performances système et une expérience client inacceptable s’il ne contrôle pas totalement la mémoire allouée à l’ordinateur physique ou virtuel sur lequel il est exécuté. Par conséquent, l’utilisation de fonctionnalités de mémoire dynamique pour Exchange n’est pas prise en charge.

Exigences en matière de virtualisation de matériel

## Clustering de basculement basé sur l’hôte et migration d’Exchange

Vous trouverez ci-dessous les réponses à certaines questions fréquemment posées à propos de la technologie de basculement basé sur l’hôte et la migration avec des groupes de disponibilité de base de données (DAG) Exchange 2013:

  - **La société Microsoft prend-elle en charge une technologie de migration tierce ?**
    
    Microsoft n’est pas en mesure d’affirmer qu’elle prend en charge l’intégration de produits d’hyperviseurs tiers pour l’utilisation de ces technologies avec Exchange, car elles ne font pas partie du programme SVVP (Server Virtualization Validation Program). Le SVVP couvre les autres aspects de la prise en charge par Microsoft d’hyperviseurs tiers. Vous devez vous assurer que votre fournisseur d’hyperviseur prend en charge l’association de leur technologie de migration et clustering avec Exchange. En d’autres termes, si votre fournisseur d’hyperviseur prend en charge sa technologie de migration avec Exchange, Microsoft prend en charge Exchange avec la technologie de migration du fournisseur.

  - **Comment Microsoft définit-elle le clustering de basculement basé sur l’hôte ?**
    
    Le clustering de basculement basé sur l’hôte se rapporte à n’importe quelle technologie donnant la possibilité de réagir de manière automatique aux pannes au niveau de l’hôte, et de démarrer les machines virtuelles affectées sur des serveurs alternatifs. L’utilisation de cette technologie est prise en charge à condition qu’en cas de panne, la machine virtuelle soit lancée à l’aide d’un démarrage à froid sur l’hôte alternatif. Cette technologie aide à s’assurer que la machine virtuelle ne vient pas d’un état enregistré qui a perduré sur le disque car il serait périmé par rapport aux autres membres du DAG.

  - **Qu’entend Microsoft par prise en charge de la migration ?**
    
    La technologie de migration se rapporte à n’importe quelle technologie qui permet le déplacement planifié d’une machine virtuelle d’un ordinateur hôte vers un autre. Ce déplacement peut également être le résultat d’un déplacement automatisé provenant d’un équilibrage de charge des ressources et non d’une panne du système. Les migrations sont prises en charge à la condition que les machines virtuelles ne sortent pas d’un état enregistré qui a perduré sur le disque. Cela signifie que la technologie qui déplace une machine virtuelle en transportant l’état et la mémoire de la machine virtuelle sur le réseau sans temps d’arrêt perçu est prise en charge pour l’utilisation avec Exchange. Un fournisseur d’hyperviseurs tiers doit prendre en charge la technologie de migration, alors que Microsoft prend en charge Exchange lorsqu’il est utilisé dans cette configuration.

Exigences en matière de virtualisation de matériel

