---
title: 'Configurer des substitutions de disponibilité gérée: Exchange 2013 Help'
TOCTitle: Configurer des substitutions de disponibilité gérée
ms:assetid: c8f315b3-1d5e-4ad9-8bea-9c3a4a13ebfc
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dn482055(v=EXCHG.150)
ms:contentKeyID: 59890420
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurer des substitutions de disponibilité gérée

 

_**Sapplique à :** Exchange Online, Exchange Server 2013 SP1_

_**Dernière rubrique modifiée :** 2015-11-30_

La disponibilité gérée effectue un sondage continu pour détecter d’éventuels problèmes avec les composants Exchange ou leurs dépendances. Cette fonctionnalité effectue également des actions de récupération pour s'assurer que l’utilisateur final ne rencontre aucun problème avec l’un de ces composants. Toutefois, il peut arriver que les paramètres prédéfinis ne conviennent pas à votre environnement. Les sondes, les moniteurs et les répondeurs de disponibilité gérée peuvent être personnalisés en créant une substitution.

Les deux types de substitutions sont les suivants : local et global. Comme son nom l’indique, une substitution locale est disponible uniquement sur le serveur sur lequel elle est créée, et une substitution globale est utilisée pour appliquer une substitution à plusieurs serveurs. Chaque type de substitution peut être créé pour une durée déterminée ou pour une version spécifique d’Exchange, mais pas en même temps.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Lorsque vous créez une substitution, elle ne prend pas effet immédiatement. Le service de gestion de l’intégrité de Microsoft Microsoft Exchange vérifie que la configuration est modifiée toutes les 10 minutes et charge les modifications de configuration détectées. Si vous ne voulez pas attendre, vous pouvez redémarrer le service.</td>
</tr>
</tbody>
</table>


Pour d’autres tâches de gestion relatives à la disponibilité gérée, consultez la rubrique [Gérer les indicateurs d'intégrité et l'intégrité du serveur](manage-health-sets-and-server-health-exchange-2013-help.md).

## Ce qu’il faut savoir avant de commencer

  - Durée d’exécution estimée de chaque procédure : 5 minutes

  - Vous pouvez uniquement utiliser l'environnement de ligne de commande Exchange Management Shell pour effectuer cette tâche. Pour apprendre à ouvrir l’environnement de ligne de commande Environnement de ligne de commande Exchange Management Shell dans votre organisation Exchange locale, reportez-vous à [Ouvrir le Shell](https://technet.microsoft.com/fr-fr/library/dd638134\(v=exchg.150\)).

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

## Utilisation de l’Environnement de ligne de commande Exchange Management Shell pour créer des substitutions locales

Pour créer une substitution locale pour une durée spécifique, utilisez la syntaxe suivante.

    Add-ServerMonitoringOverride -Server <ServerName> -Identity <HealthSetName>\<MonitoringItemName>[\<TargetResource>] -ItemType <Probe | Monitor | Responder | Maintenance> -PropertyName <PropertyName> -PropertyValue <Value> -Duration <dd.hh:mm:ss>

Pour créer une substitution locale pour une version spécifique d’Exchange, utilisez la syntaxe suivante.

    Add-ServerMonitoringOverride -Server <ServerName> -Identity <HealthSetName>\<MonitoringItemName>[\<TargetResource>] -ItemType <Probe | Monitor | Responder | Maintenance> -PropertyName <PropertyName> -PropertyValue <Value> -Version <15.01.xxxx.xxx>

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Lorsque vous créez la substitution, les valeurs utilisées dans la paramètre <em>Identity</em> respectent la casse.</td>
</tr>
</tbody>
</table>


Cet exemple ajoute une substitution locale qui désactive le répondeur `ActiveDirectoryConnectivityConfigDCServerReboot` sur le serveur nommé EXCH03 pendant 20 jours.

    Add-ServerMonitoringOverride -Server EXCH03 -Identity "AD\ActiveDirectoryConnectivityConfigDCServerReboot" -ItemType Responder -PropertyName Enabled -PropertyValue 0 -Duration 20.00:00:00

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez bien créé une substitution locale, utilisez la cmdlet **Get-ServerMonitoringOverride** pour afficher la liste des substitutions locales :

    Get-ServerMonitoringOverride  -Server <ServerIdentity> | Format-List

