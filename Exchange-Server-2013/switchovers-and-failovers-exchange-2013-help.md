---
title: 'Switchovers et basculements: Exchange 2013 Help'
TOCTitle: Switchovers et basculements
ms:assetid: 75388645-cae1-402e-bf02-c4949d3e2c31
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dd298067(v=EXCHG.150)
ms:contentKeyID: 62523886
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Switchovers et basculements

 

_**Sapplique à :**Exchange Server 2013 SP1_

_**Dernière rubrique modifiée :**2015-12-02_

Les permutations et les basculements sont deux formes de panne rencontrées dans Microsoft Exchange Server 2013.

  - Une *permutation* est une panne planifiée d’une base de données ou d’un serveur qui est initiée explicitement par une cmdlet ou par le système de disponibilité géré dans Exchange 2013. Les permutations sont généralement effectuées pour préparer une opération de maintenance. Les permutations impliquent le déplacement de la copie de base de données de boîtes aux lettres active vers un autre serveur du groupe de disponibilité de base de données (DAG). Si aucune cible saine n’est trouvée pendant une permutation, les administrateurs reçoivent une erreur et la base de données de boîte aux lettres reste en exécution ou montée.

  - Un *basculement* désigne des événements inattendus qui provoquent l’indisponibilité des services, des données ou des deux. Un basculement suppose que la défaillance du système soit automatiquement réparée en activant une copie de base de données de boîtes aux lettres passive pour la convertir en copie active. Si aucune cible saine n’est trouvée pendant un basculement, la base de données de boîte aux lettres est démontée.

Exchange 2013 est spécifiquement conçu pour gérer les permutations et les basculements.

Souhaitez-vous rechercher des tâches de gestion liées à la haute disponibilité et la résilience de site ? Consultez la rubrique [Gestion de la haute disponibilité et de la résilience de site](managing-high-availability-and-site-resilience-exchange-2013-help.md).

## Permutations

Il existe trois types de permutation dans Exchange 2013 :

  - Permutation de base de données

  - Permutation de serveur

  - Permutation de centre de données

## Permutation de base de données

Une *permutation de base de données* est le processus par lequel une base de données active individuelle est permutée vers une autre copie de base de données (copie passive), qui est ensuite définie comme nouvelle copie de base de données active. Les permutations de base de données peuvent se produire dans un centre de données et entre plusieurs centres de données. Une permutation de base de données peut être effectuée via le Centre d’administration Exchange (CAE) ou l’environnement de ligne de commande Exchange Management Shell. Quelle que soit l’interface utilisée, le processus de permutation est le suivant :

1.  L’administrateur initie une permutation de base de données pour déplacer la copie de base de données de boîtes aux lettres active vers un autre serveur.

2.  Le client utilisé pour la tâche lance un appel de procédure distante au service de réplication Microsoft Exchange sur un membre du DAG.

3.  Si le membre du DAG ne détient pas le rôle de gestionnaire Active Manager principal (PAM), il redirige la tâche vers le rôle PAM.

4.  La tâche émet un appel de procédure distante (RPC) au service de réplication Microsoft Exchange sur le serveur qui détient le rôle PAM.

5.  Le Gestionnaire Active Manager principal lit et met à jour les informations sur l’emplacement de la base de données qui sont stockées dans la base de données du cluster pour le DAG.

6.  Le Gestionnaire Active Manager principal contacte le service de réplication Microsoft Exchange sur le membre du DAG dont la copie passive est activée en tant que nouvelle copie de base de données de boîtes aux lettres active.

7.  Le service de réplication Microsoft Exchange du serveur cible interroge les services de réplication Microsoft Exchange sur tous les autres membres du DAG pour déterminer la source de journal optimale pour la copie de base de données.

8.  La base de données est démontée du serveur actuel et le service de réplication Microsoft Exchange du serveur cible copie les journaux restants vers ce dernier.

9.  Le service de réplication Microsoft Exchange du serveur cible sollicite le montage d’une base de données.

10. Le service de banque d’informations Microsoft Exchange sur le serveur cible relit les fichiers journaux et monte la base de données.

11. Tous les codes d’erreur sont renvoyés vers le service de réplication Microsoft Exchange du serveur cible.

12. Le Gestionnaire Active Manager principal met à jour les informations sur l’état de la copie de base de données dans la base de données du cluster pour le DAG.

13. Tous les codes d’erreur sont renvoyés par le service de réplication Microsoft Exchange du serveur cible vers le service de réplication Microsoft Exchange du Gestionnaire Active Manager principal.

14. Le service de réplication Microsoft Exchange du Gestionnaire Active Manager principal renvoie toutes les erreurs vers l’interface d’administration où la tâche a été appelée.

15. Remote PowerShell renvoie les résultats de l’opération vers l’interface d’administration appelante.

Pour connaître la procédure détaillée d’exécution d’une permutation de base de données, consultez la rubrique [Activer une copie de la base de données de boîtes aux lettres](activate-a-mailbox-database-copy-exchange-2013-help.md).

## Permutation de serveur

