---
title: 'Journalisation de l’agent anti-courrier indésirable: Exchange 2013 Help'
TOCTitle: Journalisation de l’agent anti-courrier indésirable
ms:assetid: dbd478d2-7993-4931-80db-5b2f7d4269bd
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb124795(v=EXCHG.150)
ms:contentKeyID: 50479371
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Journalisation de l’agent anti-courrier indésirable

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2015-03-09_

Les journaux de l'agent enregistrent les actions effectuées sur un message par des agents de blocage de courrier indésirable spécifiques dans Microsoft Exchange Server 2013. Seuls les agents suivants peuvent écrire des informations dans le journal de l'agent :

  - Agent de filtrage des connexions

  - Agent de filtrage du contenu

  - Agent d'application de règles de transport Edge

  - Agent de filtrage des destinataires

  - Agent de filtrage des expéditeurs

  - Agent d'ID de l'expéditeur

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>L'agent de filtrage des connexions et l'agent de règles Edge ne ​​sont pas disponibles sur les serveurs de boîtes aux lettres.</td>
</tr>
</tbody>
</table>


Les informations écrites dans le journal de l'Agent dépendent de l'Agent, de l'événement SMTP et de l'action réalisée sur le message.

La cmdlet **Set-TransportService** de l'environnement de ligne de commande Exchange Management Shell vous permet d'exécuter toutes les tâches de configuration du journal de l'agent. Les options suivantes peuvent être sélectionnées pour les journaux de l'agent :

  - Activer ou désactiver la journalisation de l'agent. Par défaut, le suivi des messages est activé.

  - Spécifier l'emplacement des fichiers journaux de l'agent. La valeur par défaut est %ExchangeInstallPath%TransportRoles\\Logs\\Hub\\AgentLog.

  - Spécifier la taille maximale de chaque fichier journal de l'agent. La taille par défaut est 10 mégaoctets (Mo).

  - Spécifier la taille maximale du répertoire contenant les fichiers journaux de l'agent. La taille par défaut est 250 Mo.

  - Spécifier l'âge maximal des fichiers journaux de l'agent. L'âge par défaut est 7 jours.

Exchange utilise l'enregistrement circulaire pour limiter le nombre de journaux de l'agent en fonction de la taille et de l'âge du fichier afin de mieux gérer l'espace disque utilisé par les fichiers journaux.

**Contenu de cette rubrique**

Vue d'ensemble des agents de transport

Structure des fichiers journaux de l'agent

Informations écrites dans le journal de l'agent

Rechercher les journaux de l'agent

## Vue d'ensemble des agents de transport

Les agents peuvent uniquement agir sur les messages à certains points dans la séquence de commandes SMTP utilisée pour transporter les messages via le service de transport sur un serveur de boîtes aux lettres ou un serveur de transport Edge. Ces points d'accès dans la séquence de commande SMTP sont appelés *événements SMTP*. Chaque agent dispose d'une valeur prioritaire pouvant lui être affectée. Toutefois, les événements SMTP doivent toujours se produire selon un ordre établi. Par conséquent, la priorité de l'Agent dépend de l'événement SMTP. Si deux agents peuvent agir sur un message lors du même événement SMTP, l'Agent disposant de la priorité la plus élevée agit d'abord sur le message.

Le tableau suivant répertorie les événements SMTP dans leur ordre d'apparition et les agents qui écrivent des informations dans le journal de l'Agent selon un ordre de priorité décroissant pour chaque événement SMTP.

### Événements SMTP dans leur ordre d'apparition et agents écrivant des informations dans le journal de l'Agent selon l'ordre de priorité pour chaque événement SMTP

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Événement SMTP</th>
<th>Agent</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>OnConnect</strong></p></td>
<td><p>Agent de filtrage des connexions</p></td>
</tr>
<tr class="even">
<td><p><strong>OnMailCommand</strong></p></td>
<td><p>Agent de filtrage des connexions</p>
<p>Agent de filtrage des expéditeurs</p></td>
</tr>
<tr class="odd">
<td><p><strong>OnRcptCommand</strong></p></td>
<td><p>Agent de filtrage des connexions</p>
<p>Agent de filtrage des destinataires</p></td>
</tr>
<tr class="even">
<td><p><strong>OnEndOfHeaders</strong></p></td>
<td><p>Agent de filtrage des connexions</p>
<p>Agent d'ID de l'expéditeur</p>
<p>Agent de filtrage des expéditeurs</p></td>
</tr>
<tr class="odd">
<td><p><strong>OnEndOfData</strong></p></td>
<td><p>Agent d'application de règles de transport Edge</p>
<p>Agent de filtrage du contenu</p></td>
</tr>
</tbody>
</table>


<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>L'agent de filtrage des connexions et l'agent de règles Edge ne ​​sont pas disponibles sur les serveurs de boîtes aux lettres.</td>
</tr>
</tbody>
</table>


Pour plus d'informations sur les agents, les événements SMTP et la priorité de l'agent, consultez la rubrique [Agents de transport](transport-agents-exchange-2013-help.md).

Retour au début

## Structure des fichiers journaux de l'agent

