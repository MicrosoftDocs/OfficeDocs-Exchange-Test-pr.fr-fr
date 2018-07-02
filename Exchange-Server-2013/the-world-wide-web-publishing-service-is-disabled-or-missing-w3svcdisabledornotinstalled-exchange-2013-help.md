---
title: 'Le service de publication World Wide Web est désactivé ou manquant_W3SVCDisabledOrNotInstalled: Exchange 2013 Help'
TOCTitle: Le service de publication World Wide Web est désactivé ou manquant_W3SVCDisabledOrNotInstalled
ms:assetid: 2d26d778-ddf1-4225-b5e2-f6b49d819c94
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/ms.exch.setupreadiness.w3svcdisabledornotinstalled(v=EXCHG.150)
ms:contentKeyID: 50477748
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Le service de publication World Wide Web est désactivé ou manquant\_W3SVCDisabledOrNotInstalled

 

_**Sapplique à :**Exchange Server_

_**Dernière rubrique modifiée :**2012-06-05_

Le contenu de cette rubrique n'a pas été mis à jour pour Microsoft Exchange Server 2013. Bien qu'il n'ait pas été encore mis à jour, il peut toujours être applicable pour Exchange 2013. Si vous avez toujours besoin d'aide, consultez les ressources de communauté ci-dessous.

Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), et [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

Le programme d’installation de Microsoft® Exchange Server 2007 ne peut pas poursuivre son exécution car sa tentative d’installation du rôle Mailbox Server ou Client Access a détecté que le service de publication sur le World Wide Web est désactivé ou n’est pas installé sur cet ordinateur.

L’installation d’Exchange 2007 nécessite que le service de publication sur le World Wide Web soit installé sur l’ordinateur sur lequel vous installez Microsoft Exchange et défini sur une autre valeur que désactivé.

Pour résoudre ce problème, vérifiez que le service de publication sur le World Wide Web est installé et n’est pas désactivé sur l’ordinateur local, puis recommencez l’installation de Microsoft Exchange.

Pour vérifier que le service de publication sur le World Wide Web est installé et n’est pas désactivé

1.  Cliquez avec le bouton droit sur **Poste de travail** sur le Bureau, puis cliquez sur **Gérer**.

2.  Développez le nœud **Services et applications**, puis cliquez sur le nœud **Services**.

3.  Dans le volet droit, recherchez le **service de publication World Wide Web**.
    
    Si le **service de publication World Wide Web** n’est pas affiché dans la liste des services installés, exécutez la procédure suivante pour l’installer.

4.  Si le **service de publication World Wide Web** est affiché, mais que son état n’est pas **Démarré**, exécutez la procédure suivante pour le démarrer.

5.  Cliquez avec le bouton droit sur **Service de publication World Wide Web** , puis cliquez sur **Propriétés**.

6.  Vérifiez que le **type de démarrage** est **Automatique** et que l’**état du service** est défini sur **Démarré**.

7.  Cliquez sur **Appliquer**, puis sur **OK**.

Pour installer le service de publication sur le World Wide Web

1.  Cliquez sur le menu **Démarrer**, sélectionnez successivement **Paramètres** et **Panneau de configuration**, puis cliquez sur **Ajout/Suppression de programmes**.

2.  Cliquez sur **Ajouter/Supprimer des composants Windows**.

3.  Dans la liste **Composants**, cochez la case **Serveur d’applications**, puis cliquez sur **Détails**.

4.  Sélectionnez **Gestionnaire des services IIS**, puis cliquez sur **Détails**.

5.  Sélectionnez **Service World Wide Web**, puis cochez la case.

6.  Cliquez sur **OK** à deux reprises pour revenir à la liste **Composants**, puis cliquez sur **Suivant**.

7.  Cliquez sur **Terminer** lorsque le service IIS est installé.