Une permutation de serveur est le processus par lequel toutes les bases de données actives sur un membre du DAG sont activées sur un ou plusieurs membres du DAG. Comme pour la permutation de base de données, une permutation de serveur peut se produire tant au sein d’un centre de données qu’entre plusieurs centres de données, et peut être lancée par le Centre d’administration Exchange ou l’environnement de ligne de commande Exchange Management Shell. Quelle que soit l’interface utilisée, le processus de permutation de serveur est le suivant :

1.  L’administrateur initie la permutation d’un serveur pour déplacer toutes les copies de base de données de boîtes aux lettres actives vers un ou plusieurs autres serveurs.

2.  L’opération est constituée des mêmes étapes que celles décrites plus haut dans cette rubrique pour les permutations de base de données (étapes 2 à 4), pour chacune des bases de données actives sur le serveur actuel.

3.  Le Gestionnaire Active Manager principal lit et met à jour les informations sur l’emplacement de la base de données qui sont stockées dans la base de données du cluster pour le DAG.

4.  Il contacte le service de réplication Microsoft Exchange de chaque membre du DAG sur lequel une copie passive est activée.

5.  Le service de réplication Microsoft Exchange des serveurs cible interroge les services de réplication Microsoft Exchange de tous les autres membres du DAG pour déterminer la source de journal optimale pour la copie de base de données.

6.  La base de données est démontée du serveur actuel et le service de réplication Microsoft Exchange de chaque serveur cible copie les journaux restants.

7.  Le service de réplication Microsoft Exchange de chaque serveur cible sollicite le montage d’une base de données.

8.  Le service de banque d’informations Microsoft Exchange sur chaque serveur cible relit les fichiers journaux et monte la base de données.

9.  Tous les codes d’erreur sont renvoyés vers le service de réplication Microsoft Exchange du serveur cible.

10. Le Gestionnaire Active Manager principal met à jour les informations sur l’état de la copie de base de données dans la base de données du cluster pour le DAG.

11. Tous les codes d’erreur sont renvoyés par le service de réplication Microsoft Exchange du serveur cible vers le service de réplication Microsoft Exchange du Gestionnaire Active Manager principal.

12. Le service de réplication Microsoft Exchange du Gestionnaire Active Manager principal renvoie toutes les erreurs vers l’interface d’administration où la tâche a été appelée.

13. Remote PowerShell renvoie les résultats de l’opération vers l’interface d’administration appelante.

Pour connaître la procédure détaillée d’exécution d’une permutation de serveur, consultez la rubrique [Effectuer un basculement de serveur](perform-a-server-switchover-exchange-2013-help.md).

## Permutation de centre de données

Dans une configuration de résilience de site, la récupération automatique suite à une défaillance au niveau du site peut se produire dans un DAG, ce qui permet au système de messagerie de conserver un état fonctionnel. Cette configuration nécessite au moins trois emplacements, car elle nécessite le déploiement de membres du DAG dans deux emplacements et le déploiement du serveur témoin du DAG dans un troisième emplacement.

Si vous ne disposez pas de trois emplacements, ou si vous disposez de trois emplacements mais que vous voulez contrôler les actions de récupération au niveau du centre de données, vous pouvez configurer un DAG pour une récupération manuelle en cas de défaillance au niveau du site. Dans ce cas, vous devez exécuter un processus appelé *permutation de centre de données*. Comme dans de nombreux scénarios de récupération d’urgence, la planification et la préparation préliminaires d’une permutation de centre de données permettent de simplifier le processus de récupération et de réduire la durée de la panne.

En raison des nombreuses modifications apportées à l’architecture d’Exchange 2013, y compris la consolidation des rôles serveur, l’exécution d’une permutation de centre de données dans Exchange 2013 est beaucoup plus facile qu’elle ne l’était dans Exchange 2010. Pour obtenir des instructions détaillées sur les étapes d’exécution d’une permutation de centre de données, voir [Switchovers de centre de données](datacenter-switchovers-exchange-2013-help.md).

## Basculements

Le basculement est un processus d’activation automatique qui peut se produire au niveau de la base de données, du serveur ou du centre de données. Les basculements ont lieu suite à la défaillance d’une base de données spécifique (perte de stockage isolé, par exemple), d’un serveur complet (défaut de la carte mère ou coupure de courant, par exemple) ou d’un site complet (perte de tous les membres du DAG d’un site, par exemple).

