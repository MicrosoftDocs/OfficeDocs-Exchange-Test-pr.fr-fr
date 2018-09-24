---
title: 'Développement des fichiers modèles de stratégie DLP: Exchange 2013 Help'
TOCTitle: Développement des fichiers modèles de stratégie DLP
ms:assetid: 4b263547-aef4-4ee8-aa4f-fa64a5863189
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ674703(v=EXCHG.150)
ms:contentKeyID: 50478076
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Développement des fichiers modèles de stratégie DLP

 

_**Sapplique à :** Exchange Online, Exchange Server 2013_

_**Dernière rubrique modifiée :** 2015-03-09_

Cette vue d'ensemble décrit les composants d'une définition de schéma XML pour les fichiers de modèle de stratégie de protection contre la perte de données (DLP). Elle fournit également un exemple de fichier de stratégie au format XML. Il est utile de comprendre l'ensemble de l'architecture DLP et du processus de développement des règles avant de commencer. Pour plus d'informations, consultez les rubriques [Protection contre la perte de données](https://docs.microsoft.com/fr-fr/exchange/security-and-compliance/data-loss-prevention/data-loss-prevention) et [Définition de vos modèles DLP et types d'informations](define-your-own-dlp-templates-and-information-types-exchange-2013-help.md).

Afin de faciliter l'adoption et la gestion des solutions de protection contre la perte de données, un modèle conceptuel connu sous le nom de stratégies DLP et modèles de stratégies est introduit dans Microsoft Exchange Server 2013. Les modèles de stratégie DLP fournissent une conception préliminaire pour la stratégie DLP prévue. Un modèle de stratégie DLP doit, pour être utilisable, encapsuler toutes les directives et objets de données requis pour répondre aux objectifs d'une stratégie spécifique, par exemple une réglementation ou des besoins professionnels. Le modèle n'est pas spécifique à l'environnement. Il s'agit seulement d'une définition ou d'un modèle de stratégie utilisé dans le cadre de la configuration du produit ou fourni par des fournisseurs de logiciels et partenaires indépendants. De plus, les stratégies DLP sont des instanciations d'exécution des modèles spécifiques à l'environnement de déploiement. Votre structure de stratégie de messagerie existante peut incorporer des stratégies DLP par le biais de l'utilisation de règles de transport. Les règles de transport offrent une grande flexibilité dans l'adaptation et l'expression de la richesse de vos solutions DLP.

## Structure et sources du modèle de stratégie

Les modèles de stratégie DLP sont généralement influencés par plusieurs sources, notamment les directives de traitement sur le serveur, les stratégies de l'ordinateur client ou d'autres constructions de stratégies, comme l'illustre l'image ci-dessous :

![Facteurs influençant les modèles de stratégie](images/JJ674703.12f48e4f-d7b8-4ddd-87e8-8477983252ec(EXCHG.150).gif "Facteurs influençant les modèles de stratégie")

Les opérations de gestion simples sont disponibles pour les modèles de stratégie DLP par le biais d'Exchange Management Shell et des interfaces basées sur Internet, telles que le centre d'administration Exchange, dotées de fonctionnalités d'importation, d'exportation, de suppression et de requête. Une stratégie DLP est créée en référençant un modèle de stratégie DLP dans le cadre du processus de création. Ces modèles de stratégie DLP référencés peuvent se rapporter à des modèles installés dans le système, qui sont stockés dans des services de domaine Active Directory ou directement fournis comme entrées à partir de stratégies fournies en externe.

