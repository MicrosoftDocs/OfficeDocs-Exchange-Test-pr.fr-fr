---
title: 'Création d’une étendue de gestion personnalisée pour les recherches de découverte électronique sur place: Exchange 2013 Help'
TOCTitle: Création d’une étendue de gestion personnalisée pour les recherches de découverte électronique sur place
ms:assetid: 1543aefe-3709-402c-b9cd-c11fe898aad1
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dn741464(v=EXCHG.150)
ms:contentKeyID: 62219861
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Création d’une étendue de gestion personnalisée pour les recherches de découverte électronique sur place

 

_**Sapplique à :** Exchange Online, Exchange Server 2013_

_**Dernière rubrique modifiée :** 2015-01-21_

Vous pouvez utiliser une étendue de gestion personnalisée pour permettre à des personnes ou à des groupes spécifiques d'utiliser la découverte électronique sur place pour rechercher un sous-ensemble de boîtes aux lettres dans votre organisation Exchange 2013 ou Exchange Online. Par exemple, vous pouvez permettre à un gestionnaire de découverte de rechercher uniquement les boîtes aux lettres des utilisateurs dans un emplacement ou un service spécifique. Pour cela, vous pouvez créer une étendue de gestion personnalisée. Cette étendue de gestion personnalisée utilise un filtre de destinataire pour contrôler les boîtes aux lettres qui peuvent être recherchées. Les étendues de filtre de destinataire utilisent des filtres pour cibler des destinataires spécifiques en fonction du type de destinataire ou d'autres propriétés de destinataire.

Pour la découverte électronique sur place, la seule propriété sur une boîte aux lettres d'utilisateur que vous pouvez utiliser pour créer un filtre de destinataire pour une étendue personnalisée est l'appartenance au groupe de distribution (le nom de propriété réel est *MemberOfGroup*). Si vous utilisez d'autres propriétés, telles que *CustomAttributeN*, *Department* ou *PostalCode*, la recherche échoue lorsqu'elle est exécutée par un membre du groupe de rôles auquel est affectée l'étendue personnalisée.

Pour en savoir plus sur les étendues de gestion, consultez les rubriques suivantes :

  - [Présentation des portées du rôle de gestion](understanding-management-role-scopes-exchange-2013-help.md)

  - [Présentation des filtres d’attribution du rôle de gestion](understanding-management-role-scope-filters-exchange-2013-help.md)

## Ce qu’il faut savoir avant de commencer

  - Durée d’exécution estimée : 15 minutes

  - Comme indiqué précédemment, vous pouvez utiliser uniquement l'appartenance à un groupe comme filtre de destinataire pour créer une étendue de filtre de destinataire personnalisée destinée à être utilisée pour la découverte électronique. Les autres propriétés de destinataire ne peuvent pas être utilisées pour créer une étendue personnalisée pour des recherches de découverte électronique. Notez que l'appartenance à un groupe de distribution dynamique ne peut pas être utilisée non plus.

  - Suivez les étapes 1 à 3 pour permettre à un gestionnaire de découverte d'exporter les résultats de la recherche pour une recherche de découverte électronique qui utilise une étendue de gestion personnalisée.

  - Si votre gestionnaire de découverte ne doit pas afficher l'aperçu des résultats de la recherche, vous pouvez ignorer l'étape 4.

  - Si votre gestionnaire de découverte ne doit pas copier les résultats de la recherche, vous pouvez ignorer l'étape 5.

## Étape 1 : Organiser les utilisateurs en groupes de distribution pour la découverte électronique

Pour rechercher un sous-ensemble de boîtes aux lettres dans votre organisation ou pour limiter l'étendue des boîtes aux lettres source qu'un gestionnaire de découverte peut rechercher, vous devez organiser le sous-ensemble de boîtes aux lettres en un ou plusieurs groupes de distribution. Lorsque vous créerez une étendue de gestion personnalisée à l'étape 2, vous utiliserez ces groupes de distribution comme filtre de destinataire pour créer une étendue de gestion personnalisée. Cela permet à un gestionnaire de découverte de rechercher uniquement les boîtes aux lettres des utilisateurs qui sont membres d'un groupe spécifié.

