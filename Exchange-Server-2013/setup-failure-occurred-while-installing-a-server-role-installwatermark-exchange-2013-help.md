---
title: 'Échec du programme d’installation lors de l’installation d’un rôle serveur'
TOCTitle: Échec du programme d’installation lors de l’installation d’un rôle serveur_InstallWatermark
ms:assetid: ad89ebd5-f9bb-40c1-8811-09b145c2b341
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/ms.exch.setupreadiness.installwatermark(v=EXCHG.150)
ms:contentKeyID: 50478990
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Échec du programme d’installation lors de l’installation d’un rôle serveur\_InstallWatermark

 

_**Sapplique à :** Exchange Server_

_**Dernière rubrique modifiée :** 2016-12-09_

Le contenu de cette rubrique n'a pas été mis à jour pour Microsoft Exchange Server 2013. Bien qu'il n'ait pas été encore mis à jour, il peut toujours être applicable pour Exchange 2013. Si vous avez toujours besoin d'aide, consultez les ressources de communauté ci-dessous.

Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), et [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

Le programme d'installation Microsoft Exchange Server 2007 ne peut pas poursuivre son exécution car le programme d'installation a échoué lors de l'installation d'un rôle serveur.

L'installation d'Exchange 2007 nécessite qu'un rôle serveur soit correctement réinstallé ou supprimé du processus d'installation avant de pouvoir continuer une autre tâche d'installation.

Pour résoudre ce problème, réinstallez le rôle serveur échoué ou supprimez-le.

**Pour réinstaller le rôle serveur en échec pour la ligne de commande**

1.  Ouvrez une fenêtre d'invite de commandes et naviguez jusqu'à l'emplacement des fichiers d'installation.

2.  Exécutez la commande suivante :
    
    ```powershell
Setup /roles:<Failed Server Role>
```
    
    Sélectionnez un ou plusieurs des rôles suivants dans une liste séparée par des virgules :
    
    ClientAccess (ou CA, ou C)
    
    EdgeTransport (ou ET, ou E)
    
    > [!NOTE]
    > Le rôle serveur de transport Edge ne peut pas coexister sur le même ordinateur qu'un autre rôle serveur.
    
    > [!NOTE]
    > Vous devez déployer le rôle serveur de transport Edge dans le réseau de périmètre et à l’extérieur de la forêt Active Directory.
    
    HubTransport (ou HT, ou H)
    
    Mailbox (ou MB, ou M)
    
    UnifiedMessaging (ou MU, ou U)
    
    ManagementTools (ou MT, ou T)
    
    > [!NOTE]
    > En choisissant Outils de gestion, vous installez la console de gestion Exchange, les cmdlets Exchange pour l’environnement de ligne de commandeExchange Management Shell, le fichier d’aide Exchange, l’outil Exchange Best Practices Analyzer et l’Assistant Dépannage Exchange. Si vous installez un autre rôle serveur, les outils de gestion sont installés automatiquement.
    
    Par exemple, pour ajouter le rôle serveur de transport Hub à un serveur de boîte aux lettres existant, entrez les informations suivantes : **%LocalExchangeInstallationDir%\\bin\\Setup.com /role:HubTransport /Mode:Install**

> [!NOTE]
> Si un rôle serveur Exchange Server 2007 avait été installé, l'Assistant Installation est exécuté en mode maintenance. Si aucun rôle serveur Exchange 2007 n'avait été installé, l'Assistant Installation commence à l'endroit où il s'est arrêté.


**Pour utiliser l'Assistant Installation d'Exchange Server 2007 en mode maintenance pour réinstaller le rôle serveur en échec**

1.  Ouvrez une session sur le serveur sur lequel vous souhaitez réinstaller un rôle serveur.

2.  Ouvrez Panneau de configuration, puis double-cliquez sur **Ajout/Suppression de programmes**.

3.  Dans la page **Modifier ou supprimer des programmes**, sélectionnez **Microsoft Exchange Server**, puis cliquez sur **Modifier**.

4.  Dans l’Assistant Installation Exchange Server 2007, dans la page **Mode de maintenance d’Exchange**, cliquez sur **Suivant**.

5.  Dans la page **Sélection des rôles serveur**, cochez les cases des rôles serveur à installer, puis cliquez sur **Suivant**.
    
    > [!NOTE]
    > Le rôle serveur de transport Edge ne peut pas coexister sur le même ordinateur qu'un autre rôle serveur.
    
    > [!NOTE]
    > Vous devez déployer le rôle serveur de transport Edge dans le réseau de périmètre et à l’extérieur de la forêt Active Directory.
    
    > [!NOTE]
    > En sélectionnant Outils de gestion, vous installez la console de gestion Exchange, les cmdlets Exchange pour l’environnement de ligne de commande Exchange Management Shell et le fichier d’aide d’Exchange. Les outils de gestion sont installés automatiquement si vous installez un autre rôle serveur.


6.  Si vous avez sélectionné **Rôle de transport Hub** et si vous installez Exchange 2007 dans une forêt disposant d’une organisation Exchange Server 2003 ou Exchange 2000 Server existante, dans la page **Paramètres du flux de messagerie**, sélectionnez un serveur tête de pont dans l’organisation existante membre du groupe de routage Exchange 2003 ou Exchange 2000 dans lequel vous voulez créer un connecteur de groupe de routage.

7.  Sur la page **Tests de préparation**, affichez l’état pour déterminer si les vérifications des prérequis de l’organisation et du rôle serveur ont été réalisées avec succès. Si l’opération est terminée, cliquez sur **Installer** pour installer Exchange 2007.

8.  Dans la page **Achèvement**, cliquez sur **Terminer**.

**Pour utiliser l'Assistant Installation d'Exchange Server 2007 pour réinstaller le rôle serveur en échec si aucun rôle serveur n'avait été installé**

1.  Suivez les étapes de la rubrique « Procédure d’exécution d’une installation personnalisée à l’aide de l’Assistant Installation d’Exchange Server 2007 » ([https://go.microsoft.com/fwlink/?LinkId=86648](https://go.microsoft.com/fwlink/?linkid=86648)) dans la documentation sur le produit Exchange Server 2007.

**Pour supprimer le rôle serveur qui a échoué**

1.  Suivez les étapes de la rubrique sur la procédure de suppression des rôles serveur Exchange 2007 Server ([https://go.microsoft.com/fwlink/?LinkId=86649](https://go.microsoft.com/fwlink/?linkid=86649)) dans la documentation sur le produit Exchange Server 2007.

## Pour plus d'informations

Pour plus d’informations sur la procédure d’installation d’Exchange 2007 sans assistance, voir la rubrique « Procédure d’installation d’Exchange 2007 en mode sans assistance » ([https://go.microsoft.com/fwlink/?LinkId=86476](https://go.microsoft.com/fwlink/?linkid=86476)).

