---
title: 'Concepts et composants en matière de téléphonie: Exchange 2013 Help'
TOCTitle: Concepts et composants en matière de téléphonie
ms:assetid: ce70bf6a-db85-411b-8b93-2987703963a9
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb124606(v=EXCHG.150)
ms:contentKeyID: 54652777
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Concepts et composants en matière de téléphonie

 

_**Sapplique à :** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2013-04-25_

Si vous planifiez et déployez la messagerie unifiée MicrosoftExchange 2013 sur votre réseau, vous devez comprendre le fonctionnement des réseaux de téléphonie et de la messagerie unifiée. Cette rubrique offre une vue d'ensemble des composants et des concepts relatifs à l'infrastructure de téléphonie qui vous aideront à planifier et à déployer des serveurs exécutant la messagerie unifiée Exchange 2013.

**Contenu de cette rubrique**

Présentation

Concepts et composants

Réseaux de commutation par circuits

Réseaux de commutation par paquets

PBX

IP/PBX

PBX compatibles SIP

VoIP

Passerelles VoIP

## Présentation

Dans les versions de Microsoft Exchange antérieures à Exchange Server 2007, la principale responsabilité de l'administrateur d'Exchange était la gestion des messages électroniques et, parfois, la gestion d'une infrastructure réseau. Les versions antérieures d'Exchange ne disposaient pas des fonctionnalités de messagerie unifiée. Les administrateurs d'Exchange Server version 5.5, d'Exchange 2000 Server et d'Exchange Server 2003 devaient se concentrer sur l'environnement et l'infrastructure de réseau d'Exchange et s'appuyer sur les consultants en téléphonie pour gérer l'infrastructure ainsi que l'environnement de téléphonie.

## Concepts et composants

Pour déployer correctement la messagerie unifiée dans Exchange 2013, vous devez bien connaître les concepts de téléphonie et les composants téléphoniques de base. Une fois que vous avez acquis une bonne compréhension de la notion de téléphonie, vous pouvez intégrer avec succès la messagerie unifiée Exchange 2013 dans une organisation Exchange 2013. Les concepts de base et les composants sont les suivants :

  - Réseaux de commutation de circuits et de commutation de paquets

  - PBX (Private Branch eXchange)

  - PBX IP

  - VoIP (Voice over Internet Protocol)

  - Passerelles VoIP

## Réseaux de commutation par circuits

Dans les réseaux de commutation de circuits, tels que le réseau téléphonique commuté (RTC), plusieurs appels sont transmis via le même moyen de transmission. Le cuivre est souvent utilisé comme moyen de transmission dans le RTC. Toutefois, un câble en fibre optique peut également être utilisé.

Un réseau de commutation de circuits est un réseau utilisant une connexion dédiée. Une connexion dédiée est un circuit ou un canal installé entre deux nœuds afin de les faire communiquer. Après qu'un appel a été établi entre deux nœuds, la connexion ne peut être utilisée que par ces nœuds. Lorsque l'un des nœuds met fin à l'appel, la connexion est annulée.

> [!NOTE]
> RTC est le regroupement des réseaux téléphoniques de commutation de circuits du monde entier. Ce regroupement est similaire à Internet, le regroupement de réseaux publics de commutation de paquets basés sur le protocole IP du monde entier.


Il existe deux types de base de réseaux de commutation de circuits : analogique et numérique. Le type analogique a été conçu pour la transmission vocale. Pendant longtemps, le RTC était uniquement analogique mais, aujourd'hui, les réseaux de commutation de circuits tels que le RTC sont passés de l'analogique au numérique. Pour permettre la prise en charge d'un signal de transmission vocale analogique sur un réseau numérique, le signal de transmission analogique doit être codé ou converti dans un format numérique avant d'entrer dans le réseau WAN de téléphonie. Du côté réception de la connexion, le signal numérique doit être décodé ou reconverti en signal analogique.

