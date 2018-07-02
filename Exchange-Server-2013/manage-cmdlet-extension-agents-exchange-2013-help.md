---
title: 'Gérer des agents d’extension de cmdlet: Exchange 2013 Help'
TOCTitle: Gérer des agents d’extension de cmdlet
ms:assetid: 9141b3cb-ad13-4415-be2f-aa89f91445f5
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dd298143(v=EXCHG.150)
ms:contentKeyID: 50555446
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Gérer des agents d’extension de cmdlet

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2012-11-19_

Cette rubrique explique comment activer, désactiver, afficher et modifier la propriété des agents d’extension de cmdlet dans Microsoft Exchange Server 2013. Pour plus d’informations sur les agents d’extension de cmdlet dans Exchange 2013, voir [Agents d’extension des cmdlets](cmdlet-extension-agents-exchange-2013-help.md).

## Ce qu’il faut savoir avant de commencer ?

  - Durée d’exécution estimée de chaque procédure : moins de 5 minutes

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez entrée « agents d’extension de cmdlet » dans la rubrique [Autorisations d’infrastructure Exchange et Shell](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md).

  - Avant d’activer le `Scripting Agent`, vous devez vérifier qu’il est configuré correctement. Pour plus d’informations sur `Scripting Agent`, voir [Agents d’extension des cmdlets](cmdlet-extension-agents-exchange-2013-help.md).

  - Vous devez utiliser l’environnement de ligne de commande Exchange Management Shell pour effectuer ces procédures.

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

<table>
<thead>
<tr class="header">
<th><img src="images/Bb125224.tip(EXCHG.150).gif" title="Conseil" alt="Conseil" />Conseil :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.</td>
</tr>
</tbody>
</table>


## Que souhaitez-vous faire ?

## Activer un agent d’extension de cmdlet

Lorsque vous activez un agent d’extension de cmdlet dans Exchange 2013, l’agent est exécuté sur chaque serveur qui exécute Exchange 2013 dans l’organisation. Quand un agent est activé, il est mis à la disposition des cmdlets qui peuvent ensuite utiliser l’agent pour effectuer des opérations supplémentaires.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ673034.Caution(EXCHG.150).gif" title="Attention" alt="Attention" />Attention :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Avant d’activer un agent, assurez-vous que vous connaissez son fonctionnement et l’impact qu’il aura sur votre organisation.</td>
</tr>
</tbody>
</table>


