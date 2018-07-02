---
title: 'Sauvegarde, restauration et récupération d’urgence: Exchange 2013 Help'
TOCTitle: Sauvegarde, restauration et récupération d’urgence
ms:assetid: 394fc4ed-fa02-41fa-9159-cc2754ff8875
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dd876874(v=EXCHG.150)
ms:contentKeyID: 50477929
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Sauvegarde, restauration et récupération d’urgence

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2016-12-09_

Dans le cadre de la planification de protection de vos données, il est important de comprendre les différentes manières de protéger les données et de déterminer celle qui convient le mieux à votre organisation. La planification de protection des données est un processus complexe qui dépend des nombreuses décisions que vous prenez au cours de la phase de planification de votre déploiement.

En règle générale, les sauvegardes sont utilisées dans les situations suivantes :

  - **Récupération d’urgence**   En cas de défaillance logicielle ou matérielle, de plusieurs copies de bases de données dans un DAG assurent une haute disponibilité et un basculement rapide avec une perte de données nulle ou minime. Ainsi, vous éliminez les temps morts et la perte de productivité qui représente un coût significatif lors de la récupération d’une sauvegarde à un moment antérieur sur un disque ou une bande. Les groupes de disponibilité de base de données peuvent être étendus à plusieurs sites et peuvent fournir une résilience en cas de défaillance de disque, serveur, réseau et centre de données.

  - **Récupération d’éléments supprimés accidentellement**   Historiquement, dans une situation où un utilisateur supprimait des éléments qui devaient être récupérés ultérieurement, cela impliquait la recherche de supports de sauvegarde sur lesquels les données qui devaient être récupérées étaient stockées. Puis, les éléments choisis obtenus étaient fournis à l’utilisateur. Avec le nouveau dossier Éléments récupérables dans Exchange 2013 et la stratégie de rétention qui peut lui être appliquée, il est possible de conserver toutes les données supprimées et modifiées pour une période spécifiée. Ainsi, la récupération de ces éléments est plus simple et plus rapide. Cette opération permet de réduire la charge sur les administrateurs Exchange et le service d’assistance informatique en permettant aux utilisateurs finaux de récupérer eux-mêmes les éléments supprimés accidentellement. Elle permet ainsi de réduire les coûts d’administration et la complexité associés à la récupération d’un élément unique. Pour plus d’informations, consultez les rubriques [Stratégie et conformité de messagerie](messaging-policy-and-compliance-exchange-2013-help.md) et [Protection contre la perte de données](technical-overview-of-dlp-data-loss-prevention-in-exchange.md).

  - **Stockage des données sur le long terme**   Parfois, les sauvegardes sont effectuées pour archivage et la bande est généralement utilisée pour conserver des clichés à un moment précis des données pendant de longues périodes du fait d’exigences de confidentialité. Les nouvelles fonctionnalités d’archivage, de recherche de boîtes aux lettres multiples et de rétention de messages dans Exchange 2013 fournissent une solution pour conserver efficacement les données de manière à les rendre accessibles à l’utilisateur pendant de longues périodes. Ceci élimine les restaurations coûteuses à partir d’une bande et augmente la productivité. Pour plus d’informations, voir [Archivage inaltérable dans Exchange 2013](in-place-archiving-in-exchange-2013-exchange-2013-help.md), [Découverte électronique locale](in-place-ediscovery-exchange-2013-help.md) et [Conservation inaltérable et conservation pour litige](in-place-hold-and-litigation-hold-exchange-2013-help.md).

  - **Cliché de base de données à un moment précis**   Si une copie antérieure des données de la boîte aux lettres effectuée à un moment précis est requise pour votre organisation, Exchange offre la possibilité de créer une copie retardée de base de données dans un environnement de groupe de disponibilité de base de données. Cette opération peut être utile dans les rares cas où une altération logique du stockage se réplique dans plusieurs copies de base de données du groupe de disponibilité de base de données, impliquant de revenir à un moment précis antérieur. Cette opération peut également être utile si un administrateur supprime accidentellement des boîtes aux lettres ou les données d’un utilisateur. La récupération à partir d’une copie retardée peut être plus rapide que la restauration à partir d’une sauvegarde car les copies retardées ne nécessitent pas un processus de copie long du serveur de sauvegarde vers le serveur Exchange. Cela peut considérablement réduire le coût total de possession en réduisant les temps morts.

