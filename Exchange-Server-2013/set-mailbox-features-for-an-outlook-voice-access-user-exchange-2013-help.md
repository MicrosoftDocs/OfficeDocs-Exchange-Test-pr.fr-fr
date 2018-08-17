---
title: 'Définir les fonctions de BAL pr un utilisateur d’OVA: Exchange 2013 Help'
TOCTitle: Définir les fonctionnalités de boîte aux lettres pour un utilisateur d'Outlook Voice Access
ms:assetid: a56bfd75-7bc5-49b9-b098-06855a720dcd
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb124030(v=EXCHG.150)
ms:contentKeyID: 50555464
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Définir les fonctionnalités de boîte aux lettres pour un utilisateur d'Outlook Voice Access

 

_**Sapplique à :** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2013-02-22_

Les paramètres de l'interface utilisateur de téléphonie (TUI) sont utilisés quand un utilisateur accède au système de messagerie unifiée par le biais d'Outlook Voice Access. Lorsque vous modifiez les paramètres de configuration de l'interface utilisateur de téléphonie d'un utilisateur à extension messagerie unifiée, vous modifiez les propriétés et les valeurs correspondantes dans la boîte aux lettres de l'utilisateur.

Vous pouvez modifier les paramètres de l'interface utilisateur de téléphonie (TUI) suivants pour un utilisateur à extension messagerie unifiée :

  - Autoriser l'accès abonné

  - Autoriser l'accès TUI au calendrier

  - Autoriser l'accès TUI aux messages électroniques

  - Autoriser la reconnaissance vocale

Pour connaître les tâches de gestion supplémentaires relatives aux utilisateurs de la messagerie unifiée, consultez la rubrique [Définir les fonctionnalités de boîte aux lettres pour un utilisateur d'Outlook Voice Access](set-mailbox-features-for-an-outlook-voice-access-user-exchange-2013-help.md).

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : 5 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Boîtes aux lettres de messagerie unifiée » dans la rubrique [Autorisations de messagerie unifiée](unified-messaging-permissions-exchange-2013-help.md).

  - Avant d'effectuer ces procédures, vérifiez que le destinataire Exchange existant est à extension messagerie unifiée et messagerie vocale. Pour obtenir la procédure détaillée, consultez la rubrique [Activation de la messagerie vocale pour un utilisateur](enable-a-user-for-voice-mail-exchange-2013-help.md).

  - Avant d'exécuter ces procédures, vérifiez qu'un plan de numérotation de messagerie unifiée a été créé. Pour obtenir la procédure détaillée, consultez la rubrique [Créer un plan de numérotation de messagerie unifiée](create-a-um-dial-plan-exchange-2013-help.md).

  - Avant d'effectuer ces procédures, vérifiez qu'une stratégie de boîte aux lettres de messagerie unifiée a été créée. Pour obtenir la procédure détaillée, consultez la rubrique [Créer une stratégie de boîte aux lettres de messagerie unifiée](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..


## Utiliser l'environnement de ligne de commande Exchange Management Shell pour modifier les paramètres de l'interface utilisateur de téléphonie d'un utilisateur unique à extension messagerie unifiée

Cet exemple active l'accès à la messagerie électronique et au calendrier à l'aide de l'interface utilisateur de téléphonie pour l'utilisateur à extension messagerie unifiée Tony Smith.

    Set-UMMailbox -Identity tony@contoso.com TUIAccessToCal True -TUIAccessToEmail True -OperatorNumber 111111 -DisableMissedCallNotification False -AnonCallBlock True

> [!NOTE]
> Les paramètres de l'interface utilisateur de téléphonie des utilisateurs sont également accessibles dans les stratégies de boîte aux lettres de messagerie unifiée. La modification des paramètres de l'interface utilisateur de téléphonie (TUI) dans une stratégie de boîte aux lettres de messagerie unifiée affecte tous les utilisateurs qui sont associés à cette stratégie. Pour plus d'informations sur la modification des paramètres de l'interface utilisateur de téléphonie dans une stratégie de boîte aux lettres de messagerie unifiée, consultez la rubrique <a href="set-mailbox-features-for-outlook-voice-access-users-exchange-2013-help.md">Définitions des fonctionnalités de boîte aux lettres pour des utilisateurs d’Outlook Voice Access</a>.

