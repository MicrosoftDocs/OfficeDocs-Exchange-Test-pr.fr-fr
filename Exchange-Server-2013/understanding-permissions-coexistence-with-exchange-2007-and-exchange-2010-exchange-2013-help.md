---
title: 'Présentation de la coexistence des autorisations dans Exchange 2007 et Exchange 2010: Exchange 2013 Help'
TOCTitle: Présentation de la coexistence des autorisations dans Exchange 2007 et Exchange 2010
ms:assetid: 28ab1433-23ee-4914-8f21-9a32578792e5
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dd335157(v=EXCHG.150)
ms:contentKeyID: 54915099
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Présentation de la coexistence des autorisations dans Exchange 2007 et Exchange 2010

 

_**Sapplique à :** Exchange Server 2010 Service Pack 2 (SP2), Exchange Server 2013_

_**Dernière rubrique modifiée :** 2015-04-07_

Quand vous installez Microsoft Exchange Server 2013 dans une organisation Microsoft Exchange Server 2010 ou Microsoft Exchange Server 2007 existante, vous devez comprendre le fonctionnement des autorisations dans la nouvelle organisation. Consultez la section ci-dessous qui s'applique à votre organisation.

  - Installation d'Exchange 2013 dans une organisation Exchange 2010 existante

  - Installation d'Exchange 2013 dans une organisation Exchange 2007 existante

## Installation d'Exchange 2013 dans une organisation Exchange 2010 existante

Exchange 2013 utilise le même modèle d’autorisations de contrôle d’accès en fonction du rôle (RBAC) que celui utilisé dans Exchange 2010. Quand vous installez Exchange 2013 dans une organisation Exchange 2010 existante, les mêmes groupes de rôles de gestion, rôles de gestion et étendues de gestion s'appliquent aux serveurs et destinataires Exchange 2013 et Exchange 2010. Les membres des groupes de rôles, les utilisateurs affectés à des rôles, peuvent administrer un serveur ou un destinataire Exchange 2013 ou Exchange 2013 qui est inclus dans l’étendue du groupe de rôles ou du rôle. Si vous n'utilisez pas d'étendues au sein de votre organisation et si vous souhaitez que les membres de vos groupes de rôles existants puissent gérer les serveurs et les destinataires Exchange 2010 et Exchange 2013, aucune action supplémentaire n'est nécessaire. Ces administrateurs seront en mesure de gérer les serveurs et les destinataires Exchange 2013 ajoutés à l'organisation. Si vous souhaitez consulter un rappel sur le fonctionnement des autorisations dans Exchange 2010 et Exchange 2013, consultez la rubrique [Autorisations](permissions-exchange-2013-help.md).

Dans la nouvelle organisation, vous souhaitez peut-être séparer la gestion des serveurs et des destinataires Exchange 2010 et Exchange 2013. Vous pouvez interdire la gestion des serveurs et des destinataires Exchange 2013 au groupe d'administrateurs chargés de la gestion des serveurs et des destinataires Exchange 2010 et vice-versa. Dans ce cas, les étendues de gestion permettent de définir les serveurs et les destinataires que chaque groupe d'administrateurs peut gérer. Après avoir créé les étendues souhaitées, vous pouvez copier des groupes de rôles existants, ajouter des administrateurs dans chaque groupe, puis ajouter les étendues à ces groupes de rôles. Quand vous avez terminé, les membres de chaque groupe de rôles ne pourront gérer que les serveurs et les destinataires qui correspondent à leur étendue respective.

Pour plus d'informations sur les groupes de rôles, les étendues, la copie de groupes de rôles et l'ajout d'étendues à des groupes de rôles, consultez les rubriques suivantes :

  - [Gérer des groupes de rôles](manage-role-groups-exchange-2013-help.md)

  - [Créer une étendue normale ou exclusive](create-a-regular-or-exclusive-scope-exchange-2013-help.md)

  - [Présentation des groupes de rôles de gestion](understanding-management-role-groups-exchange-2013-help.md)

  - [Présentation des portées du rôle de gestion](understanding-management-role-scopes-exchange-2013-help.md)

## Installation d'Exchange 2013 dans une organisation Exchange 2007 existante

