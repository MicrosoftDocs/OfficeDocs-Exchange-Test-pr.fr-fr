---
title: 'Modif. de la haute dispo. et de la résilience de site par rapp. aux vrs préc.'
TOCTitle: Modifications apportées à la haute disponibilité et la résilience de site par rapport aux versions précédentes
ms:assetid: de53c00b-091c-4a31-aacc-1bd40c756ce2
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dn789066(v=EXCHG.150)
ms:contentKeyID: 62519736
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Modifications apportées à la haute disponibilité et la résilience de site par rapport aux versions précédentes

 

_**Sapplique à :** Exchange Server 2013 SP1_

_**Dernière rubrique modifiée :** 2015-04-07_

Exchange 2013 utilise des groupes de disponibilité de base de données et des copies de bases de données de boîtes aux lettres, en plus d’autres fonctionnalités comme la récupération d’élément unique, les stratégies de rétention et les copies de bases de données retardées pour fournir la haute disponibilité, la résilience de site et la protection des données natives d’Exchange. La plateforme de haute disponibilité, la banque d’informations Exchange et le moteur de stockage extensible (ESE) ont tous été améliorés pour offrir une plus grande disponibilité, une gestion plus facile et une réduction des coûts. Ces améliorations sont les suivantes :

  - **Réduction des opérations d’entrée et de sortie par seconde (E/S par seconde) par rapport à Exchange 2010**   Cela vous permet de bénéficier de disques disposant d’une capacité plus élevée et d’E/S par seconde aussi efficaces que possible.

  - **Disponibilité gérée**   Avec la disponibilité gérée, la surveillance interne et les fonctionnalités orientées récupération sont étroitement intégrées afin d’aider à prévenir les défaillances, à restaurer proactivement les services et à initialiser les basculements automatiques de serveurs ou à alerter les administrateurs afin qu’ils prennent des mesures. L’accent est mis sur le suivi et la gestion de l’expérience utilisateur final plutôt que simplement sur le temps d’activité du serveur et des composants pour contribuer à la conservation d’une disponibilité permanente du service.

  - **Banque gérée**   La Banque gérée est le nom donné aux processus de la Banque d’informations qui ont été réécrits sous Exchange 2013. La nouvelle Banque gérée est écrite en C\# et elle est étroitement intégrée avec le Service de réplication Microsoft Exchange (MSExchangeRepl.exe) afin de fournir une plus grande disponibilité grâce à une résilience accrue.

  - **Prise en charge de bases de données multiples par disque** Exchange 2013 comprend des améliorations qui vous permettent de prendre en charge de bases de données multiples (mélange de copies actives et passives) sur le même disque, ce qui améliore l’efficacité des disques en tirant parti d’une plus grande capacité et d’un nombre d’opérations d’E/S par seconde accru.

  - **AutoReseed**   Le réamorçage automatique vous permet de restaurer rapidement la redondance des bases de données après une défaillance de disque. Si un disque est défectueux, la copie de la base de données stockée sur ce disque est copiée à partir de la copie de base de données active vers un disque de rechange sur le même serveur. Si plusieurs copies de bases de données ont été stockées sur le disque défectueux, elles peuvent toutes être automatiquement réamorcées sur un disque de rechange. Cela permet des réamorçages plus rapides, car les bases de données actives se trouvent probablement sur de multiples serveurs et les données sont copiées de manière parallèle.

  - **Récupération automatique après défaillance du stockage**   Cette fonctionnalité se situe dans la continuité des innovations lancées par Exchange 2010 afin de permettre une récupération système après des défaillances qui ont une incidence sur la résilience ou la redondance. En plus des vérifications d’erreur d’Exchange 2010, Exchange 2013 présente des fonctionnalités de récupération supplémentaires pour les temps d’E/S élevés, l’utilisation excessive de mémoire par MSExchangeRepl.exe et les cas extrêmes où le système est dans un tel état que les threads ne peuvent pas être planifiés.

  - **Améliorations apportées aux copies retardées**   Les copies retardées se gèrent de manière plus autonome grâce à l’exécution de la journalisation automatique. Les copies retardées liront automatiquement les fichiers journaux dans différentes situations, telles que la mise à jour corrective de pages et les scénarios d’espace disque faible. Si le système détecte que la mise à jour corrective de pages est nécessaire pour une copie retardée, les journaux seront automatiquement relus dans la copie retardée pour exécuter la mise à jour corrective de pages. Les copies retardées appelleront également cette fonction de relecture automatique lorsque le seuil d’espace disque faible a été atteint et lorsque la copie retardée a été détectée comme étant la seule copie disponible pendant une période spécifique. De plus, les copies retardées peuvent tirer parti de Safety Net, ce qui facilite la récupération ou l’activation.

  - **Améliorations apportées aux alertes de copie unique**   L’alerte de copie unique introduite dans Exchange 2010 n’est plus un script planifié de manière séparée. Elle est maintenant intégrée aux composants de disponibilité gérée au sein du système et constitue une fonction native dans Exchange.

  - **Auto-configuration du réseau DAG**   Les réseaux de groupes de disponibilité des bases de données (DAG) peuvent être automatiquement configurés par le système en fonction de paramètres de configuration. En plus des options de configuration manuelle, les DAG peuvent aussi faire la distinction entre les réseaux de réplication et MAPI, et configurer des réseaux DAG automatiquement.