Les modèles de stratégie DLP sont représentés sous forme de documents XML. Un schéma XML unique est utilisé pour les stratégies fournies dans Exchange, ainsi qu'en externe. La structure conceptuelle du document XML est représentée dans le tableau ci-dessous, qui indique les éléments principaux. L'ensemble des définitions de composants de stratégie vous permet d'atteindre un objectif de stratégie spécifique, par exemple une réglementation ou des besoins professionnels.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Élément structurel</th>
<th>Définition ou exemple</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Éditeur</p></td>
<td><p>Microsoft ou Partenaire</p></td>
</tr>
<tr class="even">
<td><p>Version</p></td>
<td><p>15.0.1.0</p></td>
</tr>
<tr class="odd">
<td><p>Nom de la stratégie</p></td>
<td><p>PCI-DSS</p></td>
</tr>
<tr class="even">
<td><p>Description</p></td>
<td><p>La stratégie PCI DSS DLP permet de détecter la présence d’informations sujettes aux normes de sécurité des données ‎(PCI DSS)‎, notamment des numéros de carte de crédit ou de carte bancaire. L’utilisation de cette stratégie ne garantit la conformité avec aucune réglementation. À l’issue de votre test, effectuez les modifications de configuration nécessaires dans Exchange de sorte que la transmission des informations respecte les stratégies de votre organisation. Par exemple, vous pourriez avoir besoin de configurer TLS avec des partenaires commerciaux connus ou d’ajouter des actions de règle de transport plus restrictives, comme l’ajout d’une protection des droits pour des messages qui contiennent ce type de données.</p></td>
</tr>
<tr class="odd">
<td><p>Métadonnées</p></td>
<td><p>Balises pour décrire la réglementation locale, nationale ou régionale, les mots clés, etc.</p></td>
</tr>
<tr class="even">
<td><p>Ensemble de constructions de stratégie</p></td>
<td><ol>
<li><p>Définitions des règles de transport, telles que les conditions et les actions.</p></li>
<li><p>Définitions des comportements des clients de messagerie qui contrôlent l'expérience du client par l'intermédiaire de notifications interactives.</p></li>
<li><p>De manière facultative, références de configuration qui doivent être coordonnées avec les paramètres spécifiques à l'environnement du client.</p></li>
</ol></td>
</tr>
<tr class="odd">
<td><p>Ensemble de classifications de données</p></td>
<td><ol>
<li><p>Spécifie les entités ou les affinités de classification.</p></li>
<li><p>Les entités comportent le nombre et le niveau de confiance ; les affinités n'ont que le niveau de confiance.</p></li>
<li><p>Possède son propre ensemble de propriétés et son schéma de classification.</p></li>
</ol></td>
</tr>
</tbody>
</table>


## Définition du format du modèle de stratégie

Les modèles de stratégie DLP sont exprimés comme des documents XML qui adhèrent au schéma suivant. Notez que le code XML respecte la casse. Par exemple, `dlpPolicyTemplates` fonctionnera, mais `DlpPolicyTemplates` ne fonctionnera pas.

```XML
<?xml version="1.0" encoding="UTF-8"?>
<dlpPolicyTemplates>
  <dlpPolicyTemplate id="F7C29AEC-A52D-4502-9670-141424A83FAB" mode="Audit" state="Enabled" version="15.0.2.0">
    <contentVersion>4</contentVersion>
    <publisherName>Microsoft</publisherName>
    <name>
      <localizedString lang="en">PCI-DSS</localizedString>
    </name>
    <description>
      <localizedString lang="en">Detects the presence of information subject to Payment Card Industry Data Security Standard (PCI-DSS) compliance requirements.</localizedString>
    </description>
    <keywords></keywords>
    <ruleParameters></ruleParameters>
    <ruleParameters/>
    <policyCommands>
      <!-- The contents below are applied/executed as rules directly in PS - -->
      <commandBlock>
        <![CDATA[ new-transportRule "PCI-DSS: Monitor Payment Card Information Sent To Outside" -DlpPolicy "%%DlpPolicyName%%" -SentToScope NotInOrganization -SetAuditSeverity High -MessageContainsDataClassifications @{Name="Credit Card Number"; MinCount="1" } -Comments "Monitors payment card information sent to outside the organization as part of the PCI-DSS DLP Policy."]]>
      </commandBlock>
      <commandBlock>
        <![CDATA[ new-transportRule "PCI-DSS: Monitor Payment Card Information Sent To Within" -DlpPolicy "%%DlpPolicyName%%" -Comments "Monitors payment card information sent inside the organization as part of the PCI-DSS DLP Policy." -SentToScope InOrganization -SetAuditSeverity Low -MessageContainsDataClassifications @{Name="Credit Card Number"; MinCount="1" } ]]>
      </commandBlock>
    </policyCommands>
    <policyCommandsResources></policyCommandsResources>
  </dlpPolicyTemplate>
</dlpPolicyTemplates>
```

Si un paramètre inclus dans votre fichier XML pour tout élément comporte un espace, ce paramètre doit être mis entre guillemets pour fonctionner correctement. Dans l'exemple ci-dessous, le paramètre qui suit `-SentToScope` est acceptable et n'est pas entre guillemets car il s'agit d'une chaîne de caractères continue sans espace. En revanche, le paramètre fourni pour –`Comments` n'apparaîtra pas dans le centre d'administration Exchange, car il n'est pas entre guillemets alors qu'il comporte des espaces.

