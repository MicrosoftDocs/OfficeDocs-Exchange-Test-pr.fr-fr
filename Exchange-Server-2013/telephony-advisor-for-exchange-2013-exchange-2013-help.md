---
title: 'Gestionnaire de téléphonie pour Exchange 2013: Exchange 2013 Help'
TOCTitle: Gestionnaire de téléphonie pour Exchange 2013
ms:assetid: e9f760f2-5901-4ed2-95a5-724555cc700e
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Ee364753(v=EXCHG.150)
ms:contentKeyID: 50555514
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Gestionnaire de téléphonie pour Exchange 2013

 

_**Sapplique à :** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2017-07-25_

La messagerie unifiée nécessite d'intégrer Microsoft Exchange au système de téléphonie existant de votre organisation. Un déploiement réussi nécessite une analyse attentive de votre infrastructure de téléphonie existante et d'effectuer les étapes de planification correctes pour déployer la messagerie unifiée.

La phase de planification peut représenter un défi important pour les administrateurs Exchange ayant peu ou pas d'expérience du réseau téléphonique. Pour relever ce défi, consultez la rubrique Resources to Help with Your UM Deployment plus loin dans cette rubrique.

Pour consulter les passerelles VoIP prises en charge pour la messagerie unifiée, déterminer si votre PBX est pris en charge via un modèle ou un fabricant de passerelle VoIP spécifique ou si votre PBX IP est pris en charge via une connexion SIP directe, ou pour identifier les contrôleurs de frontière de session (SBC) pris en charge pour la messagerie unifiée Exchange Online, cliquez sur l'un des liens suivants :

  - Supported VoIP gateways

  - Supported PBXs when using an AudioCodes VoIP gateway

  - Supported PBXs when using a dialogic VoIP gateway
    
      - PBXs supported when using a DMG1000 series Media Gateway
    
      - PBXs supported when using a DMG 2000 series Media Gateway
    
      - PBXs supported when using a DMG3000 series Media Gateway

  - Supported IP PBXs

  - Supported IP PBXs when using SIP media gateways

  - Exchange Unified Messaging, Office Communications Server 2007 R2, and Microsoft Lync Server

## Ressources pour faciliter le déploiement de votre messagerie unifiée

