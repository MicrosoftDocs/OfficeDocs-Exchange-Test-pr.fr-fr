---
title: 'Le composant de modèle de processus de service d’activation des processus Windows est required_LonghornWASProcessModelInstalled: Exchange 2013 Help'
TOCTitle: Le composant de modèle de processus de service d’activation des processus Windows est required_LonghornWASProcessModelInstalled
ms:assetid: 8cc13dbb-4921-4c07-8602-d26613d7730a
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/ms.exch.setupreadiness.longhornwasprocessmodelinstalled(v=EXCHG.150)
ms:contentKeyID: 50478664
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Le composant de modèle de processus de service d’activation des processus Windows est required\_LonghornWASProcessModelInstalled

 

_**Sapplique à :**Exchange Server_

_**Dernière rubrique modifiée :**2015-04-07_

Le contenu de cette rubrique n'a pas été mis à jour pour Microsoft Exchange Server 2013. Bien qu'il n'ait pas été encore mis à jour, il peut toujours être applicable pour Exchange 2013. Si vous avez toujours besoin d'aide, consultez les ressources de communauté ci-dessous.

Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), et [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

Le programme d’installation d’Exchange Server 2010 ne peut pas poursuivre l’installation sur l’ordinateur Windows Server 2008 ou Windows Server 2008 R2 car la fonctionnalité Modèle de processus du service d’activation des processus Windows n’est pas installée sur le serveur.

Le service d’activation des processus Windows généralise le modèle de processus Internet Information Services (IIS) en éliminant la dépendance envers le protocole HTTP. Toutes les fonctionnalités d’IIS précédemment disponibles uniquement pour les applications HTTP sont désormais disponibles pour les applications hébergeant des services Windows Communication Foundation (WCF), à l’aide de protocoles non-HTTP. IIS 7.0 utilise également le service d’activation des processus Windows pour l’activation basée sur des messages sur HTTP.

Le modèle de processus héberge les services web et WCF. Introduit dans IIS 6.0, le modèle de processus est une nouvelle architecture bénéficiant d’une protection rapide contre les incidents, d’un contrôle de l’intégrité et du recyclage.

Pour résoudre ce problème, installez la fonctionnalité Modèle de processus du service d'activation des processus Windows sur ce serveur, puis réexécutez le programme d'installation d'Exchange 2010.

Installer le service d’activation des processus Windows - fonctionnalité de modèle de processus à l’aide de l’outil Gestionnaire de serveur

1.  Cliquez sur **Démarrer**, sur **Outils d'administration**, puis sur **Gestionnaire de serveur**.

2.  Dans le volet de navigation gauche, cliquez avec le bouton droit sur **Fonctionnalités**, puis cliquez sur **Ajouter des fonctionnalités**.

3.  Dans le volet **Sélectionner des fonctionnalités**, faites défiler vers le bas vers **Service d’activation des processus Windows**.

4.  Cochez les cases correspondant à **Modèle de processus**.

5.  Cliquez sur **Suivant** dans le volet **Sélectionner des fonctionnalités**, puis cliquez sur **Installer** dans le volet **Confirmer les sélections d’installation**.

6.  Cliquez sur **Fermer** pour quitter l’assistant Ajouter des services de rôle.

