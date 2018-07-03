---
title: 'Configurer le partage fédéré: Exchange 2013 Help'
TOCTitle: Configurer le partage fédéré
ms:assetid: b25ae450-def3-4797-a5fc-6e9bcee71a5d
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ657483(v=EXCHG.150)
ms:contentKeyID: 50479025
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configurer le partage fédéré

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2015-04-07_

Grâce au partage fédéré disponible dans Exchange Server 2013, les utilisateurs peuvent partager des informations avec des destinataires au sein d’organisations fédérées externes. comme le partage de leurs informations de disponibilité (aussi connue sous le nom de disponibilité du calendrier) à des fins de planification ou, en fonction de la nature de la relation professionnelle, le partage d’informations de calendrier plus détaillées. Pour en savoir plus sur le partage fédéré, voir [Partage](sharing-exchange-2013-help.md).

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159813.important(EXCHG.150).gif" title="Important" alt="Important" />Important :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Cette fonctionnalité d’Exchange Server 2013 n’est pas entièrement compatible avec les systèmes Office 365 exécutés par 21Vianet en Chine et certaines limitations de fonctionnalités peuvent s’appliquer. Pour plus d’informations, voir <a href="https://go.microsoft.com/fwlink/?linkid=313640">En savoir plus sur Office 365 exécuté par 21Vianet</a>.</td>
</tr>
</tbody>
</table>


## Ce qu’il faut savoir avant de commencer ?

  - Durée d’exécution estimée de cette tâche : 1 heure.

  - Les procédures décrites dans cette rubrique requièrent des autorisations spécifiques. Consultez chaque procédure pour savoir quelles autorisations sont nécessaires.

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.


## Comment procéder ?

## Étape 1 : Créer et configurer une approbation de fédération

Une approbation de fédération établit une relation d’approbation entre une organisation Exchange 2013 et le système d’authentification Azure Active Directory, et constitue une condition requise du partage fédéré.

Pour plus d'informations, consultez la rubrique [Configurer une approbation de fédération](configure-a-federation-trust-exchange-2013-help.md).

## Étape 2 : Créer une relation d’organisation

Une relation d’organisation permet aux utilisateurs de votre organisation Exchange de partager des informations de disponibilité du calendrier dans le cadre d’un partage fédéré avec d’autres organisations Exchange fédérées. Le partage fédéré peut être configuré entre deux organisations Exchange 2013 fédérées ou entre une organisation Exchange 2013 fédérée et des organisations Exchange 2010 fédérées.

Pour plus d'informations, consultez la rubrique [Créer une relation d’organisation](create-an-organization-relationship-exchange-2013-help.md).

## Étape 3 : Créer une stratégie de partage

Les stratégies de partage permettent un partage établi par utilisateur, et de personne à personne, des informations de calendrier et de contacts avec les différents types d’utilisateurs externes. Elles prennent en charge le partage des informations de calendrier et de contact avec les organisations externes fédérées, les organisations externes non fédérées et les utilisateurs individuels ayant un accès à Internet. Si vous n’avez pas à configurer de partage de personne à personne ou de contact (partage de niveau organisationnel uniquement), vous n’avez pas à configurer une stratégie de partage.

Pour plus d'informations, consultez la rubrique [Créer une stratégie de partage](create-a-sharing-policy-exchange-2013-help.md).

## Étape 4 : Configurer un enregistrement DNS public de découverte automatique

Vous devez ajouter un enregistrement CNAME à votre DNS public. Le nouvel enregistrement CNAME doit pointer vers un serveur d’accès au client Exchange 2013 sur Internet qui exécute le service de découverte automatique.

Pour obtenir des instructions détaillées sur l’ajout d’enregistrements CNAME, reportez-vous au service d’hôte pour vos enregistrements DNS publics. Il s’agit d’un service Internet qui peut aussi héberger votre site Web de domaine.

