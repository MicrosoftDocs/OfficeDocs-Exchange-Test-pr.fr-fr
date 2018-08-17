---
title: 'Mettre à niveau Exchange 2013 vers le nouveau Service Pack ou màj cumulative'
TOCTitle: Mettre à niveau Exchange 2013 vers la mise à jour cumulative la plus récente ou vers le Service Pack le plus récent
ms:assetid: 928a4a0b-0082-4d50-a696-bfaf2782f42d
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ983803(v=EXCHG.150)
ms:contentKeyID: 52062981
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Mettre à niveau Exchange 2013 vers la mise à jour cumulative la plus récente ou vers le Service Pack le plus récent

 

_**Sapplique à :** Exchange Online, Exchange Server, Exchange Server 2013_

_**Dernière rubrique modifiée :** 2015-09-04_

Si vous disposez de Microsoft Exchange Server 2013, vous pouvez le mettre à niveau vers la mise à jour cumulative la plus récente ou le Service Pack le plus récent pour Exchange 2013. Vous pouvez utiliser l’Assistant Configuration d’Exchange 2013 pour mettre à niveau la version d'Exchange 2013 que vous utilisez actuellement. Pour plus d’informations sur la mise à jour cumulative la plus récente ou le Service Pack le plus récent pour Exchange 2013, consultez la rubrique [Mises à jour pour Exchange 2013](updates-for-exchange-2013-exchange-2013-help.md). Pour en savoir plus sur Exchange 2013, consultez la rubrique [Nouveautés d'Exchange 2013](what-s-new-in-exchange-2013-exchange-2013-help.md).

> [!WARNING]
> Après avoir mis à niveau Exchange 2013 vers une mise à jour cumulative plus récente ou un Service Pack plus récent, vous ne pouvez plus revenir en arrière. Si vous désinstallez la nouvelle version, vous supprimez Exchange du serveur.


## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : 60 minutes

  - Veillez à lire les notes de publication avant d'installer Exchange 2013. Pour plus d'informations, consultez la rubrique [Notes de publication relatives à Exchange 2013](release-notes-for-exchange-2013-exchange-2013-help.md).

  - Assurez-vous que tous les serveurs sur lesquels vous souhaitez installer la mise à jour cumulative ou le Service Pack satisfont aux exigences et aux conditions préalables du système. Pour plus d'informations, consultez les rubriques [Configuration requise pour Exchange 2013](exchange-2013-system-requirements-exchange-2013-help.md) et [Conditions préalables pour Exchange 2013](exchange-2013-prerequisites-exchange-2013-help.md).
    
    > [!WARNING]
    > Les paramètres par serveur personnalisés de vos fichiers de configuration d’application XML Exchange, par exemple les fichiers web.config sur les serveurs d’accès au client ou le fichier EdgeTransport.exe.config sur les serveurs de boîtes aux lettres, seront remplacés lors de l’installation d’une mise à jour cumulative Exchange. Veuillez enregistrer ces informations pour configurer à nouveau votre serveur après l’installation. Vous devez reconfigurer ces paramètres après avoir installé une mise à jour cumulative Exchange.


  - Une fois la mise à jour cumulative ou le Service Pack installé, vous devez redémarrer l’ordinateur pour que les changements soient pris en compte dans le Registre et le système d’exploitation.

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.


## Installer la mise à jour cumulative ou le Service Pack pour Exchange 2013

Vous pouvez installer la mise à jour cumulative ou le Service Pack pour Exchange 2013 en utilisant l’Assistant Installation ou en mode sans assistance. Pour obtenir des instructions détaillées, consultez les rubriques suivantes :

  - [Installer Exchange 2013 à l’aide de l’Assistant Installation](install-exchange-2013-using-the-setup-wizard-exchange-2013-help.md)

  - [Installation d’Exchange 2013 en mode sans assistance](install-exchange-2013-using-unattended-mode-exchange-2013-help.md)

Si l’ordinateur sur lequel vous avez installé un Service Pack ou une mise à jour cumulative est membre d’un groupe de disponibilité de base de données (DAG), suivez les étapes de la section [Exécution de la maintenance sur les groupes du groupe de disponibilité de base de données (DAG)](managing-database-availability-groups-exchange-2013-help.md) de la rubrique [Gestion de groupes de disponibilité de base de données](managing-database-availability-groups-exchange-2013-help.md).

