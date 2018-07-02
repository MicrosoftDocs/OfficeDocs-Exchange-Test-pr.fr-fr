---
title: 'Disponibilité gérée: Exchange 2013 Help'
TOCTitle: Disponibilité gérée
ms:assetid: ceb99e6f-6dca-446d-abfb-3e6fc6a72704
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dn482056(v=EXCHG.150)
ms:contentKeyID: 59890421
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Disponibilité gérée

 

_**Sapplique à :** Exchange Online, Exchange Server 2013 SP1_

_**Dernière rubrique modifiée :** 2017-03-29_

S’assurer que les utilisateurs ont une bonne expérience de messagerie a toujours été l’objectif principal des administrateurs de système de messagerie. Pour aider à garantir la disponibilité et la fiabilité de votre organisation Microsoft Exchange Server 2013, tous les aspects du système doivent être surveillés activement, et tous les problèmes détectés doivent être résolus rapidement. Dans les versions précédentes de Exchange, la surveillance des composants critiques du système impliquait généralement l’utilisation d’une application externe telle que Microsoft System Center 2012 Operations Manager pour collecter des données et pour fournir des actions de récupération pour des problèmes détectés à la suite de l’analyse des données recueillies. Exchange 2010 et les versions antérieures incluaient des manifestes d’intégrité et des moteurs de corrélation sous la forme de packs de gestion. Ces composants permettaient à Operations Manager de déterminer si un composant particulier était intègre ou non. En outre, Operations Manager utilisait également l’infrastructure de la cmdlet de diagnostic intégrée à Exchange 2010 pour exécuter des transactions synthétiques pour divers aspects du système.

Exchange 2013 adopte une nouvelle approche de surveillance et cherche à améliorer l’expérience de l’utilisateur final de manière native avec une fonctionnalité appelée *Disponibilité gérée*, qui fournit des actions de récupération et de surveillance intégrées.

## Disponibilité gérée

La disponibilité gérée, également appelée *Surveillance active* ou *Surveillance active locale*, est l’intégration des actions de récupération et de surveillance intégrées avec la plateforme de haute disponibilité Exchange. Elle est conçue pour détecter des problèmes et procéder à une récupération dès qu’ils apparaissent ou sont découverts par le système. À la différence des techniques et solutions externes de surveillance précédentes pour Exchange, la disponibilité gérée ne tente pas d’identifier ni de communiquer la cause première d’un incident. Au contraire, elle se concentre sur les aspects de récupération qui visent trois domaines clés de l’expérience utilisateur :

  - **Disponibilité**   Les utilisateurs peuvent-ils accéder à ce service ?

  - **Latence**   Quelle est l’expérience pour les utilisateurs ?

  - **Erreurs**   Les utilisateurs peuvent-ils faire ce qu’ils veulent ?

La consolidation du rôle serveur et les autres modifications d’architecture dans Exchange 2013 nécessitent une nouvelle approche des méthodes de surveillance et du modèle d’intégrité utilisés dans les versions précédentes de ’Exchange. La disponibilité gérée a été conçue pour gérer ces modifications et fournir une solution native de surveillance de l’intégrité et de récupération. Elle s’écarte des tronçons distincts et individuels de surveillance du système pour se rapprocher de la surveillance de l’expérience utilisateur de bout en bout et de la protection de l’expérience de l’utilisateur final par le biais d’actions orientées récupération.

La disponibilité gérée est un processus interne qui s'exécute sur chaque serveur Exchange 2013. Elle interroge et analyse des centaines de paramètres d’intégrité par seconde. Si un élément est considéré comme incorrect, il sera généralement corrigé automatiquement. Cependant, il existera toujours des problèmes que la disponibilité gérée ne sera pas en mesure de corriger elle-même. Dans ce cas, la disponibilité gérée fait remonter le problème à un administrateur par le biais de la journalisation des événements.

La disponibilité gérée est implémentée sous la forme de deux services :

  - **Service de gestionnaire d’intégrité Exchange (MSExchangeHMHost.exe)**   Il s’agit d’un processus contrôleur permettant de gérer des processus de travail. Il permet de générer, d’exécuter et de démarrer et d’arrêter le processus de travail, selon les besoins. Il permet également de récupérer le processus de travail en cas d’échec de ce dernier, afin d’empêcher le processus de travail de devenir un point de défaillance unique.

  - **Processus de travail du gestionnaire d’intégrité Exchange (MSExchangeHMWorker.exe)**   Il s’agit du processus de travail qui est chargé de réaliser les tâches d’exécution dans la structure de disponibilité gérée.

