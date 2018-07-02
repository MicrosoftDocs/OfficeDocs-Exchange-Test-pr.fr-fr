---
title: 'Adresses de messagerie et carnets d’adresses: Exchange 2013 Help'
TOCTitle: Adresses de messagerie et carnets d’adresses
ms:assetid: b97d0f68-691a-42af-9a6c-4dcc37b28a42
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ657488(v=EXCHG.150)
ms:contentKeyID: 50479061
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Adresses de messagerie et carnets d’adresses

 

_**Sapplique à :**Exchange Server 2013_

_**Dernière rubrique modifiée :**2015-03-09_

Les destinataires (utilisateurs, ressources, contacts et groupes) sont tout objet à extension messagerie dans Active Directory auquel Microsoft Exchange peut remettre ou vers lequel il peut acheminer des messages. Pour qu'un destinataire puisse recevoir ou envoyer des messages électroniques, il doit avoir une adresse de messagerie. Les carnets d'adresses constituent la méthode qui permet aux utilisateurs de se trouver en vue de s'envoyer des messages électroniques. Il existe plusieurs méthodes d'organisation des carnets d'adresses. Consultez la rubrique Terminologie clé pour obtenir des descriptions détaillées des fonctionnalités des carnets d'adresses dans Exchange Server 2013.

## Terminologie clé

Les termes suivants définissent les composants clés associés aux adresses de messagerie et aux carnets d'adresses dans Exchange 2013.

  - **stratégies de carnet d'adresses**  
    Les stratégies de carnet d’adresses vous permettent de segmenter des utilisateurs en groupes spécifiques pour fournir des vues personnalisées de la liste d’adresses globale de votre organisation. Lorsque vous créez une stratégie de carnet d'adresses, vous affectez une LAG, un carnet d'adresses en mode hors connexion, une liste de pièces ainsi qu'une ou plusieurs listes d'adresses à la stratégie. Vous pouvez alors attribuer la stratégie de carnet d'adresses à des utilisateurs de boîtes aux lettres et leur donner accès à une LAG personnalisée dans Outlook et Outlook Web App. L'objectif est de fournir un mécanisme plus simple de segmentation LAG pour des organisations locales nécessitant plusieurs LAG.

<!-- end list -->

  - **listes d'adresses**  
    Une liste d'adresses est un sous-ensemble de liste d'adresses globale (LAG). Chaque liste d'adresses est un recueil d'un ou plusieurs types de destinataires à extension messagerie (par exemple, utilisateurs, contacts, groupes, dossiers publics, conférences et autres ressources). Les listes d'adresses permettent d'organiser les destinataires et les ressources, ce qui facilite la recherche de destinataires et de ressources. Les listes d'adresses sont mises à jour de façon dynamique. Par conséquent, lorsque de nouveaux destinataires sont ajoutés à votre organisation, ils sont automatiquement ajoutés aux listes d'adresses appropriées.

<!-- end list -->

  - **stratégies d'adresse de messagerie**  
    Les stratégies d'adresse de messagerie génèrent les adresses de messagerie principales et secondaires pour vos destinataires, de façon à ce qu'ils puissent recevoir et envoyer des messages. Par défaut, Exchange contient une stratégie d'adresse de messagerie pour chaque utilisateur à extension messagerie.

<!-- end list -->

  - **carnets d'adresses hiérarchiques**  
    Le carnet d’adresses hiérarchique permet aux utilisateurs de rechercher des destinataires dans leur carnet d’adresses à l’aide d’une hiérarchie d’organisation, telle qu’une structure de gestion ou d’ancienneté. Normalement, les utilisateurs sont limités à la liste d’adresses globale par défaut et ses propriétés de destinataire associées, et la structure de la liste d’adresses globale ne reflète souvent pas exactement les relations hiérarchiques ou d’ancienneté des destinataires de votre organisation. Le fait de pouvoir personnaliser un carnet d'adresses hiérarchique reflétant la structure métier propre à votre organisation permet à vos utilisateurs de trouver efficacement les destinataires internes.

<!-- end list -->

  - **carnets d'adresses en mode hors connexion**  
    Un carnet d'adresses en mode hors connexion est une copie d'un regroupement de listes d'adresses qui a été téléchargé de sorte qu'un utilisateur Microsoft Outlook puisse accéder aux informations qu'il contient tout en étant déconnecté du serveur.

## Documentation relative aux adresses de messagerie et aux carnets d'adresses

Le tableau suivant renvoie à des rubriques qui vous aident à comprendre et à gérer des adresses de messagerie et des carnets d'adresses dans Exchange 2013.


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
<td><p><a href="address-lists-exchange-2013-help.md">Listes d’adresses</a></p></td>
<td><p>Apprenez à utiliser les listes d'adresses et les listes d'adresses globales pour organiser vos listes de destinataires afin d'en faciliter l'accès.</p></td>
</tr>
<tr class="even">
<td><p><a href="address-book-policies-exchange-2013-help.md">Stratégies de carnet d’adresses</a></p></td>
<td><p>Apprenez à séparer vos listes d'adresses de vos listes d'adresses globales en organisations virtuelles distinctes.</p></td>
</tr>
<tr class="odd">
<td><p><a href="details-templates-exchange-2013-help.md">Modèles de détails</a></p></td>
<td><p>Apprenez à personnaliser des certes de visite dans Outlook.</p></td>
</tr>
<tr class="even">
<td><p><a href="email-address-policies-exchange-2013-help.md">Stratégies d'adresse de messagerie</a></p></td>
<td><p>Découvrez les adresses de messagerie de proxy qui permettent de faciliter la localisation des destinataires.</p></td>
</tr>
<tr class="odd">
<td><p><a href="hierarchical-address-books-exchange-2013-help.md">Carnets d’adresses hiérarchiques</a></p></td>
<td><p>Apprenez-en plus sur la personnalisation des listes d’adresses globales et des listes d’adresses qui vous permet de vous conformer à la structure unique de votre organisation.</p></td>
</tr>
<tr class="even">
<td><p><a href="offline-address-books-exchange-2013-help.md">Carnets d’adresses en mode hors connexion</a></p></td>
<td><p>Apprenez-en plus sur la manière d’offrir aux utilisateurs un accès hors connexion aux listes d’adresses de votre organisation.</p></td>
</tr>
</tbody>
</table>