Les réseaux de commutation de circuits présentent des avantages et des inconvénients. Les réseaux de commutation de circuits présentent plusieurs inconvénients. Les réseaux de commutation de circuits peuvent être relativement inefficaces en raison du gaspillage possible de la bande passante. Ce n'est pas le cas lorsque VoIP est utilisé sur un réseau de commutation de paquets. VoIP partage la bande passante disponible avec les autres applications de réseau et utilise plus efficacement la bande passante. Un autre inconvénient des réseaux de commutation de circuits est la nécessité de prévoir le nombre maximal d'appels téléphoniques requis pour les heures de pleine activité, puis payer pour l'utilisation du ou des circuits nécessaires pour prendre en charge un nombre maximal d'appels.

La commutation de circuits présente un gros avantage sur les réseaux de commutation de paquets. Dans un réseau de commutation par circuits, lorsque vous utilisez un circuit, vous disposez du circuit tout entier, sans concurrence d'autres utilisateurs. Ce n'est pas le cas avec les réseaux de commutation par paquets.

> [!NOTE]
> La hiérarchie numérique synchrone (SDH) est devenue le principal protocole de transmission pour la plupart des réseaux RTC. La SDH est acheminée via des réseaux de fibres optiques.


Présentation

## Réseaux de commutation par paquets

La commutation de paquets est une technique consistant à diviser un message de données en unités plus petites appelées paquets. Les paquets sont envoyés à leur destination par la meilleure route disponible, puis sont réassemblés côté réception.

Dans les réseaux de commutation de paquets tels qu'Internet, les paquets sont acheminés vers leur destination via la route la plus appropriée, mais tous les paquets qui voyagent entre deux hôtes n'empruntent pas la même route, même s'ils font partie d'un même message. Cela garantit presque que les paquets parviendront à destination à des moments différents et dans le désordre. Dans un réseau de commutation de paquets, les paquets (messages ou fragments de messages) sont acheminés individuellement entre les nœuds sur les liaisons de données qui peuvent être partagées par d'autres nœuds. Contrairement à la commutation de circuits, avec la commutation par paquets, plusieurs connexions aux nœuds sur le réseau partagent la bande passante disponible.

> [!NOTE]
> Avec la commutation de circuits, tous les paquets parviennent à destination dans l'ordre et par le même chemin.


Les réseaux de commutation de paquets permettent la transmission de données via Internet dans le monde entier. Un réseau de données public ou un réseau de commutation de paquets est l'équivalent au niveau des données du RTC.

Les réseaux de commutation de paquets sont également utilisés dans des environnements tels que les réseaux LAN et WAN. Un environnement de commutation de paquets WAN est basé sur des circuits téléphoniques, mais ceux-ci sont organisés de telle sorte qu'ils établissent une connexion permanente avec leur point de terminaison. Dans un environnement de commutation de paquets LAN, tels qu'un réseau Ethernet, la transmission des paquets de données est basée sur des commutateurs de paquets, des routeurs et des câbles LAN. Dans un LAN, le commutateur établit une connexion entre deux segments juste assez longs pour envoyer le paquet actuel. Les paquets entrants sont enregistrés dans une zone de mémoire temporaire ou mémoire tampon. Dans un LAN basé sur Ethernet, une structure Ethernet contient la charge utile ou la portion données du paquet et un en-tête spécial incluant les informations d'adresse du contrôle d'accès media (MAC) pour la source et la destination du paquet. Lorsque les paquets arrivent à destination, ils sont remis en ordre par un assembleur de paquets. Un assembleur de paquets est nécessaire à cause des différentes routes que les paquets peuvent emprunter.

Le réseau de commutation de paquets a permis à Internet d'exister et, par la même occasion, rendu les réseaux de données (particulièrement les réseaux IP basés sur LAN) plus disponibles et répandus.

Présentation

## PBX

