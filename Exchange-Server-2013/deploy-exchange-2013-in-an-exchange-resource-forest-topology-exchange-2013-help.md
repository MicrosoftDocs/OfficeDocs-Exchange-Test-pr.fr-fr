---
title: 'Déploiement d’Exchange 2013 dans une topologie de forêt ressource Exchange | Microsoft Docs'
TOCTitle: Déploiement d’Exchange 2013 dans une topologie de forêt ressource Exchange
ms:assetid: 537a7b2b-d002-40a6-84ae-fd02635f9e23
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Aa998031(v=EXCHG.150)
ms:contentKeyID: 51407186
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Déploiement d’Exchange 2013 dans une topologie de forêt ressource Exchange

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2016-12-09_

Cette rubrique décrit la procédure de déploiement de Microsoft Exchange 2013 dans une topologie de forêt ressource Exchange. Une forêt ressource Exchange est également appelée forêt Exchange dédiée. Cette rubrique suppose que vous n’avez pas de topologie Exchange 2013 existante.

La figure suivante montre une organisation Exchange avec une forêt ressource.

**Exemple d’une organisation Exchange avec une forêt ressource Exchange**

![Organisation Exchange complexe avec forêt de ressources](images/Aa998031.706725cf-e520-4b89-a275-acd8fb58943a(EXCHG.150).gif "Organisation Exchange complexe avec forêt de ressources")

## Ce qu’il faut savoir avant de commencer ?

Pour effectuer la procédure suivante dans Exchange 2013, vérifiez ce qui suit :

  - Vous disposez des deux forêts Active Directory suivantes :
    
      - Une forêt contient les comptes d’utilisateurs de votre organisation. Dans cette procédure, cette forêt est appelée *forêt de comptes*.
    
      - Une forêt ne contient pas de compte d’utilisateur et ne dispose pas encore d’Exchange. Dans cette procédure, cette forêt est appelée *forêt Exchange*. Vous allez utiliser la procédure pour installer Exchange 2013 dans cette forêt.

  - Vous avez correctement configuré un DNS (Domain Name System) pour la résolution de noms dans les forêts au sein de votre organisation. Pour vérifier que votre DNS est correctement configuré, effectuez un test ping sur chaque forêt depuis l’autre forêt/les autres forêts de votre organisation. Pour plus d’informations sur la configuration DNS, consultez le [guide des opérations des serveurs DNS](https://go.microsoft.com/fwlink/p/?linkid=282295).

## Déploiement d’Exchange 2013 dans une topologie de forêt ressource Exchange

1.  Depuis un contrôleur de domaine de la forêt Exchange, créez une approbation sortante unidirectionnelle afin que la forêt Exchange approuve la forêt de comptes. Pour obtenir la procédure détaillée, consultez la page [Partenaires Microsoft](https://go.microsoft.com/fwlink/p/?linkid=69130).
    
    > [!NOTE]
    > Bien qu’il soit recommandé de créer une approbation de forêt, vous pouvez également créer une approbation externe. Si vous créez une approbation externe, lorsque vous créez des boîtes aux lettres liées à l’étape 3, dans la page <strong>Compte principal</strong> de l’Assistant Nouvelle boîte aux lettres, vous devez spécifier un compte d’utilisateur pouvant accéder au contrôleur de domaine dans la forêt approuvée. Vous ne pouvez pas utiliser les informations d’identification avec lesquelles vous êtes actuellement connecté. Si vous créez des boîtes aux lettres liées à l’aide de la cmdlet <strong>New-Mailbox</strong>, vous devez spécifier un compte d’utilisateur pouvant accéder au contrôleur de domaine dans la forêt approuvée à l’aide du paramètre <em>LinkedCredential</em>.


2.  Dans la forêt Exchange, installez Exchange 2013. Installez Exchange comme vous le feriez dans le cadre d’un scénario de forêt unique. Pour obtenir la procédure détaillée d’installation d’Exchange 2013, consultez l’une des rubriques suivantes :
    
      - [Déployer une nouvelle installation d’Exchange 2013](deploy-a-new-installation-of-exchange-2013-exchange-2013-help.md)
    
      - [Installer Exchange 2013 à l’aide de l’Assistant Installation](install-exchange-2013-using-the-setup-wizard-exchange-2013-help.md)

3.  Dans la forêt Exchange, pour chaque utilisateur dans la forêt de comptes qui disposera d’une boîte aux lettres dans la forêt Exchange, créez une boîte aux lettres associée à un compte externe. Pour obtenir la procédure détaillée, voir [Gérer les boîtes aux lettres liées](manage-linked-mailboxes-exchange-2013-help.md).

