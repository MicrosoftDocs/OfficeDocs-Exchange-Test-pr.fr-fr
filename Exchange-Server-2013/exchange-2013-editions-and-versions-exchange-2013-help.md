---
title: 'Exchange 2013 : éditions et versions: Exchange 2013 Help'
TOCTitle: 'Exchange 2013 : éditions et versions'
ms:assetid: b563b543-fb3f-4465-9a54-cbfd680aee1f
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb232170(v=EXCHG.150)
ms:contentKeyID: 50555481
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange 2013 : éditions et versions

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2016-12-09_

Microsoft Exchange Server 2013 est disponible dans deux éditions serveur : Standard Edition et Enterprise Edition. Enterprise Edition peut évoluer et atteindre jusqu’à 50 bases de données montées par serveur dans les versions finalisées (RTM) et de mise à jour cumulative 1 (CU1), et jusqu’à 100 bases de données montées par serveur dans la mise à jour cumulative 2 (CU2) et versions ultérieures ; Standard Edition est limitée à 5 bases de données montées par serveur. Une base de données montée est une base de données en cours d’utilisation. Il peut s’agir d’une base de données de boîtes aux lettres active qui est montée afin d’être utilisée par les clients, ou une base de données de boîtes aux lettres passive montée dans la récupération pour la réplication et la relecture de journal. Vous pouvez créer plus de bases de données que les limites décrites ci-dessus, mais vous ne pouvez monter que le nombre maximal indiqué plus haut. La base de données de récupération n’entre pas dans cette limite.

Ces éditions sous licence sont définies par une clé de produit. Lorsque vous entrez une clé de produit sous licence valide, l'édition prise en charge pour le serveur est établie. Les clés de produit ne peuvent être utilisées que pour des échanges et des mises à niveau de clé d’une même édition, mais pas pour un changement de niveau d’édition. Vous pouvez utiliser une clé de produit valide pour passer de la version d’évaluation d’Exchange 2013 à Standard Edition ou Enterprise Edition. Vous pouvez également utiliser une clé de produit valide pour passer de Standard Edition à Enterprise Edition.

Vous pouvez également renouveler la licence du serveur avec la clé de produit de la même édition. Par exemple, si vous aviez deux serveurs Standard Edition avec deux clés, mais avez utilisé de manière accidentelle la même clé sur les deux serveurs, vous pouvez la remplacer par l’autre clé qui vous a été fournie. Vous pouvez procéder ainsi sans réinstaller ou reconfigurer quoi que ce soit. Une fois que vous avez entré la clé de produit et redémarré le service de banque d’informations Microsoft Exchange, l’édition correspondant à cette clé de produit est activée.

Aucune perte de fonctionnalité ne se produira lors de l’expiration de la version d’évaluation. Vous pouvez donc conserver les environnements lab, de formation, de démonstration et autres environnements de test au-delà de 120 jours sans devoir réinstaller la version d’évaluation d’Exchange 2013.

Comme indiqué précédemment, vous ne pouvez pas utiliser de clés de produit pour passer d’Enterprise Edition à Standard Edition, ni pour revenir à la version d’évaluation. Ces types de mise à niveau vers une version antérieure ne sont possibles qu’en désinstallant Exchange 2013, en réinstallant Exchange 2013, puis en entrant la clé de produit appropriée.

## Versions d’Exchange 2013

Pour obtenir une liste des versions Exchange 2013 et des informations sur le téléchargement et l’installation de la dernière version de Exchange 2013, consultez les rubriques suivantes :

  - [Mises à jour d’Exchange Server : numéros de version et dates de sortie](https://technet.microsoft.com/fr-fr/library/hh135098\(v=exchg.150\))

  - [Mettre à niveau Exchange 2013 vers la mise à jour cumulative la plus récente ou vers le Service Pack le plus récent](upgrade-exchange-2013-to-the-latest-cumulative-update-or-service-pack-exchange-2013-help.md)

Pour afficher le numéro de version de la version de Microsoft Exchange 2013 que vous exécutez, exécutez la commande ci-après dans l’environnement de ligne de commande Exchange Management Shell.

    Get-ExchangeServer | fl name,edition,admindisplayversion

## Types de licence Exchange 2013

La licence Exchange 2013 dépend du modèle de licence d’accès client/serveur à l’instar de la licence Exchange 2010. Les types de licence sont les suivants :

  - **Licence serveur**   Une licence doit être associée à chaque instance du logiciel serveur exécuté. La licence serveur est disponible en deux éditions : Standard Edition et Enterprise Edition.

  - **Licences d’accès client (CAL)**   Exchange 2013 est également disponible en deux éditions de licence d’accès client, Standard CAL et Enterprise CAL. Vous pouvez combiner et faire correspondre comme vous le souhaitez les éditions serveur avec les deux types de licence d’accès client (CAL). Par exemple, vous pouvez utiliser une licence d’accès client Enterprise avec Exchange 2013 Standard Edition. De même, vous pouvez utiliser une licence d’accès client Standard avec Exchange 2013 Enterprise Edition.

Pour plus d’informations sur les types de licences Exchange, voir [Licences](https://go.microsoft.com/fwlink/p/?linkid=392675).