Il est difficile de créer des instructions pour déployer des réseaux téléphoniques. Ils peuvent être très différents les uns des autres parce qu'ils peuvent inclure des passerelles VoIP, des PBX IP et des PBX dont les paramètres de configuration, le microprogramme et la configuration requise diffèrent. Cependant, plusieurs ressources sont disponibles pour vous aider à réussir le déploiement de la messagerie unifiée :

  - **Spécialistes de la messagerie unifiée**   Les spécialistes de la messagerie unifiée sont des intégrateurs système qui ont reçu une formation technique sur la messagerie unifiée Exchange menée par l'équipe d'ingénieurs Exchange. Pour permettre une transition homogène vers la messagerie unifiée à partir de systèmes de messagerie vocale hérités, Microsoft recommande à tous ses clients de s'adjoindre les services d'un spécialiste de la messagerie unifiée. Pour obtenir des informations sur les contacts, consultez la page [Spécialistes de la messagerie unifiée Microsoft Exchange Server 2013](https://go.microsoft.com/fwlink/p/?linkid=262708) ou [Microsoft Pinpoint pour la messagerie unifiée](https://go.microsoft.com/fwlink/p/?linkid=261951).

  - **Notes de configuration des passerelles VoIP, des PBX IP et des PBX pris en charge**   Ces notes de configuration contiennent des paramètres de configuration et d'autres informations très utiles lors de la configuration des passerelles VoIP, des PBX IP et des PBX pour communiquer avec les serveurs de messagerie unifiée situés sur votre réseau. Pour plus d'informations, consultez la rubrique [Notes de configuration pour les passerelles VoIP, les PBX IP et les PBX pris en charge](configuration-notes-for-supported-voip-gateways-ip-pbxs-and-pbxs-exchange-2013-help.md).

  - **Notes de configuration pour les contrôleurs de frontière de session pris en charge**   Ces notes de configuration contiennent des paramètres de configuration et d'autres informations très utiles lors de la configuration de contrôleurs de frontière de session pour communiquer avec les serveurs de messagerie unifiée situés dans des déploiements de messagerie unifiée hybrides et Exchange Online. Pour plus d'informations, consultez la rubrique [Notes de configuration pour les contrôleurs de frontière de session pris en charge](configuration-notes-for-supported-session-border-controllers-exchange-2013-help.md).
    
    > [!NOTE]
    > Messagerie unifiée Exchange Online de prise en charge pour les systèmes PBX tiers via des connexions directes à partir du client géré SBCs prendra fin dans 2018 de juillet. Consultez le blog d’équipe Exchange <a href="https://blogs.technet.microsoft.com/exchange/2017/07/18/discontinuation-of-support-for-session-border-controllers-in-exchange-online-unified-messaging/">d’arrêt de la prise en charge des contrôleurs de bordure session Exchange Online de la messagerie unifiée</a> pour plus d’informations.


Avant de consulter un spécialiste de messagerie unifiée, vous devez pouvoir répondre aux questions clés qu'ils vous poseront. Cela vous permettra de rendre la conversation plus productive :

  - Combien existe t-il d'utilisateurs de téléphone ou de messagerie vocale, ou les deux, dans votre organisation ?

  - À combien d'utilisateurs envisagez-vous de fournir la messagerie unifiée ?

  - Quels PBX envisagez-vous d'utiliser pour l'intégration avec la messagerie unifiée ?

  - De combien de PBX dispose votre organisation ? Spécifiez les fournisseurs, types (circuit ou IP), modèles et versions de microprogramme.

  - Les PBX sont-ils mis en réseau, centralisés ou situés dans plusieurs emplacements ?

  - Quels systèmes de messagerie vocale sont actuellement utilisés par votre organisation ? Spécifiez les fournisseurs, types, modèles et versions de microprogramme.

  - Comment les systèmes de messagerie vocale sont-ils intégrés dans vos PBX (Analogique, T1/E1, PRI, Digital set emulation, VoIP, autre) ?

  - Utilisez-vous actuellement des réseaux de messagerie vocale ?

  - Quel type de système de télécopie votre organisation utilise-t-elle ? Prend-il en charge l'acheminement des télécopies entrantes vers Exchange ?

  - Votre organisation utilise-t-elle des standards automatiques ?

  - Avez-vous besoin d'une prise en charge des utilisateurs de téléphone uniquement, c'est-à-dire, des utilisateurs qui n'ont pas accès à la messagerie électronique ?

## Passerelles VoIP prises en charge

L'intégration de la messagerie unifiée à des PBX nécessite l'utilisation d'une ou de plusieurs passerelles VoIP pour convertir les protocoles de commutation par circuits utilisés par des PBX basés sur le multiplexage par répartition dans le temps (MRT) en protocoles IP et à commutation de paquets utilisés par la messagerie unifiée. Des fournisseurs de passerelles VoIP disposant de plusieurs modèles de passerelles VoIP et de passerelles multimédia ont été testés et sont pris en charge pour la messagerie unifiée.

Le test de l'interopérabilité de la messagerie unifiée avec des passerelles VoIP, des PBX IP et des contrôleurs de frontière de session (SBC) est maintenant intégré au programme d'interopérabilité d'ouverture des communications unifiées de Microsoft. Pour plus d'informations, consultez la page du [programme d'interopérabilité d'ouverture des communications unifiées de Microsoft](http://go.microsoft.com/fwlink/p/?linkid=140722).

Le programme d'éligibilité au [Programme d'interopérabilité d'ouverture des communications unifiées de Microsoft](http://go.microsoft.com/fwlink/p/?linkid=140722) pour des passerelles VoIP, des PBX IP et des passerelles VoIP avancées garantit aux clients la transparence de la configuration et de la prise en charge lors de l'utilisation des passerelles et des PBX IP de téléphonie qualifiés avec des logiciels de communication unifiée de Microsoft. Seuls les produits satisfaisant à des exigences de test strictes et complètes, et conformes aux spécifications et plans de test, obtiennent cette qualification.

Pour plus d'informations sur la configuration des passerelles VoIP, des PBX IP, des PBX et des SBC, consultez l'une des ressources suivantes :

  - [Notes de configuration pour les passerelles VoIP, les PBX IP et les PBX pris en charge](configuration-notes-for-supported-voip-gateways-ip-pbxs-and-pbxs-exchange-2013-help.md)

  - [Notes de configuration pour les contrôleurs de frontière de session pris en charge](configuration-notes-for-supported-session-border-controllers-exchange-2013-help.md)

L'interopérabilité des fournisseurs de passerelles VoIP suivants a été vérifiée :

  - AudioCodes

  - Dialogic

  - Le tableau suivant présente le fournisseur de passerelles VoIP, le modèle de passerelle VoIP et les protocoles pris en charge par chaque modèle.

### Passerelles VoIP prises en charge pour la messagerie unifiée

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Fournisseur</th>
<th>Modèle</th>
<th>Protocoles pris en charge</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>AudioCodes</p></td>
<td><p>MediaPack 114/8 FXO</p></td>
<td><ul>
<li><p>Analogique avec In-Band DTMF</p></li>
<li><p>Analogique avec SMDI</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>AudioCodes</p></td>
<td><p>Mediant 1000</p></td>
<td><ul>
<li><p>Analogique avec In-Band DTMF</p></li>
<li><p>Analogique avec SMDI</p></li>
<li><p>BRI Q.SIG</p></li>
<li><p>T1/E1 Q.SIG</p></li>
<li><p>IP à IP</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>AudioCodes</p></td>
<td><p>Mediant 2000</p></td>
<td><ul>
<li><p>T1/E1 CAS</p></li>
<li><p>T1/E1 Q.SIG</p></li>
<li><p>IP à IP</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Dialogic</p></td>
<td><p>DMG1000PBXDNIW</p></td>
<td><p>Digital Set Emulation</p></td>
</tr>
<tr class="odd">
<td><p>Dialogic</p></td>
<td><p>DMG1000LSW</p></td>
<td><ul>
<li><p>Analogique avec In-Band DTMF</p></li>
<li><p>Analogique avec SMDI</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Dialogic</p></td>
<td><p>DMG2000</p></td>
<td><ul>
<li><p>T1 CAS</p></li>
<li><p>T1/E1 Q.SIG</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Dialogic</p></td>
<td><p>DMG3000</p></td>
<td><ul>
<li><p>BRI Q.SIG</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>NET</p></td>
<td><p>VX1200</p></td>
<td><ul>
<li><p>T1 Q.SIG</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Sonus</p></td>
<td><p>SBC 1000/2000 2.2.1 ou version ultérieure</p></td>
<td><ul>
<li><p>Signalisation TDM (RNIS) : AT&amp;T 4ESS/5ESS, Nortel DMS- 100, Euro IDSN (ETSI 300-102), QSIG, NTT InsNet (Japon), ANSI National ISDN-2 (NI-2)</p></li>
<li><p>Signalisation TDM (CAS) : T1 CAS (E&amp;M, démarrage en boucle) ; E1 CAS (R2)</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Quintum</p></td>
<td><p>Tenor DX Series</p></td>
<td><ul>
<li><p>T1 Q.SIG</p></li>
</ul></td>
</tr>
</tbody>
</table>


## PBX pris en charge lors de l'utilisation d'une passerelle VoIP AudioCodes

Le tableau suivant présente les PBX qui sont pris en charge avec des passerelles VoIP AudioCodes, notamment MediaPack-114 FXO, MediaPack-118 FXO et Mediant 2000.

### PBX pris en charge avec une passerelle VoIP AudioCodes

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Fabricant du PBX</th>
<th>Modèle/type de PBX</th>
<th>Modèle AudioCodes « x » - remplacer par 4 ou 8 selon le besoin « y » - remplacer par 1, 2, 4, 8 ou 16 selon le besoin</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Alcatel</p></td>
<td><p>OmniPCX 4400</p></td>
<td><ul>
<li><p>MediaPack 11x/FXO/AC/SIP-0</p></li>
<li><p>Mediant2000/ySpans/SIP</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Aastra</p></td>
<td><p>M1000, M2000</p></td>
<td><ul>
<li><p>Mediant2000/ySpans/SIP</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Avaya</p></td>
<td><p>Definity G3</p></td>
<td><ul>
<li><p>MediaPack 11x/FXO/AC/SIP-0</p></li>
<li><p>Mediant1000/ySpans/SIP</p></li>
<li><p>Mediant2000/ySpans/SIP</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Avaya</p></td>
<td><p>Magix/Merlin</p></td>
<td><ul>
<li><p>MediaPack 11x/FXO/AC/SIP-0</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Avaya</p></td>
<td><p>S8300</p></td>
<td><ul>
<li><p>MediaPack 11x/FXO/AC/SIP-0</p></li>
<li><p>Mediant1000/ySpans/SIP</p></li>
<li><p>Mediant2000/ySpans/SIP</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Avaya</p></td>
<td><p>S8700</p></td>
<td><ul>
<li><p>MediaPack 11x/FXO/AC/SIP-0</p></li>
<li><p>Mediant1000/ySpans/SIP</p></li>
<li><p>Mediant2000/ySpans/SIP</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Avaya</p></td>
<td><p>IP Office</p></td>
<td><ul>
<li><p>MediaPack 11x/FXO/AC/SIP-0</p></li>
<li><p>Mediant2000/ySpans/SIP</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Cisco</p></td>
<td><p>CallManager 4.x</p></td>
<td><ul>
<li><p>Mediant1000/IP à IP</p></li>
<li><p>Mediant2000/IP à IP</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>NEC</p></td>
<td><p>Electra Elite</p></td>
<td><ul>
<li><p>MediaPack 11x/FXO/AC/SIP-0</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>NEC</p></td>
<td><p>NEAX2400</p></td>
<td><ul>
<li><p>MediaPack 11x/FXO/AC/SIP-0</p></li>
<li><p>Mediant2000/ySpans/SIP/RS232</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>NeXspan</p></td>
<td><p>S</p></td>
<td><ul>
<li><p>MediaPack 11x/FXO/AC/SIP-0</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Nortel</p></td>
<td><p>Communication Server-1000M, 1000S, 1000E</p></td>
<td><ul>
<li><p>Mediant1000/ySpans/SIP</p></li>
<li><p>Mediant2000/ySpans/SIP</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Nortel</p></td>
<td><p>Meridian 11c, 51c, 61c, 81c</p></td>
<td><ul>
<li><p>Mediant1000/ySpans/SIP</p></li>
<li><p>Mediant2000/ySpans/SIP</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Panasonic</p></td>
<td><p>KX-TES824, KX-TEA308</p></td>
<td><ul>
<li><p>MediaPack 11x/FXO/AC/SIP-0</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Panasonic</p></td>
<td><p>KX-TDA30, KX-TDA100, KX-TDA200, KX-TDA600</p></td>
<td><ul>
<li><p>MediaPack 11x/FXO/AC/SIP-0</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Shortel</p></td>
<td><p>Système de téléphonie IP</p></td>
<td><ul>
<li><p>MediaPack 11x/FXO/AC/SIP-0</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Siemens</p></td>
<td><p>HiCom 150E</p></td>
<td><ul>
<li><p>MediaPack 11x/FXO/AC/SIP-0</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Siemens</p></td>
<td><p>HiPath 3550</p></td>
<td><ul>
<li><p>MediaPack 11x/FXO/AC/SIP-0</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Siemens</p></td>
<td><p>HiPath 4000</p></td>
<td><ul>
<li><p>MediaPack 11x/FXO/AC/SIP-0</p></li>
<li><p>Mediant1000/ySpans/SIP</p></li>
<li><p>Mediant2000/ySpans/SIP</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Tadiran Telecom</p></td>
<td><p>Coral Flexicom, Coral IPX</p></td>
<td><ul>
<li><p>MediaPack 11x/FXO/AC/SIP-0</p></li>
<li><p>Mediant1000/ySpans/SIP</p></li>
<li><p>Mediant2000/ySpans/SIP</p></li>
</ul></td>
</tr>
</tbody>
</table>


## PBX pris en charge lors de l'utilisation d'une passerelle VoIP Dialogic

Chaque modèle de passerelle VoIP Dialogic prend en charge différents PBX. Les tableaux suivants présentent le fabricant et le modèle de PBX, ainsi que la passerelle VoIP Dialogic pouvant être utilisée. Chaque passerelle VoIP utilise des méthodes de signalisation, des densités et des protocoles différents.

## PBX pris en charge lors de l'utilisation d'une passerelle multimédia de la série DMG1000

Le tableau suivant présente les PBX pris en charge avec la passerelle Dialogic Media Gateway (DMG1000) à faible densité. Cependant, lorsqu'une DMG1000 est utilisée, une signalisation supplémentaire (RS232 SMDI, MD110, protocoles MCI, ou signalisation Inband DTMF) est requise.

### PBX pris en charge lors de l'utilisation d'une passerelle VoIP de la série Dialogic DMG1000 à faible densité

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Fabricant du PBX</th>
<th>Modèle/type de PBX</th>
<th>Modèle DMG et signalisation supplémentaire</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Aastra</p></td>
<td><p>Aastra MD110 (anciennement Ericsson MD110)</p></td>
<td><p>DMG1008LSW</p>
<p>Connectivité analogique à l'aide du protocole MD110 RS232</p></td>
</tr>
<tr class="even">
<td><p>Alcatel</p></td>
<td><p>Omni PCX 4400</p></td>
<td><p>DMG1008LSW</p></td>
</tr>
<tr class="odd">
<td><p>Avaya</p></td>
<td><p>Definity G3 S8100, S8300, S8700 et S8710 (Communications Mgr SW V2.0 ou versions ultérieures)</p></td>
<td><p>DMG1008DNIW</p></td>
</tr>
<tr class="even">
<td><p>Intercom</p></td>
<td><p></p></td>
<td><p>DMG1008LSW</p>
<p>Connectivité analogique utilisant le protocole série SMDI</p></td>
</tr>
<tr class="odd">
<td><p>Mitel</p></td>
<td><p>SX-200D, SX-200 Light, SX-2000 Light, SX-2000 S, SX-2000 VS, SX-200 ICP</p></td>
<td><p>DMG1008MTLDNIW</p></td>
</tr>
<tr class="even">
<td><p>NEC</p></td>
<td><p>2000, 2400, 2400 IPX</p></td>
<td><p>DMG1008DNIW</p></td>
</tr>
<tr class="odd">
<td><p>Nortel</p></td>
<td><p>Meridian 1 - Option 11, 21, 21A, 51, 61, 71 et 81</p>
<p>Meridian SL1 - Generic X11, Release 15 ou versions ultérieures</p>
<p>Nortel Communication Server - 1000M, 1000S, 1000E avec V3.0 ou versions ultérieures</p></td>
<td><p>DMG1008DNIW</p></td>
</tr>
<tr class="even">
<td><p>Nortel</p></td>
<td><p>SL 100</p></td>
<td><p>DMG1008LSW</p>
<p>Connectivité analogique utilisant le protocole série SMDI</p></td>
</tr>
<tr class="odd">
<td><p>Siemens</p></td>
<td><p>HiCom 300E CS</p></td>
<td><p>DMG1008DNIW</p></td>
</tr>
<tr class="even">
<td><p>Siemens</p></td>
<td><p>HiCom 300E (européen)</p></td>
<td><p>DMG1008LSW</p>
<p>Connectivité analogique utilisant une signalisation Inband DTMF</p></td>
</tr>
<tr class="odd">
<td><p>Siemens/ROLM</p></td>
<td><p>8000 (version de logiciel 80003 ou versions ultérieures)<br />
9000 (toutes les versions)</p>
<p>9751 (toutes les versions de logiciel 9005)</p>
<p>9751 (version de logiciel 9006.4 ou versions ultérieures)</p></td>
<td><p>DMG1008RLMDNIW</p></td>
</tr>
<tr class="even">
<td><p>Siemens</p></td>
<td><p>HiPath 4000</p></td>
<td><p>DMG1008LSW</p></td>
</tr>
<tr class="odd">
<td><p>Toshiba</p></td>
<td><p>CTX (SW version AR1ME021.00)</p></td>
<td><p>DMG1008LSW</p></td>
</tr>
<tr class="even">
<td><p>Autres</p></td>
<td><p>Divers</p></td>
<td><p>DMG1008LSW</p>
<p>Connectivité analogique utilisant Inband DTMF ou SMDI</p></td>
</tr>
</tbody>
</table>


## PBX pris en charge lors de l'utilisation d'une passerelle multimédia de la série DMG 2000

Le tableau suivant présente les PBX pris en charge avec la passerelle Dialogic Media Gateway (DMG2000) T1/E1. La passerelle DMG2000, proposée en densités à plage unique (DMG2030DTIQ), double plage (DMG2060DTIQ) ou quatre plages (DMG2120DTIQ), prend en charge les protocoles suivants :

  - T1 CAS

  - T1 Q.SIG

  - E1 Q.SIG

  - T1 NI-2

  - T1 5ESS

  - T1 DMS100

Si la signalisation CAS (Channel Associated Signaling) est utilisée, une signalisation supplémentaire (RS232 SMDI, MD110, protocoles MCI, ou signalisation Inband DTMF) est requise. Si la signalisation Q.SIG est utilisée, le PBX doit prendre en charge les services supplémentaires qui sont associés aux informations relatives aux appelants et appelés ainsi que les fonctionnalités de transfert d'appels requises par la messagerie unifiée .

### PBX pris en charge avec une passerelle multimédia DMG2000

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Fabricant du PBX</th>
<th>Modèle/type de PBX</th>
<th>Version de logiciel requise</th>
<th>Protocole et signalisation supplémentaire</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Alcatel</p></td>
<td><p>Omni PCX 4400</p></td>
<td><p>Version 3.2.712.5</p></td>
<td><p>T1 Q.SIG</p>
<p>E1 Q.SIG</p></td>
</tr>
<tr class="even">
<td><p>Avaya</p></td>
<td><p>Definity G3</p></td>
<td><p>Version 3 ou versions ultérieures</p></td>
<td><p>T1 CAS</p></td>
</tr>
<tr class="odd">
<td><p>Avaya</p></td>
<td><p>S8500</p></td>
<td><p>Manager SW V2.0 ou versions ultérieures</p></td>
<td><p>T1 CAS</p>
<p>T1 Q.SIG</p>
<p>E1 Q.SIG</p></td>
</tr>
<tr class="even">
<td><p>Ericsson</p></td>
<td><p>MD110</p></td>
<td><p>Release MX1 TSW R2A (BC13)</p></td>
<td><p>E1 Q.SIG</p></td>
</tr>
<tr class="odd">
<td><p>Intercom</p></td>
<td><p></p></td>
<td><p></p></td>
<td><p>CAS (avec le protocole série SMDI)</p></td>
</tr>
<tr class="even">
<td><p>NEC</p></td>
<td><p>2400 IMX</p></td>
<td><p>Release 5200 Dec. 92 1b ou versions ultérieures</p></td>
<td><p>CAS (avec le protocole série MCI)</p></td>
</tr>
<tr class="odd">
<td><p>NEC</p></td>
<td><p>2400 IPX</p></td>
<td><p>R17 Release 03.46.001</p></td>
<td><p>T1 Q.SIG</p></td>
</tr>
<tr class="even">
<td><p>Nortel</p></td>
<td><p>Meridian 1- Option 11</p></td>
<td><p>Release 15 ou versions ultérieures, les options 19 et 46 sont requises</p></td>
<td><p>T1 Q.SIG</p>
<p>E1 Q.SIG</p></td>
</tr>
<tr class="odd">
<td><p>Nortel</p></td>
<td><p>Communication Server 1000</p></td>
<td><p>Version 2121, Release 4</p></td>
<td><p>T1 Q.SIG</p>
<p>E1 Q.SIG</p></td>
</tr>
<tr class="even">
<td><p>Siemens</p></td>
<td><p>HiCom 300E CS</p></td>
<td><p>Release 9006.4 ou versions ultérieures (Remarque : téléchargement du logiciel uniquement en Amérique du Nord)</p></td>
<td><p>T1 CAS</p></td>
</tr>
<tr class="odd">
<td><p>Siemens</p></td>
<td><p>HiPath 4000</p></td>
<td><p>V2 SMR 9 SMPO</p></td>
<td><p>T1 Q.SIG</p>
<p>E1 Q.SIG</p></td>
</tr>
<tr class="even">
<td><p>Mitel</p></td>
<td><p>SX-2000 S, SX-2000 VS</p></td>
<td><p>LW 34</p></td>
<td><p>T1 Q.SIG</p>
<p>E1 Q.SIG</p></td>
</tr>
<tr class="odd">
<td><p>Mitel</p></td>
<td><p>3300</p></td>
<td><p>Version 5.1.4.8</p></td>
<td><p>T1 Q.SIG</p>
<p>E1 Q.SIG</p></td>
</tr>
</tbody>
</table>


## PBX pris en charge lors de l'utilisation d'une passerelle multimédia de la série DMG4008BRI

La passerelle multimédia de la série DMG4000 comporte plusieurs options d'interface MRT. La passerelle DMG4008BRI prend en charge les densités 4 ports/8 canaux et les protocoles suivants :

  - ISDN BRI Q.SIG

  - ETSI-DSS1 (Euro ISDN)

  - NET 3 (Belgique)

  - VN3 (France)

  - 1TR6 (Allemagne)

  - INS-64 (Japon)

  - 5ESS Custom (Amérique du nord - AT\&T)

  - National ISDN (NI1 - Amérique du nord)

Le tableau suivant présente les PBX pris en charge avec la série de passerelle multimédia Dialogic 4000 (DMG4008).

### PBX pris en charge avec une passerelle multimédia DMG4008BRI

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Fabricant du PBX</th>
<th>Modèle/type de PBX</th>
<th>Version de logiciel requise</th>
<th>Protocole et signalisation supplémentaire</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Siemens</p></td>
<td><p>HiCom 300</p></td>
<td><p>SA300-V3.05</p></td>
<td><p>BRI-Q.SIG (ECMAV2)</p></td>
</tr>
<tr class="even">
<td><p>Siemens</p></td>
<td><p>HiPath 4000</p></td>
<td><p>S.0 B4400</p></td>
<td><p>BRI-Q.SIG (ECMAV2)</p></td>
</tr>
</tbody>
</table>


## PBX IP pris en charge

La messagerie unifiée prend également en charge les PBX IP. Le tableau suivant présente les PBX IP pris en charge avec une connexion SIP directe à la messagerie unifiée.

### PBX IP pris en charge lors de l'utilisation d'une connexion SIP directe

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Fabricant du PBX</th>
<th>Modèle/type de PBX</th>
<th>Version de logiciel requise</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Aastra</p></td>
<td><p>MX-ONE</p></td>
<td><p>4.0</p></td>
</tr>
<tr class="even">
<td><p>Avaya</p></td>
<td><p>Aura</p></td>
<td><p>5.2.1 avec le Service Pack 5 (SP5)</p></td>
</tr>
<tr class="odd">
<td><p>Avaya</p></td>
<td><p>Communication Server 2100</p></td>
<td><p>CS2100 SE13</p></td>
</tr>
<tr class="even">
<td><p>Cisco</p></td>
<td><p>Call Manager, Unified Communications Manager</p></td>
<td><p>5.1, 6.x, 7.0 and8.0</p></td>
</tr>
</tbody>
</table>


## PBX IP pris en charge lors de l'utilisation de passerelles multimédia SIP

La messagerie unifiée prend également en charge les PBX IP utilisant des passerelles multimédia SIP. Le tableau suivant présente les PBX IP pris en charge avec les fonctionnalités IP à IP des passerelles multimédias SIP dans le cadre d'une connexion à la messagerie unifiée.

### PBX IP pris en charge lors de l'utilisation d'une passerelle multimédia SIP

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Fabricant du PBX</th>
<th>Modèle/type de PBX</th>
<th>Modèle de passerelle SIP</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Cisco</p></td>
<td><p>Call Manager 4.x</p></td>
<td><p>AudioCodes Mediant 1000/2000 (fonction IP à IP activée)</p></td>
</tr>
</tbody>
</table>


## Messagerie unifiée Exchange, Office Communications Server 2007 R2 et Microsoft Lync Server

Pour les déploiements hybrides et locaux, la messagerie unifiée Exchange peut être déployée avec Microsoft Office Communications Server 2007 R2, Microsoft Lync Server 2010 ou Lync Server 2013 pour offrir aux utilisateurs de votre organisation les services suivants : messagerie vocale, messagerie instantanée, présence utilisateur améliorée et téléconférence audio ainsi qu'une expérience de messagerie et de messagerie électronique intégrée. Pour plus d'informations, consultez les rubriques suivantes :

  - [Présentation du déploiement de la messagerie unifiée Exchange 2013 et de Lync Server](deploying-exchange-2013-um-and-lync-server-overview-exchange-2013-help.md)

  - [Microsoft Lync Server 2013](https://go.microsoft.com/fwlink/p/?linkid=202010)

Pour plus d'informations sur le programme d'interopérabilité d'ouverture des communications unifiées de Microsoft destiné à une infrastructure de téléphonie en entreprise, notamment la recherche de passerelles RTPC (réseau téléphonique public commuté) SIP et de PBX IP qualifiés, et sur la procédure d'inscription et de participation au programme pour les fournisseurs d'infrastructures de téléphonie, consultez la page [Programme d'interopérabilité d'ouverture des communications unifiées de Microsoft](https://go.microsoft.com/fwlink/p/?linkid=132071).