```XML
<CommandBlock><![CDATA[ new-transportRule "PCI-DSS: Monitor Payment Card Information Sent To Within" -DlpPolicy "PCI-DSS" -Comments Monitors payment card information sent inside the organization -SentToScope InOrganization -SetAuditSeverity Low -MessageContainsDataClassifications @{Name="Credit Card Number"; MinCount="1" } ]]> </CommandBlock>
```

## Élément localizedString

Le format du modèle permet de localiser des chaînes dans le modèle qui doit être présenté à l'utilisateur final, par exemple dans le cadre de la sélection des modèles de stratégie DLP installés. L'élément localizedString peut être utilisé pour fournir des définitions multiples pour les champs Nom et Description.

## Nœud ruleParameters

Il s'agit d'un ensemble de paramètres facultatifs qui doivent être fournis au cours de la phase d'instanciation du modèle lors de la création d'une stratégie DLP à mapper sur des objets spécifiques de déploiement. Par exemple, un groupe de distribution réel disponible dans le déploiement.

## Élément dlpPolicyTemplate

Il s'agit de l'élément racine pour le modèle de stratégie DLP, requis pour chaque modèle. Le tableau suivant présente les attributs disponibles :


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Nom de l'attribut</th>
<th>Obligatoire ?</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Version</p></td>
<td><p>Oui</p></td>
<td><p>Numéro de version utilisé dans ce document de modèle de stratégie DLP.</p></td>
</tr>
<tr class="even">
<td><p>State</p></td>
<td><p>Non</p></td>
<td><p>Configuration par défaut facultative pour l'état de la stratégie.</p></td>
</tr>
<tr class="odd">
<td><p>Mode</p></td>
<td><p>Non</p></td>
<td><p>Configuration par défaut facultative pour le mode de la stratégie.</p></td>
</tr>
<tr class="even">
<td><p>Id</p></td>
<td><p>Non</p></td>
<td><p>GUID visant à identifier de manière unique cette définition de modèle de stratégie DLP dans le format suivant :« A29C69BF-4F98-47F1-9A99-5771DFD2C27F ».</p></td>
</tr>
</tbody>
</table>


Les éléments enfants incluent la séquence d'éléments suivante.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Élément enfant</th>
<th>(minimum, maximum)</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>PublisherName</p></td>
<td><p>(1, 1)</p></td>
<td><p>Métadonnées pour l’éditeur du modèle</p></td>
</tr>
<tr class="even">
<td><p>Name</p></td>
<td><p>(1, 1)</p></td>
<td><p>Nom localisable pour ce modèle.</p></td>
</tr>
<tr class="odd">
<td><p>Description</p></td>
<td><p>(1, 1)</p></td>
<td><p>Description localisable pour ce modèle.</p></td>
</tr>
<tr class="even">
<td><p>Keywords</p></td>
<td><p>(1, 1)</p></td>
<td><p>Liste des mots clés qui s'appliquent à ce modèle. Un modèle peut avoir une liste de mots clés vide.</p></td>
</tr>
<tr class="odd">
<td><p>RuleParameters</p></td>
<td><p>(0, 1)</p></td>
<td><p>Liste des paramètres du modèle utilisés dans la définition de la stratégie.</p></td>
</tr>
<tr class="even">
<td><p>PolicyCommands</p></td>
<td><p>(0, 1)</p></td>
<td><p>Liste des définitions de règles de transport pour cette stratégie. Cet élément est facultatif.</p></td>
</tr>
</tbody>
</table>


## Modèle de stratégie DLP : Commandes de stratégie

Cette partie du modèle de stratégie contient la liste des commandes Exchange Management Shell utilisées pour instancier la définition de la stratégie. Le processus d'importation exécutera chaque commande dans le cadre du processus d'instanciation. Vous trouverez ici des exemples de commandes de stratégie.

