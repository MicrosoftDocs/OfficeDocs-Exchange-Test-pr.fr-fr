---
title: 'Haute disponibilité et résilience de site: Exchange 2013 Help'
TOCTitle: Haute disponibilité et résilience de site
ms:assetid: 6628285e-d07c-443d-866b-be784ad1ed1e
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dd638137(v=EXCHG.150)
ms:contentKeyID: 50478319
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Haute disponibilité et résilience de site

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2016-12-15_

Vous pouvez protéger vos bases de données de boîtes aux lettres Exchange Server 2013 et les données qu’elles contiennent en configurant vos bases de données et serveurs de boîtes aux lettres pour la haute disponibilité et la résilience de site. Exchange 2013 réduit les coûts et la complexité du déploiement d’une solution de messagerie à hautes disponibilité et résilience, tout en fournissant des niveaux de disponibilité de données et de service élevés et en prenant en charge les boîtes aux lettres volumineuses.

Exchange 2013 permet aux clients de toutes tailles et de tous segments de déployer économiquement un service de messagerie en continu dans leur organisation en tirant parti des capacités de réplication natives et de l’architecture à haute disponibilité présentées dans Exchange 2010. Pour obtenir la liste des différences entre Exchange 2010 et Exchange 2007, voir [Modifications apportées à la haute disponibilité et la résilience de site par rapport aux versions précédentes](changes-to-high-availability-and-site-resilience-over-previous-versions-exchange-2013-help.md).

**Contenu de cette rubrique**

Terminologie clé

Groupes de disponibilité de base de données

Copies de bases de données de boîtes aux lettres

Active Manager

Résilience de site

API de réplication tierce

Documentation relative à la haute disponibilité et à la résilience de site

## Terminologie clé

Les termes clés suivants sont importants pour comprendre la haute disponibilité et la résilience de site :

  - *Active Manager*  
    Composant Exchange interne exécuté dans le service de réplication Microsoft Exchange qui est responsable de la surveillance des échecs et de l'action corrective via le basculement au sein d'un groupe de disponibilité de base de données (DAG).

<!-- end list -->

  - *AutoDatabaseMountDial*  
    Paramètre de propriété d'un serveur de boîtes aux lettres qui détermine si une copie de base de données passive sera automatiquement montée en tant que nouvelle copie active, en fonction du nombre de fichiers journaux manquants pour la copie montée.

<!-- end list -->

  - *Mode Réplication continue - blocage*  
    En mode blocage, chaque fois qu'une mise à jour est enregistrée dans le tampon journal actif de la copie de la base de données active, elle est envoyée dans le tampon journal de chacune des copies de base de données de boîtes aux lettres passives. Lorsque le tampon journal est plein, chaque copie de base de données constitue, inspecte et crée le fichier journal suivant dans la séquence de génération.

<!-- end list -->

  - *Mode Réplication continue - fichier*  
    En mode fichier, les fichiers du journal des transactions fermé sont envoyés de la copie de base de données active vers une ou plusieurs copies de base de données passives.

<!-- end list -->

  - *Groupe de disponibilité de base de données*  
    Groupe de 16 serveurs de boîtes aux lettres Exchange 2013 qui héberge un ensemble de bases de données répliquées.

<!-- end list -->

  - *Mobilité de la base de données*  
    Possibilité qu'une base de données de boîtes aux lettres Exchange 2013 soit répliquée et montée sur d'autres serveurs de boîtes aux lettres Exchange 2013.

<!-- end list -->

  - *Centre de données*  
    En général, il s'agit d'un site Active Directory, mais il peut aussi s'agir d'un site physique. Dans le cadre de cette documentation, « centre de données » équivaut à « site Active Directory ».

<!-- end list -->

  - *mode de coordination de l'activation du centre de données*  
    Propriété du paramètre DAG qui, s'il est activé, force le service de réplication Microsoft Exchange à obtenir l'autorisation permettant de monter les bases de données au démarrage.

<!-- end list -->

  - *Récupération d'urgence*  
    Tout processus utilisé pour récupérer manuellement suite à une défaillance. Il peut s'agir d'une défaillance qui affecte un seul élément ou un emplacement physique complet.

