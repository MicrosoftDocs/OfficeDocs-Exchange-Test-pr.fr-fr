---
title: 'Découverte électronique locale: Exchange 2013 Help'
TOCTitle: Découverte électronique locale
ms:assetid: 6377cb7a-3416-4e15-8571-c45d2160fc6f
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dd298021(v=EXCHG.150)
ms:contentKeyID: 50478328
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Découverte électronique locale

 

_**Sapplique à :** Exchange Online, Exchange Server 2013_

_**Dernière rubrique modifiée :** 2017-01-17_

> [!NOTE]
> Nous avons différé la date d’échéance du 1er juillet 2017 pour créer ds recherches de découverte électronique inaltérable dans Exchange Online (dans les plans autonomes Office 365 et Exchange Online). Mais plus tard cette année ou au début de l’année prochaine, vous ne pourrez pas créer des recherches dans Exchange Online. Pour créer des recherches de découverte électronique, veuillez commencer à utiliser la <a href="https://go.microsoft.com/fwlink/?linkid=847843">recherche de contenu</a> dans le Centre de conformité et sécurité Office 365. Lorsque nous aurons désactivé les nouvelles recherches de découverte électronique inaltérable, vous pourrez toujours modifier les recherches de découverte électronique inaltérable existantes, et la création de nouvelles recherches de découverte électronique inaltérable sera toujours prise en charge dans les déploiements hybrides Exchange Server 2013 et Exchange.


Si votre organisation satisfait à des exigences de découverte légale (dans le cadre d’une stratégie organisationnelle, d’exigences de conformité ou de procès), la découverte électronique locale dans Microsoft Exchange Server 2013 et Exchange Online vous permet d’effectuer des recherches de découverte de contenu approprié dans les boîtes aux lettres. Exchange 2013 et Exchange Online offrent également des fonctionnalités de recherche fédérée et l’intégration à Microsoft SharePoint 2013 et Microsoft SharePoint Online. Le Centre de découverte électronique de SharePoint vous permet de rechercher et de conserver tous les contenus relatifs à un cas, y compris des sites web SharePoint 2013 et SharePoint Online, des documents, des partages de fichiers indexés par SharePoint, du contenu de boîtes aux lettres dans SharePoint 2013 et du contenu Exchange archivé. Vous pouvez également utiliser la découverte électronique locale dans un environnement Exchange hybride pour effectuer des recherches sur site et dans des boîtes aux lettres en nuage dans la même catégorie.

**Contenu de cette rubrique**

Fonctionnement de la découverte électronique locale

Recherche Exchange

Groupe de rôles Gestion de la découverte et rôles de gestion

Étendues de gestion personnalisées pour la découverte électronique locale

Intégration à SharePoint Server 2013 et SharePoint Online

Découverte électronique dans un déploiement Exchange hybride

Boîtes aux lettres de détection

Utilisation de la découverte électronique locale

Estimation, aperçu et copie des résultats de la recherche

Exportation des résultats de recherche dans un fichier PST

Différences dans les résultats de recherche

Journalisation des recherches de découverte électronique locale

Découverte électronique locale et archive permanente

Conservation de boîtes aux lettres pour la découverte électronique locale

Limites et stratégies de limitation des découvertes électroniques locales

Documentation relative à la découverte électronique locale

> [!NOTE]
> La découverte électronique locale est une fonctionnalité puissante qui permet à un utilisateur disposant des autorisations appropriées de recevoir potentiellement l'accès à tous les enregistrements de messagerie stockés dans l'organisation Exchange 2013 ou Exchange Online. Il est essentiel de contrôler et de surveiller les activités de découverte, notamment l'ajout de membres au groupe de rôles Gestion de la découverte, l'attribution du rôle de gestion Recherche de boîte aux lettres et l'attribution de l'autorisation d'accès aux boîtes aux lettres de découverte.


## Fonctionnement de la découverte électronique locale

La découverte électronique locale utilise les index de contenu créés par le service de recherche Exchange. Le contrôle d'accès en fonction du rôle (RBAC) fournit le groupe de rôles [Gestion de la détection](discovery-management-exchange-2013-help.md) pour déléguer les tâches de découverte au personnel non technique, sans qu'il soit nécessaire d'accorder des privilèges élevés susceptibles de permettre à un utilisateur d'apporter des modifications opérationnelles à la configuration Exchange. Le Centre d'administration Exchange (CAE) inclut une interface de recherche conviviale destinée au personnel non technique, tel que des officiers de justice et des responsables de la mise en conformité, les responsables des enregistrements et les spécialistes des ressources humaines (RH).

Les utilisateurs autorisés peuvent effectuer une recherche de découverte électronique locale en sélectionnant les boîtes aux lettres, puis en spécifiant des critères de recherche tels que mots-clés, dates de début et de fin, adresses de l’expéditeur et du destinataire, et types de messages. Une fois la recherche terminée, les utilisateurs autorisés peuvent sélectionner l’une des actions suivantes :

  - **Estimation des résultats de recherche**   Cette option permet d’obtenir une estimation de la taille totale et du nombre d’éléments renvoyés par la recherche d’après les critères spécifiés.

  - **Aperçu des résultats de la recherche**   Cette option affiche un aperçu des résultats. Les messages renvoyés depuis chaque boîte aux lettres faisant l'objet d'une recherche sont affichés.

  - **Copier les résultats de la recherche**   Cette option vous permet de copier des messages dans une boîte aux lettres de découverte.

  - **Exporter les résultats de la recherche**   Une fois les résultats de la recherche copiés dans une boîte aux lettres de découverte, vous pouvez les exporter vers un fichier PST.

![Obtenir une estimation, obtenir un aperçu, copier et exporter les résultats de la recherche](images/Dd298021.6356971a-34ed-4586-8229-030448d4fe2d(EXCHG.150).gif "Obtenir une estimation, obtenir un aperçu, copier et exporter les résultats de la recherche")

## Recherche Exchange

La découverte électronique locale utilise les index de contenu créés par le service de recherche Exchange. Le service de recherche Exchange s'est vu attribuer de nouveaux outils pour l'utilisation de Microsoft Search Foundation, une plateforme de recherche enrichie au niveau des performances d'indexation et d'interrogation ainsi que de la fonctionnalité de recherche. Microsoft Search Foundation est également utilisé par les autres produits Office, y compris SharePoint 2013. Il offre par conséquent une meilleure interopérabilité et une syntaxe de requête similaire pour tous ces produits.

Avec un simple moteur d'indexation de contenu, aucune ressource supplémentaire n'est utilisée pour parcourir et indexer les bases de données de boîtes aux lettres pour la découverte électronique locale lorsque les services informatiques reçoivent des demandes de découverte électronique.

La découverte électronique locale utilise le langage KQL (Keyword Query Language), une syntaxe de requête semblable à la syntaxe de recherche avancée (AQS) utilisée par la Recherche instantanée dans Microsoft Outlook et Outlook Web App. Les utilisateurs connaissant le KQL peuvent aisément créer des demandes de recherche puissantes pour effectuer des recherches dans les index de contenu.

