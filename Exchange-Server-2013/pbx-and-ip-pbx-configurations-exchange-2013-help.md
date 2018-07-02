---
title: 'Configuration des PBX et PBX IP: Exchange 2013 Help'
TOCTitle: Configuration des PBX et PBX IP
ms:assetid: fb086680-6e3e-477a-a5d8-e24ca30196ee
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb430797(v=EXCHG.150)
ms:contentKeyID: 54652784
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configuration des PBX et PBX IP

 

_**Sapplique à :**Exchange Server 2010 Service Pack 2 (SP2), Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :**2016-12-09_

De plus en plus, les organisations achètent, installent et entretiennent les composants matériels, par exemple PBX (Private Branch eXchanges) ou PBX IP, nécessaires à la prise en charge de leur propre système téléphonique. De nombreuses organisations achètent leur propre matériel téléphonique et forment leur personnel pour réduire les coûts associés à la maintenance des systèmes téléphoniques et mieux contrôler les fonctionnalités de téléphonie proposées.

Pour qu’une organisation détienne et entretienne son réseau téléphonique, elle doit acheter les composants matériels téléphoniques requis. Elle doit également prendre en considération la maintenance quotidienne de l’équipement de téléphonie et la formation requise pour que son personnel puisse utiliser le système téléphonique. Cette rubrique traite des différents types de systèmes de téléphonie présents dans les organisations ou les entreprises ainsi que les composants matériels téléphoniques requis. Elle présente également différents types de configuration téléphonique.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159813.important(EXCHG.150).gif" title="Important" alt="Important" />Important :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Nous conseillons à tous les clients qui projettent de déployer une messagerie unifiée Microsoft Exchange 2013 de solliciter l’aide d’un spécialiste en messagerie unifiée. Celui-ci vous aidera à opérer une mise à niveau harmonieuse à partir d’un système de messagerie vocale hérité. Le déploiement d’un nouveau système de messagerie unifiée ou la mise à niveau d’un système de messagerie vocale hérité requiert une connaissance approfondie des PBX, des IP PBX et de la messagerie unifiée. Pour plus d’informations sur les personnes à contacter, consultez le site web <a href="https://go.microsoft.com/fwlink/p/?linkid=261951">Microsoft PinPoint</a>.</td>
</tr>
</tbody>
</table>


**Contenu de cette rubrique**

Vue d'ensemble des systèmes téléphoniques

Configurations des PBX hérités ou traditionnels

Configuration PBX IP

Identification de l'appelant et de l'appelé

## Vue d’ensemble des systèmes téléphoniques

Dans les réseaux de commutation de circuits, tels que le réseau téléphonique commuté (RTC), plusieurs appels sont transmis via le même moyen de transmission. Dans le RTC, le cuivre est souvent utilisé comme moyen de transmission. Toutefois, un câble en fibre optique peut également être utilisé.

Un réseau de commutation par circuits est un réseau utilisant une connexion dédiée. Une connexion dédiée est un circuit ou un canal installé entre deux nœuds afin de leur permettre de communiquer. Après qu’un appel a été établi entre deux nœuds, la connexion ne peut être utilisée que par ces nœuds. Lorsque l’un des nœuds met fin à l’appel, la connexion est annulée.

