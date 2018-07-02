---
title: 'Application des règles DLP pour évaluer les messages: Exchange 2013 Help'
TOCTitle: Application des règles DLP pour évaluer les messages
ms:assetid: 1ac77020-26ff-410c-ab09-4f28a99d67a1
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dn329050(v=EXCHG.150)
ms:contentKeyID: 56269223
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Application des règles DLP pour évaluer les messages

 

_**Sapplique à :**Exchange Online, Exchange Server 2013_

_**Dernière rubrique modifiée :**2015-03-09_

Vous pouvez configurer des règles d’informations sensibles au sein de vos stratégies de protection contre la perte de données (DLP) Microsoft Exchange afin de détecter des données très spécifiques dans les messages électroniques. Cette rubrique vous permettra de comprendre comment ces règles sont appliquées et comment les messages sont évalués. Vous pouvez éviter les interruptions de flux de travail pour les utilisateurs de la messagerie et atteindre un haut degré de précision dans les détections DLP si vous savez comment vos règles sont appliquées. Nous allons utiliser la règle relative aux informations de carte de crédit fournie par Microsoft comme exemple. Lorsque vous activez une règle de transport ou une stratégie DLP, l’agent des règles de transport Exchange compare tous les messages que les utilisateurs envoient aux ensembles de règles que vous créez.

## Préciser les besoins