## Réduction du nombre d’opération d’E/S par seconde par rapport à Exchange 2010

Dans Exchange 2010, les copies de base de données passives ont une très faible profondeur de point de contrôle, ce qui est nécessaire pour un basculement rapide. En outre, la copie passive effectue une prélecture agressive des données afin de maintenir une profondeur de point de contrôle de 5 mégaoctets (Mo). En raison de l’utilisation d’une faible profondeur de point de contrôle et de la réalisation de ces opérations de prélecture agressive, le nom d’E/S par seconde d’une copie de base de données passive était égal à celui d’une copie active dans Exchange 2010.

Dans Exchange 2013, le système peut fournir un basculement rapide tout en utilisant une grande profondeur de point de contrôle sur la copie passive (100 Mo). Puisque les copies passives ont une profondeur de point de contrôle de 100 Mo, elles ont été déréglées pour ne plus être aussi agressives. En raison de l’augmentation de la profondeur de point de contrôle et du déréglage des prélectures agressives, le nombre d’E/S par seconde d’une copie passive correspond à environ la moitié de celui de la copie active dans Exchange 2013.

La définition d’une plus grande profondeur de point de contrôle sur la copie passive génère également d’autres changements. Lors du basculement dans Exchange 2010, le cache de base de données est vidé, car la base de données est convertie d’une copie passive en une copie active. Dans Exchange 2013, la journalisation ESE a été réécrite pour que le cache soit conservé lors de la transition de la copie passive en copie active. Comme ESE n’a pas besoin de vider le cache, vous bénéficiez d’un basculement rapide.

Une autre modification a été apportée au processus de maintenance de base de données en arrière-plan. Ce processus traite désormais environ 1 à 2 Mo par seconde et par copie.

Le résultat de ces changements est qu’Exchange 2013 offre une diminution de moitié du nombre d’E/S par seconde par rapport à Exchange 2010.

## Disponibilité gérée

La disponibilité gérée est l’intégration de la surveillance intégrée et active et de la plateforme de haute disponibilité Exchange 2013. Grâce à la disponibilité gérée, le système peut déterminer le moment approprié pour basculer une base de données en fonction de l’état du service. La disponibilité gérée est une infrastructure interne qui est déployée sur les rôles serveur d’accès au client et de boîtes aux lettres dans Exchange 2013. La disponibilité gérée comprend trois principaux composants asynchrones qui fonctionnent en permanence. Le premier composant est le moteur de sonde chargé de la prise de mesures sur le serveur et de la collecte de données. Les résultats de ces mesures sont transférés vers le deuxième composant, le moniteur. Le moniteur contient toute la logique métier utilisée par le système sur la base de ce qui doit être ou non considéré comme intègre sur les données collectées. Comme un moteur de reconnaissance de suites logiques, le moniteur recherche les différentes suites logiques sur toutes les mesures collectées, puis détermine ce qu’il considère comme intègre. Enfin, il y a le moteur de répondeur, qui est chargé des mesures de récupération. Lorsqu’un élément est défectueux, la première mesure consiste à tenter de récupérer ce composant. Ces actions peuvent se dérouler en plusieurs phases. Par exemple, la première tentative peut être le redémarrage du pool d’applications, la seconde le redémarrage du service, la troisième le redémarrage du serveur et la quatrième la déconnexion du serveur de façon à ce qu’il n’accepte plus de trafic. Si les mesures de récupération ont échoué, le système transfère le problème à un être humain grâce à des notifications dans le journal d’événements.

La disponibilité gérée est implémentée sous la forme de deux services :

  - **Exchange Health Manager Service (MSExchangeHMHost.exe)**   Il s’agit d’un processus contrôleur qui permet de gérer les processus de travail. Il est utilisé pour créer, exécuter, démarrer et arrêter le processus de travail selon les besoins. Il est également utilisé pour récupérer le processus de travail en cas de blocage afin d’empêcher que le processus de travail soit un point de défaillance unique.

  - **Processus Exchange Health Manager Worker (MSExchangeHMWorker.exe)**   Il s’agit du processus de travail chargé d’effectuer les tâches d’exécution.

La disponibilité gérée utilise un stockage persistant pour remplir ses fonctions :

  - Les fichiers de configuration XML sont utilisés pour initialiser les définitions d’éléments de travail lors du démarrage du processus de travail.

  - Le registre est utilisé pour stocker des données d’exécution, telles que des signets.

  - L’infrastructure de journal des événements du canal Crimson est utilisée pour stocker les résultats d’éléments de travail.

