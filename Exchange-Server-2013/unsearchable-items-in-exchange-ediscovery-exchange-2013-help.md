---
title: 'Éléments impossibles à rechercher dans la découverte électronique Exchange: Exchange 2013 Help'
TOCTitle: Éléments impossibles à rechercher dans la découverte électronique Exchange
ms:assetid: 32550081-9af9-474b-ae7b-28f1e68cad41
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dn602498(v=EXCHG.150)
ms:contentKeyID: 61071980
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Éléments impossibles à rechercher dans la découverte électronique Exchange

 

_**Sapplique à :** Exchange Online, Exchange Server 2013_

_**Dernière rubrique modifiée :** 2016-12-09_

Dans la découverte électronique locale pour Exchange Server 2013 et Exchange Online, les éléments impossibles à rechercher sont des éléments de boîtes aux lettres qui ne peuvent pas être indexés par la recherche Exchange ou qui n’ont été que partiellement indexés. Un élément impossible à rechercher contient généralement un fichier, qui ne peut pas être indexé, joint à un message électronique. Voici certaines des raisons pour lesquelles les fichiers ne peuvent pas être indexés pour la recherche et sont renvoyés en tant qu’éléments impossibles à rechercher lorsqu’ils sont joints à un message électronique :

  - Le type de fichier n’est pris en charge pour l’indexation car un filtre de recherche (également appelé *IFilter*) destiné à indexer le format de fichier n’est pas installé.

  - Le type de fichier est désactivé pour l’indexation.

  - Le type de fichier est pris en charge pour l’indexation, mais une erreur d’indexation s’est produite pour un fichier spécifique.

  - Un fichier est chiffré avec des technologies autres que celles de Microsoft.

  - Un fichier est protégé par mot de passe.

Pour réussir la recherche de découverte électronique, votre organisation peut demander d’examiner les éléments impossibles à rechercher. Vous pouvez indiquer si vous souhaitez inclure les éléments impossibles à rechercher lorsque vous copiez les résultats de la recherche de découverte électronique vers une boîte aux lettres de découverte ou que vous exportez des résultats vers un fichier PST.

## Types de fichier non pris en charge pour la recherche

