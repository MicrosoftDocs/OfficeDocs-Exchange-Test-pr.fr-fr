---
title: 'Régulation du flux: Exchange 2013 Help'
TOCTitle: Régulation du flux
ms:assetid: 03003544-e802-4988-9427-5fc4da64dcb8
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb201658(v=EXCHG.150)
ms:contentKeyID: 52062933
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Régulation du flux

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2015-03-09_

La régulation du flux est une fonctionnalité d'analyse des ressources du système fournie par le service Microsoft Exchange Transport sur les serveurs de transport Edge et de boîtes aux lettres dans Microsoft Exchange 2013.

Exchange détecte si une pression est exercée sur des ressources vitales, comme l'espace disque et la mémoire disponibles. Il prend alors des mesures pour essayer d'empêcher la non-disponibilité du service. L'objectif de la régulation du flux est de prévenir la saturation des ressources système et de permettre au serveur Exchange de traiter les messages existants avant d'en accepter de nouveaux. Lorsque l'utilisation des ressources système revient à un niveau normal, le serveur Exchange reprend peu à peu un fonctionnement normal et recommence à accepter les nouveaux messages.

Dans Exchange 2013, quand une pression est exercée sur les ressources du service de transport d'un serveur de boîtes aux lettres ou d'un serveur de transport Edge, les connexions entrantes sont acceptées, mais les messages entrants sur ces connexions sont soit acceptés à un rythme plus lent soit rejetés. Lorsqu'un hôte SMTP tente d'établir une connexion avec un serveur Exchange dont les ressources subissent une pression, la connexion aboutit. Cependant, quand l'hôte émet la commande **MAIL FROM** pour envoyer un message, selon la ressource se trouvant sous pression, le service de transport retarde l'accusé de réception de la commande **MAIL FROM** ou rejette la connexion.

**Contenu de cette rubrique**

Ressources analysées

Actions entreprises par le transport Exchange quand une ressource est sous pression

Options de configuration de la régulation du flux dans le fichier EdgeTransport.exe.config

Informations d'enregistrement de la fonctionnalité de régulation du flux

## Ressources analysées

La fonctionnalité de régulation du flux analyse les ressources système suivantes :

  - l'espace disponible sur le disque dur qui stocke la base de données des files d'attente de messages ;

  - l'espace disponible sur le disque dur qui stocke les journaux de transactions de la base de données des files d'attente de messages ;

  - le nombre de transactions de base de données des files d'attente de messages non validées en mémoire ;

  - la mémoire utilisée par le processus EdgeTransport.exe ;

  - la mémoire utilisée par tous les autres processus.

  - Nombre de messages de la file d'attente de soumission.

Pour chaque ressource système analysée sur un serveur de boîtes aux lettres ou de transport Edge, les trois niveaux d'utilisation des ressources suivants sont appliqués :

  - **Normal**   L'utilisation de la ressource n'est pas excessive. Le serveur accepte les nouvelles connexions et les nouveaux messages.

  - **Moyen**   L'utilisation de la ressource commence à être importante. La fonctionnalité de régulation du flux est appliquée au serveur de manière limitée. Les messages provenant d'expéditeurs appartenant à un domaine faisant autorité sont transmis. Toutefois, selon la ressource spécifique sous pression, le serveur utilise les intervalles de répulsion pour retarder la réponse du serveur ou rejeter les commandes **MAIL FROM** entrantes provenant d'autres sources.

  - **Élevé**   L'utilisation de la ressource est excessive. La fonctionnalité de régulation du flux est entièrement appliquée. Tous les flux de messagerie sont interrompus et le serveur refuse les nouvelles commandes **MAIL FROM** entrantes.

Les sections suivantes expliquent comment Exchange gère la situation quand une ressource spécifique est sous pression.

## Espace disponible sur le disque dur pour la base de données des files d'attente de messages

