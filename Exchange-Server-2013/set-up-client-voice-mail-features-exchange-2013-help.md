---
title: 'Configurer les fonctionnalités de messagerie vocale cliente: Exchange 2013 Help'
TOCTitle: Configurer les fonctionnalités de messagerie vocale cliente
ms:assetid: 5e661cfd-d34e-4caa-91a5-967bbecb75eb
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ673529(v=EXCHG.150)
ms:contentKeyID: 50555399
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configurer les fonctionnalités de messagerie vocale cliente

 

_**Sapplique à :**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :**2013-02-20_

Cette rubrique décrit les fonctionnalités du client qui octroient aux utilisateurs à extension messagerie unifiée Exchange un accès à la messagerie électronique et aux messages vocaux de leur boîte aux lettres. Ces fonctionnalités vous permettent d'offrir aux utilisateurs un accès simplifié à la messagerie vocale et à la messagerie électronique, ainsi qu'une expérience utilisateur globale améliorée.

**Contenu de la rubrique**

Prise en charge du client de messagerie vocale

Outlook Voice Access

Transfert d'appels

Aperçu de messagerie vocale

Réception de télécopies

## Prise en charge du client de messagerie vocale

**Clients Exchange ActiveSync**   Le protocole Microsoft Exchange ActiveSync permet de connecter des clients mobiles, tels que ceux que l'on retrouve sur les appareils mobiles compatibles Internet, à une boîte aux lettres Exchange. Les utilisateurs peuvent accéder à leur boîte aux lettres et consulter leurs messages électroniques, consulter et modifier des informations du calendrier et de contact, et écouter leurs messages vocaux sur des appareils mobiles. Ils peuvent également synchroniser la messagerie électronique, la messagerie vocale, des éléments de calendrier et des informations de contact avec d'autres appareils.

**Intégration à Outlook**   Microsoft Outlook permet aux utilisateurs d'accéder à leur boîte aux lettres Exchange et de consulter les messages électroniques de leur boîte de réception, de consulter et de modifier les informations de calendrier, et d'écouter les messages vocaux à l'aide du Lecteur Windows Media Microsoft, qui est intégré aux messages électroniques. Grâce à un client de messagerie pris en charge, les utilisateurs bénéficient de fonctionnalités supplémentaires, telles que la fonctionnalité Lire sur le téléphone.

**Intégration à Outlook Web App**   Microsoft Outlook Web App propose aux utilisateurs un ensemble d'interfaces de messagerie unifiée et des outils comparables à un client de messagerie complet comme Outlook. Grâce à Outlook Web App, les utilisateurs peuvent accéder à leur boîte aux lettres Exchange à l'aide d'un navigateur web compatible. Comme Outlook, Outlook Web App incorpore le Lecteur Windows Media dans des messages électroniques de sorte que les utilisateurs peuvent écouter les messages vocaux, et permet aux utilisateurs d'accéder à d'autres fonctionnalités, telles que Lire sur le téléphone.

## Outlook Voice Access

Dans la messagerie unifiée Exchange, un utilisateur à extension messagerie unifiée peut appeler un numéro de téléphone interne ou externe qui est configuré dans un plan de numérotation de messagerie unifiée pour accéder à sa boîte aux lettres et utiliser le système de menus d'Outlook Voice Access. Grâce à ce menu, les utilisateurs à extension messagerie unifiée peuvent lire des messages électroniques, écouter des messages vocaux, interagir avec leur calendrier Outlook, accéder à leurs contacts personnels et réaliser certaines tâches comme la configuration de leur code confidentiel Outlook Voice Access ou l'enregistrement de messages d'accueil vocaux. Pour plus d'informations, consultez la rubrique [Configuration d’Outlook Voice Access](setting-up-outlook-voice-access-exchange-2013-help.md).

## Transfert d'appels

Un utilisateur à extension messagerie unifiée peut créer et configurer des règles de répondeur automatique à l'aide d'Outlook ou d'Outlook Web App. Les règles de répondeur automatique permettent aux utilisateurs de contrôler le mode de traitement de leurs appels entrants. Les règles sont appliquées aux appels entrants de la même manière que les règles de boîte de réception sont appliquées aux messages électroniques entrants, et sont enregistrées avec d'autres paramètres vocaux dans la boîte aux lettres de l'utilisateur. Pour chaque boîte aux lettres à extension messagerie unifiée, vous pouvez configurer jusqu'à neuf règles de répondeur automatique. Ces règles sont indépendantes des règles de boîte de réception et ne font pas partie intégrante du quota de stockage des règles de boîte de réception de l'utilisateur. Pour plus d'informations, consultez la rubrique [Activation du transfert d'appels pour des utilisateurs de messagerie vocale](allow-voice-mail-users-to-forward-calls-exchange-2013-help.md).

## Aperçu de messagerie vocale

La fonctionnalité Aperçu de messagerie vocale est destinée aux utilisateurs qui reçoivent leurs messages vocaux du système de messagerie vocale de messagerie unifiée. Grâce à une version texte des enregistrements audio, cette fonctionnalité améliore l'expérience de messagerie vocale. Pour plus d'informations, consultez la rubrique [Activer la transcription des messages vocaux pour les utilisateurs](allow-users-to-see-a-voice-mail-transcript-exchange-2013-help.md).

## Réception de télécopies

La messagerie unifiée transfère les appels de télécopie entrants d'un utilisateur à extension messagerie vers une solution partenaire de télécopie dédiée qui établit l'appel de télécopie avec l'expéditeur de la télécopie et la reçoit pour le compte de l'utilisateur. Avant que vos utilisateurs à extension messagerie unifiée ne puissent recevoir des messages de télécopie dans leur boîte de réception, vous devez procéder comme suit :

  - Activez l'envoi et la réception de télécopies entrantes sur le plan de numérotation de messagerie unifiée associé aux utilisateurs en définissant le paramètre *FaxEnabled* sur `$true`.

  - Activez l'envoi et la réception de télécopies entrantes sur le plan de numérotation de messagerie unifiée associé aux utilisateurs en définissant le paramètre *Allowfax* sur `$true`.

  - Activez l'envoi et la réception de télécopies entrantes pour les utilisateurs en définissant le paramètre *FaxEnabled* sur `$true`.

  - Configurez l'URI du serveur de télécopie partenaire pour autoriser l'envoi et la réception de télécopies entrantes.

  - Configurez l'authentification entre le serveur de boîtes aux lettres et le serveur du partenaire de télécopie.

