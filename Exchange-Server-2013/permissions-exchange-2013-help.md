---
title: 'Autorisations: Exchange 2013 Help'
TOCTitle: Autorisations
ms:assetid: d8dd605e-0af1-4e18-9ce6-e51d04e161ba
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dd351175(v=EXCHG.150)
ms:contentKeyID: 50479303
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Autorisations

 

_**Sapplique à :** Exchange Server, Exchange Server 2013_

_**Dernière rubrique modifiée :** 2015-03-09_

Microsoft Exchange Server 2013 comprend un large éventail d’autorisations prédéfinies, basées sur le modèle des autorisations du contrôle d’accès basé sur un rôle (RBAC), que vous pouvez utiliser de manière immédiate pour donner facilement des autorisations à vos administrateurs et utilisateurs. Vous pouvez utiliser les autorisations proposées par Exchange 2013 afin que votre nouvelle organisation soit opérationnelle rapidement.

> [!NOTE]
> Plusieurs fonctionnalités et concepts RBAC ne sont pas abordés dans cette rubrique, car il s'agit de fonctionnalités avancées. Si la fonctionnalité abordée dans cette rubrique ne répond pas à vos besoins et que vous souhaitez personnaliser votre modèle d'autorisations, consultez la rubrique <a href="understanding-role-based-access-control-exchange-2013-help.md">Présentation du contrôle d'accès basé sur un rôle</a>.


Vous recherchez une liste de toutes les rubriques consacrées aux autorisations ? Voir Documentation relative aux autorisations.

**Contenu de cette rubrique**

Autorisations basées sur des rôles

Groupes de rôles et stratégies d'attribution de rôle

Utilisation de groupes de rôles

Utilisation de stratégies d'attribution de rôle

## Autorisations basées sur des rôles

Dans Exchange 2013, les autorisations que vous concédez aux administrateurs et aux utilisateurs sont basées sur des rôles de gestion. Un rôle définit un ensemble de tâches qu'un administrateur ou un utilisateur peuvent réaliser. Par exemple, un rôle de gestion appelé `Mail Recipients` définit les tâches qu'une personne peut réaliser sur un ensemble de boîtes aux lettres, contacts et groupes de distribution. Lorsqu'un rôle est assigné à un administrateur ou à un utilisateur, il obtient les autorisations associées à ce rôle.

Il existe deux types de rôles : les rôles administratifs et les rôles d'utilisateur final :

  - **Rôles administratifs**   Ces rôles comportent des autorisations qu'il est possible d'assigner à des administrateurs ou des utilisateurs spécialistes utilisant des groupes de rôles qui ont une fonction de gestion dans l'organisation Exchange comme des destinataires, des serveurs ou des bases de données.

  - **Rôles d'utilisateur final**   Ces rôles, assignés à l'aide de stratégies d'attribution de rôle, permettent aux utilisateurs de gérer des aspects de leurs propres boîtes aux lettres et groupes de distribution. Les rôles d'utilisateur final commencent par le préfixe `My`.

Les rôles concèdent aux administrateurs et utilisateurs auxquels ils sont attribués des autorisations pour réaliser des tâches en mettant à leur disposition des cmdlets. Du fait que le Centre d'Administration Exchange et l'environnement de ligne de commande Exchange Management Shell utilisent des cmdlets pour gérer Exchange, l'accès à une cmdlet donne à l'administrateur ou à l'utilisateur l'autorisation de réaliser des tâches dans chacune des interfaces de gestion Exchange.

Exchange 2013 comprend environ 86 rôles que vous pouvez utiliser pour accorder des autorisations. Pour obtenir une liste des rôles intégrés à Exchange 2013, consultez la rubrique [Rôles de gestion intégrés](built-in-management-roles-exchange-2013-help.md).

Autorisations basées sur des rôles

## Groupes de rôles et stratégies d'attribution de rôle

