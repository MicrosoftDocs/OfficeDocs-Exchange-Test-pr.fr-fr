---
title: 'Gestionnaire de l’aperçu de messagerie vocale: Exchange 2013 Help'
TOCTitle: Gestionnaire de l’aperçu de messagerie vocale
ms:assetid: 0957dd54-df6d-4b50-9db5-4757f548b899
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Ee364730(v=EXCHG.150)
ms:contentKeyID: 51407153
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Gestionnaire de l’aperçu de messagerie vocale

 

_**Sapplique à :** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2016-12-09_

La messagerie unifiée Exchange Microsoft propose une fonctionnalité appelée Aperçu de messagerie vocale. Celle-ci utilise la reconnaissance vocale automatique (ASR) pour ajouter aux messages vocaux une version texte de leur contenu audio. La reconnaissance vocale n'est pas extrêmement précise, surtout si elle est utilisée pour enregistrer des sons transmis par téléphone qui contiennent des voix et des bruits inconnus. Certaines organisations nécessitent systématiquement des transcriptions parfaites (ou presque) des messages. Le programme Partenaires d'aperçu de messagerie vocale peut aider à satisfaire leurs exigences.

L'aperçu de messagerie vocale s'appuie sur les [technologies Microsoft Speech](http://go.microsoft.com/fwlink/p/?linkid=187348) pour fournir une version texte des enregistrements audio. Le texte du message vocal est affiché dans des messages électroniques dans MicrosoftOutlook Web App, Outlook 2010 ou versions ultérieures, ainsi que d'autres programmes de messagerie.

Par défaut, quand vous activez la messagerie unifiée pour un utilisateur dans un déploiement local ou hybride, les aperçus de messages vocaux sont envoyés si un module linguistique de messagerie unifiée pris en charge est installé. Quand vous activez la messagerie unifiée pour un utilisateur dans Exchange Online, tous les modules linguistiques de messagerie unifiée sont installés. Toutefois, l'aperçu de messagerie vocale n'est pas pris en charge dans toutes les langues installées.

Certains partenaires d'aperçu de messagerie vocale offrent une prise en charge de la transcription améliorée pour la fonctionnalité Aperçu de messagerie vocale. Ces partenaires emploient des personnes pour corriger les transcriptions de messagerie vocale qui ont été créées à l'aide de la reconnaissance vocale (ASR). Chaque partenaire d'aperçu de messagerie vocale doit satisfaire un ensemble d'exigences afin d'être certifié pour interagir avec la messagerie unifiée Exchange.

Si vous déterminez que les aperçus de messages vocaux envoyés à vos utilisateurs ne sont pas suffisamment précis, vous pouvez contacter un des partenaires certifiés aperçu de messagerie vocale répertoriés à [Microsoft Pinpoint](https://go.microsoft.com/fwlink/p/?linkid=281966) et signe avec eux pour un coût supplémentaire.

**Contenu de cette rubrique**

Vue d’ensemble

Exchange Unified Messaging Voice Mail Partner program

Voice Mail Preview partners certified for Exchange Unified Messaging

Configuring Voice Mail Preview partners

VoIP or media gateways and IP PBX support

## Vue d'ensemble

Quand la fonction de messagerie unifiée enregistre le son d'un message vocal, elle emploie la reconnaissance vocale pour créer un texte d'aperçu de message vocal à partir du fichier audio, puis envoie le message complet pour remise à l'utilisateur concerné. Pour chaque message vocal créé, la messagerie unifiée établit un niveau de confiance concernant l'aperçu du message vocal joint au message. Elle évalue la correspondance entre l'enregistrement et les mots, les chiffres et les phrases contenus dans le message. Si le système trouve des correspondances facilement, le niveau de confiance sera élevé. Un niveau de confiance plus élevé est généralement associé à une précision plus élevée.

La précision du texte d'aperçu des messages vocaux dépend de nombreux facteurs, mais ceux-ci ne peuvent pas toujours être contrôlés. Toutefois, le texte présente généralement une meilleure précision lorsque :

  - Le message vocal est simple et l'appelant n'utilise pas d'argot, de jargon technique ou autres mots ou expressions inhabituels.

  - L'appelant utilise un langage facilement reconnaissable et transposable par le système de messagerie vocale. De façon générale, les messages vocaux des appelants qui ne parlent pas trop rapidement ou trop bas, et qui n'ont pas d'accent trop prononcé, permettront de transcrire plus aisément les mots et les phrases.

  - Le message vocal ne contient pas de bruit de fond et d'écho, et la qualité audio est régulière.

La plupart des clients qui utilisent la messagerie unifiée estiment que les aperçus de messages vocaux sont suffisamment précis pour leurs utilisateurs. Toutefois, lorsque l'ASR est appliquée aux enregistrements réalisés par téléphone avec des voix et des bruits de fond inconnus, le texte de l'aperçu présente généralement une précision insuffisante. Si le niveau de confiance est constamment bas ou si les aperçus de messages vocaux reçus ne sont pas très précis, vous pouvez renforcer la précision de la manière suivante :

  - Souscrivez à un service de transcription vocale auprès d'un partenaire d'aperçu de messagerie vocale.

  - Une fois inscrit auprès d'un partenaire d'aperçu de messagerie vocale, définissez-le de sorte qu'il fonctionne avec la messagerie unifiée. Pour plus d'informations sur la configuration d'un partenaire d'aperçu de messagerie vocale dans la messagerie unifiée, consultez la rubrique [Configurer les services de partenaires d’aperçu de messagerie vocale pour les utilisateurs](configure-voice-mail-preview-partner-services-for-users-exchange-2013-help.md).

Suite à l'inscription auprès d'un partenaire d'aperçu de messagerie vocale, les serveurs Exchange de votre organisation redirigent les messages vocaux et leur fichier audio joint vers le partenaire choisi au lieu de générer des textes d'aperçu des messages vocaux et d'envoyer les messages vocaux vers la boîte aux lettres de l'utilisateur. Le message électronique et le texte d'aperçu du message vocal généré par le partenaire d'aperçu de message vocal sont ensuite envoyés aux serveurs Exchange de votre organisation pour remise dans la boîte aux lettres du destinataire.

> [!NOTE]
> Il est recommandé que tous les clients qui envisagent de déployer la messagerie unifiée obtiennent l’assistance d’un spécialiste de la messagerie UNIFIÉE. Un spécialiste de la messagerie UNIFIÉE vous aide à assurer une transition en douceur vers la messagerie UNIFIÉE à partir d’un système de messagerie vocale hérité. Exécution d’un nouveau déploiement ou de mise à niveau d’un système de messagerie vocale hérité requiert une connaissance significative sur les passerelles VoIP, le PBX IP, les PBX, contrôleurs de bordure de session (SBCs) et de la messagerie unifiée. Pour plus d’informations sur la façon de contacter un spécialiste de la messagerie UNIFIÉE, consultez le <a href="http://go.microsoft.com/fwlink/p/?linkid=262708">Microsoft Exchange Server 2013 unifiée (MU) spécialistes de la messagerie</a> ou <a href="https://go.microsoft.com/fwlink/p/?linkid=261951">Microsoft Pinpoint pour la messagerie unifiée</a>.


Retour au début

## Programme Partenaires d'aperçu de messagerie vocale pour la messagerie unifiée Exchange

Pour obtenir une certification d'interopérabilité avec la messagerie unifiée Exchange, le partenaire doit répondre aux exigences contenues dans les spécifications pour l'interopérabilité des partenaires d'aperçu de messagerie vocale et la solution partenaire doit être agréée par un fournisseur de certification indépendant. Si vous souhaitez certifier votre service de transcription pour qu'il fonctionne avec la messagerie unifiée Exchange, envoyez une demande au programme [Partenaires d'aperçu de messagerie vocale pour la messagerie unifiée Exchange](mailto:vmppp@microsoft.com).

## Partenaires d'aperçu de messagerie vocale certifiés pour la messagerie unifiée Exchange

Si vous avez déjà déployé la messagerie unifiée dans votre organisation et que vous recherchez un partenaire agréé d’Aperçu de messagerie vocale fournir des services de prise en charge de transcription, consultez [Microsoft PinPoint](https://go.microsoft.com/fwlink/p/?linkid=281966). Ces fournisseurs de logiciels ont été certifiés comme interopérables avec la messagerie UNIFIÉE d’Exchange.

## Configuration des partenaires d'aperçu de messagerie vocale

Une fois la messagerie unifiée configurée, elle transfère les messages vocaux avec le fichier audio à un partenaire d'aperçu de messagerie vocale dédié, qui utilise alors le fichier audio pour créer le texte d'aperçu du message vocal. Toutefois, pour permettre aux utilisateurs de recevoir l'aperçu de messagerie vocale avec leur message vocal dans leur boîte aux lettres, vous devez configurer une stratégie de boîte aux lettres de messagerie unifiée, associer les utilisateurs à cette stratégie, puis demander aux utilisateurs de vérifier s'ils peuvent recevoir des aperçus de messages vocaux dans leurs messages vocaux dans Outlook 2010 ou version ultérieure, ou Outlook Web App. Pour plus d'informations sur la configuration d'un partenaire d'aperçu de messagerie vocale dans la messagerie unifiée, consultez la rubrique [Configurer les services de partenaires d’aperçu de messagerie vocale pour les utilisateurs](configure-voice-mail-preview-partner-services-for-users-exchange-2013-help.md).

## Passerelles VoIP ou multimédias et prise en charge de PBX IP

La configuration de passerelles VoIP et de PBX IP pour votre organisation constitue une tâche de déploiement difficile. Vous devez la réaliser correctement pour pouvoir déployer la messagerie unifiée avec un partenaire d'aperçu de messagerie vocale. Pour obtenir des informations d'aide à la configuration de vos passerelles IP et PBX IP et pour accéder aux dernières informations de configuration, consultez la rubrique [Gestionnaire de téléphonie pour Exchange 2013](telephony-advisor-for-exchange-2013-exchange-2013-help.md) ou [Notes de configuration pour les passerelles VoIP, les PBX IP et les PBX pris en charge](configuration-notes-for-supported-voip-gateways-ip-pbxs-and-pbxs-exchange-2013-help.md).

Test d’interopérabilité de la messagerie UNIFIÉE d’Exchange grâce à des passerelles VoIP a été intégrée à la Microsoft programme d’interopérabilité Open Unified Communications. Pour plus d’informations, consultez [Microsoft Unified Communications Ouvrir programme d’interopérabilité](https://go.microsoft.com/fwlink/p/?linkid=132071).

Retour au début

