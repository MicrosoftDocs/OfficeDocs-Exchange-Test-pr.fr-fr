---
title: 'Afficher les entrées de rôle: Exchange 2013 Help'
TOCTitle: Afficher les entrées de rôle
ms:assetid: d9bb0d14-db59-456c-8f50-a8d7f7323df9
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dd351179(v=EXCHG.150)
ms:contentKeyID: 50479356
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Afficher les entrées de rôle

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2012-10-03_

Chaque entrée de rôle de gestion représente une cmdlet unique ou un script. Les paramètres inclus dans une entrée de rôle déterminent les paramètres sur la cmdlet ou le script auxquels un utilisateur peut accéder.

Les entrées d'identité de rôle sont constituées du nom du rôle de gestion auquel l'entrée de rôle est associée et de la cmdlet ou du script auquel l'entrée de rôle fait référence. Pour plus d'informations sur les entrées de rôle dans Microsoft Exchange Server 2013, voir [Présentation des rôles de gestion](understanding-management-roles-exchange-2013-help.md).

Souhaitez-vous rechercher les autres tâches de gestion associées aux entrées de rôle ? Consultez la rubrique [Autorisations avancées](advanced-permissions-exchange-2013-help.md).

## Ce qu’il faut savoir avant de commencer ?

  - Durée d’exécution estimée de chaque procédure : 5 minutes

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Rôles de gestion » dans la rubrique [Autorisations pour la gestion des rôles](role-management-permissions-exchange-2013-help.md).

  - Vous devez utiliser l’environnement de ligne de commande Exchange Management Shell pour effectuer ces procédures.

  - Cette rubrique utilise le traitement en pipeline, la cmdlet **Format-List** , des objets et des propriétés. Pour plus d’informations sur ces concepts, consultez les rubriques suivantes :
    
      - [Traitement en pipeline](https://technet.microsoft.com/fr-fr/library/aa998260\(v=exchg.150\))
    
      - [Utilisation de la sortie de la commande](working-with-command-output-exchange-2013-help.md)
    
      - [Données structurées](https://technet.microsoft.com/fr-fr/library/aa996386\(v=exchg.150\))

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.


## Que souhaitez-vous faire ?

## Afficher une liste d'entrées de rôle

La cmdlet **Get-ManagementRoleEntry** permet de produire une liste des entrées de rôle. Lorsque vous utilisez la cmdlet **Get-ManagementRoleEntry**, vous devez spécifier une valeur contenant le nom du rôle qui contient les entrées de rôle que vous souhaitez répertorier et le nom de la cmdlet permettant de les répertorier. En combinant le nom du rôle et le nom de la cmdlet avec le caractère générique (\*), vous pouvez obtenir des listes d'entrées de rôle spécifiques ou larges.

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Get-ManagementRoleEntry](https://technet.microsoft.com/fr-fr/library/dd335210\(v=exchg.150\)).

## Afficher une liste de toutes les entrées de rôle sur un rôle

Pour afficher une liste des entrées de rôle sur un rôle spécifique, utilisez la syntaxe suivante.

```powershell
Get-ManagementRoleEntry <role name>\*
```

Cet exemple extrait toutes les entrées de rôle sur le rôle `Recipient Administrators`.

```powershell
Get-ManagementRole "Recipient Administrators\*"
```

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Get-ManagementRoleEntry](https://technet.microsoft.com/fr-fr/library/dd335210\(v=exchg.150\)).

## Afficher une liste des rôles contenant une entrée de rôle spécifique

Pour afficher une liste de tous les rôles contenant une entrée de rôle spécifique, utilisez la syntaxe suivante.

```powershell
Get-ManagementRoleEntry *\<cmdlet name>
```

Cet exemple extrait tous les rôles contenant l'entrée de rôle **Set-Mailbox**.

```powershell
Get-ManagementRoleEntry *\Set-Mailbox
```

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Get-ManagementRoleEntry](https://technet.microsoft.com/fr-fr/library/dd335210\(v=exchg.150\)).

## Afficher une liste ciblée des rôles contenant des entrées de rôle similaires

Pour afficher une liste des rôles ciblés contenant des cmdlets avec des noms similaires, utilisez la syntaxe suivante.

```powershell
Get-ManagementRoleEntry *<partial role name>*\*<partial cmdlet name>*
```

Cet exemple produit une liste des entrées de rôle contenant la chaîne `Mailbox` et qui sont sur des rôles dont le nom comprend la chaîne `Tier 1`.

```powershell
Get-ManagementRoleEntry "*Tier 1*\*Mailbox*"
```

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Get-ManagementRoleEntry](https://technet.microsoft.com/fr-fr/library/dd335210\(v=exchg.150\)).

## Afficher une seule entrée de rôle

Pour afficher les détails d'une entrée de rôle, utilisez la syntaxe suivante.

```powershell
Get-ManagementRoleEntry <role name>\<cmdlet name> | Format-List
```

Cet exemple extrait les détails de l'entrée de rôle **Set-Mailbox** sur le rôle `Recipient Administrators`.

```powershell
Get-ManagementRoleEntry "Recipient Administrators\Set-Mailbox" | Format-List
```

S'il n'est pas possible d'afficher tous les paramètres d'une entrée de rôle à l'aide de la cmdlet **Format-List**, voir « Afficher les paramètres d'une entrée de rôle » plus bas dans cette rubrique.

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Get-ManagementRoleEntry](https://technet.microsoft.com/fr-fr/library/dd335210\(v=exchg.150\)).

## Afficher les paramètres d'une entrée de rôle

Certaines entrées de rôle contiennent plus de paramètres qu'il n'est possible d'afficher en canalisant les résultats de la cmdlet **Get-ManagementRoleEntry** vers la cmdlet **Format-List**. Si vous devez afficher tous les paramètres sur une entrée de rôle, accédez directement à la propriété **Parameters** de l'objet d'entrée de rôle.

Pour afficher les paramètres stockés dans la propriété **Parameters** d'un objet d'entrée de rôle, utilisez la syntaxe suivante.

```powershell
(Get-ManagementRoleEntry <role name>\<cmdlet name>).Parameters
```

Cet exemple extrait les paramètres sur l'entrée de rôle **Set-Mailbox** sur le rôle Mail Recipients.

```powershell
(Get-ManagementRoleEntry "Mail Recipients\Set-Mailbox").Parameters
```

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Get-ManagementRoleEntry](https://technet.microsoft.com/fr-fr/library/dd335210\(v=exchg.150\)).