Par défaut, la base de données des files d'attente de messages est située dans %ExchangeInstallPath%TransportRoles\\data\\Queue. Exchange surveille l'utilisation de l'espace disque pour cet emplacement. Le niveau élevé d'utilisation de l'espace disque est calculé à l'aide de la formule suivante :

100 \* (*hard disk size* - *fixed constant*) / *hard drive size*

La valeur de *fixed constant* est de 500 mégaoctets (Mo).

Les résultats de cette formule sont exprimés sous la forme d'un pourcentage de l'espace disponible total sur le disque dur utilisé. Les résultats de la formule sont toujours arrondis au nombre entier inférieur le plus proche. Par défaut, le niveau moyen d'utilisation du disque dur est inférieur de 2 % au niveau élevé. Par défaut, le niveau normal d'utilisation du disque dur est inférieur de 4 % au niveau élevé.

Retour au début

## Espace disponible sur le disque dur pour les journaux de transaction de la base de données des files d'attente de messages

Par défaut, les journaux de transaction de la base de données des files d'attente de messages est située dans %ExchangeInstallPath%TransportRoles\\data\\Queue. Exchange surveille l'utilisation de l'espace disque pour cet emplacement. Le fichier de configuration d'application %ExchangeInstallPath%Bin\\EdgeTransport.exe.config contient une clé *DatabaseCheckPointDepthMax* dont la valeur par défaut est 384 Mo. Cette clé contrôle la taille autorisée totale des journaux de transactions non validés existant sur le disque dur. Ce paramètre est utilisé dans la formule qui calcule l'utilisation du disque dur.

> [!NOTE]
> La valeur du paramètre <em>DatabaseCheckPointDepthMax</em> s'applique à toutes les bases de données du moteur ESE (Extensible Storage Engine) relatives au transport qui existent sur le serveur de boîtes aux lettres ou de transport Edge. Cela inclut la base de données des files d'attente de messages et la base de données de filtres IP.


Par défaut, le niveau élevé d’utilisation du disque dur est calculé à l’aide de la formule suivante :

100 \* (*hard drive size* - Min(5 Go, 3\**DatabaseCheckPointDepthMax*)) / *hard drive size*

Les résultats de la formule sont toujours arrondis au nombre entier inférieur le plus proche. Par défaut, le niveau moyen d'utilisation du disque dur est inférieur de 2 % au niveau élevé. Le niveau normal d'utilisation du disque dur est inférieur de 4 % au niveau élevé.

Retour au début

## Nombre de transactions de base de données des files d'attente de messages non validées en mémoire

La liste des modifications apportées à la base de données des files d'attente de messages est enregistrée jusqu'à ce que ces modifications soient validées dans un journal de transactions. La liste est ensuite validée dans la base de données des files d'attente de messages. Ces transactions de base de données des files d'attente de messages en attente qui sont gardées en mémoire sont appelées *compartiments de version*. Le nombre de compartiments de version peut augmenter jusqu'à atteindre des niveaux élevés en raison d'un volume élevé de messages entrants inattendu, d'attaques de courrier indésirable, d'intégrité de la base de données des files d'attente de messages ou de performances du disque dur.

Quand Exchange commence à recevoir des messages, ces derniers sont regroupés par lots puis préparés sous forme de compartiments de version. Si un message entrant comporte une pièce jointe volumineuse, cette dernière peut être scindée en plusieurs lots. Ces lots en cours de traitement sont appelés *points de lot*. Le nombre de points de lot en suspens peut dépasser les seuils définis, en particulier s'il existe un volume élevé inattendu de messages entrants comportant des pièces jointes volumineuses.

