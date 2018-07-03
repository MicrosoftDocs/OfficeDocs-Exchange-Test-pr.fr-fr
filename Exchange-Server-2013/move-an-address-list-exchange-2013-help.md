---
title: "Déplacer une liste d'adresses: Exchange 2013 Help"
TOCTitle: Déplacer une liste d'adresses
ms:assetid: c843bbd5-6c0e-41e1-b749-7ae87c1beb25
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb124534(v=EXCHG.150)
ms:contentKeyID: 50479156
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Déplacer une liste d'adresses

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2012-10-14_

Cette rubrique décrit le déplacement d’une liste d’adresses existante dans un nouveau conteneur sous la liste d’adresses racine.

Pour les autres tâches de gestion relatives aux listes d’adresses, voir [Procédures des listes d'adresses](address-list-procedures-exchange-2013-help.md).

## Ce qu’il faut savoir avant de commencer ?

  - Durée d’exécution estimée de chaque procédure : 5 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Listes d’adresses » dans la rubrique [Autorisations pour configurer les adresses de messagerie et les carnets d’adresses](email-address-and-address-book-permissions-exchange-2013-help.md).

  - Vous ne pouvez pas utiliser le Centre d’administration Exchange (CAE) pour effectuer cette procédure. Vous devez utiliser l'environnement de ligne de commande Exchange Management Shell.

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.


## Utiliser l'environnement de ligne de commande Exchange Management Shell pour déplacer une liste d'adresses

Cet exemple utilise le GUID de la liste d'adresses pour déplacer la liste d'adresses dans le conteneur Building 4, qui se trouve dans le conteneur All Users\\Sales.

    Move-AddressList -Identity c3fffd8e-026b-41b9-88c4-8c21697ac8ac -Target "\All Users\Sales\Building4"

Tapez **Y** pour confirmer le déplacement de cette liste d'adresses, puis appuyez sur ENTRÉE.

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Move-AddressList](https://technet.microsoft.com/fr-fr/library/bb124520\(v=exchg.150\)).

