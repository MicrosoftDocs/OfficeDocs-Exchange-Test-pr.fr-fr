---
title: 'Hub Transport role not detected in local site_BridgeheadRoleNotPresentInSite: Exchange 2013 Help'
TOCTitle: Hub Transport role not detected in local site_BridgeheadRoleNotPresentInSite
ms:assetid: f318c947-81a8-4c18-975a-0f1e7868042a
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/ms.exch.setupreadiness.bridgeheadrolenotpresentinsite(v=EXCHG.150)
ms:contentKeyID: 50479553
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Hub Transport role not detected in local site\_BridgeheadRoleNotPresentInSite

 

_**Sapplique à :** Exchange Server_

_**Dernière rubrique modifiée :** 2012-06-05_

Le contenu de cette rubrique n'a pas été mis à jour pour Microsoft Exchange Server 2013. Bien qu'il n'ait pas été encore mis à jour, il peut toujours être applicable pour Exchange 2013. Si vous avez toujours besoin d'aide, consultez les ressources de communauté ci-dessous.

Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), et [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

Microsoft® Exchange Server 2007 setup displays this warning because an existing Hub Transport server role could not be detected in the local Active Directory® directory service site.

You have chosen to install the Mailbox Server role before an instance of the Hub Transport role is installed in the Active Directory site.

Exchange 2007 Hub Transport Services are deployed inside your organization's Active Directory. Hub Transport Services handle all mail flow inside the organization, applies organizational mail flow routing rules, and are responsible for delivering messages to a recipient's mailbox.

Users will be able to log on to their mailboxes, but mail cannot be sent or received from this mailbox server until a Hub Transport role is installed.

