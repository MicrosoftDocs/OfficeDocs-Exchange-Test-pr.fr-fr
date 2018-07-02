---
title: 'Migration de vos dossiers publics vers Groupes Office 365: Exchange 2013 Help'
TOCTitle: Migration de vos dossiers publics vers Groupes Office 365
ms:assetid: d89e727b-675a-4623-b572-260f8b44b966
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Mt843872(v=EXCHG.150)
ms:contentKeyID: 74468715
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Migration de vos dossiers publics vers Groupes Office 365

 

_**Sapplique à :** Exchange Online, Exchange Server 2010, Exchange Server 2013_

_**Dernière rubrique modifiée :** 2017-09-25_

**Résumé** : Pourquoi devez-vous ou ne devez-vous pas migrer vos dossiers publics Exchange vers Groupes Office 365.

Cet article compare les dossiers publics et Groupes Office 365, et explique quelle est la meilleure solution pour votre organisation. Les dossiers publics existent depuis aussi longtemps qu’Exchange, tandis que la fonction Groupes a été introduite plus récemment. Si vous souhaitez migrer une partie ou la totalité de vos dossiers publics vers Groupes, cet article décrit le fonctionnement du processus et fournit des liens vers des articles qui vous guident tout au long du processus, étape par étape.

## Que sont les dossiers publics ?

Les [Dossiers publics](public-folders-exchange-2013-help.md) contiennent les différents types de données et sont organisés en une structure hiérarchique.

Les dossiers publics ne sont pas recommandés dans les situations suivantes :

  - **Archivage des données**. Les utilisateurs qui ont des limites de boîtes aux lettres emploient parfois des dossiers publics au lieu de boîtes aux lettres pour archiver des données. Cette pratique est déconseillée, car elle affecte le stockage dans les dossiers publics et va à l’encontre de l’objectif des limites de boîtes aux lettres.

  - **Partage de documents et collaboration**. Les dossiers publics n’intègrent pas de fonction de gestion des documents, comme la fonctionnalité de contrôle de version, d’archivage et d’extraction, et les notifications automatiques de modification du contenu.

## Qu’est-ce que Groupes Office 365 ?

Les groupes dans Office 365 vous permettent de choisir un ensemble de personnes avec lesquelles vous souhaitez collaborer et de configurer facilement une collection de ressources à partager avec ces personnes. Vous n’avez pas à vous soucier d’attribuer manuellement des autorisations à toutes ces ressources, car les membres du groupe reçoivent automatiquement les autorisations nécessaires pour les outils et les ressources fournis par le groupe lorsqu’ils sont ajoutés. Les groupes constituent une expérience nouvelle et améliorée pour les tâches que permettaient d’effectuer les listes de distribution et boîtes aux lettres partagées auparavant.

