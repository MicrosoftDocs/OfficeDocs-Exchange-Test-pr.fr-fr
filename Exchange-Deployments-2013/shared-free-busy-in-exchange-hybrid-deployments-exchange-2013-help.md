---
title: 'Partage des disponibilités dans des déploiements hybrides Exchange: Exchange 2013 Help'
TOCTitle: Partage des disponibilités dans des déploiements hybrides Exchange
ms:assetid: bd3884de-80ee-4ff2-a8a3-eacd5aa3e51b
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ650274(v=EXCHG.150)
ms:contentKeyID: 50479673
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Partage des disponibilités dans des déploiements hybrides Exchange

 

_**Sapplique à :**Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :**2016-04-29_

Le partage des informations de disponibilité (également appelées disponibilité de calendrier) entre les utilisateurs d’une organisation locale et ceux d’une organisation Exchange Online est l’un des principaux avantages d’un déploiement hybride. Les utilisateurs des deux organisations peuvent consulter leurs calendriers mutuels, comme s’ils se trouvaient physiquement dans la même organisation. Cela facilite et optimise la planification des réunions et des ressources.

Dans un déploiement hybride, plusieurs composants sont requis pour activer la fonctionnalité de disponibilité partagée entre votre organisation Exchange locale et Exchange Online.

  - **Approbation de fédération**   Les organisations locale et du service Office 365 doivent toutes deux établir une approbation de fédération avec le système d’authentification Azure AD. Une approbation de fédération est une relation un-à-un avec le système d’authentification Azure AD qui définit les paramètres de votre organisation Exchange. Le système utilise ces paramètres lorsqu’il sert de courtier d’approbation entre votre organisation locale et l’organisation du service Office 365 afin d’échanger des informations de disponibilité entre les utilisateurs de l’organisation locale et de l’organisation Exchange Online.
    
    Une approbation de fédération est automatiquement configurée avec le système pour votre organisation du service Office 365 lorsque le compte est créé. L’Assistant Configuration hybride vérifie automatiquement s’il existe une approbation de fédération avec le système d’authentification Azure AD pour l’organisation locale. Si tel est le cas, la fédération existante est utilisée pour prendre en charge le déploiement hybride. Dans le cas contraire, l’Assistant crée une approbation de fédération pour l’organisation locale avec le système d’authentification Azure AD. L’Assistant ajoute également tout domaine sélectionné dans l’Assistant Configuration hybride à l’approbation de fédération de l’organisation locale.
    
    Pour plus d’informations, consultez la rubrique [Partage](https://technet.microsoft.com/fr-fr/library/dd638083\(v=exchg.150\)).

  - **Relations des organisations**   Des relations des organisations sont requises pour l’organisation locale et l’organisation Exchange Online et sont configurées automatiquement par l’assistant Configuration hybride. Une relation d’organisation définit le niveau des informations de disponibilité partagées pour une organisation.
    
    Par défaut, le niveau d’accès aux informations de disponibilité est **Disponibilité d’accès avec l’heure, plus objet et emplacement** pour les relations des organisations locale et Exchange Online. Si vous souhaitez modifier l’accès en partage aux informations de disponibilité entre les utilisateurs de l’organisation locale et de l’organisation Exchange, vous pouvez configurer manuellement le niveau d’accès aux relations des organisations une fois que l’assistant Configuration hybride a terminé.
    
    Pour plus d’informations, consultez la rubrique [Partage](https://technet.microsoft.com/fr-fr/library/dd638083\(v=exchg.150\)).

Lors de la configuration de votre organisation pour un déploiement hybride, la configuration de l’accès au calendrier de disponibilité partagé est automatiquement effectuée par l’Assistant Configuration hybride dans tous les scénarios. La création d’une approbation de fédération avec le système d’authentification Azure AD et la configuration des relations d’organisation pour l’organisation locale et Exchange Online sont des conditions essentielles à un déploiement hybride. Si vous ne souhaitez pas autoriser l’accès en partage aux informations de disponibilité entre les utilisateurs de l’organisation locale et de l’organisation Exchange Online dans le déploiement hybride, vous pouvez désactiver manuellement le partage en utilisant l’Environnement de ligne de commande Exchange Management Shell et la cmdlet [Set-HybridConfiguration](https://technet.microsoft.com/fr-fr/library/hh529932\(v=exchg.150\)) une fois que l’Assistant Configuration hybride a terminé.

Les fonctions de déploiement hybride décrites dans le tableau suivant ont des dépendances sur les approbations de fédération et les relations des organisations.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Zone de messagerie</th>
<th>Fonction</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Client de messagerie</p></td>
<td><ul>
<li><p>Suivi des messages</p></li>
<li><p>Infos-courrier</p></li>
<li><p>Recherche dans plusieurs boîtes aux lettres</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Conformité</p></td>
<td><ul>
<li><p>Archivage Exchange Online</p></li>
<li><p>Découverte électronique locale Exchange</p></li>
</ul></td>
</tr>
</tbody>
</table>

