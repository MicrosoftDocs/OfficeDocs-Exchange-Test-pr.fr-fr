---
title: 'Enregistrement dans le journal de protocole: Exchange 2013 Help'
TOCTitle: Enregistrement dans le journal de protocole
ms:assetid: 40da446b-bcc3-4a97-ace7-a54f6ddebd79
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Aa997624(v=EXCHG.150)
ms:contentKeyID: 50478017
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Enregistrement dans le journal de protocole

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2015-03-09_

L'enregistrement dans le journal de protocole enregistre les conversations SMTP entre les serveurs de messagerie dans le cadre de la remise des messages. Ces conversations SMTP se produisent sur les connecteurs d'envoi et de réception disponibles dans le service de transport frontal sur les serveurs d'accès au client, le service de transport sur ​​des serveurs de boîtes aux lettres et le service de transport de boîtes aux lettres sur ​​des serveurs de boîtes aux lettres. Vous pouvez utiliser l'enregistrement dans le journal de protocole pour identifier les problèmes de flux de messagerie.

Par défaut, l'enregistrement dans le journal de protocole est désactivé sur les connecteurs d'envoi et de réception. L'enregistrement dans le journal de protocole est activé ou désactivé sur chacun des connecteurs. D'autres options de journal de protocole sont définies pour tous les connecteurs de réception ou tous les connecteurs d'envoi qui existent dans chaque service de transport individuel sur le serveur. Tous les connecteurs de réception dans un service de transport partagent les mêmes fichiers journaux de protocole et options de journal de protocole. Ces fichiers journaux de protocole et options de journal de protocole sont distincts des fichiers journaux de protocole et des options de journal de protocole du connecteur d'envoi dans le service de transport sur le même serveur.

Les options suivantes sont disponibles pour les journaux de protocole de tous les connecteurs d'envoi ou de réception dans chaque service de transport sur le serveur Exchange :

  - Spécifier l'emplacement des fichiers journaux de protocole des connecteurs d'envoi ou de réception.

  - Spécifier la taille maximale des fichiers journaux de protocole des connecteurs d'envoi ou de réception. La taille par défaut est de 10 mégaoctets (Mo).

  - Spécifier la taille maximale du répertoire contenant les fichiers journaux de protocole des connecteurs d'envoi ou de réception. La taille par défaut est 250 Mo.

  - Spécifier l'âge maximal des fichiers journaux de protocole des connecteurs d'envoi ou de réception. L'âge par défaut est 30 jours.

Par défaut, Exchange utilise l'enregistrement circulaire pour limiter le nombre de journaux de protocole en fonction de la taille et de l'ancienneté du fichier afin de contrôler l'espace disque utilisé par les fichiers journaux.

Un connecteur d'envoi spécial, appelé connecteur d'envoi intra-organisationnel, existe dans le service de transport sur chaque serveur de boîtes aux lettres et dans le service de transport frontal sur chaque serveur d'accès au client. Ce connecteur est créé de façon implicite, invisible et ne requiert aucune gestion. Le connecteur d'envoi intra-organisationnel est utilisé par les services de transport suivants :

  - **Service de transport sur les serveurs de boîtes aux lettres**
    
      - Relaie des messages vers le service de transport et le service de transport de boîtes aux lettres sur d'autres serveurs de boîtes aux lettres Exchange 2013 dans l'organisation.
    
      - Relaie des messages vers d'autres serveurs de transport Hub Exchange 2007 ou Exchange 2010 dans l'organisation.
    
      - Relaie des messages vers des serveurs de transport Edge dans le réseau de périmètre.

  - **Service de transport frontal sur les serveurs d'accès au client**   Relaie des messages vers le service de transport sur des serveurs de boîtes aux lettres Exchange 2013 dans l'organisation.

Un connecteur d'envoi équivalent, appelé connecteur d'envoi de remise de boîte aux lettres, existe dans le service de transport de boîtes aux lettres sur chaque serveur de boîtes aux lettres. Ce connecteur est aussi créé de façon implicite, invisible et ne requiert aucune gestion. Le connecteur d'envoi de remise de boîte aux lettres permet de relayer des messages vers le service de transport et le service de transport de boîtes aux lettres sur d'autres serveurs de boîtes aux lettres dans l'organisation.

