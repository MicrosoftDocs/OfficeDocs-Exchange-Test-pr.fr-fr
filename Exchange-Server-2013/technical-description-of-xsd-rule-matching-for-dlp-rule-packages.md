---
title: 'Méthodes et techniques de mise en correspondance pour les packages de règles: Exchange 2013 Help'
TOCTitle: Méthodes et techniques de mise en correspondance pour les packages de règles
ms:assetid: 09fe9278-d077-452c-b7e5-729b3dc70b1b
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ674702(v=EXCHG.150)
ms:contentKeyID: 50477482
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Méthodes et techniques de mise en correspondance pour les packages de règles

 

_**Sapplique à :** Exchange Online, Exchange Server 2013_

_**Dernière rubrique modifiée :** 2016-07-28_

Cette rubrique décrit les techniques permettant de faire correspondre les éléments Pattern et Evidence dans un fichier XML de protection contre la pertes de données (DLP, Data Loss Prevention) destiné à accueillir votre package de règles de types d'informations sensibles. Vous devez d'abord créer un fichier XML bien formé, puis l'importer en utilisant le Centre d'administration Exchange (CAE) ou l'environnement de ligne de commande Exchange Management Shell qui vous aideront à créer votre solution DLP Microsoft Exchange Server 2013. Vous devez disposer d'un fichier XML DLP avant d'utiliser les méthodes de correspondance décrites ci-dessous. Pour plus d'informations sur la définition de vos modèles DLP et fichiers XML, consultez la rubrique [Définition de vos modèles DLP et types d'informations](define-your-own-dlp-templates-and-information-types-exchange-2013-help.md).

## Élément Match

L'élément `Match` est utilisé dans les éléments `Pattern` et `Evidence` pour représenter le mot clé, l'expression régulière (regex) ou la fonction sous-jacent(e) à mettre en correspondance. La définition de la correspondance même est stockée à l'extérieur de l'élément `Rule` et est référencée via l'attribut obligatoire `idRef`. Vous pouvez inclure plusieurs éléments `Match` dans une définition Pattern. Ils peuvent être inclus directement dans l'élément `Pattern` ou combinés à l'aide de l'élément `Any` pour définir des sémantiques de correspondance.

    <?xml version="1.0" encoding="utf-8"?>
    <Rules packageId="...">
            ...
    <Entity id="...">
      <Pattern confidenceLevel="85">
                 <IdMatch idRef="FormattedSSN" />
                 <Match idRef="USDate" />
                 <Match idRef="USAddress" />
      </Pattern>
    </Entity>
            ...
             <Keyword id="FormattedSSN "> ... </Keyword>
             <Regex id=" USDate "> ... </Regex>
             <Regex id="USAddress"> ... </Regex>
            ...
    
    </Rules>

## Définition de correspondances basées sur des mots clés

Il est fréquent d'utiliser une règle de correspondance basée sur des expressions de chaîne de mots clés réservés. Pour cela, vous devez utiliser l'élément `Keyword`. L'élément Keyword a un attribut « id » qui sert de référence dans les règles Entity ou Affinity correspondantes. Un élément Keyword peut être référencé dans plusieurs règles Entity et Affinity.

La mise en correspondance peut être effectué en utilisant une correspondance exacte ou les algorithmes de correspondance en fonction de word. Correspondance exacte utilise un algorithme qui respecte la casse qui recherche du texte dans la langue spécifiée. Correspondance de mot applique un algorithme de correspondance basé sur des limites de word. Les termes à mettre en correspondance peuvent être incluses inline dans la définition du mot clé à l’aide de l’élément sous-fonctionnalités de termes.

<table>
<thead>
<tr class="header">
<th><img src="images/Bb125224.tip(EXCHG.150).gif" title="Conseil" alt="Conseil" />Conseil :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Utilisez le style de correspondance à constante au lieu de la correspondance regex pour augmenter l'efficacité et les performances. Utilisez la correspondance regex uniquement dans le cas où les correspondances à constante sont insuffisantes et où les expressions régulières exigent de la souplesse.</td>
</tr>
</tbody>
</table>


    <Keyword id="Word_Example">
        <Group matchStyle="word">
           <Term>card verification</Term>
           <Term>cvn</Term>
           <Term>cid</Term>
           <Term>cvc2</Term>
           <Term>cvv2</Term>
           <Term>pin block</Term>
           <Term>security code</Term>
        </Group>
    </Keyword>
    ...
    <Keyword id="String_Example">
        <Group matchStyle="string">
           <Term>card</Term>
           <Term>pin</Term>
           <Term>security</Term>
        </Group>
    </Keyword>

## Définition de correspondances basées sur des expressions régulières

La méthode de correspondance basée sur des expressions régulières est elle aussi couramment utilisée. En raison de sa souplesse d’utilisation, la correspondance basée sur des expressions régulières sert souvent à appliquer des correspondances pour des données telles que des numéros de permis de conduire ou des adresses. Les modèles d'expression régulière sont définis à l'aide d'une syntaxe d'expression régulière courante. Le tableau suivant propose des exemples de certains des jetons d'expression régulière les plus courants actuellement disponibles.

<table>
<thead>
<tr class="header">
<th><img src="images/Bb125224.tip(EXCHG.150).gif" title="Conseil" alt="Conseil" />Conseil :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Utilisez le style de correspondance à constante au lieu de la correspondance regex pour augmenter l'efficacité. Utilisez la correspondance regex uniquement dans le cas où les correspondances à constante sont insuffisantes et où les expressions régulières exigent de la souplesse.</td>
</tr>
</tbody>
</table>



<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Symbole</th>
<th>Signification</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>c</p></td>
<td><p>Correspond une fois au caractère littéral c, sauf s'il s'agit d'un caractère spécial.</p></td>
</tr>
<tr class="even">
<td><p>^</p></td>
<td><p>Correspond au début d'une ligne.</p></td>
</tr>
<tr class="odd">
<td><p>.</p></td>
<td><p>Correspond à tout caractère qui n'est pas une nouvelle ligne.</p></td>
</tr>
<tr class="even">
<td><p>$</p></td>
<td><p>Correspond à la fin d'une ligne.</p></td>
</tr>
<tr class="odd">
<td><p>|</p></td>
<td><p>OU logique entre des expressions.</p></td>
</tr>
<tr class="even">
<td><p>()</p></td>
<td><p>Regroupe des sous-expressions.</p></td>
</tr>
<tr class="odd">
<td><p>[]</p></td>
<td><p>Définit une classe de caractères.</p></td>
</tr>
<tr class="even">
<td><p>*</p></td>
<td><p>Correspond à l'expression qui précède zéro ou plusieurs fois.</p></td>
</tr>
<tr class="odd">
<td><p>+</p></td>
<td><p>Correspond à l'expression qui précède une ou plusieurs fois.</p></td>
</tr>
<tr class="even">
<td><p>?</p></td>
<td><p>Correspond à l'expression qui précède zéro ou une fois.</p></td>
</tr>
<tr class="odd">
<td><p>{<em>n</em>}</p></td>
<td><p>Correspond à l'expression précédente <em>n</em> fois.</p></td>
</tr>
<tr class="even">
<td><p>{<em>n,</em>}</p></td>
<td><p>Correspond à l'expression précédente au moins <em>n</em> fois.</p></td>
</tr>
<tr class="odd">
<td><p>{<em>n, m</em>}</p></td>
<td><p>Correspond à l'expression précédente au moins <em>n</em> fois et au plus <em>m</em> fois.</p></td>
</tr>
<tr class="even">
<td><p>\d</p></td>
<td><p>Correspond à un chiffre.</p></td>
</tr>
<tr class="odd">
<td><p>\D</p></td>
<td><p>Correspond à un caractère qui n'est pas un chiffre.</p></td>
</tr>
<tr class="even">
<td><p>\w</p></td>
<td><p>Correspond à un caractère alphabétique, y compris le trait de soulignement.</p></td>
</tr>
<tr class="odd">
<td><p>\W</p></td>
<td><p>Correspond à un caractère qui n'est pas un caractère alphabétique.</p></td>
</tr>
<tr class="even">
<td><p>\s</p></td>
<td><p>Correspond à un espace (\t, \n, \r ou \f).</p></td>
</tr>
<tr class="odd">
<td><p>\S</p></td>
<td><p>Correspond à un caractère autre qu'un espace.</p></td>
</tr>
<tr class="even">
<td><p>\t</p></td>
<td><p>Tabulation.</p></td>
</tr>
<tr class="odd">
<td><p>\n</p></td>
<td><p>Nouvelle ligne.</p></td>
</tr>
<tr class="even">
<td><p>\r</p></td>
<td><p>Retour chariot.</p></td>
</tr>
<tr class="odd">
<td><p>\f</p></td>
<td><p>Saut de page.</p></td>
</tr>
<tr class="even">
<td><p>\<em>m</em></p></td>
<td><p>Échappement <em>m</em>, où <em>m</em> est l'un des métacaractères décrits ci-dessus : ^, ., $, |, (), [], *, +, ?, \ ou /.</p></td>
</tr>
</tbody>
</table>


L'élément Regex a un attribut « id » qui sert de référence dans les règles Entity ou Affinity correspondantes. Un élément Regex peut être référencé dans plusieurs règles Entity et Affinity. L'expression Regex est définie comme la valeur de l'élément Regex.

    <Regex id="CCRegex">
         \bcc\#\s|\bcc\#\:\s
    </Regex>
    ...
    <Regex id="ItinFormatted">
        (?:^|[\s\,\:])(?:9\d{2})[- ](?:[78]\d[-       ]\d{4})(?:$|[\s\,]|\.\s)
    </Regex>
    ...
    <Regex id="NorthCarolinaDriversLicenseNumber">
        (^|\s|\:)(\d{1,8})($|\s|\.\s)
    </Regex>

## Combinaison de plusieurs éléments de correspondance

Pour augmenter la confiance de correspondance, il est courant de définir une sémantique entre plusieurs éléments Match, par exemple pour qu'une ou plusieurs correspondances se produisent. L'élément Any permet de définir la logique entre plusieurs correspondances. Il peut être utilisé comme sous-élément dans l'élément Pattern. Il contient un ou plusieurs éléments Match enfants et définit la logique entre les correspondances. Vous trouverez ci-dessous des exemples de code XML concernant les éléments Any quand la correspondance porte sur tous les éléments, sur aucun élément (logique « not ») et sur un nombre exact d'éléments.

L'attribut facultatif minMatches (valeur par défaut = 1) permet de définir le nombre minimum d'éléments Match à respecter pour garantir une correspondance. De même, l'attribut facultatif maxMatches (valeur par défaut = nombre d'éléments Match enfants) permet de définir le nombre maximum d'éléments Match à respecter pour garantir une correspondance. Ces conditions sont combinées à l'aide d'opérateurs logiques basés sur l'utilisation des attributs minMatches et maxMatches. Les sémantiques suivantes sont possibles :

  - Correspondance à tous les enfants Match enfants
    
    Aucune correspondance avec les éléments Match enfants
    
    Correspondance avec un sous-ensemble exact d'éléments Match enfants