Pour plus d’informations sur la disponibilité gérée, consultez la rubrique [Disponibilité gérée](managed-availability-exchange-2013-help.md).

## Banque gérée

Toutes les versions antérieures d’Exchange Server, d’Exchange Server 4.0 à Exchange Server 2010, prennent en charge l’exécution d’une seule instance du processus de la banque d’informations (Store.exe) sur le rôle serveur de boîte aux lettres. Cette instance de banque unique héberge toutes les bases de données sur le serveur : actives, passives, retardées et de récupération. Dans les architectures Exchange précédentes, il y avait parfois une isolation minime, voire inexistante, entre les différentes bases de données hébergées sur un serveur de boîtes aux lettres. Un problème avec une seule base de données de boîtes aux lettres peut avoir un impact négatif sur toutes les autres bases de données, et les incidents résultant d’un endommagement de boîte aux lettres peuvent influer sur le service pour tous les utilisateurs dont les bases de données sont hébergées sur ce serveur.

L’autre défi avec une seule instance de banque dans les versions précédentes d’Exchange tient au fait que le moteur de stockage extensible (ESE) s’adapte bien de 8 à 12 cœurs de processeur. Au-delà, cependant, les problèmes de communication entre les processeurs et de synchronisation du cache entraînent un redimensionnement négatif. Étant donné que les serveurs actuels sont beaucoup plus importants, et qu’ils proposent plus de 16 systèmes centraux, cela compliquerait la gestion de l’affinité des 8 à 12 cœurs pour ESE, les autres cœurs servant pour les processus non liés à la banque (par exemple, les assistants, la tâche Rechercher la fondation, la disponibilité gérée, etc.). En outre, l’architecture précédente restreignait la mise à l’échelle pour le processus de banque.

Le processus Store.exe a considérablement évolué au fil des années, tout comme Exchange Server. Toutefois, en tant que processus unique, à terme, son évolutivité est limitée, et il représente un point de défaillance unique. En raison de ces limites, Store.exe a été abandonné dans Exchange 2013 et remplacé par la banque gérée.

Pour plus d’informations, voir [Banque gérée](managed-store-exchange-2013-help.md).

## Plusieurs bases de données par volume

Même si les améliorations apportées au stockage dans Exchange 2013 sont d’abord conçues pour les configurations JBOD, elles peuvent être utilisées par toutes les configurations de stockage prises en charge. L’une des fonctionnalités est la possibilité d’héberger plusieurs bases de données sur le même volume. Cette fonctionnalité vise à optimiser Exchange pour les grands disques. Ces optimisations permettent une utilisation beaucoup plus efficace des disques disposant d’une capacité élevée, d’E/S par seconde et de durées de réamorçage, et elles permettent de relever les défis associés à l’exécution dans une configuration de stockage JBOD :

  - Les tailles de base de données doivent pouvoir être gérées.

  - Les opérations de réamorçage doivent être rapides et fiables.

  - La capacité de stockage augmente, contrairement aux E/S par seconde.

  - Les disques qui hébergent les copies de base de données passives sont sous-utilisés pour ce qui est des E/S par seconde.

  - Les copies retardées ont des exigences de stockage asymétriques.

  - Vous avez peu de marge de manœuvre pour effectuer une récupération à partir d’un espace disque faible.

La tendance à l’augmentation des capacités de stockage continue ; des lecteurs 8 téraoctets (To) seront en effet bientôt disponibles. Si vous utilisez des lecteurs de 8 téraoctets (To) et que vous suivez les meilleures pratiques Exchange relatives à la taille maximale des bases de données (2 téraoctets), vous gaspillez plus de 5 téraoctets d’espace disque. Une solution consiste à augmenter la taille des bases de données. Toutefois, elle réduit la facilité de gestion, car de longs délais de réamorçage sont nécessaires et, dans certains cas, les délais de réamorçage deviennent ingérables sur le plan opérationnel, et la fiabilité de la copie de cette quantité de données sur le réseau est compromise.

De plus, dans le modèle Exchange 2010, le disque qui stocke une copie passive est sous-exploité en E/S par seconde. En cas de copie passive retardée, non seulement le disque est sous-exploité en E/S par seconde, mais il est aussi asymétrique par sa taille, par rapport aux disques employés pour stocker les copies actives et passives non retardées.

Afin de poursuivre une pratique bien établie, Exchange 2013 est optimisé de façon à pouvoir utiliser plus efficacement des disques de grande taille (8 To) dans une configuration JBOD. Dans Exchange 2013, avec plusieurs bases de données par disque, des disques de même taille peuvent stocker plusieurs copies de base de données, y compris des copies retardées. L’objectif est de gérer la répartition des utilisateurs sur les différents volumes existants, ce qui vous permet de bénéficier d’une conception symétrique où, lors des opérations normales, chaque membre du DAG héberge une combinaison de copies actives, passives et parfois retardées sur les mêmes volumes.

