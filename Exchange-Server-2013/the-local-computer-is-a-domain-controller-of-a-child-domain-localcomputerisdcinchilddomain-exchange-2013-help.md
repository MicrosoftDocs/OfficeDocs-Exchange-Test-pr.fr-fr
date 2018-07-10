---
title: 'L’ordinateur local est un contrôleur de domaine d’un domaine enfant_LocalComputerIsDCInChildDomain: Exchange 2013 Help'
TOCTitle: L’ordinateur local est un contrôleur de domaine d’un domaine enfant_LocalComputerIsDCInChildDomain
ms:assetid: 7db1dcc0-d953-41b8-b081-2a47a70950c4
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/ms.exch.setupreadiness.localcomputerisdcinchilddomain(v=EXCHG.150)
ms:contentKeyID: 50478561
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# L’ordinateur local est un contrôleur de domaine d’un domaine enfant\_LocalComputerIsDCInChildDomain

 

_**Sapplique à :** Exchange Server_

_**Dernière rubrique modifiée :** 2012-06-05_

Le contenu de cette rubrique n'a pas été mis à jour pour Microsoft Exchange Server 2013. Bien qu'il n'ait pas été encore mis à jour, il peut toujours être applicable pour Exchange 2013. Si vous avez toujours besoin d'aide, consultez les ressources de communauté ci-dessous.

Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), et [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

Le programme d’installation de Microsoft® Exchange Server 2007 ne peut pas poursuivre son exécution car l’ordinateur local est un contrôleur de domaine pour un domaine enfant.

Le programme d’installation d’Exchange 2007 ne peut pas effectuer d’installation sur un contrôleur de domaine pour un domaine enfant, sauf si ce contrôleur de domaine est un serveur de catalogue global.

Pour résoudre ce problème, élevez le contrôleur de domaine au rang de serveur de catalogue global ou installez Exchange 2007 sur un ordinateur qui n’est pas contrôleur de domaine, un serveur membre, dans le domaine enfant, puis recommencez l’installation de Microsoft Exchange.

Correction de cet avertissement en faisant du serveur Exchange un serveur de catalogue global

1.  Sur le contrôleur de domaine, cliquez sur **Démarrer**, pointez sur **Programmes**, cliquez sur **Outils d’administration**, puis cliquez sur **Sites et services Active Directory**.

2.  Dans l’arborescence de la console, double-cliquez sur **Sites**, sur le nom du site, puis sur **Serveurs**.

3.  Double-cliquez sur le contrôleur de domaine cible.

4.  Dans le volet des résultats, cliquez avec le bouton droit sur **Paramètres NTDS**, puis cliquez sur **Propriétés**.

5.  Sous l’onglet **Général**, activez la case à cocher **Catalogue global**.

6.  Redémarrez le contrôleur de domaine.