Par défaut, l'enregistrement dans le journal de protocole pour le connecteur d'envoi de remise de boîte aux lettres est aussi désactivé. Vous pouvez activer ou désactiver l'enregistrement dans le journal de protocole pour le connecteur d'envoi de remise de boîte aux lettres à l'aide du paramètre *MailboxDeliveryConnectorProtocolLoggingLevel* de la cmdlet **Set-MailboxTransportService**. Si vous activez la journalisation du protocole pour le connecteur d'envoi de remise de boîte aux lettres, la journalisation est effectuée dans les journaux de protocole du connecteur d'envoi pour le service de transport de boîtes aux lettres sur le serveur de boîtes aux lettres.

**Contenu de cette rubrique**

Structure des fichiers journaux de protocole

Informations écrites dans le journal de protocole

## Structure des fichiers journaux de protocole

Par défaut, les fichiers journaux de protocole se trouvent aux emplacements suivants :

  - **Fichiers journaux de protocole du connecteur de réception pour le service de transport sur des serveurs de boîtes aux lettres**   %ExchangeInstallPath%TransportRoles\\Logs\\Hub\\ProtocolLog\\SmtpReceive

  - **Fichiers journaux de protocole du connecteur de réception pour le service de transport de boîtes aux lettres sur des serveurs de boîtes aux lettres**   %ExchangeInstallPath%TransportRoles\\Logs\\Mailbox\\ProtocolLog\\SmtpReceive

  - **Fichiers journaux de protocole du connecteur de réception pour le service de transport frontal sur des serveurs d'accès au client**   %ExchangeInstallPath%TransportRoles\\Logs\\FrontEnd\\ProtocolLog\\SmtpReceive

  - **Fichiers journaux de protocole du connecteur d'envoi pour le service de transport sur des serveurs de boîtes aux lettres**   %ExchangeInstallPath%TransportRoles\\Logs\\Hub\\ProtocolLog\\SmtpSend

  - **Fichiers journaux de protocole du connecteur d'envoi pour le service de transport de boîtes aux lettres sur des serveurs de boîtes aux lettres**   %ExchangeInstallPath%TransportRoles\\Logs\\Mailbox\\ProtocolLog\\SmtpSend

  - **Fichiers journaux de protocole du connecteur d'envoi pour le service de transport frontal sur des serveurs d'accès au client**   %ExchangeInstallPath%TransportRoles\\Logs\\FrontEnd\\ProtocolLog\\SmtpSend

La convention d'appellation des fichiers journaux dans chaque répertoire des journaux de protocole est *prefixyyyymmdd-nnnn*.log. Les espaces réservés correspondent aux informations suivantes :

  - L'espace réservé *prefix* est SEND pour les connecteurs d'envoi ou RECV pour les connecteurs de réception.

  - L'espace réservé *aaaammjj* correspond à une date au format UTC (Coordinated Universal Time) à laquelle le fichier journal a été créé. L'espace réservé *aaaa* = année, *mm* = mois et *jj* = jour.

  - L'espace réservé *nnnn* est un numéro d'instance qui commence à la valeur 1 pour chaque jour.

Les informations sont consignées dans le fichier journal jusqu'à ce que la taille du fichier atteigne la valeur maximale spécifiée ; un nouveau fichier journal avec un numéro d'instance incrémenté est alors ouvert. Ce processus est répété au cours de la journée. L'enregistrement circulaire supprime les fichiers journaux les plus anciens lorsque le répertoire des journaux de protocole atteint la taille maximale spécifiée ou lorsqu'un fichier journal atteint l'âge maximal spécifié.

Les fichiers journaux de protocole sont des fichiers texte contenant des données au format CSV (valeurs séparées par une virgule). Chaque fichier journal de protocole comporte un en-tête avec les informations suivantes :

  - **\#Software**   Nom du logiciel ayant créé le fichier journal de protocole. En règle générale, la valeur est Microsoft Exchange Server.

  - **\#Version**   Numéro de version du logiciel ayant créé le fichier journal de protocole. La valeur actuelle est 15.0.0.0.

  - **\#Log-Type**   Valeur de type de journal de ce champ qui est SMTP Receive Protocol Log ou SMTP Send Protocol Log.

  - **\#Date**   Date-heure au format UTC de création du fichier journal. La date-heure UTC est représentée au format de date-heure ISO 8601 : yyyy-mm-dd*yyyy-mm-dd*Thh:mm:ss.fff*hh:mm:ss.fff*Z, où yyyyy*yyyy* = année, mm*mm* = mois, dd*dd* = jour, T indique le début du composant temps, hh*hh* = heure, mm*mm* = minute, ss*ss* = seconde, fff*fff* = fractions de seconde et Z correspond à Zulu (qui est une autre manière de désigner le temps universel).

  - **\#Fields**   Noms de champ séparés par des virgules utilisés dans les fichiers journaux de protocole.

