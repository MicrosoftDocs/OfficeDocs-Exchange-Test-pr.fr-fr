﻿---
title: 'Gestion du serveur: Exchange 2013 Help'
TOCTitle: Gestion du serveur
ms:assetid: 30cbc4de-adb3-42e8-922f-7661095bdb8c
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dd876866(v=EXCHG.150)
ms:contentKeyID: 50477809
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Gestion du serveur

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2015-03-09_

La gestion du serveur Le groupe de rôles de gestion est l’un des groupes de rôles intégrés qui créent un modèle d’autorisations de contrôle d’accès basé sur un rôle (RBAC) dans Microsoft Exchange Server 2013. Un ou plusieurs rôles de gestion sont affectés aux groupes de rôles qui contiennent les autorisations requises pour effectuer un ensemble de tâches données. Les membres d’un groupe de rôles sont autorisés à accéder aux rôles de gestion attribués au groupe de rôles. Pour plus d’informations sur les groupes de rôles, consultez la rubrique [Présentation des groupes de rôles de gestion](understanding-management-role-groups-exchange-2013-help.md).

Les administrateurs membres de ce groupe de rôles peuvent se charger de la configuration propre au serveur pour les fonctionnalités de transport, d’accès au client et de boîte aux lettres, telles que les copies de bases de données, les certificats, les files d’attente de transport, les connecteurs d’envoi, les répertoires virtuels et les protocoles d’accès au client.

Ce groupe de rôles est similaire au rôle d’administrateurs de serveur Exchange de Microsoft Exchange Server 2007. Il permet de gérer la configuration des serveurs physiques. Toutefois, à la différence du rôle d’administrateurs de serveur Exchange d’Exchange 2007, qui permettait d’accéder uniquement à un serveur local exécutant Exchange 2007, le groupe de rôles Gestion du serveur permet d’afficher et de configurer tous les serveurs Exchange Server 2010 de l’organisation.

Si vous souhaitez autoriser les administrateurs à gérer uniquement certains serveurs de votre organisation, vous pouvez changer les étendues de gestion appliquées à ce groupe de rôles. Vous pouvez aussi créer un groupe de rôles, basé sur le groupe de rôles Gestion du serveur, et personnaliser les étendues de gestion pour le nouveau groupe de rôles. Pour plus d’informations, consultez la section « Personnalisation d’un groupe de rôles » plus loin dans cette rubrique.

