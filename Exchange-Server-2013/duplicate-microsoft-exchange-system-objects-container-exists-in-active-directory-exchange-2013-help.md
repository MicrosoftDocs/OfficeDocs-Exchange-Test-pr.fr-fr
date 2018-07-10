---
title: "Un conteneur d'objets système Microsoft Exchange dupliqué existe dans Active Directory: Exchange 2013 Help"
TOCTitle: Un conteneur d'objets système Microsoft Exchange dupliqué existe dans Active Directory
ms:assetid: cd0f45ab-89de-4653-b50d-c1157c2329d5
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/ms.exch.setupreadiness.adiniterrorrule(v=EXCHG.150)
ms:contentKeyID: 50479252
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Un conteneur d'objets système Microsoft Exchange dupliqué existe dans Active Directory

 

_**Sapplique à :** Exchange Server_

_**Dernière rubrique modifiée :** 2013-02-18_

Le programme d'installation de Microsoft Exchange Server 2013 ne peut pas continuer, car il a détecté un conteneur d'objets système Microsoft Exchange dupliqué dans le contexte d'appellation de domaine Active Directory. Quand le programme d'installation détecte un conteneur d'objets système Microsoft Exchange dupliqué, vous devez supprimer le conteneur dupliqué avant de pouvoir continuer l'installation. S'il existe un conteneur d'objets système Microsoft Exchange dupliqué, vous ne pouvez pas résoudre le problème en réexécutant **DomainPrep**. Vous devez identifier et supprimer le conteneur dupliqué qui est incorrect.

Pour résoudre ce problème, procédez comme suit :

1.  Connectez-vous au contrôleur de domaine avec des informations d'identification d'administrateur.

2.  Dans **Outils d'administration**, cliquez sur **Utilisateurs et ordinateurs Active Directory**.

3.  Dans le volet de la console de gestion **Utilisateurs et ordinateurs Active Directory**, cliquez sur le menu **Affichage** dans la barre d'outils et sélectionnez **Fonctionnalités avancées**.

4.  Localisez le conteneur d'objets système Microsoft Exchange dupliqué.

5.  Vérifiez que ce conteneur dupliqué ne contient pas d'objets Active Directory valides.

6.  Cliquez avec le bouton droit sur le conteneur d'objets système Microsoft Exchange dupliqué qui est incorrect, puis cliquez sur **Supprimer**.

7.  Confirmez la suppression en cliquant sur **Oui** dans la boîte de dialogue Active Directory.

> [!NOTE]
> Si vous souhaitez que la modification soit immédiatement répliquée, vous devez démarrer manuellement la réplication entre les contrôleurs de domaine.


Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), et [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

Avez-vous trouvé ce que vous cherchez ? Veuillez prendre une minute pour [nous envoyer votre avis à l'adresse](mailto:exsetuphelpfeedback@microsoft.com?subject=exchange%202013%20setup%20help%20feedback) au sujet des informations que vous souhaitiez y trouver.

