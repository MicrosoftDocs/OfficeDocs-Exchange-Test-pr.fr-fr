---
title: "Désactiver la messagerie vocale d'un utilisateur: Exchange 2013 Help"
TOCTitle: Désactiver la messagerie vocale d'un utilisateur
ms:assetid: cecc9c0d-377d-489e-9db4-d487e9c0b552
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb124691(v=EXCHG.150)
ms:contentKeyID: 50479258
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Désactiver la messagerie vocale d'un utilisateur

 

_**Sapplique à :** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2012-11-05_

Vous pouvez désactiver la messagerie unifiée (MU) pour un utilisateur à extension messagerie unifiée. Lorsque vous effectuez cette opération, l'utilisateur ne peut plus utiliser les fonctionnalités de messagerie vocale unifiées. Si vous préférez, lorsque vous désactivez la messagerie unifiée pour un utilisateur, vous pouvez conserver les paramètres de messagerie unifiée pour l'utilisateur.

Pour découvrir d'autres tâches de gestion relatives aux utilisateurs à extension messagerie vocale, consultez la rubrique [Voix des procédures de l'utilisateur à extension messagerie](voice-mail-enabled-user-procedures-exchange-2013-help.md).

## Ce qu’il faut savoir avant de commencer ?

  - Durée d’exécution estimée : Moins d’une minute.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Boîtes aux lettres de messagerie unifiée » dans la rubrique [Autorisations de messagerie unifiée](unified-messaging-permissions-exchange-2013-help.md).

  - Avant d'effectuer cette procédure, vérifiez qu'un plan de numérotation de messagerie unifiée a été créé. Pour obtenir la procédure détaillée, consultez la rubrique [Créer un plan de numérotation de messagerie unifiée](create-a-um-dial-plan-exchange-2013-help.md).

  - Avant d'effectuer cette procédure, vérifiez qu'une stratégie de boîte aux lettres de messagerie unifiée a été créée. Pour obtenir la procédure détaillée, consultez la rubrique [Créer une stratégie de boîte aux lettres de messagerie unifiée](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Avant d'effectuer ces procédures, vérifiez que l'utilisateur existant est actuellement activé pour la messagerie unifiée. Pour obtenir la procédure détaillée, consultez la rubrique [Activation de la messagerie vocale pour un utilisateur](enable-a-user-for-voice-mail-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..


## Que souhaitez-vous faire ?

## Utiliser le CAE pour désactiver la messagerie unifiée et la messagerie vocale d’un utilisateur

1.  Dans le CAE, cliquez sur **Destinataires**.

2.  Dans la liste, sélectionnez l’utilisateur dont vous voulez désactiver la boîte aux lettres pour la messagerie unifiée.

3.  Dans le volet d’informations, sous **Fonctions de téléphone et de voix**, puis sous **Messagerie unifiée**, cliquez sur **Désactiver**.

4.  Dans la boîte de dialogue **Avertissement**, cliquez sur **Oui** pour confirmer la désactivation de la messagerie unifiée pour l’utilisateur.

## Utiliser l’environnement de ligne de commande Exchange Management Shell pour désactiver la messagerie unifiée et la messagerie vocale d’un utilisateur

Cet exemple désactive la messagerie unifiée et la messagerie vocale de l’utilisateur tonysmith@contoso.com, mais conserve les paramètres de boîte aux lettres de messagerie unifiée.

    Disable-UMMailbox -Identity tonysmith@contoso.com -KeepProperties $True

