---
title: 'Résolution des destinataires: Exchange 2013 Help'
TOCTitle: Résolution des destinataires
ms:assetid: 09deda5a-d405-45b1-a3ff-fefd3d76cdea
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb430743(v=EXCHG.150)
ms:contentKeyID: 52062934
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Résolution des destinataires

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2016-03-17_

La *résolution des destinataires* est le processus de développement et de résolution de tous les destinataires d'un message. L'action de résolution des destinataires met en correspondance un destinataire avec l'objet Active Directory approprié au sein de l'organisation Microsoft Exchange. L'action de développement des destinataires affiche tous les groupes de distribution en une liste de destinataires individuels. La résolution des destinataires permet une application correcte des règles de limites des messages et des destinataires alternatifs à chaque destinataire.

Dans une organisation Microsoft Exchange Server 2013, la résolution des destinataires est réalisée par le catégoriseur dans le service de transport sur les serveurs de boîtes aux lettres. Une catégorisation de chaque message intervient après qu'un nouveau message a été placé dans la file d'attente de soumission. Une résolution des destinataires, outre la conversion de contenu et le routage, est effectuée sur le message avant son placement dans une file d'attente de remise. Le catégoriseur effectue une résolution des destinataires avant le routage. Le composant du catégoriseur responsable de la résolution des destinataires est souvent appelé *résolveur*.

**Contenu de cette rubrique**

Résolution de niveau supérieur

Expansion

Bifurcation et contrôle de l'expansion des destinataires

Diagnostics de résolution des destinataires

## Résolution de niveau supérieur

La *résolution de niveau supérieur* est la première étape de la résolution des destinataires. La résolution de niveau supérieur associe chaque destinataire d'un message entrant à l'objet destinataire correspondant dans Active Directory. Durant une résolution de niveau supérieur, le catégoriseur crée une liste contenant l'expéditeur et les adresses de messagerie initiales des destinataires, non développées, figurant dans le message. Le catégoriseur utilise cette liste d'adresses de messagerie pour envoyer une requête à Active Directory afin d'identifier des objets à extension messagerie dont les attributs d'adresse de messagerie correspondent. Quand une correspondance est trouvée, les propriétés de l'objet Active Directory correspondant sont mises en cache en vue d'un usage ultérieur. Les restrictions applicables aux expéditeurs des messages sont également appliquées.

## Adresses de messagerie des destinataires

Une résolution de niveau supérieur commence par un message et la liste initiale, non développée, des destinataires de l'*enveloppe de message*. L'enveloppe de message contient les commandes utilisées pour la transmission des messages via les serveurs de messagerie SMTP. L'adresse de messagerie de l'expéditeur est contenue dans la commande **MAIL FROM:**  . L'adresse de messagerie de chaque destinataire est contenue dans une commande **RCPT TO:**  distincte. L'expéditeur et les destinataires d'enveloppe sont généralement créés à partir de l'expéditeur et des destinataires des champs d'en-tête `To:`, `From:`, `Cc:` et `Bcc:` de l'en-tête du message. Ce n'est toutefois pas toujours le cas. Les champs d'en-tête `To:`, `From:`, `Cc:` et `Bcc:` d'un message sont aisément falsifiables et peuvent ne pas correspondre aux adresses électroniques réelles d'expéditeur ou de destinataire utilisées pour transmettre le message.

## Adresses de messagerie encapsulées

Les adresses de messagerie SMTP standard suivent les spécifications des normes RFC 2821 et RFC 2822, et présentent, par exemple, la forme chris@contoso.com. Toutefois, une adresse de messagerie n'est pas forcément une adresse SMTP encapsulée dans une adresse SMTP correcte. Exchange prend en charge les adresses encapsulées utilisant la méthode d'encapsulation IMCEA (Internet Mail Connector Encapsulated Address).

Cette méthode d'encapsulation nécessite le codage des caractères incorrects dans les adresses de messagerie SMTP. Les caractères alphanumériques, le signe égal (=) et le tiret (-) ne requièrent pas de codage. Les autres caractères utilisent la syntaxe de codage suivante :

  - Une barre oblique (/) est remplacée par un trait de soulignement (\_).

  - Les autres caractères US-ASCII sont remplacés par un signe plus (+) et les deux chiffres de leur valeur ASCII sont écrits en hexadécimal. Par exemple, la valeur codée de l'espace est `+20`.

La méthode d'encapsulation IMCEA utilise la syntaxe suivante : `IMCEA<Type>-<address>@<domain>`

L'espace réservé \<*Type*\> identifie le type d'adresse non-SMTP, par exemple, `EX`, `X400` ou `FAX`.

