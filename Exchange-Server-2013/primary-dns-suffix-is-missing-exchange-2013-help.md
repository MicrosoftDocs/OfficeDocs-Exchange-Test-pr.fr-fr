---
title: 'Suffixe DNS principal manquant: Exchange 2013 Help'
TOCTitle: Suffixe DNS principal manquant
ms:assetid: 310765bf-a650-4a3d-a5e4-6173b559d4f6
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/ms.exch.setupreadiness.fqdnmissing(v=EXCHG.150)
ms:contentKeyID: 61204568
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Suffixe DNS principal manquant

 

_**Sapplique à :** Exchange Server_

_**Dernière rubrique modifiée :** 2014-01-15_

Le programme d’installation de Microsoft Exchange Server 2013 ne peut pas continuer car le suffixe DNS principal de l’ordinateur sur lequel vous installez Exchange n’a pas été configuré.

Pour résoudre ce problème, ajoutez un suffixe DNS principal à l’ordinateur en suivant la procédure ci-dessous, puis réexécutez le programme d’installation.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159813.important(EXCHG.150).gif" title="Important" alt="Important" />Important :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>La modification du nom d’ordinateur ou du suffixe DNS principal après l’installation d’Exchange 2013 n’est pas prise en charge.</td>
</tr>
</tbody>
</table>


1.  Ouvrez une session sur l’ordinateur où vous souhaitez installer le rôle de transport Edge en tant qu’utilisateur membre du groupe Administrateurs local.

2.  Ouvrez le **Panneau de configuration**, puis double-cliquez sur **Système**.

3.  Dans la section **Paramètres de nom d’ordinateur, de domaine et de groupe de travail**, cliquez sur **Modifier les paramètres**.

4.  Dans la fenêtre **Propriétés système**, assurez-vous que l’onglet **Nom de l’ordinateur** est sélectionné, puis cliquez sur **Modifier...**.

5.  Dans la fenêtre **Modification du nom ou du domaine de l’ordinateur**, cliquez sur **Autres...**.

6.  Dans **Suffixe DNS principal de cet ordinateur**, saisissez le nom de domaine DNS pour le serveur de transport Edge. Par exemple, contoso.com.

7.  Cliquez sur **OK** pour fermer chaque fenêtre.

Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), et [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

Avez-vous trouvé ce que vous cherchez ? Veuillez prendre une minute pour [nous envoyer votre avis à l'adresse](mailto:exsetuphelpfeedback@microsoft.com?subject=exchange%202013%20setup%20help%20feedback) au sujet des informations que vous souhaitiez y trouver.

