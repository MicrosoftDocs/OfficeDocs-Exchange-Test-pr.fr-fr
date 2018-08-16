---
title: 'Portabilité des bases de données: Exchange 2013 Help'
TOCTitle: Portabilité des bases de données
ms:assetid: 387b727a-ce51-4910-b5c4-613c693fa5bd
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dd876873(v=EXCHG.150)
ms:contentKeyID: 51407177
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Portabilité des bases de données

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2017-01-30_

La fonctionnalité de portabilité des bases de données permet de déplacer une base de données de boîte aux lettres Microsoft Exchange Server 2013 ou de la monter sur un autre serveur de boîte aux lettres de la même organisation exécutant Exchange 2013 qui possède des bases de données de la même version de schéma de base de données. Les bases de données de boîtes aux lettres des versions antérieures d'Exchange ne peuvent pas être déplacées vers un serveur de boîtes aux lettres exécutant Exchange 2013. Grâce à cette fonctionnalité, la suppression des étapes manuelles qui étaient sources d'erreurs fréquentes dans le processus de récupération optimise la fiabilité. En outre, la portabilité des bases de données réduit la durée globale de récupération des différents scénarios d'échec.

Lors de l’utilisation de la portabilité des bases de données pour récupérer une base de données de boîtes aux lettres, la version du système d’exploitation et celle d’Exchange Server doivent être identiques sur les serveurs Exchange source et cible. Par exemple, si une base de données de boîtes aux lettres Exchange 2013 a été précédemment montée sur un serveur exécutant Windows Server 2012, la portabilité des bases de données fonctionnera uniquement si vous migrez la base de données vers un serveur exécutant également Windows Server 2012 et Exchange 2013.

Pour plus d'informations sur la récupération d'une base de données à l'aide de la fonctionnalité de portabilité des bases de données, consultez la rubrique [Déplacer une base de données de boîtes aux lettres à l’aide de la portabilité de base de données](move-a-mailbox-database-using-database-portability-exchange-2013-help.md).

