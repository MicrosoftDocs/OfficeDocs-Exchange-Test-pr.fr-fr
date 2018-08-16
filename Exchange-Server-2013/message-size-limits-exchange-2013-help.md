---
title: 'Tailles limites des messages: Exchange 2013 Help'
TOCTitle: Tailles limites des messages
ms:assetid: b6a3840d-b821-4e53-877b-59c16be77206
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb124345(v=EXCHG.150)
ms:contentKeyID: 50479048
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Tailles limites des messages

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2015-08-20_

Vous pouvez appliquer des limites aux messages qui se déplacent dans l'organisation Microsoft Exchange Server 2013. Vous pouvez limiter la taille totale d'un message ou la taille des composants individuels d'un message, tels que l'en-tête du message, les pièces jointes au message et le nombre de destinataires. Vous pouvez appliquer des limites à toute l'organisation Exchange de manière globale, ou de façon spécifique pour un connecteur ou un objet utilisateur.

Au moment de définir les tailles limites des messages pour votre organisation Exchange, prenez en compte les questions suivantes :

  - Quelles tailles limites dois-je imposer à tous les messages entrants ?

  - Quelles tailles limites dois-je imposer à tous les messages sortants ?

  - Quel est le quota de boîte aux lettres pour mon organisation Exchange ?

  - En quoi les tailles limites des messages choisies affectent la taille du quota de boîte aux lettres ?

  - Y a-t-il des utilisateurs dans mon organisation Exchange qui doivent échanger des messages dépassant la taille autorisée indiquée ?

  - Ma topologie réseau Exchange inclut-elle d'autres systèmes de messagerie ou des divisions distinctes dotées de tailles limites de messages différentes ?

Cette rubrique contient des informations qui vous aideront à répondre à ces questions.

**Contenu de cette rubrique**

Types de tailles limites des messages

Portée des limites

Ordre de priorité des tailles limites des messages

Messages exemptés de tailles limites

## Types de tailles limites des messages

Voici les différentes catégories de tailles limites disponibles pour chaque message :

  - **Tailles limites d'en-tête de message**   Ces limites s'appliquent à la taille totale de tous les champs d'en-tête de message présents dans un message. Les tailles du corps de message ou des pièces jointes ne sont pas prises en compte. Dans la mesure où les champs d'en-tête sont en texte brut, la taille de l'en-tête est déterminée par le nombre de caractères dans chaque champ d'en-tête et le nombre total de champs d'en-tête. Chaque caractère du texte correspond à un octet.
    
    > [!NOTE]
    > Certains pare-feu ou serveurs proxy tiers appliquent leurs propres limites de taille d'en-tête de message. Ces pare-feu ou serveurs proxy tiers peuvent avoir des difficultés à traiter des messages contenant des noms de fichier de pièce jointe d'une longueur supérieure à 50 caractères ou contenant des caractères autres que US-ASCII.


  - **Tailles limites des messages**   Ces limites s'appliquent à la taille totale d'un message, ce qui inclut l'en-tête du message, le corps du message et les pièces jointes. Les tailles limites des messages peuvent être imposées sur les messages entrants ou sortants. Pour le flux de messagerie interne, Exchange utilise l'en-tête de message `X-MS-Exchange-Organization-OriginalSize:` personnalisé pour enregistrer la taille d'origine du message au moment où celui-ci entre dans l'organisation Exchange. Chaque fois qu'un message est vérifié par rapport aux tailles limites spécifiées, la valeur la plus faible de l'en-tête de la taille de message actuelle ou de la taille de message d'origine est utilisée. La taille du message peut varier en raison de la conversion de contenu, du codage et du traitement par l'agent.

  - **Tailles limites des pièces jointes**   Ces limites s'appliquent à la taille maximale autorisée d'une seule pièce jointe dans un message. Le message peut contenir de nombreuses pièces jointes qui augmentent considérablement la taille totale du message. Toutefois, la taille limite des pièces jointes s'applique unique à la taille d'une seule pièce jointe.

  - **Limites des destinataires**   Ces limites s'appliquent au nombre total de destinataires d'un message. Lors de la rédaction d'un message, les destinataires apparaissent dans les champs d'en-tête `To:`, `Cc:` et `Bcc:`. Lors du dépôt du message pour remise, les destinataires du message sont convertis en entrées `RCPT TO:` dans l'enveloppe de message. Un groupe de distribution est considéré comme un destinataire unique lors du dépôt du message.

