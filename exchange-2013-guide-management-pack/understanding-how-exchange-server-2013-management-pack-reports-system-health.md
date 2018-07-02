---
title: Présentation de la création de rapports sur l'intégrité du système par le pack d'administration Exchange Server 2013
TOCTitle: Présentation de la création de rapports sur l'intégrité du système par le pack d'administration Exchange Server 2013
ms:assetid: 6ca8847f-93fe-458d-bd43-7afad7fdd2f4
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dn195910(v=EXCHG.150)
ms:contentKeyID: 53275524
ms.date: 04/03/2015
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Présentation de la création de rapports sur l'intégrité du système par le pack d'administration Exchange Server 2013

 

_**Dernière rubrique modifiée :**  2015-03-09_

Cette rubrique fournit des informations sur la manière dont le pack d'administration Exchange Server 2013 analyse l'intégrité du système Exchange et génère des rapports à ce sujet. Dans le pack d'administration Exchange 2013, les informations relatives à l'état d'intégrité sont regroupées de façon simple. Chaque fois que les informations d'intégrité sont douteuses et que le répondeur d'escalade est déclenché, l'événement suivant est journalisé dans le journal des événements Windows :

## Disponibilité gérée

Plusieurs changements d'architecture ont été introduits dans Exchange Server 2013. L'un de ces changements clés est la fonctionnalité *Disponibilité gérée* où tous les composants Exchange 2013 disposent de moniteurs intégrés qui détectent les problèmes et tentent de récupérer la disponibilité du service. Le pack d'administration Exchange 2013 repose sur cette fonctionnalité. Tout problème ne pouvant pas être corrigé automatiquement est signalé au pack d'administration Exchange 2013 sous forme d'alerte. Chaque composant d'Exchange 2013 s'auto-analyse à l'aide de trois composants de base nommés sondes, moniteurs et répondeurs.

![Disponibilité gérée](images/Dn195910.dd5febae-d05e-4089-a3f5-1691b2d9a3d7(EXCHG.150).png "Disponibilité gérée")

  - **Probes**   Ensembles de collecteurs de données qui mesurent divers composants. Il existe trois types de sondes :
    
      - Les transactions synthétiques qui mesurent les opérations utilisateur synthétiques de bout en bout et les contrôles qui mesurent le trafic réel.
    
      - Les contrôles qui mesurent le trafic client réel.
    
      - Les notifications qui permettent à Exchange d'effectuer une action immédiate. Un bon exemple de cela est la notification déclenchée lors de l'expiration d'un certificat.

  - **Moniteurs**   Les données collectées par les sondes sont transmises aux moniteurs qui les analysent pour détecter des conditions spécifiques et, en fonction de ces dernières, déterminent si le composant en question est intègre ou non.

  - **Répondeurs**   Si un moniteur détermine qu'un composant n'est pas intègre, il déclenche un répondeur. Si le problème est récupérable, le répondeur tente de récupérer le composant à l'aide de la logique intégrée. Plusieurs répondeurs sont disponibles pour chaque composant, mais le répondeur pertinent pour le pack d’administration Exchange 2013 est le *répondeur d’escalade*. Lors de son déclenchement, le répondeur d'escalade génère un événement que le pack d'administration Exchange 2013 reconnaît, et fournit dans cette alerte les informations appropriées afin que les administrateurs disposent des données nécessaires pour corriger le problème.

Dans Exchange 2013, chaque composant utilise un ensemble spécifique de sondes, de moniteurs et de répondeurs pour s'auto-analyser. Ces collections de sondes et de moniteurs sont appelées *informations d'intégrité*. Par exemple, il existe un certain nombre de sondes qui recueillent des données sur divers aspects du service ActiveSync. Ces données sont traitées pas un ensemble désigné de moniteurs qui déclenchent les répondeurs appropriés pour corriger tout problème détecté dans le service ActiveSync. Collectivement, ces composants constituent les informations d'intégrité ActiveSync.

Dans Exchange les informations d'intégrité sont organisées en quatre catégories correspondant au tableau de bord du pack d'administration :

  - Points de contact du client

  - Composants du service

  - Ressources du serveur

  - Dépendances clés

Pour la liste complète des informations d'intégrité Exchange, consultez la rubrique [Appendix A: Exchange health sets](appendix-a-exchange-health-sets.md).

Pour plus d'informations sur la disponibilité gérée, consultez la rubrique [État et performances du serveur](https://technet.microsoft.com/fr-fr/library/jj150551\(v=exchg.150\)).

## Comment les informations sont regroupées

