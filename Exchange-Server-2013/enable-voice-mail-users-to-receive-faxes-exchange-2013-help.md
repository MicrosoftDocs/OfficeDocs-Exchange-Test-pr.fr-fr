---
title: 'Activ. réception de télécopies pr utlsr de messag. voc.: Exchange 2013 Help'
TOCTitle: Activation de la réception de télécopies pour les utilisateurs de messagerie vocale
ms:assetid: 451ab0ea-21e1-4c1f-ae62-4ba7cdfd1e4d
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb232022(v=EXCHG.150)
ms:contentKeyID: 52062953
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Activation de la réception de télécopies pour les utilisateurs de messagerie vocale

 

_**Sapplique à :** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2015-04-07_

Microsoft La messagerie unifiée Exchange permet de remettre des messages vocaux à des boîtes aux lettres et permet aux utilisateurs de recevoir des télécopies dans leur boîte aux lettres. Dans la messagerie unifiée, une télécopie est envoyée à la boîte aux lettres d’un utilisateur sous la forme d’un message électronique auquel est joint un fichier image de format .tif. L’utilisateur peut ouvrir le fichier attaché à l’aide d’une application logicielle capable d’ouvrir et d’afficher des fichiers image portant l’extension .tif. Cette rubrique présente la télécopie et la manière dont elle fonctionne dans la messagerie unifiée.

> [!NOTE]
> Bien que la messagerie unifiée ne permette pas aux utilisateurs d’envoyer des télécopies sortantes, de nombreuses solutions tierces, telles que des services de télécopie sur Internet, des services de télécopie par messagerie ou des applications de serveur de télécopie tierces permettent d’envoyer des télécopies sortantes.


**Table des matières**

Vue d’ensemble de la télécopie

Méthodes de télécopie

T.38

Vue d’ensemble de la télécopie avec la messagerie unifiée

Réception de télécopies entrantes

Méthodes de référence d’appel de télécopie

Configuration de la télécopie

Numéros de téléphone et télécopie

Journalisation des messages de télécopie de messagerie unifiée

## Vue d’ensemble de la télécopie

Le mot fax est une abréviation du mot facsimile. Il s’agit d’une technologie utilisée pour transférer des documents par voie électronique. Généralement, les télécopies sont envoyées et reçues par des télécopieurs ou des modems de télécopie pour ordinateur à l’aide du RTC (réseau téléphonique commuté), réseau de téléphonie ou basé sur un circuit. Toutefois, d’autres options permettent d’envoyer et de recevoir des télécopies.

La plupart des organisations actuelles souhaitent que leurs utilisateurs puissent envoyer et recevoir des télécopies. Les organisations utilisent une ou plusieurs des méthodes décrites dans la liste suivante pour envoyer ou recevoir des télécopies sur le RTC ou sur Internet. Chacune de ces méthodes présente des avantages et des inconvénients.

  - Télécopieurs traditionnels et télécopie à partir d’un ordinateur

  - Télécopie à l’aide de serveurs ou de passerelles de télécopie

  - Télécopie à l’aide d’un réseau VoIP (Voice over IP)

  - Télécopie à l’aide d’une application cliente de messagerie

Pour envoyer une télécopie, il se peut que les utilisateurs au sein d’une organisation doivent effectuer les opérations suivantes :

  - imprimer une épreuve du document à télécopier et utiliser un appareil de télécopie pour l’envoyer ;

  - enregistrer le document sur leur ordinateur et utiliser un modem de télécopie pour envoyer la télécopie, mais cela nécessite une ligne téléphonique connectée à l’ordinateur ;

  - utiliser un service de télécopie sur Internet permettant de télécopier un document à partir d’une application logicielle spécifique du vendeur ;

  - envoyer une télécopie sortante à un serveur de télécopie à l’aide d’une application logicielle configurée pour utiliser le serveur de télécopie.

Pour recevoir une télécopie, il se peut que les utilisateurs au sein d’une organisation doivent effectuer les opérations suivantes :

  - recevoir une télécopie sur un appareil de télécopie à l’intérieur de l’organisation ;

  - recevoir une télécopie à l’aide d’un modem de télécopie installé sur leur ordinateur ;

  - recevoir une télécopie à partir d’un service de télécopie sur Internet ;

  - recevoir une télécopie d’un serveur de télécopie configuré sur un réseau ;

  - Recevoir une télécopie en provenance d’un serveur de partenaire de télécopie utilisant la messagerie unifiée pour remettre la télécopie à l’aide d’un réseau VoIP.

Retour au début

## Méthodes de télécopie

Il existe plusieurs options pour l’envoi et la réception de télécopies, notamment les suivantes :