Les journaux de l'agent résident dans %ExchangeInstallPath%TransportRoles\\Logs\\Hub\\AgentLog.

La convention d'appellation pour les fichiers journaux de l'Agent est AGENTLOG*aaaammjj-nnnn*.log. Les espaces réservés correspondent aux informations suivantes :

  - L'espace réservé *aaaammjj* est la date au format UTC (temps universel coordonné) à laquelle le fichier journal a été créé. Dans l'espace réservé, *aaaa* = année, *mm* = mois et *jj* = jour.

  - L'espace réservé *nnnn* est un numéro d'instance qui commence à la valeur 1 pour chaque jour.

Les informations sont consignées dans le fichier journal jusqu'à ce que la taille du fichier atteigne la valeur maximale spécifiée ; un nouveau fichier journal avec un numéro d'instance incrémenté est alors ouvert. Ce processus est répété au cours de la journée. L'enregistrement circulaire supprime les fichiers journaux les plus anciens lorsque le répertoire des journaux de l'agent atteint la taille maximale spécifiée ou lorsqu'un fichier journal atteint l'âge maximal spécifié.

Les fichiers journaux de l'Agent sont des fichiers texte contenant des données au format CSV (valeurs séparées par des virgules). Chaque fichier journal de l'Agent comporte un en-tête avec les informations suivantes :

  - **\#Software**   Nom du logiciel ayant créé le fichier journal de l'Agent. En règle générale, la valeur est Microsoft Exchange Server.

  - **\#Version**   Numéro de version du logiciel ayant créé le fichier journal de l'Agent. La valeur actuelle est 15.0.0.0.

  - **\#Log-Type**   Type de journal (la valeur est « Agent Log »).

  - **\#Date**   Date-heure, au format de temps universel coordonné, de création du fichier journal. La date-heure UTC est représentée au format de date-heure ISO 8601 : yyyy-mm-dd*yyyy-mm-dd*Thh:mm:ss.fff*hh:mm:ss.fff*Z, où yyyyy*yyyy* = année, mm*mm* = mois, dd*dd* = jour, T indique le début du composant temps, hh*hh* = heure, mm*mm* = minute, ss*ss* = seconde, fff*fff* = fractions de seconde et Z correspond à Zulu (qui est une autre manière de désigner le temps universel).

  - **\#Fields**   Noms de champ séparés par des virgules utilisés dans les fichiers journaux de l'Agent.

Retour au début

## Informations écrites dans le journal de l'agent

Le journal de l'Agent stocke chaque transaction d'agent sur une seule ligne dans le journal. Les informations stockées sur chaque ligne sont organisées par champs. Ces champs sont séparés par des virgules. Me nom du champ est généralement suffisamment descriptif pour déterminer le type d'information qu'il contient. Toutefois, certains champs peuvent être vides. Ou le type d'informations stockées dans le champ peut évoluer en fonction de l'Agent ou de l'action réalisée par l'Agent sur le message. Le tableau suivant décrit les champs utilisés pour classer chaque transaction d'agent.

