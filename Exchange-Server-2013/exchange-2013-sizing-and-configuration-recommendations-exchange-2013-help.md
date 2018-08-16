---
title: 'Config. de srv de transp. Edge avec la config. clonée: Exchange 2013 Help'
TOCTitle: Recommandations en matière de dimensionnement et de configuration d'Exchange 2013
ms:assetid: 4c4ba2fc-014a-46fb-949a-2dabba92c4a5
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dn879075(v=EXCHG.150)
ms:contentKeyID: 63892220
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Recommandations en matière de dimensionnement et de configuration d'Exchange 2013

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2017-03-27_

Exchange 2013 utilise plus de ressources système que les versions antérieures d'Exchange. En dimensionnant correctement votre infrastructure Exchange 2013, puis en vérifiant certaines configurations recommandées pour les composants liés à Exchange dans cette infrastructure, vous pouvez créer les conditions d'un déploiement aux performances optimales.

## Dimensionnement d'Exchange 2013

Le dimensionnement correct d’Exchange 2013 est l’une des façons les plus efficaces de prévenir les problèmes de performances. La calculatrice des conditions requises du rôle du serveur Exchange 2013 est [disponible ici](https://go.microsoft.com/fwlink/p/?linkid=523844). La version la plus récente est la version 6.6, mais nous vous recommandons de consulter régulièrement les mises à jour. Pour utiliser cette calculatrice correctement, vous devez consulter les instructions dans la [calculatrice des conditions requises du rôle du serveur Exchange 2013](https://go.microsoft.com/fwlink/p/?linkid=386677) et les publications de blog sur le [dimensionnement des déploiements Exchange 2013](https://go.microsoft.com/fwlink/p/?linkid=301990).

Il est important de commencer avec la calculatrice avant d'acheter et de déployer votre matériel  ; vous devez tout d'abord déterminer vos besoins en ressources globaux en fonction des résultats de la calculatrice. Vous pouvez utiliser la calculatrice pour entrer les exigences de votre organisation et utiliser les résultats pour obtenir des instructions sur la mise à l'échelle de votre matériel. La calculatrice n'indique pas le nombre de serveurs à utiliser, mais elle vous permet d'estimer l'impact d'une charge de travail Exchange sur un ensemble de serveurs donné. Vous devez tester des configurations différentes pour voir l'impact sur les performances, afin de répondre aux besoins de configuration matérielle et aux besoins commerciaux spécifiques de votre environnement.

Pour simplifier les déploiements et obtenir le meilleur du matériel, le groupe des produits Exchange recommande l'utilisation de serveurs à rôles multiples. L'utilisation de serveurs à rôles multiples vous offre une disponibilité accrue au niveau de la couche du serveur d'accès aux client (CAS), car un plus grand nombre de serveurs d'accès au client est disponible pour traiter les demandes pendant un scénario d'échec. Le principal critère de conception pour Exchange 2013 est d'utiliser des serveurs d'entrée de gamme « plus petits » (évolution horizontale plutôt qu'évolution verticale). La conception et le test ont été effectués avec deux ordinateurs socket contenant jusqu’à 20 cœurs de processeur, avec un maximum de 96 gigaoctets (Go) de RAM. Si votre matériel plus important, vous devez envisager d'autres options, par exemple utiliser ce matériel pour d'autres besoins et acheter de plus petits serveurs pour votre environnement Exchange 2013, ou virtualiser.

