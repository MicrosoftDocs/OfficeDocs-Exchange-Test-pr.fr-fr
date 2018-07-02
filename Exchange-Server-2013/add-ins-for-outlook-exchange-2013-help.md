---
title: 'Applications pour Outlook: Exchange 2013 Help'
TOCTitle: Applications pour Outlook
ms:assetid: 28b6f2a1-a235-4023-b561-6fd304962775
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ943753(v=EXCHG.150)
ms:contentKeyID: 52062946
ms.date: 04/27/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Applications pour Outlook

 

_**Sapplique à :**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :**2017-03-13_

**Résumé** : Vue d’ensemble des compléments pour Outlook, qui fonctionnent avec Outlook sur les ordinateurs Windows et MacIntosh, sur les appareils mobiles et dans Outlook Web App et Outlook sur le web.

Les compléments pour Outlook sont des applications qui étendent l’utilité des clients Outlook en ajoutant des informations ou des outils auxquels les utilisateurs peuvent recourir sans avoir à quitter Outlook. Les compléments sont créés par des développeurs tiers et peuvent être installés à partir d’un fichier, d’une URL ou d’Office Store. Par défaut, tous les utilisateurs peuvent installer des compléments. Les administrateurs Exchange peuvent utiliser les rôles pour contrôler les droits des utilisateurs en matière d’installation de compléments.

<table>
<thead>
<tr class="header">
<th><img src="images/Bb125224.tip(EXCHG.150).gif" title="Conseil" alt="Conseil" />Conseil :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Pour plus d’informations sur les compléments pour Outlook du point de vue de l’utilisateur final, consultez la rubrique d’aide <a href="https://go.microsoft.com/fwlink/p/?linkid=2823">Compléments installés</a> sur Office.com. Cette rubrique offre une vue d’ensemble des compléments et présente également certains des compléments pour Outlook susceptibles d’être installés par défaut.</td>
</tr>
</tbody>
</table>


## Compléments Office Store et compléments personnalisés

Les clients Outlook prennent en charge un vaste éventail de compléments disponibles via l’Office Store. Outlook prend également en charge les compléments personnalisés que vous pouvez créer et distribuer à des utilisateurs au sein de votre organisation.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>L’accès à Office Store n’est pas pris en charge pour les boîtes aux lettres ou les organisations de certains pays. Si l’option <strong>Ajouter à partir d’Office Store</strong> n’apparaît pas dans le <strong>Centre d’administration Exchange</strong> sous <strong>Organisation</strong> &gt; <strong>Compléments</strong> &gt; <img src="images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif" title="Icône Ajouter" alt="Icône Ajouter" />, vous pourrez peut-être installer un complément pour Outlook depuis un emplacement de fichier ou une URL. Pour plus d’informations, contactez votre fournisseur de services.</td>
</tr>
</tbody>
</table>


<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Certains compléments pour Outlook sont installés par défaut. Les compléments par défaut pour Outlook s’activent uniquement sur du texte en anglais. Par exemple, les adresses postales allemandes situées dans le corps d’un message n’activeront pas le complément Bing Cartes.</td>
</tr>
</tbody>
</table>


## Accès aux compléments et installation

Par défaut, tous les utilisateurs peuvent installer et supprimer des compléments. Les administrateurs Exchange disposent d’un certain nombre de commandes pour la gestion des compléments et l’accès des utilisateurs à ceux-ci. Les administrateurs peuvent empêcher les utilisateurs d’installer des compléments qui ne sont pas téléchargés à partir d’Office Store (ils sont « chargés de manière indépendante » à partir d’un fichier ou d’une URL). Les administrateurs peuvent également empêcher les utilisateurs d’installer des compléments Office Store, ainsi que des compléments pour le compte d’autres utilisateurs. Il est également possible d’assigner des utilisateurs à un rôle qui leur permet d’installer des compléments pour votre organisation ou pour un sous-ensemble d’utilisateurs dans votre organisation.

Pour empêcher les utilisateurs d’installer un complément qui n’est pas issu d’Office Store, supprimez-leur le rôle **My Custom Apps**. Pour empêcher les utilisateurs d’installer des compléments depuis Office Store, supprimez-leur le rôle **My Marketplace Apps**. Pour plus d’informations, consultez la rubrique [Désigner les administrateurs et utilisateurs qui peuvent installer et gérer des compléments pour Outlook](specify-the-administrators-and-users-who-can-install-and-manage-add-ins-for-outlook-exchange-2013-help.md).

Pour installer des compléments pour une partie ou l’ensemble des utilisateurs de votre organisation, consultez la rubrique [Installation ou suppression d’applications pour votre organisation](install-or-remove-add-ins-for-outlook-for-your-organization-exchange-2013-help.md).

Le cas échéant, vous pouvez restreindre la mise à disposition d’un complément à certains utilisateurs de votre organisation. Pour plus d’informations, consultez la rubrique [Gestion de l’accès des utilisateurs aux applications pour Outlook](manage-user-access-to-add-ins-for-outlook-exchange-online-help.md).

## Tâches administratives courantes avec les compléments pour Outlook

Il existe quelques scénarios courants que gèrent les administrateurs Exchange dans leur organisation.

**Si vous souhaitez empêcher les utilisateurs finals d’installer des compléments pour Outlook sur tous les clients Outlook, apportez les modifications suivantes aux rôles du centre d’administration Exchange** :

  - Pour empêcher les utilisateurs d’installer des compléments de l’Office Store, supprimez le rôle **My Marketplace** de ces derniers.

  - Pour empêcher les utilisateurs de charger des compléments à partir de sources autres qu’Office Store, supprimez le rôle **My Custom Apps** de ces derniers.

  - Pour empêcher les utilisateurs d’installer tous les compléments, supprimez les deux rôles ci-dessus de ces derniers.

Pour plus d’informations, voir la rubrique [Désigner les administrateurs et utilisateurs qui peuvent installer et gérer des compléments pour Outlook](specify-the-administrators-and-users-who-can-install-and-manage-add-ins-for-outlook-exchange-2013-help.md).

**Si vos utilisateurs finals sont actuellement capables d’accéder aux compléments et que vous voulez supprimer cet accès, utilisez la cmdlet `Get-App` pour voir les compléments que chaque utilisateur a installés.**

Ensuite, utilisez la cmdlet `Remove-App` pour supprimer des compléments d’un ou de plusieurs utilisateurs. 

Pour plus d’informations, voir [Get-App](https://technet.microsoft.com/fr-fr/library/jj218673\(v=exchg.150\)) et [Remove-App](https://technet.microsoft.com/fr-fr/library/jj218709\(v=exchg.150\)) pour Exchange 2013. Pour Exchange Online ou Exchange 2016, cliquez [ici](https://go.microsoft.com/fwlink/p/?linkid=8447).

## Autoriser les administrateurs et les utilisateurs à installer des compléments

Vous pouvez spécifier les administrateurs de votre organisation qui disposent des autorisations pour installer et gérer les compléments pour Outlook. Vous pouvez également spécifier les utilisateurs au sein de votre organisation qui disposent des autorisations pour installer et gérer des compléments pour leur propre utilisation. Pour plus d’informations, consultez la rubrique [Désigner les administrateurs et utilisateurs qui peuvent installer et gérer des compléments pour Outlook](specify-the-administrators-and-users-who-can-install-and-manage-add-ins-for-outlook-exchange-2013-help.md).

