---
title: 'Afficher les étendues des rôles: Exchange 2013 Help'
TOCTitle: Afficher les étendues des rôles
ms:assetid: 0bb3a434-6651-473a-94eb-4eb9a34e6f70
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dd335084(v=EXCHG.150)
ms:contentKeyID: 50477528
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Afficher les étendues des rôles

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2012-10-03_

Les étendues des rôles de gestion déterminent quels objets sont mis à la disposition de l’utilisateur pour que ceux-ci puissent être modifiés à l’aide des cmdlets et des paramètres qui lui sont attribués. Vous pouvez afficher les étendues pour déterminer celles qui ont été ajoutées à votre organisation, la configuration d’une étendue spécifique ou les étendues orphelines.

Pour plus d’informations sur les étendues de rôles de gestion dans Exchange Server 2013, voir [Présentation des portées du rôle de gestion](understanding-management-role-scopes-exchange-2013-help.md).

Souhaitez-vous rechercher les autres tâches de gestion relatives aux étendues des rôles ? Consultez la rubrique [Autorisations avancées](advanced-permissions-exchange-2013-help.md).

## Ce qu’il faut savoir avant de commencer ?

  - Durée d’exécution estimée de chaque procédure : 5 minutes

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Étendues de gestion » dans la rubrique [Autorisations pour la gestion des rôles](role-management-permissions-exchange-2013-help.md).

  - Vous devez utiliser l’environnement de ligne de commande Exchange Management Shell pour effectuer ces procédures.

  - Cette rubrique décrit l’utilisation du pipelining et de la cmdlet **Format-List**. Pour plus d’informations sur ces concepts, consultez les rubriques suivantes :
    
      - [Traitement en pipeline](https://technet.microsoft.com/fr-fr/library/aa998260\(v=exchg.150\))
    
      - [Utilisation de la sortie de la commande](working-with-command-output-exchange-2013-help.md)

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.


## Que souhaitez-vous faire ?

## Afficher une étendue spécifique

Vous pouvez afficher les détails d’une étendue en transférant la sortie de la cmdlet **Get-ManagementScope** vers la cmdlet **Format-List**.

Pour afficher les détails d’une étendue spécifique, utilisez la syntaxe suivante.

```powershell
Get-ManagementScope <scope name> | Format-List
```

Cet exemple montre comment récupérer les détails de l’étendue de serveurs de Seattle.

```powershell
Get-ManagementScope "Seattle Servers" | Format-List
```

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Get-ManagementScope](https://technet.microsoft.com/fr-fr/library/dd298180\(v=exchg.150\)).

## Liste de toutes les étendues

Cet exemple récupère une liste des étendues de votre organisation.

```powershell
Get-ManagementScope
```

Cette cmdlet récupère les étendues exclusives et normales. Si vous désirez uniquement renvoyer des étendues exclusives ou normales, consultez la section « Afficher l’ensemble des étendues exclusives ou normales uniquement » ultérieurement dans cette rubrique.

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Get-ManagementScope](https://technet.microsoft.com/fr-fr/library/dd298180\(v=exchg.150\)).

## Liste de toutes les étendues orphelines

*Étendues orphelines* sont les étendues qui n’ont pas été associées à des attributions de rôles de gestion.

Cet exemple récupère la liste des étendues orphelines.

```powershell
Get-ManagementScope -Orphan
```

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Get-ManagementScope](https://technet.microsoft.com/fr-fr/library/dd298180\(v=exchg.150\)).

## Liste de toutes les étendues exclusives ou normales uniquement

Par défaut, la cmdlet **Get-ManagementScope** renvoie la liste des étendues qui contiennent des étendues exclusives et normales à la fois. Si vous désirez uniquement renvoyer des étendues exclusives ou normales, utilisez la syntaxe suivante.

```powershell
Get-ManagementScope -Exclusive < $true | $false >
```

Cet exemple montre comment renvoyer uniquement des étendues exclusives.

```powershell
Get-ManagementScope -Exclusive $true
```

Cet exemple montre comment renvoyer uniquement une liste d’étendues normales.

```powershell
Get-ManagementScope -Exclusive $false
```

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Get-ManagementScope](https://technet.microsoft.com/fr-fr/library/dd298180\(v=exchg.150\)).

