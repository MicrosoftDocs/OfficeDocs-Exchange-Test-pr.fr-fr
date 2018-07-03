---
title: 'Désactiver les appels des utilisateurs qui ne sont pas activés pour la MU: Exchange 2013 Help'
TOCTitle: Désactiver les appels des utilisateurs qui ne sont pas activés pour la MU
ms:assetid: 272ff4ab-b4d9-4647-98e2-7c171f9dfc3f
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ673516(v=EXCHG.150)
ms:contentKeyID: 50477688
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Désactiver les appels des utilisateurs qui ne sont pas activés pour la MU

 

_**Sapplique à :** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2012-11-05_

Vous pouvez activer ou désactiver les appels à partir des utilisateurs qui ne sont pas activés pour la messagerie unifiée. Par défaut, la messagerie unifiée autorise le transfert via un standard automatique des appels entrants provenant d’appelants non authentifiés aux utilisateurs à extension messagerie unifiée. Lorsque ce paramètre est activé, les utilisateurs externes à l’organisation peuvent transférer des appels aux utilisateurs à extension messagerie unifiée.

Si cette option est désactivée pour un utilisateur à extension messagerie unifiée, la boîte aux lettres de l’utilisateur peut toujours être localisée via une recherche d’annuaire. Toutefois, si un appelant externe tente de transférer un appel à l’utilisateur, le système indiquera : « Désolé, je ne peux pas transférer l’appel à cet utilisateur.» L’appelant est ensuite transféré à l’opérateur si un opérateur a été configuré sur le standard automatique. Si aucun opérateur n’est configuré sur le standard automatique, l’appel est transféré à un opérateur du plan de numérotation (le cas échéant). Si aucune extension opérateur n’a été configurée sur le standard automatique à reconnaissance vocale, le standard automatique de secours DTMF ou le plan de numérotation, le système répond en disant « Désolé. Ni l’opérateur ni le service à tonalité ne sont disponibles. »

Pour d’autres tâches de gestion relatives aux utilisateurs activés pour la messagerie vocale, consultez la rubrique [Voix des procédures de l'utilisateur à extension messagerie](voice-mail-enabled-user-procedures-exchange-2013-help.md).

## Ce qu’il faut savoir avant de commencer ?

  - Durée d'exécution estimée : Moins d’une minute.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Boîtes aux lettres de messagerie unifiée » dans la rubrique [Autorisations de messagerie unifiée](unified-messaging-permissions-exchange-2013-help.md).

  - Avant d’effectuer cette procédure, vérifiez qu’un plan de numérotation de messagerie unifiée a été créé. Pour obtenir la procédure détaillée, consultez la rubrique [Créer un plan de numérotation de messagerie unifiée](create-a-um-dial-plan-exchange-2013-help.md).

  - Avant d'effectuer cette procédure, vérifiez qu'une stratégie de boîte aux lettres de messagerie unifiée a été créée. Pour obtenir la procédure détaillée, consultez la rubrique [Créer une stratégie de boîte aux lettres de messagerie unifiée](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Avant d’effectuer cette procédure, vérifiez que la boîte aux lettres de l’utilisateur est à extension messagerie unifiée. Pour obtenir la procédure détaillée, consultez la rubrique [Activation de la messagerie vocale pour un utilisateur](enable-a-user-for-voice-mail-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..


## Utiliser l’environnement de ligne de commande Exchange Management Shell pour désactiver les appels provenant d’utilisateurs sans extension messagerie unifiée

Cet exemple empêche Tony Smith de recevoir des appels vocaux d’appelants sans extension messagerie unifiée.

    Set UMMailbox -Identity tony@contoso.com -AllowUMCallsFromNonUsers None

