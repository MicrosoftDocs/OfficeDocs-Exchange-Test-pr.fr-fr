---
title: 'Connecter la messag. unifiée à votre système téléphonique: Exchange 2013 Help'
TOCTitle: Connecter la messagerie unifiée pour votre système téléphonique
ms:assetid: 92c3e029-f732-4d6d-b147-2b3006d5f088
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ673544(v=EXCHG.150)
ms:contentKeyID: 50555454
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Connecter la messagerie unifiée pour votre système téléphonique

 

_**Sapplique à :** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2012-11-30_

La messagerie unifiée combine la messagerie vocale et la messagerie électronique dans une boîte aux lettres accessible à partir de nombreux types d’appareils. Les utilisateurs peuvent écouter leurs messages vocaux de leur boîte de réception de messagerie électronique ou à l’aide d’Outlook Voice Access à partir d’un téléphone.

Lorsque vous déployez une messagerie unifiée dans une organisation Microsoft Exchange, vous devez installer, déployer et configurer une passerelle unique ou plusieurs passerelles VoIP (Voice over IP) pour se connecter aux PBX (Private Branch eXchanges) de votre réseau de téléphonie, ou installer, déployer et configurer des PBX compatibles SIP (Session Initiation Protocol) ou des PBX IP. Si vous procédez à une mise à niveau de votre système de messagerie vocale actuel, vous devez déployer les appareils qui se connectent à votre réseau de téléphonie, installer vos serveurs d’accès au client et de boîtes aux lettres Exchange, puis créer les composants de messagerie unifiée requis qui permettent à votre réseau de téléphonie de se connecter à votre réseau de données. Les appels entrants de votre réseau de téléphonie peuvent ainsi se connecter à vos passerelles VoIP, PBX IP ou PBX compatibles SIP, et permettre à ces appareils de se connecter à votre organisation Exchange.

Si vous installez, déployez et configurez Microsoft Office Communications Server 2007 R2 ou Microsoft Lync Server, il n’est pas nécessaire d’utiliser des passerelles VoIP, des PBX IP ni des PBX compatibles SIP pour se connecter directement à la messagerie unifiée Exchange. Au lieu de cela, un serveur de médiation Lync et une passerelle VoIP ou une passerelle VoIP avancée disposant des fonctionnalités d’un serveur de médiation et d’une passerelle VoIP doit vous permettre de vous connecter à la messagerie unifiée Exchange. Les utilisateurs de la messagerie unifiée autorisés sur Enterprise Voice peuvent récupérer, écouter et répondre à des messages vocaux et générer des appels sortants. Ils bénéficient également d’un accès à d’autres fonctions liées à Lync, notamment la présence et la messagerie instantanée en utilisant Office Communicator ou un client Lync.

Les informations suivantes vont vous permettre d’installer et de déployer une messagerie unifiée, puis d’activer des fonctions de messagerie vocale pour les utilisateurs de votre organisation :

  - [Connexion d’une passerelle VoIP, d’un IP PBX ou d’un contrôleur SBC à la messagerie unifiée](connect-a-voip-gateway-ip-pbx-or-session-border-controller-to-um-exchange-2013-help.md)   Pour en savoir plus la connexion des passerelles VoIP ou PBX IP à la messagerie unifiée.

  - [Gestionnaire de téléphonie pour Exchange 2013](https://docs.microsoft.com/fr-fr/exchange/voice-mail-unified-messaging/telephone-system-integration-with-um/telephony-advisor-for-exchange-2013)   Pour en savoir plus sur les passerelles VoIP, PBX IP et PBX pris en charge.

  - [Notes de configuration pour les passerelles VoIP, les PBX IP et les PBX pris en charge](https://docs.microsoft.com/fr-fr/exchange/voice-mail-unified-messaging/telephone-system-integration-with-um/configuration-notes-for-voip-gateways)   Pour en savoir plus sur la configuration de vos passerelles VoIP, PBX IP et PBX.