Supposons que vous devez agir sur les informations de carte de crédit dans les messages. Les actions à entreprendre une fois ces informations trouvées ne figurent pas dans cette rubrique, mais vous pouvez en savoir plus à ce sujet dans [Courrier des actions de règle de flux dans Exchange en ligne](https://technet.microsoft.com/fr-fr/library/jj919237\(v=exchg.150\)). Vous devez vous assurer avec un maximum de certitude que les éléments détectés dans un message sont de véritables données de carte de crédit et non l’utilisation légitime de groupes de chiffres qui ressemblent à des données de carte de crédit (par exemple, un code de réservation ou un numéro d’immatriculation). Pour cela, nous allons établir clairement que les informations suivantes doivent être considérées comme celles d’une carte de crédit.

**    Margie’s Travel,  
    J’ai reçu des informations de carte de crédit mises à jour pour Christian.  
    Christian Lacombe  
    Visa : 4111 1111 1111 1111  
    Expire fin : 2/2012  
    Veuillez mettre à jour son profil de voyage.**

Déterminons aussi clairement que les informations suivantes ne doivent pas être considérées comme celles d’une carte de crédit.

**    Bonjour Alexandre,  
    J’espère également être à Hawaii. Mon code de réservation est 1234 1234 1234 1234 et je serai là en mars 2012.  
    Cordialement, Camille**

L’extrait de code XML suivant montre comment les besoins exprimés plus haut sont actuellement définis dans une règle relative aux informations sensibles qui est fournie avec Exchange et incorporée dans l’un des modèles de stratégie DLP indiqués.

    <Entity id="50842eb7-edc8-4019-85dd-5a5c1f2bb085" patternsProximity="300" recommendedConfidence="85">
          <Pattern confidenceLevel="85">
            <IdMatch idRef="Func_credit_card" />
            <Any minMatches="1">
              <Match idRef="Keyword_cc_verification" />
              <Match idRef="Keyword_cc_name" />
              <Match idRef="Func_expiration_date" />
            </Any>
          </Pattern>
        </Entity>

## Critères spéciaux dans votre solution

La définition de règle XML indiquée précédemment comprend des critères spéciaux. Cela accroît la probabilité que la règle détecte uniquement les informations importantes et non des informations vaguement associées. Pour plus d’informations sur le schéma XML pour les règles et les modèles DLP, voir [Définition de vos modèles DLP et types d'informations](define-your-own-dlp-templates-and-information-types-exchange-2013-help.md).

La règle de carte de crédit comporte une section de code XML pour des modèles, qui inclut un identificateur de correspondance principale, ainsi que des preuves corroborantes supplémentaires. Ces trois exigences sont expliquées ici :

1.  `<IdMatch idRef="Func_credit_card" />  ` : cela nécessite la correspondance d’une carte de crédit de fonction personnelle, qui est définie en interne. Cette fonction comprend les validations suivantes :
    
    1.  Elle correspond à une expression régulière (dans ce cas, pour 16 chiffres) qui peut également inclure des variantes, comme un espace séparateur, pour correspondre également à **4111 1111 1111 1111** ou un trait d’union séparateur pour correspondre aussi à **4111-1111-1111-1111**.
    
    2.  Elle évalue l’algorithme de somme de contrôle de Lhun par rapport au nombre à 16 chiffres, afin de garantir avec un maximum de certitude qu’il s’agit d’un numéro de carte de crédit.
    
    3.  Elle exige une correspondance obligatoire, après quoi la preuve corroborante est évaluée.

2.  `<Any minMatches="1">  ` : cette section indique que la présence d’au moins un des éléments suivants de la preuve est obligatoire.

3.  La preuve corroborante peut résider dans la correspondance de l’une de ces trois fonctions :
    
    `<Match idRef="Keyword_cc_verification" />`
    
    `<Match idRef="Keyword_cc_name" />`
    
    `<Match idRef="Func_expiration_date" />`
    
    Ces trois éléments indiquent simplement le caractère obligatoire d’une liste de mots clés pour les cartes de crédit, du nom des cartes de crédit ou d’une date d’expiration. La date d’expiration est définie et évaluée en interne comme une autre fonction.

## Processus d’évaluation du contenu par rapport aux règles

Ces cinq étapes représentent les actions que Exchange effectue pour comparer votre règle aux messages électroniques. Dans notre exemple de règle de carte de crédit, les étapes réalisées sont les suivantes.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Étape</th>
<th>Action</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>1. Obtention du contenu</p></td>
<td><p>Christian Lacombe</p>
<p>Visa : 4111 1111 1111 1111</p>
<p>Expire fin : 2/2012</p></td>
</tr>
<tr class="even">
<td><p>2. Analyse d’expressions régulières</p></td>
<td><p>4111 1111 1111 1111 -&gt; un nombre de 16 chiffres est détecté</p></td>
</tr>
<tr class="odd">
<td><p>3. Analyse de fonctions</p></td>
<td><ul>
<li><p>4111 1111 1111 1111 -&gt; correspond à la somme de contrôle</p></li>
<li><p>1234 1234 1234 1234 -&gt; ne correspond pas</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>4. Éléments de preuve supplémentaires</p></td>
<td><ol>
<li><p>Le mot clé Visa est proche des chiffres.</p></li>
<li><p>Une expression régulière pour une date (2/2012) est proche des chiffres.</p></li>
</ol></td>
</tr>
<tr class="odd">
<td><p>5. Verdict</p></td>
<td><ol>
<li><p>Il existe une expression régulière qui correspond à une somme de contrôle.</p></li>
<li><p>Les éléments de preuve supplémentaires augmentent le niveau de confiance.</p></li>
</ol>
<p></p></td>
</tr>
</tbody>
</table>


La façon dont cette règle est configurée par Microsoft oblige les preuves corroborantes (comme les mots clés) à faire partie du contenu du message électronique afin de correspondre à la règle. Ainsi, le message électronique suivant ne serait pas détecté comme contenant des informations de carte de crédit :

**    Margie’s Travel,  
    J’ai reçu des informations mises à jour pour Christian.  
    Christian Lacombe  
    4111 1111 1111 1111  
    Veuillez mettre à jour son profil de voyage**.

Vous pouvez utiliser une règle personnalisée qui définit un modèle sans preuve supplémentaire, comme le montre l’exemple suivant. Cela permet de détecter les messages contenant uniquement le numéro de carte de crédit et aucune preuve corroborante.

``` 
      <Pattern confidenceLevel="85">
         <IdMatch idRef="Func_credit_card" />
      </Pattern>
    </Entity>
```

L’exemple de cartes de crédit dans le présent article peut également être étendu à d’autres règles relatives aux informations sensibles. Pour visualiser la liste complète des règles fournies par Microsoft dans Exchange, utilisez la cmdlet [Get-ClassificationRuleCollection](https://technet.microsoft.com/fr-fr/library/jj218696\(v=exchg.150\)) dans l’environnement de ligne de commande Exchange Management Shell de la manière suivante :

    $rule_collection = Get-ClassificationRuleCollection

    $rule_collection[0].SerializedClassificationRuleCollection | Set-Content oob_classifications.xml -Encoding byte

## Pour plus d’informations

[Protection contre la perte de données](technical-overview-of-dlp-data-loss-prevention-in-exchange.md)

[Règles de flux de messagerie (règles de transport) dans Exchange Online](https://technet.microsoft.com/fr-fr/library/jj919238\(v=exchg.150\))

[Utilisation de PowerShell avec Exchange 2013 (Exchange Management Shell)](https://technet.microsoft.com/fr-fr/library/bb123778\(v=exchg.150\))

[Exchange Online PowerShell](https://technet.microsoft.com/fr-fr/library/jj200677\(v=exchg.150\))

