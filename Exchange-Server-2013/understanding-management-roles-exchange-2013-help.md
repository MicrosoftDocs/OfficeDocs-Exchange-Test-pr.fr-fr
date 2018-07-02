---
title: 'Présentation des rôles de gestion: Exchange 2013 Help'
TOCTitle: Présentation des rôles de gestion
ms:assetid: 887b0a64-84b1-4b8c-9547-e456ea6f5dbd
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dd298116(v=EXCHG.150)
ms:contentKeyID: 50478628
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Présentation des rôles de gestion

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2015-04-07_

Les rôles de gestion font partie du modèle d'autorisations de contrôle d'accès basé sur les rôles (Role Based Access Control ou RBAC) utilisé dans Microsoft Exchange Server 2013. Les rôles agissent en tant que regroupement logique de cmdlets qui sont associées pour fournir un accès afin d'afficher ou de modifier la configuration des composants Exchange 2013, comme les boîtes aux lettres, les règles de transport et les destinataires. Les rôles de gestion peuvent ensuite être associés à un niveau supérieur pour former des regroupements plus importants, appelés groupes de rôles de gestion et stratégies d'attribution de rôle de gestion, lesquels permettent de gérer des zones de fonctionnalités et la configuration des destinataires. Les groupes de rôles et les stratégies d'attribution de rôle accordent respectivement des autorisations aux administrateurs et aux utilisateurs finals. Pour plus d'informations sur les groupes de rôles de gestion et les stratégies d'attribution de rôle de gestion, consultez la rubrique [Présentation du contrôle d'accès basé sur un rôle](understanding-role-based-access-control-exchange-2013-help.md).

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


**Table des matières**

Rôles de gestion intégrés

Rôles de gestion de niveau supérieur non délimités

Rôles de gestion personnalisés

Hiérarchie des rôles de gestion

Entrées de rôles de gestion

Entrées de rôle de niveau supérieur non délimité

Types de rôle de gestion

Pour plus d'informations

Les étendues de rôles de gestion et les attributions de rôles de gestion constituent des composants essentiels au fonctionnement des rôles de gestion. Pour plus d'informations sur ces composants, consultez les rubriques suivantes :

  - [Présentation des portées du rôle de gestion](understanding-management-role-scopes-exchange-2013-help.md)

  - [Présentation des attributions de rôles de gestion](understanding-management-role-assignments-exchange-2013-help.md)

Souhaitez-vous rechercher les tâches de gestion liées aux rôles de gestion ? Consultez la rubrique [Autorisations](permissions-exchange-2013-help.md).

## Rôles de gestion intégrés

Exchange 2013 propose de nombreux rôles de gestion intégrés que vous pouvez utiliser pour administrer votre organisation. Chaque rôle comprend les cmdlets et les paramètres dont les utilisateurs ont besoin pour gérer des composants Exchange spécifiques. Voici des exemples de rôles de gestion intégrés :

  - **Destinataires de courrier**   Permet aux administrateurs de gérer les boîtes aux lettres, les contacts et les utilisateurs de courrier électronique.

  - **Règles de transport**   Permet aux administrateurs ou aux utilisateurs spécialistes d'attribuer le rôle permettant de gérer la fonctionnalité des règles de transport.

  - **Groupes de distribution**   Permet aux administrateurs ou aux utilisateurs spécialistes d'attribuer le rôle permettant de gérer les groupes de distribution et leurs membres.

  - **MyPersonalInformation**   Permet aux utilisateurs finaux de modifier leur numéro de téléphone personnel et l'adresse de leur site Web.

Pour obtenir une liste complète des rôles de gestion inclus dans Exchange 2013, consultez [Rôles de gestion intégrés](built-in-management-roles-exchange-2013-help.md).

Vous pouvez associer les rôles intégrés fournis avec Exchange 2013 afin de créer un modèle d'autorisations adapté à votre activité professionnelle. Par exemple, si vous souhaitez que les membres d'un groupe de rôles gèrent les destinataires et les dossiers publics, vous attribuez les rôles Destinataires de messagerie et Dossiers publics au groupe de rôles. Dans la plupart des cas, vous attribuez des rôles aux groupes de rôles ou des stratégies d'attribution de rôles. Vous pouvez également attribuer des rôles de gestion d'attribution directement aux utilisateurs si vous souhaitez contrôler les autorisations à un niveau détaillé. Pour simplifier votre modèle d'autorisations, nous vous conseillons d'utiliser des groupes de rôles et des stratégies d'attribution de rôles plutôt que des attributions directes de rôles d'utilisateur.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Vous pouvez uniquement attribuer des rôles de gestion d'utilisateur final aux stratégies d'attribution de rôles.</td>
</tr>
</tbody>
</table>


Les rôles de gestion intégrés ne sont pas modifiables. Toutefois, vous pouvez créer des rôles de gestion calqués sur les rôles de gestion intégrés, puis attribuer ces nouveaux rôles à des groupes de rôles ou à des stratégies d'attribution de rôles. Vous pouvez ensuite modifier les nouveaux rôles de gestion pour les adapter à vos besoins. Il est très rare d'avoir à réaliser cette tâche, d'ailleurs réservée aux utilisateurs avancés.

Pour plus d'informations sur la création de rôles personnalisés calqués sur les rôles intégrés Exchange, consultez Rôles de gestion personnalisés plus loin dans cette rubrique.

Vous devez attribuer des rôles de gestion pour qu'ils prennent effet. Dans la plupart des cas, vous attribuez des rôles de gestion aux groupes de rôles et aux stratégies d'attribution de rôles. Dans certains cas, vous pouvez également attribuer des rôles directement aux utilisateurs. Mais il est très rare d'avoir à réaliser cette tâche, d'ailleurs réservée aux utilisateurs avancés.

Pour plus d'informations sur l'attribution de rôle de gestion, consultez les rubriques suivantes :

  - [Gérer des groupes de rôles](manage-role-groups-exchange-2013-help.md)

  - [Gérer les stratégies d’attribution des rôles](manage-role-assignment-policies-exchange-2013-help.md)

  - [Ajouter un rôle à un utilisateur ou un groupe de sécurité universel](add-a-role-to-a-user-or-usg-exchange-2013-help.md)

Pour plus d'informations sur les attributions des rôles de gestion, consultez la rubrique [Présentation des attributions de rôles de gestion](understanding-management-role-assignments-exchange-2013-help.md).

Retour au début

## Rôles de gestion de niveau supérieur non délimités

Les rôles de gestion de niveau supérieur non délimités sont un type spécial de rôles de gestion qui vous permettent d'autoriser les utilisateurs RBAC d'accéder à des scripts personnalisés et à des cmdlets non Exchange. Les rôles de gestion standard permettent uniquement d'accéder aux cmdlets Exchange. Si vous devez donner accès à des cmdlets non Exchange à exécuter sur un serveur Exchange, ou si vous souhaitez publier un script exécutable par d'autres utilisateurs, vous devez les ajouter à un rôle non délimité. Ces rôles sont dits de niveau supérieur car si un rôle non délimité est créé sans qu'il soit dérivé d'un rôle parent, il ne dispose d'aucun parent et présente le même niveau que les rôles de gestion intégrés fournis avec Exchange 2013. Pour indiquer que vous souhaitez créer une entrée de rôle de niveau supérieur non délimité, vous devez utiliser le commutateur *UnscopedTopLevel* avec la cmdlet **New-ManagementRole**.

Les rôles non délimités sont appelés ainsi car, contrairement aux rôles de gestion standard, leur étendue ne peut pas être restreinte à une cible spécifique. Les rôles non délimités s'appliquent toujours à toute l'organisation. En conséquence, une personne bénéficiant d'un rôle non délimité peut modifier tous les objets dans l'organisation Exchange 2013. Pour cette raison, veillez à ce que les scripts et les cmdlets rendus disponibles via un rôle non délimité soient parfaitement testés pour être certain de savoir ce qu'ils vont modifier. De même, soyez vigilant lors de l'attribution des rôles non délimités.

Des éléments tels que des groupes de rôles, des rôles de gestion, des utilisateurs et des groupes de sécurité universelle (USG) peuvent être attribués aux rôles non délimités. Ils ne peuvent pas être attribués à des stratégies d'attribution de rôles de gestion.

