---
title: 'Intégrer des systèmes téléphoniques à la messag. unif.: Exchange 2013 Help | Microsoft Docs'
TOCTitle: Intégration des systèmes téléphoniques à la messagerie unifiée
ms:assetid: b8790117-b040-4c84-9d34-005c75088e76
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ673558(v=EXCHG.150)
ms:contentKeyID: 50555484
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Intégration des systèmes téléphoniques à la messagerie unifiée

 

_**Sapplique à :** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2016-12-09_

Pour déployer correctement une messagerie unifiée, vous devez bien connaître les concepts de téléphonie de base et les composants téléphoniques. Une fois les principes de téléphonie acquis, vous pouvez intégrer la messagerie unifiée à votre organisation Exchange. Les concepts de base et les composants sont les suivants :

  - Réseaux de commutation de circuits et de commutation de paquets

  - PBX (Private Branch eXchange)

  - IP/PBX

  - VoIP (Voice over Internet Protocol)

  - Passerelles VoIP

Dans un environnement local, hybride ou Office 365, la connexion et la configuration des composants téléphoniques requis constituent l'étape la plus complexe et la plus importante du déploiement réussi d'une messagerie unifiée, avec ou sans Lync Server Voix Entreprise. Vous devez connecter et configurer des passerelles VoIP, passerelles VoIP avancées, PBX, PBX IP et contrôleurs de frontière de session (SBC) pour un réseau de téléphonie traditionnel et connecter un réseau téléphonique si vous allez utiliser Microsoft Lync Server et une messagerie unifiée.