Les rôles donnent l'autorisation de réaliser des tâches dans Exchange 2013, mais vous devez pouvoir les attribuer facilement aux administrateurs et aux utilisateurs. Voici ce que vous propose Exchange 2013 :

  - **Groupes de rôles**   Les groupes de rôles vous permettent d'accorder des autorisations à des administrateurs et à des utilisateurs spécialistes.

  - **Stratégies d'attribution de rôle**   Les stratégies d'attribution de rôle vous permettent d'accorder aux utilisateurs finaux les autorisations de modifier les paramètres de leurs propres boîtes aux lettres ou groupes de distribution.

Pour plus d'informations sur les groupes de rôles et les stratégies d'attribution de rôles, consultez les sections suivantes.

## Groupes de rôles

Il faut attribuer au moins un rôle ou plus à chacun des administrateurs gérant Exchange 2013. Il est possible que les administrateurs disposent de plus d'un rôle car leur travail englobe plusieurs facettes de Exchange. Par exemple, un administrateur peut gérer à la fois les destinataires et les serveurs Exchange. Dans ce cas, cet administrateur peut se voir attribuer les rôles `Mail Recipients` et `Exchange Servers`.

De façon à faciliter l'attribution de plusieurs rôles à un administrateur, Exchange 2013 comprend les groupes de rôles. Les groupes de rôles sont des groupes universels de sécurité (USG) spéciaux utilisés par Exchange 2013. Ils peuvent contenir des utilisateurs Active Directory, des groupes universels de sécurité et d'autres groupes de rôles. Lorsqu'un rôle est assigné à un groupe de rôles, les autorisations accordées par ce rôle s'étendent à tous les membres du groupe de rôles. Cela vous permet d'assigner de multiples rôles à de nombreux membres de groupes de rôles à la fois. Les groupes de rôles englobent généralement des domaines de gestion plus larges, comme par exemple la gestion des destinataires. Ils sont uniquement utilisés par les rôles administratifs, non par les rôles d'utilisateur final.

> [!NOTE]
> Il est possible d'attribuer un rôle directement à un utilisateur ou un groupe universel de sécurité sans utiliser de groupe de rôle. Cependant, cette méthode d'attribution de rôle est une procédure avancée qui n'est pas abordée dans cette rubrique. Nous vous recommandons d'utiliser les groupes de rôles pour gérer les autorisations.


La figure suivante montre la relation entre les utilisateurs, les groupes de rôles et les rôles.

**Rôles, groupes de rôles et membres de groupes de rôles**

![Relations des rôles, des groupes de rôles et des membres](images/Dd351175.3fb0b47d-333a-4953-ae38-d710d327bde0(EXCHG.150).gif "Relations des rôles, des groupes de rôles et des membres")

Exchange 2013 comprend plusieurs groupes de rôles intégrés, chacun accordant des autorisations pour gérer des domaines différents de Exchange 2013. Certains groupes de rôles peuvent se chevaucher. Le tableau suivant répertorie chaque groupe de rôles avec une description de son utilisation. Si vous souhaitez voir les rôles attribués à chaque groupe de rôles, cliquez sur le nom du groupe de rôles dans la colonne « Groupe de rôles », puis ouvrez la section « Rôles de gestion attribués à ce groupe de rôles ».

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
<td><p>Les administrateurs membres du groupe de rôles Gestion de l’organisation disposent d'un accès administratif sur toute l'organisation Exchange 2013 et peuvent réaliser pratiquement n'importe quelle tâche relative à un objet Exchange 2013, à quelques exceptions près, comme le rôle <code>Discovery Management</code>.</p>

> [!IMPORTANT]
> Du fait que le groupe de rôles Gestion de l’organisation est un rôle très puissant, seuls des utilisateurs ou des groupes universels de sécurité qui exécutent des tâches administratives au niveau organisationnel peuvent affecter l'intégralité de l'organisation Exchange s'ils sont membres de ce groupe de rôles.

