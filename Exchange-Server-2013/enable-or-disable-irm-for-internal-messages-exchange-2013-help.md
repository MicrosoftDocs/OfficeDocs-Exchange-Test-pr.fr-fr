---
title: 'Activer ou désactiver la technologie IRM pour les messages internes: Exchange 2013 Help'
TOCTitle: Activer ou désactiver la technologie IRM pour les messages internes
ms:assetid: a6a17f57-5304-41f1-954d-7301857d54a1
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb124077(v=EXCHG.150)
ms:contentKeyID: 50478831
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Activer ou désactiver la technologie IRM pour les messages internes

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2012-10-12_

Dans Microsoft Exchange Server 2013, la gestion des droits relatifs à l’information (IRM) est activée par défaut pour les messages internes. Cela vous permet de créer des règles de protection du transport et de protection Microsoft Outlook afin d’activer la protection IRM pour les messages pendant leur transport et sur les clients Microsoft Outlook 2010. L’activation de la gestion des droits relatifs à l’information est requise pour toutes les autres fonctionnalités IRM dans Exchange Server 2013, telles que le déchiffrement du transport, des règles de journal, IRM dans Microsoft Office Outlook Web App et IRM dans Microsoft Exchange ActiveSync.

> [!CAUTION]
> La désactivation de la gestion IRM pour les messages internes a également pour effet de désactiver toutes les fonctionnalités IRM dans l’organisation Exchange. Les fonctionnalités IRM côté client dans Outlook (notamment la capacité de lire, transférer et créer des messages protégés par IRM ou d’y répondre en utilisant un serveur Active Directory (AD RMS)), ne sont pas affectées.


Si vous souhaitez rechercher des tâches de gestion supplémentaires relatives à IRM, consultez [Procédures de gestion des droits relatifs à l’information](information-rights-management-procedures-exchange-2013-help.md).

## Ce qu’il faut savoir avant de commencer ?

  - Durée d'exécution estimée : 1 minute.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l’entrée « Protection des droits » dans la rubrique [Stratégie de messagerie et autorisations de conformité](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

  - Vous ne pouvez pas utiliser la console de gestion Exchange pour activer la gestion des droits relatifs à l’information pour les messages internes. Vous devez utiliser l'environnement de ligne de commande Exchange Management Shell.

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.


## Utiliser l’environnement de ligne de commande Exchange Management Shell pour activer la gestion des droits relatifs à l’information (IRM) pour les messages internes

Cet exemple active la gestion IRM pour les messages internes de l’organisation Exchange.

    Set-IRMConfiguration -InternalLicensingEnabled $true

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, consultez la rubrique [Set-IRMConfiguration](https://technet.microsoft.com/fr-fr/library/dd979792\(v=exchg.150\)).

## Utiliser l’environnement de ligne de commande Exchange Management Shell pour désactiver la gestion des droits relatifs à l’information (IRM) pour les messages internes

Cet exemple désactive la gestion IRM pour les messages internes de l’organisation Exchange.

    Set-IRMConfiguration -InternalLicensingEnabled $false

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Set-IRMConfiguration](https://technet.microsoft.com/fr-fr/library/dd979792\(v=exchg.150\)).

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez activé ou désactivé IRM pour les messages internes, utilisez la cmdlet [Get-IRMConfiguration](https://technet.microsoft.com/fr-fr/library/dd776120\(v=exchg.150\)) pour vérifier la configuration.

