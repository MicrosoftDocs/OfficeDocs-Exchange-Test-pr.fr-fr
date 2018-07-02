---
title: 'Conditions de règles de transport (prédicats): Exchange 2013 Help'
TOCTitle: Conditions de règle de flux de messagerie et exceptions (prédicats)
ms:assetid: c918ea00-1e68-4b8b-8d51-6966b4432e2d
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dd638183(v=EXCHG.150)
ms:contentKeyID: 50479163
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Conditions de règles de transport (prédicats)

 

_**Sapplique à :**Exchange Server 2013_

_**Dernière rubrique modifiée :**2017-12-20_

Les conditions et les exceptions des règles de flux de messagerie (également nommées règles de transport) identifient les messages auxquels la règle est appliquée ou non. Par exemple, si la règle ajoute une clause d’exclusion de responsabilité aux messages, vous pouvez configurer la règle de telle sorte qu’elle s’applique uniquement aux messages qui contiennent des mots spécifiques, aux messages envoyés par des utilisateurs spécifiques ou à tous les messages, à l’exception de ceux envoyés par les membres d’un groupe spécifique. Collectivement, les conditions et les exceptions des règles de flux de messagerie sont également appelées *prédicats*, car pour chaque condition, il existe une exception correspondante qui utilise les mêmes paramètres et la même syntaxe. La seule différence réside dans le fait que les conditions spécifient les messages à inclure, tandis que les exceptions spécifient les messages à exclure.

La plupart des conditions et des exceptions possèdent une propriété qui requiert une ou plusieurs valeurs. Par exemple, la condition **L’expéditeur est** nécessite l’expéditeur du message. Certaines conditions ont deux propriétés. Par exemple, la condition **Un en-tête de message inclut n’importe lequel de ces mots** requiert une propriété pour spécifier le champ d’en-tête du message et une deuxième pour spécifier le texte à rechercher dans le champ d’en-tête. Certaines conditions ou exceptions n’ont aucune propriété. Par exemple, la condition **N’importe quelle pièce jointe possède un contenu exécutable** recherche simplement les pièces jointes des messages dont le contenu est exécutable.

Pour plus d’informations sur les règles de flux de courrier dans Exchange Server 2013, consultez [Règles de transport ou de flux de messagerie](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md).

