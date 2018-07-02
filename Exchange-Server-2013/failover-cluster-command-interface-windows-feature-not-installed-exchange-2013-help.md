---
title: 'Fonctionnalité Windows Interface de commande de cluster de basculement non installée: Exchange 2013 Help'
TOCTitle: Fonctionnalité Windows Interface de commande de cluster de basculement non installée
ms:assetid: 0d839514-5ab7-497d-8945-41392b4c3980
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/ms.exch.setupreadiness.rsatclusteringcmdinterfaceinstalled(v=EXCHG.150)
ms:contentKeyID: 51407155
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Fonctionnalité Windows Interface de commande de cluster de basculement non installée

 

_**Sapplique à :**Exchange Server_

_**Dernière rubrique modifiée :**2014-12-03_

Le programme d’installation de Microsoft Exchange Server 2013 ne peut pas continuer, car une fonctionnalité Windows requise fait défaut sur l’ordinateur local. Vous devez installer cette fonctionnalité Windows pour poursuivre l’installation d’Exchange 2013.

La configuration de Exchange 2013 requiert que la fonctionnalité Windows **Interface de commande de cluster de basculement** soit installée sur l’ordinateur pour pouvoir poursuivre l’installation.

Procédez comme suit pour installer la fonctionnalité Windows sur cet ordinateur. Si un redémarrage est requis pour terminer l’installation de cette fonctionnalité, vous devez quitter le programme d’installation d’Exchange 2013, redémarrer et relancer le programme d’installation.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Vous serez peut-être amené à installer d’autres mises à jour ou d’autres fonctionnalités Windows pour pouvoir poursuivre le programme d’installation d’Exchange 2013. Pour obtenir la liste complète des mises à jour et des fonctionnalités Windows requises, voir <a href="exchange-2013-prerequisites-exchange-2013-help.md">Conditions préalables pour Exchange 2013</a>.</td>
</tr>
</tbody>
</table>


1.  Ouvrez Windows PowerShell sur l’ordinateur local.

2.  Exécutez la commande suivante pour installer la fonctionnalité Windows requise.
    
        Install-WindowsFeature RSAT-Clustering-CmdInterface

Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), et [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

Avez-vous trouvé ce que vous cherchez ? Veuillez prendre une minute pour [nous envoyer votre avis à l'adresse](mailto:exsetuphelpfeedback@microsoft.com?subject=exchange%202013%20setup%20help%20feedback) au sujet des informations que vous souhaitiez y trouver.

