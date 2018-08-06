---
title: 'Clauses d’excl. de resp., signatures, pieds de p. ou en-têtes pr l’organisation| Microsoft Docs'
TOCTitle: Clauses d’exclusion de responsabilité, signatures, pieds de page ou en-têtes à l’échelle de l’organisation
ms:assetid: e45e33c9-e53b-427c-ada5-70901bc399b8
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dn600437(v=EXCHG.150)
ms:contentKeyID: 61060488
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Clauses d’exclusion de responsabilité, signatures, pieds de page ou en-têtes à l’échelle de l’organisation

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2015-03-09_

Vous pouvez ajouter une clause d’exclusion de responsabilité de messagerie électronique, une clause d’exclusion de responsabilité juridique, un énoncé de divulgation, une signature ou toute autre information en haut ou au bas des messages électroniques qui entrent dans votre organisation ou qui en sortent. Ceci peut être nécessaire pour des raisons juridiques, légales ou réglementaires, pour identifier les messages électroniques potentiellement dangereux ou pour d’autres raisons propres à votre organisation.

Pour configurer une clause d’exclusion de responsabilité, créez une règle de transport qui comprend les conditions (par exemple, lorsque l’expéditeur appartient à un groupe particulier ou lorsque le message contient des modèles de texte spécifiques), ainsi que le texte à ajouter. Pour appliquer plusieurs clauses d’exclusion de responsabilité à un même message électronique, utilisez plusieurs règles de transport.

> [!important]
> <ul>
> <li><p>Si vous voulez que les informations soient ajoutées uniquement aux messages sortants, vous devez ajouter une condition (par exemple, que les destinataires soient situés en dehors de l’organisation). Par défaut, les règles de transport sont appliquées aux messages entrants et sortants.</p></li>
> </ul>


**Contenu**

Exemples

Étendue de votre clause d’exclusion de responsabilité

Mise en forme de votre clause d’exclusion de responsabilité

Options de secours si l’ajout d’une clause d’exclusion de responsabilité est impossible

Pour plus d’informations

