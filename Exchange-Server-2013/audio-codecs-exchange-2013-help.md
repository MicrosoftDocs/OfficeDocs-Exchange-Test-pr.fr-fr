---
title: 'Codecs audio: Exchange 2013 Help'
TOCTitle: Codecs audio
ms:assetid: 6c39d65c-c2d3-4128-aae9-8596602819c3
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Aa998670(v=EXCHG.150)
ms:contentKeyID: 54652760
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Codecs audio

 

_**Sapplique à :** Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2016-12-09_

Dans la messagerie unifiée, un codec audio est utilisé pour stocker des messages vocaux. Un autre codec est utilisé entre une passerelle VoIP ou un PBX (Private Branch eXchange) IP et le serveur de boîtes aux lettres exécutant le service de messagerie unifiée Microsoft Exchange ou le serveur d'accès au client exécutant le service routeur des appels de messagerie unifiée Microsoft Exchange. La messagerie unifiée est compatible avec les quatre codecs audio suivants pour créer et stocker des messages vocaux :

  - MP3 (par défaut)

  - Windows Media Audio (WMA)

  - Group System Mobile (GSM) 06.10

  - G.711 PCM (Pulse Code Modulation) Linear

<table>
<thead>
<tr class="header">
<th><img src="images/Bb125224.warning(EXCHG.150).gif" title="Avertissement" alt="Avertissement" />Avertissement :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Les codecs G.711 (PCMA et PCMU) et G.723.1 sont des codecs VoIP utilisés entre une passerelle VoIP et les serveurs de boîtes aux lettres et d'accès au client.</td>
</tr>
</tbody>
</table>


La sélection du codec audio approprié en fonction des besoins et exigences de votre organisation fait partie de la planification de votre système de messagerie unifiée. Cette rubrique décrit les codecs audio que la messagerie unifiée peut utiliser et vous aide à planifier votre déploiement de messagerie unifiée.

## Codecs

Le terme *codec* est une combinaison des mots « codage » et « décodage » utilisée avec des données audio numériques. Un codec est un logiciel qui transforme les données numériques dans un format de fichier audio ou un format de flux audio. Les codecs permettent de convertir un signal vocal analogique en un signal vocal numérique. Les différences entre les codecs relèvent de la qualité du son, de la bande passante requise pour les utiliser et des besoins du système pour l'encodage.

Deux types de codecs sont utilisés dans la messagerie unifiée :

  - Le codec utilisé entre une passerelle VoIP, un PBX IP ou un PBX compatible SIP et les serveurs de boîtes aux lettres et d'accès au client ou le codec utilisé entre un PBX et une passerelle VoIP.

  - Le codec utilisé pour encoder et stocker des messages vocaux pour les utilisateurs.

Quand vous utilisez un téléphone ordinaire sur le réseau téléphonique commuté (RTC), votre voix est transférée dans un format analogique sur la ligne de téléphone. Avec la voix sur IP (VoIP), votre voix doit être convertie en signaux numériques. Ce processus de conversion est appelé encodage. L'encodage est exécuté par un codec. Une fois que la voix numérisée a atteint sa destination, elle doit être décodée au format analogique d'origine afin que la personne recevant l'appel puisse entendre et comprendre l'appelant.

## Codec VoIP

Dans la messagerie unifiée, trois types de codecs peuvent être utilisés entre les passerelles VoIP ou les PBX IP et les serveurs de boîtes aux lettres et d'accès au client.

  - G.711 µ-law

  - G.711 A-law

  - G.723.1

G.711 est une norme développée pour fonctionner avec les codecs audio. Deux algorithmes principaux sont définis dans la norme pour G.711 : l'algorithme µ-law, utilisé en Amérique du Nord et au Japon, et l'algorithme A-law, utilisé en Europe et dans les autres pays. Le codec audio G.723.1 est principalement utilisé dans les applications VoIP et requiert l'acquisition d'une licence. G.723.1 est un type de codec à forte compression de haute qualité.

Un serveur de boîtes aux lettres ou d'accès au client et une passerelle VoIP ou un PBX IP pris en charge peuvent inclure les codecs G.711 et G.723.1. Par défaut, le premier codec à être utilisé est G.723.1. Pour utiliser un autre codec entre les serveurs de boîtes aux lettres et d'accès au client et la passerelle VoIP ou le PBX IP, nous vous conseillons de modifier la configuration sur la passerelle VoIP ou le PBX IP. Le tableau suivant indique certains codecs VoIP courants.

