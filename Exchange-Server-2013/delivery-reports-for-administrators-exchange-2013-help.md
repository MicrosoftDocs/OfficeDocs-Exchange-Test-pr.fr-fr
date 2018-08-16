---
title: 'Rapports de remise pour les administrateurs: Exchange 2013 Help'
TOCTitle: Rapports de remise pour les administrateurs
ms:assetid: d98623d3-e0b7-4cb9-93fb-6351b4a06137
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ919241(v=EXCHG.150)
ms:contentKeyID: 51407238
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Rapports de remise pour les administrateurs

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2016-12-09_

Grâce aux rapports de remise pour les administrateurs, vous pouvez assurer le suivi des informations de remise des messages envoyés ou reçus par une boîte aux lettres spécifique de votre organisation. Les rapports de remise pour les administrateurs utilisent le Centre d'administration Exchange (CAE) pour effectuer une recherche ciblée des journaux de suivi des messages. La recherche est toujours limitée à une boîte aux lettres spécifique. Vous pouvez rechercher des messages que la boîte aux lettres a envoyés ou reçus, et vous pouvez filtrer les résultats de la recherche par l'objet du message.

Le contenu du corps du message n'est pas renvoyé dans un rapport de remise, mais la ligne d'objet figure dans les résultats. Si vous souhaitez rechercher des messages électroniques spécifiques en fonction de leur contenu dans les boîtes aux lettres de votre organisation, consultez la rubrique [Découverte électronique locale](in-place-ediscovery-exchange-2013-help.md).

Les recherches des rapports de remise peuvent s'avérer utiles dans les situations suivantes :

  - Un responsable donne une mauvaise appréciation à un stagiaire, car celui-ci n'a pas remis son travail à temps. Le stagiaire insiste sur le fait qu'il a envoyé un message en y joignant le travail demandé. Le responsable vous demande de vérifier l'état du message.

  - Un bulletin de sécurité a été envoyé aux utilisateurs en leur demandant une réponse immédiate, mais personne n'a répondu. Est-ce qu'ils ignorent le message ou est-ce qu'ils ne l'ont tout simplement pas reçu ?

  - Des utilisateurs se plaignent du fait que personne ne reçoive leurs messages. Ils vérifient l'état de remise de leur courrier mais ne comprennent pas ce qui se passe. Il est possible qu'une règle soit appliquée aux messages au niveau de l'organisation.

Une fois que vous avez créé une recherche de rapport de remise, le rapport de remise résultant affiche les informations suivantes : expéditeurs et destinataires du message, ligne d'objet et date d'envoi du message. Le rapport de remise affiche également l'état de remise du message, ainsi que les raisons d'un éventuel retard ou échec de la remise.

## Plus d'informations sur les rapports de remise

  - Voici comment créer un rapport de remise : [Suivre les messages avec des rapports de remise](track-messages-with-delivery-reports-exchange-2013-help.md).

  - Les organisations Exchange locales peuvent utiliser l'environnement de ligne de commande Exchange Management Shell pour interroger les journaux de suivi des messages directement. Pour plus d'informations, consultez la rubrique [Recherche des journaux de suivi des messages](search-message-tracking-logs-exchange-2013-help.md).

  - Les utilisateurs peuvent effectuer le suivi de leurs propres messages. Pour plus d'informations, consultez la rubrique [Rapports de remise](https://go.microsoft.com/fwlink/?linkid=279920).

  - Si votre organisation comporte une version précédente d'Exchange, vous devez tenir compte du fonctionnement de la fonctionnalité de création de rapports de remise d'Exchange 2013 entre différentes version d'Exchange.
    
      - Les rapports de remise Exchange 2013 peuvent effectuer le suivi de messages sur différents serveurs Exchange 2010 au sein du même site Active Directory.
    
      - Les rapports de remise Exchange 2013 ne peuvent pas effectuer le suivi de messages sur différents serveurs Exchange 2007 au sein du même site Active Directory. La fonctionnalité de création de rapports de remise utilise un appel de procédure distant et une interface de service web qui n'existe pas dans Exchange 2007.