Vous pouvez peut-être utiliser des groupes de distribution existants à des fins de découverte électronique ou vous pouvez en créer. Consultez Plus d’informations à la fin de cette rubrique pour obtenir des conseils sur la façon de créer des groupes de distribution qui peuvent être utilisés pour limiter les recherches de la découverte électronique.

## Étape 2 : Créer une étendue de gestion personnalisée

Vous allez à présent créer une étendue de gestion personnalisée qui est définie par l'appartenance à un groupe de distribution (en utilisant le filtre de destinataire *MemberOfGroup*). Lorsque cette étendue est appliquée à un groupe de rôles utilisé pour la découverte électronique, les membres du groupe de rôles peuvent rechercher les boîtes aux lettres des utilisateurs qui sont membres du groupe de distribution utilisé pour créer l'étendue de gestion personnalisée.

Cette procédure utilise les commandes Exchange Management Shell pour créer une étendue personnalisée nommée Étendue de découverte électronique des utilisateurs Ottawa. Elle spécifie le groupe de distribution nommé Utilisateurs Ottawa pour le filtre de destinataire de l'étendue personnalisée.

1.  Exécutez cette commande pour obtenir et enregistrer les propriétés du groupe Utilisateurs Ottawa dans une variable, qui est utilisée dans la commande suivante.
    
        $DG = Get-DistributionGroup -Identity "Ottawa Users"

2.  Exécutez cette commande pour créer une étendue de gestion personnalisée basée sur l'appartenance au groupe de distribution des utilisateurs Ottawa.
    
        New-ManagementScope "Ottawa Users eDiscovery Scope" -RecipientRestrictionFilter "MemberOfGroup -eq '$($DG.DistinguishedName)'"
    
    Le nom distinctif du groupe de distribution, qui est contenu dans la variable **$DG**, est utilisé pour créer le filtre de destinataire pour la nouvelle étendue de gestion.

## Étape 3 : Créer un groupe de rôles de gestion

Dans cette étape, vous créez un groupe de rôles de gestion et affectez l'étendue personnalisée que vous avez créée à l'étape 2. Ajoutez les rôles Recherche de boîte aux lettres et Suspens pour raisons juridiques pour que les membres du groupe de rôles puissent effectuer des recherches de découverte électronique sur place et soumettre des boîtes aux lettres à un blocage sur place ou les placer en suspension pour litige. Vous pouvez également ajouter des membres à ce groupe de rôles afin qu'ils puissent rechercher les boîtes aux lettres des membres du groupe de distribution utilisé pour créer l'étendue personnalisée à l'étape 2.

Dans les exemples suivants, le groupe de sécurité des gestionnaires de découverte électronique des utilisateurs Ottawa sera ajouté comme membres de ce groupe de rôles. Vous pouvez utiliser le Centre d’administration Exchange ou l’environnement Exchange Management Shell pour cette étape.

## Utiliser l'environnement Exchange Management Shell pour créer un groupe de rôles de gestion

Exécutez cette commande pour créer un groupe de rôles qui utilise l'étendue personnalisée créée à l'étape 2. La commande ajoute également les rôles Recherche de boîte aux lettres et Suspens pour raisons juridiques, et ajoute le groupe de sécurité des gestionnaires de découverte électronique des utilisateurs Ottawa comme membres du nouveau groupe de rôles.

    New-RoleGroup "Ottawa Discovery Management" -Roles "Mailbox Search","Legal Hold" -CustomRecipientWriteScope "Ottawa Users eDiscovery Scope" -Members "Ottawa Users eDiscovery Managers"

## Utiliser le Centre d’administration Exchange pour créer un groupe de rôles de gestion

1.  Dans le Centre d’administration Exchange, accédez à **Autorisations**\>**Rôles d'administrateur** et cliquez ensuite sur **Nouveau**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter").