Exchange 2013 inclut les autorisations de contrôle d'accès en fonction du rôle (RBAC) qui remplacent le modèle d'autorisation basé sur les entrées de contrôle d'accès (ACE) Active Directory utilisé dans Microsoft Exchange Server 2007. RBAC est le mécanisme d'autorisation utilisé pour la plupart des tâches de gestion d'Exchange 2013. Ce mécanisme couvre les domaines de gestion suivants :

  - Environnement de ligne de commande Exchange Management Shell

  - Centre d'administration Exchange (CAE)

  - Services web Exchange

Pour plus d'informations sur la planification de la coexistence entre Exchange 2013 et Exchange 2007, consultez la rubrique [Mise à niveau d'Exchange 2007 vers Exchange 2013](upgrade-from-exchange-2007-to-exchange-2013-exchange-2013-help.md).

Souhaitez-vous rechercher les tâches de gestion liées aux autorisations ? Consultez la rubrique [Autorisations](permissions-exchange-2013-help.md).

## Autorisations Exchange 2013

Le modèle d'autorisations RBAC d'Exchange 2013 se caractérise par des groupes de rôles de gestion auxquels sont attribués un ou plusieurs rôles de gestion. Les rôles de gestion contiennent des autorisations qui permettent aux administrateurs de réaliser diverses tâches dans l'organisation Exchange. Les administrateurs sont ajoutés en tant que membres des groupes de rôles et se voient accorder toutes les autorisations inhérentes aux rôles. Le tableau ci-après fournit un exemple décrivant les groupes de rôles, certains rôles qui leur sont attribués et le type d'utilisateur susceptible d'être membre du groupe de rôles.

### Exemples de groupes de rôles et de rôles dans Exchange 2013

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Groupe de rôles de gestion</th>
<th>Rôles de gestion</th>
<th>Membres de ce groupe de rôles</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Gestion de l’organisation</p></td>
<td><p>Voici quelques-uns des rôles affectés à ce groupe de rôles :</p>
<ul>
<li><p>Listes d'adresses</p></li>
<li><p>Exchange Servers</p></li>
<li><p>Journalisation</p></li>
<li><p>Destinataires de message</p></li>
<li><p>Dossiers publics</p></li>
</ul></td>
<td><p>Les utilisateurs chargés de gérer l'organisation Exchange 2013 entière doivent être membres de ce groupe. À quelques exceptions près, les membres de ce groupe de rôles peuvent gérer quasiment tous les aspects de l'organisation Exchange 2013.</p>
<p>Par défaut, le compte d'utilisateur servant à la préparation d'Active Directory pour Exchange 2013 est membre de ce groupe de rôles.</p>
<p>Pour obtenir des informations détaillées sur ce groupe de rôles, ainsi qu'une liste complète des rôles qui lui sont attribués, consultez la rubrique <a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a>.</p></td>
</tr>
<tr class="even">
<td><p>Afficher uniquement la gestion de l’organisation</p></td>
<td><p>Les rôles suivants sont affectés à ce groupe de rôles :</p>
<ul>
<li><p>Analyse</p></li>
<li><p>Afficher uniquement la configuration</p></li>
<li><p>Afficher uniquement les destinataires</p></li>
</ul></td>
<td><p>Les utilisateurs qui consultent la configuration de l'organisation Exchange 2013 entière doivent être membres de ce groupe. Ces utilisateurs doivent pouvoir afficher la configuration du serveur et les informations sur les destinataires. Ils doivent également être capables de réaliser des fonctions d'analyse sans qu'il soit possible de modifier la configuration de l'organisation ou des destinataires.</p>
<p>Pour plus d'informations sur ce groupe de rôles, consultez la rubrique <a href="view-only-organization-management-exchange-2013-help.md">Gestion de l’organisation en affichage seul</a>.</p></td>
</tr>
<tr class="odd">
<td><p>Gestion des destinataires</p></td>
<td><p>Les rôles suivants sont attribués à ce groupe de rôles :</p>
<ul>
<li><p>Groupes de distribution</p></li>
<li><p>Dossiers publics à extension messagerie</p></li>
<li><p>Création de destinataires de message</p></li>
<li><p>Destinataires de message</p></li>
<li><p>Suivi de messages</p></li>
<li><p>Migration</p></li>
<li><p>Déplacement de boîtes aux lettres</p></li>
<li><p>Stratégies de destinataire</p></li>
</ul></td>
<td><p>Les utilisateurs chargés de gérer des destinataires dans l'organisation Exchange 2013, notamment des boîtes aux lettres, des contacts et des groupes de distribution, doivent être membres de ce groupe de rôles. Ces utilisateurs peuvent créer des destinataires, modifier ou supprimer des destinataires existants ou encore déplacer des boîtes aux lettres.</p>
<p>Pour obtenir des informations détaillées sur ce groupe de rôles, ainsi qu'une liste complète des rôles qui lui sont attribués, consultez la rubrique <a href="recipient-management-exchange-2013-help.md">Gestion des destinataires</a>.</p></td>
</tr>
<tr class="even">
<td><p>Gestion du serveur</p></td>
<td><p>Voici quelques-uns des rôles attribués à ce groupe de rôles :</p>
<ul>
<li><p>Bases de données</p></li>
<li><p>Connecteurs Exchange</p></li>
<li><p>Serveurs Exchange</p></li>
<li><p>Connecteurs de réception</p></li>
<li><p>Files d'attente de transport</p></li>
</ul></td>
<td><p>Les utilisateurs qui gèrent la configuration du serveur Exchange, notamment des connecteurs de réception, des certificats, des bases de données et des répertoires virtuels, doivent être membres de ce groupe de rôles. Ils peuvent modifier la configuration du serveur Exchange, créer des bases de données et redémarrer et manipuler des files d'attente de transport.</p>
<p>Pour obtenir des informations détaillées sur ce groupe de rôles, ainsi qu'une liste complète des rôles qui lui sont attribués, consultez la rubrique <a href="server-management-exchange-2013-help.md">Gestion du serveur</a>.</p></td>
</tr>
<tr class="odd">
<td><p>Gestion de la découverte</p></td>
<td><p>Les rôles suivants sont attribués à ce groupe de rôles :</p>
<ul>
<li><p>Conservation légale</p></li>
<li><p>Recherche de boîte aux lettres</p></li>
</ul></td>
<td><p>Les utilisateurs qui effectuent des recherches de boîtes aux lettres pour des actes de procédure ou qui configurent des conservations légales, doivent être membres de ce groupe de rôles.</p>
<p>Voici un exemple de groupe de rôles susceptible de contenir des administrateurs non Exchange (par exemple, le personnel du service juridique). Le personnel juridique peut accomplir ses tâches sans l'intervention d'administrateurs Exchange.</p>
<p>Pour obtenir des informations détaillées sur ce groupe de rôles, ainsi qu'une liste complète des rôles qui lui sont attribués, consultez la rubrique <a href="discovery-management-exchange-2013-help.md">Gestion de la détection</a>.</p></td>
</tr>
</tbody>
</table>


