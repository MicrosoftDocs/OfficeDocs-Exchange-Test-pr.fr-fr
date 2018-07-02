---
title: 'Désinstaller les modules linguistiques de messagerie unifiée_AdditionalUMLangPackExists: Exchange 2013 Help'
TOCTitle: Désinstaller les modules linguistiques de messagerie unifiée_AdditionalUMLangPackExists
ms:assetid: 3a7e2621-0553-44f5-8029-c72fea25af3c
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/ms.exch.setupreadiness.additionalumlangpackexists(v=EXCHG.150)
ms:contentKeyID: 50477933
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Désinstaller les modules linguistiques de messagerie unifiée\_AdditionalUMLangPackExists

 

_**Sapplique à :** Exchange Server_

_**Dernière rubrique modifiée :** 2016-12-09_

Le contenu de cette rubrique n'a pas été mis à jour pour Microsoft Exchange Server 2013. Bien qu'il n'ait pas été encore mis à jour, il peut toujours être applicable pour Exchange 2013. Si vous avez toujours besoin d'aide, consultez les ressources de communauté ci-dessous.

Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), et [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

Le programme d’installation de Microsoft Exchange Server 2007 ne peut pas poursuivre son exécution car la mise à niveau du rôle serveur de messagerie unifiée a échoué.

L’installation d’Exchange nécessite que tous les modules linguistiques du rôle serveur de messagerie unifiée, excepté le module linguistique Anglais des États-Unis, soient désinstallés avant de pouvoir poursuivre la mise à niveau du rôle serveur de messagerie unifiée.

Les modules linguistiques de messagerie unifiée inclus dans Exchange 2007 contiennent des messages d’assistance vocaux préenregistrés et une aide de conversion de texte par synthèse vocale pour une langue donnée.

Les modules linguistiques de messagerie unifiée d’Exchange 2007 permettent aux appelants et aux utilisateurs d’Outlook Voice Access d’interagir avec le système de messagerie unifiée dans plusieurs langues.

Les modules linguistiques existants autres que celui pour l’Anglais des États-Unis doivent être désinstallés afin de pouvoir installer de nouveaux modules linguistiques.

Pour résoudre ce problème, désinstallez tous les modules linguistiques du rôle serveur de messagerie unifiée, excepté le module linguistique Anglais des États-Unis, et réexécutez le programme d’installation d’Exchange 2007.

Pour plus d’informations sur la désinstallation des modules linguistiques du rôle serveur de messagerie unifiée, consultez la rubrique [Procédure de suppression d’un module linguistique de messagerie unifiée d’un serveur de messagerie unifiée](https://go.microsoft.com/fwlink/?linkid=85973) dans la documentation sur le produit Exchange 2007.

