---
title: 'Suivi des messages: Exchange 2013 Help'
TOCTitle: Suivi des messages
ms:assetid: bada2ea7-6d7c-4630-b7f1-67f56818f0ff
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb124375(v=EXCHG.150)
ms:contentKeyID: 51407231
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Suivi des messages

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2016-12-09_

Dans Microsoft Exchange Server 2013, le journal de suivi des messages est un enregistrement détaillé de toute l'activité de messagerie, regroupant les messages échangés avec le service de transport sur les serveurs de boîtes aux lettres, les boîtes aux lettres sur les serveurs de boîtes aux lettres et les serveurs de transport Edge. Les journaux de suivi des messages sont utiles pour les investigations sur les messages ainsi que pour l'analyse, les rapports et le dépannage du flux de messagerie.

Dans Exchange 2013, vous pouvez utiliser la cmdlet **Set-TransportService** ou **Set-MailboxServer** pour toutes les tâches de configuration du suivi des messages, car le serveur de boîtes aux lettres Exchange 2013 contient le service de transport et les boîtes aux lettres. Chacune de ces cmdlets permet d'apporter à la configuration du suivi des messages les changements suivants :

  - Activer ou désactiver le suivi des messages. Par défaut, le suivi des messages est activé.

  - Spécifier l'emplacement des journaux de suivi des messages.

  - Spécifier une taille maximale pour les fichiers journaux de suivi des messages. La valeur par défaut est 10 Mo.

  - Spécifier la taille maximale du répertoire contenant les fichiers journaux de suivi des messages : La valeur par défaut est de 1 000 MB.

  - Spécifier l'âge maximal des journaux de suivi des messages : La valeur par défaut est 30 jours.

  - Activer ou désactiver l'enregistrement de l'objet des messages dans les journaux de suivi des messages. Par défaut, cette option est activée.

> [!NOTE]
> Vous pouvez également utiliser le Centre d'administration Exchange (CAE) pour activer ou désactiver le suivi des messages, et spécifier l'emplacement des fichiers journaux de suivi des messages.


Par défaut, Exchange utilise un enregistrement circulaire pour limiter le nombre de journaux de suivi des messages en fonction de la taille et de l'âge des fichiers, afin de contrôler l'espace disque occupé par les fichiers journaux de suivi des messages.

**Contenu de cette rubrique**

Recherche dans le journal de suivi des messages

Structure des fichiers journaux de suivi des messages

Champs des fichiers journaux de suivi des messages

Types d'événements dans le journal de suivi des messages

Valeurs de source dans le journal de suivi des messages

Exemples d'entrées du journal de suivi des messages

Problèmes de sécurité pour le journal de suivi des messages

## Recherche dans le journal de suivi des messages