Retour au début

## Portée des limites

Voici les différentes catégories de portée des limites pour chaque message :

  - **Limites de l'organisation**   Ces limites s'appliquent à tous les serveurs de boîtes aux lettres Exchange 2013 et de transport Hub Exchange 2010 et Exchange 2007 existants dans l'organisation. Si un serveur de transport Edge est installé dans le réseau de périmètre, les limites indiquées s'appliquent au serveur spécifique.

  - **Limites du connecteur**   Ces limites s'appliquent aux messages qui utilisent le connecteur d'envoi, de réception, d'agent de remise ou étranger spécifié pour la remise des messages. Les connecteurs d'envoi sont définis dans le service de transport sur les serveurs de boîtes aux lettres et de transport Edge. Les connecteurs de réception sont définis dans le service de transport des serveurs de boîtes aux lettres, dans le service de transport frontal des serveurs d'accès au client, et sur les serveurs de transport Edge.

  - **Liens de site Active Directory**   Le service de transport des serveurs de boîtes aux lettres utilise des sites Active Directory et les coûts qui sont attribués aux liens de site IP Active Directory sont l'un des facteurs à prendre en compte pour déterminer le chemin de routage le moins cher entre des serveurs de boîtes aux lettres au sein de l'organisation. Vous pouvez attribuer des tailles limites des messages aux liens de site Active Directory de votre organisation.

  - **Limites du serveur**   Ces limites s'appliquent à un serveur de boîtes aux lettres ou à un serveur de transport Edge spécifique. Vous pouvez paramétrer les limites de message indiquées indépendamment sur chaque serveur de boîtes aux lettres ou de transport Edge.
    
    Si vous utilisez Outlook Web App, le paramètre de taille limite maximale de la demande HTTP sur les serveurs d'accès au client détermine également la taille des messages que les utilisateurs d'Outlook Web App peuvent envoyer.

  - **Limites de l'utilisateur**   Ces limites s'appliquent à un objet utilisateur spécifique, tel qu'une boîte aux lettres, un contact, un groupe de distribution ou un dossier public.

Les tableaux suivants présentent les limites des messages, dont des informations sur la configuration des limites dans l'environnement de ligne de commande Exchange Management Shell ou le Centre d'administration Exchange (CAE).

### Limites de l'organisation

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Taille limite</th>
<th>Valeur par défaut</th>
<th>Configuration Shell</th>
<th>Configuration du CAE</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Taille maximale des messages reçus</p></td>
<td><p>10 Mo</p></td>
<td><p>Cmdlet : <strong>Set-TransportConfig</strong></p>
<p>Paramètre : <em>MaxReceiveSize</em></p></td>
<td><p><strong>Flux de messagerie</strong>&gt;<strong>Connecteurs de réception</strong>&gt;<strong>Plus d'options</strong><img src="images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif" title="Icône Options supplémentaires" alt="Icône Options supplémentaires" />&gt;<strong>Paramètres de transport de l'organisation</strong>&gt; onglet <strong>Limites</strong>&gt;<strong>Taille maximale des messages reçus</strong></p></td>
</tr>
<tr class="even">
<td><p>Taille maximale des messages envoyés</p></td>
<td><p>10 Mo</p></td>
<td><p>Cmdlet : <strong>Set-TransportConfig</strong></p>
<p>Paramètre : <em>MaxSendSize</em></p></td>
<td><p><strong>Flux de messagerie</strong>&gt;<strong>Connecteurs de réception</strong>&gt;<strong>Plus d'options</strong><img src="images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif" title="Icône Options supplémentaires" alt="Icône Options supplémentaires" />&gt;<strong>Paramètres de transport de l'organisation</strong>&gt; onglet <strong>Limites</strong>&gt;<strong>Taille maximale des messages envoyés</strong></p></td>
</tr>
<tr class="odd">
<td><p>Nombre maximal de destinataires par message</p>


