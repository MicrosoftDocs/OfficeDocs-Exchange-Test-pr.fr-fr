---
title: 'Options d’encodage des messages: Exchange 2013 Help'
TOCTitle: Options d’encodage des messages
ms:assetid: c1d9edbb-d87c-41e5-881b-cd612d83d7e4
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb310794(v=EXCHG.150)
ms:contentKeyID: 50479138
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Options d’encodage des messages

 

_**Sapplique à :** Exchange Online, Exchange Server 2013_

_**Dernière rubrique modifiée :** 2016-12-09_

Les options de codage des messages disponibles dans Microsoft Exchange spécifient les caractéristiques des messages, comme les jeux de caractères MIME et non MIME, le codage binaire et le format des pièces jointes. Vous pouvez spécifier les options de codage des messages aux emplacements suivants :

  - paramètres de domaine distant

  - paramètres d’utilisateur et de contact de messagerie

  - Paramètres Microsoft Outlook
    
      - format des messages
    
      - format de message Internet
    
      - Format de message de destinataire Internet
    
      - options de codage de jeu de caractères de message

**Contenu**

Options de codage de messages pour les messages envoyés aux domaines distants

Options de codage de messages pour des contacts et des utilisateurs de messagerie

Options de codage des messages disponibles dans Outlook

Options d’encodage des messages disponibles dans Outlook Web App

Ordre de priorité des options de codage des messages

Pour plus d'informations

## Options de codage de messages pour les messages envoyés aux domaines distants

Lorsque vous configurez les options de codage de messages pour un domaine distant, les paramètres spécifiques sont appliqués à tous les messages envoyés à ce domaine. Pour les domaines distants de votre organisation, les options suivantes d’encodage des messages sont mises à votre disposition :


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>Paramètre</strong></p></td>
<td><p><strong>Disponible dans le Centre d’administration Exchange (EAC) dans Exchange Online Dedicated</strong></p></td>
<td><p><strong>Disponible dans l’environnement de ligne de commande Exchange Management Shell</strong></p></td>
</tr>
<tr class="even">
<td><p><strong>Jeu de caractères MIME</strong>   Le jeu de caractères que vous spécifiez sera utilisé uniquement pour les messages MIME qui n’ont pas de jeu de caractères spécifié. La définition de ce paramètre ne remplacera pas les jeux de caractères qui sont déjà spécifiés dans le courrier sortant.</p>
<p><strong>Jeu de caractères non MIME</strong>   Ce paramètre est utilisé si l’une des conditions suivantes est définie sur true :</p>
<ul>
<li><p>messages entrants provenant d’un domaine distant et dont la valeur du paramètre <em>charset=</em> est manquante dans le champ de l’en-tête MIME Content-Type: Type de contenu MIME</p></li>
<li><p>La valeur du jeu de caractères MIME est manquante dans les messages sortants à destination d’un domaine distant.</p></li>
</ul>
<p></p></td>
<td><p>Oui</p></td>
<td><p>Oui</p></td>
</tr>
<tr class="odd">
<td><p><strong>Type de contenu</strong>   Vous pouvez spécifier le type de contenu des messages MIME envoyés aux destinataires du domaine distant. Vous pouvez utiliser les paramètres suivants :</p>
<ul>
<li><p><strong>MimeHtmlText</strong>   Tous les messages sont convertis en messages MIME utilisant une mise en forme HTML, sauf si le message d’origine est un message texte. Si tel est le cas, le message sortant sera un message MIME utilisant une mise en forme de texte. Il s’agit du paramètre par défaut.</p></li>
<li><p><strong>MimeText</strong>   Tous les messages sont convertis en messages MIME utilisant une mise en forme de texte.</p></li>
<li><p><strong>MimeHtml</strong>   Tous les messages sont convertis en messages MIME utilisant une mise en forme HTML.</p></li>
</ul></td>
<td><p>Non</p></td>
<td><p>Oui</p></td>
</tr>
<tr class="even">
<td><p><strong>Taille de retour à la ligne</strong>   Vous pouvez spécifier le nombre maximal de caractères pouvant être inclus sur une seule ligne de texte dans le corps d’un message électronique. Il se peut que des applications de messagerie clientes antérieures n’acceptent que 78 caractères par ligne. Cette option est uniquement disponible avec l’environnement de ligne de commande Exchange Management Shell.</p>
<p></p></td>
<td><p>Non</p></td>
<td><p>Oui</p></td>
</tr>
</tbody>
</table>


