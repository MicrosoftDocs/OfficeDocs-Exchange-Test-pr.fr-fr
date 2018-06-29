---
title: 'Personnaliser les types d’informations sensibles DLP intégrées: Exchange 2013 Help'
TOCTitle: Personnaliser les types d’informations sensibles DLP intégrées
ms:assetid: 3f8bf141-2e7c-4ea7-b102-dfd6c41539da
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dn781122(v=EXCHG.150)
ms:contentKeyID: 62757561
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Personnaliser les types d’informations sensibles DLP intégrées

 

_**Sapplique à :**Exchange Online, Exchange Server 2013_

_**Dernière rubrique modifiée :**2016-05-26_

Lorsque vous recherchez des informations sensibles dans un courrier électronique, vous devez décrire ces informations dans ce que l’on appelle une *règle*. La protection contre la perte de données (DLP) comprend un pack de 51 règles pour les types d’informations sensibles les plus courants que vous pouvez utiliser immédiatement. Pour utiliser ces règles, vous devez les inclure dans une stratégie. Vous voudrez peut-être ajuster ces règles intégrées pour répondre aux besoins spécifiques de votre organisation, et vous pouvez le faire en créant un type d’informations sensibles personnalisé. Cette rubrique vous montre comment personnaliser le fichier XML qui contient la collection de règles existante pour détecter un plus large éventail d’informations potentielles relatives aux cartes de crédit.

Vous pouvez prendre cet exemple et l’appliquer à d’autres types d’informations sensibles intégrés. Pour obtenir la liste des types d’informations sensibles par défaut et des définitions XML, voir la rubrique [Éléments recherchés par les types d’informations sensibles dans Exchange](what-the-sensitive-information-types-in-exchange-look-for-exchange-online-help.md).

Cette rubrique vous guide à travers les sections suivantes pour les personnalisations de règle XML :

  - Exporter le fichier XML des règles actuelles

  - Rechercher la règle à modifier dans le fichier XML

  - Modifier le XML et créer un type d’informations sensibles

  - Supprimer l’exigence de preuve crédible d’un type d’informations sensibles

  - Rechercher des mots clés propres à votre organisation

  - Télécharger votre règle

Pour savoir en quoi consistent les différentes parties des règles et ce qu’elles font, voir Glossaire terminologique à la fin de cette rubrique.

## Exporter le fichier XML des règles actuelles

