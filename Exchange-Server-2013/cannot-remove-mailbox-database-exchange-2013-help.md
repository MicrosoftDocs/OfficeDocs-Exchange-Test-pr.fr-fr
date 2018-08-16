---
title: 'Impossible de supprimer la BDD de BAL: Exchange 2013 Help'
TOCTitle: Impossible de supprimer la base de données de boîtes aux lettres
ms:assetid: 5881e4c0-c2e2-48db-84b4-7f9ce3cf46a7
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/ms.exch.setupreadiness.unwillingtoremovemailboxdatabase(v=EXCHG.150)
ms:contentKeyID: 50478141
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Impossible de supprimer la base de données de boîtes aux lettres

 

_**Sapplique à :** Exchange Server_

_**Dernière rubrique modifiée :** 2012-11-08_

Impossible de poursuivre le programme d’installation de Microsoft Exchange Server 2013 car il ne peut pas supprimer une base de données de boîte aux lettres d’utilisateur du serveur local sans risquer une éventuelle perte de données.

Le programme d’installation d’Exchange 2013 vérifie si toutes les bases de données de boîtes aux lettres sont supprimées du serveur avant la suppression du rôle serveur de boîte aux lettres. Il se peut toutefois que des boîtes aux lettres utilisateur restent sur le serveur.

Pour résoudre ce problème, déplacez toutes les boîtes de données du serveur vers un autre serveur Exchange ou, si les boîtes aux lettres et les données qu’elles contiennent ne sont plus nécessaires, désactivez les boîtes aux lettres. Réexécutez ensuite le programme d’installation Exchange 2013.

  - Pour plus d’informations sur l’identification d’une boîte aux lettres dans la base de données, consultez la rubrique [Get-Mailbox](https://technet.microsoft.com/fr-fr/library/bb123685\(v=exchg.150\)).

  - Pour plus d’informations sur le déplacement d’une boîte aux lettres, consultez la rubrique [Déplacements de boîtes aux lettres dans Exchange 2013](mailbox-moves-in-exchange-2013-exchange-2013-help.md).

  - Pour plus d’informations sur la désactivation d’une boîte aux lettres, consultez la rubrique [Disable-Mailbox](https://technet.microsoft.com/fr-fr/library/aa997210\(v=exchg.150\)).

  - Pour plus d’informations sur la suppression d’une base de données de boîtes aux lettres, consultez la rubrique [Gestion des bases de données de boîtes aux lettres dans Exchange 2013](manage-mailbox-databases-in-exchange-2013-exchange-2013-help.md).

Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), et [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

Avez-vous trouvé ce que vous cherchez ? Veuillez prendre une minute pour [nous envoyer votre avis à l'adresse](mailto:exsetuphelpfeedback@microsoft.com?subject=exchange%202013%20setup%20help%20feedback) au sujet des informations que vous souhaitiez y trouver.