Quand les compartiments de version ou les points de lot sont sous pression, le serveur Exchange commence à limiter les connexions entrantes en retardant l'accusé de réception des messages entrants. Exchange réduit la vitesse du flux de messagerie entrant à l'aide d'intervalles de répulsion, ce qui génère un délai sur les commandes **MAIL FROM**. Si la condition de pression de la ressource se poursuit, Exchange augmente progressivement le délai de répulsion. Une fois que l'utilisation de la ressource revient à la normale, Exchange commence progressivement à réduire le délai d'accusé de réception afin de revenir à un fonctionnement normal. Par défaut, Exchange commence à retarder les accusés de réception des messages de 10 secondes quand une ressource est sous pression. Si la pression sur la ressource se poursuit, le délai est augmenté par incréments de 5 secondes jusqu'à 55 secondes.

Exchange conserve un historique d'utilisation des compartiments de version et des points de lot de la ressource. Si l'utilisation de la ressource ne descend pas sous le niveau normal pendant un nombre spécifique d'intervalles entre deux interrogations, appelé profondeur de l'historique, Exchange arrête le délai de répulsion et commence à rejeter les messages entrants tant que l'utilisation de la ressource ne retrouve pas son niveau normal. Par défaut, les profondeurs de l'historique pour les compartiments de version et les points de lot sont respectivement dans des intervalles entre deux interrogations de 10 et 300.

Retour au début

## Mémoire utilisée par le processus EdgeTransport.exe

Par défaut, le niveau élevé d'utilisation de la mémoire par le processus EdgeTransport.exe est calculé à l'aide de la formule suivante :

75 % de la mémoire physique totale ou 1 To, selon celle de ces deux valeurs qui est la plus faible.

Ce calcul n'inclut pas la mémoire virtuelle disponible sur le disque dur dans le fichier d'échange ou la mémoire utilisée par d'autres processus. Les résultats de cette formule sont exprimés sous la forme d'un pourcentage de la mémoire totale utilisée par le processus EdgeTransport.exe. Les résultats de la formule sont toujours arrondis au nombre entier inférieur le plus proche.

Par défaut, le niveau moyen d'utilisation de la mémoire par le fichier EdgeTransport.exe est calculé comme 73 % de la mémoire physique totale ou inférieur de 2 % à la valeur du niveau élevé, selon celle de ces deux valeurs qui est la plus faible. Par défaut, le niveau normal d'utilisation de la mémoire par le fichier EdgeTransport.exe est calculé comme 71 % de la mémoire physique totale ou inférieur de 4 % à la valeur du niveau élevé, selon celle de ces deux valeurs qui est la plus faible.

Si l'utilisation de la mémoire par le processus EdgeTransport.exe est supérieure au niveau normal spécifié, le *nettoyage de la mémoire* est forcé. Le processus de nettoyage de la mémoire recherche les objets inutilisés existant dans la mémoire et récupère la mémoire utilisée par ces objets.

Exchange conserve un historique de l'utilisation de la mémoire du processus EdgeTransport.exe. Si l'utilisation ne descend pas sous le niveau normal pendant un nombre spécifique d'intervalles entre deux interrogations, appelé profondeur de l'historique, Exchange commence à rejeter les messages entrants tant que l'utilisation de la ressource ne retrouve pas son niveau normal. Par défaut, la profondeur de l'historique pour l'utilisation de la mémoire par EdgeTransport.exe est de 30 intervalles entre deux interrogations.

Retour au début

## Mémoire utilisée par tous les processus

Par défaut, le niveau élevé d'utilisation de la mémoire par tous les processus correspond à 94 % de la mémoire physique totale. Cette valeur n'inclut pas la mémoire virtuelle disponible sur le disque dur dans le fichier d'échange.

Quand le niveau d'utilisation de la mémoire spécifié est atteint, la *mise en attente des messages* survient. La mise en attente du message consiste à supprimer les éléments inutiles des messages placés en file d'attente et mis en cache dans la mémoire. Les messages complets sont mis en cache dans la mémoire en vue d'optimiser les performances. La suppression du contenu MIME des messages placés en files d'attente dans la mémoire réduit la mémoire utilisée et entraîne une latence plus importante, car les messages sont directement lus à partir de la base de données des files d'attente de messages. La mise en attente des messages est activée par défaut.

