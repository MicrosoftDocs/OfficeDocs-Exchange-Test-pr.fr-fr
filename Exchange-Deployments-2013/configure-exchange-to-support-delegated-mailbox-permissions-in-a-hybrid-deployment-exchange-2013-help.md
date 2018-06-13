---
title: 'Configurer Exchange pour prendre en charge des autorisations de boîtes aux lettres déléguées dans un déploiement hybride: Exchange 2013 Help'
TOCTitle: Configurer Exchange pour prendre en charge des autorisations de boîtes aux lettres déléguées dans un déploiement hybride
ms:assetid: a2a10cb3-4557-4ff5-8191-c653522f4512
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Mt784505(v=EXCHG.150)
ms:contentKeyID: 74447338
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurer Exchange pour prendre en charge des autorisations de boîtes aux lettres déléguées dans un déploiement hybride

 

_**Dernière rubrique modifiée :**2018-01-30_

Les autorisations de boîtes aux lettres déléguées permettent à un utilisateur de gérer une partie de la boîte aux lettres d’un autre utilisateur. L’exemple courant est celui d’un administrateur adjoint qui doit gérer la boîte aux lettres et le calendrier d’un cadre. Les déploiements hybrides entre une organisation Exchange locale et Office 365 prennent en charge les autorisations de boîtes aux lettres déléguées **Accès total** et **Envoyer de la part de**. Toutefois, selon la version d’Exchange que vous avez installée dans votre organisation locale, vous devrez peut-être effectuer une configuration supplémentaire pour utiliser des autorisations de boîtes aux lettres déléguées dans un déploiement hybride. Le tableau suivant indique quelles versions d’Exchange prennent en charge les autorisations de boîtes aux lettres déléguées dans un déploiement hybride et si une configuration supplémentaire est nécessaire pour cette version.

  - **Exchange 2016** Aucune configuration supplémentaire n’est nécessaire.

  - **Exchange 2013** Une mise à jour cumulative Exchange 2013 (CU) et une configuration supplémentaire prises en charge sont nécessaires.

  - **Exchange 2010** Un correctif cumulatif Exchange 2010 (RU) et une configuration supplémentaire prises en charge sont nécessaires.

Pour plus d’informations concernant les exigences spécifiques pour prendre en charge des autorisations de boîtes aux lettres déléguées dans un déploiement hybride, consultez [Autorisations dans les déploiements hybrides Exchange](permissions-in-exchange-hybrid-deployments-exchange-2013-help.md).

Les sections suivantes vous guident tout au long de la configuration des déploiements locaux d’Exchange 2013 et Exchange 2010 pour activer la prise en charge des autorisations de boîtes aux lettres déléguées. Avant de suivre ces étapes, vous devez vous assurer que vous avez installé les dernières versions CU Exchange 2013 ou RU Exchange SP3. Pour plus d’informations, voir [Configuration requise pour un déploiement hybride](hybrid-deployment-prerequisites-exchange-2013-help.md).

## Exchange 2013

Ce que vous devez faire pour activer la prise en charge des autorisations de boîtes aux lettres déléguées dépend de plusieurs facteurs. Si vous avez déplacé des boîtes aux lettres vers Office 365 et à ce moment-là :


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>L’élément suivant été installé...</th>
<th>Et la synchronisation d’objet des ACL de l’organisation a été...</th>
<th>Alors, vous devez...</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>CU9 Exchange 2013 ou une version antérieure</p></td>
<td><p>Cette fonctionnalité n’est pas disponible dans CU9 Exchange 2013 et version antérieure.</p></td>
<td><p>Configurer manuellement chaque boîte aux lettres pour prendre en charge les ACL</p></td>
</tr>
<tr class="even">
<td><p>CU10 Exchange 2013 ou version ultérieure</p></td>
<td><p>Désactivé</p></td>
<td><ol>
<li><p>Activer la synchronisation d’objet des ACL au niveau de l’organisation</p></li>
<li><p>Activez manuellement les ACL sur chaque boîte aux lettres déplacée vers Office 365 avant que la synchronisation d’objet des ACL ait été activée au niveau de l’organisation.</p></li>
</ol>
<p>Aucune configuration supplémentaire n’est nécessaire pour les boîtes aux lettres déplacées vers Office 365 une fois la synchronisation d’objet des ACL activée au niveau de l’organisation.</p></td>
</tr>
<tr class="odd">
<td><p>CU10 Exchange 2013 ou version ultérieure</p></td>
<td><p>Activé</p></td>
<td><p>Aucune configuration supplémentaire n’est nécessaire</p></td>
</tr>
</tbody>
</table>


## Activer la synchronisation d’objet des ACL

Pour activer la synchronisation d’objet des ACL au niveau de l’organisation, procédez comme suit.

