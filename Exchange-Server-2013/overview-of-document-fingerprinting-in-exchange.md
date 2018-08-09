---
title: 'Présentation de la création d’empreinte numérique de document dans Exchange'
TOCTitle: Création d’une empreinte numérique de document
ms:assetid: 1e0c579c-26e0-462a-a1b0-d7506dfe05fa
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dn635176(v=EXCHG.150)
ms:contentKeyID: 61204567
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Création d’une empreinte numérique de document

 

_**Sapplique à :** Exchange Online, Exchange Server 2013_

_**Dernière rubrique modifiée :** 2014-09-11_

Les professionnels de l’informatique de votre organisation gèrent toutes sortes d’informations sensibles au cours d’une journée typique. La *création d’une empreinte numérique de document* facilite la protection de ces informations en identifiant les formulaires standard utilisés au sein de votre organisation. Cette rubrique décrit les concepts de la création d’une empreinte numérique de document. Si vous souhaitez apprendre à créer une empreinte numérique de document, consultez la rubrique [Protection des données de formulaire avec la création d’une empreinte numérique de document](protect-form-data-with-document-fingerprinting-exchange-2013-help.md).

## Scénario de base de création d’une empreinte numérique de document

La création d’une empreinte numérique de document est une fonctionnalité de protection contre la perte de données (DLP) qui permet de convertir un formulaire standard en un type d’informations sensibles que vous pouvez utiliser pour définir des règles de transport et des stratégies DLP. Par exemple, vous pouvez créer une empreinte numérique de document basée sur un modèle de brevet vierge, puis créer une stratégie DLP qui détecte et bloque tous les modèles de brevet sortants comportant des informations sensibles. Vous pouvez éventuellement configurer des [Conseils de stratégie](technical-overview-of-policy-tips-in-exchange-online-and-exchange-2013.md) afin d’informer les expéditeurs qu’ils pourraient être en train d’envoyer des informations sensibles et qu’ils doivent vérifier que les bénéficiaires sont habilités à recevoir les brevets. Ce processus fonctionne avec n’importe quel formulaire texte utilisé dans votre organisation. Voici d’autres exemples de formulaires que vous pouvez télécharger :

  - Formulaires officiels

  - Formulaires de conformité relatifs à la loi américaine HIPAA (Health Insurance Portability Accountability Act)

  - Formulaires d’informations sur les employés pour les services de ressources humaines

  - Formulaires personnalisés créés spécialement pour votre organisation

Dans l’idéal, votre organisation a pour habitude professionnelle d’utiliser certains formulaires pour la transmission d’informations sensibles. Après avoir téléchargé un formulaire vide pour le convertir en empreinte numérique de document et avoir configuré la stratégie correspondante, l’agent DLP détecte tous les documents dans le courrier sortant qui correspondent à cette empreinte.

## Fonctionnement de l’empreinte numérique de document

Vous avez probablement déjà deviné que les documents n’ont pas d’empreintes digitales réelles, mais le nom contribue à expliquer la fonctionnalité. De la même manière que les empreintes digitales d’une personne répondent à des modèles uniques, les documents répondent à des modèles de mots uniques. Lorsque vous téléchargez un fichier, l’agent DLP identifie le modèle de mots unique dans le document, crée une empreinte numérique de document basée sur ce modèle et utilise cette empreinte pour détecter les documents sortants contenant le même modèle. C’est pourquoi le téléchargement d’un formulaire ou d’un modèle permet de créer le type d’empreinte numérique de document le plus efficace. Toute personne qui remplit un formulaire utilise le même ensemble de mots d’origine, puis ajoute ses propres mots au document. Tant que le document sortant n’est pas protégé par mot de passe et qu’il contient l’intégralité du texte du formulaire d’origine, l’agent DLP peut déterminer si le document correspond à l’empreinte numérique de document.

L’exemple suivant montre ce qui se passe si vous créez une empreinte numérique de document basée sur un modèle de brevet, mais vous pouvez utiliser n’importe quel formulaire comme base pour la création d’une empreinte numérique de document.

**Exemple d’un document de brevet correspondant à l’empreinte numérique de document d’un modèle de brevet**

