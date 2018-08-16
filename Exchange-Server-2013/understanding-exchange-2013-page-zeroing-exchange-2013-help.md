---
title: 'Fonction de mise à zéro des pages d’Exchange 2013: Exchange 2013 Help'
TOCTitle: Présentation de la fonctionnalité de mise à zéro des pages d’Exchange 2013
ms:assetid: 0ca7b188-efbc-4c0d-bcfe-5138cffc803c
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Gg549096(v=EXCHG.150)
ms:contentKeyID: 61627796
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Présentation de la fonctionnalité de mise à zéro des pages d’Exchange 2013

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2016-12-09_

## Mise à zéro des pages dans Exchange 2013

La *mise à zéro* est un mécanisme de sécurité qui écrit des zéros ou un modèle binaire sur des données supprimées, afin que les données supprimées soient plus difficiles à récupérer. Dans Exchange Server 2013, une base de données ESE utilise les *pages* en tant qu’unité de stockage, et par conséquent, elle implémente la *mise à zéro des pages*. La mise à zéro des pages est activée par défaut et ne peut pas être désactivée. Les opérations de mise à zéro des pages sont enregistrées dans les fichiers du journal des transactions afin que la mise à zéro des pages soit appliquée de manière uniforme à l’ensemble des copies d’une base de données. La mise à zéro d’une page sur une base de données active entraîne la mise à zéro de la page sur une copie passive de la base de données.

> [!NOTE]
> Le moteur ESE (Extensible Storage Engine) ne dispose d’aucun mécanisme pour donner la priorité à la réutilisation des pages mises à zéro sur l’allocation d’un nouvel espace. Les tables pour lesquelles l’allocation de l’espace s’effectue de manière séquentielle ignoreront involontairement les pages fragmentées ou mises à zéro en faveur de pages séquentielles nouvelles ou libres. Cette approche réduit le nombre d’opérations d’entrée/sortie par seconde (IOPS) de la base de données.


Dans Exchange 2013, les fonctions de mise à zéro réduisent l’impact sur les performances des serveurs, notamment :

  - **Optimisation du stockage et de la capacité réseau**   ESE écrit un enregistrement de mise à zéro des pages dans le fichier journal des transactions au lieu de consigner l’image de page complète. Cette approche réduit les E/S d’écriture de journal et réduit les besoins en bande passante pour l’envoi des fichiers journaux.

  - **Optimisation des E/S du disque de base de données**   Dans Exchange 2010 RTM et les versions antérieures, la mise à zéro des pages avait lieu uniquement pendant une sauvegarde ou une maintenance planifiée, ce qui provoquait une augmentation du nombre d’E/S sur le disque de base de données. Dans Exchange 2010 SP1 les versions ultérieures (notamment Exchange 2013), la mise à zéro des pages est exécutée par défaut et au moment de la transaction. Dans la majorité des cas, la mise à zéro se produit immédiatement après la suppression définitive. Cette conception permet à la base de données de tirer parti de la fonction de profondeur du point de contrôle du moteur. Ainsi, les pages de modifications restent dans le cache de base de données pour un laps de temps donné, afin d’éviter que les mises à jour de pages supplémentaires qui se produisent juste après causent des E/S d’écriture de base de données supplémentaires. Grâce à cette conception, la mise à zéro des pages n’a pas d’impact significatif sur les E/S de base de données, c’est pourquoi elle est activée par défaut.

## Mise en œuvre de la mise à zéro des pages dans la base de données ESE

La mise à zéro des pages écrit un modèle binaire sur un enregistrement supprimé de manière définitive. Le modèle de mise à zéro des pages est propre aux opérations du moteur ESE et diffère selon que des opérations d’exécution ou de maintenance sont réalisées. Le tableau suivant répertorie les schémas de remplissage qui correspondent à des opérations d’exécution particulières.

### Modèle de remplissage de la mise à zéro des pages lors de l’exécution ESE

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Opération d’exécution d’ESE</th>
<th>Modèle de remplissage</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Remplacement</p></td>
<td><p>R</p></td>
</tr>
<tr class="even">
<td><p>Suppression d’enregistrement/de valeur longue</p></td>
<td><p>D</p></td>
</tr>
<tr class="odd">
<td><p>Espace de page libéré</p></td>
<td><p>H</p></td>
</tr>
</tbody>
</table>


Le tableau suivant répertorie les schémas de remplissage correspondant à des opérations spécifiques effectuées pendant une opération de maintenance de base de données ESE en arrière-plan.

### Modèle de remplissage de la mise à zéro des pages lors de la maintenance de base de données ESE en arrière-plan

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Opération de maintenance de base de données ESE en arrière-plan</th>
<th>Modèle de remplissage</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Suppression d’enregistrement</p></td>
<td><p>D</p></td>
</tr>
<tr class="even">
<td><p>Suppression de valeur longue</p></td>
<td><p>L</p></td>
</tr>
<tr class="odd">
<td><p>Espace libéré sur la page partiellement utilisée</p></td>
<td><p>Z</p></td>
</tr>
<tr class="even">
<td><p>Espace libéré sur la page inutilisée</p></td>
<td><p>U</p></td>
</tr>
</tbody>
</table>


## Maintenance de base de données en arrière-plan

