---
title: 'Créer une stratégie de BAL de messagerie unifiée: Exchange 2013 Help'
TOCTitle: Créer une stratégie de boîte aux lettres de messagerie unifiée
ms:assetid: 7f20874b-c46c-4505-9a78-f63eacb578ff
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb123510(v=EXCHG.150)
ms:contentKeyID: 50555432
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.Servers.UnifiedMessaging.CreateUMMailboxPolicyWizardForm.CreateUMMailboxPolicyWizardPage
ms.translationtype: HT
---

# Créer une stratégie de boîte aux lettres de messagerie unifiée

 

_**Sapplique à :** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2013-03-08_

Vous pouvez créer une stratégie de boîte aux lettres de messagerie unifiée pour appliquer un jeu commun de paramètres de stratégie de messagerie unifiée, par exemple, des paramètres de stratégie de code confidentiel ou des restrictions d'appel, à une série de boîtes aux lettres activées pour la messagerie unifiée. Les stratégies de boîte aux lettres de messagerie unifiée associent un utilisateur à extension messagerie unifiée à un plan de numérotation de messagerie unifiée et appliquent un ensemble commun de stratégies ou de paramètres de sécurité à plusieurs boîtes aux lettres à extension messagerie unifiée. Elles sont utiles pour l'application et la standardisation des paramètres de configuration de la messagerie unifiée pour les utilisateurs à extension messagerie unifiée.

Par défaut, lorsqu'un plan de numérotation de messagerie unifiée est créé, une stratégie de boîte aux lettres de messagerie unifiée est également créée. Après avoir déployé la messagerie unifiée dans votre organisation, vous devrez peut-être créer des stratégies de boîte aux lettres de messagerie unifiée supplémentaires ou en modifier des existantes.

Pour découvrir d'autres tâches de gestion relatives aux stratégies de boîte aux lettres de messagerie unifiée, consultez la rubrique [Procédures de stratégie de boîte aux lettres de messagerie unifiée](um-mailbox-policy-procedures-exchange-2013-help.md).

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : 3 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l'entrée « Stratégies de boîte aux lettres de messagerie unifiée » dans la rubrique [Autorisations de messagerie unifiée](unified-messaging-permissions-exchange-2013-help.md).

  - Avant d'exécuter ces procédures, vérifiez qu'un plan de numérotation de messagerie unifiée a été créé. Pour obtenir la procédure détaillée, consultez la rubrique [Créer un plan de numérotation de messagerie unifiée](https://docs.microsoft.com/fr-fr/exchange/voice-mail-unified-messaging/connect-voice-mail-system/create-um-dial-plan).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..


## Que souhaitez-vous faire ?

## Utiliser le Centre d'administration Exchange (CAE) pour créer une stratégie de boîte aux lettres de messagerie unifiée

1.  
    
    Dans le Centre d'administration Exchange, accédez à **Messagerie unifiée** \> **Plans de numérotation de messagerie unifiée**. Dans l'affichage Liste, sélectionnez le plan de numérotation de messagerie unifiée à modifier, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

2.  Dans la page **Plan de numérotation de messagerie unifiée**, sous **Stratégies de boîte aux lettres de messagerie unifiée**, cliquez sur **Nouveau** ![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter").

3.  Dans la page **Nouvelle stratégie de boîte aux lettres de messagerie unifiée**, dans le champ **Nom**, entrez le nom de la nouvelle stratégie de boîte aux lettres de messagerie unifiée.
    
    Ce champ permet de spécifier un nom unique pour la stratégie de boîte aux lettres de messagerie unifiée. Il s'agit du nom complet qui apparaît dans le CAE. Si vous devez modifier le nom complet de la stratégie de boîte aux lettres de messagerie unifiée après sa création, vous devez d'abord la supprimer, puis en créer une autre avec le nom approprié. Il n'est pas possible de supprimer une stratégie de boîte aux lettres de messagerie unifiée si l'un des utilisateurs à extension messagerie unifiée y est associé.
    
    Le nom de la stratégie de boîte aux lettres de messagerie unifiée est obligatoire, mais est uniquement utilisé à des fins d'affichage. Dans la mesure où votre organisation peut utiliser plusieurs stratégies de boîte aux lettres de messagerie unifiée, nous vous recommandons d'utiliser des noms significatifs pour chaque stratégie. La longueur maximale d'un nom de stratégie de boîte aux lettres de messagerie unifiée est de 64 caractères pouvant contenir des espaces. Toutefois, ce nom ne peut pas contenir les caractères suivants : " / \\ \[ \] : ; | = , + \* ? \< \>.

4.  Cliquez sur **Enregistrer** pour enregistrer la nouvelle stratégie de boîte aux lettres de messagerie unifiée. Lorsque vous enregistrez la stratégie de boîte aux lettres de messagerie unifiée, l'ensemble des paramètres par défaut, y compris les stratégies de messagerie unifiée, les fonctionnalités de messagerie vocale et les paramètres de messagerie vocale protégée sont activés. Si vous souhaitez personnaliser ou modifier les paramètres par défaut, utilisez la cmdlet **Set-UMMailbox** pour modifier les paramètres de la stratégie de boîte aux lettres de messagerie unifiée que vous venez de créer.

## Utiliser le shell pour créer une stratégie de boîte aux lettres de messagerie unifiée

Cet exemple crée une nouvelle stratégie de boîte aux lettres de messagerie unifiée, appelée `MyUMMailboxPolicy`, qui est associée au plan de numérotation de messagerie unifiée appelé `MyUMDialPlan`.

    New-UMMailboxPolicy -Name MyUMMailboxPolicy -UMDialPlan MyUMDialPlan