Retour au début

## Nombre de messages de la file d'attente de soumission.

La file d'attente de soumission est associée au service de transport sur les serveurs de boîtes aux lettres Exchange 2013 et les serveurs de transport Edge. Le catégoriseur traite chaque message dans la file d’attente de soumission. Cette catégorisation a pour effet de mettre le message en fil d'attente de remise. Pour plus d'informations, consultez les rubriques [Flux de messagerie](mail-flow-exchange-2013-help.md) et [Files d'attente](queues-exchange-2013-help.md). Un grand nombre de messages dans la file d'attente de soumission indique que le catégoriseur rencontre des difficultés pour traiter les messages.

Quand la file d'attente de soumission est sous pression, le serveur Exchange commence à limiter les connexions entrantes en retardant l'accusé de réception des messages entrants. Exchange réduit la vitesse du flux de messagerie entrant à l'aide d'intervalles de répulsion, ce qui génère un délai sur les commandes **MAIL FROM**. Si la condition de pression de la ressource se poursuit, Exchange augmente progressivement le délai de répulsion. Une fois que l'utilisation de la ressource revient à la normale, Exchange commence progressivement à réduire le délai d'accusé de réception afin de revenir à un fonctionnement normal. Par défaut, Exchange commence à retarder les accusés de réception des messages de 10 secondes quand une ressource est sous pression. Si la pression sur la ressource se poursuit, le délai est augmenté par incréments de 5 secondes jusqu'à 55 secondes.

Exchange conserve un historique de l'utilisation de la file d'attente de soumission. Si l'utilisation de la ressource ne descend pas sous le niveau normal pendant un nombre spécifique d'intervalles entre deux interrogations, appelé profondeur de l'historique, Exchange arrête le délai de répulsion et commence à rejeter les messages entrants tant que l'utilisation de la ressource ne retrouve pas son niveau normal. Par défaut, la profondeur de l'historique pour la file d'attente de soumission est de 300 intervalles entre deux interrogations.

## Actions entreprises par le transport Exchange quand une ressource est sous pression

Le tableau suivant résume les actions prises par le transport Exchange quand une ressource spécifique est sous pression.

