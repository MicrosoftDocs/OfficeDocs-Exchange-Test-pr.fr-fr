---
title: 'Présentation des groupes de rôles de gestion: Exchange 2013 Help'
TOCTitle: Présentation des groupes de rôles de gestion
ms:assetid: 2a92e06c-523e-4fd4-a937-152562b7741d
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dd638105(v=EXCHG.150)
ms:contentKeyID: 50477722
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Présentation des groupes de rôles de gestion

 

_**Sapplique à :** Exchange Online, Exchange Server 2013_

_**Dernière rubrique modifiée :** 2015-03-09_

Un *groupe de rôles de gestion* est un groupe de sécurité universel utilisé dans le modèle d’autorisations de contrôle d’accès basé sur les rôles (RBAC) dans Microsoft Exchange Server 2013. Un groupe de rôles de gestion simplifie l’attribution des rôles de gestion à un groupe d’utilisateurs. Le même ensemble de rôles est attribué à tous les membres d’un groupe de rôles. Des rôles administrateurs et spécialistes sont attribués aux groupes de rôles. Ils définissent les principales tâches administratives dans Exchange 2013 comme la gestion de l’organisation, la gestion des destinataires et d’autres tâches. Les groupes de rôles vous permettent d’attribuer plus facilement un plus grand ensemble d’autorisations à un groupe d’administrateurs et d’utilisateurs spécialistes.

> [!NOTE]  
> Cette rubrique traite de la fonctionnalité RBAC avancée. Si vous souhaitez gérer des autorisations Exchange 2013 de base, comme l’utilisation du centre d’administration Exchange pour ajouter et supprimer des membres dans les groupes de rôles, créer et modifier des groupes de rôles ou créer et modifier des stratégies d’attribution de rôles, consultez la rubrique <a href="permissions-exchange-2013-help.md">Autorisations</a>.


**Table des matières**

Couches des groupes de rôles

Gestion du groupe de rôles

Groupes de rôles intégrés

Groupes de rôles liés

Délégation de groupe de rôles

Appartenance au groupe de rôles

Flux de travail de création de groupe de rôles

> [!NOTE]  
> Si vous souhaitez attribuer des autorisations à des utilisateurs pour qu’ils gèrent leurs propres groupes de distribution ou boîtes aux lettres, consultez la rubrique <a href="understanding-management-role-assignment-policies-exchange-2013-help.md">Présentation des stratégies d’attribution de rôle de gestion</a>.


## Couches des groupes de rôles

Voici les couches qui constituent le modèle de groupe de rôles :

  - **Membre d’un groupe de rôles**   Un *membre d’un groupe de rôles* est une boîte aux lettres, un groupe de sécurité universel ou un autre groupe de rôles qui peut être ajouté en tant que membre d’un groupe de rôles. Lorsqu’une boîte aux lettres, un groupe de sécurité universel ou un autre groupe de rôles est ajouté en tant que membre d’un groupe de rôles, les attributions qui ont été effectuées entre les rôles de gestion et un groupe de rôles sont appliquées au nouveau membre. Cette action permet d’accorder au nouveau membre toutes les autorisations fournies par les rôles de gestion.

  - **Groupe de rôles de gestion**   Le *groupe de rôles de gestion* est un groupe de sécurité universel spécial qui comprend des boîtes aux lettres, des groupes de sécurité universels et d’autres groupes de rôles appartenant à ce groupe de rôles. C’est là que vous ajoutez et supprimez des membres et c’est aussi là où les rôles de gestion sont attribués. L’association de tous les rôles sur un groupe de rôles définit tout ce que les membres ajoutés à un groupe de rôles peuvent gérer dans l’organisation Exchange.

  - **Attribution d’un rôle de gestion**   Une *attribution de rôle de gestion* représente le lien entre un rôle de gestion et un groupe de rôles. L’attribution d’un rôle de gestion à un groupe de rôles permet aux membres du groupe d’utiliser des cmdlets et des paramètres définis dans le rôle de gestion. Les attributions de rôles peuvent utiliser des étendues de gestion pour contrôler les endroits où l’attribution peut être utilisée. Pour plus d’informations, voir [Présentation des attributions de rôles de gestion](understanding-management-role-assignments-exchange-2013-help.md).

  - **Étendue de rôle de gestion**   Une *étendue de rôle de gestion* représente l’étendue de l’influence ou de l’impact sur une attribution de rôle. Quand un rôle avec une étendue est attribué à un groupe de rôles, l’étendue de gestion vise spécifiquement les objets que l’attribution est autorisée à gérer. L’attribution et son étendue sont ensuite accordées aux membres du groupe de rôles, qui limite ce que peuvent gérer ces membres. Une étendue peut être constituée de listes de serveurs ou de bases de données, d’unités d’organisation ou de filtres sur des objets serveur, base de données ou destinataire. Pour plus d’informations, voir [Présentation des portées du rôle de gestion](understanding-management-role-scopes-exchange-2013-help.md).

  - **Rôle de gestion**   Un *rôle de gestion* est un conteneur pour un groupe d’entrées de rôles de gestion. Les rôles sont utilisés pour définir les tâches spécifiques que les membres d’un groupe de rôles auxquels le rôle a été attribué peuvent effectuer. Pour plus d’informations, voir [Présentation des rôles de gestion](understanding-management-roles-exchange-2013-help.md).

  - **Entrées de rôle de gestion**   Les *entrées de rôle de gestion* sont les entrées individuelles d’un rôle de gestion qui donnent accès aux cmdlets, scripts et autres autorisations spéciales permettant d’accéder à l’exécution d’une tâche spécifique. Le plus souvent, les entrées de rôle sont constituées d’un script ou d’une cmdlet unique et des paramètres accessibles par le rôle de gestion et par conséquent, par le groupe de rôles auquel le rôle est attribué.