Cette rubrique fournit des informations sur la manière dont le pack d'administration Exchange Server 2013 analyse l'intégrité du système Exchange et génère des rapports à ce sujet. Dans le pack d'administration Exchange 2013, les informations relatives à l'état d'intégrité sont regroupées de façon simple. Chaque fois que les informations d'intégrité sont douteuses et que le répondeur d'escalade est déclenché, l'événement suivant est journalisé dans le journal des événements Windows :


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Nom du journal</p></td>
<td><p>Microsoft-Exchange-ManagedAvailability/Monitoring</p></td>
</tr>
<tr class="even">
<td><p>Source</p></td>
<td><p>Disponibilité gérée</p></td>
</tr>
<tr class="odd">
<td><p>Date</p></td>
<td><p>&lt;<em>date et heure de l'événement</em>&gt;</p></td>
</tr>
<tr class="even">
<td><p>ID d'évènement</p></td>
<td><p>4</p></td>
</tr>
<tr class="odd">
<td><p>Catégorie de la tâche</p></td>
<td><p>Analyse</p></td>
</tr>
<tr class="even">
<td><p>Niveau</p></td>
<td><p>Erreur</p></td>
</tr>
<tr class="odd">
<td><p>Mots clés</p></td>
<td><p>&lt;<em>aucune</em>&gt;</p></td>
</tr>
<tr class="even">
<td><p>Utilisateur</p></td>
<td><p>SYSTÈME</p></td>
</tr>
<tr class="odd">
<td><p>Ordinateur</p></td>
<td><p>&lt;<em>Nom de domaine complet (FQDN) du serveur Exchange</em>&gt;</p></td>
</tr>
<tr class="even">
<td><p>Description</p></td>
<td><p>&lt;<em>généré de façon dynamique par le répondeur d'escalade</em>&gt;</p></td>
</tr>
</tbody>
</table>


L'agent du pack d'administration détecte et traite cet événement. La Disponibilité gérée peut utiliser cet événement pour générer des alertes dans SCOM. Une fois le problème correspondant résolu et les informations d'intégrité rétablies dans un état intègre, l'événement suivant est consigné dans le journal des événements Windows :


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Nom du journal</p></td>
<td><p>Microsoft-Exchange-ManagedAvailability/Monitoring</p></td>
</tr>
<tr class="even">
<td><p>Source</p></td>
<td><p>Disponibilité gérée</p></td>
</tr>
<tr class="odd">
<td><p>Date</p></td>
<td><p>&lt;<em>date et heure de l'événement</em>&gt;</p></td>
</tr>
<tr class="even">
<td><p>ID d'évènement</p></td>
<td><p>1</p></td>
</tr>
<tr class="odd">
<td><p>Catégorie de la tâche</p></td>
<td><p>Analyse</p></td>
</tr>
<tr class="even">
<td><p>Niveau</p></td>
<td><p>Informations</p></td>
</tr>
<tr class="odd">
<td><p>Mots clés</p></td>
<td><p>&lt;<em>aucune</em>&gt;</p></td>
</tr>
<tr class="even">
<td><p>Utilisateur</p></td>
<td><p>SYSTÈME</p></td>
</tr>
<tr class="odd">
<td><p>Ordinateur</p></td>
<td><p>&lt;<em>Nom de domaine complet (FQDN) du serveur Exchange</em>&gt;</p></td>
</tr>
<tr class="even">
<td><p>Description</p></td>
<td><p>&lt;<em>généré de façon dynamique par le répondeur d'escalade</em>&gt;</p></td>
</tr>
</tbody>
</table>


Les packs d'administration qui analysaient les versions précédentes d'Exchange étaient complètement centralisés. Les agents de chaque serveur Exchange collectaient des données et un moteur de corrélation central comparait et évaluait toutes les données rapportées par les agents pour déterminer l'intégrité globale du service. Dans des environnements de grande taille, ce processus générait des corrélations complexes, entraînant des retards dans la génération d'alertes. Exchange 2013 n'utilise plus de corrélation d'alertes. Au lieu de cela, chaque serveur effectue sa propre analyse et alerte SCOM si nécessaire, ce qui rend l'architecture hautement évolutive.

En fonction de l'impact de l'événement et des informations d'intégrité qui le déclenchent, le problème apparaît sur la console SCOM dans une catégorie différente. Si l'événement a une incidence sur les utilisateurs, l'indicateur des points de contact du client apparaît comme non intègre. Si l'événement entraîne l'indisponibilité d'un composant entier tel OWA, l'indicateur de composant service apparaît comme non intègre. Si le problème est lié à un serveur particulier, l'indicateur d'intégrité du serveur correspondant apparaît comme non intègre. Enfin, si le problème a trait à une ressource dont Exchange dépend, l'indicateur des dépendances clés apparaît comme non intègre. Pour plus d'informations sur ces catégories, consultez la rubrique [Mise en route avec le pack d'administration Exchange Server 2013](getting-started-with-exchange-server-2013-management-pack.md).

