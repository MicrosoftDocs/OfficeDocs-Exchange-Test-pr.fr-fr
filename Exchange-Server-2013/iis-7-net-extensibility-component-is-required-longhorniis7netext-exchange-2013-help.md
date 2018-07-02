---
title: 'Le composant Extensibilité .NET ISS 7 est requis_LonghornIIS7NetExt: Exchange 2013 Help'
TOCTitle: Le composant Extensibilité .NET ISS 7 est requis_LonghornIIS7NetExt
ms:assetid: 8b481626-b68a-4fba-b66e-a02c03856bfd
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/ms.exch.setupreadiness.longhorniis7netext(v=EXCHG.150)
ms:contentKeyID: 50478650
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Le composant Extensibilité .NET ISS 7 est requis\_LonghornIIS7NetExt

 

_**Sapplique à :**Exchange Server_

_**Dernière rubrique modifiée :**2012-06-05_

Le contenu de cette rubrique n'a pas été mis à jour pour Microsoft Exchange Server 2013. Bien qu'il n'ait pas été encore mis à jour, il peut toujours être applicable pour Exchange 2013. Si vous avez toujours besoin d'aide, consultez les ressources de communauté ci-dessous.

Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), et [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

Microsoft® Le programme d’installation d’Exchange Server 2010 ne peut pas poursuivre son exécution, car le composant obligatoire Extensibilité .NET IIS 7 n’est pas installé sur le serveur cible.

Pour qu’Exchange 2010 utilise la fonctionnalité d’accès à distance Windows PowerShell, le composant Extensibilité .NET IIS 7 doit être installé sur le serveur cible.

Pour résoudre cette erreur, utilisez le Gestionnaire de serveur pour installer le composant Extensibilité .NET IIS 7 sur ce serveur, puis réexécutez le programme d’installation d’Exchange 2010.

Installez le composant Extensibilité .NET IIS 7 dans Windows Server 2008 ou dans Windows Server 2008 R2 à l’aide de l’outil Gestionnaire de serveur.

1.  Cliquez sur **Démarrer**, sur **Outils d’administration**, puis sur **Gestionnaire de serveur**.

2.  Dans le volet de navigation gauche, développez **Rôles**, puis cliquez avec le bouton droit sur **Serveur Web (IIS)** et sélectionnez **Ajouter des services de rôle**.

3.  Dans le volet **Sélectionner les services de rôle**, faites défiler jusqu’à **Développement d’applications**.

4.  Cochez la case sous **Extensibilité .NET**.

5.  Cliquez sur **Suivant** dans le volet **Sélectionner les services de rôle**, puis sur **Installer** dans le volet **Confirmer les sélections d’installation**.

6.  Cliquez sur **Fermer** pour quitter l’Assistant Ajouter des services de rôle.