Vous recherchez des procédures ? Voir [Clauses d’exclusion de responsabilité, signatures, pieds de page ou en-têtes de message à l’échelle de l’organisation dans Office 365](https://technet.microsoft.com/fr-fr/library/dn600323\(v=exchg.150\)).

## Exemples

Voici quelques idées d’utilisation de clauses d’exclusion de responsabilité.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Type</th>
<th>Exemple de texte ajouté</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Juridique : messages sortants</p></td>
<td><p>Ce courrier électronique et tous les fichiers associés sont confidentiels. Seule la personne ou l’entité à laquelle ils sont adressés peut les utiliser. Si vous avez reçu ce message par erreur, veuillez en avertir le gestionnaire du système.</p></td>
</tr>
<tr class="even">
<td><p>Juridique : messages entrants</p></td>
<td><p>Les employés sont expressément priés de ne pas faire de déclarations diffamatoires, de ne pas porter atteinte au copyright et de ne pas autoriser toute violation de copyright ou de tout autre droit via leurs communications par messagerie électronique. Les employés qui reçoivent ce type de courrier électronique doivent en informer immédiatement leur superviseur.</p></td>
</tr>
<tr class="odd">
<td><p>Note indiquant que le message a été envoyé à un alias</p></td>
<td><p>Ce message a été envoyé au groupe de discussion des ventes.</p></td>
</tr>
<tr class="even">
<td><p>Signature : extrait des données pour chaque employé</p></td>
<td><p>Kathleen Mayer<br />
Service des ventes<br />
Contoso<br />
www.contoso.com<br />
kathleen@contoso.com<br />
Mobile : 111-222-1234</p></td>
</tr>
<tr class="odd">
<td><p>Annonce publicitaire</p></td>
<td><p>Cliquez ici pour consulter les offres spéciales de mars.</p></td>
</tr>
</tbody>
</table>


Les exemples de cet article ne sont pas destinés à être utilisés en l’état. Modifiez-les en fonction de vos besoins.

## Étendue de votre clause d’exclusion de responsabilité

Lorsque vous travaillez sur vos clauses d’exclusion de responsabilité, réfléchissez aux messages auxquelles elles doivent s’appliquer. Par exemple, vous aurez peut-être besoin de clauses d’exclusion de responsabilité différentes pour les messages internes et externes ou pour les messages envoyés par des utilisateurs appartenant à des services spécifiques. Pour vous assurer que seul le premier message d’une conversation contient une clause d’exclusion de responsabilité, ajoutez une exception qui recherche un texte unique dans votre clause d’exclusion de responsabilité.

Voici quelques exemples de conditions et d’exceptions que vous pouvez utiliser.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Description</th>
<th>Conditions et exceptions dans le CAE</th>
<th>Conditions et exceptions dans l’interpréteur de commandes</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>En dehors de votre organisation, si le message d’origine ne comprend pas le texte de votre clause d’exclusion de responsabilité, comme « CONTOSO LEGAL NOTICE »</p></td>
<td><p>Condition : <strong>Le destinataire est situé</strong> &gt;<strong>À l’extérieur de l’organisation</strong></p>
<p>Exception : <strong>L’objet ou le corps</strong> &gt;<strong>L’objet ou le corps correspond à ces modèles de texte</strong> &gt;<strong>CONTOSO LEGAL NOTICE</strong></p></td>
<td><pre><code>-FromScope NotInOrganization -ExceptIf -SubjectOrBodyMatches &quot;CONTOSO LEGAL NOTICE&quot;</code></pre></td>
</tr>
<tr class="even">
<td><p>Messages entrants comportant des fichiers exécutables en pièce jointe</p></td>
<td><p>Condition 1 : <strong>L’expéditeur est situé</strong> &gt;<strong>À l’extérieur de l’organisation</strong></p>
<p>Condition 2 : <strong>Toute pièce jointe</strong> &gt;<strong>contient un exécutable</strong></p></td>
<td><pre><code>-FromScope NotInOrganization -AttachmentHasExecutableContent</code></pre></td>
</tr>
<tr class="odd">
<td><p>L’expéditeur fait partie du service marketing.</p></td>
<td><p>Condition : <strong>L’expéditeur</strong> &gt;<strong>est membre de ce groupe</strong> &gt;<strong>group name</strong></p></td>
<td><pre><code>-FromMemberOf &quot;Marketing Team&quot;</code></pre></td>
</tr>
<tr class="even">
<td><p>Chaque message envoyé par un expéditeur externe au groupe de discussion des ventes</p></td>
<td><p>Condition 1 : <strong>L’expéditeur est situé</strong> &gt;<strong>À l’extérieur de l’organisation</strong></p>
<p>Condition 2 : <strong>Le message</strong> &gt;<strong>La zone À ou Cc contient cette personne</strong> &gt;<strong>group name</strong></p></td>
<td><pre><code>-FromScope NotInOrganization -SentTo &quot;Sales Discussion Group&quot; -PrependSubject &quot;Sent to Sales Discussion Group: &quot;</code></pre></td>
</tr>
<tr class="odd">
<td><p>Ajouter une annonce publicitaire aux messages sortants pendant un mois</p></td>
<td><p>Condition 1 : <strong>Le destinataire est situé</strong> &gt;<strong>À l’extérieur de l’organisation</strong></p>
<p>Spécifiez les dates dans la partie inférieure de la boîte de dialogue <strong>Nouvelle règle</strong>.</p></td>
<td><p>-ApplyHtmlDisclaimerLocation ’Prepend’ -SentToScope ’NotInOrganization’ –ActivationDate ‘03/1/2014’ –ExpiryDate ‘03/31/2014’</p></td>
</tr>
</tbody>
</table>


Pour obtenir la liste complète des conditions de règle de transport permettant de cibler la clause d’exclusion de responsabilité, voir l’une des rubriques suivantes :

  - [Exceptions (prédicat) et conditions de règles de flux de messagerie dans Exchange Online](https://technet.microsoft.com/fr-fr/library/jj919235\(v=exchg.150\)) (Exchange Online)

  - [Conditions de règles de transport (prédicats)](mail-flow-rule-conditions-and-exceptions-predicates-in-exchange-2013-exchange-2013-help.md) (Exchange 2013)

  - [Exceptions (prédicat) et conditions de règles de flux de messagerie dans Exchange Online](https://technet.microsoft.com/fr-fr/library/jj919235\(v=exchg.150\)) (Exchange Online Protection)

## Mise en forme de votre clause d’exclusion de responsabilité

Vous pouvez mettre en forme votre clause d’exclusion de responsabilité en fonction de vos besoins. Voici les détails que vous pouvez y inclure.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Type d’information</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Texte</p></td>
<td><p>La longueur maximale est de 5 000 caractères, y compris toutes les balises HTML et les feuilles de style CSS incluses.</p></td>
</tr>
<tr class="even">
<td><p>Balises HTML et feuilles de style CSS incluses</p></td>
<td><p>Vous pouvez utiliser les styles HTML et CSS pour mettre en forme le texte. Par exemple, utilisez la balise <code>&lt;HR&gt;</code> pour ajouter une ligne avant la clause d’exclusion de responsabilité.</p>
<p>Le style HTML est ignoré dans une clause d’exclusion de responsabilité si celle-ci est ajoutée à un message en texte brut.</p></td>
</tr>
<tr class="odd">
<td><p>Ajouter des images</p></td>
<td><p>Utilisez la balise <code>&lt;IMG&gt;</code> pour pointer vers une image disponible sur Internet. Par exemple, <code>&lt;IMG src=&quot;http://contoso.com/images/companylogo.gif&quot; alt=&quot;Contoso logo&quot;&gt;</code>.</p>
<p>N’oubliez pas que, par défaut, Outlook Web App et Outlook bloquent le contenu web externe, y compris les images. Il est possible que les utilisateurs doivent alors effectuer une action spécifique pour voir le contenu externe bloqué. Cela signifie que les images ajoutées à l’aide de la balise <code>IMG</code> ne seront peut-être pas visibles par défaut. Nous vous recommandons de tester une clause d’exclusion de responsabilité avec des balises <code>IMG</code> sur les clients de messagerie que les destinataires risquent d’utiliser pour vous assurer que l’affichage est correct.</p></td>
</tr>
<tr class="even">
<td><p>Ajouter des informations pour les signatures personnalisées</p></td>
<td><p>Si vous voulez harmoniser le format des signatures et faire en sorte qu’elles contiennent les mêmes informations, vous pouvez ajouter des renseignements uniques pour chaque employé, comme <code>DisplayName</code>, <code>FirstName</code>, <code>LastName</code>, <code>PhoneNumber</code>, <code>Email</code>, <code>FaxNumber</code> et <code>Department</code>. Ces informations doivent être entourées de deux symboles de pourcentage (%%). Par exemple, pour utiliser <code>DisplayName</code>, vous devez écrire <strong>%%DisplayName%%</strong> dans votre clause d’exclusion de responsabilité.</p>
<p>Lors du déclenchement d’une règle de clause d’exclusion de responsabilité, les valeurs correspondantes pour cet utilisateur sont insérées. Les données proviennent du compte d’utilisateur Active Directory de l’expéditeur (pour le serveur Exchange local) ou du compte Office 365 de l’expéditeur pour Exchange Online.</p>
<p>Pour obtenir la liste complète des attributs disponibles dans les clauses d’exclusion de responsabilité et les signatures personnalisées, voir la description de la propriété <code>ADAttribute</code> dans <a href="mail-flow-rule-conditions-and-exceptions-predicates-in-exchange-2013-exchange-2013-help.md">Conditions de règles de transport (prédicats)</a> (Exchange Server), <a href="https://technet.microsoft.com/fr-fr/library/jj919235(v=exchg.150)">Exceptions (prédicat) et conditions de règles de flux de messagerie dans Exchange Online</a> (Exchange Online) ou <a href="https://technet.microsoft.com/fr-fr/library/jj919234(v=exchg.150)">Mail flux conditions et les exceptions (prédicat) dans Exchange Online Protection</a> (Exchange Online Protection).</p></td>
</tr>
</tbody>
</table>


Par exemple, voici un exemple de clause d’exclusion de responsabilité HTML qui comprend une signature, une balise `IMG` et une feuille de style CSS imbriquée.

    <div style="font-size:9pt;  font-family: 'Calibri',sans-serif;">
    %%displayname%%</br>
    %%title%%</br>
    %%company%%</br>
    %%street%%</br>
    %%city%%, %%state%% %%zipcode%%</div>
    &nbsp;</br>
    <div style="background-color:#D5EAFF; border:1px dotted #003333; padding:.8em; ">
    <div><img alt="Fabrikam"  src="http://fabrikam.com/images/fabrikamlogo.png"></div>
    <span style="font-size:12pt;  font-family: 'Cambria','times new roman','garamond',serif; color:#ff0000;">HTML Disclaimer Title</span></br>
    <p style="font-size:8pt; line-height:10pt; font-family: 'Cambria','times roman',serif;">This message contains confidential information and is intended only for the individual(s) addressed in the message. If you are not the named addressee, you should not disseminate, distribute, or copy this e-mail. If you are not the intended recipient, you are notified that disclosing, distributing, or copying this e-mail is strictly prohibited.  </p>
    <span style="padding-top:10px; font-weight:bold; color:#CC0000; font-size:10pt; font-family: 'Calibri',Arial,sans-serif; "><a href="http://www.fabrikam.com">Fabrikam, Inc. </a></span></br></br>
    </div>

## Options de secours si l’ajout d’une clause d’exclusion de responsabilité est impossible

Certains messages, tels que les messages chiffrés, empêchent Exchange de modifier le contenu du message d’origine. Vous pouvez contrôler la façon dont votre organisation gère ces messages. Vous pouvez choisir de placer un message non modifiable dans une enveloppe de message contenant la clause d’exclusion de responsabilité, de rejeter le message s’il est impossible d’y ajouter une clause d’exclusion de responsabilité ou de remettre le message sans clause d’exclusion de responsabilité.

La liste suivante décrit chaque action de secours :

  - **Wrap** : si la cause d’exclusion de responsabilité ne peut pas être insérée dans le message d’origine, Exchange place celle-ci dans une nouvelle enveloppe de message. La clause d’exclusion de responsabilité est ensuite insérée dans le nouveau message. S’il n’est pas possible de placer le message original dans une nouvelle enveloppe, celui-ci n’est pas remis. L’expéditeur reçoit un rapport de non-remise (NDR) expliquant pourquoi le message n’a pas été remis.
    
    > [!NOTE]
    > Si un message original est placé dans une nouvelle enveloppe de message, les règles de transport suivantes sont appliquées à la nouvelle enveloppe de message, et pas au message original. C’est pourquoi vous devez configurer les règles de transport avec des actions de clause d’exclusion de responsabilité qui placent les messages originaux dans un nouveau corps de message après avoir configuré les autres règles de transport.


  - **Reject** : s’il n’est pas possible d’insérer la clause d’exclusion de responsabilité dans le message d’origine, Exchange ne remet pas le message. L’expéditeur reçoit une notification de non-remise expliquant pourquoi le message n’a pas été remis.

  - **Ignore** : s’il n’est pas possible d’insérer la clause d’exclusion de responsabilité dans le message d’origine, Exchange remet celui-ci sans le modifier. Aucune clause d’exclusion de responsabilité n’est ajoutée.

## Pour plus d’informations

[Clauses d’exclusion de responsabilité, signatures, pieds de page ou en-têtes de message à l’échelle de l’organisation dans Office 365](https://technet.microsoft.com/fr-fr/library/dn600323\(v=exchg.150\))

[Règles de transport ou de flux de messagerie](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md) (Exchange Server 2013)

[Règles de flux de messagerie (règles de transport) dans Exchange Online](https://technet.microsoft.com/fr-fr/library/jj919238\(v=exchg.150\)) (Exchange Online)

[Règles de flux de messagerie (règles de transport) dans Exchange Online Protection](https://technet.microsoft.com/fr-fr/library/dn271424\(v=exchg.150\)) (Exchange Online Protection)