Les DAG et les copies de base de données de boîtes aux lettres assurent la redondance complète et la récupération rapide des données et des services qui permettent d’accéder aux données. Le tableau suivant dresse la liste des actions de récupération à effectuer pour de nombreux types de défaillance. Certaines défaillances requièrent l’intervention de l’administrateur pour déclencher la récupération. D’autres sont automatiquement gérées par le système.


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
<th>Description</th>
<th>Activation automatique</th>
<th>Action de réparation automatique</th>
<th>État lors de la réparation : Actif</th>
<th>État lors de la réparation : Passif</th>
<th>Actions de réparation</th>
<th>Commentaires</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Erreur logicielle de la base de données Extensible Storage Engine (ESE) : Les lecteurs de stockage de la base de données renvoient des erreurs lors de certaines opérations de lecture (par exemple, erreur -1018).</p></td>
<td><p>Brève interruption possible.</p>
<p>Basculement automatique possible.</p></td>
<td><p>Correction automatique d’une page incorrecte.</p></td>
<td><p>Permutation manuelle, basculement automatique ou réparation en ligne.</p></td>
<td><p>Échec</p></td>
<td><p>Reconstruction RAID, réparation de la base de données et de la copie de base de données, restauration et exécution de la récupération, puis correction de la page ou correction de la page à partir de la copie.</p></td>
<td><p>Il existe d’autres codes d’erreur logicielle de base de données.</p>
<p>N’inclut pas les erreurs de bloc du système de fichiers NTFS.</p>
<p>Si une opération de basculement ou de permutation est effectuée, le serveur hôte est mis à jour.</p></td>
</tr>
<tr class="even">
<td><p>Erreur de base de données « <em>semi-logicielle »</em> ESE : Les lecteurs de stockage de la base de données renvoient des erreurs lors de certaines opérations d’écriture.</p></td>
<td><p>Brève interruption pendant le basculement automatique.</p></td>
<td><p>Reconstruction automatique du volume/disque après un éventuel remplacement du lecteur.</p></td>
<td><p>Démontée si elle ne peut pas être récupérée.</p></td>
<td><p>Failed</p></td>
<td><p>La reconstruction RAID peut remédier au problème.</p>
<p>Copie et réparation, restauration et exécution de la récupération, ou reconstruction du volume/disque après un éventuel remplacement.</p></td>
<td><p>Le terme « erreur d’écriture semi-logicielle ESE » signifie que certaines opérations d’écriture aboutissent.</p>
<p>N’inclut pas une erreur de bloc NTFS.</p></td>
</tr>
<tr class="odd">
<td><p>Erreur de journal « semi-logicielle » ESE : Les lecteurs de stockage des données du journal renvoient des erreurs non résolues lors de certaines opérations de lecture ou d’écriture.</p></td>
<td><p>Brève interruption pendant le basculement automatique.</p></td>
<td><p>Reconstruction automatique du volume/disque après un éventuel remplacement du lecteur.</p></td>
<td><p>Démontée si elle ne peut pas être récupérée.</p></td>
<td><p>Failed</p></td>
<td><p>La reconstruction RAID peut remédier au problème.</p>
<p>Copie et réparation, restauration et exécution de la récupération, ou reconstruction du volume/disque après un éventuel remplacement.</p></td>
<td><p>Le terme « erreur de lecture/écriture semi-logicielle ESE » signifie que certaines opérations de lecture/écriture aboutissent.</p>
<p>En cas d’échec de la base de données, la récupération automatique se produira avant le début du traitement de la récupération des données du journal.</p></td>
</tr>
<tr class="even">
<td><p>Erreur logicielle ou épuisement des ressources ESE : Erreur d’interruption de l’instance par ESE (par exemple, ID d’événement 1022, profondeur excessive du point de contrôle).</p></td>
<td><p>Brève interruption pendant le basculement automatique.</p></td>
<td><p>Aucun.</p></td>
<td><p>Démontée si elle ne peut pas être récupérée.</p></td>
<td><p>Failed</p></td>
<td><p>Remédiez au problème de ressource sous-jacent.</p></td>
<td><p>Cette erreur peut dissimuler d’autres problèmes.</p></td>
</tr>
<tr class="odd">
<td><p>Erreurs de bloc NTFS : Les lecteurs de stockage de la base de données ou des journaux détectent une erreur de lecture ou d’écriture sur une structure de contrôle NTFS.</p></td>
<td><p>Brève interruption pendant le basculement automatique.</p></td>
<td><p>Reconstruction complète du volume après un éventuel remplacement du lecteur.</p></td>
<td><p>Démontée si elle ne peut pas être récupérée.</p></td>
<td><p>Failed</p></td>
<td><p>La reconstruction RAID peut remédier au problème. Les utilitaires NTFS peuvent résoudre les problèmes NTFS. Une récupération Exchange peut s’avérer nécessaire.</p></td>
<td><p>Ce problème est plus susceptible de se produire lorsque RAID n’est pas utilisé. S’il affecte le volume de journal actif, certains fichiers journaux récents seront perdus.</p>
<p>N’inclut pas les erreurs automatiquement résolues par NTFS ni sa pile logicielle ou matérielle sous-jacente.</p></td>
</tr>
<tr class="even">
<td><p>Erreur du lecteur de base de données ou de journal : Un lecteur de stockage de la base de données ou des journaux a échoué complètement et n’est plus accessible.</p></td>
<td><p>Brève interruption pendant le basculement automatique.</p></td>
<td><p>Reformatage ou remplacement du lecteur, suivi d’une reconstruction du volume complet.</p></td>
<td><p>Démontée si elle ne peut pas être récupérée.</p></td>
<td><p>Failed</p></td>
<td><p>Remplacement du lecteur suivi d’une éventuelle reconstruction RAID.</p>
<p>Remplacement du lecteur suivi d’une reconstruction du volume complet.</p>
<p>Reconstruction du volume complet.</p></td>
<td><p>Non applicable.</p></td>
</tr>
<tr class="odd">
<td><p>Échec du volume de base de données ou de journal : Le volume échoue en raison d’un problème lié à NTFS ou à un volume de niveau inférieur.</p></td>
<td><p>Brève interruption pendant le basculement automatique.</p></td>
<td><p>Reformatage ou remplacement du lecteur.</p></td>
<td><p>Démontée si elle ne peut pas être récupérée.</p></td>
<td><p>Failed</p></td>
<td><p>Remplacement du lecteur suivi d’une éventuelle reconstruction RAID.</p>
<p>Remplacement du lecteur suivi d’une reconstruction du volume complet.</p>
<p>Reconstruction du volume complet.</p></td>
<td><p>Non applicable.</p></td>
</tr>
<tr class="even">
<td><p>Espace du volume de base de données ou de journal insuffisant : L’espace du système de fichiers NTFS, ainsi que des fichiers de base de données ou journaux est saturé.</p></td>
<td><p>Basculement automatique si une autre copie ne se trouve pas dans un état similaire.</p></td>
<td><p>Aucun.</p></td>
<td><p>Démontée.</p></td>
<td><p>Failed</p></td>
<td><p>Exécution de sauvegardes complètes ou incrémentielles, suppression manuelle des journaux, attente de l’expiration du délai, reprise de la copie de la base de donnés ou réparation de la copie de base de données défaillante.</p></td>
<td><p>Non applicable.</p></td>
</tr>
<tr class="odd">
<td><p>L’administrateur démonte la base de données incorrecte.</p></td>
<td><p>Si le basculement automatique n’est pas bloqué par l’administrateur, une brève interruption se produira.</p>
<p>Si le basculement automatique est évité, une panne se produira jusqu’à ce que la base de données soit montée.</p></td>
<td><p>Aucun.</p></td>
<td><p>Démontée.</p></td>
<td><p>Non applicable</p></td>
<td><p>L’administrateur corrige l’erreur.</p></td>
<td><p>Non applicable.</p></td>
</tr>
<tr class="even">
<td><p>L’administrateur suspend la copie de base de données incorrecte.</p></td>
<td><p>Selon la configuration et la copie affectée, la récupération automatique peut être évitée.</p></td>
<td><p>Aucun.</p></td>
<td><p>Non applicable.</p></td>
<td><p>Suspendu</p></td>
<td><p>L’administrateur corrige l’erreur.</p></td>
<td><p>Non applicable.</p></td>
</tr>
<tr class="odd">
<td><p>L’administrateur démonte une base de données pour le stockage, NTFS ou la maintenance du volume.</p></td>
<td><p>Si le basculement automatique n’est pas bloqué par l’administrateur, une brève interruption se produira.</p>
<p>Si le basculement automatique est bloqué, une panne se produira jusqu’à ce que l’administrateur termine la tâche.</p></td>
<td><p>Aucun.</p></td>
<td><p>Démontée.</p></td>
<td><p>Non applicable</p></td>
<td><p>L’administrateur termine la tâche.</p></td>
<td><p>Non applicable.</p></td>
</tr>
<tr class="even">
<td><p>L’administrateur suspend une copie de base de données pour le stockage, NTFS ou la maintenance du volume.</p></td>
<td><p>Selon la configuration et la copie affectée, la récupération automatique peut être évitée.</p></td>
<td><p>Aucun.</p></td>
<td><p>Non applicable.</p></td>
<td><p>Suspended</p></td>
<td><p>L’administrateur termine les opérations.</p></td>
<td><p>Non applicable.</p></td>
</tr>
<tr class="odd">
<td><p>L’administrateur démonte une base de données en vue de sa maintenance hors connexion.</p></td>
<td><p>Panne nécessitant une réparation.</p></td>
<td><p>Aucun.</p></td>
<td><p>Démontée.</p></td>
<td><p>Suspended</p></td>
<td><p>L’administrateur termine les opérations.</p></td>
<td><p>Les copies de base de données actives et passives sont différentes.</p>
<p>L’administrateur doit suspendre les copies.</p></td>
</tr>
<tr class="even">
<td><p>Défaillance du réseau de stockage (SAN), du disque ou du contrôleur de stockage.</p></td>
<td><p>Brève interruption pendant le basculement automatique.</p></td>
<td><p>Aucun.</p></td>
<td><p>Démontée.</p></td>
<td><p>N’importe lequel</p></td>
<td><p>Réparation du matériel.</p></td>
<td><p>Une copie de base de données passive sera à l’état dans lequel elle se trouvait avant la panne du système.</p></td>
</tr>
<tr class="odd">
<td><p>Maintenance du matériel de serveur.</p></td>
<td><p>Brève interruption pendant le basculement automatique (sauf en cas de blocage par un administrateur).</p></td>
<td><p>Aucun.</p></td>
<td><p>Démontée.</p></td>
<td><p>N’importe lequel</p></td>
<td><p>Achèvement des actions.</p></td>
<td><p>Une copie de base de données passive sera à l’état dans lequel elle se trouvait avant l’arrêt du système.</p></td>
</tr>
<tr class="even">
<td><p>Maintenance du logiciel de serveur.</p></td>
<td><p>Brève interruption pendant le basculement automatique (sauf en cas de blocage par un administrateur).</p></td>
<td><p>Aucun.</p></td>
<td><p>Démontée.</p></td>
<td><p>N’importe lequel</p></td>
<td><p>Achèvement des actions.</p></td>
<td><p>Une copie de base de données passive sera à l’état dans lequel elle se trouvait avant l’arrêt du système.</p></td>
</tr>
<tr class="odd">
<td><p>Le service de banque d’informations Microsoft Exchange est arrêté ou a été interrompu par un administrateur.</p></td>
<td><p>Brève interruption pendant le basculement automatique.</p></td>
<td><p>Aucun.</p></td>
<td><p>Démontée.</p></td>
<td><p>N’importe lequel</p></td>
<td><p>Redémarrage du service de banque d’informations Microsoft Exchange.</p></td>
<td><p>Non applicable.</p></td>
</tr>
<tr class="even">
<td><p>Échec du service de banque d’informations Microsoft Exchange ; le système d’exploitation fonctionne toujours.</p></td>
<td><p>Brève interruption pendant le basculement automatique.</p></td>
<td><p>Le Gestionnaire de contrôle des services redémarre le service de banque d’informations Microsoft Exchange.</p></td>
<td><p>Démontée.</p></td>
<td><p>N’importe lequel</p></td>
<td><p>Redémarrage manuel ou automatique du service de banque d’informations Microsoft Exchange.</p></td>
<td><p>Une copie de base de données passive sera à l’état dans lequel elle se trouvait avant l’échec du service de banque d’informations Exchange.</p></td>
</tr>
<tr class="odd">
<td><p>Échec partiel du service de banque d’informations Microsoft Exchange ; une partie de la banque Exchange cesse de fonctionner, mais n’est pas identifiée comme entièrement défaillante.</p></td>
<td><p>Brève interruption possible pendant le basculement automatique.</p></td>
<td><p>Aucun.</p></td>
<td><p>Montée et partiellement fonctionnelle.</p></td>
<td><p>N’importe lequel, mais peut ne fonctionner que partiellement</p></td>
<td><p>Redémarrage du système d’exploitation ou du service de banque d’informations Microsoft Exchange.</p></td>
<td><p>Non applicable.</p></td>
</tr>
<tr class="even">
<td><p>Échec du serveur : Le serveur échoue pour l’une des raisons suivantes :</p>
<ul>
<li><p>Panne de courant totale</p></li>
<li><p>Défaillance Échec non résolu du processeur, de la carte mère ou de la carte d’insertion</p></li>
<li><p>Erreur d’arrêt du système d’exploitation</p></li>
<li><p>Le système d’exploitation ne répond plus</p></li>
<li><p>Échec total de la communication</p></li>
</ul></td>
<td><p>Brève interruption pendant le basculement automatique.</p></td>
<td><p>Redémarrage de l’ordinateur.</p></td>
<td><p>Démontée.</p></td>
<td><p>N’importe lequel</p></td>
<td><p>Rétablissement de l’alimentation, modification des paramètres du système d’exploitation, modification des paramètres du matériel, remplacement du matériel, redémarrage du système d’exploitation, réparation du système d’exploitation, réparation du matériel ou résolution des problèmes de communication.</p></td>
<td><p>Non applicable.</p></td>
</tr>
<tr class="odd">
<td><p>Le DAG détecte une défaillance du quorum.</p></td>
<td><p>Panne nécessitant une réparation.</p></td>
<td><p>Aucun.</p></td>
<td><p>Démontée.</p></td>
<td><p>N’importe lequel</p></td>
<td><p>Réparation du quorum défaillant, affectation d’un nouveau quorum ou restauration du réseau responsable de la défaillance du quorum.</p></td>
<td><p>Une copie de base de données passive sera à l’état dans lequel elle se trouvait avant la panne du système.</p></td>
</tr>
<tr class="even">
<td><p>Échec de communication du réseau MAPI : Le serveur n’est plus disponible sur le réseau MAPI.</p></td>
<td><p>Brève interruption pendant le basculement automatique ; doit être sans perte.</p></td>
<td><p>Aucun. Tentatives de communication répétées.</p></td>
<td><p>Démontée.</p></td>
<td><p>N’importe lequel</p></td>
<td><p>Résolution du problème de communication en remédiant aux problèmes matériels ou logiciels.</p></td>
<td><p>Non applicable.</p></td>
</tr>
<tr class="odd">
<td><p>Échec de communication du réseau de réplication : Le serveur ne peut pas recevoir de pulsations, journaliser les copies ni s’amorcer sur le réseau de réplication défaillant.</p></td>
<td><p>Brève interruption possible de la copie ou de l’amorçage lorsque la charge de travail est permutée vers un autre réseau.</p></td>
<td><p>Aucun. Tentatives de communication répétées.</p></td>
<td><p>Aucun.</p></td>
<td><p>N’importe lequel</p></td>
<td><p>Résolution du problème de communication en remédiant aux problèmes matériels ou logiciels.</p></td>
<td><p>Résilience affectée par une défaillance.</p></td>
</tr>
<tr class="even">
<td><p>Plusieurs échecs de communication réseau : Le serveur ne peut pas recevoir de pulsations, journaliser les copies ni s’amorcer sur plusieurs réseaux.</p></td>
<td><p>Brève interruption pendant le basculement automatique ; doit être sans perte.</p></td>
<td><p>Aucun. Tentatives de communication répétées.</p></td>
<td><p>Démontée.</p></td>
<td><p>N’importe lequel</p></td>
<td><p>Résolution du problème de communication en remédiant aux problèmes matériels ou logiciels.</p></td>
<td><p>Au moins un réseau fonctionne toujours.</p></td>
</tr>
<tr class="odd">
<td><p>Échec partiel d’un ou de plusieurs réseaux : Les réseaux rencontrent un nombre d’erreurs élevé.</p></td>
<td><p>Échec non détecté ; aucune action.</p></td>
<td><p>Aucun.</p></td>
<td><p>Montée, mais problèmes de performances possibles.</p></td>
<td><p>N’importe lequel</p></td>
<td><p>Résolution du problème de communication en remédiant aux problèmes matériels ou logiciels.</p></td>
<td><p>Le réseau rencontre un nombre d’erreurs anormalement élevé.</p></td>
</tr>
<tr class="even">
<td><p>Blocage du système d’exploitation non détecté : Le système d’exploitation ne répond plus, mais n’est pas détecté par l’analyse ou le clustering.</p></td>
<td><p>Aucun.</p></td>
<td><p>Aucun.</p></td>
<td><p>N’importe lequel.</p></td>
<td><p>N’importe lequel</p></td>
<td><p>Redémarrage ou arrêt des ressources qui ne répondent pas.</p></td>
<td><p>Le blocage n’est pas détecté. Par conséquent, aucune action n’est effectuée.</p>
<p>Certaines fonctionnalités peuvent être opérationnelles.</p></td>
</tr>
<tr class="odd">
<td><p>Le lecteur du système d’exploitation détecte une erreur.</p></td>
<td><p>Brève interruption pendant le basculement automatique.</p></td>
<td><p>Aucun.</p></td>
<td><p>Démontée.</p></td>
<td><p>N’importe lequel</p></td>
<td><p>Remplacement du lecteur et reconstruction du serveur ou du volume via RAID.</p></td>
<td><p>Non applicable.</p></td>
</tr>
<tr class="even">
<td><p>Espace du lecteur de système d’exploitation insuffisant.</p></td>
<td><p>Brève interruption pendant le basculement automatique.</p></td>
<td><p>Aucun.</p></td>
<td><p>Démontée.</p></td>
<td><p>N’importe lequel</p></td>
<td><p>Libération manuelle d’espace sur le volume.</p></td>
<td><p>Non applicable.</p></td>
</tr>
<tr class="odd">
<td><p>Le lecteur contenant les fichiers binaires Exchange détecte une défaillance du volume ou du lecteur.</p></td>
<td><p>Brève interruption pendant le basculement automatique.</p></td>
<td><p>Aucun.</p></td>
<td><p>Démontée.</p></td>
<td><p>N’importe lequel</p></td>
<td><p>Remplacement du lecteur et réinstallation de l’application ou reconstruction du volume via RAID.</p></td>
<td><p>Non applicable.</p></td>
</tr>
<tr class="even">
<td><p>Espace du lecteur contenant les fichiers binaires Exchange insuffisant.</p></td>
<td><p>Brève interruption pendant le basculement automatique.</p></td>
<td><p>Aucun.</p></td>
<td><p>Démontée.</p></td>
<td><p>N’importe lequel</p></td>
<td><p>Libération manuelle d’espace sur le volume.</p></td>
<td><p>Non applicable.</p></td>
</tr>
<tr class="odd">
<td><p>Nouveau journal non valide détecté : La séquence du journal est entravée par un fichier existant.</p></td>
<td><p>Brève interruption pendant le basculement automatique ; problème interprété comme un événement isolé ne concernant pas les autres copies.</p></td>
<td><p>Aucun.</p></td>
<td><p>Démontée.</p></td>
<td><p>Failed</p></td>
<td><p>Suppression des journaux gênants après détermination de la source.</p></td>
<td><p>Les journaux gênants ne doivent pas être répliqués.</p></td>
</tr>
<tr class="even">
<td><p>La fonctionnalité de réplication continue détecte un journal non valide : La fonctionnalité de relecture détecte un journal inapproprié pendant la copie ou la relecture.</p></td>
<td><p>Non applicable.</p></td>
<td><p>Suppression du journal.</p></td>
<td><p>Non applicable.</p></td>
<td><p>Failed</p></td>
<td><p>Suppression du journal non valide ; déplacement du flux de journaux à l’origine du problème.</p></td>
<td><p>Non applicable.</p></td>
</tr>
</tbody>
</table>


