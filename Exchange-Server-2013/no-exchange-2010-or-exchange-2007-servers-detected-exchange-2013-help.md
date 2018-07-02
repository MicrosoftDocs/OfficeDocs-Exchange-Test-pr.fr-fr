---
title: 'Aucun serveur Exchange 2010 ou Exchange 2007 détecté: Exchange 2013 Help'
TOCTitle: Aucun serveur Exchange 2010 ou Exchange 2007 détecté
ms:assetid: 789cabab-c769-4a16-a6c8-3db82cff8861
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/ms.exch.setupreadiness.noe14serverwarning(v=EXCHG.150)
ms:contentKeyID: 50478508
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Aucun serveur Exchange 2010 ou Exchange 2007 détecté

 

_**Sapplique à :** Exchange Server_

_**Dernière rubrique modifiée :** 2012-11-08_

Le programme d’installation de Microsoft Exchange Server 2013 a affiché cet avertissement car aucun rôle de serveur Exchange Server 2010 ou Exchange Server 2007 n’existe dans l’organisation.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ673034.Caution(EXCHG.150).gif" title="Attention" alt="Attention" />Attention :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Si vous poursuivez l’installation d’Exchange Server 2013, vous ne serez pas en mesure d’ajouter ultérieurement des serveurs Exchange 2010 ou Exchange 2007 à l’organisation.</td>
</tr>
</tbody>
</table>


Avant de déployer Exchange 2013, tenez compte des facteurs suivants qui peuvent nécessiter le déploiement de serveurs Exchange 2010 ou Exchange 2007 avant le déploiement d’Exchange 2013 :

  - **Applications tierces ou développées en interne**   Il est possible que des applications développées pour d’anciennes versions d’Exchange ne soient pas compatibles avec Exchange 2013. Vous devrez peut-être maintenir des serveurs Exchange 2010 ou Exchange 2007 pour prendre en charge ces applications.

  - **Exigences de coexistence ou de migration**   Si vous planifiez de migrer des boîtes aux lettres dans votre organisation, certaines solutions peuvent nécessiter l’utilisation de serveurs Exchange 2010 ou Exchange 2007.

Si vous décidez de déployer des serveurs Exchange 2010 ou Exchange 2007, vous devez le faire avant de déployer Exchange 2013. Active Directory doit être préparé pour chaque version d’Exchange dans l’ordre suivant :

1.  Exchange 2007

2.  Exchange 2010

3.  Exchange 2013

Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), et [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

Avez-vous trouvé ce que vous cherchez ? Veuillez prendre une minute pour [nous envoyer votre avis à l'adresse](mailto:exsetuphelpfeedback@microsoft.com?subject=exchange%202013%20setup%20help%20feedback) au sujet des informations que vous souhaitiez y trouver.