### Actions de régulation du flux prises par les serveurs de de boîtes aux lettres et de transport Edge en réponse à une ressource sous pression

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Ressource sous pression</th>
<th>Niveau d'utilisation</th>
<th>Actions prises</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Espace disque pour la base de données des files d'attente de messages</p></td>
<td><p>Moyen</p></td>
<td><ul>
<li><p>Rejeter les messages entrants provenant de serveurs non Exchange</p></li>
<li><p>Rejeter les envois de message à partir des répertoires de collecte et de relecture</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Espace disque pour la base de données des files d'attente de messages</p></td>
<td><p>Élevé</p></td>
<td><ul>
<li><p>Rejeter les messages entrants provenant d'autres serveurs Exchange</p></li>
<li><p>Rejeter les envois de messages à partir des bases de données de boîtes aux lettres par le service de dépôt de transport de boîte aux lettres sur les serveurs de boîtes aux lettres</p></li>
<li><p>Rejeter les messages entrants provenant de serveurs non Exchange</p></li>
<li><p>Rejeter les envois de messages à partir des répertoires de collecte et de relecture</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Espace disque pour les journaux de transactions de la base de données des files d'attente de messages</p></td>
<td><p>Moyen</p></td>
<td><ul>
<li><p>Rejeter les messages entrants provenant de serveurs non Exchange</p></li>
<li><p>Rejeter les envois de messages à partir des répertoires de collecte et de relecture</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Espace disque pour les journaux de transactions de la base de données des files d'attente de messages</p></td>
<td><p>Élevé</p></td>
<td><ul>
<li><p>Rejeter les messages entrants provenant d'autres serveurs Exchange</p></li>
<li><p>Rejeter les envois de messages à partir des bases de données de boîtes aux lettres par le service de dépôt de transport de boîte aux lettres sur les serveurs de boîtes aux lettres</p></li>
<li><p>Rejeter les messages entrants provenant de serveurs non Exchange</p></li>
<li><p>Rejeter les envois de messages à partir des répertoires de collecte et de relecture</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Compartiments de version</p></td>
<td><p>Moyen</p></td>
<td><p>Introduire ou incrémenter le délai de répulsion aux messages entrants. Si le niveau normal n'est pas atteint pour l'intégralité de la profondeur de l'historique des compartiments de version, procédez comme suit :</p>
<ul>
<li><p>Rejeter les messages entrants provenant de serveurs non Exchange</p></li>
<li><p>Rejeter les envois de messages à partir des répertoires de collecte et de relecture</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Compartiments de version</p></td>
<td><p>Élevé</p></td>
<td><p>Introduire ou incrémenter le délai de répulsion aux messages entrants. Si le niveau normal n'est pas atteint pour l'intégralité de la profondeur de l'historique des compartiments de version, procédez comme suit :</p>
<ul>
<li><p>Rejeter les messages entrants provenant d'autres serveurs Exchange</p></li>
<li><p>Rejeter les envois de messages à partir des bases de données de boîtes aux lettres par le service de dépôt de transport de boîte aux lettres sur les serveurs de boîtes aux lettres</p></li>
<li><p>Rejeter les messages entrants provenant de serveurs non Exchange</p></li>
<li><p>Rejeter les envois de messages à partir des répertoires de collecte et de relecture</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Point de lot</p></td>
<td><p>Moyen</p></td>
<td><p>Introduire ou incrémenter le délai de répulsion aux messages entrants. Si le niveau normal n'est pas atteint pour l'intégralité de la profondeur de l'historique des points de lot, procédez comme suit :</p>
<ul>
<li><p>Rejeter les messages entrants provenant de serveurs non Exchange</p></li>
<li><p>Rejeter les envois de messages à partir des répertoires de collecte et de relecture</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Point de lot</p></td>
<td><p>Élevé</p></td>
<td><p>Introduire ou incrémenter le délai de répulsion aux messages entrants. Si le niveau normal n'est pas atteint pour l'intégralité de la profondeur de l'historique des points de lot, procédez comme suit :</p>
<ul>
<li><p>Rejeter les messages entrants provenant d'autres serveurs Exchange</p></li>
<li><p>Rejeter les envois de messages à partir des bases de données de boîtes aux lettres par le service de dépôt de transport de boîte aux lettres sur les serveurs de boîtes aux lettres</p></li>
<li><p>Rejeter les messages entrants provenant de serveurs non Exchange</p></li>
<li><p>Rejeter les envois de messages à partir des répertoires de collecte et de relecture</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Mémoire utilisée par le processus EdgeTransport.exe</p></td>
<td><p>Moyen</p></td>
<td><ul>
<li><p>Rejeter les messages entrants provenant de serveurs non Exchange</p></li>
<li><p>Rejeter les envois de messages à partir des répertoires de collecte et de relecture</p></li>
<li><p>Forcer un nettoyage de la mémoire</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Mémoire utilisée par le processus EdgeTransport.exe</p></td>
<td><p>Élevé</p></td>
<td><ul>
<li><p>Rejeter les messages entrants provenant d'autres serveurs Exchange</p></li>
<li><p>Rejeter les envois de messages à partir des bases de données de boîtes aux lettres par le service de dépôt de transport de boîte aux lettres sur les serveurs de boîtes aux lettres</p></li>
<li><p>Rejeter les messages entrants provenant de serveurs non Exchange</p></li>
<li><p>Rejeter les envois de messages à partir des répertoires de collecte et de relecture</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Mémoire utilisée par tous les processus</p></td>
<td><p>Moyen</p></td>
<td><ul>
<li><p>Rejeter les messages entrants provenant de serveurs non Exchange</p></li>
<li><p>Rejeter les envois de messages à partir des répertoires de collecte et de relecture</p></li>
<li><p>Forcer un nettoyage de la mémoire</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Mémoire utilisée par tous les processus</p></td>
<td><p>Élevé</p></td>
<td><ul>
<li><p>Rejeter les messages entrants provenant d'autres serveurs Exchange</p></li>
<li><p>Rejeter les envois de messages à partir des bases de données de boîtes aux lettres par le service de dépôt de transport de boîte aux lettres sur les serveurs de boîtes aux lettres</p></li>
<li><p>Rejeter les messages entrants provenant de serveurs non Exchange</p></li>
<li><p>Rejeter les envois de messages à partir des répertoires de collecte et de relecture</p></li>
<li><p>Vider le cache DNS optimisé à partir de la mémoire</p></li>
<li><p>Démarrer la mise en attente des messages</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Nombre de messages de la file d'attente de soumission</p></td>
<td><p>Moyen</p></td>
<td><p>Introduire ou incrémenter le délai de répulsion aux messages entrants. Si le niveau normal n'est pas atteint pour l'intégralité de la profondeur de l'historique de file d'attente de soumission, procédez comme suit :</p>
<ul>
<li><p>Rejeter les messages entrants provenant de serveurs non Exchange</p></li>
<li><p>Rejeter les envois de messages à partir des répertoires de collecte et de relecture</p></li>
<li><p>Forcer un nettoyage de la mémoire</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Nombre de messages de la file d'attente de soumission</p></td>
<td><p>Élevé</p></td>
<td><p>Introduire ou incrémenter le délai de répulsion aux messages entrants. Si le niveau normal n'est pas atteint pour l'intégralité de la profondeur de l'historique de file d'attente de soumission, procédez comme suit :</p>
<ul>
<li><p>Rejeter les messages entrants provenant d'autres serveurs Exchange</p></li>
<li><p>Rejeter les envois de messages à partir des bases de données de boîtes aux lettres par le service de dépôt de transport de boîte aux lettres sur les serveurs de boîtes aux lettres</p></li>
<li><p>Rejeter les messages entrants provenant de serveurs non Exchange</p></li>
<li><p>Rejeter les envois de messages à partir des répertoires de collecte et de relecture</p></li>
<li><p>Vider le cache DNS optimisé à partir de la mémoire</p></li>
<li><p>Démarrer la mise en attente des messages</p></li>
</ul></td>
</tr>
</tbody>
</table>


