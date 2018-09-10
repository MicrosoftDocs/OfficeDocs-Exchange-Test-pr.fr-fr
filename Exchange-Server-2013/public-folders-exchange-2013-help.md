---
title: 'Dossiers publics: Exchange 2013 Help'
TOCTitle: Dossiers publics
ms:assetid: 94c4fb69-9234-4b34-8c1c-da2a0a11da65
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ150538(v=EXCHG.150)
ms:contentKeyID: 50478729
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Dossiers publics

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2017-03-27_

Les dossiers publics sont conçus pour assurer un accès partagé et offrir une manière simple et efficace de collecter, d'organiser et de partager des informations avec d'autres personnes de votre groupe de travail ou de votre organisation. Les dossiers publics aident à organiser un contenu sous la forme d’une hiérarchie profonde, facile à parcourir. Les utilisateurs peuvent voir la hiérarchie complète dans Outlook, ce qui leur permet de parcourir aisément le contenu qui les intéresse.

> [!NOTE]
> Des dossiers publics sont disponibles dans les clients Outlook suivants : Outlook Web App pour Exchange 2013, Outlook 2007, Outlook 2010, Outlook 2013 et Outlook pour Mac.


Les dossiers publics peuvent également servir de méthode d'archivage pour des groupes de distribution. Lorsque vous activez la messagerie unifiée pour un dossier public et ajoutez ce dernier comme membre du groupe de distribution, le courrier envoyé au groupe est automatiquement ajouté au dossier public pour référence ultérieure.

> [!NOTE]
> Pour accéder à des dossiers publics sur des serveurs Exchange 2013, vous devez utiliser Outlook 2007 ou une version ultérieure.