**Télécopie à l’aide de télécopieurs traditionnels et d’ordinateurs**   Pour envoyer et recevoir des télécopies, vous pouvez utiliser un scanneur, un modem de télécopie connecté à un ordinateur, une imprimante avec des fonctionnalités de télécopie intégrées ou un appareil de télécopie dédié. Ces appareils permettent de transmettre des données sous forme d’impulsions sur une ligne téléphonique vers un autre périphérique de télécopie, généralement un autre appareil de télécopie ou un ordinateur équipé d’un modem de télécopie. Les impulsions sont ensuite converties en images ou utilisées pour imprimer l’image sur papier.

La méthode de télécopie traditionnelle requiert au moins une ligne téléphonique connectée au périphérique émetteur et récepteur et ne permet d’envoyer ou de recevoir qu’une seule télécopie à la fois. Un inconvénient de l’envoi et de la réception de télécopies à l’aide d’un modem de télécopie est que l’ordinateur doit être sous tension et exécuter un logiciel ou un service de télécopie. Ce type de télécopie à partir d’un ordinateur n’utilise pas Internet pour envoyer ou recevoir des télécopies.

**Télécopie traditionnelle et basée sur un ordinateur**

![Envoi traditionnel de télécopie](images/Bb232022.7bdc1cab-9504-4314-a6e0-eccdfe2a9cd6(EXCHG.150).gif "Envoi traditionnel de télécopie")

**Serveurs ou passerelles de télécopie et services de télécopie sur Internet**   Il existe plusieurs façons d’envoyer et de recevoir des télécopies sur Internet. Parmi celles-ci figurent l’utilisation d’une application logicielle sur un ordinateur ou l’utilisation d’un client de messagerie pour recevoir des télécopies. Le plus souvent, ce type de télécopie implique l’utilisation d’un serveur ou d’une passerelle de télécopie pour opérer la conversion entre les télécopies et les messages électroniques. Cette solution a gagné en popularité parce qu’elle permet aux organisations de supprimer les appareils de télécopie ou de ne plus en acheter. Elle élimine également la nécessité d’installer des lignes téléphoniques supplémentaires. Ce type de télécopie implique la création du document, notamment d’une page de couverture avec les informations d’identification correctes et l’envoi du document à un appareil de télécopie traditionnel. Par exemple, l’utilisateur se sert d’une application logicielle telle que Microsoft Word ou Outlook pour créer et envoyer la télécopie au serveur ou à la passerelle de télécopie. Le serveur ou la passerelle de télécopie reçoit la télécopie, puis l’envoie à l’aide d’une ligne téléphonique traditionnelle à un appareil ou à un modem de télécopie installé sur un ordinateur.

**Télécopie avec serveurs ou passerelles de télécopie**

![Envoi de télécopies avec des serveurs/passerelles de télécopie](images/Bb232022.d6fa2402-b4ca-4313-956c-62e5fe7731ad(EXCHG.150).gif "Envoi de télécopies avec des serveurs/passerelles de télécopie")

Les services de télécopie sur Internet permettent à un utilisateur d’envoyer des télécopies à partir d’un ordinateur via Internet. Une application logicielle telle que Word ou Outlook permet de créer et d’envoyer la télécopie à un service de télécopie Internet. De nombreuses sociétés offrent des services de télécopie sur Internet basés sur un abonnement ou une facturation au message envoyé. Les services de télécopie sur Internet offrent les avantages suivants :

  - Aucun appareil de télécopie n’est requis.

  - Aucun élément logiciel ni matériel ne doit être installé.

  - Aucune ligne téléphonique dédiée n’est requise.

  - Confidentialité.

  - Il est possible d’envoyer plusieurs télécopies à la fois.

  - Il est possible de recevoir des télécopies lorsque l’ordinateur est éteint.

La figure suivante illustre la manière dont les services de télécopie sur Internet permettent d’envoyer et de recevoir des télécopies.

**Services de télécopie Internet**

![Services de télécopie sur Internet](images/Bb232022.5d0fb3d6-95f4-4fbf-80e5-64f5de553e65(EXCHG.150).gif "Services de télécopie sur Internet")

**Télécopie à l’aide d’une application cliente de messagerie** Des télécopies peuvent être envoyées et reçues par un appareil de télécopie sur Internet, puis reçues par un client de messagerie tel qu’Outlook.

Le protocole T.37 a été conçu pour permettre à un appareil de télécopie d’envoyer des messages de télécopie sur Internet à un client de messagerie. Les télécopies sont envoyées sur Internet en tant que pièces jointes, généralement comme fichiers .tif ou .pdf. Pour ce type de télécopie, un appareil de télécopie prenant en charge iFax ou T.37 est requis, en plus d’une adresse de messagerie, pour l’appareil de télécopie émetteur et récepteur. Par souci de compatibilité avec les appareils de télécopie et modems de télécopie traditionnels, tous les appareils de télécopie T.37 prennent en charge la télécopie standard à l’aide d’une ligne téléphonique. Toutefois, dans certains cas, il est possible d’utiliser des appareils de télécopie T.37 avec une passerelle de télécopie déjà utilisée. La figure suivante illustre la manière dont les appareils de télécopie de type T.37 et les clients de messagerie permettent d’envoyer et de recevoir des télécopies.