</td>
</tr>
<tr class="even">
<td><p><a href="view-only-organization-management-exchange-2013-help.md">Gestion de l’organisation en affichage seul</a></p></td>
<td><p>Les administrateurs membres du groupe de rôles Afficher uniquement la gestion de l’organisation peuvent afficher les propriétés de n'importe quel objet de l'organisation Exchange.</p></td>
</tr>
<tr class="odd">
<td><p><a href="recipient-management-exchange-2013-help.md">Gestion des destinataires</a></p></td>
<td><p>Les administrateurs membres du groupe de rôles Gestion des destinataires disposent d'un accès administratif pour créer ou modifier des destinataires Exchange 2013 au sein de l'organisation Exchange 2013.</p></td>
</tr>
<tr class="even">
<td><p><a href="um-management-exchange-2013-help.md">Gestion de messagerie unifiée</a></p></td>
<td><p>Les administrateurs membres du groupe de rôles de gestion de messagerie unifiée peuvent gérer des fonctionnalités dans l'organisation Exchange comme la configuration du service de messagerie unifiée, les propriétés de messagerie unifiée des boîtes aux lettres, les invites de messagerie unifiée et la configuration du standard automatique de messagerie unifiée.</p></td>
</tr>
<tr class="odd">
<td><p><a href="help-desk-exchange-2013-help.md">Support technique</a></p></td>
<td><p>Par défaut, le groupe de rôles Support technique permet à ses membres d'afficher et de modifier les options Microsoft OfficeOutlook Web App des utilisateurs de l'organisation. notamment le nom complet, l'adresse et le numéro de téléphone de l'utilisateur. les options non disponibles dans Outlook Web App, par exemple, les options permettant de modifier la taille d'une boîte aux lettres ou de configurer la base de données de boîtes aux lettres dans laquelle une boîte aux lettres se trouve.</p></td>
</tr>
<tr class="even">
<td><p><a href="hygiene-management-exchange-2013-help.md">Gestion de l’hygiène</a></p></td>
<td><p>Les utilisateurs membres du groupe de rôles Gestion de l'hygiène peuvent configurer les fonctionnalités d'antivirus et de blocage du courrier indésirable de Exchange 2013. Les programmes tiers intégrés à Exchange 2013 peuvent ajouter des comptes de service à ce groupe de rôles afin de permettre à ces programmes d'accéder aux cmdlets requises pour extraire et configurer Exchange.</p></td>
</tr>
<tr class="odd">
<td><p><a href="records-management-exchange-2013-help.md">Gestion des enregistrements</a></p></td>
<td><p>Les utilisateurs membres du groupe de rôles Gestion des enregistrements peuvent configurer les fonctionnalités de conformité, comme les balises de stratégie de rétention, les classifications de message et les règles de transport.</p></td>
</tr>
<tr class="even">
<td><p><a href="discovery-management-exchange-2013-help.md">Gestion de la détection</a></p></td>
<td><p>Les administrateurs ou les utilisateurs membres du groupe de rôles Gestion de la découverte peuvent effectuer des recherches de boîtes aux lettres dans l'organisation Exchange pour des données répondant à des critères spécifiques et peuvent également configurer des suspensions pour litige de boîtes aux lettres.</p></td>
</tr>
<tr class="odd">
<td><p><a href="public-folder-management-exchange-2013-help.md">Gestion des dossiers publics</a></p></td>
<td><p>Les administrateurs qui sont membres du groupe de rôles de gestion des dossiers publics peuvent gérer des dossiers publics sur des serveurs exécutant Exchange 2013.</p></td>
</tr>
<tr class="even">
<td><p><a href="server-management-exchange-2013-help.md">Gestion du serveur</a></p></td>
<td><p>Les administrateurs membres du groupe de rôles Gestion du serveur peuvent se charger de la configuration propre au serveur pour les fonctionnalités de transport, de messagerie unifiée, d'accès client et de boîte aux lettres, telles que les copies de bases de données, les certificats, les files d'attente de transport, les connecteurs d'envoi, les répertoires virtuels et les protocoles d'accès client.</p></td>
</tr>
<tr class="odd">
<td><p><a href="delegated-setup-exchange-2013-help.md">Installation déléguée</a></p></td>
<td><p>Les administrateurs membres du groupe de rôles Installation déléguée peuvent déployer des serveurs exécutant Exchange 2013 qui ont été précédemment mis en service par un membre du groupe de rôles Gestion de l’organisation.</p></td>
</tr>
<tr class="even">
<td><p><a href="compliance-management-exchange-2013-help.md">Gestion de la conformité</a></p></td>
<td><p>Les utilisateurs membres du groupe de rôles Gestion de la conformité peuvent configurer et gérer les paramètres de conformité Exchange conformément à la stratégie de leur organisation.</p></td>
</tr>
</tbody>
</table>