La figure suivante affiche chacune des couches du groupe de rôles dans la liste précédente et la manière dont les couches sont associées.

**Couches de groupes de rôles de gestion**

![Couches de groupes de rôles de gestion](images/Dd638105.a98c237c-7bdb-434b-8c98-22509e46cccf(EXCHG.150).gif "Couches de groupes de rôles de gestion")

Pour plus d’informations sur le contrôle d’accès basé sur un rôle, consultez la rubrique [Présentation du contrôle d'accès basé sur un rôle](understanding-role-based-access-control-exchange-2013-help.md).

Retour au début

## Gestion du groupe de rôles

Lorsque vous créez un groupe de rôles, vous créez le groupe universel de sécurité qui contient les membres du groupe de rôles et vous créez les attributions entre le groupe de rôles et les rôles de gestion que vous spécifiez. D’autre part, vous pouvez éventuellement spécifier une étendue de gestion à appliquer aux attributions de rôles et vous pouvez ajouter les boîtes aux lettres que vous désirez faire appartenir au nouveau groupe de rôles.

Une fois le groupe de rôles créé, chaque couche devient un objet indépendant. Le groupe de rôles reste le point central de la jointure de toutes les couches. Toutefois, chaque couche est gérée individuellement. Par exemple, pour modifier l’étendue de gestion que vous avez appliquée au groupe de rôles lors de sa création, vous devez modifier l’étendue sur chaque attribution de rôle individuelle après la création du groupe de rôles. La gestion du modèle de groupe de rôles se fait à l’aide des cmdlets qui gèrent les couches individuelles du modèle de groupe de rôles.

Le tableau suivant répertorie la couche des groupes de rôles et les rubriques relatives à la procédure que vous pouvez utiliser pour gérer chaque couche.

### Rubriques de gestion des groupes de rôles

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Couche du modèle de groupe de rôles</th>
<th>Rubrique de gestion</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Membre du groupe de rôles</p></td>
<td><p><a href="manage-role-group-members-exchange-2013-help.md">Gérer les membres de groupes de rôles</a></p>
<p></p></td>
</tr>
<tr class="even">
<td><p>Groupe de rôles</p></td>
<td><p><a href="manage-role-groups-exchange-2013-help.md">Gérer des groupes de rôles</a></p>
<p></p></td>
</tr>
<tr class="odd">
<td><p>Rôles de gestion et attributions</p></td>
<td><p><a href="manage-role-groups-exchange-2013-help.md">Gérer des groupes de rôles</a></p></td>
</tr>
<tr class="even">
<td><p>Entrées de rôles de gestion</p></td>
<td><p><a href="add-a-role-entry-to-a-role-exchange-2013-help.md">Ajouter une entrée de rôle à un rôle</a></p>
<p><a href="change-a-role-entry-exchange-2013-help.md">Modifier une entrée de rôle</a></p>
<p><a href="remove-a-role-entry-from-a-role-exchange-2013-help.md">Supprimer une entrée de rôle d'un rôle</a></p>

> [!NOTE]  
> La modification des entrées de rôle de gestion dans les rôles de gestion d’un groupe de rôles est une tâche avancée et elle n’est généralement pas requise dans la plupart des cas. Au lieu de cela, vous pouvez utiliser un rôle de gestion préexistant qui convient à vos besoins. Pour plus d’informations, voir <a href="built-in-role-groups-exchange-2013-help.md">Groupes de rôles intégrés</a>.

</td>
</tr>
</tbody>
</table>


Retour au début

## Groupes de rôles intégrés

Les groupes de rôles intégrés sont des rôles fournis avec Exchange 2013. Ils vous fournissent un ensemble de groupes de rôles que vous pouvez utiliser pour donner différents niveaux d’autorisations administratives à des groupes d’utilisateurs. Vous pouvez ajouter des utilisateurs à tous les groupes de rôles intégrés ou en supprimer. Vous pouvez aussi ajouter des attributions de rôles à la majorité des groupes de rôles intégrés ou en supprimer. Les seules exceptions sont les suivantes :

  - Vous ne pouvez pas supprimer d’attributions de rôle de délégation du groupe de rôles Gestion de l’organisation.

  - Vous ne pouvez pas supprimer le rôle de gestion des rôles du groupe de rôles Gestion de l’organisation.

Le tableau suivant répertorie tous les groupes de rôles intégrés inclus dans Exchange 2013. Pour plus d’informations sur les groupes de rôles intégrés, consultez la rubrique [Groupes de rôles intégrés](built-in-role-groups-exchange-2013-help.md).

### Groupes de rôles intégrés

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Groupe de rôles</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p></td>
<td><p>Les administrateurs membres du groupe de rôles Gestion de l’organisation disposent d’un accès administratif à toute l’organisation Exchange 2013 et peuvent réaliser presque n’importe quelle tâche relative à un objet Exchange 2013, avec quelques exceptions. Par défaut, les membres de ce groupe de rôles ne peuvent pas réaliser de recherches de boîtes aux lettres ni faire de gestion de rôles de gestion de la direction supérieure non étendus.</p></td>
</tr>
<tr class="even">
<td><p><a href="view-only-organization-management-exchange-2013-help.md">Gestion de l’organisation en affichage seul</a></p></td>
<td><p>Les administrateurs membres du groupe de rôles Afficher uniquement la gestion de l’organisation peuvent afficher les propriétés de n’importe quel objet de l’organisation Exchange.</p></td>
</tr>
<tr class="odd">
<td><p><a href="recipient-management-exchange-2013-help.md">Gestion des destinataires</a></p></td>
<td><p>Les administrateurs membres du groupe de rôles Gestion des destinataires disposent d’un accès administratif pour créer ou modifier des destinataires Exchange 2013 au sein de l’organisation Exchange 2013.</p></td>
</tr>
<tr class="even">
<td><p><a href="um-management-exchange-2013-help.md">Gestion de messagerie unifiée</a></p></td>
<td><p>Les administrateurs qui sont membres du groupe de rôles Gestion de la messagerie unifiée peuvent gérer des fonctionnalités dans l’organisation Exchange comme la configuration du service de messagerie unifiée, les propriétés de messagerie unifiée des boîtes aux lettres, les invites de messagerie unifiée et la configuration du standard automatique de messagerie unifiée.</p></td>
</tr>
<tr class="odd">
<td><p><a href="discovery-management-exchange-2013-help.md">Gestion de la détection</a></p></td>
<td><p>Les administrateurs ou les utilisateurs qui sont membres du groupe de rôles Gestion de la découverte peuvent effectuer des recherches de boîtes aux lettres dans l’organisation Exchange pour des données qui correspondent aux critères spécifiques et peuvent également configurer des suspensions pour litige de boîtes aux lettres.</p></td>
</tr>
<tr class="even">
<td><p><a href="records-management-exchange-2013-help.md">Gestion des enregistrements</a></p></td>
<td><p>Les utilisateurs membres du groupe de rôles Gestion des enregistrements peuvent configurer les fonctionnalités de conformité, comme, entre autres, les balises de stratégie de rétention, les classifications de message et les règles de transport.</p></td>
</tr>
<tr class="odd">
<td><p><a href="server-management-exchange-2013-help.md">Gestion du serveur</a></p></td>
<td><p>Les administrateurs membres de ce groupe de rôles peuvent se charger de la configuration propre au serveur pour les fonctionnalités de transport, d’accès au client et de boîte aux lettres, telles que les copies de bases de données, les certificats, les files d’attente de transport, les connecteurs d’envoi, les répertoires virtuels et les protocoles d’accès au client.</p></td>
</tr>
<tr class="even">
<td><p><a href="help-desk-exchange-2013-help.md">Support technique</a></p></td>
<td><p>Les utilisateurs membres du groupe de rôles de support technique peuvent assurer une gestion limitée des destinataires Exchange 2013.</p></td>
</tr>
<tr class="odd">
<td><p><a href="hygiene-management-exchange-2013-help.md">Gestion de l’hygiène</a></p></td>
<td><p>Les utilisateurs membres du groupe de rôles Gestion de l’hygiène peuvent configurer les fonctionnalités anti-spam et d’anti-programme malveillant d’Exchange 2013. Les programmes tiers intégrés à Exchange 2013 peuvent ajouter des comptes de service à ce groupe de rôles afin de permettre à ces programmes d’accéder aux cmdlets requises pour extraire et configurer Exchange.</p></td>
</tr>
<tr class="even">
<td><p><a href="compliance-management-exchange-2013-help.md">Gestion de la conformité</a></p></td>
<td><p>Les utilisateurs membres du groupe de rôles Gestion de la conformité peuvent configurer et gérer la configuration de la conformité d’Exchange conformément à leurs stratégies.</p></td>
</tr>
<tr class="odd">
<td><p><a href="public-folder-management-exchange-2013-help.md">Gestion des dossiers publics</a></p></td>
<td><p>Les administrateurs qui sont membres du groupe de rôles de gestion des dossiers publics peuvent gérer des dossiers publics sur des serveurs exécutant Exchange 2013.</p></td>
</tr>
<tr class="even">
<td><p><a href="delegated-setup-exchange-2013-help.md">Installation déléguée</a></p></td>
<td><p>Les administrateurs membres du groupe de rôles Installation déléguée peuvent déployer des serveurs exécutant Exchange 2013 qui ont été précédemment mis en service par un membre du groupe de rôles Gestion de l’organisation.</p></td>
</tr>
</tbody>
</table>


Retour au début

## Groupes de rôles liés

Les groupes de rôles liés sont utilisés dans des organisations qui installent Exchange 2013 dans une forêt de ressources dédiée et placent les utilisateurs dans d’autres forêts étrangères approuvées. Les groupes de rôles liés, comme leur nom le laisse entendre, créent un lien entre un groupe de rôles de la forêt Exchange et un groupe universel de sécurité dans une forêt étrangère. Ils s’avèrent particulièrement utiles lorsque les comptes d’utilisateur AD DS Active Directory (Domain Services) des administrateurs d’Exchange ne résident pas dans la même forêt de ressources qu’Exchange. Les groupes de rôle liés peuvent uniquement être associés à un groupe universel de sécurité étranger. De plus, il n’est pas nécessaire de créer une approbation bidirectionnelle entre la forêt Exchange et la forêt étrangère. La forêt Exchange doit approuver la forêt étrangère mais il n’est pas nécessaire que cette dernière approuve la forêt Exchange.

Pour plus d’informations sur les autorisations dans les topologies à plusieurs forêts, consultez la rubrique [Présentation des autorisations sur plusieurs forêts](understanding-multiple-forest-permissions-exchange-2013-help.md).

Un groupe de rôles lié se compose de deux parties :

  - **Groupe de rôles lié**   Le groupe de rôles lié est un objet conteneur qui associe le groupe universel de sécurité aux attributions de rôles de gestion attribuées au groupe de rôles.

  - **Groupe universel de sécurité étranger**   Le groupe universel de sécurité étranger contient les membres auxquels doivent être accordées les autorisations fournies par le groupe de rôles lié.

Lorsque vous créez un groupe de rôles lié, vous fournissez un contrôleur de domaine dans la forêt étrangère qui contient les utilisateurs pour lesquels vous désirez gérer la forêt Exchange et le groupe universel de sécurité qui contient ces utilisateurs comme membres, le nom du groupe universel de sécurité étranger et les informations de connexion requises pour accéder à la forêt étrangère. Exchange ajoute l’identificateur de sécurité du groupe universel de sécurité au groupe de rôles lié. L’identificateur de sécurité du groupe universel de sécurité étant la seule identification du groupe universel de sécurité étranger, nous vous recommandons vivement de spécifier la forêt étrangère dans le nom du groupe de rôles si vous disposez de plusieurs forêts étrangères.

Un groupe de rôles lié ne contient pas de membres. Tous les membres de ce groupe de rôles sont gérés à l’aide du groupe universel de sécurité étranger. Autrement dit, il est impossible d’utiliser les cmdlets **Update-RoleGroupMember**, **Add-RoleGroupMember** ou **Remove-RoleGroupMember** pour ajouter ou supprimer des membres du groupe de rôles. Lorsque vous ajoutez des membres au groupe universel de sécurité étranger, les autorisations fournies par le groupe de rôles lié leur sont accordées.

Il est impossible de transformer un groupe de rôles standard, qui contient ses propres membres, en groupe de rôles lié et vice-versa. Si vous souhaitez transformer le groupe de rôles d’un groupe de rôles standard en groupe de rôles lié, vous devez créer un nouveau groupe de rôles lié et dupliquer les attributions des rôles de gestion présents sur le groupe de rôle standard sur le groupe de rôles lié. Cela est également le cas pour les groupes de rôles intégrés car il s’agit de groupes de rôles standard. Si vous désirez assurer l’ensemble de la gestion de votre forêt Exchange à partir d’une forêt étrangère, vous devez créer de nouveaux groupes de rôles liés et ajouter les rôles de gestion qui existent sur les groupes de rôles intégrés aux nouveaux groupes de rôles liés. Pour plus d’informations sur cette procédure, consultez la rubrique [Créer des groupes de rôles lié qui reflètent les groupes de rôles intégrés](create-linked-role-groups-that-mirror-built-in-role-groups-exchange-2013-help.md).

Retour au début

## Délégation de groupe de rôles

Par défaut, les membres du groupe de rôles Gestion de l’organisation peuvent ajouter des membres aux groupes de rôles et en supprimer. Toutefois, vous voudrez peut-être permettre aux utilisateurs non membres du groupe de rôles Gestion de l’organisation d’ajouter et de supprimer des membres du groupe de rôles. Si tel est le cas, vous pouvez utiliser la délégation de groupe de rôles.

La délégation de groupe de rôles est contrôlée par la propriété **ManagedBy** sur chaque groupe de rôles. La propriété **ManagedBy** contient une liste d’utilisateurs pouvant ajouter et supprimer des membres de ce groupe de rôles ou modifier la configuration d’un groupe de rôles. Aucune autorisation n’est attribuée aux utilisateurs par le groupe de rôles à moins d’appartenir également au groupe de rôles.

Si la propriété **ManagedBy** est définie sur un groupe de rôles, seuls les utilisateurs qui sont répertoriés comme gestionnaires de groupe de rôles sur cette propriété peuvent modifier un groupe de rôles ou l’appartenance à un groupe de rôles par défaut. Cependant, un paramètre facultatif sur les cmdlets qui modifient les groupes de rôles ou l’appartenance à des groupes de rôles peut supprimer cette restriction. Le commutateur *BypassSecurityGroupManagerCheck* peut être utilisé par des utilisateurs membres du rôle Gestion de l’organisation ou auxquels a été attribué, directement ou indirectement, le rôle de gestion de gestion des rôles. Lorsque ce commutateur est utilisé, la propriété **ManagedBy** est ignorée et l’utilisateur peut modifier le groupe de rôles ou son appartenance au groupe de rôles.

Si la propriété **ManagedBy** n’est pas définie sur un groupe de rôles, seuls les utilisateurs membres du rôle Gestion de l’organisation ou auxquels a été attribué, directement ou indirectement, le rôle de gestion de gestion des rôles peuvent modifier un groupe de rôle ou leur appartenance à un groupe de rôles.

> [!NOTE]  
> Les rôles attribués à un groupe de rôles peuvent être attribués à l’aide des attributions de rôles de délégation. Grâce aux attributions de rôles de délégation, les membres d’un groupe de rôles auquel a été attribué un rôle délégué peuvent attribuer ce rôle à un autre groupe de rôles, stratégie d’attribution, utilisateur ou groupe universel de sécurité. Les membres du groupe de rôles peuvent uniquement attribuer ce rôle et ne peuvent pas déléguer le groupe de rôles, à moins d’être également ajoutés à la propriété <strong>ManagedBy</strong>. Pour plus d’informations sur les attributions des rôles délégués, consultez la rubrique <a href="understanding-management-role-assignments-exchange-2013-help.md">Présentation des attributions de rôles de gestion</a>.


Pour plus d’informations sur la gestion de la délégation des groupes de rôles, consultez la rubrique [Gérer des groupes de rôles](manage-role-groups-exchange-2013-help.md).

Retour au début

## Appartenance au groupe de rôles

Lorsqu’un utilisateur devient membre d’un groupe de rôle, les rôles de gestion attribués au groupe de rôle sont attribués à l’utilisateur. Si un utilisateur est membre de plusieurs groupes de rôles, les rôles de gestion de chaque groupe de rôle sont regroupés et attribués à l’utilisateur. Les utilisateurs, les groupes universels de sécurité et les autres groupes de rôles peuvent être membres de groupes de rôles.

Seuls les utilisateurs membres des groupes de rôles Gestion de l’organisation ou de gestion des rôles et les utilisateurs auxquels la capacité d’ajouter des utilisateurs à des groupes de rôles et d’en supprimer a été déléguée peuvent gérer l’appartenance aux groupes de rôles.

Pour plus d’informations sur la gestion de l’appartenance au groupe de rôles, consultez la rubrique [Gérer les membres de groupes de rôles](manage-role-group-members-exchange-2013-help.md).

## Flux de travail de création de groupe de rôles

Comme mentionné précédemment, un groupe de rôles est constitué de plusieurs couches. Pour vous aider à comprendre ce qui se passe lorsqu’un groupe de rôles est créé, réfléchissez à l’exemple suivant, qui crée un nouveau groupe de rôles.

```powershell
New-RoleGroup -Name "Seattle Recipient Management" -Roles "Mail Recipients", "Distribution Groups", "Move Mailboxes", "UM Mailboxes" -CustomRecipientWriteScope "Seattle Users", -ManagedBy "Brian", "David", "Katie" -Members "Ray", "Jenn", "Maria", "Chris", "Maija", "Carter", "Jenny", "Sam", "Lukas", "Isabel", "Katie"
```

Lorsque la commande précédente est exécutée, voici ce qui se produit :

1.  Un nouvel objet groupe de rôles, qui est un groupe universel de sécurité spécial, appelé Gestion des destinataires de Seattle est créé.

2.  Les boîtes aux lettres de Ray, Jenn, Maria, Chris, Maija, Carter, Jenny, Sam, Lukas, Isabel et Katie sont ajoutées comme membres du groupe de rôles. Ces utilisateurs reçoivent les autorisations fournies par ce groupe de rôles.

3.  Les utilisateurs Brian et David sont ajoutés à la propriété **ManagedBy** du groupe de rôles. Ceux-ci peuvent ajouter des membres au groupe de rôles et en supprimer ; toutefois, aucune autorisation fournie par le groupe de rôles ne leur est attribuée car ils n’en sont pas membres. Katie est également ajoutée à la propriété **ManagedBy** du groupe de rôles. Parce qu’elle est ajoutée à la propriété **ManagedBy** et qu’elle est membre du groupe de rôles, elle peut ajouter des membres au groupe de rôles ou en supprimer. Elle peut également recevoir les autorisations fournies par le groupe de rôles.

4.  Les attributions de rôle de gestion suivantes sont créées. Les attributions de rôle attribuent au groupe de rôles chaque rôle de gestion spécifié dans la commande. L’étendue de gestion Utilisateurs de Seattle est ajoutée à chaque attribution de rôle. Le nom de chaque attribution de rôle est l’association entre le rôle de gestion attribué et le nom du groupe de rôles.
    
      - `Mail Recipients_Seattle Recipient Management`
    
      - `Distribution Groups_Seattle Recipient Management`
    
      - `Move Mailboxes_Seattle Recipient Management`
    
      - `UM Mailboxes_Seattle Recipient Management`

Si vous comparez les résultats de cette commande à la figure des couches de groupes de rôles de gestion précédemment dans cette rubrique, vous pourrez voir l’endroit où chaque étape est liée aux couches du groupe de rôles. Vous pouvez ensuite vous reporter aux rubriques consacrées à la gestion des groupes de rôles de gestion contenues dans « Gestion des groupes de rôles » précédemment dans cette rubrique pour gérer chaque couche de groupe de rôles.

Retour au début

