---
title: 'Nouveautés des règles de transport: Exchange 2013 Help'
TOCTitle: Nouveautés des règles de transport
ms:assetid: 0c2fc0b5-3cd2-4d79-aa2b-0c7622ae15a8
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ150483(v=EXCHG.150)
ms:contentKeyID: 50477532
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Nouveautés des règles de transport

 

_**Sapplique à :** Exchange Online, Exchange Server 2013_

_**Dernière rubrique modifiée :** 2014-10-03_

Dans Microsoft Exchange Server 2013, plusieurs améliorations ont été apportées aux règles de transport. Cette rubrique décrit brièvement quelques-unes des principales modifications et améliorations apportées. Pour plus d’informations sur les règles de transport, consultez la rubrique [Règles de transport ou de flux de messagerie](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md).

## Prise en charge des stratégies de prévention des pertes de données (DLP, Data Loss Prevention)

Dans Exchange 2013, les fonctionnalités DLP peuvent aider les organisations à ne plus divulguer accidentellement de données sensibles. Les règles de transport ont été mises à jour pour prendre en charge la création de règles qui accompagnent et mettent en œuvre les stratégies DLP. Pour en savoir plus sur la prise en charge DLP dans les règles de transport, consultez les rubriques suivantes :

[Intégration des règles d'informations sensibles aux règles de transport](integrating-sensitive-information-rules-with-transport-rules-exchange-2013-help.md)

[Protection contre la perte de données](technical-overview-of-dlp-data-loss-prevention-in-exchange.md)

## Nouveaux prédicats et actions

La fonctionnalité des règles de transport a été étendue grâce à l’ajout de nouveaux prédicats et actions. Chaque prédicat répertorié ci-dessous peut être utilisé comme une condition ou une exception quand vous créez des règles de transport.

Pour obtenir des informations détaillées sur l’utilisation de ces nouveaux prédicats et actions, reportez-vous aux rubriques [Conditions de règles de transport (prédicats)](mail-flow-rule-conditions-and-exceptions-predicates-in-exchange-2013-exchange-2013-help.md) et [Actions de règle de transport](mail-flow-rule-actions-in-exchange-2013-exchange-2013-help.md).

## Nouveaux prédicats

  -  **AttachmentExtensionMatchesWords**   Utilisé pour détecter les messages contenant des pièces jointes avec des extensions spécifiques.

  -  **AttachmentHasExecutableContent**   Utilisé pour détecter les messages contenant des pièces jointes dont le contenu est exécutable.

  -  **HasSenderOverride** Utilisé pour détecter les messages dont l’expéditeur a choisi d’ignorer une restriction de stratégie DLP.

  -  **MessageContainsDataClassifications**   Utilisé pour détecter des informations sensibles dans le corps du message et les pièces jointes. Pour obtenir la liste complète des classifications de données disponibles, consultez la rubrique [Éléments recherchés par les types d’informations sensibles dans Exchange](what-the-sensitive-information-types-in-exchange-look-for-exchange-online-help.md).

  -  **MessageSizeOver**   Utilisé pour détecter des messages dont la taille globale est supérieure ou égale à la limite spécifiée.

  -  **SenderIPRanges**   Utilisé pour détecter les messages envoyés à partir d’un ensemble spécifique de plages d’adresses IP.

## Nouvelles actions

  -  **GenerateIncidentReport**   Génère un rapport de compte rendu d’incident qui est envoyé à l’adresse SMTP spécifiée. Cette action utilise également un paramètre appelé *IncidentReportOriginalMail* qui accepte l’une des deux valeurs suivantes : IncludeOriginalMail ou DoNotIncludeOriginalMail.

  -  **NotifySender**   Indique comment est notifié l’expéditeur d’un message qui ne respecte pas une stratégie DLP. Vous pouvez choisir d’informer l’expéditeur et d’acheminer le message normalement ou de rejeter le message et d’en notifier l’expéditeur.

  -  **StopRuleProcessing**   Interrompt le traitement de toutes les règles suivantes sur le message.

  -  **ReportSeverityLevel**   Définit le niveau de gravité spécifié dans le rapport de compte rendu d’incident. L’action peut avoir les valeurs suivantes : Informatif, Faible, Moyen, Élevé et Désactivé.

  -  **RouteMessageOutboundRequireTLS**   Requiert un chiffrement TLS (Transport Layer Security) lorsque ce message est acheminé à l’extérieur de votre organisation. Si le chiffrement TLS n’est pas pris en charge, le message est rejeté et n’est pas remis.

## Autres modifications apportées aux règles de transport

  - **Prise en charge de la syntaxe d’expression régulière étendue**   Dans Exchange 2013, les règles de transport reposent sur la fonctionnalité d’expression régulière (regex) de Microsoft.NET Framework et prennent maintenant en charge la syntaxe d’expression régulière étendue.

  - **Invocation de l’agent de règles de transport**   Dans Exchange 2013, la principale modification architecturale concernant les règles de transport est que l’agent de règles de transport est invoqué avec onResolvedMessage. Dans les versions antérieures d’Exchange, l’agent de règles était invoqué avec onRoutedMessage. Cette modification nous a permis d’ajouter de nouvelles actions, comme celle requérant un chiffrement TLS, pour changer la méthode d’acheminement d’un message. Pour en savoir plus sur l’architecture des règles de transport dans Exchange 2013, consultez la rubrique [Règles de transport ou de flux de messagerie](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md).

  - **Informations détaillées sur les règles de transport dans les journaux de suivi des messages**   Des informations détaillées sur les règles de transport figurent désormais dans les journaux de suivi des messages. Elles indiquent quelles règles ont été déclenchées pour un message spécifique et précisent les actions qui ont été prises une fois ces règles traitées.

  - **Nouvelle fonctionnalité de contrôle des règles**Exchange 2013 contrôle les règles de transport configurées et évalue leur coût d’exécution lorsque vous les créez, ainsi que dans le cadre d’un fonctionnement normal. Exchange peut détecter et générer des alertes pour les règles qui retardent la remise du courrier.