## Basculement de base de données

Un basculement de base de données se produit lorsqu’une copie de base de données qui était active ne peut plus l’être. Les événements ci-dessous se produisent dans le cadre d’un basculement de base de données :

1.  La défaillance de la base de données est détectée par le service de banque d’informations Microsoft Exchange.

2.  Le service de banque d’informations Microsoft Exchange écrit les événements d’erreur d’écriture dans le journal des événements du canal Crimson.

3.  Le Gestionnaire Active Manager sur le serveur qui contient la base de données défaillante détecte les événements d’échec.

4.  Le Gestionnaire Active Manager demande l’état de la copie de base de données aux autres serveurs qui contiennent une copie de la base de données.

5.  Les autres serveurs renvoient l’état de la copie de base de données au Gestionnaire Active Manager.

6.  Le Gestionnaire Active Manager principal initie un déplacement de la base de données active vers un autre serveur du groupe de disponibilité de base de données en utilisant un algorithme de sélection de la meilleure copie.

7.  Le Gestionnaire Active Manager principal met l’emplacement de montage de la base de données à jour dans la base de données du cluster pour refléter le serveur sélectionné.

8.  Le Gestionnaire Active Manager principal envoie une requête au Gestionnaire Active Manager sur le serveur sélectionné afin de devenir maître de la base de données.

