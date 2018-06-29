---
title: 'Prise en charge du protocole IPv6 dans Exchange 2013: Exchange 2013 Help'
TOCTitle: Prise en charge du protocole IPv6 dans Exchange 2013
ms:assetid: 33543023-eb9a-4102-b990-84a818a52814
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Gg144561(v=EXCHG.150)
ms:contentKeyID: 50477870
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Prise en charge du protocole IPv6 dans Exchange 2013

 

_**Sapplique à :**Exchange Server 2013_

_**Dernière rubrique modifiée :**2016-12-09_

Le protocole IPv6 (Internet Protocol Version 6) est la version la plus récente du protocole Internet (IP). IPv6 est conçu pour corriger un grand nombre d'insuffisances d'IPv4, la précédente version du protocole Internet.

Dans Exchange Server 2013, le protocole IPv6 est pris en charge uniquement quand le protocole IPv4 est également installé et activé. En cas de déploiement d'Exchange 2013 dans cette configuration, et si le réseau prend en charge les protocoles IPv4 et IPv6, tous les serveurs Exchange peuvent échanger des données avec des périphériques, des serveurs et des clients utilisant des adresses IPv6.

Cette rubrique traite de l'adressage IPv6 dans Exchange 2013. Pour des informations générales sur le protocole IPv6, consultez la page [IPv6](https://go.microsoft.com/fwlink/p/?linkid=92582).

**Table des matières**

Prise en charge du protocole IPv6 dans les composants Exchange 2013

Activer ou désactiver les protocoles du système d'exploitation

Principes fondamentaux des adresses IPv6

## Prise en charge du protocole IPv6 dans les composants Exchange 2013

Le tableau suivant décrit les composants d'Exchange 2013 affectés par le protocole IPv6.

### Fonctionnalités d'Exchange 2013 et IPv6

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Fonctionnalité</th>
<th>Prise en charge IPv6</th>
<th>Commentaires</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Liste d'adresses IP autorisées et liste d'adresses IP bloquées dans l'agent de filtrage des connexions</p></td>
<td><p>Oui</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Fournisseurs de liste d'adresses IP autorisées et fournisseurs de liste d'adresses IP bloquées dans l'agent de filtrage des connexions.</p></td>
<td><p>Non</p></td>
<td><p>Il n'existe pas actuellement de protocole standard largement accepté pour la recherche d'adresses IPv6. La plupart des fournisseurs de listes d'adresses IP bloquées ne prennent pas en charge les adresses IPv6. C'est pourquoi, si vous autorisez des connexions anonymes à partir d'adresses IPv6 inconnues sur un connecteur de réception, vous augmentez la probabilité que des expéditeurs de courrier indésirable contournent les listes d'adresses bloquées et parviennent à faire pénétrer du courrier indésirable dans votre organisation.</p></td>
</tr>
<tr class="odd">
<td><p>Réputation de l'expéditeur dans l'Agent d'analyse de protocole</p></td>
<td><p>Non</p></td>
<td><p>L'Agent d'analyse de protocole ne calcule pas le niveau de réputation de l'expéditeur (SRL) pour les messages émis par des expéditeurs IPv6. Pour plus d'informations sur la réputation de l'expéditeur, consultez la rubrique <a href="sender-reputation-and-the-protocol-analysis-agent-exchange-2013-help.md">Réputation de l’expéditeur et agent d’analyse de protocole</a>.</p></td>
</tr>
<tr class="even">
<td><p>ID de l'expéditeur</p></td>
<td><p>Oui</p></td>
<td><p>Pour plus d'informations, consultez la rubrique <a href="sender-id-exchange-2013-help.md">ID de l'expéditeur</a>.</p></td>
</tr>
<tr class="odd">
<td><p>Connecteurs de réception</p></td>
<td><p>Oui</p></td>
<td><p>Des adresses IPv6 peuvent être acceptées pour les composants suivants :</p>
<ul>
<li><p>Liaisons d'adresses IP locales</p></li>
<li><p>Adresses IP distantes</p></li>
<li><p>Plages d'adresses IP</p></li>
</ul>
<p>Il est fortement déconseillé de configurer les connecteurs de réception pour accepter des connexions anonymes d'adresses IPv6 inconnues. Si votre organisation doit recevoir des messages électroniques provenant d'expéditeurs utilisant des adresses IPv6, créez un connecteur de réception dédié limitant les adresses IP distantes aux adresses IPv6 spécifiques utilisées par ces expéditeurs.</p>
<p>Pour plus d'informations, consultez la rubrique <a href="receive-connectors-exchange-2013-help.md">Connecteurs de réception</a>.</p></td>
</tr>
<tr class="even">
<td><p>Connecteurs d'envoi</p></td>
<td><p>Oui</p></td>
<td><p>Des adresses IPv6 peuvent être acceptées pour les composants suivants :</p>
<ul>
<li><p>Adresses IP d'hôte actif</p></li>
<li><p>Paramètre <em>SourceIPAddress</em> pour les connecteurs d'envoi configurés sur des serveurs de transport Edge</p></li>
</ul>
<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Si vous voulez spécifier une adresse IPv6 pour le paramètre <em>SourceIPAddress</em>, veillez à ce que les enregistrements DNS AAAA et de ressource de messagerie Exchange (MX) appropriés soient configurés correctement. Cela permet de garantir la remise du message si un serveur de messagerie distant tente d'effectuer un type quelconque de test de recherche inversée sur l'adresse IPv6 spécifiée.</td>
</tr>
</tbody>
</table>