**Envoi par télécopie avec courrier électronique**

![Envoi par télécopie avec courrier électronique](images/Bb232022.086f086b-dc39-4439-a694-7a98e03e65d1(EXCHG.150).gif "Envoi par télécopie avec courrier électronique")

**Télécopie à l’aide d’un réseau VoIP**   VoIP (protocole voix sur IP) est une technologie qui englobe du matériel et des logiciels permettant d’utiliser un réseau IP comme moyen de transmission pour les appels téléphoniques. Sur un réseau VoIP, les données vocales sont envoyées par paquets à l’aide du protocole IP au lieu des transmissions par circuit traditionnelles ou des lignes téléphoniques de commutation par circuits du RTC. Une passerelle VoIP que vous connectez à votre réseau IP utilise le protocole VoIP pour échanger des paquets de données vocales entre un serveur d’accès au client exécutant le service routeur d’appels de messagerie unifiée Microsoft Exchange et un serveur de boîtes aux lettres exécutant le service de messagerie unifiée Microsoft Exchange ou un système d’autocommutateur privé (PBX). Vous pouvez également utiliser un PBX IP pour disposer à la fois des fonctions d’une passerelle IP et de celles d’un PBX.

Il existe deux types basiques de réseaux : les réseaux de commutation par circuits et les réseaux de commutation par paquets. Un réseau de commutation par circuits est un réseau utilisant une connexion dédiée. Une connexion dédiée est un circuit ou un canal installé entre deux nœuds afin de leur permettre de communiquer. Après qu’un appel a été établi entre deux nœuds, la connexion peut être utilisée uniquement par ces derniers. Lorsque l’un des nœuds met fin à l’appel, la connexion est annulée. Dans les réseaux de commutation par circuits, tels que le Réseau téléphonique commuté (RTC), plusieurs appels sont transmis via le même moyen de transmission. Dans le RTC, le cuivre est souvent utilisé comme moyen de transmission. Toutefois, un câble en fibre optique peut également être utilisé.

Dans les réseaux de commutation par paquets tels qu’Internet ou un réseau local (LAN), les paquets sont routés vers leur destination via la route la plus appropriée, mais tous les paquets qui voyagent entre deux hébergeurs n’empruntent pas la même route, même s’ils font partie d’un même message. Cela garantit presque que les paquets parviendront à destination à des moments différents et dans le désordre. Dans un réseau de commutation par paquets, les paquets (messages ou fragments de messages) sont routés individuellement entre les nœuds sur les liaisons de données qui peuvent être partagées par d’autres nœuds. Contrairement à la commutation par circuits, avec la commutation par paquets, plusieurs connexions aux nœuds sur le réseau partagent la bande passante disponible. Le réseau de commutation par paquets a permis à Internet d’exister et, par la même occasion, rendu les réseaux de données (particulièrement les réseaux VoIP et les réseaux IP basés sur LAN) plus disponibles et répandus.

Retour au début

## T.38

T.38 est une norme et un protocole de télécopie qui permet de transmettre des télécopies sur un réseau de type IP. Un réseau de type IP utilisant le protocole T.38 se sert de SMTP (Simple Mail Transfer Protocol) et de MIME (Multipurpose Internet Mail Extension) pour envoyer un message à la boîte aux lettres d’un destinataire. T.38 autorise les transmissions de télécopie IP pour les périphériques de télécopie et les passerelles de télécopie à IP activé. Les périphériques peuvent inclure des hôtes de type réseau IP, tels que des ordinateurs et des imprimantes clients. Dans la messagerie unifiée Exchange, les images de télécopie sont des documents distincts codés comme des fichiers .tif et joints à un message électronique. Le message électronique et le fichier .tif en pièce jointe sont tous deux envoyés à la boîte aux lettres à extension messagerie unifiée de l’utilisateur.

La messagerie unifiée s’appuie sur les capacités de la passerelle à traduire ou à convertir les protocoles basés sur le MRT (multiplexage par répartition dans le temps) ou la commutation par circuits téléphoniques tels que RNIS et QSIG à partir d’un PBX, en protocoles basés sur IP ou VoIP tels que SIP (Session Initiated Protocol), RTP (Realtime Transport Protocol) ou T.38 pour la réception de télécopies. La passerelle VoIP fait partie intégrante de la fonctionnalité et du fonctionnement de la messagerie unifiée. La passerelle VoIP est responsable de la détection des tonalités de télécopie. Les serveurs d’accès au client et de boîtes aux lettres s’appuient sur la passerelle VoIP pour envoyer une notification de détection de télécopie. Ensuite, les serveurs d’accès au client et de boîtes aux lettres renégocient la session de média et utilisent le protocole T.38.

