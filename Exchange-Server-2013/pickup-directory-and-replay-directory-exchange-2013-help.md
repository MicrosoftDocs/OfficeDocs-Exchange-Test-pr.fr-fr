---
title: 'Répertoire de collecte et répertoire de relecture: Exchange 2013 Help'
TOCTitle: Répertoire de collecte et répertoire de relecture
ms:assetid: ae191700-953f-411c-906f-dc90feec3d5a
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb124230(v=EXCHG.150)
ms:contentKeyID: 50478991
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Répertoire de collecte et répertoire de relecture

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2016-12-09_

Par défaut, les répertoires de collecte et de relecture existent sur chaque serveur de boîtes aux lettres Microsoft Exchange Server 2013 ou serveur de transport Edge. Les fichiers de message électronique correctement mis en forme que vous copiez dans le répertoire de collecte ou de relecture sont soumis à des fins de remise. Le répertoire de collecte est utilisé par des administrateurs pour tester le flux de messagerie ou par des applications qui doivent créer et soumettre leurs propres messages. Le répertoire de relecture reçoit des messages de serveurs de passerelle étrangers et peut servir à déposer de nouveau des messages exportés par les administrateurs à partir des files d'attente de serveurs Exchange.

**Contenu de cette rubrique**

Anatomie d'un fichier de message électronique

Procédure de traitement des messages par les répertoires de collecte et de relecture

Conditions requises pour les fichiers de messages du répertoire de collecte

Modifications de l'en-tête des messages du répertoire de collecte

Conditions requises pour les fichiers de messages du répertoire de relecture

Modifications de l'en-tête des messages du répertoire de relecture

Défaillances dans le traitement des messages des répertoires de collecte et de relecture

Considérations de sécurité pour les répertoires de collecte et de relecture

Autorisations des répertoires de collecte et de relecture

## Anatomie d'un fichier de message électronique