Même si les cmdlets Exchange ne peuvent pas être ajoutées sous la forme d'entrées de rôle de gestion dans un rôle non délimité, vous pouvez toutefois les inclure à des scripts que vous ajoutez ensuite comme entrées de rôle. Cela vous permet de créer des scripts personnalisés effectuant des tâches Exchange que vous pouvez attribuer aux utilisateurs. Cela s'avère utile, par exemple, lorsqu'un utilisateur doit effectuer une tâche nécessitant des privilèges très élevés et dépassant normalement son niveau administratif, et que la création d'un nouveau rôle de gestion ou d'un groupe de rôles pose certains problèmes. Vous pouvez créer un script réalisant la fonction spécifique, l'ajouter à un rôle non délimité, puis attribuer ce rôle à l'utilisateur. L'utilisateur peur alors réaliser uniquement la fonction spécifique fournie par le script.

Une entrée de rôle que vous ajoutez à un rôle non délimité doit également être désignée comme une entrée de rôle de niveau supérieur non délimité. Pour plus d'informations sur les entrées de rôle de niveau supérieur non délimité, consultez Entrées de rôle de niveau supérieur non délimité plus loin dans ce chapitre.

Le groupe de rôles Gestion de l’organisation, par défaut, ne dispose pas d'autorisations pour créer ou gérer des groupes de rôles non délimités. Cette caractéristique évite ainsi la création ou la modification accidentelle de groupes de rôles non délimités. Le groupe de rôles Gestion de l’organisation peut déléguer le rôle de gestion Gestion de rôles non délimités à lui-même ainsi qu'aux autres bénéficiaires de rôles. Pour plus d'informations sur la création d'un rôle de gestion de niveau supérieur non délimité, consultez la rubrique [Créer un rôle non délimité](create-an-unscoped-role-exchange-2013-help.md).

Retour au début

## Rôles de gestion personnalisés

Vous pouvez créer des rôles de gestion personnalisés calqués sur les rôles intégrés Exchange lorsque les rôles de gestion intégrés ne répondent pas aux besoins de vos utilisateurs. Lorsque vous créez un rôle de gestion personnalisé, le nouveau rôle enfant hérite de toutes les entrées du rôle de gestion du rôle parent. Vous pouvez alors choisir les entrées du rôle de gestion que vous souhaitez conserver dans le rôle de gestion personnalisé, puis supprimer toutes les entrées non désirées.

Les rôles personnalisés deviennent des enfants du rôle utilisé pour créer le rôle. Vous pouvez uniquement utiliser des entrées existant dans le rôle parent avec le nouveau rôle enfant. Pour plus d'informations, consultez les sections suivantes présentées ci-après dans cette rubrique :

  - Hiérarchie des rôles de gestion

  - Entrées de rôles de gestion

La création de rôles de gestion personnalisés passe par plusieurs étapes. Il s'agit d'une tâche avancée que vous serez rarement amené à effectuer. Avant de créer un rôle de gestion personnalisé, assurez-vous qu'aucun des rôles de gestion intégrés ne fournit les autorisations dont vous avez besoin. Pour plus d'informations sur les rôles de gestion intégrés, ou si vous souhaitez créer des rôles de gestion personnalisés, consultez les rubriques suivantes :

  - [Rôles de gestion intégrés](built-in-management-roles-exchange-2013-help.md)

  - [Autorisations avancées](advanced-permissions-exchange-2013-help.md)

Pour plus d'informations sur la création d'un rôle de gestion, consultez la rubrique [Créer un rôle](create-a-role-exchange-2013-help.md).

Retour au début

## Hiérarchie des rôles de gestion

Les rôles de gestion sont régis par une hiérarchie parent - enfant. Les rôles de gestion intégrés, fournis par défaut avec Exchange 2013, occupent le haut de la hiérarchie. Lorsque vous créez un rôle, une copie du rôle parent est générée. Le nouveau rôle est un enfant du rôle que vous avez copié. Vous pouvez alors personnaliser le nouveau rôle pour l'adapter aux besoins des administrateurs ou des utilisateurs auxquels vous souhaitez l'attribuer.

Les rôles personnalisés peuvent être utilisés pour créer d'autres rôles. Lorsque vous créez un rôle à partir d'un rôle personnalisé existant, ce dernier reste un enfant de son rôle parent, mais devient également parent du nouveau rôle. Chaque fois qu'un rôle est copié, le nouveau rôle enfant ne peut contenir que les entrées de rôle présentes dans le rôle parent.

Chaque rôle de gestion bénéficie d'un type de rôle non modifiable. Le type définit le contexte sommaire d'utilisation du rôle. Le type de rôle est copié à partir du rôle parent à la création du rôle enfant.

**Hiérarchie des rôles de gestion**

![Diagramme hiérarchique des rôles de gestion RBAC](images/Dd298116.6851c829-ca8f-40e7-a67c-cc9e85c33953(EXCHG.150).gif "Diagramme hiérarchique des rôles de gestion RBAC")

La figure précédente illustre la relation hiérarchique entre plusieurs rôles de gestion. Les rôles Destinataires de messagerie et Support technique sont des rôles intégrés. Tous les rôles enfants dérivés de ces rôles héritent du type de rôle de chaque rôle intégré. Par exemple, tous les rôles enfants dérivés, directement ou indirectement, du rôle Destinataires de messagerie héritent du type de rôle `MailRecipients`.

Le rôle personnalisé Administrateurs des destinataires Seattle est enfant du rôle intégré Destinataires de messagerie, mais également parent des rôles personnalisés Administrateurs des destinataires Ventes Seattle et Administrateurs des destinataires Section juridique Seattle. Le rôle personnalisé Administrateurs des destinataires Seattle peut uniquement contenir un sous-ensemble de cmdlets qui sont disponibles dans le rôle Destinataires de messagerie. Les rôles enfants du rôle personnalisé Administrateurs des destinataires Seattle peuvent uniquement contenir les cmdlets également présentes dans ce rôle. Par exemple, si une cmdlet existe dans le rôle Destinataires de messagerie, mais qu'elle ne se trouve pas dans le rôle personnalisé Administrateurs des destinataires Seattle, la cmdlet ne peut pas être ajoutée au rôle personnalisé Administrateurs des destinataires Ventes Seattle.

Le modèle de fonctionnement des rôles présentés ci-dessus s'applique à tous les rôles personnalisés. Pour plus d'informations sur la façon dont l'accès aux cmdlets est contrôlé sur les rôles de gestion, consultez Entrées de rôles de gestion plus loin dans cette rubrique.

Retour au début

## Entrées de rôles de gestion

Chaque rôle de gestion, qu’il s’agisse d’un rôle Exchange personnalisé ou non délimité, doit disposer au moins d’une entrée de rôle de gestion. Une entrée se compose d'une seule cmdlet et de ses paramètres, d'un script ou d'une autorisation spéciale que vous souhaitez rendre disponible. Si une cmdlet ou un script ne se présente pas comme une entrée sur un rôle de gestion, cette cmdlet ou ce script n'est pas accessible via le rôle. De même, si un paramètre n'existe pas dans une entrée, le paramètre de cette cmdlet ou de ce script n'est pas accessible via ce rôle.

Exchange 2013 vous permet de gérer des entrées de rôles de gestion d'après les rôles Exchange intégrés de niveau supérieur et les entrées de rôles en fonction des rôles de gestion de niveau supérieur non délimités. Les rôles Exchange intégrés de niveau supérieur peuvent uniquement contenir des entrées de rôles qui sont des cmdlets Exchange 2013. Pour ajouter des scripts personnalisés ou des cmdlets non Exchange pour les mettre à disposition des utilisateurs, vous devez les ajouter sous la forme d'entrées de rôles non délimités dans un rôle de niveau supérieur non délimité. Pour plus d'informations sur les entrées de rôles non délimités, consultez Entrées de rôle de niveau supérieur non délimité plus loin dans cette rubrique.

Toutes les entrées de rôle, qu'il s'agisse d'une entrée de rôle basée sur les cmdlets Exchange ou d'une entrée de rôle non délimité, sont sujettes à des principes communs décrits dans les sections suivantes.

Pour plus d'informations sur la gestion des entrées de rôles, consultez [Les entrées de rôle et les rôles de gestion](management-roles-and-role-entries-exchange-2013-help.md).

## Relation entre les rôles de gestion parents et enfants

Comme indiqué plus haut, une entrée de rôle de gestion (comprenant la cmdlet et ses paramètres) doit se trouver dans le rôle parent immédiat pour permettre son ajout au rôle enfant. Par exemple, si le rôle parent ne dispose d’aucune entrée pour **New-Mailbox**, le rôle enfant ne peut pas hériter de cette cmdlet. En outre, si **Set-Mailbox** se trouve dans le rôle parent mais que le paramètre *Database* a été supprimé de cette entrée, le paramètre *Database* de la cmdlet **Set-Mailbox** ne peut pas être ajouté à l'entrée sur le rôle enfant.

