---
title: 'Passerelles IP de messagerie unifiée: Exchange 2013 Help'
TOCTitle: Passerelles IP de messagerie unifiée
ms:assetid: 991d77e0-3995-44ab-bedf-52ff7a0301ab
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb123890(v=EXCHG.150)
ms:contentKeyID: 50478776
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Passerelles IP de messagerie unifiée

 

_**Sapplique à :**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :**2014-06-24_

Une passerelle IP de messagerie unifiée représente un périphérique matériel de passerelle VoIP, de PBX IP ou de contrôleur de limite de session (SBC) physique. Pour pouvoir utiliser une passerelle VoIP, un PBX IP ou un SBC afin de répondre aux appels entrants et d'effectuer des appels sortants pour les utilisateurs de messagerie vocale, une passerelle IP de messagerie unifiée doit être créée dans le service d'annuaire.

**Table des matières**

Présentation des passerelles IP de messagerie unifiée

Passerelles IP de messagerie unifiée

Prise en charge d'IPv6 pour les passerelles IP de messagerie unifiée

Activation et désactivation d'une passerelle IP de messagerie unifiée

## Présentation des passerelles IP de messagerie unifiée

En général, le terme *« passerelle »* décrit un périphérique physique connectant deux réseaux incompatibles. Avec la messagerie unifiée Exchange et les autres solutions de messagerie unifiée, la passerelle VoIP est utilisée pour faire la conversion entre le réseau téléphonique de type réseau téléphonique commuté (RTC)/multiplexage par répartition dans le temps (MRT) ou basé sur la commutation de circuits, et un réseau de données IP (Internet Protocol) ou à commutation de paquets. Un PBX IP fait également la conversion entre le réseau RTC et un réseau à commutation de paquets de sorte que lorsqu’un PBX IP est utilisé, aucune passerelle VoIP n’est requise. Une passerelle VoIP est uniquement nécessaire si vous connectez un périphérique matériel PBX hérité à votre déploiement de messagerie unifiée.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Un réseau à commutation de paquets est un réseau dans lequel les paquets (messages ou fragments de messages) sont individuellement routés entre des périphériques tels que des routeurs, commutateurs, passerelle VoIP, PBX IP et SBC. Il diffère d'un réseau à commutation de circuit qui configure une connexion dédiée entre deux nœuds pour leur usage exclusif le temps de la communication.</td>
</tr>
</tbody>
</table>


La messagerie unifiée Exchange s'appuie sur la capacité de la passerelle VoIP à convertir les protocoles basés sur le MRT ou la commutation de circuits, tels que le réseau numérique à intégration de services (RNIS) ou QSIG, à partir d'un PBX en protocoles basés sur IP ou VoIP, tels que SIP (Session Initiation Protocol), RTP (Realtime Transport Protocol) ou T.38 pour la transmission de télécopies en temps réel.

Les PBX IP sont également utilisés lors de la connexion d'un réseau téléphonique basé sur la commutation de circuits à un réseau de données ou à commutation de paquets. Ils sont également utilisés pour convertir les protocoles basés sur la commutation de circuits en protocoles basés sur VoIP ou IP, tels que SIP, RTP et SRTP.

Les SBC sont un peu différents des passerelles VoIP et PBX IP. Au lieu de connecter un réseau à commutation de circuits à un réseau à commutation de paquets, ils sont utilisés pour connecter deux réseaux de données sur un réseau public tel qu’Internet ou sur un réseau étendu (WAN) privé. En messagerie unifiée, les SBC sont utilisés dans un déploiement hybride dans lequel la messagerie unifiée utilise certains composants sur site et d'autres, tels que les boîtes aux lettres, situés dans le nuage.

## Configurations de périphériques VoIP

Bien qu'il existe différents types et fabricants de PBX, passerelles VoIP, PBX IP et SBC, les configurations de périphériques VoIP de base sont au nombre de trois :

  - **PBX IP**   Périphérique unique qui effectue la conversion entre le réseau téléphonique RTC/MRT ou basé sur la commutation de circuits et un réseau de données IP ou à commutation de paquets

  - **PBX (hérité) et passerelle VoIP**   Deux composants distincts qui, ensemble, effectuent la conversion entre le réseau téléphonique RTC/MRT ou basé sur la commutation de circuits et un réseau de données IP ou à commutation de paquets

  - **SBC**   Un ou plusieurs périphériques qui connectent deux types de réseaux IP tels qu'un LAN et un centre de données.

