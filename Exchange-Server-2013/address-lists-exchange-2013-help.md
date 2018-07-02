---
title: 'Listes d’adresses: Exchange 2013 Help'
TOCTitle: Listes d’adresses
ms:assetid: 8ee2672a-3a45-4897-8cc0-fa23c374dbf9
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb232119(v=EXCHG.150)
ms:contentKeyID: 50478698
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Listes d’adresses

 

_**Sapplique à :** Exchange Online, Exchange Server 2013_

_**Dernière rubrique modifiée :** 2014-12-02_

Une *liste d'adresses* est un ensemble d'objets destinataire et d'autres objets Active Directory. Chaque liste d'adresses peut contenir un ou plusieurs types d'objets (par exemple, des utilisateurs, des contacts, des groupes, des dossiers publics et des ressources en termes de salles et d'équipements). Les listes d'adresses permettent d'organiser les destinataires et les ressources, ce qui facilite la recherche de destinataires et de ressources. Les listes d'adresses sont mises à jour de façon dynamique. Par conséquent, lorsque de nouveaux destinataires sont ajoutés à votre organisation, ils sont automatiquement ajoutés aux listes d'adresses appropriées.

Comme illustré dans la figure suivante, les applications clientes, comme Microsoft Outlook, affichent les listes d'adresses disponibles fournies par Exchange.

**Liste d'adresses globale telle qu'elle s'affiche dans Microsoft Office Outlook 2007**

![Listes d’adresses affichées dans Outlook 2007](images/Bb232119.54d7729c-2e28-4863-8944-b0c37dabbbb3(EXCHG.150).gif "Listes d’adresses affichées dans Outlook 2007")

Les listes d'adresses résident dans Active Directory. Aussi, les utilisateurs mobiles déconnectés du réseau le sont également de ces listes d'adresses côté serveur. Vous pouvez toutefois créer des carnets d'adresses en mode hors connexion pour les utilisateurs déconnectés du réseau. Ces carnets d'adresses en mode hors connexion peuvent être téléchargés sur le disque dur d'un utilisateur. Souvent, pour économiser les ressources, les carnets d'adresses en mode hors connexion constituent des sous-ensembles d'informations extraits des listes d'adresses résidant sur vos serveurs. Pour plus d'informations, consultez la rubrique [Carnets d’adresses en mode hors connexion](offline-address-books-exchange-2013-help.md).

**Contenu de cette rubrique**

Listes d'adresses par défaut

Listes d'adresses personnalisées

Meilleures pratiques pour la création de listes d'adresses

## Listes d'adresses par défaut