2.  Dans **Nouveau groupe de rôles**, fournissez les informations suivantes :
    
      - **Nom**   Entrez un nom descriptif pour le nouveau groupe de rôles. Pour cet exemple, vous utiliserez **Gestion de la découverte Ottawa**.
    
      - **Portée d'écriture**   Sélectionnez l'étendue de gestion personnalisée que vous avez créée à l'étape 2. Cette étendue sera appliquée au nouveau groupe de rôles.
    
      - **Rôles**   Cliquez sur **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter") et ajoutez les rôles **Suspens pour raisons juridiques** et **Recherche de boîte aux lettres** au nouveau groupe de rôles.
    
      - **Membres**   Cliquez sur **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter") et sélectionnez les utilisateurs, le groupe de sécurité ou les groupes de rôles que vous souhaitez ajouter comme membres du nouveau groupe de rôles. Pour cet exemple, les membres du groupe de sécurité **Gestionnaires de découverte électronique Ottawa** pourront rechercher uniquement les boîtes aux lettres des utilisateurs qui sont membres du groupe de distribution **Utilisateurs Ottawa**.

3.  Cliquez sur **Enregistrer** pour créer le groupe de rôles.
    
    Voici un exemple de fenêtre **Nouveau groupe de rôles** un fois que vous avez terminé.
    
    ![Créer un groupe de rôles pour une étendue personnalisée](images/Dn741464.a6e3419f-d5d9-404f-890d-ad35f499756f(EXCHG.150).gif "Créer un groupe de rôles pour une étendue personnalisée")  

## Étape 4 (facultatif) : Ajouter des gestionnaires de découverte comme membres du groupe de distribution utilisé pour créer l'étendue de gestion personnalisée

Vous devez effectuer cette étape uniquement si vous souhaitez permettre à un gestionnaire de découverte d'afficher un aperçu des résultats de la recherche de découverte électronique.

Exécutez cette commande pour ajouter le groupe de sécurité Gestionnaires de découverte électronique des utilisateurs Ottawa comme membre du groupe de distribution Utilisateurs Ottawa.

    Add-DistributionGroupMember -Identity "Ottawa Users" -Member "Ottawa Users eDiscovery Managers"

Vous pouvez également utiliser le CAE pour ajouter des membres à un groupe de distribution. Pour plus d’informations, voir [Création et gestion de groupes de distribution](create-and-manage-distribution-groups-exchange-2013-help.md).

## Étape 5 (facultatif) : Ajouter une boîte aux lettres de découverte comme membre du groupe de distribution utilisé pour créer l'étendue de gestion personnalisée

Vous devez effectuer cette étape uniquement si vous souhaitez permettre à un gestionnaire de découverte de copier des résultats de la recherche de découverte électronique.

Exécutez cette commande pour ajouter une boîte aux lettres de découverte appelée Boîte aux lettres de découverte Ottawa comme membre du groupe de distribution Utilisateurs Ottawa.

    Add-DistributionGroupMember -Identity "Ottawa Users" -Member "Ottawa Discovery Mailbox"

> [!NOTE]
> Pour ouvrir une boîte aux lettres de découverte et afficher les résultats de la recherche, les gestionnaires de découverte doivent disposer d'autorisations d'accès complet pour la boîte aux lettres de découverte. Pour plus d’informations, consultez la rubrique <a href="create-a-discovery-mailbox-exchange-2013-help.md">Créer une boîte aux lettres de découverte</a>.


## Comment savoir si cela a fonctionné ?