Comme vous ne pouvez pas ajouter des entrées de rôle de gestion aux rôles enfants si les entrées ne figurent pas dans les rôles parents, et comme le rôle est basé sur un type spécifique, vous devez choisir soigneusement le rôle parent à copier lorsque vous souhaitez créer un rôle personnalisé.

Retour au début

## Noms des entrées de rôle de gestion

Les noms des entrées de rôle de gestion sont une combinaison du rôle de gestion auquel ils sont associés et du nom de cmdlet ou du script. Le nom de rôle et la cmdlet ou le script sont séparés par une barre oblique inverse (\\). Par exemple, le nom de l'entrée de rôle correspondant à la cmdlet **Set-Mailbox**, sur le rôle Destinataires de messagerie, est `Mail Recipients\Set-Mailbox`. Si le nom d'une entrée de rôle contient des espaces, placez le nom complet entre guillemets (").

Le caractère générique (\*) peut être utilisé dans le nom d'une entrée de rôle pour renvoyer toutes les entrées de rôle correspondant à votre saisie. Le caractère générique peut être utilisé librement des deux côtés de la barre oblique inverse. Le tableau suivant contient quelques variations sur le mode d'utilisation du caractère générique dans le nom d'une entrée de rôle.

**Nom d'entrée de rôle de gestion contenant des caractères génériques**


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Exemple</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>*\*</code></p></td>
<td><p>Retourne une liste de toutes les entrées de rôle pour tous les rôles.</p></td>
</tr>
<tr class="even">
<td><p><code>*\Set-Mailbox</code></p></td>
<td><p>Retourne une liste de toutes les entrées de rôle contenant la cmdlet <strong>Set-Mailbox</strong>.</p></td>
</tr>
<tr class="odd">
<td><p><code>Mail Recipients\*</code></p></td>
<td><p>Renvoie une liste de toutes les entrées de rôle sur le rôle Destinataires de messagerie.</p></td>
</tr>
<tr class="even">
<td><p><code>Mail Recipients\*Mailbox</code></p></td>
<td><p>Renvoie une liste de toutes les entrées de rôle sur le rôle Destinataires de messagerie qui contiennent des cmdlets se terminant par Mailbox.</p></td>
</tr>
<tr class="odd">
<td><p><code>My*\*Group*</code></p></td>
<td><p>Renvoie une liste de toutes les entrées de rôle dont le nom de cmdlet contient la chaîne Group pour tous les rôles commençant par My.</p></td>
</tr>
</tbody>
</table>


## Entrées de rôle de niveau supérieur non délimité

Les entrées de rôle de niveau supérieur non délimité sont utilisées avec les rôles de gestion de niveau supérieur non délimité pour créer des rôles basés sur des scripts personnalisés ou des cmdlets non Exchange. Chaque entrée de rôle non délimité est associée à un script personnalisé ou à une cmdlet non Exchange. Pour indiquer que vous souhaitez créer une entrée de rôle non délimité sur un rôle non délimité, vous devez spécifier le paramètre *UnscopedTopLevel* sur la cmdlet **Add-ManagementRoleEntry**.

Lorsque vous ajoutez l'entrée de rôle non délimité, vous devez spécifier tous les paramètres pouvant être utilisés avec le script ou la cmdlet non Exchange. Exchange tente de vérifier les paramètres que vous fournissez lors de l'ajout de l'entrée de rôle. Seuls les paramètres que vous ajoutez à l'entrée de rôle lors de sa création seront mis à disposition des utilisateurs affectés au rôle non délimité. Si vous ajoutez des paramètres au script ou à la cmdlet non Exchange, ou si les paramètres sont renommés, vous devez mettre à jour l'entrée de rôle manuellement. Exchange ne vérifie pas si les paramètres d'une entrée de rôle non délimité sont modifiés. Si le paramètre d'une entrée de rôle change dans un script et que vous essayez d'utiliser ce paramètre, la commande échoue.

Les scripts que vous ajoutez à une entrée de rôle non délimité doivent résider dans le répertoire des scripts Exchange 2013 sur tous les serveurs auxquels les administrateurs et les utilisateurs se connectent à l'aide de l'environnement de ligne de commande Exchange Management Shell. Si vous essayez d'ajouter une entrée de rôle non délimité à un script qui n'existe pas dans le répertoire des scripts Exchange 2013 sur le serveur que vous utilisez pour ajouter l'entrée de rôle, une erreur se produit. Par défaut, le répertoire de scripts Exchange 2013 est installé à l’emplacement suivant : C:\\Program Files\\Microsoft\\Exchange Server\\V15\\RemoteScripts.

Les cmdlets non Exchange que vous ajoutez à une entrée de rôle non délimité doivent être installées sur tous les serveurs Exchange 2013 auxquels les administrateurs et les utilisateurs se connectent à l'aide du Shell pour utiliser ces cmdlets. Si vous essayez d'ajouter une entrée de rôle non délimité à une cmdlet Exchange qui n'est pas installée sur le serveur Exchange 2013 que vous utilisez pour ajouter l'entrée de rôle, une erreur se produit. Lorsque vous ajoutez une cmdlet non Exchange, vous devez spécifier le nom du composant logiciel enfichable Windows PowerShell contenant la cmdlet non Exchange.

Pour plus d'informations sur l'ajout d'une entrée de rôle de gestion non délimité, consultez la rubrique [Ajouter une entrée de rôle à un rôle](add-a-role-entry-to-a-role-exchange-2013-help.md).

Retour au début

## Types de rôle de gestion

Les types de rôle de gestion sont le fondement de tous les rôles de gestion. Les types définissent les étendues implicites définies sur tous les rôles de gestion d'un type de rôle donné et permettent également de regrouper les rôles connexes. Tous les rôles de gestion dérivant du rôle de gestion intégré parent disposent du même type de rôle. Consultez la figure relative à la hiérarchie des rôles de gestion plus haut dans cette rubrique pour obtenir une illustration de cette relation. Les types de rôle de gestion représentent également le nombre maximum de cmdlets (et de leurs paramètres) pouvant être ajouté à un rôle associé à un type de rôle.

Les types de rôle de gestion sont répartis en plusieurs catégories :

  - **Administratif ou spécialiste**   Rôles associés à des types de rôle administratif ou spécialiste et disposant d'une portée plus importante au sein de l'organisation Exchange. Les rôles de ce type permettent de réaliser des tâches telles que la gestion des destinataires ou des serveurs, la configuration de l'organisation, l'administration de la conformité, les audits, etc.

  - **Centré sur l'utilisateur**   Rôles associés à un type de rôle centré sur l'utilisateur et dont la portée est étroitement liée à un utilisateur individuel. Les rôles de ce type permettent de réaliser des tâches telles que la configuration des profils utilisateur et autogestion, gestion des groupes de distribution dont les utilisateurs sont propriétaires, etc.
    
    Les noms des rôles associés aux types de rôle centré sur l'utilisateur et des rôles centrés sur l'utilisateur commencent par Ma, Mon ou Mes.

  - **Spécialité**   Rôles associés à des types de rôle de spécialité qui permettent de réaliser des tâches ne correspondant pas aux types de rôle centré sur l'utilisateur ou administratif. Les rôles de ce type permettent de réaliser des tâches telles que l'emprunt d'identité d'application et l'utilisation de scripts ou de cmdlets non Exchange.

Le tableau suivant répertorie tous les types de rôle de gestion administratif présents dans Exchange 2013 et indique si la configuration autorisée par le type de rôle s'applique à l'intégralité de l'organisation Exchange ou uniquement à un serveur individuel. Pour plus d'informations sur chacun des rôles de gestion associés à ces types de rôle, comprenant une description de chaque rôle, les bénéficiaires éventuels des rôles ainsi que d'autres informations, consultez [Rôles de gestion intégrés](built-in-management-roles-exchange-2013-help.md).

**Types de rôle administratif**


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Type de rôle de gestion</th>
<th>Rôle de gestion intégré</th>
<th>Description</th>
<th>Organisation ou serveur</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>ActiveDirectoryPermissions</code></p></td>
<td><p><a href="active-directory-permissions-role-exchange-2013-help.md">Rôle des autorisations Active Directory</a></p></td>
<td><p>Ce type de rôle est associé à des rôles permettant aux administrateurs de configurer les autorisations Active Directory au sein d'une organisation. Certaines fonctionnalités reposant sur les autorisations Active Directory ou sur une liste de contrôle d'accès (ACL) comprennent les connecteurs de réception et d'envoi de transport, ainsi que les autorisations de boîtes aux lettres Envoyer en tant que et Envoyer de la part de.</p>
<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Les autorisations définies directement sur des objets Active Directory risquent de ne pas être appliquées via RBAC.</td>
</tr>
</tbody>
</table>

</td>
<td><p>Organisation</p></td>
</tr>
<tr class="even">
<td><p><code>AddressLists</code></p></td>
<td><p><a href="address-lists-role-exchange-2013-help.md">Rôle des listes d’adresses</a></p></td>
<td><p>Ce type de rôle est associé aux rôles permettant aux administrateurs de gérer les listes d'adresses, les listes d'adresses globales et les listes d'adresses en mode hors connexion au sein d'une organisation.</p></td>
<td><p>Organisation</p></td>
</tr>
<tr class="odd">
<td><p><code>ApplicationImpersonation</code></p></td>
<td><p><a href="applicationimpersonation-role-exchange-2013-help.md">Rôle ApplicationImpersonation</a></p></td>
<td><p>Ce type de rôle est associé aux rôles qui permettent aux applications d'assumer l'identité des utilisateurs dans une organisation pour effectuer des tâches pour leur compte.</p></td>
<td><p>Organisation</p></td>
</tr>
<tr class="even">
<td><p><code>ArchiveApplication</code></p></td>
<td><p><a href="archiveapplication-role-exchange-2013-help.md">Rôle ArchiveApplication</a></p></td>
<td><p>Ce type de rôle est associé à des rôles permettant à des applications partenaires d'archiver des éléments dans des boîtes aux lettres utilisateur d'une organisation.</p></td>
<td><p>Organisation</p></td>
</tr>
<tr class="odd">
<td><p><code>AuditLogs</code></p></td>
<td><p><a href="audit-logs-role-exchange-2013-help.md">Rôle Journaux d’audit</a></p></td>
<td><p>Ce type de rôle est associé à des rôles permettant aux administrateurs de gérer la configuration de l'enregistrement d'audit d'administrateur au sein d'une organisation.</p></td>
<td><p>Organisation</p></td>
</tr>
<tr class="even">
<td><p><code>CmdletExtensionAgents</code></p></td>
<td><p><a href="cmdlet-extension-agents-role-exchange-2013-help.md">Rôle des agents d’extension de cmdlet</a></p></td>
<td><p>Ce type de rôle est associé à des rôles permettant aux administrateurs de gérer les agents d'extension de cmdlets au sein d'une organisation.</p></td>
<td><p>Organisation</p></td>
</tr>
<tr class="odd">
<td><p><code>DataLossPrevention</code></p></td>
<td><p><a href="data-loss-prevention-role-exchange-2013-help.md">Rôle de protection contre la perte de données</a></p></td>
<td><p>Ce type de rôle est associé à des rôles qui créent et gèrent des stratégies de protection contre la perte de données (DLP) et les règles au sein de celles-ci dans une organisation.</p></td>
<td><p>Organisation</p></td>
</tr>
<tr class="even">
<td><p><code>DatabaseAvailabilityGroups</code></p></td>
<td><p><a href="database-availability-groups-role-exchange-2013-help.md">Rôle des groupes de disponibilité de base de données</a></p></td>
<td><p>Ce type de rôle est associé à des rôles permettant aux administrateurs de gérer les groupes de disponibilité de base de données (DAG) au sein d'une organisation. Les administrateurs pour lesquels ce rôle est attribué directement ou indirectement sont les administrateurs au plus haut niveau responsables de la configuration haute disponibilité d'une organisation.</p></td>
<td><p>Organisation</p></td>
</tr>
<tr class="odd">
<td><p><code>DatabaseCopies</code></p></td>
<td><p><a href="database-copies-role-exchange-2013-help.md">Rôle des copies de base de données</a></p></td>
<td><p>Ce type de rôle est associé à des rôles permettant aux administrateurs de gérer les copies de base de données sur des serveurs individuels.</p></td>
<td><p>Serveur</p></td>
</tr>
<tr class="even">
<td><p><code>Databases</code></p></td>
<td><p><a href="databases-role-exchange-2013-help.md">Rôle des bases de données</a></p></td>
<td><p>Ce type de rôle est associé à des rôles permettant aux administrateurs de créer, gérer, monter et démonter des bases de données de boîtes aux lettres sur des serveurs individuels.</p></td>
<td><p>Serveur</p></td>
</tr>
<tr class="odd">
<td><p><code>DisasterRecovery</code></p></td>
<td><p><a href="disaster-recovery-role-exchange-2013-help.md">Rôle de récupération d’urgence</a></p></td>
<td><p>Ce type de rôle est associé à des rôles permettant aux administrateurs de restaurer des boîtes aux lettres et des bases de données de boîtes aux lettres, de créer des bases de données de boîtes aux lettres et d'exécuter des basculements et des commutations pour des groupes de disponibilité de base de données au sein d'une organisation.</p></td>
<td><p>Organisation</p></td>
</tr>
<tr class="even">
<td><p><code>DistributionGroups</code></p></td>
<td><p><a href="distribution-groups-role-exchange-2013-help.md">Rôle des groupes de distribution</a></p></td>
<td><p>Ce type de rôle est associé aux rôles permettant aux administrateurs de créer et de gérer des groupes de distribution et leurs membres au sein d'une organisation.</p></td>
<td><p>Organisation</p></td>
</tr>
<tr class="odd">
<td><p><code>EdgeSubscriptions</code></p></td>
<td><p><a href="edge-subscriptions-role-exchange-2013-help.md">Rôle des abonnements Edge</a></p></td>
<td><p>Ce type de rôle est associé à des rôles permettant aux administrateurs de gérer la synchronisation et l'abonnement Edge entre des serveurs de transport Edge Exchange 2010 et des serveurs de boîtes aux lettres Exchange 2013 au sein d'une organisation.</p></td>
<td><p>Organisation</p></td>
</tr>
<tr class="even">
<td><p><code>EmailAddressPolicies</code></p></td>
<td><p><a href="e-mail-address-policies-role-exchange-2013-help.md">Rôle des stratégies d’adresses de messagerie</a></p></td>
<td><p>Ce type de rôle est associé à des rôles permettant aux administrateurs de gérer des stratégies d'adresse de messagerie au sein d'une organisation.</p></td>
<td><p>Organisation</p></td>
</tr>
<tr class="odd">
<td><p><code>ExchangeConnectors</code></p></td>
<td><p><a href="exchange-connectors-role-exchange-2013-help.md">Rôle des connecteurs Exchange</a></p></td>
<td><p>Ce type de rôle est associé à des rôles qui permettent aux administrateurs de créer, de modifier, d’afficher et de supprimer des connecteurs d’agent de remise.</p></td>
<td><p>Organisation</p></td>
</tr>
<tr class="even">
<td><p><code>ExchangeServerCertificates</code></p></td>
<td><p><a href="exchange-server-certificates-role-exchange-2013-help.md">Rôle des certificats d’Exchange Server</a></p></td>
<td><p>Ce type de rôle est associé à des rôles permettant aux administrateurs de créer, importer, exporter et gérer des certificats de serveur Exchange sur des serveurs individuels.</p></td>
<td><p>Serveur</p></td>
</tr>
<tr class="odd">
<td><p><code>ExchangeServers</code></p></td>
<td><p><a href="exchange-servers-role-exchange-2013-help.md">Rôle des serveurs Exchange</a></p></td>
<td><p>Ce type de rôle est associé à des rôles permettant aux administrateurs de gérer la configuration du serveur Exchange sur des serveurs individuels.</p></td>
<td><p>Serveur</p></td>
</tr>
<tr class="even">
<td><p><code>ExchangeVirtualDirectories</code></p></td>
<td><p><a href="exchange-virtual-directories-role-exchange-2013-help.md">Rôle des répertoires virtuels Exchange</a></p></td>
<td><p>Ce type de rôle est associé à des rôles permettant aux administrateurs de gérer Outlook Web App, Microsoft ActiveSync, le carnet d'adresses en mode hors connexion, le service de découverte automatique, Windows PowerShell et les répertoires virtuels du Centre d'administration Exchange (CAE) sur des serveurs individuels.</p></td>
<td><p>Serveur</p></td>
</tr>
<tr class="odd">
<td><p><code>FederatedSharing</code></p></td>
<td><p><a href="federated-sharing-role-exchange-2013-help.md">Rôle de partage fédéré</a></p></td>
<td><p>Ce type de rôle est associé à des rôles permettant aux administrateurs de gérer le partage entre les forêts et les organisations au sein d'une organisation.</p></td>
<td><p>Organisation</p></td>
</tr>
<tr class="even">
<td><p><code>InformationRightsManagement</code></p></td>
<td><p><a href="information-rights-management-role-exchange-2013-help.md">Rôle de gestion des droits relatifs à l’information</a></p></td>
<td><p>Ce type de rôle est associé aux rôles permettant aux administrateurs de gérer les fonctionnalités de gestion des droits relatifs à l'information d'Exchange au sein d'une organisation.</p></td>
<td><p>Organisation</p></td>
</tr>
<tr class="odd">
<td><p><code>Journaling</code></p></td>
<td><p><a href="journaling-role-exchange-2013-help.md">Rôle de journalisation</a></p></td>
<td><p>Ce type de rôle est associé à des rôles permettant aux administrateurs de gérer la configuration de journalisation au sein d'une organisation.</p></td>
<td><p>Organisation</p></td>
</tr>
<tr class="even">
<td><p><code>LegalHold</code></p></td>
<td><p><a href="legal-hold-role-exchange-2013-help.md">Rôle de conservation légale</a></p></td>
<td><p>Ce type de rôle est associé à des rôles permettant aux administrateurs de configurer les données d'une boîte aux lettres pour déterminer si elles doivent être conservées pour l'arbitrage de litiges au sein d'une organisation.</p></td>
<td><p>Organisation</p></td>
</tr>
<tr class="odd">
<td><p><code>MailboxImportExport</code></p></td>
<td><p><a href="mailbox-import-export-role-exchange-2013-help.md">Rôle d’importation et d’exportation de boîtes aux lettres</a></p></td>
<td><p>Ce type de rôle est associé aux rôles qui permettent aux administrateurs d'importer et d'exporter le contenu d'une boîte aux lettres et d'en supprimer le contenu inutile.</p></td>
<td><p>Organisation</p></td>
</tr>
<tr class="even">
<td><p><code>MailboxSearch</code></p></td>
<td><p><a href="mailbox-search-role-exchange-2013-help.md">Rôle de recherche de boîte aux lettres</a></p></td>
<td><p>Ce type de rôle est associé à des rôles permettant aux administrateurs d'effectuer des recherches dans le contenu d'une ou plusieurs boîtes aux lettres au sein d'une organisation.</p></td>
<td><p>Organisation</p></td>
</tr>
<tr class="odd">
<td><p><code>MailboxSearchApplication</code></p></td>
<td><p><a href="mailboxsearchapplication-role-exchange-2013-help.md">Rôle MailboxSearchApplication</a></p></td>
<td><p>Ce type de rôle est associé à des rôles permettant à des applications partenaires de définir et d'afficher l'état de la suspension légale d'une boîte aux lettres au sein d'une organisation.</p></td>
<td><p>Organisation</p></td>
</tr>
<tr class="even">
<td><p><code>MailEnabledPublicFolders</code></p></td>
<td><p><a href="mail-enabled-public-folders-role-exchange-2013-help.md">Rôle des dossiers publics à extension messagerie</a></p></td>
<td><p>Ce type de rôle est associé à des rôles permettant aux administrateurs de configurer les dossiers publics individuels avec ou sans extension de messagerie dans une organisation.</p>
<p>Ce type de rôle vous permet de gérer uniquement les propriétés de messagerie des dossiers publics. Il ne vous permet pas de gérer les propriétés des dossiers publics qui ne sont pas des propriétés de la messagerie. Pour gérer les propriétés des dossiers publics qui ne sont pas des propriétés de la messagerie, vous devez disposer d'un rôle associé au type de rôle <code>PublicFolders</code>.</p></td>
<td><p>Organisation</p></td>
</tr>
<tr class="odd">
<td><p><code>MailRecipientCreation</code></p></td>
<td><p><a href="mail-recipient-creation-role-exchange-2013-help.md">Rôle Création de destinataires de message</a></p>
<p></p></td>
<td><p>Ce type de rôle est associé à des rôles permettant aux administrateurs de créer des boîtes aux lettres, des utilisateurs de messagerie, des contacts de messagerie, des groupes de distribution et des groupes de distribution dynamiques au sein d'une organisation. Les rôles associés à ce type de rôle peuvent être associés à des rôles associés avec le type de rôle <code>MailRecipients</code> pour permettre la création et la gestion des destinataires.</p>
<p>Ce type de rôle ne vous permet d'attribuer une extension de messagerie aux dossiers publics. Pour ce faire, vous devez disposer d'un rôle associé au type de rôle <code>MailEnabledPublicFolders</code>.</p>
<p>Si votre organisation utilise un modèle d'autorisations divisées dans lequel la création des destinataires est effectuée par un groupe différent de celui chargé de gérer les destinataires, attribuez le rôle <code>MailRecipientCreation</code> au groupe responsable de la création des destinataires et le rôle <code>MailRecipients</code> au groupe réalisant la gestion des destinataires.</p></td>
<td><p>Organisation</p></td>
</tr>
<tr class="even">
<td><p><code>MailRecipients</code></p></td>
<td><p><a href="mail-recipients-role-exchange-2013-help.md">Rôle des destinataires de messagerie</a></p></td>
<td><p>Ce type de rôle est associé à des rôles permettant aux administrateurs de gérer les boîtes aux lettres, les utilisateurs de messagerie, les contacts de messagerie, les groupes de distribution et les groupes de distribution dynamiques au sein d'une organisation. Les rôles associés à ce type de rôle ne peuvent pas créer ces destinataires, mais peuvent être combinés avec des rôles associés avec le type de rôle <code>MailRecipientCreation</code> pour permettre la création et la gestion des destinataires.</p>
<p>Ce type de rôle ne vous permet pas de gérer des dossiers publics à extension messagerie ou des groupes de distribution. Pour gérer les dossiers publics à extension de messagerie, vous devez disposer d'un rôle associé au type de rôle <code>MailEnabledPublicFolders</code>. Pour gérer des groupes de distribution, vous devez disposer d'un rôle associé au type de rôle <code>DistributionGroups</code>.</p>
<p>Si votre organisation utilise un modèle d'autorisations divisées dans lequel la création des destinataires est effectuée par un groupe différent de celui chargé de gérer les destinataires, attribuez le rôle <code>MailRecipientCreation</code> au groupe responsable de la création des destinataires et le rôle <code>MailRecipients</code> au groupe réalisant la gestion des destinataires.</p></td>
<td><p>Organisation</p></td>
</tr>
<tr class="odd">
<td><p><code>MailTips</code></p></td>
<td><p><a href="mail-tips-role-exchange-2013-help.md">Rôle des conseils de messagerie</a></p></td>
<td><p>Ce type de rôle est associé à des rôles permettant aux administrateurs de gérer les conseils de messagerie au sein d'une organisation.</p></td>
<td><p>Organisation</p></td>
</tr>
<tr class="even">
<td><p><code>MessageTracking</code></p></td>
<td><p><a href="message-tracking-role-exchange-2013-help.md">Rôle de suivi des messages</a></p></td>
<td><p>Ce type de rôle est associé à des rôles permettant aux administrateurs d'effectuer le suivi des messages au sein d'une organisation.</p></td>
<td><p>Organisation</p></td>
</tr>
<tr class="odd">
<td><p><code>Migration</code></p></td>
<td><p><a href="migration-role-exchange-2013-help.md">Rôle de migration</a></p></td>
<td><p>Ce rôle type est associé à des rôles permettant aux administrateurs de migrer des boîtes aux lettres et leur contenu vers ou depuis un serveur.</p></td>
<td><p>Serveur</p></td>
</tr>
<tr class="even">
<td><p><code>Monitoring</code></p></td>
<td><p><a href="monitoring-role-exchange-2013-help.md">Rôle d’analyse</a></p></td>
<td><p>Ce type de rôle est associé à des rôles permettant aux administrateurs d'analyser les services Microsoft Exchange et la disponibilité des composants au sein d'une organisation. En plus des administrateurs, les rôles associés à ce type de rôle peuvent être utilisés avec le compte de service employé par les applications d'analyse pour collecter des informations relatives à l'état des serveurs Exchange.</p></td>
<td><p>Organisation</p></td>
</tr>
<tr class="odd">
<td><p><code>MoveMailboxes</code></p></td>
<td><p><a href="move-mailboxes-role-exchange-2013-help.md">Rôle Déplacer des boîtes aux lettres</a></p></td>
<td><p>Ce type de rôle est associé à des rôles permettant aux administrateurs de déplacer des boîtes aux lettres entre les serveurs d'une organisation et entre les serveurs de l'organisation et locale et d'une autre organisation.</p></td>
<td><p>Organisation</p></td>
</tr>
<tr class="even">
<td><p><code>OfficeExtensionApplication</code></p></td>
<td><p><a href="officeextensionapplication-role-exchange-2013-help.md">Rôle OfficeExtensionApplication</a></p></td>
<td><p>Ce type de rôle est associé à des rôles permettant à des applications d'extension Microsoft Office d'accéder aux boîtes aux lettres utilisateur au sein d'une organisation.</p></td>
<td><p>Organisation</p></td>
</tr>
<tr class="odd">
<td><p><code>OrgCustomApps</code></p></td>
<td><p><a href="org-custom-apps-role-exchange-2013-help.md">Rôle Org Custom Apps</a></p></td>
<td><p>Ce type de rôle est associé à des rôles permettant aux administrateurs d'afficher et de modifier des applications personnalisées de leur organisation au sein d'une organisation.</p></td>
<td><p>Organisation</p></td>
</tr>
<tr class="even">
<td><p><code>OrgMarketplaceApps</code></p></td>
<td><p><a href="org-marketplace-apps-role-exchange-2013-help.md">Rôle Org Marketplace Apps</a></p></td>
<td><p>Ce type de rôle est associé à des rôles permettant aux administrateurs d'afficher et de modifier des applications Marketplace de leur organisation au sein d'une organisation.</p></td>
<td><p>Organisation</p></td>
</tr>
<tr class="odd">
<td><p><code>OrganizationClientAccess</code></p></td>
<td><p><a href="organization-client-access-role-exchange-2013-help.md">Rôle d’accès au client de l’organisation</a></p></td>
<td><p>Ce type de rôle est associé à des rôles permettant aux administrateurs de gérer les paramètres du serveur d'accès au client au sein d'une organisation.</p></td>
<td><p>Organisation</p></td>
</tr>
<tr class="even">
<td><p><code>OrganizationConfiguration</code></p></td>
<td><p><a href="organization-configuration-role-exchange-2013-help.md">Rôle de configuration de l’organisation</a></p></td>
<td><p>Ce type de rôle est associé à des rôles permettant aux administrateurs de gérer les paramètres applicables à toute l'organisation au sein d'une organisation. Ce type de rôle permet de contrôler notamment les éléments de configuration d'organisation suivants :</p>
<ul>
<li><p>Activation ou désactivation de la fonctionnalité Infos-courrier pour l'organisation.</p></li>
<li><p>L'URL de la page d'accueil des dossiers gérés.</p></li>
<li><p>L'adresse SMTP des destinataires Microsoft Exchange et les adresses de messagerie de secours.</p></li>
<li><p>La configuration du schéma de propriétés de la boîte aux lettres de ressources.</p></li>
<li><p>Les adresses URL de l'aide pour le Centre d'administration Exchange et Outlook Web App.</p></li>
</ul>
<p>Ce type de rôle ne comprend pas les autorisations associées aux types de rôle <code>OrganizationClientAccess</code> ou <code>OrganizationTransportSettings</code>.</p></td>
<td><p>Organisation</p></td>
</tr>
<tr class="odd">
<td><p><code>OrganizationTransportSettings</code></p></td>
<td><p><a href="organization-transport-settings-role-exchange-2013-help.md">Rôle des paramètres de transport de l’organisation</a></p></td>
<td><p>Ce type de rôle est associé à des rôles permettant aux administrateurs de gérer les paramètres de transport au niveau de toute l'organisation, tels que les messages système, la configuration des sites Active Directory et d'autres paramètres de transport applicables globalement à l'organisation.</p>
<p>Ce rôle ne vous permet pas de créer ou de gérer des connecteurs de réception ou d'envoi de transport, des files d'attente, l'hygiène, les agents, les domaines distants et acceptés ou les règles. Pour créer ou gérer chacune des fonctionnalités de transport, vous devez disposer des rôles associés aux types de rôle suivants :</p>
<ul>
<li><p><strong>Connecteurs de réception</strong> <code>ReceiveConnectors</code></p></li>
<li><p><strong>Connecteurs d'envoi</strong> <code>SendConnectors</code></p></li>
<li><p><strong>Files d'attente de transport</strong> <code>TransportQueues</code></p></li>
<li><p><strong>Hygiène de transport</strong> <code>TransportHygiene</code></p></li>
<li><p><strong>Agents de transport</strong> <code>TransportAgents</code></p></li>
<li><p><strong>Domaines acceptés et distants</strong> <code>RemoteAndAcceptedDomains</code></p></li>
<li><p><strong>Règles de transport</strong> <code>TransportRules</code></p></li>
</ul></td>
<td><p>Organisation</p></td>
</tr>
<tr class="even">
<td><p><code>POP3AndIMAP4Protocols</code></p></td>
<td><p><a href="pop3-and-imap4-protocols-role-exchange-2013-help.md">Rôle des protocoles POP3 et IMAP4</a></p></td>
<td><p>Ce type de rôle est associé à des rôles permettant aux administrateurs de gérer la configuration POP3 et IMAP (paramètres d'authentification et de connexion, par exemple) sur des serveurs individuels.</p></td>
<td><p>Serveur</p></td>
</tr>
<tr class="odd">
<td><p><code>PublicFolders</code></p></td>
<td><p><a href="public-folders-role-exchange-2013-help.md">Rôle Dossiers publics</a></p></td>
<td><p>Ce type de rôle est associé à des rôles permettant aux administrateurs de gérer les dossiers publics au sein d'une organisation.</p>
<p>Ce type de rôle ne permet pas de gérer si des dossiers publics sont à extension messagerie. Pour activer ou désactiver l'extension de messagerie d'un dossier public, vous devez disposer d'un rôle associé au type de rôle <code>MailEnabledPublicFolders</code>.</p></td>
<td><p>Organisation</p></td>
</tr>
<tr class="even">
<td><p><code>ReceiveConnectors</code></p></td>
<td><p><a href="receive-connectors-role-exchange-2013-help.md">Rôle des connecteurs de réception</a></p></td>
<td><p>Ce type de rôle est associé à des rôles permettant aux administrateurs de gérer la configuration des connecteurs de réception (notamment les limites de taille) sur un serveur individuel.</p></td>
<td><p>Serveur</p></td>
</tr>
<tr class="odd">
<td><p><code>RecipientPolicies</code></p></td>
<td><p><a href="recipient-policies-role-exchange-2013-help.md">Rôle des stratégies de destinataire</a></p></td>
<td><p>Ce type de rôle est associé à des rôles permettant aux administrateurs de gérer des stratégies de destinataire, comme des stratégies de mise en service et d'appareil mobile, au sein d'une organisation.</p></td>
<td><p>Organisation</p></td>
</tr>
<tr class="even">
<td><p><code>RemoteAndAcceptedDomains</code></p></td>
<td><p><a href="remote-and-accepted-domains-role-exchange-2013-help.md">Rôle des domaines acceptés et distants</a></p></td>
<td><p>Ce type de rôle est associé à des rôles permettant aux administrateurs de gérer les domaines acceptés et distants au sein d'une organisation.</p></td>
<td><p>Organisation</p></td>
</tr>
<tr class="odd">
<td><p><code>ResetPassword</code></p></td>
<td><p><a href="reset-password-role-exchange-2013-help.md">Rôle de réinitialisation de mot de passe</a></p></td>
<td><p>Ce type de rôle est associé à des rôles permettant aux utilisateurs de réinitialiser leurs mots de passe et aux administrateurs de réinitialiser les mots de passe des utilisateurs au sein d'une organisation.</p></td>
<td><p>Organisation</p></td>
</tr>
<tr class="even">
<td><p><code>RetentionManagement</code></p></td>
<td><p><a href="retention-management-role-exchange-2013-help.md">Rôle de gestion de la rétention</a></p></td>
<td><p>Ce type de rôle est associé à des rôles permettant aux administrateurs de gérer les stratégies de rétention au sein d'une organisation.</p></td>
<td><p>Organisation</p></td>
</tr>
<tr class="odd">
<td><p><code>RoleManagement</code></p></td>
<td><p><a href="role-management-role-exchange-2013-help.md">Rôle de gestion des rôles</a></p></td>
<td><p>Ce type de rôle est associé à des rôles permettant aux administrateurs de gérer les groupes de rôles de gestion, les stratégies d'attribution de rôle, les rôles de gestion, les entrées de rôle, les attributions et les étendues au sein d'une organisation.</p>
<p>Les rôles attribués aux utilisateurs et associés à ce type de rôle peuvent remplacer la propriété <strong>Groupe de rôles géré par</strong>, configurer n'importe quel groupe de rôles et ajouter ou supprimer des membres dans n'importe quel groupe de rôles.</p></td>
<td><p>Organisation</p></td>
</tr>
<tr class="even">
<td><p><code>SecurityGroupCreationAndMembership</code></p></td>
<td><p><a href="security-group-creation-and-membership-role-exchange-2013-help.md">Création du groupe de sécurité et rôle de membre</a></p></td>
<td><p>Ce type de rôle est associé aux rôles permettant aux administrateurs de créer et de gérer des groupes universels de sécurité et leurs membres au sein d'une organisation.</p>
<p>Si votre organisation utilise un modèle d'autorisations divisées dans lequel la création et la gestion des groupes universels de sécurité sont réalisées par un groupe différent de celui qui gère les serveurs Exchange, attribuez à ce groupe les rôles associés à ce type de rôle.</p></td>
<td><p>Organisation</p></td>
</tr>
<tr class="odd">
<td><p><code>SendConnectors</code></p></td>
<td><p><a href="send-connectors-role-exchange-2013-help.md">Rôle Connecteurs d’envoi</a></p></td>
<td><p>Ce type de rôle est associé à des rôles permettant aux administrateurs de gérer les connecteurs d'envoi de transport au sein d'une organisation.</p></td>
<td><p>Organisation</p></td>
</tr>
<tr class="even">
<td><p><code>SupportDiagnostics</code></p></td>
<td><p><a href="support-diagnostics-role-exchange-2013-help.md">Prise en charge du rôle de diagnostics</a></p></td>
<td><p>Ce type de rôle est associé avec des rôles permettant aux administrateurs de réaliser des diagnostics avancés sous la direction des services de Support Microsoft au sein d'une organisation.</p>
<table>
<thead>
<tr class="header">
<th><img src="images/JJ673034.Caution(EXCHG.150).gif" title="Attention" alt="Attention" />Attention :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Les rôles associés à ce type de rôle accordent des autorisations aux cmdlets et aux scripts qui doivent uniquement être utilisés sous la direction du Support Microsoft.</td>
</tr>
</tbody>
</table>

</td>
<td><p>Organisation</p></td>
</tr>
<tr class="odd">
<td><p><code>TeamMailboxes</code></p></td>
<td><p><a href="team-mailboxes-role-exchange-2013-help.md">Rôle de boîtes aux lettres d’équipe</a></p></td>
<td><p>Ce type de rôle est associé à des rôles permettant aux administrateurs de définir une ou plusieurs stratégies de mise en service de boîtes aux lettres de site et de gérer des boîtes aux lettres de site au sein d'une organisation. Les rôles attribués aux administrateurs associés à ce type de rôle peuvent gérer des boîtes aux lettres de site qui ne leur appartiennent pas.</p></td>
<td><p>Organisation</p></td>
</tr>
<tr class="even">
<td><p><code>TeamMailboxLifecycleApplication</code></p></td>
<td><p><a href="teammailboxlifecycleapplication-role-exchange-2013-help.md">Rôle TeamMailboxLifecycleApplication</a></p></td>
<td><p>Ce type de rôle est associé à des rôles permettant à des applications partenaires de mettre à jour des états de cycle de vie de boîtes aux lettres de site au sein d'une organisation.</p></td>
<td><p>Organisation</p></td>
</tr>
<tr class="odd">
<td><p><code>TransportAgents</code></p></td>
<td><p><a href="transport-agents-role-exchange-2013-help.md">Rôle des agents de transport</a></p></td>
<td><p>Ce type de rôle est associé à des rôles permettant aux administrateurs de gérer les agents de transport au sein d'une organisation.</p></td>
<td><p>Organisation</p></td>
</tr>
<tr class="even">
<td><p><code>TransportHygiene</code></p></td>
<td><p><a href="transport-hygiene-role-exchange-2013-help.md">Rôle d’hygiène de transport</a></p></td>
<td><p>Ce type de rôle est associé à des rôles permettant aux administrateurs de gérer des fonctionnalités anti-courrier indésirable et anti-programme malveillant au sein d'une organisation.</p></td>
<td><p>Organisation</p></td>
</tr>
<tr class="odd">
<td><p><code>TransportQueues</code></p></td>
<td><p><a href="transport-queues-role-exchange-2013-help.md">Rôle des files d’attente de transport</a></p></td>
<td><p>Ce type de rôle est associé à des rôles permettant aux administrateurs de gérer les files d'attente de transport sur des serveurs individuels.</p></td>
<td><p>Serveur</p></td>
</tr>
<tr class="even">
<td><p><code>TransportRules</code></p></td>
<td><p><a href="transport-rules-role-exchange-2013-help.md">Rôle des règles de transport</a></p></td>
<td><p>Ce type de rôle est associé à des rôles permettant aux administrateurs de gérer les règles de transport au sein d'une organisation.</p></td>
<td><p>Organisation</p></td>
</tr>
<tr class="odd">
<td><p><code>UMMailboxes</code></p></td>
<td><p><a href="um-mailboxes-role-exchange-2013-help.md">Rôle des boîtes aux lettres de messagerie unifiée</a></p></td>
<td><p>Ce type de rôle est associé à des rôles permettant aux administrateurs de gérer la configuration de message unifiée des boîtes aux lettres et des autres destinataires au sein d'une organisation.</p></td>
<td><p>Organisation</p></td>
</tr>
<tr class="even">
<td><p><code>UMPrompts</code></p></td>
<td><p><a href="um-prompts-role-exchange-2013-help.md">Rôle Messages de messagerie unifiée</a></p></td>
<td><p>Ce type de rôle est associé aux rôles permettant aux administrateurs de créer et de gérer les invites vocales personnalisées de messagerie unifiée au sein d'une organisation.</p></td>
<td><p>Organisation</p></td>
</tr>
<tr class="odd">
<td><p><code>UnifiedMessaging</code></p></td>
<td><p><a href="unified-messaging-role-exchange-2013-help.md">Rôle de messagerie unifiée</a></p></td>
<td><p>Ce type de rôle est associé à des rôles permettant aux administrateurs de gérer des services de messagerie unifiée au sein d'une organisation.</p>
<p>Ce rôle ne vous permet pas de gérer une configuration de boîte aux lettres spécifique à la messagerie unifiée ou des invites de messagerie unifiée. Pour gérer la configuration des boîtes aux lettres spécifique à la messagerie unifiée, utilisez les rôles associés au type de rôle <code>UMMailboxes</code>. Pour gérer les invites de messagerie unifiée, utilisez les rôles associés au type de rôle <code>UMPrompts</code>.</p></td>
<td><p>Organisation</p></td>
</tr>
<tr class="even">
<td><p><code>UnScopedRoleManagement</code></p></td>
<td><p><a href="unscoped-role-management-role-exchange-2013-help.md">Rôle de gestion de rôle non délimité</a></p></td>
<td><p>Ce type de rôle est associé aux rôles permettant aux administrateurs de créer et de gérer les rôles de gestion de niveau supérieur non délimités au sein d'une organisation.</p></td>
<td><p>Organisation</p></td>
</tr>
<tr class="odd">
<td><p><code>UserOptions</code></p></td>
<td><p><a href="user-options-role-exchange-2013-help.md">Rôle des options de l’utilisateur</a></p></td>
<td><p>Ce type de rôle est associé à des rôles permettant aux administrateurs d'afficher les options Outlook Web App d'un utilisateur au sein d'une organisation. Les rôles associés à ce type de rôle peuvent être utilisés pour aider un utilisateur à diagnostiquer des problèmes avec sa configuration.</p></td>
<td><p>Organisation</p></td>
</tr>
<tr class="even">
<td><p><code>UserApplication</code></p></td>
<td><p><a href="userapplication-role-exchange-2013-help.md">Rôle UserApplication</a></p></td>
<td><p>Ce type de rôle est associé à des rôles permettant à des applications partenaires d'agir pour le compte d'utilisateurs finaux au sein d'une organisation.</p></td>
<td><p>Organisation</p></td>
</tr>
<tr class="odd">
<td><p><code>ViewOnlyAuditLogs</code></p></td>
<td><p><a href="view-only-audit-logs-role-exchange-2013-help.md">Rôle Journaux d’audit en affichage seul</a></p></td>
<td><p>Ce type de rôle est associé à des rôles permettant aux administrateurs d'effectuer des recherches dans le journal d'audit d'administrateur au sein d'une organisation.</p></td>
<td><p>Organisation</p></td>
</tr>
<tr class="even">
<td><p><code>ViewOnlyConfiguration</code></p></td>
<td><p><a href="view-only-configuration-role-exchange-2013-help.md">Rôle de configuration en affichage seul</a></p></td>
<td><p>Ce type de rôle est associé à des rôles permettant aux administrateurs d'afficher tous les paramètres (ne concernant pas les destinataires) de configuration d'Exchange au sein d'une organisation. Les exemples de configuration qui sont affichables sont la configuration du serveur, la configuration du transport, la configuration de la base de données et la configuration à l'échelle de l'organisation.</p>
<p>Les rôles associés avec ce type de rôle peuvent être combinés avec des rôles associés au type de rôle <code>ViewOnlyRecipients</code> pour créer un rôle pouvant afficher chaque objet d'une organisation.</p></td>
<td><p>Organisation</p></td>
</tr>
<tr class="odd">
<td><p><code>ViewOnlyRecipients</code></p></td>
<td><p><a href="view-only-recipients-role-exchange-2013-help.md">Rôle Destinataires en affichage uniquement</a></p></td>
<td><p>Ce type de rôle est associé à des rôles permettant aux administrateurs d'afficher la configuration des destinataires, comme les boîtes aux lettres, les utilisateurs de messagerie, les contacts de messagerie, les groupes de distribution et les groupes de distribution dynamique.</p>
<p>Les rôles associés à ce type de rôle peuvent être combinés avec des rôles associés au type de rôle <code>ViewOnlyConfiguration</code> pour créer un rôle pouvant afficher chaque objet de l'organisation.</p></td>
<td><p>Organisation</p></td>
</tr>
<tr class="even">
<td><p><code>WorkloadManagement</code></p></td>
<td><p><a href="workloadmanagement-role-exchange-2013-help.md">Rôle WorkloadManagement</a></p></td>
<td><p>Ce type de rôle est associé à des rôles permettant aux administrateurs de gérer des stratégies de gestion de la charge de travail au sein d'une organisation. Les administrateurs peuvent configurer des définitions de l'intégralité de la ressource, des classifications de la charge de travail et activer ou désactiver la gestion de la charge de travail.</p></td>
<td><p>Organisation</p></td>
</tr>
</tbody>
</table>


Le tableau suivant répertorie tous les types de rôle de gestion centré sur l'utilisateur dans Exchange 2013.

**Types de rôle centré sur l'utilisateur**


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Type de rôle de gestion</th>
<th>Rôles intégrés centrés sur l'utilisateur</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>MyBaseOptions</code></p></td>
<td><p><a href="mybaseoptions-role-exchange-2013-help.md">Rôle MyBaseOptions</a></p></td>
<td><p>Ce type de rôle est associé à des rôles permettant aux utilisateurs individuels d'afficher et de modifier la configuration de base de leurs boîtes aux lettres et des paramètres associés.</p></td>
</tr>
<tr class="even">
<td><p><code>MyContactInformation</code></p></td>
<td><p><a href="myaddressinformation-role-exchange-2013-help.md">Rôle de MyAddressInformation</a></p>
<p><a href="mycontactinformation-role-exchange-2013-help.md">Rôle MyContactInformation</a></p>
<p><a href="mymobileinformation-role-exchange-2013-help.md">Rôle de MyMobileInformation</a></p>
<p><a href="mypersonalinformation-role-exchange-2013-help.md">Rôle de MyPersonalInformation</a></p></td>
<td><p>Ce type de rôle est associé à des rôles permettant aux utilisateurs individuels de modifier leurs informations de contact. Ces informations comprennent leurs numéros de téléphone et adresse.</p></td>
</tr>
<tr class="odd">
<td><p>MyCustomApps</p></td>
<td><p><a href="my-custom-apps-role-exchange-2013-help.md">Rôle My Custom Apps</a></p></td>
<td><p>Ce type de rôle est associé à des rôles permettant aux utilisateurs individuels d'afficher et de modifier leurs applications personnalisées.</p></td>
</tr>
<tr class="even">
<td><p>MyDiagnostics</p></td>
<td><p><a href="mydiagnostics-role-exchange-2013-help.md">Rôle MyDiagnostics</a></p></td>
<td><p>Ce type de rôle est associé à des rôles permettant aux utilisateurs individuels d'effectuer des diagnostics de base sur leur boîte aux lettres comme, par exemple, la récupération des informations de diagnostic de calendrier.</p></td>
</tr>
<tr class="odd">
<td><p><code>MyDistributionGroupMembership</code></p></td>
<td><p><a href="mydistributiongroupmembership-role-exchange-2013-help.md">Rôle MyDistributionGroupMembership</a></p></td>
<td><p>Ce type de rôle est associé à des rôles permettant aux utilisateurs individuels d'afficher et de modifier leur appartenance aux groupes de distribution d'une organisation, à condition que ces groupes de distribution permettent la modification de l'appartenance.</p></td>
</tr>
<tr class="even">
<td><p><code>MyDistributionGroups</code></p></td>
<td><p><a href="mydistributiongroups-role-exchange-2013-help.md">Rôle MyDistributionGroups</a></p></td>
<td><p>Ce type de rôle est associé à des rôles permettant aux utilisateurs individuels de créer, de modifier et d'afficher les groupes de distribution, et de modifier, d'afficher, de supprimer et d'ajouter des membres dans les groupes de distribution qu'ils possèdent.</p></td>
</tr>
<tr class="odd">
<td><p><code>MyProfileInformation</code></p></td>
<td><p><a href="mydisplayname-role-exchange-2013-help.md">Rôle de MyDisplayName</a></p>
<p><a href="myname-role-exchange-2013-help.md">Rôle de MyName</a></p>
<p><a href="myprofileinformation-role-exchange-2013-help.md">Rôle MyProfileInformation</a></p></td>
<td><p>Ce type de rôle est associé à des rôles permettant aux utilisateurs individuels de modifier leur nom.</p></td>
</tr>
<tr class="even">
<td><p>MyMarketplaceApps</p></td>
<td><p><a href="my-marketplace-apps-role-exchange-2013-help.md">Rôle My Marketplace Apps</a></p></td>
<td><p>Ce type de rôle est associé à des rôles permettant aux utilisateurs individuels d'afficher et de modifier leurs applications Marketplace.</p></td>
</tr>
<tr class="odd">
<td><p><code>MyRetentionPolicies</code></p></td>
<td><p><a href="myretentionpolicies-role-exchange-2013-help.md">Rôle MyRetentionPolicies</a></p></td>
<td><p>Ce type de rôle est associé à des rôles permettant aux utilisateurs individuels d'afficher leurs balises de rétention, et d'afficher et de modifier leurs paramètres de balises de rétention et leurs valeurs par défaut.</p></td>
</tr>
<tr class="even">
<td><p>MyTeamMailboxes</p></td>
<td><p><a href="myteammailboxes-role-exchange-2013-help.md">Rôle MyTeamMailboxes</a></p></td>
<td><p>Ce type de rôle est associé à des rôles permettant à des utilisateurs individuels de créer des boîtes aux lettres de site et de les connecter à des sites Microsoft SharePoint.</p></td>
</tr>
<tr class="odd">
<td><p><code>MyTextMessaging</code></p></td>
<td><p><a href="mytextmessaging-role-exchange-2013-help.md">Rôle MyTextMessaging</a></p></td>
<td><p>Ce type de rôle est associé à des rôles permettant aux utilisateurs individuels de créer, d'afficher et de modifier leurs paramètres de messagerie texte.</p></td>
</tr>
<tr class="even">
<td><p><code>MyVoiceMail</code></p></td>
<td><p><a href="myvoicemail-role-exchange-2013-help.md">Rôle MyVoiceMail</a></p></td>
<td><p>Ce type de rôle est associé à des rôles permettant aux utilisateurs individuels d'afficher et de modifier leurs paramètres de messagerie vocale.</p></td>
</tr>
</tbody>
</table>


Retour au début

## Pour plus d'informations

[New-ManagementRole](https://technet.microsoft.com/fr-fr/library/dd298073\(v=exchg.150\))

[New-ManagementRoleAssignment](https://technet.microsoft.com/fr-fr/library/dd335193\(v=exchg.150\))

[Set-ManagementRoleAssignment](https://technet.microsoft.com/fr-fr/library/dd335173\(v=exchg.150\))

[New-ManagementScope](https://technet.microsoft.com/fr-fr/library/dd335137\(v=exchg.150\))

[Set-ManagementScope](https://technet.microsoft.com/fr-fr/library/dd297996\(v=exchg.150\))

[New-ManagementRoleAssignment](https://technet.microsoft.com/fr-fr/library/dd335193\(v=exchg.150\))

[Set-ManagementRoleAssignment](https://technet.microsoft.com/fr-fr/library/dd335173\(v=exchg.150\))

