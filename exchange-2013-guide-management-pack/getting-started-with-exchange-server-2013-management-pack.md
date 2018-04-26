---
title: Mise en route avec le pack d'administration Exchange Server 2013
TOCTitle: Mise en route avec le pack d'administration Exchange Server 2013
ms:assetid: 72d1609f-ab32-44d8-aa40-b1de587442d2
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dn195908(v=EXCHG.150)
ms:contentKeyID: 53275525
ms.date: 01/09/2015
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Mise en route avec le pack d'administration Exchange Server 2013

 

_**Dernière rubrique modifiée :** 2013-04-08_

Exchange Server 2013 Management Pack ajoute un conteneur dans la section **Analyse** de la console SCOM. Quand vous développez le conteneur Exchange Server 2013, vous remarquez qu'il ne compte que trois vues.

![Conteneurs du pack d'administration Exchange 2013](images/Dn195908.253b4ec5-2103-4b0c-a22e-5ebd24d08600(EXCHG.150).png "Conteneurs du pack d'administration Exchange 2013")

## Alertes actives – Exchange rencontre-t-il un problème ?

La vue **Alertes active** vous indique toutes les alertes déclenchées qui sont actuellement actives dans votre organisation Exchange. Vous pouvez cliquer sur n'importe quelle alerte pour afficher plus d'informations dans le volet d'informations. Cette vue vous donne principalement une réponse Oui/Non à la question « Mon déploiement Exchange rencontre-t-il un problème ? » Chaque alerte correspond à un ou plusieurs problèmes pour des informations d'intégrité particulières. Plusieurs alertes peuvent être déclenchées en fonction du problème en question.

## Intégrité de l'organisation – Quelles sont les conséquences ?

Si vous voyez une alerte dans la vue Alertes actives, vous devez tout d'abord vérifier la vue **Intégrité de l'organisation**. Il s'agit de la source d'informations principale concernant l'intégrité globale de votre organisation. Elle vous indique quel élément de votre organisation en particulier est touché, par exemple les sites Active Directory et les groupes de disponibilité de base de données.

![Intégrité de l'organisation](images/Dn195908.603c920b-7b88-4956-87d9-09d93fa6cba3(EXCHG.150).png "Intégrité de l'organisation")

## Intégrité du serveur – Sur quel serveur faut-il résoudre des problèmes ?

La vue **Intégrité du serveur** fournit des détails sur les serveurs individuels de votre organisation. Vous pouvez consulter l'intégrité individuelle de tous vos serveurs. ?À l'aide de cette vue, vous pouvez limiter les problèmes à un serveur particulier.

![Intégrité du serveur](images/Dn195913.c863be83-fc4b-4daf-a18b-27b1aae15b1d(EXCHG.150).png "Intégrité du serveur")

## Catégories d'analyse

En découvrant les trois vues du tableau de bord d'Exchange Server 2013, vous avez dû remarquer qu'en plus de la colonne **État**, trois autres indicateurs d'intégrité sont fournis.

![Indicateurs d'intégrité Exchange](images/Dn195908.dd10ed0b-abe5-41aa-8d43-b4fb10133984(EXCHG.150).png "Indicateurs d'intégrité Exchange")

Chacun d'eux vous donne une vue d'ensemble des aspects particuliers de votre déploiement Exchange.

  - **Points de contact du client** Cet indicateur montre ce que voient vos utilisateurs. Si cet indicateur est intègre, cela signifie que le problème est probablement sans conséquence pour vos utilisateurs. Par exemple, supposons qu'un membre de DAG rencontre des problèmes, mais que la base de données ait basculé correctement. Vous voyez dans ce cas des indicateurs non intègres pour ce DAG particulier, mais l'indicateur des points de contacts du client sont intègres, car les utilisateurs ne rencontrent pas d'interruption du service.

  - **Composants du service** Cet indicateur vous montre l'état du service particulier associé au composant. Par exemple, l'indicateur de composant du service pour OWA indique si l'ensemble du service OWA est intègre.

  - **Ressources du serveur** Cet indicateur montre l'état des ressources physiques qui ont des conséquences sur les fonctionnalités du serveur.

  - **Dépendances clés** Cet indicateur montre l'état des ressources externes dont dépend le déploiement Exchange, telles que la connectivité réseau, le DNS ou Active Directory.

Les vues du pack de gestion d'Exchange Server 2013 offrent une vue simple mais puissante qui permet de déterminer de manière simple et rapide si votre organisation est intègre. Cependant, les vues sont également structurées de manière à vous guider rapidement à la cause du problème en cas d'alerte. Pour en savoir plus sur l'utilisation d'Exchange Server 2013 Management Pack pour résoudre les problèmes, consultez la section [Utilisation du pack d'administration Exchange Server 2013 à des fins de dépannage](using-the-exchange-server-2013-management-pack-for-troubleshooting.md).