<!-- end list -->

  - *API de réplication tierce Exchange*  
    API fournie par Exchange qui permet d'utiliser une réplication synchrone tierce pour un groupe de disponibilité de base de données au lieu de la réplication continue.

<!-- end list -->

  - *Disponibilité élevée*  
    Solution qui fournit la disponibilité du service et des données et qui récupère automatiquement suite à des défaillances affectant le service ou les données (telle qu'une défaillance du réseau, de stockage ou du serveur).

<!-- end list -->

  - *Déploiement incrémentiel*  
    Possibilité de déployer la haute disponibilité et la résilience de site après l'installation d'Exchange 2013.

<!-- end list -->

  - *Copie retardée de la base de données de boîtes aux lettres*  
    Copie d'une base de données de boîtes aux lettres dont le retard de relecture du journal est supérieur à zéro.

<!-- end list -->

  - *Copie de base de données de boîtes aux lettres*  
    Base de données de boîtes aux lettres (fichier .edb et journaux) active ou passive.

<!-- end list -->

  - *Résilience de boîte aux lettres*  
    Nom d'une solution unifiée à haute disponibilité et de résilience de site dans Exchange 2013.

<!-- end list -->

  - *Gestion de la disponibilité*  
    Ensemble de processus internes constitué de sondes, d'analyseurs et de répondeurs qui intègrent la surveillance et la haute disponibilité dans tous les rôles serveur et tous les protocoles.

<!-- end list -->

  - *\*over* (prononcé « étoile-over »)  
    Abréviation de *basculements*. Un basculement est une activation manuelle d'une ou de plusieurs copies de bases de données. Un failover est une activation automatique d'une ou de plusieurs copies de bases de données.

<!-- end list -->

  - *Filet de sécurité*  
    Appelée auparavant benne de transport, cette fonction du service de transport stocke une copie de tous les messages pendant *X* jours. Le paramètre par défaut est 2 jours.

<!-- end list -->

  - *Redondance des clichés instantanés*  
    Fonctionnalité du serveur de transport qui fournit la redondance des messages pendant toute la durée de leur transit.

<!-- end list -->

  - *Résilience de site*  
    Configuration qui étend l'infrastructure de messagerie à plusieurs sites Active Directory pour fournir une continuité opérationnelle au système de messagerie en cas d'échec affectant l'un des sites.

Terminologie clé

## Groupes de disponibilité de base de données

Un groupe de disponibilité de base de données est le composant de base de l'architecture de haute disponibilité et de résilience de site intégrée à Exchange 2013. Un DAG est un groupe composé d'un maximum de 16 serveurs de boîtes aux lettres qui hébergent un ensemble de bases de données. Il permet la récupération automatique au niveau de la base de données suite à des échecs affectant des bases de données individuelles, des réseaux ou des serveurs. N'importe quel serveur d'un groupe de disponibilité de base de données peut héberger une copie de base de données de boîtes aux lettres provenant d'un serveur quelconque du groupe de disponibilité de base de données. Lorsqu'un serveur est ajouté à un groupe de disponibilité de base de données, il fonctionne avec les autres serveurs du groupe pour assurer la récupération automatique à la suite de défaillances affectant des bases de données de boîtes aux lettres, par exemple la défaillance d'un disque ou d'un serveur. Pour plus d'informations sur les groupes de disponibilité de base de données, consultez la rubrique [Groupe de disponibilité de base de données (DAG)](database-availability-groups-dags-exchange-2013-help.md).

Terminologie clé

## Copies de bases de données de boîtes aux lettres

Les fonctions de haute disponibilité et de résilience de site intégrées pour la première fois dans Exchange 2010 sont utilisées dans Exchange 2013 pour créer et gérer les copies de base de données. Exchange 2013 exploite également le concept de mobilité de base de données, à savoir les basculements au niveau de la base de données, gérés par Exchange.

La mobilité de base de données déconnecte les bases de données des serveurs et ajoute la prise en charge maximale de 16 copies d'une base de données unique. Elle offre également une expérience native pour la création de copies d'une base de données.

La définition d'une copie de base de données en tant que base de données de boîtes aux lettres active est appelée également *basculement*. Quand une défaillance affectant une base de données ou l'accès à une base de données se produit et qu'une nouvelle base de données devient la copie active, ce processus est appelé *basculement*. Ce processus fait également référence à une défaillance du serveur dans laquelle un ou plusieurs serveurs mettent en ligne les bases de données précédemment en ligne sur le serveur défaillant. Lorsqu'un basculement se produit, les autres serveurs Exchange 2013 en sont informés presque immédiatement et redirigent le trafic client et de messagerie vers la nouvelle base de données active.

Par exemple, si une base de données active dans un groupe de disponibilité de base de données échoue en raison d'une défaillance de stockage sous-jacente, Active Manager procédera à une récupération automatique en basculant une copie de base de données sur un autre serveur de boîtes aux lettres dans le groupe de disponibilité de base de données. Dans Exchange 2013, la disponibilité gérée ajoute de nouveaux comportements pour récupérer d'une perte d'accès du protocole à une base de données, y compris le recyclage des pools de processus d'application, le redémarrage des services et des serveurs, et le lancement des basculements de base de données.

Pour plus d'informations sur les copies de base de données de boîtes aux lettres, consultez la rubrique [Copies de bases de données de boîtes aux lettres](mailbox-database-copies-exchange-2013-help.md).

Terminologie clé

## Active Manager

Exchange 2013 utilise le composant Active Manager intégré pour la première fois dans Exchange 2010 pour gérer l'intégrité, l'état, la réplication continue de la base de données et de la copie de base de données, ainsi que les autres aspects de la haute disponibilité du serveur de boîtes aux lettres. Pour plus d'informations sur Active Manager, consultez la rubrique [Active Manager](active-manager-exchange-2013-help.md).

Terminologie clé

## Résilience de site

Même si Exchange 2013 continue à utiliser les DAG et le clustering avec basculement Windows pour la haute disponibilité et la résilience de site du rôle serveur de boîtes aux lettres, la résilience de site n'est pas identique dans Exchange 2013. La résilience de site est bien meilleure dans Exchange 2013, car elle a été simplifiée. Les changements architecturaux sous-jacents qui ont été effectués dans Exchange 2013 ont un impact significatif sur les éléments de récupération d'une configuration de résilience de site.

Dans Exchange 2010, la récupération de boîte aux lettres (DAG) et d'accès au client (groupe de serveurs d'accès au client) étaient liés. Si vous perdiez tous vos serveurs d'accès au client ou l'adresse IP virtuelle pour le groupe, ou si vous perdiez une partie importante de votre DAG, vous étiez dans l'obligation de procéder à un basculement de centre de données. Il s'agit d'un processus bien documenté et généralement bien compris, même si sa réalisation prend du temps et qu'une intervention humaine est nécessaire pour lancer le processus.