> [!NOTE]
> Bien que <code>SMTP</code> et <code>X500</code> soient théoriquement des valeurs correctes pour &lt;<em>Type</em>&gt;, la résolution des destinataires Exchange rejette toute adresse codée IMCEA utilisant l'un de ces types.


L'espace réservé \<*address*\> est l'adresse d'origine codée. L'espace réservé \<*domain*\> représente le domaine SMTP utilisé pour encapsuler l'adresse non-SMTP, par exemple, contoso.com.

Avec la méthode d'encapsulation IMCEA, les adresses ne sont encapsulées que quand le domaine correspond au domaine faisant autorité par défaut au sein de l'organisation Exchange. Pour plus d'informations sur les domaines acceptés, consultez la rubrique [Domaines acceptés](accepted-domains-exchange-2013-help.md).

La longueur maximale d'une adresse de messagerie SMTP dans Exchange est de 571 caractères. Cette limite inclut les éléments suivants :

  - 315 caractères pour la partie nom de l'adresse ;

  - 255 caractères pour le nom de domaine ;

  - Le caractère « @ » qui sépare la partie nom de l'adresse du nom de domaine.

Notez qu'Exchange ne prend pas en charge les messages codés à l'aide de la méthode d'encapsulation IMCEA si la partie nom de l'adresse dépasse 315 caractères, même si l'adresse de messagerie complète ne dépasse pas 571 caractères.

## Résolution d'adresse

Pour chaque message, l'adresse de messagerie de l'expéditeur et toutes les adresses de messagerie des destinataires sont ajoutées à une liste utilisée pour envoyer une requête à Active Directory. Toutes les adresses encapsulées sont « désencapsulées » avant leur ajout à la liste d'adresses de messagerie. La requête Active Directory est effectuée sur un maximum de 20 adresses à la fois. Si la requête Active Directory rencontre des erreurs passagères, le message est renvoyé à la file d'attente de soumission et différé le temps indiqué par la clé *ResolverRetryInterval* dans le fichier de configuration de l'application XML `%ExchangeInstallPath%Bin\EdgeTransport.exe.config` associé au service de transport Microsoft Exchange. La valeur par défaut est 30 minutes.

Le tableau suivant décrit les objets destinataires trouvés dans Active Directory. Pour plus d'informations sur les types de destinataires, consultez la rubrique [Recipients](recipients-exchange-2013-help.md).

### Objets destinataires d'Active Directory

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Type de destinataire Active Directory</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>DistributionGroup</p></td>
<td><p>Tout objet groupe à extension messagerie. Les types d'objet groupe de distribution sont les suivants :</p>
<ul>
<li><p><strong>MailUniversalDistributionGroup</strong>   Objet groupe de distribution universel.</p></li>
<li><p><strong>MailUniversalSecurityGroup</strong>   Objet groupe universel de sécurité ayant une adresse de messagerie.</p></li>
<li><p><strong>MailNonUniversalGroup</strong>   Objet groupe de sécurité local ou global ayant une adresse de messagerie.</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>DynamicDistributionGroup</p></td>
<td><p>Objet ayant la classe Active Directory <strong>msExchDynamicDistributionList</strong>. Pour plus d'informations, consultez la rubrique <a href="https://docs.microsoft.com/fr-fr/exchange/recipients-in-exchange-online/manage-dynamic-distribution-groups/manage-dynamic-distribution-groups">Gérer des groupes de distribution dynamiques</a>.</p></td>
</tr>
<tr class="odd">
<td><p>Mailbox</p></td>
<td><p>Objet utilisateur ayant une adresse de messagerie et un paramètre <em>Database</em> défini.</p></td>
</tr>
<tr class="even">
<td><p>MailUser</p></td>
<td><p>Objet utilisateur ayant une adresse de messagerie sans paramètre <em>Database</em> défini. Pour plus d'informations, consultez la rubrique <a href="https://docs.microsoft.com/fr-fr/exchange/recipients-in-exchange-online/manage-mail-users">Gérer les utilisateurs de messagerie</a>.</p></td>
</tr>
<tr class="odd">
<td><p>MailContact</p></td>
<td><p>Objet contact ayant une adresse de messagerie. Généralement, un contact de messagerie est utilisé pour des destinataires situés à l'extérieur de l'organisation Exchange. Un contact de messagerie est également utilisé dans des environnements Exchange inter-forêts. Pour plus d'informations, consultez la rubrique <a href="https://docs.microsoft.com/fr-fr/exchange/recipients-in-exchange-online/manage-mail-contacts">Gérer les contacts de messagerie</a>.</p></td>
</tr>
<tr class="even">
<td><p>MailPublicFolder</p></td>
<td><p>Objet dossier public ayant une adresse de messagerie.</p></td>
</tr>
<tr class="odd">
<td><p>MicrosoftExchangeRecipient</p></td>
<td><p>Objet ayant la classe Active Directory <strong>msExchExchangeServerRecipient</strong>. Pour plus d'informations sur l'objet destinataire Microsoft Exchange, consultez la rubrique <a href="recipients-exchange-2013-help.md">Recipients</a>.</p></td>
</tr>
<tr class="even">
<td><p>SystemAttendantMailbox</p></td>
<td><p>Objet ayant la classe Active Directory <strong>exchangeAdminService</strong>. Il ne peut y avoir qu'une seule boîte aux lettres de surveillance du système au sein de l'organisation Exchange.</p></td>
</tr>
<tr class="odd">
<td><p>SystemMailbox</p></td>
<td><p>Objet utilisateur ayant une adresse de messagerie et situé dans le conteneur d'objets système Microsoft Exchange. Il ne peut y avoir qu'une seule boîte aux lettres système pour chaque base de données de boîtes aux lettres au sein de l'organisation Exchange.</p></td>
</tr>
</tbody>
</table>