Si vous travaillez dans une petite organisation ne comptant que quelques administrateurs, vous souhaiterez peut-être ajouter ces administrateurs au groupe de rôles Gestion de l’organisation uniquement ; il se peut que vous n'ayez jamais besoin d'utiliser les autres groupes de rôles. Si vous travaillez dans une organisation plus grande, il se peut que vos administrateurs s'occupent de tâches spécifiques dans Exchange, comme la gestion des destinataires ou des serveurs. Dans ces cas, vous pouvez ajouter un administrateur au groupe de rôles Gestion des destinataires, et un autre administrateur au groupe de rôles Gestion du serveur. Ces administrateurs peuvent ensuite gérer leurs domaines spécifiques d'Exchange 2013, mais ne disposeront pas d'autorisations pour gérer d'autres domaines en dehors de leurs responsabilités.

Si les groupes de rôles intégrés à Exchange 2013 ne correspondent pas à la fonction de vos administrateurs, il vous est possible de créer des groupes de rôles et d'y ajouter des rôles. Pour plus d'informations, consultez la section Utilisation de groupes de rôles plus loin dans cette rubrique.

Autorisations basées sur des rôles

## Stratégies d'attribution de rôle

Exchange 2013 propose des stratégies d'attribution de rôle de façon à vous permettre de contrôler les paramètres que vos utilisateurs peuvent configurer dans leurs propres boîtes aux lettres et groupes de distribution. Ces paramètres comprennent leur nom complet, coordonnées, paramètres de messagerie vocale et appartenance au groupe de distribution.

Votre organisation Exchange 2013 peut disposer de multiples stratégies d'attribution de rôle, offrant différents niveaux d'autorisations pour les différents types d'utilisateurs de vos organisations. Certains utilisateurs sont autorisés à modifier leur adresse ou à créer des groupes de distribution, tandis que d'autres non, en fonction de la stratégie d'attribution de rôle associée à leur boîte aux lettres. Les stratégies d'attribution de rôle sont ajoutées directement aux boîtes aux lettres, et chaque boîte aux lettres ne peut être associée qu'à une stratégie d'attribution de rôle à la fois.

Parmi les stratégies d'attribution de rôle de votre organisation, une est marquée comme la stratégie par défaut. La stratégie d'attribution de rôle par défaut est associée à de nouvelles boîtes aux lettres auxquelles aucune stratégie d'attribution de rôle spécifique n'a été attribuée lors de leur création. La stratégie d'attribution de rôle par défaut doit contenir les autorisations s'appliquant à la majorité de vos boîtes aux lettres.

Les autorisations sont ajoutées aux stratégies d'attribution de rôle à l'aide de rôles d'utilisateur final. Les rôles d'utilisateur final commencent par `My` et accordent les autorisations aux utilisateurs pour gérer leurs propres boîtes aux lettres et groupes de distribution. Ils ne peuvent pas être utilisés pour gérer une autre boîte aux lettres. Seuls les rôles d'utilisateur final peuvent être attribués aux stratégies d'attribution de rôle.

