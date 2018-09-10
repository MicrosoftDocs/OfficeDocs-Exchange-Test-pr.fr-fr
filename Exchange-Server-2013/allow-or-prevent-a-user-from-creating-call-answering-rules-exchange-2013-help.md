---
title: 'Autoriser ou empêcher un utlsr de créer des règles de répondeur auto. d’appel'
TOCTitle: Autoriser ou empêcher un utilisateur de créer des règles de répondeur automatique d'appel
ms:assetid: 81863440-8b21-4523-bdab-6a2311889a0d
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dd298097(v=EXCHG.150)
ms:contentKeyID: 50555419
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Autoriser ou empêcher un utilisateur de créer des règles de répondeur automatique d'appel

 

_**Sapplique à :** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2013-02-22_

Vous pouvez indiquer si vous souhaitez que des utilisateurs individuels puissent créer et gérer leurs propres règles de réponse aux appels en configurant les propriétés de leur boîte aux lettres. Par défaut, ils peuvent créer des règles de répondeur automatique.

Vous pouvez activer ou désactiver des règles de répondeur automatique pour plusieurs utilisateurs à extension messagerie unifiée en configurant des règles de répondeur automatique dans un plan de numérotation de messagerie unifiée ou dans une stratégie de boîte aux lettres de messagerie unifiée.

> [!NOTE]
> Vous ne pouvez pas utiliser le Centre d'administration Exchange pour configurer cette fonctionnalité. Vous devez utiliser l'environnement de ligne de commande Exchange Management Shell ou désactiver les règles de répondeur automatique pour un utilisateur de la messagerie vocale.


Pour les autres tâches de gestion visant à autoriser les utilisateurs à transférer des appels, consultez la rubrique [Transfert d'appels de procédures](https://docs.microsoft.com/fr-fr/exchange/voice-mail-unified-messaging/set-up-client-voice-mail-features/forwarding-calls-procedures).

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : moins d'une minute.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Boîtes aux lettres de messagerie unifiée » dans la rubrique [Autorisations de messagerie unifiée](unified-messaging-permissions-exchange-2013-help.md).

  - Avant d'effectuer cette procédure, vérifiez qu'un plan de numérotation de messagerie unifiée a été créé. Pour obtenir la procédure détaillée, consultez la rubrique [Créer un plan de numérotation de messagerie unifiée](https://docs.microsoft.com/fr-fr/exchange/voice-mail-unified-messaging/connect-voice-mail-system/create-um-dial-plan).

  - Avant d'effectuer cette procédure, vérifiez qu'une stratégie de boîte aux lettres de messagerie unifiée a été créée. Pour connaître la procédure détaillée, consultez la rubrique [Créer une stratégie de boîte aux lettres de messagerie unifiée](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Avant d'effectuer cette procédure, vérifiez que la boîte aux lettres de l'utilisateur est à extension messagerie unifiée. Pour connaître la procédure détaillée, consultez la rubrique [Activation de la messagerie vocale pour un utilisateur](https://docs.microsoft.com/fr-fr/exchange/voice-mail-unified-messaging/set-up-voice-mail/enable-a-user-for-voice-mail).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..


## Utiliser l'environnement de ligne de commande Exchange Management Shell pour activer ou désactiver les règles de réponse aux appels pour un utilisateur à extension messagerie unifiée

Cet exemple active les règles de répondeur automatique pour l'utilisateur tony@contoso.com.

    Set-UMMailbox -Identity tony@contoso.com -CallAnsweringRulesEnabled $true

Cet exemple montre comment désactiver les règles de réponse aux appels pour l'utilisateur tony@contoso.com.

    Set-UMMailbox -Identity tony@contoso.com -CallAnsweringRulesEnabled $false