Ce tableau montre qu'Exchange 2013 offre un niveau de contrôle plus détaillé des autorisations que vous accordez à vos administrateurs. Vous pouvez choisir parmi 12 groupes de rôles différents dans Exchange 2013. Pour obtenir une liste complète des groupes de rôles et des autorisations accordées, consultez la rubrique [Groupes de rôles intégrés](built-in-role-groups-exchange-2013-help.md).

Parce qu'Exchange 2013 inclut de nombreux groupes de rôles et qu'une personnalisation supplémentaire est possible en créant des groupes de rôles avec différentes combinaisons de rôles, la manipulation des listes de contrôle d'accès (ACL) avec des objets Active Directory n'est désormais plus nécessaire et n'aura aucune incidence. Les listes de contrôle d'accès ne sont plus employées pour appliquer des autorisations à des administrateurs individuels ou des groupes dans Exchange 2013. Toutes les tâches, notamment la création d'une boîte aux lettres par un administrateur ou l'accès d'un utilisateur à une boîte aux lettres, sont gérées via le contrôle d'accès basé sur un rôle (RBAC). Le contrôle d'accès basé sur un rôle (RBAC) autorise la tâche, puis Exchange l'exécute pour le compte de l'utilisateur s'il est autorisé. Exchange exécute la tâche dans le groupe universel de sécurité du sous-système approuvé Exchange. À quelques exceptions près, toutes les listes de contrôle d'accès dans des objets Active Directory auxquels Exchange 2010 doit accéder sont autorisées dans le groupe universel de sécurité du sous-système approuvé Exchange. Cet aspect change fondamentalement le mode de gestion des autorisations dans Exchange 2007.

