---
title: 'Le service de système d’événement COM+ doit être démarré pour pouvoir poursuivre l’installation_EventSystemStopped: Exchange 2013 Help'
TOCTitle: Le service de système d’événement COM+ doit être démarré pour pouvoir poursuivre l’installation_EventSystemStopped
ms:assetid: 3b8d2ba3-87fb-4749-b4d1-5dfec97e1ca4
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/ms.exch.setupreadiness.eventsystemstopped(v=EXCHG.150)
ms:contentKeyID: 50477941
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Le service de système d’événement COM+ doit être démarré pour pouvoir poursuivre l’installation\_EventSystemStopped

 

_**Sapplique à :**Exchange Server_

_**Dernière rubrique modifiée :**2012-06-05_

Le contenu de cette rubrique n'a pas été mis à jour pour Microsoft Exchange Server 2013. Bien qu'il n'ait pas été encore mis à jour, il peut toujours être applicable pour Exchange 2013. Si vous avez toujours besoin d'aide, consultez les ressources de communauté ci-dessous.

Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), et [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

Le programme d’installation de Microsoft Exchange Server 2007 ne peut pas poursuivre son exécution car sa tentative d’installer les rôles serveur d’accès au client ou de transport Edge a échoué parce que le système d’événement COM+ n’est pas démarré sur l’ordinateur cible.

L’installation d’Exchange 2007 nécessite que le statut du système d’événement COM+ soit défini sur **Démarré** sur l’ordinateur sur lequel vous installez Microsoft Exchange.

Le système d’événement COM+ prend en charge la notification d’événement de système pour les composants COM+ qui fournissent une distribution automatique d’événements aux composants COM d’abonnement.

Les deux rôles serveurs ont des dépendances sur les composants COM+ qui s’abonnent au système d’événement COM+.

Pour résoudre ce problème, vérifiez que le statut du système d’événement COM+ est défini sur **Démarré** sur l’ordinateur local, puis réexécutez le programme d’installation de Microsoft Exchange.

Pour définir le statut du système d’événement COM+ sur « Démarré »

1.  Cliquez avec le bouton droit sur **Poste de travail** puis cliquez sur **Gérer**.

2.  Développez le nœud **Services et applications**, puis cliquez sur le nœud **Services**.

3.  Dans le volet droit, recherchez **Système d’événement Com+**.

4.  Cliquez avec le bouton droit sur **Système d’événement Com+**, puis cliquez sur **Propriétés**.

5.  Définissez le **type de démarrage** sur **Automatique** et le**statut du service** sur **Démarré**.

6.  Cliquez sur **Appliquer**, puis sur **OK**.

