---
title: 'Journalisation du protocole pour POP3 et IMAP4: Exchange 2013 Help'
TOCTitle: Journalisation du protocole pour POP3 et IMAP4
ms:assetid: 212ed3d5-0c98-4346-a860-1cfcac5d73c4
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dd335141(v=EXCHG.150)
ms:contentKeyID: 50555360
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Journalisation du protocole pour POP3 et IMAP4

 

_**Sapplique à :**Exchange Server 2013_

_**Dernière rubrique modifiée :**2015-03-09_

Vous pouvez utiliser la journalisation du protocole pour vérifier les connexions POP3 et IMAP4 dans votre environnement Exchange. Cette opération peut être utile si vous effectuez des dépannages relatifs aux performances POP3 ou IMAP4.

## Activation de l’enregistrement dans le journal de protocole POP3 et IMAP4

Vous pouvez activer, désactiver ou modifier l’enregistrement dans le journal de protocole à l’aide de l’environnement de ligne de commande Exchange Management Shell. Si vous activez la journalisation du protocole à l’aide de l’environnement de ligne de commande Exchange Management Shell, les paramètres de journalisation du protocole seront utilisés. Dans la plupart des cas, les paramètres par défaut sont suffisants.

En outre, vous pouvez activer, désactiver et modifier les options de la journalisation de protocole en modifiant les fichiers de configuration Microsoft.Exchange.Pop3.exe.config et Microsoft.Exchange.Imap4.exe.config situés sur votre serveur d’accès au client MicrosoftExchange Server 2013. Pour plus d’informations sur la gestion des paramètres de protocoles POP3 et IMAP4, consultez la rubrique [Configurer la journalisation du protocole pour POP3 et IMAP4](configure-protocol-logging-for-pop3-and-imap4-exchange-2013-help.md).

## Vérification du journal de protocole

Les fichiers journaux de protocole sont des fichiers texte contenant des données au format CSV (valeurs séparées par une virgule). Le journal de protocole stocke chaque événement de protocole sur une seule ligne. Les informations stockées sur chaque ligne sont organisées par champs. Ces champs sont séparés par des virgules. Le tableau suivant décrit les champs utilisés pour classer chaque événement de protocole.

### Champs utilisés pour classifier chaque événement de protocole

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
<td><p>date-heure</p></td>
<td><p>Date et heure de l’événement de protocole. La valeur a le format <em>yyyy-mm-ddhh:mm:ss.fffZ</em>, où <em>yyyy</em> = année, <em>mm</em> = mois, <em>dd</em> = jour, <em>hh</em> = heure, <em>mm</em> = minute, <em>ss</em> = seconde, <em>fff</em> = fractions de seconde et <em>Z</em> signifie Zulu. Zulu est une autre manière d’indiquer l’heure universelle coordonnée (UTC).</p></td>
</tr>
<tr class="even">
<td><p>id de connecteur</p></td>
<td><p>Ce champ n’est pas utilisé pour l’enregistrement dans le journal de protocole POP3 et IMAP4.</p></td>
</tr>
<tr class="odd">
<td><p>id de session</p></td>
<td><p>GUID qui identifie de façon unique la session SMTP associée à un événement de protocole.</p></td>
</tr>
<tr class="even">
<td><p>nombre de séquences</p></td>
<td><p>Compteur démarrant à 0 et incrémenté pour chaque événement dans la même session.</p></td>
</tr>
<tr class="odd">
<td><p>point final local</p></td>
<td><p>Point de terminaison local d’une session POP3 ou IMAP4. Ce dernier comprend une adresse IP et un numéro de port TCP, formatés comme suit : <em>&lt;Adresse IP&gt;</em> :<em>&lt;port&gt;</em>.</p></td>
</tr>
<tr class="even">
<td><p>point final distant</p></td>
<td><p>Point de terminaison distant d’une session POP3 ou IMAP4. Ce dernier comprend une adresse IP et un numéro de port TCP, formatés comme suit : <em>&lt;Adresse IP&gt;</em> :<em>&lt;port&gt;</em>.</p></td>
</tr>
<tr class="odd">
<td><p>événement</p></td>
<td><p>Caractère unique représentant l’événement de protocole. Les valeurs possibles pour l’événement sont les suivantes :</p>
<ul>
<li><p>+   Connexion</p></li>
<li><p>-   Déconnexion</p></li>
<li><p>&gt;   Envoi</p></li>
<li><p>&lt;   Réception</p></li>
<li><p>*   Informations</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>données</p></td>
<td><p>Informations sous forme de texte associées à l’événement POP3 ou IMAP4.</p></td>
</tr>
<tr class="odd">
<td><p>contexte</p></td>
<td><p>Ce champ n’est pas utilisé pour l’enregistrement dans le journal de protocole POP3 et IMAP4.</p></td>
</tr>
</tbody>
</table>

