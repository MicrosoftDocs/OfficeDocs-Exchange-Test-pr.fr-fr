---
title: 'Propriétés de message indexées par la recherche Exchange: Exchange 2013 Help'
TOCTitle: Propriétés de message indexées par la recherche Exchange
ms:assetid: a9754dc1-44aa-4076-8b59-a5d39246d5b0
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ983804(v=EXCHG.150)
ms:contentKeyID: 52063010
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Propriétés de message indexées par la recherche Exchange

 

_**Sapplique à :**Exchange Online, Exchange Server 2013_

_**Dernière rubrique modifiée :**2015-04-17_

Le service de recherche Exchange indexe de nombreuses propriétés d'éléments, notamment l'expéditeur, les destinataires, le corps des messages et les pièces jointes aux messages électroniques.

## Propriétés indexées par le service de recherche Exchange

Le tableau suivant contient la liste de toutes les propriétés d'éléments indexées par le service de recherche Exchange.


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
<th>Propriété</th>
<th>Type</th>
<th>Utilisable dans une requête</th>
<th>Peut faire l'objet d'une recherche</th>
<th>Affichable dans les résultats d'une recherche</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Account</p></td>
<td><p>Chaîne</p></td>
<td><p>Oui</p></td>
<td><p>Oui</p></td>
<td><p>Non</p></td>
</tr>
<tr class="even">
<td><p>Assistantname</p></td>
<td><p>Chaîne</p></td>
<td><p>Oui</p></td>
<td><p>Oui</p></td>
<td><p>Non</p></td>
</tr>
<tr class="odd">
<td><p>Attachment</p></td>
<td><p>Chaîne</p></td>
<td><p>Oui</p></td>
<td><p>Oui</p></td>
<td><p>Non</p></td>
</tr>
<tr class="even">
<td><p>Attachmentfilenames</p></td>
<td><p>Chaîne</p></td>
<td><p>Oui</p></td>
<td><p>Oui</p></td>
<td><p>Non</p></td>
</tr>
<tr class="odd">
<td><p>Attachmentmetaproperties</p></td>
<td><p>Chaîne</p></td>
<td><p>Non</p></td>
<td><p>Oui</p></td>
<td><p>Non</p></td>
</tr>
<tr class="even">
<td><p>Attachmentcount</p></td>
<td><p>Entier</p></td>
<td><p>Non</p></td>
<td><p>Non</p></td>
<td><p>Oui</p></td>
</tr>
<tr class="odd">
<td><p>Bcc</p></td>
<td><p>Chaîne</p></td>
<td><p>Oui</p></td>
<td><p>Oui</p></td>
<td><p>Non</p></td>
</tr>
<tr class="even">
<td><p>Body</p></td>
<td><p>Chaîne</p></td>
<td><p>Oui</p></td>
<td><p>Oui</p></td>
<td><p>Non</p></td>
</tr>
<tr class="odd">
<td><p>Businessaddress</p></td>
<td><p>Chaîne</p></td>
<td><p>Oui</p></td>
<td><p>Oui</p></td>
<td><p>Non</p></td>
</tr>
<tr class="even">
<td><p>Businessmainphone</p></td>
<td><p>Chaîne</p></td>
<td><p>Oui</p></td>
<td><p>Oui</p></td>
<td><p>Non</p></td>
</tr>
<tr class="odd">
<td><p>Businessphonenumber</p></td>
<td><p>Chaîne</p></td>
<td><p>Oui</p></td>
<td><p>Oui</p></td>
<td><p>Non</p></td>
</tr>
<tr class="even">
<td><p>Carphonenumber</p></td>
<td><p>Chaîne</p></td>
<td><p>Oui</p></td>
<td><p>Oui</p></td>
<td><p>Non</p></td>
</tr>
<tr class="odd">
<td><p>Catégorie</p></td>
<td><p>Chaîne</p></td>
<td><p>Oui</p></td>
<td><p>Oui</p></td>
<td><p>Non</p></td>
</tr>
<tr class="even">
<td><p>Cc</p></td>
<td><p>Chaîne</p></td>
<td><p>Oui</p></td>
<td><p>Oui</p></td>
<td><p>Non</p></td>
</tr>
<tr class="odd">
<td><p>Companyname</p></td>
<td><p>Chaîne</p></td>
<td><p>Oui</p></td>
<td><p>Oui</p></td>
<td><p>Non</p></td>
</tr>
<tr class="even">
<td><p>Compositeitemid</p></td>
<td><p>Chaîne</p></td>
<td><p>Non</p></td>
<td><p>Non</p></td>
<td><p>Oui</p></td>
</tr>
<tr class="odd">
<td><p>Conversationid</p></td>
<td><p>Entier</p></td>
<td><p>Non</p></td>
<td><p>Non</p></td>
<td><p>Oui</p></td>
</tr>
<tr class="even">
<td><p>Conversationtopic</p></td>
<td><p>Chaîne</p></td>
<td><p>Oui</p></td>
<td><p>Oui</p></td>
<td><p>Non</p></td>
</tr>
<tr class="odd">
<td><p>Departmentname</p></td>
<td><p>Chaîne</p></td>
<td><p>Oui</p></td>
<td><p>Oui</p></td>
<td><p>Non</p></td>
</tr>
<tr class="even">
<td><p>Displayname</p></td>
<td><p>Chaîne</p></td>
<td><p>Oui</p></td>
<td><p>Oui</p></td>
<td><p>Non</p></td>
</tr>
<tr class="odd">
<td><p>Displaynameprefix</p></td>
<td><p>Chaîne</p></td>
<td><p>Oui</p></td>
<td><p>Oui</p></td>
<td><p>Non</p></td>
</tr>
<tr class="even">
<td><p>Documentid</p></td>
<td><p>Entier</p></td>
<td><p>Oui</p></td>
<td><p>Non</p></td>
<td><p>Oui</p></td>
</tr>
<tr class="odd">
<td><p>Emailaddress</p></td>
<td><p>Chaîne</p></td>
<td><p>Oui</p></td>
<td><p>Oui</p></td>
<td><p>Non</p></td>
</tr>
<tr class="even">
<td><p>Emaildisplayname</p></td>
<td><p>Chaîne</p></td>
<td><p>Oui</p></td>
<td><p>Oui</p></td>
<td><p>Non</p></td>
</tr>
<tr class="odd">
<td><p>Emailoriginaldisplayname</p></td>
<td><p>Chaîne</p></td>
<td><p>Oui</p></td>
<td><p>Oui</p></td>
<td><p>Non</p></td>
</tr>
<tr class="even">
<td><p>Errorcode</p></td>
<td><p>Entier</p></td>
<td><p>Oui</p></td>
<td><p>Non</p></td>
<td><p>Oui</p></td>
</tr>
<tr class="odd">
<td><p>Fileas</p></td>
<td><p>Chaîne</p></td>
<td><p>Oui</p></td>
<td><p>Oui</p></td>
<td><p>Non</p></td>
</tr>
<tr class="even">
<td><p>Firstname</p></td>
<td><p>Chaîne</p></td>
<td><p>Oui</p></td>
<td><p>Oui</p></td>
<td><p>Non</p></td>
</tr>
<tr class="odd">
<td><p>Folderid</p></td>
<td><p>Chaîne</p></td>
<td><p>Oui</p></td>
<td><p>Non</p></td>
<td><p>Non</p></td>
</tr>
<tr class="even">
<td><p>From</p></td>
<td><p>Chaîne</p></td>
<td><p>Oui</p></td>
<td><p>Oui</p></td>
<td><p>Non</p></td>
</tr>
<tr class="odd">
<td><p>Homeaddress</p></td>
<td><p>Chaîne</p></td>
<td><p>Oui</p></td>
<td><p>Oui</p></td>
<td><p>Non</p></td>
</tr>
<tr class="even">
<td><p>Homephone</p></td>
<td><p>Chaîne</p></td>
<td><p>Oui</p></td>
<td><p>Oui</p></td>
<td><p>Non</p></td>
</tr>
<tr class="odd">
<td><p>Importance</p></td>
<td><p>Entier</p></td>
<td><p>Oui</p></td>
<td><p>Non</p></td>
<td><p>Non</p></td>
</tr>
<tr class="even">
<td><p>Ispartiallyprocessed</p></td>
<td><p>Booléen</p></td>
<td><p>Oui</p></td>
<td><p>Non</p></td>
<td><p>Oui</p></td>
</tr>
<tr class="odd">
<td><p>Ispermanentfailure</p></td>
<td><p>Booléen</p></td>
<td><p>Oui</p></td>
<td><p>Non</p></td>
<td><p>Oui</p></td>
</tr>
<tr class="even">
<td><p>Itemclass</p></td>
<td><p>Chaîne</p></td>
<td><p>Oui</p></td>
<td><p>Non</p></td>
<td><p>Non</p></td>
</tr>
<tr class="odd">
<td><p>Kind</p></td>
<td><p>Chaîne</p></td>
<td><p>Oui</p></td>
<td><p>Oui</p></td>
<td><p>Non</p></td>
</tr>
<tr class="even">
<td><p>Lastattempttime</p></td>
<td><p>DateTime</p></td>
<td><p>Oui</p></td>
<td><p>Non</p></td>
<td><p>Oui</p></td>
</tr>
<tr class="odd">
<td><p>Lastname</p></td>
<td><p>Chaîne</p></td>
<td><p>Oui</p></td>
<td><p>Oui</p></td>
<td><p>Non</p></td>
</tr>
<tr class="even">
<td><p>Mailboxguid</p></td>
<td><p>Chaîne</p></td>
<td><p>Oui</p></td>
<td><p>Non</p></td>
<td><p>Oui</p></td>
</tr>
<tr class="odd">
<td><p>Manager</p></td>
<td><p>Chaîne</p></td>
<td><p>Oui</p></td>
<td><p>Oui</p></td>
<td><p>Non</p></td>
</tr>
<tr class="even">
<td><p>Meetinglocation</p></td>
<td><p>Chaîne</p></td>
<td><p>Oui</p></td>
<td><p>Oui</p></td>
<td><p>Non</p></td>
</tr>
<tr class="odd">
<td><p>Middlename</p></td>
<td><p>Chaîne</p></td>
<td><p>Oui</p></td>
<td><p>Oui</p></td>
<td><p>Non</p></td>
</tr>
<tr class="even">
<td><p>Mobilephonenumber</p></td>
<td><p>Chaîne</p></td>
<td><p>Oui</p></td>
<td><p>Oui</p></td>
<td><p>Non</p></td>
</tr>
<tr class="odd">
<td><p>Nickname</p></td>
<td><p>Chaîne</p></td>
<td><p>Oui</p></td>
<td><p>Oui</p></td>
<td><p>Non</p></td>
</tr>
<tr class="even">
<td><p>Officelocation</p></td>
<td><p>Chaîne</p></td>
<td><p>Oui</p></td>
<td><p>Oui</p></td>
<td><p>Non</p></td>
</tr>
<tr class="odd">
<td><p>Otheraddress</p></td>
<td><p>Chaîne</p></td>
<td><p>Oui</p></td>
<td><p>Oui</p></td>
<td><p>Non</p></td>
</tr>
<tr class="even">
<td><p>Participants</p></td>
<td><p>Chaîne</p></td>
<td><p>Oui</p></td>
<td><p>Oui</p></td>
<td><p>Non</p></td>
</tr>
<tr class="odd">
<td><p>Primarytelephonenumber</p></td>
<td><p>Chaîne</p></td>
<td><p>Oui</p></td>
<td><p>Oui</p></td>
<td><p>Non</p></td>
</tr>
<tr class="even">
<td><p>Received</p></td>
<td><p>Heure/Date</p></td>
<td><p>Oui</p></td>
<td><p>Non</p></td>
<td><p>Non</p></td>
</tr>
<tr class="odd">
<td><p>Receivedby</p></td>
<td><p>Chaîne</p></td>
<td><p>Oui</p></td>
<td><p>Oui</p></td>
<td><p>Non</p></td>
</tr>
<tr class="even">
<td><p>Receivedrepresenting</p></td>
<td><p>Chaîne</p></td>
<td><p>Oui</p></td>
<td><p>Oui</p></td>
<td><p>Non</p></td>
</tr>
<tr class="odd">
<td><p>Recipients</p></td>
<td><p>Chaîne</p></td>
<td><p>Oui</p></td>
<td><p>Oui</p></td>
<td><p>Non</p></td>
</tr>
<tr class="even">
<td><p>Sent</p></td>
<td><p>Heure/Date</p></td>
<td><p>Oui</p></td>
<td><p>Non</p></td>
<td><p>Non</p></td>
</tr>
<tr class="odd">
<td><p>Sharinginfo</p></td>
<td><p>Chaîne</p></td>
<td><p>Oui</p></td>
<td><p>Non</p></td>
<td><p>Non</p></td>
</tr>
<tr class="even">
<td><p>Size</p></td>
<td><p>Entier</p></td>
<td><p>Oui</p></td>
<td><p>Non</p></td>
<td><p>Non</p></td>
</tr>
<tr class="odd">
<td><p>Subject</p></td>
<td><p>Chaîne</p></td>
<td><p>Oui</p></td>
<td><p>Oui</p></td>
<td><p>Non</p></td>
</tr>
<tr class="even">
<td><p>Tasktitle</p></td>
<td><p>Chaîne</p></td>
<td><p>Oui</p></td>
<td><p>Oui</p></td>
<td><p>Non</p></td>
</tr>
<tr class="odd">
<td><p>Title</p></td>
<td><p>Chaîne</p></td>
<td><p>Oui</p></td>
<td><p>Oui</p></td>
<td><p>Non</p></td>
</tr>
<tr class="even">
<td><p>To</p></td>
<td><p>Chaîne</p></td>
<td><p>Oui</p></td>
<td><p>Oui</p></td>
<td><p>Non</p></td>
</tr>
<tr class="odd">
<td><p>Umaudionotes</p></td>
<td><p>Chaîne</p></td>
<td><p>Oui</p></td>
<td><p>Oui</p></td>
<td><p>Non</p></td>
</tr>
<tr class="even">
<td><p>Watermark</p></td>
<td><p>Entier</p></td>
<td><p>Non</p></td>
<td><p>Non</p></td>
<td><p>Oui</p></td>
</tr>
<tr class="odd">
<td><p>Yomicompanyname</p></td>
<td><p>Chaîne</p></td>
<td><p>Oui</p></td>
<td><p>Non</p></td>
<td><p>Oui</p></td>
</tr>
<tr class="even">
<td><p>Yomifirstname</p></td>
<td><p>Chaîne</p></td>
<td><p>Oui</p></td>
<td><p>Oui</p></td>
<td><p>Non</p></td>
</tr>
<tr class="odd">
<td><p>Yomilastname</p></td>
<td><p>Chaîne</p></td>
<td><p>Oui</p></td>
<td><p>Oui</p></td>
<td><p>Non</p></td>
</tr>
</tbody>
</table>