<!-- end list -->

    <Any minMatches="3" maxMatches="3">
        <Match idRef="USDate" />
        <Match idRef="USAddress" />
        <Match idRef="Name" />
    </Any>

    <Any maxMatches="0">
        <Match idRef="USDate" />
        <Match idRef="USAddress" />
        <Match idRef="Name" />
    </Any>

    <Any minMatches="1" maxMatches="1">
        <Match idRef="USDate" />
        <Match idRef="USAddress" />
        <Match idRef="Name" />
    </Any>

## Augmentation du niveau de confiance avec davantage de preuves

Pour les règles basées sur des entités, il est également possible d'augmenter le niveau de confiance en définissant plusieurs éléments Pattern, chacun avec un nombre croissant de preuves corroborantes. À cette fin, utilisez les attributs minMatches et maxMatches pour l'élément Any afin de créer des modèles indépendants dont le niveau de confiance augmente avec le nombre de preuves corroborantes. Par exemple :

  - si un élément de preuve corroborante est trouvé : le niveau de confiance est de 65 %

  - si deux éléments sont trouvés : le niveau de confiance est de 75%

  - si trois éléments sont trouvés : le niveau de confiance est de 85%

<!-- end list -->

    <Entity id="..." patternsProximity="300" >
        <Pattern confidenceLevel="65">
            <IdMatch idRef="UnformattedSSN" />
            <Any maxMatches="1">
                <Match idRef="USDate" />
                <Match idRef="USAddress" />
                <Match idRef="Name" />
            </Any>
        </Pattern>
        <Pattern confidenceLevel="75">
            <IdMatch idRef="UnformattedSSN" />
            <Any minMatches="2" maxMatches="2">
                <Match idRef="USDate" />
                <Match idRef="USAddress" />
                <Match idRef="Name" />
            </Any>
        </Pattern>
        <Pattern confidenceLevel="85">
            <IdMatch idRef="UnformattedSSN" />
            <Any minMatches="3">
                <Match idRef="USDate" />
                <Match idRef="USAddress" />
                <Match idRef="Name" />
            </Any>
        </Pattern>
    </Entity>

