---
title: 'Formats de fichier indexés par la recherche Exchange: Exchange 2013 Help'
TOCTitle: Formats de fichier indexés par le service de recherche Exchange
ms:assetid: e5110ac1-28e1-4554-acc3-85d08c997bc5
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Ee633485(v=EXCHG.150)
ms:contentKeyID: 52063013
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Formats de fichier indexés par le service de recherche Exchange

 

_**Sapplique à :** Exchange Online, Exchange Server 2013_

_**Dernière rubrique modifiée :** 2015-07-21_

Dans MicrosoftExchange Server 2013 et Exchange Online, le service de recherche Exchange comprend des filtres destinés à indexer les types de formats de fichiers les plus courants inclus en tant que pièces jointes de messages. Vous pouvez également installer des filtres pour indexer des types de fichiers supplémentaires.

> [!NOTE]
> Dans Exchange 2013, il n'est pas nécessaire d’installer et d’enregistrer Microsoft Office Filter Pack.


Quand vous gérez ou utilisez le service de recherche Exchange et les fonctionnalités dépendantes (comme la [Découverte électronique locale](in-place-ediscovery-exchange-2013-help.md)), tenez compte des différences qu'il existe entre des éléments impossibles à rechercher et des formats de fichiers dont l’indexation a été désactivée ou qui contiennent du contenu qui ne peut pas être indexé :

  - **Éléments impossibles à rechercher**   Quand le service de recherche Exchange ne parvient pas à indexer un type de fichier en particulier pour quelque raison que ce soit (si aucun filtre n'est installé, par exemple), la recherche du type de fichier échoue. Les messages contenant de telles pièces jointes sont marqués comme *partiellement indexés*. Les éléments impossibles à rechercher peuvent être récupérés à l'aide de la cmdlet [Get-FailedContentIndexDocuments](https://technet.microsoft.com/fr-fr/library/dd351154\(v=exchg.150\)). Lors de la copie des résultats de recherche de découverte électronique locale vers une boîte aux lettres de découverte ou lors de l’exportation des résultats de la recherche vers un fichier PST, vous pouvez inclure des éléments impossibles à rechercher. Pour plus d’informations, consultez la rubrique [Éléments impossibles à rechercher dans la découverte électronique Exchange](unsearchable-items-in-exchange-ediscovery-exchange-2013-help.md).

  - **Formats de fichiers avec du contenu impossible à indexer**   Certains types de fichiers, tels que WMV (Windows Media Video), n'incluent pas de contenu impossible à indexer et, par conséquent, ne sont pas indexés. Les messages contenant des pièces jointes correspondant à ces types de fichiers ne sont pas renvoyés en tant qu'éléments impossibles à rechercher dans les recherches de découverte électronique locale.

  - **Formats de fichiers désactivés** Dans les organisations locales, un administrateur peut désactiver l'indexation d'un format de fichier spécifique. Les messages contenant une pièce jointe d’un format désactivé ne sont pas renvoyés comme éléments impossibles à rechercher.

> [!Important]  
> Même si une pièce jointe de message peut être impossible à rechercher ou est dans un format de fichier ne pouvant pas être indexé, l’objet du message, le corps du message et d’autres métadonnées peuvent être indexés pour que le message puisse être renvoyé dans les recherches.


Pour les autres tâches de gestion relatives au service de recherche Exchange dans des organisations locales, consultez la rubrique [Procédures relatives au service de recherche Exchange](exchange-search-procedures-exchange-2013-help.md).

## Filtres par défaut

Le tableau suivant répertorie les filtres de recherche par défaut installés sur un serveur de boîtes aux lettres Exchange 2013 et dans Exchange Online. Vous pouvez récupérer la liste des filtres par défaut à l'aide de la cmdlet [Get-SearchDocumentFormat](https://technet.microsoft.com/fr-fr/library/jj873755\(v=exchg.150\)).


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Filtre</th>
<th>Extension de fichier</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Message électronique</p></td>
<td><p>.eml</p></td>
</tr>
<tr class="even">
<td><p>Format GIF (Graphics Interchange Format)</p></td>
<td><p>.gif</p></td>
</tr>
<tr class="odd">
<td><p>JPEG</p></td>
<td><p>.jpeg</p></td>
</tr>
<tr class="even">
<td><p>Microsoft Excel</p></td>
<td><p>.xls, .xlt, .xlsx, .xlsm, .xlb, .xlc, .xlsb</p></td>
</tr>
<tr class="odd">
<td><p>Fichier Excel</p></td>
<td><p>odbcexcel</p></td>
</tr>
<tr class="even">
<td><p>Microsoft InfoPath</p></td>
<td><p>.infopathml</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft Office Binder</p></td>
<td><p>.obt, obd</p></td>
</tr>
<tr class="even">
<td><p>Microsoft PowerPoint</p></td>
<td><p>.pptx, .pptm, .ppt, .ppsx, .ppsm, .pps, .ppam, .potm, .pot, .potx</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft Publisher</p></td>
<td><p>.pub</p></td>
</tr>
<tr class="even">
<td><p>Microsoft Word</p></td>
<td><p>.doc, .docm, .dotx, .dotm, .dot, .docx</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft XML Paper Specification</p></td>
<td><p>.xps</p></td>
</tr>
<tr class="even">
<td><p>OneNote</p></td>
<td><p>.one</p></td>
</tr>
<tr class="odd">
<td><p>Présentation OpenDocument</p></td>
<td><p>.odp</p></td>
</tr>
<tr class="even">
<td><p>Feuille de calcul OpenDocument</p></td>
<td><p>.ods</p></td>
</tr>
<tr class="odd">
<td><p>Texte OpenDocument</p></td>
<td><p>.odt</p></td>
</tr>
<tr class="even">
<td><p>Élément Outlook</p></td>
<td><p>.msg</p></td>
</tr>
<tr class="odd">
<td><p>Portable Document Format</p></td>
<td><p>.pdf</p></td>
</tr>
<tr class="even">
<td><p>Format RTF (Rich Text Format)</p></td>
<td><p>.rtf</p></td>
</tr>
<tr class="odd">
<td><p>Texte</p></td>
<td><p>.txt</p></td>
</tr>
<tr class="even">
<td><p>vCalendar</p></td>
<td><p>.vcs</p></td>
</tr>
<tr class="odd">
<td><p>vCard</p></td>
<td><p>.vcf</p></td>
</tr>
<tr class="even">
<td><p>Visio</p></td>
<td><p>.vdw, .vsd, .vss, .vst, .vsx, .vtx, .vssx, .vssm, .vsdm, .vstx, .vstm, .vdx</p></td>
</tr>
<tr class="odd">
<td><p>Archive web</p></td>
<td><p>.mhtml</p></td>
</tr>
<tr class="even">
<td><p>Page web</p></td>
<td><p>.html</p></td>
</tr>
<tr class="odd">
<td><p>Document XML</p></td>
<td><p>.xml</p></td>
</tr>
<tr class="even">
<td><p>Archive ZIP</p></td>
<td><p>.zip</p></td>
</tr>
</tbody>
</table>


## Formats de fichiers désactivés

Le tableau suivant répertorie les filtres de recherche qui sont désactivés pour l’indexation par défaut sur un serveur de boîtes aux lettres Exchange 2013 et dans Exchange Online. Dans Exchange 2013, les administrateurs peuvent désactiver ou réactiver un format de fichier pris en charge pour l’indexation à l’aide de la cmdlet [Set-SearchDocumentFormat](https://technet.microsoft.com/fr-fr/library/jj873756\(v=exchg.150\)). Cette cmdlet n'est pas disponible dans Exchange Online.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Filtre</th>
<th>Extension de fichier</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>AVI</p></td>
<td><p>.avi</p></td>
</tr>
<tr class="even">
<td><p>Bitmap</p></td>
<td><p>.bmp</p></td>
</tr>
<tr class="odd">
<td><p>MP3</p></td>
<td><p>.mp3</p></td>
</tr>
<tr class="even">
<td><p>MPEG</p></td>
<td><p>.mpeg</p></td>
</tr>
<tr class="odd">
<td><p>PNG</p></td>
<td><p>.png</p></td>
</tr>
<tr class="even">
<td><p>Microsoft Windows Wave Audio</p></td>
<td><p>.wav</p></td>
</tr>
</tbody>
</table>

