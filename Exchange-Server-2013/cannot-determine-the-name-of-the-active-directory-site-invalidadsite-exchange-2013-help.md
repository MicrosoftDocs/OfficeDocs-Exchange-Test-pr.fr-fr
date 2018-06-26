---
title: 'Impossible de déterminer le nom du site Active Directory_InvalidADSite: Exchange 2013 Help'
TOCTitle: Impossible de déterminer le nom du site Active Directory_InvalidADSite
ms:assetid: ef96e077-08a0-4108-9f7d-0d61758abcd4
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/ms.exch.setupreadiness.invalidadsite(v=EXCHG.150)
ms:contentKeyID: 50479529
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Impossible de déterminer le nom du site Active Directory\_InvalidADSite

 

_**Sapplique à :**Exchange Server_

_**Dernière rubrique modifiée :**2016-12-09_

Le contenu de cette rubrique n'a pas été mis à jour pour Microsoft Exchange Server 2013. Bien qu'il n'ait pas été encore mis à jour, il peut toujours être applicable pour Exchange 2013. Si vous avez toujours besoin d'aide, consultez les ressources de communauté ci-dessous.

Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), et [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

Le programme d’installation de Microsoft® Exchange Server 2007 ne peut pas poursuivre son exécution car ce serveur ne semble pas appartenir à un site de service d’annuaire Active Directory® valide.

Le programme d’installation de Microsoft Exchange nécessite que le serveur utilisé pour l’installation d’Exchange 2007 appartienne à un site Active Directory valide.

Pour résoudre ce problème, vérifiez que le serveur local est membre d’un site Active Directory valide, puis recommencez l’installation d’Exchange Server 2007.

Vous pouvez utiliser l’option **/DsGetSite** de l’outil de ligne de commande Nltest.exe afin de vérifier et d’afficher l’appartenance à un site. Pour plus d’informations, voir "Nltest.exe: Présentation de NLTest dans la bibliothèque d’outils et de paramètres de la *référence technique de Windows Server 2003* ([https://go.microsoft.com/fwlink/?LinkId=27734](https://go.microsoft.com/fwlink/?linkid=27734)).

Pour plus d’informations sur le dépannage d’Active Directory, voir la section sur le dépannage des opérations d’Active Directory du guide des opérations de *Windows Server 2003* (<https://go.microsoft.com/fwlink/?linkid=68099>).