Retour au début

## Options de codage de messages pour des contacts et des utilisateurs de messagerie

Lorsque vous configurez les options de codage de messages pour un contact ou un utilisateur de messagerie, cette option est appliquée à tous les messages envoyés à ce destinataire spécifique. Pour les contacts et les utilisateurs de messagerie de votre organisation, les options de configuration de codage des messages suivantes sont disponibles :

  - **UsePreferMessageFormat**   Ce paramètre indique si les paramètres de format de message configurés pour le contact de messagerie remplacent les paramètres globaux configurés pour le domaine distant. Si vous désactivez ce paramètre, Microsoft Exchange ignore les options de codage des autres messages pour ce destinataire et le codage des messages est déterminé par la configuration du domaine distant ou des paramètres configurés par l’expéditeur du message.

  - **MessageFormat**   Ce paramètre spécifie le format du message. Vous pouvez spécifier le format de message Texte ou Mime. La valeur de cette option dépend du paramètre *MessageBodyFormat*. Si le format du corps de message est HTML ou TextAndHtml, vous devez définir ce paramètre sur Mime.

  - **MessageBodyFormat**   Ce paramètre spécifie le format du corps de message. Vous pouvez spécifier Texte, HTML ou TextAndHtml. La valeur de cette option dépend du paramètre *MessageFormat*. Si le format du message est Texte, vous devez également définir ce paramètre sur Texte.

  - **MacAttachmentFormat**   Ce paramètre indique le format des pièces jointes des messages envoyés pour le système d’exploitation Apple Macintosh. Vous pouvez spécifier BinHex, UuEncode, AppleSingle ou AppleDouble. La valeur de cette option dépend du paramètre *MessageFormat*. Si le format du message choisi est Texte, vous devez définir ce paramètre sur BinHex ou UuEncode. Si le format choisi est Mime, vous devez définir ce paramètre sur BinHex, AppleSingle ou AppleDouble.

