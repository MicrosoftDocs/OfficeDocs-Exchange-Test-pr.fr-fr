---
title: 'Planification et déploiement: Exchange 2013 Help'
TOCTitle: Planification et déploiement
ms:assetid: 692c59e3-f0b0-4cef-a66e-751aa740abae
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Aa998636(v=EXCHG.150)
ms:contentKeyID: 50478352
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Planification et déploiement

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2016-12-09_

Avez-vous besoin d’aide pour effectuer une installation d’Exchange ? Cet article fournit des conseils pour préparer un déploiement de Microsoft Exchange Server 2013, ainsi que des liens vers des articles dont vous aurez besoin au cours du déploiement.

Les sections suivantes contiennent des liens vers des informations qui vous expliquent comment planifier puis déployer Microsoft Exchange Server 2013.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159813.important(EXCHG.150).gif" title="Important" alt="Important" />Important :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Nous vous conseillons vivement de lire la rubrique <a href="release-notes-for-exchange-2013-exchange-2013-help.md">Notes de publication relatives à Exchange 2013</a> avant de commencer votre déploiement. Les notes de publication contiennent des informations importantes sur les problèmes que vous pourriez rencontrer pendant ou après votre déploiement.</td>
</tr>
</tbody>
</table>


**Contenu de cette rubrique**

Planification pour Exchange 2013

Déploiement d’une installation d’Exchange 2013

Présentation du programme d'installation de Microsoft Exchange 2013

Pour plus d'informations

## Planification pour Exchange 2013

Utilisez les liens suivants pour accéder aux informations qui vous aideront à planifier le déploiement d'Exchange Server 2013 dans votre organisation.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159813.important(EXCHG.150).gif" title="Important" alt="Important" />Important :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Consultez la section Création d'un environnement de test relative à l'installation d'Exchange 2013 dans un environnement de test, plus loin dans cette rubrique.</td>
</tr>
</tbody>
</table>


  - [Serveurs de boîtes aux lettres et d’accès au client](mailbox-and-client-access-servers-exchange-2013-help.md)  
    Nous vous recommandons de consulter des informations sur les rôles de serveur d'accès au client et de boîte aux lettres qui sont inclus dans Exchange 2013.

<!-- end list -->

  - [Configuration requise pour Exchange 2013](exchange-2013-system-requirements-exchange-2013-help.md)  
    Passez en revue la configuration système requise à respecter dans votre organisation pour pouvoir installer Exchange 2013.

<!-- end list -->

  - [Conditions préalables pour Exchange 2013](exchange-2013-prerequisites-exchange-2013-help.md)  
    Découvrez les fonctionnalités de Windows Server 2008 R2 Service Pack 1 (SP1) ou de Windows Server 2012 ainsi que les autres logiciels que vous devez installer pour réussir l'installation d'Exchange 2013.

<!-- end list -->

  - [Assistant de déploiement Exchange Server](exchange-server-deployment-assistant-exchange-2013-help.md)  
    Utilisez cet outil pour générer une liste de contrôle personnalisée en vue de la planification, de l'installation ou de la mise à niveau vers Exchange 2013. Des conseils sont disponibles pour plusieurs scénarios, y compris pour un déploiement local, hybride et en nuage.

<!-- end list -->

  - [Active Directory](active-directory-exchange-2013-help.md)  
    Lisez cette rubrique pour savoir comment Exchange 2013 utilise Active Directory et comment votre déploiement Active Directory affecte votre déploiement Exchange.

<!-- end list -->

  - [Détection anti-programmes malveillants](anti-malware-protection-exchange-2013-help.md)  
    Lisez cette rubrique afin de comprendre les options de protection anti-programme malveillant pour Exchange 2013.