Vous trouverez ci-dessous un exemple de configuration qui utilise plusieurs bases de données par volume.

**Configuration utilisant plusieurs bases de données par volume**

![Plusieurs bases de données par volume](images/Dn789066.c5e7d6c8-3e77-4f72-a873-5e9aaded9aa3(EXCHG.150).gif "Plusieurs bases de données par volume")

La configuration ci-dessus offre une conception symétrique. Les quatre serveurs ont les quatre mêmes bases de données, qui sont toutes hébergées sur un seul disque par serveur. L’élément clé est que le nombre de copies de chaque base de données dont vous disposez doit être égal au nombre de copies de base de données sur chaque disque. Dans l’exemple ci-dessus, il existe quatre copies de chaque base de données : une copie active, deux copies passives et une copie retardée. Puisqu’il existe quatre copies de chaque base de données, la bonne configuration est celle qui comporte quatre copies par volume. En outre, la préférence d’activation est configurée afin d’être équilibrée dans le DAG et sur chaque serveur. Par exemple, la copie active aura une valeur de préférence d’activation de 1, la première copie passive une valeur de préférence d’activation de 2, la deuxième copie passive une valeur de préférence d’activation de 3 et la copie retardée une valeur de préférence d’activation de 4.

En plus de fournir une meilleure répartition des utilisateurs dans les volumes existants, l’utilisation de plusieurs bases de données par disque offre l’avantage supplémentaire de réduire la durée de restauration de la protection des données en cas de défaillance nécessitant un réamorçage (par exemple, une défaillance de disque).

À mesure que la taille d’une base de données augmente, son réamorçage prend de plus en plus de temps. Par exemple, le réamorçage d’une base de données de 2 téraoctets peut prendre 23 heures, alors que le réamorçage d’une base de données de 8 téraoctets peut prendre jusqu’à 93 heures (presque 4 jours). Les deux amorçages se produiraient à une fréquence moyenne de 20 Mo par seconde. Cela signifie généralement qu’une base de données de très grande taille ne peut pas être amorcée dans un délai raisonnable sur le plan opérationnel.

Dans un scénario impliquant une seule copie de base de données par disque, l’opération d’amorçage est effectivement liée à la source, car elle amorce toujours le disque à partir d’une seule source. En divisant le volume en plusieurs copies de base de données et en stockant sur des membres de DAG distincts la copie active des bases de données passives d’un volume donné, le système n’est plus lié à la source dans le contexte de réamorçage du disque. Lorsqu’un disque défectueux est remplacé, il peut être réamorcé depuis plusieurs sources. Cela permet au système de réamorcer et de restaurer la protection des données pour ces bases de données dans un délai beaucoup plus court.

Si vous utilisez plusieurs bases de données par volume, nous vous recommandons de respecter les meilleures pratiques et exigences suivantes :

  - Utilisez une seule partition de disque logique unique par disque physique. Ne créez pas plusieurs partitions sur le disque. Chaque copie de base de données et ses fichiers compagnons (tels que les journaux des transactions et l’index de contenu) doivent être hébergés dans un répertoire unique de la partition unique.

  - Le nombre de copies de base de données configurées par volume doit être égal au nombre de copies de chaque base de données. Par exemple, si vous avez quatre copies de vos bases de données, vous devez utiliser quatre copies de base de données par volume.

  - Les copies de base de données doivent avoir les mêmes voisins. (par exemple, elles doivent toutes partager le même disque sur chaque serveur.)

  - La préférence d’activation sur le DAG doit être équilibrée afin que chaque copie de base de données sur un disque ait une valeur unique de préférence d’activation.

## AutoReseed

La fonctionnalité de réamorçage automatique, AutoReseed, remplace une action généralement initiée par l’administrateur en cas de défaillance d’un disque, d’endommagement d’une base de données ou de tout autre problème nécessitant le réamorçage d’une copie de base de données. La fonctionnalité AutoReseed permet de restaurer automatiquement la redondance de base de données après une défaillance de disque par le biais de disques de rechange qui ont été configurés sur le système.

Pour plus d’informations, voir [AutoReseed](autoreseed-exchange-2013-help.md). Pour obtenir la procédure détaillée de configuration de la fonctionnalité AutoReseed, voir [Configuration d’AutoReseed pour un groupe de disponibilité de base de données](configure-autoreseed-for-a-database-availability-group-exchange-2013-help.md).

## Récupération automatique suite à des défaillances de stockage

La récupération automatique suite à des défaillances de stockage s’inscrit dans la continuité des innovations initiées dans Exchange 2010 afin de permettre la récupération du système suite à des défaillances ayant une incidence sur la résilience ou la redondance. Outre les comportements de vérification d’erreur Exchange 2010, Exchange 2013 inclut des comportements de récupération supplémentaires pour les temps d’E/S élevés, l’utilisation excessive de mémoire par le service de réplication Microsoft Exchange (MSExchangeRepl.exe) et des cas sérieux où il n’est pas possible de planifier les threads.