Pour définir les options de codage de messages pour des contacts et des utilisateurs de messagerie, vous devez utiliser ces paramètres dans l’environnement de ligne de commande Exchange Management Shell. Pour plus d’informations, consultez les rubriques suivantes :

  - [Enable-MailContact](https://technet.microsoft.com/fr-fr/library/aa996001\(v=exchg.150\))

  - [New-MailContact](https://technet.microsoft.com/fr-fr/library/bb124519\(v=exchg.150\))

  - [Set-MailContact](https://technet.microsoft.com/fr-fr/library/aa995950\(v=exchg.150\))

  - [Enable-MailUser](https://technet.microsoft.com/fr-fr/library/aa996549\(v=exchg.150\))

  - [New-MailUser](https://technet.microsoft.com/fr-fr/library/aa996335\(v=exchg.150\))

  - [Set-MailUser](https://technet.microsoft.com/fr-fr/library/aa995971\(v=exchg.150\))

Retour au début

## Options de codage des messages disponibles dans Outlook

En tant qu’expéditeur, vous pouvez spécifier les options de codage des messages dans Outlook à l’une des étapes suivantes :

  - En configurant le format de message par défaut sur texte brut ou HTML.

  - En définissant le format du message composé sur texte brut ou HTML dans la zone **Format** de l’onglet **Options**.

  - En configurant les options de codage des messages pour les messages envoyés à tous les destinataires en dehors de l’organisation Exchange. Ces options sont intitulées *Format des messages Internet*. Les options s’appliquent uniquement aux destinataires distants et non aux destinataires dans l’organisation Exchange.

  - En configurant les options de codage des messages pour les messages envoyés à des destinataires spécifiques en dehors de l’organisation Exchange. Ces options sont intitulées *Format des messages des destinataires Internet*. Les options s’appliquent uniquement aux destinataires distants dans votre dossier Contacts, et non aux destinataires dans l’organisation Exchange.

Par défaut, Outlook utilise un codage automatique de jeu de caractères des messages en analysant l’intégralité du texte du message sortant afin de déterminer le codage à utiliser. Ce paramètre s’applique aux messages envoyés à des destinataires sur Internet et dans l’organisation Exchange. Toutefois, vous pouvez ignorer ce dernier et spécifier un codage de votre choix pour les messages sortants.

Retour au début

## Options d’encodage des messages disponibles dans Outlook Web App

En tant qu’expéditeur, vous pouvez spécifier les options d’encodage des messages dans Outlook Web App de l’une des façons suivantes :

  - En configurant le format de message par défaut sur texte brut ou HTML dans la section **Format de message** de la page **Paramètres** \> **Options** \> **Paramètres**.

  - En définissant le format du message composé sur texte brut ou HTML à l’aide du menu **Plus d’options** (…) et en sélectionnant **Passer en mode texte brut** ou **Passer en mode HTML**.

Retour au début

## Ordre de priorité des options de codage des messages

Exchange utilise l’ordre de priorité décrit dans la liste suivante pour déterminer les options de codage pour les messages sortants envoyés à des destinataires en dehors de l’organisation Exchange :

1.  Paramètres de domaine distant

2.  Paramètres Outlook ou Outlook Web App

3.  paramètres d’utilisateur ou de contact de messagerie

La liste spécifie l’ordre de priorité de la plus basse à la plus élevée. Un paramètre défini dans un niveau supérieur peut en remplacer un défini dans un niveau inférieur.

Le tableau suivant décrit l’ordre de priorité des options de codage des messages, de la priorité la plus faible à la priorité la plus haute.

### Ordre de priorité des options de codage des messages, de la priorité la plus faible à la priorité la plus haute

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
<th>Valeurs</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Paramètre d’entrée de domaine distant, à l’aide du CAE ou de la cmdlet <strong>Set-RemoteDomain</strong></p></td>
<td><p><em>CharacterSet</em></p></td>
<td><p>Spécifié</p></td>
</tr>
<tr class="even">
<td><p>Paramètre d’entrée de domaine distant, à l’aide du CAE ou de la cmdlet <strong>Set-RemoteDomain</strong></p></td>
<td><p><em>NonMimeCharacterSet</em></p></td>
<td><p>Spécifié</p></td>
</tr>
<tr class="odd">
<td><p>Paramètre Outlook</p></td>
<td><p>Codage de jeu de caractères de message</p></td>
<td><ul>
<li><p>Sélectionner automatiquement</p></li>
<li><p>Spécifié</p></li>
</ul></td>
</tr>
</tbody>
</table>


Lorsque vous définissez le jeu de caractères non-MIME pour un domaine distant, ce jeu de caractères est affecté aux types de messages suivants :

  - Messages sortants à destination d’un domaine distant configuré ne contenant pas un jeu de caractères spécifié.

  - Messages entrants provenant d’un domaine distant configuré ne contenant pas un jeu de caractères spécifié.

La valeur de la page de code ANSI Windows pour le serveur de transport permet d’attribuer un jeu de caractères aux types de messages suivants :

  - Messages internes ne contenant pas un jeu de caractères spécifié.

  - Messages internes contenant un jeu de caractères spécifié, mais ne contenant pas une page de code de serveur spécifiée.

Si un message contient un jeu de caractères spécifié mais non valide, le serveur de transport tente de le remplacer par un jeu de caractères valide.

Le tableau suivant décrit l’ordre de priorité des options de codage des messages en texte brut, de la priorité la plus faible à la priorité la plus haute.

### Ordre de priorité des options de codage des messages en texte brut, de la priorité la plus faible à la priorité la plus haute

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
<th>Valeurs</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Set-RemoteDomain</strong></p></td>
<td><p><em>LineWrapSize</em></p></td>
<td><ul>
<li><p>Entre 0 et 132</p></li>
<li><p>illimité</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Paramètres Outlook</p></td>
<td><p>format des messages</p></td>
<td><p>Texte brut</p></td>
</tr>
<tr class="odd">
<td><p>Paramètres Outlook</p></td>
<td><p>format de message Internet</p></td>
<td><p>Options de texte brut :</p>
<ul>
<li><p>Coder les pièces jointes au format UuEncode lors de l’envoi d’un message en texte brut</p></li>
<li><p>Retour à la ligne automatique après <em>nn</em> caractères</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Paramètres Outlook</p></td>
<td><p>format de message de destinataire Internet</p></td>
<td><p>Format de texte brut :</p>
<ul>
<li><p>Coder les pièces jointes au format UuEncode</p></li>
<li><p>Utiliser le format de pièce jointe BinHex Mac</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p><strong>Set-MailUser</strong></p>
<p><strong>Set-MailContact</strong></p></td>
<td><p><em>UsePreferMessageFormat</em></p></td>
<td><ul>
<li><p><code>$true</code></p></li>
<li><p><code>$false</code></p></li>
</ul>
<p>Si la valeur est <code>$false</code> ou si le destinataire n’est pas spécifié comme utilisateur ou contact de messagerie dans l’organisation, les paramètres d’utilisateur ou de contact de messagerie sont ignorés.</p></td>
</tr>
<tr class="even">
<td><p><strong>Set-MailUser</strong></p>
<p><strong>Set-MailContact</strong></p></td>
<td><p><em>MessageFormat</em></p></td>
<td><p>Texte</p></td>
</tr>
<tr class="odd">
<td><p><strong>Set-MailUser</strong></p>
<p><strong>Set-MailContact</strong></p></td>
<td><p><em>MessageBodyFormat</em></p></td>
<td><p>Texte</p></td>
</tr>
<tr class="even">
<td><p><strong>Set-MailUser</strong></p>
<p><strong>Set-MailContact</strong></p></td>
<td><p><em>MacAttachmentFormat</em></p></td>
<td><ul>
<li><p>BinHex</p></li>
<li><p>UUEncode</p></li>
</ul></td>
</tr>
</tbody>
</table>


Le tableau suivant décrit l’ordre de priorité des options de codage des messages MIME, de la priorité la plus faible à la priorité la plus haute.

### Ordre de priorité des options de codage des messages MIME, de la priorité la plus faible à la priorité la plus haute

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
<th>Valeurs</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Set-RemoteDomain</strong></p></td>
<td><p><em>ContentType</em></p></td>
<td><ul>
<li><p><code>MimeHtmlText</code></p></li>
<li><p><code>MimeText</code></p></li>
<li><p><code>MimeHtml</code></p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Paramètres Outlook ou Outlook Web App</p></td>
<td><p>format des messages</p></td>
<td><ul>
<li><p>Texte simple</p></li>
<li><p>HTML</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Paramètres Outlook</p></td>
<td><p>format de message de destinataire Internet</p></td>
<td><p>Format de message MIME</p>
<ul>
<li><p>Texte simple</p></li>
<li><p>Inclure du texte brut et HTML</p></li>
<li><p>HTML</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>Set-MailUser</strong></p>
<p><strong>Set-MailContact</strong></p></td>
<td><p><em>UsePreferMessageFormat</em></p></td>
<td><p><code>$true</code></p>
<p><code>$false</code></p>
<p>Si la valeur est <code>$false</code> ou si le destinataire n’est pas spécifié comme utilisateur ou contact de messagerie dans l’organisation, les paramètres d’utilisateur ou de contact de messagerie sont ignorés.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Set-MailUser</strong></p>
<p><strong>Set-MailContact</strong></p></td>
<td><p><em>MessageFormat</em></p></td>
<td><ul>
<li><p>Texte</p></li>
<li><p>Mime</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>Set-MailUser</strong></p>
<p><strong>Set-MailContact</strong></p></td>
<td><p><em>MessageBodyFormat</em></p></td>
<td><ul>
<li><p><code>Text</code></p></li>
<li><p><code>Html</code></p></li>
<li><p><code>TextAndHtml</code></p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p><strong>Set-MailUser</strong></p>
<p><strong>Set-MailContact</strong></p></td>
<td><p><em>MacAttachmentFormat</em></p></td>
<td><ul>
<li><p>BinHex</p></li>
<li><p>AppleSingle</p></li>
<li><p>AppleDouble</p></li>
</ul></td>
</tr>
</tbody>
</table>


Retour au début

## Pour plus d'informations

[Options d’encodage des messages](message-encoding-options-exchange-2013-help.md)

[Options de conversion TNEF](tnef-conversion-options-exchange-2013-help.md)

[Domaines distants](remote-domains-exchange-2013-help.md)

[Domaines distants dans Exchange Online](https://technet.microsoft.com/fr-fr/library/jj966211\(v=exchg.150\))

[Gérer les utilisateurs de messagerie](https://docs.microsoft.com/fr-fr/exchange/recipients-in-exchange-online/manage-mail-users)

[Gérer les contacts de messagerie](https://docs.microsoft.com/fr-fr/exchange/recipients-in-exchange-online/manage-mail-contacts)

[Modifier le format des messages dans Outlook](https://go.microsoft.com/fwlink/p/?linkid=397890)