Pour prendre en charge la messagerie unifiée, l'un ou les deux types de configurations de périphériques IP/VoIP sont utilisés lors de la connexion d'une infrastructure de réseau téléphonique à une infrastructure de réseau de données ou lors de la connexion d'un déploiement sur site à un déploiement de messagerie unifiée dans le nuage.

## Passerelles IP de messagerie unifiée

La passerelle IP de messagerie unifiée contient un ou plusieurs groupements de postes et paramètres de configuration de messagerie unifiée. Les groupements de postes de messagerie unifiée sont utilisés pour lier une passerelle IP de messagerie unifiée à un plan de numérotation de messagerie unifiée. L'association de la passerelle IP de messagerie unifiée et d'un groupement de postes de messagerie unifiée établit un lien entre une passerelle VoIP, un PBX IP, ou un SBC et un plan de numérotation de messagerie unifiée. En créant plusieurs groupements de postes de messagerie unifiée, vous pouvez associer une passerelle IP de messagerie unifiée unique à plusieurs plans de commutation des appels de messagerie unifiée.

Une fois que vous aurez créé une passerelle IP de messagerie unifiée, les serveurs Exchange liés à cette dernière envoient une demande SIP OPTIONS à la passerelle VoIP, au PBX IP ou au SBC pour s'assurer que le périphérique répond. Si la passerelle VoIP, le PBX IP ou le SBC ne répond pas à la demande, un serveur Exchange journalise un événement avec l'ID 1400 indiquant que la demande a échoué. Le cas échéant, vérifiez que la passerelle VoIP, le PBX IP ou le SBC est disponible et en ligne et que la messagerie unifiée est correctement configurée.

Un serveur de boîtes aux lettres communique uniquement avec les passerelles VoIP, les PBX IP ou les SBC répertoriés comme homologues SIP approuvés. Dans certains cas, si deux passerelles VoIP, PBX IP ou SBC sont configurés pour utiliser la même adresse IP, un événement avec l'ID 1175 sera journalisé. La messagerie unifiée protège contre les demandes non autorisées en récupérant l'URL interne du répertoire virtuel des services web de messagerie unifiée et utilise ensuite l'URL pour construire la liste des noms de domaines complets pour les homologues SIP approuvés. Lorsque deux noms de domaines complets sont résolus sur la même adresse IP, cet événement est journalisé.

## Prise en charge d'IPv6 pour les passerelles IP de messagerie unifiée

Le protocole IPv6 (Internet Protocol Version 6) est la version la plus récente du protocole Internet (IP). IPv6 est conçu pour corriger un grand nombre d'insuffisances d'IPv4, la précédente version du protocole Internet. Dans les déploiements locaux et hybrides Microsoft Exchange Server 2010, IPv6 n'était pris en charge que quand IPv4 était également utilisé.

Dans les déploiements locaux et hybrides Exchange 2013, les composants de messagerie unifiée et les services de reconnaissance vocale s'exécutent uniquement sur des serveurs d'accès au client et de boîtes aux lettres. Parce que l’architecture de messagerie unifiée a changé et requiert désormais Unified Communications Managed API (UCMA) v4.0 pour prendre en charge les protocoles IPv4 et IPv6, ainsi que d’autres fonctionnalités Exchange, les serveurs d’accès au client et de boîtes aux lettres dotés de services et de composants de messagerie unifiée prennent intégralement en charge les réseaux IPv6 et ne requièrent pas IPv4.

Dans les déploiements locaux, hybrides et Exchange Online, les administrateurs d'entreprise et Exchange Online de messagerie unifiée peuvent utiliser IPv6 lorsqu'ils connectent la messagerie unifiée à des périphériques compatibles IPv6, notamment des périphériques comme les routeurs, les passerelles IP, les PBX IP et les serveurs Microsoft Office Communications Server 2007 R2 et Microsoft Lync. Cependant, pour des raisons d'interopérabilité et de compatibilité descendante, le protocole IPv4 peut être utilisé sans effectuer d'autres modifications de la configuration si le paramètre *IPAddressFamily* est défini sur `Any` sur les passerelles IP de messagerie unifiée.

