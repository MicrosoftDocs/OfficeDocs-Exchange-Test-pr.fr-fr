---
title: 'Une ou plusieurs files d’attente contiennent des messages_MessagesInQueue: Exchange 2013 Help'
TOCTitle: Une ou plusieurs files d’attente contiennent des messages_MessagesInQueue
ms:assetid: 3ffcdc7e-c1b7-49a7-8e5f-b30c0397908d
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/ms.exch.setupreadiness.messagesinqueue(v=EXCHG.150)
ms:contentKeyID: 50477961
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Une ou plusieurs files d’attente contiennent des messages\_MessagesInQueue

 

_**Sapplique à :** Exchange Server_

_**Dernière rubrique modifiée :** 2012-06-05_

Le contenu de cette rubrique n'a pas été mis à jour pour Microsoft Exchange Server 2013. Bien qu'il n'ait pas été encore mis à jour, il peut toujours être applicable pour Exchange 2013. Si vous avez toujours besoin d'aide, consultez les ressources de communauté ci-dessous.

Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), et [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

Le programme d’installation de Microsoft® Exchange Server 2007 affiche cet avertissement car la tentative de désinstallation d’un rôle Transport pourrait entraîner une perte de données dans une file d’attente de transport.

Il lance une vérification pour s’assurer que les files d’attente de transport sont vides avant de supprimer les rôles qui assurent leur gestion.

Si vous supprimez les rôles Transport avant la remise des messages que les files d’attente correspondantes contiennent, ces messages seront bloqués indéfiniment.

Pour résoudre ce problème, examinez les files d’attente référencées afin de vous assurer qu’elles sont vides, pour pouvoir continuer l’installation.

**Pour afficher le contenu d’une file d’attente**

1.  Ouvrez Exchange Management Console.

2.  Dans l'arborescence de la console, cliquez sur **Boîte à outils**.

3.  Dans le volet Résultats, cliquez sur **Afficheur des files d’attente Exchange**.

4.  Dans le volet Actions, cliquez sur **Ouvrir l'outil**.

5.  Dans l’Afficheur des files d’attente, cliquez sur l’onglet **Files d’attente**. La liste des files d’attente sur le serveur auquel vous êtes connecté s’affiche.

6.  Cliquez avec le bouton droit sur la file d’attente souhaitée, puis sélectionnez **Propriétés** pour afficher les propriétés de la file d’attente.

**Pour afficher les messages d’une file d’attente**

1.  Observez les étapes 1 à 4.

2.  Dans l’Afficheur des files d’attente, cliquez sur l’onglet **Messages**. La liste de tous les messages sur le serveur auquel vous êtes connecté s’affiche. Pour limiter l’affichage à une seule file d’attente, cliquez sur l’onglet **Files d’attente**, double-cliquez sur le nom de la file d’attente, puis cliquez sur l’onglet Serveur\\File d’attente qui s’affiche.

3.  Pour afficher des informations détaillées sur un message, sélectionnez-le, puis cliquez sur **Propriétés** dans le volet Actions.