Un objet dont des propriétés critiques sont manquantes ou incorrectes est classifié par la requête Active Directory comme objet non valide. Par exemple, un objet groupe de distribution dynamique sans adresse de messagerie est considéré comme non valide. Les messages envoyés aux destinataires qui sont classés comme objets non valides génèrent une notification d'échec de remise.

Pour chaque adresse de messagerie, une seule requête initiale est effectuée pour toutes les propriétés de destinataire possibles, telles que les identificateurs de destinataire, le type de destinataire, les limites de message, les adresses de messagerie et les destinataires alternatifs. Les propriétés applicables pour le destinataire sont mises en cache en vue d'un usage futur. La résolution des destinataires classifie les destinataires en fonction de similitudes dans la manière dont ils sont résolus et de la similitude des propriétés de destinataire applicables.

Le filtre LDAP utilisé pour la résolution d'adresse est décrit comme suit :

  - Pour le type d'adresse de messagerie **EX**, le filtre LDAP est basé sur l'attribut Active Directory **legacyExchangeDN** ou **proxyAddresses** du destinataire. L'attribut Active Directory **legacyExchangeDN** prime.

  - Pour tous les autres types d'adresses de messagerie, l'attribut Active Directory **proxyAddresses** du destinataire est utilisé comme filtre LDAP.

Si l'adresse de messagerie utilisée dans le message ne correspond pas à l'adresse SMTP principale de l'objet Active Directory correspondant, le catégoriseur réécrit l'adresse de messagerie dans le message pour la faire correspondre à l'adresse SMTP principale. L'adresse de messagerie d'origine est enregistrée dans l'entrée `ORCPT=` de la commande **RCPT TO:**  dans l'enveloppe de message.

## Restrictions applicables au message de l'expéditeur

La taille utilisée pour la restriction de la taille du message de l'expéditeur est la valeur du champ d'en-tête **X-MS-Exchange-Organization-OriginalSize:**  dans l'en-tête du message. Exchange utilise ce champ d'en-tête pour enregistrer la taille d'origine du message quand il est entré dans l'organisation Exchange. Chaque fois qu'un message est vérifié par rapport aux limites de taille de message spécifiées, la valeur la plus faible de l'en-tête de la taille de message actuelle ou de la taille de message d'origine est utilisée. La taille du message peut varier en raison de la conversion de contenu, du codage et du traitement par l'agent. Si ce champ d'en-tête n'existe pas, il est créé à l'aide de la valeur de taille de message actuelle. Si le message est trop volumineux, une notification d'échec de remise est générée et tout traitement de message supplémentaire est interrompu.

La limite du nombre de destinataires de l'expéditeur n'est appliquée que dans le service de transport sur le premier serveur de boîte aux lettres qui traite le message. Le nombre de destinataires de l'enveloppe de message non développé d'origine est comparé à la limite de destinataires de l'expéditeur. Le nombre de destinataires de l'enveloppe de message non développé d'origine est utilisé pour éviter les problèmes de remise partielle de message qui se produisaient dans Microsoft Exchange Server 2003 quand des listes de distribution imbriquées utilisaient des serveurs d'expansion distants.

L'expéditeur du message et tous les destinataires sont marqués comme résolus par l'enregistrement d'une propriété étendue dans le message. Cette propriété étendue permet au message de contourner la résolution de niveau supérieur s'il doit de nouveau passer par une nouvelle résolution des destinataires. Il se peut qu'un message doive passer par une nouvelle résolution des destinataires suite au redémarrage du service de transport Microsoft Exchange.

Retour au début

## Expansion