</td>
<td><p>5000</p></td>
<td><p>Cmdlet : <strong>Set-TransportConfig</strong></p>
<p>Paramètre : <em>MaxRecipientEnvelopeLimit</em></p></td>
<td><p><strong>Flux de messagerie</strong>&gt;<strong>Connecteurs de réception</strong>&gt;<strong>Plus d'options</strong><img src="images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif" title="Icône Options supplémentaires" alt="Icône Options supplémentaires" />&gt;<strong>Paramètres de transport de l'organisation</strong>&gt; onglet <strong>Limites</strong>&gt;<strong>Nombre maximal de destinataires</strong></p></td>
</tr>
<tr class="even">
<td><p>Taille maximale des pièces jointes selon les règles de transport applicables à tous les serveurs de boîtes aux lettres de l'organisation</p></td>
<td><p>Non configurée</p></td>
<td><p>Cmdlets : <strong>New-TransportRule</strong>, <strong>Set-TransportRule</strong></p>
<p>Paramètre : <em>AttachmentSizeOver</em></p></td>
<td><p><strong>Flux du courrier</strong>&gt;<strong>Règles</strong>&gt;<strong>Ajouter</strong><img src="images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif" title="Icône Ajouter" alt="Icône Ajouter" /> ou <strong>Modifier</strong><img src="images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif" title="Icône Modifier" alt="Icône Modifier" />.</p>
<p>Utilisez le prédicat <strong>Appliquer cette règle si</strong>&gt;<strong>Toute pièce jointe</strong>&gt;<strong>présente une taille supérieure ou égale à</strong></p>
<p>Utilisez le prédicat <strong>Appliquer cette règle si</strong>&gt;<strong>La taille du message</strong>&gt;<strong>est supérieure ou égale à</strong></p></td>
</tr>
<tr class="odd">
<td><p>Taille maximale des messages selon les règles de transport applicables à tous les serveurs de boîtes aux lettres de l'organisation</p></td>
<td><p></p></td>
<td><p>Cmdlets : <strong>New-TransportRule</strong>, <strong>Set-TransportRule</strong></p>
<p>Paramètre : <em>MessageSizeOver</em></p></td>
<td><p><strong>Flux du courrier</strong>&gt;<strong>Règles</strong>&gt;<strong>Ajouter</strong><img src="images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif" title="Icône Ajouter" alt="Icône Ajouter" /> ou <strong>Modifier</strong><img src="images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif" title="Icône Modifier" alt="Icône Modifier" />.</p>
<p>Utilisez le prédicat <strong>Appliquer cette règle si</strong>&gt;<strong>La taille du message</strong>&gt;<strong>est supérieure ou égale à</strong></p></td>
</tr>
</tbody>
</table>


Retour au début

### Limites du connecteur

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Taille limite</th>
<th>Valeur par défaut</th>
<th>Configuration Shell</th>
<th>Configuration du CAE</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Taille maximale d'en-tête via un connecteur de réception</p></td>
<td><p>128 Ko</p></td>
<td><p>Cmdlets : <strong>New-ReceiveConnector</strong>, <strong>Set-ReceiveConnector</strong></p>
<p>Paramètre : <em>MaxHeaderSize</em></p></td>
<td><p>N/A</p>
<p></p></td>
</tr>
<tr class="even">
<td><p>Taille maximale des messages via un connecteur de réception</p>

> [!NOTE]  
> La taille réelle du message peut être inférieure en raison de l'encodage et de la conversion du contenu du message.