Pour plus d’informations sur le contrôle d’accès basé sur un rôle (RBAC), voir [Présentation du contrôle d'accès basé sur un rôle](understanding-role-based-access-control-exchange-2013-help.md).

## Appartenance au groupe de rôles

Si vous souhaitez ajouter ou supprimer des membres dans ce groupe de rôle, consultez la rubrique [Gérer les membres de groupes de rôles](manage-role-group-members-exchange-2013-help.md).

Par défaut, seuls les membres du groupe de rôles Gestion de l’organisation peuvent ajouter des membres de ce groupe de rôles ou en supprimer. Pour plus d’informations sur l’ajout de délégués de groupe de rôles supplémentaires, consultez la rubrique « Ajouter ou supprimer un délégué de groupe de rôles » dans [Gérer des groupes de rôles](manage-role-groups-exchange-2013-help.md).

Vous pouvez utiliser la commande suivante pour afficher une liste des utilisateurs ou des groupes de sécurité universelle qui sont membres de ce groupe de rôles.

```powershell
Get-RoleGroupMember "Server Management"
```

Pour plus d’informations sur les membres d’un groupe de rôles, voir [View the members of a role group](manage-role-group-members-exchange-2013-help.md) dans [Gérer les membres de groupes de rôles](manage-role-group-members-exchange-2013-help.md).

## Personnalisation d’un groupe de rôles

Ce groupe de rôles est attribué aux rôles de gestion par défaut. Les rôles inclus sont répertoriés dans la section « Rôles de gestion attribués à ce groupe de rôles ». Vous pouvez ajouter ou supprimer des attributions de rôles dans ce groupe de rôles pour qu’ils correspondent aux besoins de votre organisation.

Les groupes de rôles fournis avec Exchange 2013 sont conçus pour correspondre à des tâches plus précises. En attribuant des rôles à un groupe de rôles, vous permettez aux membres de ce groupe de rôles d’effectuer les tâches associées au rôle. Par exemple, le rôle de journalisation permet la gestion de l’agent de journalisation et des règles de journalisation. Pour plus d’informations sur la façon dont les rôles sont attribués aux groupes de rôles, voir [Présentation des attributions de rôles de gestion](understanding-management-role-assignments-exchange-2013-help.md).

Les rôles attribués à ce groupe de rôles bénéficient d’étendues de gestion par défaut. Les étendues de gestion déterminent les objets Exchange qui peuvent être visualisés ou modifiés par les membres d’un groupe de rôles. Vous pouvez modifier les étendues associées aux attributions entre les rôles et les groupes de rôles. Par exemple, vous souhaitez peut-être effectuer cette opération si vous voulez uniquement que les membres d’un groupe de rôles puissent modifier les destinataires qui se trouvent dans une unité d’organisation ou un emplacement spécifique. Pour plus d’informations sur les étendues de gestion, voir [Présentation des portées du rôle de gestion](understanding-management-role-scopes-exchange-2013-help.md).

Pour plus d’informations sur la manière de personnaliser ce groupe de rôles, consultez les rubriques suivantes :

  - [Gérer des groupes de rôles](manage-role-groups-exchange-2013-help.md)

  - [Gérer les membres de groupes de rôles](manage-role-group-members-exchange-2013-help.md)

Si vous souhaitez créer un groupe de rôles et attribuer certains des rôles affectés à ce groupe de rôles au nouveau groupe de rôles, consultez la section « Créer un groupe de rôles » dans la rubrique [Gérer des groupes de rôles](manage-role-groups-exchange-2013-help.md).

## Rôles de gestion attribués à ce groupe de rôles

Le tableau suivant répertorie tous les rôles de gestion qui sont attribués à ce groupe de rôles et les attributs suivants de chaque attribution de rôle :

  - **Attribution normale**   Permet aux membres du groupe de rôles d’accéder aux entrées de rôle de gestion rendues disponibles par le rôle de gestion associé.

  - **Attribution de délégation**   Permet aux membres du groupe de rôles d’affecter le rôle spécifié à d’autres groupes de rôles, des stratégies d’attribution de rôle, des utilisateurs ou des groupes de sécurité universels.

  - **Étendue de lecture du destinataire**   Détermine quels membres des objets du destinataire du groupe de rôles sont autorisés en lecture à partir de Active Directory.

  - **Étendue d’écriture du destinataire**   Détermine quels membres des objets du destinataire du groupe de rôles sont autorisés à effectuer des modifications dans Active Directory.

  - **Étendue de lecture de configuration**   Détermine quels membres des objets serveur et de configuration du groupe de rôles sont autorisés en lecture à partir de Active Directory.

  - **Étendue d’écriture du destinataire**   Détermine quels membres des objets du destinataire du groupe de rôles sont autorisés à effectuer des modifications dans Active Directory.

Pour plus d’informations sur les attributions de rôle et les étendues de gestion, consultez les rubriques suivantes :

  - [Présentation des attributions de rôles de gestion](understanding-management-role-assignments-exchange-2013-help.md)

  - [Présentation des portées du rôle de gestion](understanding-management-role-scopes-exchange-2013-help.md)

### Rôles de gestion attribués à ce groupe de rôles

<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>Rôle de gestion</th>
<th>Attribution normale</th>
<th>Attribution de délégation</th>
<th>Étendue de lecture du destinataire</th>
<th>Étendue d’écriture du destinataire</th>
<th>Étendue de lecture de configuration</th>
<th>Étendue d'écriture de configuration</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="database-copies-role-exchange-2013-help.md">Rôle des copies de base de données</a></p></td>
<td><p>X</p></td>
<td><p></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="databases-role-exchange-2013-help.md">Rôle des bases de données</a></p></td>
<td><p>X</p></td>
<td><p></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="exchange-connectors-role-exchange-2013-help.md">Rôle des connecteurs Exchange</a></p></td>
<td><p>X</p></td>
<td><p></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="exchange-server-certificates-role-exchange-2013-help.md">Rôle des certificats d’Exchange Server</a></p></td>
<td><p>X</p></td>
<td><p></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="exchange-servers-role-exchange-2013-help.md">Rôle des serveurs Exchange</a></p></td>
<td><p>X</p></td>
<td><p></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="exchange-virtual-directories-role-exchange-2013-help.md">Rôle des répertoires virtuels Exchange</a></p></td>
<td><p>X</p></td>
<td><p></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="monitoring-role-exchange-2013-help.md">Rôle d’analyse</a></p></td>
<td><p>X</p></td>
<td><p></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="pop3-and-imap4-protocols-role-exchange-2013-help.md">Rôle des protocoles POP3 et IMAP4</a></p></td>
<td><p>X</p></td>
<td><p></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="receive-connectors-role-exchange-2013-help.md">Rôle des connecteurs de réception</a></p></td>
<td><p>X</p></td>
<td><p></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="transport-queues-role-exchange-2013-help.md">Rôle des files d’attente de transport</a></p></td>
<td><p>X</p></td>
<td><p></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
</tbody>
</table>