Plusieurs types ou catégories de systèmes téléphoniques recensés dans les entreprises et les organisations comprennent un réseau de téléphonie basé sur un circuit, sur le protocole IP ou sur les deux. Chaque type de système de téléphonie présente des avantages et des inconvénients qui lui sont propres et dont vous devez tenir compte lorsque vous projetez de mettre en place un système de téléphonie.

  - **Centrex :** Centrex est un type de service téléphonique que les sociétés de téléphonie louent aux entreprises et aux organisations. Un système de téléphonie Centrex traditionnel n’oblige pas les entreprises ou les organisations à acheter le matériel téléphonique utilisé sur le site pour prendre en charge le système de téléphonie. En général, les systèmes Centrex sont utilisés par de petits bureaux qui paient la location des services Centrex à une société de téléphonie sur la base du nombre de lignes ou en mensualités. Les systèmes de téléphonie Centrex sont parfois utilisés par des organisations plus grandes, mais ils sont plus fréquemment employés par des organisations privées, publiques ou gouvernementales. Centrex utilise souvent des lignes de téléphone analogiques pour la connexion à une entreprise ou à une organisation. Cependant, il peut aussi utiliser des circuits T1 avec un démultiplexeur sur site pour prendre en charge les lignes téléphoniques analogiques et numériques ou RNIS.
    
    Dans un système de téléphonie basé sur Centrex, le bureau de la société de téléphonie fait office de central téléphonique. Il est spécialement conçu pour prendre en charge les besoins d’une organisation particulière. Le central téléphonique achemine les appels internes vers le numéro de téléphone interne ou externe approprié. Centrex utilise le central téléphonique de la société de téléphonie pour acheminer les appels internes vers un numéro de poste. Par exemple, avec Centrex, le central téléphonique de la société sait reconnaître les numéros de postes internes. Ainsi, un employé appartenant au réseau de téléphonie de l’entreprise peut contacter un autre employé, situé sur le même réseau ou sur le même plan de numérotation, en composant un numéro de poste à 4 chiffres. Lorsqu’un appel est effectué vers un numéro de poste interne, il est transféré vers le central téléphonique de la société de téléphonie avant d’être acheminé vers le numéro de poste à l’origine de l’appel.

*IP Centrex* est une variante du système de téléphonie Centrex traditionnel. Dans un système téléphonique IP Centrex, l’appel passe par une passerelle VoIP (Voice over IP) située dans le central téléphonique d’une société de téléphonie ou sur site chez un fournisseur de service. Avec ce type de système, la passerelle VoIP convertit l’appel en paquets de données IP qui peuvent être envoyés par Internet ou par un réseau VoIP. Cependant, si l’appel passe par Internet, il existe en général une autre passerelle VoIP pour recevoir l’appel et le convertir en appel de commutation de circuits.

Les organisations qui possèdent actuellement un système de téléphonie Centrex traditionnel doivent installer, déployer et entretenir une ou plusieurs passerelles IP pour que la messagerie unifiée fonctionne correctement. La messagerie unifiée peut nécessiter l’installation, le déploiement et la maintenance de passerelles VoIP pour fonctionner avec IP Centrex. Plusieurs variables déterminent si vous avez besoin d’une passerelle VoIP. Ces variables incluent le type de téléphone utilisé dans votre organisation (analogique, numérique ou IP) et les protocoles pris en charge par le système IP Centrex.

  - **Téléphone à clé :** Dans un système de téléphone à clé, le central de la société de téléphonie est connecté à l’organisation par le biais de lignes téléphoniques analogiques ou numériques standard. Un seul numéro de poste est connecté à plusieurs téléphones de façon à ce qu’ils sonnent tous en même temps lorsque l’organisation reçoit un appel sur ce numéro.

Avec les systèmes de téléphone à clé, les utilisateurs individuels partagent des lignes par le biais de leurs téléphones. C’est pourquoi les appelants ne reçoivent pas un signal occupé lorsqu’ils essayent d’appeler une organisation. Les systèmes de téléphone à clé sont, en général, utilisés par les petits bureaux où le volume des appels internes est élevé mais celui des appels externes est bas.

