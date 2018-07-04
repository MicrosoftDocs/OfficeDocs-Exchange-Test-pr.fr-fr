---
title: 'Gestion de l’organisation: Exchange 2013 Help'
TOCTitle: Gestion de l’organisation
ms:assetid: 0bfd21c1-86ac-4369-86b7-aeba386741c8
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dd335087(v=EXCHG.150)
ms:contentKeyID: 50477536
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Gestion de l’organisation

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2015-03-09_

Le Gestion de l’organisation Le groupe de rôles de gestion est l’un des groupes de rôles intégrés qui créent un modèle d’autorisations de contrôle d’accès basé sur un rôle (RBAC) dans Microsoft Exchange Server 2013. Un ou plusieurs rôles de gestion sont affectés aux groupes de rôles qui contiennent les autorisations requises pour effectuer un ensemble de tâches données. Les membres d’un groupe de rôles sont autorisés à accéder aux rôles de gestion attribués au groupe de rôles. Pour plus d’informations sur les groupes de rôles, consultez la rubrique [Présentation des groupes de rôles de gestion](understanding-management-role-groups-exchange-2013-help.md).

Les administrateurs membres du groupe de rôles Gestion de l’organisation disposent d’un accès administratif à toute l’organisation Exchange 2013 et peuvent réaliser presque n’importe quelle tâche relative à un objet Exchange 2013, avec quelques exceptions. Par défaut, les membres de ce groupe de rôles ne peuvent pas réaliser de recherches de boîtes aux lettres ni faire de gestion de rôles de gestion de la direction supérieure non étendus. Pour plus d’informations, consultez la section « Attributions de rôle de délégation uniquement » plus loin dans cette rubrique.

> [!NOTE]
> Le groupe de rôles Gestion de l’organisation est un rôle très puissant et, à ce titre, seuls des utilisateurs ou des groupes de sécurité universels qui exécutent des tâches administratives au niveau organisationnel peuvent affecter l’intégralité de l’organisation Exchange s’ils sont membres de ce groupe de rôles.


Ce groupe de rôles correspond au rôle Administrateurs de l’organisation Exchange dans Exchange Server 2007.