</td>
<td><p><strong>Service de transport sur les serveurs de boîtes aux lettres</strong></p>
<p>35 Mo pour les connecteurs de réception de proxy client et par défaut</p>
<p><strong>Service de transport frontal sur un serveur d'accès au client</strong></p>
<p>36 Mo pour les connecteurs de réception frontaux de proxy sortants et frontaux par défaut.</p>
<p>35 Mo pour le connecteur de réception frontal de client.</p></td>
<td><p>Cmdlets : <strong>New-ReceiveConnector</strong>, <strong>Set-ReceiveConnector</strong></p>
<p>Paramètre : <em>MaxMessageSize</em></p></td>
<td><p><strong>Flux de messagerie</strong>&gt;<strong>Connecteurs de réception</strong>&gt;<strong>Modifier</strong><img src="images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif" title="Icône Modifier" alt="Icône Modifier" />&gt; onglet <strong>Général</strong>&gt;<strong>Taille maximale des messages reçus</strong></p></td>
</tr>
<tr class="odd">
<td><p>Nombre maximal de destinataires par message via un connecteur de réception</p></td>
<td><p><strong>Service de transport sur les serveurs de boîtes aux lettres</strong></p>
<p>5 000 pour le connecteur de réception par défaut</p>
<p>200 pour le connecteur de réception de proxy client</p>
<p><strong>Service de transport frontal sur un serveur d'accès au client</strong></p>
<p>200 pour les connecteurs de réception frontaux par défaut, frontaux de client et frontaux de proxy.</p>

> [!NOTE]  
> Si le nombre de destinataires est dépassé pour un expéditeur anonyme, le message est accepté pour les 200 premiers destinataires. La plupart des serveurs de messagerie SMTP détectent qu'une limite des destinataires est appliquée. Le serveur de messagerie SMTP continue à renvoyer le message par groupes de 200 destinataires jusqu'à ce qu'il ait été remis à tous les destinataires.

</td>
<td><p>Cmdlets : <strong>New-ReceiveConnector</strong>, <strong>Set-ReceiveConnector</strong></p>
<p>Paramètre : <em>MaxRecipientsPerMessage</em></p></td>
<td><p>N/A</p></td>
</tr>
<tr class="even">
<td><p>Taille maximale des messages via un connecteur d'envoi</p></td>
<td><p>10 Mo</p></td>
<td><p>Cmdlets : <strong>New-SendConnector</strong>, <strong>Set-SendConnector</strong></p>
<p>Paramètre : <em>MaxMessageSize</em></p></td>
<td><p><strong>Flux de messagerie</strong>&gt;<strong>Connecteurs d'envoi</strong>&gt;<strong>Modifier</strong><img src="images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif" title="Icône Modifier" alt="Icône Modifier" />&gt; onglet <strong>Général</strong>&gt;<strong>Taille maximale des messages envoyés</strong></p>
<p></p></td>
</tr>
<tr class="odd">
<td><p>Taille maximale des messages via un lien de site Active Directory</p></td>
<td><p>Illimité</p></td>
<td><p>Cmdlet : <strong>Set-AdSiteLink</strong></p>
<p>Paramètre : <em>MaxMessageSize</em></p></td>
<td><p>N/A</p></td>
</tr>
<tr class="even">
<td><p>Taille maximale des messages via un connecteur d'agent de remise</p></td>
<td><p>Illimité</p></td>
<td><p>Cmdlets : <strong>New-DeliveryAgentConnector</strong>, <strong>Set-DeliveryAgentConnector</strong></p>
<p>Paramètre : <em>MaxMessageSize</em></p></td>
<td><p>N/A</p></td>
</tr>
<tr class="odd">
<td><p>Taille maximale des messages via un connecteur étranger</p></td>
<td><p>Illimité</p></td>
<td><p><strong>Cmdlet : Set-ForeignConnector</strong> Paramètre : <em>MaxMessageSize</em></p></td>
<td><p>N/A</p></td>
</tr>
</tbody>
</table>


Retour au début

