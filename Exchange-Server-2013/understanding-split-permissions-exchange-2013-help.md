---
title: 'Présentation des autorisations fractionnées: Exchange 2013 Help'
TOCTitle: Présentation des autorisations fractionnées
ms:assetid: 2b709e15-63a2-4841-94bc-b289b71166d0
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dd638106(v=EXCHG.150)
ms:contentKeyID: 50477789
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Présentation des autorisations fractionnées

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2015-04-07_

Les organisations qui séparent la gestion des objets Microsoft Exchange Server 2013 et des objets Active Directory utilisent un modèle d’*autorisations fractionnées*. Les autorisations fractionnées permettent aux organisations d’attribuer des autorisations spécifiques et des tâches correspondantes à des groupes spécifiques au sein de l’organisation. Cette séparation du travail aide à maintenir les normes et les flux de travail et contribue au contrôle des modifications dans l’organisation.

Le plus haut niveau d’autorisations fractionnées est la séparation de la gestion Exchange et Active Directory. De nombreuses organisations possèdent deux groupes : les administrateurs qui gèrent l’infrastructure Exchange de l’organisation, y compris les serveurs et les destinataires, et les administrateurs qui gèrent l’infrastructure Active Directory. C’est une séparation importante pour nombre d’organisations car l’infrastructure Active Directory s’étend souvent sur plusieurs endroits, domaines, services, applications et même sur plusieurs forêts Active Directory. Les administrateurs Active Directory doivent s’assurer que les changements apportés à Active Directory n’ont pas de répercussion néfaste sur d’autres services. Par conséquent, généralement, seul un petit groupe d’administrateurs a l’autorisation de gérer l’infrastructure.

Cela dit, l’infrastructure de Exchange, y compris les serveurs et les destinataires, peut aussi être complexe et exiger des connaissances spéciales. En outre, Exchange stocke des informations extrêmement confidentielles sur l’activité de l’organisation. Potentiellement, les administrateurs d’Exchange peuvent accéder à ces informations. En limitant le nombre d’administrateurs Exchange, l’organisation limite le nombre de personnes pouvant apporter des changements à la configuration d’Exchange et pouvant accéder aux informations sensibles.

Les autorisations fractionnées font généralement la distinction entre la création des principaux de sécurité dans Active Directory, tels que les utilisateurs et les groupes de sécurité, et la configuration de ces objets. Cela permet de réduire le risque d’accès non autorisés au réseau via le contrôle des créateurs d’objets qui en autorisent l’accès. Le plus souvent, seuls les administrateurs d’Active Directory peuvent créer des principaux de sécurité alors que les autres administrateurs, tels que les administrateurs d’Exchange, peuvent gérer les attributs spécifiques des objets Active Directory existants.

Pour prendre en charge les besoins changeants de séparation de la gestion de Exchange et Active Directory, Exchange 2013 vous permet de choisir si vous souhaitez un modèle d’autorisations partagées ou un modèle d’autorisations divisées. Exchange 2013 offre deux types de modèles d’autorisations divisées : RBAC et Active Directory. Exchange 2013 sélectionne par défaut un modèle d’autorisations partagées.

**Contenu de cette rubrique**

Explication du contrôle de l’accès basé sur un rôle et d’Active Directory

Autorisations partagées

Autorisations fractionnées

Autorisations fractionnées RBAC

Autorisations fractionnées Active Directory

## Explication du contrôle de l’accès basé sur un rôle et d’Active Directory