Lorsqu'un rôle d'utilisateur final est attribué à une stratégie d'attribution de rôle, toutes les boîtes aux lettres associées à cette stratégie d'attribution de rôle reçoivent les autorisations accordées à ce rôle. Cela vous permet d'ajouter ou de supprimer des autorisations à des ensembles d'utilisateurs sans devoir configurer de boîtes aux lettres individuelles. La figure suivante présente les éléments suivants :

  - Les rôles d'utilisateur final peuvent être attribués aux stratégies d'attribution de rôle. Les stratégies d'attribution de rôle peuvent partager les mêmes rôles d'utilisateur final.

  - Les stratégies d'attribution de rôle sont associées à des boîtes aux lettres. Chaque boîte aux lettres ne peut être associée qu'à une seule stratégie d'attribution de rôle.

  - Lorsqu'une boîte aux lettres est associée à une stratégie d'attribution de rôle, les rôles d'utilisateur final s'appliquent à cette boîte aux lettres. Les autorisations accordées par les rôles sont accordées à l'utilisateur de la boîte aux lettres.

**Rôles, stratégies d'attribution de rôle et boîtes aux lettres**

![Rôle, stratégie d’attribution de rôle, relation de boîte aux lettres](images/Dd351175.82e07b3d-da59-465b-b349-e0bfde369ace(EXCHG.150).gif "Rôle, stratégie d’attribution de rôle, relation de boîte aux lettres")

La stratégie d'attribution de rôle Stratégie d'attribution de rôle par défaut est incluse dans Exchange 2013. Comme son nom l'indique, c'est la stratégie d'attribution de rôle par défaut. Si vous souhaitez modifier les autorisations accordées par cette stratégie d'attribution de rôle, ou bien si vous souhaitez créer des stratégies d'attribution de rôle, consultez la section Utilisation de stratégies d'attribution de rôle plus loin dans cette rubrique.

## Utilisation de groupes de rôles

Pour gérer vos autorisations à l'aide de groupes de rôles dans Exchange 2013, nous vous recommandons d'utiliser le Centre d'administration Exchange. Lorsque vous utilisez le Centre d'administration Exchange pour gérer des groupes de rôles, vous pouvez ajouter et supprimer des rôles et des membres, créer des groupes de rôles et copier des groupes de rôles en quelques clics de souris. Le Centre d'administration Exchange propose des boîtes de dialogue simples pour réaliser ces tâches, comme la boîte de dialogue **Nouveau groupe de rôles** illustrée dans la figure suivante.

**Boîte de dialogue Nouveau groupe de rôles dans le CAE**

![Boîte de dialogue Nouveau groupe de rôle dans le CAE](images/Dd351175.e0577090-73e6-4671-ae98-78a8064fde87(EXCHG.150).jpg "Boîte de dialogue Nouveau groupe de rôle dans le CAE")

Exchange 2013 inclut plusieurs groupes de rôles que sépare les autorisations en domaines d'administration spécifiques. Si ces groupes de rôles existants accordent les autorisations dont ont besoin vos administrateurs pour gérer votre organisation Exchange 2013, il vous suffit d'ajouter vos administrateurs comme membres des groupes de rôles adéquats. Après avoir ajouté des administrateurs à un groupe de rôles, ils peuvent gérer les fonctionnalités associées à ce groupe de rôles. Pour ajouter ou supprimer des membres dans un groupe de rôles, ouvrez le groupe de rôles dans le Centre d'administration Exchange, puis ajoutez ou supprimez des membres dans la liste des membres. Pour obtenir une liste des groupes de rôles intégrés, consultez la rubrique [Groupes de rôles intégrés](built-in-role-groups-exchange-2013-help.md).

> [!IMPORTANT]
> Si un administrateur est membre de plus d'un groupe de rôles, Exchange 2013 accorde à l'administrateur toutes les permissions accordées par les groupes de rôles dont il ou elle est membre.