Retour au début

## Options de configuration de la régulation du flux dans le fichier EdgeTransport.exe.config

Toutes les options de configuration de la régulation du flux sont disponibles dans le fichier XML de configuration d'application %ExchangeInstallPath%Bin\\EdgeTransport.exe.config.

> [!CAUTION]
> Ces paramètres sont répertoriés sous forme de référence uniquement. Il est fortement déconseillé de modifier les paramètres de régulation du flux dans le fichier EdgeTransport.exe.config. La modification des paramètres de régulation du flux peut entraîner une dégradation des performance ou une perte de données. Nous vous conseillons d'identifier et de corriger la cause première de tout événement de régulation du flux que vous pouvez rencontrer.


### Options de configuration de la régulation du flux

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Nom de clé</th>
<th>Valeur par défaut</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>EnableResourceMonitoring</em></p></td>
<td><p>true</p></td>
</tr>
<tr class="even">
<td><p><em>ResourceMonitoringInterval</em></p></td>
<td><p><code>00:00:02</code> (2 secondes).</p></td>
</tr>
<tr class="odd">
<td><p><em>PercentageDatabaseDiskSpaceUsedHighThreshold</em></p></td>
<td><p>0. Cette valeur indique que la formule par défaut est utilisée.</p></td>
</tr>
<tr class="even">
<td><p><em>PercentageDatabaseDiskSpaceUsedMediumThreshold</em></p></td>
<td><p>0. La valeur indique que la valeur réelle est inférieure de 2 % à la valeur du paramètre <em>PercentageDatabaseDiskSpaceUsedHighThreshold</em>.</p></td>
</tr>
<tr class="odd">
<td><p><em>PercentageDatabaseDiskSpaceUsedNormalThreshold</em></p></td>
<td><p>0. La valeur indique que la valeur réelle est inférieure de 2 % à la valeur du paramètre <em>PercentageDatabaseDiskSpaceUsedMediumThreshold</em>.</p></td>
</tr>
<tr class="even">
<td><p><em>PercentageDatabaseLoggingDiskSpaceUsedHighThreshold</em></p></td>
<td><p>0. Cette valeur indique que la formule par défaut est utilisée.</p></td>
</tr>
<tr class="odd">
<td><p><em>PercentageDatabaseLoggingDiskSpaceUsedMediumThreshold</em></p></td>
<td><p>0. La valeur indique que la valeur réelle est inférieure de 2 % à la valeur du paramètre <em>PercentageDatabaseLoggingDiskSpaceUsedHighThreshold</em>.</p></td>
</tr>
<tr class="even">
<td><p><em>PercentageDatabaseLoggingDiskSpaceUsedNormalThreshold</em></p></td>
<td><p>0. La valeur indique que la valeur réelle est inférieure de 2 % à la valeur du paramètre <em>PercentageDatabaseLoggingDiskSpaceUsedMediumThreshold</em>.</p></td>
</tr>
<tr class="odd">
<td><p><em>PercentagePrivateBytesUsedHighThreshold</em></p></td>
<td><p>0. Cette valeur indique que le calcul par défaut est utilisé.</p></td>
</tr>
<tr class="even">
<td><p><em>PercentagePrivateBytesUsedMediumThreshold</em></p></td>
<td><p>0. La valeur indique que la valeur réelle est inférieure de 2 % à la valeur du paramètre <em>PercentagePrivateBytesUsedHighThreshold</em>.</p></td>
</tr>
<tr class="odd">
<td><p><em>PercentagePrivateBytesUsedNormalThreshold</em></p></td>
<td><p>0. La valeur indique que la valeur réelle est inférieure de 2 % à la valeur du paramètre <em>PercentagePrivateBytesUsedMediumThreshold</em>.</p></td>
</tr>
<tr class="even">
<td><p><em>VersionBucketsHighThreshold</em></p></td>
<td><p>200</p></td>
</tr>
<tr class="odd">
<td><p><em>VersionBucketsMediumThreshold</em></p></td>
<td><p>120</p></td>
</tr>
<tr class="even">
<td><p><em>VersionBucketsNormalThreshold</em></p></td>
<td><p>80</p></td>
</tr>
<tr class="odd">
<td><p><em>VersionBucketsHistoryDepth</em></p></td>
<td><p>10</p></td>
</tr>
<tr class="even">
<td><p><em>BatchPointHighThreshold</em></p></td>
<td><p>4000</p></td>
</tr>
<tr class="odd">
<td><p><em>BatchPointMediumThreshold</em></p></td>
<td><p>2000</p></td>
</tr>
<tr class="even">
<td><p><em>BatchPointNormalThreshold</em></p></td>
<td><p>1000</p></td>
</tr>
<tr class="odd">
<td><p><em>BatchPointHistoryDepth</em></p></td>
<td><p>300</p></td>
</tr>
<tr class="even">
<td><p><em>BatchPointUseCostForPressure</em></p></td>
<td><p>true</p></td>
</tr>
<tr class="odd">
<td><p><em>BatchPointBatchSize</em></p></td>
<td><p>40</p></td>
</tr>
<tr class="even">
<td><p><em>BatchPointBatchTimeout</em></p></td>
<td><p><code>00:00:00.100</code> (0,1 secondes).</p></td>
</tr>
<tr class="odd">
<td><p><em>BatchPointItemExpiryInterval</em></p></td>
<td><p><code>00:05:00</code> (5 minutes)</p></td>
</tr>
<tr class="even">
<td><p><em>SMTPBaseThrottlingDelayInterval</em></p></td>
<td><p><code>00:00:00</code></p></td>
</tr>
<tr class="odd">
<td><p><em>SMTPMaxThrottlingDelayInterval</em></p></td>
<td><p><code>00:00:55</code> (55 secondes).</p></td>
</tr>
<tr class="even">
<td><p><em>SMTPStepThrottlingDelayInterval</em></p></td>
<td><p><code>00:00:05</code> (5 secondes).</p></td>
</tr>
<tr class="odd">
<td><p><em>SMTPStartThrottlingDelayInterval</em></p></td>
<td><p><code>00:00:10</code> (10 secondes).</p></td>
</tr>
<tr class="even">
<td><p><em>PercentagePhysicalMemoryUsedLimit</em></p></td>
<td><p>94</p></td>
</tr>
<tr class="odd">
<td><p><em>DehydrateMessagesUnderMemoryPressure</em></p></td>
<td><p>true</p></td>
</tr>
<tr class="even">
<td><p><em>PrivateBytesHistoryDepth</em></p></td>
<td><p>30</p></td>
</tr>
<tr class="odd">
<td><p><em>SubmissionQueueHighThreshold</em></p></td>
<td><p>10000</p></td>
</tr>
<tr class="even">
<td><p><em>SubmissionQueueMediumThreshold</em></p></td>
<td><p>4000</p></td>
</tr>
<tr class="odd">
<td><p><em>SubmissionQueueNormalThreshold</em></p></td>
<td><p>2000</p></td>
</tr>
<tr class="even">
<td><p><em>SubmissionQueueHistoryDepth</em></p></td>
<td><p>300</p></td>
</tr>
</tbody>
</table>


