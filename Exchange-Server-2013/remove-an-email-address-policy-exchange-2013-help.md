---
title: "Supprimer une stratégie d'adresses de messagerie: Exchange 2013 Help"
TOCTitle: Supprimer une stratégie d'adresses de messagerie
ms:assetid: f1d05223-7d41-406d-8fae-f4227be1c1c2
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb125181(v=EXCHG.150)
ms:contentKeyID: 50479519
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Supprimer une stratégie d'adresses de messagerie

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2012-10-13_

Par défaut, Exchange inclut une stratégie d'adresse de messagerie qui spécifie l'alias du destinataire comme partie locale de l'adresse de messagerie et utilise le domaine accepté par défaut. La partie locale d'une adresse de messagerie correspond au nom qui apparaît devant le signe @. Cette stratégie d'adresse de messagerie s'applique à tous les utilisateurs au sein de l'organisation. Vous ne pouvez pas supprimer cette stratégie.

Pour d'autres tâches de gestion relatives aux stratégies d'adresse de messagerie, voir [Procédures des stratégies d'adresse de messagerie](email-address-policy-procedures-exchange-2013-help.md).

## Que devez-vous savoir avant de commencer ?

  - Durée d'exécution estimée : 5 minutes.

  - Si vous supprimez une stratégie d'adresse de messagerie utilisée par les destinataires comme stratégie principale et si aucune autre stratégie n'est configurée pour les destinataires, la stratégie par défaut est utilisée.

  - Vous ne pouvez pas supprimer la stratégie par défaut. Si vous voulez supprimer la stratégie par défaut, vous devez d'abord affecter une autre stratégie comme stratégie par défaut.

  - Si la stratégie d'adresse de messagerie que vous supprimez contient plus de 3 000 destinataires, vous devez utiliser l'environnement de ligne de commande pour effectuer cette procédure.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Stratégies d’adresses de messagerie électronique » dans la rubrique [Adresses de messagerie et carnets d’adresses](email-addresses-and-address-books-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!WARNING]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.


## Que souhaitez-vous faire ?

## Utiliser le Centre d’administration Exchange (CAE) pour supprimer une stratégie d'adresse de messagerie

1.  Accédez à **Flux de messagerie** \> **Politiques d'adresse électronique**.

2.  Dans la liste affichée, sélectionnez la stratégie d'adresse de messagerie que vous souhaitez supprimer, puis cliquez sur **Supprimer**![Icône Supprimer](images/Dd979797.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "Icône Supprimer").

3.  Dans l'avertissement, cliquez sur **Oui** pour supprimer la stratégie.

## Utiliser l’environnement de ligne de commande pour supprimer une stratégie d'adresse de messagerie

Cet exemple supprime la stratégie d'adresse de messagerie South East Offices.

    Remove-EmailAddressPolicy -Identity "South East Offices"

Tapez **Y** pour confirmer la suppression de la stratégie, puis appuyez sur ENTRÉE.

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Remove-EmailAddressPolicy](https://technet.microsoft.com/fr-fr/library/bb124504\(v=exchg.150\)).