Ces systèmes sont devenus de plus en plus sophistiqués et peuvent fonctionner avec la messagerie unifiée si une passerelle VoIP est ajoutée. Cependant, certains systèmes moins perfectionnés peuvent ne pas fonctionner même si une passerelle VoIP prise en charge est utilisée.

  - **PBX :** Un PBX hérité est un périphérique téléphonique qui agit comme un commutateur pour les appels dans un réseau de commutation de circuits ou téléphonique. Un PBX hérité ne possède pas de carte réseau et ne peut pas transmettre les paquets IP. Certaines entreprises ou organisations ne pouvant pas transmettre les paquets IP, elles ont remplacé les PBX hérités par des PBX IP. Pour obtenir la liste des PBX pris en charge par la messagerie unifiée, voir [Gestionnaire de téléphonie pour Exchange 2013](telephony-advisor-for-exchange-2013-exchange-2013-help.md).
    
    Les PBX sont utilisés par la plupart des entreprises de taille moyenne à grande. Un PBX permet à ses utilisateurs ou abonnés de partager un certain nombre de lignes extérieures pour établir des appels téléphoniques considérés comme externes au PBX. Un PBX est une solution beaucoup moins onéreuse que le fait de donner à chaque utilisateur d’une entreprise une ligne téléphonique externe dédiée. Des téléphones, en plus des télécopieurs, des modems et de nombreux autres périphériques de communication peuvent être connectés à un PBX.
    
    L’équipement PBX est généralement installé dans les locaux d’une organisation et connecte les appels entre les téléphones situés sur le site de l’entreprise et la compagnie de téléphone. Un nombre limité de lignes extérieures, également appelées lignes spécialisées, sont généralement disponibles pour établir et recevoir des appels externes à l’entreprise à partir d’une source externe telle que le RTC.
    
    Pour permettre à un PBX hérité de fonctionner avec la messagerie unifiée, vous devez déployer une passerelle VoIP prise en charge. Pour obtenir la liste des passerelles VoIP prises en charge, voir [Gestionnaire de téléphonie pour Exchange 2013](telephony-advisor-for-exchange-2013-exchange-2013-help.md).

  - **PBX IP :** Un PBX IP est équipé d’un adaptateur de réseau qui prend en charge le protocole IP. Il s’agit d’un équipement de commutation téléphonique que l’on trouve en général dans une organisation ou dans une entreprise plutôt que dans les bureaux d’une société de téléphonie. Il existe deux types de PBX IP : traditionnel et hybride. Ces deux types de PBX IP prennent en charge le protocole IP pour envoyer des conversations vocales en paquets vers les téléphones VoIP. Cependant, les PBX IP hybrides se connectent aussi bien aux téléphones analogiques traditionnels qu’aux téléphones numériques.
    
    Les PBX IP sont souvent plus faciles à administrer que les PBX hérités, car les administrateurs peuvent plus facilement configurer leurs services PBX IP en utilisant un navigateur Internet ou un autre utilitaire IP. En outre, aucun fil, câble ou tableau de connexions supplémentaire ne doit être installé. Avec un PBX IP, vous pouvez déplacer un téléphone IP simplement en le débranchant et en le rebranchant ailleurs. Cela vous permet d’éviter les appels de service coûteux nécessaires au déplacement d’un téléphone de PBX hérité. En outre, les organisations qui possèdent un PBX IP ne s’exposent pas aux coûts d’infrastructure supplémentaires requis pour la maintenance et la gestion de réseaux de commutation de circuits et de paquets distincts. Pour obtenir la liste des PBX IP pris en charge par la messagerie unifiée, voir [Gestionnaire de téléphonie pour Exchange 2013](telephony-advisor-for-exchange-2013-exchange-2013-help.md).
    
    Retour au début

## Configuration des PBX hérités ou traditionnels

Sur les réseaux téléphoniques équipés de PBX hérités ou traditionnels, un PBX agit de la façon suivante :

  - Il crée des connexions ou des circuits entre les combinés de deux utilisateurs.

  - Il assure la maintenance de cette connexion aussi longtemps que les utilisateurs en ont besoin.

  - Il fournit des informations à des fins comptables (il permet de mesurer les appels, par exemple).

Outre les trois fonctions énoncées ci-dessus, les PBX peuvent offrir d’autres fonctionnalités d’appels telles que :

  - Les standards automatiques

  - Décompte des appels

  - Prise d’appels

  - Transfert d’appel

  - Appel en attente

  - Téléconférence

  - DID (Direct Inward Dialing)

  - Ne pas déranger (DND)

Même si l’on recense plusieurs fabricants de PBX, ils appartiennent tous à deux catégories de base : analogue et numérique. Ces types de PBX sont souvent appelées PBX *legacy* ou *traditional*.

En général, les systèmes PBX sont connectés au central téléphonique de la société de téléphonie à l’aide de lignes téléphoniques spéciales, comme les lignes T1 et E1. Ces lignes disposent de canaux multiples. Elles sont aussi appelées *trunk lines.*. Elles permettent au central téléphonique ou au PBX d’envoyer plusieurs appels par la même ligne, pour une meilleure efficacité, en utilisant un plan de câblage simplifié. Un PBX peut aussi fonctionner avec des lignes analogiques ou RNIS.

En configurant votre PBX en conséquence, vous pouvez contrôler le nombre de canaux ou de lignes que vous souhaitez configurer pour recevoir des appels externes, mais aussi décider du nombre de canaux ou de lignes affectés aux appels internes. Une telle configuration permet d’éviter les signaux occupés et de configurer le nombre de canaux ou de lignes qui peuvent être affectés aux applications telles que les centres d’appels. Une bonne configuration de votre PBX permet de gérer à moindre coût les canaux ou lignes de votre organisation, car elle réduit les besoins en location de lignes.

