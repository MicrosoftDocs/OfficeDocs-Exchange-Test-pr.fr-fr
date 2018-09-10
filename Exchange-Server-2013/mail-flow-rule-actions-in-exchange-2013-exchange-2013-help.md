---
title: 'Actions de règle de transport: Exchange 2013 Help'
TOCTitle: Actions de règle de flux de messagerie
ms:assetid: 5d11a955-b1cc-4150-a0b9-a8cc48ba9bde
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Aa998315(v=EXCHG.150)
ms:contentKeyID: 50478178
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Actions de règle de transport

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2017-05-03_

Les actions de règles de flux de messagerie (également nommées règles de transport) spécifient ce que vous voulez faire des messages qui répondent aux conditions de la règle. Par exemple, vous pouvez créer une règle qui transfère les messages d’expéditeurs spécifiques à un modérateur, ou ajoute une clause d’exclusion de responsabilité ou une signature personnalisée à tous les messages sortants.

Les actions nécessitent généralement des propriétés supplémentaires. Par exemple, lorsque la règle redirige un message, vous devez indiquer où rediriger celui-ci. Certaines actions ont plusieurs propriétés, disponibles ou obligatoires. Par exemple, lorsque la règle ajoute un champ d’en-tête à l’en-tête du message, vous devez spécifier le nom et la valeur de l’en-tête. Lorsque la règle ajoute une clause d’exclusion de responsabilité aux messages, vous devez spécifier le texte de l’exclusion, mais aussi indiquer où insérer le texte ou ce qu’il faut faire si la clause d’exclusion ne peut pas être ajoutée au message. En règle générale, vous pouvez configurer plusieurs actions dans une règle, mais certaines actions sont exclusives. Par exemple, une règle ne peut pas rejeter et rediriger un même message.

Pour plus d’informations sur les règles de flux de messagerie dans Exchange Server 2013, consultez la rubrique [Règles de transport ou de flux de messagerie](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md).

Pour plus d’informations sur les conditions et les exceptions des règles de flux de messagerie, consultez la rubrique [Conditions de règles de transport (prédicats)](mail-flow-rule-conditions-and-exceptions-predicates-in-exchange-2013-exchange-2013-help.md).

