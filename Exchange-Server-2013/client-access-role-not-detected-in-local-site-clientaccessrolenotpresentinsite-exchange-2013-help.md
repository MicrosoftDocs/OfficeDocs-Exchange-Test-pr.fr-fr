---
title: 'Client Access role not detected in local site_ClientAccessRoleNotPresentInSite: Exchange 2013 Help'
TOCTitle: Client Access role not detected in local site_ClientAccessRoleNotPresentInSite
ms:assetid: b5bfc6af-9c55-46c0-a293-6078b64e87dd
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/ms.exch.setupreadiness.clientaccessrolenotpresentinsite(v=EXCHG.150)
ms:contentKeyID: 50479040
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Client Access role not detected in local site\_ClientAccessRoleNotPresentInSite

 

_**Sapplique à :** Exchange Server_

_**Dernière rubrique modifiée :** 2012-06-05_

Le contenu de cette rubrique n'a pas été mis à jour pour Microsoft Exchange Server 2013. Bien qu'il n'ait pas été encore mis à jour, il peut toujours être applicable pour Exchange 2013. Si vous avez toujours besoin d'aide, consultez les ressources de communauté ci-dessous.

Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), et [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

Microsoft® Exchange Server 2007 setup displayed this warning because an existing Client Access role could not be detected in the local Active Directory® directory service site.

You have chosen to install the Mailbox Server role before an instance of the Client Access role is installed in the Active Directory site.

The Client Access server role accepts connections to your Exchange 2007 server from a variety of different clients. Software clients such as Microsoft Outlook Express and Eudora use POP3 or IMAP4 connections to communicate with the Exchange server. Hardware clients, such as mobile devices, use ActiveSync, POP3, or IMAP4 to communicate with the Exchange server.

If users access their Inbox by using any client other than Microsoft Office Outlook®, you must install the Client Access server role in your Exchange organization.

Users will be able to logon to their mailboxes with Outlook but will not be able to use Outlook Web Access or mobile devices against the same mailbox until a Client Access role is present in the local Active Directory site.