### Limites du serveur

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Taille limite</th>
<th>Valeur par défaut</th>
<th>Configuration Shell</th>
<th>Configuration du CAE</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Taille maximale d'en-tête des messages du répertoire de collecte</p></td>
<td><p>64 Ko</p></td>
<td><p>Cmdlet : <strong>Set-TransportService</strong></p>
<p>Paramètre : <em>PickupDirectoryMaxHeaderSize</em></p></td>
<td><p>N/A</p></td>
</tr>
<tr class="even">
<td><p>Nombre maximal de destinataires pour chaque message du répertoire de collecte</p></td>
<td><p>100</p></td>
<td><p>Cmdlet : <strong>Set-TransportService</strong></p>
<p>Paramètre : <em>PickupDirectoryMaxRecipientsPerMessage</em></p></td>
<td><p>N/A</p></td>
</tr>
<tr class="odd">
<td><p>Limites de taille de messages spécifique au client pour Outlook Web App, Exchange ActiveSync et les clients services web Exchange</p></td>
<td><p>Outlook Web App   35 Mo</p>
<p>Exchange ActiveSync   10 Mo</p>
<p>Services web Exchange   64 Mo</p>

> [!NOTE]  
> Ces valeurs sont environ 33 % supérieures à la taille maximale réelle des messages, en raison du traitement associé au codage Base64.

</td>
<td><p>Vous configurez ces valeurs dans le fichier de configuration d'application XML web.config approprié sur les serveurs d'accès aux client. Pour plus d'informations, consultez la rubrique <a href="configure-client-specific-message-size-limits-exchange-2013-help.md">Configuration des limites de taille de message propres au client</a>.</p></td>
<td><p>N/A</p></td>
</tr>
</tbody>
</table>


Retour au début

### Limites de l'utilisateur

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Taille limite</th>
<th>Valeur par défaut</th>
<th>Configuration Shell</th>
<th>Configuration du CAE</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Taille maximale des messages pouvant être envoyés par ce destinataire</p></td>
<td><p>Illimité</p></td>
<td><p>Cmdlets :</p>
<p><strong>Set-DistributionGroup</strong></p>
<p><strong>Set-DynamicDistributionGroup</strong></p>
<p><strong>Set-Mailbox</strong></p>
<p><strong>Set-MailContact</strong></p>
<p><strong>Set-MailUser</strong></p>
<p><strong>Set-MailPublicFolder</strong></p>
<p><strong>Set-RemoteMailbox</strong></p>
<p>Paramètre : <em>MaxSendSize</em></p></td>
<td><p>Pour les boîtes aux lettres :</p>
<p><strong>Destinataires</strong>&gt;<strong>Boîtes aux lettres</strong>&gt;<strong>Modifier</strong><img src="images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif" title="Icône Modifier" alt="Icône Modifier" />&gt;<strong>Fonctionnalités de boîte aux lettres</strong>&gt;<strong>Flux de messagerie</strong>&gt;<strong>Restrictions de taille des messages</strong>&gt;<strong>Afficher les détails</strong>&gt;<strong>Messages envoyés</strong></p>

> [!NOTE]    
> Ce paramètre n'est pas configurable avec le CAE pour d'autres types de destinataires.

</td>
</tr>
<tr class="even">
<td><p>Taille maximale des messages pouvant être envoyés à ce destinataire</p></td>
<td><p>Illimité</p>
<p>Stratégie d'approvisionnement de boîte aux lettres de site : 36 Mo</p></td>
<td><p>Cmdlets :</p>
<p><strong>Set-DistributionGroup</strong></p>
<p><strong>Set-DynamicDistributionGroup</strong></p>
<p><strong>Set-Mailbox</strong></p>
<p><strong>Set-MailContact</strong></p>
<p><strong>Set-MailUser</strong></p>
<p><strong>Set-MailPublicFolder</strong></p>
<p><strong>New-SiteMailboxProvisioningPolicy</strong></p>
<p><strong>Set-SiteMailboxProvisioningPolicy</strong></p>
<p>Paramètre : <em>MaxReceiveSize</em></p></td>
<td><p>Pour les boîtes aux lettres :</p>
<p><strong>Destinataires</strong>&gt;<strong>Boîtes aux lettres</strong>&gt;<strong>Modifier</strong><img src="images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif" title="Icône Modifier" alt="Icône Modifier" />&gt;<strong>Fonctionnalités de boîte aux lettres</strong>&gt;<strong>Flux de messagerie</strong>&gt;<strong>Restrictions de taille des messages</strong>&gt;<strong>Afficher les détails</strong>&gt;<strong>Messages reçus</strong></p>