Voici quelques méthodes permettant de vérifier si vous avez implémenté avec succès les étendues de gestion personnalisées pour la découverte électronique. Lors de la vérification, assurez-vous que l'utilisateur qui exécute les recherches de découverte électronique est un membre du groupe de rôles qui utilise l'étendue de gestion personnalisée.

  - Créez une recherche de découverte électronique et sélectionnez le groupe de distribution utilisé pour créer l'étendue de gestion personnalisée comme source des boîtes aux lettres à rechercher. Toutes les boîtes aux lettres doivent être recherchées avec succès.

  - Créez une recherche de découverte électronique et recherchez les boîtes aux lettres des utilisateurs qui ne sont pas membres du groupe de distribution utilisé pour créer l'étendue de gestion personnalisée. La recherche doit échouer car le gestionnaire de découverte peut rechercher uniquement des boîtes aux lettres pour les utilisateurs qui sont membres du groupe de distribution utilisé pour créer l'étendue de gestion personnalisée. Dans ce cas, une erreur de type « Impossible d'effectuer une recherche dans la boîte aux lettres \<*name of mailbox*\>, car l'utilisateur actuel n'a pas l'autorisation d'accéder à la boîte aux lettres » est renvoyée.

  - Créez une recherche de découverte électronique et recherchez les boîtes aux lettres des utilisateurs qui sont membres du groupe de distribution utilisé pour créer l'étendue de gestion personnalisée. Dans la même recherche, incluez les boîtes aux lettres des utilisateurs qui ne sont pas membres. La recherche devrait réussir partiellement. Les boîtes aux lettres des membres du groupe de distribution utilisé pour créer l'étendue de gestion personnalisée doivent être recherchées avec succès. La recherche des boîtes aux lettres pour les utilisateurs qui ne sont pas membres du groupe devrait échouer.

