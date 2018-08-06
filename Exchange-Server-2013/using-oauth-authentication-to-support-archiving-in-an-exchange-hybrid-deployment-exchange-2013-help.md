---
title: 'Utiliser l’auth. OAuth pr prendre en chg l’archiv. dans dplmt hybride Exchange | Microsoft Docs'
TOCTitle: Utilisation de l’authentification OAuth pour prendre en charge l’archivage dans un déploiement hybride Exchange
ms:assetid: deb882b1-1ae2-40f3-a71c-423fafe3d66a
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dn689104(v=EXCHG.150)
ms:contentKeyID: 62247325
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Utilisation de l’authentification OAuth pour prendre en charge l’archivage dans un déploiement hybride Exchange

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2016-12-09_

Si vous êtes dans un déploiement hybride Exchange 2013 et que vous utilisez l’archivage Exchange Online pour Exchange Server, vous devez configurer l’authentification OAuth entre vos organisations sur site et les organisations Exchange Online après la mise à niveau vers la mise à jour cumulative 5 d’Exchange 2013. L’archivage Exchange Online vous permet de disposer d’une archive sur le cloud pour vos utilisateurs avec des boîtes aux lettres sur site. Dans ce scénario, l’assistant de gestion des enregistrements de messagerie (MRM) sur votre serveur de boîtes aux lettres local applique des stratégies d’archivage et déplace automatiquement les messages de la boîte aux lettres d’un utilisateur vers son archive sur le cloud. Dans la mise à jour cumulative 5 d’Exchange 2013, l’authentification OAuth est utilisée.

Pour obtenir des instructions détaillées sur la configuration de l’authentification OAuth, consultez la rubrique [Configurer l’authentification OAuth entre des organisations Exchange et Exchange Online](configure-oauth-authentication-between-exchange-and-exchange-online-organizations-exchange-2013-help.md).

## Qu’est-ce que l’authentification OAuth ?

L’authentification OAuth est un protocole d’authentification S2S qui permet aux applications de s’authentifier mutuellement. Avec l’authentification OAuth, les informations d’identification et mots de passe de l’utilisateur ne sont pas transmis d’un ordinateur à un autre. Au lieu de cela, l’authentification et l’autorisation reposent sur l'échange de jetons de sécurité. Ces jetons donnent accès à un ensemble de ressources spécifique, pour une période donnée.

L’authentification OAuth implique généralement trois composants : un serveur d’autorisation unique et deux domaines qui doivent communiquer entre eux. Les jetons de sécurité sont émis par le serveur d’autorisation (également appelé serveur de jeton de sécurité) pour les deux domaines qui doivent communiquer entre eux. Ces jetons vérifient que les communications provenant d’un domaine doivent être approuvées par l’autre domaine. En utilisant l’authentification OAuth entre une organisation Exchange locale et Exchange Online, la fonction du serveur d’autorisation est fournie par Services de contrôle d’accès Azure Active Directory (ACS) dans votre organisation Office 365. Par exemple, lors d’une recherche de découverte électronique entre différents locaux, les services ACS Azure Active Directory émettent des jetons qui vérifient qu’un administrateur ou un responsable de la mise en conformité de l’organisation Exchange sur site est en mesure d’accéder aux boîtes aux lettres dans l’organisation Exchange Online, et vice-versa.

## Configuration de l’authentification OAuth pour la prise en charge de l’archivage

Comme indiqué précédemment, consultez la rubrique [Configurer l’authentification OAuth entre des organisations Exchange et Exchange Online](configure-oauth-authentication-between-exchange-and-exchange-online-organizations-exchange-2013-help.md) pour obtenir des instructions sur la configuration de l’authentification OAuth pour la prise en charge de l’archivage dans un déploiement hybride Exchange.

Si l’authentification OAuth n’est pas configurée pour votre déploiement hybride Exchange, vous ne pouvez pas utiliser de stratégies d’archivage pour déplacer automatiquement des éléments à partir d’une boîte aux lettres principale d’un utilisateur dans votre organisation sur site vers l’archive dans le cloud de l’utilisateur dans Exchange Online.

## Plus d’informations

  - Vous devez également configurer l’authentification OAuth pour pouvoir effectuer des recherches eDiscovery entre différents locaux dans vos boîtes aux lettres sur site et dans le cloud dans une seule recherche eDiscovery. Consultez la rubrique [Utilisation de l’authentification OAuth pour prendre en charge la découverte électronique dans un déploiement hybride Exchange](using-oauth-authentication-to-support-ediscovery-in-an-exchange-hybrid-deployment-exchange-2013-help.md).

  - Vous pouvez également configurer l’authentification OAuth pour permettre à d’autres applications, telles que SharePoint 2013 et Lync Server 2013, de s’authentifier auprès d’Exchange 2013. Pour plus d’informations, voir [Configuration de l’authentification OAuth avec SharePoint 2013 et Lync 2013](configure-oauth-authentication-with-sharepoint-2013-and-lync-2013-exchange-2013-help.md).

  - Vous pouvez configurer une authentification de serveur à serveur entre Exchange 2013 et SharePoint 2013 afin que les administrateurs et les responsables de la mise en conformité puissent utiliser le centre eDiscovery dans SharePoint 2013 pour effectuer des recherches dans les boîtes aux lettres Exchange 2013. Pour plus d’informations, voir [Configurer Exchange pour le Centre de découverte électronique SharePoint](configure-exchange-for-sharepoint-ediscovery-center-exchange-2013-help.md).

  - Vous pouvez configurer un déploiement hybride Exchange à l’aide de l’Assistant de configuration hybride dans Exchange 2013. Pour une liste de contrôle de configuration de déploiement hybride personnalisée et détaillée, consultez l’[assistant de déploiement Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=277105).