Un PBX peut acheminer des numéros de téléphone particuliers vers un téléphone précis ; les utilisateurs peuvent donc avoir un numéro de téléphone ou de poste personnel. C’est ce qu’on appelle un numéro de téléphone DID (Direct Inward Dial). Lorsque qu’un numéro de téléphone est composé, la société de téléphonie envoie le numéro DID vers le PBX à l’aide du service d’identification du numéro composé (DNIS). Comme la société de téléphonie utilise ce service, il n’est pas nécessaire qu’un opérateur intervienne pour acheminer l’appel. Le PBX dispose des informations nécessaires pour acheminer correctement l’appel vers le numéro composé par l’appelant. Pour obtenir la liste des PBX pris en charge par la messagerie unifiée, voir [Gestionnaire de téléphonie pour Exchange 2013](telephony-advisor-for-exchange-2013-exchange-2013-help.md).

Retour au début

## PBX analogiques et numériques

Les PBX analogiques envoient des informations vocales et de signalisation d’appel, comme la fréquence vocale d’un numéro composé, sous forme de son analogique. Le son n’est donc jamais numérisé. Pour diriger l’appel correctement, le PBX et le central de la société de téléphonie doivent écouter les informations de signalisation.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Le terme technique de la numérotation multifréquence est « numérotation en fréquences vocales ». Lorsque l’appelant appuie sur une touche d’un clavier téléphonique, le téléphone génère deux tonalités distinctes : une tonalité à haute fréquence et une à basse fréquence. Lorsqu’une personne parle dans le combiné, une seule tonalité ou fréquence est émise. L’envoi de deux tonalités avec des fréquences différentes en même temps réduit la possibilité que les tonalités de signalisation soient interprétées comme voix humaine ou qu’une voix humaine soit interprétée comme tonalités de signalisation.</td>
</tr>
</tbody>
</table>


Les PBX numériques codent ou numérisent les sons analogiques en format numérique. Les PBX numériques codent en général les sons vocaux à l’aide d’un codec audio standard comme G.711 ou G.729. Une fois la voix numérique codée, elle est envoyée dans un canal à l’aide de la commutation de circuits. La commutation de circuits établit une connexion ouverte de bout en bout. Elle laisse le canal ouvert pendant la durée de l’appel pour l’utilisation exclusive de l’appelant. Cependant, la méthode de signalisation utilisée par le PBX dépend des fabricants. Ces derniers peuvent en effet avoir développé une méthode de signalisation propre pour la configuration des appels.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Les PBX numériques peuvent prendre en charge les lignes spécialisées numériques comme analogiques.</td>
</tr>
</tbody>
</table>


Dans les organisations de grande taille, le PBX permet aux employés situés dans différents endroits de se contacter en composant un numéro de poste. Cette opération s’effectue avec un seul PBX ou avec plusieurs PBX mis en réseau. Les PBX situés en différents endroits peuvent être connectés à un seul réseau transparent de commutation de circuits à l’aide de lignes T1 ou E1. Lorsque ces lignes relient des PBX, elles sont souvent appelées *tie lines*. Les PBX communiquent les uns avec les autres via ces lignes privées en utilisant un protocole de PBX vers PBX comme QSIG. Le protocole QSIG permet à plusieurs PBX de se comporter comme un seul PBX.

Ce type d’environnement PBX peut aussi comprendre des fonctionnalités avancées, comme le transfert d’appel ou la téléconférence. En plus de permettre des fonctionnalités avancées, deux PBX connectés peuvent aussi permettre à l’organisation d’économiser de l’argent car les frais découlant des longues distances qui séparent les employés situés en différents endroits sont réduits. En effet, un appel passé entre deux employés reste sur la ligne privée entre les PBX et nécessite que l’utilisateur ne compose que le numéro de poste de l’autre utilisateur au lieu de passer un appel longue distance.