Si aucun des groupes de rôles compris dans Exchange 2013 ne dispose des autorisations dont vous avez besoin, vous pouvez utiliser le Centre d'administration Exchange pour créer un groupe de rôles et ajouter les rôles possédant les autorisations dont vous avez besoin. Pour votre nouveau groupe de rôles :

1.  Vous lui choisissez un nom.

2.  Vous sélectionnez les rôles que vous voulez ajouter au groupe de rôles.

3.  Vous ajoutez des membres au groupe de rôles.

4.  Vous enregistrez le groupe de rôles.

Après la création de votre groupe de rôles, vous le gérez comme n'importe quel groupe de rôles.

Si un groupe de rôles existant dispose de certaines mais pas de toutes les autorisations nécessaires, vous pouvez le copier et y apporter des modifications pour créer un groupe de rôles. Vous pouvez copier un groupe de rôles existant puis y apporter des modifications sans affecter le groupe de rôles initial. Dans ce processus de copie, vous pouvez ajouter un nouveau nom et une description, ajouter et supprimer des rôles au sein du nouveau groupe de rôles et ajouter de nouveaux membres. Lorsque vous créez ou copiez un groupe de rôles, vous utilisez la même boîte de dialogue que celle illustrée sur la figure précédente.

Les groupes de rôles existants peuvent également être modifiés. Vous pouvez ajouter et supprimer des rôles dans des groupes de rôles existants, et ajouter et supprimer simultanément des membres dans ces derniers, via une boîte de dialogue du Centre d'administration Exchange semblable à celle illustrée dans la figure précédente. En ajoutant et en supprimant des rôles au sein des groupes de rôles, vous activez et désactivez des fonctionnalités administratives pour les membres de ce groupe de rôles. Pour obtenir une liste de rôles que vous pouvez ajouter à un groupe de rôles, consultez la rubrique [Rôles de gestion intégrés](built-in-management-roles-exchange-2013-help.md).

> [!NOTE]
> Bien que vous puissiez modifier les rôles assignés aux groupes de rôles intégrés, nous vous recommandons de copier des groupes de rôles intégrés, de modifier la copie du groupe de rôles, puis d'ajouter des membres à la copie du groupe de rôles.


Autorisations basées sur des rôles

## Utilisation de stratégies d'attribution de rôle

Pour gérer les autorisations que vous accordez aux utilisateurs finaux pour gérer leur propre boîte aux lettres dans Exchange 2013, nous vous recommandons d'utiliser le Centre d'administration Exchange. Lorsque vous utilisez le Centre d'administration Exchange pour gérer les autorisations des utilisateurs finaux, vous pouvez ajouter et supprimer des rôles, et créer des stratégies d'attribution de rôle en quelques clics de souris. Le Centre d'administration Exchange propose des boîtes de dialogue simples pour réaliser ces tâches, comme la boîte de dialogue **Stratégie d'attribution de rôle** illustrée dans la figure suivante.

**Boîte de dialogue Stratégie d'attribution de rôle dans le CAE**

![Boîte de dialogue Stratégie d’attribution de rôle dans le CAE](images/Dd351175.ecdf3cd4-d50e-4014-95f8-1bd5dafacaff(EXCHG.150).jpg "Boîte de dialogue Stratégie d’attribution de rôle dans le CAE")

Exchange 2013 comprend une stratégie d'attribution de rôle appelée Stratégie d'attribution de rôle par défaut. Cette stratégie d'attribution de rôle permet aux utilisateurs dont les boîtes aux lettres y sont associées de :

  - Rejoindre ou quitter des groupes de distribution permettant aux groupes de gérer leur propre appartenance.

  - Visualiser et modifier des paramètres de boîtes aux lettres basiques de leur propre boîte aux lettres, comme les règles de boîte de réception, le comportement du vérificateur d'orthographe, les paramètres relatifs au courrier indésirable et les périphériques Microsoft ActiveSync.

  - Modifiez leurs informations de contact, telles que l'adresse et le numéro de téléphone professionnels, le numéro de téléphone mobile et le numéro de récepteur de radiomessagerie.

  - Créer, modifier ou visualiser les paramètres des messages texte.

  - Visualiser ou modifier les paramètres de la messagerie vocale.

  - Afficher et modifier leurs applications de place de marché.

  - Créer des boîtes aux lettres d'équipe et les connecter aux listes Microsoft SharePoint.