Pour exporter le fichier XML, vous devez utiliser Environnement de ligne de commande Exchange Management Shell ou . Pour Exchange Server 2013, consultez la rubrique [Utilisation de PowerShell avec Exchange 2013 (Exchange Management Shell)](https://technet.microsoft.com/fr-fr/library/bb123778\(v=exchg.150\)). Pour Exchange Online, consultez la rubrique [Connexion à Exchange Online à l'aide de Remote PowerShell](https://technet.microsoft.com/fr-fr/library/jj984289\(v=exchg.150\)).

1.  Dans Environnement de ligne de commande Exchange Management Shell ou Exchange Online PowerShell, saisissez **Get-ClassificationRuleCollection** pour afficher les règles de votre organisation à l’écran. Si vous n’avez pas créé votre propre règle, vous ne verrez que les règles intégrées par défaut, sous le libellé « Package de règles Microsoft ».

2.  Stockez les règles de votre organisation dans une variable en saisissant **$ruleCollections = Get-ClassificationRuleCollection**. Le stockage d’un élément dans une variable le rend facilement disponible ultérieurement dans un format adapté aux commandes PowerShell distantes.

3.  Créez un fichier au format XML contenant toutes les données en saisissant **Set-Content -path "C:\\custompath\\exportedRules.xml" -Encoding Byte -Value $ruleCollections.SerializedClassificationRuleCollection**. (**Set-content** est la partie de la cmdlet qui écrit le XML dans le fichier.)
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ159813.important(EXCHG.150).gif" title="Important" alt="Important" />Important :</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Assurez-vous que vous utilisez l’emplacement de fichier dans lequel votre pack de règles est effectivement stocké. <strong>C:\custompath\</strong> est un espace réservé.</td>
    </tr>
    </tbody>
    </table>


## Rechercher la règle à modifier dans le fichier XML

Les cmdlets ci-dessus ont exporté l’ensemble de la *collection de règles*, ce qui inclut les 51 règles par défaut que nous fournissons. Ensuite, vous devez rechercher la règle de numéro de carte de crédit spécifique à modifier.

1.  Utilisez un éditeur de texte pour ouvrir le fichier XML que vous avez exporté dans la section précédente.

2.  Faites défiler l’écran jusqu’à la balise **\<Rules\>**, qui constitue le début de la section qui contient les règles DLP. (Étant donné que ce fichier XML contient les informations de toute la collection de règles, il contient d’autres informations dans la partie supérieure que vous avez besoin de faire défiler pour parvenir aux règles.)

3.  Recherchez **Func\_credit\_card** pour trouver la définition de règle de numéro de carte de crédit. (Dans le langage XML, les noms des règles ne peuvent pas contenir d’espaces, qui sont donc généralement remplacés par des traits de soulignement, et les noms des règles sont parfois abrégés. Par exemple, la règle de numéro de sécurité sociale des États-Unis est abrégée par « SSN ». Le XML de la règle de numéro de carte de crédit doit ressembler à l’exemple de code suivant.
    
        <Entity id="50842eb7-edc8-4019-85dd-5a5c1f2bb085"
               patternsProximity="300" recommendedConfidence="85">
              <Pattern confidenceLevel="85">
               <IdMatch idRef="Func_credit_card" />
                <Any minMatches="1">
                  <Match idRef="Keyword_cc_verification" />
                  <Match idRef="Keyword_cc_name" />
                  <Match idRef="Func_expiration_date" />
                </Any>
              </Pattern>
            </Entity>

Maintenant que vous avez localisé la définition de règle de numéro de carte de crédit dans le XML, vous pouvez personnaliser le XML de la règle pour répondre à vos besoins. (Pour un rappel sur les définitions XML, voir Glossaire terminologique à la fin de cette rubrique.)

## Modifier le XML et créer un type d’informations sensibles

Tout d’abord, vous devez créer un type d’informations sensibles, car vous ne pouvez pas modifier directement les règles par défaut. Vous pouvez effectuer de nombreuses actions avec les types d’informations sensibles personnalisés, comme l’illustre la section [Développement de packages de règles des informations sensibles](technical-description-of-xml-schema-for-dlp-rule-packages.md). Pour cet exemple, nous allons rester simples et nous contenter de supprimer les preuves crédibles et d’ajouter des mots clés à la règle de numéro de carte de crédit.

Toutes les définitions de règle XML sont construites sur le modèle général suivant. Vous devez copier et coller le XML de définition de numéro de carte de crédit dans le modèle, modifier certaines valeurs (remarquez les espaces réservés « . . .” dans l’exemple suivant), puis télécharger le XML modifié en tant que nouvelle règle pouvant être utilisée dans des stratégies.

    <?xml version="1.0" encoding="utf-16"?>
    <RulePackage xmlns="http://schemas.microsoft.com/office/2011/mce">
      <RulePack id=". . .">
        <Version major="1" minor="0" build="0" revision="0" />
        <Publisher id=". . ." /> 
        <Details defaultLangCode=". . .">
          <LocalizedDetails langcode=" . . . ">
             <PublisherName>. . .</PublisherName>
             <Name>. . .</Name>
             <Description>. . .</Description>
          </LocalizedDetails>
        </Details>
      </RulePack>
      
     <Rules>
       <!-- Paste the Credit Card Number rule definition here.--> 
    
          <LocalizedStrings>
             <Resource idRef=". . .">
               <Name default="true" langcode=" . . . ">. . .</Name>
               <Description default="true" langcode=". . ."> . . .</Description>
             </Resource>
          </LocalizedStrings>
    
       </Rules>
    </RulePackage>

Vous obtenez maintenant quelque chose qui ressemble au XML suivant. Étant donné que les packages de règles et les règles sont identifiés par leur GUID unique, vous devez générer deux GUID : un pour le package de règles et un pour remplacer le GUID de la règle de numéro de carte de crédit. (Le GUID pour l’ID d’entité dans l’exemple de code suivant est celui de la définition de notre règle intégrée, que vous devez remplacer.) Il existe plusieurs façons de générer des GUID, mais vous pouvez le faire facilement dans PowerShell en saisissant **\[guid\]::NewGuid()**.

    <?xml version="1.0" encoding="utf-16"?>
    <RulePackage xmlns="http://schemas.microsoft.com/office/2011/mce">
      <RulePack id="8aac8390-e99f-4487-8d16-7f0cdee8defc">
        <Version major="1" minor="0" build="0" revision="0" />
        <Publisher id="8d34806e-cd65-4178-ba0e-5d7d712e5b66" />
        <Details defaultLangCode="en">
          <LocalizedDetails langcode="en">
            <PublisherName>Contoso Ltd.</PublisherName>
            <Name>Financial Information</Name>
            <Description>Modified versions of the Microsoft rule package</Description>
          </LocalizedDetails>
        </Details>
      </RulePack>
      
     <Rules>
        <Entity id="db80b3da-0056-436e-b0ca-1f4cf7080d1f"
           patternsProximity="300" recommendedConfidence="85">
          <Pattern confidenceLevel="85">
            <IdMatch idRef="Func_credit_card" />
            <Any minMatches="1">
              <Match idRef="Keyword_cc_verification" />
              <Match idRef="Keyword_cc_name" />
              <Match idRef="Func_expiration_date" />
            </Any>
          </Pattern>
        </Entity>
    
          <LocalizedStrings>
             <Resource idRef="db80b3da-0056-436e-b0ca-1f4cf7080d1f"> 
    <!-- This is the GUID for the preceding Credit Card Number entity because the following text is for that Entity. -->
               <Name default="true" langcode="en-us">Modified Credit Card Number</Name>
               <Description default="true" langcode="en-us">Credit Card Number that looks for additional keywords, and another version of Credit Card Number that doesn't require keywords (but has a lower confidence level)</Description>
             </Resource>
          </LocalizedStrings>
    
       </Rules>
    </RulePackage>

## Supprimer l’exigence de preuve crédible d’un type d’informations sensibles

Maintenant que vous disposez d’un nouveau type d’informations sensibles que vous pouvez télécharger vers votre environnement Exchange, la prochaine étape consiste à rendre la règle plus spécifique. Modifiez la règle de sorte qu’elle recherche uniquement un nombre à 16 chiffres qui passe la somme de contrôle, mais qu’elle ne nécessite pas de preuve (crédible) supplémentaire (par exemple, des mots clés). Pour ce faire, vous devez retirer la partie du XML qui recherche la preuve crédible. La preuve crédible est très utile pour réduire les faux positifs car généralement, il existe certains mots clés ou une date d’expiration près du numéro de carte de crédit. Si vous supprimez cette preuve, vous devez également ajuster votre probabilité de trouver un numéro de carte de crédit en abaissant le paramètre **confidenceLevel**, qui est défini sur 85 dans l’exemple.

    <Entity id="db80b3da-0056-436e-b0ca-1f4cf7080d1f" patternsProximity="300"
          <Pattern confidenceLevel="85">
            <IdMatch idRef="Func_credit_card" />
          </Pattern>
        </Entity>

## Rechercher des mots clés propres à votre organisation

Vous voulez peut-être exiger des preuves crédibles, mais aussi des mots clés différents ou supplémentaires, et vous voulez aussi peut-être modifier l’endroit où rechercher ces preuves. Vous pouvez ajuster le paramètre **patternsProximity** afin de développer ou réduire la fenêtre pour la preuve probante autour du numéro à 16 chiffres. Pour ajouter vos propres mots clés, vous devez définir une liste de mots clés et la référencer dans votre règle. Le XML suivant ajoute les mots clés « company card » et « Contoso card » de sorte que tous les messages qui contiennent ces expressions au sein des 150 caractères d’un numéro de carte de crédit soient identifiés comme des numéros de carte de crédit.

    <Rules>
    <! -- Modify the patternsProximity to be "150" rather than "300." -->
        <Entity id="db80b3da-0056-436e-b0ca-1f4cf7080d1f" patternsProximity="150" recommendedConfidence="85">
          <Pattern confidenceLevel="85">
            <IdMatch idRef="Func_credit_card" />
            <Any minMatches="1">
              <Match idRef="Keyword_cc_verification" />
              <Match idRef="Keyword_cc_name" />
    <!-- Add the following XML, which references the keywords at the end of the XML sample. -->
              <Match idRef="My_Additional_Keywords" />
              <Match idRef="Func_expiration_date" />
            </Any>
          </Pattern>
        </Entity>
    <!-- Add the following XML, and update the information inside the <Term> tags with the keywords that you want to detect. -->
        <Keyword id="My_Additional_Keywords">
          <Group matchStyle="word">
            <Term caseSensitive="false">company card</Term>
            <Term caseSensitive="false">Contoso card</Term>
          </Group>
        </Keyword>

## Télécharger votre règle

Pour télécharger votre règle, vous devez procéder comme suit.

1.  Enregistrez-la en tant que fichier .xml avec le codage Unicode. Ceci est important car la règle ne fonctionne pas si le fichier est enregistré dans un codage différent.

2.  Connectez-vous à Environnement de ligne de commande Exchange Management Shell ou Exchange Online PowerShell. Pour Exchange Server 2013, consultez la rubrique [Utilisation de PowerShell avec Exchange 2013 (Exchange Management Shell)](https://technet.microsoft.com/fr-fr/library/bb123778\(v=exchg.150\)). Pour Exchange Online, consultez la rubrique [Connexion à Exchange Online à l'aide de Remote PowerShell](https://technet.microsoft.com/fr-fr/library/jj984289\(v=exchg.150\)).

3.  Dans Environnement de ligne de commande Exchange Management Shell ou Exchange Online PowerShell, saisissez **New-ClassificationRuleCollection -FileData (Get-Content -Path "C:\\custompath\\MyNewRulePack.xml " -Encoding Byte)**.
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ159813.important(EXCHG.150).gif" title="Important" alt="Important" />Important :</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Assurez-vous que vous utilisez l’emplacement de fichier dans lequel votre pack de règles est effectivement stocké. <strong>C:\custompath\</strong> est un espace réservé.</td>
    </tr>
    </tbody>
    </table>


4.  Pour confirmer, saisissez **Y**, puis appuyez sur **Entrée**.

5.  Vérifiez que votre nouvelle règle a été téléchargée en saisissant **Get-DataClassification**, qui affiche désormais le nom de votre règle.

Pour commencer à utiliser la nouvelle règle afin de détecter des informations sensibles, vous devez l’ajouter à une stratégie DLP. Pour découvrir comment ajouter la règle à une stratégie, voir [Gestion de stratégies de protection contre la perte de données (DLP)](manage-dlp-policies-exchange-2013-help.md).

## Glossaire terminologique

Voici les définitions des termes que vous avez rencontrés au cours de cette procédure.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Terme</th>
<th>Définition</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Entité</p></td>
<td><p>Les entités sont ce que nous appelons des types d’informations sensibles, comme les numéros de carte de crédit. Chaque entité possède un GUID unique qui constitue son ID. Si vous copiez un GUID et que vous le recherchez dans le XML, vous trouvez la définition de règle XML, ainsi que toutes les traductions localisées de cette règle XML. Vous pouvez également trouver cette définition en localisant le GUID de la traduction, puis en recherchant ce GUID.</p></td>
</tr>
<tr class="even">
<td><p>Fonctions</p></td>
<td><p>Le fichier XML fait référence à <strong>Func_credit_card</strong>, qui est une fonction dans le code compilé. Les fonctions sont utilisées pour exécuter des expressions régulières complexes et vérifier que les sommes de contrôle correspondent pour nos règles intégrées. Étant donné que tout ceci se passe dans le code, certaines variables ne figurent pas dans le fichier XML.</p></td>
</tr>
<tr class="odd">
<td><p>IdMatch</p></td>
<td><p>Il s’agit de l’identificateur auquel le modèle tente de correspondre, par exemple un numéro de carte de crédit. Vous pouvez en lire plus à ce sujet et au sujet des balises <strong>Match</strong> dans <a href="technical-description-of-xml-schema-for-dlp-rule-packages.md">Entity rules</a>.</p></td>
</tr>
<tr class="even">
<td><p>Listes de mots clés</p></td>
<td><p>Le fichier XML fait également référence à <strong>keyword_cc_verification</strong> et à <strong>keyword_cc_name</strong>, qui sont des listes de mots clés dans lesquelles nous recherchons des correspondances à l’intérieur du paramètre <strong>patternsProximity</strong> pour l’entité. Ces éléments ne sont actuellement pas affichés dans le fichier XML.</p></td>
</tr>
<tr class="odd">
<td><p>Modèle</p></td>
<td><p>Le modèle contient la liste de ce que le type sensible recherche. Cela inclut des mots clés, des expressions régulières et des fonctions internes (qui effectuent des tâches telles que la vérification des sommes de contrôle). Ces types d’informations sensibles peuvent avoir plusieurs modèles avec des niveaux de confiance uniques. Ceci est utile lors de la création d’un type d’informations sensibles qui renvoie un niveau de confiance élevé si des preuves crédibles sont trouvées et un niveau de confiance faible dans le cas contraire.</p></td>
</tr>
<tr class="even">
<td><p>confidenceLevel</p></td>
<td><p>Il s’agit du niveau de confiance appliqué lorsque le moteur DLP trouve une correspondance. Ce niveau de confiance est associé à une correspondance pour le modèle si les exigences du modèle sont remplies. C’est la mesure de confiance à prendre en considération lorsque vous utilisez des règles de transport Exchange.</p></td>
</tr>
<tr class="odd">
<td><p>patternsProximity</p></td>
<td><p>Lorsque nous trouvons ce qui ressemble à un modèle de numéro de carte de crédit, <strong>patternsProximity</strong> correspond à la proximité de recherche de preuves crédibles autour de ce numéro.</p></td>
</tr>
<tr class="even">
<td><p>recommendedConfidence</p></td>
<td><p>Il s’agit du niveau de confiance que nous recommandons pour cette règle. La confiance recommandée s’applique aux entités et aux affinités. Pour les entités, ce nombre n’est jamais évalué par rapport au paramètre <strong>confidenceLevel</strong> pour le modèle. Il s’agit d’une simple suggestion pour vous aider à choisir un niveau de confiance, si vous voulez en appliquer un. Pour les affinités, le paramètre <strong>confidenceLevel</strong> du modèle doit être supérieur au nombre <strong>recommendedConfidence</strong> pour une action de règle de transport Exchange à appeler. Le paramètre <strong>recommendedConfidence</strong> correspond au niveau de confiance par défaut utilisé dans les règles de transport Exchange qui appelle une action. Si vous le souhaitez, vous pouvez modifier manuellement la règle de transport Exchange à appeler pour le faire à partir du niveau de confiance du modèle.</p></td>
</tr>
</tbody>
</table>


## Pour plus d’informations

  - [Application des règles DLP pour évaluer les messages](how-dlp-rules-are-applied-to-evaluate-messages-exchange-2013-help.md)

  - [Création d'une stratégie personnalisée de protection contre la perte de données (DLP)](create-a-custom-dlp-policy-exchange-2013-help.md)

  - [Éléments recherchés par les types d’informations sensibles dans Exchange](what-the-sensitive-information-types-in-exchange-look-for-exchange-online-help.md)