Les journaux de suivi des messages contiennent d'importantes quantités de données résultant du passage des messages par un serveur de boîtes aux lettres Exchange 2013. Pour effectuer des recherches dans les journaux de suivi des messages, plusieurs options sont possibles.

  - **Get-MessageTrackingLog**   Cette cmdlet permet aux administrateurs de rechercher dans les journaux de suivi des messages des informations sur les messages à l'aide d'un vaste éventail de critères de filtrage. Pour plus d'informations, consultez la rubrique [Recherche des journaux de suivi des messages](search-message-tracking-logs-exchange-2013-help.md).

  - **Rapports de remise pour les administrateurs**   Les administrateurs peuvent utiliser l'onglet **Rapports de remise** dans le CAE, ou les cmdlets sous-jacentes **Search-MessageTrackingReport** et **Get-MesageTrackingReport**, pour rechercher dans les journaux de suivi des messages des informations sur les messages échangés avec une boîte aux lettres spécifique au sein de l'organisation. Pour plus d'informations, consultez la rubrique [Rapports de remise pour les administrateurs](delivery-reports-for-administrators-exchange-2013-help.md).

  - **Rapports de remise pour les utilisateurs**   Les utilisateurs peuvent utiliser l'onglet **Rapports de remise** dans Outlook Web App pour rechercher dans les journaux de suivi des messages des informations sur les messages échangés avec leur propre boîte aux lettres. Pour plus d'informations, consultez la rubrique [Rapports de remise](https://go.microsoft.com/fwlink/?linkid=279920).

Retour au début

## Structure des fichiers journaux de suivi des messages

Par défaut, les fichiers journaux de suivi des messages se trouvent dans %ExchangeInstallPath%TransportRoles\\Logs\\MessageTracking.

La convention d'affectation de noms pour les fichiers journaux conservés dans le répertoire de suivi des messages est `MSGTRK`*aaaammjj-nnnn*`.log`, `MSGTRKMA`*aaaammjj-nnnn*`.log`, `MSGTRKMD`*aaaammjj-nnnn*`.log` et `MSGTRKMS`*aaaammjj-nnnn*`.log` . Les différents journaux sont utilisés par les services suivants :

  - **MSGTRK**   Ces journaux sont associés au service de transport.

  - **MSGTRKMA**   Ces journaux sont associés aux approbations et rejets appliqués par le transport modéré. Pour plus d'informations, consultez la rubrique [Gérer l’approbation des messages](manage-message-approval-exchange-2013-help.md).

  - **MSGTRKMD**   Ces journaux sont associés aux messages remis aux boîtes aux lettres par le service de remise de transport de boîte aux lettres.

  - **MSGTRKMS**   Ces journaux sont associés aux messages envoyés à partir de boîtes aux lettres par le service de dépôt de transport de boîte aux lettres.

Les espaces réservés dans les noms de fichiers journaux correspondent aux informations suivantes :

  - L'espace réservé *yyyymmdd* est la date au format UTC (temps universel coordonné) à laquelle le fichier journal a été créé. *yyyy* = année, *mm* = mois et *dd* = jour.

  - L'espace réservé *nnnn* est un numéro d'instance qui commence à la valeur 1 quotidiennement pour chaque préfixe de nom de fichier journal de suivi des messages.

Les informations sont écrites dans chaque fichier journal jusqu'à ce que la taille du fichier atteigne la valeur maximale spécifiée pour chaque fichier journal. Puis, un nouveau fichier journal avec un numéro d'instance incrémenté est alors ouvert. Ce processus est répété au cours de la journée. La fonctionnalité de rotation du fichier journal supprime les fichiers journaux les plus anciens quand l'une des conditions suivantes est vraie :

  - Un fichier journal a atteint l'âge maximal spécifié.

  - Le répertoire des journaux de suivi des messages a atteint la taille maximale spécifiée.
    
    > [!IMPORTANT]
    > La taille maximale du répertoire des journaux de suivi des messages est calculée comme la taille totale de tous les fichiers journaux dont le nom porte le même préfixe. Les fichiers ne répondant pas à cette convention de préfixe de sont pas comptabilisés dans le calcul de la taille totale du répertoire. La modification du nom d'anciens fichiers journaux ou la copie d'autres fichiers dans le répertoire des journaux de suivi des messages peut avoir pour effet que la taille du répertoire dépasse la taille maximale spécifiée.
    > Pour les serveurs de boîtes aux lettres Exchange 2013, la taille maximale du répertoire de suivi des messages est égale à trois fois la valeur spécifiée. Si les fichiers journaux de suivi des messages générés par les quatre différents services portent des préfixes de nom différents, la quantité de données et la fréquence d'écriture de ces dernières dans les fichiers journaux <strong>MSGTRKMA</strong> sont négligeables en comparaison des fichiers journaux portant les trois autres préfixes.


Les fichiers journaux de suivi des messages sont des fichiers texte contenant des données au format CSV (valeurs séparées par des virgules). Chaque fichier journal de suivi des messages comporte un en-tête avec les informations suivantes :

  - **\#Software:**    Nom du logiciel ayant créé le fichier journal de suivi des messages. Généralement, la valeur est Microsoft Exchange Server.

  - **\#Version:**    Numéro de version du logiciel ayant créé le fichier journal de suivi des messages. Actuellement, la valeur actuelle est 15.0.0.0.

  - **\#Log-Type:**    Type de journal, à savoir Journal de suivi des messages.

  - **\#Date:**    Date-heure UTC de création du fichier journal. La date-heure UTC est représentée au format de date-heure ISO 8601 : yyyy-mm-dd*yyyy-mm-dd*Thh:mm:ss.fff*hh:mm:ss.fff*Z, où yyyyy*yyyy* = année, mm*mm* = mois, dd*dd* = jour, T indique le début du composant temps, hh*hh* = heure, mm*mm* = minute, ss*ss* = seconde, fff*fff* = fractions de seconde et Z correspond à Zulu (qui est une autre manière de désigner le temps universel).

  - **\#Fields:**    Noms de champ séparés par des virgules, utilisés dans les fichiers journaux de suivi des messages.

Retour au début

## Champs des fichiers journaux de suivi des messages

Le journal de suivi des messages indique chaque événement de message sur une seule ligne dans le journal. Les informations d'événement de message sont organisées par champs, ces derniers étant séparés par des virgules. Le nom du champ est généralement suffisamment descriptif pour déterminer le type d'informations qu'il contient. Toutefois, certains champs peuvent être vides, ou les types d'informations qu'ils contiennent peuvent varier en fonction du type d'événement de message et du type de fichier journal de suivi des messages dans lequel l'événement a été enregistré. Le tableau suivant présente des descriptions générales des champs utilisés pour classifier chaque événement de suivi de message.


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
<td><p>Date et heure UTC de l'événement de suivi de message. La date-heure UTC est représentée au format de date-heure ISO 8601 : yyyy-mm-dd<em>yyyy-mm-dd</em>Thh:mm:ss.fff<em>hh:mm:ss.fff</em>Z, où yyyyy<em>yyyy</em> = année, mm<em>mm</em> = mois, dd<em>dd</em> = jour, T indique le début du composant temps, hh<em>hh</em> = heure, mm<em>mm</em> = minute, ss<em>ss</em> = seconde, fff<em>fff</em> = fractions de seconde et Z correspond à Zulu (qui est une autre manière de désigner le temps universel).</p></td>
</tr>
<tr class="even">
<td><p><strong>client-ip</strong></p></td>
<td><p>Adresse IPv4 ou IPv6 du serveur de messagerie ou du client de messagerie ayant déposé le message.</p></td>
</tr>
<tr class="odd">
<td><p><strong>client-hostname</strong></p></td>
<td><p>Nom d'hôte ou nom de domaine complet (FQDN) du serveur de messagerie ou du client de messagerie ayant déposé le message.</p></td>
</tr>
<tr class="even">
<td><p><strong>server-ip</strong></p></td>
<td><p>Adresse IPv4 ou IPv6 du serveur Exchange source ou de destination.</p></td>
</tr>
<tr class="odd">
<td><p><strong>server-hostname</strong></p></td>
<td><p>Nom d'hôte ou nom de domaine complet (FQDN) du serveur de destination.</p></td>
</tr>
<tr class="even">
<td><p><strong>source-context</strong></p></td>
<td><p>Informations supplémentaires associées au champ <strong>source</strong>. Par exemple, informations sur l'agent de transport.</p></td>
</tr>
<tr class="odd">
<td><p><strong>connector-id</strong></p></td>
<td><p>Nom du connecteur d'envoi ou de réception source ou de destination. Par exemple, <em>NomServeur</em>\<em>NomConnecteur</em> ou <em>NomConnecteur</em>.</p></td>
</tr>
<tr class="even">
<td><p><strong>source</strong></p></td>
<td><p>Composant de transport Exchange responsable de l'événement de suivi de message. Les valeurs pouvant figurer dans ce champ sont décrites dans la section Valeurs de source dans le journal de suivi des messages, plus loin dans cette rubrique.</p></td>
</tr>
<tr class="odd">
<td><p><strong>event-id</strong></p></td>
<td><p>Type de l'événement de message. Les types d'événements sont décrits dans la section Types d'événements dans le journal de suivi des messages, plus loin dans cette rubrique.</p></td>
</tr>
<tr class="even">
<td><p><strong>internal-message-id</strong></p></td>
<td><p>Identificateur de message attribué par le serveur Exchange traitant actuellement le message.</p>
<p>La valeur <strong>internal-message-id</strong> d'un message spécifique diffère dans le journal de suivi des messages de chaque serveur Exchange impliqué dans la transmission du message. Voici un exemple de valeur : <code>73014444033</code>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>message-id</strong></p></td>
<td><p>Valeur du champ d'en-tête <strong>Message-Id:</strong> figurant dans l'en-tête du message. Si le champ d'en-tête <strong>Message-Id:</strong> est vide ou inexistant, une valeur arbitraire est attribuée. Cette valeur est constante pendant toute la durée de vie du message. Pour les messages créés dans Exchange, la valeur est au format <code>&lt;GUID@ServerFQDN&gt;</code>, et inclut les crochets pointus (<code>&lt; &gt;</code>). Par exemple, <code>&lt;4867a3d78a50438bad95c0f6d072fca5@mailbox01.contoso.com&gt;</code>. D'autres systèmes de messagerie peuvent utiliser une syntaxe et des valeurs différentes.</p></td>
</tr>
<tr class="even">
<td><p><strong>network-message-id</strong></p></td>
<td><p>Valeur unique d'ID de message qui persiste dans les copies du message éventuellement créées suite à une bifurcation ou à une expansion du groupe de distribution. Voici un exemple de valeur : <code>1341ac7b13fb42ab4d4408cf7f55890f</code>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>recipient-address</strong></p></td>
<td><p>Adresse de messagerie des destinataires du message. Les adresses de messagerie multiples sont séparées par des points-virgules (;).</p></td>
</tr>
<tr class="even">
<td><p><strong>recipient-status</strong></p></td>
<td><p>Ce champ contient l'état de destinataire de tous les destinataires séparés par des points-virgules (;). Les valeurs d'état des destinataires sont présentées dans le même ordre que les valeurs du champ <strong>recipient-address</strong>. Les valeurs d'état sont, par exemple, <code>250 2.1.5 Recipient OK</code> ou <code>550 4.4.7 QUEUE.Expired;&lt;ErrorText&gt;</code>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>total-bytes</strong></p></td>
<td><p>Taille du message qui inclut des pièces jointes, en octets.</p></td>
</tr>
<tr class="even">
<td><p><strong>recipient-count</strong></p></td>
<td><p>Nombre de destinataires du message.</p></td>
</tr>
<tr class="odd">
<td><p><strong>related-recipient-address</strong></p></td>
<td><p>Ce champ est utilisé avec des événements <strong>EXPAND</strong>, <strong>REDIRECT</strong> et <strong>RESOLVE</strong> pour afficher d'autres adresses de messagerie de destinataires associées au message.</p></td>
</tr>
<tr class="even">
<td><p><strong>reference</strong></p></td>
<td><p>Ce champ contient des informations supplémentaires pour des types d'événements spécifiques. Par exemple :</p>
<p><strong>DSN</strong>   Contient le lien de rapport, qui est la valeur <strong>Message-Id</strong> de la notification d'état de remise (DSN) associée éventuellement générée suite à cet événement. S'il s'agit d'un message DSN, le champ <strong>Reference</strong> contient la valeur <strong>Message-Id</strong> du message d'origine pour lequel cette DSN a été générée.</p>
<p><strong>EXPAND</strong>   Le champ Référence contient la valeur <strong>related-recipient-address</strong> des messages associés.</p>
<p><strong>RECEIVE</strong>   Le champ Référence peut contenir la valeur <strong>Message-Id</strong> du message associé si ce dernier a été généré par d'autres processus tels qu'une journalisation ou des règles de boîte de réception.</p>
<p><strong>SEND</strong>   Le champ Référence contient la valeur <strong>Internal-Message-Id</strong> d'un message DSN.</p>
<p><strong>THROTTLE</strong>   Le champ Référence contient le motif de limitation du message.</p>
<p><strong>TRANSFER</strong>   Le champ Reference contient la valeur Internal-Message-Id du message en cours de transfert.</p>
<p>Pour les messages générés par des règles de boîte de réception, le champ <strong>Référence</strong> contient la valeur <strong>Internal-Message-Id</strong> du message entrant suite auquel la règle de boîte de réception a généré le message sortant.</p>
<p>Pour les autres types d'événements, le champ <strong>Référence</strong> peut contenir la valeur <strong>Internal-Message-Id</strong> pour des messages ayant fait l'objet d'une bifurcation.</p>
<p>Pour tous les autres types d'événements, le champ <strong>Référence</strong> est généralement vide.</p></td>
</tr>
<tr class="odd">
<td><p><strong>message-subject</strong></p></td>
<td><p>Objet du message trouvé dans le champ d'en-tête <code>Subject:</code>. Le suivi des objets de messages est contrôlé par le paramètre <em>MessageTrackingLogSubjectLoggingEnabled</em> pour la cmdlet <strong>Set-TransportService</strong> ou <strong>Set-MailboxServer</strong>. Par défaut, le suivi de l'objet des messages est activé.</p></td>
</tr>
<tr class="even">
<td><p><strong>sender-address</strong></p></td>
<td><p>Adresse de messagerie spécifiée dans le champ d'en-tête <code>Sender:</code> ou <code>From:</code> si <code>Sender:</code> n'est pas présent.</p></td>
</tr>
<tr class="odd">
<td><p><strong>return-path</strong></p></td>
<td><p>Adresse de messagerie de retour spécifiée par <code>MAIL FROM:</code> dans l'enveloppe de message. Bien que ce champ ne soit jamais vide, il peut contenir une valeur d'adresse d'expéditeur nulle, représentée par <code>&lt;&gt;</code>.</p></td>
</tr>
<tr class="even">
<td><p><strong>message-info</strong></p></td>
<td><p>Informations supplémentaires sur le message. Par exemple :</p>
<ul>
<li><p>Date et heure UTC d'origine du message pour les événements <strong>DELIVER</strong> et <strong>SEND</strong>. Les date et heure d'origine indiquent le moment auquel le message est entré dans l'organisation Exchange. La date-heure UTC est représentée au format de date-heure ISO 8601 : yyyy-mm-dd<em>yyyy-mm-dd</em>Thh:mm:ss.fff<em>hh:mm:ss.fff</em>Z, où yyyyy<em>yyyy</em> = année, mm<em>mm</em> = mois, dd<em>dd</em> = jour, T indique le début du composant temps, hh<em>hh</em> = heure, mm<em>mm</em> = minute, ss<em>ss</em> = seconde, fff<em>fff</em> = fractions de seconde et Z correspond à Zulu (qui est une autre manière de désigner le temps universel).</p></li>
<li><p>Erreurs d'authentification. Par exemple, en cas d'erreurs d'authentification, la valeur <code>11a</code> et le type d'authentification utilisé peuvent s'afficher.</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p><strong>directionality</strong></p></td>
<td><p>Direction du message. Par exemple, <code>Incoming</code>, <code>Undefined</code> et <code>Originating</code>.</p></td>
</tr>
<tr class="even">
<td><p><strong>tenant-id</strong></p></td>
<td><p>Ce champ n'est pas utilisé dans les organisations Exchange 2013 locales.</p></td>
</tr>
<tr class="odd">
<td><p><strong>original-client-ip</strong></p></td>
<td><p>Adresse IPv4 ou IPv6 du client d'origine.</p></td>
</tr>
<tr class="even">
<td><p><strong>original-server-ip</strong></p></td>
<td><p>Adresse IPv4 ou IPv6 du serveur d'origine.</p></td>
</tr>
<tr class="odd">
<td><p><strong>custom-data</strong></p></td>
<td><p>Ce champ contient des données relatives à des types d'événements spécifiques. Par exemple, l'agent de règle de transport utilise ce champ pour enregistrer le GUID de la règle de transport la stratégie DLP appliquée au message. Pour plus d'informations sur ces valeurs d'agent de règle de transport, consultez la section « Journalisation des données » de la rubrique <a href="view-dlp-policy-detection-reports-exchange-2013-help.md">Afficher les rapports de détection de stratégies DLP</a>.</p></td>
</tr>
</tbody>
</table>


Retour au début

## Types d'événements dans le journal de suivi des messages

Dans le champ **event-id**, divers types d'événements sont utilisés pour classifier les événements de messages dans le journal de suivi des messages. Certains événements de messages apparaissent dans un seul type de fichier journal de suivi des messages, et d'autres dans tous les types de journaux de suivi des messages. Le tableau suivant présente les types d'événements utilisés pour classifier chaque événement de message.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Nom de l'événement</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>AGENTINFO</strong></p></td>
<td><p>Cet événement est utilisé par les agents transport pour journaliser des données personnalisées.</p></td>
</tr>
<tr class="even">
<td><p><strong>BADMAIL</strong></p></td>
<td><p>Un message soumis par le répertoire de collecte ou de relecture ne peut pas être remis ou retourné.</p></td>
</tr>
<tr class="odd">
<td><p><strong>DEFER</strong></p></td>
<td><p>La remise du message a été retardée.</p></td>
</tr>
<tr class="even">
<td><p><strong>DELIVER</strong></p></td>
<td><p>Un message a été remis à une boîte aux lettres locale.</p></td>
</tr>
<tr class="odd">
<td><p><strong>DROP</strong></p></td>
<td><p>Un message a été supprimé sans notification d’état de remise (également appelée notification de non-remise ou notification d’échec de remise). Par exemple :</p>
<ul>
<li><p>Messages de demande d’approbation de modération terminée.</p></li>
<li><p>Courriers indésirables supprimés sans avertissement, sans notification d’échec de remise.</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>DSN</strong></p></td>
<td><p>Une notification d'état de remise a été générée.</p></td>
</tr>
<tr class="odd">
<td><p><strong>DUPLICATEDELIVER</strong></p></td>
<td><p>Un message en double a été remis au destinataire. Une duplication peut se produire si un destinataire est membre de plusieurs groupes de distribution imbriqués. Les messages en double sont détectés et supprimés par la banque d'informations.</p></td>
</tr>
<tr class="even">
<td><p><strong>DUPLICATEEXPAND</strong></p></td>
<td><p>Durant l'expansion du groupe de distribution, un destinataire en double a été détecté.</p></td>
</tr>
<tr class="odd">
<td><p><strong>DUPLICATEREDIRECT</strong></p></td>
<td><p>Un autre destinataire du message était déjà destinataire.</p></td>
</tr>
<tr class="even">
<td><p><strong>EXPAND</strong></p></td>
<td><p>Un groupe de distribution a été développé.</p></td>
</tr>
<tr class="odd">
<td><p><strong>FAIL</strong></p></td>
<td><p>La remise du message a échoué. Les sources incluent <strong>SMTP</strong>, <strong>DNS</strong>, <strong>QUEUE</strong> et <strong>ROUTING</strong>.</p></td>
</tr>
<tr class="even">
<td><p><strong>HADISCARD</strong></p></td>
<td><p>Un message de cliché instantané a été écarté après remise de la copie principale au saut suivant. Pour plus d'informations, consultez la rubrique <a href="shadow-redundancy-exchange-2013-help.md">Redondance des clichés instantanés</a>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>HARECEIVE</strong></p></td>
<td><p>Le serveur a reçu un message de cliché instantané dans le groupe de disponibilité de base de données (DAG) ou le site Active Directory locaux.</p></td>
</tr>
<tr class="even">
<td><p><strong>HAREDIRECT</strong></p></td>
<td><p>Un message de cliché instantané a été créé.</p></td>
</tr>
<tr class="odd">
<td><p><strong>HAREDIRECTFAIL</strong></p></td>
<td><p>La création d'un message de cliché instantané a échoué. Les détails figurent dans le champ <strong>source-context</strong>.</p></td>
</tr>
<tr class="even">
<td><p><strong>INITMESSAGECREATED</strong></p></td>
<td><p>Un message a été envoyé à un destinataire modéré. Le message a donc été transmis à la boîte aux lettres d'arbitrage pour approbation. Pour plus d'informations, consultez la rubrique <a href="manage-message-approval-exchange-2013-help.md">Gérer l’approbation des messages</a>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>LOAD</strong></p></td>
<td><p>Un message a été chargé avec succès au démarrage.</p></td>
</tr>
<tr class="even">
<td><p><strong>MODERATIONEXPIRE</strong></p></td>
<td><p>Aucun modérateur d'un destinataire modéré n'ayant jamais approuvé ou rejeté le message, ce dernier a expiré. Pour plus d'informations sur les destinataires modérés, consultez la rubrique <a href="manage-message-approval-exchange-2013-help.md">Gérer l’approbation des messages</a>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>MODERATORAPPROVE</strong></p></td>
<td><p>Un modérateur d'un destinataire modéré ayant approuvé le message, ce dernier a été remis au destinataire.</p></td>
</tr>
<tr class="even">
<td><p><strong>MODERATORREJECT</strong></p></td>
<td><p>Un modérateur d'un destinataire modéré ayant rejeté le message, ce dernier n'a pas été remis au destinataire.</p></td>
</tr>
<tr class="odd">
<td><p><strong>MODERATORSALLNDR</strong></p></td>
<td><p>Aucune des demandes d'approbation envoyées à tous les modérateurs d'un destinataire modéré n'ayant pu être remise, des notifications d'échec de remise (NDR) ont été générées.</p></td>
</tr>
<tr class="even">
<td><p><strong>NOTIFYMAPI</strong></p></td>
<td><p>Un message a été détecté dans la boîte d'envoi d'une boîte aux lettres sur le serveur local.</p></td>
</tr>
<tr class="odd">
<td><p><strong>NOTIFYSHADOW</strong></p></td>
<td><p>Un message a été détecté dans la boîte d'envoi d'une boîte aux lettres sur le serveur local, et un cliché instantané du message doit être créé.</p></td>
</tr>
<tr class="even">
<td><p><strong>POISONMESSAGE</strong></p></td>
<td><p>Un message a été placé dans la file d'attente de messages incohérents ou supprimé de cette dernière.</p></td>
</tr>
<tr class="odd">
<td><p><strong>PROCESS</strong></p></td>
<td><p>Le traitement du message a réussi.</p></td>
</tr>
<tr class="even">
<td><p><strong>PROCESSMEETINGMESSAGE</strong></p></td>
<td><p>Un message de réunion a été traité par le service de remise de transport de boîte aux lettres.</p></td>
</tr>
<tr class="odd">
<td><p><strong>RECEIVE</strong></p></td>
<td><p>Un message a été reçu par le composant de réception SMTP du service de transport, ou des répertoires de collecte ou de relecture (source : <code>SMTP</code>). Ou un message a été déposé à partir d'une boîte aux lettres au service de dépôt de transport de boîte aux lettres (source : <code>STOREDRIVER</code>).</p></td>
</tr>
<tr class="even">
<td><p><strong>REDIRECT</strong></p></td>
<td><p>Un message a été redirigé vers un autre destinataire après une recherche Active Directory.</p></td>
</tr>
<tr class="odd">
<td><p><strong>RESOLVE</strong></p></td>
<td><p>Les destinataires d'un message ont été résolus dans une adresse de messagerie différente après une recherche Active Directory.</p></td>
</tr>
<tr class="even">
<td><p><strong>RESUBMIT</strong></p></td>
<td><p>Un message a été resoumis automatiquement à partir du filet de sécurité. Pour plus d'informations, consultez la rubrique <a href="safety-net-exchange-2013-help.md">Safety Net</a>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>RESUBMITDEFER</strong></p></td>
<td><p>Un message resoumis à partir du filet de sécurité a été différé.</p></td>
</tr>
<tr class="even">
<td><p><strong>RESUBMITFAIL</strong></p></td>
<td><p>La resoumission d'un message à partir du filet de sécurité a échoué.</p></td>
</tr>
<tr class="odd">
<td><p><strong>SEND</strong></p></td>
<td><p>Un message a été échangé par SMTP entre des services de transport.</p></td>
</tr>
<tr class="even">
<td><p><strong>SUBMIT</strong></p></td>
<td><p>Le service de dépôt de transport de boîtes aux lettres a transmis le message au service de transport. Pour les événements <strong>SUBMIT</strong>, la propriété <strong>source-context</strong> contient les détails suivants :</p>
<ul>
<li><p><strong>MDB</strong>   GUID de base de données de boîtes aux lettres.</p></li>
<li><p><strong>Mailbox</strong>   GUID de boîte aux lettres.</p></li>
<li><p><strong>Event</strong>   Numéro de la séquence d'événements.</p></li>
<li><p><strong>MessageClass</strong>   Type de message. Par exemple, <code>IPM.Note</code>.</p></li>
<li><p><strong>CreationTime</strong>   Date et heure de dépôt du message.</p></li>
<li><p><strong>ClientType</strong>   Par exemple, <code>User</code>, <code>OWA</code> ou <code>ActiveSync</code>.</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p><strong>SUBMITDEFER</strong></p></td>
<td><p>La transmission du message à partir du service de dépôt de transport de boîte aux lettres au service de transport a été différée.</p></td>
</tr>
<tr class="even">
<td><p><strong>SUBMITFAIL</strong></p></td>
<td><p>La transmission du message à partir du service de dépôt de transport de boîte aux lettres au service de transport a échoué.</p></td>
</tr>
<tr class="odd">
<td><p><strong>SUPPRESSED</strong></p></td>
<td><p>La transmission du message a été supprimée.</p></td>
</tr>
<tr class="even">
<td><p><strong>THROTTLE</strong></p></td>
<td><p>Le message a été limité.</p></td>
</tr>
<tr class="odd">
<td><p><strong>TRANSFER</strong></p></td>
<td><p>Les destinataires ont été déplacés dans un message transféré à cause de la conversion de contenu, des limites relatives aux destinataires du message ou aux agents. Les sources peuvent être <strong>ROUTING</strong> ou <strong>QUEUE</strong>.</p></td>
</tr>
</tbody>
</table>


Retour au début

## Valeurs de source dans le journal de suivi des messages

Les valeurs du champ **source** dans le journal de suivi des messages indiquent le composant de transport responsable de l'événement de suivi de message. Le tableau suivant décrit les valeurs du champ **source**.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Valeur de source</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>ADMIN</strong></p></td>
<td><p>La source de l'événement était une intervention humaine. Par exemple, un administrateur a utilisé l'Afficheur des files d'attente pour supprimer un message, ou déposé des fichiers de messages à l'aide du répertoire de relecture.</p></td>
</tr>
<tr class="even">
<td><p><strong>AGENT</strong></p></td>
<td><p>La source de l'événement était un agent de transport.</p></td>
</tr>
<tr class="odd">
<td><p><strong>APPROVAL</strong></p></td>
<td><p>La source de l'événement était la structure d'approbation utilisée avec les destinataires modérés. Pour plus d'informations, consultez la rubrique <a href="manage-message-approval-exchange-2013-help.md">Gérer l’approbation des messages</a>.</p></td>
</tr>
<tr class="even">
<td><p><strong>BOOTLOADER</strong></p></td>
<td><p>La source de l’événement était l’existence de messages non traités sur le serveur au démarrage. Ceci est lié au type d’événement <strong>LOAD</strong>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>DNS</strong></p></td>
<td><p>La source de l'événement était une DNS.</p></td>
</tr>
<tr class="even">
<td><p><strong>DSN</strong></p></td>
<td><p>La source de l'événement était une notification d'état de remise (DSN). Par exemple, un rapport de non-remise (NDR).</p></td>
</tr>
<tr class="odd">
<td><p><strong>GATEWAY</strong></p></td>
<td><p>La source de l'événement était un connecteur étranger. Pour plus d'informations, consultez la rubrique <a href="foreign-connectors-exchange-2013-help.md">Connecteurs étrangers</a>.</p></td>
</tr>
<tr class="even">
<td><p><strong>MAILBOXRULE</strong></p></td>
<td><p>La source de l'événement était une règle de boîte de réception. Pour plus d'informations, consultez la rubrique <a href="https://go.microsoft.com/fwlink/?linkid=285479">Règles de la boîte de réception</a>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>MEETINGMESSAGEPROCESSOR</strong></p></td>
<td><p>La source de l’événement était le processeur de messages de réunion qui met à jour des calendriers en fonction des mises à jour de réunion.</p></td>
</tr>
<tr class="even">
<td><p><strong>ORAR</strong></p></td>
<td><p>La source de l'événement était un destinataire suppléant demandé par l'expéditeur (ORAR). Vous pouvez activer ou désactiver les destinataires ORAR sur les connecteurs de réception à l'aide du paramètre <em>OrarEnabled</em> sur la cmdlet <strong>New-ReceiveConnector</strong> ou <strong>Set-ReceiveConnector</strong>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>PICKUP</strong></p></td>
<td><p>La source de l'événement était le répertoire de collecte. Pour plus d'informations, consultez la rubrique <a href="pickup-directory-and-replay-directory-exchange-2013-help.md">Répertoire de collecte et répertoire de relecture</a>.</p></td>
</tr>
<tr class="even">
<td><p><strong>POISONMESSAGE</strong></p></td>
<td><p>La source de l'événement était l'identificateur de message incohérent. Pour plus d'informations sur les messages incohérents et la file d'attente de messages incohérents, consultez la rubrique <a href="queues-exchange-2013-help.md">Files d'attente</a></p></td>
</tr>
<tr class="odd">
<td><p><strong>PUBLICFOLDER</strong></p></td>
<td><p>La source de l'événement était un dossier public à extension messagerie.</p></td>
</tr>
<tr class="even">
<td><p><strong>QUEUE</strong></p></td>
<td><p>La source de l'événement était une file d'attente.</p></td>
</tr>
<tr class="odd">
<td><p><strong>REDUNDANCY</strong></p></td>
<td><p>La source de l'événement était une redondance de cliché instantané. Pour plus d'informations, consultez la rubrique <a href="shadow-redundancy-exchange-2013-help.md">Redondance des clichés instantanés</a>.</p></td>
</tr>
<tr class="even">
<td><p><strong>ROUTING</strong></p></td>
<td><p>La source de l'événement était le composant de résolution de routage du catégoriseur dans le service de transport.</p></td>
</tr>
<tr class="odd">
<td><p><strong>SAFETYNET</strong></p></td>
<td><p>La source de l'événement était un filet de sécurité. Pour plus d'informations, consultez la rubrique <a href="safety-net-exchange-2013-help.md">Safety Net</a>.</p></td>
</tr>
<tr class="even">
<td><p><strong>SMTP</strong></p></td>
<td><p>Le message a été déposé par le composant d'envoi ou de réception SMTP du service de transport.</p></td>
</tr>
<tr class="odd">
<td><p><strong>STOREDRIVER</strong></p></td>
<td><p>La source de l'événement était un dépôt MAPI à partir d'une boîte aux lettres sur le serveur local.</p></td>
</tr>
</tbody>
</table>


Retour au début

## Exemples d'entrées du journal de suivi des messages

Un message sans événement échangé entre deux utilisateurs génère plusieurs entrées dans le journal de suivi des messages. Vous pouvez voir les résultats à l'aide de la cmdlet **Get-MessageTrackingLog**. Pour plus d'informations, consultez la rubrique [Recherche des journaux de suivi des messages](search-message-tracking-logs-exchange-2013-help.md).

Ceci est un exemple condensé des entrées du journal de suivi des messages créées lorsque l'utilisateur chris@contoso.com envoie avec succès un message de test à l'utilisateur michelle@contoso.com. Les deux utilisateurs ont des boîtes aux lettres sur le même serveur.

    EventId    Source      Sender            Recipients             MessageSubject
    -------    ------      ------            ----------             --------------
    NOTIFYMAPI STOREDRIVER                   {}
    RECEIVE    STOREDRIVER chris@contoso.com {michelle@contoso.com} test
    SUBMIT     STOREDRIVER chris@contoso.com {michelle@contoso.com} test
    HAREDIRECT SMTP        chris@contoso.com {michelle@contoso.com} test
    RECEIVE    SMTP        chris@contoso.com {michelle@contoso.com} test
    AGENTINFO  AGENT       chris@contoso.com {michelle@contoso.com} test
    SEND       SMTP        chris@contoso.com {michelle@contoso.com} test
    DELIVER    STOREDRIVER chris@contoso.com {michelle@contoso.com} test

Retour au début

## Problèmes de sécurité pour le journal de suivi des messages

Aucun contenu de message n'est stocké dans le journal de suivi des messages. Par défaut, la ligne d'objet d'un message électronique est enregistrée dans le journal de suivi des messages. Vous pouvez désactiver l'enregistrement de l'objet des messages pour vous conformer à des exigences de confidentialité et de sécurité renforcées. Avant d'activer ou de désactiver l'enregistrement de l'objet des messages, vérifiez la stratégie appliquée par votre organisation en matière de divulgation des informations de la ligne d'objet. Pour plus d'informations, consultez la rubrique [Configuration du suivi des messages](configure-message-tracking-exchange-2013-help.md).

Retour au début

