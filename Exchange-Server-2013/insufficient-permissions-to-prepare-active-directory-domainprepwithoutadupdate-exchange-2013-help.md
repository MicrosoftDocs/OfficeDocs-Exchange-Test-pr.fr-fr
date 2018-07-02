---
title: 'Autorisations insuffisantes pour préparer Active Directory_DomainPrepWithoutADUpdate: Exchange 2013 Help'
TOCTitle: Autorisations insuffisantes pour préparer Active Directory_DomainPrepWithoutADUpdate
ms:assetid: 4283c4b9-983f-460e-a5de-42b2772eae0d
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/ms.exch.setupreadiness.domainprepwithoutadupdate(v=EXCHG.150)
ms:contentKeyID: 50477982
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Autorisations insuffisantes pour préparer Active Directory\_DomainPrepWithoutADUpdate

 

_**Sapplique à :**Exchange Server_

_**Dernière rubrique modifiée :**2016-12-09_

Le contenu de cette rubrique n'a pas été mis à jour pour Microsoft Exchange Server 2013. Bien qu'il n'ait pas été encore mis à jour, il peut toujours être applicable pour Exchange 2013. Si vous avez toujours besoin d'aide, consultez les ressources de communauté ci-dessous.

Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), et [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

Le programme d’installation de Microsoft Exchange Server 2007 ne peut pas poursuivre son exécution car la tentative de préparation de domaine a échoué.

Le programme d’installation d’Exchange nécessite que le service d’annuaire Active Directory soit modifié pour Exchange Server 2007 avant de pouvoir préparer des domaines dans Active Directory.

Le compte utilisé pour exécuter la commande **setup /PrepareAD** ne dispose pas des autorisations suffisantes pour exécuter cette commande même s’il semble appartenir au groupe Administrateurs de l’entreprise. Le compte peut avoir expiré.

Pour résoudre ce problème, vérifiez que le compte de l’utilisateur connecté est valide et appartient au groupe Administrateurs de l’entreprise, ou connectez-vous à l’aide d’un compte qui dispose de ces autorisations et réexécutez **setup /PrepareAD**.

Pour plus d’informations sur la façon d’exécuter le processus PrepareAD, reportez-vous à la section « Comment pour préparer Active Directory et domaines » ([https://go.microsoft.com/fwlink/?LinkId=78453](https://go.microsoft.com/fwlink/?linkid=78453)).

Pour plus d’informations sur les autorisations Active Directory nécessaires avec Microsoft Exchange, reportez-vous à la section « Travailler avec Active Directory des autorisations dans Exchange Server » ([https://go.microsoft.com/fwlink/?LinkId=47592](https://go.microsoft.com/fwlink/?linkid=47592)).

