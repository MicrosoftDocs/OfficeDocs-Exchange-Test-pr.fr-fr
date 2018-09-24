---
title: "Permet d'afficher un rôle: Exchange 2013 Help"
TOCTitle: Permet d'afficher un rôle
ms:assetid: 1875b15f-22db-4ede-b310-ea894d6211c8
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dd335117(v=EXCHG.150)
ms:contentKeyID: 50477584
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Permet d'afficher un rôle

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2012-10-03_

Les rôles de gestion peuvent être répertoriés de différentes façons en fonction des informations que vous souhaitez obtenir. Par exemple, vous pouvez choisir de renvoyer uniquement les rôles d’un type de rôle donné, les rôles qui contiennent uniquement des cmdlets et des paramètres spécifiques ou encore afficher les détails d’un rôle de gestion précis. Pour plus d’informations sur les rôles de gestion dans Microsoft Exchange Server 2013, voir [Présentation des rôles de gestion](understanding-management-roles-exchange-2013-help.md).

Pour afficher la liste de toutes les entrées de rôle de gestion d’un rôle, consultez [Afficher les entrées de rôle](view-role-entries-exchange-2013-help.md).

Souhaitez-vous rechercher les autres tâches de gestion relatives aux rôles ? Consultez la rubrique [Autorisations avancées](advanced-permissions-exchange-2013-help.md).

