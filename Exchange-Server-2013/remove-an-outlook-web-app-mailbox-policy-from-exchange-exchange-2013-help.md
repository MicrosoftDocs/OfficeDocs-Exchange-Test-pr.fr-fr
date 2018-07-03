---
title: "Suppression d'une stratégie de boîte aux lettres Outlook Web App dans Exchange: Exchange 2013 Help"
TOCTitle: Suppression d'une stratégie de boîte aux lettres Outlook Web App dans Exchange
ms:assetid: edab7bac-b62c-4b82-8f21-dcac77cf0e8f
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dd351239(v=EXCHG.150)
ms:contentKeyID: 50479510
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Suppression d'une stratégie de boîte aux lettres Outlook Web App dans Exchange

 

_**Sapplique à :** Exchange Online, Exchange Server 2013_

_**Dernière rubrique modifiée :** 2013-03-15_

Vous pouvez supprimer une stratégie de boîte aux lettres MicrosoftOutlook Web App d'une organisation Exchange à l'aide du Centre d'administration Exchange (CAE) ou de l'environnement de ligne de commande Exchange Management Shell.

Pour les autres tâches de gestion relatives aux stratégies de boîte aux lettres Outlook Web App, consultez la rubrique [Stratégies de boîte aux lettres de Outlook Web App](outlook-web-app-mailbox-policies-exchange-2013-help.md).

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée de chaque procédure : 3 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l'entrée « Stratégies de boîte aux lettres de messagerie unifiée Outlook Web App » dans la rubrique [Autorisations des clients et des périphériques mobiles](clients-and-mobile-devices-permissions-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..


## Que souhaitez-vous faire ?

## Utiliser le CAE pour supprimer une stratégie de boîte aux lettres Outlook Web App

1.  Dans le CAE, cliquez sur **Autorisations** \> **Stratégies Outlook Web App**.

2.  Dans le volet de résultats, sélectionnez la stratégie de boîte aux lettres à supprimer.

3.  Cliquez sur le bouton **Supprimer**.

4.  Dans la fenêtre de confirmation, cliquez sur **Oui** pour supprimer la stratégie de boîte aux lettres ou sur **Non** pour annuler.

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour supprimer une stratégie de boîte aux lettres d'Outlook Web App

Cet exemple crée une stratégie de boîte aux lettres d'Outlook Web App nommée `Policy1`.

    Remove-OwaMailboxPolicy -Name Policy1 

Pour plus d'informations sur la syntaxe et les paramètres, consultez la rubrique [Remove-OwaMailboxPolicy](https://technet.microsoft.com/fr-fr/library/dd298103\(v=exchg.150\)).

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez bien supprimé une stratégie de boîte aux lettres Outlook Web App, procédez comme suit :

  - Dans le centre d'administration Exchange, cliquez sur **autorisations** \> **stratégies Outlook Web App**. La stratégie que vous avez supprimé doit n'apparaît plus dans la liste.