Retour au début

## Informations d'enregistrement de la fonctionnalité de régulation du flux

La liste suivante répertorie les entrées du journal des événements qui sont générées par des événements de régulation du flux spécifiques dans Exchange :

  - **Entrée du journal des événements correspondant à une augmentation du niveau d'utilisation des ressources**
    
    Type d'événement : Erreur
    
    Source de l'événement : MSExchangeTransport
    
    Catégorie d'événement : gestionnaire des ressources
    
    ID de l'événement : 15004
    
    Description : La pression sur les ressources a diminué, passant de *Previous Utilization Level* à *Current Utilization Level*.

  - **Entrée du journal des événements correspondant à une diminution du niveau d'utilisation des ressources**
    
    Type d'événement : Informations
    
    Source de l'événement : MSExchangeTransport
    
    Catégorie d'événement : gestionnaire des ressources
    
    ID de l'événement : 15005
    
    Description : La pression sur les ressources a diminué, passant de *Previous Utilization Level* à *Current Utilization Level*.

  - **Entrée de journal des événements correspondant à un espace disque disponible extrêmement faible**
    
    Type d'événement : Erreur
    
    Source de l'événement : MSExchangeTransport
    
    Catégorie d'événement : gestionnaire des ressources
    
    ID de l'événement : 15006
    
    Description : Le service de transport Microsoft Exchange rejette les messages car l'espace disque disponible est en dessous du seuil configuré. Une action d'administration peut être requise pour libérer de l'espace disque pour que le service poursuive les opérations.

  - **Entrée de journal des événements correspondant à une mémoire disponible extrêmement faible**
    
    Type d'événement : Erreur
    
    Source de l'événement : MSExchangeTransport
    
    Catégorie d'événement : gestionnaire des ressources
    
    ID de l'événement : 15007
    
    Description : Le service de transport Microsoft Exchange rejette les envois de messages, car le service continue à consommer plus de mémoire que le seuil configuré. Ceci peut nécessiter le redémarrage du service pour continuer à fonctionner normalement.

Retour au début