Même dans les environnements JBOD, les contrôleurs de baies de stockage peuvent rencontrer des problèmes, tels qu’un arrêt ou un blocage. Exchange 2010 incluait des fonctionnalités de détection et de récupération des E/S bloquées qui assuraient une meilleure résilience. Ces fonctions sont répertoriées dans le tableau suivant.


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
<th>Vérification</th>
<th>Action</th>
<th>Seuil</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Détection des E/S bloquées de la base de données ESE</p></td>
<td><p>ESE recherche la présence d’E/S exceptionnelles</p></td>
<td><p>Génère un élément de défaillance dans le canal Crimson pour redémarrer le serveur</p></td>
<td><p>240 secondes</p></td>
</tr>
<tr class="even">
<td><p>Pulsation du canal des éléments défectueux</p></td>
<td><p>S’assure que les éléments de défaillance peuvent être écrits vers le canal Crimson et lus à partir de ce dernier</p></td>
<td><p>Le service de réplication contrôle la pulsation du canal Crimson et redémarre le serveur suite à des défaillances</p></td>
<td><p>30 secondes</p></td>
</tr>
<tr class="odd">
<td><p>Pulsation de disque système</p></td>
<td><p>Vérifie l’état du disque système du serveur</p></td>
<td><p>Envoie régulièrement des E/S non mises en mémoire tampon au disque système ; redémarre le serveur à l’expiration du délai de pulsation</p></td>
<td><p>120 secondes</p></td>
</tr>
</tbody>
</table>


Exchange 2013 améliore la résilience du serveur et du stockage en incluant de nouveaux comportements pour d’autres situations sérieuses. Ces conditions et comportements sont décrits dans le tableau suivant.


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
<th>Vérification</th>
<th>Action</th>
<th>Seuil</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>État du système incorrect</p></td>
<td><p>Aucun thread, y compris les threads non gérés, ne peut être planifié</p></td>
<td><p>Redémarrer le serveur</p></td>
<td><p>302 secondes</p></td>
</tr>
<tr class="even">
<td><p>Temps d’E/S élevés</p></td>
<td><p>Mesures de la latence de fonctionnement des E/S</p></td>
<td><p>Redémarrer le serveur</p></td>
<td><p>41 secondes</p></td>
</tr>
<tr class="odd">
<td><p>Utilisation de la mémoire du service de réplication</p></td>
<td><p>Mesurer la plage de travail de MSExchangeRepl.exe</p></td>
<td><ol>
<li><p>Enregistrer l’événement 4395 dans le canal Crimson avec une demande de fin de service</p></li>
<li><p>Initier la fin de MSExchangeRepl.exe</p></li>
<li><p>Si la fin du service échoue, redémarrer le serveur</p></li>
</ol></td>
<td><p>4 gigaoctets (Go)</p></td>
</tr>
<tr class="even">
<td><p>Événement système 129 (réinitialisation du bus)</p></td>
<td><p>Vérifier la présence de l’événement 129 dans les journaux des événements système</p></td>
<td><p>Redémarrer le serveur</p></td>
<td><p>Lorsque l’événement se produit</p></td>
</tr>
<tr class="odd">
<td><p>Blocage de la base de données de cluster</p></td>
<td><p>Les mises à jour du Gestionnaire de mises à jour globales sont bloquées</p></td>
<td><p>Redémarrer le serveur</p></td>
<td><p>Lorsque l’événement se produit</p></td>
</tr>
</tbody>
</table>


## Améliorations apportées à la copie retardée

Les améliorations apportées à la copie retardée incluent l’intégration à Safety Net et la lecture automatique des fichiers journaux dans certains scénarios. Safety Net est une fonction de transport qui remplace la fonction Exchange 2010 appelée benne de transport. Safety Net est semblable à une benne de transport, car il s’agit d’une file d’attente de remise qui est associée au service de transport sur un serveur de boîtes aux lettres. Cette file d’attente stocke les copies des messages qui ont été correctement remis à la base de données de boîtes aux lettres active sur le serveur de boîtes aux lettres. Chaque base de données de boîtes aux lettres active sur le serveur de boîtes aux lettres a sa propre file d’attente qui stocke les copies des messages remis. Vous pouvez spécifier la durée pendant laquelle Safety Net stocke les copies des messages correctement remis avant leur expiration et leur suppression automatique.

Safety Net assume une part de responsabilité en ce qui concerne la redondance des clichés instantanés dans des environnements DAG. Dans les environnements DAG, la redondance des clichés instantanés n’a pas besoin de conserver une autre copie du message remis dans une file d’attente de clichés instantanés pendant qu’elle attend que message remis soit répliqué vers les copies passives des bases de données de boîtes aux lettres sur les autres serveurs de boîtes aux lettres du DAG. La copie du message remis est déjà stockée dans Safety Net. Ainsi, la redondance des clichés instantanés peut de nouveau remettre le message à partir de Safety Net si nécessaire.