L'expansion intervient après la résolution de niveau supérieur. L'expansion développe complètement les niveaux de destinataires imbriqués en destinataires individuels. L'expansion peut nécessiter plusieurs itérations du processus d'expansion afin de développer tous les destinataires. Les destinataires ne doivent pas tous être développés. En revanche, tous les destinataires doivent passer par le processus d'expansion. Le processus d'expansion applique également des restrictions de message de destinataire pour tous les types de destinataires.

La liste suivante décrit les types de destinataires qui nécessitent une expansion :

  - **Groupes de distribution et groupes de distribution dynamiques**   Les groupes de distribution sont développés sur la base de la propriété Active Directory **memberOf**. Les groupes de distribution dynamiques sont développés à l'aide de la définition de requête Active Directory. Si le paramètre *ExpansionServer* est défini pour le groupe, ce dernier n'est pas développé par le serveur actuel. Le groupe de distribution est routé vers le serveur spécifié pour l'expansion.
    
    > [!NOTE]
    > Si vous sélectionnez un serveur de transport spécifique de votre organisation comme serveur d'extension, l'utilisation du groupe de distribution dépend de la disponibilité du serveur d'extension. Si le serveur d'expansion est indisponible, aucun message envoyé au groupe de distribution ne peut être remis. Si vous projetez d'utiliser des serveurs d'expansion spécifiques pour vos groupes de distribution, afin de réduire le risque d'interruption de service, vous devez envisager d'implémenter des solutions de disponibilité élevée pour ces serveurs.


  - **Autres destinataires**   Le paramètre *ForwardingAddress* peut être défini pour des boîtes aux lettres et des dossiers publics à extension messagerie. Le paramètre *ForwardingAddress* redirige tous les messages vers le destinataire alternatif spécifié. C'est ce qu'on appelle un *destinataire transféré*. Quand une adresse de remise alternative est spécifiée dans le paramètre *ForwardingAddress* et que le paramètre *DeliverToMailboxAndForward* est défini sur `$true`, le message est remis au destinataire d'origine et au destinataire alternatif. C'est ce qu'on appelle un *destinataire remis et transféré*.

  - **Chaînes de contact**   Une *chaîne de contact* est un utilisateur de messagerie ou un contact de messagerie dont le paramètre *ExternalEmailAddress* est défini sur l'adresse de messagerie d'un autre destinataire au sein de l'organisation Exchange.

## Détection de boucles de destinataires

Lors de l'expansion des groupes de distribution, des destinataires alternatifs et des chaînes de contact, le catégoriseur vérifie la présence de *boucles de destinataires*. Une boucle de destinataires est un problème de configuration de destinataire qui a pour effet qu'un message est remis aux mêmes destinataires en une boucle infinie. La liste suivante décrit les différents types de boucles de destinataires :

  - **Boucle de destinataires inoffensive**   Une boucle de destinataires inoffensive aboutit à la réussite de la remise du message. La liste suivante décrit deux scénarios où des boucles de destinataires inoffensives peuvent apparaître :
    
      - quand deux groupes de distribution se contiennent l'un l'autre comme membres ;
    
      - quand des boîtes aux lettres ou des dossiers publics à extension messagerie sont définis pour remettre et transférer l'un à l'autre. Cela se produit quand le paramètre *DeliverToMailboxAndForward* des deux destinataires est défini sur `$true` et que le paramètre *ForwardingAddress* est défini pour un transfert de l'un à l'autre.
    
    En cas de détection d'une boucle de destinataires inoffensive, le message est remis au destinataire mais aucune autre tentative de remise du message au même destinataire n'a lieu.

  - **Boucle de destinataires interrompue**   Une boucle de destinataires interrompue empêche la remise du message. Une boucle de destinataires interrompue se produit par exemple quand des boîtes aux lettres ou des dossiers publics à extension messagerie ont le paramètre *ForwardingAddress* défini pour un transfert de l'un à l'autre. Quand le catégoriseur détecte une boucle de destinataires interrompue, l'activité d'expansion relative au destinataire en cours est interrompue et une notification d'échec de remise est envoyée au destinataire.

La détection de boucles de destinataires n'empêche pas la remise de messages en double. Par exemple, le groupe de distribution C est sujet à un problème de remise de messages en double si les conditions suivantes sont vraies :

  - Les groupes de distribution B et C sont membres du groupe de distribution A.

  - Le groupe de distribution C est également membre du groupe de distribution B.

## Redirection de notification de remise pour des groupes de distribution

Lors de l'expansion d'un groupe de distribution, le type de message est contrôlé pour déterminer s'il s'agit d'un message de notification de remise. Si le message est une notification de remise, les paramètres de redirection du groupe de distribution sont contrôlés pour déterminer si une redirection de la notification de remise est requise. Vous pouvez décider de supprimer les notifications de remise car elles risquent de divulguer des informations non voulues sur le groupe de distribution et ses membres.