Pour comprendre les autorisations fractionnées, vous devez d’abord comprendre le fonctionnement d’un modèle d’autorisations du contrôle de l’accès basé sur un rôle (RBAC) Exchange 2013 avec Active Directory. Le modèle RBAC maîtrise qui peut effectuer les actions, et sur quels objets ces actions peuvent être effectuées. Pour plus d’informations sur les divers composants RBAC évoqués dans ce sujet, voir [Présentation du contrôle d'accès basé sur un rôle](understanding-role-based-access-control-exchange-2013-help.md).

Dans Exchange 2013, toutes les tâches effectuées sur les objets Exchange doivent passer par l’environnement de ligne de commande Exchange Management Shell ou l’interface du Centre d’administration Exchange (CAE). Ces deux outils de gestion utilisent RBAC pour autoriser toutes les tâches effectuées.

RBAC est un composant qui existe sur chaque serveur exécutant Exchange 2013. RBAC vérifie si l’utilisateur effectuant l’action y est autorisé:

  - Si ce n’est pas le cas, RBAC met l’action en échec.

  - Si l’utilisateur a l’autorisation, RBAC vérifie s’il est bien autorisé à effectuer l’action sur l’objet spécifique demandé :
    
      - Si l’utilisateur est autorisé, RBAC permet à l’action de continuer.
    
      - Si l’utilisateur n’est pas autorisé, RBAC n’autorise pas la poursuite de l’action.

Si RBAC autorise une action, celle-ci est effectuée dans le contexte du sous-système approuvé Exchange et non pas dans le contexte de l’utilisateur. Le sous-système approuvé Exchange est un groupe universel de sécurité disposant de l’accès en lecture et écriture à tous les objets associés à Exchange dans l’organisation Exchange. C’est aussi un membre des groupes de sécurité locaux des administrateurs et le groupe universel de sécurité des autorisations Windows Exchange qui permettent à Exchange de créer et de gérer des objets Active Directory.

> [!CAUTION]
> N’effectuez aucune modification manuelle à l’appartenance au groupe de sécurité du sous-système approuvé Exchange. Ne l’ajoutez pas dans des listes de contrôle d’accès (ACL) et ne le supprimez pas de ces listes. En effectuant vous-même les modifications au groupe de sécurité universelle du sous-système approuvé Exchange, vous risqueriez de causer des dommages irréparables à votre organisation Exchange.


Il faut bien comprendre que les autorisations Active Directory d’un utilisateur n’importent pas lors de l’utilisation des outils de gestion Exchange. Si l’utilisateur a l’autorisation, via RBAC, d’effectuer une action dans les outils de gestion Exchange, il peut effectuer l’action quelles que soient ses autorisations Active Directory. À l’inverse, si un utilisateur est un Administrateur d’entreprise dans Active Directory mais n’est pas autorisé à effectuer une action telle que la création d’une boîte aux lettres dans les outils de gestion Exchange, l’action échouera car l’utilisateur n’a pas les autorisations requises selon RBAC.

> [!IMPORTANT]  
> Bien que le modèle des autorisations RBAC ne s’applique pas à l’outil de gestion des utilisateurs et ordinateurs Active Directory, les utilisateurs et ordinateurs Active Directory ne peuvent pas gérer la configuration Exchange. Ainsi, même si un utilisateur a l’accès pour modifier quelques attributs sur les objets Active Directory, tels que le nom complet de l’utilisateur, il doit employer les outils de gestion Exchange, et doit donc disposer de l’autorisation RBAC, pour gérer les attributs Exchange.


Retour au début

## Autorisations partagées

Le modèle des autorisations partagées est le modèle par défaut d’Exchange 2013. Vous n’avez pas besoin de changer quoi que ce soit si c’est le modèle d’autorisations que vous souhaitez utiliser. Ce modèle ne sépare pas la gestion des objets Exchange et Active Directory du cadre des outils de gestion Exchange. Il permet aux administrateurs utilisant les outils de gestion Exchange de créer des principaux de sécurité dans Active Directory.

Le tableau suivant répertorie les rôles permettant la création de principaux de sécurité dans Exchange et les groupes de rôles de gestion auxquels ils sont affectés par défaut.

### Rôles de gestion du principal de sécurité

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Rôle de gestion</th>
<th>Groupe de rôles</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="mail-recipient-creation-role-exchange-2013-help.md">Rôle Création de destinataires de message</a></p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gestion des destinataires</a></p></td>
</tr>
<tr class="even">
<td><p><a href="security-group-creation-and-membership-role-exchange-2013-help.md">Création du groupe de sécurité et rôle de membre</a></p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p></td>
</tr>
</tbody>
</table>


Seuls les groupes de rôles, les utilisateurs ou les groupes de sécurité universels affectés au rôle Création de destinataires de message peuvent créer des principaux de sécurité tels que les utilisateurs Active Directory. Par défaut, les groupes de rôles Gestion de l’organisation et Gestion des destinataires sont affectés à ce rôle. Par conséquent, les membres de ces groupes de rôles peuvent créer des principaux de sécurité.

Seuls les groupes de rôles, les utilisateurs ou les groupes de sécurité universels affectés au rôle Création et appartenance au groupe de sécurité peuvent créer des groupes de sécurité ou gérer leur appartenance. Par défaut, seul le groupe de rôles Gestion de l’organisation est affecté à ce rôle. Par conséquent, seuls les membres du groupe de rôles Gestion de l’organisation peuvent créer ou gérer l’appartenance des groupes de sécurité.

Vous pouvez attribuer les rôles Création du destinataire, Création et appartenance au groupe de sécurité aux autres groupes de rôles, utilisateurs ou groupes de sécurité si vous voulez permettre à d’autres de créer des principaux de sécurité.

Pour permettre la gestion des principaux de sécurité existants dans Exchange 2013, le rôle Destinataires de message est attribué par défaut aux groupes de rôles Gestion de l’organisation et Gestion des destinataires. Seuls les groupes de rôles, les utilisateurs ou les groupes de sécurité universels affectés au rôle Destinataires de message peuvent gérer des principaux de sécurité existants. Si vous souhaitez que d’autres groupes de rôles, d’autres utilisateurs ou d’autres groupes de sécurité universels puissent gérer les principaux de sécurité existants, vous devez leur attribuer le rôle de Destinataires de message.

Pour plus d’informations sur l’ajout de rôles à des groupes de rôles, à des utilisateurs ou à des groupes de sécurité universels, voir les rubriques suivantes :

  - [Gérer des groupes de rôles](manage-role-groups-exchange-2013-help.md)

  - [Ajouter un rôle à un utilisateur ou un groupe de sécurité universel](add-a-role-to-a-user-or-usg-exchange-2013-help.md)

Si vous êtes passé à un modèle d’autorisations fractionnées et que vous voulez retourner à un modèle d’autorisations partagées, voir [Configurer Exchange 2013 pour les autorisations partagées](configure-exchange-2013-for-shared-permissions-exchange-2013-help.md).

Retour au début

## Autorisations fractionnées

Si votre organisation sépare la gestion Exchange de la gestion Active Directory, vous devrez configurer Exchange pour qu’il prenne en charge le modèle d’autorisations fractionnées. Si vous l’avez configuré correctement, seuls les administrateurs à qui vous avez donné l’autorisation de créer des principaux de sécurité, les administrateurs Active Directory par exemple, pourront le faire et seuls les administrateurs Exchange seront en mesure de modifier les attributs Exchange sur les principaux de sécurité existants. Cette séparation d’autorisations se retrouve plus ou moins dans les lignes de partition du domaine et de configuration dans Active Directory. Les partitions sont également appelées contextes d’appellation. La partition de domaine stocke les utilisateurs, les groupes et d’autres objets pour un domaine spécifique. La partition de configuration stocke des informations sur la configuration de la forêt entière pour les services qu’utilise Active Directory, tel que Exchange. Les données stockées dans la partition de domaine sont généralement gérées par les administrateurs Active Directory, bien que les objets puissent contenir des attributs spécifiques à Exchange qui peuvent être gérés par les administrateurs Exchange. Les données stockées dans la partition de configuration sont gérées par les administrateurs de chaque service respectif qui stocke des données dans cette partition. Pour Exchange, il s’agit généralement des administrateurs Exchange.

Exchange 2013 prend en charge les deux types d’autorisations fractionnées suivants :

  - **autorisations fractionnées RBAC**   Les autorisations pour créer des principaux de sécurité dans la partition du domaine Active Directory sont contrôlées par RBAC. Seuls les serveurs Exchange, les services et les membres des groupes de rôles appropriés peuvent créer des principaux de sécurité.

  - **autorisations fractionnées Active Directory**   Les autorisations pour créer des principaux de sécurité dans la partition du domaine Active Directory sont totalement supprimées de tout utilisateur, service ou serveur Exchange. Aucune option n’est fournie dans RBAC pour créer des principaux de sécurité. La création de principaux de sécurité dans Active Directory doit être effectuée à l’aide des outils de gestion Active Directory.
    
    > [!IMPORTANT]  
    > Bien que les autorisations fractionnées Active Directory puissent uniquement être activées ou désactivées en exécutant le programme d’installation sur un ordinateur sur lequel Exchange 2013 est installé, la configuration des autorisations fractionnées Active Directory s’applique à la fois aux serveurs Exchange 2013 et Exchange 2010. Cela n’a cependant aucune incidence sur les serveurs Microsoft Exchange Server 2007.


Si votre organisation choisit d’utiliser un modèle d’autorisations fractionnées plutôt que d’autorisations partagées, il est conseillé d’utiliser le modèle d’autorisations fractionnées RBAC. Le modèle d’autorisations fractionnées RBAC offre beaucoup plus de flexibilité en fournissant presque la même séparation de l’administration que les autorisations fractionnées Active Directory, à l’exception du fait que les serveurs et services Exchange peuvent créer des principaux de sécurité dans le modèle d’autorisations fractionnées RBAC.

Vous êtes invité à activer les autorisations fractionnées Active Directory lors de l’installation. Si vous choisissez d’activer les autorisations fractionnées Active Directory, vous ne pourrez les changer en autorisations partagées ou en autorisations fractionnées RBAC qu’en réexécutant le programme d’installation et en désactivant les autorisations fractionnées Active Directory. Ce choix s’applique à tous les serveurs Exchange 2010 et Exchange 2013 de l’organisation.

Les sections suivantes reviennent en détail sur les autorisations fractionnées RBAC et Active Directory.

Retour au début

## Autorisations fractionnées RBAC

Le modèle de sécurité RBAC modifie les attributions des rôles de gestion par défaut afin de distinguer ceux qui peuvent créer les principaux de sécurité dans la partition du domaine Active Directory de ceux qui administrent les données de l’organisation Exchange dans la partition de configuration Active Directory. Les principaux de sécurité, tels que les utilisateurs dotés de boîtes aux lettres et associés à des groupes de distribution, peuvent être créés par des administrateurs qui sont membres des rôles Création de destinataires de message et Création et appartenance au groupe de sécurité. Ces autorisations restent séparées des autorisations requises pour créer des principaux de sécurité en dehors des outils de gestion Exchange. Les administrateurs Exchange qui ne sont pas affectés aux rôles Création du destinataire de messagerie ou Création et appartenance au groupe de sécurité peuvent toujours modifier les attributs Exchange sur les principaux de sécurité. Les administrateurs Active Directory ont également la possibilité d’utiliser les outils de gestion Exchange pour créer des principaux de sécurité Active Directory.

Les serveurs Exchange et le sous-système approuvé Exchange ont également les autorisations de créer des principaux de sécurité dans Active Directory de la part d’utilisateurs et de programmes tiers s’intégrant à RBAC.

Les autorisations fractionnées RBAC sont un bon choix pour votre organisation si les conditions suivantes sont remplies :

  - Votre organisation ne requiert pas que la création de principaux de sécurité soit effectuée en utilisant uniquement les outils de gestion Active Directory ni uniquement par les utilisateurs à qui des autorisations Active Directory spécifiques ont été attribuées.

  - Votre organisation permet aux services, tels que les serveurs Exchange, de créer des principaux de sécurité.

  - Vous souhaitez simplifier le processus requis pour créer des boîtes aux lettres, des utilisateurs à extension messagerie, des groupes de distribution et des groupes de rôles en autorisant leur création depuis les outils de gestion Exchange.

  - Vous souhaitez gérer l’appartenance aux groupes de distribution et aux groupes de rôles dans les outils de gestion Exchange.

  - Vous avez des programmes tiers qui demandent que les serveurs Exchange soient capables de créer des principaux de sécurité en leur nom.

Si votre organisation requiert une séparation complète entre l’administration Exchange et Active Directory où aucune administration Active Directory ne peut être effectuée à l’aide des outils de gestion Exchange ni par les services Exchange, voir Autorisations fractionnées Active Directory plus loin dans cette rubrique.

Basculer des autorisations partagées aux autorisations fractionnées RBAC est un processus manuel dans lequel vous supprimez les autorisations requises pour créer des principaux de sécurité des groupes de rôles où elles sont accordées par défaut. Le tableau suivant répertorie les rôles permettant la création de principaux de sécurité dans Exchange et les groupes de rôles de gestion auxquels ils sont affectés par défaut.

### Rôles de gestion du principal de sécurité

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Rôle de gestion</th>
<th>Groupe de rôles</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="mail-recipient-creation-role-exchange-2013-help.md">Rôle Création de destinataires de message</a></p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gestion des destinataires</a></p></td>
</tr>
<tr class="even">
<td><p><a href="security-group-creation-and-membership-role-exchange-2013-help.md">Création du groupe de sécurité et rôle de membre</a></p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p></td>
</tr>
</tbody>
</table>


Par défaut, les membres des groupes de rôles Gestion de l’organisation et Gestion des destinataires peuvent créer des principaux de sécurité. Vous devez transférer la capacité de création des principaux de sécurité à partir des groupes de rôles intégrés vers un nouveau groupe de rôles que vous créez.

Pour configurer des autorisations fractionnées RBAC, vous devez procéder comme suit :

1.  Désactivez les autorisations fractionnées Active Directory si elles sont activées.

2.  Créez un groupe de rôles qui contiendra les administrateurs Active Directory pouvant créer des principaux de sécurité.

3.  Créez des attributions normales et de rôles de délégation entre le rôle Création du destinataire de message et le nouveau groupe de rôles.

4.  Créez des attributions normales et de rôles de délégation entre le rôle Création et appartenance au groupe de sécurité et le nouveau groupe de rôles.

5.  Supprimez les attributions de rôle ordinaires et de gestion de délégation entre le rôle Création de destinataires de message et les groupes de rôles Gestion de l’organisation et Gestion des destinataires.

6.  Supprimez les attributions de rôle ordinaires et de délégation entre le rôle Création et appartenance au groupe de sécurité et le groupe de rôles Gestion de l’organisation.

Une fois que vous aurez fait cela, seuls les membres du nouveau groupe de rôles que vous créez pourront créer des principaux de sécurité tels que des boîtes aux lettres. Le nouveau groupe pourra uniquement créer les objets. Il ne pourra pas configurer les attributs Exchange sur le nouvel objet. Un administrateur Active Directory, qui est membre du nouveau groupe, devra créer l’objet puis un administrateur Exchange devra configurer les attributs Exchange sur l’objet. Les administrateurs Exchange ne pourront pas utiliser les cmdlets suivantes :

  - **New-Mailbox**

  - **New-MailContact**

  - **New-MailUser**

  - **New-RemoteMailbox**

  - **Remove-Mailbox**

  - **Remove-MailContact**

  - **Remove-MailUser**

  - **Remove-RemoteMailbox**

Toutefois, les administrateurs Exchange pourront créer et gérer des objets spécifiques à Exchange, tels que les règles de transport, les groupes de distribution, etc. et gérer les attributs liés à Exchange sur n’importe quel objet.

De plus, les fonctionnalités associées dans le CAE et Outlook Web App, telles que l’Assistant Nouvelle boîte aux lettres, ne seront plus disponibles ou généreront une erreur si vous tentez de les utiliser.

Si vous souhaitez que le nouveau groupe de rôles puisse gérer les attributs Exchange sur le nouvel objet, il faut alors lui attribuer le rôle Destinataires de message.

Pour plus d’informations sur la configuration du modèle des autorisations fractionnées, voir [Configurer Exchange 2013 pour les autorisations divisées](configure-exchange-2013-for-split-permissions-exchange-2013-help.md).

Retour au début

## Autorisations fractionnées Active Directory

Avec les autorisations fractionnées Active Directory, la création de principaux de sécurité dans la partition du domaine Active Directory, tels que les boîtes aux lettres et les groupes de distribution, doit être effectuée à l’aide des outils de gestion Active Directory. Plusieurs modifications sont effectuées aux autorisations accordées au sous-système approuvé Exchange et aux serveurs Exchange pour limiter ce que les administrateurs et les serveurs Exchange peuvent faire. Les modifications suivantes ont lieu lorsque vous activez les autorisations fractionnées Active Directory :

  - La création de boîtes aux lettres, d’utilisateurs à extension messagerie, de groupes de distributions et d’autres principaux de sécurité est supprimée des outils de gestion Exchange.

  - L’ajout et la suppression de membres de groupes ne peuvent pas être effectués depuis les outils de gestion Exchange.

  - Toutes les autorisations accordées au sous-système approuvé Exchange et aux serveurs Exchange pour créer des principaux de sécurité sont supprimées.

  - Les serveurs Exchange et les outils de gestion Exchange peuvent seulement modifier les attributs Exchange des principaux de sécurité existants dans Active Directory.

Par exemple, pour créer une boîte aux lettres sur laquelle les autorisations fractionnées Active Directory sont activées, un utilisateur doit d’abord être créé à l’aide des outils Active Directory par un utilisateur ayant les autorisations Active Directory requises. Ensuite, l’utilisateur peut avoir une boîte aux lettres activée à l’aide des outils de gestion Exchange. Seuls les attributs liés à Exchange de la boîte aux lettres peuvent être modifiés par les administrateurs Exchange à l’aide des outils de gestion Exchange.

Les autorisations fractionnées Active Directory sont un bon choix pour votre organisation si les conditions suivantes sont remplies :

  - Votre organisation requiert que les principaux de sécurité soit créés en utilisant uniquement les outils de gestion Active Directory ou uniquement par les utilisateurs auxquels ont été accordées des autorisations Active Directory spécifiques.

  - Vous souhaitez séparer complètement la capacité de créer des principaux de sécurité de ceux qui gèrent l’organisation Exchange.

  - Vous souhaitez effectuer toute la gestion des groupes de distribution, y compris la création de groupes de distribution et l’ajout et la suppression de membres dans ces groupes, à l’aide des outils de gestion Active Directory.

  - Vous ne souhaitez pas que les serveurs Exchange ou les programmes tiers qui utilisent Exchange en leur nom créent des principaux de sécurité.

> [!important]
> Basculer vers les autorisations fractionnées Active Directory est un choix que vous pouvez faire lorsque vous installez Exchange 2013 soit à l’aide de l’Assistant Installation, soit à l’aide du paramètre <em>ActiveDirectorySplitPermissions</em> en exécutant <code>setup.exe</code> depuis la ligne de commande. Vous pouvez également activer ou désactiver les autorisations fractionnées Active Directory après avoir installé Exchange 2013 en exécutant à nouveau <code>setup.exe</code> dans la ligne de commande. Pour activer les autorisations fractionnées Active Directory, définissez le paramètre <em>ActiveDirectorySplitPermissions</em> sur <code>true</code>. Pour le désactiver, définissez-le sur <code>false</code>. Vous devez toujours spécifier le basculement <em>PrepareAD</em> en même temps que le paramètre <em>ActiveDirectorySplitPermissions</em>.
> Si vous possédez plusieurs domaines dans la même forêt, vous devez également spécifier le même commutateur <em>PrepareAllDomains</em> lorsque vous appliquez les autorisations fractionnées Active Directory ou exécuter le programme d’installation avec le commutateur <em>PrepareDomain</em> dans chaque domaine. Si vous choisissez d’exécuter le programme d’installation avec le commutateur <em>PrepareDomain</em> dans chaque domaine plutôt que d’utiliser le commutateur <em>PrepareAllDomains</em>, vous devez préparer chaque domaine contenant les serveurs Exchange, les objets à extension messagerie ou les serveurs de catalogue global accessibles via un serveur Exchange.


> [!important]
> Vous ne pouvez pas activer les autorisations fractionnées Active Directory si vous avez installé Exchange 2010 ou Exchange 2013 sur un contrôleur de domaine.
> Après avoir activé ou désactivé les autorisations fractionnées Active Directory, il est conseillé de redémarrer les serveurs Exchange 2010 et Exchange 2013 de votre organisation pour les obliger à sélectionner le nouveau jeton d’accès Active Directory avec les autorisations mises à jour.


Exchange 2013 obtient les autorisations fractionnées Active Directory en supprimant les autorisations et les appartenances du groupe de sécurité Autorisations Exchange Windows. Ce groupe de sécurité, en autorisations partagées et en autorisations fractionnées RBAC, est autorisé à beaucoup d’objets et d’attributs ne faisant pas partie d’Exchange à travers Active Directory. En supprimant les autorisations et les appartenances à ce groupe de sécurité, les administrateurs et services Exchange ne peuvent plus créer ou modifier ces objets n’appartenant pas à ExchangeActive Directory.

Pour obtenir la liste des modifications qui sont effectuées sur le groupe de sécurité Autorisations Exchange Windows et sur d’autres composants Exchange lorsque vous activez ou désactivez les autorisations fractionnées Active Directory, consultez le tableau suivant.

> [!NOTE]
> Les attributions de rôle aux groupes de rôles qui permettent aux administrateurs Exchange de créer des principaux de sécurité sont supprimées lorsque les autorisations fractionnées Active Directory sont activées. Cela est effectué pour supprimer l’accès aux cmdlets qui généreraient une erreur lorsqu’elles seraient exécutées car elles n’ont pas les autorisations de créer l’objet Active Directory associé.


### Modifications d’autorisations fractionnées Active Directory

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Action</th>
<th>Modifications apportées par Exchange</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Activer les autorisations fractionnées Active Directory lors de la première installation du serveur Exchange 2013</p></td>
<td><p>Les actions suivantes se produisent lorsque vous activez les autorisations fractionnées Active Directory soit à l’aide de l’assistant Installation soit en exécutant <code>setup.exe</code> avec les paramètres <code>/PrepareAD</code> et <code>/ActiveDirectorySplitPermissions:true</code> :</p>
<ul>
<li><p>Une unité d’organisation (OU) appelée <strong>Groupes de protection de Microsoft Exchange</strong> est créée.</p></li>
<li><p>Le groupe de sécurité <strong>Autorisations Windows Exchange</strong> est créé dans l’OU <strong>Groupes protégés Microsoft Exchange</strong>.</p></li>
<li><p>Le groupe de sécurité <strong>Sous-système approuvé Exchange</strong> n’est pas ajouté au groupe de sécurité <strong>Autorisations Windows Exchange</strong>.</p></li>
<li><p>La création d’attributions de rôles de gestion sans délégation aux rôles de gestion avec les types de rôles de gestion suivants est ignorée :</p>
<ul>
<li><p><code>MailRecipientCreation</code></p></li>
<li><p><code>SecurityGroupCreationandMembership</code></p></li>
</ul></li>
<li><p>Les entrées de contrôle d’accès (ACE) qui auraient été attribuées au groupe de sécurité <strong>Autorisations Windows Exchange</strong> ne sont pas ajoutées à l’objet de domaine Active Directory.</p></li>
</ul>
<p>Si vous exécutez le programme d’installation avec le commutateur <em>PrepareAllDomains</em> ou <em>PrepareDomain</em>, l’événement suivant se produit dans chaque domaine enfant qui est préparé :</p>
<ul>
<li><p>Toutes les ACE attribuées au groupe de sécurité <strong>Autorisations Windows Exchange</strong> sont supprimées de l’objet du domaine.</p></li>
<li><p>Les entrées de contrôle d’accès (ACE) sont paramétrées dans chaque domaine, à l’exception des éventuelles ACE affectées au groupe de sécurité <strong>Autorisations Windows Exchange</strong>.</p></li>
</ul>
<p></p></td>
</tr>
<tr class="even">
<td><p>Passer d’autorisations partagées ou d’autorisations fractionnées RBAC à des autorisations fractionnées Active Directory</p></td>
<td><p>Les actions suivantes se produisent lorsque vous exécutez la commande <code>setup.exe</code> avec les paramètres <code>/PrepareAD</code> et <code>/ActiveDirectorySplitPermissions:true</code> :</p>
<ul>
<li><p>Une OU appelée <strong>Groupes protégés Microsoft Exchange</strong> est créée.</p></li>
<li><p>Le groupe de sécurité <strong>Autorisations Windows Exchange</strong> est déplacé vers l’OU <strong>Groupes protégés Microsoft Exchange</strong>.</p></li>
<li><p>Le groupe de sécurité <strong>Sous-système approuvé Exchange</strong> est supprimé du groupe de sécurité <strong>Autorisations Windows Exchange</strong>.</p></li>
<li><p>Toute attribution de rôles sans délégation aux rôles de gestion avec les types de rôles suivants est supprimée :</p>
<ul>
<li><p><code>MailRecipientCreation</code></p></li>
<li><p><code>SecurityGroupCreationandMembership</code></p></li>
</ul></li>
<li><p>Toutes les ACE attribuées au groupe de sécurité <strong>Autorisations Windows Exchange</strong> sont supprimées de l’objet du domaine.</p></li>
</ul>
<p>Si vous exécutez le programme d’installation avec le commutateur <em>PrepareAllDomains</em> ou <em>PrepareDomain</em>, l’événement suivant se produit dans chaque domaine enfant qui est préparé :</p>
<ul>
<li><p>Toutes les ACE attribuées au groupe de sécurité <strong>Autorisations Windows Exchange</strong> sont supprimées de l’objet du domaine.</p></li>
<li><p>Les entrées de contrôle d’accès (ACE) sont paramétrées dans chaque domaine, à l’exception des éventuelles ACE affectées au groupe de sécurité <strong>Autorisations Windows Exchange</strong>.</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Passer d’autorisations fractionnées Active Directory à des autorisations partagées ou des autorisations fractionnées RBAC</p></td>
<td><p>Les actions suivantes se produisent lorsque vous exécutez la commande <code>setup.exe</code> avec les paramètres <code>/PrepareAD</code> et <code>/ActiveDirectorySplitPermissions:false</code> :</p>
<ul>
<li><p>Le groupe de sécurité <strong>Autorisations Windows Exchange</strong> est déplacé vers l’OU <strong>Groupes de sécurité de Microsoft Exchange</strong>.</p></li>
<li><p>L’OU <strong>Groupes protégés Microsoft Exchange</strong> est supprimée.</p></li>
<li><p>Le groupe de sécurité <strong>Sous-systèmes approuvés Exchange</strong> est ajouté au groupe de sécurité <strong>Autorisations Windows Exchange</strong>.</p></li>
<li><p>Les ACE sont ajoutées à l’objet du domaine pour le groupe de sécurité <strong>Autorisations Windows Exchange</strong>.</p></li>
</ul>
<p>Si vous exécutez le programme d’installation avec le commutateur <em>PrepareAllDomains</em> ou <em>PrepareDomain</em>, l’événement suivant se produit dans chaque domaine enfant qui est préparé :</p>
<ul>
<li><p>Les ACE sont ajoutées à l’objet du domaine pour le groupe de sécurité <strong>Autorisations Windows Exchange</strong>.</p></li>
<li><p>Les ACE sont paramétrées dans chaque domaine, y compris les ACE affectées au groupe de sécurité <strong>Autorisations Windows Exchange</strong>.</p></li>
</ul>
<p>Les attributions de rôles pour les rôles Création du destinataire de messagerie, Création du groupe de sécurité et Appartenance ne sont pas créées automatiquement lors du passage d’autorisations fractionnées Active Directory à des autorisations partagées. Si des attributions de rôle de délégation ont été personnalisées avant l’activation des autorisations fractionnées Active Directory, ces personnalisations restent intactes. Pour créer des attributions de rôles entre ces rôles et le groupe de rôles Gestion de l’organisation, voir <a href="configure-exchange-2013-for-shared-permissions-exchange-2013-help.md">Configurer Exchange 2013 pour les autorisations partagées</a>.</p></td>
</tr>
</tbody>
</table>


Après avoir activé les autorisations fractionnées Active Directory, les cmdlets suivantes ne sont plus disponibles :

  - **New-Mailbox**

  - **New-MailContact**

  - **New-MailUser**

  - **New-RemoteMailbox**

  - **Remove-Mailbox**

  - **Remove-MailContact**

  - **Remove-MailUser**

  - **Remove-RemoteMailbox**

Après avoir activé les autorisations divisées Active Directory, les cmdlets suivantes sont accessibles mais vous ne pouvez pas les utiliser pour créer des groupes de distribution ni pour modifier l’appartenance au groupe de distribution :

  - **Add-DistributionGroupMember**

  - **New-DistributionGroup**

  - **Remove-DistributionGroup**

  - **Remove-DistributionGroupMember**

  - **Update-DistributionGroupMember**

Certaines cmdlets, bien que toujours disponibles, ne peuvent proposer que des fonctionnalités limitées lorsqu’elles sont utilisées avec les autorisations fractionnées Active Directory. En effet, elles peuvent vous permettre de configurer les objets destinataires qui sont dans la partition Active Directory du domaine et les objets de configuration Exchange qui sont dans la partition Active Directory de configuration. Elles peuvent également vous permettre de configurer les attributs relatifs à Exchange sur les objets stockés dans la partition de domaine. Les tentatives d’utiliser les cmdlets pour créer des objets ou modifier les attributs non relatifs à Exchange sur les objets dans la partition de domaine, généreront une erreur. Par exemple, la cmdlet **Add-ADPermission** renverra une erreur si vous tentez d’ajouter des autorisations à une boîte aux lettres. Cependant, la cmdlet **Add-ADPermission** aboutira si vous configurez les autorisations sur un connecteur de réception. En effet, une boîte aux lettres est stockée dans la partition de domaine alors que les connecteurs de réception sont stockés dans la partition de configuration.

De plus, les fonctionnalités associées dans le Centre d’administration Exchange et Outlook Web App, telles que l’Assistant Nouvelle boîte aux lettres, ne seront plus disponibles ou généreront une erreur si vous tentez de les utiliser.

Toutefois, les administrateurs Exchange pourront créer et gérer des objets spécifiques à Exchange, tels que les règles de transport, etc.

Pour plus d’informations sur la configuration d’un modèle d’autorisations fractionnées Active Directory, voir [Configurer Exchange 2013 pour les autorisations divisées](configure-exchange-2013-for-split-permissions-exchange-2013-help.md).

Retour au début