Avec Safety Net, l’activation d’une copie de base de données retardée devient beaucoup plus simple. Par exemple, supposons qu’il existe une copie retardée dont le délai d’attente de relecture est de 2 jours. Dans ce cas, vous devez configurer Safety Net pour une période de 2 jours. Si vous vous retrouvez dans une situation où vous devez utiliser votre copie retardée, vous pouvez suspendre la réplication vers celle-ci et la copier deux fois (afin de conserver la nature retardée de la base de données et de créer une copie supplémentaire au cas où vous en auriez besoin). Ensuite, prenez une copie et supprimez tous les fichiers journaux, à l’exception de ceux qui se trouvent dans la plage requise. Montez la copie, ce qui déclenche l’envoi d’une demande automatique à Safety Net pour remettre de nouveau les messages électroniques des deux derniers jours. Grâce à Safety Net, vous n’avez pas besoin de rechercher le point de départ de l’endommagement. Vous recevez le courrier électronique des deux derniers jours, moins les données habituellement perdues lors d’un basculement avec perte.

Les copies retardées peuvent désormais se gérer elles-mêmes en appelant la relecture automatique des journaux pour lire les fichiers journaux dans certains scénarios :

  - Lorsque le seuil d’espace disque faible est atteint

  - Lorsque la copie retardée est physiquement endommagée et doit faire l’objet d’une mise à jour corrective de pages

  - Quand il y a moins de trois copies intègres disponibles (actives ou passives uniquement, les copies de base de données retardées ne sont pas comptées) pendant plus de 24 heures

Dans Exchange 2010, la mise à jour corrective de pages n’était pas disponible pour les copies retardées. Dans Exchange 2013, la mise à jour corrective de pages est disponible pour les copies retardées via cette fonction de lecture automatique. Si le système détecte qu’une mise à jour corrective de page est nécessaire pour une copie retardée, les journaux sont automatiquement relus dans la copie retardée pour exécuter la mise à jour corrective de page. Les copies retardées appellent également cette fonction de relecture automatique lorsque le seuil d’espace disque faible est atteint et lorsque la copie retardée a été détectée comme étant la seule copie disponible pendant une période spécifique.

Le comportement de lecture de copie retardée est désactivé par défaut, mais peut être activé en exécutant la commande suivante :

    Set-DatabaseAvailabilityGroup <DAGName> -ReplayLagManagerEnabled $true

Une fois activée, la lecture a lieu lorsque le nombre de copies est inférieur à trois. Vous pouvez modifier la valeur 3 par défaut en changeant la valeur de registre DWORD suivante :

**HKLM\\Software\\Microsoft\\ExchangeServer\\v15\\Replay\\Parameters\\ReplayLagManagerNumAvailableCopies**

Pour activer la lecture pour les seuils d’espace disque faible, vous devez configurer l’entrée de registre suivante :

**HKLM\\Software\\Microsoft\\ExchangeServer\\v15\\Replay\\Parameters\\ReplayLagLowSpacePlaydownThresholdInMB**

Après avoir configuré un de ces paramètres de registre, redémarrez le service de gestion des groupes de disponibilité de base de données (DAG) Microsoft Exchange pour que les modifications prennent effet.

À titre d’exemple, prenons un environnement où une base de données dispose de 4 copies (3 copies hautement disponibles et une copie retardée), et où le paramètre par défaut est utilisé pour *ReplayLagManagerNumAvailableCopies*. Si une copie non retardée est hors de service pour une raison quelconque (elle est par exemple suspendue, etc.), la copie retardée lira automatiquement ses fichiers journaux dans les 24 heures.

## Améliorations apportées à l’alerte de copie unique

Les principaux objectifs des opérations de messagerie Exchange 2013 quotidiennes consistent à veiller à ce que vos serveurs fonctionnent de manière fiable et que vos copies de base de données de boîtes aux lettres soient intègres. Vous devez surveiller activement le matériel, le système d’exploitation Windows et les services Exchange. Toutefois, en cas d’exécution dans un environnement de résilience de boîtes aux lettres Exchange 2013, il est important de surveiller l’intégrité et l’état du DAG et de vos copies de base de données de boîtes aux lettres. Il est particulièrement crucial de procéder à une gestion du risque de redondance des données, et de surveiller les périodes pendant lesquelles une base de données répliquée est réduite à une seule copie, et notamment dans les environnements n’utilisant pas les sauvegardes RAID (Redundant Array of Independent Disks) mais déployant à la place des configurations JBOD. Dans un environnement RAID, une seule défaillance de disque n’a pas d’incidence sur une copie de base de données de boîtes aux lettres active. Toutefois, dans un environnement JBOD, une seule défaillance de disque déclenchera un basculement de base de données.