Pour plus d’informations sur les formats de fichiers indexés par la recherche Exchange, consultez la rubrique [Formats de fichier indexés par le service de recherche Exchange](file-formats-indexed-by-exchange-search-exchange-2013-help.md).

## Groupe de rôles Gestion de la découverte et rôles de gestion

Pour que les utilisateurs autorisés puissent effectuer des recherches de découverte électronique locale, vous devez les ajouter au groupe de rôles [Gestion de la détection](discovery-management-exchange-2013-help.md). Ce groupe de rôles comprend deux rôles de gestion : le [Rôle de recherche de boîte aux lettres](mailbox-search-role-exchange-2013-help.md), qui permet à un utilisateur d'exécuter une recherche de découverte électronique locale, et le [Rôle de conservation légale](legal-hold-role-exchange-2013-help.md), qui permet à un utilisateur de placer une boîte aux lettres en archive permanente ou en mise en attente pour litige.

Par défaut, les autorisations pour exécuter des tâches relatives à la découverte électronique locale ne sont attribuées à aucun utilisateur ni administrateur Exchange. Les administrateurs Exchange membres du groupe de rôles Gestion de l'organisation peuvent ajouter des utilisateurs au groupe de rôles Gestion de la découverte et créer des groupes de rôles personnalisés pour restreindre l'étendue d'un gestionnaire de découverte à un sous-ensemble d'utilisateurs. Pour plus d'informations sur l'ajout d'utilisateurs au groupe de rôles Gestion de la découverte, consultez la rubrique [Attribution d’autorisations eDiscovery dans Exchange](assign-ediscovery-permissions-in-exchange-exchange-2013-help.md).

> [!NOTE]
> Si un utilisateur n'a pas été ajouté au groupe de rôles Gestion de la découverte ou n'a pas reçu le rôle Recherche de boîte aux lettres, l'interface utilisateur <strong>Découverte électronique et archive permanente</strong> n'est pas affichée dans le CAE et les cmdlets de découverte électronique locale ne sont pas disponibles dans l'environnement de ligne de commande Exchange Management Shell.


L'audit des modifications apportées au rôle RBAC, activé par défaut, permet de s'assurer que les enregistrements adéquats sont conservés de manière à suivre l'attribution du groupe de rôles Gestion de la découverte. Vous pouvez utiliser le rapport de groupe de rôles d’administrateur pour rechercher des modifications apportées aux groupes de rôles d’administrateur. Pour plus d’informations, consultez la rubrique [Rechercher les modifications des groupes de rôles ou les journaux d’audit de l’administrateur](search-the-role-group-changes-or-administrator-audit-logs-exchange-2013-help.md).

Retour au début

## Étendues de gestion personnalisées pour la découverte électronique locale

Vous pouvez utiliser une étendue de gestion personnalisée pour permettre à des personnes ou des groupes spécifiques d’utiliser la découverte électronique locale pour rechercher un sous-ensemble de boîtes aux lettres dans votre organisation Exchange 2013 ou Exchange Online. Par exemple, vous voudrez peut-être permettre à un gestionnaire de découverte de rechercher uniquement les boîtes aux lettres des utilisateurs dans un lieu ou un service spécifique. Pour ce faire, créez une étendue de gestion personnalisée qui utilise un filtre de destinataire personnalisé pour contrôler les boîtes aux lettres pouvant être recherchées. Les étendues de filtre de destinataire utilisent des filtres pour cibler des destinataires spécifiques en fonction de leur type ou d’autres porpriétés.

Pour la découverte électronique locale, la seule propriété sur une boîte aux lettres d’utilisateur que vous pouvez employer pour créer un filtre de destinataire pour une étendue personnalisée est l’appartenance à un groupe de distribution. Si vous utilisez d'autres propriétés, telles que *CustomAttributeN*, *Department* ou *PostalCode*, la recherche échoue lorsqu’elle est effectuée par un membre du groupe de rôles auquel l’étendue personnalisée est attribuée. Pour plus d’informations, voir [Création d’une étendue de gestion personnalisée pour les recherches de découverte électronique sur place](create-a-custom-management-scope-for-in-place-ediscovery-searches-exchange-2013-help.md).

## Intégration à SharePoint Server 2013 et SharePoint Online

Exchange 2013 et Exchange Online offrent une intégration à SharePoint 2013 et SharePoint Online, qui permet à un gestionnaire de découverte d'utiliser le Centre de découverte électronique dans SharePoint pour exécuter les tâches suivantes :

  - **Rechercher et conserver le contenu depuis un site unique** Un gestionnaire de découverte autorisé peut rechercher et conserver le contenu dans SharePoint et Exchange, y compris le contenu Lync, tel que les conversations de messagerie instantanée et les documents de réunion partagés archivés dans les boîtes aux lettres Exchange.

  - **Gestion des cas** Le Centre de découverte électronique utilise une approche de gestion des cas pour la découverte électronique, ce qui vous permet de créer des cas et de rechercher et conserver du contenu dans différents référentiels de contenus pour chaque cas.

  - **Exporter les résultats de la recherche** Un gestionnaire de découverte peut utiliser le Centre de découverte électronique pour exporter des résultats de la recherche. Le contenu des boîtes aux lettres inclus dans les résultats de la recherche est exporté vers un fichier PST.

SharePoint utilise également Microsoft Search Foundation pour l'indexation et l'interrogation du contenu. Qu'un gestionnaire de découverte utilise le CAE ou le Centre de découverte électronique pour rechercher du contenu Exchange, le même contenu de boîte aux lettres est renvoyé.

Dans les déploiements locaux, avant de pouvoir utiliser le Centre de découverte électronique dans SharePoint pour rechercher des boîtes aux lettres Exchange, vous devez établir une relation d'approbation entre les deux applications. Dans Exchange 2013 et SharePoint 2013, cela passe par l'authentification OAuth. Pour plus d'informations, consultez la rubrique [Configurer Exchange pour le Centre de découverte électronique SharePoint](configure-exchange-for-sharepoint-ediscovery-center-exchange-2013-help.md). Les recherches de découverte électronique exécutées à partir de SharePoint sont autorisées par Exchange au moyen du RBAC. Pour qu'un utilisateur SharePoint puisse exécuter une recherche de découverte électronique des boîtes aux lettres Exchange, il doit obtenir l'autorisation Gestion de la découverte déléguée dans Exchange. Pour pouvoir afficher un aperçu du contenu des boîtes aux lettres renvoyé dans une recherche de découverte électronique exécutée via le Centre de découverte électronique SharePoint, le gestionnaire de découverte doit avoir une boîte aux lettres dans la même organisation Exchange.

