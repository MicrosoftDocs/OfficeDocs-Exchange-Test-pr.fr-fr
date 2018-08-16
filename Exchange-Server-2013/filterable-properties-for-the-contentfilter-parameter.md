---
title: 'Propriétés filtrables pour le paramètre -ContentFilter: Exchange 2013 Help'
TOCTitle: Propriétés filtrables pour le paramètre -ContentFilter
ms:assetid: cf504a59-1938-489c-bb48-b27b2ac3234e
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Ff601762(v=EXCHG.150)
ms:contentKeyID: 50555494
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Propriétés filtrables pour le paramètre -ContentFilter

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2015-09-10_

Cette rubrique répertorie les propriétés filtrables pour le paramètre *ContentFilter*. Le paramètre *ContentFilter* sert à exporter des messages vers un fichier .pst compatible avec le filtre. Le paramètre *ContentFilter* est utilisé dans la cmdlet [New-MailboxExportRequest](https://technet.microsoft.com/fr-fr/library/ff607299\(v=exchg.150\)).

## Propriétés filtrables

De nombreuses propriétés du paramètre *ContentFilter* acceptent les caractères génériques. Si vous utilisez un caractère générique, optez pour l’opérateur**-like** plutôt que l’opérateur **-eq**. L’opérateur **-like** permet de chercher des modèles correspondants dans des types riches (des chaînes, par exemple) tandis que l’opérateur **-eq** permet de chercher une correspondance exacte.

Le tableau qui suit contient une liste des propriétés filtrables pour le paramètre *ContentFilter*. Il répertorie le nom de la propriété, la décrit et affiche ses valeurs acceptables, ainsi qu’un exemple de syntaxe. Pour plus d’informations sur les filtres OPATH, consultez la rubrique [Filtres dans les commandes de l’environnement de ligne de commande Exchange Management Shell du destinataire](https://technet.microsoft.com/fr-fr/library/bb124268\(v=exchg.150\)).


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
<th>Description</th>
<th>Valeurs</th>
<th>Exemple de syntaxe</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>All</p></td>
<td><p>Cette propriété renvoie tous les messages dotés d’une chaîne spécifique dans toutes les propriétés indexées. Vous pouvez, par exemple, utiliser cette propriété pour exporter tous les messages affichant l’utilisateur « Ayla » en tant que destinataire ou expéditeur, ou bien afficher le nom dans le corps du message.</p></td>
<td><p>Chaîne</p>
<p>Caractère générique</p></td>
<td><pre><code>-ContentFilter {All -like &#39;*Ayla*&#39;}</code></pre></td>
</tr>
<tr class="even">
<td><p>Attachment</p></td>
<td><p>Cette propriété renvoie des messages dotés d’une chaîne spécifique dans le contenu ou le nom de fichier d’une pièce jointe.</p></td>
<td><p>Chaîne</p>
<p>Caractère générique</p></td>
<td><pre><code>-ContentFilter {Attachment -like &#39;*.jpg&#39;}</code></pre></td>
</tr>
<tr class="odd">
<td><p>BCC</p></td>
<td><p>Cette propriété renvoie des messages envoyés et dotés d’un destinataire spécifié dans le champ Cci.</p></td>
<td><p>Nom complet</p>
<p>Alias</p>
<p>Adresse SMTP</p>
<p>LegacyDN</p>
<p>Caractère générique</p></td>
<td><pre><code>-ContentFilter {(BCC -eq &#39;ayla@contoso.com&#39;) -or (BCC -eq &#39;tony@contoso.com&#39;)}</code></pre></td>
</tr>
<tr class="even">
<td><p>Body</p></td>
<td><p>Cette propriété renvoie des messages dotés d’une chaîne spécifiée dans le corps du message.</p></td>
<td><p>Chaîne</p>
<p>Caractère générique</p></td>
<td><pre><code>-ContentFilter {Body -like &#39;*prospectus*&#39;}</code></pre></td>
</tr>
<tr class="odd">
<td><p>Category</p></td>
<td><p>Cette propriété renvoie les messages pour lesquels une catégorie correspondante existe. Les catégories sont définies par les utilisateurs ou des règles de boîte de réception.</p></td>
<td><p>Chaîne</p>
<p>Caractère générique</p></td>
<td><pre><code>-ContentFilter {Category -like &#39;*Blue*&#39;}</code></pre></td>
</tr>
<tr class="even">
<td><p>CC</p></td>
<td><p>Cette propriété renvoie des messages envoyés et dotés d’un destinataire spécifié dans le champ Cc.</p></td>
<td><p>Nom complet</p>
<p>Alias</p>
<p>Adresse SMTP</p>
<p>LegacyDN</p>
<p>Caractère générique</p></td>
<td><pre><code>-ContentFilter {(CC -eq &#39;ayla@contoso.com&#39;) -or (CC -eq &#39;tony@contoso.com&#39;)}</code></pre></td>
</tr>
<tr class="odd">
<td><p>Expires</p></td>
<td><p>Cette propriété renvoie les messages dont la date et l’heure d’expiration sont précisées.</p></td>
<td><p>Horodatage</p></td>
<td><pre><code>-ContentFilter {Expires -lt &#39;01/01/2013&#39;}</code></pre></td>
</tr>
<tr class="even">
<td><p>HasAttachment</p></td>
<td><p>Cette propriété renvoie des messages avec ou sans pièces jointes.</p></td>
<td><p>Booléen</p>
<p><code>$true</code> ou <code>$false</code></p></td>
<td><pre><code>-ContentFilter {HasAttachment -eq $true}</code></pre></td>
</tr>
<tr class="odd">
<td><p>Importance</p></td>
<td><p>Cette propriété renvoie les messages dont le niveau d’importance est précisé.</p></td>
<td><p>0 ou « Faible »</p>
<p>1 ou « Normal »</p>
<p>2 ou « Élevé »</p></td>
<td><pre><code>-ContentFilter {Importance -eq &#39;high&#39;}</code></pre>
<pre><code>-ContentFilter {Importance -eq 2}</code></pre></td>
</tr>
<tr class="even">
<td><p>IsFlagged</p></td>
<td><p>Cette propriété renvoie des messages qui ont signalés par l’utilisateur ou une règle de boîte de réception.</p></td>
<td><p>Booléen</p>
<p><code>$true</code> ou  <code>$false</code></p></td>
<td><pre><code>-ContentFilter {IsFlagged -eq $true}</code></pre></td>
</tr>
<tr class="odd">
<td><p>IsRead</p></td>
<td><p>Cette propriété renvoie des messages qui ont été lus, ou pas, par l’utilisateur.</p></td>
<td><p>Booléen</p>
<p><code>$true</code> ou  <code>$false</code></p></td>
<td><pre><code>-ContentFilter {IsRead -eq $true}</code></pre></td>
</tr>
<tr class="even">
<td><p>MessageKind</p></td>
<td><p>Cette propriété renvoie des messages qui sont du type spécifié.</p></td>
<td><p>Calendrier</p>
<p>Contact</p>
<p>Doc</p>
<p>Email</p>
<p>Télécopie</p>
<p>InstantMessage</p>
<p>Journal</p>
<p>Remarque</p>
<p>Publier</p>
<p>RSSFeed</p>
<p>Tâche</p>
<p>Messagerie vocale</p></td>
<td><pre><code>-ContentFilter {MessageKind -eq &#39;Calendar&#39;}</code></pre>
<pre><code>-ContentFilter {MessageKind -ne &#39;Email&#39;}</code></pre></td>
</tr>
<tr class="odd">
<td><p>MessageLocalee</p></td>
<td><p>Cette propriété renvoie des messages munis des paramètres régionaux spécifiés.</p></td>
<td><p>CultureInfo</p></td>
<td><pre><code>-ContentFilter {MessageLocale -ne &#39;en-US&#39;}</code></pre>
<pre><code>-ContentFilter {MessageLocale -eq &#39;tr-TR&#39;}</code></pre></td>
</tr>
<tr class="even">
<td><p>Participants</p></td>
<td><p>Cette propriété renvoie des messages qui affichent le destinataire spécifié dans les champs À, Cci ou Cc.</p></td>
<td><p>Nom complet</p>
<p>Alias</p>
<p>Adresse SMTP</p>
<p>LegacyDN</p>
<p>Caractère générique</p></td>
<td><pre><code>-ContentFilter {(Participants -eq &#39;ayla@contoso.com&#39;) -or (Participants -eq &#39;tony@contoso.com&#39;)}</code></pre></td>
</tr>
<tr class="odd">
<td><p>PolicyTag</p></td>
<td><p>Cette propriété renvoie les messages dotés d’une balise de stratégie. La banque d’informations Exchange conserve les balises de stratégie sous la forme de GUID. Par conséquent, la chaîne peut contenir soit une valeur GUID explicite qui est alors recherchée par la balise PR_POLICY_TAG, soit une chaîne contenant un caractère générique.</p>
<p>Si la valeur fournie n’est pas un GUID, la commande utilise les informations Active Directory pour convertir les noms en GUID.</p></td>
<td><p>Chaîne</p>
<p>Caractère générique</p></td>
<td><pre><code>-ContentFilter {PolicyTag -ne &#39;00000000-0000-0000-0000-000000000000&#39;}</code></pre></td>
</tr>
<tr class="even">
<td><p>Received</p></td>
<td><p>Cette propriété renvoie les messages qui ont été reçus par le destinataire aux date et heure de réception précisées.</p></td>
<td><p>Horodatage</p></td>
<td><pre><code>-ContentFilter {Received -lt &#39;01/01/2013 9:00&#39;}</code></pre>
<pre><code>-ContentFilter {(Received -lt &#39;01/01/2013&#39;) -and (Received -gt &#39;01/01/2012&#39;)}</code></pre></td>
</tr>
<tr class="odd">
<td><p>Sender</p></td>
<td><p>Cette propriété renvoie les messages qui ont été reçus de l’expéditeur spécifié.</p></td>
<td><p>Nom complet</p>
<p>Alias</p>
<p>Adresse SMTP</p>
<p>LegacyDN</p>
<p>Caractère générique</p></td>
<td><pre><code>ContentFilter {Sender -eq &#39;tony&#39;}</code></pre></td>
</tr>
<tr class="even">
<td><p>Sent</p></td>
<td><p>Cette propriété renvoie les messages qui ont été envoyés par le destinataire aux date et heure d’envoi précisées.</p></td>
<td><p>Horodatage</p></td>
<td><pre><code>-ContentFilter {Sent -lt &#39;01/01/2013 9:00&#39;}</code></pre>
<pre><code>-ContentFilter {(Sent -lt &#39;01/01/2013&#39;) -and (Sent -gt &#39;01/01/2012&#39;)}</code></pre></td>
</tr>
<tr class="odd">
<td><p>Size</p></td>
<td><p>Cette propriété renvoie des messages d’une taille spécifique.</p></td>
<td><p>B (octets)</p>
<p>KB (kilo-octets)</p>
<p>MB (mégaoctets)</p></td>
<td><pre><code>-ContentFilter {Size -gt &#39;10KB&#39;}</code></pre></td>
</tr>
<tr class="even">
<td><p>Subject</p></td>
<td><p>Cette propriété renvoie des messages dotés d’une chaîne spécifiée dans l’objet du message.</p></td>
<td><p>Chaîne</p>
<p>Caractère générique</p></td>
<td><pre><code>-ContentFilter {Subject -like &#39;*meeting*&#39;}</code></pre></td>
</tr>
<tr class="odd">
<td><p>To</p></td>
<td><p>Cette propriété renvoie des messages envoyés et dotés du destinataire spécifié dans le champ À.</p></td>
<td><p>Nom complet</p>
<p>Alias</p>
<p>Adresse SMTP</p>
<p>LegacyDN</p>
<p>Caractère générique</p></td>
<td><pre><code>-ContentFilter {To -eq &#39;aylakol&#39;}</code></pre></td>
</tr>
</tbody>
</table>