Retour au début

## Vue d’ensemble de la télécopie avec la messagerie unifiée

Dans la messagerie unifiée, l’utilisateur reçoit les images de télécopie en tant que documents séparés codés comme fichiers image .tif joints à un message électronique. Le message électronique et le fichier .tif en pièce jointe sont tous deux envoyés à la boîte aux lettres à extension messagerie unifiée de l’utilisateur.

L’envoi d’un message de télécopie à la boîte aux lettres de l’utilisateur présente plusieurs avantages. Ces avantages sont les suivants :

  - Vous pouvez réduire le nombre d’appareils de télécopie physiques ou traditionnels.

  - Le nombre de lignes téléphoniques utilisées pour télécopier au sein d’une organisation peut être réduit, car le serveur de boîtes aux lettres peut mettre en file d’attente de nombreuses télécopies et envoyer chacune d’elles quand une des lignes téléphoniques devient disponible.

  - Les télécopies reçues en tant que fichier image .tif sont de meilleure qualité qu’une télécopie traditionnelle. Les télécopies entrantes peuvent être imprimées par une imprimante locale ou partagée.

  - Les télécopies envoyées à la boîte aux lettres de l’utilisateur sont mieux sécurisées que les télécopies imprimées, car il y a moins de probabilité qu’elles soient interceptées par quelqu’un d’autre que le destinataire.

  - Les utilisateurs peuvent recevoir des télécopies sans quitter leur bureau.

  - Il est possible de surveiller les messages de télécopie reçus pour s’assurer qu’ils sont conformes aux stratégies de sécurité d’une organisation.

Un message de télécopie ne peut être envoyé qu’à un seul utilisateur à extension messagerie unifiée. La messagerie unifiée ne peut pas transmettre de messages de télécopie à une liste de distribution. Si vous nécessitez cette fonctionnalité, procédez comme suit :

1.  Créez une boîte aux lettres pour répondre aux appels de télécopie. Il s’agira de la boîte aux lettres destinée à la liste de distribution.

2.  Activez la messagerie unifiée pour la boîte aux lettres de liste de distribution.

3.  Créez une règle pour cette boîte aux lettres à extension messagerie unifiée. La règle sera configurée pour transmettre tous les messages à la liste de distribution sélectionnée.

Retour au début

## Réception de télécopies entrantes

La réception d’une télécopie sur un réseau VoIP diffère de la réception d’une télécopie sur un appareil de télécopie standard ou à l’aide d’un serveur de télécopie localisé sur un réseau de type IP. Pour permettre l’envoi et la réception de télécopies sur un réseau VoIP, vous devez disposer d’une passerelle VoIP ou d’un PBX IP prenant en charge le protocole T.38, et d’un serveur le prenant également en charge. Le protocole T.38 permet d’effectuer des transmissions de télécopie de type IP pour des hôtes basés sur un réseau IP, tels que des ordinateurs clients, des imprimantes avec des fonctionnalités de télécopie intégrées et des serveurs tels qu’un serveur de boîtes aux lettres.

> [!IMPORTANT]  
> L’envoi et la réception de télécopies à l’aide de T.38 ou G.711 ne sont pas pris en charge dans un environnement où la messagerie unifiée et Microsoft Office Communications Server 2007 R2 ou Microsoft Lync Server sont intégrés.


Quand un PBX reçoit un appel, il le transfère vers le poste approprié. Si le poste de l’utilisateur ne répond pas, le PBX transmet l’appel à une passerelle VoIP qui le transmet à son tour au serveur de boîtes aux lettres approprié. Le serveur de boîtes aux lettres détermine si l’appel est un appel vocal ou de télécopie en fonction du protocole utilisé. En cas d’utilisation du protocole SIP, le serveur de boîtes aux lettres traite l’appel comme un message vocal. En revanche, en cas d’utilisation du protocole T.38 à partir de la passerelle IP, le serveur de boîtes aux lettres détecte que l’appel est une télécopie et le traite de la manière décrite dans le paragraphe suivant. Un serveur de boîtes aux lettres transfère les appels de télécopie entrants à un serveur de partenaire de télécopie dédié qui établit ensuite l’appel de télécopie avec l’expéditeur de la télécopie et reçoit cette dernière de la part de l’utilisateur à extension messagerie unifiée. Le serveur du partenaire de télécopie envoie ensuite la télécopie incluse en tant que pièce jointe .tif dans le message SMTP à la boîte aux lettres du destinataire.