Pour obtenir des instructions étape par étape sur la configuration d’un centre eDiscovery dans une organisation Office 365, consultez la rubrique [Configurer un centre eDiscovery dans SharePoint Online](https://go.microsoft.com/fwlink/p/?linkid=331600).

## Découverte électronique dans un déploiement Exchange hybride

Pour effectuer des recherches de découverte électronique entre différents locaux dans une organisation hybride Exchange 2013, vous devrez configurer l’authentification OAuth (Open Authorization) entre votre organisation Exchange sur site et des organisations Exchange Online afin de pouvoir utiliser la découverte électronique locale pour effectuer des recherches dans des boîtes aux lettres sur site et informatiques. L’authentification OAuth est un protocole d’authentification S2S qui permet aux applications de s’authentifier mutuellement.

L’authentification OAuth prend en charge les scénarios de découverte électronique suivants dans un déploiement hybride Exchange :

  - Les recherches dans des boîtes aux lettres sur site utilisant l’Archivage Exchange Online pour des boîtes aux lettres d’archivage informatiques.

  - Les recherches dans des boîtes aux lettres sur site et informatiques dans la même recherche de découverte électronique.

  - Les recherches dans des boîtes aux lettres sur site à l’aide du centre de découverte électronique dans SharePoint Online.

Pour plus d’informations sur les scénarios de découverte électronique nécessitant la configuration de l’authentification OAuth dans un déploiement hybride Exchange, consultez la rubrique [Utilisation de l’authentification OAuth pour prendre en charge la découverte électronique dans un déploiement hybride Exchange](using-oauth-authentication-to-support-ediscovery-in-an-exchange-hybrid-deployment-exchange-2013-help.md). Pour obtenir des instructions détaillées sur la configuration de l’authentification OAuth afin qu’elle prenne en charge la découverte électronique, consultez la rubrique [Configurer l’authentification OAuth entre des organisations Exchange et Exchange Online](configure-oauth-authentication-between-exchange-and-exchange-online-organizations-exchange-2013-help.md).

## Boîtes aux lettres de détection

Une fois la recherche de découverte électronique locale créée, vous pouvez copier les résultats de la recherche dans une boîte aux lettres cible. Le CAE vous permet de sélectionner une boîte aux lettres de découverte comme boîte aux lettres cible. Une boîte aux lettres de découverte est un type spécial de boîte aux lettres offrant les avantages suivants :

  - **Sélection de boîte aux lettres cible simplifiée et sécurisée**   Quand vous utilisez le CAE pour copier les résultats de la recherche de la découverte électronique locale, seules les boîtes aux lettres de découverte sont disponibles sous la forme d'un référentiel dans lequel les résultats de la recherche sont stockés. Il n'est pas nécessaire de trier une liste potentiellement exhaustive de boîtes aux lettres disponibles dans l'organisation. Elle élimine également le risque pour un gestionnaire de découverte de sélectionner par inadvertance la boîte aux lettres d'un autre utilisateur ou une boîte aux lettres non sécurisée dans laquelle des messages confidentiels peuvent être éventuellement stockés.

  - **Quota de stockage de boîte aux lettres élevé**   La boîte aux lettres cible doit pouvoir stocker une quantité importante de données de messages susceptibles d'être renvoyées par une recherche de découverte électronique locale. Par défaut, les boîtes aux lettres de découverte présentent un quota de stockage de 50 gigaoctets (Go). Ce quota de stockage ne peut pas être augmenté.

  - **Plus sécurisées par défaut**   Comme tous les types de boîtes aux lettres, une boîte aux lettres de découverte est associée à un compte d’utilisateur Active Directory. Cependant, ce compte est désactivé par défaut. Seuls les utilisateurs explicitement autorisés à accéder à une boîte aux lettres de découverte y ont accès. Les membres du groupe de rôles Gestion de la découverte reçoivent les autorisations d’accès total à la boîte aux lettres de découverte par défaut. Aucune autorisation d’accès aux boîtes aux lettres ne sera attribuée à un utilisateur pour les boîtes aux lettres de découverte supplémentaires que vous créez.

  - **Remise de courrier électronique désactivée**   Bien qu'une boîte aux lettres de découverte apparaisse dans les listes d'adresses d'Exchange, les utilisateurs ne peuvent pas lui envoyer de courrier électronique. La remise du courrier électronique aux boîtes aux lettres de découverte est prohibée au moyen de restrictions de remise. Cela préserve l'intégrité des résultats de la recherche copiés dans une boîte aux lettres de découverte.

Le programme d'installation d'Exchange 2013 crée une boîte aux lettres de découverte unique avec le nom complet **Boîte aux lettres de découverte**. Vous pouvez utiliser l'environnement de ligne de commande Exchange Management Shell pour créer des boîtes aux lettres de découverte supplémentaires. Par défaut, aucune autorisation d'accès aux boîtes aux lettres n'est attribuée pour les boîtes aux lettres de découverte que vous créez. Vous pouvez attribuer les autorisations d'accès total à un gestionnaire de découverte pour lui permettre d'accéder aux messages copiés dans une boîte aux lettres de découverte. Pour plus d'informations, consultez la rubrique [Créer une boîte aux lettres de découverte](create-a-discovery-mailbox-exchange-2013-help.md).

Par ailleurs, la découverte électronique locale utilise une boîte aux lettres système dotée du nom complet **SystemMailbox{e0dc1c29-89c3-4034-b678-e6c29d823ed9}** pour contenir les métadonnées de la découverte électronique locale. Les boîtes aux lettres système ne sont visibles ni dans le CAE, ni dans les listes d'adresses Exchange. Dans une organisation locale, avant de supprimer une base de données de boîtes aux lettres contenant la boîte aux lettres système de la découverte électronique locale, vous devez déplacer la boîte aux lettres vers une autre base de données de boîtes aux lettres. Si la boîte aux lettres est supprimée ou endommagée, vos gestionnaires de découverte ne pourront pas exécuter des recherches de découverte électronique tant que la boîte aux lettres n'aura pas été recréée. Pour plus d'informations, consultez la rubrique [Re-create the Discovery system mailbox](re-create-the-discovery-system-mailbox-exchange-2013-help.md).

Retour au début

## Utilisation de la découverte électronique locale

Les utilisateurs qui ont été ajoutés au groupe de rôles Gestion de la découverte peuvent effectuer des recherches de découverte électronique locale. Vous pouvez effectuer une recherche en utilisant l'interface web du CAE. Ainsi, l'utilisation de la découverte électronique locale est simplifiée pour le personnel non technique, tels que les responsables d'enregistrements, les responsables de la mise en conformité ou les spécialistes juridiques et des ressources humaines. Vous pouvez également utiliser l'environnement de ligne de commande Exchange Management Shell pour effectuer une recherche. Pour plus d’informations, consultez la rubrique [Créer une recherche de découverte électronique inaltérable](create-an-in-place-ediscovery-search-exchange-2013-help.md).

> [!NOTE]
> Dans les organisations locales, vous pouvez utiliser la découverte électronique locale pour rechercher des boîtes aux lettres situées sur les serveurs de boîtes aux lettres Exchange 2013. Pour rechercher des boîtes aux lettres situées sur des serveurs de boîtes aux lettres Exchange 2010, utilisez la recherche sur un serveur Exchange 2010.
> Dans un déploiement hybride, qui est un environnement contenant des boîtes aux lettres à la fois sur vos serveurs de boîtes aux lettres locaux et dans une organisation en nuage, vous pouvez effectuer des recherches de découverte électronique locale de vos boîtes aux lettres en nuage en utilisant le CAE de votre organisation locale. Si vous avez l'intention de copier des messages vers une boîte aux lettres de découverte, vous devez sélectionner une boîte aux lettres de découverte locale. Les messages de boîtes aux lettres en nuage qui sont retournés dans des résultats de recherches sont copiés vers la boîte aux lettres de découverte locale. Pour en savoir plus sur les déploiements hybrides, consultez la rubrique <a href="https://technet.microsoft.com/fr-fr/library/jj200581(v=exchg.150)">Déploiements hybrides Exchange Server</a>.


L'Assistant **Découverte électronique locale et archive permanente** dans le CAE vous permet de créer une recherche de découverte électronique locale et d'utiliser également l'archive permanente pour rechercher des résultats en attente. Quand vous créez une recherche de découverte électronique locale, un objet de recherche est créé dans la boîte aux lettres système de découverte électronique locale. Cet objet peut être utilisé pour démarrer, arrêter, modifier et supprimer la recherche. Après avoir créé la recherche, vous pouvez choisir d'obtenir une estimation des résultats de la recherche, qui contient des statistiques de mots clés vous permettant de déterminer l'efficacité de la requête. Vous pouvez également effectuer un aperçu instantané des éléments renvoyés dans la recherche, qui vous permet d'afficher le contenu des messages, le nombre de messages renvoyés depuis chaque boîte aux lettres source et le nombre total de messages. Vous pouvez utiliser ces informations pour affiner votre requête si nécessaire.

Une fois satisfait des résultats de la recherche, vous pouvez les copier dans une boîte aux lettres de découverte. Vous pouvez également utiliser le CAE ou Outlook pour exporter une boîte aux lettres de découverte ou certains contenus dans un fichier PST.

Quand vous créez une recherche de découverte électronique locale, vous devez spécifier les paramètres suivants :

  - **Nom**   Le nom de la recherche permet d'identifier la recherche. Quand vous copiez des résultats de la recherche dans une boîte aux lettres de découverte, un dossier est créé dans cette dernière à partir du nom et de l'horodateur de la recherche pour n'identifier que les résultats de la recherche dans une boîte aux lettres de découverte.

  - **Boîtes aux lettres**   Vous pouvez décider de rechercher toutes les boîtes aux lettres dans votre organisation Exchange 2013 ou Exchange Online, ou de spécifier les boîtes aux lettres à rechercher. Les boîtes aux lettres principale et d’archivage d’un utilisateur sont comprises dans la recherche. Si vous souhaitez utiliser la même recherche pour placer les éléments en conservation, vous devez spécifier les boîtes aux lettres. Enfin, vous pouvez spécifier un groupe de distribution pour inclure les utilisateurs de boîtes aux lettres qui appartiennent au groupe. L’appartenance au groupe est calculée une fois lors de la création de la recherche. Les modifications suivantes de l’appartenance au groupe ne sont pas automatiquement reflétées dans la recherche.
    
    Dans Exchange Online, vous pouvez également spécifier des groupes Office 365 en tant que source de contenu afin qu’une recherche soit réalisée dans la boîte aux lettres de groupe ou que celle-ci soit placée en conservation. Lorsque vous ajoutez un groupe Office 365 à une recherche de découverte électronique inaltérable, la recherche est effectuée uniquement dans la boîte aux lettres de groupe, et non dans les boîtes aux lettres des membres du groupe.

  - **Requête de recherche**   Vous pouvez inclure tout le contenu des boîtes aux lettres à partir des boîtes aux lettres spécifiées ou utiliser une requête de recherche pour renvoyer les éléments les plus pertinents pour le cas ou l'investigation. Dans une requête de recherche, vous pouvez spécifier les paramètres suivants :
    
      - **Mots clés**   Vous pouvez spécifier des mots clés et des expressions pour rechercher le contenu d'un message. Vous pouvez également utiliser les opérateurs logiques **AND**, **OR** et **NOT**. De plus, Exchange 2013 prend également en charge l'opérateur **NEAR**, qui vous permet de rechercher un mot ou une phrase à proximité d'un autre mot ou d'une autre phrase.
        
        Pour rechercher une correspondance exacte d'une expression composée de plusieurs mots, vous devez inclure l'expression entre guillemets. Par exemple, la recherche de la phrase "plan et concurrence" renvoie des messages qui contiennent une correspondance exacte de la phrase, alors que la saisie de **plan AND concurrence** renvoie des messages qui contiennent les mots **plan** et **concurrence** indépendamment de leur emplacement.
        
        Exchange 2013 prend également en charge la syntaxe KQL pour des recherches de découverte électronique locale.
        
        > [!NOTE]
        > La découverte électronique locale ne prend pas en charge les expressions régulières.
        
        Vous devez écrire les opérateurs logiques comme **AND** et **OR** en majuscules pour qu'ils soient considérés comme des opérateurs plutôt que des mots clés. Nous vous recommandons d'utiliser des parenthèses explicites dans toutes les requêtes combinant plusieurs opérateurs logiques (AND, OR, NOT, etc.) afin d'éviter des erreurs ou des interprétations incorrectes. Par exemple, si vous souhaitez rechercher des messages contenant soit MotA ou MotB ET soit MotC ou MotD, vous devez utiliser **(MotA OR MotB) AND (MotC OR MotD)**.
    
      - **Dates de début et de fin**   Par défaut, la découverte électronique locale ne limite pas les recherches à une plage de dates. Pour rechercher des messages envoyés à une plage de dates spécifique, vous pouvez affiner la recherche en saisissant une date de début et une date de fin. Si vous n'indiquez aucune date de fin, la recherche renvoie les derniers résultats chaque fois que vous la relancez.
    
      - **Expéditeurs et destinataires**   Pour réduire le champ de la recherche, vous pouvez indiquer les expéditeurs ou les destinataires des messages. Vous pouvez utiliser des adresses de messagerie, des noms complets ou le nom d'un domaine pour rechercher des éléments envoyés ou reçus par tous les utilisateurs de ce domaine. Par exemple, pour rechercher un message électronique envoyé à ou par Contoso, Ltd, spécifiez **@contoso.com** dans la zone **De** ou le champ **À/Cc** dans le CAE. Vous pouvez également spécifier **@contoso.com** dans les paramètres *Senders* ou *Recipients* de l'environnement de ligne de commande Exchange Management Shell.
    
      - **Types de messages**   Par défaut, tous les types de messages font l'objet de recherches. Vous pouvez restreindre la recherche en sélectionnant des types de messages spécifiques tels que messages électroniques, contacts, documents, journaux, réunions, notes et contenus Lync.

La capture d’écran suivante présente l’exemple d’une requête de recherche dans le CAE.

![Configurer une requête de recherche de découverte électronique](images/Dd298021.a3626569-8700-421e-8b4e-7ec520b28272(EXCHG.150).png "Configurer une requête de recherche de découverte électronique")

Quand vous utilisez la découverte électronique locale, considérez également ce qui suit :

  - **Pièces jointes**   Les pièces jointes des recherches de découverte électronique locale prises en charge par la recherche Exchange. Pour plus d'informations, consultez la rubrique [Formats de fichier indexés par le service de recherche Exchange](file-formats-indexed-by-exchange-search-exchange-2013-help.md). Dans un déploiement local, vous pouvez ajouter une prise en charge de types de fichiers supplémentaires en installant des filtres de recherche (également appelés iFilter) pour le type de fichiers sur les serveurs de boîtes aux lettres.

  - **Éléments impossibles à rechercher**   Les éléments impossibles à rechercher sont des éléments de boîtes aux lettres qui ne peuvent pas être indexés par le service de recherche Exchange. L'inexistence d'un filtre de recherche pour un fichier joint, une erreur de filtre ou des messages chiffrés sont des motifs de non indexation. Pour réussir la recherche de découverte électronique, votre organisation peut demander d'inclure de tels éléments pour vérification. Lors de la copie des résultats de la recherche vers une boîte aux lettres de découverte ou lors de l’exportation des résultats de la recherche vers un fichier PST, vous pouvez inclure des éléments impossibles à rechercher. Pour plus d’informations, consultez la rubrique [Éléments impossibles à rechercher dans la découverte électronique Exchange](unsearchable-items-in-exchange-ediscovery-exchange-2013-help.md).

  - **Éléments chiffrés**   Dans la mesure où les messages chiffrés via S/MIME ne sont pas indexés par le service de recherche Exchange, la découverte électronique locale ne recherche pas ces messages. Si vous choisissez d'inclure les éléments impossibles à rechercher dans les résultats de la recherche, ces messages chiffrés S/MIME sont copiés dans la boîte aux lettres de découverte.

  - **Éléments protégés par IRM**   Les messages protégés par la Gestion des droits relatifs à l'information (IRM) sont indexés par le service de recherche Exchange et donc inclus dans les résultats de la recherche s'ils correspondent aux paramètres de la requête. Les messages doivent être protégés en utilisant un cluster Active Directory Rights Management Services (AD RMS) dans la même forêt Active Directory que celle du serveur de boîtes aux lettres. Pour plus d'informations, consultez la rubrique [Gestion des droits relatifs à l’information](information-rights-management-exchange-2013-help.md).
    
	> [!IMPORTANT]
    > Si le service de recherche Exchange ne parvient pas à indexer un message protégé par IRM, que ce soit en raison d'une erreur de déchiffrement ou de la désactivation de la fonctionnalité IRM, le message protégé n'est pas ajouté à la liste des éléments défaillants. Si vous choisissez d'inclure les éléments impossibles à rechercher dans les résultats de la recherche, il est possible que ces derniers n'incluent pas les messages protégés par IRM qui n'ont pas pu être déchiffrés.
    > Pour inclure les messages protégés par IRM dans une recherche, vous pouvez créer une autre recherche pour inclure des messages comportant des pièces jointes .rpmsg. Vous pouvez utiliser la chaîne de requête <code>attachment:rpmsg</code> pour rechercher tous les messages protégés par IRM dans les boîtes aux lettres spécifiées, qu'elles soient correctement indexées ou pas. Il peut en résulter une duplication des résultats de la recherche dans des scénarios où une recherche renvoie des messages correspondant aux critères de recherche, notamment des messages protégés par IRM qui ont été correctement indexés. La recherche ne renvoie pas les messages protégés par IRM qui n'ont pas pu être indexés.
    > L'exécution d'une deuxième recherche pour tous les messages protégés inclut également les messages protégés par IRM ayant été correctement indexés et renvoyés lors de la première recherche. De plus, il est possible que les messages protégés par IRM renvoyés lors de la deuxième recherche ne correspondent pas aux critères de la recherche, tels que les mots clés utilisés pour la première recherche.


  - **Déduplication**   Quand vous copiez des résultats de recherche dans une boîte aux lettres de découverte, vous pouvez activer la *déduplication* des résultats de la recherche pour ne copier qu'une seule instance d'un message unique dans la boîte aux lettres de découverte. Les avantages de la déduplication sont les suivants :
    
      - Réduction des besoins en stockage et réduction de la taille de la boîte aux lettres de détection grâce à la réduction du nombre de messages copiés.
    
      - Réduction de la charge de travail des gestionnaires de découverte, conseil juridique ou autres impliqués dans la vérification des résultats de la recherche.
    
      - Réduction du coût de la découverte électronique, en fonction du nombre d'éléments dupliqués exclus des résultats de la recherche.

Retour au début

## Estimation, aperçu et copie des résultats de la recherche

Une fois la recherche de découverte électronique locale terminée, vous pouvez afficher les estimations des résultats de recherche dans le volet d’informations du CAE. Les estimations incluent le nombre d'éléments renvoyés et la taille totale de ces éléments. Vous pouvez également afficher des statistiques sur les mots clés, qui renvoient les informations détaillées sur le nombre d'éléments renvoyés pour chaque mot clé utilisé dans la requête de recherche. Cette information est utile pour déterminer l'efficacité de la requête. Si la requête est trop large, l'ensemble de données renvoyé peut être bien plus important et demander la vérification de plus de ressources et l'augmentation des coûts de découverte électronique. Si la requête est trop étroite, le nombre d'enregistrements renvoyés peut être considérablement réduit voire nul. Vous pouvez utiliser les estimations et les statistiques sure les mots clés pour affiner la requête et répondre à vos besoins.

> [!NOTE]
> Dans Exchange 2013, les statistiques sur les mots clés incluent également des statistiques sur les propriétés hors mots clés telles que les dates, les types de messages et les expéditeurs/destinataires spécifiés dans une requête de recherche.


Il est également possible d'afficher les résultats de la recherche pour vous assurer que les messages renvoyés contiennent le contenu recherché et affiner la recherche si nécessaire. L'aperçu de la recherche de découverte électronique affiche le nombre de messages renvoyés à partir de chaque boîte aux lettres faisant l'objet d'une recherche et le nombre total de messages renvoyés par la recherche. L'aperçu est généré rapidement et n'implique pas de copier des messages dans une boîte aux lettres de découverte.

Lorsque la quantité et la qualité des résultats de la recherche vous conviennent, vous pouvez les copier dans une boîte aux lettres de découverte. Quand vous copiez des messages, les options suivantes s'offrent à vous :

  - **Inclure les éléments impossibles à rechercher**   Pour plus d'informations sur les types d'éléments considérés comme impossible à rechercher, consultez la section traitant des éléments de recherche dont vous devez tenir compte dans la section précédente.

  - **Activer la déduplication**   La déduplication réduit le jeu de données en n'incluant qu'une seule instance d'un seul enregistrement si plusieurs instances sont trouvées dans une ou plusieurs boîtes aux lettres recherchées.

  - **Activer la journalisation complète**   Par défaut, seule la journalisation de base est activée lorsque vous copiez des éléments. Vous pouvez sélectionner l'option de journalisation complète pour inclure des informations relatives à tous les enregistrements renvoyés par la recherche.

  - **M'envoyer un message lorsque la copie est terminée**   Une recherche de découverte électronique locale peut potentiellement renvoyer un grand nombre d'enregistrements. La copie des messages renvoyés vers une boîte aux lettres de découverte peut prendre du temps. Utilisez cette option pour obtenir une notification par courrier électronique à la fin du processus de copie. Pour simplifier l'accès au moyen d'Outlook Web App, la notification inclut un lien vers l'emplacement de la boîte aux lettres de découverte dans lequel les messages sont copiés.

Pour plus d’informations, consultez la rubrique [Copier les résultats de la recherche de découverte automatique dans une boîte aux lettres de découverte](copy-ediscovery-search-results-to-a-discovery-mailbox-exchange-2013-help.md).

Retour au début

## Exportation des résultats de recherche dans un fichier PST

Une fois les résultats de la recherche copiés dans une boîte aux lettres de découverte, vous pouvez les exporter vers un fichier PST.

![Exporter les résultats de la recherche électronique vers un fichier PST](images/Dd298021.4ddca8af-1af5-4cb2-852c-e3a292099a58(EXCHG.150).gif "Exporter les résultats de la recherche électronique vers un fichier PST")

Une fois les résultats de la recherche vers un fichier PST, vous ou d’autres utilisateurs pouvez les ouvrir dans Outlook pour passer en revue ou imprimer des messages renvoyés dans les résultats de la recherche. Pour plus d’informations, consultez la rubrique [Exporter les résultats de la recherche électronique vers un fichier PST](export-ediscovery-search-results-to-a-pst-file-exchange-2013-help.md).

## Différences dans les résultats de recherche

Comme la découverte électronique locale effectue des recherches sur des données actives, deux recherches peuvent avoir des sources de contenu identiques et l’utilisation de la même requête de recherche peut renvoyer des résultats différents. Les résultats de la recherche estimés peuvent également être différents des résultats de recherche réels qui sont copiés dans une boîte aux lettres de découverte. Cela peut se produire même lorsque vous relancez la même recherche dans un court laps de temps. Il existe plusieurs facteurs qui peuvent affecter la cohérence des résultats de recherche :

  - L’indexation continue des courriers électroniques entrants, car Exchange Search parcourt et indexe en permanence le pipeline de transport et les bases de données de boîtes aux lettres de votre organisation.

  - Suppression des courriers électroniques par les utilisateurs ou par des processus automatisés.

  - Importation en bloc de gros volumes de courriers électroniques, dont l’indexation prend du temps.

Si les résultats sont différents pour la même recherche, envisagez de placer les boîtes aux lettres en attente pour préserver le contenu, effectuez les recherches pendant les heures creuses et gardez à l’esprit que l’indexation prend du temps après l’importation de gros volumes de courriers électroniques.

## Journalisation des recherches de découverte électronique locale

Il existe deux types de journalisation disponibles pour les recherches de découverte électronique locale :

  - **Journalisation de base**   La journalisation de base est activée par défaut pour toutes les recherches de découverte électronique locale. Elle inclut des informations sur la recherche et l'auteur de la recherche. Les informations enregistrées sur la journalisation de base s'affichent dans le corps du message électronique envoyé à la boîte aux lettres contenant les résultats de la recherche. Le message est situé dans le dossier créé pour stocker les résultats de la recherche.

  - **Journalisation complète**   La journalisation complète contient des informations sur tous les messages renvoyés par la recherche. Ces informations sont enregistrées dans un fichier de valeurs séparées par des virgules (.csv) qui est joint au message électronique contenant les informations de journalisation de base. Le nom de la recherche est utilisé pour le fichier .csv. Ces informations peuvent être nécessaires à des fins de mise en conformité ou de conservation des enregistrements. Pour activer la journalisation complète, vous devez sélectionner l’option **Activer la journalisation complète** lorsque vous copiez les résultats de la recherche dans une boîte aux lettres de découverte du CAE. Si vous utilisez l'environnement de ligne de commande Exchange Management Shell, spécifiez l'option de journalisation complète en utilisant le paramètre *LogLevel*.

> [!NOTE]
> Lors de la création ou de la modification d'une recherche de découverte électronique locale via l'environnement de ligne de commande Exchange Management Shell, vous pouvez également désactiver la journalisation.


Outre le journal de recherche inclus lorsque vous copiez les résultats de la recherche dans une boîte aux lettres de découverte, Exchange journalise également les cmdlets utilisées par le CAE ou l'environnement de ligne de commande Exchange Management Shell pour créer, modifier ou supprimer des recherches de découverte électronique locale. Ces informations sont consignées dans les entrées de journal d'audit administrateur. Pour plus d'informations, consultez la rubrique [Connexion au service d’audit administrateur](administrator-audit-logging-exchange-2013-help.md).

Retour au début

## Découverte électronique locale et archive permanente

Dans le cadre des demandes de découverte électronique, vous pouvez être amené à conserver le contenu de la boîte aux lettres jusqu'à ce qu'une décision de justice ou des données d'enquête soit rendues. Les messages supprimés ou modifiés par l'utilisateur de la boîte aux lettres ou tout autre processus doivent également être conservés. Dans Exchange 2013, cette opération est effectuée à l'aide de l'archive permanente. Pour plus d'informations, consultez la rubrique [Conservation inaltérable et conservation pour litige](in-place-hold-and-litigation-hold-exchange-2013-help.md).

Dans Exchange 2013, vous pouvez utiliser le nouvel Assistant **Découverte électronique et archive permanente** pour rechercher des éléments et les conserver aussi longtemps que nécessaire pour la découverte électronique ou pour répondre aux autres exigences commerciales. Quand vous utilisez la même recherche pour la découverte électronique locale et l'archive permanente, tenez compte des points suivants :

  - Vous ne pouvez pas utiliser l'option pour rechercher toutes les boîtes aux lettres. Vous devez sélectionner les boîtes aux lettres ou groupes de distribution.

  - Vous ne pouvez pas supprimer une recherche de découverte électronique locale si la recherche est également utilisée pour l'archive permanente. Vous devez en premier lieu désactiver l'option Archive permanente dans une recherche, puis supprimer la recherche.

## Conservation de boîtes aux lettres pour la découverte électronique locale

Quand un employé quitte une organisation, la boîte aux lettres est habituellement désactivée ou supprimée. Après avoir été désactivée, une boîte aux lettres est déconnectée du compte d'utilisateur, mais demeure dans la boîte aux lettres pendant une certaine période (30 jours par défaut). L'Assistant Dossier géré ne traite pas les boîtes aux lettres déconnectées et aucune stratégie de rétention n'est appliquée durant cette période. Vous ne pouvez pas rechercher le contenu d'une boîte aux lettres déconnectée. Quand la période de rétention de la boîte aux lettres supprimée configurée pour la base de données de boîtes aux lettres est écoulée, la boîte aux lettres est purgée de la base de données des boîtes aux lettres.

> [!NOTE]
> Dans Exchange Online, la découverte électronique locale peut rechercher du contenu dans les boîtes aux lettres inactives. Les boîtes aux lettres inactives sont des boîtes aux lettres placées en archive permanente ou mises en attente pour litige avant d'être supprimées. Les boîtes aux lettres inactives sont conservées tant qu’elles sont mises en attente. Quand l'état Archive permanente ou Mise en attente pour litige est enlevé pour une boîte aux lettres, cette dernière est définitivement supprimée. Pour plus d’informations, consultez la rubrique <a href="https://technet.microsoft.com/fr-fr/library/dn144876(v=exchg.150)">Gestion des boîtes aux lettres inactives dans Exchange Online</a>.


Dans un déploiement local, si votre organisation requiert que des paramètres de conservation soient appliqués à des messages d'employés qui ne font plus partie de l'organisation ou si vous avez besoin de conserver la boîte aux lettres d'un ancien employé pour une recherche de découverte électronique en cours ou future, vous ne devez ni désactiver, ni supprimer la boîte aux lettres. Vous pouvez prendre les mesures suivantes pour garantir que la boîte aux lettres ne soit pas accessible et que de nouveaux messages n'y soient pas remis.

1.  Désactivez le compte d'utilisateur Active Directory avec les **Utilisateurs & ordinateurs Active Directory** ou bien d'autres outils ou scripts Active Directory ou d'attribution de privilèges d'accès aux comptes. Ceci empêche la connexion à des boîtes aux lettres en utilisant le compte d'utilisateur associé.
    
    > [!NOTE]
    > Les utilisateurs disposant d'une autorisation d'accès total aux boîtes aux lettres conservent l'accès aux boîtes aux lettres. Pour empêcher l'accès des autres utilisateurs, vous devez supprimer leur autorisation d'accès total de la boîte aux lettres. Pour obtenir des informations sur la suppression des autorisations d'accès total aux boîtes aux lettres, consultez la rubrique <a href="manage-permissions-for-recipients-exchange-online-help.md">Gestion des autorisations des destinataires</a>.


2.  Définissez une très petite taille limite des messages pouvant être envoyés ou reçus par l'utilisateur de la boîte aux lettres, par exemple 1 Ko. Ceci empêche la remise de nouveaux messages en direction et en provenance de la boîte aux lettres. Pour plus d'informations, consultez la rubrique [Configurer des limites de taille de messages pour une boîte aux lettres](configure-message-size-limits-for-a-mailbox-exchange-2013-help.md).

3.  Configurez les restrictions de remise pour la boîte aux lettres de manière à ce que personne ne puisse lui envoyer de messages. Pour plus d'informations, consultez la rubrique [Configurer les restrictions de remise de message pour une boîte aux lettres](configure-message-delivery-restrictions-for-a-mailbox-exchange-2013-help.md).

> [!NOTE]
> Vous devez prendre les mesures ci-dessous en liaison avec tous les autres processus de gestion de compte requis, mais sans désactiver ou supprimer la boîte aux lettres ou le compte d'utilisateur associé.


Quand vous prévoyez d'implémenter la rétention de boîtes aux lettres pour la gestion de la rétention (MRM) ou la découverte électronique locale des messages, vous devez tenir compte de la rotation des employés. La rétention à long terme de boîtes aux lettres d'anciens employés nécessitera un stockage supplémentaire sur les serveurs de boîtes aux lettres et entraînera également une augmentation de la base de données Active Directory, étant donné que le compte d'utilisateur associé devra être retenu pendant la même durée. Des modifications de l'attribution des privilèges d'accès aux comptes et des processus de gestion dans votre organisation seront en outre nécessaires.

Retour au début

## Limites et stratégies de limitation des découvertes électroniques locales

Dans Exchange 2013 et Exchange Online, les ressources que la découverte électronique locale peut consommer sont contrôlées à l’aide des stratégies de limitation.

La stratégie de limitation par défaut contient les paramètres de limitation suivants.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Paramètre</th>
<th>Description</th>
<th>Valeur par défaut</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>DiscoveryMaxConcurrency</p></td>
<td><p>Nombre maximal de recherches de découverte électronique inaltérables pouvant être exécutées en même temps dans votre organisation</p></td>
<td><p>2</p>
> [!NOTE]
> Si une recherche de découverte électronique est lancée alors que deux recherches précédentes sont toujours en cours d’exécution, la troisième recherche ne sera pas ajoutée à la file d’attente et échouera. Vous devez patienter jusqu’à ce que l’une des recherches précédentes soit terminée avant de pouvoir lancer une nouvelle recherche.

</td>
</tr>
<tr class="even">
<td><p>DiscoveryMaxMailboxes</p></td>
<td><p>Nombre maximal de boîtes aux lettres pouvant être recherchées dans une seule recherche de découverte électronique locale.</p></td>
<td><p>Exchange Online: 10,0001</p>
<p>Exchange 2013: 5,000</p></td>
</tr>
<tr class="odd">
<td><p>DiscoveryMaxStatsSearchMailboxes</p></td>
<td><p>Nombre maximal de boîtes aux lettres consultables en une seule recherche de découverte électronique inaltérable et permettant d’afficher les statistiques sur les mots-clés.</p></td>
<td><p>100</p>
> [!NOTE]
> Une fois que vous avez exécuté une estimation de recherche de découverte électronique, vous pouvez afficher les statistiques sur les mots clés. Ces statistiques présentent des informations sur le nombre d’éléments renvoyés pour chaque mot-clé utilisé dans la requête de recherche. Si plus de 100 boîtes aux lettres source sont incluses dans la recherche, une erreur sera renvoyée si vous tentez d’afficher les statistiques sur les mots-clés.

</td>
</tr>
<tr class="even">
<td><p>DiscoveryMaxKeywords</p></td>
<td><p>Nombre maximal de mots clés pouvant être spécifiés dans une seule recherche de découverte électronique locale.</p></td>
<td><p>500</p></td>
</tr>
<tr class="odd">
<td><p>DiscoveryMaxSearchResultsPageSize</p></td>
<td><p>Nombre maximal d’éléments affichés dans une seule page lors de la prévisualisation des résultats de recherche de découverte électronique locale.</p></td>
<td><p>200</p></td>
</tr>
<tr class="even">
<td><p>DiscoverySearchTimeoutPeriod</p></td>
<td><p>Nombre de minutes pendant lequel une recherche de découverte électronique locale est exécutée avant son expiration.</p></td>
<td><p>10 minutes</p></td>
</tr>
</tbody>
</table>


> [!NOTE]
> 1   Si vous avez une organisation Office 365 et que vous lancez une recherche eDiscovery à partir du centre eDiscovery dans SharePoint Online, vous pouvez parcourir jusqu’à 1 500 boîtes aux lettres en une seule recherche.


Dans Exchange Server 2013, vous pouvez modifier les valeurs par défaut de ces paramètres en fonction de vos besoins, ou créer des stratégies de limitation supplémentaires et les affecter aux utilisateurs avec une autorisation de gestion de découverte déléguée. Dans Exchange Online, les valeurs par défaut de ces paramètres de limitation ne peuvent pas être modifiées.

## Documentation relative à la découverte électronique locale

Le tableau suivant contient des liens vers des rubriques qui vous permettront d’en savoir plus sur la découverte électronique locale et la façon de la gérer.


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
<td><p><a href="assign-ediscovery-permissions-in-exchange-exchange-2013-help.md">Attribution d’autorisations eDiscovery dans Exchange</a></p></td>
<td><p>Découvrez comment permettre à un utilisateur d’accéder à la découverte électronique locale dans le CAE pour effectuer des recherches dans des boîtes aux lettres Exchange. L’ajout d’un utilisateur au groupe de rôles Gestion de la découverte permet également à cette personne d’utiliser le Centre de découverte électronique dans SharePoint 2013 et SharePoint Online pour y effectuer des recherches dans les boîtes aux lettres Exchange.</p></td>
</tr>
<tr class="even">
<td><p><a href="create-a-discovery-mailbox-exchange-2013-help.md">Créer une boîte aux lettres de découverte</a></p></td>
<td><p>Découvrez comment utiliser l’environnement de ligne de commande Exchange Management Shell pour créer une boîte aux lettres de découverte et affecter des autorisations d’accès.</p></td>
</tr>
<tr class="odd">
<td><p><a href="create-an-in-place-ediscovery-search-exchange-2013-help.md">Créer une recherche de découverte électronique inaltérable</a></p></td>
<td><p>Découvrez comment créer une recherche de découverte électronique locale, ainsi qu’estimer et afficher ses résultats.</p></td>
</tr>
<tr class="even">
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=506799">Propriétés de message et opérateurs de recherche pour eDiscovery inaltérable</a></p></td>
<td><p>Découvrez les propriétés de message électronique qui peuvent faire l’objet d’une recherche à l’aide de la découverte électronique inaltérable. Cette rubrique fournit des exemples de syntaxe pour chaque propriété, des informations sur les opérateurs de recherche (tels que <strong>AND</strong> et <strong>OR</strong>), ainsi que des renseignements sur d’autres techniques de requête de recherche, telles que l’utilisation des guillemets (&quot; &quot;) et des caractères génériques de préfixe.</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://technet.microsoft.com/fr-fr/library/dn798915(v=exchg.150)">Limites de recherche pour la découverte électronique sur place dans Exchange Online</a></p></td>
<td><p>Découvrez les limites de la découverte électronique sur place dans Exchange Online qui permettent de maintenir l’intégrité et la qualité des services de découverte électronique pour les organisations Office 365.</p></td>
</tr>
<tr class="even">
<td><p><a href="start-or-stop-an-in-place-ediscovery-search-exchange-2013-help.md">Lancement ou arrêt d’une recherche de découverte électronique inaltérable</a></p></td>
<td><p>Découvrez comment démarrer, arrêter et redémarrer des recherches de découverte électronique locale.</p></td>
</tr>
<tr class="odd">
<td><p><a href="modify-an-in-place-ediscovery-search-exchange-2013-help.md">Modifier une recherche de découverte électronique inaltérable</a></p></td>
<td><p>Découvrez comment modifier une recherche de découverte électronique locale existante.</p></td>
</tr>
<tr class="even">
<td><p><a href="copy-ediscovery-search-results-to-a-discovery-mailbox-exchange-2013-help.md">Copier les résultats de la recherche de découverte automatique dans une boîte aux lettres de découverte</a></p></td>
<td><p>Découvrez comment copier les résultats d’une recherche de découverte électronique à une boîte aux lettres de découverte.</p></td>
</tr>
<tr class="odd">
<td><p><a href="export-ediscovery-search-results-to-a-pst-file-exchange-2013-help.md">Exporter les résultats de la recherche électronique vers un fichier PST</a></p></td>
<td><p>Découvrez comment exporter les résultats d’une recherche de découverte électronique vers un fichier PST.</p></td>
</tr>
<tr class="even">
<td><p><a href="create-a-custom-management-scope-for-in-place-ediscovery-searches-exchange-2013-help.md">Création d’une étendue de gestion personnalisée pour les recherches de découverte électronique sur place</a></p></td>
<td><p>Découvrez comment utiliser les étendues de gestion personnalisées pour limiter les boîtes aux lettres qu’un gestionnaire de découverte peut rechercher.</p></td>
</tr>
<tr class="odd">
<td><p><a href="remove-an-in-place-ediscovery-search-exchange-2013-help.md">Suppression d’une recherche de découverte électronique inaltérable</a></p></td>
<td><p>Découvrez comment supprimer une recherche de découverte électronique.</p></td>
</tr>
<tr class="even">
<td><p><a href="search-for-and-delete-messages-admin-help-exchange-2013-help.md">Recherche et suppression de messages - Aide de l’administrateur</a></p></td>
<td><p>Apprenez à utiliser la cmdlet <strong>Search-Mailbox</strong> pour rechercher et supprimer des messages électroniques.</p></td>
</tr>
<tr class="odd">
<td><p><a href="reduce-the-size-of-a-discovery-mailbox-in-exchange-exchange-2013-help.md">Réduction de la taille d’une boîte aux lettres de découverte dans Exchange</a></p></td>
<td><p>Utilisez ce processus pour réduire la taille d’une boîte aux lettres de découverte qui dépasse 50 Go.</p></td>
</tr>
<tr class="even">
<td><p><a href="delete-and-re-create-the-default-discovery-mailbox-in-exchange-exchange-2013-help.md">Suppression et recréation de la boîte aux lettres de découverte par défaut dans Exchange</a></p></td>
<td><p>Apprenez à supprimer la boîte aux lettres de découverte par défaut, à la recréer, puis à lui réattribuer des autorisations. Utilisez cette procédure si cette boîte aux lettres a dépassé la limite de 50 Go et que vous n’avez pas besoin des résultats de la recherche.</p></td>
</tr>
<tr class="odd">
<td><p><a href="re-create-the-discovery-system-mailbox-exchange-2013-help.md">Re-create the Discovery system mailbox</a></p></td>
<td><p>Découvrez comment recréer la boîte aux lettres système de découverte. Cette tâche s’applique uniquement aux entreprises Exchange 2013.</p></td>
</tr>
<tr class="even">
<td><p><a href="using-oauth-authentication-to-support-ediscovery-in-an-exchange-hybrid-deployment-exchange-2013-help.md">Utilisation de l’authentification OAuth pour prendre en charge la découverte électronique dans un déploiement hybride Exchange</a></p></td>
<td><p>En savoir plus sur les scénarios de découverte électronique nécessitant la configuration de l’authentification OAuth dans le cadre d’un déploiement hybride Exchange.</p></td>
</tr>
<tr class="odd">
<td><p><a href="configure-exchange-for-sharepoint-ediscovery-center-exchange-2013-help.md">Configurer Exchange pour le Centre de découverte électronique SharePoint</a></p></td>
<td><p>Découvrez comment configurer Exchange 2013 de façon à ce que vous puissiez utiliser le centre de découverte dans SharePoint 2013 et effectuer des recherches dans des boîtes aux lettres Exchange.</p></td>
</tr>
<tr class="even">
<td><p><a href="unsearchable-items-in-exchange-ediscovery-exchange-2013-help.md">Éléments impossibles à rechercher dans la découverte électronique Exchange</a></p></td>
<td><p>En savoir plus sur les éléments de boîtes aux lettres ne pouvant pas être indexés par la recherche Exchange et qui apparaissent dans la recherche de découverte électronique comme des éléments impossibles à rechercher.</p></td>
</tr>
</tbody>
</table>


Pour plus d’informations sur eDiscovery dans Office 365, Exchange 2013, SharePoint 2013 et Lync 2013, consultez la [FAQ sur eDiscovery](https://go.microsoft.com/fwlink/p/?linkid=386633).

Retour au début

