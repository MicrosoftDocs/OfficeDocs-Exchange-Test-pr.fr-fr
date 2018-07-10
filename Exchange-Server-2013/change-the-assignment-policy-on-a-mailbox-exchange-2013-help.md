---
title: 'Modifier la stratégie d’attribution sur une boîte aux lettres: Exchange 2013 Help'
TOCTitle: Modifier la stratégie d’attribution sur une boîte aux lettres
ms:assetid: 011690a5-233a-4c03-8842-92276f899a89
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dd638076(v=EXCHG.150)
ms:contentKeyID: 50477416
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Modifier la stratégie d’attribution sur une boîte aux lettres

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2012-10-08_

Vous pouvez modifier la stratégie d’attribution de rôle de gestion affectée à une boîte aux lettres. Lorsque vous modifiez la stratégie d’attribution d’une boîte aux lettres, la modification prend effet dès que l’utilisateur actualise la connexion (par exemple, lorsqu’il se connecte de nouveau à sa boîte aux lettres ou qu’il ouvre la page d’options de la boîte aux lettres). Pour plus d’informations sur les stratégies d’attribution dans Microsoft Exchange Server 2013, consultez la rubrique [Présentation des stratégies d’attribution de rôle de gestion](understanding-management-role-assignment-policies-exchange-2013-help.md).

Souhaitez-vous rechercher les autres tâches de gestion relatives aux autorisations ? Consultez la rubrique [Autorisations](permissions-exchange-2013-help.md).

## Ce qu’il faut savoir avant de commencer ?

  - Durée d’exécution estimée de chaque procédure : 5 minutes

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l’entrée « Groupes de rôles » dans la rubrique [Autorisations pour la gestion des rôles](role-management-permissions-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.


## Utiliser le Centre d’administration Exchange pour modifier la stratégie d’attribution d’une boîte aux lettres

1.  Dans le Centre d’administration Exchange, accédez à **Destinataires** \> **Boîtes aux lettres**.

2.  Sélectionnez la boîte aux lettres d’utilisateurs ou de ressources pour laquelle vous souhaitez modifier la stratégie d’attribution, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

3.  Sélectionnez **Fonctionnalités de boîte aux lettres**.

4.  Dans la liste **Stratégie d’attribution de rôle**, sélectionnez la stratégie d’attribution que vous souhaitez attribuer à la boîte aux lettres, puis cliquez sur **Enregistrer**.

## Utilisez l’environnement de ligne de commande Exchange Management Shell pour modifier la stratégie d’attribution d’une boîte aux lettres

Pour modifier la stratégie d’attribution qui est affectée à une boîte aux lettres, utilisez la syntaxe suivante.

    Set-Mailbox <mailbox alias or name> -RoleAssignmentPolicy <assignment policy>

Cet exemple définit la stratégie d’attribution aux utilisateurs de messagerie unifiée sur la boîte aux lettres de Fabrice.

    Set-Mailbox Brian -RoleAssignmentPolicy "Unified Messaging Users"

## Utilisez l’environnement de ligne de commande Exchange Management Shell pour modifier la stratégie d’attribution sur un groupe de boîtes aux lettres pour lesquelles une stratégie d’attribution spécifique a été affectée

> [!NOTE]
> Vous ne pouvez pas utiliser le Centre d’administration Exchange pour modifier en une fois la stratégie d’attribution d’un groupe de boîtes aux lettres.


Cette procédure utilise le pipelining, la cmdlet **Where** et le paramètre *WhatIf*. Pour plus d’informations sur ces concepts, consultez les rubriques suivantes :

  - [Traitement en pipeline](https://technet.microsoft.com/fr-fr/library/aa998260\(v=exchg.150\))

  - [Utilisation de la sortie de la commande](working-with-command-output-exchange-2013-help.md)

  - [Commutateurs WhatIf, Confirm et ValidateOnly](whatif-confirm-and-validateonly-switches-exchange-2013-help.md)

Si vous souhaitez modifier la stratégie d’attribution pour un groupe de boîtes aux lettres pour lesquelles une stratégie spécifique est attribuée, utilisez la syntaxe suivante.

    Get-Mailbox | Where { $_.RoleAssignmentPolicy -Eq "<assignment policy to find>" } | Set-Mailbox -RoleAssignmentPolicy <assignment policy to set>

Cet exemple recherche toutes les boîtes aux lettres attribuées aux utilisateurs de Redmond. Aucune stratégie d’attribution de messagerie vocale et aucune modification de la stratégie d’attribution aux utilisateurs de Redmond. Messagerie vocale activée.

    Get-Mailbox | Where { $_.RoleAssignmentPolicy -Eq "Redmond Users - No Voicemail" } | Set-Mailbox -RoleAssignmentPolicy "Redmond Users - Voicemail Enabled"

Cet exemple inclut le paramètre *WhatIf*. Ainsi, vous pouvez voir toutes les boîtes aux lettres qui seront modifiées sans effectuer de modification.

    Get-Mailbox | Where { $_.RoleAssignmentPolicy -Eq "Redmond Users - No Voicemail" } | Set-Mailbox -RoleAssignmentPolicy "Redmond Users - Voicemail Enabled" -WhatIf

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Get-Mailbox](https://technet.microsoft.com/fr-fr/library/bb123685\(v=exchg.150\)) et [Set-Mailbox](https://technet.microsoft.com/fr-fr/library/bb123981\(v=exchg.150\)).

