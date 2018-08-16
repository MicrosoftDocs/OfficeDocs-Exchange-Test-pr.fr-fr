---
title: 'Service de disponibilité dans Exchange 2013: Exchange 2013 Help'
TOCTitle: Service de disponibilité dans Exchange 2013
ms:assetid: 9722dea2-2bf8-437c-85c0-3ab65b8a07b9
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb232134(v=EXCHG.150)
ms:contentKeyID: 52063004
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Service de disponibilité dans Exchange 2013

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2016-12-09_

Le service de disponibilité Exchange 2013 fournit des informations de disponibilité aux clients Microsoft Outlook et Outlook Web App. Le service de disponibilité améliore l'expérience des professionnels de l'informatique en matière de planification des réunions et du calendrier en apportant des informations de disponibilité sécurisées, cohérentes et à jour.

Outlook et Outlook Web App utilisent le service de disponibilité pour exécuter les tâches suivantes :

  - Récupérer les informations de disponibilité actuelles pour les boîtes aux lettres Exchange 2013

  - Récupérer les informations de disponibilité actuelles d'autres organisations Exchange 2013

  - Récupérer les informations de disponibilité publiées à partir de dossiers publics pour les boîtes aux lettres situées sur des serveurs dotés de versions précédentes d'Exchange.

  - Afficher les horaires de travail des participants

  - Afficher les suggestions concernant l'heure de réunion

**Contenu de cette rubrique**

Présentation du service de disponibilité

Informations sur l'état Absent

API du service de disponibilité

Équilibrage de la charge réseau du service de disponibilité

Méthodes employées pour extraire les informations de disponibilité

## Présentation du service de disponibilité

Le service de disponibilité extrait les informations de disponibilité directement de la boîte aux lettres cible pour les utilisateurs d'Exchange 2013, Exchange 2010 ou Exchange 2007, et peut être configuré pour récupérer les informations de disponibilité pour les utilisateurs de versions antérieures d'Exchange. Pour les topologies comportant des boîtes aux lettres Exchange 2007, Exchange 2010 ou Exchange 2013 dans lesquelles tous les clients exécutent Outlook 2007 ou version ultérieure, le service de disponibilité permet de récupérer les informations de disponibilité.

Outlook utilise le service de découverte automatique Exchange pour obtenir l'URL du service de disponibilité. Pour plus d'informations sur le service de découverte automatique, consultez la rubrique [Service de découverte automatique](autodiscover-service-for-exchange-2013.md).

Vous pouvez utiliser l'environnement de ligne de commande Exchange Management Shell pour configurer le service de disponibilité. Vous ne pouvez pas le faire à l'aie du Centre d'administration Exchange (CAE).

## Informations sur l'état Absent

Par ailleurs, le service de disponibilité permet d'accéder aux réponses automatiques que les utilisateurs envoient lorsqu'ils s'absentent du bureau momentanément ou pendant une durée prolongée.

Les professionnels de l'informatique utilisent la fonctionnalité Réponse automatique (anciennement appelée Absent du bureau) d'Outlook et Outlook Web App pour informer d'autres utilisateurs qu'ils ne peuvent pas répondre aux messages électroniques. Cette dernière facilite la configuration et la gestion des réponses automatiques aussi bien pour les professionnels de l'informatique que pour les administrateurs.

## API du service de disponibilité

Le service de disponibilité fait partie intégrante de l'interface de programmation d'Exchange 2013. Il est disponible en tant que service web pour permettre aux développeurs d'élaborer des outils tiers à des fins d'intégration.

## Équilibrage de la charge réseau du service de disponibilité

L'utilisation de la fonctionnalité d'équilibrage de charge réseau sur les serveurs d'accès au client qui exécutent le service de disponibilité peut contribuer à l'amélioration des performances et de la fiabilité pour les utilisateurs qui s'appuient sur les informations de disponibilité. Outlook détecte l'URL du service de disponibilité à l'aide du service de découverte automatique. Pour utiliser l'équilibrage de charge réseau avec le service de disponibilité, vous devez modifier votre configuration.

L'URL interne est utilisée à partir de l'intranet et l'URL externe est utilisée sur Internet. Si vous voulez utiliser la même URL pour le trafic interne et externe, assurez-vous que le DNS est configuré de la manière adéquate pour router le trafic interne directement vers l'URL interne. Assurez-vous également que l'URL est accessible de manière interne et externe. Pour que les services de découverte automatique et de disponibilité fonctionnent, le DNS doit être configuré pour que mail.\<*nom de domaine*\>.com et autodiscover.mail.\<*nom de domaine*\>.com pointent vers l'IP virtuelle (VIP) de votre solution d'équilibrage de charge, où \<*nom de domaine*\> correspond au nom de votre domaine.

> [!NOTE]
> Pour plus d'informations, consultez les rubriques <a href="https://go.microsoft.com/fwlink/?linkid=45959">Références techniques sur l'équilibrage de la charge réseau</a> et <a href="https://go.microsoft.com/fwlink/?linkid=49315">Clusters d'équilibrage de la charge réseau</a>. Vous pouvez également rechercher des sites web de logiciels d'équilibrage de charge tiers.


## Méthodes employées pour extraire les informations de disponibilité

Le tableau suivant répertorie les différentes méthodes employées pour récupérer les informations de disponibilité dans diverses topologies à forêt unique.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Client</th>
<th>La boîte aux lettres extrayant les informations de disponibilité est en cours d'exécution</th>
<th>La boîte aux lettres cible est en cours d'exécution</th>
<th>Méthode d'extraction des informations de disponibilité</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Outlook 2013</p></td>
<td><p>Exchange 2013, Exchange 2010 ou Exchange 2007</p></td>
<td><p>Exchange 2013, Exchange 2010 ou Exchange 2007</p></td>
<td><p>Le service de disponibilité lit les informations de disponibilité à partir de la boîte aux lettres cible.</p></td>
</tr>
<tr class="even">
<td><p>Outlook 2007</p></td>
<td><p>Exchange 2013, Exchange 2010 ou Exchange 2007</p></td>
<td><p>Exchange 2010 ou  Exchange 2007</p></td>
<td><p>Le service de disponibilité lit les informations de disponibilité à partir de la boîte aux lettres cible.</p></td>
</tr>
<tr class="odd">
<td><p>Outlook 2007</p></td>
<td><p>Exchange 2010 ou  Exchange 2007</p></td>
<td><p>Exchange 2003</p></td>
<td><p>Le service de disponibilité établit des connexions HTTP avec le répertoire virtuel /public de la boîte aux lettres Exchange 2003.</p></td>
</tr>
<tr class="even">
<td><p>Outlook Web App</p></td>
<td><p>Exchange 2013, Exchange 2010 ou Exchange 2007</p></td>
<td><p>Exchange 2013, Exchange 2010 ou Exchange 2007</p></td>
<td><p>Outlook Web App dans Exchange 2010 ou Outlook Web Access dans Exchange 2007 appelle l'API du service de disponibilité, qui lit les informations de disponibilité à partir de la boîte aux lettres cible.</p></td>
</tr>
</tbody>
</table>