La liste suivante décrit les paramètres de redirection de notification de remise disponibles pour les groupes de distribution et les groupes de distribution dynamiques :

  - **ReportToManagerEnabled**   Ce paramètre active l'envoi de notifications de remise au gestionnaire du groupe de distribution. Les valeurs correctes sont `$true` et `$false`. La valeur par défaut est `$false`. Pour un groupe de distribution, le gestionnaire est contrôlé par le paramètre *ManagedBy* de la cmdlet **Set-Group**. Pour un groupe de distribution dynamique, le gestionnaire est contrôlé par le paramètre *ManagedBy* de la cmdlet **Set-DynamicDistributionGroup**.

  - **ReportToOriginatorEnabled**   Ce paramètre active l'envoi de notifications de remise à l'expéditeur des messages électroniques envoyés à ce groupe de distribution. Les valeurs correctes sont `$true` ou `$false`. La valeur par défaut est `$true`.
    
    > [!NOTE]
    > Les valeurs des paramètres <em>ReportToManagerEnabled</em> et <em>ReportToOriginatorEnabled</em> ne peuvent pas être toutes les deux <code>$true</code>. Si un paramètre est défini sur <code>$true</code>, l'autre doit être défini sur <code>$false</code>. Les deux paramètres peuvent avoir la valeur <code>$false</code>. Cela a pour effet de supprimer toute redirection des messages de notification de remise.


La liste suivante décrit les messages de notification de remise disponibles :

  - **Accusé de réception**   Cette notification confirme qu'un message a été remis à son destinataire.

  - **Notification d'état de remise**   Cette notification décrit le résultat de la tentative de remise d'un message. Pour plus d'informations sur les messages de notification d'état de remise, consultez la rubrique [Notifications d’état de remise et notifications d’échec de remise dans Exchange 2013](dsns-and-ndrs-in-exchange-2013-exchange-2013-help.md).

  - **Notification de disposition de message**   Cette notification décrit le statut d'un message après qu'il a été remis avec succès à un destinataire. Une notification de lecture et une notification de non-lecture sont des exemples de notifications de disposition de message. Les messages de notification de disposition de messages sont définis dans la norme RFC 2298 et sont contrôlés par le champ d'en-tête **Disposition-Notification-To:**  dans l'en-tête du message. Les paramètres de notification de disposition de message qui utilisent le champ d'en-tête `Disposition-Notification-To:` sont compatibles avec un grand nombre de serveurs de messages différents. Il est également possible de définir les paramètres de notification de disposition de message à l'aide des propriétés MAPI dans Microsoft Outlook et Exchange.

  - **Notification d'échec de remise**   Cette notification indique à l'expéditeur du message qu'il n'a pas été possible de remettre ce dernier aux destinataires spécifiés.

  - **Notification de non-lecture**   Cette notification indique qu'un message a été supprimé avant d'être lu.

  - **Notification d'absence du bureau**   Cette notification indique que le destinataire ne répondra pas aux messages électroniques. Dans la version anglaise, l'acronyme remonte au système de messagerie Microsoft d'origine où la notification correspondante était nommée « out of facility ».

  - **Notification de lecture**   Cette notification indique qu'un message a été lu.

  - **Rapport de rappel**   Cette notification indique le statut d'une demande de rappel pour un destinataire donné. Une demande de rappel est le fait pour un expéditeur de tenter de rappeler un message envoyé à l'aide d'Outlook.

Quand un message de notification de remise est envoyé à un groupe de distribution, les paramètres suivants entraînent la suppression du message de notification :

  - La redirection de la notification n'est pas définie. Ou bien la redirection de la notification est définie sur l'expéditeur du message.

  - La redirection de la notification est définie sur le gestionnaire du groupe de distribution et le message de notification de remise n'est pas une notification d'échec de remise.

Quand un message de notification de remise est envoyé à un groupe de distribution, les paramètres suivants entraînent la remise du message de notification au gestionnaire du groupe de distribution : Cela se produit quand la redirection de la notification est définie sur le gestionnaire du groupe de distribution et le message de notification de remise est une notification d'échec de remise.

Quand un message qui n'est pas un message de notification de remise est envoyé à un groupe de distribution, il est remis aux membres du groupe de distribution. Les paramètres de demande de notification sont résumés dans la liste suivante :

  - Si la redirection de la notification est définie sur l'expéditeur du message, les paramètres de demande de notification ne sont pas modifiés.

  - Si la redirection de la notification n'est pas définie, tous les paramètres de demande de notification sont supprimés. L'entrée `NOTIFY=NEVER` est ajoutée à la commande **RCPT TO:**  pour chaque destinataire figurant dans l'enveloppe de message.

  - Si la redirection de la notification est définie sur le gestionnaire du groupe de distribution, tous les paramètres de demande de notification sont supprimés, à l'exception des notifications d'échec de remise, qui sont envoyées au gestionnaire du groupe de distribution.

