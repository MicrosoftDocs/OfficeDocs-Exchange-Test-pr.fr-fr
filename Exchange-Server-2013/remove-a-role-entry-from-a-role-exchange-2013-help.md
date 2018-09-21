---
title: "Supprimer une entrée de rôle d'un rôle: Exchange 2013 Help"
TOCTitle: Supprimer une entrée de rôle d'un rôle
ms:assetid: 4736367a-750f-44d3-8a20-5149bd35e9ff
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dd297947(v=EXCHG.150)
ms:contentKeyID: 50478061
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Supprimer une entrée de rôle d'un rôle

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2012-10-03_

Les entrées de rôle d'un rôle de gestion déterminent les cmdlets et les paramètres qui sont disponibles pour un rôle de gestion. Si vous supprimez des entrées de rôles ou des paramètres d'une entrée de rôle, vous pouvez limiter les actions que les utilisateurs associés au rôle de gestion peuvent effectuer. Pour plus d’informations sur les entrées de rôles de gestion dans Microsoft Exchange Server 2013, voir [Présentation des rôles de gestion](understanding-management-roles-exchange-2013-help.md).

Souhaitez-vous rechercher les autres tâches de gestion relatives aux rôles ? Consultez la rubrique [Autorisations avancées](advanced-permissions-exchange-2013-help.md).

## Ce qu’il faut savoir avant de commencer ?

  - Durée d’exécution estimée de chaque procédure : 5 minutes

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l’entrée « Rôles de gestion » dans la rubrique [Autorisations pour la gestion des rôles](role-management-permissions-exchange-2013-help.md).

  - Vous devez utiliser l’environnement de ligne de commande Exchange Management Shell pour effectuer ces procédures.

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.


## Que souhaitez-vous faire ?

## Supprimer une entrée de rôle d'un rôle

Lorsque vous supprimez une entrée de rôle d'un rôle, les utilisateurs associés à ce rôle ne sont plus en mesure d'accéder à la cmdlet ou au script associé.

Utilisez la syntaxe suivante pour supprimer une entrée de rôle de gestion d'un rôle.

```powershell
Remove-ManagementRoleEntry <management role>\<management role entry>
```

Cet exemple supprime la cmdlet **Enable-MailUser** du rôle « Seattle Server Administrators ».

```powershell
Remove-ManagementRoleEntry "Seattle Server Administrators\Enable-MailUser"
```

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Remove-ManagementRoleEntry](https://technet.microsoft.com/fr-fr/library/dd351187\(v=exchg.150\)).

## Supprimer plusieurs entrées de rôle d'un rôle

Lorsque vous supprimez plusieurs entrées de rôle d'un rôle, les utilisateurs associés à ce rôle ne sont plus en mesure d'accéder aux cmdlets ou aux scripts associés.

Pour supprimer plusieurs entrées de rôle d'un rôle, vous devez récupérer la liste des entrées de rôle à supprimer à l'aide de la cmdlet **Get-ManagementRoleEntry**. Vous devez canaliser la sortie vers la cmdlet **Remove-ManagementRoleEntry**. Vous pouvez utiliser des caractères génériques avec la cmdlet **Get-ManagementRoleEntry** pour établir une correspondance entre plusieurs entrées de rôle. Il est judicieux d'utiliser le commutateur *WhatIf* pour vérifier que vous supprimez les entrées de rôle correctes. Utilisez la syntaxe suivante.

    Get-ManagementRoleEntry <management role>\<role entry with wildcard character> | Remove-ManagementRoleEntry -WhatIf

Cet exemple supprime toutes les entrées de rôle qui contiennent le mot « journal » du rôle « Seattle Server Administrators ».

    Get-ManagementRoleEntry "Seattle Server Administrators\*Journal*" | Remove-ManagementRoleEntry -WhatIf

Lorsque vous exécutez la commande avec le commutateur *WhatIf*, la cmdlet retourne la liste de toutes les entrées de rôle devant être supprimées. Si la liste semble correcte, exécutez à nouveau la commande sans le commutateur *WhatIf* pour supprimer les entrées de rôle.

    Get-ManagementRoleEntry "Seattle Server Administrators\*Journal*" | Remove-ManagementRoleEntry

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Get-ManagementRoleEntry](https://technet.microsoft.com/fr-fr/library/dd335210\(v=exchg.150\)) et [Remove-ManagementRoleEntry](https://technet.microsoft.com/fr-fr/library/dd351187\(v=exchg.150\)).

## Supprimer des paramètres d'une entrée de rôle d'un rôle

Lorsque vous supprimez des paramètres d'une entrée de rôle d'un rôle, les utilisateurs associés à ce rôle ne sont plus en mesure d'utiliser ces paramètres.

Utilisez la syntaxe suivante pour supprimer des paramètres d'une entrée de rôle.

    Set-ManagementRoleEntry <management role>\<role entry> -Parameters <parameter 1>,<parameter 2...> -RemoveParameter

Cet exemple supprime les paramètres *MaxSafeSenders*, *MaxSendSize*, *SecondaryAddress* et *UseDatabaseQuotaDefaults* de l'entrée de rôle **Set-Mailbox** sur le rôle « Seattle Server Administrators ».

    Set-ManagementRoleEntry "Seattle Server Administrators\Set-Mailbox" -Parameters MaxSafeSenders,MaxSendSize,SecondaryAddress,UseDatabaseQuotaDefaults -RemoveParameter

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Set-ManagementRoleEntry](https://technet.microsoft.com/fr-fr/library/dd351162\(v=exchg.150\)).