Si vous souhaitez ajouter ou supprimer des autorisations au sein de la stratégie d'attribution de rôle par défaut, ou dans toute autre stratégie d'attribution de rôle, vous pouvez utiliser le Centre d'administration Exchange. La boîte de dialogue que vous utilisez est semblable à celle de la figure précédente. Lorsque vous ouvrez la stratégie d'attribution de rôle dans le Centre d'administration Exchange, activez la case à cocher en regard des rôles que vous souhaitez lui affecter ou désactivez la case à cocher en regard des rôles que vous souhaitez supprimer. La modification que vous apportez à la stratégie d'attribution de rôle s'applique à toutes les boîtes aux lettres qui y sont associées.

Si vous souhaitez attribuer différentes autorisations d'utilisateur final aux différents types d'utilisateurs de votre organisation, vous pouvez créer des stratégies d'attribution de rôle. Lorsque vous créez une stratégie d'attribution de rôle, une boîte de dialogue semblable à celle indiquée dans la figure précédente s'affiche. Vous pouvez spécifier un nouveau nom pour la stratégie d'attribution de rôle, puis sélectionner les rôles que vous voulez attribuer à la stratégie d'attribution de rôle. Après avoir créé une stratégie d'attribution de rôle, vous pouvez l'associer à des boîtes aux lettres à l'aide du CAE.

Si vous souhaitez modifier la stratégie d'attribution de rôle par défaut, il vous faut utiliser l'environnement de ligne de commande Exchange Management Shell. Lorsque vous modifiez la stratégie d'attribution de rôle par défaut, toutes les boîtes aux lettres créées seront associées à la nouvelle stratégie d'attribution de rôle par défaut si aucune stratégie n'a été explicitement indiquée. La stratégie d'attribution de rôle associée aux boîtes aux lettres existantes ne change pas lorsque vous sélectionnez une nouvelle stratégie d'attribution de rôle par défaut.

> [!NOTE]
> Si vous activez la case à cocher pour un rôle contenant des rôles enfants, les cases à cocher de ces derniers sont également activées. Si vous désactivez la case à cocher pour un rôle contenant des rôles enfants, les cases à cocher de ces derniers sont également désactivées.<br />
Pour obtenir des informations détaillées sur les étapes de la création de stratégies d'attribution de rôles, ou apporter des modifications aux stratégies d'attribution de rôles existantes, consultez les rubriques suivantes :
> <ul>
> <li><p><a href="manage-role-assignment-policies-exchange-2013-help.md">Gérer les stratégies d’attribution des rôles</a></p></li>
> <li><p><a href="change-the-assignment-policy-on-a-mailbox-exchange-2013-help.md">Modifier la stratégie d’attribution sur une boîte aux lettres</a></p></li></ul>

Autorisations basées sur des rôles

## Documentation relative aux autorisations