Certains types de fichier, tels que les fichiers Bitmap ou MP3, ne comportent pas de contenu pouvant être indexé. Par conséquent, la recherche Exchange n’effectue pas d’indexation de texte intégral sur ces types de fichier. Ces types de fichier sont considérés comme des types de fichier non pris en charge. Il existe également des types de fichier pour lesquels l’indexation de texte intégral a été désactivée, soit par défaut, soit par un administrateur. Les types de fichier non pris en charge et désactivés sont considérés comme des éléments impossibles à rechercher dans les recherches de découverte électronique. Ces types de fichier, qui sont généralement joints à un message électronique, sont inclus dans l’ensemble de résultats lorsque vous incluez les éléments impossibles à rechercher lors de la copie ou de l’exportation des résultats de la recherche. Pour obtenir la liste des formats de fichiers pris en charge et désactivés, consultez l’article [Formats de fichier indexés par le service de recherche Exchange](file-formats-indexed-by-exchange-search-exchange-2013-help.md). Dans Exchange Server 2013, les administrateurs peuvent désactiver l’indexation pour un format de fichier pris en charge à l’aide de la cmdlet [Set-SearchDocumentFormat](https://technet.microsoft.com/fr-fr/library/jj873756\(v=exchg.150\)). Cette cmdlet n’est pas disponible dans Exchange Online.

Pour identifier les éléments impossibles à rechercher dans une boîte aux lettres spécifique, vous pouvez exécuter la cmdlet [Get-FailedContentIndexDocuments](https://technet.microsoft.com/fr-fr/library/dd351154\(v=exchg.150\)) pour obtenir la liste des éléments qui doivent être copiés ou exportés si vous choisissez d’inclure les éléments impossibles à rechercher aux résultats de la recherche.

## Messages dont le type de fichier n’est pas pris en charge renvoyés dans les résultats de la recherche

Tous les messages avec une pièce jointe non prise en charge ne sont pas automatiquement renvoyés en tant qu’éléments impossibles à rechercher. En effet, d’autres propriétés de fichier, telles que le nom de fichier, sont indexées et peuvent faire l’objet d’une recherche. Par exemple, une recherche par mot clé sur « financier » renverra un message avec une pièce jointe non prise en charge si ce mot clé apparaît dans le nom du fichier. Si le mot clé apparaissait uniquement dans le corps de la pièce jointe, le message sera renvoyé en tant qu’élément impossible à rechercher.

De même, les messages comportant des pièces jointes non prises en charge sont inclus dans les résultats de la recherche lorsque d’autres propriétés d’un élément de boîte aux lettres, qui sont indexées et qui peuvent faire l’objet d’une recherche, répondent aux critères de recherche. Les propriétés des messages qui sont indexées pour la recherche comprennent les dates d’envoi et de réception, l’expéditeur et le destinataire, le nom de fichier d’une pièce jointe et le texte dans le corps du message. Ainsi, même si la pièce jointe d’un message est impossible à rechercher, le message sera inclus dans les résultats de la recherche ordinaire si la valeur d’autres propriétés du message correspond aux critères de recherche. En fait, il est courant que les messages comportant des pièces jointes impossibles à rechercher soient inclus dans les résultats de la recherche ordinaire.

Pour obtenir la liste des propriétés de message électronique indexées pour la recherche, consultez l’article [Propriétés de message indexées par la recherche Exchange](message-properties-indexed-by-exchange-search-exchange-2013-help.md).

## Inclusion d’éléments impossibles à rechercher dans les résultats de la recherche

Il se peut que votre organisation doive identifier et effectuer un traitement supplémentaire sur les éléments impossibles à rechercher pour déterminer leur nature, leur contenu et leur pertinence. Pour inclure des éléments impossibles à rechercher aux résultats de la recherche de découverte électronique, vous pouvez utiliser l’option relative aux éléments impossibles à rechercher lors de la copie ou de l’exportation des résultats de la recherche. Pour inclure les éléments impossibles à rechercher lors de l’utilisation de la découverte électronique locale dans Exchange ou Exchange Online, sélectionnez l’option **Inclure les éléments impossibles à rechercher** lors de la copie des résultats de la recherche vers une boîte aux lettres de découverte ou lors de leur exportation vers un fichier PST. Pour inclure des éléments impossibles à rechercher lors de l’utilisation du centre de découverte électronique dans SharePoint ou SharePoint Online, sélectionnez l’option **Inclure les éléments chiffrés ou dont le format n’est pas reconnu**.

Gardez les éléments suivants à l’esprit lors de la copie ou de l’exportation d’éléments impossibles à rechercher :

  - Lors de la copie d’éléments impossibles à rechercher dans une boîte aux lettres de découverte, tous ces éléments sont copiés dans un dossier distinct nommé **Impossible à rechercher**, situé sous le dossier contenant les résultats de la recherche. Lorsque vous exportez des résultats de la recherche et incluez les éléments impossibles à rechercher, ces derniers sont exportés vers un fichier PST distinct.

  - Lorsque vous incluez les éléments impossibles à rechercher dans les résultats de la recherche, tous ces éléments présents dans les boîtes aux lettres dans lesquelles la recherche est effectuée seront renvoyés, quels que soient les critères de recherche.

  - Si vous choisissez d’inclure tous les éléments de boîtes aux lettres dans les résultats de la recherche ou si une requête de recherche n’indique aucun mot clé ou seulement une plage de dates, les éléments impossibles à rechercher peuvent ne pas être copiés dans le dossier **Impossible à rechercher** si vous sélectionnez l’option d’inclusion des éléments impossibles à rechercher. En effet, tous les éléments, y compris ceux impossibles à rechercher, seront automatiquement inclus dans les résultats de la recherche ordinaire.

  - Comme indiqué précédemment, en raison de l’indexation des propriétés et des métadonnées de message, une recherche par mot clé peut renvoyer des résultats si un mot clé apparaît dans les propriétés ou métadonnées d’un message contenant une pièce jointe impossible à rechercher. Dans ce cas, le même élément de boîte aux lettres sera renvoyé deux fois dans les résultats de la recherche. Pour éviter ce type de duplication et n’inclure qu’une copie de l’élément dans les résultats de la recherche ordinaire, vous pouvez sélectionner l’option **Enregistrer uniquement une copie de chaque message** lors de la copie ou de l’exportation des résultats de la recherche.

  - Le fait d’inclure des éléments impossibles à rechercher dans les résultats de la recherche peut également avoir une incidence sur les résultats estimés de la recherche qui sont affichés. Si vous incluez les éléments impossibles à rechercher lors de la copie des résultats de la recherche, le nombre total d’éléments estimés et la taille estimée totale comprendront les éléments impossibles à rechercher.

Pour plus d’informations sur l’inclusion d’éléments impossibles à rechercher dans les résultats de la recherche, consultez les articles suivants :

  - [Créer une recherche de découverte électronique inaltérable](create-an-in-place-ediscovery-search-exchange-2013-help.md)

  - [Exporter les résultats de la recherche électronique vers un fichier PST](export-ediscovery-search-results-to-a-pst-file-exchange-2013-help.md)

  - [SharePoint : Exporter du contenu eDiscovery et créer des rapports](https://go.microsoft.com/fwlink/p/?linkid=324757)

## Plus d’informations sur les éléments impossibles à rechercher

  - Même si un type de fichier est pris en charge par la recherche Exchange et qu’il est indexé en texte intégral, des erreurs d’indexation ou de recherche peuvent se produire, ce qui entraînera le renvoi d’un fichier en tant qu’élément impossible à rechercher. Par exemple, la recherche d’un fichier Excel très volumineux peut être partiellement réussie, mais échouera par la suite en raison du dépassement de la limite de taille. Dans ce cas, il est possible que le même fichier soit renvoyé avec les résultats de la recherche et en tant qu’élément impossible à rechercher.

  - Les fichiers joints chiffrés à l’aide des technologies Microsoft sont indexés par la recherche Exchange et seront recherchés. Les fichiers chiffrés avec les technologies autres que Microsoft sont renvoyés comme impossibles à rechercher.

  - Les messages électroniques chiffrés avec S/MIME ne sont pas indexés et sont considérés comme des éléments impossibles à rechercher. Il s’agit des messages chiffrés avec ou sans pièces jointes.

  - Les messages protégés par la Gestion des droits relatifs à l’information (IRM) sont indexés par le service de recherche Exchange et donc inclus dans les résultats de la recherche s’ils correspondent aux paramètres de requête. Pour plus d’informations sur la Gestion des droits relatifs à l’information, voir [Gestion des droits relatifs à l’information](information-rights-management-exchange-2013-help.md).

  - Comme indiqué précédemment, en raison de l’indexation des propriétés et des métadonnées de message, une recherche par mot clé peut renvoyer des résultats si ce mot clé apparaît dans les métadonnées indexées. Cependant, cette même recherche par mot clé peut ne pas renvoyer le même élément si le mot clé apparaît uniquement dans le contenu d’un élément joint dont le type de fichier n’est pas pris en charge. Dans ce cas, l’élément sera renvoyé uniquement en tant qu’élément impossible à rechercher.

  - La découverte électronique dans Exchange 2010 utilise le concept de *liste fiable*. Il s’agit de types de fichier dont le contenu ne peut pas être recherché et qui ne sont donc pas indexés par la recherche Exchange ; par exemple les fichiers vidéo Windows Media (.wmv) et audio Waveform (.wav). Puisqu’ils ne comportent pas de contenu pouvant être recherché, ces types de fichiers ne sont pas considérés comme des éléments impossibles à rechercher dans Exchange 2010. Les éléments de boîte aux lettres contenant ces types de fichiers ne sont pas renvoyés en tant qu’éléments impossibles à rechercher et ne sont pas copiés dans une boîte aux lettres de découverte.
    
    La liste fiable n’existe plus dans Exchange 2013 ni dans Exchange Online. Les types de fichier sont activés ou désactivés pour l’indexation, ou ne sont pas pris en charge. Les types de fichier non pris en charge et désactivés sont considérés comme des éléments impossibles à rechercher.