Un PBX hérité est un périphérique téléphonique qui agit comme un commutateur pour la commutation des appels dans un réseau de commutation de circuits ou téléphonique.

> [!NOTE]
> Un PBX hérité est un PBX qui ne peut pas transmettre de paquets IP. Dans de nombreuses entreprises, les PBX hérités ont été remplacés par des PBX IP.


Un PBX est un périphérique téléphonique utilisé par la plupart des sociétés de taille moyenne à grande. Un PBX permet à ses utilisateurs ou abonnés de partager un certain nombre de lignes extérieures pour établir des appels téléphoniques considérés comme externes au PBX. Un PBX est une solution beaucoup moins onéreuse que le fait de donner à chaque utilisateur d'une entreprise une ligne téléphonique externe dédiée. Des combinés téléphoniques, des télécopieurs, des modems et de nombreux autres périphériques de communication peuvent être connectés à un PBX.

L'équipement PBX est généralement installé dans les locaux d'une entreprise et connecte les appels entre les téléphones situés et installés sur le site de l'entreprise. Un nombre limité de lignes extérieures, également appelées lignes spécialisées, sont généralement disponibles pour établir et recevoir des appels externes à l'entreprise à partir d'une source externe telle que le RTC.

Dans certains systèmes, les appels d'entreprise internes passés vers des numéros de téléphone externes au moyen d'un PBX utilisent le chiffre 9 ou 0 suivi du numéro externe. Une ligne spécialisée sortante est automatiquement sélectionnée pour établir l'appel. À l'inverse, les appels passés entre utilisateurs au sein de l'entreprise ne requièrent pas en général l'utilisation de touches spéciales ou d'une ligne spécialisée externe. Cela est dû au fait que les appels internes sont acheminés ou commutés par le PBX entre des téléphones physiquement connectés au PBX.

Dans les entreprises de taille moyenne à grande, les configurations suivantes du PBX sont possibles :

  - Un PBX unique prend en charge l'ensemble de l'entreprise.

  - Un regroupement de deux PBX ou plus non mis en réseau ou interconnectés.

  - Un regroupement de deux PBX ou plus interconnectés ou mis en réseau.

> [!NOTE]
> Un plan de numérotation de messagerie unifiée Exchange 2013 peut englober plusieurs PBX ou PBX IP.


Présentation

## IP/PBX

Un PBX IP est un système PBX qui prend en charge le protocole IP pour connecter des téléphones en utilisant un LAN Ethernet ou de commutation de paquets et qui envoie ses conversations vocales par paquets IP. Un PBX IP hybride prend en charge le protocole IP pour envoyer des conversations vocales par paquets, mais connecte également des téléphones analogiques traditionnels et numériques à multiplexage par répartition dans le temps (MRT) avec commutation de circuits. Un PBX IP est un équipement de commutation téléphonique résidant dans une entreprise privée qui remplace le téléphone de la société.

Les PBX IP sont souvent plus faciles à administrer que les PBX hérités, car les administrateurs peuvent aisément configurer les services PBX IP en utilisant un navigateur Internet ou un autre utilitaire IP. En outre, aucun fil, câble ou tableau de connexions supplémentaire n'est requis. Avec un PBX IP, le déplacement d'un téléphone IP est aussi simple que le fait de débrancher un téléphone pour le brancher ailleurs, sans nécessiter des services coûteux pour déplacer un téléphone de fournisseurs de PBX hérités. En outre, les entreprises qui possèdent un PBX IP ne s'exposent pas aux coûts d'infrastructure supplémentaires requis pour la maintenance et la gestion de deux réseaux de commutation de circuits et de paquets distincts.

## PBX compatibles SIP

Un PBX compatible SIP est un appareil téléphonique qui agit comme un commutateur réseau pour la commutation des appels au sein d'un réseau téléphonique ou d'un réseau à commutation de circuits. Un PBX compatible SIP diffère toutefois d'un PBX classique en ce qu'il peut se connecter à Internet et utiliser le protocole SIP pour passer des appels sur ce réseau.

