---
title: 'FAQ : Centre d’administration Exchange: Exchange 2013 Help'
TOCTitle: 'FAQ : Centre d’administration Exchange'
ms:assetid: 3de0042f-74a6-458f-947c-3cd6eeacd6ab
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ552409(v=EXCHG.150)
ms:contentKeyID: 50477979
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# FAQ : Centre d’administration Exchange

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2015-03-09_

Cette rubrique fournit une liste de questions fréquentes pour le nouveau Centre d'administration Exchange (CAE) dans Microsoft Exchange Server 2013. Vous avez d'autres questions sur le CAE pour lesquelles vous n'avez pas trouvé de réponse ici ? Envoyez-nous un courrier électronique à l'adresse [Ex2013HelpFeedback@microsoft.com](mailto:ex2013helpfeedback@microsoft.com).

## Le CAE a-t-il été développé uniquement pour Exchange Online ?

Le CAE propose toutes les options de déploiement pour Exchange 2013. Il peut servir notamment aux clients qui souhaitent déployer localement, dans le nuage avec Exchange Online ou qui choisissent un déploiement hybride.

## Avez-vous supprimé la Console de gestion Exchange (EMC), car vous concevez l’interface principalement pour les petites et moyennes entreprises ?

Le CAE a été développé pour offrir une expérience de gestion unique et intuitive à tous nos clients. Il a été conçu pour simplifier l'exécution des tâches d'administration les plus courantes.

Nous avons créé une interface unique qui fournit un sur-ensemble de couverture des scénarios de la Console de gestion Exchange (EMC) et du Panneau de configuration Exchange (ECP). Elle doit relever les principaux défis et s'adapter aux différents scénarios des clients.

En outre, nous avons écouté les clients de toutes les tailles et leurs principales préoccupations étaient les suivantes :

  - Tenir à jour et télécharger des correctifs afin d'exploiter un outil administratif entraînent des coûts fixes d'exploitation supplémentaires, ce qui augmente les coûts de fonctionnement.

  - Le personnel informatique étant de plus en plus mobile, les clients voulaient être en mesure de gérer leurs environnements de n'importe où, et pas seulement à partir des ordinateurs de bureau et des serveurs sur lesquels leurs outils d'administration sont installés.

  - L'utilisation de plusieurs outils pour différentes options de déploiement augmente la confusion et les coûts d'exploitation et de formation.

## L'exposition de cmdlet et la journalisation de PowerShell sont-ils de retour dans le CAE ?

Nous avons pris en considération les demandes des clients à ce sujet et nous évaluons la possibilité d'y répondre dans une phase ultérieure à la version finale.

## L'EMC sera-t-elle réintroduite dans un futur pack de service ?

Non. Nous concentrons nos efforts sur l'expérience du CAE.

## Est-il possible d'utiliser l'EMC d'Exchange 2010 pour gérer des objets Exchange 2013 ?

Non. Vous ne pouvez pas utiliser la Console de gestion Exchange 2010 pour gérer des objets et des serveurs Exchange 2013. Quand les clients se mettent à niveau vers Exchange 2013, nous les encourageons à utiliser le CAE pour :

1.  gérer les boîtes aux lettres, les serveurs et les services correspondants d'Exchange 2013 ;

2.  afficher et mettre à jour les propriétés et les boîtes aux lettres Exchange 2010 ;

3.  afficher et mettre à jour les propriétés et les boîtes aux lettres Exchange 2007.

Nous recommandons aux clients d’utiliser la console de gestion Exchange 2010 pour créer et gérer des boîtes aux lettres Exchange 2010.

Nous recommandons aux clients d’utiliser la console de gestion Exchange 2007 pour créer et gérer des boîtes aux lettres Exchange 2007.

Les clients peuvent continuer à effectuer des tâches de gestion à l'aide de l'environnement de ligne de commande Exchange Management Shell et des tâches de script.

## Pourquoi la zone de recherche n’est-elle pas toujours visible ?

Dans le cadre de nos principes de conception pour Exchange 2013, nous voulions garantir l'absence de tout élément indésirable à l'écran. Cette simplicité est représentée dans l'ensemble de nos expériences d'utilisateur final, y compris dans le CAE. La zone de recherche glisse hors de l'écran quand vous cliquez sur l'icône. L'utilisateur dispose ainsi de plus d'espace pour taper sa requête dans la zone de texte, et peut faire son choix parmi les propositions qui s'affichent quand une correspondance est trouvée en temps réel. Cette amélioration nous permet de masquer toute complexité inutile sans pour autant compromettre l'expérience de gestion. Nous continuerons à améliorer toutes nos expériences en fonction de vos commentaires.