La disponibilité gérée utilise un stockage persistant pour remplir ses fonctions :

  - Les fichiers XML du dossier \\bin\\Monitoring\\config sont utilisés pour stocker les paramètres de configuration de certains éléments de surveillance et de sondage.

  - Active Directory est utilisé pour stocker les substitutions globales.

  - Le registre de Windows est utilisé pour stocker des données d’exécution, comme les signets, et les substitutions locales (propres à un serveur).

  - L’infrastructure du journal des événements du canal pourpre de Windows est utilisée pour stocker les résultats d’éléments de travail.

  - Les boîtes aux lettres d’intégrité sont utilisées pour l’activité de sondage. Plusieurs boîtes aux lettres d’intégrité seront créées sur chaque base de données de boîtes aux lettres qui existe sur le serveur.

Comme le montre l’illustration ci-dessous, la disponibilité gérée comprend trois principaux composants asynchrones qui fonctionnent en permanence.

**Composants de la disponibilité gérée**

![Disponibilité gérée dans Exchange Server 2013](images/Dn482056.7a54dcb5-1e28-4bd4-87e6-0d496b4ab796(EXCHG.150).gif "Disponibilité gérée dans Exchange Server 2013")

Le premier composant s’appelle une *sonde*. Les sondes prennent les mesures sur le serveur et collectent des données. Les résultats de ces mesures sont transmis au deuxième composant, le *moniteur*. Le moniteur contient toute la logique métier utilisée par le système sur la base de ce qui doit être ou non considéré comme intègre sur les données collectées. À l'instar d'un moteur de reconnaissance de suites logiques, le moniteur recherche les différentes suites logiques sur toutes les mesures collectées, puis détermine ce qu'il considère comme intègre. Enfin, il existe des *répondeurs* chargés des actions de récupération et d’escalade. En cas de manque d’intégrité, la première action consiste à tenter de récupérer ce composant. Ces actions peuvent se dérouler en plusieurs phases. Par exemple, la première tentative peut être le redémarrage du pool d’applications, la seconde le redémarrage du service, la troisième le redémarrage du serveur et la quatrième la déconnexion du serveur pour qu'il n'accepte plus de trafic. Si les mesures de récupération ont échoué, le système transfère le problème à un être humain grâce à des notifications dans le journal d’événements.

Il existe trois principales catégories de sondes : les sondes récurrentes, les notifications et les contrôles. Les sondes récurrentes sont des transactions synthétiques effectuées par le système pour tester l’expérience utilisateur de bout en bout. Les contrôles constituent l’infrastructure qui effectue la collecte des données de performances, y compris le trafic utilisateur et qui mesure les données collectées et les compare aux seuils définis pour déterminer les pointes de pannes des utilisateurs. L’infrastructure des contrôles est ainsi informée au moment où les utilisateurs rencontrent des problèmes. Enfin, la logique de notification permet au système de prendre immédiatement des mesures en cas d’événement grave sans devoir attendre les résultats des données collectées par une sonde. Il s'agit généralement d’exceptions ou de conditions détectables et reconnaissables sans échantillonnage important.

Les sondes récurrentes sont exécutées à quelques minutes d’intervalle et vérifient certains aspects de l’état du service. Elles peuvent transmettre un courrier électronique via Exchange ActiveSync à une boîte aux lettres de surveillance. Elles peuvent aussi être connectées à un point de terminaison RPC ou vérifier la connectivité d’accès à la boîte aux lettres du client.

Toutes les sondes sont définies au démarrage du service du Gestionnaire d’intégrité dans le canal pourpre Microsoft.Exchange.ActiveMonitoring\\ProbeDefinition. La définition de chaque sonde possède de nombreuses propriétés, mais les plus pertinentes sont les suivantes :

  - **Name** : nom de la sonde, qui commence avec un *SampleMask* du moniteur de la sonde.

  - **TypeName** : type d’objet de code de la sonde qui contient la logique de la sonde.

  - **ServiceName** : nom du groupe d’intégrité contenant cette sonde.

  - **TargetResource** : objet que la sonde valide. Cet élément est ajouté au nom de la sonde lors de son exécution afin de devenir un élément *ResultName* de résultat de la sonde.

  - **RecurrenceIntervalSeconds** : fréquence d’exécution de la sonde.

  - **TimeoutSeconds** : temps d’attente de la sonde avant échec.