### Codecs VoIP

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Codec VoIP</th>
<th>Bande passante (Kbits/s)</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>G.711</p></td>
<td><p>64</p></td>
<td><p>Ce codec implique un traitement faible. Il requiert un minimum de 128 kilo-octets par seconde (Kbits/s) pour les communications bidirectionnelles.</p></td>
</tr>
<tr class="even">
<td><p>G.723.1</p></td>
<td><p>5.3/6.3</p></td>
<td><p>Ce codec offre une compression et une qualité audio élevées. Il requiert un traitement plus important que le codec G.711. Le codec G.723.1 utilise une bande passante réduite mais offre une qualité audio plus faible.</p></td>
</tr>
</tbody>
</table>


## Codec de stockage des messages vocaux de messagerie unifiée

Les plans de numérotation de messagerie unifiée jouent un rôle crucial dans le fonctionnement de la messagerie unifiée. Par défaut, lorsque vous créez un plan de numérotation de messagerie unifiée, celui-ci utilise le codec audio MP3 pour créer et stocker des messages vocaux. Toutefois, après la création du plan de numérotation de messagerie unifiée, vous pouvez le configurer pour utiliser les codecs audio WMA, GSM 06.10 ou G.711 PCM Linear.

Chaque codec audio présente des avantages et des inconvénients. Le codec audio MP3 a été sélectionné comme codec audio par défaut pour la qualité de son et ses propriétés de compression. Les codecs audio GSM 06.10 et G.711 PCM Linear ont été inclus comme options disponibles pour leur capacité à prendre en charge d'autres types de systèmes de messagerie.

Quand vous planifiez l'utilisation de la messagerie unifiée, vous devez équilibrer la taille et la qualité relative du fichier audio créé pour les messages vocaux. En général, plus la vitesse de transmission d'un fichier audio est élevée, plus la qualité est optimale. Vous devez également prendre en compte la compression du fichier audio. Le tableau suivant décrit la vitesse de transmission d'échantillonnage (bit/s) et les propriétés de compression de chaque codec audio utilisé dans la messagerie unifiée.

### Codecs de stockage des messages vocaux de messagerie unifiée par défaut

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Codec de stockage des messages vocaux</th>
<th>Bits</th>
<th>Fichier compressé ?</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>MP3</p></td>
<td><p>16 bits</p></td>
<td><p>Oui</p></td>
</tr>
<tr class="even">
<td><p>WMA</p></td>
<td><p>16 bits</p></td>
<td><p>Oui</p></td>
</tr>
<tr class="odd">
<td><p>G.711 PCM</p></td>
<td><p>16 bits</p></td>
<td><p>Non</p></td>
</tr>
<tr class="even">
<td><p>GSM 06.10</p></td>
<td><p>8 bits</p></td>
<td><p>Oui</p></td>
</tr>
</tbody>
</table>


Dans la messagerie unifiée, le type de fichier créé pour un message vocal dépend du codec audio qui est utilisé pour créer le fichier audio du message vocal. Le codec audio MP3 crée des fichiers audio .mp3, le codec audio WMA crée des fichiers audio .wma et les codecs audio GSM 06.10 et G.711 PCM Linear produisent des fichiers audio .wav. Tous ces fichiers audio sont envoyés avec un message électronique au destinataire du message vocal.

Souvent, le codage et le décodage des données numériques impliquent la compression ou la décompression des données. La compression audio est une forme de compression des données qui réduit la taille des fichiers de données audio. L'algorithme de compression audio utilisé par le codec audio compresse les fichiers audio .wma ou .wav. Dans la messagerie unifiée, le type d'algorithme de compression audio utilisé est fonction du type de codec audio sélectionné dans les propriétés du plan de numérotation de la messagerie unifiée. Après sa création et sa compression, le fichier audio est attaché en pièce jointe au message vocal.

Parfois, au cours de la compression et de la décompression, certaines informations des données numériques sont perdues. Plus la compression d'un fichier audio est élevée, plus la conversion entraîne une perte d'informations importante. Toutefois, l'espace disque utilisé est moindre en raison de la taille réduite du fichier audio. Inversement, plus la compression est faible, moins la perte d'informations est importante. Toutefois, l'espace disque utilisé est plus conséquent en raison de la taille importante du fichier audio.

