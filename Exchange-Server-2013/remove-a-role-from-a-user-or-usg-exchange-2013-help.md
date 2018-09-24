---
title: 'Supprimer un rôle d’un utlsr ou grp universel de sécurité: Exchange 2013 Help'
TOCTitle: Supprimer un rôle d’un utilisateur ou un groupe universel de sécurité
ms:assetid: df3510ef-e0c2-4d3c-81b0-7dc3e70c01a0
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dd351196(v=EXCHG.150)
ms:contentKeyID: 50479402
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Supprimer un rôle d’un utilisateur ou un groupe universel de sécurité

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2012-10-02_

Les rôles de gestion sont attribués à des utilisateurs ou à un groupe de sécurité universelle. Si vous supprimez l'attribution d'un rôle, les utilisateurs auxquels ce rôle est attribué n'auront plus accès aux cmdlets disponibles pour ce rôle. Pour plus d’informations sur les attributions de rôles de gestion dans Microsoft Exchange Server 2013, voir [Présentation des attributions de rôles de gestion](understanding-management-role-assignments-exchange-2013-help.md).

Souhaitez-vous rechercher les autres tâches de gestion relatives aux rôles ? Consultez la rubrique [Autorisations avancées](advanced-permissions-exchange-2013-help.md).

## Ce qu’il faut savoir avant de commencer ?

  - Durée estimée de la procédure : 5 minutes

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Attribution des rôles » dans la rubrique [Autorisations pour la gestion des rôles](role-management-permissions-exchange-2013-help.md).

  - Vous devez utiliser l’environnement de ligne de commande Exchange Management Shell pour effectuer ces procédures.

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.


## Supprimer une attribution de rôle de gestion

Si vous connaissez le nom de l’attribution de rôle à supprimer, utilisez la syntaxe suivante.

```powershell
Remove-ManagementRoleAssignment <assignment name>
```

Par exemple, pour supprimer l’attribution de rôle « Tier 2 Help Desk Assignment », utilisez la commande suivante.

```powershell
Remove-ManagementRoleAssignment "Tier 2 Help Desk Assignment"
```

Si vous ne connaissez pas le nom de l’attribution de rôle à supprimer, utilisez la syntaxe suivante.

```powershell
Get-ManagementRoleAssignment -RoleAssignee <user or USG> -Role <role name> -Delegating <$true | $false> | Remove-ManagementRoleAssignment 
```

Par exemple, si vous souhaitez supprimer l’attribution de rôle standard Destinataires de messagerie, utilisez la commande suivante.

```powershell
Get-ManagementRoleAssignment -RoleAssignee davids -Role "Mail Recipients" -Delegating $false | Remove-ManagementRoleAssignment
```

