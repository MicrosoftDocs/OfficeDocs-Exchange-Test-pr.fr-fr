---
title: 'L’ordinateur local exécute déjà Exchange Server_ExchangeAlreadyInstalled: Exchange 2013 Help'
TOCTitle: L’ordinateur local exécute déjà Exchange Server_ExchangeAlreadyInstalled
ms:assetid: 3f168b5d-9910-418f-86fb-e99d852dcb5e
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/ms.exch.setupreadiness.exchangealreadyinstalled(v=EXCHG.150)
ms:contentKeyID: 50478007
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# L’ordinateur local exécute déjà Exchange Server\_ExchangeAlreadyInstalled

 

_**Sapplique à :**Exchange Server_

_**Dernière rubrique modifiée :**2012-06-05_

Le contenu de cette rubrique n'a pas été mis à jour pour Microsoft Exchange Server 2013. Bien qu'il n'ait pas été encore mis à jour, il peut toujours être applicable pour Exchange 2013. Si vous avez toujours besoin d'aide, consultez les ressources de communauté ci-dessous.

Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), et [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

Le programme d’installation de Microsoft® Exchange Server 2007 ne peut pas poursuivre son exécution car des composants antérieurs de Microsoft Exchange sont installés sur l’ordinateur local.

Le programme d’installation d’Exchange 2007 nécessite qu’aucun composant existant de Microsoft Exchange ne soit installé sur l’ordinateur local.

Pour résoudre ce problème, supprimez tous les composants de Microsoft Exchange 2000 Server ou de Microsoft Exchange Server 2003, puis recommencez l’installation de Microsoft Exchange.

Suppression des composants de Microsoft Exchange

1.  Cliquez sur **Démarrer**, pointez sur **Paramètres**, puis cliquez sur **Panneau de configuration**.

2.  Double-cliquez sur **Ajout/Suppression de programmes**.

3.  Dans la liste **Programmes actuellement installés**, cliquez sur **Microsoft Exchange**, puis sur **Modifier/Supprimer**.

4.  Dans l’Assistant Installation de Microsoft Exchange, cliquez sur **Suivant**.

5.  Dans la liste Action de la page Sélection des composants, cliquez sur la flèche vers le bas en regard de chaque composant installé, puis cliquez sur **Supprimer**.
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Les composants installés sont marqués par une coche dans la liste Action. Si vous cliquez sur <strong>Supprimer</strong>, cette coche est remplacée par le mot <strong>Supprimer</strong>.</td>
    </tr>
    </tbody>
    </table>


6.  Cliquez deux fois sur **Suivant**.

7.  Cliquez sur **Terminer**.

