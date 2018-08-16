---
title: 'Gestionnaire de télécopies pour messag. unifiée Exchange: Exchange 2013 Help'
TOCTitle: Gestionnaire de télécopies pour la messagerie unifiée Exchange
ms:assetid: 928a466d-cc0c-4160-bd4c-f0fc76b038d4
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Ee364747(v=EXCHG.150)
ms:contentKeyID: 52057119
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Gestionnaire de télécopies pour la messagerie unifiée Exchange

 

_**Sapplique à :** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2016-12-09_

La messagerie unifiée Microsoft repose sur des solutions de partenaires de télécopie agréés pour des fonctionnalités de télécopie améliorées, telles que la télécopie sortante ou le routage de télécopie. Par défaut, les utilisateurs ne sont pas configurés pour autoriser la remise de messages de télécopie entrants à un utilisateur à extension messagerie unifiée. Les serveurs Exchange envoient les demandes de télécopie à une solution de partenaire de télécopie agréé. Le serveur du partenaire de télécopie reçoit les données et les envoie à la boîte aux lettres du destinataire dans un message électronique avec la télécopie incluse en tant que pièce jointe au format .tif. Pour plus d'informations, consultez la rubrique [Activation de la réception de télécopies pour les utilisateurs de messagerie vocale](enable-voice-mail-users-to-receive-faxes-exchange-2013-help.md).

> [!NOTE]
> Nous vous conseillons que tous les clients qui projettent de déployer la messagerie unifiée sollicitent l'assistance d'un spécialiste en messagerie unifiée. Un spécialiste en messagerie unifiée vous aide à assurer une transition homogène vers la messagerie unifiée à partir d'un système de messagerie vocale hérité. La mise en place d'un nouveau déploiement ou la mise à niveau d'un système de messagerie vocale hérité requiert une connaissance réelle des PBX et de la messagerie unifiée . Pour plus d'informations sur la manière de contacter un spécialiste de la messagerie unifiée, consultez les rubriques <a href="https://go.microsoft.com/fwlink/p/?linkid=262708">Spécialistes en messagerie unifiée Microsoft Exchange Server 2013</a> ou <a href="https://go.microsoft.com/fwlink/p/?linkid=261951">Microsoft Pinpoint pour la messagerie unifiée</a>.


## Programme partenaire de télécopie pour la messagerie unifiée Exchange

Pour devenir un partenaire de télécopie agréé pour l'interopérabilité avec la messagerie unifiée , le partenaire doit répondre aux exigences contenues dans les spécifications pour l'interopérabilité du partenaire de télécopie, et la solution de télécopie doit être agréée par un fournisseur de certification indépendant. Pour plus d'informations sur la certification d'un produit de télécopie à utiliser avec la messagerie unifiée Exchange, envoyez une demande aux [partenaires de télécopie pour la messagerie unifiée Exchange 2010](mailto:fax-part@microsoft.com).

## Solutions de partenaires de télécopie agréés fonctionnant avec la messagerie unifiée

Si vous avez déjà déployé la messagerie unifiée Exchange et que vous recherchez un partenaire de télécopie pour permettre la réception de télécopie entrantes pour votre organisation, consultez la rubrique [Microsoft Pinpoint pour les partenaires de télécopie](https://go.microsoft.com/fwlink/p/?linkid=190238). Ces fournisseurs de logiciels ont obtenu une certification d'interopérabilité avec Exchange Server et incluent des solutions logicielles certifiées pour la messagerie unifiée.

## Passerelles VoIP ou multimédias et prise en charge de PBX IP

La configuration correcte des passerelles VoIP de votre organisation est une tâche de déploiement difficile qui doit être accomplie pour déployer correctement la messagerie unifiée Exchange avec la fonction de télécopie entrante. Pour trouver une solution à vos questions et obtenir les dernières informations sur la configuration de la passerelle VoIP, consultez la rubrique [Gestionnaire de téléphonie pour Exchange 2013](telephony-advisor-for-exchange-2013-exchange-2013-help.md). La rubrique [Notes de configuration pour les passerelles VoIP, les PBX IP et les PBX pris en charge](configuration-notes-for-supported-voip-gateways-ip-pbxs-and-pbxs-exchange-2013-help.md) fournit des notes et des fichiers relatifs à la configuration de la passerelle VoIP nécessaires à la configuration correcte des passerelles VoIP, PBX IP et SBC de votre organisation pour fonctionner avec la messagerie unifiée Exchange.

Le test de l'interopérabilité de la messagerie unifiée Exchange avec les passerelles IP est désormais intégré au programme d'interopérabilité d'ouverture des communications unifiées Microsoft. Pour plus d'informations, consultez la page du [programme d'interopérabilité d'ouverture des communications unifiées](http://go.microsoft.com/fwlink/p/?linkid=140722).

Le programme de qualification [Programme d'interopérabilité d'ouverture des communications unifiées Microsoft](http://go.microsoft.com/fwlink/p/?linkid=140722) pour les passerelles VoIP et les PBX IP garantit une configuration et une prise en charge transparentes lors de l'utilisation des passerelles de téléphonie et des PBX IP qualifiés avec le logiciel de communications unifiées de Microsoft.

> [!NOTE]
> L'envoi et la réception de télécopies à l'aide de T.38 ou G.711 ne sont pas pris en charge dans un environnement où la messagerie unifiée et Communications Server 2007 R2 ou Microsoft Lync Server sont intégrés.


## Déploiement et configuration de la télécopie

La messagerie unifiée transfère les appels de télécopie entrants à une solution partenaire de télécopie dédiée qui établit ensuite l'appel de télécopie avec l'expéditeur de télécopie et la reçoit de la part de l'utilisateur à extension messagerie unifiée. Toutefois, pour permettre aux utilisateurs à extension messagerie unifiée de recevoir des messages de télécopie dans leur boîte aux lettres, vous devez d'abord configurer le serveur partenaire de télécopie, puis configurer les plans de numérotations de messagerie unifiée ainsi que les stratégies de boîte aux lettres de messagerie unifiée, et autoriser les utilisateurs à extension messagerie unifiée à recevoir des télécopies. Pour plus d'informations, consultez la rubrique [Configuration des télécopies entrantes](setting-up-incoming-faxing-exchange-2013-help.md).