## Restrictions de messages pour les destinataires

Le processus d'expansion applique également toutes restrictions de message configurées pour les destinataires. Ces restrictions peuvent être configurées au niveau individuel pour chaque destinataire ou au niveau de l'organisation pour tous les serveurs de transport Hub dans l'organisation Exchange. Le tableau suivant décrit les restrictions de message configurées pour les destinataires.

### Restrictions de messages pour les destinataires

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Source</th>
<th>Paramètre</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Set-DistributionGroup</strong></p>
<p><strong>Set-DynamicDistributionGroup</strong></p>
<p><strong>Set-Mailbox</strong></p>
<p><strong>Set-MailContact</strong></p>
<p><strong>Set-MailPublicFolder</strong></p>
<p><strong>Set-MailUser</strong></p>
<p><strong>Set-TransportConfig</strong></p></td>
<td><p><em>MaxReceiveSize</em></p></td>
<td><p>Le paramètre <em>MaxReceiveSize</em> indique que la taille utilisée pour les restrictions de message configurées pour les destinataires est la valeur du champ d'en-tête <strong>X-MS-Exchange-Organization-OriginalSize:</strong> dans l'en-tête du message. Exchange utilise ce champ d'en-tête pour enregistrer la taille d'origine du message quand il est entré dans l'organisation Exchange. Chaque fois qu'un message est vérifié par rapport aux limites de taille de message spécifiées, la valeur la plus faible de l'en-tête de la taille de message actuelle ou de la taille de message d'origine est utilisée. La taille du message peut varier en raison de la conversion de contenu, du codage et du traitement par l'agent. Si ce champ d'en-tête n'existe pas, il est créé à l'aide de la valeur de taille de message actuelle. Si le message est trop volumineux, une notification d'échec de remise est générée et tout traitement de message supplémentaire est interrompu.</p></td>
</tr>
<tr class="even">
<td><p><strong>Set-DistributionGroup</strong></p>
<p><strong>Set-DynamicDistributionGroup</strong></p>
<p><strong>Set-Mailbox</strong></p>
<p><strong>Set-MailContact</strong></p>
<p><strong>Set-MailPublicFolder</strong></p>
<p><strong>Set-MailUser</strong></p></td>
<td><p><em>RequireSenderAuthenticationEnabled</em></p></td>
<td><p>Le paramètre <em>RequireSenderAuthenticationEnabled</em> exige que tous les messages envoyés au destinataire proviennent d'expéditeurs authentifiés. Si la valeur de ce paramètre est définie sur <code>$true</code>, les messages en provenance d'expéditeurs non authentifiés sont rejetés. Tous les expéditeurs qui envoient des messages aux boîtes aux lettres système et de surveillance du système doivent être authentifiés.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Set-DistributionGroup</strong></p>
<p><strong>Set-DynamicDistributionGroup</strong></p>
<p><strong>Set-Mailbox</strong></p>
<p><strong>Set-MailContact</strong></p>
<p><strong>Set-MailPublicFolder</strong></p>
<p><strong>Set-MailUser</strong></p></td>
<td><p><em>AcceptMessagesOnlyFromSendersOrMembers</em></p>
<p><em>RejectMessagesFromSendersOrMembers</em></p></td>
<td><p>Le paramètre <em>AcceptMessagesOnlyFromSendersOrMembers</em> spécifie les groupes de distribution dont les membres sont autorisés à envoyer des messages au destinataire. Notez que ce paramètre associe les fonctionnalités des anciens paramètres <em>AcceptMessagesOnlyFrom</em> et <em>AcceptMessagesOnlyFromDLMembers</em>.</p>
<p>Le paramètre <em>RejectMessagesFromSendersOrMembers</em> spécifie les expéditeurs ou les groupes de distribution dont les membres ne sont pas autorisés à envoyer des messages au destinataire. Notez que ce paramètre associe les fonctionnalités des anciens paramètres <em>RejectMessagesFrom</em> et <em>RejectMessagesFromDLMembers</em>.</p>
<p>Le catégoriseur contrôle l'autorisation du destinataire en deux fois. Le premier contrôle détermine si l'expéditeur figure dans le paramètre <em>AcceptOnlyMessagesFromSendersOrMembers</em> ou <em>RejectMessagesFromSendersOrMembers</em>. Si l'expéditeur ne figure dans aucun paramètre, les groupes de distribution figurant dans ces paramètres sont complètement développés. Cette expansion complète des groupes de distribution peut prendre du temps. Nous vous recommandons de minimiser la profondeur d'imbrication des groupes de distribution dans ces paramètres.</p></td>
</tr>
</tbody>
</table>