Les PBX compatibles SIP utilisent un format d'appel qui inclut un URI SIP contenant un numéro E.164 global et le paramètre « user=phone ». Par exemple : sip:+14255551234@contoso.com;user=phone

Le numéro E164 commence par un signe « + » et ne contient pas de paramètre de contexte téléphonique ou de séparateurs. Les PBX compatibles SIP prennent en charge les protocoles TCP et UDP. L'utilisation du protocole UDP est encore très répandue dans les systèmes hérités. Les PBX compatibles SIP prennent également en charge la sécurité via l'authentification TLS (Transport Layer Security) mutuelle et les recherches DNS.

## VoIP

Voice over Internet Protocol (VoIP) est une technologie qui contient du matériel et des logiciels qui permettent d'utiliser un réseau IP comme moyen de transmission pour les appels téléphoniques. Avec la technologie VoIP, les données vocales sont envoyées par paquets à l'aide du protocole IP au lieu des transmissions par circuit traditionnelles ou des lignes téléphoniques de commutation de circuits du RTC. Une passerelle VoIP que vous connectez à votre réseau IP utilise des protocoles VoIP pour échanger des paquets de données entre un serveur d'accès au client et un serveur de boîtes aux lettres Exchange 2013 et un système PBX.

## Passerelles VoIP

Une passerelle VoIP est un périphérique ou produit matériel tiers qui connecte un PBX hérité à votre LAN. La passerelle VoIP permet au système PBX de communiquer avec vos serveurs d'accès au client et vos serveurs de boîtes aux lettres Exchange 2013 exécutant le service routeur des appels de messagerie unifiée et le service de messagerie unifiée Microsoft Exchange.

> [!NOTE]
> La passerelle VoIP peut également se connecter à des systèmes PBX qui utilisent la VoIP au lieu des protocoles de commutation par circuits RTC.


La messagerie unifiée Exchange 2013 s'appuie sur la capacité des passerelles VoIP à traduire ou convertir les protocoles basés sur le MRT ou la commutation par circuits téléphoniques comme RNIS et QSIG à partir d'un PBX en protocoles basés sur IP ou VoIP, tels que SIP (Session Initiated Protocol), RTP (Realtime Transport Protocol) ou T.38 pour la transmission de télécopies en temps réel. La passerelle VoIP fait partie intégrante de la fonctionnalité et du fonctionnement de la messagerie unifiée.

> [!IMPORTANT]
> L'installation de la passerelle VoIP, du PBX IP ou du PBX compatible SIP doit être suivie de la création d'une passerelle IP de messagerie unifiée représentant le périphérique physique. Après la création de la passerelle IP de messagerie unifiée, les serveurs d'accès au client et de boîtes aux lettres associés à la passerelle IP de messagerie unifiée envoient une requête SIP OPTIONS à la passerelle VoIP, au PBX IP ou au PBX compatible SIP pour s'assurer qu'ils répondent. Si la passerelle VoIP ne répond pas à la requête SIP OPTIONS à partir du serveur de boîtes aux lettres, celui-ci consigne un événement avec l'ID 1088 indiquant que la demande a échoué. Pour résoudre ce problème, vérifiez que la passerelle VoIP ou le PBX IP est accessible et en ligne et que la configuration de la messagerie unifiée sur le serveur d'accès au client et sur le serveur de boîtes aux lettres est correcte.


Pour plus d'informations sur les configurations des PBX IP et des PBX, consultez la rubrique [Configuration des PBX et PBX IP](pbx-and-ip-pbx-configurations-exchange-2013-help.md).

Présentation

## Pour plus d'informations

[Protocoles, ports et services de messagerie unifiée](um-protocols-ports-and-services-exchange-2013-help.md)

[Gestionnaire de téléphonie pour Exchange 2013](telephony-advisor-for-exchange-2013-exchange-2013-help.md)

