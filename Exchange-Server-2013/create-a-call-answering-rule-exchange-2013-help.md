---
title: 'Création d’une règle de répondeur automatique: Exchange 2013 Help'
TOCTitle: Création d’une règle de répondeur automatique
ms:assetid: 0976f8f2-3449-44f1-b0d1-20c91622e827
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ898495(v=EXCHG.150)
ms:contentKeyID: 51407154
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Création d’une règle de répondeur automatique

 

_**Sapplique à :** Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2015-04-08_

Vous pouvez utiliser l'environnement de ligne de commande Exchange Management Shell pour créer une ou plusieurs règles de répondeur automatique pour un utilisateur. Vous pouvez également utiliser la cmdlet **New-UMCallAnsweringRule** dans un script Exchange Management Shell pour créer des règles de répondeur automatique pour plusieurs utilisateurs.

Les règles de répondeur automatique et les règles de boîte de réception sont appliquées de la même manière aux appels entrants et aux messages électroniques entrants. Par défaut, quand la messagerie unifiée est activée pour un utilisateur, aucune règle de répondeur automatique n'est configurée. Cependant, le système de messagerie répond aux appels entrants et les appelants sont invités à laisser un message vocal.

> [!NOTE]  
> Les utilisateurs à extension messagerie unifiée peuvent se connecter à Outlook Web App pour créer, gérer et supprimer les règles de répondeur automatique.


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


## Utiliser l'environnement de ligne de commande Exchange Management Shell pour créer une règle de répondeur automatique

Cet exemple crée la règle de répondeur automatique `MyCallAnsweringRule` dans la boîte aux lettres de Tony Smith avec la priorité 2.

    New-UMCallAnsweringRule -Name MyCallAnsweringRule -Priority 2 -Mailbox tonysmith

Cet exemple crée la règle de répondeur automatique `MyCallAnsweringRule` dans la boîte aux lettres de Tony Smith et effectue les actions suivantes :

  - Définit la règle de répondeur automatique à deux ID d'appelants.

  - Affecte la valeur 2 à la priorité de la règle de répondeur automatique.

  - Définit la règle de répondeur automatique pour permettre aux appelants d'interrompre le message d'accueil.

<!-- end list -->

    New-UMCallAnsweringRule -Name MyCallAnsweringRule -CallerIds "1,4255550100,,","1,4255550123,," -Priority 2 -CallersCanInterruptGreeting $true -Mailbox tonysmith

Cet exemple crée la règle de répondeur automatique `MyCallAnsweringRule` dans la boîte aux lettres de Tony Smith et effectue les actions suivantes :

  -  Affecte la valeur 2 à la priorité de la règle de répondeur automatique.

  -  Crée les mappages de touches pour la règle de répondeur automatique.

  -  Si l'appelant accède à la messagerie vocale de l'utilisateur et que l'état de ce dernier est défini sur Occupé, l'appelant peut :
    
      - Appuyer sur la touche 1 et être transféré vers le réceptionniste sur le poste 45678.
    
      - Appuyer sur la touche 2 et la fonction Me joindre sera utilisée pour les problèmes urgents, ensuite appeler le poste 23456 en premier, puis 45671.

<!-- end list -->

    New-UMCallAnsweringRule -Name MyCallAnsweringRule -Priority 2 -Mailbox tonysmith -ScheduleStatus 0x4 - -KeyMappings "1,1,Receptionist,,,,,45678,","5,2,Urgent Issues,23456,23,45671,50,,"

