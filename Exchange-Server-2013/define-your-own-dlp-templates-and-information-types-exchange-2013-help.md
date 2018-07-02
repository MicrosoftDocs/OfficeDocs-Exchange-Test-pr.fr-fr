---
title: "Définition de vos modèles DLP et types d'informations: Exchange 2013 Help"
TOCTitle: Définition de vos modèles DLP et types d'informations
ms:assetid: f4622dba-3347-4758-b4a2-f01b043c908c
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ674310(v=EXCHG.150)
ms:contentKeyID: 50479546
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Définition de vos modèles DLP et types d'informations

 

_**Sapplique à :** Exchange Online, Exchange Server 2013_

_**Dernière rubrique modifiée :** 2015-01-14_

Vous pouvez construire des modèles de stratégie de protection contre la perte de données (DLP) sous forme de fichiers XML indépendants de Microsoft Exchange Server 2013 et les importer ensuite au moyen du Centre d'administration Exchange (CAE) ou de l'environnement de ligne de commande Exchange Management Shell. Cette rubrique décrit la procédure et les détails de la création et de l'adaptation des fichiers XML DLP pour les utiliser dans une solution DLP. Il n'est pas indispensable de développer vos propres fichiers XML DLP, car le Centre d'administration Exchange (CAE) offre un moyen d'être rapidement opérationnel avec les modèles de stratégie DLP et les règles de transport existants pour analyser des messages.

