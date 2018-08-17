---
title: 'L’installation du premier serveur Exchange de l’org. ne peut pas être déléguée'
TOCTitle: L'installation du premier serveur Exchange de l'organisation ne peut pas être déléguée
ms:assetid: 0f4c5b2f-85ae-4160-9a53-f4b890d8ccdb
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/ms.exch.setupreadiness.delegatedfrontendtransportfirstinstall(v=EXCHG.150)
ms:contentKeyID: 50477508
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# L'installation du premier serveur Exchange de l'organisation ne peut pas être déléguée

 

_**Sapplique à :** Exchange Server_

_**Dernière rubrique modifiée :** 2014-11-05_

Impossible de poursuivre le programme d'installation de Microsoft Exchange Server 2013, car l'utilisateur connecté ne dispose pas des autorisations de compte requises pour installer le premier serveur Exchange 2013 dans l'organisation.

Bien que le programme d'installation d'Exchange 2013 autorise l'utilisation de la délégation pour installer des rôles serveur successifs, l'utilisateur doit être connecté en tant que membre du groupe de sécurité Administrateurs de l'entreprise Windows lors de l'installation du premier serveur Exchange 2013 dans l'organisation. Il s'agit d'une condition indispensable, car le programme d'installation d'Exchange 2013 crée et configure les objets du conteneur de l'organisation Exchange dans Active Directory au cours de l'installation.

> [!NOTE]
> Si vous n'avez pas préparé le schéma Active Directory pour Exchange 2013, l'utilisateur connecté doit aussi être membre du groupe de sécurité Administrateurs du schéma Windows. Il est également possible pour un autre utilisateur membre de ce même groupe de sécurité de préparer le schéma Active Directory avant l'installation d'Exchange 2013.


Pour résoudre ce problème, ajoutez l'utilisateur connecté en tant que membre du groupe de sécurité Administrateurs de l'entreprise. Vous pouvez également vous connecter à un compte membre du groupe de sécurité Administrateurs de l'entreprise. Réexécutez ensuite le programme d'installation Exchange 2013.

Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), et [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

Avez-vous trouvé ce que vous cherchez ? Veuillez prendre une minute pour [nous envoyer votre avis à l'adresse](mailto:exsetuphelpfeedback@microsoft.com?subject=exchange%202013%20setup%20help%20feedback) au sujet des informations que vous souhaitiez y trouver.