Dans un environnement téléphonique composé d’un seul ou de plusieurs PBX numérique(s) ou analogique(s), une passerelle VoIP est nécessaire entre le PBX et les serveurs d’accès au client et de boîtes aux lettres Exchange 2013 pour convertir les protocoles basés sur le circuit que l’on trouve sur un réseau téléphonique en protocoles IP présents sur un réseau de données. Pour plus d’informations sur les passerelles VoIP, consultez les rubriques suivantes :

  - [Passerelles IP de messagerie unifiée](um-ip-gateways-exchange-2013-help.md)

  - [Connecter une passerelle voix sur IP pour communiquer avec un PBX](connect-a-voip-gateway-to-communicate-with-a-pbx-exchange-2013-help.md)

Pour obtenir la liste des passerelles VoIP prises en charge pour la messagerie unifiée, voir [Gestionnaire de téléphonie pour Exchange 2013](telephony-advisor-for-exchange-2013-exchange-2013-help.md).

Retour au début

## Configuration PBX IP

Un PBX IP prend en charge le protocole IP pour connecter des téléphones en utilisant un LAN Ethernet ou un LAN de commutation de paquets. Cela permet d’envoyer des conversations vocales en paquets IP ou de données. Un PBX IP peut avoir plusieurs interfaces. Il s’agit entre autres des interfaces pour les réseaux de données et des autres interfaces qui permettent une connexion entre un réseau téléphonique ou de commutation de circuits.

Le développement des protocoles Internet en temps réel a favorisé l’envoi de messages vocaux et de télécopie par un réseau de données. De tels protocoles comprennent les protocoles VoIP utilisés avec la messagerie unifiée : Protocole SIP (Session Initiation Protocol) sur protocole TCP (Transmission Control Protocol) pour la messagerie vocale. Ces protocoles permettent d’envoyer des messages vocaux et de télécopie par le biais d’un réseau de données. Les protocoles VoIP en temps réel sont nécessaires pour l’envoi de messages vocaux via un réseau de données ou de commutation de paquets afin que l’ordre et le délai de remise soient maintenus et contrôlés. Si ces protocoles ne sont pas utilisés à cette fin, la voix humaine est rompue et paraît incohérente ou les images peuvent sembler déformées. Pour obtenir la liste des PBX IP pris en charge par la messagerie unifiée, voir [Gestionnaire de téléphonie pour Exchange 2013](telephony-advisor-for-exchange-2013-exchange-2013-help.md).

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>La messagerie unifiée prend seulement en charge SIP sur TCP.</td>
</tr>
</tbody>
</table>


## Configuration des PBX IP traditionnels

Un PBX IP standard ou traditionnel contient au moins une seule interface réseau reliée à un réseau de données à l’aide des protocoles VoIP. Il peut aussi contenir des interfaces réseau supplémentaires ou d’autres interfaces téléphoniques qui lui permettent de se connecter à un réseau téléphonique existant tel le RTC. La connexion au réseau de données autorise les communications avec d’autres hôtes VoIP situés sur le réseau de données à l’aide d’un paquet de données IP. Ces hôtes VoIP comportent d’autres PBX IP, téléphones basés sur VoIP, passerelles VoIP et serveurs d’accès au client et de boîtes aux lettres exécutant des services de messagerie unifiée. Un PBX IP traditionnel ne prend pas en charge les téléphones analogiques ou numériques. Il prend seulement en charge les téléphones VoIP.

Puisque le PBX IP peut se connecter à un réseau de données et convertir les protocoles basés sur le circuit depuis le RTC vers les protocoles VoIP à commutation de paquets, une passerelle VoIP n’est peut-être pas requise pour activer la communication avec les serveurs de messagerie unifiée situés sur le réseau de données.

## Configuration PBX IP hybride

Les PBX IP hybrides peuvent fournir des capacités VoIP, numériques ou analogiques. Si les interfaces appropriées sont installées sur un PBX IP et que le logiciel prenant en charge différents types d’interface est installé correctement, le PBX IP est considéré comme hybride. Un PBX IP hybride permet d’utiliser une combinaison de téléphones basés sur IP, analogiques ou numériques.

La plupart des PBX IP modernes peuvent prendre en charge et fournir les trois types de communication vocale. Un PBX IP traditionnel peut être mis à niveau pour devenir hybride par l’installation des interfaces et des mises à jour logicielles et de microprogramme nécessaires.

