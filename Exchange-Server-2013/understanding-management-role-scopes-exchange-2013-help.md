---
title: 'Présentation des portées du rôle de gestion: Exchange 2013 Help'
TOCTitle: Présentation des portées du rôle de gestion
ms:assetid: 24ed4a38-438a-4223-9f9c-5d4dea4b046b
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dd335146(v=EXCHG.150)
ms:contentKeyID: 50477772
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Présentation des portées du rôle de gestion

 

_**Sapplique à :** Exchange Online, Exchange Server 2013_

_**Dernière rubrique modifiée :** 2015-04-07_

Les *étendues des rôles de gestion* permettent de définir l’étendue spécifique de l’impact ou de l’influence d’un rôle de gestion lorsqu’une attribution de rôle de gestion est créée. Lorsque vous appliquez une étendue, la personne attribuée au rôle ne peut que modifier les objets contenus dans cette étendue. Une personne attribuée au rôle peut être un groupe de rôles de gestion, un rôle de gestion, une stratégie d’attribution de rôle de gestion, un utilisateur ou un groupe de sécurité universel. Pour plus d’informations sur les rôles de gestion, voir [Présentation du contrôle d'accès basé sur un rôle](understanding-role-based-access-control-exchange-2013-help.md).

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Cette rubrique traite de la fonctionnalité RBAC avancée. Si vous souhaitez gérer des autorisations Exchange 2013 de base, comme l’utilisation du centre d’administration Exchange pour ajouter et supprimer des membres dans les groupes de rôles, créer et modifier des groupes de rôles ou créer et modifier des stratégies d’attribution de rôles, consultez la rubrique <a href="permissions-exchange-2013-help.md">Autorisations</a>.</td>
</tr>
</tbody>
</table>


Chaque rôle de gestion, qu’il soit intégré ou personnalisé, a des étendues de gestion. Une étendue de gestion peut être :

  - **Normale**   Une *étendue normale* n’est pas exclusive. Elle détermine où, dans Active Directory, les objets peuvent être visibles ou modifiés par les utilisateurs auxquels le rôle de gestion est attribué. En général, un rôle de gestion indique ce qui peut être créé ou modifié et une étendue de rôle de gestion indique où la création ou la modification sont effectuées. Les étendues normales peuvent être implicites ou explicites. Toutes deux seront traitées plus loin dans cette rubrique.

  - **Exclusive**   Une *étendue exclusive* se comporte presque de la même façon qu’une étendue normale. La principale différence réside dans le fait qu’elle permet de refuser l’accès aux objets contenus dans l’étendue exclusive si les utilisateurs ne se voient pas attribuer un rôle associé à l’étendue exclusive. Toutes les étendues exclusives sont explicites, comme cela est décrit plus loin dans cette rubrique.
    
    Pour plus d’informations sur les étendues exclusives, voir [Présentation des étendues exclusives](understanding-exclusive-scopes-exchange-2013-help.md).

Les étendues peuvent être héritées du rôle de gestion, définies comme une étendue relative prédéfinie sur une attribution de rôle de gestion ou créées à l’aide de filtres personnalisés et ajoutées à une attribution de rôle de gestion. Les étendues héritées des rôles de gestion s’appellent *étendues implicites* et les étendues prédéfinies et personnalisées s’appellent *étendues explicites*. Les sections suivantes décrivent chaque type d’étendue :

  - Étendues implicites

  - Étendues explicites

  - Étendues relatives prédéfinies

  - Étendues personnalisées
    
      - Étendues filtrées de destinataire
    
      - Étendues de configuration

Chaque rôle peut posséder les types d’étendue suivants :

  - **Étendue de lecture du destinataire**   L’étendue implicite de lecture du destinataire détermine les objets destinataire que l’utilisateur auquel le rôle de gestion est attribué est autorisé à lire dans Active Directory.

  - **Étendue d’écriture du destinataire**   L’étendue implicite d’écriture du destinataire détermine les objets destinataire que l’utilisateur auquel le rôle de gestion est attribué est autorisé à modifier dans Active Directory.

  - **Étendue de lecture de configuration**   L’étendue implicite de lecture de configuration détermine les objets de configuration que l’utilisateur auquel le rôle de gestion est attribué est autorisé à lire dans Active Directory.

  - **Étendue d’écriture de configuration**   L’étendue implicite d’écriture de configuration détermine les objets organisation, base de données et serveur que l’utilisateur auquel le rôle de gestion est attribué est autorisé à modifier dans Active Directory.

Les objets destinataire incluent des boîtes aux lettres, des groupes de distribution, des utilisateurs à extension messagerie et d’autres objets. Les objets de configuration incluent les serveurs exécutant Microsoft Exchange Server 2013 ainsi que les bases de données sur les serveurs exécutant Exchange. Chaque type d’étendue peut être implicite ou explicite.

## Étendues implicites

Les étendues implicites sont des étendues par défaut qui s’appliquent à un type de rôle de gestion. Étant donné que les étendues implicites sont associées à un type de rôle de gestion, tous les rôles de gestion parent et enfant de même type ont également les mêmes étendues implicites. Les étendues implicites s’appliquent aux deux rôles de gestion intégrés et également à ceux personnalisés. Pour plus d’informations sur les rôles de gestion et leurs types, voir [Présentation des rôles de gestion](understanding-management-roles-exchange-2013-help.md).

Les tableaux suivants répertorient toutes les étendues implicites qui peuvent être définies sur les rôles de gestion.

### Étendues implicites définies sur les rôles de gestion

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Étendues implicites</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>Organization</code></p></td>
<td><p>Si <code>Organization</code> se trouve dans l’étendue d’écriture du destinataire du rôle, le rôle peut créer ou modifier les objets destinataire au sein de l’organisation Exchange.</p>
<p>Si <code>Organization</code> se trouve dans l’étendue de lecture du destinataire du rôle, le rôle peut afficher n’importe quel objet destinataire au sein de l’organisation Exchange.</p>
<p>Cette étendue est utilisée uniquement avec les étendues de lecture et d’écriture du destinataire.</p></td>
</tr>
<tr class="even">
<td><p><code>MyGAL</code></p></td>
<td><p>Si <code>MyGAL</code> se trouve dans l’étendue d’écriture du destinataire du rôle, le rôle peut afficher les propriétés de n’importe quel destinataire de la liste d’adresses globale de l’utilisateur actuel.</p>
<p>Si <code>MyGAL</code> se trouve dans l’étendue de lecture du destinataire du rôle, le rôle peut afficher les propriétés de n’importe quel destinataire de la liste d’adresses globale actuelle.</p>
<p>Cette étendue est utilisée uniquement avec les étendues de lecture du destinataire.</p></td>
</tr>
<tr class="odd">
<td><p><code>Self</code></p></td>
<td><p>Si <code>Self</code> se trouve dans l’étendue d’écriture du destinataire du rôle, le rôle peut modifier uniquement les propriétés de la boîte aux lettres de l’utilisateur actuel.</p>
<p>Si <code>Self</code> se trouve dans l’étendue de lecture du destinataire du rôle, le rôle peut afficher uniquement les propriétés de la boîte aux lettres de l’utilisateur actuel.</p>
<p>Cette étendue est utilisée uniquement avec les étendues de lecture et d’écriture du destinataire.</p></td>
</tr>
<tr class="even">
<td><p><code>MyDistributionGroups</code></p></td>
<td><p>Si <code>MyDistributionGroups</code> se trouve dans l’étendue d’écriture du destinataire du rôle, le rôle peut créer ou modifier les objets liste de distribution détenus par l’utilisateur actuel.</p>
<p>Si <code>MyDistributionGroups</code> se trouve dans l’étendue de lecture du destinataire du rôle, le rôle peut afficher les objets liste de distribution détenus par l’utilisateur actuel.</p>
<p>Cette étendue est utilisée uniquement avec les étendues de lecture et d’écriture du destinataire.</p></td>
</tr>
<tr class="odd">
<td><p><code>OrganizationConfig</code></p></td>
<td><p>Si <code>OrganizationConfig</code> se trouve dans l’étendue d’écriture de configuration du rôle, le rôle peut créer ou modifier tout objet configuration du serveur ou de la base de données au sein de l’organisation Exchange.</p>
<p>Si <code>OrganizationConfig</code> se trouve dans l’étendue de lecture de configuration du rôle, le rôle peut afficher tout objet configuration du serveur ou de la base de données au sein de l’organisation Exchange.</p>
<p>Cette étendue est utilisée uniquement avec les étendues de lecture et d’écriture de configuration.</p></td>
</tr>
<tr class="even">
<td><p><code>None</code></p></td>
<td><p>Si <code>None</code> se trouve dans une étendue, cette étendue n’est pas disponible pour le rôle. Par exemple, un rôle ayant <code>None</code> dans l’étendue d’écriture du destinataire ne peut pas modifier les objets destinataire dans l’organisation Exchange.</p></td>
</tr>
</tbody>
</table>


Si un rôle est attribué à une personne et qu’aucune étendue prédéfinie ou personnalisée n’est spécifiée, les étendues implicites définies sur le rôle sont utilisées pour contrôler les objets destinataire ou organisation que l’utilisateur peut afficher ou modifier.

L’étendue d’écriture implicite d’un rôle est toujours égale à ou inférieure à l’étendue de lecture implicite. Cela signifie qu’un rôle ne peut jamais modifier des objets invisibles par l’étendue.

Vous ne pouvez pas modifier les étendues implicites définies sur les rôles de gestion. Vous pouvez, toutefois, remplacer l’étendue d’écriture implicite et l’étendue de configuration sur un rôle de gestion. Lorsqu’une étendue relative prédéfinie ou une étendue personnalisée est utilisée sur une attribution de rôle, l’étendue d’écriture implicite est remplacée et la nouvelle étendue devient prioritaire. L’étendue de lecture implicite d’un rôle ne peut pas être remplacée et s’applique toujours. Pour plus d’informations, voir Étendues relatives prédéfinies et Étendues personnalisées.

Le tableau suivant répertorie tous les rôles de gestion intégrés et leurs étendues implicites. Pour plus d’informations sur les groupes de rôles intégrés, consultez la rubrique [Rôles de gestion intégrés](built-in-management-roles-exchange-2013-help.md).

## Étendues implicites des rôles de gestion intégrés


<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>Rôle de gestion</th>
<th>Étendue de lecture du destinataire</th>
<th>Étendue d’écriture du destinataire</th>
<th>Étendue de lecture de configuration</th>
<th>Étendue d’écriture de configuration</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>Active Directory Permissions</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Address Lists</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>ApplicationImpersonation</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>None</code></p></td>
<td><p><code>None</code></p></td>
</tr>
<tr class="even">
<td><p><code>ArchiveApplication</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Audit Logs</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Cmdlet Extension Agents</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Data Loss Prevention</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Database Availability Groups</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Database Copies</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Databases</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Disaster Recovery</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Distribution Groups</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Edge Subscriptions</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>E-Mail Address Policies</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Exchange Connectors</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Exchange Server Certificates</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Exchange Servers</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Exchange Virtual Directories</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Federated Sharing</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Information Rights Management</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Journaling</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Legal Hold</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>None</code></p></td>
</tr>
<tr class="odd">
<td><p><code>LegalHoldApplication</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Mail Enabled Public Folders</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Mail Recipient Creation</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Mail Recipients</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Mail Tips</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Mailbox Import Export</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Mailbox Search</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>None</code></p></td>
<td><p><code>None</code></p></td>
</tr>
<tr class="even">
<td><p><code>MailboxSearchApplication</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Message Tracking</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Migration</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Monitoring</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Move Mailboxes</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>OfficeExtensionApplication</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>My Custom Apps</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>My Marketplace Apps</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>MyAddressInformation</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>MyBaseOptions</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>MyContactInformation</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>MyDiagnostics</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>MyDisplayName</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>MyDistributionGroupMembership</code></p></td>
<td><p><code>MyGAL</code></p></td>
<td><p><code>MyGAL</code></p></td>
<td><p><code>None</code></p></td>
<td><p><code>None</code></p></td>
</tr>
<tr class="even">
<td><p><code>MyDistributionGroups</code></p></td>
<td><p><code>MyGAL</code></p></td>
<td><p><code>MyDistributionGroups</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>None</code></p></td>
</tr>
<tr class="odd">
<td><p><code>MyMobileInformation</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>MyName</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>MyPersonalInformation</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>MyProfileInformation</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>MyRetentionPolicies</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>MyTeamMailboxes</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>MyTextMessaging</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>MyVoiceMail</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Organization Client Access</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Organization Configuration</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Organization Transport Settings</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>POP3 And IMAP4 Protocols</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Public Folders</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Receive Connectors</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Recipient Policies</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Remote and Accepted Domains</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Reset Password</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Retention Management</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Role Management</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Security Group Creation and Membership</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Send Connectors</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Support Diagnostics</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>TeamMailboxLifecycleApplication</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Transport Agents</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Transport Hygiene</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Transport Queues</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Transport Rules</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>UM Mailboxes</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>UM Prompts</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Unified Messaging</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>UnScoped Role Management</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>UserApplication</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>User Options</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>View-Only Audit Logs</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>None</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>None</code></p></td>
</tr>
<tr class="odd">
<td><p><code>View-Only Configuration</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>None</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>None</code></p></td>
</tr>
<tr class="even">
<td><p><code>View-Only Recipients</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>None</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>None</code></p></td>
</tr>
<tr class="odd">
<td><p><code>WorkloadManagement</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
</tbody>
</table>


## Étendues explicites

Les étendues explicites sont des étendues que vous définissez vous-même pour contrôler les objets qu’un rôle de gestion peut modifier. Alors que les étendues implicites sont définies sur un rôle de gestion, les étendues explicites le sont sur une attribution de rôle de gestion. Ainsi, les étendues implicites sont appliquées systématiquement à tous les rôles de gestion à moins que vous choisissiez d’utiliser une étendue explicite de remplacement. Pour plus d’informations sur les attributions de rôle de gestion, voir [Présentation des attributions de rôles de gestion](understanding-management-role-assignments-exchange-2013-help.md).

Les étendues explicites remplacent les étendues de configuration et d’écriture implicites d’un rôle de gestion. Elles ne remplacent pas l’étendue de lecture implicite d’un rôle de gestion. L’étendue de lecture implicite continue à définir les objets lisibles par le rôle de gestion.

Les étendues explicites sont utiles lorsque l’étendue d’écriture implicite d’un rôle de gestion ne répond pas à vos besoins. Vous pouvez ajouter une étendue explicite pour inclure à peu près tout ce que vous voulez tant que la nouvelle étendue ne dépasse pas les limites de l’étendue de lecture implicite. Les cmdlets faisant partie d’un rôle de gestion doivent pouvoir lire les informations sur les objets ou les conteneurs d’objets pour pouvoir créer ou modifier les objets. Par exemple, si l’étendue de lecture implicite d’un rôle de gestion est définie sur `Self`, vous ne pouvez pas ajouter une étendue d’écriture explicite `Organization`, car cette dernière dépasse les limites de la première.

Pour plus d’informations, voir les ressources suivantes :

  - Étendues relatives prédéfinies

  - Étendues personnalisées

## Étendues relatives prédéfinies

Exchange 2013 propose plusieurs étendues d’écriture relatives prédéfinies que vous pouvez utiliser pour modifier l’étendue d’un rôle de gestion. Les étendues relatives prédéfinies répondent plus précisément à vos besoins sans avoir à créer manuellement des étendues personnalisées. Elles s’appellent étendues relatives, car elles sont relatives à la personne à laquelle l’attribution de rôle associée est affectée. Par exemple, l’étendue relative prédéfinie `Self` limite cette étendue d’écriture uniquement à l’utilisateur actuel. L’étendue relative prédéfinie `MyDistributionGroups` limite l’étendue d’écriture uniquement au groupe de distribution appartenant à l’utilisateur actuel. Les étendues relatives prédéfinies sont uniquement utilisables pour délimiter les objets destinataire. Les étendues relatives prédéfinies ne peuvent pas être utilisées pour délimiter les objets configuration. Le tableau suivant répertorie les étendues relatives prédéfinies que vous pouvez utiliser.

### Étendues relatives prédéfinies

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Étendues implicites</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>Organization</code></p></td>
<td><p>Si <code>Organization</code> se trouve dans l’étendue d’écriture du destinataire du rôle, le rôle peut créer ou modifier les objets destinataire au sein de l’organisation Exchange.</p>
<p>Si <code>Organization</code> se trouve dans l’étendue de lecture du destinataire du rôle, le rôle peut afficher n’importe quel objet destinataire au sein de l’organisation Exchange.</p>
<p>Cette étendue est utilisée uniquement avec les étendues de lecture et d’écriture du destinataire.</p></td>
</tr>
<tr class="even">
<td><p><code>Self</code></p></td>
<td><p>Si <code>Self</code> se trouve dans l’étendue d’écriture du destinataire du rôle, le rôle peut modifier uniquement les propriétés de la boîte aux lettres de l’utilisateur actuel.</p>
<p>Si <code>Self</code> se trouve dans l’étendue de lecture du destinataire du rôle, le rôle peut afficher uniquement les propriétés de la boîte aux lettres de l’utilisateur actuel.</p>
<p>Cette étendue est utilisée uniquement avec les étendues de lecture et d’écriture du destinataire.</p></td>
</tr>
<tr class="odd">
<td><p><code>MyDistributionGroups</code></p></td>
<td><p>Si <code>MyDistributionGroups</code> se trouve dans l’étendue d’écriture du destinataire du rôle, le rôle peut créer ou modifier les objets liste de distribution détenus par l’utilisateur actuel.</p>
<p>Si <code>MyDistributionGroups</code> se trouve dans l’étendue de lecture du destinataire du rôle, le rôle peut afficher les objets liste de distribution détenus par l’utilisateur actuel.</p>
<p>Cette étendue est utilisée uniquement avec les étendues de lecture et d’écriture du destinataire.</p></td>
</tr>
</tbody>
</table>


Les étendues relatives prédéfinies sont appliquées lorsque vous créez une nouvelle attribution de rôle de gestion. Lors de la création de l’attribution de rôle, à l’aide de la cmdlet **New-ManagementRoleAssignment**, vous pouvez spécifier une étendue relative prédéfinie en utilisant le paramètre *RecipientRelativeWriteScope*. Lorsque la nouvelle attribution de rôle est créée, le nouveau rôle prédéfini remplace l’étendue d’écriture implicite du rôle de gestion. Vous ne pouvez pas spécifier une étendue de destinataire personnalisée lorsque vous créez une attribution de rôle avec une étendue relative prédéfinie. En revanche, vous pouvez spécifier une étendue de configuration personnalisée, si nécessaire.

Pour plus d’informations sur l’ajout d’une attribution de rôle de gestion à une étendue relative prédéfinie, voir [Ajouter un rôle à un utilisateur ou un groupe de sécurité universel](add-a-role-to-a-user-or-usg-exchange-2013-help.md).

## Étendues personnalisées

Les étendues personnalisées sont nécessaires lorsque ni l’étendue d’écriture implicite ni l’étendue relative prédéfinie ne répondent pas à vos besoins. Les étendues personnalisées permettent de définir plus précisément l’étendue à laquelle le rôle de gestion sera appliqué. Par exemple, vous voudrez peut-être cibler une unité d’organisation spécifique, un type de destinataire particulier ou les deux. Ou vous pourriez vouloir seulement permettre à un groupe d’administrateurs de gérer un ensemble spécifique de bases de données de boîtes aux lettres.

Comme pour les étendues relatives prédéfinies, les étendues personnalisées remplacent les étendues de configuration d’organisation et d’écriture implicite définies sur les rôles de gestion. L’étendue de lecture implicite sur les rôles de gestion continue à s’appliquer et l’étendue personnalisée obtenue ne doit pas dépasser les limites de l’étendue de lecture implicite. Vous pouvez créer les trois types d’étendue personnalisée suivants :

  - **Étendue d’organisation**   Cette étendue personnalisée la plus simple est créée à l’aide du paramètre *RecipientOrganizationalUnitScope* sur la cmdlet **New-ManagementRoleAssignment**. En spécifiant une étendue d’unité d’organisation lorsqu’un rôle est attribué, l’utilisateur auquel le rôle est attribué peut modifier uniquement les objets destinataire contenus dans cette unité d’organisation. Pour plus d’informations sur l’ajout d’une attribution de rôle de gestion à une étendue d’unité d’organisation, voir [Ajouter un rôle à un utilisateur ou un groupe de sécurité universel](add-a-role-to-a-user-or-usg-exchange-2013-help.md).

  - **Étendue filtrée de destinataire**   Les étendues filtrées de destinataire utilisent des filtres permettant de cibler des destinataires en particulier selon leur type ou d’autres propriétés telles que le service, le responsable, le lieu, entre autres. Pour plus d’informations, consultez la rubrique Étendues filtrées de destinataire.

  - **Étendue de configuration**   Les étendues de configuration utilisent des filtres permettant de cibler des serveurs spécifiques en fonction de listes de serveurs ou de propriétés filtrables définissables sur les serveurs, telles qu’un site Active Directory ou un rôle serveur.  Les étendues de configuration peuvent également utiliser les étendues de base de données pour cibler des bases de données spécifiques en fonction de listes de bases de données ou de propriétés filtrables. Pour plus d’informations, consultez la rubrique Étendues de configuration.

Des étendues personnalisées de destinataire et de configuration, soit simples et vastes, soit complexes et précises, peuvent être créées à l’aide de la cmdlet **New-ManagementScope**. Lorsque vous créez une étendue de destinataire ou de configuration, seuls les objets destinataire, serveur ou base de données répondant à leurs étendues respectives sont renvoyés. Lorsque ces étendues sont appliquées à une attribution de rôle à l’aide de la cmdlet **New-ManagementRoleAssignment** ou **Set-ManagementRoleAssignment**, seuls les objets répondant aux étendues peuvent être modifiés par les personnes auxquelles est attribué le rôle. Une fois l’étendue personnalisée créée, vous ne pouvez pas changer le type d’étendue. Une étendue de destinataire est toujours une étendue de destinataire et une étendue de configuration est toujours une étendue de configuration.

Par défaut, une étendue personnalisée permet à une personne attribuée au rôle d’accéder à un ensemble d’objets qui répondent aux étendues définies. Toutefois, l’accès aux autres personnes attribuées au rôle auxquelles n’est pas attribuée également l’étendue identique ou équivalente n’est pas activement exclu. Toute étendue personnalisée peut accéder aux mêmes objets si les listes ou filtres de ces étendues correspondent aux mêmes objets. Pour certains objets, ce comportement n’est pas souhaité, par exemple, pour le personnel d’encadrement. Pour ces objets, vous pouvez définir des étendues exclusives. Les étendues exclusives utilisent les filtres ou listes de la même façon que les étendues normales, sauf qu’elles refusent l’accès aux objets inclus dans l’étendue à quiconque ne fait pas partie de l’étendue exclusive identique ou équivalente. Pour plus d’informations sur les étendues exclusives, voir [Présentation des étendues exclusives](understanding-exclusive-scopes-exchange-2013-help.md).

## Étendues filtrées de destinataire

Les étendues filtrées de destinataire vous permettent de contrôler quels objets destinataire peuvent être gérés par les personnes auquel le rôle est attribué en évaluant une ou plusieurs propriétés d’un objet destinataire par rapport à une valeur que vous définissez dans une instruction de filtrage. Les destinataires inclus dans des étendues de destinataire sont des boîtes aux lettres, des utilisateurs à extension messagerie, des groupes de distribution et des contacts de messagerie. Seuls les destinataires correspondant au filtre spécifié peuvent être gérés par les personnes auxquelles est attribué ce rôle. Un exemple d’instruction de filtrage est `{ Name -Eq "David" }` où **Name** est la propriété de l’objet destinataire en cours d’évaluation et où **David** est la valeur que vous utilisez pour l’évaluer. L’opérateur de comparaison **-Eq** indique que la valeur enregistrée dans la propriété doit être égale à la valeur spécifiée pour le filtre comme étant de type true. Si le filtre a la valeur true, le destinataire est inclus dans l’étendue.

Les étendues filtrées de destinataire sont créées en spécifiant le filtre destinataire à utiliser avec le paramètre *RecipientRestrictionFilter* sur la cmdlet **New-ManagementScope**. Par défaut, la cmdlet **New-ManagementScope** crée des étendues normales. Pour créer une étendue exclusive, intégrez le commutateur *Exclusive* au paramètre *RecipientRestrictionFilter*.

Lorsque vous créez un filtre de restriction destinataire, Exchange évalue le filtre fourni par rapport à chaque objet destinataire.de l’organisation par défaut. Pour limiter les destinataires qui seront évalués par l’étendue, vous pouvez utiliser le paramètre *RecipientRoot* en association avec le paramètre *RecipientRestrictionFilter*. Le paramètre *RecipientRoot* accepte une unité d’organisation. Lorsque vous utilisez le paramètre *RecipientRoot*, Exchange évalue uniquement les destinataires inclus dans l’unité d’organisation spécifiée par rapport au filtre que vous avez fourni.

Lorsque vous ajoutez une étendue filtrée de destinataire à une attribution de rôle, spécifiez le nom de l’étendue de destinataire dans le paramètre *CustomRecipientWriteScope* sur la cmdlet **New-ManagementRoleAssignment** si vous créez une nouvelle attribution de rôle ou sur la cmdlet **Set-ManagementRoleAssignment** si vous mettez à jour une attribution de rôle existante. Chaque attribution de rôle peut avoir une étendue de destinataire, y compris les étendues relatives prédéfinies. Vous pouvez ajouter une étendue de configuration à la même attribution de rôle à laquelle vous avez ajouté une étendue de destinataire.

Pour plus d’informations sur la syntaxe du filtre et pour obtenir la liste complète des propriétés filtrables des destinataires, voir [Présentation des filtres d’attribution du rôle de gestion](understanding-management-role-scope-filters-exchange-2013-help.md).

## Étendues de configuration

Les éléments suivants sont les deux types d’étendues de configuration proposées dans Exchange 2013 :

  - **Étendues de serveur**   Il existe deux types d’étendue de serveur : étendue filtrée de serveur et étendue de liste de serveurs. Si un objet serveur est inclus dans une étendue de serveur, il est possible de gérer la configuration d’un serveur comprenant des connecteurs de réception, des files d’attente de transport, des certificats de serveur, des répertoires virtuels, etc.
    
      - **Étendues filtrées de serveur**   Les étendues filtrées de serveur vous permettent de contrôler quels objets serveur peuvent être gérés par les personnes auxquelles le rôle est attribué en évaluant une ou plusieurs propriétés d’un objet serveur par rapport à une valeur que vous définissez dans une instruction de filtrage. Pour créer une étendue filtrée de serveur, utilisez le paramètre *ServerRestrictionFilter* sur la cmdlet **New-ManagementScope**.
    
      - **Étendues de liste de serveurs**   Les étendues de liste de serveurs vous permettent de contrôler quels objets serveur peuvent être gérés par les personnes auxquelles le rôle est attribué en définissant une liste de serveurs accessible par une personne à laquelle le rôle a été attribué. Pour créer une étendue de liste de serveurs, utilisez le paramètre *ServerList* sur la cmdlet **New-ManagementScope**.

  - **Étendues de base de données**   Il existe deux types d’étendue de base de données : étendue filtrée de base de données et étendue de liste de bases de données. Il est possible de gérer configuration de base de données si un objet base de données est inclus dans une étendue de base de données comprenant des limites de quota de base de données, la maintenance de la base de données, la réplication des dossiers publics, le montage ou non d’une base de données, etc. Outre la configuration de bases de données, les étendues de base de données peuvent aussi servir à contrôler les bases de données dans lesquelles des destinataires peuvent être créés. Si vous avez des serveurs antérieurs à Exchange 2010 SP1 dans votre organisation, consultez la section Les étendues de base de données et les versions antérieures d’Exchange plus loin dans cette rubrique.
    
      - **Étendues filtrées de base de données**   Les étendues filtrées de base de données vous permettent de contrôler quels objets base de données peuvent être gérés par les personnes auxquelles le rôle est attribué en évaluant une ou plusieurs propriétés d’un objet base de données par rapport à une valeur que vous définissez dans une instruction de filtrage. Pour créer une étendue filtrée de base de données, utilisez le paramètre *DatabaseRestrictionFilter* sur la cmdlet **New-ManagementScope**.
    
      - **Étendues de liste de bases de données**   Les étendues de liste de bases de données vous permettent de contrôler quels objets base de données peuvent être gérés par les personnes auxquelles le rôle est attribué en définissant une liste de bases de données accessible par une personne à laquelle le rôle a été attribué. Pour créer une étendue de liste des bases de données, utilisez le paramètre *DatabaseList* sur la cmdlet **New-ManagementScope**.

Pour plus d’informations sur la syntaxe du filtre et pour obtenir la liste complète des propriétés filtrables des serveurs et des bases de données, voir [Présentation des filtres d’attribution du rôle de gestion](understanding-management-role-scope-filters-exchange-2013-help.md).

Les listes de serveurs et de bases de données peuvent être définies en spécifiant chaque serveur et base de données que vous voulez inclure dans leurs étendues respectives. Plusieurs serveurs ou bases de données peuvent être spécifiés dans leurs étendues respectives en séparant les noms de serveur et de base de données par des virgules.

Lorsque vous ajoutez une étendue de configuration de serveur ou de base de données à une attribution de rôle, spécifiez le nom de l’étendue correspondante dans le paramètre *CustomConfigWriteScope* sur la cmdlet **New-ManagementRoleAssignment** si vous créez une nouvelle attribution de rôle ou sur la cmdlet **Set-ManagementRoleAssignment** si vous mettez à jour une attribution de rôle existante. Chaque attribution de rôle ne peut avoir qu’une seule étendue de configuration.

Outre le fait de contrôler quelles bases de données peuvent être gérées par les personnes auxquelles le rôle est attribué, les étendues de base de données vous permettent également de contrôler dans quelles bases de données les personnes auxquelles est attribué le rôle peuvent créer des boîtes aux lettres. C’est une fonctionnalité distincte de celle de contrôler quels destinataires peuvent être gérés par une personne à laquelle le rôle a été attribué. Si la personne à laquelle le rôle a été attribué dispose des autorisations de création d’une nouvelle boîte aux lettres, d’étendre la messagerie à un utilisateur existant ou de déplacer des boîtes aux lettres, vous pouvez alors affiner encore ces autorisations à l’aide des étendues de base de données pour contrôler la base de données dans laquelle la boîte aux lettres est créée ou dans quelle base de données une boîte aux lettres est déplacée. Le contrôle des destinataires pouvant être gérés par une personne à laquelle le rôle a été attribué est opéré avec une étendue de destinataire qui est spécifiée dans le paramètre *CustomRecipientWriteScope* sur la cmdlet **New-ManagementRoleAssignment** ou **Set-ManagementRoleAssignment**. Pour contrôler dans quelles bases de données une boîte aux lettres peut être créée ou déplacée, il faut utiliser une étendue de base de données spécifiée dans le paramètre *CustomConfigurationWriteScope* sur les mêmes cmdlets.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>La distribution automatique des boîtes aux lettres peut être contrôlée à l’aide des étendues de base de données.</td>
</tr>
</tbody>
</table>


La gestion des fonctionnalités d’Exchange peut exiger des étendues de serveur ou de base de données, ou les deux types d’étendue. Si la gestion d’une fonctionnalité requiert à la fois des étendues de serveur et de base de données, deux attributions de rôle doivent être créées et dévolues à la personne à laquelle le rôle est attribué et possédant l’accès à la gestion de la fonctionnalité. Une attribution de rôle doit être associée à l’étendue de serveur et l’autre attribution de rôle à l’étendue de base de données.

Certaines cmdlets peuvent utiliser les étendues de configuration qui ne sont pas immédiatement évidentes. Le tableau suivant inclut une liste de cmdlets et d’étendues de configuration que vous pouvez utiliser pour contrôler leur utilisation. Pour les cmdlets incluses dans les fonctionnalités spécifiques, les étendues de configuration vous permettent de contrôler dans quelles bases de données les destinataires peuvent être créés. Elles ne contrôlent pas quels destinataires peuvent être gérés. La colonne **Étendues requises** peut contenir les éléments suivants :

  - **Base de données**   Pour exécuter la cmdlet, soit la personne à laquelle le rôle est attribué doit avoir une attribution de rôle associée à une étendue de base de données qui inclut la base à gérer, soit l’étendue implicite d’écriture de configuration implicite doit inclure la base de données à gérer.

  - **Serveur**   Pour exécuter la cmdlet, soit la personne à laquelle le rôle est attribué doit avoir une attribution de rôle associée à une étendue de serveur qui inclut le serveur à gérer, soit l’étendue implicite d’écriture de configuration implicite doit inclure le serveur à gérer.

  - **Serveur ou base de données**   Pour exécuter la cmdlet, la personne à laquelle le rôle est attribué doit avoir une attribution de rôle associée soit à une étendue de base de données incluant à la base à gérer, soit à une étendue de serveur incluant le serveur dans lequel se trouve la base de données. Sinon, l’étendue implicite de configuration de rôle doit contenir la base à gérer ou contenir le serveur dans lequel se trouve la base de données et l’attribution de rôle ne peut pas avoir d’étendue d’écriture personnalisée.

  - **Serveur et base de données**   Pour exécuter cette commande, deux attributions de rôle doivent être conférées à la personne concernée. La première attribution de rôle doit inclure une étendue de base de données qui inclut la base à gérer. La deuxième attribution de rôle doit inclure une étendue de serveur qui inclut le serveur dans lequel se trouve la base de données. Des étendues de configuration personnalisées peuvent avoir été définies pour les attributions de rôle ou ces dernières peuvent hériter d’une étendue implicite d’écriture de configuration par l’intermédiaire du rôle. Pour hériter de l’étendue implicite d’écriture du rôle, l’attribution de rôle ne doit pas avoir d’étendue d’écriture personnalisée.

### Fonctionnalités et étendues de base de données et serveur applicables

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Fonctionnalités</th>
<th>Cmdlet</th>
<th>Étendues requises</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Bases de données</p></td>
<td><p><strong>Dismount-Database</strong></p></td>
<td><p>Base de données</p></td>
</tr>
<tr class="even">
<td><p>Bases de données</p></td>
<td><p><strong>Mount-Database</strong></p></td>
<td><p>Base de données</p></td>
</tr>
<tr class="odd">
<td><p>Bases de données</p></td>
<td><p><strong>Move-DatabasePath</strong></p></td>
<td><p>Serveur et base de données</p></td>
</tr>
<tr class="even">
<td><p>Bases de données</p></td>
<td><p><strong>Remove-MailboxDatabase</strong></p></td>
<td><p>Serveur ou base de données</p></td>
</tr>
<tr class="odd">
<td><p>Bases de données</p></td>
<td><p><strong>Set-MailboxDatabase</strong></p></td>
<td><p>Base de données</p></td>
</tr>
<tr class="even">
<td><p>Haute disponibilité</p></td>
<td><p><strong>Add-DatabaseAvailabilityGroupServer</strong></p></td>
<td><p>Serveur</p></td>
</tr>
<tr class="odd">
<td><p>Disponibilité élevée</p></td>
<td><p><strong>Add-MailboxDatabaseCopy</strong></p></td>
<td><p>Serveur</p></td>
</tr>
<tr class="even">
<td><p>Disponibilité élevée</p></td>
<td><p><strong>Move-ActiveMailboxDatabase</strong></p></td>
<td><p>Serveur</p></td>
</tr>
<tr class="odd">
<td><p>Disponibilité élevée</p></td>
<td><p><strong>Remove-DatabaseAvailabilityGroupServer</strong></p></td>
<td><p>Serveur</p></td>
</tr>
<tr class="even">
<td><p>Disponibilité élevée</p></td>
<td><p><strong>Remove-MailboxDatabaseCopy</strong></p></td>
<td><p>Serveur ou base de données</p></td>
</tr>
<tr class="odd">
<td><p>Disponibilité élevée</p></td>
<td><p><strong>Resume-MailboxDatabaseCopy</strong></p></td>
<td><p>Serveur ou base de données</p></td>
</tr>
<tr class="even">
<td><p>Disponibilité élevée</p></td>
<td><p><strong>Set-MailboxDatabaseCopy</strong></p></td>
<td><p>Serveur ou base de données</p></td>
</tr>
<tr class="odd">
<td><p>Disponibilité élevée</p></td>
<td><p><strong>Suspend-MailboxDatabaseCopy</strong></p></td>
<td><p>Serveur ou base de données</p></td>
</tr>
<tr class="even">
<td><p>Disponibilité élevée</p></td>
<td><p><strong>Update-MailboxDatabaseCopy</strong></p></td>
<td><p>Serveur ou base de données</p></td>
</tr>
<tr class="odd">
<td><p>Destinataires</p></td>
<td><p><strong>Connect-Mailbox</strong></p></td>
<td><p>Base de données</p></td>
</tr>
<tr class="even">
<td><p>Destinataires</p></td>
<td><p><strong>Enable-Mailbox</strong></p></td>
<td><p>Base de données</p></td>
</tr>
<tr class="odd">
<td><p>Destinataires</p></td>
<td><p><strong>New-Mailbox</strong></p></td>
<td><p>Base de données</p></td>
</tr>
<tr class="even">
<td><p>Destinataires</p></td>
<td><p><strong>New-MoveRequest</strong></p></td>
<td><p>Base de données</p></td>
</tr>
<tr class="odd">
<td><p>Résolution des problèmes</p></td>
<td><p><strong>Test-MapiConnectivity</strong></p></td>
<td><p>Base de données</p></td>
</tr>
</tbody>
</table>


## Les étendues de base de données et les versions antérieures d’Exchange

Le concept des étendues de base de données a été introduit pour la première fois dans Microsoft Exchange 2010 Service Pack 1 (SP1) et continue d’être pris en charge dans Exchange 2013. Les versions d’Exchange antérieures à Exchange 2010 SP1 prennent en charge uniquement les étendues de destinataire et les étendues de configuration de serveur. Si vous créez une nouvelle étendue de base de données sur un serveur Exchange 2010 SP1 ou ultérieur, vous recevrez l’avertissement suivant :

    WARNING: Database management scopes will only be applied when a user connects to a server running Exchange 2010 SP1 or later. Servers running a version of Exchange prior to Exchange 2010 SP1 won't apply any roles from a role assignment linked to a database scope. Database management scopes also won't be visible to the Get-ManagementScope cmdlet when it's run from a pre-Exchange 2010 SP1 server.

Lorsque vous créez une étendue de base de données, elle s’applique uniquement aux utilisateurs se connectant à des serveurs exécutant Exchange 2010 SP1 ou ultérieur. Les utilisateurs qui se connectent à des serveurs exécutant des versions antérieures à Exchange 2010 SP1 ne disposeront d’aucune attribution de rôle associée à des étendues de base de données qui leur sont appliquées. Cela signifie que les autorisations délivrées par ces attributions de rôle ne seront pas accordées aux utilisateurs se connectant à des serveurs exécutant des versions antérieures à Exchange 2010 SP1. Les étendues de base de données ne peuvent pas être créées, supprimées, modifiées ni consultées depuis des serveurs exécutant des versions antérieures à Exchange 2010 SP1.

Une étendue de base de données peut inclure n’importe quelle base de données de votre organisation Exchange. Ceci comprend des serveurs Exchange Server 2007, Exchange 2010 et Exchange 2013. Ceci vous permet de contrôler quelles bases de données peuvent être gérées par les utilisateurs, quelle que soit la version d’ Exchange. Comme pour d’autres étendues de base de données, les attributions de rôles associées à des étendues contenant des bases de données Exchange 2007 et Exchange 2010 s’appliquent uniquement aux utilisateurs se connectant à un serveur Exchange 2010 SP1 ou ultérieur.

Les utilisateurs se connectant à un serveur dont la version est antérieure à Exchange 2010 SP1 peuvent afficher et modifier les attributions de rôles associées aux étendues de base de données. Cela inclut le changement de l’étendue de configuration sur une attribution de rôle existante en une étendue de serveur si celle-ci est alors associée à une étendue de base de données. Cependant, si l’étendue de configuration sur une attribution de rôle est modifiée en étendue de serveur et si un utilisateur veut ultérieurement revenir à une étendue de base de données, ou encore passer d’une étendue de configuration à une autre étendue de base de données, cet utilisateur doit effectuer le changement lorsqu’il est connecté à un serveur Exchange 2010 SP1 ou ultérieur. Les utilisateurs ne peuvent spécifier des étendues de serveur que lorsqu’ils modifient l’étendue de configuration sur une attribution de rôle en étant connectés à un serveur dont la version est antérieure à Exchange 2010 SP1.

