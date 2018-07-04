---
title: 'Plans de numérotation de messagerie unifiée: Exchange 2013 Help'
TOCTitle: Plans de numérotation de messagerie unifiée
ms:assetid: ed7afc03-94af-4b23-8745-6a61f203c149
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb125151(v=EXCHG.150)
ms:contentKeyID: 50479499
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Plans de numérotation de messagerie unifiée

 

_**Sapplique à :** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2013-02-21_

Les plans de numérotation de messagerie unifiée constituent le composant principal de la messagerie unifiée et sont indispensables pour un déploiement correct de la messagerie unifiée sur votre réseau. Les sections suivantes présentent les plans de numérotation de messagerie unifiée et la façon dont ils sont utilisés dans un déploiement de messagerie unifiée.

## Vue d’ensemble des plans de numérotation de messagerie unifiée

Un plan de numérotation de messagerie unifiée représente un ensemble de PBX (autocommutateurs privés) ou de PBX IP qui ont des numéros d’extension utilisateur communs. Tous les postes d’utilisateurs hébergés sur les PBX ou PBX IP dans un plan de numérotation contiennent le même nombre de chiffres. Les utilisateurs peuvent appeler le poste téléphonique d’autres utilisateurs sans ajouter de numéro ni composer un numéro de téléphone complet.

Les plans de numérotation de messagerie unifiée reflètent les plans de numérotation téléphoniques. Un plan de numérotation téléphonique est configuré sur un PBX ou un PBX IP.

Dans la messagerie unifiée, les topologies de plan de numérotation de messagerie unifiée peuvent être les suivantes :

  - un plan de numérotation unique représentant un sous-ensemble des postes ou tous les postes d'une organisation disposant d'un PBX ou d'un PBX IP.

  - un plan de numérotation unique représentant un sous-ensemble des postes ou tous les postes d'une organisation disposant de plusieurs PBX ou PBX IP en réseau.

  - plusieurs plans de numérotation représentant un sous-ensemble des postes ou tous les postes d'une organisation disposant d'un PBX ou d'un PBX IP.

  - plusieurs plans de numérotation représentant un sous-ensemble des postes ou tous les postes d'une organisation disposant de plusieurs PBX ou PBX IP.

Les utilisateurs appartenant au même plan de numérotation ont les caractéristiques suivantes :

  - un numéro de poste qui identifie de manière unique la boîte aux lettres de l’utilisateur dans le plan de numérotation.

  - la capacité de passer des appels ou d’envoyer des messages vocaux à d’autres membres du plan de numérotation en utilisant uniquement le numéro de poste.

Pour plus d'informations sur l'activation de la messagerie unifiée pour un utilisateur, consultez la rubrique [Activation de la messagerie vocale pour un utilisateur](enable-a-user-for-voice-mail-exchange-2013-help.md).

Des plans de numérotation de messagerie unifiée sont utilisés dans la messagerie unifiée pour garantir que les postes téléphoniques des utilisateurs sont uniques. Dans certains réseaux téléphoniques, plusieurs PBX ou PBX IP sont présents. Dans ces réseaux de téléphonie, deux utilisateurs peuvent posséder le même numéro de poste. Les plans de numérotation de messagerie unifiée résolvent cette situation. Placer les deux utilisateurs dans deux plans de numérotation de messagerie unifiée distincts rend leur extension unique.

## Fonctionnement des plans de numérotation

Lorsque vous intégrez un réseau téléphonique à la messagerie unifiée, un ou plusieurs périphériques matériels, appelés passerelles VoIP ou PBX IP, doivent connecter votre réseau téléphonique à votre réseau IP à commutation de paquets. Les passerelles VoIP convertissent les protocoles de commutation par circuits à partir d’un PBX sur le réseau téléphonique en protocole de commutation par paquets tel qu’IP. Les PBX IP convertissent également des protocoles de commutation par circuits en un protocole de commutation par paquets. Les contrôleurs de frontière de session (SBC) vous permettent de connecter deux réseaux IP ensemble sur un WAN public ou privé, qui se retrouvent dans les déploiements en ligne ou hybrides de messagerie unifiée. Chaque passerelle VoIP, PBX IP ou contrôleur SBC de votre organisation est représenté par une passerelle IP de messagerie unifiée. Pour plus d’informations sur les passerelles IP de messagerie unifiée, consultez la rubrique [Passerelles IP de messagerie unifiée](um-ip-gateways-exchange-2013-help.md).

