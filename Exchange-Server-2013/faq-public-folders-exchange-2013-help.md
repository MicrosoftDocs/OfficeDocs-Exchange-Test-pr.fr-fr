---
title: 'FAQ : Dossiers publics: Exchange 2013 Help'
TOCTitle: 'FAQ : Dossiers publics'
ms:assetid: 1cdcdcb7-f11b-45ca-ad23-7c38f640208c
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ552408(v=EXCHG.150)
ms:contentKeyID: 50477610
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# FAQ : Dossiers publics

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2017-03-27_

Cette rubrique contient une liste des questions fréquemment posées concernant les dossiers publics d’Exchange Server 2013. Pour en savoir plus sur les dossiers publics, voir [Dossiers publics](public-folders-exchange-2013-help.md).

Certaines questions sur des dossiers publics sont-elles restées sans réponses dans ce document ? Envoyez-nous un courrier électronique à l’adresse [Ex2013HelpFeedback@microsoft.com](mailto:ex2013helpfeedback@microsoft.com).

## FAQ sur la migration des dossiers publics

Cette section contient des questions fréquemment posées à propos de la migration de dossiers publics. Pour plus d’informations, consultez [Utiliser la migration par lots pour migrer les dossiers publics vers Exchange 2013 à partir de versions antérieures](use-batch-migration-to-migrate-public-folders-to-exchange-2013-from-previous-versions-exchange-2013-help.md), [Utilisation de la migration par lot pour migrer des dossiers publics vers Office 365 et Exchange Online](https://docs.microsoft.com/fr-fr/exchange/collaboration-exo/public-folders/batch-migration-of-legacy-public-folders)ou [Utilisation de la migration par lot pour migrer des dossiers publics Exchange 2013 vers Exchange Online](https://docs.microsoft.com/fr-fr/exchange/collaboration-exo/public-folders/batch-migration-of-exchange-2013-public-folders).

## Quels sont les scénarios de migration de dossiers publics pris en charge ?

La liste suivante énumère les options disponibles pour migrer des dossiers publics vers Exchange 2013 ou Exchange Online.

  - Les dossiers publics Exchange 2007 (SP3 RU15 ou version ultérieure) peuvent être migrés vers Exchange 2013 ou Exchange Online.

  - Les dossiers publics Exchange 2010 (SP3 RU8 ou version ultérieure) peuvent être migrés vers Exchange 2013 ou Exchange Online.

  - Les dossiers publics Exchange 2013 (CU15 ou version ultérieure) peuvent être migrées vers Exchange Online.

Actuellement, seules migrations à Exchange 2013 dans la même forêt Active Directory sont pris en charge. Les migrations entre forêts seront prise en charge à l’avenir.

## Après la migration, qu’advient-il de la hiérarchie sur les serveurs Exchange 2010 ?

Durant l’étape de finalisation de la migration, un verrou est placé sur le serveur source pour en empêcher l’accès à tout utilisateur. Ce verrou reste en place pour empêcher les utilisateurs d’accéder aux dossiers publics source à l’issue de la migration. Même si vous pouvez déverrouiller ce verrou, cette opération est fortement déconseillée car les modifications ne peuvent pas être synchronisées avec Exchange 2013.

## Lors de la migration de dossiers publics, qu’advient-il des règles de dossiers publics existante ?

Les règles de dossiers publics sont migrées conjointement avec les données et conservées sous la forme de règles de dossiers publics. Elles ne sont pas converties en règles de boîte aux lettres.

## Que se passe-t-il si des modifications de la hiérarchie sont effectuées sur la source après la génération du fichier .csv initial ? Quelles seraient les répercutions de ces modifications sur la destination ?

Le fichier .csv est utilisé pour déterminer le mappage entre la hiérarchie source et la boîte aux lettres de destination. Il ne contient que les dossiers de niveau supérieur. Les dossiers enfants sous les dossiers de niveau supérieur sont automatiquement migrés. Par conséquent, si un nouveau dossier enfant est ajouté, il est migré pendant le processus. Si un nouveau dossier de niveau supérieur est créé, il l’est dans la boîte aux lettres qui contient l’exemplaire de la hiérarchie dans laquelle les opérations d’écriture sont autorisées.

## Pendant la migration vers des dossiers publics Exchange 2013, si un intervalle prolongé sépare la suspension et la finalisation, comment puis-je forcer une synchronisation Delta de sorte que les utilisateurs puissent accéder aux dossiers publics pendant la synchronisation finale ?

Vous pouvez forcer une synchronisation Delta finale avant la finalisation (avant de verrouiller la source) en exécutant la commande Shell suivante :

    Resume-PublicFolderMigrationRequest \PublicFolderMigration

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Resume-PublicFolderMigrationRequest](https://technet.microsoft.com/fr-fr/library/jj218689\(v=exchg.150\)).

## Pour la migration d’une hiérarchie distribuée géographiquement, comme puis-je m’assurer que les dossiers publics sont créés à l’endroit le plus proche des utilisateurs cibles ?

Dans le cadre du processus de migration, un fichier .csv est généré (à l’aide du script `publicfoldertomailboxmapgenerator.ps1`). Ce fichier contient le mappage dossier-boîte aux lettres de la nouvelle hiérarchie. Vous pouvez utiliser ce fichier .csv pour créer des boîtes aux lettres de dossiers publics à l’emplacement géographique approprié et modifier le fichier .csv pour placer les dossiers souhaités dans la boîte aux lettres appropriée, à proximité des utilisateurs cibles.

Vous pouvez générer le fichier .csv en entrée en exécutant le script `AggregatePFData.ps1` qui se trouve dans le répertoire \<*Dossier d’installation d’Exchange*\>\\V15\\Scripts. Exécutez le script comme suit :

    .\AggregatePFData.ps1 | Select-Object -property @{Name="FolderName"; Expression = {$_.Identity}}, @{Name="FolderSize"; Expression = {$_.TotalItemSize.Value.ToBytes()}} | Export-CSV -Path <Path followed by the name of the CSV>

## Est-ce que les autorisations de dossier public migrent ?

Oui, les autorisations sont automatiquement migrées avec les données au niveau du dossier. Vous ne devez pas exécuter cette étape séparément.

## Est-ce que les dossiers publics vont disparaître ?

Non. Les dossiers publics sont tout à fait adaptés aux scénarios d’intégration dans Outlook et de partage simples, et pour autoriser l’accès aux mêmes données par un large public.

## Quels clients prennent en charge les dossiers publics ?

Les utilisateurs d’Outlook 2007, d’Outlook 2010 et d’Outlook 2013, ainsi que d’Outlook 2011 pour Mac peuvent accéder aux dossiers publics. Cependant, les utilisateurs dont les boîtes aux lettres se trouvent sur les serveurs Exchange 2013 ne pourront pas se connecter aux dossiers publics Exchange 2007 ou Exchange 2010 à partir de clients qui utilisent les services web Exchange (EWS), comme Outlook pour Mac. Nous vous recommandons de migrer les dossiers publics hérités vers Exchange 2013 afin de maintenir l’accès pour ces utilisateurs.

## Y a-t-il des restrictions dans les clients ?

Outlook Web App est pris en charge, mais dans certaines limites. Vous pouvez ajouter et supprimer des dossiers publics favoris (dossiers publics de messagerie, de publication, de calendrier et de contact), ainsi qu’effectuer des opérations au niveau des éléments, telles que la création, la modification et la suppression de publications, et la réponse à des publications. Toutefois, vous ne pouvez pas effectuer les actions suivantes dans Outlook Web App :

  - Créer ou supprimer des dossiers publics

  - Glisser-déplacer du contenu

  - Accéder aux dossiers publics situés sur des serveurs exécutant des versions antérieures d’Exchange

> [!NOTE]
> Vous pouvez uniquement créer des règles de dossier public qui contiennent l’élément <strong>répondre en utilisant un modèle spécifique</strong> dans les dossiers publics à extension messagerie. Il peut arriver que des règles préexistantes contenant l’élément <strong>répondre en utilisant un modèle spécifique</strong> continuent de fonctionner sur des dossiers publics sans extension messagerie. Cela dit, vous ne pouvez pas créer ou modifier de règles comportant cet élément pour ce type de dossiers.


Dans un scénario hybride, Outlook sur le web et Outlook 2011 pour Mac ne sont pas pris en charge pour les dossiers publics intersites. Les utilisateurs doivent être au même emplacement que les dossiers publics pour pouvoir y accéder avec Outlook 2011 pour Mac ou Outlook sur le web. Les utilisateurs d’Outlook 2016 pour Mac peuvent accéder aux dossiers publics dans un scénario hybride, si les procédures sous [Procédures de déploiement hybride](https://technet.microsoft.com/fr-fr/library/jj200788\(v=exchg.150\).aspx) sont respectées et si la mise à jour Avril 2016 pour Outlook 2016 pour Mac a été installée sur tous les clients.

## Comment puis-je stocker une hiérarchie très importante dans une boîte aux lettres de dossier public ?

Pour plus d’informations sur les limites de stockage de dossier public, consultez la rubrique [Limites pour les dossiers publics](limits-for-public-folders-exchange-2013-help.md).

## Comment puis-je afficher la boîte aux lettres de dossiers publics de la hiérarchie ?

Exécutez la commande suivante :

    Get-OrganizationConfig | Format-List RootPublicFolderMailbox

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, consultez la rubrique [Get-OrganizationConfig](https://technet.microsoft.com/fr-fr/library/aa997571\(v=exchg.150\)).

## Comment puis-je créer des boîtes aux lettres de contenu pour des dossiers publics à l’aide de cmdlets de l’environnement de ligne de commande Exchange Management Shell ?

Exécutez la commande suivante pour créer la première boîte aux lettres de dossier public de la hiérarchie principale et les boîtes aux lettres de la hiérarchie secondaire.

    New-Mailbox -PublicFolder -Name <name of public folder>

Pour plus d’informations, consultez la rubrique [Créer un dossier public](https://docs.microsoft.com/fr-fr/exchange/collaboration-exo/public-folders/create-public-folder).

## Dans les versions précédentes d’Exchange, une option permettait de spécifier la base de données de dossiers publics de chaque base de données de boîtes aux lettres. Comment cela est-il possible dans Exchange 2013 ?

Il n’existe aucun paramètre au niveau de la base de données dans Exchange 2013. Exchange 2013 inclut une fonctionnalité de niveau boîte aux lettres qui permet de spécifier la boîte aux lettres de dossiers publics. Toutefois, par défaut, Exchange calcule automatiquement la boîte aux lettres de la hiérarchie pour chaque utilisateur.

## Comment les outils de métrique des dossiers publics sont-ils utilisés dans Exchange 2013 ?

Dans Exchange 2013, les cmdlets [Get-PublicFolderStatistics](https://technet.microsoft.com/fr-fr/library/aa998663\(v=exchg.150\)) et [Get-PublicFolderItemStatistics](https://technet.microsoft.com/fr-fr/library/ee332344\(v=exchg.150\)) vous permettent d’obtenir des données de métrique des dossiers publics. Rien n’a changé, car cette solution est identique à celle d’Exchange 2010. Les dossiers publics ne nécessitent pas de complément supplémentaire de création de rapports.

## Les dossiers publics peuvent-ils faire la différence entre l’accès interne à des dossiers publics et l’accès par un tiers ?

Dans Exchange 2013, le contrôle d’accès basé sur les rôles (RBAC) assure la gestion des autorisations de dossiers publics. Les listes de contrôle d’accès (ACL) ne sont pas utilisées dans Exchange 2013. Vous pouvez utiliser les cmdlets [Get-PublicFolderStatistics](https://technet.microsoft.com/fr-fr/library/aa998663\(v=exchg.150\)) et [Get-PublicFolderItemStatistics](https://technet.microsoft.com/fr-fr/library/ee332344\(v=exchg.150\)) pour effectuer un suivi des comptes qui effectuent des tâches administratives, puis contrôler l’accès en conséquence. Pour en savoir plus sur RBAC, consultez la rubrique [Présentation du contrôle d'accès basé sur un rôle](understanding-role-based-access-control-exchange-2013-help.md).

## Est-ce la création de journaux d’audit de boîte aux lettres est possible avec des dossiers publics ?

Non, pas pour l’instant.

## Quelles sont les limites imposées aux dossiers publics ? Quelles sont les recommandations ?

Pour plus d’informations sur les limites de dossier public, consultez la rubrique [Limites pour les dossiers publics](limits-for-public-folders-exchange-2013-help.md).

## Quelle est la procédure recommandée pour partager des boîtes aux lettres de dossier public ? Doivent-elles rester dans la même base de données ?

Dans les versions précédentes d’Exchange, vous pouviez diviser des dossiers publics entre plusieurs bases de données de dossiers publics. Vous pouvez décider de diviser le contenu d’une boîte aux lettres de dossiers publics vers une boîte aux lettres sur la même base de données de boîtes aux lettres ou sur une base de données différente. En règle générale, il est recommandé de placer une partie du contenu sur une base de données distincte afin d’équilibrer le stockage et les E/S.

## Est-il possible de définir des stratégies de rétention sur les dossiers publics ?

Tout comme les versions précédentes d’Exchange, vous pouvez définir des limites de rétention sur les éléments. Pour plus d’informations, consultez la rubrique [Limites pour les dossiers publics](limits-for-public-folders-exchange-2013-help.md).

## Est-il possible de spécifier les utilisateurs pouvant utiliser une boîte aux lettres de dossiers publics ?

Dans Exchange 2007 et Exchange 2010, vous pouvez spécifier les utilisateurs ayant eu accès à des dossiers publics spécifiques. Dans Exchange 2013, vous pouvez définir la boîte aux lettres de dossier public par défaut pour chaque utilisateur. Pour cela, exécutez la cmdlet [Set-Mailbox](https://technet.microsoft.com/fr-fr/library/bb123981\(v=exchg.150\)) en association avec le paramètre *DefaultPublicFolderMailbox*.

    Set-Mailbox -Identity kweku@contoso.com -DefaultPublicFolderMailbox "PF_Administration"

## Si la hiérarchie principale n’est plus disponible, quel impact cela a-t-il sur l’utilisateur ?

Si la boîte aux lettres de dossiers publics de la hiérarchie principale n’est plus disponible, les utilisateurs peuvent afficher, mais pas écrire dans les dossiers publics. Pour empêcher qu’une hiérarchie ne soit plus disponible, il est recommandé d’inclure vos dossiers publics dans un groupe de disponibilité de base de données (DAG). Pour en savoir plus sur les groupes de disponibilité de base de données, consultez la rubrique [Groupe de disponibilité de base de données (DAG)](database-availability-groups-dags-exchange-2013-help.md).

## Est-il possible de modifier la boîte aux lettres de dossiers publics de la hiérarchie principale ?

Non. Si vous essayez de modifier la boîte aux lettres de la hiérarchie principale, une erreur se produit.

## Les dossiers publics comportent-ils des fonctionnalités de recherche de texte intégral ?

Oui, la recherche de texte intégral est disponible pour les dossiers publics dans Exchange 2013. Cependant, vous ne pouvez pas effectuer de recherche dans plusieurs dossiers publics.

