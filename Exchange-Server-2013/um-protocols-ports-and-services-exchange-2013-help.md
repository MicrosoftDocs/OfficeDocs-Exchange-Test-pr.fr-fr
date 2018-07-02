---
title: 'Protocoles, ports et services de messagerie unifiée: Exchange 2013 Help'
TOCTitle: Protocoles, ports et services de messagerie unifiée
ms:assetid: 5997ce29-1755-48bb-8ff4-b08da549482a
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Aa998265(v=EXCHG.150)
ms:contentKeyID: 54652761
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Protocoles, ports et services de messagerie unifiée

 

_**Sapplique à :**Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :**2015-03-09_

Microsoft La messagerie unifiée Exchange 2013 nécessite l'utilisation de plusieurs ports TCP et UDP (User Datagram Protocol) pour établir une communication entre les serveurs Exchange 2013 et d'autres périphériques. En autorisant l'accès via ces ports IP, vous permettez à la messagerie unifiée de fonctionner correctement. Cette rubrique présente les ports TCP et UDP utilisés dans la messagerie unifiée Exchange 2013.

## Services et protocoles de messagerie unifiée

Exchange 2013 Les fonctionnalités et les services de messagerie unifiée dépendent des ports TCP et UDP statiques et dynamiques pour assurer le bon fonctionnement des serveurs d'accès au client exécutant le service de routeur d'appels de la messagerie unifiée Microsoft Exchange et des serveurs exécutant le service de messagerie unifiée Microsoft Exchange.Quand Exchange 2013 est installé, des règles de pare-feu Windows de trafic entrant statiques sont ajoutées pour Exchange. Si vous modifiez les ports TCP utilisés par les serveurs de boîtes aux lettres et d'accès au client, il sera peut-être nécessaire de reconfigurer les règles de pare-feu Windows pour permettre à la messagerie unifiée de fonctionner correctement.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159813.important(EXCHG.150).gif" title="Important" alt="Important" />Important :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Sur les serveurs de boîtes aux lettres et d'accès au client Exchange 2013 exécutant des composants et services de messagerie unifiée, le programme d'installation d'Exchange crée des règles de pare-feu de trafic entrant qui autorisent la communication entrante sans restrictions de port TCP. Les règles de trafic entrant suivantes pour les services de messagerie unifiée sont ajoutées :</td>
</tr>
</tbody>
</table>


1.  **SESWorker (GFW) (TCP-Entrée)**

2.  **UMCallRouter (GFW) (TCP-Entrée)**

3.  **UMCallRouter (TCP-Entrée)**

4.  **UMService (GFW) (TCP-Entrée)**

5.  **UMService (TCP-Entrée)**

6.  **UMWorkerProcess – RPC (TCP-Entrée)**

7.  **UMWorkerProcess (GFW) (TCP-Entrée)**

8.  **UMWorkerProcess (TCP-Entrée)**

## Protocole SIP (Session-Initiation Protocol)

Le protocole SIP est utilisé pour lancer, modifier et arrêter une session utilisateur interactive impliquant des éléments multimédia tels que la vidéo, le son, la messagerie instantanée, les jeux en ligne et la réalité virtuelle. Il s'agit, avec H.323, de l'un des principaux protocoles de signalisation pour VoIP (Voice over IP). La plupart des solutions VoIP normalisées utilisent des protocoles H.323 ou SIP. Toutefois, il existe également plusieurs conceptions et protocoles propriétaires. Les protocoles VoIP prennent généralement en charge des fonctions telles que la mise en attente d'appel, l'appel de conférence et le transfert d'appels.

Les clients SIP, tels que les passerelles VoIP et les PBX (Private Branch eXchange) IP peuvent utiliser le port TCP et UDP 5060 pour se connecter à des serveurs SIP, notamment à des serveurs d'accès au client exécutant le service de routeur d'appels de la messagerie unifiée Microsoft Exchange. Le protocole SIP n'est utilisé que pour configurer et discriminer des appels vocaux et vidéo. Toutes les communications vocales et vidéo utilisent le protocole RTP (Realtime Transport Protocol).

## Protocole RTP (Real-Time Transport Protocol)