Pour plus d’informations sur le contrôle d’accès basé sur un rôle, voir [Présentation du contrôle d'accès basé sur un rôle](understanding-role-based-access-control-exchange-2013-help.md).

## Appartenance au groupe de rôles

Par défaut, le compte servant à installer Exchange 2013 dans l’organisation est ajouté comme membre du groupe de rôles Gestion de l’organisation. Ce compte peut ensuite ajouter d’autres membres au groupe de rôles de votre choix.

Si vous souhaitez ajouter ou supprimer des membres dans ce groupe de rôle, consultez la rubrique [Gérer les membres de groupes de rôles](manage-role-group-members-exchange-2013-help.md).

Par défaut, seuls les membres du groupe de rôles Gestion de l’organisation peuvent ajouter des membres de ce groupe de rôles ou en supprimer. Pour plus d’informations sur l’ajout de délégués de groupe de rôles supplémentaires, consultez la rubrique « Ajouter ou supprimer un délégué de groupe de rôles » dans [Gérer des groupes de rôles](manage-role-groups-exchange-2013-help.md).

Vous pouvez utiliser la commande suivante pour afficher une liste des utilisateurs ou des groupes de sécurité universelle qui sont membres de ce groupe de rôles.

    Get-RoleGroupMember "Organization Management"

Pour plus d’informations sur les membres d’un groupe de rôles, voir [Gérer des groupes de rôles](manage-role-groups-exchange-2013-help.md).

## Personnalisation d’un groupe de rôles

Ce groupe de rôles est attribué aux rôles de gestion par défaut. Les rôles inclus sont répertoriés dans la section « Rôles de gestion attribués à ce groupe de rôles ». Vous pouvez ajouter ou supprimer des attributions de rôles dans ce groupe de rôles pour qu’ils correspondent aux besoins de votre organisation.

Les groupes de rôles fournis avec Exchange 2013 sont conçus pour correspondre à des tâches plus précises. En attribuant des rôles à un groupe de rôles, vous permettez aux membres de ce groupe de rôles d’effectuer les tâches associées au rôle. Par exemple, le rôle de journalisation permet la gestion de l’agent de journalisation et des règles de journalisation. Pour plus d’informations sur la façon dont les rôles sont attribués aux groupes de rôles, voir [Présentation des attributions de rôles de gestion](understanding-management-role-assignments-exchange-2013-help.md).

Les rôles attribués à ce groupe de rôles bénéficient d’étendues de gestion par défaut. Les étendues de gestion déterminent les objets Exchange qui peuvent être visualisés ou modifiés par les membres d’un groupe de rôles. Vous pouvez modifier les étendues associées aux attributions entre les rôles et les groupes de rôles. Par exemple, vous souhaitez peut-être effectuer cette opération si vous voulez uniquement que les membres d’un groupe de rôles puissent modifier les destinataires qui se trouvent dans une unité d’organisation ou un emplacement spécifique. Pour plus d’informations sur les étendues de gestion, voir [Présentation des portées du rôle de gestion](understanding-management-role-scopes-exchange-2013-help.md).

Pour plus d’informations sur la manière de personnaliser ce groupe de rôles, consultez les rubriques suivantes :

  - [Gérer des groupes de rôles](manage-role-groups-exchange-2013-help.md)

  - [Gérer les membres de groupes de rôles](manage-role-group-members-exchange-2013-help.md)

Si vous souhaitez créer un groupe de rôles et attribuer certains des rôles affectés à ce groupe de rôles au nouveau groupe de rôles, consultez la section « Créer un groupe de rôles » dans la rubrique [Gérer des groupes de rôles](manage-role-groups-exchange-2013-help.md).

Voici quelques méthodes que vous souhaiterez peut-être utiliser pour personnaliser ce rôle :

  - **Détenteur d’autorisations**   Si les autorisations de votre organisation sont contrôlées par un groupe spécifique autre que celui constitué par les administrateurs Exchange, vous pouvez créer un groupe de rôles et transférer les attributions de rôle du rôle Gestion des rôles au nouveau groupe de rôles. En effectuant cette opération, vous empêchez les membres du groupe de rôles Gestion de l’organisation de gérer les autorisations RBAC.

  - **Autorisations fractionnées Active Directory**   Si la création des entités de sécurité au sein de votre organisation, tels que les comptes d’utilisateurs, est contrôlée par un groupe spécifique autre que celui des administrateurs Exchange, vous pouvez créer un groupe de rôles et déplacer les attributions des rôles ordinaires et de délégation du rôle Création du destinataire de messagerie et Création du groupe de sécurité et appartenance dans le nouveau groupe de rôles. En effectuant cette opération, vous empêchez les membres du groupe de rôles Gestion de l’organisation de créer des objets Active Directory. Ils peuvent cependant continuer d’attribuer une extension de messagerie pour les nouveaux objets Active Directory. Pour plus d’informations sur les autorisations de partage, voir [Présentation des autorisations fractionnées](understanding-split-permissions-exchange-2013-help.md).

## Limitations de personnalisation

N’importe quel rôle peut être ajouté ou supprimé de ce groupe de rôle, avec les limitations suivantes :

  - Chaque rôle doit avoir au moins une attribution de rôle de délégation dans un groupe de rôle ou un groupe de sécurité universel avant que l’attribution de rôle de délégation puisse être retirée de ce groupe de rôles.

  - Le rôle Gestion des rôles doit avoir au moins une attribution de rôle de délégation dans un groupe de rôle ou un groupe de sécurité universel avant que l’attribution de rôle ordinaire puisse être retirée de ce groupe de rôles.

Ces limitations ont pour but de vous éviter d’être bloqué du système par inadvertance. En exigeant l’existence d’au moins une attribution de rôle de délégation entre chaque rôle et un ou plusieurs groupes de rôles ou groupes de sécurité universels, vous pourrez toujours attribuer des rôles à leurs utilisateurs. En exigeant l’existence d’au moins une attribution de rôle ordinaire entre le rôle Gestion des rôles et un ou plusieurs groupes de rôles ou groupes de sécurité universels, vous pourrez toujours configurer des groupes de rôles et des attributions de rôles.

> [!NOTE]
> Ces limitations requièrent que les groupes de rôles ou les groupes de sécurité universels soient les cibles des attributions de rôle de délégation ou ordinaires. Vous ne pouvez pas supprimer une attribution de rôle de délégation ou l’attribution ordinaire du rôle Gestion des rôles si la dernière attribution est effectuée auprès d’un utilisateur.


## Attributions de rôle de délégation uniquement

Certaines attributions de rôle entre le groupe de rôles Gestion de l’organisation et les rôles de gestion (recherche de boîte aux lettres et gestion des rôles non délimités, par exemple), sont des attributions de rôle de délégation uniquement. Ces rôles autorisent l’accès à des informations sensibles ou personnelles, comme le contenu des boîtes aux lettres, ou permettent la création de puissants rôles de gestion non délimités.

Les attributions de rôle de délégation uniquement permettent aux seuls membres du groupe de rôles Gestion de l’organisation d’attribuer les rôles associés à d’autres groupes de rôles, stratégies d’attribution des rôles de gestion, utilisateurs ou groupes de sécurité universels. Les autorisations que les rôles fournissent ne sont pas attribués par défaut aux membres du groupe de rôles Gestion de l’organisation. Cela évite aux informations personnelles d’être exposées accidentellement ou une élévation accidentelle des privilèges.

Les membres du groupe de rôles Gestion de l’organisation peuvent, toutefois, s’attribuer n’importe quel rôle, leur permettant en réalité d’exécuter n’importe quelle tâche. Par exemple, un membre du groupe de rôles Gestion de l’organisation peut attribuer le rôle de recherche de boîte aux lettres au groupe de rôles Gestion de l’organisation. Suite à cette attribution de rôle, les membres du groupe de rôles Gestion de l’organisation peuvent réaliser des tâches activées par le rôle Recherche de boîte aux lettres.

Pour plus d’informations sur les attributions des rôles de délégation, voir [Présentation des attributions de rôles de gestion](understanding-management-role-assignments-exchange-2013-help.md).

## Autorisations supplémentaires

Les autorisations accordées aux membres du groupe de rôles Gestion de l’organisation sont avant tout déterminées par les rôles de gestion attribués au groupe de rôles. Cependant, certaines tâches que vous devez effectuer ne sont pas prises en compte par les rôles de gestion. Certaines tâches se produisent hors des outils de gestion Exchange et par conséquent le modèle des autorisations RBAC ne s’applique pas. Pour ces tâches, les autorisations sont fournies en ajoutant le groupe de rôles Gestion de l’organisation aux listes de contrôle d’accès de certains objets Active Directory.

Des autorisations sont accordées aux tâches suivantes au moyen de listes de contrôle d’accès sur des objets Active Directory et non pas par des rôles de gestion attribués au groupe de rôles Gestion de l’organisation :

  - Exécution de DomainPrep et ForestPrep à l’aide de Setup.exe

  - Déployer des serveurs supplémentaires dans l’organisation

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
<td><p><a href="active-directory-permissions-role-exchange-2013-help.md">Rôle des autorisations Active Directory</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="address-lists-role-exchange-2013-help.md">Rôle des listes d’adresses</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="applicationimpersonation-role-exchange-2013-help.md">Rôle ApplicationImpersonation</a></p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>None</code></p></td>
<td><p><code>None</code></p></td>
</tr>
<tr class="even">
<td><p><a href="archiveapplication-role-exchange-2013-help.md">Rôle ArchiveApplication</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="audit-logs-role-exchange-2013-help.md">Rôle Journaux d’audit</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="cmdlet-extension-agents-role-exchange-2013-help.md">Rôle des agents d’extension de cmdlet</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="data-loss-prevention-role-exchange-2013-help.md">Rôle de protection contre la perte de données</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="database-availability-groups-role-exchange-2013-help.md">Rôle des groupes de disponibilité de base de données</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="database-copies-role-exchange-2013-help.md">Rôle des copies de base de données</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="databases-role-exchange-2013-help.md">Rôle des bases de données</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="disaster-recovery-role-exchange-2013-help.md">Rôle de récupération d’urgence</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="distribution-groups-role-exchange-2013-help.md">Rôle des groupes de distribution</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="edge-subscriptions-role-exchange-2013-help.md">Rôle des abonnements Edge</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="e-mail-address-policies-role-exchange-2013-help.md">Rôle des stratégies d’adresses de messagerie</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="exchange-connectors-role-exchange-2013-help.md">Rôle des connecteurs Exchange</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="exchange-server-certificates-role-exchange-2013-help.md">Rôle des certificats d’Exchange Server</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="exchange-servers-role-exchange-2013-help.md">Rôle des serveurs Exchange</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="exchange-virtual-directories-role-exchange-2013-help.md">Rôle des répertoires virtuels Exchange</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="federated-sharing-role-exchange-2013-help.md">Rôle de partage fédéré</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="information-rights-management-role-exchange-2013-help.md">Rôle de gestion des droits relatifs à l’information</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="journaling-role-exchange-2013-help.md">Rôle de journalisation</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="legal-hold-role-exchange-2013-help.md">Rôle de conservation légale</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>None</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="legalholdapplication-role-exchange-2013-help.md">Rôle LegalHoldApplication</a></p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="mail-enabled-public-folders-role-exchange-2013-help.md">Rôle des dossiers publics à extension messagerie</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="mail-recipient-creation-role-exchange-2013-help.md">Rôle Création de destinataires de message</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="mail-recipients-role-exchange-2013-help.md">Rôle des destinataires de messagerie</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="mail-tips-role-exchange-2013-help.md">Rôle des conseils de messagerie</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="mailbox-import-export-role-exchange-2013-help.md">Rôle d’importation et d’exportation de boîtes aux lettres</a></p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="mailbox-search-role-exchange-2013-help.md">Rôle de recherche de boîte aux lettres</a></p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>None</code></p></td>
<td><p><code>None</code></p></td>
</tr>
<tr class="even">
<td><p><a href="mailboxsearchapplication-role-exchange-2013-help.md">Rôle MailboxSearchApplication</a></p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="message-tracking-role-exchange-2013-help.md">Rôle de suivi des messages</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="migration-role-exchange-2013-help.md">Rôle de migration</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="monitoring-role-exchange-2013-help.md">Rôle d’analyse</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="move-mailboxes-role-exchange-2013-help.md">Rôle Déplacer des boîtes aux lettres</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="officeextensionapplication-role-exchange-2013-help.md">Rôle OfficeExtensionApplication</a></p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="organization-client-access-role-exchange-2013-help.md">Rôle d’accès au client de l’organisation</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="organization-configuration-role-exchange-2013-help.md">Rôle de configuration de l’organisation</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="organization-transport-settings-role-exchange-2013-help.md">Rôle des paramètres de transport de l’organisation</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="pop3-and-imap4-protocols-role-exchange-2013-help.md">Rôle des protocoles POP3 et IMAP4</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="public-folders-role-exchange-2013-help.md">Rôle Dossiers publics</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="receive-connectors-role-exchange-2013-help.md">Rôle des connecteurs de réception</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="recipient-policies-role-exchange-2013-help.md">Rôle des stratégies de destinataire</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="remote-and-accepted-domains-role-exchange-2013-help.md">Rôle des domaines acceptés et distants</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="reset-password-role-exchange-2013-help.md">Rôle de réinitialisation de mot de passe</a></p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="retention-management-role-exchange-2013-help.md">Rôle de gestion de la rétention</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="role-management-role-exchange-2013-help.md">Rôle de gestion des rôles</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="security-group-creation-and-membership-role-exchange-2013-help.md">Création du groupe de sécurité et rôle de membre</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="send-connectors-role-exchange-2013-help.md">Rôle Connecteurs d’envoi</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="support-diagnostics-role-exchange-2013-help.md">Prise en charge du rôle de diagnostics</a></p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="teammailboxlifecycleapplication-role-exchange-2013-help.md">Rôle TeamMailboxLifecycleApplication</a></p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="transport-agents-role-exchange-2013-help.md">Rôle des agents de transport</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="transport-hygiene-role-exchange-2013-help.md">Rôle d’hygiène de transport</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="transport-queues-role-exchange-2013-help.md">Rôle des files d’attente de transport</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="transport-rules-role-exchange-2013-help.md">Rôle des règles de transport</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="um-mailboxes-role-exchange-2013-help.md">Rôle des boîtes aux lettres de messagerie unifiée</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="um-prompts-role-exchange-2013-help.md">Rôle Messages de messagerie unifiée</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="unscoped-role-management-role-exchange-2013-help.md">Rôle de gestion de rôle non délimité</a></p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="unified-messaging-role-exchange-2013-help.md">Rôle de messagerie unifiée</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="userapplication-role-exchange-2013-help.md">Rôle UserApplication</a></p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="user-options-role-exchange-2013-help.md">Rôle des options de l’utilisateur</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="view-only-audit-logs-role-exchange-2013-help.md">Rôle Journaux d’audit en affichage seul</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>None</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>None</code></p></td>
</tr>
<tr class="even">
<td><p><a href="view-only-configuration-role-exchange-2013-help.md">Rôle de configuration en affichage seul</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>None</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>None</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="view-only-recipients-role-exchange-2013-help.md">Rôle Destinataires en affichage uniquement</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>None</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>None</code></p></td>
</tr>
<tr class="even">
<td><p><a href="workloadmanagement-role-exchange-2013-help.md">Rôle WorkloadManagement</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="my-custom-apps-role-exchange-2013-help.md">Rôle My Custom Apps</a></p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="my-marketplace-apps-role-exchange-2013-help.md">Rôle My Marketplace Apps</a></p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="mybaseoptions-role-exchange-2013-help.md">Rôle MyBaseOptions</a></p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="mycontactinformation-role-exchange-2013-help.md">Rôle MyContactInformation</a></p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="mydiagnostics-role-exchange-2013-help.md">Rôle MyDiagnostics</a></p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="mydistributiongroupmembership-role-exchange-2013-help.md">Rôle MyDistributionGroupMembership</a></p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p><code>MyGAL</code></p></td>
<td><p><code>MyGAL</code></p></td>
<td><p><code>None</code></p></td>
<td><p><code>None</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="mydistributiongroups-role-exchange-2013-help.md">Rôle MyDistributionGroups</a></p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p><code>MyGAL</code></p></td>
<td><p><code>MyDistributionGroups</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>None</code></p></td>
</tr>
<tr class="even">
<td><p><a href="myprofileinformation-role-exchange-2013-help.md">Rôle MyProfileInformation</a></p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="myretentionpolicies-role-exchange-2013-help.md">Rôle MyRetentionPolicies</a></p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="myteammailboxes-role-exchange-2013-help.md">Rôle MyTeamMailboxes</a></p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="mytextmessaging-role-exchange-2013-help.md">Rôle MyTextMessaging</a></p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="myvoicemail-role-exchange-2013-help.md">Rôle MyVoiceMail</a></p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
</tbody>
</table>

