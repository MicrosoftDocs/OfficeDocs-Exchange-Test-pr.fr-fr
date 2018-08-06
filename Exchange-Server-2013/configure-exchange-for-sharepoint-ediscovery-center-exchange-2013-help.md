---
title: 'Config. d’Exchange pour le Centre de découv. électr. SP: Exchange 2013 Help | Microsoft Docs'
TOCTitle: Configurer Exchange pour le Centre de découverte électronique SharePoint
ms:assetid: 795c1a3b-295c-4ee5-ade9-52cf3fda3f19
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ218665(v=EXCHG.150)
ms:contentKeyID: 50478514
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configurer Exchange pour le Centre de découverte électronique SharePoint

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2016-12-09_

Microsoft Exchange Server 2013 inclut des fonctionnalités utilisables avec Microsoft SharePoint Server 2013 et Microsoft Lync Server 2013, appelées *applications partenaires*. Pour vous assurer que ces applications partenaires peuvent accéder mutuellement à leurs ressources, vous devez configurer l’authentification de serveur à serveur.

Cette rubrique vous indique comment configurer l'authentification de serveur à serveur entre Exchange 2013 et SharePoint 2013 pour que les utilisateurs puissent utiliser le Centre de découverte électronique dans SharePoint 2013 afin de rechercher le contenu de boîte aux lettres Exchange Server 2013. Pour activer intégralement cette fonctionnalité, vous devez effectuer les étapes supplémentaires décrites dans SharePoint 2013. Pour obtenir plus d'informations, consultez la rubrique [Configurer la découverte électronique dans SharePoint 2013](https://go.microsoft.com/fwlink/?linkid=257727).

## Ce qu'il faut savoir avant de commencer

  - Durée d’exécution estimée de cette tâche : 30 minutes.

  - Les procédures décrites dans cette rubrique requièrent des autorisations spécifiques. Consultez chaque procédure pour savoir quelles autorisations sont nécessaires.

  - Il est possible d’installer Exchange 2013 et SharePoint 2013 dans différents domaines ou forêts. Une relation d’approbation Windows entre les forêts Exchange et SharePoint n’est pas requise, car dans ce cas, Exchange et SharePoint utilisent le protocole Oauth 2.0 pour s’approuver mutuellement.

  - Le site SharePoint 2013 doit être configuré pour utiliser SSL (Secure Sockets Layer).

  - L'[API gérée des services web Exchange](https://go.microsoft.com/fwlink/?linkid=257726) doit être installée sur chaque serveur exécutant SharePoint 2013. Réinitialisez Internet Information Server (IIS) après l’installation.

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.


## Comment procéder ?

## Étape 1 : Configurer l'authentification de serveur à serveur pour Exchange 2013 sur un serveur exécutant SharePoint Server 2013

Exécutez la commande suivante pour créer Exchange 2013 en tant qu'émetteur de jetons de sécurité approuvé dans SharePoint 2013.

    New-SPTrustedSecurityTokenIssuer -Name Exchange -MetadataEndPoint https://<Exchange Server Name or FQDN>/autodiscover/metadata/json/1

## Étape 2 : Configurer l'authentification de serveur à serveur pour SharePoint 2013 sur un serveur exécutant Exchange 2013

Effectuez cette étape sur un serveur Exchange 2013. Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l'entrée « Applications partenaires - configurer » de la rubrique [Autorisations de partage et de collaboration](sharing-and-collaboration-permissions-exchange-2013-help.md).

Exécutez cette commande pour configurer l'application partenaire SharePoint.

    cd c:\'Program Files'\Microsoft\'Exchange Server'\V15\Scripts
    .\Configure-EnterprisePartnerApplication.ps1 -AuthMetadataUrl <path to SharePoint AuthMetadataUrl> -ApplicationType SharePoint

## Étape 3 : Ajouter des utilisateurs autorisés au groupe de rôles Gestion de la découverte

Ajoutez les utilisateurs qui doivent effectuer une recherche de découverte électronique via SharePoint 2013 au groupe de rôles Gestion de la découverte dans Exchange 2013. Pour plus d'informations, consultez la rubrique [Attribution d’autorisations eDiscovery dans Exchange](assign-ediscovery-permissions-in-exchange-exchange-2013-help.md).

> [!CAUTION]
> L'ajout d'utilisateurs au groupe de rôles Gestion de la découverte permet à ces utilisateurs d'utiliser la découverte électronique locale pour effectuer une recherche dans toutes les boîtes aux lettres Exchange 2013 et accéder au contenu de messagerie électronique potentiellement sensible dans les boîtes aux lettres des utilisateurs. Par défaut, cette autorisation n’est accordée à aucun utilisateur, y compris aux membres du groupe de rôles Gestion de l’organisation. Avant d’accorder cette autorisation à un utilisateur, contactez le service juridique et le service des ressources humaines de votre organisation.

