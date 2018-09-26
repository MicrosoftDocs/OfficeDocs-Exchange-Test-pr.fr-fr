---
title: 'Supprimer une étendue de rôle: Exchange 2013 Help'
TOCTitle: Supprimer une étendue de rôle
ms:assetid: ad17cba0-a8d3-4f40-b3c9-c37e6e5c3f36
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dd351051(v=EXCHG.150)
ms:contentKeyID: 50478986
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Supprimer une étendue de rôle

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2012-10-02_

Les étendues des rôles de gestion déterminent les objets à la disposition d'un utilisateur, lequel peut ensuite modifier ces objets à l'aide des cmdlets et des paramètres qui lui sont associés. Si vous n'utilisez plus une étendue, vous pouvez la supprimer. Pour plus d’informations sur les étendues de rôles de gestion dans Exchange Server 2013, voir [Présentation des portées du rôle de gestion](understanding-management-role-scopes-exchange-2013-help.md).

## Ce qu’il faut savoir avant de commencer ?

  - Durée d’exécution estimée de chaque procédure : 5 minutes

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Étendues de gestion » dans la rubrique [Autorisations pour la gestion des rôles](role-management-permissions-exchange-2013-help.md).

  - Vous devez utiliser l’environnement de ligne de commande Exchange Management Shell pour effectuer ces procédures.

  - Pour être en mesure de supprimer une étendue, vous devez tout d'abord la supprimer des attributions de rôle de gestion susceptibles de l'utiliser. Pour plus d'informations sur la suppression d'une étendue d'une attribution de rôle, voir [Modifier une attribution de rôle](change-a-role-assignment-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.


## Utiliser l'environnement de ligne de commande Exchange Management Shell pour supprimer une étendue

Pour supprimer une étendue, utilisez la syntaxe suivante.

```powershell
Remove-ManagementScope <scope name>
```

Par exemple, pour supprimer l'étendue « Dublin Servers », utilisez la commande suivante.

```powershell
Remove-ManagementScope "Dublin Servers"
```