9.  Le Gestionnaire Active Manager sur le serveur sélectionné demande au service de réplication Microsoft Exchange d’essayer de copier les derniers journaux du serveur précédent et de définir l’indicateur montable pour la base de données.

10. Le service de réplication Microsoft Exchange copie les journaux du serveur qui contenait précédemment la copie active de la base de données.

11. Le Gestionnaire Active Manager lit le nombre maximal de journaux générés dans la base de données du cluster.

12. Le service de banque d’informations Microsoft Exchange monte la nouvelle copie de base de données active.

## Basculement de serveur

Un basculement de serveur se produit lorsque le membre du DAG ne parvient plus à réparer le réseau MAPI, ou lorsque le service de cluster sur un membre du DAG ne peut plus contacter les autres membres du DAG. Les événements suivants se produisent dans le cadre d’un basculement de serveur :

1.  Le service de cluster envoie une notification au Gestionnaire Active Manager principal dans l’un des deux cas :
    
    1.  **Nœud arrêté**   Le serveur est accessible, mais ne peut pas participer aux opérations du DAG.
    
    2.  **Réseau MAPI arrêté**   Le serveur ne peut pas être contacté sur le réseau MAPI et ne peut donc pas participer aux opérations du DAG.

2.  Si le serveur est accessible, le Gestionnaire Active Manager principal contacte Active Manager sur le serveur affecté et demande le démontage immédiat de toutes les bases de données.

