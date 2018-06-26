---
title: 'Active Directory: Exchange 2013 Help'
TOCTitle: Active Directory
ms:assetid: 8e8464df-2d1d-4d68-82de-b0c158c549c3
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb123715(v=EXCHG.150)
ms:contentKeyID: 50478672
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Active Directory

 

_**Sapplique à :**Exchange Server 2013_

_**Dernière rubrique modifiée :**2016-12-09_

Microsoft Exchange Server 2013 utilise Active Directory pour enregistrer et partager des informations d’annuaire avec Windows. La conception de forêts Active Directory pour Exchange 2013 est similaire à Exchange Server 2010, à l’exception de quelques dispositifs décrits ci-après.

## Pilote du service d’annuaire Active Directory

Le pilote du service d’annuaire Active Directory est le composant de base de Microsoft Exchange qui permet aux services Exchange de créer, de modifier, de supprimer et d’interroger des données des services de domaine Active Directory. Dans Exchange 2013, tous les accès à Active Directory sont effectués à l’aide du pilote Active Directory proprement dit. Précédemment, dans Exchange 2010, DSAccess fournissait des services de recherche d’annuaire pour des composants, comme SMTP, l’agent de transfert des messages (MTA) et le magasin Exchange.

Le pilote Active Directory exploite également la topologie Exchange Microsoft Active Directory (MSExchangeADTopology), qui permet au pilote Active Directory d’utiliser les données de topologie d’accès au service d’annuaire (DSAccess). Ces données incluent la liste des contrôleurs de domaines et des serveurs de catalogue global disponibles pour traiter les requêtes Exchange. Pour plus d’informations sur le pilote Active Directory, consultez la page des [services de domaine Active Directory](https://go.microsoft.com/fwlink/p/?linkid=110942).

## modifications du schéma Active Directory

Exchange 2013 ajoute de nouveaux attributs au schéma du service de domaine Active Directory et effectue également d’autres modifications pour des classes et des attributs existants. Pour plus d’informations sur les modifications de Active Directory lors de l’installation de Exchange 2013, consultez [Modifications apportées au schéma Active Directory d’Exchange 2013](exchange-2013-active-directory-schema-changes-exchange-2013-help.md).

## Pour plus d'informations

Pour en savoir plus sur la manière dont Exchange 2013 stocke et récupère des informations dans Active Directory afin de pouvoir en planifier un accès, consultez [Accès à Active Directory](access-to-active-directory-exchange-2013-help.md).

Pour plus d’informations sur la conception de forêts Active Directory, voir le guide de conception [AD DS Design Guide](https://go.microsoft.com/fwlink/p/?linkid=264957).

Pour plus d’informations sur les ordinateurs fonctionnant sous Windows dans un domaine Active Directory et sur le déploiement d'Exchange 2013 dans un domaine ayant un espace de noms disjoint, consultez [Scénarios d’espace de noms disjoint](disjoint-namespace-scenarios-exchange-2013-help.md).