Dans Exchange 2010, le script CheckDatabaseRedundancy.ps1 a été introduit. Comme son nom l’indique, l’objet du script était de surveiller la redondance des bases de données de boîtes aux lettres répliquées en vérifiant qu’au moins deux copies configurées sont à jour et intègres. Le script prévient un administrateur, via la génération du journal des événements, s’il n’existe qu’une seule copie intègre d’une base de données répliquée. Dans ce cas, il compte les copies actives et passives pour déterminer la redondance des bases de données.

Les conditions de copie unique incluent, entre autres :

  - Échec de la réplication d’une copie active vers une copie passive.

  - Échec de toutes les copies passives ; cela inclut les états FailedAndSuspended et Failed, en plus des états d’intégrité où la copie se trouve derrière lors de la relecture ou de la copie de journal. Notez que les copies retardées ne sont pas considérées comme étant derrière si elles sont dans l’intervalle de dix minutes de relecture de leurs journaux par rapport à la période de retard.

  - Échec de l’identification précise par le système de la génération actuelle du journal de la copie active.

Puisque la priorité absolue des administrateurs est de savoir quand il ne reste plus qu’une seule copie intègre d’une base de données, le script CheckDatabaseRedundancy.ps1 a été remplacé par une fonctionnalité native intégrée faisant partie du groupe d’intégrité DataProtection de la disponibilité gérée.

La fonctionnalité native alerte toujours les administrateurs via les notifications du journal des événements, mais pour distinguer les alertes Exchange 2013 des alertes Exchange 2010, Exchange 2013 utilise les ID d’événement suivants :

  - Événement 4138 (alerte rouge)

  - Événement 4139 (alerte verte)

Dans Exchange 2013, la fonctionnalité native a été améliorée pour diminuer le niveau de bruit généré par l’alerte lorsque plusieurs bases de données sur le même serveur entrent dans une condition de copie unique. Dans Exchange 2010, les alertes de copie unique étaient générées par base de données. Par conséquent, lorsqu’un problème au niveau du serveur concernait plusieurs bases de données et plusieurs copies de base de données, de multiples alertes pouvaient être générées. Comme plusieurs défaillances, telles que des problèmes de contrôleur ou de mémoire, concernent l’ensemble du serveur, il existe une probabilité relativement grande qu’une telle série d’alertes se produise pour chaque incident de serveur. Dans Exchange 2013, les alertes sont désormais générées par serveur. Quand une interruption concerne un serveur entier et que la redondance des données court un risque pour plusieurs copies de base de données, une seule alerte par serveur est désormais générée.

## Configuration automatique de réseau DAG

Un réseau DAG regroupe un ou plusieurs sous-réseaux utilisés soit pour le trafic de réplication, soit pour le trafic MAPI. Chaque DAG contient au maximum un réseau MAPI et aucun, un ou plusieurs réseaux de réplication. Dans Exchange 2010, les réseaux DAG initiaux (par exemple, DAGNetwork01 et DAGNetwork02) étaient créés par le système à partir des sous-réseaux énumérés par le service de cluster. Dans les environnements où plusieurs réseaux étaient utilisés et où les interfaces d’un réseau donné (par exemple, le réseau MAPI) se trouvaient sur le même sous-réseau, l’administrateur devait effectuer une petite configuration supplémentaire. Cependant, dans les environnements où les interfaces d’un réseau donné se trouvaient sur plusieurs sous-réseaux, l’administrateur devait effectuer une tâche appelée réduction des réseaux DAG.

Dans Exchange 2013, la réduction des réseaux DAG n’est plus nécessaire. Exchange 2013 utilise toujours les mêmes mécanismes de détection pour faire la distinction entre les réseaux MAPI et de réplication, mais il réduit maintenant automatiquement les réseaux DAG de façon appropriée.

En outre, par défaut, les réseaux DAG sont désormais gérés automatiquement par le système. Pour afficher les propriétés du réseau DAG à l’aide du Centre d’administration Exchange (CAE), vous devez configurer le DAG pour un contrôle manuel du réseau en modifiant les propriétés du DAG à l’aide du CAE ou de la cmdlet **Set-DatabaseAvailabilityGroup** de façon à définir le paramètre *ManualDagNetworkConfiguration* sur `True`.

## Modifications apportées à la sélection de la meilleure copie

La sélection de la meilleure copie (Best Copy Selection, BCS) est un processus d’algorithme interne permettant de rechercher la meilleure copie d’une base de données individuelle à activer, en fonction d’une liste de copies potentielles disponibles pour l’activation, de leur intégrité et de leur état. Active Manager sélectionne la meilleure copie disponible (et non bloquée) pour qu’elle devienne la nouvelle copie de base de données active en cas d’échec de la copie existante, ou si un administrateur effectue un basculement non ciblé. Dans Exchange 2010, le processus de sélection de la meilleure copie (BCS) a évalué plusieurs aspects de chaque copie de base de données pour déterminer la meilleure copie à activer. Il s’agit notamment des points suivants :

  - Longueur de la file d’attente de copie

  - Longueur de la file d’attente de relecture

  - État de la base de données

  - État de l’index de contenu