3.  Pour chacune des copies de base de données affectées :
    
    1.  Le Gestionnaire Active Manager principal demande l’état de la copie de base de données à tous les serveurs du DAG.
    
    2.  Le Gestionnaire Active Manager principal reçoit une réponse de tous les membres du DAG accessibles et actifs.
    
    3.  Le Gestionnaire Active Manager principal tente de déterminer la source de journal optimale parmi tous les serveurs chargés de répondre en demandant à chacun des répondeurs le numéro de génération de journaux le plus récent.
    
    4.  Chacun des serveurs répond par le numéro de génération de journaux.

4.  Le Gestionnaire Active Manager principal récupère l’état du catalogue d’indexation de recherche actuel dans la base de données du cluster.

5.  Selon le numéro de génération de journaux et l’intégrité du catalogue de chaque copie de base de données, le Gestionnaire Active Manager principal sélectionne les meilleures copies à activer.

6.  Le Gestionnaire Active Manager principal met l’emplacement monté de la base de données à jour dans la base de données du cluster.

7.  Le Gestionnaire Active Manager principal lance le basculement de la base de données en communiquant avec Active Manager sur un ou plusieurs serveurs.

8.  Le Gestionnaire Active Manager sur les serveurs sélectionné demande au service de réplication Microsoft Exchange d’essayer de copier les derniers journaux du serveur précédent et de définir l’indicateur montable.

