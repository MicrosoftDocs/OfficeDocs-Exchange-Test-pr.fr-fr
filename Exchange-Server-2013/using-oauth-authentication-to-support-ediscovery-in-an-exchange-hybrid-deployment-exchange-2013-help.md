---
title: 'Utilisation de l’authentification OAuth pour prendre en charge la découverte électronique dans un déploiement hybride Exchange: Exchange 2013 Help'
TOCTitle: Utilisation de l’authentification OAuth pour prendre en charge la découverte électronique dans un déploiement hybride Exchange
ms:assetid: b069f8db-fbe1-4047-ad97-d00172ee6a12
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dn497703(v=EXCHG.150)
ms:contentKeyID: 61292118
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Utilisation de l’authentification OAuth pour prendre en charge la découverte électronique dans un déploiement hybride Exchange

 

_**Sapplique à :** Exchange Online, Exchange Server 2013_

_**Dernière rubrique modifiée :** 2016-12-09_

Pour effectuer des recherches de découverte électronique entre différents locaux dans une organisation hybride Exchange 2013, vous devrez configurer l’authentification OAuth (Open Authorization) entre vos organisations Exchange sur site et Exchange Online afin de pouvoir utiliser la découverte électronique locale pour effectuer des recherches dans des boîtes aux lettres sur site et dans le cloud. L’authentification OAuth prend en charge les scénarios de découverte électronique suivants dans un déploiement hybride Exchange :

  - Les recherches dans des boîtes aux lettres sur site utilisant l’archivage Exchange Online pour des boîtes aux lettres d’archivage dans le cloud.

  - Les recherches dans des boîtes aux lettres sur site et dans le cloud dans la même recherche de découverte électronique.

Pour obtenir des instructions détaillées sur la configuration de l’authentification OAuth afin qu’elle prenne en charge la découverte électronique, consultez la rubrique [Configurer l’authentification OAuth entre des organisations Exchange et Exchange Online](configure-oauth-authentication-between-exchange-and-exchange-online-organizations-exchange-2013-help.md).

## Qu’est-ce que l’authentification OAuth ?

L’authentification OAuth est un protocole d’authentification S2S qui permet aux applications de s’authentifier mutuellement. Avec l’authentification OAuth, les informations d’identification et mots de passe de l’utilisateur ne sont pas transmis d’un ordinateur à un autre. Au lieu de cela, l’authentification et l’autorisation reposent sur l’échange de jetons de sécurité. Ces jetons donnent accès à un ensemble de ressources spécifique, pour une période donnée.

L’authentification OAuth implique généralement trois composants : un serveur d’autorisation unique et deux domaines qui doivent communiquer entre eux. Les jetons de sécurité sont émis par le serveur d’autorisation (également appelé serveur de jeton de sécurité) pour les deux domaines qui doivent communiquer entre eux. Ces jetons vérifient que les communications provenant d’un domaine doivent être approuvées par l’autre domaine. En utilisant l’authentification OAuth entre une organisation Exchange sur site et Exchange Online, la fonction du serveur d’autorisation est fournie par les services de contrôle d’accès (ACS) Active Directory de Microsoft Azure dans votre organisation Office 365. Par exemple, lors d’une recherche de découverte électronique entre différents locaux, les services ACS d’Azure émettent des jetons qui vérifient qu’un administrateur ou un responsable de la mise en conformité de l’organisation Exchange sur site est en mesure d’accéder aux boîtes aux lettres dans l’organisation Exchange Online, et vice-versa.

## Scénarios de découverte électronique dans un déploiement hybride

