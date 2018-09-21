---
title: 'Intégration à SharePoint et Lync: Exchange 2013 Help'
TOCTitle: Intégration à SharePoint et Lync
ms:assetid: 056b29f6-e0e9-4974-b763-002518857a93
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ150480(v=EXCHG.150)
ms:contentKeyID: 50477453
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Intégration à SharePoint et Lync

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2016-12-09_

MicrosoftExchange Server 2013 inclut de nombreuses fonctionnalités qui s’intègrent avec Microsoft SharePoint 2013 et Microsoft Lync 2013. Ensemble, ces produits offrent une palette de fonctionnalités qui rendent possibles certains scénarios, tels que la découverte électronique d’entreprise et la collaboration à l’aide des boîtes aux lettres de site.

## Archivage, blocage et découverte électronique (eDiscovery)

L’archivage des messages électroniques et des documents, leur conservation pendant la durée nécessaire pour respecter les exigences de conformité réglementaire et celles de l’entreprise, ainsi que la possibilité d’effectuer des recherches rapides pour satisfaire les demandes de découverte électronique, sont des opérations essentielles dans la plupart des organisations. Ensemble, Exchange 2013, SharePoint 2013 et Lync Server 2013 offrent des fonctionnalités intégrées d’archivage, de blocage et de découverte automatique qui vous permettent de conserver vos données importantes localement, dans des boîtes aux lettres Exchange, des documents SharePoint, des sites Web et du contenu Lync archivé. Le Centre eDiscovery de SharePoint 2013 permet aux gestionnaires de découverte agréés d’effectuer une recherche eDiscovery pour trouver du contenu dans ces magasins, d’afficher un aperçu des résultats de la recherche et d’exporter les données à des fins d’examen juridique.

## Archivage du contenu Lync Server 2013 dans Exchange 2013

