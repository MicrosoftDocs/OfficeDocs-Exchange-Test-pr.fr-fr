---
title: 'Lancer/arrêter une rech. de découverte électr. inaltérable: Exchange 2013 Help'
TOCTitle: Lancement ou arrêt d’une recherche de découverte électronique inaltérable
ms:assetid: 0d546763-4bf5-4523-91f4-d181b7ee4ac2
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dd335090(v=EXCHG.150)
ms:contentKeyID: 50477549
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Lancement ou arrêt d’une recherche de découverte électronique inaltérable

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2014-07-14_

Vous pouvez arrêter ou redémarrer une recherche par découverte électronique locale à tout moment. Par exemple, pour modifier les propriétés de recherche telles que les mots-clés ou les boîtes aux lettres recherchées, vous devez commencer par arrêter une recherche. Vous pouvez alors redémarrer la recherche après avoir apporté les modifications requises.

> [!CAUTION]
> Si vous relancez une recherche par découverte électronique locale, les résultats de la recherche copiés dans la boîte aux lettres de découverte spécifiée dans la recherche sont supprimés.


## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : 1 minute.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l'entrée « Découverte électronique locale » dans la rubrique [Stratégie de messagerie et autorisations de conformité](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.


## Que souhaitez-vous faire ?

## Utiliser le Centre d'administration Exchange pour démarrer ou arrêter une recherche par découverte électronique locale

1.  Accédez à **Gestion de la conformité** \> **Découverte électronique locale et archive permanente**.

2.  Pour arrêter une recherche en cours, sélectionnez la recherche, puis cliquez sur **Arrêter la recherche**.

3.  Pour démarrer une recherche interrompue, sélectionnez la recherche, puis cliquez sur **Reprendre la recherche**.

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour démarrer ou arrêter une recherche par découverte électronique locale

Pour obtenir un exemple de démarrage d'une recherche par découverte électronique locale, consultez l'exemple 1 de la rubrique [Start-MailboxSearch](https://technet.microsoft.com/fr-fr/library/dd351245\(v=exchg.150\)).

Pour obtenir un exemple d'arrêt d'une recherche par découverte électronique locale, consultez l'exemple 1 de la rubrique [Stop-MailboxSearch](https://technet.microsoft.com/fr-fr/library/dd351075\(v=exchg.150\)).