Dans Exchange 2013, Active Manager effectue les mêmes étapes et vérifications BCS pour déterminer l’intégrité de la réplication, mais inclut aussi désormais l’utilisation d’une contrainte d’ordre décroissant des états d’intégrité. Suite à ces modifications, BCS se nomme désormais BCSS (Best Copy and Server Selection).

BCSS inclut plusieurs nouvelles vérifications de l’intégrité qui font partie des composants de surveillance intégrés de la disponibilité gérée dans Exchange 2013. Active Manager effectue quatre nouvelles vérifications supplémentaires (répertoriées par ordre d’exécution) :

1.  **Tous intègres**   Recherche un serveur hébergeant une copie de la base de données concernée dont l’état de tous les composants de surveillance est intègre.

2.  **Jusqu’à une intégrité normale**   Recherche un serveur hébergeant une copie de la base de données concernée dont l’état de tous les composants de surveillance ayant une priorité normale est intègre.

3.  **Tous meilleurs que la source**   Recherche un serveur hébergeant une copie de la base de données concernée dont l’état de tous les composants de surveillance est un meilleur que celui du serveur hébergeant actuellement la copie concernée.

4.  **Identique à la source**   Recherche un serveur hébergeant une copie de la base de données concernée dont l’état de tous les composants de surveillance est le même que celui du serveur hébergeant actuellement la copie concernée.

Si BCSS est appelé suite à un basculement déclenché par un composant de surveillance de disponibilité gérée (par exemple, via un répondeur à basculement), le système applique une contrainte obligatoire supplémentaire selon laquelle l’intégrité du composant du serveur cible doit être meilleure que celle du serveur sur lequel le basculement s’est produit. Par exemple, si un échec de Microsoft Office Outlook Web App déclenche un basculement de disponibilité gérée via un répondeur à basculement, BCSS doit sélectionner un serveur hébergeant une copie de la base de données concernée sur laquelle Outlook Web App est intègre.

## Service de gestion des groupes de disponibilité de base de données (DAG)

La mise à jour cumulative 2 (CU2) de la version RTM d’Exchange 2013 offre un nouveau service sur les serveurs de boîtes aux lettres qui sont membres d’un DAG. Il s’agit du service de gestion DAG Microsoft Exchange (MSExchangeDAGMgmt). Ce nouveau service propose des fonctionnalités de surveillance de DAG internes, auparavant exécutées dans le service de réplication Microsoft Exchange (MSExchangeRepl).

## Groupes de disponibilité de base de données (DAG) sans point d’accès administratif de cluster

Tous les DAG exécutant Windows Server 2008 R2 ou Windows Server 2012 nécessitent au moins une adresse IP sur chaque sous-réseau inclus dans le réseau MAPI. Les adresses IP attribuées au DAG sont utilisées par le cluster du DAG avec le point d’accès administratif du cluster (également appelé nom du réseau de cluster) pour permettre la résolution du nom et la connectivité au cluster (ou plus précisément, la connectivité au membre du cluster qui détient actuellement le groupe de ressources principal du cluster) à l’aide du nom de cluster. Windows Server 2012 R2 vous permet de créer un cluster de basculement sans point d’accès administratif. Les clusters de basculement Windows sans points d’accès administratif ont les caractéristiques suivantes :

  - Aucune adresse IP n’est attribuée au cluster, par conséquent il n’y a pas de ressource d’adresse IP dans le groupe de ressources principal du cluster.

  - Aucun nom réseau n’est attribué au cluster, par conséquent il n’y a aucune ressource de nom de réseau dans le groupe de ressources principal du cluster.

  - Le nom du cluster n’est pas enregistré dans le DNS et il ne peut pas être résolu sur le réseau.

  - Aucun objet nom de cluster (CNO) n’est créé dans Active Directory.

  - Le cluster de basculement Windows ne peut pas être géré à l’aide de l’outil de gestion du cluster de basculement. Il doit être géré à l’aide de Windows PowerShell et les cmdlets PowerShell doivent être exécutées sur des membres individuels du cluster.

Lorsqu’il est exécuté sur Windows Server 2012 R2 ou version ultérieure, le Service Pack 1 (SP1) pour Exchange 2013 et version ultérieure vous permet de créer un DAG sans point d’accès administratif de cluster. Vous pouvez créer un DAG sans point d’accès administratif à l’aide du Centre d’administration Exchange ou à l’aide de l’environnement de ligne de commande Exchange Management Shell. Pour plus d’informations, consultez les rubriques [Creating DAGs](managing-database-availability-groups-exchange-2013-help.md) et [Créer un groupe de disponibilité de base de données](create-a-database-availability-group-exchange-2013-help.md).

