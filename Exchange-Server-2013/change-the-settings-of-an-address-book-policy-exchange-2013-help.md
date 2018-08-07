---
title: 'Modifier les param. d’une stratégie de carnet d’adresses: Exchange 2013 Help'
TOCTitle: Modifier les paramètres d’une stratégie de carnet d’adresses
ms:assetid: ba1ca350-71c2-4c60-a612-33bfa9320b5e
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Hh529941(v=EXCHG.150)
ms:contentKeyID: 50478953
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Modifier les paramètres d’une stratégie de carnet d’adresses

 

_**Sapplique à :** Exchange Online, Exchange Server 2013_

_**Dernière rubrique modifiée :** 2016-03-30_

Après avoir créé une stratégie de carnet d’adresses, vous pouvez afficher ou modifier son nom, ainsi que la liste d’adresses globale, le carnet d’adresses en mode hors connexion, la liste de salles et les listes d’adresses affectés.

Si vous souhaitez rechercher des tâches de gestion supplémentaires relatives aux stratégies de carnet d’adresses, consultez la rubrique [Procédures des stratégies de carnet d’adresses](address-book-policy-procedures-exchange-2013-help.md).

## Ce qu’il faut savoir avant de commencer ?

  - Durée d'exécution estimée : Moins de 5 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Stratégies de carnet d’adresses » dans la rubrique [Autorisations pour configurer les adresses de messagerie et les carnets d’adresses](email-address-and-address-book-permissions-exchange-2013-help.md).

  - La création d’une stratégie de carnet d’adresses pour une organisation est un processus à étapes multiples qui requiert une planification. Pour plus d’informations, consultez la rubrique [Scénario : Déploiement de stratégies de carnet d’adresses](scenario-deploying-address-book-policies-exchange-2013-help.md)

  - Vous ne pouvez pas utiliser le Centre d’administration Exchange (EAC) pour configurer des stratégies de carnet d’adresses. Vous devez utiliser l'environnement de ligne de commande Exchange Management Shell.

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

  - Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), et [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

## Que souhaitez-vous faire ?

## Modifier le carnet d’adresses en mode hors connexion, la liste de salles et la liste d’adresses globale pour des stratégies de carnet d’adresses

Cet exemple modifie le carnet d’adresses en mode hors connexion, la liste de salles et la liste d’adresses globale qu’utiliseront les utilisateurs auxquels la stratégie de carnet d’adresses intitulée « All Fabrikam ABP » est affectée.

    Set-AddressBookPolicy -Identity "All Fabrikam ABP" -OfflineAddressBook \Fabrikam-OAB-2 -GlobalAddressList "\All Fabrikam GAL" -RoomList "\All Fabrikam Rooms"

## Remplacer des listes d’adresses dans une stratégie de carnet d’adresses

Les listes d’adresses que vous spécifiez pour une stratégie de carnet d’adresses existante remplacent toutes les listes d’adresses dans la stratégie de carnet d’adresses.

Cet exemple remplace les listes d’adresses existantes par les listes d’adresses intitulées GovernmentAgencyA-Atlanta et GovernmentAgencyA-Moscow pour LA stratégie de carnet d’adresses intitulée Government Agency A.

    Set-AddressBookPolicy -Identity "Government Agency A" -AddressLists "GovernmentAgencyA-Atlanta","GovernmentAgencyA-Moscow"

## Ajouter des listes d’adresses à une stratégie de carnet d’adresses

Pour conserver les listes d’adresses qui sont déjà définies dans une stratégie de carnet d’adresses, vous devez les spécifier lorsque vous en ajoutez des nouvelles à la stratégie.

Cet exemple montre comment ajouter la liste d’adresses Contoso-Chicago à la stratégie de carnet d’adresses ABP Contoso, qui est déjà configurée pour utiliser la liste d’adresses Contoso-Seattle.

    Set-AddressBookPolicy -Identity "ABP Contoso" -AddressLists "Contoso-Chicago","Contoso-Seattle"

## Supprimer des listes d’adresses d’une stratégie de carnet d’adresses

Pour supprimer des listes d’adresses existantes qui sont déjà définies dans une stratégie de carnet d’adresses, vous devez spécifier les listes d’adresses que vous souhaitez conserver.

Par exemple, la stratégie ABP Fabrikam utilise les listes d’adresses Fabrikam-HR et Fabrikam-Finance. Pour supprimer la liste d’adresses Fabrikam-HR de la stratégie, spécifiez la liste d’adresses Fabrikam-Finance que vous souhaitez conserver.

    Set-AddressBookPolicy -Identity "ABP Fabrikam" -AddressLists Fabrikam-Finance

## Pour plus d'informations

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Set-AddressBookPolicy](https://technet.microsoft.com/fr-fr/library/hh529945\(v=exchg.150\)).

