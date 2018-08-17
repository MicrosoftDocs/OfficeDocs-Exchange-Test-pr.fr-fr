---
title: 'Gérer les stratégies d’attribution des rôles: Exchange 2013 Help'
TOCTitle: Gérer les stratégies d’attribution des rôles
ms:assetid: f93d502e-5df4-4ba0-b68d-01a17ccffb4d
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ657511(v=EXCHG.150)
ms:contentKeyID: 50479596
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Gérer les stratégies d’attribution des rôles

 

_**Sapplique à :** Exchange Online, Exchange Server 2013_

_**Dernière rubrique modifiée :** 2012-10-09_

Si vous voulez personnaliser les autorisations que vous accordez à un groupe d'utilisateurs finaux, vous devez créer une stratégie d'attribution de rôle de gestion personnalisée. Vous pouvez personnaliser la stratégie d'attribution que vous créez de sorte qu'elle réponde aux besoins spécifiques de vos utilisateurs finaux. Pour plus d’informations sur les stratégies d’attribution dans Microsoft Exchange Server 2013, consultez la rubrique [Présentation des stratégies d’attribution de rôle de gestion](understanding-management-role-assignment-policies-exchange-2013-help.md).

Souhaitez-vous rechercher les autres tâches de gestion relatives à la gestion des autorisations ? Consultez la rubrique [Autorisations](permissions-exchange-2013-help.md).