## Le CAE fonctionnera-t-il sur les tablettes ?

L’administration sur les tablettes et les appareils mobiles n’est pas prise en charge à l’heure actuelle.

## Pourquoi l'ECP d'Exchange 2010 s'ouvre lorsque j'essaie d'accéder au CAE d'Exchange 2013 ?

Si votre boîte aux lettres se trouve sur un serveur de boîtes aux lettres Exchange 2010, l'ECP d'Exchange 2010 se chargera automatiquement dans votre navigateur. Il s'agit du comportement par défaut. Vous pouvez accéder au CAE en ajoutant la version d'Exchange dans l'URL. Par exemple, pour accéder au CAE dont le répertoire virtuel est hébergé sur le serveur d'accès au client CAS01-NA, utilisez l'URL suivante : `https://CAS01-NA/ecp?ExchClientVer=15`.

## Comment limitez-vous là où le CAE peut être utilisé ?

Pour limiter l'accès Internet par rapport à l'accès Intranet, Exchange assure la partition au niveau du répertoire virtuel dans IIS. Les administrateurs peuvent explicitement autoriser ou refuser que des scénarios de gestion informatique soient effectués par des clients Internet externes, par exemple, à partir de clients qui n'ont pas rejoint un domaine dans le pare-feu de l'entreprise. Pour plus d'informations, consultez la rubrique [Désactivation de l’accès au Centre d’administration Exchange](turn-off-access-to-the-exchange-admin-center-exchange-2013-help.md).

## Qu’est-ce qui a changé pour la boîte à outils d’Exchange 2013 ?

Dans Exchange 2007 et Exchange 2010, l'EMC contenait la boîte à outils, qui vous permettait d'accéder à divers outils de gestion de votre organisation Exchange. La boîte à outils d'Exchange 2013 est considérablement réduite par rapport aux versions précédentes. L'Éditeur de modèles de détails, l'Analyseur de connectivité à distance et l'Afficheur des files d'attente sont toujours disponibles dans la boîte à outils d'Exchange 2013. Les autres outils ont été adaptés ou déplacés dans le CAE.

Le tableau suivant répertorie les modifications apportées à la boîte à outils d'Exchange 2013 :


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Outil</th>
<th>Où est-il maintenant ?</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Exchange Best Practices Analyzer (ExBPA)</p></td>
<td><p>Cet outil n'existe plus. Les vérifications de la disponibilité, qui remplacent l'outil ExBPA, permettent de s'assurer que votre forêt Active Directory et vos serveurs Exchange sont prêts pour Exchange 2013. Chaque rubrique de vérification de la disponibilité décrit les actions que vous pouvez effectuer pour résoudre les problèmes que l'on retrouve lors de ces vérifications. Nous vous recommandons de n'exécuter que les étapes décrites dans une rubrique de vérification de la disponibilité si cette vérification de la disponibilité s'est affichée lors de l'installation.</p></td>
</tr>
<tr class="even">
<td><p>Utilitaire de dépannage du flux de messagerie</p></td>
<td><p>L'utilitaire de dépannage du flux de messagerie a été retiré. Vous pouvez maintenant utiliser la fonctionnalité de suivi de la messagerie dans le CAE. Accédez à <strong>Flux de messagerie</strong> &gt; <strong>Rapports de remise</strong>.</p></td>
</tr>
<tr class="odd">
<td><p>Analyseur de performances</p></td>
<td><p>L'Analyseur de performances a été retiré de la boîte à outils. Vous pouvez toujours trouver l'Analyseur de performances sous <strong>Outils d'administration</strong> dans Windows Server 2008 et Windows Server 2012.</p></td>
</tr>
<tr class="even">
<td><p>Résolution des problèmes de performances</p></td>
<td><p>L'utilitaire de résolution des problèmes de performances a été retiré de la boîte à outils.</p></td>
</tr>
<tr class="odd">
<td><p>Visionneuse du journal de routage</p></td>
<td><p>La Visionneuse du journal de routage a été retirée.</p></td>
</tr>
<tr class="even">
<td><p>Console de gestion des dossiers publics</p></td>
<td><p>Les dossiers publics peuvent désormais être gérés à partir du CAE. Dans le CAE, accédez à <strong>Dossiers publics</strong>.</p></td>
</tr>
<tr class="odd">
<td><p>Éditeur des utilisateurs RBAC (contrôle d'accès basé sur un rôle)</p></td>
<td><p>Le contrôle d'accès basé sur un rôle est désormais géré à partir du CAE. Dans le CAE, accédez à <strong>Autorisations</strong>.</p></td>
</tr>
</tbody>
</table>

