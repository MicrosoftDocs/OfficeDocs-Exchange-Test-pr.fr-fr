---
title: 'État et performances du serveur: Exchange 2013 Help'
TOCTitle: État et performances du serveur
ms:assetid: 9d1fdec8-8273-4c71-88f1-b4edfd542c4f
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ150551(v=EXCHG.150)
ms:contentKeyID: 50478881
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# État et performances du serveur

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2015-03-09_

Comprendre l'intégrité et les performances du serveur est primordial pour concevoir et gérer une infrastructure de messagerie hautement performante. Microsoft Exchange Server 2013 apporte des améliorations à l'intégrité et aux performances du serveur.

Vous cherchez une liste de tous les sujets liés à l'intégrité et aux performances du serveur ? Voir Documentation sur l'intégrité et les performances du serveur.

## Gestion de la disponibilité

Exchange 2013 introduit le concept de *disponibilité gérée*. La disponibilité gérée s'exécute sur chaque serveur Exchange 2013. Elle est composée de deux processus, le service de gestionnaire de contrôle d'intégrité Exchange (MSExchangeHMHost.exe) et le processus de travail du gestionnaire de contrôle d'intégrité Exchange (MSExchangeHMWorker.exe), ainsi que des composants asynchrones suivants :

  - **Moteur de sonde**   Le *moteur de sonde* prend des mesures sur le serveur.

  - **Moteur de sonde de surveillance**   Le *moteur de sonde de surveillance* stocke la logique métier relative aux éléments constituant un état sain. Il fonctionne comme un moteur de reconnaissance de modèles, en recherchant des modèles et des mesures qui diffèrent d'un état sain, puis en évaluant si une fonctionnalité ou un composant est défectueux.

  - **Moteur répondeur**   Lorsque le *moteur répondeur* est alerté de l'existence d'un composant défectueux, sa première action consiste à essayer de le rétablir. La disponibilité gérée permet de procéder à des actions de rétablissement en plusieurs étapes. La première tentative peut consister à redémarrer le pool d'applications, la deuxième à redémarrer le service correspondant et la troisième à redémarrer le serveur. Enfin, la dernière tentative peut consister à placer le serveur hors connexion afin qu'il n'accepte plus de trafic. Si toutes ces actions échouent, une alerte est envoyée au support technique.

Pour plus d’informations sur la disponibilité gérée, voir [Disponibilité gérée](managed-availability-exchange-2013-help.md).

## Gestion des charges de travail

La gestion des charges de travail Exchange 2013 comprend les éléments suivants :

  - *Gestion des charges de travail utilisateur*, nouveau nom pour les fonctionnalités de limitation utilisateur d'Exchange Server 2010. Vous pouvez personnaliser ces paramètres en fonction des besoins de votre environnement.

  - La fonctionnalité de *gestion de la charge de travail du système* est une nouveauté d’Exchange 2013. Elle permet de limiter automatiquement des charges de travail Exchange spécifiques en surveillant l’état des ressources clés du serveur. Ces paramètres ne doivent être personnalisés que sous la direction du Support technique et Service clientèle Microsoft.

Pour plus d'informations, consultez la rubrique [Gestion de la charge de travail Exchange](exchange-workload-management-exchange-2013-help.md).

## Documentation sur l'intégrité et les performances du serveur

Le tableau suivant contient des liens vers des rubriques qui vous aideront à mieux comprendre et à gérer l'intégrité et les performances du serveur dans Exchange 2013.


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
<td><p><a href="exchange-workload-management-exchange-2013-help.md">Gestion de la charge de travail Exchange</a></p></td>
<td><p>Découvrez la gestion des charges de travail Exchange en contrôlant la manière dont les ressources sont consommées par des utilisateurs individuels.</p></td>
</tr>
<tr class="even">
<td><p><a href="managed-availability-exchange-2013-help.md">Disponibilité gérée</a></p></td>
<td><p>Découvrez les actions de surveillance et de récupération de ressources intégrées disponibles dans Exchange 2013.</p></td>
</tr>
</tbody>
</table>