## Ce qu’il faut savoir avant de commencer ?

  - Durée d’exécution estimée de chaque procédure : 5 minutes

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Stratégies d’attribution » dans la rubrique [Autorisations pour la gestion des rôles](role-management-permissions-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.


## Que souhaitez-vous faire ?

## Ajouter une stratégie d’attribution

Après avoir créé la nouvelle stratégie d’attribution, vous devez lui affecter des utilisateurs. Pour plus d'informations, voir [Modifier la stratégie d’attribution sur une boîte aux lettres](change-the-assignment-policy-on-a-mailbox-exchange-2013-help.md).

## Utiliser le Centre d'administration Exchange (CAE) pour créer une stratégie d’attribution

> [!NOTE]
> Vous pouvez créer des stratégies d’attribution explicites uniquement à l’aide du Centre d’administration Exchange (CAE). Pour créer une nouvelle stratégie d’attribution par défaut, vous devez faire appel à l’environnement de ligne de commande Exchange Management Shell. Pour plus d’informations, consultez la section « Utiliser l’environnement de ligne de commande Exchange Management Shell pour créer une stratégie d’attribution par défaut» plus loin dans cette rubrique.


1.  Dans le CAE, accédez à **Autorisations** \> **Rôles de l'utilisateur** et cliquez ensuite sur **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter").

2.  Dans la fenêtre de stratégie d’attribution des rôles, entrez un nom pour la nouvelle stratégie d'attribution.

3.  Activez la case à cocher en regard du ou des rôles que vous souhaitez ajouter à la stratégie d’attribution. Vous pouvez sélectionner plusieurs rôles, y compris les rôles d’utilisateur final que vous avez ajoutés. Si vous sélectionnez un rôle avec des rôles enfants, ces derniers sont automatiquement sélectionnés.

4.  Cliquez sur **Enregistrer** pour enregistrer les modifications apportées à la stratégie d’attribution.

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour créer une stratégie d'attribution explicite

Pour créer une stratégie d'attribution explicite qui peut être affectée manuellement à des boîtes aux lettres, utilisez la syntaxe suivante.

    New-RoleAssignmentPolicy <assignment policy name> -Roles <roles to assign>

Cet exemple crée la stratégie d’attribution explicite « Limited Mailbox Configuration » et lui attribue les rôles `MyBaseOptions`, `MyAddressInformation` et `MyDisplayName`.

    New-RoleAssignmentPolicy "Limited Mailbox Configuration" -Roles MyBaseOptions, MyAddressInformation, MyDisplayName

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [New-RoleAssignmentPolicy](https://technet.microsoft.com/fr-fr/library/dd638101\(v=exchg.150\)).

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour créer une stratégie d'attribution par défaut

Pour créer une stratégie d'attribution par défaut à affecter aux nouvelles boîtes aux lettres, utilisez la syntaxe suivante.

    New-RoleAssignmentPolicy <assignment policy name> -Roles <roles to assign> -IsDefault

Cet exemple crée la stratégie d’attribution par défaut « Limited Mailbox Configuration » et lui attribue les rôles `MyBaseOptions`, `MyAddressInformation` et `MyDisplayName`.

    New-RoleAssignmentPolicy "Limited Mailbox Configuration" -Roles MyBaseOptions, MyAddressInformation, MyDisplayName -IsDefault

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [New-RoleAssignmentPolicy](https://technet.microsoft.com/fr-fr/library/dd638101\(v=exchg.150\)).

## Supprimer une stratégie d’attribution

Si vous n'avez plus besoin d'une stratégie d'attribution de rôle de gestion, vous pouvez la supprimer.

## Ce qu’il faut savoir avant de commencer ?

  - Tous les utilisateurs disposant de la stratégie d'attribution doivent se voir assigner une autre stratégie d'attribution. Pour plus d'informations sur le changement de stratégie d'attribution pour une boîte aux lettres, voir [Modifier la stratégie d’attribution sur une boîte aux lettres](change-the-assignment-policy-on-a-mailbox-exchange-2013-help.md).

  - Toutes les attributions de rôle de gestion entre la stratégie d'attribution et les rôles de gestion attribués doivent être supprimées. Pour plus d'informations sur la suppression d'une attribution de rôle d'une stratégie d'attribution, voir le paragraphe Utiliser l'environnement de ligne de commande Exchange Management Shell pour supprimer un rôle d'une stratégie d'attribution plus loin dans cette rubrique.

  - Si vous souhaitez supprimer une stratégie d'attribution par défaut, il doit s'agir de la dernière stratégie d'attribution dans l'organisation Exchange 2013.

## Utiliser le Centre d'administration Exchange (CAE) pour supprimer une stratégie d’attribution

1.  Dans le CAE, accédez à **Autorisations** \> **Rôles utilisateurs**.

2.  Sélectionnez la stratégie d’attribution à supprimer, puis cliquez sur **Supprimer**![Icône Supprimer](images/Dd979797.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "Icône Supprimer").

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour supprimer une stratégie d'attribution

Pour supprimer une stratégie d'attribution, utilisez la syntaxe suivante.

    Remove-RoleAssignmentPolicy <role assignment policy>

Cet exemple supprime la stratégie d'attribution New York Temporary Users.

    Remove-RoleAssignmentPolicy "New York Temporary Users"

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Remove-RoleAssignmentPolicy](https://technet.microsoft.com/fr-fr/library/dd638190\(v=exchg.150\)).

## Afficher la liste des stratégies d'attribution ou les détails d'une stratégie d'affectation

Selon que vous utilisez le Centre d'administration Exchange (CAE) ou l’environnement de ligne de commande et en fonction des informations désirées, vous pouvez afficher les stratégies d’attribution des rôles de gestion de diverses manières.

Dans le Centre d'administration Exchange (CAE), vous affichez la liste des stratégies d’attribution et les rôles qui leur sont associés. Dans l’environnement de ligne de commande, vous pouvez afficher l’ensemble des stratégies d’attribution de votre organisation ou répertorier les boîtes aux lettres auxquelles une stratégie spécifique est attribuée, entre autres tâches.

## Utiliser le Centre d'administration Exchange (CAE) pour afficher la liste des stratégies d’attribution

1.  Dans le CAE, accédez à **Autorisations** \> **Rôles utilisateurs**. Toutes les stratégies d'attribution de l'organisation sont répertoriées ici.

2.  Pour visualiser les détails d’une stratégie d’attribution spécifique, choisissez la stratégie que vous souhaitez afficher. La description et les rôles attribués à la stratégie d’attribution apparaissent dans le volet d’informations.

## Utiliser l’environnement de ligne de commande Exchange Management Shell pour afficher la liste des stratégies d’attribution

Vous pouvez afficher la liste de toutes les stratégies d’attribution de votre organisation en ne spécifiant aucune stratégie d’attribution lors de l’exécution de la cmdlet **Get-RoleAssignmentPolicy**.

Cette procédure décrit l’utilisation du pipelining et de la cmdlet **Format-Table**. Pour plus d’informations sur ces concepts, consultez les rubriques suivantes :

  - [Traitement en pipeline](https://technet.microsoft.com/fr-fr/library/aa998260\(v=exchg.150\))

  - [Utilisation de la sortie de la commande](working-with-command-output-exchange-2013-help.md)

Pour retourner la liste de toutes les stratégies d’attribution de votre organisation, utilisez la commande suivante.

    Get-RoleAssignmentPolicy

Pour retourner une liste de propriétés spécifiques de l’ensemble des stratégies d’attribution de votre organisation, vous pouvez transférer les résultats à la cmdlet **Format-Table** et indiquez les propriétés que vous souhaitez dans la liste des résultats. Utilisez la syntaxe suivante.

    Get-RoleAssignmentPolicy | Format-Table <property 1>, <property 2...>

Cet exemple renvoie la liste de toutes les stratégies d’attribution de votre organisation et inclut les propriétés **Name** et **IsDefault**.

    Get-RoleAssignmentPolicy | Format-Table Name, IsDefault

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Get-Mailbox](https://technet.microsoft.com/fr-fr/library/bb123685\(v=exchg.150\)) ou [Get-RoleAssignmentPolicy](https://technet.microsoft.com/fr-fr/library/dd638195\(v=exchg.150\)).

## Utiliser l’environnement de ligne de commande Exchange Management Shell pour afficher les détails d’une stratégie d’attribution unique

Vous pouvez afficher les détails d’une stratégie d’attribution spécifique via la cmdlet **Get-RoleAssignmentPolicy** et en transférant la sortie à la cmdlet **Format-List**.

Cette procédure décrit l’utilisation du pipelining et de la cmdlet **Format-List**. Pour plus d’informations sur ces concepts, consultez les rubriques suivantes :

  - [Traitement en pipeline](https://technet.microsoft.com/fr-fr/library/aa998260\(v=exchg.150\))

  - [Utilisation de la sortie de la commande](working-with-command-output-exchange-2013-help.md)

Pour afficher les détails d’une stratégie d’attribution spécifique, utilisez la syntaxe suivante.

    Get-RoleAssignmentPolicy <assignment policy name> | Format-List

Cet exemple affiche les détails de la stratégie d’attribution Redmond Users - no Text Messaging.

    Get-RoleAssignmentPolicy "Redmond Users - no Text Messaging" | Format-List

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Get-Mailbox](https://technet.microsoft.com/fr-fr/library/bb123685\(v=exchg.150\)) ou [Get-RoleAssignmentPolicy](https://technet.microsoft.com/fr-fr/library/dd638195\(v=exchg.150\)).

## Utiliser l’environnement de ligne de commande Exchange Management Shell pour rechercher la stratégie d’attribution par défaut

Vous pouvez rechercher la stratégie d’attribution par défaut en transférant la sortie de la cmdlet **Get-RoleAssignmentPolicy** vers la cmdlet **Where**. La cmdlet **Where** permet de filtrer les données retournées afin d’afficher uniquement la stratégie d’attribution dont la propriété *IsDefault* est définie sur `$True`.

Cette procédure décrit l’utilisation du pipelining et de la cmdlet **Where**. Pour plus d’informations sur ces concepts, consultez les rubriques suivantes :

  - [Traitement en pipeline](https://technet.microsoft.com/fr-fr/library/aa998260\(v=exchg.150\))

  - [Utilisation de la sortie de la commande](working-with-command-output-exchange-2013-help.md)

Cet exemple retourne la stratégie d’attribution par défaut.

    Get-RoleAssignmentPolicy | Where { $_.IsDefault -eq $True }

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Get-Mailbox](https://technet.microsoft.com/fr-fr/library/bb123685\(v=exchg.150\)) ou [Get-RoleAssignmentPolicy](https://technet.microsoft.com/fr-fr/library/dd638195\(v=exchg.150\)).

## Utiliser l’environnement de ligne de commande Exchange Management Shell pour afficher les boîtes aux lettres affectées à une stratégie spécifique

Vous pouvez rechercher l’ensemble des boîtes aux lettres auxquelles une stratégie d’attribution est affectée en transférant (pipe) la sortie de la cmdlet **Get-Mailbox** vers la cmdlet **Where**. La cmdlet **Where** permet de filtrer les données retournées afin d’afficher uniquement les boîtes aux lettres dont la propriété *RoleAssignmentPolicy* est définie sur le nom de stratégie d’attribution spécifié.

Cette procédure décrit l’utilisation du pipelining et de la cmdlet **Where**. Pour plus d’informations sur ces concepts, consultez les rubriques suivantes :

  - [Traitement en pipeline](https://technet.microsoft.com/fr-fr/library/aa998260\(v=exchg.150\))

  - [Utilisation de la sortie de la commande](working-with-command-output-exchange-2013-help.md)

Utilisez la syntaxe suivante.

    Get-Mailbox | Where { $_.RoleAssignmentPolicy -Eq "<role assignment policy>" }

Cet exemple montre comment rechercher toutes les boîtes aux lettres auxquelles est affectée la stratégie Vancouver End Users.

    Get-Mailbox | Where { $_.RoleAssignmentPolicy -Eq "Vancouver End Users" }

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Get-Mailbox](https://technet.microsoft.com/fr-fr/library/bb123685\(v=exchg.150\)) ou [Get-RoleAssignmentPolicy](https://technet.microsoft.com/fr-fr/library/dd638195\(v=exchg.150\)).

## Modifier la stratégie d’attribution par défaut

Vous pouvez modifier la stratégie d'attribution de rôle de gestion qui est appliquée aux nouvelles boîtes aux lettres créées. La modification de la stratégie par défaut d'affectation des rôles ne modifie pas la stratégie d'attribution affectée aux boîtes aux lettres existantes. Pour modifier la stratégie d'attribution affectée aux boîtes aux lettres existantes, voir [Modifier la stratégie d’attribution sur une boîte aux lettres](change-the-assignment-policy-on-a-mailbox-exchange-2013-help.md).

> [!NOTE]
> Vous ne pouvez pas utiliser le Centre d'administration Exchange (CAE) pour modifier la stratégie d'attribution par défaut. Vous devez utiliser l'environnement de ligne de commande (Shell).


## Utiliser l'environnement de ligne de commande Exchange Management Shell pour modifier la stratégie d'attribution par défaut

Pour modifier la stratégie d'attribution par défaut, utilisez la syntaxe suivante.

    Set-RoleAssignmentPolicy <assignment policy name> -IsDefault

Cet exemple définit la stratégie d'attribution « Vancouver End Users » comme stratégie d'attribution par défaut.

    Set-RoleAssignmentPolicy "Vancouver End Users" -IsDefault

> [!IMPORTANT]
> La stratégie d'attribution par défaut est appliquée aux nouvelles boîtes aux lettres, même si aucun rôle de gestion n'a été affecté à la stratégie. Les stratégies d’attribution pour les boîtes aux lettres sans rôle de gestion affecté ne peuvent pas accéder aux fonctions de configuration des boîtes aux lettres dans Microsoft Outlook Web App.


Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Set-RoleAssignmentPolicy](https://technet.microsoft.com/fr-fr/library/dd638090\(v=exchg.150\)).

## Ajouter un rôle à une stratégie d’attribution

## Utiliser le Centre d'administration Exchange (CAE) pour ajouter un rôle à une stratégie d’attribution

1.  Dans le CAE, accédez à **Autorisations** \> **Rôles utilisateurs**.

2.  Sélectionnez la stratégie d’attribution à laquelle vous voulez ajouter un ou plusieurs rôles, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

3.  Activez la case à cocher en regard du ou des rôles que vous souhaitez ajouter à la stratégie d’attribution. Vous pouvez sélectionner plusieurs rôles, y compris les rôles d’utilisateur final que vous avez ajoutés. Si vous sélectionnez un rôle avec des rôles enfants, ces derniers sont automatiquement sélectionnés.

4.  Cliquez sur **Enregistrer** pour enregistrer les modifications apportées à la stratégie d’attribution.

## Utiliser l’environnement de ligne de commande Exchange Management Shell pour ajouter un rôle à une stratégie d’attribution

Pour créer une attribution de rôle de gestion entre un rôle et une stratégie d’attribution, utilisez la syntaxe suivante.

    New-ManagementRoleAssignment -Name <role assignment name> -Role <role name> -Policy <assignment policy name>

Cet exemple montre comment créer l’attribution de rôle Utilisateurs de Seattle - Messagerie vocale entre le rôle Ma messagerie vocale et la stratégie d’attribution Utilisateurs de Seattle.

    New-ManagementRoleAssignment -Name "Seattle Users - Voicemail" -Role MyVoicemail -Policy "Seattle Users"

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [New-ManagementRoleAssignment](https://technet.microsoft.com/fr-fr/library/dd335193\(v=exchg.150\)).

## Supprimer un rôle d’une stratégie d’attribution

Si vous ne souhaitez pas que les utilisateurs finaux soient autorisés à gérer certaines fonctionnalités de leur boîte aux lettres ou de leur groupe de distribution, vous pouvez supprimer le rôle de gestion qui accorde les autorisations de la stratégie d’attribution de rôle de gestion à laquelle l’utilisateur est affecté. Si la même stratégie d'attribution est attribuée à d'autres utilisateurs, ceux-ci ne seront pas non plus autorisés à gérer ces fonctionnalités.

## Utiliser le Centre d'administration Exchange (CAE) pour supprimer un rôle d'une stratégie d’attribution

1.  Dans le CAE, accédez à **Autorisations** \> **Rôles utilisateurs**.

2.  Sélectionnez la stratégie d’attribution de laquelle vous souhaitez supprimer un ou plusieurs rôles, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

3.  Désactivez la case à cocher en regard du ou des rôles à supprimer de la stratégie d’attribution. Si vous désactivez la case à cocher pour un rôle contenant des rôles enfants, les cases à cocher de ces derniers sont également désactivées.

4.  Cliquez sur **Enregistrer** pour enregistrer les modifications apportées à la stratégie d’attribution.

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour supprimer un rôle d'une stratégie d'attribution

Vous pouvez supprimer des rôles des stratégies d’attribution en récupérant l’attribution de rôle de gestion associé à l’aide de la cmdlet **Get-ManagementRoleAssignment**, puis en canalisant l’attribution de rôle renvoyée sur la cmdlet **Remove-ManagementRoleAssignment**.

Pour plus d’informations sur les attributions de rôles normales ou de délégation, voir [Présentation des attributions de rôles de gestion](understanding-management-role-assignments-exchange-2013-help.md).

Cette procédure utilise le traitement en pipeline. Pour plus d’informations sur le traitement en pipeline, voir [Traitement en pipeline](https://technet.microsoft.com/fr-fr/library/aa998260\(v=exchg.150\)).

Pour supprimer un rôle d’une stratégie d’attribution, utilisez la syntaxe suivante.

    Get-ManagementRoleAssignment -RoleAssignee <assignment policy name> -Role <role name> | Remove-ManagementRoleAssignment

Cet exemple supprime le rôle de gestion MyVoicemail qui permet aux utilisateurs de gérer les options de leur messagerie vocale, à partir de la stratégie d’attribution Seattle Users.

    Get-ManagementRoleAssignment -RoleAssignee "Seattle Users" -Role MyVoicemail | Remove-ManagementRoleAssignment

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Remove-ManagementRoleAssignment](https://technet.microsoft.com/fr-fr/library/dd351205\(v=exchg.150\)).