La messagerie unifiée exige de créer au moins un plan de numérotation de messagerie unifiée. Quand vous créez un ou plusieurs plans de numérotation, tous les serveurs Exchange de votre organisation répondent aux appels entrants. Vous devez également disposer d’une ou plusieurs passerelles IP de messagerie unifiée associées au plan de numérotation. Dans les déploiements locaux et hybrides, après avoir installé vos serveurs Exchange et associé une passerelle IP de messagerie unifiée, tous les serveurs Exchange répondent aux appels entrants pour tous les plans de numérotation. Cependant, pour les déploiements locaux et hybrides, lorsque vous intégrez Exchange et Lync Server, vous devez créer des plans de numérotation URI SIP.

> [!NOTE]
> Lorsque vous créez un plan de numérotation de messagerie unifiée, une stratégie de boîte aux lettres de messagerie unifiée par défaut est également créée. La stratégie de boîte aux lettres de messagerie unifiée est nommée Stratégie par défaut &lt;<em>Dial Plan Name</em>&gt;. Cette stratégie de boîte aux lettres de messagerie unifiée peut être supprimée ou configurée différemment.


Lorsque vous créez la première passerelle IP de messagerie unifiée et que vous spécifiez un plan de numérotation de messagerie unifiée au moment où vous la créez, un groupe de recherche de messagerie unifiée par défaut est également créé. La création de ces composants permet aux serveurs Exchange de recevoir les appels d’une passerelle VoIP, d’un PBX IP ou d’un SBC, puis de traiter les appels entrants des utilisateurs associés au plan de numérotation de messagerie unifiée. Dans les déploiements locaux ou hybrides, quand un appel parvient à la passerelle VoIP, au PBX IP ou au SBC, il transfère l’appel à un serveur d’accès au client. Le serveur d’accès au client transfère ensuite l’appel à un serveur de boîte aux lettres et ce dernier essaie d’associer le numéro de poste de l’utilisateur au plan de numérotation de messagerie unifiée correspondant.

## Types de plans de numérotation

Un URI (identificateur de ressource uniforme) est une chaîne de caractères (alphabétiques ou numériques) permettant d’identifier ou de nommer une ressource. Dans la messagerie unifiée, le rôle principal d’un URI est de permettre aux périphériques VoIP de communiquer avec d’autres périphériques à l’aide de protocoles spécifiques. Un URI définit le format ou le type de nom et de numérotation utilisé pour les informations d’appelant et de destinataire contenues dans un en-tête SIP (Session Initiation Protocol) pour un appel entrant ou sortant.

Les types de plan de numérotation de messagerie unifiée que vous créez dans la messagerie unifiée dépendent des types d’URI pris en charge par les passerelles VoIP ou les PBX IP de votre organisation. Le type d’URI correspond au type de chaîne envoyé par le PBX ou le PBX IP. Lorsque vous créez un plan de commutation des appels, vous devez connaître les types d’URI spécifiques pris en charge par vos PBX ou PBX IP. Il existe trois formats ou types d’URI pouvant être configurés sur des plans de numérotation de messagerie unifiée :

  - Numéro de poste (TeleExtn)

  - URI SIP

  - E.164

Par défaut, dans la messagerie unifiée, chaque fois que vous créez un plan de numérotation, celui-ci est configuré pour utiliser le type d’URI Numéro de poste. Après avoir créé un plan de commutation des appels, vous ne pouvez pas modifier le type d’URI. Vous devez supprimer le plan de numérotation existant et en créer un autre avec le type d’URI correct.

## Type d’URI Numéro de poste

Le type d’URI Numéro de poste est le type de plan de numérotation de messagerie unifiée le plus courant, et il est utilisé avec des PBX IP et des PBX. Lorsque vous configurez un plan de numérotation Numéro de poste (TelExtn), les passerelles VoIP, les PBX et les PBX IP que vous utilisez doivent prendre en charge le type d’URI TelExtn. Aujourd’hui, la plupart des PBX et PBX IP prennent en charge ce type d’URI.

Quand le PBX reçoit un appel auquel l’utilisateur à extension messagerie unifiée ne peut pas répondre, le PBX transfère l’appel à la passerelle VoIP. La passerelle VoIP (ou le PBX IP, le cas échéant) traduit l’appel du protocole de commutation par circuits vers le protocole IP. Dans l’en-tête du paquet SIP reçu par la passerelle VoIP ou le PBX IP, les informations concernant l’appelant et le destinataire sont présentées dans l’un des formats suivants :

  - Tél. : 512345

  - 512345@\<*IP address*\>

Le format Numéro de poste (TelExtn) utilisé est basé sur la configuration de la passerelle VoIP ou du PBX IP.

## Type d’URI SIP

