---
title: 'Protection contre la perte de données: Exchange 2013 Help'
TOCTitle: Protection contre la perte de données
ms:assetid: 7c8ed3c1-ca91-4d9b-b16b-0a2b8ac89730
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ150527(v=EXCHG.150)
ms:contentKeyID: 50477277
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Protection contre la perte de données

 

_**Sapplique à :** Exchange Online, Exchange Server 2013_

_**Dernière rubrique modifiée :** 2016-12-09_

Découvrez les stratégies DLP dans Exchange Server 2013 et Exchange Online, notamment leur contenu et la façon de les tester. Vous allez également découvrir une nouvelle fonctionnalité dans Exchange DLP.

La protection contre la perte de données (Data loss prevention, DLP) est un élément important des systèmes de messagerie d'entreprise, en raison de l'utilisation massive du courrier électronique dans les communications stratégiques pour l'entreprise qui incluent des données sensibles. Afin de respecter les exigences de conformité liées à ces données et de gérer leur utilisation dans le courrier électronique sans diminuer la productivité des utilisateurs, les fonctions DLP rendent la gestion des données sensibles plus simple qu'elle ne l'a jamais été. Pour obtenir une vue d’ensemble conceptuelle de la protection contre la perte de données, regardez la vidéo suivante.

> [!VIDEO https://www.microsoft.com/fr-fr/videoplayer/embed/31f2b48e-93ed-4be3-b46d-e7230c0fed8f]

Les stratégies DLP sont des packages simples qui contiennent des groupes de conditions composés de règles de transport, d’actions et d’exceptions que vous créez dans le Centre d’administration Exchange (CAE), puis que vous activez pour filtrer les messages électroniques et les pièces jointes. Vous pouvez créer une stratégie DLP, mais choisir de ne pas l'activer. Cela vous permet de tester vos stratégies sans affecter le flux de messagerie. Les stratégies DLP peuvent utiliser toute la puissance des règles de transport existantes. En fait, plusieurs nouveaux types de règles de transport ont été créés dans Microsoft Exchange Server 2013 et Exchange Online afin d'implémenter la nouvelle fonctionnalité DLP. Une nouvelle fonctionnalité importante des règles de transport consiste en une nouvelle approche de classification des informations sensibles pouvant être intégrée au processus de flux de messagerie. Cette nouvelle fonctionnalité DLP effectue une analyse en profondeur du contenu via des correspondances de mot clé, des correspondances de dictionnaire, l'évaluation d'expressions standard et d'autres examens de contenu en vue de détecter le contenu non conforme aux stratégies DLP de l'organisation. Dans la dernière version d’Exchange Online et d’Exchange 2013 SP1, la [Création d’une empreinte numérique de document](https://docs.microsoft.com/fr-fr/exchange/security-and-compliance/data-loss-prevention/document-fingerprinting) a été ajoutée, ce qui vous permet de détecter des informations sensibles dans des formulaires standard. Pour plus d'informations sur les règles de transport, consultez les rubriques [Règles de transport ou de flux de messagerie](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md) (Exchange 2013) ou [Règles de flux de messagerie (règles de transport) dans Exchange Online](https://technet.microsoft.com/fr-fr/library/jj919238\(v=exchg.150\)) (Exchange Online) et [Intégration des règles d'informations sensibles aux règles de transport](https://docs.microsoft.com/fr-fr/exchange/security-and-compliance/data-loss-prevention/integrate-sensitive-information-rules). Vous pouvez aussi gérer vos stratégies DLP par le biais des cmdlets Exchange Management Shell. Pour plus d'informations sur les cmdlets de stratégie et de conformité, consultez la rubrique [Cmdlets de stratégie et de conformité](https://technet.microsoft.com/fr-fr/library/dd298082\(v=exchg.150\)).

En plus des stratégies DLP personnalisables elles-mêmes, vous pouvez aussi informer les expéditeurs de messages électroniques qu'ils sont peut-être sur le point de ne pas respecter l'une de vos stratégies, avant même qu'ils envoient un message gênant. Pour ce faire, configurez les conseils de stratégie. Les conseils de stratégie sont similaires aux infos-courrier et peuvent être configurés pour présenter une courte note dans le client Microsoft Outlook 2013 qui fournit des informations sur les violations de stratégie possibles à une personne créant un message. Dans la dernière version d’Exchange Online et d’Exchange 2013 SP1, les conseils de stratégie sont également affichés dans Outlook Web App et OWA pour les périphériques. Pour plus d'informations, consultez la rubrique [Conseils de stratégie](https://docs.microsoft.com/fr-fr/exchange/security-and-compliance/data-loss-prevention/policy-tips).

> [!NOTE]
> Exchange Online : la protection contre la perte de données est une fonctionnalité étendue qui nécessite une licence Exchange Online Plan 2. Pour plus d’informations, voir <a href="https://go.microsoft.com/fwlink/p/?linkid=286154">Licences Exchange Online</a>.<br />
Exchange 2013 : la protection contre la perte de données est une fonctionnalité étendue qui nécessite une licence d’accès client (CAL) Exchange Enterprise. Pour plus d’informations sur les licences d’accès client et les licences par serveur, consultez la rubrique <a href="https://go.microsoft.com/fwlink/p/?linkid=237292">Licences Exchange Server</a>.<br />
> <strong>Licence d'accès client Exchange Enterprise avec Services :</strong> Vous devez prendre note d'une distinction de comportement si vous êtes un client Licence d'accès client Exchange Enterprise avec Services et que vous mettez en place un déploiement hybride, dans lequel certaines boîtes aux lettres se trouvent en local et d'autres dans Exchange Online. Les stratégies DLP sont appliquées dans Exchange Online. Par conséquent, les stratégies DLP ne s’appliquent pas aux messages envoyés par un utilisateur sur site à un autre, car ces messages ne quittent pas l’infrastructure sur site.


Recherchez-vous les tâches de gestion relatives à la protection contre la perte de données ? Consultez [Procédures relatives à la protection contre la perte de données (DLP)](dlp-procedures-exchange-2013-help.md) (Exchange 2013) ou [Procédures relatives à la protection contre la perte de données (DLP)](https://technet.microsoft.com/fr-fr/library/jj938003\(v=exchg.150\)) (Exchange Online).

**Contenu de cette rubrique**

Établir des stratégies visant à protéger les données sensibles

Types d'informations sensibles dans les stratégies DLP

Détection des informations sensibles avec la classification des messages traditionnelle

Détection de données de formulaire sensibles avec l’empreinte numérique de document

Les conseils de stratégie indiquent aux utilisateurs les attentes en termes de contenu sensible

Informations sur les messages traités par DLP

Conditions préalables à l'installation

Pour plus d'informations

## Établir des stratégies visant à protéger les données sensibles

Les fonctions de protection contre la perte de données peuvent vous aider à identifier et surveiller de nombreuses catégories d'informations sensibles que vous avez définies dans les conditions de vos stratégies, comme les numéros d'identification privée ou les numéros de carte de crédit. Vous avez la possibilité de définir vos propres stratégies personnalisées et règles de transport ou d'utiliser les modèles de stratégie DLP prédéfinis fournis par Microsoft pour commencer rapidement. Pour plus d'informations sur les modèles de stratégie inclus, consultez la rubrique [Modèles de stratégies DLP fournis dans Exchange](https://docs.microsoft.com/fr-fr/exchange/security-and-compliance/data-loss-prevention/dlp-policy-templates). Un *modèle de stratégie* inclut un ensemble de conditions, de règles et d'actions que vous pouvez choisir pour créer et enregistrer une stratégie DLP qui vous aidera à inspecter les messages. Les modèles de stratégie sont des modèles à partir desquels vous pouvez sélectionner ou créer vos propres règles spécifiques, de façon à créer une stratégie répondant à vos besoins en matière de protection contre la perte de données.

Il existe trois différentes méthodes pour commencer à utiliser DLP :

1.  **Appliquer un modèle prêt à l'emploi fourni par Microsoft.**   Le moyen le plus rapide de commencer à utiliser les stratégies DLP est de créer et d'implémenter une nouvelle stratégie à l'aide d'un modèle. Cela vous évite de devoir créer intégralement un nouveau groupe de règles. Vous devez déterminer le type de données à contrôler ou la règle de conformité à vérifier. Vous devez également connaître les attentes de votre organisation en matière de traitement de ces données. Pour plus d'informations, consultez les rubriques [Modèles de stratégies DLP fournis dans Exchange](https://docs.microsoft.com/fr-fr/exchange/security-and-compliance/data-loss-prevention/dlp-policy-templates) et [Création d'une stratégie DLP à partir d'un modèle](https://docs.microsoft.com/fr-fr/exchange/security-and-compliance/data-loss-prevention/create-dlp-policy-from-template).

2.  **Importer un fichier de stratégie prégénéré de l'extérieur de votre organisation.**   Vous pouvez importer des stratégies qui ont déjà été créées à l'extérieur de votre environnement de messagerie par des éditeurs de logiciels indépendant. De cette façon, vous pouvez étendre les solutions DLP qui répondent aux besoins de votre entreprise. Pour plus d'informations, consultez les rubriques [Modèles de stratégie des partenaires Microsoft](policy-templates-from-microsoft-partners-exchange-2013-help.md), [Définition de vos modèles DLP et types d'informations](define-your-own-dlp-templates-and-information-types-exchange-2013-help.md) et [Importer un modèle de stratégie DLP personnalisé à partir d’un fichier](import-a-custom-dlp-policy-template-from-a-file-exchange-2013-help.md).

3.  **Créer une stratégie personnalisée sans conditions préexistantes.**   Votre entreprise peut avoir ses propres exigences de surveillance de certains types de données généralement présents dans un système de messagerie. Vous pouvez créer intégralement une stratégie personnalisée afin de commencer à vérifier vos propres données de messages uniques et à agir sur ces dernières. Afin de créer la stratégie personnalisée, vous devrez connaître les exigences et les contraintes de l'environnement dans lequel la stratégie DLP sera appliquée. Pour plus d'informations, consultez les rubriques [Création d'une stratégie personnalisée de protection contre la perte de données (DLP)](https://docs.microsoft.com/fr-fr/exchange/security-and-compliance/data-loss-prevention/create-custom-dlp-policy).

Après avoir ajouté une stratégie, vous pouvez vérifier et modifier ses règles, la désactiver ou la supprimer complètement. Les procédures permettant de réaliser ces actions sont indiquées dans la rubrique [Gestion de stratégies de protection contre la perte de données (DLP)](manage-dlp-policies-exchange-2013-help.md).

## Types d'informations sensibles dans les stratégies DLP

Lorsque vous créez ou modifiez des stratégies DLP, vous pouvez inclure des règles qui comportent des vérifications d'informations sensibles. Les types d'informations sensibles répertoriés dans la rubrique [Éléments recherchés par les types d’informations sensibles dans Exchange](what-the-sensitive-information-types-in-exchange-look-for-exchange-online-help.md) peuvent être utilisés dans vos stratégies. Les conditions que vous établissez dans une stratégie, comme le nombre de fois qu'un élément doit être trouvé pour réaliser une action ou encore le contenu exact de cette action, peuvent être personnalisées dans vos nouvelles stratégies personnalisées afin de répondre à vos exigences de stratégies spécifiques. Pour plus d'informations sur la création de stratégies DLP, consultez la rubrique [Création d'une stratégie personnalisée de protection contre la perte de données (DLP)](https://docs.microsoft.com/fr-fr/exchange/security-and-compliance/data-loss-prevention/create-custom-dlp-policy). Pour plus d'informations sur l'ensemble complet des règles de transport, consultez la rubrique [Règles de transport ou de flux de messagerie](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md) (Exchange 2013) ou [Règles de flux de messagerie (règles de transport) dans Exchange Online](https://technet.microsoft.com/fr-fr/library/jj919238\(v=exchg.150\)) (Exchange Online).

Pour que vous puissiez utiliser facilement les règles associées aux informations sensibles, Microsoft a fourni des modèles de stratégie qui incluent déjà certains types d'informations sensibles. Cependant, vous ne pouvez pas ajouter de conditions aux modèles de stratégie pour tous les types d'informations sensibles répertoriés ici, car les modèles sont conçus pour vous aider à cibler les types les plus courants de données de conformité dans votre organisation. Pour plus d'informations sur les modèles prégénérés, consultez la rubrique [Modèles de stratégies DLP fournis dans Exchange](https://docs.microsoft.com/fr-fr/exchange/security-and-compliance/data-loss-prevention/dlp-policy-templates). Vous pouvez créer de nombreuses stratégies DLP pour votre organisation et les activer toutes de façon à examiner divers types d'informations. Vous pouvez aussi créer une stratégie DLP qui n'est pas basée sur un modèle existant. Pour commencer la création de cette stratégie, consultez la rubrique [Création d'une stratégie personnalisée de protection contre la perte de données (DLP)](https://docs.microsoft.com/fr-fr/exchange/security-and-compliance/data-loss-prevention/create-custom-dlp-policy). Pour plus d'informations sur les types d'informations sensibles, consultez la rubrique [Éléments recherchés par les types d’informations sensibles dans Exchange](what-the-sensitive-information-types-in-exchange-look-for-exchange-online-help.md).

## Détection de données de formulaire sensibles avec l’empreinte numérique de document

Avec Exchange 2013 SP1 et la dernière version d’Exchange Online, vous pouvez utiliser la [Création d’une empreinte numérique de document](https://docs.microsoft.com/fr-fr/exchange/security-and-compliance/data-loss-prevention/document-fingerprinting) afin de créer facilement un type d’informations sensibles basé sur un formulaire standard. Pour découvrir comment protéger les données de formulaire, consultez la rubrique [Protection des données de formulaire avec la création d’une empreinte numérique de document](https://docs.microsoft.com/fr-fr/exchange/security-and-compliance/data-loss-prevention/protect-data-with-fingerprinting).

## Les conseils de stratégie indiquent aux utilisateurs les attentes en termes de contenu sensible

Vous pouvez utiliser les messages de notification de conseils de stratégie pour informer les expéditeurs de messages de possibles problèmes de conformité lorsqu'ils composent un message électronique. Lorsque vous configurez un conseil de stratégie dans une stratégie DLP, le message de notification ne s’affiche que si un élément dans le message électronique de l’expéditeur répond aux conditions décrites dans votre stratégie. Les conseils de stratégie sont semblables aux infos-courrier introduites dans Microsoft Exchange 2010. Pour plus d'informations, consultez la rubrique [Conseils de stratégie](https://docs.microsoft.com/fr-fr/exchange/security-and-compliance/data-loss-prevention/policy-tips).

## Détection des informations sensibles avec la classification des messages traditionnelle

Exchange 2013 et Exchange Online intègrent une nouvelle méthode qui vous aide à gérer les données de message et de pièce jointe en les comparant à la classification des messages traditionnelle. Un facteur essentiel de la puissance d'une solution DLP est la possibilité d'identifier correctement le contenu confidentiel ou sensible pouvant être spécifique à l'organisation, aux exigences réglementaires, à la géographie ou à d'autres exigences métier. Exchange 2013 permet cette identification via une nouvelle architecture analysant le contenu en profondeur et couplée à des critères de détection que vous définissez grâce aux règles de vos stratégies DLP. La protection contre la perte de données dans Exchange 2013 repose sur la configuration d'un ensemble correct de règles d'informations sensibles, visant à fournir un haut degré de protection tout en diminuant la perturbation du flux de messagerie avec des faux positifs et des faux négatifs. Ces types de règles, appelés détection des informations sensibles au sein des informations DLP, fonctionnent dans la structure fournie par les règles de transport de façon à activer les fonctionnalités DLP.

Pour en savoir plus sur ces nouvelles fonctionnalités, consultez la rubrique [Intégration des règles d'informations sensibles aux règles de transport](https://docs.microsoft.com/fr-fr/exchange/security-and-compliance/data-loss-prevention/integrate-sensitive-information-rules). Les champs de la classification des messages traditionnelle peuvent toujours être appliqués aux messages dans Exchange et peuvent être combinés avec la nouvelle détection des informations sensibles, soit ensemble dans une stratégie DLP unique, soit simultanément afin d'être évalués indépendamment dans Exchange. Pour en savoir plus sur les classifications des messages Exchange 2010 héritées, consultez la rubrique [Présentation des classifications des messages](https://go.microsoft.com/fwlink/?linkid=266612) dans la bibliothèque TechNet.

## Informations sur les messages traités par DLP

Pour qu'Exchange 2013 obtienne des informations sur les messages et les détections de stratégies DLP dans votre environnement, consultez les rubriques [Afficher les rapports de détection de stratégies DLP](view-dlp-policy-detection-reports-exchange-2013-help.md) et [Créer des rapports de compte-rendu d’incident pour la détection de stratégies DLP](create-incident-reports-for-dlp-policy-detections-exchange-2013-help.md). Les données associées aux détections DLP sont hautement intégrées à l'outil de suivi des messages de rapports de remise d'Exchange 2013.

Pour Exchange Online, consultez les rubriques [Afficher les rapports de détection de stratégies DLP](https://technet.microsoft.com/fr-fr/library/dn904484\(v=exchg.150\)) et [Créer des rapports d’incident pour la détection de stratégies DLP](https://technet.microsoft.com/fr-fr/library/dn904486\(v=exchg.150\)).

## Conditions préalables à l'installation

Pour pouvoir utiliser les fonctions DLP, Exchange 2013 ou Exchange Online doit être configuré avec au moins une boîte aux lettres d'expéditeur. La protection contre la perte de données est une fonctionnalité étendue qui nécessite une licence d'accès client (CAL) Entreprise. Pour plus d'informations sur la prise en main d'Exchange 2013, consultez la rubrique [Planification et déploiement](planning-and-deployment-for-exchange-2013-installation-instructions.md). Pour plus d'informations sur la prise en main d'Exchange Online, consultez la rubrique [Exchange Online](https://technet.microsoft.com/fr-fr/library/jj200580\(v=exchg.150\)).

## Pour plus d'informations

Exchange 2013

  - [Stratégie et conformité de messagerie](messaging-policy-and-compliance-exchange-2013-help.md)

  - [Procédures relatives à la protection contre la perte de données (DLP)](dlp-procedures-exchange-2013-help.md)

  - [Afficher les rapports de détection de stratégies DLP](view-dlp-policy-detection-reports-exchange-2013-help.md)

  - [Création d’une empreinte numérique de document](https://docs.microsoft.com/fr-fr/exchange/security-and-compliance/data-loss-prevention/document-fingerprinting)

  - [Cmdlets de stratégie et de conformité](https://technet.microsoft.com/fr-fr/library/dd298082\(v=exchg.150\))

Exchange Online

  - [Sécurité et conformité pour Exchange Online](https://technet.microsoft.com/fr-fr/library/jj200706\(v=exchg.150\))

  - [Procédures relatives à la protection contre la perte de données (DLP)](https://technet.microsoft.com/fr-fr/library/jj938003\(v=exchg.150\))

  - [Afficher les rapports de détection de stratégies DLP](https://technet.microsoft.com/fr-fr/library/dn904484\(v=exchg.150\))

  - [Création d’une empreinte numérique de document](https://docs.microsoft.com/fr-fr/exchange/security-and-compliance/data-loss-prevention/document-fingerprinting)

