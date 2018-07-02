---
title: 'Cmdlets: Exchange 2013 Help'
TOCTitle: Cmdlets
ms:assetid: 1d741dea-1eb8-4909-850f-63d4efaa1a32
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Aa996589(v=EXCHG.150)
ms:contentKeyID: 50477731
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Cmdlets

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2015-03-09_

Une *cmdlet* (prononcez « command-let ») est la plus petite unité de fonctionnalité dans Exchange Management Shell. Les cmdlets ressemblent à des commandes intégrées dans d’autres interfaces de commande interactive, par exemple, la commande `dir` trouvée dans `cmd.exe`. Comme ces commandes familières, les cmdlets peuvent être appelées directement depuis la ligne de commande dans Exchange Management Shell et exécutées dans le contexte de l’interface de commande active, pas comme processus à part.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Depuis Microsoft Exchange Server 2007, des modifications ont été réalisées sur l’utilisation des cmdlets en interne par Exchange 2013 en raison de l’utilisation de la fonctionnalité à distance de Windows PowerShell. Ces modifications ont eu peu ou aucun impact sur la façon dont vous devez utiliser les cmdlets, mais elles peuvent offrir une flexibilité supplémentaire sur votre gestion des serveurs Exchange.</td>
</tr>
</tbody>
</table>


Les cmdlets sont généralement conçues autour de tâches d’administration récurrentes et Exchange Management Shell fournit plusieurs centaines de cmdlets pour l’exécution de tâches de gestion spécifiques à Exchange. Celles-ci sont disponibles en plus des cmdlets système non-Exchange incluses dans la conception de l’interface de commande interactive Windows PowerShell. Pour plus d’informations sur l’ouverture de l’environnement de ligne de commande Exchange Management Shell, consultez la rubrique [Ouvrir le Shell](https://technet.microsoft.com/fr-fr/library/dd638134\(v=exchg.150\)).

Toutes les cmdlets d’Exchange Management Shell sont présentées sous la forme de paires verbe-nom . Le verbe et le nom sont toujours séparés par un tiret (-), sans espace, et les noms de cmdlet sont toujours au singulier. Le verbe fait référence à l’action exécutée par la cmdlet. Le nom fait référence à l’objet auquel la cmdlet est appliquée. Par exemple, dans la cmdlet **Get-SystemMessage**, le verbe est **Get** (obtenir) et le nom **SystemMessage** (message système). Toutes les cmdlets d’Exchange Management Shell qui gèrent une fonctionnalité spécifique partagent le même nom. Le tableau suivant fournit des exemples de certains verbes disponibles dans Exchange Management Shell.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Par défaut, en cas d’omission du verbe, Exchange Management Shell considère qu’il s’agit du verbe <strong>Get</strong>. Par exemple, lorsque vous appelez <strong>Mailbox</strong>, vous obtenez le même résultat que si vous appeliez la cmdlet <strong>Get-Mailbox</strong>.</td>
</tr>
</tbody>
</table>


### Exemples de verbes dans Exchange Management Shell

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Verbe</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Disable</strong></p></td>
<td><p>Les cmdlets <strong>Disable</strong> définissent l’état <code>Enabled</code> de l’objet Exchange spécifié sur <code>$False</code>. Cela empêche l’objet de traiter des données même s’il existe.</p></td>
</tr>
<tr class="even">
<td><p><strong>Enable</strong></p></td>
<td><p>Les cmdlets <strong>Enable</strong> définissent l’état Activé de l’objet Exchange spécifié sur <code>$True</code>. Cela permet à l’objet de traiter des données.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Get</strong></p></td>
<td><p>Les cmdlets <strong>Get</strong> extraient des informations sur un objet Exchange spécifique.</p>
<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>La plupart des cmdlets <strong>Get</strong> ne renvoient que des informations récapitulatives lorsque vous les exécutez. Pour que la cmdlet <strong>Get</strong> renvoie des informations détaillées lorsque vous exécutez une commande, canalisez la commande vers la cmdlet <strong>Format-List</strong>. Pour plus d’informations sur la commande <strong>Format-List</strong>, consultez la rubrique <a href="working-with-command-output-exchange-2013-help.md">Utilisation de la sortie de la commande</a>. Pour plus d’informations sur le pipelining, voir <a href="https://technet.microsoft.com/fr-fr/library/aa998260(v=exchg.150)">Traitement en pipeline</a>.</td>
</tr>
</tbody>
</table>

</td>
</tr>
<tr class="even">
<td><p><strong>Install</strong></p></td>
<td><p>Les cmdlets <strong>Install</strong> installent un nouvel objet ou une nouvelle fonctionnalité sur un serveur Exchange.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Move</strong></p></td>
<td><p>Les cmdlets <strong>Move</strong> déplacent l’objet Exchange spécifié d’un conteneur ou d’un serveur vers un autre.</p></td>
</tr>
<tr class="even">
<td><p><strong>New</strong></p></td>
<td><p>Les cmdlets <strong>New</strong> créent un objet Exchange.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Remove</strong></p></td>
<td><p>Les cmdlets <strong>Remove</strong> suppriment l’objet Exchange spécifié.</p></td>
</tr>
<tr class="even">
<td><p><strong>Set</strong></p></td>
<td><p>Les cmdlets <strong>Set</strong> modifient les propriétés d’un objet Exchange existant.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Test</strong></p></td>
<td><p>Les cmdlets <strong>Test</strong> testent des composants Exchange spécifiques et fournissent des fichiers journaux que vous pouvez examiner.</p></td>
</tr>
<tr class="even">
<td><p><strong>Uninstall</strong></p></td>
<td><p>Les cmdlets <strong>Uninstall</strong> suppriment un objet ou une fonctionnalité d’un serveur Exchange.</p></td>
</tr>
</tbody>
</table>


La liste de cmdlets suivante fournit un exemple d’ensemble de cmdlets complet. Cet ensemble de cmdlets permet de gérer les fonctionnalités de message de notification d’état de remise (DSN) et de message de quota de boîte aux lettres d’Exchange 2013 :

  - **Get-SystemMessage**

  - **New-SystemMessage**

  - **Remove-SystemMessage**

  - **Set-SystemMessage**

