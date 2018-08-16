---
title: 'Texte du message DSN: Exchange 2013 Help'
TOCTitle: Texte du message DSN
ms:assetid: eae4a050-5ecb-4c87-b377-74edb93a5995
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb125135(v=EXCHG.150)
ms:contentKeyID: 50479488
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Texte du message DSN

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2015-03-09_

Vous pouvez inclure du texte dans un message de notification d'état de remise (DSN) dans Microsoft Exchange Server 2013 et lui donner un format HTML.

Vous pouvez inclure toute information que vous voulez afficher à l'intention du destinataire du message DSN. Par exemple, vous pouvez inclure une description détaillée du message DSN, des informations de contact pour l'Assistance et un lien vers le site Web du Support technique. Chaque message DSN peut contenir un maximum de 512 caractères.

Puisque les messages DSN peuvent être affichés en HTML, vous pouvez intégrer des balises de formatage HTML dans le texte DSN. Par exemple, pour mettre en gras une partie du texte d'un message DSN, placez le texte entre balises HTML \<B\> et \</B\>. Le tableau suivant propose des exemples de balises HTML valides utilisables dans un texte de message DSN.

### Balises HTML valides utilisables dans les messages DSN

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Balise HTML</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>&lt;B&gt;</p></td>
<td><p>Début du gras</p></td>
</tr>
<tr class="even">
<td><p>&lt;/B&gt;</p></td>
<td><p>Fin du gras</p></td>
</tr>
<tr class="odd">
<td><p>&lt;A HREF=&quot;url&quot;&gt;</p></td>
<td><p>Début du lien hypertexte</p></td>
</tr>
<tr class="even">
<td><p>&lt;/A&gt;</p></td>
<td><p>Fin du lien hypertexte</p></td>
</tr>
<tr class="odd">
<td><p>&lt;BR&gt;</p></td>
<td><p>Saut de lien</p></td>
</tr>
<tr class="even">
<td><p>&lt;EM&gt;</p></td>
<td><p>Début de l'italique</p></td>
</tr>
<tr class="odd">
<td><p>&lt;/EM&gt;</p></td>
<td><p>Fin de l'italique</p></td>
</tr>
<tr class="even">
<td><p>&lt;P&gt;</p></td>
<td><p>Début du paragraphe</p></td>
</tr>
<tr class="odd">
<td><p>&lt;/P&gt;</p></td>
<td><p>Fin du paragraphe</p></td>
</tr>
</tbody>
</table>


> [!NOTE]
> Par défaut, Exchange envoie des messages DSN HTML mais vous pouvez le configurer pour qu'il envoie des messages DSN HTML à des destinataires internes, externes ou les deux. Pour configurer ce comportement, modifiez les paramètres <em>InternalDsnSendHtml</em> et <em>ExternalDsnSendHtml</em> à l'aide de la commande <strong>Set-TransportService</strong>.
> Lorsque le paramètre <em>InternalDsnSendHtml</em> est défini sur <code>$false</code>, Exchange supprime les balises HTML des messages DSN qui sont envoyés à des destinataires internes. Lorsque le paramètre <em>ExternalDsnSendHtml</em> est défini sur <code>$false</code>, Exchange supprime les balises HTML des messages DSN qui sont envoyés à des destinataires externes.


Les caractères suivants que Microsoft Exchange utilise dans le texte du message DSN ont des significations particulières :

  - Signe supérieur à (\>)

  - Signe inférieur à (\<)

  - Esperluette (&)

  - Guillemets (")

Ces caractères servent à déterminer le début et la fin des balises HTML et du texte devant être affiché à l'intention des destinataires. Si vous voulez afficher ces caractères dans des messages DSN, vous devez utiliser les codes d'échappement présentés dans le tableau suivant.

Par exemple, si vous voulez afficher le message `"Please contact the Help Desk at <1234>."`, vous devez ajouter `"Please contact the Help Desk at &lt;1234&gt;." ` au texte du message DSN.

### Codes d'échappement de caractère d'un message DSN

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Code d'échappement</th>
<th>Caractère</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>&amp;lt;</p></td>
<td><p>&lt;</p></td>
</tr>
<tr class="even">
<td><p>&amp;gt;</p></td>
<td><p>&gt;</p></td>
</tr>
<tr class="odd">
<td><p>&amp;quot;</p></td>
<td><p>&quot;</p></td>
</tr>
<tr class="even">
<td><p>&amp;amp;</p></td>
<td><p>&amp;</p></td>
</tr>
</tbody>
</table>


> [!IMPORTANT]
> Si vous incluez une balise HTML dans un texte de message DSN qui contient des guillemets (&quot;), telle que <code>&lt;A HREF=&quot;url&quot;&gt;</code>, vous devez placer le texte complet du message DSN entre guillemets simples ('). Vous recevez un message d'erreur si vous placez le texte complet du message DSN et une balise HTML entre guillemets doubles.