Le protocole RTP définit un format de paquet standard pour la fourniture de contenu audio et vidéo sur un réseau donné, tel qu'Internet. Le protocole RTP ne fait que transporter des données vocales/vidéo sur le réseau. L'établissement et la discrimination des appels sont généralement assurés par le protocole SIP.

Le protocole RTP ne requiert pas de port TCP ou UDP standard ou statique avec lequel communiquer. Les communications RTP s'effectuent sur un numéro de port UDP pair, et le numéro impair suivant de port est utilisé pour les communications TCP. Bien qu'il n'existe pas d'affectations de plage de ports standard, le protocole RTP est généralement configuré pour utiliser les ports 1024 à 65535, et les serveurs de boîtes aux lettres exécutant le service de messagerie unifiée Microsoft Exchange suivent cette convention. Il est difficile pour le protocole RTP de traverser des pare-feu, car il utilise une plage de ports dynamique.

## Services web de messagerie unifiée

Les services web de messagerie unifiée installés sur des serveurs de boîtes aux lettres utilisent le protocole IP pour les communications réseau entre un client, le serveur de boîtes aux lettres et les ordinateurs exécutant d'autres rôles serveur Exchange 2013. Le fonctionnement correct de plusieurs fonctionnalités des clients Exchange 2013, Outlook Web App et Outlook 2013 dépend des services web de messagerie unifiée.

Les fonctionnalités clientes de messagerie unifiée suivantes dépendent des services web de messagerie unifiée :

  - Options de messagerie vocale disponibles avec Exchange 2013 et Outlook Web App, y compris la fonctionnalité Lire sur le téléphone et la possibilité de redéfinir un code confidentiel.

  - Fonctionnalité Lire sur le téléphone du client Outlook.

## Ports de messagerie unifiée

Le service de routeur d'appels de la messagerie unifiée Microsoft Exchange qui se trouve sur un serveur d'accès au client utilise SIP sur le protocole TCP (Transmission Control Protocol) ou l'authentification TLS (Transport Layer Security) mutuelle pour communiquer avec les serveurs de boîtes aux lettres qui exécutent le service de messagerie unifiée Microsoft Exchange. Afin d'éviter tout conflit de port TCP/UDP (User Datagram Protocol), le service de routeur d'appels de la messagerie unifiée Microsoft Exchange et le service de messagerie unifiée Microsoft Exchange sélectionnent et écoutent différents ports TCP par défaut. Ils peuvent accepter à la fois des connexions sécurisées et non sécurisées, en fonction de l'utilisation du protocole Mutual TLS avec le trafic SIP ou RTP. Par défaut, un serveur d'accès au client écoute les demandes SIP sur le port TCP 5060 en mode non sécurisé et le port TCP 5061 en mode Sécurisé SIP quand le protocole Mutual TLS est utilisé. Ces ports sont configurables au moyen de la cmdlet **Set-UMCallRouterSettings**. Le service de routeur d’appels de la messagerie unifiée Microsoft Exchange sur le serveur d’accès au client ne prend pas en charge le trafic de support (RTP ou SRTP). Ainsi, seuls les ports TCP, et non les ports UDP, sont utilisés. Par défaut, un serveur de boîtes aux lettres écoute les demandes SIP sur le port 5062 TCP en mode non sécurisé et le port 5063 TCP en mode Sécurisé SIP lorsque le protocole mutuel TLS est utilisé. Ces ports ne sont pas configurables à l’aide des cmdlets de l’environnement de ligne de commande Exchange Management Shell. Le service de messagerie unifiée Microsoft Exchange sur le serveur de boîtes aux lettres acceptera les connexions d'un serveur d'accès au client sur les ports SIP 5062 et 5063. Une fois que le serveur d'accès au client a redirigé la demande SIP vers un serveur de boîtes aux lettres, un canal de support RTP ou SRTP est créé à l'aide d'une passerelle VoIP, d'un PBX IP ou d'un SBC et du processus de travail de messagerie unifiée Microsoft Exchange sur le serveur de boîtes aux lettres.

Le tableau suivant résume les ports et protocoles d'Exchange 2013 et indique si les ports peuvent être modifiés.

