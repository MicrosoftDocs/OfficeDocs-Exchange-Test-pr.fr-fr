---
title: 'Import d’invites perso. d’Exchange 2007 dans Exchange 2013: Exchange 2013 Help'
TOCTitle: Importation d’invites personnalisées d’Exchange 2007 dans Exchange 2013
ms:assetid: 70c0b0bc-c0de-4e3c-8144-1fe59f86ebf4
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Gg309147(v=EXCHG.150)
ms:contentKeyID: 54652759
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Importation d’invites personnalisées d’Exchange 2007 dans Exchange 2013

 

_**Sapplique à :** Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2015-04-08_

Vous pouvez importer les fichiers audio contenant des messages d'accueil personnalisés, des annonces, des menus et des messages d'assistance vocaux de la messagerie unifiée Exchange 2007 vers la messagerie unifiée Exchange 2013. À l'aide d'un script de l'environnement de ligne de commande Exchange Management Shell, les messages d'assistance vocaux sont importés dans une boîte aux lettres système Exchange nommée {e0dc1c29-89c3-4034-b678-e6c29d823ed9}, créée lors de l'installation de Microsoft Exchange 2013. Cette boîte aux lettres système est utilisée dans la messagerie unifiée pour stocker les messages d'accueil, les annonces, les menus, les messages d'assistance vocaux et les rapports de messagerie unifiée du plan de numérotation et du standard automatique.

Les fichiers audio, au format .wav ou .wma, sont utilisés des manières suivantes :

  - Dans les plans de numérotation de messagerie unifiée, ils permettent de personnaliser les messages d'accueil et les messages d'information automatiques. Ils sont lus quand les utilisateurs d’Outlook Voice Access appellent un numéro Outlook Voice Access.

  - Sur les standards automatiques de messagerie unifiée, ils permettent de personnaliser les messages d'accueil pour les heures d'ouverture et les heures de fermeture, les messages d'information automatiques, les messages d'assistance vocaux et les menus de navigation. Ils sont lus quand les utilisateurs appellent un standard automatique de messagerie unifiée.

Le script MigrateUMCustomPrompts.ps1 vous permet de migrer une copie de l'ensemble des messages d'accueil, des annonces, des menus et des messages d'assistance vocaux personnalisés de messagerie unifiée Exchange Server 2007 vers la messagerie unifiée Exchange 2013 pour tous les plans de numérotation et les standards de messagerie unifiée Exchange 2007.

Par défaut, le script MigrateUMCustomPrompts.ps1 est situé dans le dossier \<Program Files\>\\Microsoft\\Exchange Server\\V15\\Scripts d'un serveur Exchange 2013.

> [!NOTE]
> Le script MigrateUMCustomPrompts.ps1 est inclus dans Exchange 2013. Il doit être exécuté sur un serveur de boîtes aux lettres Exchange 2013 dans la même organisation avec vos serveurs de messagerie unifiée Exchange 2007.


Pour découvrir d'autres tâches de gestion relatives aux plans de numérotation de messagerie unifiée, consultez la rubrique [Procédures de plan de numérotation de messagerie unifiée](um-dial-plan-procedures-exchange-2013-help.md).

Pour découvrir d'autres tâches de gestion relatives aux standards automatiques de messagerie unifiée, consultez la rubrique [Procédures relatives au standard automatique de messagerie unifiée](https://docs.microsoft.com/fr-fr/exchange/voice-mail-unified-messaging/automatically-answer-and-route-calls/um-auto-attendant-procedures).

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : 3 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez les entrées « Plans de numérotation de messagerie unifiée » et « Standards automatiques de messagerie unifiée » dans la rubrique [Autorisations de messagerie unifiée](unified-messaging-permissions-exchange-2013-help.md).

  - Avant d'exécuter ces procédures, vérifiez qu'un plan de numérotation de messagerie unifiée a été créé. Pour obtenir la procédure détaillée, consultez la rubrique [Créer un plan de numérotation de messagerie unifiée](https://docs.microsoft.com/fr-fr/exchange/voice-mail-unified-messaging/connect-voice-mail-system/create-um-dial-plan).

  - Avant d'exécuter ces procédures, vérifiez qu'un standard automatique de messagerie unifiée a été créé. Pour obtenir la procédure détaillée, consultez la rubrique [Créer un standard automatique de messagerie unifiée](https://docs.microsoft.com/fr-fr/exchange/voice-mail-unified-messaging/automatically-answer-and-route-calls/create-a-um-auto-attendant).

  - Vous pouvez uniquement utiliser l'environnement de ligne de commande Exchange Management Shell pour effectuer cette tâche. Pour apprendre à ouvrir l’environnement de ligne de commande Environnement de ligne de commande Exchange Management Shell dans votre organisation Exchange locale, reportez-vous à [Ouvrir le Shell](https://technet.microsoft.com/fr-fr/library/dd638134\(v=exchg.150\)).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..


## Utiliser le script MigrateUMCustomPrompts.ps1 pour migrer une copie de tous les messages d'assistance vocaux personnalisés pour les plans de numérotation et les standards automatiques de messagerie unifiée

1.  Cliquez sur **Démarrer** \>**Tous les programmes**\>**Microsoft Exchange Server 2013**\>**Environnement de ligne de commande Exchange Management Shell**.

2.  Dans l'environnement de ligne de commande Exchange Management Shell, à l'invite, tapez le chemin d'accès au script. Par exemple, tapez **cd "D:\\Program Files\\Microsoft\\Exchange Server\\V15\\Scripts"**, puis appuyez sur Entrée.

3.  À l'invite de l'environnement de ligne de commande Exchange Management Shell, tapez **".\\MigrateUMCustomPrompt",**, puis appuyez sur Entrée.

