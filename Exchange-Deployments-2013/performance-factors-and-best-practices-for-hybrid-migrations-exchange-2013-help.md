---
title: 'Facteurs de performances et meilleures pratiques pour les migrations hybrides: Exchange 2013 Help'
TOCTitle: Facteurs de performances et meilleures pratiques pour les migrations hybrides
ms:assetid: 120a7832-d2d3-47d7-b305-918360c2ef66
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Mt483789(v=EXCHG.150)
ms:contentKeyID: 70117979
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Facteurs de performances et meilleures pratiques pour les migrations hybrides

 

_<strong>Sapplique à :</strong>Exchange Server 2016_

_<strong>Dernière rubrique modifiée :</strong>2016-12-09_

Il existe de nombreux chemins pour migrer des données à partir d’une organisation de messagerie sur site vers Office 365. Lorsque vous planifiez une migration vers Office 365, une des questions courantes concerne la façon d’améliorer les performances de migration des données et la rapidité de migration. Cet article traite des performances de migration pour les déploiements hybrides Exchange. Pour obtenir des informations sur les autres méthodes de migration, voir [Performances de la migration Office 365 et des pratiques recommandées](http://go.microsoft.com/fwlink/p/?linkid=623651).

## Facteurs de performances et meilleures pratiques pour les migrations hybrides

La migration du déploiement hybride prend en charge la migration en douceur entre des serveurs Exchange locaux et Exchange Online dans Office 365.

La migration du déploiement hybride est de loin la méthode de migration la plus rapide pour la migration de données de boîtes aux lettres vers Office 365. Nous avons constaté un débit allant jusqu’à 100 Go/heure pendant les déploiements clients réels. Le tableau suivant fournit la liste des facteurs qui s’appliquent aux scénarios de migration hybride Office 365 natifs.

Si votre environnement local contient plusieurs sites se trouvant dans différents emplacements géographiques, vous pouvez améliorer les performances de migration en créant des points de terminaison de migration physiquement proches. En effet, dans un tel scénario, le processus de migration utilise le réseau Microsoft plutôt qu’un point de terminaison de migration centralisé qui a recours à votre réseau local.

## Facteur 1 : Source de données (Exchange Server)


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Liste de vérification</th>
<th>Description</th>
<th>Meilleures pratiques</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Performances du système</p></td>
<td><p>L’extraction des données est une tâche intensive. Le système source doit disposer de ressources suffisantes (temps processeur et mémoire) afin de fournir de meilleures performances de migration. Au moment de la migration, le système source approche généralement sa pleine capacité pour une charge de travail d’utilisateurs finaux ordinaire ; une charge de travail de migration supplémentaire réduit même parfois l’accès des utilisateurs finaux en raison d’une insuffisance de ressources système.</p></td>
<td><p>Surveillez les performances système lors du test de migration pilote. Si le système est occupé, nous déconseillons l’utilisation d’une planification de migration agressive pour le système en question, car elle pourrait entraîner des problèmes de disponibilité du service et de lenteur de migration. Dans la mesure du possible, améliorez les performances du système source en ajoutant des ressources matérielles et en réduisant la charge sur le système en déplaçant des tâches et des utilisateurs vers d’autres serveurs qui ne sont pas concernés par la migration.</p>
<p>Pour plus d’informations, consultez les rubriques suivantes :</p>
<ul>
<li><p><a href="http://go.microsoft.com/fwlink/p/?linkid=723566">Demandez à l’expert de performances : Redimensionnement des déploiements Exchange 2016</a></p></li>
<li><p><a href="https://technet.microsoft.com/fr-fr/library/jj150551(v=exchg.150)">État et performances du serveur</a></p></li>
<li><p><a href="http://technet.microsoft.com/fr-fr/library/dd351192.aspx">Présentation des performances d’Exchange 2010</a>.</p></li>
</ul>
<p>Lors de la migration à partir d’une organisation Exchange sur site comportant plusieurs serveurs de boîtes aux lettres et plusieurs bases de données, nous vous conseillons de créer une liste d’utilisateurs de migration distribuée de manière égale parmi les différents serveurs de boîtes aux lettres et bases de données. En fonction des performances de chaque serveur, cette liste peut être affinée en vue d’optimiser le débit.</p>
<p>Par exemple, si le serveur A présente une disponibilité des ressources supérieure de 50 pour cent à celle du serveur B, il est raisonnable de compter 50 pour cent d’utilisateurs du serveur A en plus dans le même lot de migration. Des pratiques similaires peuvent être appliquées à d’autres systèmes sources.</p>
<p>Effectuez les migrations lorsque les serveurs disposent d’une disponibilité des ressources maximale, par exemple en dehors des heures de travail ou lors des week-ends ou jours fériés.</p></td>
</tr>
<tr class="even">
<td><p>Tâches principales</p></td>
<td><p>D’autres tâches principales s’exécutent au moment de la migration. Étant donné qu’il est préférable d’effectuer la migration en dehors des heures de travail, les migrations peuvent entrer en conflit avec d’autres tâches de maintenance exécutées sur vos serveurs locaux, telles que les sauvegardes de données.</p></td>
<td><p>Examinez les autres tâches système susceptibles de s’exécuter durant la migration. Nous vous recommandons d’effectuer la migration des données lorsqu’aucune autre tâche nécessitant de nombreuses ressources ne s’exécute.</p>
<p><strong>Remarque</strong>   Pour les clients qui utilisent Microsoft Exchange localement, les tâches principales courantes sont les solutions de sauvegarde et la <a href="http://technet.microsoft.com/fr-fr/library/aa996226(exchg.65).aspx">Maintenance de la banque d’informations Exchange</a>.</p></td>
</tr>
</tbody>
</table>


## Facteur 2 : le serveur de migration

La migration du déploiement hybride est une migration par extraction et envoi de données initiée par le cloud, et un serveur hybride Exchange agit comme serveur de migration. Cet aspect ne reçoit généralement pas l’attention qu’il mérite, et les clients utilisent un ordinateur virtuel peu puissant comme serveur hybride. Cela entraîne des performances de migration médiocres.

**Meilleure pratique**

En plus de l’application des meilleures pratiques décrites précédemment, nous avons testé les meilleures pratiques suivantes, lesquelles ont permis d’améliorer les performances de migration lors de migrations réelles chez des clients :

  - Utilisez de puissants ordinateurs physiques de classe serveur au lieu d’ordinateurs virtuels pour les serveurs hybrides Exchange.

  - Utilisez plusieurs serveurs hybrides placés derrière le mécanisme d’équilibrage de la charge réseau du client.

Par exemple, lors de migrations réelles chez des clients, nous avons obtenu un débit régulier de 30 Go/heure avec la configuration suivante :

  - **Réseau **  Canal sortant 500 Mo vers Internet ; réseau interne sur 1 Go avec dorsale principale fibre de 10 Go.

  - **Matériel**   Caractéristiques des deux serveurs (physiques) Accès au client/Concentrateur:
    
      - UC: Processeur Intel® Xeon® E5520 @ 2,27 GHz 2,26 GHz (deux processeurs).
    
      - RAM: 24 Go.
    
      - Disques : huit, 146 Go par disque. Configuration RAID 5 = 960 Go d’espace total brut.

  - **MRSProxy**   Configuré avec une simultanéité de 100.

## Facteur 3 : le moteur de migration

La migration du déploiement hybride utilise les outils Office 365 natifs. Elle est soumise à la limitation de service de migration Office 365.

**Exchange 2003 et versions ultérieures d’Exchange**

Il existe une différence clé dans l’expérience de l’utilisateur final lors de la migration à partir d’Exchange 2003. À la différence des dernières versions d’Exchange, les utilisateurs finals d’Exchange 2003 ne sont pas en mesure d’accéder à leurs boîtes aux lettres lors de la migration de leurs données. Par conséquent, les clients d’Exchange 2003 se soucient généralement davantage du moment où les migrations sont planifiées et de la durée nécessaire aux migrations, en particulier quand les performances de migration sont faibles en raison de la lenteur du réseau ou de la taille importante des boîtes aux lettres.

La migration d’Exchange 2003 est également très sensible aux interruptions. Par exemple, dans une migration de client réelle, durant la migration d’une boîte aux lettres de 10 Go, un incident de service s’est produit à mi-parcours de la migration. Le serveur d’accès au client Office 365, qui traitait la migration des données, a dû être redémarré pour résoudre le problème. La migration de la boîte aux lettres a donc dû être redémarrée et il a fallu recommencer la migration des 10 Go de données. La migration n’a pas pu être reprise à partir du point où elle avait été interrompue. Exchange 2010 et les versions ultérieures d’Exchange, toutefois, peuvent reprendre les migrations après des interruptions.

**Meilleure pratique**

Certains clients choisissent d’effectuer des migrations à deux sauts pour les boîtes aux lettres Exchange 2003 sensibles et de taille importante :

  - **Premier saut**   Migrez les boîtes aux lettres d’Exchange 2003 vers un serveur Exchange 2010 ou version ultérieure, qui est généralement le serveur hybride. Le premier saut est un déplacement hors connexion, mais il s’agit en général d’une migration très rapide sur un réseau local.

  - **Second saut**   Migrez les boîtes aux lettres d’Exchange 2010 ou de version ultérieure vers Office 365.

Le second saut est un déplacement en ligne, ce qui procure une meilleure expérience utilisateur et davantage de tolérance de panne. Cette approche en deux sauts requiert une licence Exchange pour la boîte aux lettres utilisateur sur site temporaire.

**Proxy du service de réplication de boîtes aux lettres (MRSProxy)**

Le proxy MRS est la fonctionnalité de migration sur site qui fonctionne avec le service de réplication de boîtes aux lettres exécuté côté Office 365. Pour plus d’informations, consultez la rubrique [Présentation des demandes de déplacement](http://technet.microsoft.com/fr-fr/library/dd298174.aspx).

**Meilleure pratique**

Il est possible de configurer la quantité maximale de connexions MRSProxy pour le serveur hybride Exchange local. Exécutez la commande Windows PowerShell suivante.

    Set-WebServicesVirtualDirectory -Identity "EWS (Default Web Site)" -MRSMaxConnections <number between 0 and unlimited; default is 100>

<table>
<thead>
<tr class="header">
<th><img src="images/Dn986544.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Pour la plupart des migrations de clients, il est inutile de modifier la valeur de MRSMaxConnections par défaut. Si vous devez protéger le serveur source contre la surcharge de migration, vous pouvez réduire le nombre de connexions. Ce paramètre s’applique pour chaque serveur MRSProxy. Si un client a deux serveurs MRSProxy, chacun défini pour 10 connexions, il obtiendra 20 (2x10) comme quantité totale de connexions de MRSProxy. Pour plus d’informations sur la configuration du service MRSProxy dans votre organisation Exchange 2010 sur site, consultez la rubrique <a href="http://technet.microsoft.com/fr-fr/library/ee732395.aspx">Démarrer le service MRSProxy sur un serveur d’accès client distant</a>.</td>
</tr>
</tbody>
</table>


## Facteur 4 : le réseau

**Tests de vérification**

Pour les clients exécutant Exchange 2010 ou une version ultérieure, les tests de performances réseau pour les migrations hybrides peuvent être réalisés en effectuant plusieurs migrations de boîtes aux lettres tests. En guise d’alternative, vous pouvez migrer des boîtes aux lettres utilisateur réelles avec l’option -SuspendWhenReadyToComplete pour obtenir une indication des performances de migration. Une fois les tests terminés, supprimez la demande de déplacement afin d’éviter toute incidence sur les utilisateurs finals.

Pour plus d’informations sur les demandes de déplacement, consultez la rubrique [New-MoveRequest](https://technet.microsoft.com/fr-fr/library/dd351123\(v=exchg.150\)).

## Facteur 5 : le service Office 365

La limitation basée sur l’intégrité des ressources Office 365 concerne les migrations qui utilisent les migrations du déploiement hybride Office 365. Pour plus d’informations, consultez la section ci-dessus relative à la limitation basée sur l’intégrité des ressources Office 365.

