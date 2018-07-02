---
title: 'Création d’une stratégie de carnet d’adresses: Exchange 2013 Help'
TOCTitle: Création d’une stratégie de carnet d’adresses
ms:assetid: 6359abaf-e6f6-4667-8c2b-3860728b39a9
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Hh529931(v=EXCHG.150)
ms:contentKeyID: 50478327
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Création d’une stratégie de carnet d’adresses

 

_**Sapplique à :** Exchange Online, Exchange Server 2013_

_**Dernière rubrique modifiée :** 2014-12-16_

Les stratégies de carnet d'adresses vous permettent de segmenter des utilisateurs en groupes spécifiques pour fournir des vues personnalisées de la liste d'adresses globale de votre organisation. Lorsque vous créez une stratégie de carnet d'adresses, vous affectez une GAL, un carnet d'adresses en mode hors connexion, une liste de pièces ainsi qu'une ou plusieurs listes d'adresses à la stratégie. Vous pouvez alors attribuer la stratégie de carnet d'adresses à des utilisateurs de boîtes aux lettres et leur donner accès à une GAL personnalisée dans Outlook et Outlook Web App. L'objectif est de fournir un mécanisme plus simple de segmentation GAL pour des organisations locales nécessitant plusieurs GAL. Pour en savoir plus sur les carnets d'adresses en mode hors connexion, consultez la rubrique [Stratégies de carnet d’adresses](address-book-policies-exchange-2013-help.md).

Si vous souhaitez rechercher des tâches de gestion supplémentaires relatives aux stratégies de carnet d'adresses, consultez la rubrique [Procédures des stratégies de carnet d’adresses](address-book-policy-procedures-exchange-2013-help.md).

Les situations dans lesquelles cette procédure est utilisée vous intéressent ? Voir [Scénario : Déploiement de stratégies de carnet d’adresses](scenario-deploying-address-book-policies-exchange-2013-help.md).

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : Moins de 5 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Stratégies de carnet d’adresses » dans la rubrique [Autorisations pour configurer les adresses de messagerie et les carnets d’adresses](email-address-and-address-book-permissions-exchange-2013-help.md).

  - Par défaut dans Exchange Online, le rôle de liste d’adresses n’est affecté à aucun groupe de rôles. Pour utiliser les cmdlets nécessitant le rôle Liste d’adresses, vous devez ajouter ce dernier à un groupe de rôles. Pour plus d’informations, consultez la section « Ajouter un rôle à un groupe de rôles » de la rubrique [Gérer des groupes de rôles](manage-role-groups-exchange-2013-help.md).

  - La création d'une stratégie de carnet d'adresses pour une organisation est un processus à étapes multiples qui requiert une planification. Pour plus d'informations, consultez la rubrique [Scénario : Déploiement de stratégies de carnet d’adresses](scenario-deploying-address-book-policies-exchange-2013-help.md).

  - Vous ne pouvez pas utiliser le Centre d’administration Exchange (CAE) pour créer des stratégies de carnet d’adresses. Vous devez utiliser l’environnement de ligne de commande Exchange Management Shell.

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

  - Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), et [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour créer une stratégie de carnet d'adresses

Cet exemple crée une stratégie de carnet d'adresses avec les paramètres suivants :

  - **Nom** : Tous les fournisseurs de carnets d'adresses Fabrikam

  - **Liste d'adresses globale** : Tous les Fabrikam

  - **Carnet d'adresses en mode hors connexion** : Fabrikam-Tous-carnet d'adresses en mode hors connexion

  - **Liste de salles** : Toutes les salles Fabrikam

  - **Listes d'adresses** : All Fabrikam, All Fabrikam Mailboxes, All Fabrikam DLs et All Fabrikam Contacts

<!-- end list -->

    New-AddressBookPolicy -Name "All Fabrikam ABP" -AddressLists "\All Fabrikam","\All Fabrikam Mailboxes","\All Fabrikam DLs","\All Fabrikam Contacts" -OfflineAddressBook \Fabrikam-All-OAB -GlobalAddressList "\All Fabrikam" -RoomList "\All Fabrikam Rooms"

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, consultez la rubrique [New-AddressBookPolicy](https://technet.microsoft.com/fr-fr/library/hh529913\(v=exchg.150\)).

## Pour plus d'informations

[Attribuer une stratégie de carnet d’adresses à des utilisateurs de messagerie](assign-an-address-book-policy-to-mail-users-exchange-2013-help.md)