Il existe des centaines de sondes récurrentes. Beaucoup de ces sondes sont propres à des bases de données. Par conséquent, leur nombre augmente à mesure que des bases de données sont ajoutées. La plupart des sondes sont définies dans le code et ne sont donc pas directement détectables.

Les bases d’une sonde récurrente sont les suivantes : démarrer toutes les *RecurrenceIntervalSeconds* et vérifier (ou sonder) certains aspects de l’intégrité. Si le composant est en bon état, la sonde transmet et écrit un événement d’informations dans le canal Microsoft.Exchange.ActiveMonitoring\\ProbeResult avec un *ResultType* de 3. Si le contrôle échoue ou expire, la sonde échoue et écrit un événement d’erreur dans le même canal. Un *ResultType* de 4 signifie que le contrôle a échoué et un *ResultType* de 1 signifie qu’il a expiré. Un grand nombre de sondes sont réexécutées si elles expirent, jusqu’à la valeur de la propriété *MaxRetryAttempts*.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><strong>Remarque :</strong> le canal pourpre ProbeResult peut être très occupé, car des centaines de sondes sont exécutées toutes les minutes et journalisent des événements. L’impact réel sur les performances de votre serveur Exchange peur s’avérer considérable si vous tentez d’exécuter des requêtes coûteuses sur les journaux des événements dans un environnement de production.</td>
</tr>
</tbody>
</table>


Les notifications sont des sondes qui ne sont pas exécutées par l’infrastructure du Gestionnaire d’intégrité, mais par un autre service sur le serveur. Ces services effectuent leur propre surveillance, puis fournissent leurs données à l’infrastructure de disponibilité gérée en écrivant directement les résultats des sondes. Vous ne verrez pas ces sondes dans le canal ProbeDefinition, car ce canal ne décrit que les sondes exécutées par l’infrastructure de disponibilité gérée. Par exemple, le moniteur ServerOneCopyMonitor est déclenché par les résultats de la sonde écrits par le service MSExchangeDAGMgmt. Ce service effectue sa propre surveillance, détermine s’il y a un problème et enregistre le résultat de la sonde. La plupart des sondes de notification peuvent journaliser un événement rouge qui rend le moniteur défectueux et un événement vert qui rétablit l’état du moniteur.

Les contrôles sont des sondes qui journalisent les événements uniquement lorsque le compteur de performances passe au-dessus ou en dessous d’un seuil défini. Ils correspondent vraiment à un cas particulier de sondes de notification, car il s’agit d’un service qui surveille les compteurs de performances sur le serveur et qui journalise les événements dans le canal ProbeResult lorsque le seuil configuré est atteint.

Pour connaitre le compteur et le seuil considéré comme défectueux, vous pouvez consulter ce contrôle dans le moniteur. Un moniteur du type *Microsoft.Office.Datacenter.ActiveMonitoring.OverallConsecutiveSampleValueAboveThresholdMonitor* ou *Microsoft.Office.Datacenter.ActiveMonitoring.OverallConsecutiveSampleValueBelowThresholdMonitor* signifie que la sonde qu’il surveille est une sonde de contrôle.

Les moniteurs interrogent les données collectées au moyen de sondes pour déterminer si une action doit être menée selon un ensemble de règles prédéfinies. Selon la règle ou la nature du problème, un moniteur peut lancer un répondeur ou faire remonter le problème pour une intervention humaine via une entrée dans le journal des événements. De plus, les moniteurs définissent le délai au bout duquel le répondeur est exécuté après une panne, ainsi que le flux de travail de l’action de récupération. Les moniteurs ont différents états. Du point de vue de l’état système, les moniteurs ont deux états :

  - **Intègre**   Le moniteur fonctionne correctement et toutes les mesures collectées sont dans les tolérances normales des paramètres de fonctionnement

  - **Non intègre**   Le moniteur est défectueux et a lancé une action de récupération via un répondeur ou averti un administrateur par le biais d’une escalade.