### Ports d'écoute de messagerie unifiée

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Protocole</th>
<th>Port TCP</th>
<th>Port UDP</th>
<th>Est-il possible de modifier des ports ?</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>SIP (serveur d'accès au Client – service de routeur d'appels de la messagerie unifiée Microsoft)</p></td>
<td><p>5060 (non sécurisé), 5061 (sécurisé). Le service écoute sur les deux ports.</p></td>
<td><p>Non applicable</p></td>
<td><p>Oui, à l’aide de la cmdlet <strong>Set-UMCallRouterSettings</strong>.</p></td>
</tr>
<tr class="even">
<td><p>SIP (serveur de boîtes aux lettres – service de messagerie unifiée Microsoft Exchange)</p></td>
<td><p>5062 (non sécurisé), 5063 (sécurisé). Le service écoute sur les deux ports.</p></td>
<td><p>Non applicable</p></td>
<td><p>Les ports ne peuvent pas être modifiés.</p></td>
</tr>
<tr class="odd">
<td><p>SIP (serveur de boîtes aux lettres - processus de travail de messagerie unifiée)</p></td>
<td><p>5065 et 5067 pour TCP (non sécurisé). 5065 et 5067 pour une authentification TLS mutuelle (sécurisé). Si vous avez défini le mode Double, 5066 et 5068 sont également utilisés.</p></td>
<td><p>Non applicable</p></td>
<td><p>Les ports ne peuvent pas être modifiés.</p></td>
</tr>
<tr class="even">
<td><p>RTP (serveur de boîtes aux lettres - processus de travail de messagerie unifiée)</p></td>
<td><p>Non applicable</p></td>
<td><p>Ports compris entre 1024 et 65535.</p></td>
<td><p>Les ports peuvent être modifiés dans le fichier de configuration msexchangeum.config. Le fichier msexchangeum.config se trouve dans le dossier \Program Files\Microsoft\Exchange\V15\bin sur un serveur de messagerie unifiée Exchange 2013.</p></td>
</tr>
</tbody>
</table>


## Lync Server et ports de messagerie unifiée

La messagerie unifiée Exchange 2013 prend en charge le parcours NAT (Network Address Translation) et permet la prise en charge du support RTP sur un serveur de boîtes aux lettres par tunnel via un pare-feu NAT. Toutefois, pour que cela fonctionne, vous devez également avoir déployé Microsoft Office Communications Server 2007 R2 et Microsoft Lync Server 2010 ou Microsoft Lync 2013 dans votre environnement. Si vous déployez Exchange 2013 et Communications Server 2007 R2 ou Microsoft Lync Server 2010 ou Lync 2013 sur votre réseau, ce déploiement permet aux serveurs de boîtes aux lettres d'exécuter le service de messagerie unifiée Microsoft Exchange pour communiquer avec des points de terminaison en dehors d'un pare-feu NAT. Le serveur de boîtes aux lettres est associé à un pool Communications Server 2007 R2, Microsoft Lync Server 2010 ou Lync 2013 et obtient les jetons d'authentification appropriés auprès du service d'authentification A/V sur un ordinateur desservant ce pool Communications Server 2007 ou Lync Server particulier.

Le service d'authentification A/V est utilisé pour permettre aux médias vocaux RTP de traverser les périphériques et pare-feu NAT. Ceci est nécessaire car les passerelles multimédia traitent la signalisation uniquement et ne peuvent pas transporter la voix de manière sécurisée via un périphérique ou pare-feu NAT. Quand vous configurez un serveur de médiation dans Communications Server 2007 R2, Lync Server 2010 ou Lync 2013, vous spécifiez le serveur Edge A/V sur lequel le service d'authentification A/V est exécuté afin que le serveur de médiation identifie l'emplacement vers lequel transférer les paquets multimédias entrants.

Pour plus d'informations sur le déploiement de Communications Server 2007 R2, de Lync Server 2010 ou 2013 et de la messagerie unifiée Exchange 2013, consultez les rubriques suivantes :

  - [Présentation du déploiement de la messagerie unifiée Exchange 2013 et de Lync Server](deploying-exchange-2013-um-and-lync-server-overview-exchange-2013-help.md)

  - [Liste de contrôle : intégration de la messagerie unifiée d'Exchange 2013 à Lync Server](checklist-integrate-exchange-2013-um-with-lync-server-exchange-2013-help.md)