La maintenance de base de données en arrière-plan est un processus qui effectue des sommes de contrôle et analyse chaque base de données en continu. Sa fonction principale est d’effectuer des sommes de contrôle sur les pages de bases de données, mais elle gère également le nettoyage de l’espace et la mise à zéro des enregistrements et des pages qui n’ont pas été mis à zéro en raison d’un blocage de banque. La maintenance de base de données en arrière-plan traite environ 1 Mo par seconde et par base de données. Si la mise à zéro rapide des pages est pour vous une priorité, vous pouvez réduire les tailles des bases de données afin d’assurer que la mise à zéro des pages ait lieu lors de récupérations sur incident effectuées sur un délai plus court (par exemple, 24 heures).

La maintenance de base de données en arrière-plan est un processus continu, de sorte qu’aucun événement n’est associé à son début ou sa fin. Vous pouvez suivre l’avancement de la maintenance de base de données en arrière-plan en consultant la valeur d’un compteur de performance :

  - Base de données MSExchange -\> Instances -\> Durée de maintenance de base de données

Ce compteur indique le nombre de secondes qui se sont écoulées depuis la dernière exécution de la maintenance pour une base de données précise.

## Processus de mise à zéro des pages de base de données ESE

Le tableau suivant décrit les scénarios de suppression de base de données et les circonstances dans lesquelles les fonctions de mise à zéro des pages sont exécutées.

### Maintenance de base de données ESE en arrière-plan

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Scénario de suppression de base de données</th>
<th>Processus et délai nécessaire à ESE pour mettre à zéro les données de la base de données</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><ul>
<li><p>Scénario 1 : la récupération d’élément unique est désactivée et l’utilisateur supprime l’élément du dossier Éléments récupérables.</p></li>
<li><p>Scénario 2 : la récupération d’élément unique est désactivée et la période de rétention des éléments récupérables est définie sur zéro.</p></li>
<li><p>Scénario 3 : la récupération d’élément unique est activée et l’élément expire en fonction de la période de rétention des éléments supprimés.</p></li>
</ul></td>
<td><p>Un thread asynchrone écrit un masque binaire sur les données supprimées. Cette action se produit dans les millisecondes suivant la suppression de l’enregistrement. Si le processus de banque se bloque alors que la tâche de mise à zéro asynchrone est toujours en attente (ou que le nettoyage de la banque des versions est annulé en raison de la croissance de la banque d’informations), la mise à zéro est terminée lorsque la maintenance de base de données en arrière-plan traite cette section de la base de données.</p></td>
</tr>
<tr class="even">
<td><p>Scénario d’affichage : expiration des éléments de l’affichage des dossiers Outlook/Outlook Web App (par exemple, affichage Conversation)</p></td>
<td><p>La mise à zéro des données a lieu lorsque la maintenance de base de données en arrière-plan traite cette section de la base de données.</p></td>
</tr>
<tr class="odd">
<td><p>Scénario de déplacement/suppression de la boîte aux lettres : boîte aux lettres source supprimée (expiration de la boîte aux lettres supprimée dans le conteneur de dépôt)</p></td>
<td><p>La mise à zéro des données a lieu lorsque la maintenance de base de données en arrière-plan traite cette section de la base de données.</p></td>
</tr>
</tbody>
</table>


## Analyse du comportement de mise à zéro des pages

Vous pouvez mesurer et surveiller la fonctionnalité de mise à zéro en affichant deux compteurs ESE :

  - Base de données MSExchange -\> Pages de maintenance de base de données mises à zéro : indique le nombre de pages mises à zéro par le moteur de base de données depuis l’appel du compteur de performance.

  - Base de données MSExchange -\> Pages de maintenance de base de données mises à zéro/s : Indique le taux auquel les pages sont mises à zéro.

> [!NOTE]
> Pour savoir comment activer ces compteurs, consultez la page <a href="https://go.microsoft.com/fwlink/?linkid=101194">Procédure d’activation des compteurs de performance ESE étendus</a>.


La mise à zéro des pages est une fonction de maintenance de base de données. Les informations relatives aux performances de mise à zéro des pages pour les opérations d’exécution et de maintenance de base de données en arrière-plan sont donc incluses dans ces compteurs.

## Types de données de boîte aux lettres sans mise à zéro des pages

Les types de données de boîte aux lettres suivants n’ont pas de mécanisme en place pour la mise à zéro des pages :

  - Journaux de transactions de la base de données de boîte aux lettres (.log)
    
    Lorsque les journaux de transactions sont supprimés (en raison de la troncation via la sauvegarde ou l’enregistrement circulaire), il n’existe aucun processus de mise à zéro des blocs dans le système de fichiers NTFS stockant le fichier journal supprimé. Il est probable que le système NTFS réutilise rapidement cet espace disponible pour les nouveaux journaux créés. Toutefois, rien ne le garantit.

  - Fichiers de catalogue d’indexation de contenu
    
    Exchange 2013 utilise Search Foundation pour la fonctionnalité d’indexation de recherche. Le catalogue d’indexation de recherche se compose de plusieurs douzaines de fichiers, stockés sur le même volume que le fichier de base de données de boîtes aux lettres. Lorsqu’un message est définitivement supprimé de la base de données de boîtes aux lettres, le contenu associé dans le catalogue de recherche n’est pas immédiatement supprimé. La suppression du contenu a lieu lorsque Search Foundation procède à une fusion virtuelle ou principale de nombreux petits fichiers de catalogue dans un fichier unique de plus grande taille. Une fois la fusion principale terminée, les fichiers de catalogue plus petits sont supprimés. Aucun processus de mise à zéro des blocs stockant les fichiers de catalogue supprimés.