Du point de vue de l’administrateur, les moniteurs ont d’autres états qui apparaissent dans le Shell :

  - **Dégradé**   Lorsque l’état d’un moniteur est « non intègre » sur une période de 0 à 60 secondes, il est considéré comme Dégradé. Si un moniteur est dans l'état non intègre pendant plus de 60 secondes, il est considéré comme Non intègre.

  - **Désactivé**   Le moniteur a été explicitement désactivé par un administrateur.

  - **Indisponible**   Le service d’intégrité Microsoft Exchange interroge régulièrement chaque moniteur pour connaître son état. S’il ne reçoit pas de réponse à la requête, l’état du moniteur devient Indisponible.

  - **En cours de réparation**   Un administrateur définit l’état « En cours de réparation » pour indiquer au système qu’une action correctrice est en cours d’exécution par une intervention humaine : cela permet au système et aux personnes de faire la distinction avec d’autres pannes qui peuvent se produire au même moment alors que l’action correctrice est en cours d’exécution (par exemple, l’opération de réamorçage d’une copie d’une base de données).

La définition de chaque moniteur contient une propriété *SampleMask*. Lors de l’exécution du moniteur, celui-ci recherche les événements du canal ProbeResult qui possèdent un *ResultName* correspondant à l’élément *SampleMask* du moniteur. Ces événements peuvent provenir de sondes récurrentes, de notifications ou de contrôles. Si les seuils du moniteur sont atteints, celui-ci devient défectueux. Du point de vue du moniteur, les trois types de sonde sont identiques, car ils journalisent tous les événements dans le canal ProbeResult.

L’échec d’une seule sonde ne traduit pas nécessairement un dysfonctionnement au niveau du serveur. Le but des moniteurs est d’identifier correctement les problèmes réels qui doivent être corrigés. C’est la raison pour laquelle de nombreux moniteurs ne signalent un dysfonctionnement qu’après l’échec de plusieurs sondes. Et même dans ce cas, la plupart de ces problèmes peuvent être résolus automatiquement par les répondeurs. Par conséquent, le meilleur emplacement pour rechercher des problèmes qui nécessitent une intervention manuelle est le canal pourpre Microsoft.Exchange.ManagedAvailability\\Monitoring. Ce canal inclut l’erreur de sonde la plus récente.

Comme leur nom l’indique, les répondeurs exécutent une sorte de réponse à une alerte qui a été générée par un moniteur. Les répondeurs effectuent diverses actions de récupération, comme la réinitialisation d’un pool de travail d’applications et le redémarrage d’un serveur. Il existe plusieurs types de répondeurs :

  - **Répondeur de redémarrage** Arrête et redémarre un service

  - **Répondeur de réinitialisation de pool d’applications** Arrête et redémarre un pool d’applications dans IIS (Internet Information Services)

  - **Répondeur de basculement** Lance un basculement de base de données ou de serveur

  - **Répondeur de vérification d’erreurs** Lance une vérification d’erreurs sur le serveur, ce qui provoque un redémarrage du serveur

  - **Répondeur hors ligne** Rend hors service un protocole sur un serveur (rejette les demandes des clients)

  - **Répondeur en ligne** Remet en service un protocole sur un serveur (accepte les demandes des clients)

  - **Répondeur d’escalade** Transmet le problème à un administrateur via la journalisation des événements

Outre les répondeurs mentionnés ci-dessus, certains composants disposent également de leurs propres répondeurs spécialisés.

Tous les répondeurs comprennent un comportement de limitation, qui fournit un mécanisme de séquencement intégré pour le contrôle des actions de répondeur. Le comportement de limitation est conçu pour garantir que le système n’est pas compromis ni aggravé suite aux actions de récupération du répondeur. Tous les répondeurs sont limités d’une certaine façon. Lorsque la limitation se produit, l’action de récupération du répondeur peut être ignorée ou différée, selon l’action du répondeur. Par exemple, lorsque le répondeur de vérification d’erreurs est limité, son action est ignorée, et non différée.

## Indicateurs d’intégrité

Du point de vue des rapports, la disponibilité gérée offre deux vues de l’intégrité, une interne et une externe. La vue interne utilise les *indicateurs d’intégrité*. Chaque composant de Exchange 2013 (par exemple, Outlook Web App, Exchange ActiveSync, le service de banque d’informations, l’indexation de contenu, les services de transport, etc.) est surveillé par la disponibilité gérée à l’aide de sondes, de moniteurs et de répondeurs. Un groupe de sondes, de moniteurs et de répondeurs d’un composant donné est appelé un *indicateur d’intégrité*. Un indicateur d’intégrité est un groupe de sondes, de moniteurs et de répondeurs qui détermine si ce composant est intègre. L’état actuel d’un indicateur d’intégrité (par exemple, s’il est intègre ou non) est déterminé à l’aide de l’état des moniteurs de cet indicateur d’intégrité. Si tous les moniteurs d’un indicateur d’intégrité sont intègres, alors l’indicateur d’intégrité est également intègre. Si un moniteur n'est pas intègre, alors l’état de l’indicateur d’intégrité sera déterminé par son moniteur le moins intègre.

