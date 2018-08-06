---
title: 'Màn srv Exchange 2007 nécessaire vers Service Pack 3, correctif cumulatif 10 | Microsoft Docs'
TOCTitle: Les serveurs Exchange 2007 doivent être mis à niveau vers le Service Pack 3, correctif cumulatif 10
ms:assetid: b8028a00-c451-412e-86f2-1669f6eee8fc
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/ms.exch.setupreadiness.e15e12coexistenceminversionrequirement(v=EXCHG.150)
ms:contentKeyID: 50479055
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Les serveurs Exchange 2007 doivent être mis à niveau vers le Service Pack 3, correctif cumulatif 10

 

_**Sapplique à :** Exchange Server_

_**Dernière rubrique modifiée :** 2016-12-09_

Le programme d'installation de Microsoft Exchange Server 2013 ne peut pas continuer, car il a détecté un ou plusieurs serveurs Exchange Server 2007 qui n'ont pas été mis à niveau vers correctif cumulatif Exchange Server 2007 Service Pack 3 (SP3) Roll Up 10 (RU10). Avant de pouvoir installer Exchange 2013, tous les serveurs Exchange 2007 de votre organisation doivent être mis à niveau vers Exchange 2007 SP3 RU10. Cette exigence inclut les serveurs de transport Edge Exchange 2007. Pour plus d'informations, consultez la rubrique [Mise à niveau d'Exchange 2007 vers Exchange 2013](upgrade-from-exchange-2007-to-exchange-2013-exchange-2013-help.md).

> [!NOTE]
> Après avoir mis à niveau vos serveurs de transport Edge Exchange 2007 vers Exchange 2007 SP3 RU10, vous devez recréer l'abonnement Edge entre votre organisation Exchange et chaque serveur de transport Edge pour mettre à jour leur version de serveur dans Active Directory. Pour plus d'informations sur la recréation d'abonnements Edge dans Exchange 2007, consultez la rubrique <a href="https://go.microsoft.com/fwlink/?linkid=282699">Abonnement du serveur de transport Edge à l'organisation Exchange</a>.