Lorsque des utilisateurs veulent se servir de leur application cliente pour rechercher des informations sur les destinataires, ils peuvent le faire à partir des listes d'adresses disponibles. Plusieurs listes d'adresses, comme la liste d'adresses globale (LAG), sont créées par défaut. Exchange contient les listes d'adresses par défaut suivantes (celles-ci sont renseignées automatiquement avec les nouveaux utilisateurs, contacts ou salles à mesure qu'ils sont ajoutés à votre organisation) :

  - **Tous les contacts**   Cette liste d'adresses contient tous les contacts à extension messagerie de votre organisation. Les contacts à extension messagerie sont les destinataires dotés d'une adresse de messagerie externe. Si vous voulez que les informations d'un contact à extension messagerie soient disponibles pour tous les utilisateurs de votre organisation, vous devez inclure le contact dans la LAG. Pour en savoir plus sur les contacts de messagerie, consultez la rubrique [Recipients](recipients-exchange-2013-help.md).

  - **Toutes les listes de distribution**   Cette liste d’adresses contient les groupes à extension messagerie, tels que les groupes de sécurité à extension messagerie, les groupes de distribution et les groupes de distribution dynamiques de votre organisation. Les groupes à extension messagerie sont des listes de destinataires créés pour l'expédition de messages électroniques et d’autres informations en masse. Quand un message électronique est envoyé à un groupe à extension messagerie, tous les membres du groupe reçoivent une copie du message. Pour plus d'informations sur les groupes à extension messagerie, consultez la rubrique [Recipients](recipients-exchange-2013-help.md).

  - **Toutes les salles**   Cette liste d'adresses contient toutes les ressources désignées en tant que salles dans votre organisation. Les salles sont des ressources de votre organisation qui peuvent être programmées en envoyant une demande de réunion à partir d'une application cliente. Le compte d'utilisateur associé à une salle est désactivé. Pour plus d'informations sur les boîtes aux lettres de ressource, consultez la rubrique [Recipients](recipients-exchange-2013-help.md).

  - **Tous les utilisateurs**   Cette liste d'adresses contient tous les utilisateurs à extension messagerie de votre organisation. Un utilisateur à extension messagerie correspond à un utilisateur externe à votre organisation Exchange. Chaque utilisateur à extension messagerie dispose d'une adresse de messagerie externe. Tous les messages envoyés aux utilisateurs à extension messagerie sont acheminés à cette adresse de messagerie externe. Un utilisateur à extension messagerie est similaire à un contact de messagerie, à la différence qu'un utilisateur à extension messagerie dispose d'informations d'identification d'ouverture de session Active Directory et peut accéder à des ressources. Pour plus d'informations sur les utilisateurs à extension messagerie, consultez la rubrique [Recipients](recipients-exchange-2013-help.md).

  - **Liste d'adresses globale par défaut**   Cette liste d'adresses contient tous les utilisateurs, contacts, groupes ou salles à extension messagerie de l'organisation. Lors de l'installation, Exchange crée plusieurs listes d'adresses par défaut. La liste d'adresses la plus connue est la LAG. Par défaut, la LAG contient tous les destinataires d'une organisation Exchange. Autrement dit, tout objet à extension messagerie ou boîte aux lettres dans une forêt Active Directory dans laquelle Exchange est installé est répertorié dans la LAG. Pour une utilisation plus aisée, la LAG est organisée par nom, et non par adresse de messagerie. Pour plus d'informations, consultez la rubrique [Création d’une liste d’adresses globale](create-a-global-address-list-exchange-2013-help.md).

  - **Dossiers publics**   Cette liste d'adresses contient tous les dossiers publics de votre organisation. Des autorisations d'accès définissent les personnes autorisées à consulter et utiliser les dossiers. Les dossiers publics sont conservés sur des ordinateurs exécutant Exchange. Pour plus d'informations sur les dossiers publics dans Exchange 2013, consultez la rubrique [Dossiers publics](public-folders-exchange-2013-help.md). Pour plus d'informations sur les dossiers publics dans Exchange Online, consultez la rubrique [Dossiers publics dans Office 365 et Exchange Online](https://technet.microsoft.com/fr-fr/library/jj200758\(v=exchg.150\)).

## Listes d'adresses personnalisées

Une organisation Exchange peut contenir des milliers de destinataires. Si vous compilez tous vos destinataires dans les listes d'adresses par défaut, ces listes peuvent devenir très volumineuses. Pour éviter cette situation, vous pouvez créer des listes d'adresses personnalisées pour aider les utilisateurs de votre organisation à trouver plus facilement les informations qu'ils recherchent.

Prenons l'exemple d'une entreprise comportant deux grandes divisions et une organisation Exchange. La division Fourth Coffee importe et vend des grains de café. La division Contoso, Ltd propose des polices d'assurance. Pour la plupart des activités quotidiennes, les employés de Fourth Coffee ne communiquent pas avec les employés de Contoso, Ltd. Par conséquent, pour que les employés recherchent plus facilement les destinataires existant uniquement dans leur division, vous pouvez créer deux listes d'adresses personnalisées : une pour Fourth Coffee et l'autre pour Contoso, Ltd. Lors de la recherche de destinataires dans leur division, ces listes d'adresses personnalisées permettent aux employés de ne sélectionner que la liste d'adresses spécifique à leur division. Si un employé n'est pas sûr de la division à laquelle appartient le destinataire, il peut effectuer sa recherche dans la LAG qui contient les destinataires des deux divisions.

Vous pouvez également créer des sous-catégories de listes d'adresses nommées listes d'adresses hiérarchiques. Par exemple, vous pouvez créer une liste d'adresses contenant les destinataires basés à Manchester et une autre contenant les destinataires basés à Stuttgart.

## Meilleures pratiques pour la création de listes d'adresses

Si les listes d'adresses sont des outils utiles pour les utilisateurs, les listes d'adresses mal conçues peuvent être sources de frustration. Pour être sûr que vos listes d'adresses sont pratiques pour les utilisateurs, prenez en compte les meilleures pratiques suivantes :

  - Évitez de créer trop de listes d'adresses car les utilisateurs ne sauront pas dans quelle liste rechercher des destinataires.

  - Les listes d'adresses doivent faciliter la recherche des adresses par les utilisateurs dans la LAG.

  - Nommez vos listes d'adresses de telle sorte que l'utilisateur identifie immédiatement le type de destinataires qu'elles contiennent. Si vous rencontrez des difficultés pour attribuer des noms à vos listes d'adresses, créez moins de listes et rappelez à vos utilisateurs qu'ils peuvent trouver n'importe quel destinataire dans votre organisation via la LAG.
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Par défaut dans Exchange Online, le rôle de liste d’adresses n’est affecté à aucun groupe de rôles. Pour utiliser les cmdlets nécessitant le rôle Liste d’adresses, vous devez ajouter ce dernier à un groupe de rôles. Pour plus d’informations, consultez la section « Ajouter un rôle à un groupe de rôles » de la rubrique <a href="manage-role-groups-exchange-2013-help.md">Gérer des groupes de rôles</a>.</td>
    </tr>
    </tbody>
    </table>


Pour plus d'informations sur la création d'une liste d'adresses dans Exchange 2013, consultez la rubrique [Créer une liste d'adresses](create-an-address-list-exchange-2013-help.md). Pour plus d'informations sur la création d'une liste d'adresses dans Exchange Online, consultez la rubrique [Gestion des listes d’adresses dans Exchange Online](https://technet.microsoft.com/fr-fr/library/jj983798\(v=exchg.150\)).

