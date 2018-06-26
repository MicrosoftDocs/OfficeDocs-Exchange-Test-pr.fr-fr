---
title: 'Domaines: Exchange 2013 Help'
TOCTitle: Domaines
ms:assetid: 11748c2d-2e32-43a4-b77d-e0c17db6200b
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ673041(v=EXCHG.150)
ms:contentKeyID: 50477599
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Domaines

 

_**Sapplique à :**Exchange Server 2013, Office 365_

_**Dernière rubrique modifiée :**2012-10-11_

Les domaines représentent des espaces de noms SMTP pour lesquels vous configurez des répertoires de courriers électroniques et des boîtes aux lettres. En configurant les domaines qui interagissent avec votre organisation Microsoft Exchange Server 2013, vous pouvez configurer la façon dont les courriers électroniques et les divers domaines sont traités par Exchange.

## Domaines acceptés

Un domaine accepté désigne un espace de noms SMTP quelconque pour lequel votre organisation Exchange envoie ou reçoit des courriers électroniques. Parmi les domaines acceptés, on compte ceux pour lesquels l’organisation Exchange fait autorité, ainsi que les domaines de relais internes et externes. Une organisation Exchange fait autorité lorsqu'elle gère la remise des messages pour les destinataires dans le domaine accepté. Parmi les domaines acceptés, on compte également ceux pour lesquels l’organisation Exchange reçoit du courrier électronique, puis le relaie vers un serveur de messagerie en dehors de l’organisation.

Pour plus d’informations sur les domaines acceptés, consultez la rubrique [Domaines acceptés](accepted-domains-exchange-2013-help.md).

## Domaines distants

Dans Exchange 2013, vous pouvez créer des entrées de domaine distant pour définir les paramètres de transfert de messages entre votre organisation Exchange et des domaines à l’extérieur de votre organisation. Lorsque vous créez une entrée de domaine distant, vous contrôlez les types de messages envoyés à ce domaine. Vous pouvez également appliquer des stratégies de format de message et des jeux de caractères acceptables aux messages envoyés par des utilisateurs de votre organisation au domaine distant.

Les paramètres des domaines distants sont des paramètres de configuration globaux pour votre organisation Exchange. Les paramètres de domaine distant sont appliqués aux messages durant la catégorisation. Lors de la résolution de destinataire, le domaine du destinataire est comparé aux domaines distants configurés. Si une configuration de domaine distant bloque l’envoi d’un type de message particulier à des destinataires dans ce domaine, le message est supprimé. Si vous spécifiez un format de message particulier pour le domaine distant, les en-têtes et contenus des messages sont modifiés. Les paramètres s’appliquent à tous les messages traités par l’organisation Exchange.

Pour plus d'informations sur les domaines distants, consultez la rubrique [Domaines distants](remote-domains-exchange-2013-help.md).