Lorsque Lync Server 2013 est déployé dans une organisation avec Exchange 2013, vous pouvez configurer Lync pour archiver les messages instantanés et le contenu des réunions en ligne, comme des présentations ou des documents partagés, dans la boîte aux lettres Exchange 2013 de l’utilisateur. L’archivage des données Lync dans Exchange 2013 vous permet de leur appliquer des stratégies de rétention. Le contenu Lync archivé apparaît également dans les recherches eDiscovery. Pour plus d’informations sur l’archivage de contenu Lync et son déploiement, consultez les rubriques suivantes :

  - [Planification de l’archivage](https://go.microsoft.com/fwlink/p/?linkid=265005)

  - [Déploiement de l’archivage](https://go.microsoft.com/fwlink/p/?linkid=265006)

## Recherche de données Exchange, SharePoint et Lync à l’aide du Centre eDiscovery SharePoint 2013

Exchange 2013 permet à SharePoint 2013 de rechercher du contenu dans une boîte aux lettres Exchange à l’aide d’une API de recherche fédérée. SharePoint 2013 propose un Centre eDiscovery qui permet au personnel autorisé de procéder à une découverte électronique. Microsoft Search Foundation fournit à Exchange 2013 et SharePoint 2013 une infrastructure commune d’indexation et de recherche et vous permet d’utiliser la même syntaxe de requête dans les deux applications. Ainsi, une recherche eDiscovery effectuée dans SharePoint 2013 renverra le même contenu Exchange 2013 que si vous aviez lancé la même recherche en utilisant la découverte électronique sur place dans Exchange 2013. Avec le Centre eDiscovery SharePoint 2013, vous pouvez également exporter le contenu renvoyé par une recherche eDiscovery, notamment exporter le contenu Exchange 2013 vers un fichier PST.

Pour plus d’informations, consultez les rubriques suivantes :

  - [Découverte électronique locale](https://docs.microsoft.com/fr-fr/exchange/security-and-compliance/in-place-ediscovery/in-place-ediscovery)

  - [Conservation inaltérable et conservation pour litige](https://docs.microsoft.com/fr-fr/exchange/security-and-compliance/in-place-and-litigation-holds)

  - [Configurer eDiscovery dans SharePoint 2013](https://go.microsoft.com/fwlink/p/?linkid=257727)

  - [Nouveautés d’eDiscovery dans SharePoint Server 2013](https://go.microsoft.com/fwlink/?linkid=275091)

  - [Configurer Exchange pour le Centre de découverte électronique SharePoint](configure-exchange-for-sharepoint-ediscovery-center-exchange-2013-help.md)

## Boîtes aux lettres de site

Dans de nombreuses organisations, les informations résident dans deux magasins différents : les messages électroniques sont stockés dans Microsoft Exchange et les documents dans SharePoint. Deux interfaces différentes permettent d’y accéder. Cette dualité en termes d’expérience utilisateur empêche une collaboration efficace. Les boîtes aux lettres de site permettent aux utilisateurs de collaborer efficacement en regroupant les messages électroniques Exchange et les documents SharePoint. Pour les utilisateurs, une boîte aux lettres de site sert de classeur central où sont classés les messages électroniques et les documents d’un projet. Seuls les membres du site peuvent y accéder et les modifier. Les boîtes aux lettres de site sont exposées dans Outlook 2013 et permettent aux utilisateurs d’accéder facilement aux messages électroniques et documents des projets qui les intéressent. D’autre part, il est possible d’accéder au même ensemble de contenu directement depuis le site SharePoint lui-même.

Par le biais d’une boîte aux lettres de site, le contenu est conservé là où il faut. Exchange stocke les messages électroniques, offrant ainsi aux utilisateurs le même affichage de message pour les conversations par message électronique que ce qu’ils utilisent tous les jours dans leur propre boîte aux lettres. SharePoint stocke les documents ; il permet la co-création de documents et un contrôle de version au sein de l’organisation. Exchange synchronise uniquement les métadonnées nécessaires à partir de SharePoint pour créer une vue du document dans Outlook (par exemple, titre du document, date de dernière modification, auteur de la dernière modification, taille).

Les boîtes aux lettres de site sont configurées et gérées à partir de SharePoint 2013. Pour plus d’informations, consultez les rubriques suivantes:

  - [Boîtes aux lettres de site](site-mailboxes-exchange-2013-help.md)

  - [Configurer des boîtes aux lettres du site dans SharePoint Server 2013](https://go.microsoft.com/fwlink/p/?linkid=258264)

## Magasin de contacts unifié

Le magasin de contacts unifié est une fonction qui permet une gestion cohérente des contacts entre plusieurs produits Microsoft Office. Les utilisateurs peuvent stocker toutes les informations relatives à leurs contacts dans leur boîte aux lettres Exchange 2013, si bien que les mêmes informations de contact sont disponibles globalement dans Lync, Exchange, Outlook et Outlook Web App.

Vous devez d’abord installer Lync Server 2013 dans un environnement doté d’Exchange 2013 et configurer l’authentification serveur à serveur entre les deux. Ensuite, les utilisateurs peuvent commencer à migrer les contacts de Lync Server 2013 vers Exchange 2013. Pour plus d’informations, consultez la rubrique [Planification et déploiement d’un magasin de contacts unifié](https://go.microsoft.com/fwlink/p/?linkid=275092).

## Photos de l’utilisateur

La fonctionnalité Photos de l’utilisateur permet de stocker les photos haute résolution de l’utilisateur dans Exchange 2013. Les applications clientes, telles que Outlook, Outlook Web App, SharePoint 2013, Lync 2013 et les clients de messagerie mobiles, peuvent y accéder. Une photo basse résolution est également stockée dans Active Directory. Comme pour les magasins de contacts unifiés, la fonctionnalité Photos de l’utilisateur permet d’utiliser de manière cohérente une photo de profil utilisateur qui est mise à la disposition des applications clientes. Celles-ci n’ont pas besoin de posséder leurs propres photos d’utilisateur ni de les ajouter ou de les gérer différemment. Les utilisateurs peuvent gérer leurs propres photos à l’aide d’Outlook Web App, de SharePoint 2013 ou de Lync 2013. Pour des informations sur la gestion des photos dans Outlook Web App, consultez la rubrique [Mon compte](https://go.microsoft.com/fwlink/p/?linkid=269646).

## Présence de Lync dans Outlook Web App

Vous pouvez configurer les environnements Exchange 2013 dotés de Lync Server 2013 pour que les utilisateurs puissent voir les informations de présence dans Outlook Web App. Les utilisateurs peuvent voir leurs contacts et groupes de messagerie instantanée dans le volet de navigation d’Outlook Web App, accepter ou démarrer des sessions de messagerie instantanée à partir d’Outlook Web App et gérer leurs contacts et groupes de messagerie instantanée.

## Authentification OAuth

Pour que vous puissiez bénéficier des fonctions étendues décrites ci-dessus dans plusieurs produits, Exchange 2013, SharePoint 2013 et Lync Server 2013 utilisent le protocole d’autorisation OAuth qui permet une authentification serveur à serveur. Ces applications utilisent le même protocole d’authentification pour s’authentifier entre elles de manière transparente, en toute sécurité. Le mécanisme d’authentification prend en charge l’authentification en tant qu’application en utilisant le contexte d’un compte lié et l’emprunt d’identité d’un utilisateur où la demande d’accès est faite dans le contexte utilisateur.

OAuth est un protocole d’autorisation standard utilisé par de nombreux sites et services Web. Il permet aux clients d’accéder aux ressources d’un serveur de ressources sans fournir aucun nom d’utilisateur ni mot de passe. L’authentification est assurée par un serveur d’autorisation approuvé par le propriétaire des ressources. Un jeton d’accès est fourni au client. Le jeton donne accès à un ensemble spécifique de ressources pendant une période donnée. Pour plus d’informations sur l’implémentation de l’authentification OAuth d’Exchange 2013, consultez la rubrique [\[MS-XOAUTH\] : Extensions du protocole d’autorisation OAuth 2.0](https://go.microsoft.com/fwlink/p/?linkid=275093).

**OAuth dans les déploiements sur site**

Dans un déploiement sur site, Exchange 2013, SharePoint 2013 et Lync Server 2013 n’ont pas besoin d’un serveur d’autorisation pour émettre des jetons. Chacune de ces applications émet des jetons auto-signés pour accéder aux ressources fournies par d’autres applications. L’application qui permet d’accéder aux ressources, Exchange 2013, par exemple, doit approuver les jetons auto-signés présentés par l’application appelante. L’approbation est établie en créant une configuration d’*application partenaire* pour l’application appelante, qui inclut l’identificateur ApplicationID, le certificat et l’URL AuthMetadataUrl de l’application appelante. Exchange 2013, SharePoint 2013 et Lync Server 2013 publient leur document de métadonnées d’authentification dans une URL réservée.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>Serveur</strong></p></td>
<td><p><strong>AuthMetadataUrl</strong></p></td>
</tr>
<tr class="even">
<td><p>Exchange 2013</p></td>
<td><p><code>https://&lt;serverfqdn&gt;/autodiscover/metadata/json/1</code></p></td>
</tr>
<tr class="odd">
<td><p>Lync Server 2013</p></td>
<td><p><code>https://&lt;serverfqdn&gt;/metadata/json/1</code></p></td>
</tr>
<tr class="even">
<td><p>SharePoint 2013</p></td>
<td><p><code>https://&lt;serverfqdn&gt;/_layouts/15/metadata/json/1</code></p></td>
</tr>
</tbody>
</table>


**Certificat d’authentification serveur Exchange 2013**

Le programme d’installation d’Exchange 2013 crée un certificat auto-signé nommé Certificat d’authentification serveur Microsoft Exchange (Microsoft Exchange Server Auth Certificate). Ce certificat est répliqué sur tous les serveurs frontaux dans l’organisation Exchange 2013. L’empreinte du certificat est spécifiée dans la configuration d’autorisation d’Exchange 2013, avec son nom de service, un GUID réservé qui représente Exchange 2013 local. Exchange utilise la configuration d’autorisation pour publier son document de métadonnées d’authentification.

> [!IMPORTANT]
> Le certificat d’authentification serveur par défaut créé par Exchange 2013 est valable cinq ans. Vous devez vérifier que la configuration d’autorisation inclut un certificat actuel.


Lorsque Exchange 2013 reçoit une demande d’accès provenant d’une application partenaire via les services Web d’Exchange, il analyse l’en-tête `www-authenticate` de la demande https, qui contient le jeton d’accès signé par le serveur appelant utilisant sa clé privée. Le module d’authentification utilise la configuration de l’application partenaire pour valider le jeton d’accès. Il donne ensuite accès aux ressources en se basant sur les autorisations RBAC accordées à l’application. Si le jeton d’accès est émis au nom d’un utilisateur, les autorisations RBAC qui lui sont accordées sont vérifiées. Par exemple, si un utilisateur effectue une recherche eDiscovery via le Centre eDiscovery de SharePoint 2013, Exchange vérifie s’il appartient au groupe de rôles de gestion de la découverte ou si le rôle de recherche de boîte aux lettres lui est attribué et si les boîtes aux lettres faisant l’objet de la recherche se trouvent dans l’étendue de l’attribution de rôles RBAC. Pour plus d’informations, consultez la rubrique [Autorisations](permissions-exchange-2013-help.md).

## Gestion de l’authentification OAuth

Dans Exchange 2013, vous devez gérer deux objets de configuration pour permettre l’authentification OAuth avec des applications partenaires :

  - **AuthConfig**   AuthConfig est créé par le programme d’installation d’Exchange 2013. Il permet de publier les métadonnées d’authentification. Vous n’avez pas besoin de gérer la configuration d’authentification, sauf si le certificat actuel arrive à expiration et que vous devez en configurer un nouveau. Dans ce cas, vous pouvez renouveler le certificat actuel et configurer le nouveau comme certificat suivant dans AuthConfig, en précisant sa date d’effet. Le nouveau certificat est automatiquement répliqué vers d’autres serveurs Exchange 2013 dans l’organisation, le document de métadonnées d’authentification est actualisé en fonction des informations du nouveau certificat et AuthConfig active le nouveau certificat à la date d’effet.

  - **Applications partenaires**   Pour que les applications partenaires puissent demander des jetons d’accès à Exchange 2013, vous devez créer une configuration d’application partenaire. Exchange 2013 fournit le script `Configure-EnterprisePartnerApplication.ps1` qui permet de créer rapidement et facilement des configurations d’applications partenaires et de diminuer le nombre d’erreurs de configuration. Pour plus d’informations, consultez la rubrique [Configuration de l’authentification OAuth avec SharePoint 2013 et Lync 2013](configure-oauth-authentication-with-sharepoint-2013-and-lync-2013-exchange-2013-help.md).

