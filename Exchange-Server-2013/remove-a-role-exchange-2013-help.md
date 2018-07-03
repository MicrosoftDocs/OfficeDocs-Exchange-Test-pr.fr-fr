---
title: 'Supprimer un rôle: Exchange 2013 Help'
TOCTitle: Supprimer un rôle
ms:assetid: 2fb6f453-f37a-4636-8353-3f9927f81298
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dd335178(v=EXCHG.150)
ms:contentKeyID: 50477801
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Supprimer un rôle

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2012-10-03_

Les rôles de gestion qui ne sont plus requis peuvent être supprimés de votre organisation. Vous ne pouvez supprimer que les rôles de gestion que vous avez créés. Les rôles de gestion intégrés ne peuvent pas être supprimés. Pour plus d’informations sur les rôles de gestion dans Microsoft Exchange Server 2013, voir [Présentation des rôles de gestion](understanding-management-roles-exchange-2013-help.md).

Souhaitez-vous rechercher les autres tâches de gestion relatives aux rôles ? Consultez la rubrique [Autorisations avancées](advanced-permissions-exchange-2013-help.md).

## Ce qu’il faut savoir avant de commencer ?

  - Durée d’exécution estimée de chaque procédure : 5 minutes

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l’entrée « Rôles de gestion » dans la rubrique [Autorisations pour la gestion des rôles](role-management-permissions-exchange-2013-help.md).

  - Vous devez utiliser l’environnement de ligne de commande Exchange Management Shell pour effectuer ces procédures.

  - Avant de pouvoir supprimer un rôle de gestion, vous devez supprimer toutes ses attributions de rôle de gestion. Pour plus d’informations sur la suppression d’une attribution de rôle, voir [Supprimer un rôle d’un utilisateur ou un groupe universel de sécurité](remove-a-role-from-a-user-or-usg-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.


## Que souhaitez-vous faire ?

## Supprimer un rôle de gestion sans rôle enfant

Pour supprimer un rôle sans rôle enfant, utilisez la syntaxe suivante.

    Remove-ManagementRole <role name>

Cet exemple montre comment supprimer le rôle Administrateurs de serveur de Seattle.

    Remove-ManagementRole "Seattle Server Administrators"

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Remove-ManagementRole](https://technet.microsoft.com/fr-fr/library/dd351170\(v=exchg.150\)).

## Supprimer un rôle de gestion avec des rôles enfants

Si un rôle que vous désirez supprimer a des rôles enfants, vous devez également supprimer tous les rôles enfants. Vous recevez un message d’erreur si vous essayez de supprimer un rôle qui a des rôles enfants à moins que vous n’utilisiez le commutateur *Recurse*. Si vous utilisez le commutateur *Recurse* lorsque vous supprimez un rôle, le rôle que vous spécifiez et tous ses rôles enfants sont supprimés.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ673034.Caution(EXCHG.150).gif" title="Attention" alt="Attention" />Attention :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Si vous utilisez le commutateur <em>Recurse</em>, tous les rôles enfants du rôle spécifié que vous désirez supprimer sont également supprimés. Assurez-vous de connaître les rôles qui seront supprimés avant d’exécuter cette commande.</td>
</tr>
</tbody>
</table>


Pour vous assurer que vous ne supprimez que les rôles que vous désirez supprimer, utilisez le commutateur *WhatIf* avec votre commande pour le vérifier. Utilisez la syntaxe suivante.

    Remove-ManagementRole <role name> -Recurse -WhatIf

Le commutateur *WhatIf* exécute la commande sans effectuer aucune modification et signale les rôles qu’il aurait supprimés. Pour plus d’informations sur le commutateur *WhatIf*, consultez la rubrique [Commutateurs WhatIf, Confirm et ValidateOnly](whatif-confirm-and-validateonly-switches-exchange-2013-help.md).

Après avoir confirmé que seuls les rôles que vous désirez supprimer seront supprimés, exécutez la même commande sans le commutateur *WhatIf*. Cet exemple montre comment supprimer le rôle d’administrateur de Londres et tous ses rôles enfants.

    Remove-ManagementRole "London Administrators" -Recurse

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Remove-ManagementRole](https://technet.microsoft.com/fr-fr/library/dd351170\(v=exchg.150\)).

## Supprimer un rôle de gestion non délimité

Pour supprimer un rôle non délimité, vous pouvez utiliser les mêmes procédures indiquées dans Supprimer un rôle de gestion sans rôle enfant et Supprimer un rôle de gestion avec des rôles enfants précédemment dans cette rubrique. La seule différence étant que lorsque vous supprimez un rôle non délimité, vous devez spécifier le commutateur *UnScopedTopLevel* lorsque vous exécutez la commande. Cet exemple montre comment supprimer un rôle non délimité et tous ses rôles enfants.

    Remove-ManagementRole "Custom IT Scripts" -Recurse -UnScopedTopLevel

Tout comme avec la suppression des autres rôles, vous devez utiliser le commutateur *WhatIf* pour vérifier que vous supprimez les bons rôles.

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Remove-ManagementRole](https://technet.microsoft.com/fr-fr/library/dd351170\(v=exchg.150\)).