Le protocole SIP (Session Initiation Protocol) est un protocole standard pour l’initiation de sessions utilisateur interactives impliquant des éléments multimédias tels que la vidéo, la voix, la conversation et le jeu. SIP est un protocole de type demande-réponse qui répond à des demandes de clients et des réponses de serveurs. Les clients sont identifiés par des URI SIP. Il est possible d’envoyer des demandes via tout protocole de transport tel qu’UDP ou TCP. SIP détermine le point de terminaison à utiliser pour la session en sélectionnant le support de communication et les paramètres du support.

Vous pouvez créer un plan de numérotation URI SIP si Microsoft Office Communications Server 2007 R2 ou Microsoft Lync Server sont déployés dans votre environnement. Vous pouvez également créer un plan de numérotation URI SIP si votre organisation dispose de PBX IP ou de PBX compatibles SIP. Dans ce dernier cas, votre organisation doit également prendre en charge les URI SIP et le routage SIP.

Un URI SIP est le numéro de téléphone SIP de l’utilisateur. L’URI SIP ressemble à une adresse de messagerie et est écrit au format suivant : sip*:\<user name\>@\<domain or IP address\>*:*Port*. Quand un PBX ou un PBX IP compatible SIP est utilisé pour envoyer un appel à un serveur Exchange, le périphérique envoie l’URI SIP pour la partie appelante et appelée dans l’en-tête SIP et n’inclut pas de numéros de poste.

## Type d’URI E.164

E.164 est un format de numérotation standard définissant le plan de numérotation international utilisé dans le réseau téléphonique commuté (RTC) et certains réseaux de données. E.164 définit le format des numéros de téléphone. Les numéros E.164 ne peuvent pas compter plus de 15 chiffres et sont généralement notés avec un signe plus (+) devant les chiffres du numéro de téléphone. Pour composer un numéro de téléphone au format E.164 à partir d’un téléphone, le préfixe d’appel international approprié doit être inclus dans le numéro appelé. Dans un plan de numérotation E.164 pour les systèmes téléphoniques publics, chaque numéro attribué contient un code de pays (CC), un code de destination national (NDC) et un numéro d’abonné (SN).

Lorsque vous créez un plan de commutation des appels, vous avez la possibilité de créer un plan de commutation des appels E.164. Toutefois, si vous créez et configurez un plan de commutation des appels E.164, les PBX et les PBX IP doivent prendre en charge le routage E.164. L’en-tête SIP reçu en provenance d’une passerelle VoIP associée à un plan de numérotation E.164 inclut le numéro de téléphone au format E.164 pour les informations concernant l’appelant et le destinataire. Il se présente au format suivant : Tél : +14255550123. Pour les déploiements Exchange Online avec la messagerie unifiée Exchange et Lync Server, vous devez utiliser des numéros au format E.164 correct pour les numéros Outlook Voice Access et de standard automatique.

## Sécurité VoIP

Les serveurs Exchange communiquent avec des passerelles VoIP, des PBX IP et d’autres ordinateurs Exchange en mode non sécurisé, en mode sécurisé SIP ou en mode sécurisé en fonction de la configuration du plan de numérotation de messagerie unifiée. Dans les déploiements locaux et hybrides, les serveurs d’accès au client et de boîtes aux lettres peuvent fonctionner dans n’importe quel mode de configuration d’un plan de numérotation, car les serveurs écoutent simultanément le port TCP 5060 pour les requêtes non sécurisées et le port TCP 5061 pour les requêtes sécurisées s’ils sont configurés pour démarrer en mode Double. Les serveurs d’accès au client et de boîtes aux lettres répondent à tous les appels entrants de l’ensemble des plans de numérotation de messagerie unifiée, mais ces plans peuvent présenter des paramètres de sécurité VoIP différents.

Dans les déploiements locaux et hybrides, par défaut, lorsque vous créez un plan de numérotation de messagerie unifiée, ce dernier communique en mode non sécurisé, et les serveurs d’accès au client et de boîtes aux lettres envoient et reçoivent des données des passerelles VoIP, des PBX IP et des SBC sans utiliser de chiffrement. En mode non sécurisé, le canal de support RTP (Realtime Transport Protocol) et les informations de signalisation SIP ne sont pas chiffrés. Vous pouvez utiliser la cmdlet **Get-UMDialPlan** dans l’environnement de ligne de commande Exchange Management Shell pour déterminer les paramètres de sécurité d’un plan de numérotation de messagerie unifiée.

Pour les déploiements sur site et hybrides, vous pouvez configurer un serveur de messagerie et d’accès client afin qu’il utilise Mutual TLS pour chiffrer le trafic SIP et RTP vers et provenant d’autres appareils et serveurs. Lorsque vous configurez le plan de numérotation afin qu’il utilise le mode sécurisé SIP, seul le trafic de signalisation SIP sera chiffré et les canaux de support RTP continueront à utiliser le protocole TCP, qui n’est pas chiffré. Toutefois, lorsque vous configurez le plan de numérotation afin qu’il utilise le mode sécurisé, le trafic de signalisation SIP et les canaux de support RTP sont chiffrés. Un canal de signalisation sécurisé utilisant SRTP (Secure Realtime Transport Protocol) utilise également Mutual TLS pour chiffrer les données VoIP.

