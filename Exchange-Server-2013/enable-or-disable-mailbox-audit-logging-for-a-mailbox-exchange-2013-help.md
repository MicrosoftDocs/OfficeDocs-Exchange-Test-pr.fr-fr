---
title: 'Activ. ou désactiv. l’enregistrement d’audit pour une BAL: Exchange 2013 Help'
TOCTitle: Activer ou désactiver l’enregistrement d’audit pour une boîte aux lettres
ms:assetid: c4bbfd52-6196-49c7-8c31-777fbbee11f2
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Ff461937(v=EXCHG.150)
ms:contentKeyID: 50479126
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Activer ou désactiver l’enregistrement d’audit pour une boîte aux lettres

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2015-09-30_

Grâce à la fonctionnalité d’enregistrement d’audit de boîte aux lettres, vous pouvez suivre les sessions ouvertes dans une boîte aux lettres, tout comme les actions entreprises tant que l’utilisateur est connecté. Lorsque vous activez l’enregistrement d’audit de boîte aux lettres, certaines actions réalisées par les administrateurs et les délégués sont enregistrées par défaut. Aucune des actions entreprises par le propriétaire de la boîte aux lettres ne sont enregistrées. Pour plus d’informations sur les enregistrements d’audit dans les boîtes aux lettres, voir [Enregistrement d’audit dans les boîtes aux lettres](mailbox-audit-logging-exchange-2013-help.md).

> [!CAUTION]
> Un audit des actions entreprises par un propriétaire de boîte aux lettres peut générer un grand nombre d’entrées dans le journal d’audit de boîte aux lettres. C’est pourquoi il est désactivé par défaut. Nous vous recommandons d’activer uniquement l’audit d’actions de propriétaire spécifiques si des besoins professionnels ou de sécurité l’exigent.


Pour les autres tâches relatives à l’enregistrement d’audit des boîtes aux lettres, voir [Procédures d'enregistrement d’audit des boîtes aux lettres](mailbox-audit-logging-procedures-exchange-2013-help.md).

## Ce qu’il faut savoir avant de commencer ?

  - Durée d’exécution estimée : 1 minute.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Journaux d’audit des boîtes aux lettres » dans la rubrique [Stratégie de messagerie et autorisations de conformité](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

  - Vous ne pouvez pas utiliser le Centre d’administration Exchange (CAE) pour activer ou désactiver l’enregistrement d’audit des boîtes aux lettres. Vous devez utiliser l’environnement de ligne de commande Exchange Management Shell.

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.


## Que souhaitez-vous faire ?

## Utiliser l’environnement de ligne de commande Exchange Management Shell pour activer ou désactiver l’enregistrement d’audit de boîte aux lettres

Vous pouvez utiliser l’environnement de ligne de commande Exchange Management Shell pour activer ou désactiver l’enregistrement d’audit des boîtes aux lettres. Cela active ou désactive l’enregistrement de toutes les opérations spécifiées pour l’administrateur, les délégués et le propriétaire de la boite aux lettres.

Cet exemple active l’enregistrement d’audit pour la boîte aux lettres de l’utilisateur Ben Smith.

```powershell
Set-Mailbox -Identity "Ben Smith" -AuditEnabled $true
```

Cet exemple désactive l’enregistrement d’audit pour la boîte aux lettres de l’utilisateur Ben Smith.

```powershell
Set-Mailbox -Identity "Ben Smith" -AuditEnabled $false
```

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, consultez la rubrique [Set-Mailbox](https://technet.microsoft.com/fr-fr/library/bb123981\(v=exchg.150\)).

## Utiliser l’environnement de ligne de commande Exchange Management Shell pour configurer les paramètres d’enregistrement d’audit des boîtes aux lettres pour l’accès des administrateurs, des délégués et des propriétaires

Si l’enregistrement d’audit de boîte aux lettres est activé pour une boîte aux lettres, seules les actions des administrateurs, des délégués et des propriétaires spécifiées dans la configuration de l’enregistrement d’audit pour la boîte aux lettres sont journalisées.

Cet exemple précise que les actions `SendAs` ou `SendOnBehalf` effectuées par des utilisateurs délégués seront enregistrées pour la boîte aux lettres de Ben Smith.

```powershell
Set-Mailbox -Identity "Ben Smith" -AuditDelegate SendAs,SendOnBehalf -AuditEnabled $true
```

Cet exemple précise que les actions `MessageBind` ou `FolderBind` effectuées par des administrateurs seront enregistrées pour la boîte aux lettres de Ben Smith.

```powershell
Set-Mailbox -Identity "Ben Smith" -AuditAdmin MessageBind,FolderBind -AuditEnabled $true
```

Cet exemple précise que l’action `HardDelete` effectuée par le propriétaire de la boîte aux lettres sera enregistrée pour la boîte aux lettres de Ben Smith.

```powershell
Set-Mailbox -Identity "Ben Smith" -AuditOwner HardDelete -AuditEnabled $true
```

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Set-Mailbox](https://technet.microsoft.com/fr-fr/library/bb123981\(v=exchg.150\)).

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez bien activé l’enregistrement d’audit des boîtes aux lettres et que vous avez spécifié les paramètres d’enregistrement qui conviennent pour l’accès des administrateurs, des délégués ou des propriétaires, utilisez la cmdlet [Get-Mailbox](https://technet.microsoft.com/fr-fr/library/bb123685\(v=exchg.150\)) pour récupérer les paramètres d’enregistrement d’audit de boîte aux lettres pour cette boîte aux lettres.

Cet exemple illustre la récupération des paramètres de la boîte aux lettres de Ben Smith et le transfert des paramètres d’audit spécifiés, y compris la limite d’âge du journal d’audit, vers la cmdlet **Format-List**.

```powershell
Get-Mailbox "Ben Smith" | Format-List *audit*
```