La bande passante RTAudio ou l'audio haute fidélité pour l'enregistrement des messages vocaux sont aussi disponibles sous forme de codec audio. Toutefois, l'audio haute fidélité via RTAudio n'est disponible qu'après intégration de la messagerie unifiée dans [Microsoft Lync Server](https://go.microsoft.com/fwlink/p/?linkid=202010). Pour activer RTAudio en tant que codec filaire (bande étroite ou bande large), le plan de numérotation de messagerie unifiée doit être configuré en tant que plan de numérotation de type URI SIP (Session Initiation Protocol), et vous devez définir le codec de réponse aux appels sur le plan de numérotation sur MP3 ou WMA pour activer la transmission audiofréquence large bande (16 kHz).

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159813.important(EXCHG.150).gif" title="Important" alt="Important" />Important :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>RTAudio n'est pas disponible dans les environnements dans lesquels Lync Server n'est pas déployé. Ceci est dû au fait que, dans les environnements qui n’ont pas intégré Lync Server, le plan de numérotation est défini sur Numéro de poste ou E.164 et non sur URI SIP.</td>
</tr>
</tbody>
</table>


Il existe deux flux de données multimédia pour chaque appel entrant : entrant vers un serveur d'accès au client et sortant à partir d'un serveur de boîtes aux lettres. Quand le type de plan de numérotation est défini sur URI SIP et que le codec de réponse aux appels du plan de numérotation est défini sur MP3 ou WMA, un serveur d'accès au client tente de sélectionner le codec VoIP RTAudio pour le flux de données multimédia entrant. Si la négociation réussit, le codec RTAudio pour le flux entrant est utilisé pour les appels de réponse aux appels ou les appels en provenance d'un client ou d'un serveur Lync.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Les appels émis à l'aide de la fonctionnalité Émettre au téléphone n'utilisent pas le codec RTAudio. Le flux entrant pour les appels émis à l'aide de la fonctionnalité Émettre au téléphone utilisent le codec G.711 ou G.723.1.</td>
</tr>
</tbody>
</table>


Quand le codec RTAudio est utilisé, le message vocal est enregistré dans un format haute fidélité et stocké en tant que fichier audio avec une extension .mp3 ou .wma., selon la configuration du plan de numérotation. Lorsque l'utilisateur écoute le message vocal dans Outlook ou Outlook Web App, il entend le message vocal en qualité audio haute fidélité. Si la négociation échoue, le codec G.711 ou G.723.1 est utilisé. Les codecs G.711 et G.723.1 sont des codecs à faible bande passante. Lorsque le message vocal est utilisé comme codec VoIP, il est enregistré et stocké en tant que fichier de transmission audiofréquence à bande étroite avec une extension .mp3 ou .wma.

Le flux de données multimédia sortant est toujours négocié à l'aide du codec G.711 ou G.723.1. Cela signifie que les appelants entendent toujours un son à faible bande passante au téléphone. Cela s'applique également aux situations dans lesquelles l'appel est émis à l'aide de Microsoft Lync Server 2010 ou une version ultérieure.

Le format audio et le codec que les serveurs de boîtes aux lettres utilisent pour stocker la partie audio des messages vocaux dépendent non seulement du codec audio qui est configuré sur le plan de numérotation, mais également de la vitesse de transmission de l'audio que la messagerie unifiée négocie avec un pair SIP. Si votre environnement comprend Lync Server ou des points de terminaison SIP, un serveur de boîtes aux lettres négocie également le codec audio à utiliser avec un pair SIP. Par exemple, si le RTAudio à large bande est négocié comme le codec filaire, un serveur de boîtes aux lettres utilise alors le format 32 Kbps MP3 ou WMA 9.2 pour créer des messages vocaux, selon le paramètre du plan de numérotation en vigueur. Le tableau suivant illustre la relation entre le codec audio de stockage des messages vocaux et le protocole VoIP ou le codec audio qui est utilisé.

### Relation entre le codec audio de stockage et le protocole VoIP ou le codec audio

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Codec audio configuré sur un plan de numérotation de messagerie unifiée</th>
<th>VoIP ou codec filaire (faible bande passante) - G.723, G.711 ou RTAudio (8 KHz)</th>
<th>VoIP ou codec filaire (large bande) - RTAudio (16 KHz)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>G.711</p></td>
<td><p>G.711</p></td>
<td><p>Non applicable. Un serveur de boîtes aux lettres ou d'accès au client ne négocie pas la transmission audiofréquence large bande si le plan de numérotation est paramétré sur G.711.</p></td>
</tr>
<tr class="even">
<td><p>WMA</p></td>
<td><p>WMA 9-voice</p></td>
<td><p>WMA 9.2</p></td>
</tr>
<tr class="odd">
<td><p>GSM</p></td>
<td><p>GSM 6.10</p></td>
<td><p>Non applicable. Une boîte aux lettres ou un accès au client ne négocie pas la transmission audiofréquence large bande si le plan de numérotation est paramétré sur GSM.</p></td>
</tr>
<tr class="even">
<td><p>MP3</p></td>
<td><p>MP3 (16 Kbps)</p></td>
<td><p>MP3 (32 Kbps)</p></td>
</tr>
</tbody>
</table>


