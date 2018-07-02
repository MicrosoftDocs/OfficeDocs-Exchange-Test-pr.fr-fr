---
title: 'Stratégies de boîte aux lettres de messagerie unifiée: Exchange 2013 Help'
TOCTitle: Stratégies de boîte aux lettres de messagerie unifiée
ms:assetid: dfae629e-ee89-4494-a3ed-9655b67eb87e
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb124909(v=EXCHG.150)
ms:contentKeyID: 50555508
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Stratégies de boîte aux lettres de messagerie unifiée

 

_**Sapplique à :**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :**2012-11-15_

Des stratégies de boîtes aux lettres de messagerie unifiée sont requises lorsque vous activez des utilisateurs pour la messagerie unifiée. Vous créez des stratégies de boîte aux lettres de messagerie unifiée pour appliquer un ensemble commun de stratégies ou de paramètres de sécurité à une collection de boîtes aux lettres d’utilisateurs de la messagerie vocale. Les stratégies de boîtes aux lettres de messagerie unifiée permettent de spécifier des paramètres de messagerie unifiée, comme suit :

  - Stratégies de code confidentiel

  - Restrictions de numérotation

  - Autres propriétés générales de stratégies de boîte aux lettres de messagerie unifiée

Par exemple, vous pouvez créer une stratégie de boîte aux lettres de messagerie unifiée pour augmenter le niveau de sécurité du code confidentiel en réduisant le nombre maximal d'échecs de connexion pour un groupe spécifique d'utilisateurs à messagerie unifiée, tel que les cadres.

## Stratégies de boîte aux lettres de messagerie unifiée

Vous devez avoir créé au moins une stratégie de boîtes aux lettres unifiée avant de pouvoir activer des utilisateurs pour la messagerie unifiée. Vous pouvez créer des stratégies de boîtes aux lettres de messagerie unifiée pour appliquer un ensemble commun de paramètres à des groupes d’utilisateurs.

Vous pouvez créer des stratégies de boîtes aux lettres de messagerie unifiée à l’aide de l’environnement de ligne de commande Exchange Management Shell ou du Centre d’administration Exchange (EAC). Par défaut, une stratégie de boîte aux lettres de messagerie unifiée est créée après la création d’un plan de numérotation de messagerie unifiée. La nouvelle stratégie de boîte aux lettres de messagerie unifiée est automatiquement associée au plan de numérotation de messagerie unifiée et une partie du nom de ce dernier est incluse dans le nom complet de la stratégie de boîte aux lettres de messagerie unifiée. Vous pouvez modifier cette stratégie de boîtes aux lettres de messagerie unifiée par défaut.

Plusieurs utilisateurs à messagerie unifiée peuvent être reliés à une même stratégie de boîte aux lettres de messagerie unifiée. Notez que la boîte aux lettres de chaque utilisateur à extension messagerie unifiée doit être liée à une seule stratégie de boîte aux lettres de messagerie unifiée. Cela permet de contrôler les paramètres de sécurité du code confidentiel, comme le nombre minimal de chiffres dans un code confidentiel ou le nombre maximal de tentatives d’ouverture de session pour les utilisateurs à extension messagerie unifiée qui sont associés à la stratégie de boîte aux lettres de messagerie unifiée. Vous pouvez également contrôler des paramètres de texte de messages ou de restriction de numérotation pour les mêmes boîtes aux lettres à extension messagerie unifiée.