La messagerie unifiée Exchange doit toujours communiquer directement avec les homologues SIP (passerelles VoIP, PBX IP et SBC) dont le logiciel ou le microprogramme peut ne pas prendre en charge IPv6. Le cas échéant, la messagerie unifiée doit pouvoir communiquer directement avec les homologues SIP qui utilisent IPv4. Pour la messagerie vocale hébergée, la messagerie unifiée communique avec l'équipement client via des SBC, Lync Server 2010 ou Lync Server 2013. Dans les environnements hébergés, les clients SIP IPv6 tels que les SBC et les serveurs Lync peuvent être déployés pour gérer le processus de conversion IPv6 vers IPv4.

Pour les déploiements locaux et hybrides suite à l'installation de vos serveurs d'accès au client et de boîtes aux lettres, ainsi que pour les déploiements de messagerie unifiée Exchange Online, vous devez créer des passerelles IP de messagerie unifiée. Si vous voulez que vos passerelles IP de messagerie unifiée prennent en charge IPv6, vous devez également :

1.  Créez une nouvelle passerelle IP de messagerie unifiée ou configurez une passerelle IP de messagerie unifiée existante avec une adresse IPv6 pour chacune des passerelles IP, PBX IP ou SBC de votre réseau. Lorsque vous créez et configurez les passerelles IP de messagerie unifiée requises, vous devez ajouter l’adresse IPv6 ou le nom de domaine complet de la passerelle IP de messagerie unifiée. Si vous ajoutez le nom de domaine complet à la passerelle IP de messagerie unifiée, vous devez avoir créé les enregistrements DNS corrects pour résoudre le nom de domaine complet de la passerelle IP de messagerie unifiée en adresse IPv6. Si vous disposez d'une passerelle IP de messagerie unifiée existante, vous pouvez utiliser la cmdlet **Set-UMIPgateway** pour configurer l'adresse IPv6 ou le nom de domaine complet.

2.  Configurez le paramètre *IPAddressFamily* sur chaque passerelle IP de messagerie unifiée. Pour que la passerelle VoIP accepte les paquets IPv6, vous devez configurer la passerelle IP de messagerie unifiée de sorte qu'elle accepte les connexions IPv4 et IPv6 ou uniquement les connexions IPv6, en utilisant la cmdlet **Set-UMIPgateway**.

3.  Une fois que vous avez configuré vos passerelles IP de messagerie unifiée, vous devez également configurer les passerelles VoIP, les PBX IP et les SBC sur votre réseau pour prendre en charge IPv6. Pour plus d'informations, demandez au fournisseur du matériel une liste de périphériques qui prennent en charge IPv6 expliquant comment les configurer.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Le nombre maximum de passerelles IP de messagerie unifiée par plan de numérotation est de 200. Si vous en créez plus de 200, le service de messagerie unifiée ne démarre pas.</td>
</tr>
</tbody>
</table>


## Activation et désactivation d'une passerelle IP de messagerie unifiée

Par défaut, une passerelle IP de messagerie unifiée est activée après sa création. La passerelle IP de messagerie unifiée peut toutefois être activée ou désactivée. Si vous désactivez une passerelle IP de messagerie unifiée, vous pouvez la configurer pour forcer tous les serveurs Exchange à abandonner les appels existants. Sinon, vous pouvez la configurer pour forcer tous les serveurs Exchange associés à la passerelle IP de messagerie unifiée à arrêter de gérer tout nouvel appel présenté par la passerelle VoIP, le PBX IP ou le SBC.

Si vous intégrez la messagerie unifiée à Office Communications Server R2 ou à Microsoft Lync Server, vous ne devez autoriser qu’une seule passerelle IP de messagerie unifiée à émettre des appels pour les utilisateurs et désactiver les appels sortants sur toutes les autres passerelles IP de messagerie unifiée associées à vos plans de numérotation URI SIP. Utiliser l'environnement de ligne de commande Exchange Management Shell ou le Centre d'administration Exchange pour désactiver les appels sortants.

Lorsque vous choisissez la passerelle IP de messagerie unifiée à travers laquelle autoriser les appels sortants pour les déploiements locaux et hybrides, choisissez celle qui est susceptible de gérer le plus de trafic. N’autorisez pas le trafic sortant via une passerelle IP de messagerie unifiée qui se connecte à un pool de directeurs Lync Server. Il est nécessaire de s'assurer que les appels sortants vers des utilisateurs externes, émis par un serveur de boîtes aux lettres exécutant le service de messagerie unifiée Microsoft Exchange (par exemple, dans des scénarios d'appels d'émission au téléphone), traversent le pare-feu d'entreprise de façon fiable.