```powershell
<PolicyCommands>
    <!-- The contents below are applied/executed as rules directly in PS - -->
      <CommandBlock> <![CDATA[ new-transportRule "PCI-DSS: Monitor Payment Card Information Sent To Outside" -DlpPolicy "PCI-DSS" -SentToScope NotInOrganization -SetAuditSeverity High -MessageContainsDataClassifications @{Name="Credit Card Number"; MinCount="1" } -Comments "Monitors payment card information sent to outside the organization as part of the PCI-DSS DLP policy."]]></CommandBlock>
      <CommandBlock><![CDATA[ new-transportRule "PCI-DSS: Monitor Payment Card Information Sent To Within" -DlpPolicy "PCI-DSS" -Comments "Monitors payment card information sent inside the organization as part of the PCI-DSS DLP policy." -SentToScope InOrganization -SetAuditSeverity Low -MessageContainsDataClassifications @{Name="Credit Card Number"; MinCount="1" } ]]> </CommandBlock>
  </PolicyCommands>
  ``` 

Le format des cmdlets correspond à la syntaxe standard des cmdlets Exchange Management Shell pour les cmdlets utilisées. Les commandes sont exécutées dans l'ordre. Chaque nœud de commande peut contenir un bloc de script composé de plusieurs commandes. L'exemple ci-après illustre l'incorporation d'un module de règles de classification à l'intérieur d'un modèle de stratégie DLP, ainsi que l'installation du module de règles dans le cadre du processus de création de stratégie. Le module de règles de classification est incorporé dans le modèle de stratégie, puis transmis en tant que paramètre vers la cmdlet du modèle :

```powershell
<CommandBlock>
  <![CDATA[
$rulePack = [system.Text.Encoding]::Unicode.GetBytes('<?xml version="1.0" encoding="utf-16"?>
<rulePackage xmlns="http://schemas.microsoft.com/office/2011/mce">

  <RulePack id="c3f021a3-c265-4dc2-b3a7-41a1800bf518">
    <Version major="1" minor="0" build="0" revision="0"/>
    <Publisher id="e17451d3-9648-4117-a0b1-493a6d5c73ad"/>
    <Details defaultLangCode="en-us">
      <LocalizedDetails langcode="en-us">
        <PublisherName>Contoso</PublisherName>
        <Name>Contoso Sample Rule Pack</Name>
        <Description>This is a sample rule package</Description>
      </LocalizedDetails>
    </Details>
  </RulePack>

  <Rules>
    <Entity id="7cc35258-6b35-4415-baff-a76d1a018980" patternsProximity="300" recommendedConfidence="85" workload="Exchange">     

      <Pattern confidenceLevel="85">
        <IdMatch idRef="Regex_Contoso" />
        <Any minMatches="1">
          <Match idRef="Regex_conf" />
        </Any>
      </Pattern>
    </Entity>

    <Regex id="Regex_Contoso">(?i)(\bContoso\b)</Regex>
    <Regex id="Regex_conf">(?i)(\bConfidential\b)</Regex>

    <LocalizedStrings>
      <Resource idRef="7cc35258-6b35-4415-baff-a76d1a018980">
        <Name default="true" langcode="en-us">
          Confidential Information Rule
        </Name>
        <Description default="true" langcode="en-us">
          Sample rule pack - Detects Contoso confidential information
        </Description>
      </Resource>
    </LocalizedStrings>
  </Rules>

</RulePackage>

')

New-ClassificationRuleCollection -FileData $rulePack 
New-TransportRule -name "customEntity" -DlpPolicy "%%DlpPolicyName%%" -SentToScope NotInOrganization -MessageContainsDataClassifications @{Name="Confidential Information Rule"} -SetAuditSeverity High]]>
</CommandBlock> 
```

Les éléments enfants comportent la suite d'éléments suivante dans cet ordre.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Élément enfant</th>
<th>(Minimum, Maximum)</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>CommandBlock</p></td>
<td><p>(1, n)</p></td>
<td><p>Bloc de commandes exécuté dans le PowerShell. Les blocs de commandes sont tous exécutés dans l'ordre.</p></td>
</tr>
</tbody>
</table>


## Pour plus d'informations

[Protection contre la perte de données](https://docs.microsoft.com/fr-fr/exchange/security-and-compliance/data-loss-prevention/data-loss-prevention)

[Définition de vos modèles DLP et types d'informations](define-your-own-dlp-templates-and-information-types-exchange-2013-help.md)

[Importer un modèle de stratégie DLP personnalisé à partir d’un fichier](import-a-custom-dlp-policy-template-from-a-file-exchange-2013-help.md)

