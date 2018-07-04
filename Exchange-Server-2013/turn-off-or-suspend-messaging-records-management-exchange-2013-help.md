---
title: 'Désactivation ou suspension de la gestion des enregistrements de messagerie: Exchange 2013 Help'
TOCTitle: Désactivation ou suspension de la gestion des enregistrements de messagerie
ms:assetid: 631191aa-3bba-4ebf-a727-c48ed2ebe176
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Aa998580(v=EXCHG.150)
ms:contentKeyID: 52062965
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Désactivation ou suspension de la gestion des enregistrements de messagerie

 

_**Sapplique à :** Exchange Server 2010 Service Pack 2 (SP2), Exchange Server 2013_

_**Dernière rubrique modifiée :** 2013-02-14_

Pour répondre aux besoins d'un individu, d'un service informatique ou de l'entreprise, vous devez désactiver ou suspendre temporairement la gestion des enregistrements de messagerie (MRM) d'un utilisateur en particulier ou d'un serveur de boîtes aux lettres. La désactivation ou la suspension de la gestion des enregistrements de messagerie peut s'avérer nécessaire dans les cas suivants :

  - Si l'utilisateur d'une boîte aux lettres s'absente du bureau ou s'il ne parvient pas à accéder à sa messagerie, vous pouvez désactiver temporairement la gestion des enregistrements de messagerie relative à la boîte aux lettres en activant le blocage de rétention pour cette dernière. Lorsque le blocage de rétention est activé, la boîte aux lettres ne peut plus être traitée par l'Assistant Dossier géré. Lorsque l'utilisateur de la boîte aux lettres est de retour ou qu'il peut accéder de nouveau à la boîte aux lettres, vous pouvez supprimer le blocage de rétention de la boîte aux lettres.

  - Si vous devez tester ou résoudre des problèmes liés aux performances, vous pouvez désactiver temporairement la gestion des enregistrements de messagerie en supprimant la planification pour l'Assistant Dossier géré.

  - Si vous souhaitez éliminer une balise de rétention des boîtes aux lettres (qui sont associées à une stratégie de rétention à laquelle s'applique cette balise), vous pouvez supprimer la balise de la stratégie.

  - Pour cesser d'appliquer une stratégie de rétention ou de boîte aux lettres de dossier géré à une boîte aux lettres, vous pouvez supprimer la stratégie de la boîte aux lettres.

  - Si votre organisation décide de ne pas utiliser les fonctionnalités de gestion des enregistrements de messagerie, vous pouvez les désactiver définitivement pour l'ensemble de l'organisation. Vous pouvez toujours déployer ultérieurement la gestion des enregistrements de messagerie, si vous le souhaitez.

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : 1 minute

  - Les procédures décrites dans cette rubrique requièrent des autorisations spécifiques. Consultez chaque procédure pour savoir quelles autorisations sont nécessaires.

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), et [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

## Que souhaitez-vous faire ?

## Activation du blocage de rétention des boîtes aux lettres

Vous pouvez activer le blocage de rétention des boîtes aux lettres pour désactiver temporairement la gestion des enregistrements de messagerie (par exemple, lorsque les utilisateurs sont en congé). Le traitement des stratégies de rétention est alors suspendu pour la boîte aux lettres jusqu'à la désactivation du blocage de rétention. Cette fonctionnalité diffère de l'activation de l'archive permanente ou de la mise en attente pour litige.

Pour plus d'informations sur la procédure d'activation du blocage de rétention d'une boîte aux lettres, consultez la rubrique [Placer une boîte aux lettres en blocage de rétention](place-a-mailbox-on-retention-hold-exchange-2013-help.md).

Pour en savoir plus sur l'archive permanente et la mise en attente pour litige, consultez la rubrique [Conservation inaltérable et conservation pour litige](in-place-hold-and-litigation-hold-exchange-2013-help.md).

## Suppression de balises de rétention des boîtes aux lettres

Pour supprimer une balise de rétention d'une boîte aux lettres, vous devez dissocier la balise de la stratégie de rétention. Lorsque vous dissociez une balise de stratégie de rétention (RPT) pour un dossier par défaut, la balise de boîte aux lettres par défaut s'applique à tous les éléments contenus dans ce dossier. Lorsque vous dissociez une balise personnelle, elle n'est plus accessible à l'utilisateur. Les balises appliquées aux messages existants continueront à être traitées tant que vous ne les supprimez de votre organisation Exchange.

Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l'entrée « Gestion des enregistrements de messagerie » dans la rubrique [Stratégie de messagerie et autorisations de conformité](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

Cet exemple d'environnement de ligne de commande illustre la dissociation de la balise de rétention Supprimer - 3 jours de la stratégie de rétention Corp-Users.

    $tags = (Get-RetentionPolicy "Corp-Users").RetentionPolicyTagLinks
    $tags -= "Deleted Items - 3 Days"
    Set-RetentionPolicy "Corp-Users" -RetentionPolicyTagLinks $tags

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, consultez les rubriques [Get-RetentionPolicy](https://technet.microsoft.com/fr-fr/library/dd298086\(v=exchg.150\)) et [Set-RetentionPolicy](https://technet.microsoft.com/fr-fr/library/dd335196\(v=exchg.150\)).

## Suppression de stratégies de rétention des boîtes aux lettres

Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l'entrée « Application des stratégies de rétention » dans la rubrique [Stratégie de messagerie et autorisations de conformité](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

Vous pouvez cesser l'application d'une stratégie de rétention à une boîte aux lettres en supprimant la stratégie des propriétés de l'utilisateur de la boîte aux lettres.

Cet exemple d'environnement de ligne de commande montre comment supprimer la stratégie de rétention de la boîte aux lettres jpeoples.

    Set-Mailbox jpeoples -RetentionPolicy $null.

Cet exemple d'environnement de ligne de commande illustre la suppression de la stratégie de rétention de toutes les boîtes aux lettres de l'organisation Exchange.

    Get-Mailbox -ResultSize unlimited -Filter {RetentionPolicy -ne $null} | Set-Mailbox -RetentionPolicy $null

Cet exemple d'environnement de ligne de commande montre comment supprimer la stratégie de rétention Corp-Finance de tous les utilisateurs de boîtes aux lettres ayant appliqué cette stratégie.

    Get-Mailbox -ResultSize unlimited -Filter {RetentionPolicy -eq "Corp-Finance"} | Set-Mailbox -RetentionPolicy $null

Pour des informations détaillées sur la syntaxe et les paramètres, consultez les rubriques [Set-Mailbox](https://technet.microsoft.com/fr-fr/library/bb123981\(v=exchg.150\)) et [Get-Mailbox](https://technet.microsoft.com/fr-fr/library/bb123685\(v=exchg.150\)).

## Désactivation définitive de la gestion des enregistrements de messagerie pour une organisation complète

Pour désactiver la gestion des enregistrements de messagerie d'une organisation, supprimez toutes les balises et stratégies de rétention, sauf pour la stratégie ArbitrationMailbox qui est créée par le programme d'installation d'Exchange. Une fois cette opération terminée, les stratégies de rétention ne sont plus appliquées.

> [!CAUTION]
> Les stratégies de rétention incluent également les balises Déplacer vers l'archive qui permettent de déplacer des messages vers la boîte aux lettres d'archivage de l'utilisateur. Si vous supprimez une stratégie de rétention qui dispose d'une balise Déplacer vers l'archive, les messages des utilisateurs auxquels cette stratégie a été appliquée ne seront plus déplacés vers l'archive par l'Assistant Dossier géré.
> Pour éviter cette situation, supprimez uniquement les balises Supprimer et autoriser la récupération et Supprimer définitivement de votre organisation et conservez les stratégies auxquelles ont été appliquées les balises Déplacer vers l'archive. Les utilisateurs disposant d'une archive peuvent aussi déplacer manuellement des éléments dans leur boîte aux lettres d'archivage à l'aide d'Outlook ou d'Outlook Web App.
> Avant de supprimer des balises ou des stratégies de rétention, nous vous conseillons de vérifier les paramètres des balises en cours de suppression. Ne supprimez pas des balises associées à l'action de rétention Déplacer vers l'archive.


Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l'entrée « Gestion des enregistrements de messagerie » dans la rubrique [Stratégie de messagerie et autorisations de conformité](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

> [!NOTE]
> Incluez le commutateur <em>WhatIf</em> dans les commandes suivantes pour simuler l'action entreprise par la commande.


Cet exemple supprime toutes les balises de rétention dans une organisation Exchange à l'exception de la balise Ne jamais supprimer, qui est utilisée dans la stratégie ArbitrationMailbox créée par le programme d'installation d'Exchange.

    Get-RetentionPolicyTag | ? {$_.RetentionAction -ne "MoveToArchive" -and $_.Name -ne "Never Delete"} | Remove-RetentionPolicyTag

Cet exemple supprime toutes les balises de rétention à l'exception de la balise Ne jamais supprimer.

    Get-RetentionPolicyTag | ? {$_.Name -ne "Never Delete"} | Remove-RetentionPolicyTag

Cette commande supprime la stratégie de rétention Corp-Users d'une organisation Exchange.

    Remove-RetentionPolicy Corp-Users

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, consultez les rubriques suivantes :

  - [Get-RetentionPolicyTag](https://technet.microsoft.com/fr-fr/library/dd298009\(v=exchg.150\))

  - [Remove-RetentionPolicyTag](https://technet.microsoft.com/fr-fr/library/dd335092\(v=exchg.150\))

  - [Remove-RetentionPolicy](https://technet.microsoft.com/fr-fr/library/dd297962\(v=exchg.150\))

