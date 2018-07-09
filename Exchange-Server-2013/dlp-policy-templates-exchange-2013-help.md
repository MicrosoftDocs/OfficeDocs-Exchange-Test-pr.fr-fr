---
title: 'Modèles de stratégies de protection contre la perte de données (DLP): Exchange 2013 Help'
TOCTitle: Modèles de stratégies de protection contre la perte de données (DLP)
ms:assetid: c7b1a8e4-30d9-4409-85c5-f85ae023737d
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ657730(v=EXCHG.150)
ms:contentKeyID: 50479152
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Modèles de stratégies de protection contre la perte de données (DLP)

 

_**Sapplique à :** Exchange Online, Exchange Server 2013_

_**Dernière rubrique modifiée :** 2015-01-14_

Vous pouvez utiliser des modèles de stratégie de protection contre la perte de données (DLP, Data Loss Prevention) pour vous familiariser avec votre solution DLP dans Microsoft Exchange 2013. Un modèle de stratégie DLP est un modèle pour une stratégie. Vous pouvez sélectionner un modèle pour lancer le processus de création de stratégie DLP personnalisée. Au sein de la stratégie DLP, vous pouvez personnaliser les règles pour garantir qu'elles répondent à vos besoins professionnels en matière de protection contre la perte de données. Plusieurs modèles de stratégies sont fournis par Microsoft, mais il ne s'agit pas de l'unique façon d'implémenter une solution de protection contre la perte de données dans Exchange.

Souhaitez-vous rechercher les tâches de gestion liées aux stratégies de DLP ? Consultez la rubrique [Procédures relatives à la protection contre la perte de données (DLP)](dlp-procedures-exchange-2013-help.md).

**Contenu de cette rubrique**

Étendre les modèles et les types d'informations pour répondre à vos besoins

Créer votre propre modèle de stratégie DLP ou vos propres types d'informations confidentielles dans un package de règles de classification

Inclure la fonctionnalité DLP aux règles de transport existantes

Utiliser des stratégies DLP créées par Microsoft

Pour plus d'informations

## Étendre les modèles et les types d'informations pour répondre à vos besoins

Vous pouvez incorporer des modèles de stratégie et des définitions de contenu confidentiel à partir de Microsoft Partners ou à partir de fichiers que vous avez vous-même développés en tant qu'ajout aux modèles de stratégie DLP, types d'informations et règles déjà fournies dans Exchange 2013. Voici plusieurs méthodes vous permettant d'ajouter votre propre contenu DLP et d'étendre la fonctionnalité DLP. Les modèles déjà fournis par Microsoft sont un bon point de départ pour vous familiariser avec une solution DLP. Pour étendre les fonctionnalités DLP à vos propres fichiers de modèles de stratégie DLP uniques, vous devez comprendre les exigences de schéma XML relatives aux modèles de stratégies créés indépendamment de Exchange. Pour en savoir plus sur les cmdlets Exchange Management Shell associés avec les modèles de stratégie DLP, consultez les cmdlets liées à `Get-DlpPolicyTemplate` dans [Cmdlets de stratégie et de conformité](https://technet.microsoft.com/fr-fr/library/dd298082\(v=exchg.150\)). De plus, vous pouvez définir vos propres types de contenu confidentiel après avoir compris le format et la procédure permettant de les incorporer. Pour en savoir plus sur les cmdlets Exchange Management Shell associés avec les modèles de stratégie DLP, consultez les cmdlets liées à `Get-ClassificationRuleCollection` dans [Cmdlets de stratégie et de conformité](https://technet.microsoft.com/fr-fr/library/dd298082\(v=exchg.150\)).

> [!CAUTION]
> Vous devez activer vos stratégies DLP en mode Test avant de les appliquer dans votre environnement de production. Pour ces tests, nous vous recommandons de configurer des boîtes aux lettres d’exemples d’utilisateurs et d’envoyer des messages de test qui appelleront vos stratégies de test afin de confirmer les résultats.


## Créer votre propre modèle de stratégie DLP ou vos propres types d'informations confidentielles dans un package de règles de classification

Vous pouvez aussi créer un fichier de modèle de stratégie DLP qui répond à la définition de schéma XML spécifique fournie par Microsoft à partir d'Exchange, puis importer le fichier dans votre système pour pouvoir créer des stratégies DLP à partir de celui-ci. En créant vos propres fichiers de modèles, vous pouvez définir votre propre modèle de stratégies DLP que Microsoft n'a pas encore fournies. Cette procédure diffère de la création d'une stratégie DLP à l'aide du Centre d'administration Exchange (CAE), ce qui a généralement lieu après la mise à disposition des modèles de stratégie. Si vous créez un modèle de stratégie indépendant d'Exchange, vous devrez l'importer avant de pouvoir l'utiliser pour analyser des messages. Vous pouvez aussi créer vos propres définitions d'informations confidentielles, en plus de celles définies par Microsoft dans Exchange. Il existe une définition de schéma XML distincte pour les fichiers de modèles de stratégies DLP et les packages de règle de classification. Pour démarrer, consultez les rubriques suivantes :

  -  [Définition de vos modèles DLP et types d'informations](define-your-own-dlp-templates-and-information-types-exchange-2013-help.md)

  -  [Importer un modèle de stratégie DLP personnalisé à partir d’un fichier](import-a-custom-dlp-policy-template-from-a-file-exchange-2013-help.md)

## Inclure la fonctionnalité DLP aux règles de transport existantes

Vous pouvez incorporer des capacités de détection DLP aux règles de transport traditionnelles sans créer une nouvelle stratégie DLP. Si vous avez créé un ensemble de règles complet dans une version précédente d'Exchange et que vous souhaitez les dupliquer ou ajouter la détection d'informations confidentielles dans Exchange 2013, vous pouvez utiliser l'éditeur de règles de transport dans le Centre d'administration Exchange ou dans l'environnement de ligne de commande Exchange Management Shell pour incorporer ces deux fonctionnalités. Pour démarrer, consultez les rubriques suivantes :

  -  [Règles de transport ou de flux de messagerie](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md) (Exchange Server 2013)

  -  [Règles de flux de messagerie (règles de transport) dans Exchange Online](https://technet.microsoft.com/fr-fr/library/jj919238\(v=exchg.150\)) (Exchange Online)

  -  [Gestion de règles de flux de messagerie](manage-mail-flow-rules-exchange-2013-help.md)
    
  -  [Cmdlets de stratégie et de conformité](https://technet.microsoft.com/fr-fr/library/dd298082\(v=exchg.150\))

## Utiliser des stratégies DLP créées par Microsoft

De nombreuses stratégies DLP sont fournies par Microsoft. C'est le moyen le plus simple pour vous familiariser avec une solution DLP flexible et simple à implémenter. Vous pouvez utiliser les stratégies fournies comme point de départ et les personnaliser ensuite pour les conformer à vos exigences. Pour démarrer, consultez les rubriques suivantes :

  - [Modèles de stratégies DLP fournis dans Exchange](dlp-policy-templates-supplied-in-exchange-exchange-2013-help.md)

  - [Création d'une stratégie DLP à partir d'un modèle](how-to-new-dlp-data-loss-prevention-policy-template.md)

## Pour plus d'informations

[Protection contre la perte de données](technical-overview-of-dlp-data-loss-prevention-in-exchange.md)

