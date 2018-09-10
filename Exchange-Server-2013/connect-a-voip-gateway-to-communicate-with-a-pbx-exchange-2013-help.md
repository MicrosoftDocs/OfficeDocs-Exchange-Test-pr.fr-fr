---
title: 'Connecter une psrl voix sur IP pour dialoguer avec un PBX: Exchange 2013 Help'
TOCTitle: Connecter une passerelle voix sur IP pour communiquer avec un PBX
ms:assetid: 76bcdc54-3ec2-408a-bdbe-37826580dd62
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Aa998872(v=EXCHG.150)
ms:contentKeyID: 50555428
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Connecter une passerelle voix sur IP pour communiquer avec un PBX

 

_**Sapplique à :** Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2016-12-15_

Lorsque vous configurez vos réseaux de téléphonie et de données pour une messagerie unifiée dans Microsoft Exchange Server 2013, vous devez configurer les passerelles VoIP pour leur permettre de communiquer avec les serveurs d’accès au client qui exécutent le service Routeur d’appel de messagerie unifiée de Microsoft Exchange et avec les serveurs de boîtes aux lettres qui exécutent le service de messagerie unifiée de Microsoft Exchange. Vous devez également configurer les passerelles VoIP pour leur permettre de communiquer avec les PBX (Private Branch eXchange) au sein de votre organisation. Vous pouvez utiliser les informations et liens de cette rubrique pour configurer une passerelle VoIP et permettre ainsi la communication avec un PBX.

## Configuration d’une passerelle VoIP

Lorsque vous configurez une passerelle VoIP, vous devez déterminer si celle-ci est analogique, numérique ou les deux. Si l’interface de la passerelle VoIP qui se connecte à un PBX est analogique, vous devez correctement configurer les paramètres adéquats pour permettre à la passerelle VoIP de communiquer avec un PBX. Si l’interface de la passerelle VoIP qui se connecte à un PBX est numérique, il se peut qu’aucune configuration supplémentaire ne soit requise pour permettre à l’interface numérique de communiquer avec un PBX.

Les ressources suggérées suivantes de Microsoft Exchange TechCenter fournissent des informations qui vous permettent de configurer correctement vos passerelles VoIP et vos PBX :

  - **Documentation sur la passerelle VoIP, le PBX IP et le PBX pris en charge**   [Gestionnaire de téléphonie pour Exchange 2013](https://docs.microsoft.com/fr-fr/exchange/voice-mail-unified-messaging/telephone-system-integration-with-um/telephony-advisor-for-exchange-2013) inclut des fichiers de configuration et des informations d’installation que vous pouvez utiliser lors de la configuration des passerelles VoIP et des PBX.

  - **Notes de configuration et techniques**   [Notes de configuration pour les passerelles VoIP, les PBX IP et les PBX pris en charge](configuration-notes-for-supported-voip-gateways-ip-pbxs-and-pbxs-exchange-2013-help.md) inclut des fichiers de configuration et des informations d’installation que vous pouvez utiliser lors de la configuration des passerelles VoIP et des PBX.

  - **Configuration d’une passerelle VoIP AudioCodes**  La [page des ressources de serveur Microsoft Exchange](https://www.audiocodes.com/solutions/microsoft/exchange-server) fournit des informations concernant la prise en charge et la configuration pour vous permettre de configurer des passerelles VoIP AudioCodes en vue d’une utilisation avec la messagerie unifiée.

  - **Configuration d’une passerelle VoIP Dialogic**   Les dernières informations relatives à la prise en charge et la configuration des passerelles VoIP Dialogic sont disponibles sur le [site web de Dialogic](https://www.dialogic.com/)

Il est conseillé que tous les clients qui projettent de déployer la messagerie unifiée sollicitent l’assistance d’un spécialiste en messagerie unifiée. Un spécialise de messagerie unifiée Exchange va vous aider à vous assurer que la mise à niveau vers la messagerie unifiée à partir d’un système de messagerie vocale hérité ou tiers soit effectuée en douceur, et il vous aidera à planifier et à déployer un nouveau système de messagerie vocale grâce à la messagerie unifiée d’Exchange. Le déploiement d’un nouveau système de messagerie vocale ou la mise à niveau d’un système de messagerie vocale hérité nécessite une très bonne connaissance des passerelles VoIP, des PBX et de la messagerie unifiée. Pour plus d’informations sur la manière de contacter un spécialiste de la messagerie unifiée, consultez [Microsoft Exchange Server 2013 Unified Messaging (UM) Specialists](https://go.microsoft.com/fwlink/p/?linkid=262708) ou les partenaires de messagerie unifiée agréés dans [Microsoft Pinpoint](https://go.microsoft.com/fwlink/p/?linkid=261951).

## Pour plus d'informations

[Notes de configuration pour les passerelles VoIP, les PBX IP et les PBX pris en charge](configuration-notes-for-supported-voip-gateways-ip-pbxs-and-pbxs-exchange-2013-help.md)

[Connecter la messagerie unifiée à une passerelle VoIP pris en charge](connect-um-to-a-supported-voip-gateway-exchange-2013-help.md)