## Ce qu’il faut savoir avant de commencer ?

  - Durée d’exécution estimée de chaque procédure : 5 minutes

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l’entrée « Rôles de gestion » dans la rubrique [Autorisations pour la gestion des rôles](role-management-permissions-exchange-2013-help.md).

  - Vous devez utiliser l’environnement de ligne de commande Exchange Management Shell pour effectuer ces procédures.

  - Cette rubrique décrit l’utilisation du pipelining et des cmdlets **Format-List** et **Format-Table**. Pour plus d’informations sur ces concepts, consultez les rubriques suivantes :
    
      - [Traitement en pipeline](https://technet.microsoft.com/fr-fr/library/aa998260\(v=exchg.150\))
    
      - [Utilisation de la sortie de la commande](working-with-command-output-exchange-2013-help.md)

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.


## Que souhaitez-vous faire ?

## Afficher un rôle de gestion spécifique

Vous pouvez afficher les détails d’un rôle spécifique en récupérant un rôle spécifique à l’aide de la cmdlet **Get-ManagementRole** et en canalisant la sortie de la cmdlet **Format-List**.

Pour afficher les détails d’un rôle spécifique, utilisez la syntaxe suivante.

```powershell
Get-ManagementRole <role name> | Format-List
```

Cet exemple indique comment récupérer les détails du rôle de gestion Destinataires de messagerie.

```powershell
Get-ManagementRole "Mail Recipients" | Format-List
```

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Get-ManagementRole](https://technet.microsoft.com/fr-fr/library/dd351125\(v=exchg.150\)).

## Liste de tous les rôles de gestion

Vous pouvez afficher la liste de tous les rôles de gestion de votre organisation. Pour cela, ne spécifiez aucun rôle lorsque vous exécutez la commande **Get-ManagementRole**. Par défaut, le nom et le type de chaque rôle sont compris dans les résultats.

Cet exemple renvoie une liste de tous les rôles de votre organisation.

```powershell
Get-ManagementRole
```

Pour renvoyer une liste des propriétés spécifiques à tous les rôles de votre organisation, vous pouvez canaliser les résultats de la cmdlet **Format-Table** et spécifier les propriétés de votre choix dans la liste des résultats. Utilisez la syntaxe suivante.

```powershell
Get-ManagementRole | Format-Table <property 1>, <property 2...>
```

Cet exemple renvoie la liste de tous les rôles de votre organisation et comprend la propriété **Name** ainsi que toute propriété contenant le mot **Implicit** au début de son nom.

```powershell
Get-ManagementRole | Format-Table Name, Implicit*
```

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Get-ManagementRole](https://technet.microsoft.com/fr-fr/library/dd351125\(v=exchg.150\)).

## Liste des rôles de gestion contenant une cmdlet spécifique

Vous pouvez renvoyer la liste des rôles contenant un cmdlet que vous indiquez à l’aide du paramètre *Cmdlet* avec la cmdlet **Get-ManagementRole**.

Pour renvoyer la liste des rôles contenant la cmdlet que vous indiquez, utilisez la syntaxe suivante.

```powershell
Get-ManagementRole -Cmdlet <cmdlet>
```

Cet exemple indique comment renvoyer la liste de rôles contenant la cmdlet **New-Mailbox**.

```powershell
Get-ManagementRole -Cmdlet New-Mailbox
```

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Get-ManagementRole](https://technet.microsoft.com/fr-fr/library/dd351125\(v=exchg.150\)).

## Liste des rôles de gestion contenant un paramètre spécifique

Vous pouvez renvoyer la liste des rôles contenant un ou plusieurs paramètres que vous indiquez à l’aide du paramètre *CmdletParameters* avec la cmdlet **Get-ManagementRole**. Seuls les rôles qui contiennent tous les paramètres que vous spécifiez sont renvoyés.

Lorsque vous utilisez le paramètre *CmdletParameters*, vous pouvez choisir d’utiliser le paramètre *Cmdlet*. Si vous incluez le paramètre *Cmdlet*, seuls les rôles contenant les paramètres que vous spécifiez dans la cmdlet sont renvoyés. Si vous n’incluez pas le paramètre *Cmdlet*, les rôles contenant les paramètres que vous spécifiez, indépendamment de la cmldet à laquelle ils sont associés, sont renvoyés.

Pour renvoyer la liste des rôles contenant les paramètres que vous indiquez, utilisez la syntaxe suivante.

```powershell
Get-ManagementRole [-Cmdlet <cmdlet>] -CmdletParameters <parameter 1>, <parameter 2...>
```

Cet exemple renvoie la liste des rôles contenant les paramètres *Database* et *Server*, indépendamment de la cmdlet à laquelle ils sont associés.

```powershell
Get-ManagementRole -CmdletParameters Database, Server
```

Cet exemple renvoie la liste des rôles lorsque le paramètre *EmailAddresses* est uniquement spécifié dans la cmdlet **Set-Mailbox**.

```powershell
Get-ManagementRole -Cmdlet Set-Mailbox -CmdletParameters EmailAddresses
```

Vous pouvez également utiliser le caractère générique (\*) avec le paramètre *Cmdlet* ou *CmdletParameters* pour faire correspondre les noms partiels de cmdlet ou de paramètre.

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Get-ManagementRole](https://technet.microsoft.com/fr-fr/library/dd351125\(v=exchg.150\)).

## Liste des rôles de gestion d’un type de rôle spécifique

Vous pouvez renvoyer la liste des rôles en fonction d’un type de rôle donné à l’aide du paramètre *RoleType* avec la cmdlet **Get-ManagementRole**.

Pour renvoyer la liste des rôles correspondant au type de rôle que vous indiquez, utilisez la syntaxe suivante.

```powershell
Get-ManagementRole -RoleType <roletype>
```

Cet exemple indique comment renvoyer une liste de rôles en fonction du type de rôle `UmMailboxes`.

```powershell
Get-ManagementRole -RoleType UmMailboxes
```

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Get-ManagementRole](https://technet.microsoft.com/fr-fr/library/dd351125\(v=exchg.150\)).

## Liste des rôles enfants immédiats d’un rôle parent

Vous pouvez renvoyer la liste des rôles qui sont les enfants immédiats d’un rôle parent à l’aide du paramètre *GetChildren* avec la cmdlet **Get-ManagementRole**. Seuls les rôles qui contiennent le rôle que vous spécifiez comme rôle parent sont renvoyés.

Pour renvoyer la liste des rôles enfants immédiats d’un rôle parent, utilisez la syntaxe suivante.

```powershell
Get-ManagementRole <parent role name> -GetChildren
```

Cet exemple présente le renvoi d’une liste d’enfants immédiats du rôle Récupération après sinistre.

```powershell
Get-ManagementRole "Disaster Recovery" -GetChildren
```

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Get-ManagementRole](https://technet.microsoft.com/fr-fr/library/dd351125\(v=exchg.150\)).

## Liste de tous les rôles enfants sous un rôle parent

Vous pouvez renvoyer la liste de la chaîne complète de rôles, d’un rôle parent spécifié jusqu’au dernier rôle enfant, à l’aide du paramètre *Recurse* avec la cmdlet **Get-ManagementRole**. Le paramètre *Recurse* indique à la cmdlet **Get-ManagementRole** de parcourir vers le bas chaque relation parent et enfant détectée jusqu’à atteindre le dernier rôle enfant. Le rôle parent est inclus dans la liste renvoyée.

Dans cet exemple, la liste de tous les rôles enfants d’un rôle parent est renvoyée.

```powershell
Get-ManagementRole <parent role name> -Recurse
```

Cet exemple présente le renvoi de tous les rôles enfants du rôle Destinataires de messagerie.

```powershell
Get-ManagementRole "Mail Recipients" -Recurse
```

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Get-ManagementRole](https://technet.microsoft.com/fr-fr/library/dd351125\(v=exchg.150\)).