Pour plus d’informations sur les actions de règles de flux de messagerie dans Exchange Online ou Exchange Online Protection, consultez la rubrique [Courrier des actions de règle de flux dans Exchange en ligne](https://technet.microsoft.com/fr-fr/library/jj919237\(v=exchg.150\)) ou [Envoyer par courrier électronique les actions de règle de flux dans Exchange Online Protection](https://technet.microsoft.com/fr-fr/library/jj920117\(v=exchg.150\)).

## Actions des règles de flux de messagerie sur des serveurs de boîte aux lettres

Les actions disponibles dans les règles de flux de messagerie sur des serveurs de boîte aux lettres sont décrites dans le tableau suivant. Les valeurs valides de chaque propriété sont décrites dans la section Valeurs des propriétés.

**Remarques** :

  - Après avoir sélectionné une action dans le Centre d’administration Exchange (CAE), la valeur qui apparaît en fin de compte dans le champ **Effectuer les opérations suivantes** diffère souvent du chemin d’accès que vous avez sélectionné. Par ailleurs, lorsque vous créez des règles, vous pouvez parfois (en fonction de vos sélections) sélectionner un nom d’action court dans un modèle (une liste d’actions filtrée) au lieu de suivre le chemin d’accès complet. Les noms courts et les valeurs de chemin d’accès complet sont affichés dans la colonne CAE du tableau.

  - Les noms de certaines des actions qui sont renvoyées par la cmdlet **Get-TransportRuleAction** diffèrent des noms des paramètres correspondants et plusieurs paramètres peuvent être nécessaires pour une action.


<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>Action dans le centre d’administration Exchange</th>
<th>Paramètre d’action dans l’Environnement de ligne de commande Exchange Management Shell</th>
<th>Propriété</th>
<th>Description</th>
<th>Disponible dans</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Transférer le message pour approbation à ces personnes</strong></p>
<p><strong>Transférer le message pour approbation</strong> &gt; <strong>à ces personnes</strong></p></td>
<td><p><em>ModerateMessageByUser</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p>Transfère le message aux modérateurs spécifiés en tant que pièce jointe incluse dans une demande d’approbation. Pour plus d’informations, consultez la rubrique <a href="https://docs.microsoft.com/fr-fr/exchange/security-and-compliance/mail-flow-rules/common-message-approval-scenarios">Scénarios courants d’approbation des messages</a>. Vous ne pouvez pas utiliser un groupe de distribution en tant que modérateur.</p></td>
<td><p>Exchange 2010 ou version ultérieure</p></td>
</tr>
<tr class="even">
<td><p><strong>Transférer le message pour approbation au gestionnaire de l’expéditeur</strong></p>
<p><strong>Transférer le message pour approbation</strong> &gt; <strong>au gestionnaire de l’expéditeur</strong></p></td>
<td><p><em>ModerateMessageByManager</em></p></td>
<td><p>s/o</p></td>
<td><p>Transférer le message pour approbation au responsable de l’expéditeur</p>
<p>Cette action fonctionne uniquement si l’attribut <strong>Manager</strong> de l’expéditeur est défini dans Active Directory. Dans le cas contraire, le message est remis aux destinataires sans modération.</p></td>
<td><p>Exchange 2010 ou version ultérieure</p></td>
</tr>
<tr class="odd">
<td><p><strong>Rediriger le message vers ces destinataires</strong></p>
<p><strong>Rediriger le message vers</strong> &gt; <strong>ces destinataires</strong></p></td>
<td><p><em>RedirectMessageTo</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p>Redirige le message vers les destinataires spécifiés. Le message n’est pas remis aux destinataires d’origine et aucune notification n’est envoyée à l’expéditeur ou aux destinataires d’origine.</p></td>
<td><p>Exchange 2007 ou version ultérieure</p></td>
</tr>
<tr class="even">
<td><p><strong>Rejeter le message avec l’explication</strong></p>
<p><strong>Bloquer le message</strong> &gt; <strong>rejeter le message et inclure une explication</strong></p></td>
<td><p><em>RejectMessageReasonText</em></p></td>
<td><p><code>String</code></p></td>
<td><p>Renvoie le message à l’expéditeur dans une notification d’échec de remise (également appelée notification de non-remise) avec le texte spécifié comme raison de rejet. Le destinataire ne reçoit ni le message d’origine ni la notification.</p>
<p>Le code d’état étendu utilisé par défaut est <code>5.7.1</code>.</p>
<p>Lorsque vous créez ou modifiez la règle dans l’Environnement de ligne de commande Exchange Management Shell, vous pouvez spécifier le code DSN à l’aide du paramètre <em>RejectMessageEnhancedStatusCode</em>.</p></td>
<td><p>Exchange 2007 ou version ultérieure</p></td>
</tr>
<tr class="odd">
<td><p><strong>Rejeter le message avec le code d’état amélioré</strong></p>
<p><strong>Bloquer le message</strong> &gt; <strong>rejeter le message avec le code d’état amélioré de</strong></p></td>
<td><p><em>RejectMessageEnhancedStatusCode</em></p></td>
<td><p><code>DSNEnhancedStatusCode</code></p></td>
<td><p>Renvoie le message à l’expéditeur dans une notification d’échec de remise avec le code de notification d’état de remise DSN étendu spécifié. Le destinataire ne reçoit ni le message d’origine ni la notification.</p>
<p>Les codes DSN valides sont <code>5.7.1</code> ou <code>5.7.900</code>, jusqu’à <code>5.7.999</code>.</p>
<p>Le texte de motif par défaut utilisé est <code>Delivery not authorized, message refused</code>.</p>
<p>Lorsque vous créez ou modifiez la règle dans l’Environnement de ligne de commande Exchange Management Shell, vous pouvez spécifier le texte du motif du rejet à l’aide du paramètre <em>RejectMessageReasonText</em>.</p></td>
<td><p>Exchange 2007 ou version ultérieure</p></td>
</tr>
<tr class="even">
<td><p><strong>Supprimer le message sans avertir personne</strong></p>
<p><strong>Bloquer le message</strong> &gt; <strong>Supprimer le message sans avertir personne</strong></p></td>
<td><p><em>DeleteMessage</em></p></td>
<td><p>s/o</p></td>
<td><p>Supprime silencieusement le message sans envoyer de notification au destinataire ou à l’expéditeur.</p></td>
<td><p>Exchange 2007 ou version ultérieure</p></td>
</tr>
<tr class="odd">
<td><p><strong>Ajouter des destinataires dans le champ Cci</strong></p>
<p><strong>Ajouter des destinataires</strong> &gt; <strong>dans la zone Cci</strong></p></td>
<td><p><em>BlindCopyTo</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p>Ajoute un ou plusieurs destinataires dans le champ <strong>Bcc</strong> du message. Les destinataires originaux ne sont pas informés et ne peuvent pas voir les adresses supplémentaires.</p></td>
<td><p>Exchange 2007 ou version ultérieure</p></td>
</tr>
<tr class="even">
<td><p><strong>Ajouter des destinataires dans la zone À</strong></p>
<p><strong>Ajouter des destinataires</strong> &gt; <strong>dans la zone À</strong></p></td>
<td><p><em>AddToRecipients</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p>Ajoute un ou plusieurs destinataires dans le champ <strong>To</strong> du message. Les destinataires originaux peuvent voir les adresses supplémentaires.</p></td>
<td><p>Exchange 2007 ou version ultérieure</p></td>
</tr>
<tr class="odd">
<td><p><strong>Ajouter des destinataires dans le champ Cc</strong></p>
<p><strong>Ajouter des destinataires</strong> &gt; <strong>dans la zone Cc</strong></p></td>
<td><p><em>CopyTo</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p>Ajoute un ou plusieurs destinataires dans le champ <strong>Cc</strong> du message. Les destinataires originaux peuvent voir l’adresse supplémentaire.</p></td>
<td><p>Exchange 2007 ou version ultérieure</p></td>
</tr>
<tr class="even">
<td><p><strong>Ajouter le gestionnaire de l’expéditeur comme destinataire</strong></p>
<p><strong>Ajouter des destinataires</strong> &gt; <strong>ajouter le responsable de l’expéditeur en tant que destinataire</strong></p></td>
<td><p><em>AddManagerAsRecipientType</em></p></td>
<td><p><code>AddedManagerAction</code></p></td>
<td><p>Ajoute le responsable de l’expéditeur au message en tant que type de destinataire spécifié (<strong>To</strong>, <strong>Cc</strong>, <strong>Bcc</strong>) ou redirige vers le responsable de l’expéditeur sans notification à l’expéditeur ou au destinataire.</p>
<p>Cette action fonctionne uniquement si l’attribut <strong>Manager</strong> de l’expéditeur est défini dans Active Directory.</p></td>
<td><p>Exchange 2010 ou version ultérieure</p></td>
</tr>
<tr class="odd">
<td><p><strong>Ajouter une exclusion de responsabilité</strong></p>
<p><strong>Appliquer une clause d’exclusion de responsabilité au message</strong> &gt; <strong>ajouter une exclusion de responsabilité</strong></p></td>
<td><p><em>ApplyHtmlDisclaimerText</em></p>
<p><em>ApplyHtmlDisclaimerFallbackAction</em></p>
<p><em>ApplyHtmlDisclaimerTextLocation</em></p></td>
<td><p>Première propriété : <code>DisclaimerText</code></p>
<p>Deuxième propriété : <code>DisclaimerFallbackAction</code></p>
<p>Troisième propriété (Environnement de ligne de commande Exchange Management Shell uniquement) : <code>DisclaimerTextLocation</code></p></td>
<td><p>S’applique à la clause d’exclusion de responsabilité HTML spécifiée à la fin du message.</p>
<p>Lorsque vous créez ou modifiez la règle dans l’Environnement de ligne de commande Exchange Management Shell, utilisez le paramètre <em>ApplyHtmlDisclaimerTextLocation</em> avec la valeur <code>Append</code>.</p></td>
<td><p>Exchange 2007 ou version ultérieure</p></td>
</tr>
<tr class="even">
<td><p><strong>Ajouter un préfixe à la clause d’exclusion de responsabilité</strong></p>
<p><strong>Appliquer une clause d’exclusion de responsabilité au message</strong> &gt; <strong>ajouter une clause d’exclusion de responsabilité</strong></p></td>
<td><p><em>ApplyHtmlDisclaimerText</em></p>
<p><em>ApplyHtmlDisclaimerFallbackAction</em></p>
<p><em>ApplyHtmlDisclaimerTextLocation</em></p></td>
<td><p>Première propriété : <code>DisclaimerText</code></p>
<p>Deuxième propriété : <code>DisclaimerFallbackAction</code></p>
<p>Troisième propriété (Environnement de ligne de commande Exchange Management Shell uniquement) : <code>DisclaimerTextLocation</code></p></td>
<td><p>S’applique à la clause d’exclusion de responsabilité HTML spécifiée au début du message.</p>
<p>Lorsque vous créez ou modifiez la règle dans l’Environnement de ligne de commande Exchange Management Shell, utilisez le paramètre <em>ApplyHtmlDisclaimerTextLocation</em> avec la valeur <code>Prepend</code>.</p>
<p></p></td>
<td><p>Exchange 2007 ou version ultérieure</p></td>
</tr>
<tr class="odd">
<td><p><strong>Supprimer cet en-tête</strong></p>
<p><strong>Modifier les propriétés des messages</strong> &gt; <strong>supprimer un en-tête de message</strong></p></td>
<td><p><em>RemoveHeader</em></p></td>
<td><p><code>MessageHeaderField</code></p></td>
<td><p>Supprime le champ d’en-tête spécifié de l’en-tête de message.</p></td>
<td><p>Exchange 2007 ou version ultérieure</p></td>
</tr>
<tr class="even">
<td><p><strong>Attribuer cette valeur à l’en-tête du message</strong></p>
<p><strong>Modifier les propriétés des messages</strong> &gt; <strong>définir un en-tête de message</strong></p></td>
<td><p><em>SetHeaderName</em></p>
<p><em>SetHeaderValue</em></p></td>
<td><p>Première propriété : <code>MessageHeaderField</code></p>
<p>Deuxième propriété : <code>String</code></p></td>
<td><p>Ajoute ou modifie le champ d’en-tête spécifié dans l’en-tête du message et définit le champ d’en-tête sur la valeur spécifiée.</p></td>
<td><p>Exchange 2007 ou version ultérieure</p></td>
</tr>
<tr class="odd">
<td><p><strong>Appliquer une classification des messages</strong></p>
<p><strong>Modifier les propriétés des messages</strong> &gt; <strong>appliquer une classification des messages</strong></p></td>
<td><p><em>ApplyClassification</em></p></td>
<td><p><code>MessageClassification</code></p></td>
<td><p>Applique la classification des messages spécifiée au message.</p></td>
<td><p>Exchange 2007 ou version ultérieure</p></td>
</tr>
<tr class="even">
<td><p><strong>Définir le seuil de probabilité de courrier indésirable (SCL) sur</strong></p>
<p><strong>Modifier les propriétés des messages</strong> &gt; <strong>définir le seuil de probabilité de courrier indésirable (SCL)</strong></p></td>
<td><p><em>SetSCL</em></p></td>
<td><p><code>SCLValue</code></p></td>
<td><p>Définit le seuil de probabilité de courrier indésirable (SCL) du message sur la valeur spécifiée.</p></td>
<td><p>Exchange 2007 ou version ultérieure</p></td>
</tr>
<tr class="odd">
<td><p><strong>Appliquer la protection des droits au message avec</strong></p>
<p><strong>Modifier la sécurité du message</strong> &gt; <strong>appliquer la protection des droits</strong></p></td>
<td><p><em>ApplyRightsProtectionTemplate</em></p></td>
<td><p><code>RMSTemplate</code></p></td>
<td><p>Applique le modèle RMS (Rights Management Services) spécifié au message.</p>
<p>RMS nécessite des licences d’accès au client (CAL) Exchange Entreprise pour chaque boîte aux lettres. Pour plus d’informations sur les CAL, consultez <a href="https://go.microsoft.com/fwlink/p/?linkid=237292">Gestion des licences Exchange Server</a>.</p></td>
<td><p>Exchange 2010 ou version ultérieure</p></td>
</tr>
<tr class="even">
<td><p><strong>Demander un chiffrement TLS</strong></p>
<p><strong>Modifier la sécurité du message</strong> &gt; <strong>exiger le chiffrement TLS</strong></p></td>
<td><p><em>RouteMessageOutboundRequireTls</em></p></td>
<td><p><code>n/a</code></p></td>
<td><p>Force le routage des messages sortants via une connexion chiffrée par TLS.</p></td>
<td><p>Exchange 2013 ou version ultérieure</p></td>
</tr>
<tr class="odd">
<td><p><strong>Ajouter à l'objet du message le préfixe</strong></p></td>
<td><p><em>PrependSubject</em></p></td>
<td><p><code>String</code></p></td>
<td><p>Ajoute le texte spécifié au début du champ <strong>Subject</strong> du message. Envisagez d’utiliser un espace ou un signe deux-points (:) comme dernier caractère du texte spécifié pour le différencier du texte de l’objet d’origine.</p>
<p>Pour empêcher que la même chaîne soit ajoutée aux messages qui contiennent déjà le texte de l’objet (par exemple, dans les réponses), ajoutez l’exception <strong>L’objet inclut</strong> (<em>ExceptIfSubjectContainsWords</em>) à la règle.</p></td>
<td><p>Exchange 2007 ou version ultérieure</p></td>
</tr>
<tr class="even">
<td><p><strong>Avertir l'expéditeur à l'aide d'un conseil de stratégie</strong></p></td>
<td><p><em>NotifySender</em></p>
<p><em>RejectMessageReasonText</em></p>
<p><em>RejectMessageEnhancedStatusCode</em> (Environnement de ligne de commande Exchange Management Shell uniquement)</p></td>
<td><p>Première propriété : <code>NotifySenderType</code></p>
<p>Deuxième propriété : <code>String</code></p>
<p>Troisième propriété (Environnement de ligne de commande Exchange Management Shell uniquement) : <code>DSNEnhancedStatusCode</code></p></td>
<td><p>Avertit l’expéditeur ou bloque le message lorsque celui-ci correspond à une stratégie DLP.</p>
<p>Lors de l’utilisation de cette action, vous devez utiliser la condition <strong>Le message contient des informations sensibles</strong> (<em>MessageContainsDataClassification</em>).</p>
<p>Lorsque vous créez ou modifiez la règle dans l’Environnement de ligne de commande Exchange Management Shell, le paramètre <em>RejectMessageReasonText</em> est facultatif. Si vous n’utilisez pas ce paramètre, le texte par défaut <code>Delivery not authorized, message refused</code> est utilisé.</p>
<p>Dans l’Environnement de ligne de commande Exchange Management Shell, vous pouvez également utiliser le paramètre <em>RejectMessageEnhancedStatusCode</em> pour spécifier le code d’état amélioré. Si vous n’utilisez pas ce paramètre, le code d’état amélioré <code>5.7.1</code> est utilisé.</p>
<p>Cette action limite les autres conditions, exceptions et actions que vous pouvez configurer dans la règle.</p></td>
<td><p>Exchange 2013 ou version ultérieure</p></td>
</tr>
<tr class="odd">
<td><p><strong>Générer un rapport d'incident et l'envoyer à</strong></p></td>
<td><p><em>GenerateIncidentReport</em></p>
<p><em>IncidentReportContent</em></p></td>
<td><p>Première propriété : <code>Addresses</code></p>
<p>Deuxième propriété : <code>IncidentReportContent</code></p></td>
<td><p>Envoie un rapport d’incident qui contient le contenu spécifié aux destinataires spécifiés.</p>
<p>Un rapport d’incident est généré pour les messages qui correspondent aux stratégies de protection contre la perte de données dans votre organisation.</p></td>
<td><p>Exchange 2013 ou version ultérieure</p></td>
</tr>
<tr class="even">
<td><p><strong>Avertir le destinataire avec un message</strong></p></td>
<td><p><em>GenerateNotification</em></p></td>
<td><p><code>NotificationMessageText</code></p></td>
<td><p>Spécifie le texte, les balises HTML et les mots clés de message à inclure dans le message de notification envoyé aux destinataires du message. Par exemple, vous pouvez informer les destinataires que le message a été rejeté par la règle, ou marqué comme courrier indésirable et envoyé dans leur dossier Courrier indésirable.</p></td>
<td><p>Exchange 2013 ou version ultérieure</p></td>
</tr>
<tr class="odd">
<td><p>Section <strong>Propriétés de cette règle</strong> &gt; <strong>Auditer cette règle avec le niveau de gravité</strong></p></td>
<td><p><em>SetAuditSeverity</em></p></td>
<td><p><code>AuditSeverityLevel</code></p></td>
<td><p>Indique s’il faut :</p>
<ul>
<li><p>empêcher la génération d’un rapport d’incident et de l’entrée correspondante dans le journal de suivi des messages ;</p></li>
<li><p>générer un rapport d’incident et l’entrée correspondante dans le journal de suivi des messages avec le niveau de gravité spécifié (faible, moyenne ou élevée).</p></li>
</ul></td>
<td><p>Exchange 2013 ou version ultérieure</p></td>
</tr>
<tr class="even">
<td><p>Section <strong>Propriétés de cette règle</strong> &gt; <strong>Ne plus traiter de règles</strong></p>
<p><strong>Autres options</strong> &gt; section <strong>Propriétés de cette règle</strong> &gt; <strong>Ne plus traiter de règles</strong></p></td>
<td><p><em>StopRuleProcessing</em></p></td>
<td><p>s/o</p></td>
<td><p>Spécifie qu’une fois le message affecté par la règle, celui-ci est exempt de traitement par d’autres règles.</p></td>
<td><p>Exchange 2013 ou version ultérieure</p></td>
</tr>
</tbody>
</table>


Retour au début

## Actions des règles de flux de messagerie sur des serveurs de transport Edge

Un petit sous-ensemble des actions disponibles sur les serveurs de boîte aux lettres sont également disponibles sur les serveurs de transport Edge, mais certaines actions sont également disponibles uniquement sur les serveurs de transport Edge. Il n’y a aucun CAE sur les serveurs de transport Edge ; en l’occurrence, vous pouvez uniquement gérer les règles de flux de messagerie dans l’Environnement de ligne de commande Exchange Management Shell du serveur de transport Edge local. Ces actions sont décrites dans le tableau suivant : Les types de propriétés sont décrits dans la section Valeurs des propriétés.


<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>Paramètre d’action dans l’Environnement de ligne de commande Exchange Management Shell</th>
<th>Propriété</th>
<th>Description</th>
<th>Disponible sur</th>
<th>Disponible dans</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>AddToRecipients</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p>Ajoute un ou plusieurs destinataires dans le champ <strong>To</strong> du message. Les destinataires originaux peuvent voir les adresses supplémentaires.</p></td>
<td><p>Serveurs de boîtes aux lettres et serveurs de transport Edge</p></td>
<td><p>Exchange 2007 ou version ultérieure</p></td>
</tr>
<tr class="even">
<td><p><em>BlindCopyTo</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p>Ajoute un ou plusieurs destinataires dans le champ <strong>Bcc</strong> du message. Les destinataires originaux ne sont pas informés et ne peuvent pas voir les adresses supplémentaires.</p></td>
<td><p>Serveurs de boîtes aux lettres et serveurs de transport Edge</p></td>
<td><p>Exchange 2007 ou version ultérieure</p></td>
</tr>
<tr class="odd">
<td><p><em>CopyTo</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p>Ajoute un ou plusieurs destinataires dans le champ <strong>Cc</strong> du message. Les destinataires originaux peuvent voir l’adresse supplémentaire.</p></td>
<td><p>Serveurs de boîtes aux lettres et serveurs de transport Edge</p></td>
<td><p>Exchange 2007 ou version ultérieure</p></td>
</tr>
<tr class="even">
<td><p><em>DeleteMessage</em></p></td>
<td><p>s/o</p></td>
<td><p>Supprime silencieusement le message sans envoyer de notification au destinataire ou à l’expéditeur.</p></td>
<td><p>Serveurs de boîtes aux lettres et serveurs de transport Edge</p></td>
<td><p>Exchange 2007 ou version ultérieure</p></td>
</tr>
<tr class="odd">
<td><p><em>Disconnect</em></p></td>
<td><p>s/o</p></td>
<td><p>Met fin à la connexion SMTP entre le serveur d’envoi et le serveur de transport Edge sans générer de notification d’échec de remise.</p></td>
<td><p>Serveurs de transport Edge uniquement</p></td>
<td><p>Exchange 2007 ou version ultérieure</p></td>
</tr>
<tr class="even">
<td><p><em>LogEventText</em></p></td>
<td><p><code>String</code></p></td>
<td><p>Génère un événement avec le texte spécifié dans le journal d’application du serveur de transport Edge local. L’entrée contient les informations suivantes :</p>
<ul>
<li><p><strong>Niveau</strong> <code>Information</code></p></li>
<li><p><strong>Source</strong> <code>MSExchange Messaging Policies</code></p></li>
<li><p><strong>ID d’événement</strong> <code>4000</code></p></li>
<li><p><strong>Catégorie de la tâche</strong> <code>Rules</code></p></li>
<li><p><strong>EventData</strong> <code>The following message is logged by an action in the rules: &lt;text you specify&gt;.</code></p></li>
</ul></td>
<td><p>Serveurs de transport Edge uniquement</p></td>
<td><p>Exchange 2007 ou version ultérieure</p></td>
</tr>
<tr class="odd">
<td><p><em>PrependSubject</em></p></td>
<td><p><code>String</code></p></td>
<td><p>Ajoute le texte spécifié au début du champ <strong>Subject</strong> du message. Envisagez d’utiliser un espace ou un signe deux-points (:) comme dernier caractère du texte spécifié pour le différencier de l’objet d’origine.</p></td>
<td><p>Serveurs de boîtes aux lettres et serveurs de transport Edge</p></td>
<td><p>Exchange 2007 ou version ultérieure</p></td>
</tr>
<tr class="even">
<td><p><em>Quarantine</em></p></td>
<td><p>s/o</p></td>
<td><p>Achemine le message vers la boîte aux lettres de mise en quarantaine définie dans la configuration de filtrage de contenu du serveur de transport Edge. Pour plus d’informations, consultez la rubrique <a href="configure-a-spam-quarantine-mailbox-exchange-2013-help.md">Configuration d’une boîte aux lettres de mise en quarantaine du courrier indésirable</a>.</p>
<p>Si la boîte aux lettres de mise en quarantaine n’est pas configurée, le message est renvoyé à l’expéditeur dans une notification d’échec de remise.</p></td>
<td><p>Serveurs de transport Edge uniquement</p></td>
<td><p>Exchange 2010 ou version ultérieure</p></td>
</tr>
<tr class="odd">
<td><p><em>RedirectMessageTo</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p>Redirige le message vers les destinataires spécifiés. Le message n’est pas remis aux destinataires d’origine et aucune notification n’est envoyée à l’expéditeur ou aux destinataires d’origine.</p></td>
<td><p>Serveurs de boîtes aux lettres et serveurs de transport Edge</p></td>
<td><p>Exchange 2007 ou version ultérieure</p></td>
</tr>
<tr class="even">
<td><p><em>RemoveHeader</em></p></td>
<td><p><code>MessageHeaderField</code></p></td>
<td><p>Supprime le champ d’en-tête spécifié de l’en-tête de message.</p></td>
<td><p>Serveurs de boîtes aux lettres et serveurs de transport Edge</p></td>
<td><p>Exchange 2007 ou version ultérieure</p></td>
</tr>
<tr class="odd">
<td><p><em>SetHeaderName</em></p>
<p><em>SetHeaderValue</em></p></td>
<td><p>Première propriété : <code>MessageHeaderField</code></p>
<p>Deuxième propriété : <code>String</code></p></td>
<td><p>Ajoute ou modifie le champ d’en-tête spécifié dans l’en-tête du message et définit le champ d’en-tête sur la valeur spécifiée.</p></td>
<td><p>Serveurs de boîtes aux lettres et serveurs de transport Edge</p></td>
<td><p>Exchange 2007 ou version ultérieure</p></td>
</tr>
<tr class="even">
<td><p><em>SetSCL</em></p></td>
<td><p><code>SCLValue</code></p></td>
<td><p>Définit le SCL du message sur la valeur spécifiée.</p></td>
<td><p>Serveurs de boîtes aux lettres et serveurs de transport Edge</p></td>
<td><p>Exchange 2007 ou version ultérieure</p></td>
</tr>
<tr class="odd">
<td><p><em>SmtpRejectMessageRejectText</em></p>
<p><em>SmtpRejectMessageRejectStatusCode</em></p></td>
<td><p>Première propriété : <code>String</code></p>
<p>Deuxième propriété : <code>SMTPStatusCode</code></p></td>
<td><p>Met fin à la connexion SMTP entre le serveur d’envoi et le serveur de transport Edge avec le code d’état SMTP spécifié et le texte de rejet spécifié. Le destinataire ne reçoit ni le message d’origine ni la notification.</p>
<p>Les valeurs valides pour le code d’état SMTP sont des nombres entiers entre <code>400</code> et <code>500</code> selon la définition du RFC 3463.</p>
<p>Si vous spécifiez le texte de rejet sans indiquer le code d’état SMTP, le code par défaut <code>550</code> est utilisé.</p>
<p>Si vous spécifiez le code d’état SMTP sans spécifier le texte de rejet, le texte <code>Delivery not authorized, message refused</code> est utilisé.</p></td>
<td><p>Serveurs de transport Edge uniquement</p></td>
<td><p>Exchange 2007 ou version ultérieure</p></td>
</tr>
<tr class="even">
<td><p><em>StopRuleProcessing</em></p></td>
<td><p>s/o</p></td>
<td><p>Spécifie qu’une fois le message affecté par la règle, celui-ci est exempt de traitement par d’autres règles.</p></td>
<td><p>Serveurs de boîtes aux lettres et serveurs de transport Edge</p></td>
<td><p>Exchange 2013 ou version ultérieure</p></td>
</tr>
</tbody>
</table>


## Valeurs des propriétés

Les valeurs de propriétés utilisées pour les actions des règles de flux de messagerie sont décrites dans le tableau suivant.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Propriété</th>
<th>Valeurs admises</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>AddedManagerAction</code></p></td>
<td><p>Une des valeurs suivantes :</p>
<ul>
<li><p><strong>À</strong></p></li>
<li><p><strong>Cc</strong></p></li>
<li><p><strong>Cci</strong></p></li>
<li><p><strong>Rediriger</strong></p></li>
</ul></td>
<td><p>Spécifie comment inclure le responsable de l’expéditeur dans les messages.</p>
<ul>
<li><p>Si vous sélectionnez <strong>À</strong>, <strong>Cc</strong> ou <strong>Cci</strong>, le responsable de l’expéditeur est ajouté en tant que destinataire dans le champ spécifié.</p></li>
<li><p>Si vous sélectionnez <strong>Rediriger</strong>, le message est remis uniquement au responsable de l’expéditeur sans que l’expéditeur ou le destinataire n’en soit averti.</p></li>
</ul>
<p>Cette action fonctionne uniquement si l’attribut <strong>Manager</strong> de l’expéditeur est défini dans Active Directory.</p></td>
</tr>
<tr class="even">
<td><p><code>Addresses</code></p></td>
<td><p>Destinataires Exchange</p></td>
<td><p>En fonction de l’action, vous ne pouvez pas spécifier n’importe quel objet à extension messagerie de l’organisation ou vous pouvez être limité à un type d’objet spécifique. En règle générale, vous pouvez sélectionner plusieurs destinataires, mais vous pouvez seulement envoyer un rapport d’incident à un destinataire unique.</p></td>
</tr>
<tr class="odd">
<td><p><code>AuditSeverityLevel</code></p></td>
<td><p>Une des valeurs suivantes :</p>
<ul>
<li><p>Désactivez <strong>Auditer cette règle avec le niveau de gravité</strong> ou sélectionnez <strong>Auditer cette règle avec le niveau de gravité</strong>, avec la valeur <strong>Non spécifié</strong> (<code>DoNotAudit</code>)</p></li>
<li><p><strong>Faible</strong></p></li>
<li><p><strong>Moyenne</strong></p></li>
<li><p><strong>Élevée</strong></p></li>
</ul></td>
<td><p>Les valeurs <strong>Faible</strong>, <strong>Moyenne</strong> ou <strong>Élevée</strong> spécifient le niveau de gravité affecté au rapport d’incident et à l’entrée correspondante dans le journal de suivi des messages.</p>
<p>L’autre valeur empêche la génération d’un rapport d’incident et la consignation de l’entrée correspondante dans le journal de suivi des messages.</p></td>
</tr>
<tr class="even">
<td><p><code>DisclaimerFallbackAction</code></p></td>
<td><p>Une des valeurs suivantes :</p>
<ul>
<li><p><strong>Inclure dans un wrapper</strong></p></li>
<li><p><strong>Ignorer</strong></p></li>
<li><p><strong>Rejeter</strong></p></li>
</ul></td>
<td><p>Spécifie l’action à effectuer si la clause d’exclusion de responsabilité ne peut pas être appliquée à un message. Il existe des situations dans lesquelles les contenus d’un message ne peuvent pas être modifiés (par exemple si un message est chiffré). Les actions de secours disponibles sont les suivantes :</p>
<ul>
<li><p><strong>Inclure dans un wrapper</strong>   Le message d’origine est inclus dans une nouvelle enveloppe de message et le texte de la clause d’exclusion de responsabilité est inséré dans le nouveau message. Il s’agit de la valeur par défaut.</p>
<p><strong>Remarques</strong> :</p>
<ul>
<li><p>Les règles de flux de messagerie suivantes sont appliquées à la nouvelle enveloppe de message, et non au message d’origine. Par conséquent, vous devez attribuer à ces règles une priorité inférieure à celle des autres règles.</p></li>
<li><p>S’il est impossible d’inclure le message d’origine dans une nouvelle enveloppe, il n’est pas remis. Le message est renvoyé à l’expéditeur dans une notification d’échec de remise.</p></li>
</ul></li>
<li><p><strong>Ignorer</strong>   La règle n’est pas prise en compte et le message est remis sans clause d’exclusion de responsabilité</p></li>
<li><p><strong>Rejeter</strong>   le message est renvoyé à l’expéditeur dans une notification d’échec de remise.</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p><code>DisclaimerText</code></p></td>
<td><p>Chaîne HTML</p></td>
<td><p>Spécifie le texte de la clause d’exclusion de responsabilité, qui peut inclure des balises HTML, des balises de feuille de style en cascade en ligne (CSS) et des images par l’intermédiaire de la balise IMG. La longueur maximale est de 5 000 caractères, balises comprises.</p></td>
</tr>
<tr class="even">
<td><p><code>DisclaimerTextLocation</code></p></td>
<td><p>Valeur unique : <code>Append</code> ou <code>Prepend</code></p></td>
<td><p>Dans l’Environnement de ligne de commande Exchange Management Shell, vous pouvez utiliser <em>ApplyHtmlDisclaimerTextLocation</em> pour spécifier l’emplacement du texte de la clause d’exclusion de responsabilité dans le message :</p>
<ul>
<li><p><code>Append</code>   Ajoute la clause d’exclusion de responsabilité à la fin du corps de message. Il s’agit de la valeur par défaut.</p></li>
<li><p><code>Prepend</code>   Ajoute la clause d’exclusion de responsabilité au début du corps de message.</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p><code>DSNEnhancedStatusCode</code></p></td>
<td><p>Valeur de code DSN unique :</p>
<ul>
<li><p><code>5.7.1</code></p></li>
<li><p>de <code>5.7.900</code> à <code>5.7.999</code></p></li>
</ul></td>
<td><p>Spécifie le code DSN utilisé. Vous pouvez créer des DSN personnalisés à l’aide de la cmdlet <strong>New-SystemMessage</strong>.</p>
<p>Si vous ne spécifiez pas le texte du motif de rejet avec le code DSN, le texte de motif par défaut <code>Delivery not authorized, message refused</code> est utilisé.</p>
<p>Lorsque vous créez ou modifiez la règle dans l’Environnement de ligne de commande Exchange Management Shell, vous pouvez spécifier le texte du motif du rejet à l’aide du paramètre <em>RejectMessageReasonText</em>.</p></td>
</tr>
<tr class="even">
<td><p><code>IncidentReportContent</code></p></td>
<td><p>Une ou plusieurs des valeurs suivantes :</p>
<ul>
<li><p><strong>Expéditeur</strong></p></li>
<li><p><strong>Destinataires</strong></p></li>
<li><p><strong>Objet</strong></p></li>
<li><p><strong>Destinataires Cc</strong> (<code>Cc</code>)</p></li>
<li><p><strong>Destinataires Cci</strong> (<code>Bcc</code>)</p></li>
<li><p><strong>Gravité</strong></p></li>
<li><p><strong>Informations de remplacement de l’expéditeur</strong> (<code>Override</code>)</p></li>
<li><p><strong>Règles correspondantes</strong> (<code>RuleDetections</code>)</p></li>
<li><p><strong>Rapports faux positifs</strong> (<code>FalsePositive</code>)</p></li>
<li><p><strong>Classification des données détectées</strong> (<code>DataClassifications</code>)</p></li>
<li><p><strong>Contenu correspondant</strong> (<code>IdMatch</code>)</p></li>
<li><p><strong>Courrier original</strong> (<code>AttachOriginalMail</code>)</p></li>
</ul></td>
<td><p>Spécifie les propriétés du message d’origine à inclure dans le rapport d’incident. Vous pouvez inclure n’importe quelle combinaison de ces propriétés. Outre les propriétés que vous spécifiez, l’ID du message est toujours inclus. Les propriétés disponibles sont les suivantes :</p>
<ul>
<li><p><strong>Expéditeur</strong>   Expéditeur du message d’origine.</p></li>
<li><p><strong>Destinataires</strong>, <strong>Destinataires en Cc</strong> et <strong>Destinataires en Cci</strong>   Tous les destinataires du message ou uniquement les destinataires figurant dans les champs <strong>Cc</strong> ou <strong>Bcc</strong>. Pour chaque propriété, seuls les 10 premiers destinataires figurent dans le rapport d’incident.</p></li>
<li><p><strong>Objet</strong>   Champ <strong>Subject</strong> du message d’origine.</p></li>
<li><p><strong>Gravité</strong> Gravité d’audit de la règle déclenchée. Les journaux de suivi des messages incluent tous les niveaux de gravité d’audit et peuvent être filtrés par gravité d’audit. Dans le CAE, si vous désactivez la case à cocher <strong>Auditer cette règle avec le niveau de gravité</strong> (dans l’Environnement de ligne de commande Exchange Management Shell, la valeur <code>DoNotAudit</code> du paramètre <em>SetAuditSeverity</em>), les correspondances de règle ne s’affichent pas dans les rapports de règle. Si un message est traité par plusieurs règles, la gravité la plus élevée est incluse dans les rapports d’incident.</p></li>
<li><p><strong>Informations de remplacement de l’expéditeur</strong>   Remplacement si l’expéditeur a choisi de remplacer un conseil de stratégie. Si l’expéditeur a fourni une justification, les 100 premiers caractères sont également inclus.</p></li>
<li><p><strong>Règles correspondantes</strong> Liste des règles déclenchées par le message.</p></li>
<li><p><strong>Soumissions fausses-positives</strong>   Faux positif si l’expéditeur a marqué le message comme faux positif pour un conseil de stratégie.</p></li>
<li><p><strong>Classifications de données détectées</strong>   Liste des types d’informations sensibles détectés dans le message.</p></li>
<li><p><strong>Contenu correspondant</strong> Type d’informations sensibles détecté, contenu correspondant exact du message, ainsi que les 150 caractères situés avant et après les informations sensibles correspondantes.</p></li>
<li><p><strong>Courrier original</strong> L’intégralité du message ayant déclenché la règle est jointe au rapport d’incident.</p></li>
</ul>
<p>Dans l’Environnement de ligne de commande Exchange Management Shell, vous pouvez spécifier plusieurs valeurs séparées par des virgules.</p></td>
</tr>
<tr class="odd">
<td><p><code>MessageClassification</code></p></td>
<td><p>Objet de classification des messages unique</p></td>
<td><p>Dans le CAE, effectuez votre sélection dans la liste des classifications de messages disponibles.</p>
<p>Dans l’Environnement de ligne de commande Exchange Management Shell, utilisez le cmdlet <strong>Get-MessageClassification</strong> pour voir les objets de classification des messages qui sont disponibles.</p></td>
</tr>
<tr class="even">
<td><p><code>MessageHeaderField</code></p></td>
<td><p>Chaîne unique</p></td>
<td><p>Spécifie le champ d’en-tête de message SMTP à ajouter, supprimer ou modifier.</p>
<p>L’<em>en-tête de message</em> est un ensemble de champs d’en-tête obligatoires et facultatifs dans le message. Exemples de champs d’en-tête : <strong>To</strong>, <strong>From</strong>, <strong>Received</strong> et <strong>Content-Type</strong>. Les champs d’en-tête officiels sont définis dans le document RFC 5322. Les champs d’en-tête non officiels commencent par <strong>X-</strong> et sont appelés <em>en-têtes X</em>.</p></td>
</tr>
<tr class="odd">
<td><p><code>NotificationMessageText</code></p></td>
<td><p>N’importe quelle combinaison de texte brut, de balises HTML et de mots clés</p></td>
<td><p>Spécifie le texte à utiliser dans un message de notification à un destinataire.</p>
<p>En plus du texte brut et des balises HTML, vous pouvez spécifier les mots clés suivants, qui utilisent les valeurs du message d’origine :</p>
<ul>
<li><p><code>%%From%%</code></p></li>
<li><p><code>%%To%%</code></p></li>
<li><p><code>%%Cc%%</code></p></li>
<li><p><code>%%Subject%%</code></p></li>
<li><p><code>%%Headers%%</code></p></li>
<li><p><code>%%MessageDate%%</code></p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><code>NotifySenderType</code></p></td>
<td><p>Une des valeurs suivantes :</p>
<ul>
<li><p><strong>Avertir l’expéditeur, mais l’autoriser à effectuer l’envoi</strong> (<code>NotifyOnly</code>)</p></li>
<li><p><strong>Bloquer le message</strong> (<code>RejectMessage</code>)</p></li>
<li><p><strong>Bloquer le message, sauf s’il s’agit d’un faux positif</strong> (<code>RejectUnlessFalsePositiveOverride</code>)</p></li>
<li><p><strong>Bloquer le message, mais autoriser l’expéditeur à remplacer cette valeur et à effectuer l’envoi</strong> (<code>RejectUnlessSilentOverride</code>)</p></li>
<li><p><strong>Bloquer le message, mais autoriser l’expéditeur à remplacer cette valeur à l’aide d’une justification professionnelle et à effectuer l’envoi</strong> (<code>RejectUnlessExplicitOverride</code>)</p></li>
</ul></td>
<td><p>Spécifie le type de conseil de stratégie que l’expéditeur reçoit si le message ne respecte pas une stratégie DLP. Les paramètres sont décrits dans la liste suivante :</p>
<ul>
<li><p><strong>Avertir l’expéditeur, mais l’autoriser à effectuer l’envoi</strong> L’expéditeur est averti, mais le message est remis normalement.</p></li>
<li><p><strong>Bloquer le message</strong>   Le message est rejeté et l’expéditeur est informé.</p></li>
<li><p><strong>Bloquer le message, sauf s’il s’agit d’un faux positif</strong> Le message est rejeté, sauf s’il est marqué comme faux positif par l’expéditeur.</p></li>
<li><p><strong>Bloquer le message, mais autoriser l’expéditeur à remplacer cette valeur et à effectuer l’envoi</strong> Le message est rejeté, sauf si l’expéditeur a choisi d’ignorer la restriction de stratégie.</p></li>
<li><p><strong>Bloquer le message, mais autoriser l’expéditeur à remplacer cette valeur à l’aide d’une justification professionnelle et à effectuer l’envoi</strong> Similaire au type <strong>Bloquer le message, mais autoriser l’expéditeur à remplacer cette valeur et à effectuer l’envoi</strong>, mais l’expéditeur fournit également la raison pour laquelle il a ignoré la restriction de stratégie.</p></li>
</ul>
<p>Lors de l’utilisation de cette action, vous devez utiliser la condition <strong>Le message contient des informations sensibles</strong> (<em>MessageContainsDataClassification</em>).</p></td>
</tr>
<tr class="odd">
<td><p><code>RMSTemplate</code></p></td>
<td><p>Objet de modèle RMS unique</p></td>
<td><p>Spécifie le modèle Rights Management Services (RMS) appliqué au message.</p>
<p>Dans le CAE, sélectionnez le modèle RMS dans une liste.</p>
<p>Dans l’Environnement de ligne de commande Exchange Management Shell, utilisez la cmdlet <strong>Get-RMSTemplate</strong> pour afficher les modèles RMS disponibles.</p>
<p>RMS nécessite des licences d’accès au client (CAL) Exchange Entreprise pour chaque boîte aux lettres. Pour plus d’informations sur les CAL, consultez <a href="https://go.microsoft.com/fwlink/p/?linkid=237292">Gestion des licences Exchange Server</a>.</p></td>
</tr>
<tr class="even">
<td><p><code>SCLValue</code></p></td>
<td><p>Une des valeurs suivantes :</p>
<ul>
<li><p><strong>Contourner le filtrage du courrier indésirable</strong> (<code>-1</code>)</p></li>
<li><p>Nombres entiers entre 0 et 9</p></li>
</ul></td>
<td><p>Indique le seuil de probabilité de courrier indésirable (SCL) affecté au message. Plus la valeur est élevée, plus il est probable que le message soit un courrier indésirable.</p></td>
</tr>
<tr class="odd">
<td><p><code>String</code></p></td>
<td><p>Chaîne unique</p></td>
<td><p>Spécifie le texte appliqué au champ d’en-tête, à la notification d’échec de remise ou à l’entrée du journal des événements du message spécifié.</p>
<p>Dans l’Environnement de ligne de commande Exchange Management Shell, si la valeur contient des espaces, placez-la entre guillemets (&quot;).</p></td>
</tr>
</tbody>
</table>


Retour au début

## Pour plus d'informations

[Gestion de règles de flux de messagerie](https://docs.microsoft.com/fr-fr/exchange/security-and-compliance/mail-flow-rules/manage-mail-flow-rules)

[Règles de transport ou de flux de messagerie](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md)

[Conditions de règles de transport (prédicats)](mail-flow-rule-conditions-and-exceptions-predicates-in-exchange-2013-exchange-2013-help.md)

[Courrier des actions de règle de flux dans Exchange en ligne](https://technet.microsoft.com/fr-fr/library/jj919237\(v=exchg.150\)) pour Exchange Online

[Envoyer par courrier électronique les actions de règle de flux dans Exchange Online Protection](https://technet.microsoft.com/fr-fr/library/jj920117\(v=exchg.150\)) pour Exchange Online Protection

[Clauses d’exclusion de responsabilité, signatures, pieds de page ou en-têtes de message à l’échelle de l’organisation dans Office 365](https://technet.microsoft.com/fr-fr/library/dn600323\(v=exchg.150\))