Certains types de messages envoyés par des expéditeurs authentifiés sont exemptés de toute restriction. La liste suivante décrit les messages exemptés de restrictions de destinataire :

  - **Tous les messages envoyés par le destinataire Microsoft Exchange**   Ces messages incluent les messages de notification d'état de remise retardée, les états de journal, les messages de quota et d'autres messages générés par le système envoyés à des expéditeurs de messages internes. Pour en savoir plus sur le destinataire Microsoft consultez la rubrique [Recipients](recipients-exchange-2013-help.md).

  - **Tous les messages envoyés par l'adresse d'administrateur externe**   Ces messages incluent les messages DSN et d'autres messages générés par le système qui sont envoyés à des expéditeurs de messages externes. Pour plus d'informations sur l'adresse d'administrateur externe, consultez la rubrique [Configuration de l’adresse d’administrateur externe](configure-the-external-postmaster-address-exchange-2013-help.md).

Certains types de messages sont bloqués lors de leur envoi à partir de l'organisation Exchange vers des domaines externes. Les paramètres sont contrôlés par les paramètres suivants de la cmdlet **Set-RemoteDomain** :

  - *AllowedOOFType*

  - *AutoForwardEnabled*

  - *AutoReplyEnabled*

  - *DeliveryReportEnabled*

  - *NDREnabled*

Pour plus d'informations, consultez la rubrique [Domaines distants](remote-domains-exchange-2013-help.md).

Retour au début

## Bifurcation et contrôle de l'expansion des destinataires

La liste complète des destinataires de messages étant développée et résolue par la résolution des destinataires, il peut arriver que plusieurs copies d'un même message doivent être créées. Ces cas sont décrits dans les scénarios suivants :

  - **Quand des destinataires de message requièrent des paramètres de message différents**   Il peut arriver que des propriétés de message, telles que les accusés de réception, doivent être activées pour certains destinataires et désactivées pour d'autres. La création d'une nouvelle version d'un message, dont les propriétés diffèrent légèrement de celles du message d'origine est ce qu'on appelle une *bifurcation*.

  - **Limitation du nombre de destinataires de l'enveloppe d'un message**   Le processus d'expansion des destinataires peut générer des milliers de destinataires en cas d'expansion de groupes de distribution importants. Dans Exchange, au lieu de créer une seule copie du message dont l'enveloppe compte des milliers de destinataires, plusieurs copies du message avec un nombre limité de destinataires sur l'enveloppe sont créées.

## Bifurcation

La résolution des destinataires applique une bifurcation à un message si les conditions suivantes sont vraies :

  - Quand l'expéditeur du message indiqué dans **MAIL FROM:** , dans l'enveloppe de message, est mis à jour. Par exemple, quand le paramètre *ReportToManagerEnabled* d'un groupe de distribution a la valeur `$true`.

  - Quand des messages de réponse automatique, tels que des notifications d'état de remise, des notifications d'absence du bureau et des rapports de rappel, doivent être supprimés.

  - Lors de l'expansion de destinataires alternatifs.

  - Quand un champ d'en-tête **Resent-From:**  doit être ajouté à l'en-tête du message. Les champs d'en-tête Resent sont des champs informatifs qui permettent de déterminer si un message a été transféré par un utilisateur. Les champs d'en-tête Resent sont utilisés de façon à ce que le message apparaisse au destinataire comme s'il était envoyé directement par l'expéditeur d'origine. Le destinataire peut afficher l'en-tête de message pour voir qui a transféré le message. Les champs d'en-tête Resent sont définis dans la section 3.6.6 de la norme RFC 2822.

  - Quand l'historique de l'expansion du groupe de distribution doit être transmis.

## Contrôle de l'expansion des destinataires

Quand le nombre de destinataires développés est trop important, le catégoriseur fractionne le message en plusieurs copies. Cette opération vise à réduire l'utilisation des ressources du système durant l'expansion du message. Le nombre maximal de destinataires de l'enveloppe d'un message est contrôlé par la clé *ExpansionSizeLimit* du fichier de configuration d'application `%ExchangeInstallPath%Bin\EdgeTransport.exe.config`. La valeur par défaut est 1000.

> [!CAUTION]
> Nous vous recommandons de ne pas modifier la valeur de la clé <em>ExpansionSizeLimit</em> sur un serveur de transport Exchange dans un environnement de production.


Retour au début

## Diagnostics de résolution des destinataires