Pour tout savoir sur les groupes, consultez l’article [En savoir plus sur les groupes Office 365](https://go.microsoft.com/fwlink/p/?linkid=858521).

## Devez-vous migrer vos dossiers publics vers Groupes Office 365 ?

Groupes Office 365 est l’offre de collaboration de Microsoft la plus récente, ce qui signifie qu’il existe de nombreuses raisons pour lesquelles ce service serait une solution préférable aux dossiers publics, une technologie beaucoup plus ancienne. Dans Outlook, par exemple, la fonction Groupes permet de remplacer l’intégralité des dossiers publics à extension messagerie. Il est impossible de faire la liste de tous les scénarios dans lesquels Groupes Office 365 fonctionne mieux que les dossiers publics, mais voici les points forts :

  - **Collaboration avec la messagerie électronique**. La fonction Groupes dans Outlook a dédié un espace **Conversations** qui stocke tous les e-mails et permet aux utilisateurs de collaborer dessus. Le groupe peut même être configuré de façon à recevoir les messages provenant de personnes en dehors du groupe ou à l’extérieur de l’organisation. Si vous utilisez actuellement des dossiers publics à extension messagerie pour stocker, par exemple, les discussions liées au projet, ou les bons de commande qui doivent être consultés par une équipe de personnes, l’utilisation de la fonction Groupes représente une amélioration. La fonction Groupes est également préférable dans les situations où vous voulez tout simplement diffuser des informations à un ensemble d’utilisateurs.

  - **Collaboration sur des documents**. Dans Outlook, la fonction Groupes possède un onglet **Fichiers** dédié qui affiche tous les fichiers à partir du site d’équipe SharePoint du groupe, et à partir des pièces jointes d’e-mail. Vous obtenez un aperçu de tous les fichiers, vous n’avez donc plus besoin de les rechercher comme vous le feriez dans les dossiers publics. La co-création devient également plus facile. Si vous utilisez des dossiers publics pour stocker les fichiers destinés à être utilisés par plusieurs personnes, envisagez de migrer vers la fonction Groupes.

  - **Calendrier partagé**. Lors de la création, chaque groupe obtient un calendrier partagé. Tous les membres du groupe peuvent créer des événements sur ce calendrier. Quand vous avez un groupe favori, le calendrier du groupe en question peut être affiché en regard de votre calendrier personnel. Vous pouvez également vous abonner aux événements d’un groupe, auquel cas les événements créés dans ce groupe apparaissent dans votre calendrier personnel. Si vous utilisez des dossiers publics pour héberger les calendriers de votre équipe, par exemple un calendrier ou un agenda, la fonction Groupes est une meilleure expérience.

  - **Autorisations simplifiées**. Lorsque vous affectez des utilisateurs à un groupe, ils obtiennent immédiatement les autorisations dont ils ont besoin, tandis qu’avec les dossiers publics, vous devez accorder manuellement les autorisations appropriées. Les membres peuvent être ajoutés en tant que « propriétaires » ou « membres ». Les propriétaires disposent de tous les droits dans le groupe, y compris la possibilité d’effectuer des tâches de gestion de groupe. Les membres peuvent également créer du contenu et modifier des fichiers comme les propriétaires, mais les membres ne peuvent pas supprimer le contenu qu’ils n’ont pas créé. Si le modèle d’autorisations des dossiers publics est trop laborieux pour vous et que vous voulez quelque chose simple et rapide, Groupes Office 365 est la solution.

  - **Présence mobile et web**. Les dossiers publics ne sont pas accessibles via des appareils mobiles et disposent d’un ensemble limité de fonctionnalité sur le web. Groupes Office 365, en revanche, est accessible via les applications mobiles Outlook et possède un ensemble de fonctionnalités plus complètes sur le web. Si votre équipe est en déplacement et requiert un accès mobile, vous devriez utiliser Groupes Office 365.

  - **Accès à une large gamme d’applications Office 365**. Lorsque vous créez un groupe, vous déverrouillez l’accès à une large gamme d’applications sur la suite Office 365. Vous obtenez un site d’équipe SharePoint pour le stockage de fichiers et un plan sur le planificateur pour effectuer le suivi de vos tâches. Groupes Office 365 est le service aux membres qui combine les éléments de l’ensemble de la suite Office 365.

Tandis que Groupes Office 365 offre de nombreux avantages, vous devez tenir compte des quelques différences majeures que vous remarquerez après avoir arrêté d’utiliser les dossiers publics. Il s’agit essentiellement des éléments suivants :

  - **Hiérarchie de dossiers**. Si les dossiers publics sont souvent utilisés pour organiser le contenu en une hiérarchie très étendue, Groupes Office 365 possède une structure plate. Tous les e-mails du groupe figurent dans l’espace de conversations et tous les documents vont dans l’onglet **Fichiers**. En outre, vous ne pouvez pas créer de sous-dossiers dans des groupes Office 365.

  - **Rôles d’autorisation granulaire**. Tandis que les dossiers publics ont une variété de rôles d’autorisation, Groupes Office 365 ne fournit que deux rôles : propriétaire et membre.

Avant de passer à la fonction Groupes, il est également judicieux de noter les différentes limites fournies avec la création et la gestion des groupes. Consultez la rubrique *Comment gérer mes groupes ?* dans [En savoir plus sur Groupes Office 365](https://go.microsoft.com/fwlink/p/?linkid=858521) pour obtenir plus d’informations.

## Migration des dossiers publics vers Groupes Office 365

Si vous décidez de passer à Groupes Office 365, vous pouvez utiliser un processus appelé *migration par lots* pour déplacer votre messagerie et le contenu de votre calendrier de vos dossiers publics existants vers les groupes. Les étapes spécifiques de l’exécution d’une migration par lots dépendent de la version d’Exchange hébergeant actuellement votre hiérarchie de dossiers publics. À la fin de cet article, vous trouverez des liens vers des instructions pour vous guider tout au long du processus de migration par lots.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Lorsque vous avez terminé la migration d’un dossier public à extension messagerie vers un groupe particulier dans Office 365, tous les e-mails adressés au dossier public sont reçus à ce stade par le groupe.</td>
</tr>
</tbody>
</table>


Voici les principaux avantages des migrations par lots :

  - **Migration basée sur le service de réplication de boîte aux lettres**. Le processus de migration utilise les cmdlets des lots de migration. La migration à plusieurs groupes peut être déclenchée conjointement dans un lot de migration unique. Il existe également des scripts disponibles pour aider dans le processus de migration.

  - **Prend en charge les dossiers publics de courrier et de calendrier**. Les e-mails et les billets copiés s’affichent dans les groupes en tant que conversations de groupe, et les éléments de calendrier copiés sont visibles dans les calendriers de groupe. Les autres types de dossiers publics, tels que les tâches et les contacts, ne sont pas pris en charge actuellement pour cette migration.

  - **Les dossiers publics locaux peuvent être migrés directement vers Groupes Office 365**. Cette migration n’exige pas que vous déplaciez d’abord vos dossiers publics vers Office 365, puis passiez aux groupes. Les cmdlets de copie de données MRS lisent les données des dossiers publics directement à partir de votre environnement local, puis copient les données dans Groupes Office 365. Notez que les dossiers publics Exchange 2010 requièrent un point de terminaison Outlook Anywhere. Les dossiers publics Exchange 2013 et Exchange 2016 requièrent un point de terminaison basé sur le proxy MRS.

  - **Pas une migration « tout ou rien »**. Vous pouvez choisir les dossiers publics spécifiques à migrer vers les groupes ; seuls les dossiers publics choisis sont migrés.

  - **Copie des données en une étape**. Les migrations par lots sont conçues pour être une simple copie de données ponctuelle des dossiers publics sources aux groupes cibles, sans la complexité de la synchronisation incrémentielle et la finalisation.

  - **Fusionne les données des dossiers publics avec les données existantes dans un groupe**. La copie des données fusionne le contenu des dossiers publics avec le contenu du groupe existant, le cas échéant. S’il est nécessaire de copier des données incrémentielles, vous pouvez simplement exécuter la copie des données autant de fois que nécessaire. Cette opération copie les données incrémentielles dans le groupe.

## Aperçu des migrations par lots

Les étapes suivantes décrivent l’ensemble du processus de migration du contenu de vos dossiers publics vers Groupes Office 365 dans une migration par lots. Les détails spécifiques sont contenus dans les articles répertoriés ci-dessous.

1.  **Sélectionner la source** : Choisissez les dossiers publics à migrer. Vous pouvez choisir n’importe quel dossier contenant du contenu de courrier ou de calendrier.

2.  **Créer la cible** : Créez des groupes correspondants pour vos dossiers, avec les configurations de votre choix, telles que les membres, les paramètres de confidentialité et la classification des données.

3.  **Copier des données** : Utilisez les cmdlets des lots de migration pour copier des données provenant de dossiers publics vers des groupes.

4.  **Verrouiller la source** : Verrouillez les dossiers publics après avoir vérifié les données dans les groupes.

5.  **Basculement** : Copiez toutes les nouvelles données créées entre les étapes 3 et 4.

Notez que vos dossiers publics et leurs groupes correspondants restent en ligne pour vos utilisateurs au cours des étapes 1 à 3 susmentionnées. Après l’étape 3, vous pouvez décider de poursuivre ou non la migration en fonction de l’expérience des groupes et si elle répond aux besoins de vos utilisateurs et de votre organisation. À ce stade, vous pouvez restaurer votre migration et reprendre à l’aide de dossiers publics. Si vous poursuivez la migration, une fois l’étape 5 terminée, vous pouvez supprimer les dossiers publics d’origine. Même après la migration, il est possible de revenir aux dossiers publics, à condition d’avoir enregistré les fichiers de sauvegarde à partir du processus de migration et de ne pas avoir supprimé les dossiers publics d’origine.

## Conditions requises à la migration par lots et instructions étape par étape

Les conditions suivantes doivent être préalablement remplies dans votre environnement Exchange pour que vous puissiez exécuter une migration par lots. Les conditions requises spécifiques dépendent de la version d’Exchange en cours d’exécution.

1.  Si vos dossiers publics sont en local, vos serveurs doivent exécuter l’une des versions suivantes :
    
      - Exchange 2010 SP3 RU8 ou version ultérieure
    
      - Exchange 2013 CU15 ou version ultérieure
    
      - Exchange 2016 CU4 ou version ultérieure

2.  Si vos dossiers publics sont en local, vous devez disposer d’un environnement hybride Exchange configuré. Pour obtenir plus d’informations, consultez la rubrique [Déploiements hybrides Exchange Server](https://technet.microsoft.com/fr-fr/library/jj200581\(v=exchg.150\)).

**Instructions de migration**

Sélectionnez le lien approprié ci-dessous pour obtenir des instructions étape par étape sur l’exécution d’une migration par lots.

  - [Use batch migration to migrate Exchange Online public folders to Office 365 Groups](https://technet.microsoft.com/fr-fr/library/mt843871\(v=exchg.150\))

  - [Utilisation de la migration par lots pour migrer des dossiers publics Exchange 2010 vers Groupes Office 365](use-batch-migration-to-migrate-exchange-2010-public-folders-to-office-365-groups-exchange-2013-help.md)

  - [Utilisation de la migration par lots pour migrer des dossiers publics Exchange 2013 vers Groupes Office 365](use-batch-migration-to-migrate-exchange-2013-public-folders-to-office-365-groups-exchange-2013-help.md)

  - [Utilisation de la migration par lots pour migrer des dossiers publics Exchange 2016 vers Groupes Office 365](https://go.microsoft.com/fwlink/p/?linkid=859171)