La combinaison de téléphones basés IP, analogiques et numériques permet aux utilisateurs de votre organisation d’utiliser de nombreuses fonctionnalités nouvelles. De plus, cette combinaison apporte une grande flexibilité à votre environnement téléphonique. L’utilisation d’un PBX IP hydride permet aussi à votre organisation de migrer plus progressivement vers un environnement téléphonique et vers un système de messagerie vocale entièrement basés sur VoIP.

Différents facteurs déterminent si une passerelle VoIP est nécessaire lors de la connexion à des serveurs d’accès au client ou de boîtes aux lettres. L’un de ces facteurs est la compatibilité des protocoles VoIP utilisés par le PBX IP ou le PBX IP hybride et la messagerie unifiée. Si une passerelle VoIP n’est pas requise, cela réduira la complexité de l’infrastructure téléphonique et la prise en charge de la messagerie unifiée sera simplifiée.

Retour au début

## Identification de l’appelant ou de l’appelé

Cette identification est un service de société de téléphonie qui donne à la personne appelée le numéro de téléphone de l’appelant, voire son nom, ou d’autres informations sur l’appel. Ces informations sont envoyées par un câble série à l’aide de la signalisation d’appel. Lorsqu’un appel est reçu par un PBX ou un PBX IP depuis une société de téléphonie, l’appel comprend des informations d’identification d’appel, telles que :

  - le numéro de l’appelant ;

  - le numéro de l’appelé ;

  - les codes d’états comme la non-réponse, l’état ou la condition de la ligne, la ligne occupée et le transfert d’appel ;

  - la ligne ou le numéro de port utilisé pour l’appel.

  - En téléphonie, les informations de signalisation sont utilisées pour échanger des informations entre les points de terminaison d’un réseau pour configurer, contrôler et terminer des appels. Plusieurs méthodes de signalisation utilisées par les passerelles VoIP et les PBX IP sont prises en charge par la messagerie unifiée. La méthode de signalisation utilisée dépend du type d’appareil et de la méthode de signalisation utilisés par la société de téléphonie. Le facteur le plus important est la prise en charge par l’appareil connecté à la société de téléphonie et à la passerelleVo IP ou au PBX IP d’au moins une méthode de signalisation qui permet aux informations relatives à l’appelant et à l’appelé d’être envoyées par et vers les appelants. Pour plus d’informations sur les informations de configuration de la signalisation pour une passerelle VoIP prise en charge, voir [Gestionnaire de téléphonie pour Exchange 2013](telephony-advisor-for-exchange-2013-exchange-2013-help.md).

Même s’il existe d’autres méthodes de signalisation, les deux plus courantes sont les suivantes :

  - **Simplified Message Desk Interface (SMDI) :** Le protocole SMDI est utilisé pour fournir des informations relatives à la signalisation, au contrôle des appels et à l’identification de l’appelant depuis une interface entre un système téléphonique et un système de messagerie vocale. Il est utilisé pour apporter au système de messagerie vocale les informations qui lui sont nécessaires pour traiter un appel entrant. Chaque fois qu’un appel entrant est passé à l’aide du SMDI via une interface série ou RS-232, les informations envoyées permettent d’identifier la ligne ou le port, le type d’appel et les numéros de l’appelant et de l’appelé. Le câble SMDI se connecte depuis un appareil comme un PBX vers une connexion série sur la passerelle VoIP. Toutefois, SMDI est également utilisé avec les PBX IP. Le protocole SMDI ne prend en charge qu’un maximum de 10 chiffres pour chaque numéro d’appelant ou d’appelé. Il s’agit d’une limite du protocole qui ne peut pas être modifiée.

  - **In-band :** La signalisation In-band permet l’échange d’informations relatives à l’identification, au contrôle et à la signalisation des appels à partir d’une société de téléphonie. Ces informations sont envoyées par le biais du même canal et sur la même bande (de 300 Hz à 3,4 kHz) alors que la voix et les autres sons sont produits durant l’appel. Par exemple, lorsqu’un utilisateur passe un appel à l’aide de la numérotation DTMF ou multifréquence et parle à son interlocuteur, la conversation vocale et celle de tonalité utilisent le même canal et la même bande. La signalisation In-band est moins sécurisée parce que les signaux de contrôle sont exposés à l’utilisateur et cette méthode de signalisation est moins commune que le SMDI. La signalisation In-band s’applique seulement au CAS (Channel Associated Signaling).

Retour au début