La planification et le déploiement d'un nouveau déploiement de messagerie unifiée ou la mise à niveau d'un système de messagerie vocale hérité peut représenter des défis pour les organisations. Cela nécessite une connaissance étendue des passerelles VoIP, des PBX, des PBX IP, de Microsoft Lync Server et de la messagerie unifiée. Selon votre compétence technique dans Exchange et les systèmes de messagerie vocale, vous pourriez souhaiter obtenir l'assistance d'un spécialise de la messagerie unifiée. Un spécialiste en messagerie unifiée Exchange va vous aider à assurer une transition homogène d'un système de messagerie vocale hérité ou tiers vers la messagerie unifiée Exchange. Pour plus d'informations sur comment contacter un spécialiste de la messagerie unifiée, consultez [Microsoft Exchange Server 2013 Unified Messaging (UM) Specialists](http://go.microsoft.com/fwlink/p/?linkid=262708).

## Intégration de votre réseau de téléphonie

La messagerie unifiée nécessite l'intégration de votre déploiement Exchange Server dans votre réseau de téléphonie existant ou l'intégration de la messagerie unifiée dans Microsoft Lync Server pour votre organisation. Pour un déploiement et une gestion réussis de la messagerie vocale de la messagerie unifiée, vous devez effectuer une analyse rigoureuse de votre infrastructure de téléphonie existante ou de votre déploiement Microsoft Lync Server Voix Entreprise et exécuter les étapes de planification nécessaires.

## Passerelles VoIP

Lorsque vous déployez une messagerie unifiée dans une organisation Exchange, vous devez installer, déployer et configurer une passerelle VoIP unique ou plusieurs passerelles VoIP pour qu'elles se connectent aux PBX de votre réseau de téléphonie, ou installer, déployer et configurer des PBX compatibles SIP (Session Initiation Protocol) ou des PBX IP.

Une passerelle VoIP est un périphérique matériel tiers qui connecte un PBX hérité à votre LAN. La passerelle VoIP permet au système PBX de communiquer avec les serveurs Exchange de votre organisation.

La messagerie unifiée s'appuie sur les capacités de la passerelle VoIP pour traduire ou convertir les protocoles basés sur le multiplexage par répartition dans le temps (MRT) ou sur la commutation de circuits comme RNIS et QSIG à partir d'un PBX en des protocoles basés sur IP ou VoIP, comme SIP, RTP (Realtime Transport Protocol) ou T.38 pour la transmission de télécopies en temps réel. La passerelle VoIP fait partie intégrante des fonctionnalités et du fonctionnement de la messagerie unifiée. Elle peut également se connecter à des systèmes PBX qui utilisent VoIP au lieu des protocoles de commutation de circuits du réseau téléphonique public commuté (RTPC).

Le choix approprié en matière de passerelle VoIP, de système IP-PBX, PBX compatible SIP ou contrôleur SBC ne représente que la première partie de l'intégration de votre réseau de téléphonie avec la messagerie unifiée. Vous devez configurer ces appareils pour qu'ils fonctionnent avec la messagerie unifiée. Dans des déploiements locaux et hybrides, vous devez déployer les serveurs d'accès au client et de boîtes aux lettres requis, puis créer et configurer tous les composants de messagerie unifiée nécessaires. Pour Office 365 avec messagerie vocale hébergée, l'installation et la configuration d'un serveur ne sont pas obligatoires. Ces composants vous permettent d'établir la connexion entre votre réseau téléphonique et à commutation de circuits et votre réseau de données IP, et d'activer la messagerie vocale pour les utilisateurs de votre organisation. Pour obtenir plus d'informations et connaître les appareils de téléphonie pris en charge, consultez les ressources suivantes :

  - [Gestionnaire de téléphonie pour Exchange 2013](telephony-advisor-for-exchange-2013-exchange-2013-help.md)

  - [Notes de configuration pour les passerelles VoIP, les PBX IP et les PBX pris en charge](configuration-notes-for-supported-voip-gateways-ip-pbxs-and-pbxs-exchange-2013-help.md)

  - [Notes de configuration pour les contrôleurs de frontière de session pris en charge](configuration-notes-for-supported-session-border-controllers-exchange-2013-help.md)

## Microsoft Lync Server

La messagerie unifiée peut utiliser Microsoft Lync Server pour combiner les fonctions de messagerie vocale, de messagerie instantanée, d'indicateur de présence avancée, de conférence audio/vidéo et de messagerie électronique dans un environnement de communication intégré et familier. La fourniture des fonctions Voix Entreprise aux utilisateurs de votre organisation grâce à l'intégration de la messagerie unifiée et de Microsoft Lync Server présente les avantages suivants :

  - Notifications de présence améliorées grâce à une gamme d'applications qui tiennent les utilisateurs informés de la disponibilité de leurs contacts.

  - L'intégration de la messagerie instantanée, de la messagerie vocale, de la téléconférence, de la messagerie électronique et d'autres modes de communication permettent aux utilisateurs de sélectionner le mode le plus approprié à leur tâche. Les utilisateurs peuvent également passer d'une méthode à une autre en fonction de leurs besoins.

  - Disponibilité des options de communication depuis tout site équipé d'une connexion Internet.

  - Client actif (Microsoft Lync) pour la téléphonie, la messagerie instantanée et la conférence.

  - Continuité de l'expérience utilisateur sur plusieurs périphériques.

Le composant du routage de messagerie unifiée d'Exchange gère le routage entre Lync Server et les serveurs Exchange pour intégrer Lync Server avec des fonctionnalités de messagerie unifiée. Le composant de routage de messagerie unifiée Exchange présent dans Lync Server gère également le reroutage de la messagerie vocale sur le réseau téléphonique public commuté (RTPC) en cas d'indisponibilité des serveurs Exchange. Si vous avez déployé Voix Entreprise sur des sites de succursales et que ces sites ne disposent pas de liaison de réseau étendu (WAN) résiliente avec un site central, l'appareil Survivable Branch Appliance que vous déployez sur le site de de succursale fournit la messagerie vocale aux utilisateurs de la succursale, en cas d'indisponibilité d'une liaison WAN. Lorsque la liaison WAN est indisponible, l'appareil Survivable Branch Appliance procède comme suit :

  - Il réachemine des appels sans réponse sur le réseau téléphonique public commuté (RTPC) vers le serveur de boîtes aux lettres Exchange du site central.

  - Il permet à un utilisateur de récupérer des messages vocaux via le réseau téléphonique public commuté (RTPC).

  - Il met en file d'attente des notifications d'appels en absence, puis les télécharge vers le serveur Exchange lorsque la liaison WAN est restaurée.

Pour plus d'informations sur Microsoft Lync Server, consultez la rubrique [Microsoft Lync Server](https://go.microsoft.com/fwlink/p/?linkid=265752).

> [!WARNING]
> Lors de l'intégration locale de la messagerie unifiée et de Lync Server dans un déploiement local ou hybride, les notifications d'appels en absence ne sont pas disponibles pour les utilisateurs qui ont une boîte aux lettres située sur un serveur de boîtes aux lettres Exchange 2007 ou Exchange 2010. Une notification d'appel en absence est générée lorsqu'un utilisateur se déconnecte avant l'envoi de l'appel vers un serveur de boîtes aux lettres.

