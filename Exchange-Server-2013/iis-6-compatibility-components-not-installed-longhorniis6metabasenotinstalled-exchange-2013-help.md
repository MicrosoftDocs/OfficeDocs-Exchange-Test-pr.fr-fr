---
title: 'Composants de compatibilité IIS 6 non installés_LonghornIIS6MetabaseNotInstalled: Exchange 2013 Help'
TOCTitle: Composants de compatibilité IIS 6 non installés_LonghornIIS6MetabaseNotInstalled
ms:assetid: 0bd52987-d3cc-496c-ac8c-d35591405195
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/ms.exch.setupreadiness.longhorniis6metabasenotinstalled(v=EXCHG.150)
ms:contentKeyID: 50477491
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Composants de compatibilité IIS 6 non installés\_LonghornIIS6MetabaseNotInstalled

 

_**Sapplique à :** Exchange Server_

_**Dernière rubrique modifiée :** 2012-06-05_

Le contenu de cette rubrique n'a pas été mis à jour pour Microsoft Exchange Server 2013. Bien qu'il n'ait pas été encore mis à jour, il peut toujours être applicable pour Exchange 2013. Si vous avez toujours besoin d'aide, consultez les ressources de communauté ci-dessous.

Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), et [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

Microsoft® Le programme d’installation d’Exchange Server 2007 ne peut pas poursuivre sa tentative d’installation du rôle serveur d’accès au client, du rôle de boîte aux lettres ou des outils d’administration Exchange 2007 sur les systèmes d’exploitation Windows suivants :

  - Windows Server 2008 R2

  - Windows Server 2008

  - Windows 7 (outils d’administration uniquement)

  - Windows Vista (outils d’administration uniquement)

Ce problème survient, car les composants Compatibilité avec la métabase de données IIS 6 et Console de gestion IIS 6 ne sont pas installés.

L’installation d’Exchange 2007 nécessite que l’ordinateur sur lequel vous installez le rôle serveur d’accès au client ou le rôle serveur de boîtes aux lettres Exchange 2007 ou les outils d’administration d’Exchange 2007 possède les composants Compatibilité avec la métabase de données IIS 6 et Console de gestion IIS 6.

Pour résoudre ce problème, installez le composant Compatibilité avec la métabase de données IIS 6 sur l’ordinateur de destination, puis réexécutez le programme d’installation Microsoft Exchange.

**Installez les composants Compatibilité avec la gestion IIS 6.0 dans Windows Server 2008 R2 ou dans Windows Server à l’aide de l’outil Gestionnaire de serveur.**

1.  Cliquez sur **Démarrer**, cliquez sur **Outils d’administration**, puis cliquez sur **Gestionnaire de serveur**.

2.  Dans le volet de navigation, développez **Rôles**, cliquez avec le bouton droit de la souris sur **Serveur Web (IIS)**, puis sur **Ajouter des services de rôle**.

3.  Dans le volet **Sélectionner les services de rôle**, faites défiler jusqu’à **Compatibilité avec la gestion IIS 6**.

4.  Cliquez pour cocher les cases **Compatibilité avec la métabase de données IIS 6**, **Compatibilité avec le service WMI IIS 6** et **Console de gestion IIS 6**.

5.  Dans le volet **Sélectionner les services de rôle**, cliquez sur **Suivant**.

6.  Dans le volet **Confirmer les sélections pour l’installation**, cliquez sur **Installer**.

7.  Cliquez sur **Fermer** pour quitter l’Assistant Ajouter des services de rôle.

**Installer les composants Compatibilité avec la gestion IIS 6.0 dans Windows 7 ou dans Windows Vista à partir du Panneau de configuration.**

1.  Cliquez sur **Démarrer**, **Panneau de configuration**, **Programmes et fonctionnalités**, puis sur **Activer ou désactiver des fonctionnalités Windows**.

2.  Ouvrez **Services IIS**.

3.  Ouvrez **Outils d’administration web**.

4.  Ouvrez **Compatibilité avec la gestion IIS 6.0**.

5.  Cliquez pour cocher les cases **Compatibilité avec la métabase IIS 6 et la configuration IIS 6**, **Compatibilité avec le service WMI IIS 6** et **Console de gestion IIS 6**.

6.  Cliquez sur **OK**.