Le tableau suivant identifie les scénarios de découverte électronique dans un déploiement hybride Exchange qui nécessitent une authentification OAuth.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Scénario de découverte électronique</th>
<th>Authentification OAuth nécessaire ?</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Recherche de boîtes aux lettres Exchange sur site et de boîtes aux lettres Exchange Online dans la même recherche de découverte électronique initiée depuis l’organisation Exchange sur site. Par exemple, recherche de toutes les boîtes aux lettres de l’organisation dans une seule recherche de découverte électronique.</p></td>
<td><p>Oui</p></td>
</tr>
<tr class="even">
<td><p>Recherche de boîtes aux lettres Exchange sur site utilisant l’archivage Exchange Online pour des boîtes aux lettres d’archivage dans le cloud. Lorsque vous utilisez la découverte électronique locale, la boîte aux lettres principale et la boîte aux lettres d’archivage sont recherchées.</p></td>
<td><p>Oui</p></td>
</tr>
<tr class="odd">
<td><p>Recherche de boîtes aux lettres Exchange Online à partir d’une recherche de découverte électronique initiée depuis l’organisation Exchange sur site par un administrateur ou un responsable de la mise en conformité.</p></td>
<td><p>Oui</p></td>
</tr>
<tr class="even">
<td><p>Recherche de boîtes aux lettres sur site à l’aide d’une recherche de découverte électronique initiée depuis l’organisation Exchange sur site par un administrateur ou un responsable de la mise en conformité.</p></td>
<td><p>Non</p>
> [!NOTE]
> Comme indiqué précédemment, l’authentification OAuth serait nécessaire si les boîtes aux lettres sur site étaient configurées avec des boîtes aux lettres d’archivage dans le cloud.

</td>
</tr>
<tr class="odd">
<td><p>Recherche des boîtes aux lettres Exchange Online à partir d’une recherche de découverte électronique initiée à partir d’Exchange Online ou du centre de découverte électronique dans SharePoint Online par un administrateur client Office 365 ou un responsable de la mise en conformité connecté sur un compte utilisateur Office 365.</p></td>
<td><p>Non</p></td>
</tr>
</tbody>
</table>


## Configuration de l’authentification OAuth pour la prise en charge de la découverte électronique

Comme indiqué précédemment, consultez [Configurer l’authentification OAuth entre des organisations Exchange et Exchange Online](configure-oauth-authentication-between-exchange-and-exchange-online-organizations-exchange-2013-help.md) pour obtenir des instructions sur la configuration de l’authentification OAuth pour la prise en charge de la découverte électronique dans un déploiement hybride Exchange.

Si OAuth n’est pas configuré pour votre déploiement hybride Exchange, vous ne pouvez pas utiliser la découverte électronique pour rechercher des boîtes aux lettres Exchange sur site et Exchange Online dans la même recherche de découverte électronique. Vous devrez rechercher des boîtes sur site à partir d’une recherche de découverte électronique initiée depuis votre organisation locale. De même, vous pouvez seulement rechercher des boîtes aux lettres Exchange Online à partir d’une recherche de découverte électronique initiée depuis votre organisation Exchange Online ou en utilisant le centre de découverte électronique dans SharePoint Online. En outre, vous ne serez pas en mesure de rechercher des boîtes aux lettres principales sur site si leur boîte aux lettres d’archivage correspondante se trouve dans Exchange Online ou dans une organisation d’archivage Exchange Online.

## Plus d’informations

  - Vous pouvez également utiliser l’authentification OAuth pour permettre à d’autres applications, telles que SharePoint 2013 et Lync Server 2013, de s’authentifier auprès d’Exchange 2013. Pour plus d’informations, voir [Configuration de l’authentification OAuth avec SharePoint 2013 et Lync 2013](configure-oauth-authentication-with-sharepoint-2013-and-lync-2013-exchange-2013-help.md).

  - Vous pouvez configurer une authentification de serveur à serveur entre Exchange 2013 et SharePoint 2013 afin que les administrateurs et les responsables de la mise en conformité puissent utiliser le centre eDiscovery dans SharePoint 2013 pour effectuer des recherches dans les boîtes aux lettres Exchange 2013. Pour plus d’informations, voir [Configurer Exchange pour le Centre de découverte électronique SharePoint](configure-exchange-for-sharepoint-ediscovery-center-exchange-2013-help.md).

  - Vous pouvez configurer un déploiement hybride d’Exchange à l’aide de l’Assistant de Configuration hybride dans Exchange 2013. Pour obtenir un résumé de configuration du déploiement hybride personnalisé, étape par étape, consultez l' [Assistant de déploiement Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=277105).

