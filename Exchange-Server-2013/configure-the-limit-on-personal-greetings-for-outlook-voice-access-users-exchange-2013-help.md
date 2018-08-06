---
title: "Config. de la limite sur le message d’accueil personnel pour les utlsr OVA | Microsoft Docs"
TOCTitle: Configurer la limite sur le message d'accueil personnel pour les utilisateurs Outlook Voice Access
ms:assetid: d400f250-0f55-45f5-9918-5f1d7819fbdf
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb201731(v=EXCHG.150)
ms:contentKeyID: 50555501
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurer la limite sur le message d'accueil personnel pour les utilisateurs Outlook Voice Access

 

_**Sapplique à :** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2012-11-05_

Le paramètre de **limite de message d'accueil (en minutes)** vous permet d'entrer le nombre maximal de minutes pendant lesquelles les utilisateurs associés à la stratégie de boîte aux lettres de messagerie unifiée (MU) peuvent utiliser pour enregistrer leurs messages d'accueil vocaux. Ce paramètre s'applique à la fois leurs messages vocaux standard et leurs messages d'accueil vocaux d'absence du bureau. Par défaut, la durée d'accueil maximale est définie sur 5 minutes. Toutefois, vous pouvez configurer le message d'accueil de durée à toute valeur comprise entre 1 et 10 minutes au maximum.

Pour d’autres tâches de gestion relatives aux stratégies de boîte aux lettres de messagerie unifiée, voir [Procédures de stratégie de boîte aux lettres de messagerie unifiée](um-mailbox-policy-procedures-exchange-2013-help.md).

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : moins d'une minute.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Stratégies de boîte aux lettres de messagerie unifiée » dans la rubrique [Autorisations de messagerie unifiée](unified-messaging-permissions-exchange-2013-help.md).

  - Avant d'exécuter ces procédures, vérifiez qu'un plan de numérotation de messagerie unifiée a été créé. Pour obtenir la procédure détaillée, consultez la rubrique [Créer un plan de numérotation de messagerie unifiée](create-a-um-dial-plan-exchange-2013-help.md).

  - Avant d'effectuer ces procédures, vérifiez qu'une stratégie de boîte aux lettres de messagerie unifiée a été créée. Pour obtenir la procédure détaillée, consultez la rubrique [Créer une stratégie de boîte aux lettres de messagerie unifiée](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..


## Que souhaitez-vous faire ?

## Utiliser le CAE pour modifier la durée d'accueil maximale

1.  Dans le Centre d'administration Exchange, accédez à **Messagerie unifiée** \> **Plans de numérotation de messagerie unifiée**. Dans l'affichage Liste, sélectionnez le plan de numérotation de messagerie unifiée à modifier, puis, dans la barre d'outils, cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

2.  Dans la page **Plan de numérotation de messagerie unifiée**, sous **Stratégies de boîte aux lettres de messagerie unifiée**, sélectionnez la stratégie de boîte aux lettres de messagerie unifiée que vous souhaitez gérer, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

3.  Dans la page **stratégie de boîte aux lettres de messagerie unifiée** \> **Général**, sous **la limite sur le message d'accueil personnel (minutes)**, entrez la durée, en minutes, autorisée pour le message d'accueil personnel pour les utilisateurs de messagerie vocale.

4.  Cliquez sur **Enregistrer**.

## Utiliser le Shell pour modifier la durée d'accueil maximale

Cet exemple configure la durée d'accueil sur la stratégie de boîte aux lettres MU `MyUMMailboxPolicy` à 3 minutes au maximum.

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy MaxGreetingDuration 3

