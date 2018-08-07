---
title: 'Export de types de données sensibles DLP d’Exchange 2013: Exchange 2013 Help'
TOCTitle: Exportation de types d’informations sensibles DLP à partir d’Exchange
ms:assetid: 8f02fbc2-dd1c-4276-be1a-517a43fe39b2
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dn479225(v=EXCHG.150)
ms:contentKeyID: 59634340
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Exportation de types d’informations sensibles DLP à partir d’Exchange 2013

 

_**Sapplique à :** Exchange Online, Exchange Server 2013_

_**Dernière rubrique modifiée :** 2016-05-04_

Vous pouvez afficher ou modifier les détails au sein de vos stratégies DLP sans utiliser le Centre d’administration Exchange (EAC) ou les applets de commande Environnement de ligne de commande Exchange Management Shell en exportant les stratégies, enregistrant dans un fichier XML, la modification de ce fichier XML. En règle générale vous souhaitez ensuite réimporter le fichier XML dans Exchange. De cette façon, les stratégies peuvent être modifiés indépendamment du Exchange. Toutefois, ils doivent répondre aux exigences de format spécifique, également appelés schéma XML, afin de fonctionner correctement.

Pour découvrir d’autres tâches de gestion relatives à la protection contre la perte de données, consultez la rubrique [Gestion de stratégies de protection contre la perte de données (DLP)](manage-dlp-policies-exchange-2013-help.md).

## Ce qu’il faut savoir avant de commencer

  - Durée d’exécution estimée : 15 minutes

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l’entrée « Protection contre la perte de données » dans la rubrique [Stratégie de messagerie et autorisations de conformité](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.


## Que souhaitez-vous faire ?

Le Centre d’administration Exchange ne permet pas d’exporter des stratégies ou des modèles de protection contre la perte de données dans un fichier externe. Utilisez l’Environnement de ligne de commande Exchange Management Shell pour effectuer cette tâche.

## Utilisez le Environnement de ligne de commande Exchange Management Shell pour exporter les types d'informations sensibles DLP

Cet exemple exporte tous les types d’informations sensibles de protection contre la perte de données (DLP) et leurs attributs dans un fichier XML dans le chemin C:\\My Documents\\exportedInformationTypes.xml. Nous vous recommandons de faire une copie de sauvegarde de votre collection de types d’informations sensibles DLP actuelle. Pour y parvenir, vous pouvez par exemple exporter le fichier XML, en faire immédiatement une copie, puis le renommer.

1.  Ouvrez l’Environnement de ligne de commande Exchange Management Shell.

2.  Saisissez **Get-ClassificationRuleCollection** et les types d’informations sensibles de votre organisation devraient s’afficher à l’écran. Si vous n’avez pas créé vos propres types d’informations sensibles, vous ne verrez que la valeur par défaut, c’est-à-dire la collection de types d’informations sensibles intégrés, intitulées « Package de règles Microsoft ».

3.  Stockez les types d’informations sensibles dans une variable en saisissant **$ruleCollections = Get-ClassificationRuleCollection**.

4.  À présent, créez un fichier au format XML contenant toutes les données en saisissant **Set-Content -path "C:\\My Documents\\exportedRules.xml" -Encoding Byte -Value $ruleCollections.SerializedClassificationRuleCollection**.

Vous pouvez maintenant modifier le fichier XML pour ajuster les stratégies en fonction de vos besoins. Pour apprendre à personnaliser les types d’informations sensibles intégrés, voir [Personnaliser les types d’informations sensibles DLP intégrées](customize-the-built-in-dlp-sensitive-information-types-exchange-2013-help.md). Pour plus de détails sur la réimportation de stratégies dans Exchange, voir [Importer un modèle de stratégie DLP personnalisé à partir d’un fichier](import-a-custom-dlp-policy-template-from-a-file-exchange-2013-help.md).

## Pour plus d’informations

[Éléments recherchés par les types d’informations sensibles dans Exchange](what-the-sensitive-information-types-in-exchange-look-for-exchange-online-help.md)

[Personnaliser les types d’informations sensibles DLP intégrées](customize-the-built-in-dlp-sensitive-information-types-exchange-2013-help.md)

[Importer un modèle de stratégie DLP personnalisé à partir d’un fichier](import-a-custom-dlp-policy-template-from-a-file-exchange-2013-help.md)

