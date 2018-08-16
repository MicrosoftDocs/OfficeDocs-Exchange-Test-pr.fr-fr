---
title: 'Activer connexion à la messag. voc. sans code confidentiel: Exchange 2013 Help'
TOCTitle: Activation de la connexion à la messagerie vocale sans code confidentiel
ms:assetid: 54133753-317c-42ef-9b0d-ca9f2d2d6bd7
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Gg602127(v=EXCHG.150)
ms:contentKeyID: 54652754
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Activation de la connexion à la messagerie vocale sans code confidentiel

 

_**Sapplique à :** Exchange Server 2010 Service Pack 2 (SP2), Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2015-04-08_

Vous pouvez configurer la messagerie unifiée pour permettre aux utilisateurs de se connecter à leur messagerie vocale sans utiliser de code confidentiel. Par défaut, les utilisateurs d'Outlook Voice Access sont invités à saisir un code confidentiel pour se connecter à leur boîte aux lettres et accéder à leurs messages vocaux et électroniques, leur calendrier, leurs contacts personnels, l'annuaire et les options personnelles.

> [!WARNING]
> En permettant à un utilisateur unique ou à un groupe d'utilisateurs à extension messagerie vocale de se connecter sans code confidentiel, cela réduit le niveau de sécurité de la messagerie vocale et pose un risque de sécurité pour votre organisation.


Pour activer les connexions sans code confidentiel, vous devez définir le paramètre *AllowPinlessVoiceMailAccess* sur `$true` dans la stratégie de boîte aux lettres de messagerie unifiée, et définir le paramètre *PinlessAccessToVoiceMailEnabled* sur `$true` dans la boîte aux lettres de messagerie unifiée. Par défaut, ces deux paramètres sont définis sur `$false`, ce qui oblige les utilisateurs d'Outlook Voice Access à saisir leur code confidentiel pour accéder à leur messagerie vocale.

Vous pouvez définir ces deux paramètres sur `$true` pour autoriser les connexions sans code confidentiel, soit pour un nombre élevé d'utilisateurs associés à une boîte aux lettres de messagerie unifiée, soit pour une seule boîte aux lettres de messagerie unifiée (ou pour un nombre réduit de ces boîtes). Même si vous activez les connexions sans code confidentiel pour un groupe d'utilisateurs (ou un seul) à extension messagerie unifiée, ils devront encore saisir leur code confidentiel pour accéder à leur messagerie électronique, leur calendrier, leurs contacts personnels, l'annulaire ou leurs options personnelles.

Pour activer les connexions sans code confidentiel pour un utilisateur, les conditions suivantes doivent être réunies :

  - Vous avez exécuté la cmdlet suivante sur la stratégie de boîte aux lettres de messagerie unifiée : `Set-UMMailboxPolicy -id MyUMMailboxPolicy -AllowPinlessVoiceMailAccess $true`

  - Vous avez exécuté la cmdlet suivante sur la boîte aux lettres de l’utilisateur à extension messagerie unifiée : `Set-UMMailbox -id tonys@contoso.com -PinlessAccessToVoiceMailEnabled $true`

  - L'utilisateur à extension messagerie unifiée est associé à la même stratégie de boîte aux lettres de messagerie unifiée pour laquelle vous avez activé les connexions sans code confidentiel.

  - L’utilisateur à extension messagerie unifiée se connecte à Outlook Voice Access en appelant un numéro de téléphone qui lui a été attribué.

  - Vous pouvez uniquement utiliser l'environnement de ligne de commande Exchange Management Shell pour effectuer cette tâche. Pour apprendre à ouvrir l’environnement de ligne de commande Environnement de ligne de commande Exchange Management Shell dans votre organisation Exchange locale, reportez-vous à [Ouvrir le Shell](https://technet.microsoft.com/fr-fr/library/dd638134\(v=exchg.150\)). Pour apprendre à utiliser Windows PowerShell afin de vous connecter à Exchange Online, consultez la rubrique [Connexion à Exchange Online PowerShell](https://go.microsoft.com/fwlink/p/?linkid=396554).

Pour d'autres tâches relatives aux stratégies de boîte aux lettres de messagerie unifiée, consultez la rubrique [Procédures de stratégie de boîte aux lettres de messagerie unifiée](um-mailbox-policy-procedures-exchange-2013-help.md).

Pour d'autres tâches relatives aux boîtes aux lettres de messagerie unifiée, consultez la rubrique [Voix des procédures de l'utilisateur à extension messagerie](voice-mail-enabled-user-procedures-exchange-2013-help.md).

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : 3 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l'entrée « Stratégies de boîte aux lettres de messagerie unifiée » dans la rubrique [Autorisations de messagerie unifiée](unified-messaging-permissions-exchange-2013-help.md).

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l'entrée « Boîtes aux lettres de messagerie unifiée » dans la rubrique [Autorisations de messagerie unifiée](unified-messaging-permissions-exchange-2013-help.md).

  - Avant d'exécuter ces procédures, vérifiez qu'un plan de numérotation de messagerie unifiée a été créé. Pour obtenir la procédure détaillée, consultez la rubrique [Créer un plan de numérotation de messagerie unifiée](create-a-um-dial-plan-exchange-2013-help.md).

  - Avant d'effectuer ces procédures, vérifiez qu'une stratégie de boîte aux lettres de messagerie unifiée a été créée. Pour obtenir la procédure détaillée, consultez la rubrique [Créer une stratégie de boîte aux lettres de messagerie unifiée](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Avant d'effectuer ces procédures, vérifiez que la messagerie unifiée et la messagerie vocale ont été activées pour le ou les utilisateurs. Pour obtenir la procédure détaillée, consultez la rubrique [Activation de la messagerie vocale pour un utilisateur](enable-a-user-for-voice-mail-exchange-2013-help.md).

## Que souhaitez-vous faire ?

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour activer l'accès sans code confidentiel à la messagerie vocale pour des utilisateurs à extension messagerie unifiée dans la stratégie de boîte aux lettres de messagerie unifiée

Cet exemple illustre l'activation de l'accès sans code confidentiel à la messagerie vocale, dans une stratégie de boîte aux lettres de messagerie unifiée appelée `MyUMMailboxPolicy`, pour les utilisateurs associés à la stratégie de boîte aux lettres qui se connectent (par appel) à Outlook Voice Access.

    Set-UMMailboxPolicy -id MyUMMailboxPolicy -AllowPinlessVoiceMailAccess $true

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour activer l'accès sans code confidentiel à la messagerie vocale sur la boîte aux lettres d'un utilisateur à extension messagerie unifiée

Cet exemple illustre l'activation d'un accès sans code confidentiel à la messagerie vocale pour un utilisateur qui se connecte (par appel) à Outlook Voice Access pour atteindre la boîte aux lettres appelée `tonys@contoso.com`.

    Set-UMMailbox -id tonys@contoso.com -PinlessAccessToVoiceMailEnabled $true