1.  Installez la dernière version d’Azure Active Directory Connect (AAD Connect) sur l’ensemble de vos serveurs AAD Connect. Ceci est nécessaire pour autoriser AAD Connect à synchroniser les attributs nécessaires pour prendre en charge les autorisations hybrides. Vous pouvez télécharger AAD Connect sur [Microsoft Azure Active Directory Connect](http://go.microsoft.com/fwlink/p/?linkid=510956).

2.  Ouvrez l’environnement de ligne de commande Exchange Management Shell sur un serveur fonctionnant avec la dernière CU Exchange 2013 disponible ou immédiatement antérieure.

3.  Exécutez la commande suivante.
    
        Set-OrganizationConfig -ACLableSyncedObjectEnabled $True

Après cela, les boîtes aux lettres déplacées vers Office 365 seront correctement configurées pour prendre en charge les autorisations de boîtes aux lettres déléguées. Si les boîtes aux lettres ont été déplacées vers Office 365 avant d’accomplir ces étapes, vous devez activer manuellement les ACL sur ces boîtes aux lettres en suivant les étapes dans Activer les ACL sur des boîtes aux lettres à distance.

<table>
<thead>
<tr class="header">
<th><img src="images/Dn151301.important(EXCHG.150).gif" title="Important" alt="Important" />Important :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>ACL ne sont pas activées sur les boîtes aux lettres distants créés dans Office 365. Si vous créez une boîte aux lettres distant dans Office 365, vous devez suivre les instructions dans les ACL activer de section de boîtes aux lettres distants pour activer des ACL sur cette boîte aux lettres distant. Pour éviter cette étape supplémentaire, nous vous conseillons de créer la boîte aux lettres sur un serveur d’Exchange sur site et puis déplacez la boîte aux lettres vers Office 365.</td>
</tr>
</tbody>
</table>


## Activer les ACL sur des boîtes aux lettres à distance

Pour activer les ACL sur des boîtes aux lettres déplacées vers Office 365 avant que la synchronisation d’objet des ACL ait été activée au niveau de l’organisation, procédez comme suit.

1.  Ouvrez l’environnement de ligne de commande Exchange Management Shell sur un serveur fonctionnant avec la dernière CU Exchange 2013 disponible ou immédiatement antérieure.

2.  Pour activer les ACL sur une seule boîte aux lettres, exécutez la commande suivante.
    
        Get-AdUser <Identity> | Set-AdObject -Replace @{msExchRecipientDisplayType=-1073741818}

3.  Pour activer les ACL sur toutes les boîtes aux lettres déplacées vers Office 365, exécutez la commande suivante.
    
        Get-RemoteMailbox | ForEach { Get-AdUser -Identity $_.Guid | Set-ADObject -Replace @{msExchRecipientDisplayType=-1073741818}}

4.  Pour vérifier que les boîtes aux lettres ont été correctement mises à jour, exécutez la commande suivante.
    
        Get-RemoteMailbox | ForEach { Get-AdUser -Identity $_.Guid -Properties msExchRecipientDisplayType | Format-Table -AutoSize DistinguishedName, msExchRecipientDisplayType}

## Exchange 2010

Les serveurs Exchange 2010 SP3 prennent en charge la configuration des ACL sur les boîtes aux lettres à distance. Toutefois, cette configuration doit être définie manuellement sur chaque boîte aux lettres. Contrairement aux versions plus récentes d’Exchange, Exchange 2010 n’offre pas la possibilité de définir cette fonctionnalité au niveau de l’organisation. Vous devez suivre les étapes ci-dessous sur les boîtes aux lettres que vous avez précédemment déplacées vers Office 365 et sur les boîtes aux lettres qui seront déplacées d’un serveur Exchange 2010 SP3 vers Office 365 à l’avenir.

## Activer les ACL sur des boîtes aux lettres à distance

Pour activer les ACL sur les boîtes aux lettres déplacées vers Office 365, procédez comme suit.

1.  Ouvrez l’environnement de ligne de commande Exchange Management Shell sur un serveur fonctionnant avec la dernière version du RU Exchange 2010 SP3 ou immédiatement antérieure.

2.  Pour activer les ACL sur une seule boîte aux lettres, exécutez la commande suivante.
    
        Get-AdUser <Identity> | Set-AdObject -Replace @{msExchRecipientDisplayType=-1073741818}

3.  Pour activer les ACL sur toutes les boîtes aux lettres déplacées vers Office 365, exécutez la commande suivante.
    
        Get-RemoteMailbox | ForEach { Get-AdUser -Identity $_.Guid | Set-ADObject -Replace @{msExchRecipientDisplayType=-1073741818}}

4.  Pour vérifier que les boîtes aux lettres ont été correctement mises à jour, exécutez la commande suivante.
    
        Get-RemoteMailbox | ForEach { Get-AdUser -Identity $_.Guid -Properties msExchRecipientDisplayType | Format-Table -AutoSize DistinguishedName, msExchRecipientDisplayType}

