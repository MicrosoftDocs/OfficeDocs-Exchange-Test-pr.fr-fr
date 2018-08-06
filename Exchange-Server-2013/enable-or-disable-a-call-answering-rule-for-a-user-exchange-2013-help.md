---
title: 'Activer/désactiver règle de répondeur auto. pour un utlsr: Exchange 2013 Help | Microsoft Docs'
TOCTitle: Activer ou désactiver une règle de répondeur automatique pour un utilisateur
ms:assetid: f9e40ac3-117f-44f6-9ab1-dc9f4c72e8ac
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dn140252(v=EXCHG.150)
ms:contentKeyID: 54652747
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Activer ou désactiver une règle de répondeur automatique pour un utilisateur

 

_**Sapplique à :** Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2015-04-08_

Vous pouvez utiliser l'environnement de ligne de commande Exchange Management Shell pour activer ou désactiver une ou plusieurs règles de répondeur automatique pour un utilisateur. Vous pouvez également utiliser les cmdlets **Enable-UMCallAnsweringRule** ou **Disable-UMCallAnsweringRule** dans un script de l'environnement de ligne de commande Exchange Management Shell pour activer ou désactiver une ou plusieurs règles de répondeur automatique pour différents utilisateurs.

Les règles de répondeur automatique et les règles de boîte de réception sont appliquées de la même manière aux appels entrants et aux messages électroniques entrants. Par défaut, quand la messagerie unifiée est activée pour un utilisateur, aucune règle de répondeur automatique n'est configurée. Cependant, le système de messagerie répond aux appels entrants et les appelants sont invités à laisser un message vocal.

Pour découvrir d'autres tâches de gestion relatives aux règles de répondeur automatique, consultez la rubrique [Transfert d'appels de procédures](forwarding-calls-procedures-exchange-2013-help.md).

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : moins d'une minute.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l'entrée « Règles de répondeur automatique de messagerie unifiée » dans la rubrique [Autorisations de messagerie unifiée](unified-messaging-permissions-exchange-2013-help.md).

  - Avant d'effectuer cette procédure, vérifiez qu'un plan de numérotation de messagerie unifiée a été créé. Pour obtenir la procédure détaillée, consultez la rubrique [Créer un plan de numérotation de messagerie unifiée](create-a-um-dial-plan-exchange-2013-help.md).

  - Avant d'effectuer cette procédure, vérifiez qu'une stratégie de boîte aux lettres de messagerie unifiée a été créée. Pour obtenir la procédure détaillée, consultez la rubrique [Créer une stratégie de boîte aux lettres de messagerie unifiée](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Avant d'effectuer cette procédure, vérifiez que la boîte aux lettres de l'utilisateur est à extension messagerie unifiée. Pour obtenir la procédure détaillée, consultez la rubrique [Activation de la messagerie vocale pour un utilisateur](enable-a-user-for-voice-mail-exchange-2013-help.md).

  - Vous pouvez uniquement utiliser l'environnement de ligne de commande Exchange Management Shell pour effectuer cette tâche. Pour apprendre à ouvrir l’environnement de ligne de commande Environnement de ligne de commande Exchange Management Shell dans votre organisation Exchange locale, reportez-vous à [Ouvrir le Shell](https://technet.microsoft.com/fr-fr/library/dd638134\(v=exchg.150\)). Pour apprendre à utiliser Windows PowerShell afin de vous connecter à Exchange Online, consultez la rubrique [Connexion à Exchange Online PowerShell](https://go.microsoft.com/fwlink/p/?linkid=396554).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..


## Que souhaitez-vous faire ?

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour activer une règle de répondeur automatique

Quand une règle de répondeur automatique est créée, elle est activée. Vous pouvez utiliser l'environnement de ligne de commande Exchange Management Shell pour activer une règle de répondeur automatique qui a été désactivée. L'activation d'une règle de répondeur automatique active la cmdlet **Enable-UMCallAnsweringRule** pour récupérer la règle de répondeur automatique comprenant les conditions et les actions pour une règle de répondeur automatique spécifiée.

Cet exemple active la règle de répondeur automatique `MyUMCallAnsweringRule` dans la boîte aux lettres de Tony Smith.

    Enable-UMCallAnsweringRule -Identity MyUMCallAnsweringRule -Mailbox tonysmith

L'exemple utilise le commutateur *WhatIf* pour tester si la règle de répondeur automatique `MyUMCallAnsweringRule` dans la boîte aux lettres de Tony Smith est prête à être activée et s'il existe des erreurs dans la commande.

    Enable-UMCallAnsweringRule -Identity MyUMCallAnsweringRule -Mailbox tonysmith -WhatIf

Cet exemple active la règle de répondeur automatique `MyUMCallAnsweringRule` dans la boîte aux lettres de Tony Smith et invite l'utilisateur connecté à confirmer l'activation de la règle de répondeur automatique.

    Enable-UMCallAnsweringRule -Identity MyUMCallAnsweringRule -Mailbox tonysmith -Confirm

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour désactiver une règle de répondeur automatique

La désactivation d'une règle de répondeur automatique l'empêche d'être récupérée et traitée lors de la réception d'un appel entrant. Quand vous créez une règle de répondeur automatique, nous vous recommandons de la désactiver lors de la configuration des conditions et des actions. Cela empêche le traitement de la règle de répondeur automatique lors de la réception d'un appel entrant tant que la règle de répondeur automatique n'est pas correctement configurée.

Cet exemple désactive la règle de répondeur automatique `MyUMCallAnsweringRule` dans la boîte aux lettres pour Tony Smith.

    Disable -UMCallAnsweringRule -Identity MyUMCallAnsweringRule -Mailbox tonysmith

Cet exemple utilise le commutateur *WhatIf* pour tester si la règle de répondeur automatique `MyUMCallAnsweringRule` dans la boîte aux lettres de Tony Smith est prête à être désactivée et s'il existe des erreurs dans la commande.

    Disable -UMCallAnsweringRule -Identity MyUMCallAnsweringRule -Mailbox tonysmith -WhatIf

Cet exemple désactive la règle de répondeur automatique `MyUMCallAnsweringRule` dans la boîte aux lettres de Tony Smith et invite l'utilisateur connecté à confirmer la désactivation de la règle de répondeur automatique.

    Disable-UMCallAnsweringRule -Identity MyUMCallAnsweringRule -Mailbox tonysmith -Confirm

