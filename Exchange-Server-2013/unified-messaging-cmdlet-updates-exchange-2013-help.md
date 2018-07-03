---
title: 'Mises à jour des cmdlets de messagerie unifiée: Exchange 2013 Help'
TOCTitle: Mises à jour des cmdlets de messagerie unifiée
ms:assetid: a42c6643-67ed-4003-854a-ac1d66efb965
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ150557(v=EXCHG.150)
ms:contentKeyID: 50478825
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Mises à jour des cmdlets de messagerie unifiée

 

_**Sapplique à :** Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2015-03-09_

Beaucoup de cmdlets messagerie unifiée (MU) qui existaient dans Exchange Server 2010 ont été transféré pour Exchange Server 2013, mais il y a eu des changements à certains de ces cmdlets. En outre, les nouvelles cmdlets ont été ajoutées pour Exchange 2013.

## Paramètres mis à jour et nouvelles cmdlets de messagerie unifiée

Ce qui suit est une liste des paramètres mis à jour et nouvels cmdlets pour Exchange 2013.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Cmdlet</th>
<th>Paramètres</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>New-UMIPGateway</p></td>
<td><p><code>[-IPAddressFamily &lt;IPv4Only | IPv6Only | Any&gt;]</code></p></td>
</tr>
<tr class="even">
<td><p>Set-UMIPGateway</p></td>
<td><p><code>[-IPAddressFamily &lt;IPv4Only | IPv6Only | Any&gt;]</code></p></td>
</tr>
<tr class="odd">
<td><p>Get-UMMailbox</p></td>
<td><p><code>[-AccountPartition &lt;AccountPartitionIdParameter&gt;]</code></p></td>
</tr>
<tr class="even">
<td><p>Set-UMMailbox</p></td>
<td><p><code>[-ImListMigrationCompleted &lt;$true | $false&gt; -VoiceMailAnalysisEnabled &lt;$true | $false&gt;]</code></p></td>
</tr>
<tr class="odd">
<td><p>Test de connexion</p></td>
<td><p><code>[-CallRouter &lt;SwitchParameter&gt;]</code></p></td>
</tr>
<tr class="even">
<td><p>Nouveau-UMCallAnsweringRule</p></td>
<td><p><code>[-Name &lt;String&gt; [-CallerIds &lt;MultiValuedProperty&gt;] [-CallersCanInterruptGreeting &lt;$true | $false&gt;] [-CheckAutomaticReplies &lt;$true | $false&gt;] [-Confirm [&lt;SwitchParameter&gt;]] [-DomainController &lt;Fqdn&gt;] [-ExtensionsDialed &lt;MultiValuedProperty&gt;] [-KeyMappings &lt;MultiValuedProperty&gt;] [-Mailbox &lt;MailboxIdParameter&gt;] [-Organization &lt;OrganizationIdParameter&gt;] [-Priority &lt;Int32&gt;] [-ScheduleStatus &lt;Int32&gt;] [-TimeOfDay &lt;TimeOfDay&gt;] [-WhatIf [&lt;SwitchParameter&gt;]]</code></p></td>
</tr>
<tr class="odd">
<td><p>Supprimer-UMCallAnsweringRule</p></td>
<td><p><code>[-Identity &lt;UMCallAnsweringRuleIdParameter&gt; [-Confirm [&lt;SwitchParameter&gt;]] [-DomainController &lt;Fqdn&gt;] [-Mailbox &lt;MailboxIdParameter&gt;] [-WhatIf [&lt;SwitchParameter&gt;]]</code></p></td>
</tr>
<tr class="even">
<td><p>Obtenir-UMCallAnsweringRule</p></td>
<td><p><code>[-Identity &lt;UMCallAnsweringRuleIdParameter&gt;] [-DomainController &lt;Fqdn&gt;] [-Mailbox &lt;MailboxIdParameter&gt;]</code></p></td>
</tr>
<tr class="odd">
<td><p>Ajuster-UMCallAnsweringRule</p></td>
<td><p><code>[-Identity &lt;UMCallAnsweringRuleIdParameter&gt; [-CallerIds &lt;MultiValuedProperty&gt;] [-CallersCanInterruptGreeting &lt;$true | $false&gt;] [-CheckAutomaticReplies &lt;$true | $false&gt;] [-Confirm [&lt;SwitchParameter&gt;]] [-DomainController &lt;Fqdn&gt;] [-ExtensionsDialed &lt;MultiValuedProperty&gt;] [-KeyMappings &lt;MultiValuedProperty&gt;] [-Mailbox &lt;MailboxIdParameter&gt;] [-Name &lt;String&gt;] [-Priority &lt;Int32&gt;] [-ScheduleStatus &lt;Int32&gt;] [-TimeOfDay &lt;TimeOfDay&gt;] [-WhatIf [&lt;SwitchParameter&gt;]]</code></p></td>
</tr>
<tr class="even">
<td><p>Activer-UMCallAnsweringRule</p></td>
<td><p><code>[-Identity &lt;UMCallAnsweringRuleIdParameter&gt; [-Confirm [&lt;SwitchParameter&gt;]] [-DomainController &lt;Fqdn&gt;] [-Mailbox &lt;MailboxIdParameter&gt;] [-WhatIf [&lt;SwitchParameter&gt;]]</code></p></td>
</tr>
<tr class="odd">
<td><p>Désactiver-UMCallAnsweringRule</p></td>
<td><p><code>[-Identity &lt;UMCallAnsweringRuleIdParameter&gt; [-Confirm [&lt;SwitchParameter&gt;]] [-DomainController &lt;Fqdn&gt;] [-Mailbox &lt;MailboxIdParameter&gt;] [-WhatIf [&lt;SwitchParameter&gt;]]</code></p></td>
</tr>
<tr class="even">
<td><p>Obtenir-UMCallRouterSettings</p></td>
<td><p><code>[-DomainController &lt;Fqdn&gt;] [-Server &lt;ServerIdParameter&gt;]</code></p></td>
</tr>
<tr class="odd">
<td><p>Ajuster-UMCallRouterSettings</p></td>
<td><p><code>Set-UMCallRouterSettings [-Confirm [&lt;SwitchParameter&gt;]] [-DialPlans &lt;MultiValuedProperty&gt;] [-DomainController &lt;Fqdn&gt;] [-IPAddressFamily &lt;IPv4Only | IPv6Only | Any&gt;] [-IPAddressFamilyConfigurable &lt;$true | $false&gt;] [-Server &lt;ServerIdParameter&gt;] [-SipTcpListeningPort &lt;Int32&gt;] [-SipTlsListeningPort &lt;Int32&gt;] [-UMPodRedirectTemplate &lt;String&gt;] [-UMStartupMode &lt;TCP | TLS | Dual&gt;] [-WhatIf [&lt;SwitchParameter&gt;]]</code></p></td>
</tr>
<tr class="even">
<td><p>Désactivé-UMService</p></td>
<td><p><code>-Identity &lt;UMServerIdParameter&gt; [-Confirm [&lt;SwitchParameter&gt;]] [-DomainController &lt;Fqdn&gt;] [-Immediate &lt;$true | $false&gt;] [-WhatIf [&lt;SwitchParameter&gt;]]</code></p>
> [!NOTE]
> Cette cmdlet fonctionne avec des serveurs de messagerie unifiée Exchange 2007 et 2010 uniquement.

</td>
</tr>
<tr class="odd">
<td><p>Activé-UMService</p></td>
<td><p><code>-Identity &lt;UMServerIdParameter&gt; [-Confirm [&lt;SwitchParameter&gt;]] [-DomainController &lt;Fqdn&gt;] [-WhatIf [&lt;SwitchParameter&gt;]]</code></p>
> [!NOTE]
> Cette cmdlet fonctionne avec des serveurs de messagerie unifiée Exchange 2007 et 2010 uniquement.

</td>
</tr>
<tr class="even">
<td><p>Obtenir-UMService</p></td>
<td><p><code>[-Identity &lt;UMServerIdParameter&gt;] [-DomainController &lt;Fqdn&gt;]</code></p></td>
</tr>
<tr class="odd">
<td><p>Jeu-UMService</p></td>
<td><p><code>Set-UMService -Identity &lt;UMServerIdParameter&gt; [-Confirm [&lt;SwitchParameter&gt;]] [-DialPlans &lt;MultiValuedProperty&gt;] [-DomainController &lt;Fqdn&gt;] [-GrammarGenerationSchedule &lt;ScheduleInterval[]&gt;] [-IPAddressFamily &lt;IPv4Only | IPv6Only | Any&gt;] [-IPAddressFamilyConfigurable &lt;$true | $false&gt;] [-IrmLogEnabled &lt;$true | $false&gt;] [-IrmLogMaxAge &lt;EnhancedTimeSpan&gt;] [-IrmLogMaxDirectorySize &lt;Unlimited&gt;] [-IrmLogMaxFileSize &lt;ByteQuantifiedSize&gt;] [-IrmLogPath &lt;LocalLongFullPath&gt;] [-MaxCallsAllowed &lt;Int32&gt;] [-SIPAccessService &lt;ProtocolConnectionSettings&gt;] [-UMStartupMode &lt;TCP | TLS | Dual&gt;] [-WhatIf [&lt;SwitchParameter&gt;]]</code></p></td>
</tr>
</tbody>
</table>


Pour plus de détails au sujet de toutes les cmdlets de messagerie unifiée, voir [Cmdlets de messagerie unifiée](https://technet.microsoft.com/fr-fr/library/aa997665\(v=exchg.150\)).