Quand un serveur de boîtes aux lettres reçoit un signal de télécopie T.38 entrant d’une passerelle VoIP, il interroge l’annuaire à l’aide du protocole LDAP (Lightweight Directory Access Protocol) pour déterminer si le destinataire prévu de l’appel de télécopie entrant est autorisé à recevoir de tels appels, et pour déterminer l’adresse SIP du serveur du partenaire de télécopie. Après vérification de ces informations, le serveur de boîtes aux lettres envoie une demande de référence d’appel de télécopie à la passerelle VoIP ou à l’homologue SIP, qui transmet ensuite la demande de télécopie au serveur du partenaire de télécopie. Une fois l’appel de télécopie correctement établi, l’expéditeur de la télécopie envoie le support et les données de télécopie au serveur du partenaire de télécopie. Après avoir reçu le support et les données de télécopie, le serveur du partenaire de télécopie utilise SMTP pour envoyer un message électronique à un serveur de boîtes aux lettres. Ce message contient une image .tif de la télécopie et des en-têtes X spéciaux pour le destinataire de la télécopie.

Une fois le message de télécopie authentifié et envoyé à partir d’un serveur du partenaire de télécopie valide, l’assistant Boîte aux lettres de messagerie unifiée sur le serveur de boîtes aux lettres émet un appel RPC au service de messagerie unifiée Microsoft Exchange. Cela garantit que les propriétés du message de télécopie correspondent à celles des messages de télécopie créés par un serveur de boîtes aux lettres. Enfin, le serveur de boîte aux lettres envoie à nouveau le message de télécopie final, qui comprend le message électronique et la pièce jointe .tif pour les télécopies entrantes. Ensuite, à l’aide de MAPI RPC, la version finale et mise en forme de la télécopie est remise au serveur de boîte aux lettres qui contient la boîte aux lettres du destinataire souhaité.

Retour au début

## Méthodes de référence d’appel de télécopie

Un appel de télécopie entrant peut être signalé à un serveur de boîtes aux lettres via SIP re-INVITE à partir de la passerelle VoIP (passerelle multimédia) ou d’un homologue SIP (passerelle média), d’une notification de CNG (tonalité de télécopie entrante) par l’homologue SIP ou d’une détection CNG par le serveur de boîtes aux lettres. Les sous-sections suivantes détaillent le renvoi d’appel de télécopie dans chaque cas.

## Re-INVITE à partir de l’homologue SIP

Un appel entrant au numéro de pilote de la messagerie unifiée est dirigé vers la messagerie unifiée en tant qu’INVITE avec un profil SDP vocal (RTP/audio).

1.  La messagerie unifiée accepte l’invitation et les flux de données multimédia sont établis. Une fois l’appel établi, la transmission de télécopie est initialisée par l’appelant.

2.  L’homologue SIP détecte la tonalité de télécopie appelante (CNG). L’homologue SIP émet un message re-INVITE au serveur de boîtes aux lettres, cette fois en spécifiant un profil de télécopie (T.38 ou G.711) dans le protocole SDP.

3.  La messagerie unifiée répond à l’invitation avec une réponse « 200 OK » qui met l’homologue SIP « en attente ».

4.  La messagerie unifiée émet un message REFER, référant l’homologue SIP (CNG) à un point de terminaison de solution de partenaire de télécopie, obtenu à partir de ses données de configuration.

5.  L’homologue SIP envoie la session de télécopie INVITE à la solution de partenaire de télécopie.

6.  La solution partenaire de télécopie accepte l’invitation et une session de média est établie avec l’homologue SIP.

## Notifications de CNG par un homologue SIP

Un appel entrant au numéro de pilote de la messagerie unifiée est dirigé vers la messagerie unifiée en tant qu’INVITE avec un profil SDP vocal (RTP/audio).

1.  La messagerie unifiée accepte l’invitation et les flux de données multimédia sont établis. Une fois l’appel établi, la transmission de télécopie est initialisée par l’appelant.

2.  L’homologue SIP détecte la tonalité de télécopie entrante (CNG). Il informe le serveur de messagerie unifiée de la télécopie en envoyant une notification de CNG dans le flux RTP, conforme à la norme RFC 4733.

3.  La messagerie unifiée répond à la notification en émettant immédiatement un message REFER, référant l’homologue SIP à un point de terminaison de solution de partenaire de télécopie obtenu à partir de ses données de configuration.

4.  L’homologue SIP envoie la session de télécopie INVITE à la solution de partenaire de télécopie.

5.  La solution de partenaire de télécopie accepte l’invitation.

6.  Une session de média est établie avec l’homologue SIP.

## Détection de CNG par un serveur de boîtes aux lettres

Un appel entrant au numéro de pilote de la messagerie unifiée est dirigé vers la messagerie unifiée en tant qu’INVITE avec un profil SDP vocal (RTP/audio). La messagerie unifiée accepte l’invitation et les flux de données multimédia sont établis.