Vous pouvez configurer le mode de sécurité VoIP lorsque vous créez un nouveau plan de numérotation ou après avoir créé un plan de numérotation à l’aide d’EAC ou de la cmdlet **Set-UMDialPlan**. Lorsque vous configurez le plan de numérotation de messagerie unifiée afin qu’il utilise le mode sécurisé SIP ou le mode sécurisé, les serveurs de messagerie unifiée qui sont associés au plan de numérotation de messagerie unifiée chiffrent le trafic de signalisation SIP ou les canaux de support RTP, ou bien les deux. Toutefois, pour qu’un serveur de messagerie unifiée puisse recevoir et envoyer des données chiffrées, vous devez configurer correctement le plan de numérotation de messagerie unifiée et les appareils de sorte que les passerelles IP ou les PBX IP puissent prendre en charge Mutual TLS.

## Outlook Voice Access

Il existe deux types d’appelants qui accèdent au système de messagerie vocale à l’aide du numéro Outlook Voice Access configuré sur un plan de numérotation de messagerie unifiée : les appelants non authentifiés et les appelants authentifiés. Lorsque des appelants composent le numéro Outlook Voice Access configuré dans un plan de numérotation, ils sont considérés comme anonymes ou non authentifiés jusqu’à ce qu’ils entrent des informations incluant leur numéro de poste de messagerie vocale et leur code confidentiel. La seule option disponible pour les appelants anonymes ou non authentifiés est la fonctionnalité de recherche dans l’annuaire. Une fois que les appelants ont entré leur numéro de poste de messagerie vocale et leur code confidentiel, ils sont authentifiés et peuvent accéder à leur boîte aux lettres. Une fois qu’ils ont accédé au système de messagerie vocale, ils utilisent la fonctionnalité Outlook Voice Access.

Outlook Voice Access est une série d’invites vocales permettant à l’appelant d’accéder à des informations de messagerie électronique, de messagerie vocale, de calendrier et autres. Outlook Voice Access permet aux utilisateurs authentifiés de parcourir les informations personnelles de leur boîte aux lettres, d’établir des appels ou de localiser des utilisateurs à l’aide d’entrées DTMF (numérotation en fréquences vocales), également appelées entrées à tonalité, ou d’entrées vocales.

## Numéros Outlook Voice Access

Une fois que vous avez créé un plan de numérotation de messagerie unifiée, vous devez ajouter au moins un numéro Outlook Voice Access. Les numéros Outlook Voice Access sont également appelés numéros pilotes de plan de numérotation. Ce numéro est utilisé par les utilisateurs Outlook Voice Access pour accéder à leur boîte aux lettres, et il leur permet d’effectuer des recherches dans l’annuaire.

Par défaut, lorsque vous créez un plan de numérotation de messagerie unifiée, aucun numéro Outlook Voice Access n’est configuré. Pour permettre aux utilisateurs d’utiliser la fonctionnalité Outlook Voice Access, vous devez configurer au moins un numéro de téléphone ou un numéro de poste. Le nombre de caractères alphanumériques dans le numéro Outlook Voice Access ne peut pas dépasser 20. Lorsque vous configurez ce numéro sur le plan de numérotation, il s’affiche dans les options de messagerie vocale de Microsoft Outlook et d’Outlook Web App.

Vous pouvez utiliser le champ **Numéros Outlook Voice Access** du plan de numérotation de messagerie unifiée pour ajouter un numéro de téléphone ou d’extension qu’un utilisateur appellera pour accéder au système de messagerie vocale via Outlook Voice Access. Dans la plupart des cas, vous entrez un numéro de poste ou un numéro de téléphone externe. Toutefois, dans la mesure où ce champ accepte tous les caractères alphanumériques, un URI SIP peut être utilisé si vous utilisez un PBX IP, un PBX compatible SIP, Office Communications Server 2007 R2 ou Microsoft Lync Server.

En fonction des besoins de votre organisation, vous pouvez configurer un ou plusieurs numéros Outlook Voice Access. Vous pouvez utiliser un seul ou plusieurs numéros Outlook Voice Access dans un même plan de numérotation de messagerie unifiée, mais vous ne pouvez pas utiliser un seul numéro Outlook Voice Access qui recouvre plusieurs plans de numérotation de messagerie unifiée.

