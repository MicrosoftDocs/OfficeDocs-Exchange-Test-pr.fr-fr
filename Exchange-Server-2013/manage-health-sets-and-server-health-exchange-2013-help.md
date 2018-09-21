---
title: 'Gérer les indic. d’intégrité et l’intégrité du serveur: Exchange 2013 Help'
TOCTitle: Gérer les indicateurs d'intégrité et l'intégrité du serveur
ms:assetid: a4f84312-6cfa-4f17-9707-676aadab1143
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dn482054(v=EXCHG.150)
ms:contentKeyID: 59890419
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Gérer les indicateurs d'intégrité et l'intégrité du serveur

 

_**Sapplique à :** Exchange Online, Exchange Server 2013 SP1_

_**Dernière rubrique modifiée :** 2013-12-02_

Vous pouvez utiliser les cmdlets de rapports d’intégrité intégrés pour effectuer diverses tâches liées à la disponibilité gérée, telles que :

  - Affichage de l’intégrité d’un serveur ou d’un groupe de serveurs

  - Affichage de la liste des indicateurs d’intégrité

  - Affichage de la liste des sondes, des moniteurs et des répondeurs associés à un indicateur d’intégrité particulier

  - Affichage de la liste des moniteurs et de leur intégrité actuelle

## Ce qu’il faut savoir avant de commencer

  - Durée d'exécution estimée de chaque procédure : 2 minutes

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]  
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.


## Que souhaitez-vous faire ?

## Afficher l’intégrité du serveur

Vous pouvez utiliser le Shell pour obtenir un résumé de l’intégrité d’un serveur exécutant Exchange 2013.

## Utiliser le Shell pour afficher l’intégrité du serveur

Exécutez l’une des commandes suivantes pour afficher les indicateurs d’intégrité et les informations d’intégrité sur un serveur exécutant Exchange 2013.
```
```powershell
Get-HealthReport -Identity <ServerName>
```
```
```
    Get-ServerHealth -Identity <ServerName> | Format-Table Server,CurrentHealthSetState,Name,HealthSetName,AlertValue,HealthGroupName -Auto
```

Exécutez l’une des commandes suivantes pour afficher les indicateurs d’intégrité sur un serveur ou un groupe de disponibilité de base de données exécutant Exchange 2013.
```
```powershell
Get-ExchangeServer | Get-HealthReport -RollupGroup
```
```
```
```powershell
Get-ExchangeServer | Get-HealthReport -RollupGroup -HealthSetName <HealthSet>
```
```
```
    (Get-DatabaseAvailabiltyGroup <DAGName>).Servers | Get-HealthReport -RollupGroup
```

## Afficher la liste des indicateurs d’intégrité

Un indicateur d’intégrité est un groupe de sondes, d’analyses et de répondeurs d’un composant qui déterminent si le composant est intègre ou non. Vous pouvez utiliser le Shell pour afficher la liste des indicateurs d’intégrité sur un serveur exécutant Exchange 2013.

## Utiliser le Shell pour afficher une liste d’indicateurs d’intégrité

Exécutez la commande suivante pour afficher les indicateurs d’intégrité sur un serveur exécutant Exchange 2013.

```powershell
Get-HealthReport -Server <ServerName>
```

## Afficher les sondes, les moniteurs et les répondeurs pour un indicateur d’intégrité

Un indicateur d’intégrité est un groupe de sondes, d’analyses et de répondeurs d’un composant qui déterminent si le composant est intègre ou non. Vous pouvez utiliser le Shell pour afficher la liste des sondes, des moniteurs et des répondeurs associés à un indicateur d’intégrité sur un serveur exécutant Exchange 2013.

## Utiliser le Shell pour afficher les sondes, les moniteurs et les répondeurs pour un indicateur d’intégrité

Exécutez la commande suivante pour afficher les sondes, les moniteurs et les répondeurs associés à un indicateur d’intégrité sur un serveur exécutant Exchange 2013.

    Get-MonitoringItemIdentity -Server <ServerName> -Identity <HealthSetName> | Format-Table Identity,ItemType,Name -Auto

## Afficher la liste des moniteurs et leur intégrité actuelle

L’intégrité d’un moniteur est signalée en utilisant le « pire » des moniteurs dans l’indicateur d’intégrité. Vous pouvez afficher les détails d’un indicateur d’intégrité pour savoir quels moniteurs sont intègres et ceux qui ne le sont pas.

## Utiliser le Shell pour afficher une liste de moniteurs et leur intégrité actuelle

Exécutez la commande suivante pour afficher la liste des moniteurs et leur intégrité actuelle sur un serveur exécutant Exchange 2013.

    Get-ServerHealth -HealthSet <HealthSetName> -Server <ServerName> | Format-Table Name, AlertValue -Auto