1.  Une fois l’appel établi, la transmission de télécopie est initialisée par l’appelant.

2.  Le serveur de boîtes aux lettres détecte la tonalité de télécopie (CNG) dans le flux audio RTP.

3.  La messagerie unifiée répond à la notification en émettant immédiatement un message REFER, référant l’homologue SIP à un point de terminaison de solution de partenaire de télécopie obtenu à partir de ses données de configuration.

4.  L’homologue SIP envoie la session de télécopie INVITE à la solution de partenaire de télécopie.

5.  La solution de partenaire de télécopie accepte l’invitation.

6.  Une session de média est établie avec l’homologue SIP.

Retour au début

## Configuration de la télécopie

Par défaut, lorsque vous installez le rôle serveur de boîtes aux lettres, le serveur n’est pas configuré pour permettre le traitement des appels de télécopie entrants ou leur remise à un utilisateur à extension messagerie unifiée. Pour configurer la messagerie unifiée avec un serveur du partenaire de télécopie, vous devez configurer la stratégie de boîte aux lettres de messagerie unifiée et configurer l’authentification entre le serveur de boîtes aux lettres et le serveur du partenaire de télécopie. Pour plus d’informations, voir [Configuration des télécopies entrantes](https://docs.microsoft.com/fr-fr/exchange/voice-mail-unified-messaging/set-up-client-voice-mail-features/set-up-incoming-faxing).

Retour au début

## Numéros de téléphone et télécopie

La messagerie unifiée Exchange offre les options suivantes lors de la configuration des utilisateurs à extension messagerie unifiée pour la réception de messages de télécopie :

  - un numéro de téléphone DID (Direct Inward Dial) pour un utilisateur, utilisé pour la télécopie et la messagerie vocale ;

  - un numéro de téléphone DID séparé pour un utilisateur, utilisé pour la réception de télécopies ;

  - un numéro de télécopie central pour tous les utilisateurs, qui reçoit toutes les télécopies.

## Numéro de téléphone DID unique

Lorsque vous activez un utilisateur pour la messagerie unifiée à l’aide de la page **Activer la boîte aux lettres de messagerie unifiée** ou de la cmdlet **Enable-UMMailbox**, vous devez spécifier au moins un numéro de poste unique pour l’utilisateur. Ce numéro de poste est activé individuellement pour chaque utilisateur et doit être unique à l’intérieur d’un plan de numérotation donné. Ce poste est utilisé par la messagerie unifiée pour localiser l’utilisateur approprié et pour remettre des messages vocaux et de télécopie à la boîte aux lettres de l’utilisateur. Pour plus d’informations, voir [Enable-UMMailbox](https://technet.microsoft.com/fr-fr/library/aa998033\(v=exchg.150\)).

À l’aide d’un numéro DID unique, vous pouvez configurer la télécopie de sorte qu’un utilisateur ait recours à un seul numéro DID pour les fonctions voix et télécopie. Cette configuration est facile à administrer et évite d’avoir des numéros DID superflus. Si l’utilisateur est absent ou au téléphone lors de l’arrivée d’un appel de télécopie, la messagerie unifiée répond à l’appel, détecte la tonalité de télécopie, crée le message de télécopie et l’envoie à l’utilisateur.

Si un utilisateur dont la télécopie est configurée à l’aide d’un seul numéro de téléphone DID reçoit un appel en provenance d’un appareil de télécopie lorsqu’il n’est pas absent ou au téléphone, il peut faire ce qui suit :

  - ne pas répondre au téléphone quand il sonne, de sorte que l’appel de télécopie soit transféré vers un serveur de boîtes aux lettres qui y répond, et que le message de télécopie soit créé et transféré vers la boîte aux lettres de l’utilisateur ;

  - répondre à l’appel de télécopie, puis se le transmettre à lui-même, de sorte que l’appel soit transféré vers un serveur de boîtes aux lettres qui y répond, et que le message de télécopie soit créé et transféré vers la boîte aux lettres de l’utilisateur ;

  - attendre que l’appelant tente de nouveau d’envoyer la télécopie et laisser le système transférer l’appel vers un serveur de boîtes aux lettres.

En résumé, l’utilisation d’un numéro DID unique requiert que l’utilisateur exécute des actions supplémentaires pour pouvoir recevoir des messages de télécopie.

Retour au début

## Plusieurs numéros de téléphone DID

Lorsque vous activez un utilisateur pour la messagerie unifiée, vous devez entrer au moins un numéro de poste pour cet utilisateur. Vous pouvez ajouter plusieurs numéros de poste pour un utilisateur à extension messagerie unifiée en utilisant le Centre d’administration Exchange (CAE). Pour plus d’informations, voir [Ajouter un numéro de poste](https://docs.microsoft.com/fr-fr/exchange/voice-mail-unified-messaging/set-up-voice-mail/add-extension-number).

L’ajout de plusieurs numéros de poste est utile quand un utilisateur à extension messagerie unifiée :

  - reçoit de nombreuses télécopies ;

  - ne souhaite pas devoir répondre au téléphone ou recevoir des télécopies ;

  - ne souhaite pas entendre de tonalité de télécopie quand il répond au téléphone.

L’ajout de plusieurs postes est plus complexe que l’utilisation d’un poste unique et peut nécessiter des paramètres de configuration supplémentaires sur un PBX ou un PBX IP. Pour configurer plusieurs numéros de poste pour un utilisateur à extension messagerie unifiée, vous devez avoir des numéros de poste DID disponibles mais non utilisés dans votre organisation. Nous vous déconseillons d’utiliser plusieurs numéros pour un utilisateur à extension messagerie unifiée si votre organisation possède un nombre limité de numéros de poste DID disponibles.

L’avantage de l’utilisation de plusieurs numéros de téléphone DID est que l’utilisateur à extension messagerie unifiée reçoit les appels vocaux sur un seul numéro de poste DID, et les appels de télécopie sur un autre. L’utilisation de numéros DID distincts pour les appels vocaux et de télécopie est plus facile pour l’utilisateur.

Si vous configurez deux numéros de poste DID pour un utilisateur spécifique, les numéros de poste DID peuvent être associés à des plans de numérotation de messagerie unifiée distincts. Pour utiliser deux numéros DID, vous pouvez créer un plan de numérotation et utiliser un serveur de boîtes aux lettres comme serveur dédié à la réception des appels de télécopie et au transfert des messages de télécopie aux utilisateurs. Pour plus d’informations, voir [Créer un plan de numérotation de messagerie unifiée](https://docs.microsoft.com/fr-fr/exchange/voice-mail-unified-messaging/connect-voice-mail-system/create-um-dial-plan).

Les options de configuration de plusieurs numéros de poste DID pour des utilisateurs à extension messagerie unifiée sont les suivantes :

  - **Un poste pour la télécopie sans messagerie unifiée et un autre pour la voix**   Ce type de configuration est activé pour chaque utilisateur et utilisé lorsque vous disposez de numéros de poste DID supplémentaires ou inutilisés. Un numéro de poste DID est publié comme numéro de messagerie vocale et l’autre comme numéro de télécopie de l’utilisateur. Les appels vocaux qui reçoivent une réponse parce que l’utilisateur ne répond pas au téléphone ou parce qu’une tonalité d’occupation est émise, sont transférés vers un serveur de boîtes aux lettres, et un message vocal est créé et envoyé à la boîte aux lettres de l’utilisateur à extension messagerie unifiée. L’autre numéro de poste peut être connecté à un appareil de télécopie ou un autre ordinateur disposant d’un modem de télécopie. Avec cette configuration, un serveur de boîtes aux lettres ne traite pas les appels de télécopie, et les messages de télécopie ne sont pas envoyés à la boîte aux lettres de l’utilisateur à extension messagerie unifiée.

  - **Un poste pour la télécopie et un autre pour la voix**   Ce type de configuration est activé individuellement pour chaque utilisateur et peut être utilisé lorsque votre organisation possède de nombreux numéros de poste DID disponibles. Dans cette configuration, les deux numéros de poste DID qui reçoivent une réponse parce que l’utilisateur ne répond pas au téléphone ou parce qu’une tonalité d’occupation est émise, sont transférés vers un serveur de boîtes aux lettres qui crée un message vocal ou de télécopie en fonction de numéro de poste DID appelé. Bien que l’utilisateur publie un numéro pour la voix et un autre pour la télécopie, le serveur de boîtes aux lettres détecte le type d’appel reçu sur le numéro de poste DID et peut créer un message vocal ou de télécopie à partir des appels adressés à l’un des numéros de poste DID. Cela est très utile quand un utilisateur ne dispose pas d’un appareil de télécopie ou d’un ordinateur dédié équipé d’un modem de télécopie pour répondre aux appels de télécopie entrants.

  - **Un poste « fantôme » pour la télécopie et un pour les appels vocaux**   Ce type de configuration est activé individuellement pour chaque utilisateur. Il s’agit fondamentalement de la même configuration que celle utilisant deux numéros DID (un pour la télécopie et l’autre pour la voix). Toutefois, dans cette configuration, le numéro publié pour les appels de télécopie pour l’utilisateur à extension messagerie unifiée est configuré dans le PBX comme poste « fantôme ». Les appels entrants reçus sur ce numéro de poste DID « fantôme » sont toujours transférés vers un serveur de boîtes aux lettres.
    
    L’avantage de ce type de configuration est que les appels de télécopie entrants reçoivent la réponse d’un serveur de boîtes aux lettres. Lorsque le téléphone sonne sans réponse, une télécopie est créée et transmise par le serveur de boîtes aux lettres vers la boîte aux lettres de l’utilisateur à extension messagerie unifiée sans déranger l’utilisateur. Cela se produit automatiquement car, aucun périphérique de téléphonie ou de télécopie n’étant placé à proximité de l’utilisateur, ce dernier n’entend pas la sonnerie de l’appel entrant.
    
    Les inconvénients de ce type de configuration sont que vous devez disposer de postes DID supplémentaires, et configurer le PBX ou le PBX IP pour transférer l’appel vers un serveur de boîtes aux lettres.

## Numéro de télécopie central

Lorsque vous activez un utilisateur pour la messagerie unifiée à l’aide de la page **Activer la boîte aux lettres de messagerie unifiée** ou de la cmdlet **Enable-UMMailbox**, vous devez spécifier au moins un numéro de poste unique pour l’utilisateur. Toutefois, si vous devez configurer un numéro de télécopie central pour les télécopies entrantes, vous devez configurer une boîte aux lettres à extension messagerie unifiée séparée servant à recevoir toutes les télécopies.

Dans certaines organisations, en particulier celles qui reçoivent de nombreuses télécopies quotidiennement, il peut être opportun de publier un seul numéro de télécopie pour l’ensemble de l’organisation. Ce numéro de télécopieur est alors utilisé par tous les appelants soumettant des télécopies destinées à des utilisateurs au sein de l’organisation.

La publication d’un seul numéro de télécopie pour toute l’organisation permet à celle-ci de contrôler les types de télécopies reçus par les utilisateurs. L’avantage de cette configuration est qu’elle ne requiert qu’un seul numéro de poste DID ou un seul numéro de téléphone externe. De même, elle ne requiert pas de numéro DID distinct de télécopieur pour chaque utilisateur à extension messagerie unifiée. Toutefois, elle requiert un « préposé aux télécopies » ou une autre personne pour distribuer les télécopies entrantes aux utilisateurs au sein de l’organisation sur la base des informations incluses dans la page de garde de la télécopie ou dans le message de télécopie proprement dit.

> [!NOTE]
> L’utilisation d’un numéro de télécopie central avec une reconnaissance optique de caractères (OCR) n’est pas disponible dans la messagerie unifiée Exchange. Ce type de configuration peut utiliser un numéro de télécopieur central. Toutefois, au lieu qu’une personne route la télécopie vers le destinataire, le logiciel de télécopie reçoit la télécopie, effectue l’OCR, puis tente de localiser le destinataire sur la base des informations figurant dans la page de garde ou dans le message de télécopie.


L’utilisation d’un numéro de télécopie unique pour l’ensemble de l’organisation est utile dans les situations suivantes :

  - Un utilisateur au sein de l’organisation reçoit trop de télécopies dans sa boîte aux lettres pour les gérer efficacement.

  - Un utilisateur reçoit trop de télécopies indésirables dans sa boîte aux lettres.

  - Les besoins de l’entreprise sont trop complexes pour garantir la création d’une règle de transport pour accepter les télécopies entrantes et les router vers la boîte aux lettres prévue. Cela risque de ne pas être pratique, par exemple, si votre organisation requiert le routage de certaines télécopies vers un groupe et d’autres vers un autre. Pour plus d’informations, voir [Règles de transport ou de flux de messagerie](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md).

  - Le filtrage de messages de télécopie à l’aide d’Outlook n’est pas efficace.

Retour au début

## Journalisation des messages de télécopie de messagerie unifiée

De nombreuses organisations qui implémentent la journalisation peuvent également utiliser une messagerie unifiée pour consolider leur infrastructure de messagerie électronique, de messagerie vocale et de télécopie. Cependant, vous pouvez ne pas vouloir que le traitement de la journalisation génère des états de journal pour les messages générés par la messagerie unifiée. Dans ce cas, vous pouvez décider de journaliser les messages vocaux et les messages de notification d’appel en absence qui sont traités par un serveur de boîtes aux lettres, ou d’ignorer de tels messages. Si votre organisation n’exige pas la journalisation des messages vocaux et des notifications d’appels en absence, vous pouvez réduire l’espace disque requis pour stocker les états de journal en ignorant ces messages. Lorsque vous activez ou désactivez la journalisation des messages vocaux et des messages de notification d’appel en absence, votre changement s’applique à tous les services de transport dans votre organisation. Pour plus d’informations, voir [Journalisation](journaling-exchange-2013-help.md).

> [!NOTE]
> Les messages contenant des télécopies qui sont générés par un serveur de boîtes aux lettres sont toujours journalisés, même si vous configurez une règle de journal qui spécifie de ne pas journaliser les messages vocaux de messagerie unifiée et les messages de notification d’appel en absence.


Retour au début

