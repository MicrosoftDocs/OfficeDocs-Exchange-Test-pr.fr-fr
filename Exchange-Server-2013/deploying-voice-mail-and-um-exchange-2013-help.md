---
title: 'Déployer la messagerie vocale et la messagerie unifiée: Exchange 2013 Help'
TOCTitle: Déploiement de la messagerie vocale et la messagerie unifiée
ms:assetid: 3df61b62-a1e4-41fb-969c-319189ae4e42
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ673519(v=EXCHG.150)
ms:contentKeyID: 50477980
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Déploiement de la messagerie vocale et la messagerie unifiée

 

_**Sapplique à :** Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2016-12-09_

La messagerie unifiée (MU) Microsoft Exchange vous permet d’offrir des services de messagerie vocale aux utilisateurs de votre organisation. Lors du déploiement de la messagerie unifiée, vous devez intégrer votre déploiement Exchange Server au circuit de téléphonie existant de votre organisation ou à Microsoft Lync Server. Un déploiement réussi nécessite une analyse attentive de votre infrastructure de téléphonie existante et d’effectuer les étapes de planification appropriées pour déployer et gérer la messagerie vocale dans la messagerie unifiée. Si vous intégrez Exchange à Lync Server, vous devez également vous familiariser avec ce produit.

Lorsque vous déployez la messagerie unifiée, plusieurs options s’offrent à vous, selon le matériel téléphonique disponible dans votre organisation. Si vous connectez la messagerie unifiée à votre réseau téléphonique, il est possible que votre organisation dispose de l’une des configurations téléphoniques suivantes :

  - Une ou plusieurs passerelles VoIP avec un ou plusieurs PBX

  - Un ou plusieurs PBX IP

  - Un ou plusieurs PBX à extension SIP

  - Microsoft Office Communications Server 2007 R2 ou Microsoft Lync Server 2010 ou 2013

> [!WARNING]
> Lorsque vous déployez la messagerie unifiée Exchange dans un environnement hébergé ou hybride, vous devez déployer des contrôleurs de frontière de session (SBC). Les SBC ne permettent pas à la messagerie unifiée de se connecter à un réseau téléphonique ou de fournir une tonalité à une organisation. Cependant, ils connectent votre déploiement de messagerie unifiée local à un centre de données à l’aide du protocole IP sur un réseau WAN public ou privé.


**Matériel de téléphonie**   Le bon choix en matière de passerelle VoIP, PBX IP ou contrôleur SBC ne constitue que la première étape du processus d’intégration de votre réseau de téléphonie à la messagerie unifiée. Vous devez configurer ces périphériques pour qu’ils fonctionnent avec la messagerie unifiée, déployer les serveurs d’accès au client et les serveurs de boîtes aux lettres requis, et créer et configurer tous les composants de messagerie unifiée nécessaires. Ces composants vous permettent de connecter votre réseau de protocole basé sur un circuit à votre réseau de données IP et activer la messagerie vocale pour les utilisateurs de votre organisation. Pour plus d’informations, consultez la rubrique [Gestionnaire de téléphonie pour Exchange 2013](https://docs.microsoft.com/fr-fr/exchange/voice-mail-unified-messaging/telephone-system-integration-with-um/telephony-advisor-for-exchange-2013).

**Microsoft Lync Server**   La messagerie unifiée peut utiliser Microsoft Lync Server pour faire converger les fonctions de messagerie vocale, de messagerie instantanée, d’indicateur de présence amélioré, de conférence audio/vidéo et de messagerie électronique dans un environnement de communication intégré et familier. L’intégration de la messagerie unifiée et de Lync Server présente les avantages suivants :

  - Notifications de présence améliorées grâce à une gamme d'applications qui tiennent les utilisateurs informés de la disponibilité de leurs contacts.

  - Intégration de la messagerie instantanée, de la messagerie vocale, de la téléconférence, de la messagerie électronique et d’autres méthodes de communication permettant aux utilisateurs de sélectionner la méthode la mieux adaptée à leur tâche. Les utilisateurs peuvent également passer d’une méthode à une autre en fonction de leurs besoins.

  - Disponibilité des options de communication depuis tout site équipé d'une connexion Internet.

  - Client actif (Microsoft Lync) pour la téléphonie, la messagerie instantanée et la conférence.

  - Continuité de l’expérience utilisateur sur plusieurs périphériques.

Pour plus d’informations sur Lync Server, consultez la page [Microsoft Lync Server](https://go.microsoft.com/fwlink/p/?linkid=265752).

## Étapes de déploiement

De nombreuses options de déploiement sont possibles pour la messagerie unifiée. Chaque option possède plusieurs étapes en commun qui sont obligatoires pour créer un système évolutif à haute disponibilité prenant en charge des nombres importants d’utilisateurs. Ces étapes sont les suivantes :

1.  Déployez et configurez vos composants de téléphonie ou Microsoft Lync Server pour la messagerie unifiée.

2.  Vérifiez que vous avez installé correctement les serveurs d’accès au client et de boîtes aux lettres nécessaires pour la messagerie unifiée.
    
    > [!WARNING]
    > Vous devez déployer au moins un serveur de boîtes aux lettres Exchange 2013 dans votre organisation avant de configurer les passerelles VoIP ou les PBX IP pour envoyer le trafic SIP ou RTP de messagerie unifiée vers les serveurs d’accès client Exchange 2013.


3.  Créez et configurez les composants de messagerie unifiée requis, notamment les plans de numérotation, les passerelles IP, les groupements de postes et les stratégies de boîte aux lettres de messagerie unifiée.

4.  Procédez aux tâches postérieures au déploiement, notamment le déploiement des certificats pour l’authentification TLS, la création des standards automatiques de messagerie unifiée et les fonctionnalités propres au client.

Pour obtenir des informations détaillées sur le déploiement de la messagerie unifiée, voir [Déploiement de la messagerie unifiée Exchange 2013](deploy-exchange-2013-um-exchange-2013-help.md).

Si vous intégrez votre environnement de messagerie unifiée à Office Communications Server, plusieurs éléments supplémentaires sont à prendre en compte pour la planification. Pour plus d’informations, consultez la rubrique [Présentation du déploiement de la messagerie unifiée Exchange 2013 et de Lync Server](deploying-exchange-2013-um-and-lync-server-overview-exchange-2013-help.md).