<!-- end list -->

  - [Déploiements hybrides Exchange Server](https://technet.microsoft.com/fr-fr/library/jj200581\(v=exchg.150\))  
    Lisez cette rubrique pour savoir comment planifier un déploiement hybride avec Microsoft Office 365 et votre organisation Exchange 2013 locale.

<!-- end list -->

  - [Planification d'une haute disponibilité et d'une résilience de site](planning-for-high-availability-and-site-resilience-exchange-2013-help.md)  
    Lisez cette rubrique pour savoir comment effectuer votre planification de façon à répondre aux exigences en matière de haute disponibilité et de continuité de l'activité.

<!-- end list -->

  - [Intégration à SharePoint et Lync](integration-with-sharepoint-and-lync-exchange-2013-help.md)  
    Lisez cette rubrique pour savoir comment intégrer Exchange 2013, Microsoft SharePoint 2013 et Microsoft Lync 2013 afin d'activer l'archivage inter-produits, la suspension et la découverte électronique ; les boîtes aux lettres de site ; l'authentification ; la présence Lync ; etc.

<!-- end list -->

  - [Planification de la messagerie unifiée](planning-for-unified-messaging-exchange-2013-help.md)  
    Lisez cette rubrique afin d'en savoir plus sur la planification de la messagerie unifiée Exchange 2013.

<!-- end list -->

  - [Options de configuration du stockage Exchange 2013](exchange-2013-storage-configuration-options-exchange-2013-help.md)  
    Lisez cette rubrique pour obtenir des informations sur les architectures de stockage, les types de disques et les configurations de stockage prises en charge par le rôle serveur de boîtes aux lettres Exchange 2013.

<!-- end list -->

  - [Virtualisation d'Exchange 2013](exchange-2013-virtualization-exchange-2013-help.md)  
    Lisez cette rubrique pour en savoir plus sur la procédure de déploiement d'Exchange 2013 dans un environnement virtualisé.

<!-- end list -->

  - [Architecture mutualisée dans Exchange 2013](multi-tenancy-in-exchange-2013-exchange-2013-help.md)  
    Lisez cette rubrique pour en savoir plus sur la manière dont vous pouvez configurer Exchange 2013 afin d’héberger plusieurs organisations ou divisions discrètes qui d’ordinaire ne partagent pas de courriers électroniques, de données, d’utilisateurs, de listes d’adresses globales ni aucun autre objet Exchange couramment utilisé.

<!-- end list -->

  - [Technologies de développement Exchange](https://go.microsoft.com/fwlink/p/?linkid=268448)  
    Cette rubrique contient des informations importantes sur les interfaces de programmation d'applications (API) disponibles pour les applications qui utilisent Exchange 2013.

## Création d'un environnement de test

Avant d'installer Exchange 2013 pour la première fois, nous vous recommandons de l'installer dans un environnement de test isolé. Cette approche réduit le risque de temps mort pour les utilisateurs et d'impact négatif dans l'environnement de production.

L'environnement de test agira en tant que « validation technique » pour votre nouvelle conception Exchange 2013 et permettra de poursuivre ou d'annuler toute implémentation avant d'effectuer le déploiement dans vos environnements de production. Le fait de disposer d'un environnement de test exclusif pour la validation et les tests vous permet d'effectuer des contrôles de pré-installation pour vos environnements de production à venir. En effectuant d'abord l'installation dans un environnement de test, nous pensons que votre organisation réussira l'implémentation dans un environnement de production.

Pour de nombreuses organisations, le coût de la mise en place d'un laboratoire de test risque d'être élevé en raison de la nécessité de dupliquer l'environnement de production. Afin de réduire le coût matériel associé à un laboratoire de prototype, nous vous recommandons d'utiliser la virtualisation à l'aide des technologies Hyper-V Windows Server 2008 R2 ou Windows Server 2012. Hyper-V offre la virtualisation des serveurs en permettant à plusieurs systèmes d'exploitation virtuels de fonctionner sur une seule machine physique.

Pour plus d’informations sur Hyper-V, consultez la rubrique [Virtualisation de serveur](https://go.microsoft.com/fwlink/p/?linkid=117704). Pour plus d’informations sur la prise en charge par Microsoft d’Exchange 2013 dans un environnement de production sur des logiciels de virtualisation de matériel, consultez la section « Virtualisation de matériel » dans la rubrique[Configuration requise pour Exchange 2013](exchange-2013-system-requirements-exchange-2013-help.md).

## Déploiement d’une installation d’Exchange 2013

La phase de déploiement est la période au cours de laquelle vous installez Exchange 2013 dans votre organisation. Avant de commencer une phase de déploiement, vous devez planifier votre organisation Exchange. Pour plus d'informations, consultez la section Planification pour Exchange 2013 plus haut dans cette rubrique.

Utilisez les liens suivants pour accéder aux informations dont vous avez besoin pour déployer Exchange 2013.

  - [Préparation d’Active Directory et des domaines](prepare-active-directory-and-domains-exchange-2013-help.md)  
    Découvrez les étapes à suivre pour préparer votre forêt Active Directory pour Exchange 2013 et connaître les modifications qu'apporte Exchange à votre forêt.

<!-- end list -->

  - [Installer Exchange 2013 à l’aide de l’Assistant Installation](install-exchange-2013-using-the-setup-wizard-exchange-2013-help.md)  
    Suivez les étapes décrites dans cette rubrique pour utiliser l'Assistant Installation d'Exchange 2013, afin d'installer Exchange 2013 dans une nouvelle organisation Exchange.

<!-- end list -->

  - [Installation d’Exchange 2013 en mode sans assistance](install-exchange-2013-using-unattended-mode-exchange-2013-help.md)  
    Suivez les étapes décrites dans cette rubrique pour utiliser l'installation sans assistance d'Exchange 2013, afin d'installer Exchange 2013 dans une nouvelle organisation Exchange.

<!-- end list -->

  - [Installer le rôle de transport Edge d’Exchange 2013 à l’aide de l’Assistant Installation](install-the-exchange-2013-edge-transport-role-using-the-setup-wizard-exchange-2013-help.md)  
    Suivez les étapes de cette rubrique pour utiliser l’Assistant Installation Exchange 2013 afin d’installer le rôle serveur de transport Edge Exchange 2013 dans un réseau de périmètre.

<!-- end list -->

  - [Mettre à niveau Exchange 2013 vers la mise à jour cumulative la plus récente ou vers le Service Pack le plus récent](upgrade-exchange-2013-to-the-latest-cumulative-update-or-service-pack-exchange-2013-help.md)  
    Suivez les étapes décrites dans cette rubrique pour appliquer la mise à jour cumulative la plus récente ou le Service Pack le plus récent pour des serveurs Exchange 2013 dans votre organisation.

<!-- end list -->

  - [Mise à niveau d'Exchange 2010 vers Exchange 2013](upgrade-from-exchange-2010-to-exchange-2013-exchange-2013-help.md)  
    Suivez les étapes décrites dans cette rubrique pour installer Exchange 2013 dans une organisation Exchange 2010 existante.

<!-- end list -->

  - [Mise à niveau d'Exchange 2007 vers Exchange 2013](upgrade-from-exchange-2007-to-exchange-2013-exchange-2013-help.md)  
    Suivez les étapes décrites dans cette rubrique pour installer Exchange 2013 dans une organisation Exchange 2007 existante.

<!-- end list -->

  - [Déploiement de topologies à plusieurs forêts pour Exchange 2013](deploy-multiple-forest-topologies-for-exchange-2013-exchange-2013-help.md)  
    Lisez cette rubrique pour obtenir des informations qui vous aideront à déployer Exchange 2013 dans une organisation contenant plus d'une forêt Active Directory.

<!-- end list -->

  - [Déploiement de la messagerie vocale et la messagerie unifiée](deploying-voice-mail-and-um-exchange-2013-help.md)  
    Lisez cette rubrique pour obtenir des informations qui vous aideront à mieux maîtriser le déploiement de la messagerie unifiée Exchange 2013, qu'il s'agisse d'un nouveau déploiement ou d'une mise à niveau.

<!-- end list -->

  - [Procédures de déploiement hybride](https://technet.microsoft.com/fr-fr/library/jj200788\(v=exchg.150\))  
    Lisez cette rubrique pour obtenir des informations qui vous aideront à déployer Exchange 2013 dans un déploiement hybride existant.

<!-- end list -->

  - [Tâches consécutives à l’installation d’Exchange 2013](exchange-2013-post-installation-tasks-exchange-2013-help.md)  
    Découvrez les tâches de post-installation vous permettant de finaliser votre installation d'Exchange 2013.

## Présentation du programme d'installation de Microsoft Exchange 2013

Vous pouvez opter pour différents types ou modes dans le programme d'installation d'Exchange 2013 pour installer et maintenir sur votre système diverses éditions et versions de Microsoft Exchange 2013.

## Éditions et versions de Microsoft Exchange

Exchange 2013 se décline en deux éditions serveur : Standard Edition et Enterprise Edition. Ces éditions sous licence sont définies par une clé de produit. Pour plus d’informations, consultez la rubrique [Gestion des licences Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=237292).

## Types d'installation de Microsoft Exchange

Vous disposez des options suivantes pour l'installation de Microsoft Exchange 2013 :

  - **Interface utilisateur du programme d'installation d'Exchange**   L'exécution de Setup.exe sans commutateur de ligne de commande est un processus interactif dans lequel vous êtes guidé par l'Assistant Installation d'Exchange 2013.

  - **Installation sans assistance d'Exchange**   L'exécution de Setup.exe avec des commutateurs de ligne de commande vous permet d'installer Exchange à partir d'une ligne de commande interactive ou via un script.

Setup.exe est disponible sur le DVD d'Exchange 2013 ou dans les fichiers source que vous avez téléchargés.

## Modes d'installation de Microsoft Exchange

Le programme d'installation d'Exchange 2013 propose plusieurs modes d'installation :

  - **Install**   Utilisez ce mode pour installer un nouveau rôle serveur ou ajouter un rôle serveur à une installation existante (mode maintenance). Vous pouvez utiliser ce mode dans l'Assistant Installation d'Exchange ou dans l'installation sans assistance.

  - **Uninstall**   Utilisez ce mode pour supprimer l’installation Exchange d’un ordinateur. Vous pouvez utiliser ce mode dans l'Assistant Installation d'Exchange ou dans l'installation sans assistance.

  - **Upgrade**   Sélectionnez ce mode lorsque vous disposez d’une installation existante d’Exchange et que vous installez une mise à jour cumulative ou un Service Pack. Vous pouvez utiliser ce mode dans l'Assistant Installation d'Exchange ou dans l'installation sans assistance.
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Exchange 2013 ne prend pas en charge les mises à niveau sur place à partir des versions précédentes d'Exchange. Ce mode permet uniquement d’installer les mises à jour cumulatives ou Service Packs.</td>
    </tr>
    </tbody>
    </table>


  - **RecoverServer**   Utilisez ce mode lorsqu'un serveur a connu une défaillance irrémédiable et que vous avez besoin de récupérer des données. Vous devez installer un serveur à l'aide du même nom complet de domaine (FQDN) que le serveur défaillant, puis exécuter le programme d'installation avec le commutateur **/m:RecoverServer**. Ne spécifiez pas les rôles à restaurer. Le programme d'installation détecte l'objet serveur Exchange dans Active Directory et installe la configuration et les fichiers correspondants automatiquement. Après avoir récupéré le serveur, vous pouvez restaurer des bases de données et reconfigurer les autres paramètres. Pour fonctionner en mode **RecoverServer**, vous ne pouvez pas installer Exchange sur le serveur. L'objet serveur Exchange doit exister dans Active Directory. Vous pouvez uniquement utiliser ce mode pendant une installation sans assistance.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Vous devez mener à terme un mode d'installation avant d'en utiliser un autre.</td>
</tr>
</tbody>
</table>


## Pour plus d'informations

[Prise en charge du protocole IPv6 dans Exchange 2013](ipv6-support-in-exchange-2013-exchange-2013-help.md)

[Centre d’administration Exchange dans Exchange 2013](exchange-admin-center-in-exchange-2013-exchange-2013-help.md)

[Support linguistique Exchange 2013](exchange-2013-language-support-exchange-2013-help.md)

[Tests de préparation Exchange 2013](exchange-2013-readiness-checks-exchange-2013-help.md)