9.  Lorsque la base de données peut être montée, le Gestionnaire Active Manager sur les serveurs monte les bases de données.

Pour plus d’informations sur le processus de sélection de la meilleure copie par le Gestionnaire Active Manager, consultez la rubrique [Active Manager](active-manager-exchange-2013-help.md).

## Basculements de centres de données

Des modifications importantes ont été apportées dans Exchange 2013 ; elles permettent de relever les défis d’une configuration de résilience de site Exchange 2010. Grâce à la simplification de l’espace de noms, la consolidation des rôles serveur, la séparation de serveur d’accès au client et de récupération de DAG (dans Exchange 2013, il n’est pas nécessaire que l’espace de noms soit déplacé avec le DAG), et les changements concernant l’équilibrage de charge, Exchange 2013 fournit de nouvelles options de résilience de site, telles que la possibilité d’utiliser un seul espace de noms global. En outre, si vous disposez de plus de deux emplacements où déployer des composants de services de messagerie, Exchange 2013 offre également la possibilité de configurer le service de messagerie pour effectuer un basculement automatique pour les défaillances qui nécessitaient une intervention manuelle dans Exchange 2010.

La résilience de site a été simplifiée sur le plan opérationnel dans Exchange 2013. Exchange tire parti de la tolérance de panne intégrée à l’espace de noms par le biais de plusieurs adresses IP et de l’équilibrage de charge (et, si nécessaire, de la possibilité de mettre des serveurs en service et hors service). L’un des changements les plus importants que nous avons apporté à Exchange 2013 a été de tirer parti de la capacité des clients à mettre en cache plusieurs adresses IP renvoyées par un serveur DNS en réponse à une demande de résolution de nom. Si l’on suppose que le client a la capacité de mettre en cache plusieurs adresses IP (ce qui est le cas pour presque tous les clients HTTP et puisque presque tous les protocoles d’accès au client dans Exchange 2013 sont basés sur HTTP (Outlook, Outlook Anywhere, EAS, EWS, OWA, EAC, RPS, etc.), tous les clients HTTP pris en charge peuvent utiliser plusieurs adresses IP), le basculement est de ce fait possible côté client. Vous pouvez configurer DNS pour remettre plusieurs adresses IP à un client lors de la résolution de noms. Le client demande mail.contoso.com et reçoit deux adresses IP, ou quatre adresses IP, par exemple. Néanmoins, de nombreuses adresses IP reçues par le client seront utilisées de façon fiable par celui-ci. Cela s’avère bénéfique pour le client, car si l’une des adresses IP échoue, il peut se connecter à une ou plusieurs autres. Si un client en essaie une mais qu’elle échoue, il attend environ 20 secondes puis essaie la suivante dans la liste. Ainsi, si vous perdez la connectivité à votre tableau de serveur d’accès au client (CAS) principal, et que vous disposez d’une deuxième adresse IP publiée pour un deuxième tableau CAS, la récupération pour les clients se fait automatiquement (et en 21 secondes environ).