Le tableau suivant contient des liens vers des rubriques qui vous permettront d'en savoir plus sur les autorisations et leur gestion dans Exchange 2013.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Rubrique</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="understanding-role-based-access-control-exchange-2013-help.md">Présentation du contrôle d'accès basé sur un rôle</a></p></td>
<td><p>Découvrez chacun des composants du contrôle d’accès basé sur les rôles (RBAC) et comment créer des modèles d’autorisations avancées si les groupes de rôles et les rôles de gestion ne sont pas suffisants.</p></td>
</tr>
<tr class="even">
<td><p><a href="understanding-multiple-forest-permissions-exchange-2013-help.md">Présentation des autorisations sur plusieurs forêts</a></p></td>
<td><p>Apprenez à implémenter des autorisations RBAC dans les organisations dotées de forêts de comptes et de ressources.</p></td>
</tr>
<tr class="odd">
<td><p><a href="understanding-split-permissions-exchange-2013-help.md">Présentation des autorisations fractionnées</a></p></td>
<td><p>Découvrez comment fractionner Exchange et la gestion des principaux de sécurité à l'aide des autorisations fractionnées RBAC et Active Directory.</p></td>
</tr>
<tr class="even">
<td><p><a href="understanding-permissions-coexistence-with-exchange-2007-and-exchange-2010-exchange-2013-help.md">Présentation de la coexistence des autorisations dans Exchange 2007 et Exchange 2010</a></p></td>
<td><p>Configurez des autorisation pour activer l'administration d'Exchange 2013 dans des organisations Exchange 2007 et Exchange 2010 existantes.</p></td>
</tr>
<tr class="odd">
<td><p><a href="manage-role-groups-exchange-2013-help.md">Gérer des groupes de rôles</a></p></td>
<td><p>Configurez les autorisations pour les administrateurs et les utilisateurs spécialistes d'Exchange à l'aide de groupes de rôles.</p></td>
</tr>
<tr class="even">
<td><p><a href="manage-role-group-members-exchange-2013-help.md">Gérer les membres de groupes de rôles</a></p></td>
<td><p>Ajoutez et supprimez des membres dans des groupes de rôles. En ajoutant et en supprimant des membres dans des groupes de rôles, vous déterminez qui est autorisé à administrer les fonctionnalités Exchange.</p></td>
</tr>
<tr class="odd">
<td><p><a href="manage-linked-role-groups-exchange-2013-help.md">Gérer des groupes de rôles liés</a></p></td>
<td><p>Configurez les autorisations pour les administrateurs et les utilisateurs spécialistes d'Exchange dans les déploiements Exchange à forêts multiples.</p></td>
</tr>
<tr class="even">
<td><p><a href="manage-role-assignment-policies-exchange-2013-help.md">Gérer les stratégies d’attribution des rôles</a></p></td>
<td><p>Configurez les fonctionnalités auxquelles les utilisateurs finaux ont accès sur leurs boîtes aux lettres à l'aide de stratégies d'attribution de rôle.</p></td>
</tr>
<tr class="odd">
<td><p><a href="change-the-assignment-policy-on-a-mailbox-exchange-2013-help.md">Modifier la stratégie d’attribution sur une boîte aux lettres</a></p></td>
<td><p>Configurez la stratégie d'attribution de rôle qui doit être appliquée à une ou plusieurs boîtes aux lettres.</p></td>
</tr>
<tr class="even">
<td><p><a href="create-linked-role-groups-that-mirror-built-in-role-groups-exchange-2013-help.md">Créer des groupes de rôles lié qui reflètent les groupes de rôles intégrés</a></p></td>
<td><p>Recréez les groupes de rôles intégrés sous forme de groupes de rôles liés dans les déploiements Exchange à forêts multiples.</p></td>
</tr>
<tr class="odd">
<td><p><a href="view-effective-permissions-exchange-2013-help.md">Afficher les autorisations effectives</a></p></td>
<td><p>Consultez la liste des utilisateurs disposant d'autorisations pour administrer les fonctionnalités Exchange.</p></td>
</tr>
<tr class="even">
<td><p><a href="feature-permissions-exchange-2013-help.md">Autorisations des fonctionnalités</a></p></td>
<td><p>Obtenez des informations détaillées plus sur les autorisations requises pour gérer les fonctionnalités et les services Exchange.</p></td>
</tr>
<tr class="odd">
<td><p><a href="advanced-permissions-exchange-2013-help.md">Autorisations avancées</a></p></td>
<td><p>Utilisez les fonctionnalités RBAC avancées pour créer des modèles d'autorisations hautement personnalisés répondant aux besoins de n'importe quelle organisation.</p></td>
</tr>
</tbody>
</table>

