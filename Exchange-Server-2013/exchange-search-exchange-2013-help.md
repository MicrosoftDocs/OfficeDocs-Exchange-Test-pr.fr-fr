---
title: 'Service de recherche Exchange: Exchange 2013 Help'
TOCTitle: Service de recherche Exchange
ms:assetid: 967e2a13-4e54-486a-ac22-08768674abbb
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb232132(v=EXCHG.150)
ms:contentKeyID: 52063003
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Service de recherche Exchange

 

_**Sapplique à :**Exchange Server 2013_

_**Dernière rubrique modifiée :**2015-09-17_

La taille des boîtes aux lettres et la quantité de données qui y sont stockées sous forme de messages et de pièces jointes étant en constante augmentation, il est primordial que les utilisateurs soient en mesure de rechercher et de localiser rapidement les messages dont ils ont besoin. L'[Archivage inaltérable dans Exchange 2013](in-place-archiving-in-exchange-2013-exchange-2013-help.md) vous permet de réduire ou d'éliminer l'utilisation de fichiers .pst en déplaçant les éléments anciens et peu utilisés vers l'archive. L’utilisateur peut ainsi stocker plus de données de boîtes aux lettres et la recherche dans les boîtes aux lettres d’archivage et principale de l’utilisateur devient un outil de productivité essentiel. La [Découverte électronique locale](in-place-ediscovery-exchange-2013-help.md) permet aux utilisateurs autorisés de rechercher du contenu dans des boîtes aux lettres se trouvant dans des organisations Exchange locales et en nuage afin de satisfaire aux demandes de découverte électronique, aux audits de réglementation ou aux recherches internes. La découverte électronique locale utilise les index de contenu créés par le service de recherche Exchange.

Le service de recherche Exchange est différent de l'indexation de texte intégral disponible dans Exchange Server 2003. Des améliorations ont été apportées pour améliorer les performances, l'indexation du contenu et la recherche. De nouveaux éléments sont indexés presque immédiatement après leur création ou leur transmission à la boîte aux lettres, en offrant aux utilisateurs une méthode rapide, stable et plus fiable de recherche des données de boîte aux lettres. L'indexation du contenu est activée par défaut et aucune configuration initiale n'est requise.

Souhaitez-vous rechercher les tâches de gestion liées au service de recherche Exchange ? Consultez la rubrique [Procédures relatives au service de recherche Exchange](exchange-search-procedures-exchange-2013-help.md).

## Nouveautés

Les modifications suivantes sont apportées au service de recherche Exchange dans Exchange 2013 :

  - Le moteur d'indexation du contenu sous-jacent est remplacé par Microsoft Search Foundation, qui offre des performances et des fonctionnalités améliorées et constitue le moteur d'indexation de contenu sous-jacent standard dans Exchange et SharePoint. L'interface de gestion reste cependant identique.

  - Par défaut, Search Foundation gère les formats de fichiers de pièces jointes les plus courants. Il n'est plus nécessaire d'installer Microsoft Office Filter Packs pour Exchange Search. Pour obtenir une liste des formats de fichiers gérés par le service de recherche Exchange, consultez la rubrique [Formats de fichier indexés par le service de recherche Exchange](file-formats-indexed-by-exchange-search-exchange-2013-help.md).
    
    Vous pouvez ajouter la prise en charge d'autres formats de fichiers en installant IFilters, comme dans Exchange 2010.

  - L'indexation de contenu est plus efficace, car elle traite désormais les messages dans le pipeline de transport. Par conséquent, les messages adressés à plusieurs destinataires ou groupes de distribution ne sont traités qu'une fois. Un flux d'annotations est joint au message, ce qui accélère considérablement l'indexation de contenu tout en consommant moins de ressources.