Pour obtenir la procédure détaillée pour l’affichage de l’intégrité d’un serveur ou de l’état des indicateurs d’intégrité, voir [Gérer les indicateurs d'intégrité et l'intégrité du serveur](manage-health-sets-and-server-health-exchange-2013-help.md).

## Groupes d’intégrité

La vue externe de la disponibilité gérée est composée de *groupes d’intégrité*. Les groupes d’intégrité sont exposés à System Center Operations Manager 2007 R2 et à System Center Operations Manager 2012.

Il existe quatre principaux groupes d’intégrité :

  - **Points de contact du client** Les composants qui affectent les interactions des utilisateurs en temps réel, tels que les protocoles ou la banque d’informations

  - **Composants de service** Les composants sans interactions directes des utilisateurs en temps réel, tels que le service de réplication de boîtes aux lettre Microsoft Exchange ou le processus de génération de carnet d’adresses en mode hors connexion (OABGen)

  - **Composants de serveur** Les ressources physiques du serveur, telles que l’espace disque, la mémoire et la mise en réseau

  - **Disponibilité des dépendances** La capacité du serveur à accéder aux dépendances nécessaires, telles que Active Directory, DNS, etc.

Lors de l’installation, Exchange Management Pack System Center Operations Manager (SCOM) agit comme un portail sur la santé pour l’affichage des informations relatives à l’environnement de Exchange. Le tableau de bord SCOM inclut trois modes de fonctionnement du serveur Exchange:

  - **Alertes actives** Les répondeurs d’escalade écrivent des événements dans le journal des événements Windows et ceux-ci sont utilisés par le moniteur dans SCOM. Cela apparaît sous forme d’alertes dans la vue Alertes actives.

  - **Intégrité de l’organisation** Un résumé cumulatif de l’intégrité globale de l’intégrité de l’organisation Exchange est affiché dans cette vue. Ces cumuls comprennent l’affichage de l’intégrité pour les différents groupes de disponibilité de base de données, et de l’intégrité de sites Active Directory spécifiques.

  - **Intégrité du serveur** Les indicateurs d’intégrité associés sont réunis en groupes d’intégrité et résumés dans cette vue.

## Substitutions

Les substitutions offrent à l’administrateur la possibilité de configurer certains aspects des sondes, des moniteurs et des répondeurs de disponibilité gérée. Les substitutions peuvent être utilisées pour régler certains des seuils utilisés par la disponibilité gérée. Elles peuvent également être utilisées pour permettre des actions d’urgence pour les événements imprévus qui peuvent nécessiter des paramètres de configuration différents des valeurs par défaut prédéfinies.

Les substitutions peuvent être créées et appliquées à un seul serveur (elles sont alors appelées *substitutions de serveur*), ou elles peuvent être appliquées à un groupe de serveurs (elles sont alors appelées *substitutions globales* ). Les données de configuration des substitutions de serveur sont stockées dans le Registre de Windows sur le serveur sur lequel la substitution est appliquée. Les données de configuration des substitutions globales sont stockées dans Active Directory.

Les substitutions peuvent être configurées pour durer indéfiniment, ou elles peuvent être configurées pour une durée déterminée. En outre, les substitutions globales peuvent être configurées pour s'appliquer à tous les serveurs, ou seulement aux serveurs exécutant une version spécifique de Exchange.

Lorsque vous configurez une substitution, elle ne prend pas effet immédiatement. Le service du gestionnaire d’intégrité Microsoft Exchange vérifie que les données de configuration sont mises à jour toutes les 10 minutes. En outre, les substitutions globales dépendent de la latence de réplication Active Directory.

Pour obtenir la procédure détaillée d’affichage et de configuration des substitutions de serveur ou globales, voir [Configurer des substitutions de disponibilité gérée](configure-managed-availability-overrides-exchange-2013-help.md).

## Cmdlets et tâches de gestion

Il existe trois tâches opérationnelles principales que les administrateurs effectueront généralement pour la disponibilité gérée :

  - Extraction ou affichage de l’intégrité du système

  - Affichage des indicateurs d’intégrité et des détails des sondes, moniteurs et répondeurs

  - Gestion des substitutions