## Plus d’informations

  - Étant donné que les groupes de distribution sont utilisés dans ce scénario pour limiter les recherches de découverte électronique et non pour délivrer un message, tenez compte des points suivants lorsque vous créez et configurez des groupes de distribution pour la découverte électronique :
    
      - Créez des groupes de distribution avec une appartenance fermée afin que seuls les propriétaires du groupe puissent ajouter des membres au groupe ou en supprimer. Si vous créez le groupe dans l’environnement Exchange Management Shell, utilisez la syntaxe `MemberJoinRestriction closed` et `MemberDepartRestriction closed`.
    
      - Activez la modération de groupe afin que les messages envoyés au groupe soient d'abord envoyés aux modérateurs de groupe qui peuvent approuver ou rejeter le message en conséquence. Si vous créez le groupe dans l’environnement Exchange Management Shell, utilisez la syntaxe `ModerationEnabled $true`. Si vous utilisez le CAE, vous pouvez activer la modération après avoir créé le groupe.
    
      - Masquez le groupe de distribution du carnet d'adresses partagé de l'organisation. Utilisez le CAE ou la cmdlet **Set-DistributionGroup** une fois que le groupe est créé. Si vous créez le groupe dans l’environnement Exchange Management Shell, utilisez la syntaxe `HiddenFromAddressListsEnabled $true`.
    
    Dans l'exemple suivant, la première commande crée un groupe de distribution avec une appartenance fermée et la modération est activée. La deuxième commande masque le groupe dans le carnet d'adresses partagé.
    
        New-DistributionGroup -Name "Vancouver Users eDiscovery Scope" -Alias VancouverUserseDiscovery -MemberJoinRestriction closed -MemberDepartRestriction closed -ModerationEnabled $true
    
        Set-DistributionGroup "Vancouver Users eDiscovery Scope" -HiddenFromAddressListsEnabled $true
    
    Pour plus d'informations sur la création et la gestion des groupes de distribution, consultez la rubrique [Création et gestion de groupes de distribution](create-and-manage-distribution-groups-exchange-2013-help.md).

  - Bien que vous puissiez utiliser l'appartenance au groupe de distribution uniquement comme filtre de destinataire pour une étendue de gestion personnalisée utilisée pour la découverte électronique, vous pouvez utiliser d'autres propriétés de destinataire pour ajouter des utilisateurs à ce groupe de distribution. Voici quelques exemples d'utilisation des cmdlets **Get-Mailbox** et **Get-Recipient** pour renvoyer un groupe d'utilisateurs spécifique sur la base d'attributs de boîte aux lettres ou d'utilisateur courants.
    
        Get-Recipient -RecipientTypeDetails UserMailbox -ResultSize unlimited -Filter 'Department -eq "HR"'
    
        Get-Mailbox -RecipientTypeDetails UserMailbox -ResultSize unlimited -Filter 'CustomAttribute15 -eq "VancouverSubsidiary"'
    
        Get-Recipient -RecipientTypeDetails UserMailbox -ResultSize unlimited -Filter 'PostalCode -eq "98052"'
    
        Get-Recipient -RecipientTypeDetails UserMailbox -ResultSize unlimited -Filter 'StateOrProvince -eq "WA"'
    
        Get-Mailbox -RecipientTypeDetails UserMailbox -ResultSize unlimited -OrganizationalUnit "namsr01a002.sdf.exchangelabs.com/Microsoft Exchange Hosted Organizations/contoso.onmicrosoft.com"

  - Vous pouvez ensuite utiliser les exemples du point précédent pour créer une variable qui peut être utilisée avec la cmdlet **Add-DistributionGroupMember** pour ajouter un groupe d'utilisateurs à un groupe de distribution. Dans l'exemple suivant, la première commande crée une variable qui contient toutes les boîtes aux lettres d'utilisateurs qui ont la valeur **Vancouver** pour la propriété *Department* dans leur compte d'utilisateur. La deuxième commande ajoute ces utilisateurs au groupe de distribution aux utilisateurs Vancouver.
    
        $members = Get-Recipient -RecipientTypeDetails UserMailbox -ResultSize unlimited -Filter 'Department -eq "Vancouver"'
    
        $members | ForEach {Add-DistributionGroupMember "Ottawa Users" -Member $_.Name}

  - Vous pouvez utiliser la cmdlet **Add-RoleGroupMember** pour ajouter un membre à un groupe de rôles existant qui est utilisé pour limiter des recherches de découverte électronique. Par exemple, la commande suivante ajoute l'utilisateur admin@ottawa.contoso.com au groupe de rôles Gestion de la découverte Ottawa.
    
        Add-RoleGroupMember "Vancouver Discovery Management" -Member paralegal@vancouver.contoso.com
    
    Vous pouvez également utiliser le CAE pour ajouter des membres à un groupe de rôles. Pour plus d’informations, consultez la section relative à l’ajout de membres à un groupe de rôles dans [Gérer les membres de groupes de rôles](manage-role-group-members-exchange-2013-help.md).

  - Dans Exchange Online, la recherche de boîtes aux lettres inactives ne peut pas être effectuée à l’aide d’une étendue de gestion personnalisée utilisée pour la découverte électronique. Ceci est dû au fait qu’une boîte aux lettres inactive ne peut pas être membre d’un groupe de distribution. Par exemple, supposons qu’un utilisateur est membre d’un groupe de distribution qui a été utilisé pour créer une étendue de gestion personnalisée pour la découverte électronique. Ensuite, cet utilisateur quitte l’organisation et sa boîte aux lettres devient inactive (en plaçant la boîte aux lettres en conservation inaltérable ou pour litige, puis en supprimant le compte d’utilisateur Office 365 correspondant). En conséquence, l’utilisateur est supprimé en tant que membre des groupes de distribution, y compris du groupe qui a été utilisé pour créer l’étendue de gestion personnalisée servant à la découverte électronique. Si un gestionnaire de découverte (qui est membre du groupe de rôles auquel a été affectée l’étendue de gestion personnalisée) essaie de rechercher la boîte aux lettres inactive, la recherche échoue. Pour rechercher des boîtes aux lettres inactives, le gestionnaire de découverte doit être membre du groupe de rôles Gestion de la découverte ou de tout groupe de rôles qui dispose des autorisations nécessaires de recherche dans toute l’organisation.
    
    Pour de plus amples informations sur les boîtes aux lettres inactives, consultez la rubrique [Boîtes aux lettres inactives dans Exchange Online](https://technet.microsoft.com/fr-fr/library/dn798632\(v=exchg.150\)).

