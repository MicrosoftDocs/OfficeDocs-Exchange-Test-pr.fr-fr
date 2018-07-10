---
title: 'Ce serveur est la source d’un connecteur d’envoi_ServerIsSourceForSendConnector: Exchange 2013 Help'
TOCTitle: Ce serveur est la source d’un connecteur d’envoi_ServerIsSourceForSendConnector
ms:assetid: 151c0014-c90c-4c52-8e74-4b3f1bc7aaf1
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/ms.exch.setupreadiness.serverissourceforsendconnector(v=EXCHG.150)
ms:contentKeyID: 50477655
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Ce serveur est la source d’un connecteur d’envoi\_ServerIsSourceForSendConnector

 

_**Sapplique à :** Exchange Server_

_**Dernière rubrique modifiée :** 2016-12-09_

Le contenu de cette rubrique n'a pas été mis à jour pour Microsoft Exchange Server 2013. Bien qu'il n'ait pas été encore mis à jour, il peut toujours être applicable pour Exchange 2013. Si vous avez toujours besoin d'aide, consultez les ressources de communauté ci-dessous.

Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), et [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

Le programme d’installation de Microsoft Exchange Server 2007 ne peut pas poursuivre son exécution car sa tentative de supprimer le rôle serveur de transport Hub a échoué. L’ordinateur local est la source pour un ou plusieurs connecteurs d’envoi dans l’organisation Exchange.

Un connecteur d’envoi constitue une passerelle logique via laquelle les messages sortants sont envoyés.

Le programme d’installation d’Exchange 2007 nécessite que tous les connecteurs d’envoi pour une organisation Exchange soient déplacés ou supprimés du serveur de transport Hub avant de pouvoir supprimer le rôle serveur.

Pour résoudre ce problème, déplacez ou supprimez tous les connecteurs d’envoi de l’ordinateur local puis réexécutez le programme d’installation.

Pour plus d’informations sur la modification ou la suppression de connecteurs d’envoi, voir les rubriques suivantes dans la documentation sur le produit Exchange Server 2007 :

  - « Procédure de suppression d’un connecteur d’envoi » ([https://go.microsoft.com/fwlink/?LinkId=86655](https://go.microsoft.com/fwlink/?linkid=86655)).

  - « Procédure de modification de la configuration d’un connecteur d’envoi » ([https://go.microsoft.com/fwlink/?LinkId=86656](https://go.microsoft.com/fwlink/?linkid=86656)).