Les informations de rapport et de diagnostic en relation avec la résolution des destinataires sont fournies par des compteurs de performance et des entrées de journal de suivi des messages. Ces sources peuvent vous aider à identifier et diagnostiquer des problèmes liés à la résolution des destinataires.

## Compteurs de performance pour la résolution des destinataires

Le tableau suivant décrit les compteurs de performance disponibles pour la résolution des destinataires.

### Compteurs de performance pour la résolution des destinataires

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Nom du compteur</th>
<th>Nom complet</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>AmbiguousRecipientsTotal</p></td>
<td><p>Destinataires ambigus</p></td>
<td><p>Nombre total de destinataires ambigus détectés durant la résolution des destinataires. Des destinataires ambigus sont des destinataires différents qui ont des attributs Active Directory <strong>legacyExchangeDN</strong> ou <strong>proxyAddresses</strong> correspondants.</p></td>
</tr>
<tr class="even">
<td><p>AmbiguousSendersTotal</p></td>
<td><p>Expéditeurs ambigus</p></td>
<td><p>Nombre d'expéditeurs ambigus détectés durant la résolution des destinataires. Des expéditeurs ambigus sont des expéditeurs différents qui ont des attributs Active Directory <strong>legacyExchangeDN</strong> ou <strong>proxyAddresses</strong> correspondants.</p></td>
</tr>
<tr class="odd">
<td><p>FailedRecipientsTotal</p></td>
<td><p>Remise échouée aux destinataires</p></td>
<td><p>Nombre de remises échouées aux destinataires détectées durant la résolution des destinataires.</p></td>
</tr>
<tr class="even">
<td><p>LoopRecipientsTotal</p></td>
<td><p>Destinataires en boucle</p></td>
<td><p>Nombre de destinataires pour lesquels la résolution des destinataires a échoué en raison de boucles de destinataires.</p></td>
</tr>
<tr class="odd">
<td><p>MessagesChippedTotal</p></td>
<td><p>Messages fragmentés</p></td>
<td><p>Nombre total de copies du même message créées durant la résolution des destinataires pour contrôler le nombre de destinataires de l'enveloppe d'un message unique. Dans Exchange, ce processus est appelé <em>fragmentation</em>.</p></td>
</tr>
<tr class="even">
<td><p>MessagesCreatedTotal</p></td>
<td><p>Messages créés</p></td>
<td><p>Nombre de messages créés durant la résolution des destinataires.</p></td>
</tr>
<tr class="odd">
<td><p>MessagesRetriedTotal</p></td>
<td><p>Messages dont la remise a été retentée</p></td>
<td><p>Nombre de messages planifiés pour une nouvelle tentative durant la résolution des destinataires.</p></td>
</tr>
<tr class="even">
<td><p>UnresolvedOrgRecipientsTotal</p></td>
<td><p>Nombre de destinataires d'organisation non résolus</p></td>
<td><p>Nombre de destinataires non résolus d'un domaine faisant autorité détectés durant la résolution des destinataires.</p></td>
</tr>
<tr class="odd">
<td><p>UnresolvedOrgSendersTotal</p></td>
<td><p>Nombre d'expéditeurs d'organisation non résolus</p></td>
<td><p>Nombre d'expéditeurs non résolus d'un domaine faisant autorité détectés durant la résolution des destinataires.</p></td>
</tr>
</tbody>
</table>


## Événements de résolution des destinataires dans le journal de suivi des messages

Le tableau suivant décrit les événements de résolution des destinataires consignés dans le journal de suivi des messages.

### Événements de résolution des destinataires dans le journal de suivi des messages

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Événement de suivi des messages</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>EXPAND</p></td>
<td><p>Cet événement indique qu'un groupe de distribution a été développé.</p></td>
</tr>
<tr class="even">
<td><p>REDIRECT</p></td>
<td><p>Cet événement indique qu'un message envoyé à un destinataire de boîte aux lettres ou un destinataire de dossier public à extension messagerie a été redirigé vers un destinataire alternatif, comme spécifié par le paramètre <em>ForwardingAddress</em>.</p></td>
</tr>
<tr class="odd">
<td><p>RESOLVE</p></td>
<td><p>Cet événement indique que l'adresse de messagerie d'un destinataire a été remplacée par l'adresse de messagerie SMTP principale de l'objet destinataire Active Directory correspondant.</p></td>
</tr>
<tr class="even">
<td><p>TRANSFER</p></td>
<td><p>Cet événement indique qu'une bifurcation ou un fractionnement de message a eu lieu.</p></td>
</tr>
</tbody>
</table>


Pour plus d'informations sur le suivi des messages, consultez la rubrique [Suivi des messages](message-tracking-exchange-2013-help.md).

