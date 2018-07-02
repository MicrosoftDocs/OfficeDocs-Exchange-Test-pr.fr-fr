---
title: 'Enregistrement de la connectivité: Exchange 2013 Help'
TOCTitle: Enregistrement de la connectivité
ms:assetid: c31fd710-4ae4-4d9a-8936-d056e7ca2748
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb124500(v=EXCHG.150)
ms:contentKeyID: 50479111
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Enregistrement de la connectivité

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2015-03-09_

La journalisation de connexion consigne l’activité de connexion sortante utilisée pour transmettre des messages en provenance d’un service de transport sur le serveur Exchange. Le but du journal de connectivité n’est pas de suivre la transmission des messages électroniques individuels. Le journal de connectivité suit plutôt l’activité de connexion de la source à la destination, indépendamment du nombre de messages transmis. L’enregistrement de la connectivité est disponible dans le service de transport frontal sur les serveurs d’accès au client, le service de transport sur ​​des serveurs de boîtes aux lettres et la boîte aux lettres du service de transport sur ​​des serveurs de boîtes aux lettres. La liste suivante décrit les types d’information enregistrés dans le journal de connectivité :

  - Source

  - Destination

  - Informations de résolution DNS

  - informations détaillées sur les échecs de connexion

  - nombre de messages et d’octets transmis

Vous utilisez les cmdlets **Set-TransportService**, **Set-FrontEndTransportService** et **Set-MailboxTransportService** de l’environnement de ligne de commande Exchange Management Shell pour exécuter toutes les tâches de configuration du journal de connectivité. Les options suivantes sont disponibles pour les journaux de connectivité :

  - Activer ou désactiver l’enregistrement de la connectivité. Par défaut, le suivi des messages est activé.

  - Spécifier l’emplacement des fichiers journaux de connectivité.

  - Spécifier la taille maximale des fichiers journaux individuels de connectivité. La taille par défaut est 10 mégaoctets (Mo).

  - Spécifier la taille maximale du répertoire contenant les fichiers journaux de connectivité. La taille par défaut est 1000 Mo.

  - Spécifier l’âge maximal des fichiers journaux de connectivité. L’âge par défaut est 30 jours.

Par défaut, Exchange utilise l’enregistrement circulaire pour limiter le nombre de journaux de connectivité à partir de la taille et de l’âge du fichier afin de contrôler l’espace disque utilisé par les fichiers journaux de connectivité.

**Contenu de cette rubrique**

Structure des fichiers journaux de connectivité

Informations consignées dans le journal de connectivité

## Structure des fichiers journaux de connectivité

Par défaut, les fichiers journaux de connectivité se trouvent aux emplacements suivants :

  - **Transport service**   %ExchangeInstallPath%TransportRoles\\Logs\\Hub\\Connectivity

  - **Front End Transport service**   %ExchangeInstallPath%TransportRoles\\Logs\\FrontEnd\\Connectivity

  - **Mailbox Transport service**   %ExchangeInstallPath%TransportRoles\\Logs\\Mailbox\\Connectivity

La convention d’appellation pour les fichiers journaux de connectivité est CONNECTLOG*aaammjj-nnnn*.log. Les espaces réservés correspondent aux informations suivantes :

  - L’espace réservé *aaaammjj* est la date au format UTC (temps universel coordonné) à laquelle le fichier journal a été créé. L’espace réservé *aaaa* = année, *mm* = mois et *jj* = jour.

  - L’espace réservé *nnnn* est un numéro d’instance qui commence à la valeur 1 pour chaque jour.

Les informations sont consignées dans le fichier journal jusqu’à ce que la taille du fichier atteigne la valeur maximale spécifiée ; un nouveau fichier journal avec un numéro d’instance incrémenté est alors ouvert. Ce processus est répété au cours de la journée. L’enregistrement circulaire supprime les fichiers journaux les plus anciens lorsque le répertoire des journaux de connectivité atteint la taille maximale spécifiée ou lorsqu’un fichier journal atteint l’âge maximal spécifié.