Il est préférable de créer des serveurs supplémentaires (évolution horizontale) plutôt que d’ajouter des ressources à des serveurs existants, plus importants (évolution verticale). L’évolution horizontale permet à votre environnement de tirer parti des fonctionnalités de haute disponibilité intégrées dans Exchange 2013. Pour comprendre pourquoi cette configuration est recommandée, veuillez consulter en détail les publications [Architecture préférée](https://go.microsoft.com/fwlink/p/?linkid=523782) et [Impact de la résilience de site sur la disponibilité](https://go.microsoft.com/fwlink/p/?linkid=523845).

La calculatrice ne tient pas compte des produits tiers exécutés sur les serveurs Exchange ni des produits qui interagissent avec Exchange (y compris les applications développées en interne), ce qui signifie que vous devez veiller à en tenir compte pendant le redimensionnement. Lync Server, par exemple, et les applications tierces Exchange Web Services (EWS) et les appareils ActiveSync peuvent tous augmenter de façon considérable les besoins en processeur par utilisateur. Vous pouvez consulter la documentation des produits tiers pour plus d'informations sur la façon dont cela affecte Exchange. La création d'une référence de performances pour Exchange avant d'implémenter des solutions tierces est recommandée.

## Configurations de performances recommandées

Les optimisations de performances suivantes sont recommandées pour votre environnement Exchange 2013.

## Alimentation

Définissez le BIOS de façon à ce qu'il permette au système d'exploitation (SE) de gérer l'alimentation.

Dans le système d'exploitation, activez le schéma d'alimentation hautes performances.

## Traitement

Désactivez l'hyper-threading sur les serveurs Exchange physiques. En cas de virtualisation, l'hyper-threading peut être activé sur le serveur physique, mais seul le nombre requis de processeurs virtuels doit être alloué à chaque serveur virtuel (ne pas dépasser le nombre processeurs virtuels) et seul le nombre de cœurs de processeur physique pour les calculs de dimensionnement doit être utilisé.

Dans Exchange Server 2013 Service Pack 1 ou version ultérieure, vous pouvez activer le déchargement SSL pour réduire la consommation d'UC par les serveurs d'accès au client, mais la configuration complexe du déchargement SSL risque de ne pas être avantageuse.

## .NET Framework


<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>Version d’Exchange</th>
<th>.NET Framework 4.7.1</th>
<th>.NET Framework 4.6.2</th>
<th>.NET Framework 4.6.1</th>
<th>.NET Framework 4.5.2</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Exchange 2013 CU19</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange 2013 CU16 - CU18</p></td>
<td><p></p></td>
<td><p> X</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


Si vous ne pouvez pas installer .NET 4.5.2, consultez l’article 2995145 de la Base de connaissances Microsoft « [Problèmes de performances ou de délais lorsque vous vous connectez à Exchange Server 2013 qui est en cours d’exécution dans Windows Server](https://go.microsoft.com/fwlink/p/?linkid=524159) ». Les correctifs dans cet article ont été développés en fonction des conclusions internes sur l’utilisation de la mémoire du processus de travail de la banque d’informations. En appliquant ces correctifs, vous réduirez la consommation de mémoire globale pour tous les processus gérés (y compris le processus de travail de la banque d’informations), ainsi que le temps total du processeur passé au nettoyage de la mémoire .NET.

## Correctifs logiciels

L'équipe de performances Exchange recommande d'installer tous les correctifs logiciels suivants liés aux performances.

  - [La mise à jour qui améliore la résilience de cluster dans Windows Server 2012 est disponible](https://go.microsoft.com/fwlink/p/?linkid=524088)

  - [Correctifs et mises à jour recommandés pour les clusters de basculement Windows Server 2012](https://go.microsoft.com/fwlink/p/?linkid=524089)

  - [Correctifs et mises à jour recommandés pour les clusters de basculement Windows Server 2012 R2](https://go.microsoft.com/fwlink/p/?linkid=524090)

  - [Affectation de processeur RSS incorrecte sur un ordinateur basé sur Windows 8 ou Windows Server 2012 disposant de processeurs multicœurs](https://go.microsoft.com/fwlink/p/?linkid=324140)

  - [Problèmes de performances ou de délais lorsque vous vous connectez à Exchange Server 2013 qui est en cours d’exécution dans Windows Server](https://go.microsoft.com/fwlink/p/?linkid=312962)

  - [Problème de connectivité Outlook si SSLOffloading est « True » dans Exchange 2013](https://go.microsoft.com/fwlink/p/?linkid=524091)

  - [Connexion serveur longue pour Outlook après un basculement de base de données dans Exchange Server 2013](https://go.microsoft.com/fwlink/p/?linkid=524092)

  - [Performances ralenties dans Outlook Web App lorsque Lync est intégré à Exchange Server 2013](https://go.microsoft.com/fwlink/p/?linkid=524093)

  - [EMS prend beaucoup de temps à exécuter la première commande dans un environnement Exchange Server 2013 Cumulative Update 5](https://go.microsoft.com/fwlink/p/?linkid=524094)

  - [Latence de routage des messages si IPv6 est activé dans Exchange Server 2013](https://go.microsoft.com/fwlink/p/?linkid=524095)

  - [Utilisation élevée du processeur par une application qui dépend d’un client LDAP Microsoft dans Windows Server 2008 R2 SP1](https://go.microsoft.com/fwlink/p/?linkid=530287)

  - [Usage intensif de l’UC lorsque vous utilisez RPC sur le protocole HTTP dans Windows 8.1 ou Windows Server 2012 R2](https://go.microsoft.com/fwlink/p/?linkid=619127)

## Réseau

Avec Exchange 2013, une carte réseau unique est recommandée car il n'est plus nécessaire de fractionner les réseaux MAPI et de réplication. Pour plus d’informations, consultez la rubrique [Network requirements](planning-for-high-availability-and-site-resilience-exchange-2013-help.md).

Utilisez les paramètres de déchargement SNP par défaut disponibles et assurez-vous que RSS est activé (la valeur par défaut dans Windows Server 2012 et les versions ultérieures). RSS vous aide à mettre l'utilisation du processeur à l'échelle, en particulier sur 10GbE.

Vérifiez que le système d'exploitation ne désactive pas la carte réseau pour économiser de l'énergie.

Mettez à jour les pilotes de carte réseau (NIC). Contactez votre fournisseur sur une base mensuelle pour connaître les mises à jour de pilote appropriées.

## Internet Information Services (IIS)

Pendant l'installation, Exchange modifie certaines limites de connexion pour les services IIS. Aucun autre réglage d'IIS n'est recommandé.

Évitez les personnalisations lorsque cela est possible. Toute modification apportée à web.config ou aux clés de registre peut être remplacée par des mises à jour cumulatives d'Exchange ou de Windows.

## Stockage

Des instructions pour le stockage d'Exchange 2013 sont disponibles dans [Options de configuration du stockage Exchange 2013](exchange-2013-storage-configuration-options-exchange-2013-help.md).

## Virtualisation

Consultez [Requirements for hardware virtualization](exchange-2013-virtualization-exchange-2013-help.md). Notez également qu'Exchange n'est pas sensible à la technologie NUMA (Non-Uniform Memory Access) Par conséquent, il est recommandé d'utiliser les paramètres NUMA par défaut du fabricant du matériel.

## Active Directory

Surveillez les performances du serveur d’annuaire, car les requêtes Active Directory ont un impact direct sur votre déploiement Exchange.

La durée de recherche LDAP est un compteur essentiel pour évaluer l'intégrité d'Active Directory. Surveillez le processeur sur vos contrôleurs de domaine. Les problèmes d'UC sur les contrôleurs de domaine se traduiront par un gain de performances sur les serveurs Exchange.

Exécutez les « Diagnostics Active Directory » intégrés sur le contrôleur de domaine dans l'analyseur de performances situé sous « Ensemble de collecteur de données » pour identifier la cause des problèmes de performances du contrôleur de domaine.

Prévoyez suffisamment de mémoire vive sur les contrôleurs de domaine pour pouvoir mettre en cache le fichier de base de données AD entier.

Il est recommandé de déployer un cœur de catalogue global Active Directory pour chaque ensemble de 8 cœurs de boîte aux lettres traitant la charge active (sur la base des cœurs de catalogue global 64 bits).

## Équilibrage de charge

Tous les serveurs d'accès au client doivent recevoir approximativement le même nombre de connexions entrantes.

Pour tous les protocoles, Exchange 2013 ne requiert pas l'affinité de session entre un serveur d'accès au client donné et l'équilibreur de charge.

Un équilibreur de charge matériel ou logiciel permet de gérer tout le trafic entrant vers les serveurs d'accès au client. La sélection peut se faire de diverses manières, par exemple, selon le principe de « tourniquet » (round-robin) où chaque connexion entrante aboutit au serveur cible suivant dans une liste circulaire, ou selon le principe du nombre de connexions le moins élevé où l'équilibrage de charge envoie chaque connexion au serveur ayant le plus petit nombre de connexions à ce moment. Ces méthodes sont décrites plus en détail dans [Équilibrage de charge](load-balancing-exchange-2013-help.md). Vous devez également déterminer les éléments suivants :

  - Le principe de « tourniquet » (round-robin) présente le problème de convergence lente avec des connexions à longue durée de vie (telles que RPC/HTTP). Comme de nouveaux ordinateurs sont mis en ligne, l'équilibre des connexions prises en charge sur les ordinateurs cibles prendra beaucoup de temps pour converger.

  - Avec le principe du nombre de connexions le moins élevé, sachez qu'il est possible pour un serveur d'accès au client d'être surchargé et de ne plus répondre durant une panne de serveur d'accès au client ou au cours de la maintenance des correctifs. Dans le contexte des performances d'Exchange, l'authentification est une opération coûteuse.

En raison d'un certain nombre de limitations avec Windows Network Load Balancing (NLB) dans un environnement Exchange 2013, détaillées dans [Équilibrage de charge](load-balancing-exchange-2013-help.md), nous déconseillons l'utilisation de Windows NLB.

## Distribution de base de données et d'utilisateurs

Maintenez une répartition équilibrée d'utilisateurs par base de données et de bases de données actives par serveur. Distribuez uniformément la consommation d'espace disque de la base de données et équilibrez les utilisateurs considérables sur toutes les bases de données.

Vous devez profiler votre base d'utilisateurs pour comprendre la façon dont ils interagissent avec Exchange (appareils, Outlook et OWA) et l'impact de ces interactions du point de vue des performances. Consultez les blogs de la calculatrice à partir de la Section 2 pour mieux comprendre comment profiler l'utilisation d'Exchange par utilisateur.

Configurez les préférences d'activation de copie de base de données et les paramètres « MaximumPreferredActiveDatabases » (par serveur) pour maintenir l'équilibre pendant un basculement.

Le script RedistributeActiveDatabases.ps1 rééquilibrera les bases de données actives sur les nœuds DAG.

Envisagez d’appliquer des limites de nombre d’éléments strictes correspondant à Office 365. Vous pouvez le faire à l’aide de la cmdlet Set-Mailbox et des informations fournies dans [Limites de dossier de boîte aux lettres](https://go.microsoft.com/fwlink/p/?linkid=398779).

## Fichier d’échange

Définir la taille maximale pour le fichier d’échange de 32778 Mo si vous utilisez plus de 32 Go de RAM.

Le fichier d'échange ne doit pas être hébergé sur le même lecteur que les fichiers de base de données Exchange ou des fichiers journaux de base de données.

Il est impératif que vous utilisiez un fichier d'échange de taille fixe et que vous n'autorisiez pas Windows à gérer la taille. Augmenter le fichier d'échange peut être une tâche nécessitant de nombreuses performances et peut entraîner des problèmes si Exchange est soumis à des contraintes.

Si vous avez besoin d’obtenir un fichier d’image mémoire complète, utilisez l’article 969028 de la Base de connaissances Microsoft sur [Comment générer un noyau ou un fichier d’image mémoire complète de Windows Server 2008 et Windows Server 2008 R2](https://go.microsoft.com/fwlink/p/?linkid=524044), pour le fichier d’image mémoire dédié.

## Mode Outlook

Le mode mis en cache est recommandé. Pour comprendre l’avantage de l’utilisation du mode mis en cache, consultez [Choisir entre le mode Exchange mis en cache et le mode En ligne pour Outlook 2013](https://go.microsoft.com/fwlink/p/?linkid=524045).

Il est important de noter que les performances peuvent être affectées par les compléments de serveur et les compléments Outlook tiers. Lorsque vous utilisez le mode en ligne, les clients peuvent s'attendre à des problèmes de performances issus de compléments tiers, d'un grand nombre d'éléments, des affichages restreints, du nombre d'utilisateurs accédant à la boîte aux lettres, entre autres. Les clients hérités peuvent rencontrer plus d'impact par des nombres d'éléments et des performances élevés qu'Outlook 2013.

Si la principale raison pour laquelle Outlook est configuré en mode en ligne dans une organisation est une raison de sécurité, envisagez d'utiliser BitLocker à la place.

Outlook 2013 offre une nouvelle fonctionnalité « Curseur de synchronisation » pour réduire le temps de téléchargement et la taille du fichier OST. Veuillez consulter [Configurer le mode Exchange mis en cache dans Outlook 2013](https://go.microsoft.com/fwlink/p/?linkid=390456) pour plus d’informations.

Vérifiez tous les mois si des mises à jour clients d'Outlook prises en charge dans votre environnement sont disponibles.

## Logiciel tiers

Comme meilleure pratique, désinstallez ou désactivez les logiciels tiers lors de la résolution des problèmes de performances d'Exchange. La liste suivante répertorie les types de logiciels tiers qui, selon le support Microsoft, ont le plus souvent affecté les performances d'Exchange 2013.

  - Solutions antivirus

  - Logiciels de prévention d'intrusion

  - Logiciels de sauvegarde

  - Logiciels d'audit, pour les fichiers et les utilisateurs

  - Solutions d'archivage