Étant donné qu’il existe des fonctionnalités natives d’Exchange 2013 qui apportent une réponse à chacun de ces scénarios d’une manière efficace et rentable, vous êtes en mesure de réduire ou d’éliminer l’utilisation des sauvegardes traditionnelles dans votre environnement.

Protection des données natives Exchange

Technologies de sauvegarde prises en charge

Enregistreur VSS Exchange 2013

Récupération Exchange Server

Récupération d’un Dépôt de contacts unifié

Base de données de récupération

Portabilité des bases de données

Portabilité de tonalité

## Protection des données natives Exchange

L’[architecture préférée](https://blogs.technet.com/b/exchange/archive/2014/04/21/the-preferred-architecture.aspx) de Microsoft pour Exchange Server 2013 tire parti d’un concept connu sous le nom de protection des données natives d’Exchange. La protection des données natives d’Exchange repose sur des fonctionnalités Exchange intégrées visant à protéger vos données de boîtes aux lettres, sans utiliser de sauvegardes (même si vous pouvez toujours utiliser ces fonctionnalités et effectuer des sauvegardes). Exchange 2013 comprend plusieurs nouvelles fonctionnalités et modifications de base qui, lorsqu’elles sont déployées et configurées correctement, peuvent assurer la protection des données natives. Vous n’avez donc plus besoin d’effectuer de sauvegardes traditionnelles de vos données. En exploitant les fonctions de haute disponibilité intégrées à Exchange 2013 pour minimiser les temps morts et la perte de données en cas de récupération d’urgence, il est également possible de réduire le coût total de possession du système de messagerie. En associant ces fonctionnalités à d’autres fonctions intégrées, telles que la conservation légale, vous pouvez réduire, voire éliminer, l’utilisation de sauvegardes ponctuelles traditionnelles et ainsi réaliser des économies.

En plus d’établir si Exchange 2013 vous permet de prendre vos distances avec les sauvegardes ponctuelles traditionnelles, nous vous recommandons d’évaluer le coût de votre infrastructure de sauvegarde actuelle. Pensez aux coûts que représentent le temps mort pour l’utilisateur final et la perte de données engendrée pendant une tentative de récupération d’urgence avec votre infrastructure de sauvegarde actuelle. Votre évaluation doit également inclure les coûts du matériel, de l’installation et des licences, ainsi que les frais de gestion associés à la récupération des données et à la maintenance des sauvegardes. En fonction de la configuration requise pour votre organisation, il est fort probable qu’un environnement Exchange 2013 pur, constitué d’au moins trois copies de base de données de boîtes aux lettres, offre un coût total de possession inférieur à un environnement avec sauvegardes.

Vous devez tenir compte d’un certain nombre de problèmes avant d’utiliser les fonctionnalités intégrées à Exchange 2013 comme fonctionnalités de remplacement des systèmes de sauvegarde traditionnelle. Certains aspects propres à votre organisation doivent également être pris en compte. Examinez les questions ci-dessous et notez que cette liste n’est pas exhaustive :

  - Vous devez déterminer le nombre de copies de la base de données qui doivent être déployées. Il est vivement recommandé de déployer au moins trois copies (non retardées) d’une base de données de boîtes aux lettres avant d’éliminer les formes classiques de protection de la base de données, telles que les sauvegardes RAID (Redundant Array of Independent Disks) ou VSS traditionnelles.

  - Vous devez définir clairement vos objectifs en termes de temps et de points de récupération et penser à l’utilisation d’un jeu combiné de fonctionnalités intégrées à la place de sauvegardes traditionnelles pour permettre de satisfaire ces objectifs.

  - Vous devriez déterminer combien de copies de chaque base de données sont nécessaires pour couvrir les différents scénarios d’échecs pour lesquels votre système doit être protégé.

  - Vous devez déterminer si l’élimination de l’utilisation d’un groupe de disponibilité de base de données ou de certains de ses membres prend en compte des coûts suffisants pour prendre en charge une solution de sauvegarde traditionnelle. Si tel est le cas, vous devez évaluer si cette solution permet d’améliorer votre objectif de temps de récupération ou vos contrats de niveau de service sur l’objectif de temps de récupération.

  - Vous devez envisager la possibilité de perdre une copie ponctuelle si le membre du groupe de disponibilité de base de données hébergeant la copie subit un échec qui affecte la copie ou l’intégrité de celle-ci.

  - Exchange 2013 vous permet de déployer des boîtes aux lettres beaucoup plus importantes, avec une taille de base de données de boîtes aux lettres maximale de 2 téra-octets (lorsque deux copies de base de données de boîtes aux lettres à haute disponibilité ou plus sont en cours d’utilisation). Selon les boîtes aux lettres plus importantes que la plupart des organisations sont susceptibles de déployer, vous devez déterminer votre objectif de récupération si vous devez relire un grand nombre de fichiers journaux lors de l’activation d’une copie de base de données ou d’une copie de base de données retardée.

  - Vous devez réfléchir aux moyens de détecter et de prévenir la réplication de l’altération logique d’une copie de base de données active dans des copies passives de la base de données. et notamment déterminer le plan de récupération pour cette situation et la fréquence avec laquelle ce scénario s’est produit dans le passé. Si une altération logique se produit fréquemment dans votre organisation, nous vous recommandons de prendre en compte ce scénario dans votre conception en utilisant une ou plusieurs copies retardées avec une fenêtre disposant d’un délai d’attente de relecture suffisant pour vous permettre de détecter et d’agir sur l’altération logique lorsqu’elle se produit mais avant que la corruption ne soit répliquée aux autres copies de base de données.

Une des fonctionnalités effectuée à la fin d’une sauvegarde réussie, totale ou incrémentielle est la troncature des fichiers journaux de transaction qui ne sont plus nécessaires pour la récupération de la base de données. Si les sauvegardes ne sont pas effectuées, la troncature du journal ne se produit pas. Pour empêcher une création de fichiers journaux, activez l’enregistrement circulaire pour vos bases de données répliquées. Lorsque vous associez un enregistrement circulaire avec réplication continue, vous obtenez un nouveau type d’enregistrement circulaire appelé enregistrement circulaire de réplication continue (CRCL), différent de l’enregistrement circulaire ESE (Extensible Storage Engine). Tandis que l’enregistrement circulaire ESE est effectué et géré par le service Banque d’informations de Microsoft Exchange, le CRCL est effectué et géré par le service de réplication de Microsoft Exchange. Une fois activé, l’enregistrement circulaire ESE ne génère pas de fichiers journaux supplémentaires mais remplace le fichier journal en cours si nécessaire. Toutefois, dans un environnement de réplication continue, des fichiers journaux sont nécessaires pour l’envoi et la relecture de journal. Par conséquent, lorsque vous activez le CRCL, le fichier journal en cours n’est pas remplacé et des fichiers journaux fermés sont générés pour le processus d’envoi et de relecture de journal.

Plus particulièrement, le service de réplication Microsoft Exchange gère le CRCL de façon que le journal soit tenu à jour en permanence et qu’aucun journal ne soit supprimé s’il est encore nécessaire pour la réplication. Le service de réplication de Microsoft Exchange et le service Banque d’informations Microsoft Exchange communiquent à l’aide d’appels de procédure distante (RPC) pour indiquer quels fichiers journaux peuvent être supprimés.

Pour que la troncature se produise sur les copies de base de données de boîtes aux lettres à haute disponibilité (non retardées), les conditions suivantes doivent être vérifiées :

  - Le fichier journal a été sauvegardé ou le CRCL est activé.

  - Le fichier journal se situe sous le point de contrôle.

  - Les autres copies non retardées de la base de données acceptent la suppression.

  - Le fichier journal a été inspecté par toutes les copies retardées de la base de données.

Pour que la troncature se produise sur les copies de base de données retardées, les conditions suivantes doivent être vérifiées :

  - Le fichier journal se situe sous le point de contrôle.

  - Le fichier journal est plus ancien que ReplayLagTime + TruncationLagTime.

  - Le fichier journal est supprimé sur la copie active de la base de données.

Protection des données natives Exchange

## Technologies de sauvegarde prises en charge

Exchange 2013 prend en charge uniquement les sauvegardes basées sur VSS compatibles avec Exchange. Exchange 2013 comprend un plug-in pour la sauvegarde Windows Server qui vous permet de créer et de restaurer des sauvegardes de données Exchange basées sur VSS. Pour sauvegarder et restaurer Exchange 2013, vous devez utiliser une application compatible Exchange qui prend en charge l’enregistreur VSS pour Exchange 2013, telle que Windows Server Backup (avec plug-in VSS), Microsoft System Center Data Protection Manager ou une application VSS tierce compatible Exchange.

Pour obtenir la procédure détaillée de sauvegarde et de restauration des données Exchange à l’aide de Windows Server Backup, consultez la rubrique [Utilisation de la Sauvegarde Windows Server pour sauvegarder et restaurer des données Exchange](using-windows-server-backup-to-back-up-and-restore-exchange-data-exchange-2013-help.md).

Protection des données natives Exchange

## Enregistreur VSS Exchange 2013

Exchange 2013 introduit une modification significative de l’architecture de l’enregistreur VSS par rapport à celle utilisée dans Exchange 2010 et Exchange 2007. Ces versions antérieures de Exchange incluaient deux enregistreurs VSS : l’un à l’intérieur du service Banque d’informations Microsoft Exchange (store.exe) et l’autre à l’intérieur du service de réplication Microsoft Exchange (msexchangerepl.exe). Dans Exchange, la fonctionnalité d’enregistreur VSS qui se trouvait jusqu’ici dans le service Banque d’informations Microsoft Exchange a été déplacée vers le service de réplication Microsoft Exchange. Le nouvel enregistreur, appelé Microsoft Exchange Writer, est maintenant utilisé par les applications VSS compatibles Exchange pour sauvegarder des copies de base de données actives et passives, et pour restaurer des copies de base de données sauvegardées. Bien que le nouvel enregistreur s’exécute dans le service de réplication Microsoft Exchange, il requiert l’exécution du service Banque d’informations Microsoft Exchange pour être publié. Par conséquent, les deux services sont nécessaires pour sauvegarder ou restaurer des bases de données Exchange.

Protection des données natives Exchange

## Récupération Exchange Server

La majorité des paramètres de configuration pour les serveurs de boîtes aux lettres et d’accès au client sont stockés dans Active Directory. Tout comme dans les versions antérieures d’Exchange, Exchange 2013 inclut un paramètre de configuration pour la récupération des serveurs perdus. Ce paramètre, */m:RecoverServer*, est utilisé pour reconstruire et recréer un serveur perdu en utilisant les paramètres et les informations de configuration stockés dans Active Directory. Toutefois, sachez qu’il existe plusieurs paramètres qui ne sont pas restaurés, comme les modifications apportées aux fichiers web.config locaux et à d’autres fichiers de configuration. En outre, les entrées de Registre personnalisées ne sont pas restaurées. Nous vous recommandons d’utiliser un processus de gestion des modifications fiable pour suivre et recréer ces modifications.

Pour obtenir la procédure détaillée de récupération d’un serveur Exchange 2013 perdu, consultez la rubrique [Récupérer un serveur Exchange](recover-an-exchange-server-exchange-2013-help.md). Pour obtenir la procédure détaillée de récupération d’un serveur perdu membre d’un groupe de disponibilité de base de données, consultez la rubrique [Récupérer un serveur membre de groupe de disponibilité de la base de données](recover-a-database-availability-group-member-server-exchange-2013-help.md).

Protection des données natives Exchange

## Récupération d’un Dépôt de contacts unifié

Quand Microsoft Lync Server 2013 est utilisé dans un environnement Exchange 2013, les informations de contact de l’utilisateur Lync sont stockées dans un dossier spécial de contact de sa boîte aux lettres. Celui-ci est appelé Dépôt de contacts unifié (UCS). Si vous restaurez une boîte aux lettres migrée à partir d’un UCS, la liste des contacts de messagerie instantanée de l’utilisateur cible risque d’être endommagée. Si l’utilisateur a été migré depuis la dernière sauvegarde, la restauration de la boîte aux lettres entraînera une perte totale de la liste des contacts de l’utilisateur. Dans les cas moins graves, seules les modifications apportées par l’utilisateur à la liste de contacts depuis la dernière sauvegarde seront perdues. Pour limiter le risque de perte de données potentielle, assurez-vous que l’utilisateur est migré vers le serveur de messagerie instantanée avant de restaurer la boîte aux lettres.

Protection des données natives Exchange

## Base de données de récupération

Une base de données de récupération est une base de données de boîtes aux lettres spéciale qui vous permet de monter une base de données de boîtes aux lettres restaurée et d’extraire des données à partir de la base de données restaurée, dans le cadre d’une opération de récupération. La cmdlet [New-MailboxRestoreRequest](https://technet.microsoft.com/fr-fr/library/ff829875\(v=exchg.150\)) permet d’extraire des données d’une base de données de récupération. Une fois extraites, les données peuvent être exportées dans un dossier ou fusionnées avec les données d’une boîte aux lettres existante. Les bases de données de récupération vous permettent de récupérer des données à partir d’une sauvegarde ou d’une copie de base de données sans perturber l’accès des utilisateurs aux données actuelles.

Il n’est pas possible d’utiliser une base de données de récupération pour une base de données de boîtes aux lettres d’une version antérieure de Exchange. En outre, la boîte aux lettres cible utilisée pour l’extraction et la fusion de données doit se trouver dans la même forêt Active Directory que la base de données montée dans la base de données de récupération.

Pour plus d’informations, voir [Récupérer des bases de données](recovery-databases-exchange-2013-help.md). Pour obtenir la procédure détaillée de création d’une base de données de récupération, consultez la rubrique [Créer une base de données de récupération](create-a-recovery-database-exchange-2013-help.md). Pour obtenir la procédure détaillée d’utilisation d’une base de données de récupération, consultez la rubrique [Restaurer des données à l’aide d’une base de données de récupération](restore-data-using-a-recovery-database-exchange-2013-help.md).

Protection des données natives Exchange

## Portabilité des bases de données

La portabilité des bases de données est une fonctionnalité qui permet à une base de données de boîtes aux lettres Exchange 2013 d’être déplacée et montée sur un autre serveur de boîtes aux lettres Exchange 2013 de la même organisation. Grâce à cette fonctionnalité, la suppression des étapes manuelles qui étaient sources d’erreurs fréquentes dans le processus de récupération optimise la fiabilité. En outre, la portabilité des bases de données réduit la durée globale de récupération des différents scénarios d’échec.

Pour plus d’informations, voir [Portabilité des bases de données](database-portability-exchange-2013-help.md). Pour obtenir la procédure détaillée de l’utilisation de la portabilité de la base de données, voir la rubrique [Déplacer une base de données de boîtes aux lettres à l’aide de la portabilité de base de données](move-a-mailbox-database-using-database-portability-exchange-2013-help.md).

Protection des données natives Exchange

## Portabilité de tonalité

La portabilité de tonalité est une fonctionnalité qui assure pendant un certain temps la continuité de l’activité en cas de pannes nuisant au fonctionnement d’une base de données de boîtes aux lettres, d’un serveur ou d’un site entier. La portabilité de tonalité permet aux utilisateurs de disposer d’une boîte aux lettres temporaire pour envoyer et recevoir des messages pendant que leur boîte aux lettres est restaurée ou réparée. La boîte aux lettres temporaire peut se trouver sur le même serveur de boîtes aux lettres Exchange 2013 ou sur tout autre serveur de boîtes aux lettres Exchange 2013 de votre organisation. Cela permet à un autre serveur d’héberger les boîtes aux lettres d’utilisateurs qui se trouvaient auparavant sur un serveur qui n’est plus disponible. Les clients qui prennent en charge le service de découverte automatique, tels que Microsoft Outlook, sont automatiquement redirigés vers le nouveau serveur sans qu’il soit nécessaire de mettre à jour manuellement le profil de bureau des utilisateurs. Une fois que les données de la boîte aux lettres d’origine d’un utilisateur sont restaurées, un administrateur peut fusionner la boîte aux lettres restaurée et la boîte aux lettres de tonalité et générer ainsi une boîte aux lettres à jour unique.

Le processus d’utilisation de la portabilité de tonalité est appelé *récupération de tonalité*. Une récupération de tonalité implique la création d’une base de données vide sur un serveur de boîtes aux lettres pour remplacer la base de données défectueuse. Cette base de données vide, appelée *base de données de tonalité* permet aux utilisateurs d’envoyer et de recevoir des messages électroniques pendant la récupération de la base de données défectueuse. Après récupération de la base de données défectueuse, la base de données de tonalité et la base de données récupérée sont permutées, puis les données de la base de données de tonalité sont fusionnées dans une base de données récupérée.

Pour plus d’informations, voir [Portabilité de tonalité](dial-tone-portability-exchange-2013-help.md). Pour obtenir la procédure détaillée de l’exécution d’une récupération de tonalité, voir [Réalisation d’une récupération de tonalité](perform-a-dial-tone-recovery-exchange-2013-help.md).

Protection des données natives Exchange