Cet exemple montre comment activer un agent d’extension de cmdlet à l’aide de la cmdlet **Enable-CmdletExtensionAgent**. Vous devez indiquer le nom de l’agent à activer lorsque vous exécutez la cmdlet. Avant d’activer le `Scripting Agent`, assurez-vous d’avoir bien déployé le fichier de configuration `ScriptingAgentConfig.xml` sur tous les serveurs de votre organisation. Si vous ne commencez pas par déployer le fichier de configuration et que vous activez le `Scripting``Agent`, toutes les cmdlets non-**Get** échoueront lors de leur exécution. Cet exemple montre comment activer le `Scripting Agent`.

    Enable-CmdletExtensionAgent "Scripting Agent"

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Enable-CmdletExtensionAgent](https://technet.microsoft.com/fr-fr/library/dd335192\(v=exchg.150\)).

## Désactiver un agent d’extension de cmdlet

Lorsque vous désactivez un agent d’extension de cmdlet dans Exchange 2013, l’agent est désactivé sur tous les serveurs de l’organisation qui exécutent Exchange 2013. Lorsqu’un agent est désactivé, il n’est pas mis à la disposition des cmdlets. Les cmdlets ne peuvent plus utiliser l’agent pour effectuer d’autres opérations.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ673034.Caution(EXCHG.150).gif" title="Attention" alt="Attention" />Attention :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Avant de désactiver un agent, assurez-vous que vous connaissez le fonctionnement de l'agent, ainsi que les conséquences que la désactivation de l'agent entraînera dans l'organisation.</td>
</tr>
</tbody>
</table>


Pour désactiver un agent d'extension de cmdlet, utilisez la cmdlet **Disable-CmdletExtensionAgent**. Lorsque vous exécutez la cmdlet, indiquez le nom de l'agent que vous voulez désactiver. Cet exemple désactive l'agent `Scripting Agent`.

    Disable-CmdletExtensionAgent "Scripting Agent"

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Disable-CmdletExtensionAgent](https://technet.microsoft.com/fr-fr/library/dd298132\(v=exchg.150\)).

## Afficher les agents d’extension de cmdlet existants

L’affichage des agents d’extension de cmdlet vous permet de voir les agents qui sont exécutés en premier et ceux qui sont activés dans une organisation Exchange 2013. Pour plus d’informations sur le traitement en pipeline et la cmdlet **Format-Table**, consultez les rubriques suivantes :

  - [Traitement en pipeline](https://technet.microsoft.com/fr-fr/library/aa998260\(v=exchg.150\))

  - [Utilisation de la sortie de la commande](working-with-command-output-exchange-2013-help.md)

Cet exemple indique les détails d’un agent d’extension de cmdlet spécifique à l’aide de la cmdlet **Get-CmdletExtensionAgent**. Dans cet exemple, les détails de `Mailbox Permissions Agent` sont renvoyés.

    Get-CmdletExtensionAgent "Mailbox Permissions Agent"

Dans cet exemple, nous récupérons plusieurs agents d’extension de cmdlet à l’aide de la cmdlet **Get-CmdletExtensionAgent**, puis canalisons la sortie vers la cmdlet **Format-Table**. Cet exemple affiche une liste de tous les agents d’extension de cmdlet, et en utilisant la cmdlet **Format-Table**, les propriétés **Name**, **Enabled** et **Priority** de chaque agent sont affichées dans un tableau.

    Get-CmdletExtensionAgent | Format-Table Name, Enabled, Priority

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Get-CmdletExtensionAgent](https://technet.microsoft.com/fr-fr/library/dd297946\(v=exchg.150\)).

## Modifier la priorité d’un agent d’extension de cmdlet

La possibilité de modifier la priorité d’un agent d’extension de cmdlet dans Exchange 2013 est une option utile si vous souhaitez qu’un agent soit appelé par une cmdlet avant un autre agent. Ceci est particulièrement utile si vous créez un script personnalisé exécuté dans l’`Scripting Agent` et que vous souhaitez que ce script soit prioritaire sur un agent intégré. Pour plus d’informations sur `Scripting Agent`, voir [Agents d’extension des cmdlets](cmdlet-extension-agents-exchange-2013-help.md).

<table>
<thead>
<tr class="header">
<th><img src="images/JJ673034.Caution(EXCHG.150).gif" title="Attention" alt="Attention" />Attention :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>La modification de la priorité ou le remplacement de la fonctionnalité d’un agent intégré est une opération avancée. Assurez-vous que vous comprenez totalement les modifications que vous effectuez.</td>
</tr>
</tbody>
</table>


Le classement des agents va de zéro au nombre maximal d’agents. Plus l’agent est près de zéro, plus il est prioritaire. Les agents dont la priorité est élevée sont appelés en premier. Pour plus d’informations sur la priorité des agents, consultez la rubrique [Agents d’extension des cmdlets](cmdlet-extension-agents-exchange-2013-help.md).

Cet exemple montre comment modifier la priorité d’un agent d’extension de cmdlet à l’aide de la cmdlet **Set-CmdletExtensionAgent**. Dans cet exemple, la priorité de l’`Scripting Agent` est passée à 3.

    Set-CmdletExtensionAgent "Scripting Agent" -Priority 3

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Set-CmdletExtensionAgent](https://technet.microsoft.com/fr-fr/library/dd335175\(v=exchg.150\)).

