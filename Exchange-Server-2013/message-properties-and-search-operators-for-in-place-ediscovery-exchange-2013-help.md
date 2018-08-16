---
title: 'Propriétés de msg et opérateurs de rech. pour la découv. électr. inaltérable'
TOCTitle: Propriétés de message et opérateurs de recherche pour la découverte électronique inaltérable
ms:assetid: 402b74e4-8853-4c51-9737-1a9c19f8e3dd
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dn774955(v=EXCHG.150)
ms:contentKeyID: 62617681
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Propriétés de message et opérateurs de recherche pour la découverte électronique inaltérable

 

_**Sapplique à :** Exchange Online, Exchange Server 2013_

_**Dernière rubrique modifiée :** 2016-12-09_

Cette rubrique décrit les propriétés des messages électroniques Exchange que vous pouvez effectuer une recherche à l’aide de la découverte électronique locale et de l’archive permanente dans Exchange Server 2013 et Exchange Online. Elle décrit également les opérateurs de recherche booléens et d’autres techniques de requête de recherche qui permettent d’affiner les résultats de recherche de la découverte électronique.

La découverte électronique inaltérable utilise le langage KQL (Keyword Query Language). Pour plus d’informations, voir [Référence sur la syntaxe Keyword Query Language](https://go.microsoft.com/fwlink/?linkid=269603).

## Propriétés pouvant faire l’objet d’une recherche dans Exchange

Le tableau suivant répertorie les propriétés de message électronique consultables à l’aide d’une recherche de découverte électronique inaltérable ou à l’aide de la cmdlet **New-MailboxSearch** ou **Set-MailboxSearch**. Il inclut un exemple de syntaxe *property:value* pour chaque propriété et une description des résultats de recherche renvoyés par ces exemples.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Propriété</th>
<th>Description de la propriété</th>
<th>Exemples</th>
<th>Résultats de recherche renvoyés par les exemples</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Attachment</p></td>
<td><p>Nom des fichiers joints à un message électronique.</p></td>
<td><p>attachment:annualreport.ppt</p>
<p>attachment:annual*</p></td>
<td><p>Messages comportant un fichier joint nommé annualreport.ppt.</p>
<p>Dans le deuxième exemple, l’utilisation du caractère générique permet de renvoyer les messages dont le nom d’une pièce jointe contient le mot « annual ».</p></td>
</tr>
<tr class="even">
<td><p>Bcc</p></td>
<td><p>Champ Cci d’un message électronique.1</p></td>
<td><p>bcc:pilarp@contoso.com</p>
<p>bcc:pilarp</p>
<p>bcc:&quot;Pilar Pinilla&quot;</p></td>
<td><p>Tous les exemples renvoient des messages dont « Pilar Pinilla » est en copie carbone invisible.</p></td>
</tr>
<tr class="odd">
<td><p>Category</p></td>
<td><p>Catégories à rechercher. Les utilisateurs peuvent définir les catégories à l’aide d’Outlook ou d’Outlook Web App. Les valeurs possibles sont les suivantes :</p>
<ul>
<li><p>blue</p></li>
<li><p>green</p></li>
<li><p>orange</p></li>
<li><p>purple</p></li>
<li><p>red</p></li>
<li><p>yellow</p></li>
</ul></td>
<td><p>category:=&quot;Red Category&quot;</p></td>
<td><p>Messages auxquels a été attribuée la catégorie « red » dans les boîtes aux lettres source.</p></td>
</tr>
<tr class="even">
<td><p>Cc</p></td>
<td><p>Champ Cc d’un message électronique.1</p></td>
<td><p>cc:pilarp@contoso.com</p>
<p>cc:&quot;Pilar Pinilla&quot;</p></td>
<td><p>Dans les deux exemples, les résultats renvoient les messages contenant « Pilar Pinilla » dans le champ Cc.</p></td>
</tr>
<tr class="odd">
<td><p>From</p></td>
<td><p>Expéditeur d’un message électronique.1</p></td>
<td><p>from:pilarp@contoso.com</p>
<p>from:contoso.com</p></td>
<td><p>Messages envoyés par l’utilisateur indiqué ou à partir d’un domaine spécifié.</p></td>
</tr>
<tr class="even">
<td><p>Importance</p></td>
<td><p>Importance d’un message électronique, que l’expéditeur peut préciser lors de l’envoi. Par défaut, les messages sont envoyés avec une importance normale, à moins que l’expéditeur préfère une importance <strong>haute</strong> ou <strong>faible</strong>.</p></td>
<td><p>importance:high</p>
<p>importance:medium</p>
<p>importance:low</p></td>
<td><p>Messages marqués comme ayant une importance haute, normale ou faible.</p></td>
</tr>
<tr class="odd">
<td><p>Kind</p></td>
<td><p>Type de message à rechercher. Valeurs possibles :</p>
<ul>
<li><p>contacts</p></li>
<li><p>docs</p></li>
<li><p>email</p></li>
<li><p>faxes</p></li>
<li><p>im</p></li>
<li><p>journals</p></li>
<li><p>meetings</p></li>
<li><p>notes</p></li>
<li><p>posts</p></li>
<li><p>rssfeeds</p></li>
<li><p>tasks</p></li>
<li><p>voicemail</p></li>
</ul></td>
<td><p>kind:email</p>
<p>kind:email OR kind:im OR kind:voicemail</p></td>
<td><p>Messages électroniques correspondant aux critères de recherche. Le deuxième exemple renvoie des messages électroniques, des conversations de messagerie instantanée et des messages vocaux correspondant aux critères de recherche.</p></td>
</tr>
<tr class="even">
<td><p>Participants</p></td>
<td><p>Tous les champs de contacts compris dans un message électronique ; De, À, Cc et Cci.1</p></td>
<td><p>participants:garthf@contoso.com</p>
<p>participants:contoso.com</p></td>
<td><p>Messages envoyés par ou à garthf@contoso.com.</p>
<p>Le deuxième exemple renvoie tous les messages envoyés à ou par un utilisateur du domaine contoso.com.</p></td>
</tr>
<tr class="odd">
<td><p>Received</p></td>
<td><p>Date à laquelle un message électronique a été reçu par un destinataire.</p></td>
<td><p>received:04/15/2014</p>
<p>received&gt;=01/01/2014 AND received&lt;=03/31/2014</p></td>
<td><p>Messages reçus le 15 avril 2014. Le deuxième exemple renvoie tous les messages reçus entre le 1er janvier 2014 et le 31 mars 2014.</p></td>
</tr>
<tr class="even">
<td><p>Recipients</p></td>
<td><p>Tous les champs de destinataires compris dans un message électronique ; À, Cc et Cci.1</p></td>
<td><p>recipients:garthf@contoso.com</p>
<p>recipients:contoso.com</p></td>
<td><p>Messages envoyés à garthf@contoso.com.</p>
<p>Le deuxième exemple renvoie les messages envoyés à tous les destinataires du domaine contoso.com.</p></td>
</tr>
<tr class="odd">
<td><p>Sent</p></td>
<td><p>Date à laquelle un message électronique a été envoyé par l’expéditeur.</p></td>
<td><p>sent:07/01/2014</p>
<p>sent&gt;=06/01/2014 AND sent&lt;=07/01/2014</p></td>
<td><p>Messages envoyés à la date indiquée ou entre les dates spécifiées.</p></td>
</tr>
<tr class="even">
<td><p>Size</p></td>
<td><p>Taille d’un élément, en octets.</p></td>
<td><p>taille &gt; 26214400</p>
<p>size:1..1048576</p></td>
<td><p>Messages de plus de 25 Mo.</p>
<p>Le deuxième exemple renvoie les messages dont la taille est comprise entre 1 et 1 048 576 octets (1 Mo).</p></td>
</tr>
<tr class="odd">
<td><p>Subject</p></td>
<td><p>Texte de la ligne d’objet d’un message électronique.</p></td>
<td><p>subject:&quot;Quarterly Financials&quot;</p>
<p>subject:northwind</p></td>
<td><p>Messages contenant l’expression exacte « Quarterly Financials » à n’importe quel endroit de la ligne d’objet.</p>
<p>Le deuxième exemple renvoie tous les messages contenant le mot « northwind » dans la ligne d’objet.</p></td>
</tr>
<tr class="even">
<td><p>To</p></td>
<td><p>Champ À d’un message électronique.1</p></td>
<td><p>to:annb@contoso.com</p>
<p>to:annb</p>
<p>to:&quot;Ann Beebe&quot;</p></td>
<td><p>Tous les exemples renvoient les messages dans lesquels « Ann Beebe » est indiqué sur la ligne À.</p></td>
</tr>
</tbody>
</table>


> [!NOTE]
> 1   Pour la valeur d’une propriété de destinataire, vous pouvez utiliser l’adresse SMTP, le nom d’affichage ou l’alias afin d’indiquer un utilisateur. Par exemple, vous pouvez utiliser annb@contoso.com, annb ou « Ann Beebe » pour spécifier l’utilisateur Ann Beebe.


## Opérateurs de recherche pris en charge

Les opérateurs booléens, tels que **AND** et **OR**, vous permettent de définir des recherches plus précises dans des boîtes aux lettres en incluant des mots spécifiques dans la requête de recherche ou en les excluant. D’autres techniques, comme l’utilisation d’opérateurs de propriété (tels que \>= ou ...), les guillemets, les parenthèses et les caractères génériques vous permettent d’affiner les requêtes de recherche de découverte électronique. Le tableau suivant répertorie les opérateurs disponibles pour restreindre ou élargir les résultats de recherche.

> [!NOTE]
> Vous devez utiliser des opérateurs booléens en majuscules dans vos requêtes de recherche. Par exemple, utilisez <strong>AND</strong>, et non <strong>and</strong>. L’utilisation d’opérateurs en lettres minuscules dans les requêtes de recherche renverra une erreur.



<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Opérateur</th>
<th>Utilisation</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>AND</p></td>
<td><p>keyword1 AND keyword2</p></td>
<td><p>Renvoie les messages qui incluent tous les mots-clés spécifiés ou toutes les expressions <code>property:value</code> indiquées.</p></td>
</tr>
<tr class="even">
<td><p>+</p></td>
<td><p>keyword1 +keyword2 +keyword3</p></td>
<td><p>Renvoie les éléments qui contiennent <em>soit</em><code>keyword2 </code>soit <code>keyword3</code><em>, et</em> qui contiennent également <code>keyword1</code>. Par conséquent, cet exemple équivaut à la requête <code>(keyword2 OR keyword3) AND keyword1</code>.</p>
<p>Notez que la requête <code>keyword1 + keyword2</code> (avec un espace après le symbole <strong>+</strong>) revient au même que d’utiliser l’opérateur <strong>AND</strong>. Cette requête est équivalente à <code>&quot;keyword1 + keyword2&quot;</code> et renvoie des éléments contenant l’expression exacte <code>&quot;keyword1 + keyword2&quot;</code>.</p></td>
</tr>
<tr class="odd">
<td><p>OR</p></td>
<td><p>keyword1 OR keyword2</p></td>
<td><p>Renvoie les messages qui incluent au moins un des mots-clés spécifiés ou une des expressions <code>property:value</code> indiquées.</p></td>
</tr>
<tr class="even">
<td><p>NOT</p></td>
<td><p>keyword1 NOT keyword2</p>
<p>NOT from:&quot;Ann Beebe&quot;</p></td>
<td><p>Exclut les messages qui incluent un mot-clé spécifié ou une expression <code>property:value</code> indiquée. Par exemple, <code>NOT from:&quot;Ann Beebe&quot;</code> exclut les messages envoyés par Ann Beebe.</p></td>
</tr>
<tr class="odd">
<td><p>-</p></td>
<td><p>keyword1 -keyword2</p></td>
<td><p>Identique à l’opérateur <strong>NOT</strong>. Cette requête renvoie les éléments qui contiennent <code>keyword1</code> et exclut les éléments qui contiennent <code>keyword2</code>.</p></td>
</tr>
<tr class="even">
<td><p>NEAR</p></td>
<td><p>keyword1 NEAR(n) keyword2</p></td>
<td><p>Renvoie les messages qui incluent des mots proches les uns des autres, n étant égal au nombre de mots. Par exemple, <code>best NEAR(5) worst</code> renvoie les messages où le mot « worst » est situé à 5 mots maximum du mot « best ». Si aucun nombre n’est spécifié, la distance par défaut est de huit mots.</p></td>
</tr>
<tr class="odd">
<td><p>:</p></td>
<td><p>property:value</p></td>
<td><p>Le signe deux-points (:) dans la syntaxe <code>property:value</code> signale que la valeur de propriété recherchée est égale à la valeur spécifiée. Par exemple, <code>recipients:garthf@contoso.com</code> renvoie les messages envoyés à garthf@contoso.com.</p></td>
</tr>
<tr class="even">
<td><p>&lt;</p></td>
<td><p>property&lt;value</p></td>
<td><p>Indique que la propriété recherchée est inférieure à la valeur spécifiée.1</p></td>
</tr>
<tr class="odd">
<td><p>&gt;</p></td>
<td><p>property&gt;value</p></td>
<td><p>Indique que la propriété recherchée est supérieure à la valeur spécifiée.1</p></td>
</tr>
<tr class="even">
<td><p>&lt;=</p></td>
<td><p>property&lt;=value</p></td>
<td><p>Indique que la propriété recherchée est inférieure ou égale à la valeur spécifiée.1</p></td>
</tr>
<tr class="odd">
<td><p>&gt;=</p></td>
<td><p>property&gt;=value</p></td>
<td><p>Indique que la propriété recherchée est supérieure ou égale à la valeur spécifiée.1</p></td>
</tr>
<tr class="even">
<td><p>..</p></td>
<td><p>property:value1..value2</p></td>
<td><p>Indique que la propriété recherchée est supérieure ou égale à value1 et inférieure ou égale à value2.1</p></td>
</tr>
<tr class="odd">
<td><p>&quot; &quot;</p></td>
<td><p>&quot;fair value&quot;</p>
<p>subject:&quot;Quarterly Financials&quot;</p></td>
<td><p>Utilisez des guillemets doubles (&quot; &quot;) pour rechercher une expression ou un terme exact dans un mot-clé et des requêtes de recherche <code>property:value</code>.</p></td>
</tr>
<tr class="even">
<td><p>*</p></td>
<td><p>cat*</p>
<p>subject:set*</p></td>
<td><p>Les recherches par caractères génériques préfixées (où l’astérisque est placée à la fin d’un mot) correspondent à zéro ou plusieurs caractères dans les mots-clés ou les requêtes <code>property:value</code>. Par exemple, <code>subject:set*</code> renvoie les messages contenant les mots « set », « setup » et « setting » (et d’autres mots commençant par « set ») présents dans la ligne d’objet.</p></td>
</tr>
<tr class="odd">
<td><p>( )</p></td>
<td><p>(fair OR free) AND from:contoso.com</p>
<p>(IPO OR initial) AND (stock OR shares)</p>
<p>(quarterly financials)</p></td>
<td><p>Les parenthèses regroupent des expressions booléennes, des éléments <code>property:value</code> et des mots-clés. Par exemple, <code>(quarterly financials)</code> renvoie les éléments contenant les mots « quarterly » et « financials ».</p></td>
</tr>
</tbody>
</table>


> [!NOTE]
> 1   Utilisez cet opérateur pour les propriétés ayant des valeurs de date ou des valeurs numériques.


## Caractères non pris en charge dans les requêtes de recherche

En règle générale, les caractères non pris en charge dans une requête de recherche entraînent une erreur ou renvoient des résultats inattendus. Les caractères non pris en charge sont souvent masqués et sont généralement ajoutés à la requête lorsque vous la copiez (ou que vous en copiez des parties) à partir d’autres applications (par exemple, Microsoft Word ou Microsoft Excel), puis que vous les collez dans la zone de mot clé de la page de requête, dans la recherche de découverte électronique inaltérable.

Voici la liste des caractères non pris en charge pour une requête de recherche de découverte électronique inaltérable.

  - **Guillemets anglais**   Les guillemets anglais simples et doubles (également appelée *guillemets courbes*) ne sont pas pris en charge. Seuls les guillemets droits peuvent être utilisés dans une requête de recherche.

  - **Caractères non imprimables et de contrôle**   Les caractères non imprimables et de contrôle ne représentent pas des symboles écrits, comme des caractères alphanumériques. Il peut s’agir de caractères servant à mettre en forme le texte ou à séparer des lignes.

  - **Marques gauche-à-droite et droite-à-gauche**   Il s’agit de caractères de contrôle permettant d’indiquer l’orientation du texte pour les langues se lisant de gauche à droite (telles que l’anglais et le français) et celles se lisant de droite à gauche (comme l’arabe et l’hébreu).

  - **Opérateurs booléens en minuscules**   Comme expliqué précédemment, vous devez utiliser des opérateurs booléens en majuscules, par exemple **AND** et **OR**, dans une requête de recherche. Notez que la syntaxe de la requête indique souvent qu’un opérateur booléen est utilisé, même s’il est en minuscules ; par exemple, `(WordA or WordB) and (WordC or WordD)`.

**Comment empêcher les caractères non pris en charge dans vos requêtes de recherche ?**Le meilleur moyen d’éviter les caractères non pris en charge est de saisir la requête dans la zone de mot clé. Vous pouvez aussi copier votre requête à partir de Word ou d’Excel, puis la coller dans un éditeur de texte brut, comme le Bloc-notes Microsoft. Enregistrez ensuite le fichier texte, puis sélectionnez **ANSI** dans la liste déroulante **Encodage**. Cette action supprime tout le formatage et tous les caractères non pris en charge. Vous pouvez ensuite copier la requête du fichier texte vers la zone de mot clé de la requête.

## Conseils et astuces pour la recherche

  - Les recherches par mot-clé ne respectent pas la casse. Par exemple, **cat** et **CAT** renvoient les mêmes résultats.

  - Un espace entre deux mots-clés ou deux expressions `property:value` revient au même que l’utilisation de l’opérateur **AND**. Par exemple, `from:"Sara Davis" subject:reorganization` renvoie tous les messages envoyés par Sara Davis contenant le mot **reorganization** dans la ligne d’objet.

  - Utilisez la syntaxe correspondant au format `property:value`. Les valeurs ne respectent pas la casse et doivent être collées à l’opérateur. Si un espace est présent, la valeur prévue fera l’objet d’une recherche en texte intégral. Exemple : **pilarp** permet de rechercher « pilarp » en tant que mot-clé, et non les messages qui ont été envoyés à pilarp.

  - Lorsque vous lancez une recherche sur une propriété de destinataire, telle que To, From, Cc ou Recipients, vous pouvez utiliser une adresse SMTP, un alias ou un nom d’affichage pour désigner un destinataire. Par exemple, vous pouvez saisir pilarp@contoso.com, pilarp ou « Pilar Pinilla ».

  - Vous pouvez utiliser uniquement des recherches par caractères génériques préfixées (par exemple, **cat\*** ou **set\***). Les recherches par caractères génériques suffixées (\*cat) ou les recherches par caractères génériques de sous-chaîne (\*cat\*) ne sont pas prises en charge.

  - Lorsque vous recherchez une propriété, utilisez des guillemets (" ") si la valeur est composée de plusieurs mots. Par exemple, **subject:budget Q1** renvoie des messages contenant **budget** sur la ligne d’objet et qui contiennent **Q1** n’importe où dans le message ou dans n’importe quelle propriété du message. L’utilisation de **subject:"budget Q1"** renvoie tous les messages contenant **budget Q1** n’importe où sur la ligne d’objet.