La substitution doit apparaître dans la liste.

## Utilisation de l’Environnement de ligne de commande Exchange Management Shell pour supprimer des substitutions locales

Pour supprimer une substitution locale, utilisez la syntaxe suivante.

    Remove-ServerMonitoringOverride -Server <ServerName> -Identity <HealthSetName>\<MonitoringItemName>[\<TargetResource>] -ItemType <ExistingItemTypeValue> -PropertyName <PropertytoRemove>

Cet exemple supprime la substitution locale existante du répondeur `ActiveDirectoryConnectivityConfigDCServerReboot` dans le groupe d’intégrité Exchange du serveur EXCH01.

    Remove-ServerMonitoringOverride -Server EXCH01 -Identity Exchange\ActiveDirectoryConnectivityConfigDCServerReboot -ItemType Responder -PropertyName Enabled

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez bien supprimé une substitution locale, utilisez la cmdlet **Get-ServerMonitoringOverride** pour afficher la liste des substitutions locales :

    Get-ServerMonitoringOverride  -Server <ServerIdentity> | Format-List

La substitution supprimée ne doit pas apparaître dans la liste.

## Utilisation de l’Environnement de ligne de commande Exchange Management Shell pour créer des substitutions globales

Pour créer une substitution globale pour une durée spécifique, utilisez la syntaxe suivante.

    Add-GlobalMonitoringOverride -Identity <HealthSetName>\<MonitoringItemName>[\<TargetResource>] -ItemType <Probe | Monitor | Responder | Maintenance> -PropertyName <PropertytoOverride> -PropertyValue <NewPropertyValue> -Duration <dd.hh:mm:ss>

Pour créer une substitution globale pour une version spécifique d’Exchange, utilisez la syntaxe suivante.

    Add-GlobalMonitoringOverride -Identity <HealthSetName>\<MonitoringItemName>[\<TargetResource>] -ItemType <Probe | Monitor | Responder | Maintenance> -PropertyName <PropertytoOverride> -PropertyValue <NewPropertyValue> -ApplyVersion <15.01.xxxx.xxx>

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Lorsque vous créez la substitution, les valeurs utilisées dans la paramètre <em>Identity</em> respectent la casse.</td>
</tr>
</tbody>
</table>


Cet exemple ajoute une substitution globale qui désactive la sonde `OnPremisesInboundProxy` pendant 30 jours.

    Add-GlobalMonitoringOverride -Identity "FrontendTransport\OnPremisesInboundProxy" -ItemType Probe -PropertyName Enabled -PropertyValue 0 -Duration 30.00:00:00

Cet exemple ajoute une substitution globale qui désactive le répondeur `StorageLogicalDriveSpaceEscalate` pour tous les serveurs exécutant la version d’Exchange 15.01.0225.042.

    Add-GlobalMonitoringOverride -Identity "MailboxSpace\StorageLogicalDriveSpaceEscalate" -PropertyName Enabled -PropertyValue 0 -ItemType Responder -ApplyVersion "15.01.0225.042"

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez bien créé une substitution globale, utilisez la cmdlet **Get-GlobalMonitoringOverride** pour afficher la liste des substitutions globales :

    Get-GlobalMonitoringOverride

La substitution doit apparaître dans la liste.

## Utilisation de l’Environnement de ligne de commande Exchange Management Shell pour supprimer des substitutions globales

Pour supprimer une substitution globale, utilisez la syntaxe suivante.

    Remove-GlobalMonitoringOverride -Identity <HealthSetName>\<MonitoringItemName>[\<TargetResource>] -ItemType <ExistingItemTypeValue> -PropertyName <OverriddenProperty>

Cet exemple supprime la substitution globale existante de la propriété `ExtensionAttributes` de la sonde `OnPremisesInboundProxy` dans le groupe d’intégrité `FrontEndTransport`.

    Remove-GlobalMonitoringOverride -Identity FrontEndTransport\OnPremisesInboundProxy -ItemType Probe -PropertyName ExtensionAttributes

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez bien supprimé une substitution globale, utilisez la cmdlet **Get-GlobalMonitoringOverride** pour afficher la liste des substitutions globales :

    Get-GlobalMonitoringOverride

La substitution supprimée ne doit pas apparaître dans la liste.