Les journaux de connectivité sont des fichiers texte contenant des données au format CSV (valeurs séparées par des virgules). Chacun d’eux comporte un en-tête contenant les informations suivantes :

  - **\#Software**   Nom du logiciel ayant créé le fichier journal de connectivité. En règle générale, la valeur est Microsoft Exchange Server.

  - **\#Version**   Numéro de version du logiciel ayant créé le fichier journal de connectivité. La valeur actuelle est 15.0.0.0.

  - **\#Log-Type**   Valeur du type de champ, qui est Transport Connectivity Log.

  - **\#Date**   Date-heure UTC de création du fichier journal. La date-heure UTC est représentée au format de date-heure ISO 8601 : yyyy-mm-dd*yyyy-mm-dd*Thh:mm:ss.fff*hh:mm:ss.fff*Z, où yyyyy*yyyy* = année, mm*mm* = mois, dd*dd* = jour, T indique le début du composant temps, hh*hh* = heure, mm*mm* = minute, ss*ss* = seconde, fff*fff* = fractions de seconde et Z correspond à Zulu (qui est une autre manière de désigner le temps universel).

  - **\#Fields**   Noms de champ séparés par des virgules utilisés dans les fichiers journaux de connectivité.

Retour au début

## Informations consignées dans le journal de connectivité

Le journal de connectivité écrit chaque événement de connexion du service de transport sortant sur une ligne du journal de connectivité. Les informations stockées sur chaque ligne sont organisées par champs. Ces champs sont séparés par des virgules. Le tableau suivant décrit les champs utilisés pour classer chaque événement de connexion sortant.

### Champs utilisés pour classer chaque événement de connexion

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Nom de champ</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>date-time</strong></p></td>
<td><p>Date et heure, au format UTC, de l’événement de connexion. La date-heure UTC est représentée au format de date-heure ISO 8601 : yyyy-mm-dd<em>yyyy-mm-dd</em>Thh:mm:ss.fff<em>hh:mm:ss.fff</em>Z, où yyyyy<em>yyyy</em> = année, mm<em>mm</em> = mois, dd<em>dd</em> = jour, T indique le début du composant temps, hh<em>hh</em> = heure, mm<em>mm</em> = minute, ss<em>ss</em> = seconde, fff<em>fff</em> = fractions de seconde et Z correspond à Zulu (qui est une autre manière de désigner le temps universel).</p></td>
</tr>
<tr class="even">
<td><p><strong>session</strong></p></td>
<td><p>GUID unique pour chaque session SMTP ; même GUID pour chaque événement associé à la session SMTP. Pour les sessions MAPI dans le service de transport de boîtes aux lettres, le champ de session est vide.</p></td>
</tr>
<tr class="odd">
<td><p><strong>source</strong></p></td>
<td><p><strong>SMTP</strong> pour les connexions SMTP, <strong>MAPI</strong> pour les connexions de service de transport de boîtes aux lettres vers la base de données de boîtes aux lettres locale.</p></td>
</tr>
<tr class="even">
<td><p><strong>destination</strong></p></td>
<td><p>Nom de la destination.</p></td>
</tr>
<tr class="odd">
<td><p><strong>direction</strong></p></td>
<td><p>Un seul caractère qui représente le début, le milieu ou la fin de la connexion. Les valeurs possibles pour le champ de direction sont les suivantes :</p>
<ul>
<li><p><strong>+</strong> Connexion</p></li>
<li><p><strong>-</strong>   Déconnexion</p></li>
<li><p><strong>&gt;</strong>   Envoi</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>description</strong></p></td>
<td><p>Informations textuelles associées à l’événement de connexion. Les valeurs suivantes sont des exemples de valeurs pour le champ de description :</p>
<ul>
<li><p>Nombre et taille des messages transmis</p></li>
<li><p>Informations de résolution de l’enregistrement DNS MX pour les domaines de destination</p></li>
<li><p>Informations de résolution DNS pour les serveurs de boîtes aux lettres de destination</p></li>
<li><p>Messages d’établissement de connexion</p></li>
<li><p>Messages d’échec de connexion</p></li>
</ul></td>
</tr>
</tbody>
</table>


Lorsque le service de transport définit une connexion à une destination, il se peut qu’il soit prêt à envoyer un ou plusieurs messages. La connexion et les processus de transmission des messages génèrent plusieurs événements qui sont écrits sur plusieurs lignes dans le journal de connectivité. Les connexions simultanées à différentes destinations créent des entrées dans le journal de connectivité liées à différentes destinations qui sont entrecroisées. Toutefois, vous pouvez utiliser les champs date-heure, session, source et direction pour organiser les entrées du journal de connectivité pour chaque connexion distincte du début à la fin.

Retour au début