Pour plus d’informations sur les conditions et les exceptions dans les règles de flux de courrier dans Exchange Online Protection ou Exchange Online, consultez [Exceptions (prédicat) et conditions de règles de flux de messagerie dans Exchange Online](https://technet.microsoft.com/fr-fr/library/jj919235\(v=exchg.150\)) ou [Mail flux conditions et les exceptions (prédicat) dans Exchange Online Protection](https://technet.microsoft.com/fr-fr/library/jj919234\(v=exchg.150\)).

## Conditions et exceptions applicables aux règles de flux de messagerie sur les serveurs de boîte aux lettres

Les tableaux dans les sections suivantes décrivent les conditions et les exceptions qui sont disponibles dans les règles de flux de messagerie sur les serveurs de boîtes aux lettres. Les types de propriétés sont décrits dans la section types de propriété .

Expéditeurs

Destinataires

Objet ou corps du message

Pièces jointes

N'importe quels destinataires

Types d'informations sensibles, valeurs À et Cc, taille et jeux de caractères des messages

Expéditeur et destinataire

Propriétés de message

En-têtes de messages

**Remarques** :

  - Après que vous avez sélectionné une condition ou une exception dans le Centre d’administration Exchange (CAE), la valeur obtenue dans le champ **Appliquer cette règle si** ou **Sauf si** diffère souvent (plus courte) de la valeur du chemin d’accès sélectionnée. Par ailleurs, lorsque vous créez de nouvelles règles basées sur un modèle (une liste filtrée de scénarios), vous pouvez souvent sélectionner un nom de condition court au lieu de suivre le chemin d’accès complet. Les noms courts et les valeurs de chemin d’accès complet sont présentés dans la colonne CAE des tableaux.

  - Si vous sélectionnez **\[Appliquer à tous les messages\]** dans le CAE, vous ne pouvez pas spécifier d’autres conditions. L’équivalent dans l’Environnement de ligne de commande Exchange Management Shell consiste à créer une règle sans spécifier de paramètres de condition.

  - Les paramètres et les propriétés sont identiques dans les conditions et les exceptions. Ainsi, la sortie de la cmdlet **Get-TransportRulePredicate** n’affiche pas les exceptions séparément. De plus, les noms de certains des prédicats renvoyés par cette cmdlet diffèrent des noms de paramètres correspondants, et un prédicat peut nécessiter plusieurs paramètres.

## Expéditeurs

Pour les conditions et les exceptions qui examinent l’adresse de l’expéditeur, vous pouvez spécifier où la règle doit rechercher l’adresse de l’expéditeur.

Dans le CAE, dans la section **Propriétés de cette règle**, cliquez sur **Faire correspondre l’adresse de l’expéditeur dans le message**. Notez que vous devrez peut-être cliquer sur **Autres options** pour afficher ce paramètre. Dans l’Environnement de ligne de commande Exchange Management Shell, le paramètre est *SenderAddressLocation*. Les valeurs disponibles sont :

  - **En-tête**   Examinez uniquement les expéditeurs dans l’en-tête du message (par exemple, les champs **From**, **Sender** ou **Reply-To**). Il s’agit de la valeur par défaut et de la manière dont les règles de flux de messagerie fonctionnaient avant la mise à jour cumulative 1 d’Exchange 2013 (CU1).

  - **Enveloppe**    Examiner uniquement les expéditeurs de l’enveloppe de message (la valeur de **MAIL FROM** qui a été utilisée dans la transmission SMTP, lequel est généralement stockée dans le champ **Return-Path** ). Notez que recherche enveloppe de messages n’est disponible que pour les conditions suivantes (et les exceptions correspondantes) :
    
      - **L’expéditeur est** (*From*)
    
      - **L’expéditeur est membre de** (*FromMemberOf*)
    
      - **L’adresse de l’expéditeur inclut** (*FromAddressContainsWords*)
    
      - **L’adresse de l’expéditeur correspond à** (*FromAddressMatchesPatterns*)
    
      - **Le domaine de l’expéditeur est** (*SenderDomainIs*)

  - **En-tête ou enveloppe** (`HeaderOrEnvelope`)   Examinez les expéditeurs dans l’en-tête et dans l’enveloppe du message.


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
<th>Condition ou exception dans le CAE</th>
<th>Paramètres de condition et d’exception dans l’Environnement de ligne de commande Exchange Management Shell</th>
<th>Type de propriété</th>
<th>Description</th>
<th>Disponible dans</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>L'expéditeur est</strong></p>
<p><strong>L’expéditeur</strong> &gt; <strong>est cette personne</strong></p></td>
<td><p><em>From</em></p>
<p><em>ExceptIfFrom</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p>Messages envoyés par les boîtes aux lettres, les utilisateurs de messagerie ou les contacts de messagerie spécifiés dans l’organisation Exchange.</p></td>
<td><p>Exchange 2007 ou version ultérieure</p></td>
</tr>
<tr class="even">
<td><p><strong>L'expéditeur est localisé</strong></p>
<p><strong>L’expéditeur</strong> &gt; <strong>est interne/externe</strong></p></td>
<td><p><em>FromScope</em></p>
<p><em>ExceptIfFromScope</em></p></td>
<td><p><code>UserScopeFrom</code></p></td>
<td><p>Messages envoyés par des expéditeurs internes ou externes.</p></td>
<td><p>Exchange 2007 ou version ultérieure</p></td>
</tr>
<tr class="odd">
<td><p><strong>L'expéditeur est membre de</strong></p>
<p><strong>L’expéditeur</strong> &gt; <strong>est membre de ce groupe</strong></p></td>
<td><p><em>FromMemberOf</em></p>
<p><em>ExceptIfFromMemberOf</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p>Messages envoyés par un membre du groupe spécifié.</p></td>
<td><p>Exchange 2007 ou version ultérieure</p></td>
</tr>
<tr class="even">
<td><p><strong>L'adresse de l'expéditeur inclut</strong></p>
<p><strong>L’expéditeur</strong> &gt; <strong>l’adresse comprend l’un des mots suivants</strong></p></td>
<td><p><em>FromAddressContainsWords</em></p>
<p><em>ExceptIfFromAddressContainsWords</em></p></td>
<td><p><code>Words</code></p></td>
<td><p>Messages contenant les mots spécifiés dans l’adresse de l’expéditeur.</p></td>
<td><p>Exchange 2007 ou version ultérieure</p></td>
</tr>
<tr class="odd">
<td><p><strong>L'adresse de l'expéditeur correspond à</strong></p>
<p><strong>L’expéditeur</strong> &gt; <strong>l’adresse correspond à l’un de ces modèles de texte</strong></p></td>
<td><p><em>FromAddressMatchesPatterns</em></p>
<p><em>ExceptIfFromAddressMatchesPatterns</em></p></td>
<td><p><code>Patterns</code></p></td>
<td><p>Messages dans lesquels l’adresse de messagerie de l’expéditeur contient des modèles de texte qui correspondent aux expressions régulières spécifiées.</p></td>
<td><p>Exchange 2007 ou version ultérieure</p></td>
</tr>
<tr class="even">
<td><p><strong>Les propriétés spécifiées de l'expéditeur contiennent l'un de ces mots</strong></p>
<p><strong>L’expéditeur</strong> &gt; <strong>possède des propriétés spécifiques, y compris l’un de ces mots</strong></p></td>
<td><p><em>SenderADAttributeContainsWords</em></p>
<p><em>ExceptIfSenderADAttributeContainsWords</em></p></td>
<td><p>Première propriété : <code>ADAttribute</code></p>
<p>Deuxième propriété : <code>Words</code></p></td>
<td><p>Messages dans lesquels l’attribut Active Directory spécifié de l’expéditeur contient l’un des mots spécifiés.</p>
<p>Notez que l’attribut <strong>Country</strong> requiert la valeur de code pays à deux lettres (par exemple, DE pour l’Allemagne).</p></td>
<td><p>Exchange 2010 ou version ultérieure</p></td>
</tr>
<tr class="odd">
<td><p><strong>Les propriétés spécifiées de l'expéditeur correspondent à ces modèles de texte</strong></p>
<p><strong>L’expéditeur</strong> &gt; <strong>possède des propriétés spécifiques correspondant à ces modèles de texte</strong></p></td>
<td><p><em>SenderADAttributeMatchesPatterns</em></p>
<p><em>ExceptIfSenderADAttributeMatchesPatterns</em></p></td>
<td><p>Première propriété : <code>ADAttribute</code></p>
<p>Deuxième propriété : <code>Patterns</code></p></td>
<td><p>Messages dans lesquels l’attribut Active Directory spécifié de l’expéditeur contient des modèles de texte qui correspondent aux expressions régulières spécifiées.</p></td>
<td><p>Exchange 2010 ou version ultérieure</p></td>
</tr>
<tr class="even">
<td><p><strong>L'expéditeur a remplacé le conseil de stratégie</strong></p>
<p><strong>L’expéditeur</strong> &gt; <strong>a remplacé le conseil concernant la stratégie</strong></p></td>
<td><p><em>HasSenderOverride</em></p>
<p><em>ExceptIfHasSenderOverride</em></p></td>
<td><p>s/o</p></td>
<td><p>Messages dans lesquels l’expéditeur a choisi de remplacer une stratégie de protection contre la perte de données (DLP). Pour plus d’informations sur les stratégies DLP, consultez la rubrique <a href="technical-overview-of-dlp-data-loss-prevention-in-exchange.md">Protection contre la perte de données</a>.</p></td>
<td><p>Exchange 2013 ou version ultérieure</p></td>
</tr>
<tr class="odd">
<td><p><strong>L'adresse IP de l'expéditeur se trouve dans la plage</strong></p>
<p><strong>L’expéditeur</strong> &gt; <strong>l’adresse IP se situe dans l’une de ces plages ou correspond exactement</strong></p></td>
<td><p><em>SenderIPRanges</em></p>
<p><em>ExceptIfSenderIPRanges</em></p></td>
<td><p><code>IPAddressRanges</code></p></td>
<td><p>Messages dans lesquels l’adresse IP de l’expéditeur correspond à l’adresse IP spécifiée ou figure dans la plage d’adresses IP spécifiée.</p></td>
<td><p>Exchange 2013 ou version ultérieure</p></td>
</tr>
<tr class="even">
<td><p><strong>Le domaine de l'expéditeur est</strong></p>
<p><strong>L’expéditeur</strong> &gt; <strong>le domaine est</strong></p></td>
<td><p><em>SenderDomainIs</em></p>
<p><em>ExceptIfSenderDomainIs</em></p></td>
<td><p><code>DomainName</code></p></td>
<td><p>Messages dans lesquels le domaine de l’adresse de messagerie de l’expéditeur correspond à la valeur spécifiée.</p>
<p>Si vous devez rechercher des domaines de l’expéditeur qui <em>contiennent</em> le domaine spécifié (par exemple, n’importe quel sous-domaine d’un domaine), utilisez la condition <strong>L’adresse de l’expéditeur correspond à</strong> (<em>FromAddressMatchesPatterns</em>) et spécifiez le domaine en utilisant la syntaxe : <code>'@domain\.com$'</code>.</p></td>
<td><p>Exchange 2013 ou version ultérieure</p></td>
</tr>
</tbody>
</table>


Retour au début

## Destinataires


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
<th>Condition ou exception dans le CAE</th>
<th>Paramètres de condition et d’exception dans l’Environnement de ligne de commande Exchange Management Shell</th>
<th>Type de propriété</th>
<th>Description</th>
<th>Disponible dans</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Le destinataire est</strong></p>
<p><strong>Le destinataire</strong> &gt; <strong>est cette personne</strong></p></td>
<td><p><em>SentTo</em></p>
<p><em>ExceptIfSentTo</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p>Messages où l’un des destinataires est la boîte aux lettres spécifiée, un utilisateur de messagerie ou courrier contact dans l’organisation Exchange. Les destinataires peuvent être dans les champs <strong>To</strong>, <strong>Cc</strong>ou <strong>Bcc</strong> du message.</p>
<p><strong>Remarque:</strong> vous ne pouvez pas spécifier les groupes de distribution ou des groupes de sécurité à extension messagerie. Si vous devez effectuer une action sur les messages qui sont envoyés à un groupe, utilisez la condition <strong>pour la boîte contient</strong> (<em>AnyOfToHeader</em>) à la place.</p></td>
<td><p>Exchange 2007 ou version ultérieure</p></td>
</tr>
<tr class="even">
<td><p><strong>Le destinataire est localisé</strong></p>
<p><strong>Le destinataire</strong> &gt; <strong>est interne/externe</strong></p></td>
<td><p><em>SentToScope</em></p>
<p><em>ExceptIfSentToScope</em></p></td>
<td><p><code>UserScopeTo</code></p></td>
<td><p>Messages qui sont envoyés à des destinataires internes, des destinataires externes, des destinataires externes dans des organisations partenaires ou des destinataires externes dans des organisations non partenaires.</p></td>
<td><p>Exchange 2007 ou version ultérieure</p></td>
</tr>
<tr class="odd">
<td><p><strong>Le destinataire est membre de</strong></p>
<p><strong>Le destinataire</strong> &gt; <strong>est membre de ce groupe</strong></p></td>
<td><p><em>SentToMemberOf</em></p>
<p><em>ExceptIfSentToMemberOf</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p>Messages qui contiennent des destinataires qui sont membres du groupe spécifié. Le groupe peut se trouver dans les champs <strong>To</strong>, <strong>Cc</strong> ou <strong>Bcc</strong> du message.</p></td>
<td><p>Exchange 2007 ou version ultérieure</p></td>
</tr>
<tr class="even">
<td><p><strong>L'adresse du destinataire inclut</strong></p>
<p><strong>Le destinataire</strong> &gt; <strong>l’adresse comprend l’un des mots suivants</strong></p></td>
<td><p><em>RecipientAddressContainsWords</em></p>
<p><em>ExceptIfRecipientAddressContainsWords</em></p></td>
<td><p><code>Words</code></p></td>
<td><p>Messages contenant les mots spécifiés dans l’adresse du destinataire.</p>
<p><strong>Remarque</strong> : cette condition ne tient pas compte des messages qui sont envoyés aux adresses proxy du destinataire. Elle correspond uniquement aux messages qui sont envoyés à l’adresse de messagerie principale du destinataire.</p></td>
<td><p>Exchange 2010 ou version ultérieure</p></td>
</tr>
<tr class="odd">
<td><p><strong>L'adresse du destinataire correspond à</strong></p>
<p><strong>Le destinataire</strong> &gt; <strong>l’adresse correspond à l’un de ces modèles de texte</strong></p></td>
<td><p><em>RecipientAddressMatchesPatterns</em></p>
<p><em>ExceptIfRecipientAddressMatchesPatterns</em></p></td>
<td><p><code>Patterns</code></p></td>
<td><p>Messages dans lesquels l’adresse de messagerie du destinataire contient des modèles de texte qui correspondent aux expressions régulières spécifiées.</p>
<p><strong>Remarque</strong> : cette condition ne tient pas compte des messages qui sont envoyés aux adresses proxy du destinataire. Elle correspond uniquement aux messages qui sont envoyés à l’adresse de messagerie principale du destinataire.</p></td>
<td><p>Exchange 2010 ou version ultérieure</p></td>
</tr>
<tr class="even">
<td><p><strong>Les propriétés spécifiées de l'expéditeur contiennent l'un de ces mots</strong></p>
<p><strong>Le destinataire</strong> &gt; <strong>possède des propriétés spécifiques, y compris l’un de ces mots</strong></p></td>
<td><p><em>RecipientADAttributeContainsWords</em></p>
<p><em>ExceptIfRecipientADAttributeContainsWords</em></p></td>
<td><p>Première propriété : <code>ADAttribute</code></p>
<p>Deuxième propriété : <code>Words</code></p></td>
<td><p>Messages dans lesquels l’attribut Active Directory spécifié d’un destinataire contient certains mots spécifiés.</p>
<p>Notez que l’attribut <strong>Country</strong> requiert la valeur de code pays à deux lettres (par exemple, DE pour l’Allemagne).</p></td>
<td><p>Exchange 2010 ou version ultérieure</p></td>
</tr>
<tr class="odd">
<td><p><strong>Les propriétés spécifiées du destinataire correspondent à ces modèles de texte</strong></p>
<p><strong>Le destinataire</strong> &gt; <strong>possède des propriétés spécifiques correspondant à ces modèles de texte</strong></p></td>
<td><p><em>RecipientADAttributeMatchesPatterns</em></p>
<p><em>ExceptIfRecipientADAttributeMatchesPatterns</em></p></td>
<td><p>Première propriété : <code>ADAttribute</code></p>
<p>Deuxième propriété : <code>Patterns</code></p></td>
<td><p>Messages dans lesquels l’attribut Active Directory spécifié d’un destinataire contient des modèles de texte qui correspondent à l’expression régulière spécifiée.</p></td>
<td><p>Exchange 2010 ou version ultérieure</p></td>
</tr>
<tr class="even">
<td><p><strong>Le domaine d'un destinataire est</strong></p>
<p><strong>Le destinataire</strong> &gt; <strong>le domaine est</strong></p></td>
<td><p><em>RecipientDomainIs</em></p>
<p><em>ExceptIfRecipientDomainIs</em></p></td>
<td><p><code>DomainName</code></p></td>
<td><p>Messages dans lesquels le domaine de l’adresse de messagerie d’un destinataire correspond à la valeur spécifiée.</p>
<p>Si vous devez rechercher des domaines de destinataires qui <em>contiennent</em> le domaine spécifié (par exemple, n’importe quel sous-domaine d’un domaine), utilisez la condition <strong>L’adresse du destinataire correspond à</strong> (<em>RecipientAddressMatchesPatterns</em>) et spécifiez le domaine en utilisant la syntaxe : <code>'@domain\.com$'</code>.</p></td>
<td><p>Exchange 2013 ou version ultérieure</p></td>
</tr>
</tbody>
</table>


Retour au début

## Objet ou corps du message

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>La recherche de mots clés ou de modèles de texte dans l’objet ou dans d’autres champs d’en-tête du message est effectuée <em>après</em> que le codage utilisé avec la méthode MIME pour transmettre le message binaire entre les serveurs SMTP a été décodé en texte ASCII. Vous ne pouvez pas utiliser de conditions ou d’exceptions pour rechercher les valeurs codées brutes (en règle générale, en base 64) dans l’objet ou d’autres champs d’en-tête des messages.</td>
</tr>
</tbody>
</table>



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
<th>Condition ou exception dans le CAE</th>
<th>Paramètres de condition et d’exception dans l’Environnement de ligne de commande Exchange Management Shell</th>
<th>Type de propriété</th>
<th>Description</th>
<th>Disponible dans</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>L'objet ou le corps inclut</strong></p>
<p><strong>L’objet ou le corps</strong> &gt; <strong>l’objet ou le corps inclut l’un de ces mots</strong></p></td>
<td><p><em>SubjectOrBodyContainsWords</em></p>
<p><em>ExceptIfSubjectOrBodyContainsWords</em></p></td>
<td><p><code>Words</code></p></td>
<td><p>Messages dans lesquels le champ <strong>Subject</strong> ou le corps comporte les mots spécifiés.</p></td>
<td><p>Exchange 2007 ou version ultérieure</p></td>
</tr>
<tr class="even">
<td><p><strong>L'objet ou le corps correspond à</strong></p>
<p><strong>L’objet ou le corps</strong> &gt; <strong>l’objet ou le corps correspond à ces modèles de texte</strong></p></td>
<td><p><em>SubjectOrBodyMatchesPatterns</em></p>
<p><em>ExceptIfSubjectOrBodyMatchesPatterns</em></p></td>
<td><p><code>Patterns</code></p></td>
<td><p>Messages dans lesquels le champ <strong>Subject</strong> ou le corps du message contient des modèles de texte qui correspondent aux expressions régulières spécifiées.</p></td>
<td><p>Exchange 2007 ou version ultérieure</p></td>
</tr>
<tr class="odd">
<td><p><strong>L'objet inclut</strong></p>
<p><strong>L’objet ou le corps</strong> &gt; <strong>l’objet inclut l’un de ces mots</strong></p></td>
<td><p><em>SubjectContainsWords</em></p>
<p><em>ExceptIfSubjectContainsWords</em></p></td>
<td><p><code>Words</code></p></td>
<td><p>Messages dans lesquels le champ <strong>Subject</strong> contient les mots spécifiés.</p></td>
<td><p>Exchange 2007 ou version ultérieure</p></td>
</tr>
<tr class="even">
<td><p><strong>L'objet correspond à</strong></p>
<p><strong>L’objet ou le corps</strong> &gt; <strong>l’objet correspond à ces modèles de texte</strong></p></td>
<td><p><em>SubjectMatchesPatterns</em></p>
<p><em>ExceptIfSubjectMatchesPatterns</em></p></td>
<td><p><code>Patterns</code></p></td>
<td><p>Messages dans lesquels le champ <strong>Subject</strong> contient des modèles de texte qui correspondent aux expressions régulières spécifiées.</p></td>
<td><p>Exchange 2007 ou version ultérieure</p></td>
</tr>
</tbody>
</table>


Retour au début

## Pièces jointes

Pour plus d’informations sur comment les règles de flux de messagerie inspecter les pièces jointes de messages, consultez [Utiliser des règles de transport pour analyser les pièces jointes des messages](use-transport-rules-to-inspect-message-attachments-exchange-2013-help.md).


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
<th>Condition ou exception dans le CAE</th>
<th>Paramètres de condition et d’exception dans l’Environnement de ligne de commande Exchange Management Shell</th>
<th>Type de propriété</th>
<th>Description</th>
<th>Disponible dans</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Tout contenu de pièce jointe inclut</strong></p>
<p><strong>N’importe quelle pièce jointe <strong>&gt;</strong> le contenu inclut l’un de ces mots</strong></p></td>
<td><p><em>AttachmentContainsWords</em></p>
<p><em>ExceptIfAttachmentContainsWords</em></p></td>
<td><p><code>Words</code></p></td>
<td><p>Messages dans lesquels une pièce jointe contient les mots spécifiés.</p></td>
<td><p>Exchange 2010 ou version ultérieure</p></td>
</tr>
<tr class="even">
<td><p><strong>Tout contenu de pièce jointe correspond à</strong></p>
<p><strong>N’importe quelle pièce jointe</strong> &gt; <strong>le contenu correspond à ces modèles de texte</strong></p></td>
<td><p><em>AttachmentMatchesPatterns</em></p>
<p><em>ExceptIfAttachmentMatchesPatterns</em></p></td>
<td><p><code>Patterns</code></p></td>
<td><p>Messages dans lesquels une pièce jointe contient des modèles de texte qui correspondent aux expressions régulières spécifiées.</p>
<p><strong>Remarque:</strong> seul les premier 150 kilo-octets (Ko des pièces jointes) sont analysés.</p></td>
<td><p>Exchange 2010 ou version ultérieure</p></td>
</tr>
<tr class="odd">
<td><p><strong>Le contenu d'une pièce jointe ne peut pas être inspecté</strong></p>
<p><strong>N’importe quelle pièce jointe</strong> &gt; <strong>le contenu ne peut pas être inspecté</strong></p></td>
<td><p><em>AttachmentIsUnsupported</em></p>
<p><em>ExceptIfAttachmentIsUnsupported</em></p></td>
<td><p>s/o</p></td>
<td><p>Messages où une pièce jointe n’est pas reconnue en mode natif par Exchange, et que le IFilter requis n’est pas installé sur le serveur de boîtes aux lettres. Pour plus d’informations, consultez <a href="register-filter-pack-ifilters-with-exchange-2013-exchange-2013-help.md">Inscrire les IFilters Filter Pack avec Exchange 2013</a>.</p></td>
<td><p>Exchange 2010 ou version ultérieure</p></td>
</tr>
<tr class="even">
<td><p><strong>Le nom de fichier d'une pièce jointe correspond à</strong></p>
<p><strong>N’importe quelle pièce jointe</strong> &gt; <strong>le nom de fichier correspond à ces modèles de texte</strong></p></td>
<td><p><em>AttachmentNameMatchesPatterns</em></p>
<p><em>ExceptIfAttachmentNameMatchesPatterns</em></p></td>
<td><p><code>Patterns</code></p></td>
<td><p>Messages dans lesquels le nom de fichier d’une pièce jointe contient des modèles de texte qui correspondent aux expressions régulières spécifiées.</p></td>
<td><p>Exchange 2010 ou version ultérieure</p></td>
</tr>
<tr class="odd">
<td><p><strong>L'extension d'un fichier de pièce jointe correspond à</strong></p>
<p><strong>N’importe quelle pièce jointe</strong> &gt; <strong>l’extension de fichier comprend ces mots</strong></p></td>
<td><p><em>AttachmentExtensionMatchesWords</em></p>
<p><em>ExceptIfAttachmentExtensionMatchesWords</em></p></td>
<td><p><code>Words</code></p></td>
<td><p>Messages dans lesquels l’extension de fichier de la pièce jointe correspond à l’un des mots spécifiés.</p></td>
<td><p>Exchange 2013 ou version ultérieure</p></td>
</tr>
<tr class="even">
<td><p><strong>Une pièce jointe présente une taille supérieure ou égale à</strong></p>
<p><strong>N’importe quelle pièce jointe &gt; la taille est supérieure ou égale à</strong></p></td>
<td><p><em>AttachmentSizeOver</em></p>
<p><em>ExceptIfAttachmentSizeOver</em></p></td>
<td><p><code>Size</code></p></td>
<td><p>Messages dans lesquels toutes les pièces jointes sont supérieures ou égales à la valeur spécifiée.</p>
<p>Dans le CAE, vous pouvez uniquement spécifier la taille en kilo-octets (Ko).</p></td>
<td><p>Exchange 2007 ou version ultérieure</p></td>
</tr>
<tr class="odd">
<td><p><strong>Le message n'a pas terminé l'analyse</strong></p>
<p><strong>N’importe quelle pièce jointe</strong> &gt; <strong>n’a pas terminé l’analyse</strong></p></td>
<td><p><em>AttachmentProcessingLimitExceeded</em></p>
<p><em>ExceptIfAttachmentProcessingLimitExceeded</em></p></td>
<td><p>s/o</p></td>
<td><p>Messages pour lesquels le moteur de règles n’a pas pu terminer l’analyse des pièces jointes. Vous pouvez utiliser cette condition pour créer des règles qui fonctionnent conjointement pour identifier et traiter les messages dont le contenu n’a pas pu être entièrement analysé.</p></td>
<td><p>Exchange 2013 ou version ultérieure</p></td>
</tr>
<tr class="even">
<td><p><strong>Une pièce jointe comporte un contenu exécutable</strong></p>
<p><strong>N’importe quelle pièce jointe</strong> &gt; <strong>contient un exécutable</strong></p></td>
<td><p><em>AttachmentHasExecutableContent</em></p>
<p><em>ExceptIfAttachmentHasExecutableContent</em></p></td>
<td><p>s/o</p></td>
<td><p>Messages dans lesquels une pièce jointe est un fichier exécutable. Le système examine les propriétés du fichier au lieu de se fier à l’extension du fichier.</p></td>
<td><p>Exchange 2013 ou version ultérieure</p></td>
</tr>
<tr class="odd">
<td><p><strong>Toutes les pièces jointes sont protégées par mot de passe</strong></p>
<p><strong>N’importe quelle pièce jointe</strong> &gt; <strong>est protégé par mot de passe</strong></p></td>
<td><p><em>AttachmentIsPasswordProtected</em></p>
<p><em>ExceptIfAttachmentIsPasswordProtected</em></p></td>
<td><p>s/o</p></td>
<td><p>Messages dans lesquels une pièce jointe est protégée par mot de passe (et ne peut donc pas être analysée). La détection de mot de passe fonctionne uniquement pour les documents Office et les fichiers .zip.</p></td>
<td><p>Exchange 2013 ou version ultérieure</p></td>
</tr>
</tbody>
</table>


Retour au début

## N’importe quels destinataires

Les conditions et les exceptions de cette section fournissent une fonctionnalité unique qui affecte *tous* les destinataires lorsque le message contient au moins l’un des destinataires spécifiés. Par exemple, supposons que vous disposez d’une règle qui rejette les messages. Si vous utilisez une condition de destinataire à partir de la section Destinataires, le message est uniquement rejeté pour les destinataires spécifiés. Par exemple, si la règle détecte le destinataire spécifié dans un message, mais que le message contient cinq autres destinataires, le message est rejeté pour ce destinataire spécifique et est remis aux cinq autres.

Si vous ajoutez une condition de destinataire à partir de cette section, ce même message est rejeté pour le destinataire détecté et les cinq autres.

À l’inverse, une exception de destinataire à partir de cette section *empêche* l’application de la règle à *tous* les destinataires du message, et non uniquement aux destinataires détectés.

**Remarque** : cette condition ne tient pas compte des messages qui sont envoyés aux adresses proxy du destinataire. Elle correspond uniquement aux messages qui sont envoyés à l’adresse de messagerie principale du destinataire.


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
<th>Condition ou exception dans le CAE</th>
<th>Paramètres de condition et d’exception dans l’Environnement de ligne de commande Exchange Management Shell</th>
<th>Type de propriété</th>
<th>Description</th>
<th>Disponible dans</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Chaque adresse de destinataire comprend</strong></p>
<p><strong>Tout destinataire</strong> &gt; <strong>l’adresse comprend l’un des mots suivants</strong></p></td>
<td><p><em>AnyOfRecipientAddressContainsWords</em></p>
<p><em>ExceptIfAnyOfRecipientAddressContainsWords</em></p></td>
<td><p><code>Words</code></p></td>
<td><p>Messages dans lesquels les champs <strong>To</strong>, <strong>Cc</strong> ou <strong>Bcc</strong> contiennent les mots spécifiés.</p></td>
<td><p>Exchange 2013 ou version ultérieure</p></td>
</tr>
<tr class="even">
<td><p><strong>Chaque adresse de destinataire correspond à</strong></p>
<p><strong>Tout destinataire</strong> &gt; <strong>l’adresse correspond à l’un de ces modèles de texte</strong></p></td>
<td><p><em>AnyOfRecipientAddressMatchesPatterns</em></p>
<p><em>ExceptIfAnyOfRecipientAddressMatchesPatterns</em></p></td>
<td><p><code>Patterns</code></p></td>
<td><p>Messages dans lesquels les champs <strong>To</strong>, <strong>Cc</strong> ou <strong>Bcc</strong> contiennent des modèles de texte qui correspondent aux expressions régulières spécifiées.</p></td>
<td><p>Exchange 2013 ou version ultérieure</p></td>
</tr>
</tbody>
</table>


Retour au début

## Types d’informations sensibles, valeurs À et Cc, taille et jeux de caractères des messages

Les conditions de cette section qui recherchent des valeurs dans les champs **To** et **Cc** se comportent comme les conditions de la section tous les destinataires (*tous les* destinataires du message sont affectés par la règle, pas seulement l’a détectées destinataires).

**Remarque** : cette condition ne tient pas compte des messages qui sont envoyés aux adresses proxy du destinataire. Elle correspond uniquement aux messages qui sont envoyés à l’adresse de messagerie principale du destinataire.


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
<th>Condition ou exception dans le CAE</th>
<th>Paramètres de condition et d’exception dans l’Environnement de ligne de commande Exchange Management Shell</th>
<th>Type de propriété</th>
<th>Description</th>
<th>Disponible dans</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Le message contient des informations sensibles</strong></p>
<p><strong>Le message</strong> &gt; <strong>contient l’un de ces types d’informations sensibles</strong></p></td>
<td><p><em>MessageContainsDataClassifications</em></p>
<p><em>ExceptIfMessageContainsDataClassifications</em></p></td>
<td><p><code>SensitiveInformationTypes</code></p></td>
<td><p>Messages qui contiennent des informations sensibles définies par les stratégies de protection contre la perte de données (DLP).</p>
<p>Cette condition est requise pour les règles utilisant l’action <strong>Notifier l’expéditeur à l’aide d’un conseil de stratégie</strong> (<em>NotifySender</em>).</p></td>
<td><p>Exchange 2013 ou version ultérieure</p></td>
</tr>
<tr class="even">
<td><p><strong>La zone À contient</strong></p>
<p><strong>Le message</strong> &gt; <strong>La zone À contient cette personne</strong></p></td>
<td><p><em>AnyOfToHeader</em></p>
<p><em>ExceptIfAnyOfToHeader</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p>Messages dans lesquels le champ <strong>To</strong> contient l’un des destinataires spécifiés.</p></td>
<td><p>Exchange 2007 ou version ultérieure</p></td>
</tr>
<tr class="odd">
<td><p><strong>La zone À contient un membre de</strong></p>
<p><strong>Le message</strong> &gt; <strong>La zone À contient un membre de ce groupe</strong></p></td>
<td><p><em>AnyOfToHeaderMemberOf</em></p>
<p><em>ExceptIfAnyOfToHeaderMemberOf</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p>Messages dans lesquels le champ <strong>To</strong> contient un destinataire qui est membre du groupe spécifié.</p></td>
<td><p>Exchange 2007 ou version ultérieure</p></td>
</tr>
<tr class="even">
<td><p><strong>La zone Cc contient</strong></p>
<p><strong>Le message</strong> &gt; <strong>La zone Cc contient cette personne</strong></p></td>
<td><p><em>AnyOfCcHeader</em></p>
<p><em>ExceptIfAnyOfCcHeader</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p>Messages dans lesquels le champ <strong>Cc</strong> contient l’un des destinataires spécifiés.</p></td>
<td><p>Exchange 2007 ou version ultérieure</p></td>
</tr>
<tr class="odd">
<td><p><strong>La zone Cc contient un membre de</strong></p>
<p><strong>Le message</strong> &gt; <strong>contient un membre de ce groupe</strong></p></td>
<td><p><em>AnyOfCcHeaderMemberOf</em></p>
<p><em>ExceptIfAnyOfCcHeaderMemberOf</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p>Messages dans lesquels le champ <strong>Cc</strong> contient un destinataire qui est membre du groupe spécifié.</p></td>
<td><p>Exchange 2007 ou version ultérieure</p></td>
</tr>
<tr class="even">
<td><p><strong>La zone À ou Cc contient</strong></p>
<p><strong>Le message</strong> &gt; <strong>La zone À ou Cc contient cette personne</strong></p></td>
<td><p><em>AnyOfToCcHeader</em></p>
<p><em>ExceptIfAnyOfToCcHeader</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p>Messages dans lesquels les champs <strong>To</strong> ou <strong>Cc</strong> contiennent l’un des destinataires spécifiés.</p></td>
<td><p>Exchange 2007 ou version ultérieure</p></td>
</tr>
<tr class="odd">
<td><p><strong>La zone À ou Cc contient un membre de</strong></p>
<p><strong>Le message</strong> &gt; <strong>La zone À ou Cc contient un membre de ce groupe</strong></p></td>
<td><p><em>AnyOfToCcHeaderMemberOf</em></p>
<p><em>ExceptIfAnyOfToCcHeaderMemberOf</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p>Messages dans lesquels les champs <strong>To</strong> ou <strong>Cc</strong> contiennent un destinataire qui est membre du groupe spécifié.</p></td>
<td><p>Exchange 2007 ou version ultérieure</p></td>
</tr>
<tr class="even">
<td><p><strong>La taille du message est supérieure ou égale à</strong></p>
<p><strong>Le message</strong> &gt; <strong>la taille est supérieure ou égale à</strong></p></td>
<td><p><em>MessageSizeOver</em></p>
<p><em>ExceptIfMessageSizeOver</em></p></td>
<td><p><code>Size</code></p></td>
<td><p>Messages dans lesquels la taille totale (message plus pièces jointes) est supérieure ou égale à la valeur spécifiée.</p>
<p>Dans le CAE, vous pouvez uniquement spécifier la taille en kilo-octets (Ko).</p>
<p><strong>Remarque</strong> : Les limites de taille des messages dans les boîtes aux lettres sont évaluées avant les règles de flux de messagerie. Si un message est trop volumineux pour une boîte aux lettres, il est refusé avant qu’une règle avec cette condition puisse agir sur le message.</p></td>
<td><p>Exchange 2013 ou version ultérieure</p></td>
</tr>
<tr class="odd">
<td><p><strong>Le nom du jeu de caractères du message contient l'un de ces mots</strong></p>
<p><strong>Le message</strong> &gt; <strong>le nom du jeu de caractères contient l’un de ces mots</strong></p></td>
<td><p><em>ContentCharacterSetContainsWords</em></p>
<p><em>ExceptIfContentCharacterSetContainsWords</em></p></td>
<td><p><code>CharacterSets</code></p></td>
<td><p>Messages qui contiennent l’un des noms de jeux de caractères spécifiés.</p></td>
<td><p>Exchange 2013 ou version ultérieure</p></td>
</tr>
</tbody>
</table>


Retour au début

## Expéditeur et du destinataire


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
<th>Condition ou exception dans le CAE</th>
<th>Paramètres de condition et d’exception dans l’Environnement de ligne de commande Exchange Management Shell</th>
<th>Type de propriété</th>
<th>Description</th>
<th>Disponible dans</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>L’expéditeur est l’un des destinataires</strong></p>
<p><strong>L’expéditeur et le destinataire</strong> &gt; <strong>la relation de l’expéditeur à un destinataire est</strong></p></td>
<td><p><em>SenderManagementRelationship</em></p>
<p><em>ExceptIfSenderManagementRelationship</em></p></td>
<td><p><code>ManagementRelationship</code></p></td>
<td><p>Messages dans lesquels l’expéditeur est le responsable d’un destinataire ou est sous la responsabilité d’un destinataire.</p></td>
<td><p>Exchange 2010 ou version ultérieure</p></td>
</tr>
<tr class="even">
<td><p><strong>Le message est entre les membres de ces groupes</strong></p>
<p><strong>L’expéditeur et le destinataire</strong> &gt; <strong>le message est entre les membres de ces groupes</strong></p></td>
<td><p><em>BetweenMemberOf1</em> et <em>BetweenMemberOf2</em></p>
<p><em>ExceptIfBetweenMemberOf1</em> et <em>ExceptIfBetweenMemberOf2</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p>Messages envoyés entre les membres des groupes spécifiés.</p></td>
<td><p>Exchange 2007 ou version ultérieure</p></td>
</tr>
<tr class="odd">
<td><p><strong>Le responsable de l'expéditeur ou du destinataire est</strong></p>
<p><strong>L’expéditeur et le destinataire</strong> &gt; <strong>le responsable de l’expéditeur ou du destinataire est cette personne</strong></p></td>
<td><p><em>ManagerForEvaluatedUser</em> et <em>ManagerAddress</em></p>
<p><em>ExceptIfManagerForEvaluatedUser</em> et <em>ExceptIfManagerAddress</em></p></td>
<td><p>Première propriété : <code>EvaluatedUser</code></p>
<p>Deuxième propriété : <code>Addresses</code></p></td>
<td><p>Messages dans lesquels un utilisateur spécifié est le responsable de l’expéditeur, ou un utilisateur spécifié est le responsable d’un destinataire.</p></td>
<td><p>Exchange 2010 ou version ultérieure</p></td>
</tr>
<tr class="even">
<td><p><strong>La propriété de l'expéditeur et de n'importe quel destinataire compare</strong></p>
<p><strong>L’expéditeur et le destinataire</strong> &gt; <strong>la propriété de l’expéditeur et celle des destinataires sont considérées comme</strong></p></td>
<td><p><em>ADAttributeComparisonAttribute</em> et <em>ADComparisonOperator</em></p>
<p><em>ExceptIfADAttributeComparisonAttribute</em> et <em>ExceptIfADComparisonOperator</em></p></td>
<td><p>Première propriété : <code>ADAttribute</code></p>
<p>Deuxième propriété : <code>Evaluation</code></p></td>
<td><p>Messages dans lesquels l’attribut Active Directory spécifié pour l’expéditeur et le destinataire correspond ou ne correspond pas.</p></td>
<td><p>Exchange 2010 ou version ultérieure</p></td>
</tr>
</tbody>
</table>


Retour au début

## Propriétés de message


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
<th>Condition ou exception dans le CAE</th>
<th>Paramètres de condition et d’exception dans l’Environnement de ligne de commande Exchange Management Shell</th>
<th>Type de propriété</th>
<th>Description</th>
<th>Disponible dans</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Le type de message est</strong></p>
<p><strong>Les propriétés du message</strong> &gt; <strong>inclure le type de message</strong></p></td>
<td><p><em>MessageTypeMatches</em></p>
<p><em>ExceptIfMessageTypeMatches</em></p></td>
<td><p><code>MessageType</code></p></td>
<td><p>Messages du type spécifié.</p>
<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Lors de la Outlook ou Outlook Web App est configuré pour transférer un message, la propriété <strong>ForwardingSmtpAddress</strong> est ajoutée au message. Le type de message n’est pas modifié pour <code>AutoForward</code>.</td>
</tr>
</tbody>
</table>

</td>
<td><p>Exchange 2010 ou version ultérieure</p></td>
</tr>
<tr class="even">
<td><p><strong>Le message est classé comme</strong></p>
<p><strong>Les propriétés du message</strong> &gt; <strong>incluent cette classification</strong></p></td>
<td><p><em>HasClassification</em></p>
<p><em>ExceptIfHasClassification</em></p></td>
<td><p><code>MessageClassification</code></p></td>
<td><p>Messages qui ont la classification de message spécifiée. Il s’agit d’une classification personnalisée des messages que vous pouvez créer dans votre organisation à l’aide de la cmdlet <strong>New-MessageClassification</strong>.</p></td>
<td><p>Exchange 2007 ou version ultérieure</p></td>
</tr>
<tr class="odd">
<td><p><strong>Le message n'est doté d'aucune classification</strong></p>
<p><strong>Les propriétés du message</strong> &gt; <strong>n’incluent aucune classification</strong></p></td>
<td><p><em>HasNoClassification</em></p>
<p><em>ExceptIfHasNoClassification</em></p></td>
<td><p>s/o</p></td>
<td><p>Messages qui n’ont pas de classification de messages.</p></td>
<td><p>Exchange 2010 ou version ultérieure</p></td>
</tr>
<tr class="even">
<td><p><strong>Le message a un seuil de probabilité de courrier indésirable supérieur ou égal à</strong></p>
<p><strong>Les propriétés du message</strong> &gt; <strong>incluent un seuil SCL supérieur ou égal à</strong></p></td>
<td><p><em>SCLOver</em></p>
<p><em>ExceptIfSCLOver</em></p></td>
<td><p><code>SCLValue</code></p></td>
<td><p>Messages auxquels un seuil de probabilité de courrier indésirable (SCL) supérieur ou égal à la valeur spécifiée est affecté.</p></td>
<td><p>Exchange 2007 ou version ultérieure</p></td>
</tr>
<tr class="odd">
<td><p><strong>La valeur de l'importance du message est définie sur</strong></p>
<p><strong>Les propriétés du message</strong> &gt; <strong>incluent le niveau d’importance</strong></p></td>
<td><p><em>WithImportance</em></p>
<p><em>ExceptIfWithImportance</em></p></td>
<td><p><code>Importance</code></p></td>
<td><p>Messages marqués avec le niveau d’importance spécifié.</p></td>
<td><p>Exchange 2007 ou version ultérieure</p></td>
</tr>
</tbody>
</table>


Retour au début

## En-têtes de message

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>La recherche de mots clés ou de modèles de texte dans l’objet ou dans d’autres champs d’en-tête du message est effectuée <em>après</em> que le codage utilisé avec la méthode MIME pour transmettre le message binaire entre les serveurs SMTP a été décodé en texte ASCII. Vous ne pouvez pas utiliser de conditions ou d’exceptions pour rechercher les valeurs codées brutes (en règle générale, en base 64) dans l’objet ou d’autres champs d’en-tête des messages.</td>
</tr>
</tbody>
</table>



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
<th>Condition ou exception dans le CAE</th>
<th>Paramètres de condition et d’exception dans l’Environnement de ligne de commande Exchange Management Shell</th>
<th>Type de propriété</th>
<th>Description</th>
<th>Disponible dans</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Un en-tête de message inclut</strong></p>
<p><strong>Un en-tête de message</strong> &gt; <strong>inclut l’un de ces mots</strong></p></td>
<td><p><em>HeaderContainsMessageHeader</em> et <em>HeaderContainsWords</em></p>
<p><em>ExceptIfHeaderContainsMessageHeader</em> et <em>ExceptIfHeaderContainsWords</em></p></td>
<td><p>Première propriété : <code>MessageHeaderField</code></p>
<p>Deuxième propriété : <code>Words</code></p></td>
<td><p>Les messages qui contiennent le champ d’en-tête spécifié et la valeur de ce champ d’en-tête contient les mots spécifiés.</p>
<p>Le nom du champ d’en-tête et la valeur du champ d’en-tête sont toujours utilisés ensemble.</p></td>
<td><p>Exchange 2007 ou version ultérieure</p></td>
</tr>
<tr class="even">
<td><p><strong>Un en-tête de message correspond à</strong></p>
<p><strong>Un en-tête de message</strong> &gt; <strong>correspond à ces modèles de texte</strong></p></td>
<td><p><em>HeaderMatchesMessageHeader</em> et <em>HeaderMatchesPatterns</em></p>
<p><em>ExceptIfHeaderMatchesMessageHeader</em> et <em>ExceptIfHeaderMatchesPatterns</em></p></td>
<td><p>Première propriété : <code>MessageHeaderField</code></p>
<p>Deuxième propriété : <code>Patterns</code></p></td>
<td><p>Les messages qui contiennent le champ d’en-tête spécifié et la valeur de ce champ d’en-tête contient les expressions régulières spécifiées.</p>
<p>Le nom du champ d’en-tête et la valeur du champ d’en-tête sont toujours utilisés ensemble.</p></td>
<td><p>Exchange 2007 ou version ultérieure</p></td>
</tr>
</tbody>
</table>


Retour au début

## Conditions et exceptions pour les règles de flux de messagerie sur les serveurs de transport Edge

Les conditions et les exceptions disponibles dans les règles de flux de messagerie sur les serveurs de transport Edge sont un petit sous-ensemble des celles disponibles sur les serveurs de boîte aux lettres. Il n’y a aucun CAE sur les serveurs de transport Edge ; en l’occurrence, vous pouvez uniquement gérer les règles de flux de messagerie dans l’Environnement de ligne de commande Exchange Management Shell du serveur de transport Edge local. Les conditions et les exceptions sont décrites dans le tableau suivant. Les types de propriétés sont décrits dans la section Types de propriétés.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Paramètres de condition et d’exception dans l’Environnement de ligne de commande Exchange Management Shell</th>
<th>Type de propriété</th>
<th>Description</th>
<th>Disponible dans</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>AnyOfRecipientAddressContainsWords</em></p>
<p><em>ExceptIfAnyOfRecipientAddressContainsWords</em></p></td>
<td><p><code>Words</code></p></td>
<td><p>Messages dans lesquels les champs <strong>To</strong>, <strong>Cc</strong> ou <strong>Bcc</strong> contiennent des mots spécifiés.</p>
<p>Lorsqu’un message contient le destinataire spécifié, l’action de règle est appliquée (ou non appliquée) à <em>tous les</em> destinataires du message. Par exemple, le message est rejeté pour tous les destinataires du message, et pas uniquement pour le destinataire spécifié.</p></td>
<td><p>Exchange 2013 ou version ultérieure</p></td>
</tr>
<tr class="even">
<td><p><em>AnyOfRecipientAddressMatchesPatterns</em></p>
<p><em>ExceptIfAnyOfRecipientAddressMatchesPatterns</em></p></td>
<td><p><code>Patterns</code></p></td>
<td><p>Messages dans lesquels les champs <strong>To</strong>, <strong>Cc</strong> ou <strong>Bcc</strong> contiennent des modèles de texte qui correspondent aux expressions régulières spécifiées.</p>
<p>Lorsqu’un message contient le destinataire spécifié, l’action de règle est appliquée (ou non appliquée) à <em>tous les</em> destinataires du message. Par exemple, le message est rejeté pour tous les destinataires du message, et pas uniquement pour le destinataire spécifié.</p></td>
<td><p>Exchange 2013 ou version ultérieure</p></td>
</tr>
<tr class="odd">
<td><p><em>AttachmentSizeOver</em></p>
<p><em>ExceptIfAttachmentSizeOver</em></p></td>
<td><p><code>Size</code></p></td>
<td><p>Messages avec des pièces jointes dans lesquels n’importe quelle pièce jointe est supérieure ou égale à la valeur spécifiée.</p></td>
<td><p>Exchange 2007 ou version ultérieure</p></td>
</tr>
<tr class="even">
<td><p><em>FromAddressContainsWords</em></p>
<p><em>ExceptIfFromAddressContainsWords</em></p></td>
<td><p><code>Words</code></p></td>
<td><p>Messages contenant les mots spécifiés dans l’adresse de l’expéditeur.</p></td>
<td><p>Exchange 2007 ou version ultérieure</p></td>
</tr>
<tr class="odd">
<td><p><em>FromAddressMatchesPatterns</em></p>
<p><em>ExceptIfFromAddressMatchesPatterns</em></p></td>
<td><p><code>Patterns</code></p></td>
<td><p>Messages dans lesquels l’adresse de messagerie de l’expéditeur contient des modèles de texte qui correspondent aux expressions régulières spécifiées.</p></td>
<td><p>Exchange 2007 ou version ultérieure</p></td>
</tr>
<tr class="even">
<td><p><em>FromScope</em></p>
<p><em>ExceptIfFromScope</em></p></td>
<td><p><code>UserScopeFrom</code></p></td>
<td><p>Messages envoyés par des expéditeurs internes ou externes.</p></td>
<td><p>Exchange 2007 ou version ultérieure</p></td>
</tr>
<tr class="odd">
<td><p><em>HeaderContainsMessageHeader</em> et <em>HeaderContainsWords</em></p>
<p><em>ExceptIfHeaderContainsMessageHeader</em> et <em>ExceptIfHeaderContainsWords</em></p></td>
<td><p>Première propriété : <code>MessageHeaderField</code></p>
<p>Deuxième propriété : <code>Words</code></p></td>
<td><p>Les messages qui contiennent le champ d’en-tête spécifié et la valeur de ce champ d’en-tête contient les mots spécifiés.</p>
<p>Le nom du champ d’en-tête et la valeur du champ d’en-tête sont toujours utilisés ensemble.</p></td>
<td><p>Exchange 2007 ou version ultérieure</p></td>
</tr>
<tr class="even">
<td><p><em>HeaderMatchesMessageHeader</em> et <em>HeaderMatchesPatterns</em></p>
<p><em>ExceptIfHeaderMatchesMessageHeader</em> et <em>ExceptIfHeaderMatchesPatterns</em></p></td>
<td><p>Première propriété : <code>MessageHeaderField</code></p>
<p>Deuxième propriété : <code>Patterns</code></p></td>
<td><p>Les messages qui contiennent le champ d’en-tête spécifié et la valeur de ce champ d’en-tête contient les expressions régulières spécifiées.</p>
<p>Le nom du champ d’en-tête et la valeur du champ d’en-tête sont toujours utilisés ensemble.</p></td>
<td><p>Exchange 2007 ou version ultérieure</p></td>
</tr>
<tr class="odd">
<td><p><em>MessageSizeOver</em></p>
<p><em>ExceptIfMessageSizeOver</em></p></td>
<td><p><code>Size</code></p></td>
<td><p>Messages dans lesquels la taille totale (message plus pièces jointes) est supérieure ou égale à la valeur spécifiée.</p></td>
<td><p>Exchange 2013 ou version ultérieure</p></td>
</tr>
<tr class="even">
<td><p><em>SCLOver</em></p>
<p><em>ExceptIfSCLOver</em></p></td>
<td><p><code>SCLValue</code></p></td>
<td><p>Messages auxquels un seuil de probabilité de courrier indésirable (SCL) supérieur ou égal à la valeur spécifiée est affecté.</p></td>
<td><p>Exchange 2007 ou version ultérieure</p></td>
</tr>
<tr class="odd">
<td><p><em>SubjectContainsWords</em></p>
<p><em>ExceptIfSubjectContainsWords</em></p></td>
<td><p><code>Words</code></p></td>
<td><p>Messages dans lesquels le champ <strong>Subject</strong> contient les mots spécifiés.</p></td>
<td><p>Exchange 2007 ou version ultérieure</p></td>
</tr>
<tr class="even">
<td><p><em>SubjectMatchesPatterns</em></p>
<p><em>ExceptIfSubjectMatchesPatterns</em></p></td>
<td><p><code>Patterns</code></p></td>
<td><p>Messages dans lesquels le champ <strong>Subject</strong> contient des modèles de texte qui correspondent aux expressions régulières spécifiées.</p></td>
<td><p>Exchange 2007 ou version ultérieure</p></td>
</tr>
<tr class="odd">
<td><p><em>SubjectOrBodyContainsWords</em></p>
<p><em>ExceptIfSubjectOrBodyContainsWords</em></p></td>
<td><p><code>Words</code></p></td>
<td><p>Messages dans lesquels le champ <strong>Subject</strong> ou le corps contient les mots spécifiés.</p></td>
<td><p>Exchange 2007 ou version ultérieure</p></td>
</tr>
<tr class="even">
<td><p><em>SubjectOrBodyMatchesPatterns</em></p>
<p><em>ExceptIfSubjectOrBodyMatchesPatterns</em></p></td>
<td><p><code>Patterns</code></p></td>
<td><p>Messages dans lesquels le champ <strong>Subject</strong> ou le corps du message contient des modèles de texte qui correspondent aux expressions régulières spécifiées.</p></td>
<td><p>Exchange 2007 ou version ultérieure</p></td>
</tr>
</tbody>
</table>


Retour au début

## Types de propriétés

Les types de propriétés utilisés dans les conditions et les exceptions sont décrits dans le tableau suivant.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Si la propriété est une chaîne, les espaces ne sont pas autorisés.</td>
</tr>
</tbody>
</table>



<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Type de propriété</th>
<th>Valeurs admises</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>ADAttribute</code></p></td>
<td><p>Sélectionner dans une liste prédéfinie d’attributs Active Directory</p></td>
<td><p>UNRESOLVED_TOKENBLOCK_VAL(PD_Transport_Rules_ADAttributes_Snippet)</p>
<p>Dans le CAE, si vous souhaitez spécifier plusieurs mots ou modèles de texte pour un même attribut, séparez les valeurs par des virgules. Par exemple, la valeur <strong>San Francisco,Palo Alto</strong> pour l’attribut <strong>Ville</strong> recherche « Ville est égale à San Francisco » ou « Ville est égale à Palo Alto ».</p>
<p>Dans l’Environnement de ligne de commande Exchange Management Shell, utilisez la syntaxe <code>&quot;AttributeName1:Value1,Value 2 with spaces,Value3...&quot;,&quot;AttributeName2:Word4,Value 5 with spaces,Value6...&quot;</code>, où <code>Value</code> est le modèle de mots ou de texte que vous voulez faire correspondre.</p>
<p>Par exemple, <code>&quot;City:San Francisco,Palo Alto&quot;</code> ou <code>&quot;City:San Francisco,Palo Alto&quot;</code>,<code>&quot;Department:Sales,Finance&quot;</code>.</p>
<p>Lorsque vous spécifiez plusieurs attributs ou plusieurs valeurs pour un même attribut, l’opérateur <strong>or</strong> est utilisé. N’utilisez pas de valeurs avec espaces de début ou de fin.</p>
<p>Notez que l’attribut <strong>Country</strong> requiert la valeur de code pays ISO 3166-1 à deux lettres (par exemple, DE pour l’Allemagne). Pour rechercher des valeurs, consultez <a href="https://go.microsoft.com/fwlink/p/?linkid=331680">https://go.microsoft.com/fwlink/p/?LinkId=331680</a>.</p></td>
</tr>
<tr class="even">
<td><p><code>Addresses</code></p></td>
<td><p>Destinataires Exchange</p></td>
<td><p>En fonction de la nature de la condition ou de l’exception, il se peut que vous ne puissiez pas spécifier n’importe quel objet à extension messagerie de l’organisation (par exemple, pour des conditions concernant le destinataire) ou que vous soyez limité à un type d’objet spécifique (par exemple, les groupes pour des conditions d’appartenance à un groupe). Par ailleurs, la condition ou l’exception peut nécessiter une seule valeur ou en accepter plusieurs.</p>
<p>Dans l’Environnement de ligne de commande Exchange Management Shell, séparez les valeurs multiples à l’aide de virgules.</p>
<p><strong>Remarque</strong> : cette condition ne tient pas compte des messages qui sont envoyés aux adresses proxy du destinataire. Elle correspond uniquement aux messages qui sont envoyés à l’adresse de messagerie principale du destinataire.</p></td>
</tr>
<tr class="odd">
<td><p><code>CharacterSets</code></p></td>
<td><p>Tableau de noms de jeux de caractères</p></td>
<td><p>Un ou plusieurs jeux de caractères de contenu qui existent dans un message. Par exemple :</p>
<ul>
<li><p><code>Arabic/iso-8859-6</code></p></li>
<li><p><code>Chinese/big5</code></p></li>
<li><p><code>Chinese/euc-cn</code></p></li>
<li><p><code>Chinese/euc-tw</code></p></li>
<li><p><code>Chinese/gb2312</code></p></li>
<li><p><code>Chinese/iso-2022-cn</code></p></li>
<li><p><code>Cyrillic/iso-8859-5</code></p></li>
<li><p><code>Cyrillic/koi8-r</code></p></li>
<li><p><code>Cyrillic/windows-1251</code></p></li>
<li><p><code>Greek/iso-8859-7</code></p></li>
<li><p><code>Hebrew/iso-8859-8</code></p></li>
<li><p><code>Japanese/euc-jp</code></p></li>
<li><p><code>Japanese/iso-022-jp</code></p></li>
<li><p><code>Japanese/shift-jis</code></p></li>
<li><p><code>Korean/euc-kr</code></p></li>
<li><p><code>Korean/johab</code></p></li>
<li><p><code>Korean/ks_c_5601-1987</code></p></li>
<li><p><code>Turkish/windows-1254</code></p></li>
<li><p><code>Turkish/iso-8859-9</code></p></li>
<li><p><code>Vietnamese/tcvn</code></p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><code>DomainName</code></p></td>
<td><p>Tableau de domaines SMTP</p></td>
<td><p>Par exemple, <code>contoso.com</code> ou <code>eu.contoso.com</code>.</p>
<p>Dans l’Environnement de ligne de commande Exchange Management Shell, vous pouvez spécifier plusieurs domaines séparés par des virgules.</p></td>
</tr>
<tr class="odd">
<td><p><code>EvaluatedUser</code></p></td>
<td><p>Valeur unique <strong>Expéditeur</strong> ou <strong>Destinataire</strong></p></td>
<td><p>Indique si la règle recherche le responsable de l’expéditeur ou le responsable du destinataire.</p></td>
</tr>
<tr class="even">
<td><p><code>Evaluation</code></p></td>
<td><p>Valeur unique <strong>Égal</strong> ou <strong>Différent de</strong> (<code>NotEqual</code>)</p></td>
<td><p>Lorsque vous comparez les attributs Active Directory de l’expéditeur et des destinataires, indique si les valeurs doivent correspondre ou non.</p></td>
</tr>
<tr class="odd">
<td><p><code>Importance</code></p></td>
<td><p>Valeur unique <strong>Faible</strong>, <strong>Normal</strong> ou <strong>Élevé</strong></p></td>
<td><p>Le niveau d’Importance attribué au message par l’expéditeur dans Outlook ou Outlook Web App.</p></td>
</tr>
<tr class="even">
<td><p><code>IPAddressRanges</code></p></td>
<td><p>Tableau d’adresses ou de plages d’adresses IP</p></td>
<td><p>Entrez les adresses IPv4 à l’aide de la syntaxe suivante :</p>
<ul>
<li><p><strong>Adresse IP unique</strong>   Par exemple, <code>192.168.1.1</code>.</p></li>
<li><p><strong>Plage d’adresses IP</strong>   Par exemple, <code>192.168.0.1-192.168.0.254</code>.</p></li>
<li><p><strong>Plage d’adresses IP CIDR (Classless InterDomain Routing)</strong>   Par exemple, <code>192.168.0.1/25</code>.</p></li>
</ul>
<p>Dans l’Environnement de ligne de commande Exchange Management Shell, vous pouvez spécifier plusieurs adresses ou plages d’adresses IP séparées par des virgules.</p></td>
</tr>
<tr class="odd">
<td><p><code>ManagementRelationship</code></p></td>
<td><p>Valeur unique <strong>Responsable</strong> ou <strong>Collaborateur direct</strong> (<code>DirectReport</code>)</p></td>
<td><p>Spécifie la relation entre l’expéditeur et n’importe lequel des destinataires. La règle contrôle l’attribut <strong>Manager</strong> dans Active Directory pour voir si l’expéditeur est le responsable d’un destinataire ou si l’expéditeur est sous la responsabilité d’un destinataire.</p></td>
</tr>
<tr class="even">
<td><p><code>MessageClassification</code></p></td>
<td><p>Classification des messages unique</p></td>
<td><p>Dans le CAE, effectuez une sélection dans la liste des classifications de messages que vous avez créée.</p>
<p>Dans l’Environnement de ligne de commande Exchange Management Shell, utilisez la cmdlet <strong>Get-MessageClassification</strong> pour identifier la classification des messages. Par exemple, utilisez la commande suivante pour rechercher les messages dont la classification est <code>Company Internal</code> et ajouter la valeur <code>CompanyInternal</code> à l’objet du message.</p>
<p><code>New-TransportRule &quot;Rule Name&quot; -HasClassification @(Get-MessageClassification &quot;Company Internal&quot;).Identity -PrependSubject &quot;CompanyInternal&quot;</code></p></td>
</tr>
<tr class="odd">
<td><p><code>MessageHeaderField</code></p></td>
<td><p>Chaîne unique</p></td>
<td><p>Spécifie le nom du champ d’en-tête. Le nom du champ d’en-tête est toujours associé à la valeur dans le champ d’en-tête (correspondance de modèle word ou texte).</p>
<p>L’<em>en-tête de message</em> est un ensemble de champs d’en-tête obligatoires et facultatifs dans le message. Exemples de champs d’en-tête : <strong>To</strong>, <strong>From</strong>, <strong>Received</strong> et <strong>Content-Type</strong>. Les champs d’en-tête officiels sont définis dans le document RFC 5322. Les champs d’en-tête non officiels commencent par <strong>X-</strong> et sont appelés <em>en-têtes X</em>.</p></td>
</tr>
<tr class="even">
<td><p><code>MessageType</code></p></td>
<td><p>Valeur de type de message unique</p></td>
<td><p>Spécifie l’un des types de messages suivants :</p>
<ul>
<li><p><strong>Réponse automatique</strong> (<code>OOF</code>)</p></li>
<li><p><strong>Transfert automatique</strong> (<code>AutoForward</code>)</p></li>
<li><p><strong>Chiffré</strong></p></li>
<li><p><strong>Calendrier</strong></p></li>
<li><p><strong>Contrôlé par autorisation</strong> (<code>PermissionControlled</code>)</p></li>
<li><p><strong>Messagerie vocale</strong></p></li>
<li><p><strong>Signé</strong></p></li>
<li><p><strong>Demande d’approbation</strong> (<code>ApprovalRequest</code>)</p></li>
<li><p><strong>Confirmation de lecture</strong> (<code>ReadReceipt</code>)</p></li>
</ul>
<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Lors de la Outlook ou Outlook Web App est configuré pour transférer un message, la propriété <strong>ForwardingSmtpAddress</strong> est ajoutée au message. Le type de message n’est pas modifié pour <code>AutoForward</code>.</td>
</tr>
</tbody>
</table>

</td>
</tr>
<tr class="odd">
<td><p><code>Patterns</code></p></td>
<td><p>Tableau d’expressions régulières</p></td>
<td><p>Spécifie une ou plusieurs expressions régulières utilisées pour identifier les modèles de texte dans les valeurs. Pour plus d’informations, voir <a href="https://go.microsoft.com/fwlink/p/?linkid=180327">Syntaxe des expressions régulières</a>.</p>
<p>Dans l’Environnement de ligne de commande Exchange Management Shell, vous spécifiez plusieurs expressions régulières séparées par des virgules et placez chaque expression régulière entre guillemets (&quot;).</p></td>
</tr>
<tr class="even">
<td><p><code>SCLValue</code></p></td>
<td><p>Une des valeurs suivantes :</p>
<ul>
<li><p><strong>Contourner le filtrage du courrier indésirable</strong> (<code>-1</code>)</p></li>
<li><p>Nombres entiers entre 0 et 9</p></li>
</ul></td>
<td><p>Indique le seuil de probabilité de courrier indésirable (SCL) affecté à un message. Plus la valeur est élevée, plus il est probable que le message soit un courrier indésirable.</p></td>
</tr>
<tr class="odd">
<td><p><code>SensitiveInformationTypes</code></p></td>
<td><p>Tableau des types d’informations sensibles</p></td>
<td><p>Spécifie un ou plusieurs types d’informations sensibles qui sont définis dans votre organisation. Pour obtenir une liste des types d’informations sensibles intégrées, consultez <a href="what-the-sensitive-information-types-in-exchange-look-for-exchange-online-help.md">Éléments recherchés par les types d’informations sensibles dans Exchange</a>.</p>
<p>Dans l’Environnement de ligne de commande Exchange Management Shell, utilisez la syntaxe <code>@{&lt;SensitiveInformationType1&gt;},@{&lt;SensitiveInformationType2&gt;},...</code>. Par exemple, pour rechercher du contenu qui contient au moins deux numéros de carte de crédit et au moins un numéro de routage ABA, utilisez la valeur <code>@{Name=&quot;Credit Card Number&quot;; minCount=&quot;2&quot;},@{Name=&quot;ABA Routing Number&quot;; minCount=&quot;1&quot;}</code>.</p></td>
</tr>
<tr class="even">
<td><p><code>Size</code></p></td>
<td><p>Valeur de taille unique</p></td>
<td><p>Spécifie la taille d’une pièce jointe ou de l’ensemble du message.</p>
<p>Dans le CAE, vous pouvez uniquement spécifier la taille en kilo-octets (Ko).</p>
<p>Dans l’Environnement de ligne de commande Exchange Management Shell, lorsque vous entrez une valeur, qualifiez-la à l’aide de l’une des unités suivantes :</p>
<ul>
<li><p><code>B</code> (octets)</p></li>
<li><p><code>KB</code> (kilo-octets)</p></li>
<li><p><code>MB</code> (mégaoctets)</p></li>
<li><p><code>GB</code> (gigaoctets)</p></li>
</ul>
<p>Par exemple, <code>20MB</code></p>
<p>Les valeurs non qualifiées sont généralement traitées comme des octets, mais les petites valeurs peuvent être arrondies au kilo-octet le plus proche.</p></td>
</tr>
<tr class="odd">
<td><p><code>UserScopeFrom</code></p></td>
<td><p>Valeur unique <strong>Dans l’organisation</strong> (<code>InOrganization</code>) ou <strong>Hors de l’organisation</strong> (<code>NotInOrganization</code>)</p></td>
<td><p>Un expéditeur est considéré comme étant situé à l’intérieur de l’organisation si l’une des conditions suivantes est vraie :</p>
<ul>
<li><p>L’expéditeur est une boîte aux lettres, un utilisateur de messagerie, un groupe ou un dossier public à extension messagerie existant au sein de l’Active Directory de l’organisation.</p></li>
<li><p>Adresse e-mail de l’expéditeur est dans un domaine accepté configuré comme domaine faisant autorité ou un domaine de relais interne, <strong>et</strong> le message a été envoyé ou reçu via une connexion authentifiée. Pour plus d’informations sur les domaines acceptés, consultez <a href="accepted-domains-exchange-2013-help.md">Domaines acceptés</a>.</p></li>
</ul>
<p>Un expéditeur est considéré comme étant situé hors de l’organisation si l’une des conditions suivantes est vraie :</p>
<ul>
<li><p>L’adresse de messagerie de l’expéditeur n’est pas dans un domaine accepté.</p></li>
<li><p>L’adresse de messagerie de l’expéditeur est dans un domaine accepté configuré en tant que domaine de relais externe.</p></li>
</ul>
<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Pour déterminer si des contacts de messagerie sont considérés comme étant situés à l’intérieur ou à l’extérieur de l’organisation, l’adresse de l’expéditeur est comparée aux domaines acceptés de l’organisation.</td>
</tr>
</tbody>
</table>

</td>
</tr>
<tr class="even">
<td><p><code>UserScopeTo</code></p></td>
<td><p>Une des valeurs suivantes :</p>
<ul>
<li><p><strong>Dans l’organisation</strong> (<code>InOrganization</code>)</p></li>
<li><p><strong>Hors de l’organisation</strong> (<code>NotInOrganization</code>)</p></li>
<li><p><strong>Dans une organisation partenaire externe</strong> (<code>ExternalPartner</code>)</p></li>
<li><p><strong>Dans une organisation non partenaire externe</strong> (<code>ExternalNonPartner</code>)</p></li>
</ul></td>
<td><p>Un destinataire est considéré comme étant situé à l’intérieur de l’organisation si l’une des conditions suivantes est vraie :</p>
<ul>
<li><p>Le destinataire est une boîte aux lettres, un utilisateur de messagerie, un groupe ou un dossier public à extension messagerie existant au sein de l’Active Directory de l’organisation.</p></li>
<li><p>L’adresse de messagerie du destinataire se trouve dans un domaine accepté configuré en tant que domaine faisant autorité ou un domaine de relais interne, <strong>et</strong> le message a été envoyé ou reçu via une connexion authentifiée.</p></li>
</ul>
<p>Un destinataire est considéré comme étant situé hors de l’organisation si l’une des conditions suivantes est vraie :</p>
<ul>
<li><p>L’adresse de messagerie du destinataire n’est pas dans un domaine accepté.</p></li>
<li><p>L’adresse de messagerie du destinataire est dans un domaine accepté configuré en tant que domaine de relais externe.</p></li>
</ul>
<p>Les organisations partenaires externes sont des domaines externes dans lesquels vous avez configuré la sécurité de domaine (authentification TLS mutuelle) pour l’envoi de messages.</p>
<p>Les organisations non partenaires externes sont tous les autres domaines externes qui ne sont pas considérés comme des domaines partenaires.</p></td>
</tr>
<tr class="odd">
<td><p><code>Words</code></p></td>
<td><p>Tableau de chaînes</p></td>
<td><p>Spécifie un ou plusieurs mots à rechercher. Les mots ne tiennent pas compte de la casse et peuvent être entourés d’espaces et de signes de ponctuation. Les caractères génériques et les correspondances partielles ne sont pas pris en charge.</p>
<p>Par exemple, « contoso » génère les mêmes résultats que « Contoso. ». Toutefois, si le texte est entouré d’autres caractères, il n’est pas considéré comme constituant une correspondance. Par exemple, « contoso » ne correspond pas aux valeurs suivantes :</p>
<ul>
<li><p>Acontoso</p></li>
<li><p>Contosoa</p></li>
<li><p>Acontosob</p></li>
</ul>
<p>L’astérisque (*) est traité comme un caractère littéral et n’est pas utilisé comme caractère générique.</p></td>
</tr>
</tbody>
</table>


Retour au début

## Pour plus d'informations

[Règles de transport ou de flux de messagerie](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md)

[Actions de règle de transport](mail-flow-rule-actions-in-exchange-2013-exchange-2013-help.md)

[Procédures de règle transport ou de flux de messagerie](mail-flow-or-transport-rule-procedures-exchange-2013-help.md)

[Exceptions (prédicat) et conditions de règles de flux de messagerie dans Exchange Online](https://technet.microsoft.com/fr-fr/library/jj919235\(v=exchg.150\)) pour Exchange Online

[Mail flux conditions et les exceptions (prédicat) dans Exchange Online Protection](https://technet.microsoft.com/fr-fr/library/jj919234\(v=exchg.150\)) pour Exchange Online Protection