<p>Pour plus d'informations, consultez la rubrique <a href="send-connectors-exchange-2013-help.md">Connecteurs d'envoi</a>.</p></td>
</tr>
<tr class="odd">
<td><p>Limites de fréquence des messages entrants</p></td>
<td><p>Partielle</p></td>
<td><p>Les limites de fréquence des messages entrants que vous pouvez définir sur un connecteur de réception, telles que les paramètres <em>MaxInboundConnectionPercentagePerSource</em>, <em>MaxInboundConnectionPerSource</em> et <em>TarpitInterval</em> ne s'appliquent qu'à l'adresse IPv6 globale. Les adresses IPv6 de liaison locale et de site local ne sont pas affectées par les limites de fréquence de messages entrants spécifiées.</p></td>
</tr>
<tr class="even">
<td><p>Messagerie unifiée</p></td>
<td><p>Oui</p></td>
<td><p>Pour plus d'informations, consultez la rubrique <a href="ipv6-support-in-unified-messaging-exchange-2013-help.md">Prise en charge d’IPv6 dans la messagerie unifiée</a>.</p></td>
</tr>
<tr class="odd">
<td><p>Membre de groupe de disponibilité de base de données (DAG)</p></td>
<td><p>Oui</p></td>
<td><p>Les adresses IPv6 statiques sont prises en charge par Windows Server et le service de cluster. Toutefois, l'utilisation d'adresses IPv6 statiques est contraire aux meilleures pratiques. Exchange 2013 ne prend pas en charge la configuration d'adresses IPv6 statiques en cours d'installation.</p>
<p>Les clusters de basculement prennent en charge le protocole ISATAP (Intrasite Automatic Tunneling Addressing Protocol). Ils ne prennent en charge que les adresses IPv6 permettant un enregistrement dynamique dans DNS. Des adresses de liaison locale ne peuvent pas être utilisées dans un cluster.</p>
<p>Pour plus d'informations sur la configuration réseau requise du DAG, consultez la section « Configuration réseau requise » dans <a href="planning-for-high-availability-and-site-resilience-exchange-2013-help.md">Planification d'une haute disponibilité et d'une résilience de site</a>.</p></td>
</tr>
</tbody>
</table>


Retour au début

## Activer ou désactiver les protocoles du système d'exploitation

