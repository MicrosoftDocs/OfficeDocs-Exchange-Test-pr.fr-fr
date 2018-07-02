---
title: 'La définition du lecteur du groupe de stockage est manquante_MailboxLogDriveDoesNotExist: Exchange 2013 Help'
TOCTitle: La définition du lecteur du groupe de stockage est manquante_MailboxLogDriveDoesNotExist
ms:assetid: fe210f29-60cb-4d34-877e-1356a21dc02a
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/ms.exch.setupreadiness.mailboxlogdrivedoesnotexist(v=EXCHG.150)
ms:contentKeyID: 50479646
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# La définition du lecteur du groupe de stockage est manquante\_MailboxLogDriveDoesNotExist

 

_**Sapplique à :** Exchange Server_

_**Dernière rubrique modifiée :** 2016-12-09_

Le contenu de cette rubrique n'a pas été mis à jour pour Microsoft Exchange Server 2013. Bien qu'il n'ait pas été encore mis à jour, il peut toujours être applicable pour Exchange 2013. Si vous avez toujours besoin d'aide, consultez les ressources de communauté ci-dessous.

Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), et [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

Le programme d'installation de Microsoft® Exchange Server 2007 Disaster Recovery ne peut pas poursuivre son exécution car il ne peut pas accéder à la définition de lecteur de la base de données du groupe de stockage utilisée lors de l'installation précédente sur ce serveur.

Le programme d'installation de Microsoft Exchange Disaster Recovery nécessite que les mêmes définitions de lecteur de la base de données du groupe de stockage que celles utilisées précédemment pour ce serveur soient disponibles pendant la restauration.

Pour résoudre ce problème, configurez les lecteurs de manière à correspondre à la configuration de lecteurs logiques d’origine, puis recommencez l’installation de Microsoft Exchange Disaster Recovery.

**Attribution ou modification d’une lettre de lecteur**

1.  Ouvrez **Gestion de l’ordinateur(Local)**.

2.  Dans l’arborescence de la console, cliquez sur **Gestion de l’ordinateur (local)**, sur **Stockage**, puis sur **Gestion des disques**.

3.  Cliquez avec le bouton droit sur une partition, un lecteur logique ou un volume, puis cliquez sur **Modifier la lettre de lecteur et les chemins d’accès**.

4.  Exécutez l’une des procédures suivantes :
    
      - Pour attribuer une lettre de lecteur, cliquez sur **Ajouter**, sur la lettre à utiliser, puis sur **OK**.
    
      - Pour modifier une lettre de lecteur, cliquez sur celle-ci, sur **Modifier**, sur la lettre à utiliser, puis sur **OK**.

Pour plus d’informations sur la procédure d’attribution de lettres de lecteur, consultez la rubrique Affecter, modifier ou supprimer une lettre de lecteur ([https://go.microsoft.com/fwlink/?LinkId=66764](https://go.microsoft.com/fwlink/?linkid=66764)).