Codecs

## Taille de message de messagerie unifiée

Vous pouvez configurer la messagerie unifiée pour utiliser l'un des quatre codecs audio suivants pour la création de messages vocaux : MP3, WMA, GSM 06.10 et G.711 PCM Linear. Par défaut, le format MP3 est sélectionné.

Le codec audio WMA est toujours stocké au format Windows Media et la pièce jointe est un fichier avec une extension de nom de fichier .wma. Les fichiers audio codés à l'aide des codecs audio GSM ou G.711 PCM Linear sont toujours stockés au format RIFF/WAV et la pièce jointe est un fichier avec une extension de nom de fichier .wav.

La taille des messages vocaux de messagerie unifiée dépend de la taille de la pièce jointe contenant les données vocales. Par ailleurs, la taille de la pièce jointe dépend des facteurs suivants :

  - durée de l'enregistrement du message vocal ;

  - codec audio utilisé ;

  - format de stockage du fichier audio.

La figure suivante montre en quoi la taille du fichier audio dépend de la durée de l'enregistrement du message vocal pour les trois codecs audio que vous pouvez utiliser dans la messagerie unifiée.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Dans cette figure, la durée moyenne d'un message vocal de réponse aux appels est d'environ 30 secondes.</td>
</tr>
</tbody>
</table>


**Taille de fichier audio**

![UM\_Message\_Sizing](images/Aa998670.76ca4891-450f-4ffd-9493-aac8d0d23a5d(EXCHG.150).gif "UM_Message_Sizing")

## MP3

Le format MP3 est le format de fichier audio des messages vocaux sélectionné par défaut. Il s'agit d'un format de fichier audio répandu qui permet de réduire considérablement la taille du fichier audio. Ce format est principalement utilisé par les lecteurs MP3 ou les périphériques audio personnels. Le codec audio MP3 est un type de codec multi-plates-formes utilisé pour assurer la compatibilité avec de nombreux périphériques et téléphones mobiles, ainsi qu'avec différents systèmes d'exploitation d'ordinateurs.

## WMA

Des trois codecs audio, WMA est le plus compressé. La compression est d'environ 11 000 octets pour 10 secondes de données audio. Toutefois, le format de fichier .wma a une section d'en-tête beaucoup plus importante que le format de fichier .wav. La section d'en-tête du fichier .wma est d'environ 7 kilo-octets (Ko) alors que la section d'en-tête du fichier .wav est inférieure à 100 octets. Bien que les enregistrements audio WMA soient enregistrés pour une durée supérieure à 15 secondes, leur taille est inférieure à celle des enregistrements audio GSM. Par conséquent, utilisez le codec audio WMA pour obtenir des fichiers audio de qualité optimale et de taille réduite.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Si vous utilisez les notifications Push à partir de votre déploiement local pour OWA pour les périphériques, vous ne pouvez pas utiliser le format WMA. OWA pour les périphériques ne prend en charge que le format de fichier MP3.</td>
</tr>
</tbody>
</table>


## G.711 PCM Linear

Le codec audio G.711 PCM Linear crée des fichiers audio .wav non compressés. Par conséquent, les fichiers audio G.711 PCM Linear .wav occupent davantage d'espace, quelle que soit leur durée, que les codecs audio GSM et WMA. Les fichiers audio G.711 PCM Linear .wav occupent un peu plus de 160 000 octets pour 10 secondes de données audio. Les fichiers audio G.711 PCM Linear .wav ont la meilleure qualité audio des trois codecs audio utilisés par la messagerie unifiée. Toutefois, la qualité de fichiers audio comparables créés en utilisant les codecs audio WMA et GSM est acceptable pour la plupart des utilisateurs qui écoutent les messages vocaux.

## GSM

Le codec audio GSM crée des fichiers audio .wav compressés. Les fichiers audio GSM .wav occupent un peu plus de 16 000 octets pour 10 secondes de données audio. Toutefois, GSM crée un fichier audio dont la taille est supérieure à celle du fichier audio créé par le codec audio WMA. Par conséquent, lors de l'équilibrage entre la taille et la qualité du message vocal, cette solution n'est pas la plus adaptée.

Codecs

