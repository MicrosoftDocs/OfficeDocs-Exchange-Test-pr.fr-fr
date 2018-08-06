---
title: 'Supprimer une recherche de découverte électr. inaltérable: Exchange 2013 Help | Microsoft Docs'
TOCTitle: Suppression d’une recherche de découverte électronique inaltérable
ms:assetid: 78461a78-1255-4a26-9d36-c6b8eb82a4f9
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dd298078(v=EXCHG.150)
ms:contentKeyID: 50478505
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Suppression d’une recherche de découverte électronique inaltérable

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2014-07-14_

Dans Microsoft Exchange Server 2013, vous pouvez utiliser la découverte électronique locale pour rechercher un contenu de boîte aux lettres. Vous pouvez supprimer une recherche de découverte électronique locale à tout moment. Lorsque vous supprimez une recherche de découverte électronique locale, les résultats de recherche sont supprimés de la boîte aux lettres de découverte.

> [!CAUTION]
> La suppression d'une recherche de découverte électronique locale supprime les résultats de recherche copiés vers une boîte aux lettres de découverte.


## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : 2 à 5 minutes.

  - Pour supprimer une recherche de découverte électronique locale pour laquelle l'archive permanente est activée, vous devez d'abord supprimer l'archive permanente de la recherche. Pour plus d'informations, consultez la rubrique [Créer ou supprimer une conservation inaltérable](create-or-remove-an-in-place-hold-exchange-2013-help.md).

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l'entrée « Découverte électronique locale » dans la rubrique [Stratégie de messagerie et autorisations de conformité](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

## Que souhaitez-vous faire ?

## Utiliser le Centre d'administration Exchange (CAE) pour supprimer une recherche de découverte électronique locale

1.  Accédez à **Gestion de la conformité** \> **Découverte électronique et archives locales**.

2.  Dans l'affichage Liste, sélectionnez la recherche de découverte électronique locale à supprimer, puis cliquez sur **Supprimer**![Icône Supprimer](images/Dd979797.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "Icône Supprimer").

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour supprimer une recherche de découverte électronique locale

Exemples

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez correctement supprimé une recherche de découverte électronique locale, procédez de l'une des façons suivantes :

  - Utilisez le Centre d'administration Exchange (CAE) pour vérifier que la recherche n'apparaît plus dans l'affichage Liste de l'onglet **Découverte électronique locale et archive permanente**.

  - Exemples

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.