**Remarques sur les propriétés indexées** :

  - Les **propriétés utilisables dans une requête** peuvent être utilisées dans des requêtes AQS (syntaxe de recherche avancée) par des clients de recherche tels que Outlook Web App dans les paires `property:value`, par exemple, `from:bsuneja@cotoso.com`. Vous pouvez également utiliser un sous-ensemble des propriétés répertoriées dans le tableau précédent dans des requêtes de recherche pour la découverte électronique inaltérable. Pour obtenir la liste de ces propriétés, voir [Propriétés de message et opérateurs de recherche pour la découverte électronique inaltérable](message-properties-and-search-operators-for-in-place-ediscovery-exchange-2013-help.md).

  - Les **propriétés pouvant faire l’objet d’une recherche** sont des propriétés qui ne peuvent pas être spécifiées dans des paires `property:value`, mais une recherche par mot-clé renvoie la valeur éventuellement détectée dans une propriété pouvant faire l’objet d’une recherche. Par exemple, vous ne pouvez pas utiliser `body:Contoso` pour rechercher la chaîne `contoso` dans le corps du message uniquement. Toutefois, une recherche de cette chaîne renvoie tous les éléments contenant la propriété dans n'importe quelle propriété pouvant faire l'objet d'une recherche.

  - Les **propriétés affichables dans les résultats d'une recherche**, telles que `documenteid` et `ispartiallyprocessed`, sont renvoyées pour chaque recherche.