![Brevet correspondant à une empreinte de document.](images/Dn635176.9c952770-2cd4-4f62-9735-6d073344be7f(EXCHG.150).png "Brevet correspondant à une empreinte de document.")

Le modèle de brevet contient les champs vides « Titre du brevet », « Inventeurs » et « Description », ainsi que des descriptions pour chacun de ces champs ; ces éléments constituent le modèle de mots. Lorsque vous téléchargez le modèle de brevet d’origine, il est dans l’un des types de fichier pris en charge et en texte brut. L’agent DLP utilise un algorithme pour convertir ce modèle de mots en empreinte numérique de document. Il s’agit d’un petit fichier XML Unicode contenant une valeur de hachage unique représentant le texte d’origine. L’empreinte numérique est ensuite enregistrée en tant que classification des données dans Active Directory. (Par mesure de sécurité, le document d’origine n’est pas stocké sur le service ; seule la valeur de hachage est stockée et le document d’origine ne peut pas être recréé à partir de la valeur de hachage.) L’empreinte numérique de brevet devient alors un type d’informations sensibles que vous pouvez associer à une stratégie DLP. Après avoir associé l’empreinte numérique à une stratégie DLP, l’agent DLP détecte les messages électroniques sortants contenant des documents correspondant à l’empreinte numérique de brevet et les traite conformément à la stratégie de votre organisation. Par exemple, vous voudrez peut-être configurer une stratégie DLP qui empêche certains employés d’envoyer des messages sortants contenant des brevets. L’agent DLP utilise l’empreinte numérique de brevet pour détecter des brevets et bloquer ces messages électroniques. Vous voudrez peut-être également laisser à votre service juridique la possibilité d’envoyer des brevets à d’autres organisations pour des raisons professionnelles. Vous pouvez autoriser des services spécifiques à envoyer des informations sensibles en créant des exceptions pour ces services dans votre stratégie DLP ou vous pouvez leur permettre de passer outre un conseil de stratégie s’ils disposent d’une justification. Pour plus d’informations sur la création d’exceptions et de règles de stratégie DLP, consultez la rubrique [Procédures relatives à la protection contre la perte de données (DLP)](https://technet.microsoft.com/fr-fr/library/jj938003\(v=exchg.150\)) et pour en savoir plus sur la configuration de conseils de stratégie dont les utilisateurs peuvent ne pas tenir compte, consultez l’article [Gérer les conseils de stratégie](how-to-configure-and-manage-policy-tips-a-dlp-feature-exchange.md).

## Types de fichiers pris en charge

L’empreinte numérique de document prend en charge les mêmes types de fichier que ceux pris en charge dans les règles de transport. Pour obtenir la liste des types de fichier pris en charge, voir [Utiliser des règles de flux de messagerie pour analyser les pièces jointes des messages](https://technet.microsoft.com/fr-fr/library/jj919236\(v=exchg.150\)). Remarque rapide concernant les types de fichiers : ni les règles de transport ni la création d’empreinte numérique de document ne prend en charge le type de fichier .dotx, ce qui peut porter à confusion, car il s’agit d’un fichier de modèle dans Word Lorsque vous voyez le mot « modèle » dans cette rubrique et d’autres rubriques relatives à la création d’une empreinte numérique de document, il fait référence à un document que vous avez établi en tant que formulaire standard, et non au type de fichier de modèle.

## Limites de l’empreinte numérique de document

L’agent DLP d’empreinte numérique de document ne détectera pas les informations sensibles dans les cas suivants :

  - Si les fichiers sont protégés par mot de passe

  - Si les fichiers contiennent uniquement des images

  - Si les documents ne contiennent pas l’intégralité du texte du formulaire d’origine utilisé pour créer l’empreinte numérique de document

## Pour plus d’informations

[Protection des données de formulaire avec la création d’une empreinte numérique de document](protect-form-data-with-document-fingerprinting-exchange-2013-help.md)

[Intégration des règles d'informations sensibles aux règles de transport](integrating-sensitive-information-rules-with-transport-rules-exchange-2013-help.md)

[Procédures relatives à la protection contre la perte de données (DLP)](https://technet.microsoft.com/fr-fr/library/jj938003\(v=exchg.150\))