> [!NOTE]  
> Ce paramètre n'est pas configurable avec le CAE pour d'autres types de destinataires.

</td>
</tr>
<tr class="odd">
<td><p>Nombre maximal de destinataires par message envoyé par ce destinataire</p></td>
<td><p>Illimité</p></td>
<td><p>Cmdlets :</p>
<p><strong>Set-Mailbox</strong>, <strong>Set-MailUser</strong></p>
<p>Paramètre : <em>RecipientLimits</em></p>
<p></p></td>
<td><p>N/A</p></td>
</tr>
</tbody>
</table>


Retour au début

## Ordre de priorité des tailles limites des messages

Vous pouvez définir différentes tailles limites de messages à différents niveaux de l'organisation Exchange. Lorsqu'un message circule dans votre infrastructure de transport, il peut être soumis à différentes restrictions de taille des messages. Nous vous conseillons de planifier les restrictions de taille des messages de façon à s'assurer que les messages qui se trouvent dans le pipeline de transport soient rejetés le plus tôt possible s'ils enfreignent les limites de taille des messages. De façon générale, il est préférable de définir des limites plus restrictives aux niveaux où les messages pénètrent dans votre infrastructure. Par exemple, les tailles limites des messages sur les connecteurs de réception qui reçoivent des messages d'Internet doivent être inférieures ou égales à celles que vous configurez pour votre organisation Exchange interne. Accepter et traiter un message provenant d'Internet, qui serait ensuite rejeté par le service de transport sur vos serveurs de boîtes aux lettres, serait un gaspillage des ressources système pour votre serveur Exchange. Assurez-vous que les limites de votre organisation, de vos serveurs et connecteurs sont configurées de façon à minimiser tout traitement inutile des messages.

Les limites de l'utilisateur constituent la seule exception à cette approche. Les limites de l'utilisateur sont prioritaires par rapport aux autres tailles limites des messages. Par conséquent, vous pouvez configurer un utilisateur de façon à dépasser les tailles limites des messages par défaut de votre organisation. Par exemple, vous pouvez autoriser un groupe spécifique de boîtes aux lettres utilisateur à envoyer des messages plus volumineux que le reste de l'organisation en configurant des limites d'envoi et de réception personnalisées pour ces boîtes aux lettres.

Les exceptions pour les limites pour les utilisateurs s'appliquent uniquement aux échanges de messages entre utilisateurs authentifiés. Si un message est envoyé à ou reçu par un destinataire sur Internet, les limites de l'organisation sont appliquées. Supposons, par exemple, que vous avez une restriction de 10 Mo de la taille des messages pour l'organisation, mais que vous avez configuré pour les utilisateurs de votre service une taille de 50 Mo pour envoyer ou recevoir des messages. Ces utilisateurs seront en mesure d’échanger des messages de taille importante avec d’autres, mais ils ne pourront pas recevoir des messages de taille importante provenant d’Internet car de tels messages sont envoyés par des expéditeurs non authentifiés.

Retour au début

## Messages exemptés de tailles limites

La liste suivante répertorie les types de messages générés par un serveur de boîtes aux lettres ou par un serveur de transport Edge et exemptés de toutes les tailles limites des messages :

  - messages système

  - message généré par l'agent

  - messages de notification d'état de remise

  - messages d'état de journal

  - messages mis en quarantaine

Toutefois, ces messages doivent toujours respecter la valeur de l'organisation concernant le nombre maximal de destinataires par message.

Retour au début