## Exemple : Règle de sécurité sociale aux États-Unis

Cette section commence par une description indiquant comment créer une règle de correspondance d'un numéro de sécurité sociale aux États-Unis. Commencez par décrire comment identifier le contenu qui renferme le numéro de sécurité sociale. Un numéro de sécurité sociale est trouvé si :

1.  Regex correspond à un numéro de sécurité sociale (SSN) mis en forme (et compris dans la plage SSN valide)

2.  Preuve corroborante   l'une des conditions suivantes doit se produire à proximité :
    
    1.  Correspondance de mot clé {Social Security, Soc Sec, SSN, SSNS, SSN\#, SS\#, SSID}
    
    2.  Texte représentant une adresse aux États-Unis
    
    3.  Texte représentant une date
    
    4.  Texte représentant un nom

Ensuite, convertissez la description en représentation de schéma de règle, comme suit :

    <Entity id="a44669fe-0d48-453d-a9b1-2cc83f2cba77"
             patternsProximity="300" RecommendedConfidence="85">
        <Pattern confidenceLevel="85">
          <IdMatch idRef="FormattedSSN" />
          <Any minMatches="1">
              <Match idRef="SSNKeywords" />
              <Match idRef="USDate" />
              <Match idRef="USAddress" />
              <Match idRef="Name" />
          </Any>
        </Pattern>
    </Entity>

## Pour plus d'informations

[Protection contre la perte de données](technical-overview-of-dlp-data-loss-prevention-in-exchange.md)

[Définition de vos modèles DLP et types d'informations](define-your-own-dlp-templates-and-information-types-exchange-2013-help.md)

[Importer un modèle de stratégie DLP personnalisé à partir d’un fichier](import-a-custom-dlp-policy-template-from-a-file-exchange-2013-help.md)