Souhaitez-vous rechercher les tâches de gestion liées aux stratégies de DLP ? Consultez la rubrique [Procédures relatives à la protection contre la perte de données (DLP)](dlp-procedures-exchange-2013-help.md) (Exchange Server 2013) ou [Procédures relatives à la protection contre la perte de données (DLP)](https://technet.microsoft.com/fr-fr/library/jj938003\(v=exchg.150\)) (Exchange Online).

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Exchange 2013 : la protection contre la perte de données est une fonctionnalité étendue qui nécessite une licence d’accès client (CAL) Exchange Enterprise. Pour plus d’informations sur les licences d’accès client et les licences par serveur, consultez la rubrique <a href="https://go.microsoft.com/fwlink/p/?linkid=237292">Licences Exchange Server</a>.<br />
Exchange Online : la protection contre la perte de données est une fonctionnalité étendue qui nécessite une licence Exchange Online Plan 2. Pour plus d’informations, voir <a href="https://go.microsoft.com/fwlink/p/?linkid=286154">Licences Exchange Online</a>.</td>
</tr>
</tbody>
</table>


<table>
<thead>
<tr class="header">
<th><img src="images/JJ159813.important(EXCHG.150).gif" title="Important" alt="Important" />Important :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Il sort du cadre de cette documentation de recommander un modèle d'entreprise ou des informations sur les consignes de conditionnement des fichiers ou de déploiement pour les règles sur les informations sensibles, ou d'exposer comment ces règles doivent être réparties. De plus, cette documentation n'expose pas les mécanismes de protection (par exemple, le chiffrement) pour les règles développées personnalisées ; elle n'expose pas non plus comment ces mécanismes sont utilisés.</td>
</tr>
</tbody>
</table>


## Étendre les types d'informations pour répondre à vos besoins

Les sections suivantes exposent les concepts et la définition des schémas XML que vous devez connaître avant de créer vos propres fichiers XML à la fois pour les modèles de stratégie DLP et les packages de règles sur les informations sensibles qu'il est possible d'importer dans Exchange 2013 et d'utiliser comme stratégies DLP.

Dans Microsoft Exchange, la protection contre la perte de données (DLP) vous aide à appliquer aux informations sensibles une stratégie propre à votre organisation. Un facteur essentiel caractérisant la puissance d'une solution DLP constitue la capacité à identifier correctement des informations confidentielles et sensibles qui peuvent être propres à l'organisation, aux exigences réglementaires, à des caractéristiques géographiques ou à d'autres considérations professionnelles. Bien que Microsoft fournisse avec le produit des modèles de stratégie et des types d'informations sensibles qui vous permettent de commencer, vos besoins professionnels uniques peuvent nécessiter une solution personnalisée de protection contre la perte de données. C'est pourquoi Microsoft offre un moyen de créer et d'importer vos propres modèles de stratégie DLP ou vos définitions d'informations sensibles dans des packages de règles de classification. Une solution DLP précise s'appuie sur la configuration d'un ensemble de règles approprié pour le moteur de détection des informations sensibles qui offrent une forte protection tout en minimisant les faux positifs et négatifs.

## Développer vos propres modèles de stratégies DLP

Vous pouvez créer votre propre fichier modèle XML de stratégie DLP et l'importer. Cette approche d'extension de la solution DLP dans Exchange vous permet de créer des stratégies DLP qui correspondent étroitement à vos besoins de protection contre la perte de données.

La gestion des modèles personnalisés et leurs stratégies connexes est semblable à celle des stratégies DLP que vous créez à partir des modèles fournis par Microsoft. Dans un cycle de vie de stratégie DLP classique, vous devez procéder comme suit :

1.  Créez votre propre modèle de stratégie DLP, un fichier XML personnalisé. Pour en savoir plus, consultez la rubrique [Développement des fichiers modèles de stratégie DLP](xml-rule-schema-and-rule-structure-guide-for-dlp-policy-files.md).

2.  Importez votre modèle personnalisé. Pour en savoir plus, consultez la rubrique [Importer un modèle de stratégie DLP personnalisé à partir d’un fichier](import-a-custom-dlp-policy-template-from-a-file-exchange-2013-help.md).

3.  Créez une stratégie DLP basée sur votre modèle personnalisé. Pour en savoir plus, consultez la rubrique [Création d'une stratégie DLP à partir d'un modèle](how-to-new-dlp-data-loss-prevention-policy-template.md).

4.  Mettez à jour votre modèle personnalisé en répétant les étapes 1 et 2.

5.  Supprimez votre modèle personnalisé. Pour en savoir plus, consultez la rubrique [Remove-DlpPolicyTemplate](https://technet.microsoft.com/fr-fr/library/jj215739\(v=exchg.150\)).

Pour plus d'informations sur la définition des schémas XML et les concepts de développement de vos propres modèles, consultez la rubrique [Développement des fichiers modèles de stratégie DLP](xml-rule-schema-and-rule-structure-guide-for-dlp-policy-files.md).

## Développer vos propres types d'informations sensibles et la logique correspondante dans des packages de règles de classification

Vous pouvez créer vos propres définitions d'informations sensibles dans un package de règles de classification (fichier XML) et l'importer dans votre solution DLP. Le moteur de détection des informations sensibles offre des fonctions d'analyse en profondeur du contenu pour identifier les informations sensibles (ex. numéros de cartes de crédit, numéros de sécurité sociale et informations de propriété intellectuelle de la société). Un ensemble configurable d'instructions, ou de règles, contrôle ce moteur pour l'analyse du contenu. Ces règles sont regroupées dans un package de règles de classification : il s'agit d'un document XML qui correspond à une définition standard de schéma XML de package de règles. Voici comment vous pouvez développer le vôtre.

1.  Créez vos propres types d'informations sensibles, un fichier XML personnalisé. Pour en savoir plus, consultez la rubrique [Développement de packages de règles des informations sensibles](technical-description-of-xml-schema-for-dlp-rule-packages.md).

2.  Importez le type d'informations sensibles. Pour en savoir plus, consultez la rubrique [New-ClassificationRuleCollection](https://technet.microsoft.com/fr-fr/library/jj218619\(v=exchg.150\)).

3.  Créez un modèle personnalisé en fonction des types d'informations. Pour en savoir plus, consultez la rubrique [Développement de packages de règles des informations sensibles](technical-description-of-xml-schema-for-dlp-rule-packages.md).

4.  Mettez à jour votre modèle personnalisé en répétant les étapes 1 et 2.

5.  Supprimez votre modèle personnalisé. Pour en savoir plus, consultez la rubrique [Remove-ClassificationRuleCollection](https://technet.microsoft.com/fr-fr/library/jj218670\(v=exchg.150\)).

Pour plus d'informations sur les packages de règles, consultez les rubriques [Développement de packages de règles des informations sensibles](technical-description-of-xml-schema-for-dlp-rule-packages.md) et [Méthodes et techniques de mise en correspondance pour les packages de règles](technical-description-of-xsd-rule-matching-for-dlp-rule-packages.md).

## Comprendre les types de règles dans les packages de règles

Les règles dans un package configurent le processus de détection de caractéristiques de contenu bien définies, par exemple les règles de recherche d'un numéro de permis de conduire. Il existe deux principaux types de règles : Entité et affinité.

Les règles d'*entité* sont ciblées sur des identificateurs bien définis (souvent réglementés) tels que les numéros de sécurité sociale. Une collection de modèles dénombrables représente une entité. Un modèle définit une collection de correspondances avec un identificateur explicite de correspondance principale. Un permis de conduire est un exemple d'entité.

Les règles d'*affinité* sont ciblées sur un certain type de document (ex. état financier d'une entreprise). Un ensemble de preuves indépendantes représente une affinité. Une preuve est une agrégation de correspondances requises dans une certaine proximité. La loi américaine Sarbanes-Oxley est un exemple d'affinité.

## Pour plus d'informations

[Protection contre la perte de données](technical-overview-of-dlp-data-loss-prevention-in-exchange.md)

[Importer un modèle de stratégie DLP personnalisé à partir d’un fichier](import-a-custom-dlp-policy-template-from-a-file-exchange-2013-help.md)

[New-ClassificationRuleCollection](https://technet.microsoft.com/fr-fr/library/jj218619\(v=exchg.150\))

[Règles de transport ou de flux de messagerie](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md)Exchange Server 2013

[Règles de flux de messagerie (règles de transport) dans Exchange Online](https://technet.microsoft.com/fr-fr/library/jj919238\(v=exchg.150\))Exchange Online

[Éléments recherchés par les types d’informations sensibles dans Exchange](what-the-sensitive-information-types-in-exchange-look-for-exchange-online-help.md)