### Champs utilisés pour classer chaque transaction d'agent

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
<td><p><strong>Timestamp</strong></p></td>
<td><p>Date et heure, au format UTC, de l'événement de l'agent. La date-heure UTC est représentée au format de date-heure ISO 8601 : yyyy-mm-dd<em>yyyy-mm-dd</em>Thh:mm:ss.fff<em>hh:mm:ss.fff</em>Z, où yyyyy<em>yyyy</em> = année, mm<em>mm</em> = mois, dd<em>dd</em> = jour, T indique le début du composant temps, hh<em>hh</em> = heure, mm<em>mm</em> = minute, ss<em>ss</em> = seconde, fff<em>fff</em> = fractions de seconde et Z correspond à Zulu (qui est une autre manière de désigner le temps universel).</p></td>
</tr>
<tr class="even">
<td><p><strong>SessionId</strong></p></td>
<td><p>Identificateur unique de session SMTP. Cet identificateur est représenté sous la forme d'un nombre hexadécimal à 16 chiffres.</p></td>
</tr>
<tr class="odd">
<td><p><strong>LocalEndpoint</strong></p></td>
<td><p>Adresse IP locale et numéro de port acceptés par le message. Les sessions SMTP utilisent généralement le port 25.</p></td>
</tr>
<tr class="even">
<td><p><strong>RemoteEndpoint</strong></p></td>
<td><p>Adresse IP et numéro de port du serveur SMTP précédent qui s'est connecté à ce serveur pour remettre les messages. Lorsque la messagerie Internet passe par un serveur de transport Edge dans le réseau de périmètre, la valeur <strong>RemoteEndpoint</strong> du journal de l'agent sur le serveur de boîtes aux lettres est l'adresse IP du serveur de transport Edge. Même si la transmission du message s'effectue via le protocole SMTP, le numéro de port utilisé par le serveur d'envoi est un numéro aléatoire supérieur à 1 024.</p></td>
</tr>
<tr class="odd">
<td><p><strong>EnteredOrgFromIP</strong></p></td>
<td><p>Adresse IP du serveur SMTP distant qui s'est connecté en premier à l'organisation Exchange pour remettre le message. Sur un serveur de transport Edge, les valeurs de paramètres <strong>RemoteEndpoint</strong> et <strong>EnteredOrgFromIP</strong> sont les mêmes. Les agents de blocage du courrier indésirable utilisent l'adresse IP de <strong>EnteredOrgFromIP</strong> pour examiner un message.</p></td>
</tr>
<tr class="even">
<td><p><strong>MessageId</strong></p></td>
<td><p>Valeur du champ d'en-tête <code>MessageID</code>. Si ce champ n'est pas renseigné, le serveur de transport Exchange attribue une valeur arbitraire, mais uniquement si le message est accepté. Une fois attribuée, la valeur de <code>MessageID</code> est constante tout au long de la durée de vie du message.</p></td>
</tr>
<tr class="odd">
<td><p><strong>P1FromAddress</strong></p></td>
<td><p>Adresse de messagerie de l'expéditeur spécifiée par <code>MAIL FROM</code> dans l'enveloppe de message. Cette valeur est utilisée pour transporter le message entre les serveurs de messagerie SMTP. Cette valeur sert de comparaison à la valeur <strong>P2FromAddresses</strong> pour déterminer si l'adresse d'expéditeur présente dans l'en-tête de message est falsifiée.</p></td>
</tr>
<tr class="even">
<td><p><strong>P2FromAddresses</strong></p></td>
<td><p>Adresse de messagerie de l'expéditeur spécifiée dans le champ d'en-tête <code>From</code> ou dans le champ d'en-tête <code>Sender</code> de l'en-tête de message.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Recipient</strong></p></td>
<td><p>Adresse de messagerie des destinataires. Bien que le message d'origine puisse contenir plusieurs destinataires, un seul destinataire est affiché par ligne dans le journal de l'Agent.</p></td>
</tr>
<tr class="even">
<td><p><strong>NumRecipients</strong></p></td>
<td><p>Nombre total de destinataires dans le message d'origine.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Agent</strong></p></td>
<td><p>Nom de l'agent qui a effectué l'action. Les valeurs possibles sont les suivantes :</p>
<ul>
<li><p>Agent de filtrage du contenu</p></li>
<li><p>Agent de filtrage des destinataires</p></li>
<li><p>Agent de filtrage des expéditeurs</p></li>
<li><p>Agent d'ID de l'expéditeur</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>Event</strong></p></td>
<td><p>Événement SMTP où l'action a été effectuée par l'Agent. La valeur de <strong>Event</strong> dépend de l'Agent. Les événements SMTP disponibles pour chaque agent sont présentés dans le premier tableau, plus haut dans cette rubrique. Les valeurs possibles pour <strong>Event</strong> sont les suivantes :</p>
<ul>
<li><p>OnConnect</p></li>
<li><p>OnEndOfHeaders</p></li>
<li><p>OnEndOfData</p></li>
<li><p>OnMailCommand</p></li>
<li><p>OnRcptCommand</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p><strong>Action</strong></p></td>
<td><p>Action réalisée sur le message par l'Agent. Les valeurs possibles pour <strong>Action</strong> sont les suivantes :</p>
<ul>
<li><p>AcceptMessage</p></li>
<li><p>DeleteMessage</p></li>
<li><p>DeleteRecipients</p></li>
<li><p>Disconnect</p></li>
<li><p>QuarantineMessage</p></li>
<li><p>QuarantineRecipients</p></li>
<li><p>RejectAuthentication</p></li>
<li><p>RejectCommand</p></li>
<li><p>RejectConnection</p></li>
<li><p>RejectMessage</p></li>
<li><p>RejectRecipients</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>SmtpResponse</strong></p></td>
<td><p>Réponse SMTP optimisée comme définie dans RFC 2034.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Reason</strong></p></td>
<td><p>Raison de l'action prise en charge par l'Agent.</p></td>
</tr>
<tr class="even">
<td><p><strong>ReasonData</strong></p></td>
<td><p>Informations décrivant l'action prise en charge par l'Agent.</p></td>
</tr>
</tbody>
</table>


Retour au début

## Rechercher les journaux de l'agent

La cmdlet **Get-AgentLog** et le script **Get-AntiSpamFilteringReport.ps1** permettent de rechercher les journaux de l'agent.

Le script **Get-AntiSpamFilteringReport.ps1** se situe dans `%ExchangeInstallPath%Scripts`. Vous devez exécuter le script dans l'environnement de ligne de commande Exchange Management Shell à partir du dossier Scripts. Pour modifier votre emplacement dans l'environnement de ligne de commande Exchange Management Shell pour le dossier Scripts, exécutez la commande suivante :

    Cd $env:ExchangeInstallPath\Scripts

Pour exécuter le script dans le dossier Scripts, utilisez la syntaxe suivante :

    .\Get-AntiSpamFilteringReport.ps1 -report <ReportValue> [<OptionalParameters>]

Pour obtenir plus d'informations sur l'utilisation du script, exécutez la commande suivante :

    Get-Help -Detailed .\Get-AntiSpamFilteringReport.ps1

Retour au début