Dans Exchange 2013, si vous perdez votre groupe de serveurs d'accès au client pour une raison quelconque (par exemple, suite à un échec de l'équilibrage de charge), vous ne devez pas effectuer de basculement de centre de données. Si la configuration est correcte, le basculement s'effectue au niveau du client et les clients sont automatiquement redirigés vers un deuxième centre de données comportant des serveurs d'accès au client opérationnels, lesquels renvoient par proxy les communications vers le serveur de boîtes aux lettres de l'utilisateur, qui n'est pas touché par l'interruption (car vous n'effectuez aucun basculement). Vous n'avez pas besoin de travailler à la récupération du service, car le service se restaure lui-même de façon à ce que vous puissiez vous concentrer sur la résolution de l'erreur principale (par exemple, le remplacement de l'équilibrage de charge défaillant).

De plus, avec la simplification de l'espace de noms, la consolidation des rôles serveur, la dissociation des conditions requises du rôle serveur de site Active Directory, la séparation de la récupération du DAG et du groupe de serveurs d'accès au client, mais aussi avec les modifications apportées à l'équilibrage de charge, les changements apportés à Exchange 2013 permettent désormais de récupérer le groupe de serveurs d'accès au client et le DAG séparément et automatiquement sur tous les sites, offrant de ce fait des scénarios de basculement de centre de données si vous avez trois emplacements.

Dans Exchange 2010, vous pouviez déployer un DAG dans deux centres de données et héberger le témoin dans un troisième, puis activer le basculement pour le rôle serveur de boîtes aux lettres pour l'un d'eux. Toutefois, vous n'obteniez pas le basculement de la solution proprement dite, car l'espace de noms devait toujours être manuellement modifié pour les rôles autres que serveur de boîtes aux lettres.

Dans Exchange 2013, il n'est pas nécessaire de déplacer l'espace de noms en même temps que le DAG. Exchange tire partir de la tolérance de panne intégrée à l'espace de noms par le biais de plusieurs adresses IP et de l'équilibrage de charge (et, si nécessaire, la possibilité de mettre des serveurs en service et hors service). Les clients HTTP modernes fonctionnent automatiquement avec cette redondance. La pile HTTP peut accepter plusieurs adresses IP pour un nom de domaine complet (FQDN). Si la première adresse IP qu'elle teste subit une défaillance matérielle (c'est-à-dire qu'elle ne peut pas se connecter), elle teste l'adresse IP suivante dans la liste. Si la défaillance est logicielle (perte de connexion une fois la session établie, peut-être en raison d'une défaillance intermittente du service lorsque, par exemple, un périphérique dépose des paquets et doit être mis hors service), l'utilisateur doit éventuellement actualiser son navigateur.

Cela signifie que l'espace de noms n'est plus un point de défaillance unique, comme il l'était dans Exchange 2010. Dans Exchange 2010, le point de défaillance unique le plus important dans le système de messagerie est peut-être le nom de domaine complet (FQDN) que vous donnez aux utilisateurs, car il indique où aller à l'utilisateur. Dans le paradigme Exchange 2010, il n'est pas si simple de changer l'emplacement cible de ce nom de domaine complet (FQDN), car vous devez modifier le DNS, puis gérer la latence DNS, ce qui est problématique dans certaines régions du monde. Et vous avez, dans les navigateurs, des caches de noms qui sont généralement d'environ 30 minutes, voire plus, que vous devez également prendre en compte.

L'une des modifications apportées à Exchange 2013 est de permettre aux clients d'accéder à plusieurs emplacements. Si l'on suppose que le client peut accéder à plusieurs emplacements (presque tous les protocoles d'accès au client dans Exchange 2013 sont basés sur HTTP -par exemple, Outlook, Outlook Anywhere, EAS, EWS, OWA et CAE- et tous les clients HTTP pris en charge peuvent utiliser plusieurs adresses IP), le basculement est possible côté client. Vous pouvez configurer DNS pour traiter plusieurs adresses IP vers un client lors de la résolution de noms. Le client demande mail.contoso.com et retourne deux adresses IP, ou quatre adresses IP, par exemple. Néanmoins, de nombreuses adresses IP retournées par le client seront utilisées de façon fiable par celui-ci. Cela s'avère bénéfique pour le client, car si l'une des adresses IP échoue, le client peut en utiliser une ou plusieurs autres adresses IP pour se connecter. Si un client en essaie une mais qu'elle échoue, il patiente environ 20 secondes, puis essaie la suivante dans la liste. Ainsi, si vous perdez l'adresse IP virtuelle pour le groupe de serveurs d'accès au client, la récupération des clients s'effectue automatiquement et dans un délai d'environ 21 secondes.

Les avantages sont les suivants :

  - Dans Exchange 2010, si vous perdiez l'équilibrage de charge dans votre centre de données principal et n'en aviez pas d'autre sur ce site, vous deviez effectuer un basculement de centre de données. Dans Exchange 2013, si vous perdez l'équilibrage de charge dans votre site principal, il suffit de le désactiver (ou de désactiver l'adresse IP virtuelle), puis de le réparer ou le remplacer. Les clients qui n'utilisent pas encore l'adresse IP virtuelle du deuxième centre de données basculent automatiquement vers la deuxième adresse IP virtuelle sans aucune modification de l'espace de noms et du DNS. Non seulement cela signifie qu'il n'est plus nécessaire d'effectuer un basculement, mais également que tout le temps normalement associé à une récupération par basculement du centre de données n'est pas gaspillé. Dans Exchange 2010, vous deviez gérer la latence DNS (d'où la recommandation de définir la valeur de durée de vie (TTL) sur 5 minutes et l'introduction de l'URL de restauration automatique). Dans Exchange 2013, cette opération n'est pas nécessaire, car vous bénéficiez d'un basculement rapide (20 secondes) de l'espace de noms entre les adresses IP virtuelles (centres de données).

  - Comme vous pouvez faire basculer l'espace de noms entre des centres de données, tout ce dont vous avez besoin pour réaliser un basculement du centre de données, c'est d'un mécanisme de basculement du rôle serveur de boîtes aux lettres entre centres de données. Pour bénéficier d'un basculement automatique pour le DAG, vous concevez simplement une solution dans laquelle le DAG est uniformément réparti entre deux centres de données, puis placez le serveur témoin dans un troisième emplacement afin qu'il puisse être arbitré par des membres du DAG dans chaque centre de données, quel que soit l'état du réseau entre les centres de données contenant les membres du DAG. Si vous n'avez que deux centres de données et qu'un troisième emplacement physique n'est pas disponible, vous pouvez placer le serveur témoin sur une machine virtuelle Microsoft Azure. Pour plus d’informations, consultez la rubrique [Utilisation d'une machine virtuelle Microsoft Azure comme serveur témoin du groupe de disponibilité de base de données (DAG)](using-a-microsoft-azure-vm-as-a-dag-witness-server-exchange-2013-help.md).

  - Dans ce scénario, les efforts de l'administrateur sont axés sur la simple résolution du problème, non sur la restauration du service. Vous réparez simplement le composant défaillant, tandis que le service a été exécuté et l'intégrité préservée. L'urgence et le niveau de stress ressentis lors de la réparation d'un périphérique défaillant ne aucun commune mesure avec ce que vous ressentez lorsque vous travaillez à la restauration du service. Cela est préférable et pour l'utilisateur final et moins stressant pour l'administrateur.

Vous pouvez permettre le basculement sans devoir effectuer de switchbacks (parfois appelés par erreur « restaurations automatiques »). Si vous perdez les serveurs d'accès au client dans votre centre de données principal et qu'il en résulte une interruption de 20 secondes pour les clients, vous ne devez peut-être même pas effectuer de restauration automatique. À ce stade, votre première préoccupation doit être de résoudre le problème principal (par exemple, remplacer l'équilibrage de charge défaillant). Une fois que tout fonctionne à nouveau, certains clients commencent à utiliser le centre de données, tandis que d'autres restent opérationnels via le deuxième centre de données.

Exchange 2013 fournit également des fonctionnalités qui permettent aux administrateurs de gérer les défaillances intermittentes. Une défaillance intermittente est, par exemple, une situation où la connexion TCP initiale peut être établie, mais où ne se passe par la suite. Une défaillance intermittente nécessite une sorte d'action administrative supplémentaire, car elle peut résulter de la mise en service d'un appareil de rechange. Au cours de ce processus de réparation, l'appareil peut être allumé et accepter certaines demandes, mais ne pas être vraiment prêt à servir des clients tant que la procédure de configuration nécessaire n'a pas été réalisée. Dans ce scénario, l'administrateur peut procéder à un basculement de l'espace de noms en supprimant simplement le VIP pour l'appareil remplacé dans le DNS. Ainsi, au cours de cette période de maintenance, aucun client ne tentera de s'y connecter. Une fois le processus de remplacement terminé, l'administrateur peut rajouter l'adresse IP virtuelle au DNS, et les clients commencent à l'utiliser.

Pour plus de détails sur la planification et le déploiement de la résilience de site, consultez les rubriques [Planification d'une haute disponibilité et d'une résilience de site](planning-for-high-availability-and-site-resilience-exchange-2013-help.md) et [Déploiement de haute disponibilité et de résilience de site](deploying-high-availability-and-site-resilience-exchange-2013-help.md).

Terminologie clé

## API de réplication tierce

Exchange 2013 comprend également une API de réplication tierce qui permet aux organisations d'utiliser des solutions de réplication synchrone tierces à la place de la fonctionnalité intégrée de réplication continue. Microsoft prend en charge des solutions tierces qui utilisent cette API pour autant qu'elles fournissent les fonctionnalités nécessaires pour remplacer toutes les fonctionnalités de réplication continue natives désactivées à cause de l'utilisation de l'API. Ces solutions sont uniquement prises en charge lorsque l'API est utilisée au sein d'un groupe de disponibilité de base de données pour gérer et activer les copies de bases de données de boîtes aux lettres. L'utilisation de l'API en dehors de ces limites n'est pas prise en charge. En outre, la solution doit satisfaire aux conditions de prise en charge du matériel Windows applicables. (aucune validation par test n'est requise pour la prise en charge.)

Lors du déploiement d'une solution qui utilise l'API de réplication tierce intégrée, sachez que le fournisseur de la solution est responsable du support technique principal de cette solution. Microsoft prend en charge les données Exchange à la fois pour les solutions répliquées et non répliquées. Les solutions qui utilisent une réplication de données doivent adhérer à la stratégie de support Microsoft relative à la réplication de données, telle que décrite dans l'article 895847 de la base de connaissances Microsoft intitulé [Prise en charge de la réplication multi-site de données d'Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=3052%26kbid=895847). De plus, les solutions qui utilisent le modèle de ressources Cluster de basculement Windows doivent satisfaire aux exigences en matière de capacités de prise en charge des clusters Windows, telles que décrites dans l'article 943984 de la base de connaissances Microsoft intitulé [Stratégie de support Microsoft pour les clusters à basculement Windows Server 2008 ou Windows Server 2008 R2](https://go.microsoft.com/fwlink/p/?linkid=3052%26kbid=943984) ou dans l'article [Politique de support Microsoft pour les clusters de basculement Windows Server 2012](https://go.microsoft.com/fwlink/p/?linkid=3052%26kbid=2775067).

La stratégie de support de Microsoft en matière de sauvegarde et de restauration pour les déploiements qui utilisent des solutions API de réplication tierces est la même que pour les déploiements de réplication continue natifs.

Si vous êtes un partenaire à la recherche d'informations sur l'API tierce, contactez votre représentant Microsoft.

Terminologie clé

## Documentation relative à la haute disponibilité et à la résilience de site

Le tableau suivant contient les liens vers les rubriques qui vous aideront à comprendre le fonctionnement et la gestion des DAG, des copies de base de données de boîtes aux lettres, mais aussi de la sauvegarde et de la restauration pour Exchange 2013.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Rubrique</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="database-availability-groups-dags-exchange-2013-help.md">Groupe de disponibilité de base de données (DAG)</a></p></td>
<td><p>En savoir plus sur les DAG, Active Manager, le mode Datacenter Activation Coordination (DAC) et les copies de base de données de boîtes aux lettres.</p></td>
</tr>
<tr class="even">
<td><p><a href="planning-for-high-availability-and-site-resilience-exchange-2013-help.md">Planification d'une haute disponibilité et d'une résilience de site</a></p></td>
<td><p>En savoir plus sur le fonctionnement général, le matériel, le logiciel, le serveur témoin et les autres exigences et meilleures pratiques pour les DAG.</p></td>
</tr>
<tr class="odd">
<td><p><a href="deploying-high-availability-and-site-resilience-exchange-2013-help.md">Déploiement de haute disponibilité et de résilience de site</a></p></td>
<td><p>Découvrez un exemple de scénario de déploiement pour le déploiement et la configuration des DAG.</p></td>
</tr>
<tr class="even">
<td><p><a href="managing-high-availability-and-site-resilience-exchange-2013-help.md">Gestion de la haute disponibilité et de la résilience de site</a></p></td>
<td><p>En savoir plus sur les tâches de gestion de DAG, les basculements, ainsi que le mode maintenance.</p></td>
</tr>
<tr class="odd">
<td><p><a href="monitoring-database-availability-groups-exchange-2013-help.md">Surveillance des groupes de disponibilité des bases de données</a></p></td>
<td><p>En savoir plus sur les cmdlets et les scripts intégrés pour la surveillance des DAG et des copies de base de données.</p></td>
</tr>
<tr class="even">
<td><p><a href="backup-restore-and-disaster-recovery-exchange-2013-help.md">Sauvegarde, restauration et récupération d’urgence</a></p></td>
<td><p>En savoir plus sur la sauvegarde et la restauration des bases de données Exchange, les bases de données de récupération et la récupération de serveur.</p></td>
</tr>
</tbody>
</table>


Terminologie clé