Retour au début

## Informations écrites dans le journal de protocole

Le journal de protocole stocke les événements de protocole SMTP sur une seule ligne dans le journal de protocole. Les informations stockées sur chaque ligne sont organisées par champs. Ces champs sont séparés par des virgules. Le tableau suivant décrit les champs utilisés pour classer chaque protocole.

### Champs utilisés pour classer chaque événement de protocole

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
<td><p>Date et heure, au format UTC, de l'événement de protocole. La date-heure UTC est représentée au format de date-heure ISO 8601 : yyyy-mm-dd<em>yyyy-mm-dd</em>Thh:mm:ss.fff<em>hh:mm:ss.fff</em>Z, où yyyyy<em>yyyy</em> = année, mm<em>mm</em> = mois, dd<em>dd</em> = jour, T indique le début du composant temps, hh<em>hh</em> = heure, mm<em>mm</em> = minute, ss<em>ss</em> = seconde, fff<em>fff</em> = fractions de seconde et Z correspond à Zulu (qui est une autre manière de désigner le temps universel).</p></td>
</tr>
<tr class="even">
<td><p><strong>connector-id</strong></p></td>
<td><p>Nom unique du connecteur associé à l'événement SMTP.</p></td>
</tr>
<tr class="odd">
<td><p><strong>session-id</strong></p></td>
<td><p>GUID unique pour chaque session SMTP ; même GUID pour chaque événement associé à cette session SMTP.</p></td>
</tr>
<tr class="even">
<td><p><strong>sequence-number</strong></p></td>
<td><p>Compteur démarrant à 0 et incrémenté pour chaque événement dans la même session SMTP.</p></td>
</tr>
<tr class="odd">
<td><p><strong>local-endpoint</strong></p></td>
<td><p>Point de terminaison local d'une session SMTP. Il est constitué d'une adresse IP et d'un numéro de port TCP selon le format suivant : <em>&lt;adresse IP&gt;</em>:<em>&lt;port&gt;</em>.</p></td>
</tr>
<tr class="even">
<td><p><strong>remote-endpoint</strong></p></td>
<td><p>Point de terminaison distant d'une session SMTP. Il est constitué d'une adresse IP et d'un numéro de port TCP selon le format suivant : <em>&lt;adresse IP&gt;</em>:<em>&lt;port&gt;</em>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>event</strong></p></td>
<td><p>Caractère unique représentant l'événement de protocole. Les valeurs possibles pour l'événement sont les suivantes :</p>
<ul>
<li><p><strong>+</strong> Connexion</p></li>
<li><p><strong>-</strong>   Déconnexion</p></li>
<li><p><strong>&gt;</strong>   Envoi</p></li>
<li><p><strong>&lt;</strong>   Réception</p></li>
<li><p><strong>*</strong>   Informations</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>data</strong></p></td>
<td><p>Informations associées à l'événement SMTP.</p></td>
</tr>
<tr class="odd">
<td><p><strong>context</strong></p></td>
<td><p>Informations contextuelles supplémentaires pouvant être associées à l'événement SMTP.</p></td>
</tr>
</tbody>
</table>


Une conversation SMTP correspondant à l'envoi ou la réception d'un message électronique génère plusieurs événements SMTP. La survenue de ces événements SMTP entraîne l'écriture de plusieurs lignes dans le journal de protocole. Plusieurs conversations SMTP correspondant à l'envoi ou la réception de plusieurs messages électroniques peuvent se produire simultanément. Cela entraîne la création d'entrées de journal de protocole provenant de différentes conversations SMTP insérées. Vous pouvez utiliser les champs session-id et sequence-number pour trier les entrées de journal de protocole par conversation SMTP.

Retour au début