Les deux principaux outils de gestion pour la disponibilité gérée sont le journal des événements Windows et le Shell. La disponibilité gérée consigne une grande quantité d’informations dans les journaux des événements du canal Crimson Exchange ActiveMonitoring et ManagedAvailability, tels que :

  - Définitions des sondes, moniteurs et répondeurs, qui sont consignées dans les journaux d’événements \*Définition respectifs.

  - Résultats de sondes, moniteurs et répondeurs, qui sont consignés dans les journaux d’événements \*Résultats respectifs.

  - Les détails sur les actions de récupération de répondeur, y compris lorsque l’action de récupération est lancée, et qu’elle est considérée comme terminée (réussie ou non), qui sont consignés dans le journal des événements RecoveryActionResults.

Il existe 12 cmdlets utilisées pour la disponibilité gérée, qui sont décrites dans le tableau suivant.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Cmdlet</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://technet.microsoft.com/fr-fr/library/jj218703(v=exchg.150)">Get-ServerHealth</a></p></td>
<td><p>Permet d’obtenir des informations brutes sur l’intégrité du serveur, comme les indicateurs d’intégrité et leur état actuel (intègre ou non), les moniteurs d’indicateurs d’intégrité, les composants de serveur, les ressources cibles pour les sondes, les horodatages liés à l’heure de démarrage ou d’arrêt des sondes et ou des moniteurs, et les durées des transitions d’état.</p></td>
</tr>
<tr class="even">
<td><p><a href="https://technet.microsoft.com/fr-fr/library/jj218724(v=exchg.150)">Get-HealthReport</a></p></td>
<td><p>Permet d’obtenir une vue récapitulative de l’intégrité comprenant les indicateurs d’intégrité et leur état actuel.</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://technet.microsoft.com/fr-fr/library/jj218668(v=exchg.150)">Get-MonitoringItemIdentity</a></p></td>
<td><p>Permet d’afficher les sondes, les moniteurs et les répondeurs associés à un indicateur d’intégrité spécifique.</p></td>
</tr>
<tr class="even">
<td><p><a href="https://technet.microsoft.com/fr-fr/library/jj218642(v=exchg.150)">Get-MonitoringItemHelp</a></p></td>
<td><p>Permet d’afficher les descriptions de certaines des propriétés de sondes, de moniteurs et de répondeurs.</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://technet.microsoft.com/fr-fr/library/jj218628(v=exchg.150)">Add-ServerMonitoringOverride</a></p></td>
<td><p>Permet de créer une substitution locale propre au serveur d’une sonde, d’un moniteur ou d’un répondeur.</p></td>
</tr>
<tr class="even">
<td><p><a href="https://technet.microsoft.com/fr-fr/library/jj218664(v=exchg.150)">Get-ServerMonitoringOverride</a></p></td>
<td><p>Permet d’afficher la liste des substitutions locales sur le serveur spécifié.</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://technet.microsoft.com/fr-fr/library/dn482411(v=exchg.150)">Remove-ServerMonitoringOverride</a></p></td>
<td><p>Permet de supprimer une substitution locale d’un serveur spécifique.</p></td>
</tr>
<tr class="even">
<td><p><a href="https://technet.microsoft.com/fr-fr/library/jj218683(v=exchg.150)">Add-GlobalMonitoringOverride</a></p></td>
<td><p>Permet de créer une substitution globale pour un groupe de serveurs.</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://technet.microsoft.com/fr-fr/library/jj218627(v=exchg.150)">Get-GlobalMonitoringOverride</a></p></td>
<td><p>Permet d’afficher la liste des substitutions globales configurées dans l’organisation.</p></td>
</tr>
<tr class="even">
<td><p><a href="https://technet.microsoft.com/fr-fr/library/jj218675(v=exchg.150)">Remove-GlobalMonitoringOverride</a></p></td>
<td><p>Permet de supprimer une substitution globale.</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://technet.microsoft.com/fr-fr/library/jj218699(v=exchg.150)">Set-ServerComponentState</a></p></td>
<td><p>Permet de configurer l’état d’un ou plusieurs composants de serveur.</p></td>
</tr>
<tr class="even">
<td><p><a href="https://technet.microsoft.com/fr-fr/library/jj218713(v=exchg.150)">Get-ServerComponentState</a></p></td>
<td><p>Permet d’afficher l’état d’un ou plusieurs composants de serveur.</p></td>
</tr>
</tbody>
</table>