Les clients HTTP modernes (systèmes d’exploitation et navigateurs web de moins de 10 ans) fonctionnent automatiquement avec cette redondance, tout simplement. La pile HTTP peut accepter plusieurs adresses IP pour un nom de domaine complet (FQDN), de sorte que si la première adresse IP qu’elle essaie échouement sévèrement (par exemple, connexion impossible), elle essaie l’adresse IP suivante de la liste Si la défaillance est logicielle (perte de connexion une fois la session établie, peut-être en raison d’une défaillance intermittente du service lorsque, par exemple, un périphérique dépose des paquets et doit être mis hors service), l’utilisateur devra peut-être actualiser son navigateur.

Si la configuration est correcte, le basculement peut s’effectuer au niveau du client et les clients sont automatiquement redirigés vers un second centre de données comportant des serveurs d’accès au client en fonctionnement, et ces serveurs d’accès au client en fonctionnement envoient par proxy la communication vers le serveur de boîtes aux lettres de l’utilisateur, qui n’est pas touché par la panne (car vous ne procédez à aucune permutation). Vous n’avez pas besoin de travailler à la récupération du service, car le service le fait lui-même et vous pouvez ainsi vous concentrer sur la résolution de l’erreur principale (par exemple, le remplacement de l’équilibrage de charge défaillant).

Comme vous pouvez faire basculer l’espace de noms entre des centres de données, tout ce dont vous avez besoin pour réaliser un basculement du centre de données, c’est d’un mécanisme de basculement du rôle de boîtes aux lettres entre centres de données. Pour bénéficier d’un basculement automatique pour le DAG, vous concevez simplement une solution dans laquelle le DAG est uniformément réparti entre deux centres de données, puis placez le serveur témoin dans un troisième emplacement afin qu’il puisse être arbitré par des membres du DAG dans chaque centre de données, quel que soit l’état du réseau entre les centres de données contenant les membres du DAG. L’essentiel est que le troisième emplacement soit isolé des défaillances réseau susceptibles de se produire dans les emplacements contenant les membres du DAG.

Si vous n'avez que deux centres de données et que vous souhaitez pouvoir configurer un basculement automatique, vous pouvez utiliser Microsoft Azure comme troisième emplacement. Vous devez créer un réseau virtuel Azure et le connecter à vos deux centres de données à l'aide d'un VPN multi-points. Vous pourrez ensuite placer votre serveur témoin sur une machine virtuelle Microsoft Azure. Pour plus d'informations, voir [Utilisation d'une machine virtuelle Microsoft Azure comme serveur témoin du groupe de disponibilité de base de données (DAG)](using-a-microsoft-azure-vm-as-a-dag-witness-server-exchange-2013-help.md).