Un message électronique SMTP standard est constitué d'une *enveloppe de message* et d'un contenu de message. L'enveloppe de message contient les informations requises pour la transmission et la remise du message. Le contenu du message comporte les champs d'en-tête de message (communément appelé l'*en-tête de message*) et le corps du message. L'enveloppe de message est décrite dans la spécification RFC 2821, et l'en-tête de message est décrit dans la spécification RFC 2822.

Quand un expéditeur rédige un message électronique et le soumet en vue de sa remise, le message contient les informations de base requises pour la conformité aux normes SMTP, telles que l'expéditeur, le destinataire, les date et heure de rédaction du message, une ligne d'objet facultative et un corps de message facultatif. Ces informations sont contenues dans le message proprement dit et, par définition, dans l'en-tête du message.

Le serveur de messagerie de l'expéditeur génère une enveloppe de message pour le message à l'aide des informations sur l'expéditeur et le destinataire disponibles dans l'en-tête de message, puis transmet le message sur Internet afin qu'il soit remis au serveur de messagerie du destinataire. Les destinataires ne voient jamais l'enveloppe du message, car elle est générée par le processus de transmission du message et ne fait pas partie du message.

Chaque serveur impliqué dans la transmission du message peut insérer des champs d'en-tête liés au rôle du serveur dans la remise du message, ou d'autres champs d'en-tête de message spécifiques aux applications. Lorsque le destinataire ouvre le message à l'aide d'un client de messagerie, ce dernier affiche certaines des informations les plus pertinentes de l'en-tête du message, telles que l'expéditeur, les destinataires et l'objet, avec le corps du message.

Retour au début

## Procédure de traitement des messages par les répertoires de collecte et de relecture

Dans Exchange 2013, l'emplacement par défaut du répertoire de collecte est `%ExchangeInstallPath%TransportRoles\Pickup`. L'emplacement par défaut du répertoire de relecture est `%ExchangeInstallPath%TransportRoles\Replay`. Quand un fichier de message .eml correctement mis en forme est copié dans le répertoire de collecte ou de relecture, les étapes de traitement en vue du dépôt du message sont les suivantes :

1.  Les répertoires de collecte et de relecture sont contrôlés toutes les cinq secondes pour voir s'ils contiennent de nouveaux fichiers de messages. Il n'est pas possible de modifier cette fréquence d'interrogation. Vous pouvez régler la vitesse de traitement des fichiers de messages à l'aide du paramètre *PickupDirectoryMaxMessagesPerMinute* avec la cmdlet **Set-TransportService**. Ce paramètre affecte le répertoire de collecte et le répertoire de relecture. La valeur par défaut est 100 messages par minute. Les fichiers qui ne peuvent pas être ouverts sont conservés dans le répertoire de collecte et réévalués lors de l'interrogation suivante.

2.  Certaines limites imposées aux fichiers de messages dans le répertoire de collecte (telles que la taille maximale de l'en-tête et le nombre maximal de destinataires) sont vérifiées. Par défaut, la taille maximale de l'en-tête est 64 kilo-octets (Ko), et le nombre maximal de destinataires est 100. Vous pouvez modifier ces limites à l'aide de la cmdlet **Set-TransportService**. Ces paramètres affectent uniquement le répertoire de collecte.

3.  Le fichier est renommé de *\<nom\_fichier\>*.eml en *\<nom\_fichier\>*.tmp. Si le fichier *\<nom\_fichier\>*.tmp existe déjà, le fichier est renommé *\<nom\_fichier\>\<date\_heure\>*.tmp. En cas d'échec de l'attribution d'un nouveau nom au fichier, une erreur du journal des événements est générée, et le processus de collecte passe au fichier suivant.

4.  Une fois le fichier .tmp converti en message électronique, une commande **delete on close** (suppression à la fermeture) est générée pour le fichier .tmp. Le fichier .tmp semble être conservé dans le répertoire de collecte, mais il ne peut pas être ouvert.

5.  Une fois le message placé en file d'attente en vue de sa remise, une commande de fermeture (**close**) est émise, et le fichier .tmp est supprimé du répertoire de collecte. En cas d'échec de la suppression, une erreur du journal des événements est générée. Si le service de transport de Microsoft Exchange redémarre alors que le répertoire de collecte contient des fichiers .tmp, ces derniers sont renommés en fichiers .eml et traités à nouveau. Cela pourrait aboutir au transfert de messages en double.

Retour au début

## Conditions requises pour les fichiers de messages du répertoire de collecte

Un fichier de message copié dans le répertoire de collecte doit remplir les conditions suivantes pour être remis :

  - Le fichier de message doit être un fichier texte conforme au format de message SMTP de base. Les champs d'en-tête de message MIME et leur contenu sont pris en charge.

  - Le fichier de message doit être doté d'une extension .eml.

  - Les champs d'en-tête de message `Sender` ou `From` doivent contenir au moins une adresse de messagerie. Si les champs `Sender` et `From` contiennent une seule adresse de messagerie, l'adresse de messagerie figurant dans le champ `From` est utilisée comme origine du message dans l'enveloppe de message.

  - Le champ `Sender` ne peut comporter qu'une seule adresse de messagerie. Les adresses de messagerie multiples ne sont pas autorisées. Le champ `Sender` est facultatif si le champ `From` ne contient qu'une seule adresse de messagerie.

  - Plusieurs adresses de messagerie sont autorisées dans le champ `From`, mais il ne peut y en avoir qu'une seule dans le champ `Sender`. L'adresse figurant dans le champ `Sender` est utilisée comme expéditeur du message dans l'enveloppe de message.

  - Au moins une adresse de messagerie doit figurer dans les champs `To`, `Cc` ou `Bcc`.

  - Une ligne vide doit être présente entre l'en-tête du message et le corps du message.

Cet exemple présente un message au format texte brut qui utilise une mise en forme valide pour le répertoire de collecte.

    To: mary@contoso.com
    From: bob@fabrikam.com
    Subject: Message subject
    
    This is the body of the message.

Le contenu MIME est également pris en charge dans les fichiers de messages du répertoire de collecte. Le standard MIME définit une part importante du contenu du message, notamment les langues qui ne peuvent pas être représentées sous forme de texte ASCII 7 bits, HTML ou d'autre contenu multimédia. La présente rubrique n'a pas pour but de fournir une description détaillée du standard MIME et de ses spécifications. Cet exemple présente un message MIME simple qui utilise une mise en forme valide pour le répertoire de collecte.

    To: mary@contoso.com
    From: bob@fabrikam.com
    Subject: Message subject
    MIME-Version: 1.0
    Content-Type: text/html; charset="iso-8859-1"
    Content-Transfer-Encoding: 7bit
    
    <HTML><BODY>
    <TABLE>
    <TR><TD>cell 1</TD><TD>cell 2</TD></TR>
    <TR><TD>cell 3</TD><TD>cell 4</TD></TR>
    </TABLE>

    </BODY></HTML>

Retour au début

## Modifications de l'en-tête des messages du répertoire de collecte

Le répertoire de collecte supprime les champs d'en-tête de message suivants de l'en-tête du message :

  - `Received`

  - `Resent-*`

  - `Bcc`
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Toutes les adresses de messagerie figurant dans les champs <code>Bcc</code> facultatifs de l'en-tête du message sont correctement traitées. Une fois les destinataires <code>Bcc</code> promus comme destinataires de l'enveloppe de message invisibles, ils sont supprimés de l'en-tête de message afin de protéger leur identité. Si un message contient uniquement des destinataires <code>Bcc</code>, la valeur <strong>Undisclosed Recipients</strong> est ajoutée au champ <code>To</code> dans l'en-tête du message.</td>
    </tr>
    </tbody>
    </table>


Le répertoire de collecte ajoute son propre champ d'en-tête `Received` dans un message dans le cadre du processus de dépôt du message. Le champ d'en-tête `Received` est appliqué selon le format suivant.

    Received: from localhost by Pickup with Microsoft SMTP Server id <ExchangeServerVersion><datetime>

Le répertoire de collecte modifie les champs d'en-tête suivants s'ils sont manquants ou incorrects :

  - **Message-Id**   Si le champ `Message-Id` est manquant ou vide, le répertoire de collecte ajoute un champ Message-Id au format *\<GUID\>*@*\<domaine\_par\_défaut\>*.

  - **Date**   Si le champ `Date` est manquant ou de format incorrect, le répertoire de collecte ajoute les date et l'heure auxquelles il a traité le message.

Retour au début

## Conditions requises pour les fichiers de messages du répertoire de relecture

Le répertoire de relecture est utilisé pour redéposer des messages Exchange exportés et recevoir les messages de serveurs de passerelle étrangers. Ces messages sont déjà mis en forme pour le répertoire de relecture. Il n'est pas vraiment utile que des administrateurs ou des applications rédigent et déposent les nouveaux fichiers de messages à l'aide du répertoire de relecture. Le répertoire de collecte doit être utilisé pour créer et soumettre les nouveaux fichiers de messages.

Les messages du répertoire de relecture sollicitent énormément les *en-têtes X*. Les en-têtes X sont les champs d'en-tête de message non officiels et définis par l'utilisateur qui sont présents dans l'en-tête de message. Les en-têtes X ne sont pas spécifiquement mentionnés dans la spécification RFC 2822, mais l'utilisation d'un champ d'en-tête de message non défini commençant par « X- » est à présent une méthode approuvée d'ajout de champs d'en-tête de message non officiels à un message. Les en-têtes X spécifiques d'Exchange utilisés dans les fichiers de messages du répertoire de relecture peuvent définir les informations de remise qui sont normalement incluses dans l'enveloppe de message. Cette fonctionnalité est requise pour conserver les informations du message d'origine lorsque vous utilisez le répertoire de relecture pour traiter des messages exportés à partir d'un autre serveur Exchange.

Un fichier de message copié dans le répertoire de relecture doit remplir les conditions suivantes pour être remis :

  - Le fichier de message doit être un fichier texte conforme au format de message SMTP de base. Les champs d'en-tête de message MIME et leur contenu sont pris en charge.

  - Le fichier de message doit être doté d'une extension .eml.

  - Les en-têtes X doivent apparaître devant les autres champs d'en-tête traditionnels.

  - Une ligne vide doit être présente entre les champs d'en-tête et le corps du message.

Les champs d'en-tête X décrits dans la liste suivante sont obligatoires pour les messages du répertoire de relecture :

  - **X-Sender**   Cet en-tête X remplace le champ d'en-tête de message `From` obligatoire dans un message SMTP classique. Au moins un champ `X-Sender` doit contenir une adresse de messagerie. Le répertoire de relecture ignore le champ d'en-tête de message `From` s'il est présent, même si le client de messagerie du destinataire affiche la valeur du champ d'en-tête `From` comme expéditeur du message. D'autres paramètres figurent généralement dans le champ `X-Sender`, comme le montre l'exemple suivant.
    
        X-Sender: <bob@fabrikam.com> BODY=7bit RET=HDRS ENVID=12345ABCD auth=<someAuth>
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Ces paramètres sont des valeurs d'enveloppe de message habituellement générées par le serveur d'envoi. Les fichiers de messages exportés contiennent des paramètres semblables.<br />
    <code>RET</code> indique si le message entier ou seuls les en-têtes doivent être renvoyés à l'expéditeur en cas de non-remise du message. <code>RET</code> peut avoir la valeur <code>HDRS</code> ou <code>FULL</code>. <code> ENVID</code> est un identificateur d'enveloppe de message. <code>BODY</code> spécifie le codage du texte du message. <code>auth</code> spécifie un mécanisme d'authentification pour le serveur de messagerie, comme décrit dans la spécification RFC 2554.</td>
    </tr>
    </tbody>
    </table>


  - **X-Receiver**   Cet en-tête X remplace le champ d'en-tête de message `To` obligatoire dans un message SMTP classique. Au moins un champ `X-Receiver` doit contenir une adresse de messagerie. Plusieurs champs d'en-tête `X-Receiver` sont autorisés pour plusieurs destinataires. Le répertoire de relecture ignore les champs d'en-tête de message `To` s'ils sont présents, même si le client de messagerie du destinataire affiche les valeurs des champs d'en-tête de message `To` comme expéditeurs du message. D'autres paramètres facultatifs peuvent figurer dans les champs `X-Receiver`, comme le montre l'exemple suivant.
    
        X-Receiver: <mary@contoso.com> NOTIFY=NEVER ORcpt=mary@contoso.com
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Ces paramètres sont des valeurs d'enveloppe de message habituellement générées par le serveur d'envoi. Les fichiers de messages exportés contiennent des paramètres semblables. Ces paramètres sont liés aux messages de notification d'état de remise (DNS), comme décrit dans la spécification RFC 1891.<br />
    <code>NOTIFY</code> peut avoir la valeur <code>NEVER</code>, <code>DELAY</code> ou <code>FAILURE</code>. <code>ORcpt</code> préserve le destinataire d'origine du message.</td>
    </tr>
    </tbody>
    </table>


Les champs d'en-tête X décrits dans la liste suivante sont facultatifs pour les fichiers de messages du répertoire de relecture :

  - **X-CreatedBy**   Utilisé pour la fonctionnalité de pare-feu d'en-tête. Si ce champ d'en-tête X existe, il ne doit pas être vide. Si le champ d'en-tête `X-CreatedBy` n'existe pas, il est ajouté avec la valeur **Unspecified**. Généralement, la valeur de ce champ est **MSExchange15**, mais il peut également contenir le type d'espace d'adressage non SMTP défini sur un connecteur d'envoi, tel que **Notes**.

  - **X-EndOfInjectedXHeaders**   Taille en octets de tous les en-têtes X présents. Cet en-tête X doit être utilisé comme marqueur pour indiquer le dernier en-tête X avant le début des champs d'en-tête de message classiques.

  - **X-ExtendedMessageProps**   Propriétés de message étendues du message.

  - **X-HeloDomain**   Chaîne de domaine HELO/EHLO présentée au cours de la conversation de protocole SMTP initiale.

  - **X-Source**   Utilisé par l'Afficheur des files d'attente sous la colonne **MessageSourceName**. Si la valeur de cet en-tête X n'est pas spécifiée, la valeur **Replay** est utilisée. Les autres valeurs possibles pour cet en-tête X sont **Smtp Receive Connector** et **Smtp Send Connector**.

  - **X-SourceIPAddress**   Adresse IP du serveur d'envoi. La valeur de ce champ est `0.0.0.0` si aucune adresse IP n'est indiquée.

Cet exemple présente un message au format texte brut qui utilise une mise en forme valide pour le répertoire de relecture.

    X-Receiver: <mary@contoso.com> NOTIFY=NEVER ORcpt=mary@contoso.com
    X-Sender: <bob@fabrikam.com> BODY=7bit ENVID=12345AB auth=<someAuth>
    Subject: Optional message subject
    
    This is the body of the message.

Le contenu MIME est également pris en charge pour les fichiers de messages du répertoire de relecture. Le standard MIME définit une part importante du contenu du message, notamment les langues qui ne peuvent pas être représentées sous forme de texte ASCII 7 bits, HTML ou d'autre contenu multimédia. La présente rubrique n'a pas pour but de fournir une description détaillée du standard MIME et de ses spécifications. Cet exemple présente un message MIME simple qui utilise une mise en forme valide pour le répertoire de relecture.

    X-Receiver: <mary@contoso.com> NOTIFY=NEVER ORcpt=mary@contoso.com
    X-Sender: <bob@fabrikam.com> BODY=7bit ENVID=12345ABCD auth=<someAuth>
    To: mary@contoso.com
    From: bob@fabrikam.com
    Subject: Optional message subject
    MIME-Version: 1.0
    Content-Type: text/html; charset="iso-8859-1"
    Content-Transfer-Encoding: 7bit
    
    <HTML><BODY>
    <TABLE>
    <TR><TD>cell 1</TD><TD>cell 2</TD></TR>
    <TR><TD>cell 3</TD><TD>cell 4</TD></TR>
    </TABLE>

    </BODY></HTML>

Retour au début

## Modifications de l'en-tête des messages du répertoire de relecture

Le répertoire de relecture supprime le champ d'en-tête de message`Bcc` du fichier de message.

Le répertoire de relecture ajoute son propre champ d'en-tête de message `Received` à un message dans le cadre du processus de dépôt. Le champ d'en-tête Received est appliqué selon le format suivant.

    Received: from <ReceivingServerName> by Replay with <ExchangeServerVersion><DateTime>

Le répertoire de relecture modifie les champs d'en-tête de message suivants dans l'en-tête de message :

  - **Message-ID**   Si ce champ d'en-tête de message est manquant ou vide, le répertoire de relecture ajoute un champ d'en-tête Message-ID au format *\<GUID\>*@*\<domaine\_par\_défaut\>*.

  - **Date**   Si ce champ d'en-tête de message est manquant ou incorrect, le répertoire de relecture ajoute le champ d'en-tête Date en utilisant la date et l'heure auxquelles le message a été traité par le répertoire de relecture.

Retour au début

## Défaillances dans le traitement des messages des répertoires de collecte et de relecture

Un fichier de message copié dans le répertoire de collecte ou de relecture peut ne pas être correctement placé en file d'attente en vue de sa remise. Les catégories d'erreur de remise de messages suivantes peuvent se présenter :

  - **Échecs de remise**   Un fichier de message correctement mis en forme et associé à un expéditeur valide qui ne peut pas être correctement déposé pour remise génère une notification d'échec de remise (NDR). Un contenu dont la mise en forme est incorrecte ou des violations de restrictions appliquées aux messages du répertoire de collecte peuvent également générer une notification d'échec de remise. Quand une notification d'échec de remise (NDR) est générée durant le traitement d'un message, le fichier de message d'origine est joint au message NDR, puis supprimé du répertoire de collecte ou de relecture.
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>La remise d'un message correctement mis en forme déposé dans le pipeline de transport peut échouer ultérieurement. Le message est alors renvoyé à l'expéditeur, accompagné d'une NDR. Ce type de défaillance peut être dû à des problèmes de transmission non liés aux répertoires de collecte ou de relecture, tels qu'une défaillance d'un serveur de messagerie ou un problème de routage sur le chemin de remise du message.</td>
    </tr>
    </tbody>
    </table>


  - **Message incorrect**   Un message classé comme *message incorrect* présente des problèmes graves qui empêchent le dépôt du message en vue de sa remise par le répertoire de collecte ou de relecture. Un problème de message incorrect peut également survenir lorsque le message est correctement mis en forme mais que les destinataires ne sont pas valides et qu'un message de notification d'échec de remise ne peut pas être envoyé à l'expéditeur car ce dernier n'est pas valide.
    
    Les fichiers de messages identifiés comme messages incorrects sont conservés dans le répertoire de collecte ou de relecture et renommés de *\<nom\_fichier\>*.eml en *\<nom\_fichier\>*.bad. Si le fichier *\<nom\_fichier\>*.bad existe déjà, le fichier est renommé *\<nom\_fichier\>\<date\_heure\>*.bad. Si le répertoire de collecte ou de relecture contient des messages incorrects, une erreur est générée dans le journal des événements, mais les mêmes messages incorrects ne génèrent pas d'erreurs répétées dans le journal des événements.
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Composez et enregistrez toujours les fichiers de messages dans un autre emplacement avant de les copier dans le répertoire de collecte pour remise. Le répertoire de collecte est interrogé toutes les cinq secondes pour identifier la présence de nouveaux messages. Par conséquent, si vous tentez de composer et d'enregistrer les fichiers de messages dans le répertoire de collecte proprement dit, ce dernier peut essayer de traiter les fichiers de messages avant que vous ayez terminé de les composer.</td>
    </tr>
    </tbody>
    </table>


Retour au début

## Considérations de sécurité pour les répertoires de collecte et de relecture

La liste suivante décrit les problèmes de sécurité courants liés au répertoire de collecte et au répertoire de relecture :

  - Les contrôles de sécurité configurés sur un connecteur de réception, tels que les opérations de blocage du courrier indésirable et des programmes malveillants, ou de filtrage des expéditeurs et des destinataires, ne sont pas exécutés sur les messages déposés via les répertoires de collecte ou de relecture.

  - Un répertoire de collecte ou de relecture compromis peut agir comme un relais ouvert. Les messages peuvent être soumis de nouveau ou *relayés* à l'aide d'un autre serveur pour masquer la source véritable des messages.

La liste suivante décrit d'autres problèmes de sécurité s'appliquant au répertoire de relecture :

  - Les champs d'en-tête X utilisés par le répertoire de relecture permettent la création manuelle de l'enveloppe de message. Les informations des champs `X-Sender` et `X-Receiver` peuvent être totalement différentes de celles des champs d'en-tête de message `To` ou `From` affichées par les clients de messagerie. L'action consistant à emprunter l'identité d'un expéditeur et d'un domaine est souvent appelée *falsification*. Un *courrier falsifié* est un message électronique dont l'adresse d'expéditeur a été modifiée pour qu'il semble provenir d'un expéditeur autre que l'expéditeur réel du message.

  - Si la valeur du champ `X-CreatedBy` est **MSExchange15**, la destination est considérée comme fiable, et aucun pare-feu d'en-tête n'est appliqué. Un *pare-feu d'en-tête* est un dispositif permettant à Exchange de conserver les en-têtes X dans les messages transmis entre des serveurs Exchange approuvés, ou de supprimer les en-têtes X susceptibles de divulguer des informations des messages transmis à des destinations non approuvées en dehors de l'organisation Exchange. Ces en-têtes X permettent de partager des informations d'Exchange, telles que le seuil de probabilité de courrier indésirable, la signature des messages ou le chiffrement entre des serveurs Exchange autorisés. La divulgation de ces informations à des sources non autorisées peut constituer un risque pour la sécurité. Pour plus d'informations sur le pare-feu d'en-tête, consultez la rubrique [Présentation du pare-feu d'en-tête](https://go.microsoft.com/fwlink/?linkid=268394).

Une sécurité renforcée doit être appliquée au répertoire de relecture en raison des risques de sécurité supplémentaires associés au répertoire de relecture. Les utilisateurs ou applications devant générer et soumettre des messages peuvent être autorisés à accéder au répertoire de collecte, mais ils n'ont pas besoin d'accéder au répertoire de relecture.

Les répertoires de collecte et de relecture sont activés par défaut sur tous les serveurs de boîtes aux lettres et de transport Edge. Si le répertoire de collecte ou de relecture n'est pas requis sur un serveur de boîtes aux lettres ou de transport Edge de votre organisation, vous pouvez le désactiver sur ce serveur en attribuant la valeur `$null` au chemin d'accès au répertoire de collecte ou de relecture. Pour plus d'informations, consultez la rubrique [Configurer le répertoire de collecte et le répertoire de relecture](configure-the-pickup-directory-and-the-replay-directory-exchange-2013-help.md).

Retour au début

## Autorisations des répertoires de collecte et de relecture

Les autorisations suivantes sont obligatoires sur les répertoires de collecte et de relecture :

  - Administrateur : contrôle total

  - Système : contrôle total

  - Service réseau : lecture, écriture et suppression de sous-dossiers et fichiers

Par défaut, le service de transport de Microsoft Exchange utilise les informations d'identification de sécurité du compte d'utilisateur de service réseau pour gérer l'emplacement et les autorisations des répertoires de collecte et de relecture. Le compte de service réseau doit disposer de ces autorisations sur le répertoire de collecte de façon à ce que les fichiers .eml puissent être ouverts, renommés en fichiers .tmp et supprimés, ou renommés en fichiers .bad si le message est classé comme message incorrect.

Vous pouvez modifier l'emplacement de ces répertoires à l'aide des paramètres *PickupDirectoryPath* et *ReplayDirectoryPath* de la cmdlet **Set-TransportService**. Le déplacement effectif du répertoire de collecte dépend des droits attribués au compte de service réseau au nouvel emplacement du répertoire de collecte, et de l'existence du nouveau répertoire de collecte. Si le répertoire n'existe pas et que le compte de service réseau dispose des droits nécessaires à la création de dossiers et à l'application d'autorisations au nouvel emplacement, le répertoire est créé et les autorisations appropriées lui sont appliquées. Si le nouveau répertoire existe, les autorisations d'accès au dossier ne sont pas vérifiées. Chaque fois que vous modifiez l'emplacement des répertoires à l'aide du paramètre *PickupDirectoryPath* ou *ReplayDirectoryPath* avec la cmdlet **Set-TransportService**, vérifiez systématiquement que le nouveau répertoire existe et que les autorisations appropriées lui sont appliquées.

Retour au début

