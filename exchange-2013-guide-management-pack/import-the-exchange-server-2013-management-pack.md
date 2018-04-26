---
title: Importation du pack d'administration Exchange Server 2013
TOCTitle: Importation du pack d'administration Exchange Server 2013
ms:assetid: dc929928-61b8-448b-9ae5-d3fa73a18ee9
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dn195914(v=EXCHG.150)
ms:contentKeyID: 53275527
ms.date: 01/09/2015
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Importation du pack d'administration Exchange Server 2013

 

_**Dernière rubrique modifiée :** 2013-03-30_

Nous allons commencer par aborder l'importation du pack d'administration dans votre déploiement SCOM.

## Conditions préalables

Pour pouvoir importer le pack d'administration, les conditions suivantes doivent être remplies :

  - L'une des versions suivantes de System Center Operations Manager est déployée dans votre organisation :
    
      - System Center Operations Manager 2012 RTM ou version ultérieure
    
      - System Center Operations Manager 2007 R2 ou version ultérieure

  - Vous avez déjà déployé des agents SCOM sur vos serveurs Exchange. [Vérification de l'état de déploiement de l'agent](procedures-related-to-deployment.md).

  - Les agents SCOM sur vos serveurs Exchange sont exécutés sous le compte système local. [Vérification de la configuration de sécurité de l'agent](procedures-related-to-deployment.md).

  - Les agents SCOM sur vos serveurs Exchange sont configurés pour agir en tant que proxy et découvrir les objets gérés sur d'autres ordinateurs. [Vérification de la configuration du proxy de l'agent](procedures-related-to-deployment.md).

  - Votre compte d'utilisateur est membre du rôle Administrateurs Operations Manager.

## Importer le pack d'administration Exchange Server 2013

Respectez les étapes suivantes pour importer le pack d'administration Exchange Server 2013 Cette procédure suppose que vous avez extrait le contenu du pack d'administration vers un disque local sur votre serveur SCOM (System Center Operations Manager). Vous pouvez télécharger le pack d'administration Exchange Server 2013 sur.

1.  Connectez-vous à votre serveur SCOM, puis téléchargez le pack d'administration Exchange Server 2013 à partir du [Centre de téléchargement Microsoft](http://go.microsoft.com/fwlink/p/?linkid=268587).

2.  Extrayez le contenu du pack d'administration vers un dossier de votre système en exécutant le fichier `ExchangeServerManagementPack.msi`.

3.  Démarrez la console de gestion SCOM. Dans la console SCOM, cliquez sur **Administration**.

4.  Cliquez avec le bouton droit sur **Packs d'administration**, puis sélectionnez **Importer des packs d'administration**.

5.  L'Assistant Importation de packs d'administration s'ouvre. Cliquez sur **Ajouter**, puis cliquez sur **Ajouter à partir du disque**.

6.  La boîte de dialogue **Sélectionner les packs d'administration à importer** s'affiche. Recherchez le répertoire où vous avez extrait le pack d'administration. Cliquez sur le fichier `Microsoft.Exchange.15.mp`, puis sur **Ouvrir**.

7.  Dans la page **Sélectionner les packs d'administration**, le pack d'administration Exchange Server 2013 est répertorié. Cliquez sur **Installer**.

8.  La page **Importer des packs d'administration** apparaît et affiche la progression. Si un problème survient à une étape du processus d'importation, sélectionnez le pack d'administration dans la liste pour afficher les détails de l'état.

9.  Une fois l'importation terminée, cliquez sur **Fermer**.

10. Cliquez sur **Affichage** puis sur **Actualiser**, ou appuyez sur F5, pour afficher le pack d'administration Microsoft Exchange Server 2013 dans la liste des packs d'administration.

Maintenant que le pack d'administration est importé, consultez la rubrique [Mise en route avec le pack d'administration Exchange Server 2013](getting-started-with-exchange-server-2013-management-pack.md) pour en savoir plus sur le nouveau tableau de bord.