Les serveurs Exchange 2013 prennent entièrement en charge les réseaux IPv6. Par conséquent, même si vous n'utilisez pas IPv6, il n'est pas nécessaire de désactiver IPv6 sur vos serveurs Exchange.

Pour que le protocole IPv6 soit pris en charge dans Exchange 2013, IPv4 doit être installé et activé sur tous les serveurs Exchange 2013. La désinstallation du protocole IPv4 de vos serveurs Exchange 2013 n'est pas prise en charge.

Pour en savoir plus sur la prise en charge du protocole IPv6 dans Microsoft Windows, consultez [IPv6 pour Microsoft Windows : Forum Aux Questions](https://go.microsoft.com/fwlink/p/?linkid=147465).

Retour au début

## Principes fondamentaux des adresses IPv6

Un adresse IPv6 a une longueur de 128 bits. L'adresse est décrite à l'aide de la notation hexadécimale avec signe deux-points. Une notation hexadécimale avec signe deux-points décrit l'adresse 128 bits à l'aide de huit nombres hexadécimaux 16 bits à 4 chiffres séparés par le signe deux-points (:). 2001:0DB8:0000:0000:02AA:00FF:C0A8:640A correspond à un exemple d'adresse IPv6 en notation hexadécimale avec signe deux-points.

Vous pouvez exprimer une adresse IPv6 à l'aide des méthodes suivantes :

  - **Suppression des zéros non significatifs**   Vous pouvez omettre les zéros non significatifs dans n'importe lequel des huit nombres hexadécimaux à 4 chiffres dans une adresse IPv6.

  - **Compression avec double signe deux-points**   Vous pouvez utiliser le signe deux-points (::) pour représenter des signes hexadécimaux contigus de 16 bits contenant uniquement des zéros. Ces nombres comportant uniquement des zéros peuvent se trouver au début, au milieu ou à la fin de l'adresse IPv6. Vous ne pouvez utiliser une compression avec double signe deux-points qu'une seule fois dans une adresse IPv6.

  - **Notation décimale avec points de suite**   Vous pouvez exprimer les 32 derniers bits à la fin d'une adresse IPv6 en une notation décimale avec points de suite en séparant les signes 8 bits par des points (.). La notation décimale avec points de suite est fréquemment utilisée pour les adresses compatibles IPv4.

Le tableau suivant offre des exemples de notation d'adresse IPv6 ainsi que la syntaxe d'adresse IPv6 équivalente.

### Notation et syntaxe d'adresse IPv6

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Notation d'adresse IPv6</th>
<th>Syntaxe d'adresse IPv6</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Adresse IPv6 complète</p></td>
<td><p>2001:0DB8:0000:0000:02AA:00FF:C0A8:640A</p></td>
</tr>
<tr class="even">
<td><p>Adresse IPv6 utilisant des zéros non significatifs supprimés</p></td>
<td><p>2001:DB8:0:0:2AA:FF:C0A8:640A</p></td>
</tr>
<tr class="odd">
<td><p>Adresse IPv6 utilisant une compression avec double signe deux-points</p></td>
<td><p>2001:DB8::2AA:FF:C0A8:640A</p></td>
</tr>
<tr class="even">
<td><p>Adresse IPv6 utilisant une notation décimale avec points de suite</p></td>
<td><p>2001:DB8::2AA:FF:192.168.100.10</p></td>
</tr>
</tbody>
</table>


Les adresses IPv6 sont catégorisées selon les types suivants :

  - **Adresse unicast**   Paquet remis à une interface.

  - **Adresse multicast**   Paquet remis à plusieurs interfaces.

  - **Adresse anycast**   Paquet remis à l'interface la plus proche parmi plusieurs interfaces. La distance entre les interfaces est définie par le coût du routage.

Les adresses unicast IPv6 ont les portées possibles suivantes :

  - **Liaison locale**   La portée de l'adresse IPv6 est le sous-réseau local. Les adresses de liaison locale IPv6 sont comparables aux adresses de liaison locale IPv4 utilisées dans APIPA (Automatic Private IP Addressing).

  - **Site local**   La portée de l'adresse IPv6 est l'organisation locale. Les adresses de site local ont été désapprouvées par la norme RFC 3879 et remplacées par des adresses locales uniques telles que définies dans la norme RFC 4193. Les adresses de site local IPv6 et les adresses locales uniques IPv6 sont comparables à des adresses IP privées IPv4.

  - **Globale**   La portée de l'adresse IPv6 est le monde entier. Les adresses globales IPv6 sont comparables aux adresses IP publiques IPv4.

Le tableau suivant fournit une comparaison entre des éléments IPv4 et IPv6.

### Éléments IPv4 et IPv6

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Élément</th>
<th>IPv4</th>
<th>IPv6</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Adresse IP privée</p></td>
<td><p>10.0.0.0/8</p>
<p>172.16.0.0/12</p>
<p>192.168.0.0/16</p></td>
<td><p>FD00::/8</p></td>
</tr>
<tr class="even">
<td><p>Adresse de liaison locale</p></td>
<td><p>169.254.0.0/16</p></td>
<td><p>FE80::/64</p></td>
</tr>
<tr class="odd">
<td><p>Adresse de bouclage</p></td>
<td><p>127.0.0.1</p></td>
<td><p>::1</p></td>
</tr>
<tr class="even">
<td><p>Adresse non spécifiée</p></td>
<td><p>0.0.0.0</p></td>
<td><p>::</p></td>
</tr>
<tr class="odd">
<td><p>Résolution d'adresse</p></td>
<td><p>Protocole ARP (Address Resolution Protocol)</p></td>
<td><p>Découverte de voisin</p></td>
</tr>
<tr class="even">
<td><p>Résolution de nom d'hôte DNS (Domain Name System)</p></td>
<td><p>Enregistrement d'adresse (enregistrement A)</p></td>
<td><p>Enregistrement AAAA ou enregistrement A6</p></td>
</tr>
</tbody>
</table>


Pour plus d'informations sur l'adressage IPv6, consultez la rubrique [Types d'adresse IPv6](https://go.microsoft.com/fwlink/p/?linkid=98357).

## Formats d'entrée d'adresse IPv6 pris en charge

Les types de format d'entrée d'adresse IPv6 pris en charge dans Exchange 2013 sont les suivants :

  - adresse IPv6 unique

  - plage d'adresses IPv6

  - adresse IPv6 avec masque de sous-réseau

  - adresse IPv6 avec masque de sous-réseau utilisant une notation CIDR (Routage inter-domaines sans classe)

Le tableau suivant offre des exemples de formats d'entrée d'adresse IPv6 acceptables dans Exchange 2013.

### Exemples d'adresse IPv6

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Type</th>
<th>Exemple d'adresse IPv6</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Adresse unique</p></td>
<td><p>2001:DB8::2AA:FF:C0A8:640A</p></td>
</tr>
<tr class="even">
<td><p>Plage d'adresses</p></td>
<td><p>2001:DB8::2AA:FF:C0A8:640A-2001:DB8::2AA:FF:C0A8:6414</p></td>
</tr>
<tr class="odd">
<td><p>Adresse avec masque de sous-réseau</p></td>
<td><p>2001:DB8::2AA:FF:C0A8:640A(FFFF:FFFF:FFFF:FFFF::)</p></td>
</tr>
<tr class="even">
<td><p>Adresse avec masque de sous-réseau utilisant une notation CIDR</p></td>
<td><p>2001:DB8::2AA:FF:C0A8:640A/64</p></td>
</tr>
</tbody>
</table>


Dans Exchange 2013, les formats d'entrées suivants sont pris en charge :

  - Suppression des zéros non significatifs

  - Compression avec double signe deux-points

  - Notation décimale avec points de suite

Retour au début

