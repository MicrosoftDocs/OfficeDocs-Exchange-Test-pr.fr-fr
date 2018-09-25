---
title: 'Ajouter une entrée de rôle à un rôle: Exchange 2013 Help'
TOCTitle: Ajouter une entrée de rôle à un rôle
ms:assetid: 30cd37bc-b3e8-4f39-a8ba-a4c20b1b27b7
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dd335180(v=EXCHG.150)
ms:contentKeyID: 50477810
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Ajouter une entrée de rôle à un rôle

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2012-10-04_

Si vous souhaitez accorder l’accès à une cmdlet, vous devez ajouter l’entrée de rôle de gestion associée à un rôle de gestion. Une fois l’entrée ajoutée au rôle, les utilisateurs auxquels ce rôle est attribué pourront accéder à la cmdlet. Pour plus d’informations sur les entrées de rôles de gestion dans Microsoft Exchange Server 2013, voir [Présentation des rôles de gestion](understanding-management-roles-exchange-2013-help.md).

Vous ne pouvez pas ajouter des entrées de rôle à des rôles intégrés. Si vous souhaitez personnaliser des rôles, vous devez créer un nouveau rôle. Pour plus d’informations sur la création d’un nouveau rôle, consultez la rubrique [Créer un rôle](create-a-role-exchange-2013-help.md).

> [!NOTE]
> Cette rubrique ne décrit pas la façon d’ajouter des entrées de rôle de gestion non délimitées à un rôle de gestion non délimité. Pour plus d’informations sur la procédure d’ajout d’entrées de rôle non délimitées, consultez la rubrique <a href="add-a-role-entry-to-an-unscoped-top-level-role-exchange-2013-help.md">Ajouter une entrée de rôle à un rôle de niveau supérieur non délimité</a>.


Souhaitez-vous rechercher les autres tâches de gestion relatives aux rôles ? Consultez la rubrique [Autorisations avancées](advanced-permissions-exchange-2013-help.md).

## Ce qu’il faut savoir avant de commencer ?

  - Durée d’exécution estimée de chaque procédure : 5 minutes

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l’entrée « Rôles de gestion » dans la rubrique [Autorisations pour la gestion des rôles](role-management-permissions-exchange-2013-help.md).

  - Vous devez utiliser l’environnement de ligne de commande Exchange Management Shell pour effectuer ces procédures.

  - Une entrée de rôle que vous voulez ajouter à un rôle de gestion doit exister dans le rôle de gestion immédiatement parent de ce rôle.

  - Cette rubrique décrit le pipelining. Pour plus d’informations sur le pipelining, voir [Traitement en pipeline](https://technet.microsoft.com/fr-fr/library/aa998260\(v=exchg.150\)).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.


## Que souhaitez-vous faire ?

## Ajouter une seule entrée de rôle d’un rôle parent

Vous pouvez ajouter une entrée de rôle à un rôle exactement telle qu’elle apparaît sur le rôle parent à l’aide de la syntaxe suivante.

```powershell
Add-ManagementRoleEntry <child role name>\<cmdlet>
```

Cet exemple montre comment ajouter la cmdlet **Set-Mailbox** au rôle Administrateurs des destinataires.

```powershell
Add-ManagementRoleEntry "Recipient Administrators\Set-Mailbox"
```

Cette commande vérifie le rôle parent et si l’entrée de rôle existe, elle l’ajoute au rôle enfant. Si l’entrée de rôle existe sur le rôle enfant, vous pouvez inclure le paramètre *Overwrite* pour écraser l’entrée de rôle existante.

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Add-ManagementRoleEntry](https://technet.microsoft.com/fr-fr/library/dd351236\(v=exchg.150\)).

## Ajouter une seule entrée de rôle d’un rôle parent et inclure uniquement des paramètres spécifiques

Si vous souhaitez ajouter une entrée d’un rôle parent, mais souhaitez inclure uniquement des paramètres spécifiques dans l’entrée sur le rôle enfant, utilisez la syntaxe suivante.

```powershell
Add-ManagementRoleEntry <child role name>\<cmdlet> -Parameters <parameter 1>, <parameter 2>, <parameter...>
```

Cet exemple ajoute la cmdlet **Set-Mailbox** au rôle Support technique, mais inclut uniquement les paramètres *DisplayName* et *EmailAddresses* dans l’entrée sur le rôle enfant.

```powershell
Add-ManagementRoleEntry "Help Desk\Set-Mailbox" -Parameters DisplayName, EmailAddresses
```

Cette commande vérifie le rôle parent et si l’entrée de rôle existe, elle l’ajoute au rôle enfant. Si l’entrée de rôle existe sur le rôle enfant, vous pouvez inclure le paramètre *Overwrite* pour écraser l’entrée de rôle existante.

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Add-ManagementRoleEntry](https://technet.microsoft.com/fr-fr/library/dd351236\(v=exchg.150\)).

## Ajouter plusieurs entrées de rôle d’un rôle parent

Si vous voulez ajouter plusieurs entrées de rôle à un rôle, vous devez récupérer une liste d’entrées de rôle qui existent sur le rôle parent à ajouter au rôle enfant, puis ajouter ces entrées au rôle enfant. Pour ce faire, vous pouvez récupérer la liste d’entrées de rôle sur un rôle parent à l’aide de la cmdlet **Get-ManagementRoleEntry**. Ensuite, canalisez la sortie de la cmdlet **Get-ManagementRoleEntry** vers la cmdlet **Add-ManagementRoleEntry**. Pour récupérer plusieurs entrées de rôle, vous devez utiliser le caractère générique (\*).

Pour ajouter plusieurs entrées d’un rôle parent à un rôle enfant, utilisez la syntaxe suivante.

```powershell
Get-ManagementRoleEntry <parent role name>\*<partial cmdlet name>* | Add-ManagementRoleEntry -Role <child role name>
```

Cet exemple montre comment ajouter toutes les entrées de rôle qui contiennent la chaîne `Mailbox` dans le nom de la cmdlet sur le rôle parent Destinataires de message au rôle enfant Destinataires de message de Seattle.

```powershell
Get-ManagementRoleEntry "Mail Recipients\*Mailbox*" | Add-ManagementRoleEntry -Role "Seattle Mail Recipients"
```

Si les entrées de rôle existent déjà sur le rôle enfant, vous pouvez inclure le paramètre *Overwrite* pour écraser les entrées de rôle existantes.

Pour plus d’informations sur la récupération d’une liste d’entrées de rôle de gestion, voir [Afficher les entrées de rôle](view-role-entries-exchange-2013-help.md).

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, consultez les rubriques [Get-ManagementRoleEntry](https://technet.microsoft.com/fr-fr/library/dd335210\(v=exchg.150\)) et [Add-ManagementRoleEntry](https://technet.microsoft.com/fr-fr/library/dd351236\(v=exchg.150\)).