Les autorisations accordées à un utilisateur dans Active Directory sont distinctes des autorisations accordées à l'utilisateur par le contrôle d'accès en fonction du rôle (RBAC) quand l'utilisateur en question fait appel aux outils de gestion Exchange 2013.

Pour plus d'informations sur le contrôle d'accès basé sur un rôle (RBAC), consultez la rubrique [Présentation du contrôle d'accès basé sur un rôle](understanding-role-based-access-control-exchange-2013-help.md).

## Autorisations Exchange 2007

Le modèle administratif d'Exchange 2007 exploite les forêts Active Directory pour définir des limites de sécurité. Aucune autorisation de sécurité n'est isolée dans une forêt particulière. Les propriétaires de forêts et les administrateurs d'entreprise peuvent toujours accéder à l'ensemble des ressources d'un domaine. Dans Exchange 2007, vous devrez éventuellement accorder des droits d'administrateur d'entreprise et de domaine de niveau supérieur uniquement de façon temporaire.

Exchange 2007 fournit les rôles d'administrateur prédéfinis suivants :

  - **Rôle Administrateur de l'organisation Exchange**   Ce rôle accorde des autorisations pour contrôler tous les aspects de l'organisation Exchange 2007. De plus, un administrateur exerçant ce rôle peut octroyer des autorisations à d'autres administrateurs Exchange. Ce rôle est affecté au compte que vous utilisez pour installer Exchange 2007.

  - **Rôle Administrateur Exchange Affichage seul**   Ce rôle accorde des autorisations pour afficher la configuration d'Exchange. Toutefois, un administrateur auquel ce rôle a été affecté ne peut pas modifier des objets dans l'organisation Exchange 2007.

  - **Rôle Administrateur des destinataires Exchange**   Ce rôle accorde des autorisations pour gérer les destinataires de messages électroniques. Un administrateur exerçant ce rôle peut modifier des éléments liés à Exchange pour les utilisateurs, les groupes, les contacts et les groupes de distribution.

  - **Rôle Administrateur Exchange Server**   Ce rôle accorde des autorisations pour gérer un serveur spécifique. Cependant, ce rôle n'octroie pas d'autorisations pour effectuer des actions ayant un impact global sur l'organisation Exchange 2007.

  - **Rôle Administrateur de dossiers publics Exchange**   Ce rôle a été ajouté à Exchange 2007 Service Pack 1**.** Il accorde des autorisations pour gérer des dossiers publics dans l'organisation Exchange 2007.

Ce modèle d'autorisations utilise les groupes universels de sécurité (USG) pour tous les rôles, à l'exception du rôle d'administrateur d'Exchange Server. Quand vous exécutez la commande Exchange 2007**Setup /PrepareAD**, le programme d'installation crée les groupes universels de sécurité dans le domaine racine et leur confère une étendue englobant la forêt entière. Des listes de contrôle d'accès sont affectées aux groupes universels de sécurité pour gérer les objets Exchange dans Active Directory.

Dans Exchange 2007, vous pouvez différencier les administrateurs en leur attribuant divers rôles. Les autorisations sont affectées directement à l'utilisateur ou au groupe universel de sécurité dont l'utilisateur est membre. Toutes les actions de l'utilisateur sont entreprises dans le cadre de son compte Active Directory. Le tableau ci-après répertorie les rôles d'administrateur Exchange 2007 ainsi que les autorisations Exchange correspondantes.

### Rôles d'administrateur Exchange 2007

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Rôle d'administrateur</th>
<th>Membres</th>
<th>Membre de</th>
<th>Autorisations Exchange</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Administrateur de l'organisation Exchange</p></td>
<td><p>Compte d'administrateur ou compte utilisé pour installer le premier serveur Exchange 2007</p></td>
<td><p>Administrateur des destinataires Exchange</p>
<p>Groupe local d'administrateurs de <em>&lt;nom de serveur&gt;</em></p></td>
<td><p>Contrôle total du conteneur Microsoft Exchange dans Active Directory</p></td>
</tr>
<tr class="even">
<td><p>Administrateur Affichage seul d'Exchange</p></td>
<td><p>Administrateurs des destinataires Exchange</p>
<p>Administrateurs Exchange Server (<em>&lt;nom de serveur</em>&gt;)</p></td>
<td><p>Administrateurs des destinataires Exchange</p>
<p>Administrateurs Exchange Server</p></td>
<td><p>Accès en lecture au conteneur Microsoft Exchange dans Active Directory.</p>
<p>Accès en lecture à tous les domaines Windows ayant des destinataires Exchange</p></td>
</tr>
<tr class="odd">
<td><p>Administrateur des destinataires Exchange</p></td>
<td><p>Administrateurs de l'organisation Exchange</p></td>
<td><p>Administrateurs Exchange Affichage seul</p></td>
<td><p>Contrôle total des propriétés Exchange sur les objets utilisateur Active Directory</p></td>
</tr>
<tr class="even">
<td><p>Administrateur Exchange Server</p></td>
<td><p>Administrateurs de l'organisation Exchange</p></td>
<td><p>Administrateurs Affichage seul d'Exchange</p>
<p>Groupe local d'administrateurs de <em>&lt;nom de serveur</em>&gt;</p></td>
<td><p>Contrôle total de Exchange <em>&lt;nom de serveur</em>&gt;</p></td>
</tr>
<tr class="odd">
<td><p>Exchange Server</p></td>
<td><p>Chaque compte d'ordinateur Exchange 2007</p></td>
<td><p>Administrateurs Affichage seul d'Exchange</p></td>
<td><p>Spécial</p></td>
</tr>
<tr class="even">
<td><p>Administrateur de dossiers publics Exchange</p></td>
<td><p>Administrateurs de l'organisation Exchange</p></td>
<td><p>Administrateurs Affichage seul d'Exchange</p></td>
<td><p>Contrôle total de la gestion de tous les dossiers publics (droit étendu de création d'un dossier public de premier niveau accordé)</p></td>
</tr>
</tbody>
</table>


Si vous souhaitez créer des affectations d'autorisations à un niveau plus détaillé, vous pouvez modifier les listes de contrôle d'accès sur des objets Exchange 2007 individuels, tels que des listes d'adresses ou des bases de données. Vous devez ajouter le groupe d'utilisateurs ou de sécurité dont l'utilisateur est membre directement à la liste de contrôle d'accès. Ensuite, les actions sont exécutées dans le contexte de l'utilisateur particulier.

Pour plus d'informations sur la procédure de gestion des autorisations dans Exchange 2007, consultez la page [Configuration des autorisations dans Exchange Server 2007](http://go.microsoft.com/fwlink/p/?linkid=90671).

## Coexistence des autorisations dans Exchange 2013 et Exchange 2007

Étant donné que les modèles d'autorisations d'Exchange 2013 et d'Exchange 2007 sont différents, les attributions d'autorisations Exchange 2013 sont distinctes de celles d'Exchange 2007. Ce principe vaut même si les deux versions d'Exchange sont installées dans la même forêt. Sans configuration supplémentaire, les administrateurs Exchange 2013 ne disposent pas des autorisations requises pour gérer des serveurs Exchange 2007 et les administrateurs Exchange 2007 ne disposent pas des autorisations requises pour gérer des serveurs Exchange 2013. Vous devez réfléchir aux questions suivantes :

  - Souhaitez-vous accorder aux administrateurs Exchange 2013 le droit de gérer des serveurs Exchange 2007 ?

  - Souhaitez-vous accorder aux administrateurs Exchange 2007 le droit de gérer des serveurs Exchange 2013 ?

  - Souhaitez-vous personnaliser les autorisations Exchange 2013 pour les rendre compatibles avec toutes les autorisations que vous avez définies dans les listes de contrôle d'accès Exchange 2007 ?

## Octroi d'autorisations Exchange 2013 à des administrateurs Exchange 2007

Si vous souhaitez que les administrateurs Exchange 2007 gèrent des serveurs Exchange 2013, vous devez ajouter les administrateurs Exchange 2007 en tant que membres d'un ou de plusieurs groupes de rôles Exchange 2013. Vous pouvez ajouter soit des utilisateurs, soit des groupes universels de sécurité à des groupes de rôles. Les autorisations accordées aux groupes de rôles sont ensuite appliquées aux utilisateurs ou aux groupes universels de sécurité que vous avez ajoutés en tant que membres.

> [!IMPORTANT]
> Si vous utilisez des groupes de sécurité Active Directory globaux ou de domaine local, vous devez les redéfinir en tant que groupes universels de sécurité si votre intention est de les ajouter comme membres d'un groupe de rôles Exchange 2013. Exchange 2013 prend uniquement en charge les groupes universels de sécurité.


Le tableau suivant décrit le mappage entre les rôles d'administrateur Exchange 2007 et les groupes de rôles Exchange 2013.

### Rôles d'administrateur Exchange 2007 et groupes de rôles Exchange 2010

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Rôle d'administrateur Exchange 2007</th>
<th>Groupe de rôles Exchange 2013</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Administrateur de l'organisation Exchange</p></td>
<td><p>Gestion de l’organisation</p></td>
</tr>
<tr class="even">
<td><p>Administrateur des destinataires Exchange</p></td>
<td><p>Gestion des destinataires</p></td>
</tr>
<tr class="odd">
<td><p>Administrateur Exchange Server</p></td>
<td><p>Gestion du serveur</p></td>
</tr>
<tr class="even">
<td><p>Administrateur Affichage seul d'Exchange</p></td>
<td><p>Afficher uniquement la gestion de l’organisation</p></td>
</tr>
<tr class="odd">
<td><p>Exchange Server</p></td>
<td><p>Aucun groupe de rôles équivalent dans Exchange 2013</p>
<p>(Pour plus d'informations sur la création de groupes de rôles personnalisés, consultez la rubrique <a href="manage-role-groups-exchange-2013-help.md">Gérer des groupes de rôles</a>.)</p></td>
</tr>
<tr class="even">
<td><p>Administrateur de dossiers publics Exchange</p></td>
<td><p>Gestion des dossiers publics</p></td>
</tr>
</tbody>
</table>


Si tous vos administrateurs Exchange 2007 sont des membres de l'un des trois rôles administratifs d'Exchange 2007, vous pouvez ajouter les membres de chaque groupe d'administration à leur groupe de rôles Exchange 2013 équivalent. Par exemple, pour accorder à tous les administrateurs de l'organisation Exchange 2007 un accès total aux objets Exchange 2013, ajoutez le groupe universel de sécurité des administrateurs de l'organisation Exchange au groupe de rôles Gestion de l’organisation.

Pour plus d'informations sur l'ajout d'utilisateurs et de groupes universels de sécurité à des groupes de rôles, consultez la rubrique [Gérer les membres de groupes de rôles](manage-role-group-members-exchange-2013-help.md).

Si vous modifiez des listes de contrôle d'accès dans des objets Exchange 2007 pour accorder des autorisations plus granulaires à des administrateurs Exchange 2007 et si vous souhaitez leur accorder des autorisations similaires pour des serveurs Exchange 2013, procédez comme suit :

1.  Examinez les personnalisations des listes de contrôle d'accès qui ont été effectuées dans les objets Exchange 2007 et recherchez les administrateurs auxquels des autorisations ont été accordées pour chaque objet.

2.  Classez chaque objet Exchange 2007. Par exemple, déterminez si l'objet est une base de données, un serveur ou un objet de destinataire.

3.  Mappez les objets sur le groupe de rôles Exchange 2013 correspondant. Pour obtenir une liste des groupes de rôles intégrés, consultez la rubrique [Groupes de rôles intégrés](built-in-role-groups-exchange-2013-help.md).

4.  Ajoutez les utilisateurs ou les groupes universels de sécurité pour chaque type d'objet aux groupes de rôles Exchange 2013 correspondants. Pour plus d'informations sur l'ajout d'utilisateurs et de groupes universels de sécurité à des groupes de rôles, consultez la rubrique [Gérer les membres de groupes de rôles](manage-role-group-members-exchange-2013-help.md).

Une fois ces étapes terminées, les administrateurs Exchange 2007 seront membres du groupe de rôles spécifique qui est mappé aux objets Exchange 2013 appropriés. Les administrateurs Exchange 2007 peuvent faire appel aux outils de gestion Exchange 2013 pour gérer les serveurs et les destinataires Exchange 2013.

> [!IMPORTANT]
> En règle générale, la gestion des serveurs et des destinataires Exchange 2007 doit être effectuée au moyen des outils de gestion Exchange 2007. En revanche, celle des serveurs et des destinataires Exchange 2013 doit être accomplie à l'aide des outils de gestion Exchange 2013.


Si les groupes de rôles intégrés ne vous procurent pas l'ensemble précis des autorisations que vous souhaitez accorder à certains administrateurs, vous pouvez créer des groupes de rôles personnalisés. Lorsque vous créez un groupe de rôle personnalisé, vous pouvez choisir les rôles que vous souhaitez y ajouter. Vous pouvez définir les fonctionnalités spécifiques dont vous souhaitez confier la gestion aux membres du groupe de rôles. Par exemple, si vous voulez que seuls les administrateurs gèrent les groupes de distribution, créez un groupe de rôles personnalisé, puis sélectionnez uniquement le rôle Groupes de distribution. Les membres de ce groupe de rôles personnalisé ne pourront plus alors gérer que des groupes de distribution. Pour plus d'informations sur la création de groupes de rôles personnalisés, consultez la rubrique [Gérer des groupes de rôles](manage-role-groups-exchange-2013-help.md).

Si vous accordez des autorisations sélectives pour certains objets Exchange 2007 (par exemple, vous autorisez les administrateurs à gérer seulement des bases de données spécifiques), et si vous souhaitez appliquer la même configuration à vos serveurs Exchange 2013, consultez la section « Recréation de la personnalisation des listes de contrôle d'accès Exchange 2007 à l'aide d'étendues de gestion dans Exchange 2013 » plus loin dans cette rubrique.

## Octroi d'autorisations Exchange 2007 à des administrateurs Exchange 2013

Si vous souhaitez que les administrateurs Exchange 2013 gèrent les serveurs Exchange 2007, ajoutez les administrateurs Exchange 2013 aux groupes universels de sécurité ou au groupe de sécurité qui correspond au rôle d'administrateur Exchange 2007 en question. Si vous disposez de paramètres personnalisés pour les listes de contrôle d'accès, vous pouvez également ajouter les administrateurs aux listes de contrôle d'accès appropriées. Les groupes de rôles sont des groupes universels de sécurité. Vous pouvez donc les ajouter directement aux groupes universels de sécurité du rôle d'administrateur Exchange 2007.

Une fois cette opération terminée, les administrateurs Exchange 2013 feront partie du ou des rôles d'administrateur Exchange 2007 appropriés. Les administrateurs Exchange 2013 peuvent faire appel aux outils de gestion Exchange 2007 pour gérer les serveurs et les destinataires Exchange 2007.

## Recréation de la personnalisation des listes de contrôle d'accès Exchange 2007 à l'aide d'étendues de gestion dans Exchange 2013

Dans Exchange 2007, quand vous souhaitez restreindre les personnes autorisées à gérer une banque de boîtes aux lettres spécifique ou des utilisateurs en particulier, ou bien à contrôler dans quelle banque les boîtes aux lettres sont créées, vous devez modifier les listes de contrôle d'accès dans les objets à restreindre. Exchange 2013 offre les mêmes fonctionnalités, mais n'impose pas de modifier toutes les listes de contrôle d'accès. Il utilise pour cela les étendues de gestion qui sont un composant du contrôle d'accès basé sur un rôle (RBAC).

Les étendues de gestion fournissent des étendues intégrées et personnalisées pour définir les objets pouvant être gérés par les administrateurs. En appliquant des étendues de gestion, vous pouvez définir les destinataires à administrer, les bases de données de boîtes aux lettres dans lesquelles les boîtes aux lettres peuvent être créées, ainsi que les destinataires ou les serveurs dont la gestion sera confiée à un petit groupe d'administrateurs et personne d'autre.

Vous pouvez créer les types d'étendues de gestion suivants :

  - **Étendue relative prédéfinie**   Les étendues relatives prédéfinies sont disponibles dans Exchange 2013. Vous pouvez déterminer ce qu'un utilisateur peut voir et modifier. Par exemple, les étendues relatives prédéfinies permettent de déterminer si les utilisateurs voient uniquement leurs données personnelles ou les informations sur toute l'organisation.

  - **Destinataire**   Les étendues de destinataire contrôlent les destinataires qu'un administrateur peut créer, modifier ou supprimer. Elles peuvent être fondées sur une unité d'organisation, un filtre de destinataire, ou les deux. Les filtres de destinataire précisent les critères auxquels un destinataire doit répondre pour être inclus dans l'étendue. Par exemple, vous pouvez créer une étendue de filtre de destinataire qui comprend tous les utilisateurs dans un site géographique donné ou un service en particulier. Vous pouvez même combiner des unités d'organisation et des filtres de destinataire afin qu'ils correspondent uniquement à des utilisateurs d'une unité d'organisation précise travaillant sous la direction d'un responsable spécifique.

  - **Serveur**   Les étendues de serveur contrôlent les serveurs qu'un administrateur peut gérer. Vous pouvez définir des listes de serveurs ou des filtres de serveur. Les listes de serveurs permettent de définir une liste statique de serveurs qu'il est possible de gérer. Les filtres de serveur fonctionnent de la même manière que les filtres de destinataire puisqu'ils permettent de définir des critères de correspondance. Par exemple, vous pouvez créer une étendue de serveur qui correspond à tous les serveurs sur un site Active Directory en particulier.

  - **Base de données**   Les étendues de base de données contrôlent les bases de données qu'un administrateur peut gérer. Elles peuvent aussi déterminer les bases de données dans lesquelles il est possible de créer ou de déplacer des boîtes aux lettres. Tout comme les étendues de serveur, vous pouvez les définir comme des listes ou des filtres. Par exemple, vous pouvez créer une liste ou un filtre dont les administrateurs peuvent se servir pour créer ou déplacer des boîtes aux lettres dans des bases de données de boîtes aux lettres spécifiques gérées par une filiale bien précise.

  - **Exclusif**   Vous pouvez également créer des étendues de destinataire, de serveur et de base de données sous la forme d'étendues exclusives. Les étendues exclusives fonctionnent de la même manière que les entrées de contrôle d'accès refusé dans les listes de contrôle d'accès. Si un élément quelconque correspond à une étendue exclusive, seuls les administrateurs à qui une étendue exclusive a été attribuée peuvent gérer cet objet. Cela est vrai, même si une autre étendue non exclusive correspond à ce même objet. Cette fonctionnalité est particulièrement utile lorsque vous souhaitez autoriser quelques personnes dignes de confiance à gérer la boîte aux lettres d'un responsable. Même si une autre étendue de destinataire plus large et régulière inclut la boîte aux lettres du responsable, les administrateurs à qui cette étendue régulière plus large a été attribuée ne pourront pas gérer cette boîte aux lettres, sauf si une étendue exclusive leur a également été attribuée.

Les étendues de gestion sont utilisées avec des rôles de gestion, des attributions de rôle de gestion et des groupes de rôles de gestion afin de contrôler les personnes autorisées à gérer des objets, la nature de ces objets et la manière dont ils sont stockés. Pour plus d'informations, consultez les rubriques suivantes :

  - [Présentation des portées du rôle de gestion](understanding-management-role-scopes-exchange-2013-help.md)

  - [Présentation des étendues exclusives](understanding-exclusive-scopes-exchange-2013-help.md)

  - [Présentation des attributions de rôles de gestion](understanding-management-role-assignments-exchange-2013-help.md)

  - [Présentation des groupes de rôles de gestion](understanding-management-role-groups-exchange-2013-help.md)

  - [Présentation des rôles de gestion](understanding-management-roles-exchange-2013-help.md)

Pour créer le même modèle d'autorisations dans Exchange 2013 au moyen d'étendues de gestion que vous auriez définies à l'aide de listes de contrôle d'accès personnalisées, vous devez dresser un inventaire des listes de contrôle d'accès que vous avez personnalisées, puis créer des étendues de gestion qui leur correspondent. Les propriétés filtrables disponibles dans les objets destinataire, serveur et base de données peuvent vous être utiles pour créer des étendues de gestion comprenant les objets dont chacune d'entre elles devra contrôler l'accès. Pour plus d'informations sur les propriétés à utiliser dans le cadre des étendues de gestion, consultez la rubrique [Présentation des filtres d’attribution du rôle de gestion](understanding-management-role-scope-filters-exchange-2013-help.md).

Pour plus d'informations sur la procédure de création d'étendues de gestion, consultez la rubrique [Créer une étendue normale ou exclusive](create-a-regular-or-exclusive-scope-exchange-2013-help.md).

