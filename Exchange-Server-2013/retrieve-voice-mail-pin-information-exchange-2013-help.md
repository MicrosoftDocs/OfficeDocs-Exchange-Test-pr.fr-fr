---
title: 'Extraction des informations de code confidentiel de messagerie vocale: Exchange 2013 Help'
TOCTitle: Extraction des informations de code confidentiel de messagerie vocale
ms:assetid: 01517cca-99fe-46b2-b586-19e8d2707728
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Aa995900(v=EXCHG.150)
ms:contentKeyID: 54652716
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Extraction des informations de code confidentiel de messagerie vocale

 

_**Sapplique à :** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2013-04-03_

Vous pouvez extraire des informations de code confidentiel d'un utilisateur à extension de messagerie unifiée. Quand un utilisateur a été activé pour la messagerie unifiée et qu'un code confidentiel a été généré ou créé, le code confidentiel est chiffré et stocké dans la boîte aux lettres de l'utilisateur.

Quand vous extrayez des informations de code confidentiel pour un utilisateur à extension messagerie unifiée, les informations retournées sont calculées à l'aide des données chiffrées du code confidentiel stockées dans la boîte aux lettres de l'utilisateur. Cela vous permet d'afficher des informations de la boîte aux lettres de l'utilisateur et de déterminer si ce dernier peut encore accéder ou non à sa boîte aux lettres.

Pour les tâches supplémentaires concernant la sécurité du code confidentiel, consultez la rubrique [Procédures de sécurité de code confidentiel](pin-security-procedures-exchange-2013-help.md).

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : moins d'une minute.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l'entrée « Plans de numérotation de messagerie unifiée » dans la rubrique [Autorisations de messagerie unifiée](unified-messaging-permissions-exchange-2013-help.md).

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l'entrée « Boîtes aux lettres de messagerie unifiée » dans la rubrique [Autorisations de messagerie unifiée](unified-messaging-permissions-exchange-2013-help.md).

  - Avant d'exécuter ces procédures, vérifiez qu'un plan de numérotation de messagerie unifiée a été créé. Pour obtenir la procédure détaillée, consultez la rubrique [Créer un plan de numérotation de messagerie unifiée](create-a-um-dial-plan-exchange-2013-help.md).

  - Avant d'effectuer ces procédures, vérifiez qu'une stratégie de boîte aux lettres de messagerie unifiée a été créée. Pour obtenir la procédure détaillée, consultez la rubrique [Créer une stratégie de boîte aux lettres de messagerie unifiée](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Avant d'effectuer ces procédures, vérifiez que la boîte aux lettres de l'utilisateur a été activée pour la messagerie unifiée. Pour obtenir la procédure détaillée, consultez la rubrique [Activation de la messagerie vocale pour un utilisateur](enable-a-user-for-voice-mail-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..


## Que souhaitez-vous faire ?

## Utilisation du CAE pour extraire les informations de code confidentiel d'un utilisateur à extension messagerie unifiée

1.  Dans le CAE, accédez à **Destinataires**. Dans l'affichage Liste, sélectionnez la boîte aux lettres utilisateur à afficher.

2.  Dans le volet d'informations, sous **Fonctionnalités téléphoniques et vocales**, cliquez sur **Afficher les détails**.

3.  Dans la page **Boîte aux lettres de messagerie unifiée** \> **Paramètres de la boîte aux lettres de messagerie unifiée**, affichez le **statut du code confidentiel** de l'utilisateur. Dans cette page, vous pouvez également réinitialiser le code confidentiel de messagerie vocale de l'utilisateur.

## Utilisation du Shell pour extraire des informations de code confidentiel d'un utilisateur à extension messagerie unifiée

Cet exemple affiche l'ID utilisateur, indique si le code confidentiel a expiré, si la boîte aux lettres de messagerie unifiée est verrouillée et si Tony est un nouvel utilisateur.

    Get-UMMailboxPIN -identity tony@contoso.com

