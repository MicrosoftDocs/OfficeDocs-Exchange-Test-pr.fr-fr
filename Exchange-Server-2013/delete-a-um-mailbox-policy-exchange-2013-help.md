---
title: 'Supprimer une stratégie de boîte aux lettres de messagerie unifiée: Exchange 2013 Help'
TOCTitle: Supprimer une stratégie de boîte aux lettres de messagerie unifiée
ms:assetid: c8758464-3c52-4dd3-b2a6-142a99bb0628
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb124536(v=EXCHG.150)
ms:contentKeyID: 50555491
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Supprimer une stratégie de boîte aux lettres de messagerie unifiée

 

_**Sapplique à :** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2012-11-05_

Lorsque vous supprimez une stratégie de boîte aux lettres de messagerie unifiée, celle-ci n’est plus être accessible pour être associée à des destinataires activés pour la messagerie unifiée. Vous ne pouvez pas supprimer une stratégie de boîte aux lettres de messagerie unifiée si celle-ci est référencée par des boîtes aux lettres à extension messagerie unifiée, et vous ne pouvez pas supprimer un plan de numérotation de messagerie unifiée si une stratégie de boîte aux lettres de messagerie unifiée lui est associée.

Pour d’autres tâches de gestion relatives aux stratégies de boîte aux lettres de messagerie unifiée, voir [Procédures de stratégie de boîte aux lettres de messagerie unifiée](um-mailbox-policy-procedures-exchange-2013-help.md).

## Ce qu’il faut savoir avant de commencer ?

  - Durée d'exécution estimée : Moins d’une minute.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Stratégies de boîte aux lettres de messagerie unifiée » dans la rubrique [Autorisations de messagerie unifiée](unified-messaging-permissions-exchange-2013-help.md).

  - Avant d’effectuer ces procédures, vérifiez qu’une stratégie de boîte aux lettres de messagerie unifiée a été créée. Pour obtenir la procédure détaillée, consultez la rubrique [Créer une stratégie de boîte aux lettres de messagerie unifiée](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..


## Que souhaitez-vous faire ?

## Utiliser le Centre d’administration Exchange (EAC) pour supprimer une stratégie de boîte aux lettres de messagerie unifiée

1.  
    
    Dans le Centre d’administration Exchange, accédez à **Messagerie unifiée** \> **Plans de numérotation de messagerie unifiée**. Dans l’affichage de liste, sélectionnez le plan de numérotation de messagerie unifiée que vous souhaitez modifier, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

2.  Sur la page **Plan de numérotation de messagerie unifiée**, sous **Stratégies de boîte aux lettres de messagerie unifiée**, cliquez sur **Supprimer**![Icône Supprimer](images/Dd979797.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "Icône Supprimer").

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour créer une stratégie de boîte aux lettres de messagerie unifiée

L'exemple suivant supprime une stratégie de boîte aux lettres de messagerie unifiée nommée `MyUMMailboxPolicy`.

    Remove-UMMailboxPolicy -Identity MyUMMailboxPolicy

