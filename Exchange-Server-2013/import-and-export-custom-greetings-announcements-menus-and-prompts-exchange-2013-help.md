---
title: 'Importer/exporter des invites, annonces, menus et messages d’accueil perso. | Microsoft Docs'
TOCTitle: Importer et exporter des invites, des annonces, des menus et des messages d’accueil personnalisés
ms:assetid: e82da5d5-625f-4d8b-8d31-ac45513aacfd
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Ee681667(v=EXCHG.150)
ms:contentKeyID: 54652782
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Importer et exporter des invites, des annonces, des menus et des messages d’accueil personnalisés

 

_**Sapplique à :** Exchange Server 2010 Service Pack 2 (SP2), Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2015-04-08_

Vous pouvez importer et exporter les fichiers audio que vous avez enregistrés pour les utiliser dans les plans de numérotation et les standards automatiques de messagerie unifiée (MU). Par exemple, vous devez exporter et enregistrer une copie d’un fichier audio si vous effectuez une mise à niveau à partir d’une version précédente d’Exchange. Vous pourriez également avoir besoin d'importer une copie d'une invite audio enregistrée avant de configurer un plan de numérotation ou un standard automatique.

Les fichiers audio sont utilisés dans le cadre des processus suivants :

  - Dans les plans de numérotation de messagerie unifiée, ils permettent de personnaliser les messages d'accueil et les messages d'information automatiques. Ils sont lus quand les utilisateurs d’Outlook Voice Access appellent un numéro Outlook Voice Access.

  - Sur les standards automatiques de messagerie unifiée, ils permettent de personnaliser les messages d'accueil pour les heures d'ouverture et les heures de fermeture, les messages d'information automatiques, les messages d'assistance vocaux et les menus de navigation. Ils sont lus quand les utilisateurs appellent un standard automatique de messagerie unifiée.

Les formats de fichiers audio suivants sont pris en charge pour les messages d'accueil, les annonces, les menus et les invites personnalisés :

  - fichiers .wma encodés avec Windows Media Audio 9.2 - 96 kbits/s/44 kHz/stéréo 1-pass CBR (Windows Sound Recorder) ;

  - fichiers Windows Media Audio Voice 9 - 8 kbits/s/8 kHz/Mono et .wav encodés avec le codec audio PCM linéaire (16 bits/échantillon), 8 kilohertz (kHz).

Vous importez les fichiers audio utilisés par les plans de numérotation et les standards automatiques de messagerie unifiée dans la boîte aux lettres système intitulée {e0dc1c29-89c3-4034-b678-e6c29d823ed9} et exportez les fichiers audio à partir de cette boîte aux lettres. Vous pouvez importer et exporter les fichiers audio à l'aide des cmdlets **Import-UMPrompt** et **Export-UMPrompt**.

Pour les autres tâches de gestion relatives aux plans de numérotation de messagerie unifiée, consultez la rubrique [Procédures de plan de numérotation de messagerie unifiée](um-dial-plan-procedures-exchange-2013-help.md).

Pour les autres tâches de gestion relatives aux standards automatiques de messagerie unifiée, consultez la rubrique [Procédures relatives au standard automatique de messagerie unifiée](um-auto-attendant-procedures-exchange-2013-help.md).

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : 3 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez les entrées « Plans de numérotation de messagerie unifiée » et « Standards automatiques de messagerie unifiée » dans la rubrique [Autorisations de messagerie unifiée](unified-messaging-permissions-exchange-2013-help.md).

  - Avant d'exécuter ces procédures, vérifiez qu'un plan de numérotation de messagerie unifiée a été créé. Pour obtenir la procédure détaillée, consultez la rubrique [Créer un plan de numérotation de messagerie unifiée](create-a-um-dial-plan-exchange-2013-help.md).

  - Avant d'exécuter ces procédures, vérifiez qu'un standard automatique de messagerie unifiée a été créé. Pour obtenir la procédure détaillée, consultez la rubrique [Créer un standard automatique de messagerie unifiée](create-a-um-auto-attendant-exchange-2013-help.md).

  - Vous pouvez uniquement utiliser l'environnement de ligne de commande Exchange Management Shell pour effectuer cette tâche.

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..


## Que souhaitez-vous faire ?

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour importer des messages d'accueil, des annonces, des menus et des invites personnalisés dans des plans de numérotation et des standards automatiques de messagerie unifiée

Cet exemple importe le fichier de message d'accueil welcomegreeting.wav à partir de d:\\UMPrompts dans le plan de numérotation de messagerie unifiée `MyUMDialPlan`.

    [byte[]]$c = Get-content -Path "d:\UMPrompts\welcomegreeting.wav" -Encoding Byte -ReadCount 0
    Import-UMPrompt -UMDialPlan MyUMDialPlan -PromptFileName "welcomegreeting.wav" -PromptFileData $c

Cet exemple importe le fichier de message d'accueil welcomegreeting.wav à partir de d:\\UMPrompts dans le standard automatique de messagerie unifiée `MyUMAutoAttendant`.

    [byte[]]$c = Get-content -Path "d:\UMPrompts\welcomegreeting.wav" -Encoding Byte -ReadCount 0
    Import-UMPrompt -UMAutoAttendant MyUMAutoAttendant -PromptFileName "welcomegreeting.wav" -PromptFileData $c

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour exporter des messages d'accueil, des annonces, des menus et des invites personnalisés à partir de plans de numérotation et de standards automatiques de messagerie unifiée

Cet exemple exporte le message d'accueil du plan de numérotation de messagerie unifiée `MyUMDialPlan` et l'enregistre en tant que fichier welcomegreeting.wav.

    $prompt = Export-UMPrompt -PromptFileName "customgreeting.wav�? -UMDialPlan MyUMDialPlan
    set-content -Path "d:\DialPlanPrompts\welcomegreeting.wav" -Value $prompt.AudioData -Encoding Byte

Cet exemple exporte le message d'accueil pendant les heures d'ouverture utilisé pour le standard automatique de messagerie unifiée `MYUMAutoAttendant` et l'enregistre en tant que fichier BusinessHoursWelcomeGreeting.wav.

    $prompt = Export-UMPrompt -BusinessHoursWelcomeGreeting -UMAutoAttendant MyUMAutoAttendant
    set-content -Path "d:\UMPrompts\BusinessHoursWelcomeGreeting.wav" -Value $prompt.AudioData -Encoding Byte