Les dossiers publics ne sont pas conçus pour effectuer les opérations suivantes :

  - **Archivage des données** Les utilisateurs qui ont des limites de boîtes aux lettres utilisent parfois des dossiers publics au lieu de boîtes aux lettres pour archiver des données. Cette pratique est déconseillée, car elle affecte le stockage dans les dossiers publics et va à l'encontre de l'objectif des limites de boîtes aux lettres. Au lieu de cela, nous vous recommandons d'utiliser [Archivage inaltérable dans Exchange 2013](in-place-archiving-in-exchange-2013-exchange-2013-help.md) comme solution d'archivage.

  - **Partage de documents et collaboration** Les dossiers publics n’intègrent pas de fonction de contrôle de version ou d’autres fonctions de gestion des documents, telles que la fonctionnalité d’archivage et d’extraction, et les notifications automatiques de modification du contenu. Au lieu de cela, nous vous recommandons d’utiliser [SharePoint](https://go.microsoft.com/fwlink/?linkid=282474) comme solution de partage de documentation.

Pour plus d'informations sur les dossiers publics et d'autres méthodes de collaboration dans Exchange 2013, consultez la rubrique [Collaboration](collaboration-exchange-2013-help.md).

Pour parcourir certaines des questions fréquemment posées à propos des dossiers publics dans Microsoft Exchange 2013, consultez la rubrique [FAQ : Dossiers publics](faq-public-folders-exchange-2013-help.md).

Pour plus d’informations sur les limites et les quotas pour les dossiers publics, consultez la rubrique [Limites pour les dossiers publics](limits-for-public-folders-exchange-2013-help.md).

Pour obtenir la liste des tâches de gestion des dossiers publics, consultez la rubrique [Procédures relatives aux dossiers publics](public-folder-procedures-exchange-2013-help.md).

Vous recherchez la version Exchange Online de cette rubrique ? Consultez la rubrique [Dossiers publics dans Office 365 et Exchange Online](https://technet.microsoft.com/fr-fr/library/jj200758\(v=exchg.150\)).

**Contenu de cette rubrique**

Architecture des dossiers publics

Migrer des dossiers publics

Déplacements de dossiers publics

Quotas de dossiers publics

Récupération d'urgence

## Architecture des dossiers publics

Dans Exchange 2013, les dossiers publics ont été remaniés à l'aide d'une infrastructure de boîtes aux lettres, afin de tirer parti des technologies existantes de haute disponibilité et de stockage de la base de données de boîtes aux lettres. L'architecture de dossiers publics utilise des boîtes aux lettres spécialement conçues pour stocker tant la hiérarchie que le contenu des dossiers publics. Ceci signifie également qu’il n'existe plus de base de données de dossiers publics. C'est le groupe de disponibilité de base de données (DAG) qui assure la haute disponibilité haute disponibilité des boîtes aux lettres de dossiers publics. Pour en savoir plus sur les groupes DAG, consultez la rubrique [Groupe de disponibilité de base de données (DAG)](database-availability-groups-dags-exchange-2013-help.md).

Les principaux composants architecturaux des dossiers publics sont les boîtes aux lettres de dossier public qui peuvent résider dans une ou plusieurs bases de données de boîtes aux lettres.

## Boîtes aux lettres de dossiers publics

Il existe deux types de boîtes aux lettres de dossiers publics : la *boîte aux lettres de hiérarchie principale* et la *boîte aux lettres de hiérarchie secondaire*. Les deux types de boîtes aux lettres peuvent accueillir du contenu :

  - **Boîte aux lettres de hiérarchie principale**   La boîte aux lettres de hiérarchie principale est l’unique copie accessible en écriture de la hiérarchie de dossiers publics. La hiérarchie de dossiers publics est copiée dans toutes les autres boîtes aux lettres de dossiers publics, mais ces dernières sont des copies en lecture seule.

  - **Boîtes aux lettres de hiérarchie secondaire**   Les boîtes aux lettres de hiérarchie secondaire accueillent du contenu de dossier public ainsi qu’une copie en lecture seule de la hiérarchie de dossiers publics.

> [!NOTE]
> Les stratégies de rétention ne sont pas prises en charge pour les boîtes aux lettres de dossiers publics.


Vous pouvez gérer les boîtes aux lettres de dossiers publics de deux manières :

  - Dans le Centre d’administration Exchange (CAE), accédez à **Dossiers publics**\>**Boîtes aux lettres de dossiers publics**.

  - Dans l'environnement de ligne de commande Exchange Management Shell, utilisez le jeu de cmdlets **\*-Mailbox**. Pour la prise en charge des boîtes aux lettres de dossiers publics, les paramètres suivants ont été ajoutés à la cmdlet [New-Mailbox](https://technet.microsoft.com/fr-fr/library/aa997663\(v=exchg.150\)) :
    
      - *PublicFolder*   Ce paramètre est utilisé avec la cmdlet **New-Mailbox** pour créer une boîte aux lettres de dossiers publics. Lorsque vous créez une boîte aux lettres de dossiers publics, une nouvelle boîte aux lettres du type `PublicFolder` est créée. Pour plus d'informations, consultez la rubrique [Création d’une boîte aux lettres de dossiers publics](https://docs.microsoft.com/fr-fr/exchange/collaboration-exo/public-folders/create-public-folder-mailbox).
    
      - *HoldForMigration*   Ce paramètre est utilisé uniquement si vous migrez vers Exchange 2013 des dossiers publics d'une version antérieure. Pour plus d'informations, consultez la section Migrer des dossiers publics plus loin dans cette rubrique.
    
      - *IsHierarchyReady*   Ce paramètre indique si la boîte aux lettres de dossiers publics est prête à servir la hiérarchie de dossiers publics aux utilisateurs. Il est défini sur `$True` uniquement après que l’ensemble de la hiérarchie a été synchronisée sur la boîte aux lettres de dossiers publics. Si le paramètre est défini sur $False, les utilisateurs ne l’utiliseront pas pour accéder à la hiérarchie. Toutefois, si vous définissez la propriété *DefaultPublicFolderMailbox* d’une boîte aux lettres utilisateur sur une boîte aux lettres de dossiers publics spécifique, l’utilisateur peut toujours accéder à la boîte aux lettres de dossiers publics spécifiée, même si le paramètre *IsHierarchyReady* est défini sur `$False`.
    
      - *IsExcludedFromServingHierarchy* Ce paramètre empêche les utilisateurs d'accéder à la hiérarchie de dossiers publics dans la boîte aux lettres de dossiers publics spécifiée. À des fins d'équilibrage de charge, les utilisateurs sont répartis de manière égale dans les boîtes aux lettres de dossiers publics par défaut. Si ce paramètre est défini sur une boîte aux lettres de dossiers publics, cette dernière n'est pas incluse dans cet équilibrage de charge automatique et les utilisateurs ne sont pas en mesure d'y accéder pour récupérer la hiérarchie de dossiers publics. En revanche, si vous définissez la propriété *DefaultPublicFolderMailbox* d'une boîte aux lettres utilisateur sur une boîte aux lettres de dossiers publics spécifique, l'utilisateur peut toujours accéder à la boîte aux lettres de dossiers publics spécifiée, même si le paramètre *IsExcludedFromServingHierarchy* est défini pour cette boîte aux lettres de dossiers publics.

Une boîte aux lettres de hiérarchie secondaire ne sert des informations de hiérarchie de dossiers publics aux utilisateurs que si elle est explicitement spécifiée dans les boîtes aux lettres des utilisateurs, à l’aide de la propriété *DefaultPublicFolderMailbox*, ou si les conditions suivantes sont remplies :

  - La propriété *IsHierarchyReady* de la boîte aux lettres de dossiers publics est définie sur `$True`.

  - La propriété *IsExcludedFromServingHierarchy* de la boîte aux lettres de dossiers publics est définie sur `$False`.

## Hiérarchie de dossiers publics

La hiérarchie de dossiers publics contient les propriétés des dossiers et des informations d'organisation, dont l'arborescence. Chaque boîte aux lettres de dossiers publics contient une copie de la hiérarchie de dossiers publics. Il n'existe qu'une seule copie accessible en écriture de la hiérarchie, à savoir la boîte aux lettres de dossiers publics principale. Pour un dossier spécifique, les informations de hiérarchie sont utilisées pour identifier les éléments suivants :

  - Autorisations sur le dossier

  - Place du dossier dans l'arborescence de dossiers publics (avec ses dossiers parents et enfants)

> [!NOTE]
> La hiérarchie ne contient pas d'informations sur les adresses de messagerie pour les dossiers publics à extension messagerie. Les adresses de messagerie sont stockées sur l'objet annuaire dans Active Directory.


## Synchronisation de hiérarchie

Le processus de synchronisation de la hiérarchie de dossiers publics utilise une méthode de synchronisation des changements incrémentielle (ICS), mécanisme permettant de surveiller et de synchroniser les modifications apportées à la hiérarchie ou au contenu d'une banque d'informations Exchange. Ces modifications incluent la création, la modification et la suppression de dossiers et de messages. Lorsque des utilisateurs sont connectés à des boîtes aux lettres de contenu et les utilisent, une synchronisation a lieu toutes les 15 minutes. Si aucun utilisateur n'est connecté à une boîte aux lettres de contenu, la synchronisation a lieu moins souvent (toutes les 24 heures). Si une opération d'écriture, telle la création d'un dossier, est effectuée sur la hiérarchie principale, la synchronisation a lieu immédiatement (de façon synchrone) sur la boîte aux lettres de contenu.

> [!IMPORTANT]
> Étant donné qu'il n'existe qu'une seule copie accessible en écriture de la hiérarchie, la création de dossier est transmise en proxy à la boîte aux lettres de la hiérarchie par la boîte aux lettres de contenu à laquelle les utilisateurs sont connectés.


Dans une grande organisation, lorsque vous créez une boîte aux lettres de dossiers publics, la hiérarchie doit se synchroniser sur ce dossier public avant que des utilisateurs puissent s'y connecter. Autrement, les utilisateurs peuvent voir une structure de dossiers publics incomplète en se connectant avec Outlook. Pour laisser le temps nécessaire à la synchronisation sans que des utilisateurs tentent de se connecter à la nouvelle boîte aux lettres de dossiers publics, définissez le paramètre *IsExcludedFromServingHierarchy* sur la cmdlet **New-Mailbox** lors de la création de la boîte aux lettres de dossiers publics. Ce paramètre empêche les utilisateurs de se connecter à la boîte aux lettres de dossiers publics nouvellement créé. Une fois la synchronisation terminée, exécutez la cmdlet [Set-Mailbox](https://technet.microsoft.com/fr-fr/library/bb123981\(v=exchg.150\)) avec le paramètre *IsExcludedFromServingHierarchy* défini sur `false`, indiquant que la boîte aux lettres de dossiers publics est prête pour connexion. Vous pouvez également utiliser la cmdlet [Get-PublicFolderMailboxDiagnostics](https://technet.microsoft.com/fr-fr/library/jj218720\(v=exchg.150\)) pour afficher l'état de synchronisation par les propriétés *SyncInfo* et *AssistantInfo*.

Pour plus d'informations, consultez la rubrique [Créer un dossier public](create-a-public-folder-exchange-2013-help.md).

## Contenu de dossier public

Le contenu de dossier public peut inclure des messages électroniques, des publications, des documents et des formulaires électroniques. Le contenu est stocké dans la boîte aux lettres de dossiers publics, mais n'est pas répliqué sur plusieurs boîtes aux lettres de dossiers publics. Tous les utilisateurs accèdent à la même boîte aux lettres de dossiers publics pour le même contenu. Si la recherche en texte intégral de contenu de dossier public est disponible, il n'est pas possible de rechercher dans le contenu de plusieurs dossiers publics, et le contenu n'est pas indexé par Exchange Search.

> [!NOTE]
> Outlook Web App est pris en charge, mais dans certaines limites. Vous pouvez ajouter et supprimer des dossiers publics favoris, ainsi qu'effectuer des opérations au niveau élément, telles que la création, la modification et la suppression de publications, et la réponse à des publications. En revanche, vous ne pouvez pas créer ou supprimer des dossiers publics dans Outlook Web App. En outre, seuls les dossiers Courrier, Calendrier et Contact peuvent être ajoutés à la liste des Favoris dans Outlook Web App.


## Migrer des dossiers publics

Vous pouvez migrer vos dossiers publics à partir de versions précédentes d’Exchange Server vers Exchange 2013 ou vers Exchange Online. Vous pouvez également migrer vos dossiers publics Exchange 2013 vers Exchange Online.

Si vous disposez de dossiers publics Exchange 2010 SP3 ou Exchange 2007 SP3 RU10 au sein de votre organisation avant l'installation d'Exchange 2013, vous devez les migrer vers Exchange 2013. Pour ce faire, utilisez les cmdlets **PublicFolderMigrationRequst**. Pour plus d'informations, consultez la rubrique [Utiliser la migration par lots pour migrer les dossiers publics vers Exchange 2013 à partir de versions antérieures](use-batch-migration-to-migrate-public-folders-to-exchange-2013-from-previous-versions-exchange-2013-help.md). Si votre organisation passe à Exchange Online, vous pouvez migrer vos dossiers publics dans le cloud et les mettre à niveau en même temps. Pour plus d’informations, consultez les rubriques [Utilisation de la migration par lot pour migrer des dossiers publics vers Office 365 et Exchange Online](https://docs.microsoft.com/fr-fr/exchange/collaboration-exo/public-folders/batch-migration-of-legacy-public-folders) et [Utilisation de la migration par lot pour migrer des dossiers publics Exchange 2013 vers Exchange Online](use-batch-migration-to-migrate-exchange-2013-public-folders-to-exchange-online-exchange-online-help.md).

Suite aux modifications apportées à la manière dont les dossiers publics sont stockés, les boîtes aux lettres Exchange héritées ne peuvent pas accéder à la hiérarchie de dossiers publics sur des serveurs Exchange 2013 ou sur Exchange Online. Toutefois, des boîtes aux lettres utilisateur sur des serveurs Exchange 2013 ou sur Exchange Online peuvent se connecter à des dossiers publics hérités. Votre organisation ne peut pas avoir simultanément des dossiers publics Exchange 2013 et des dossiers publics hérités. Cela signifie qu'il n'y a pas de coexistence entre versions. La migration de dossiers publics vers Exchange Server 2013 ou Exchange Online est actuellement un processus de basculement unique.

C’est pourquoi, avant de migrer vos dossiers publics, nous vous recommandons de migrer vos boîtes aux lettres héritées vers Exchange 2013 ou Exchange Online. Pour plus d’informations sur la migration de boîtes aux lettres, voir [Déplacements de boîtes aux lettres dans Exchange 2013](mailbox-moves-in-exchange-2013-exchange-2013-help.md), [Effectuer une migration à basculement de la messagerie vers Office 365](https://go.microsoft.com/fwlink/p/?linkid=536689) et [Effectuer une migration intermédiaire de la messagerie vers Office 365](https://go.microsoft.com/fwlink/p/?linkid=536687).

## Déplacements de dossiers publics

Vous pouvez déplacer des dossiers publics vers une autre boîte aux lettres de dossiers publics, ainsi que déplacer des boîtes aux lettres de dossiers publics vers d'autres bases de données de dossiers publics. Pour déplacer des dossiers publics vers d'autres boîtes aux lettres de dossiers publics, utilisez le jeu de cmdlets **PublicFolderMoveRequest**. Par défaut, les sous-dossiers du dossier public déplacé ne sont pas déplacés. Si vous voulez déplacer une branche de dossiers publics, vous pouvez utiliser le script `Move-PublicFolderBranch.ps1` installé par défaut avec Exchange 2013. Pour plus d'informations, consultez la rubrique [Déplacement d'un dossier public vers une autre boîte aux lettres de dossiers publics](move-a-public-folder-to-a-different-public-folder-mailbox-exchange-2013-help.md).

Outre le déplacement de dossiers publics, vous pouvez déplacer des boîtes aux lettres de dossiers publics vers d'autres bases de données de boîtes aux lettres en utilisant le jeu de cmdlets **MoveRequest**. C'est également le jeu de cmdlets utilisé pour déplacer des boîtes aux lettres ordinaires. Pour plus d'informations, consultez la rubrique [Déplacement d'une boîte aux lettres de dossiers publics vers une autre base de données de boîtes aux lettres](move-a-public-folder-mailbox-to-a-different-mailbox-database-exchange-2013-help.md).

Les cmdlets **PublicFolderMoveRequest** et **MoveRequest** utilisent le service de réplication de boîte aux lettres pour déplacer les dossiers publics de manière asynchrone. Cela signifie que la cmdlet n'effectue pas le travail réel et que, pendant presque toute l'opération de déplacement, le dossier public et les boîtes aux lettres de dossiers publics restent disponibles pour les utilisateurs. Comme le service de réplication de boîte aux lettres exécute les déplacements de boîtes aux lettres, les demandes d'importation et d'exportation et les demandes de déplacements de dossiers publics, il est important d'envisager une gestion de la limitation de bande passante et de la charge de travail.

## Quotas de dossiers publics

Lors de leur création, les boîtes aux lettres de dossiers publics héritent automatiquement des limites de taille par défaut de la base de données de boîtes aux lettres. Par conséquent, pour évaluer précisément l'état du quota de stockage en cours lors de l'utilisation de la cmdlet [Get-Mailbox](https://technet.microsoft.com/fr-fr/library/bb123685\(v=exchg.150\)), vous devez examiner la propriété *UseDatabaseQuotaDefaults* en plus des propriétés *ProhibitSendQuota*, *ProhibitSendReceiveQuota* et *IssueWarningQuota*. Si la propriété *UseDatabaseQuotaDefaults* est définie sur `true`, les paramètres individuels des boîtes aux lettres sont ignorés et les limites de la base de données de boîtes aux lettres appliquées. Si cette propriété est définie sur `true` et si les propriétés *ProhibitSendQuota*, *ProhibitSendReceiveQuota* et *IssueWarningQuota* sont définies sur `unlimited`, la taille de boîte aux lettres n'est pas réellement illimitée. Au lieu de cela, vous devez utiliser la cmdlet **Get-MailboxDatabase** et consulter les limites de stockage de la base de données de boîtes aux lettres pour déterminer les limites de la boîte aux lettres. Si la propriété *UseDatabaseQuotaDefaults* est définie sur `false`, les paramètres individuels des boîtes aux lettres sont utilisés. Dans Exchange 2013, les limites par défaut de quota de base de données de boîtes aux lettres sont les suivantes :

  - *Quota d'avertissement* : 1,9 Go

  - *Quota d'interdiction d'envoi* : 2 Go

  - *Quota d'interdiction de réception* : 2,3 Go

Pour déterminer les quotas de base de données de boîtes aux lettres, exécutez la cmdlet [Get-MailboxDatabase](https://technet.microsoft.com/fr-fr/library/bb124924\(v=exchg.150\)).

Pour déterminer les quotas d'une boîte aux lettres de dossiers publics, utilisez la cmdlet [Set-OrganizationConfig](https://technet.microsoft.com/fr-fr/library/aa997443\(v=exchg.150\)).

## Récupération d'urgence

Les dossiers publics Exchange 2013 sont basés sur une infrastructure de boîtes aux lettres et utilisent les mêmes mécanismes en matière de disponibilité et de redondance. Chaque boîte aux lettres de dossiers publics peut avoir plusieurs copies redondantes avec basculement automatique, tout comme des boîtes aux lettres ordinaires. Pour plus d'informations, consultez la rubrique [Haute disponibilité et résilience de site](high-availability-and-site-resilience-exchange-2013-help.md).

Outre le scénario global de récupération d'urgence, vous pouvez restaurer des dossiers publics dans les situations suivantes :

  - **Restauration de dossier public récupérable**   Le dossier public a été supprimé, mais sa période de rétention n'a pas expiré.

  - **Restauration de boîte aux lettres de dossiers publics récupérable**   La boîte aux lettres de dossiers publics a été supprimée, mais sa période de rétention n'a pas expiré.

  - **Restauration de boîte aux lettres de dossiers publics à partir d'une base de données de récupération**   Vous pouvez récupérer une boîte aux lettres de dossiers publics après expiration de sa période de rétention à partir d'une sauvegarde. Vous pouvez ensuite extraire les données de la boîte aux lettres restaurée et les copier dans un dossier cible ou les fusionner avec les données d'une autre boîte aux lettres.

Dans toutes ces situations, le dossier public ou la boîte aux lettres de dossiers publics sont récupérables à l'aide des cmdlets **MailboxRestoreRequest**.

Pour plus d'informations, consultez la rubrique [Restauration de dossiers publics et de boîtes aux lettres de dossiers publics à partir de déplacements ayant échoué](restore-public-folders-and-public-folder-mailboxes-from-failed-moves-exchange-2013-help.md).

