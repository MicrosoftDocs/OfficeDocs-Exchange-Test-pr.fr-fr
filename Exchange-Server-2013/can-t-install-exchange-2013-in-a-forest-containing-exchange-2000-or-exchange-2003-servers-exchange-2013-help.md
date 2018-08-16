---
title: 'Imp. d’installer Exchange 2013 dans une forêt avec srv Exchange 2000 ou 2003'
TOCTitle: Impossible d'installer Exchange 2013 dans une forêt contenant des serveurs Exchange 2000 ou Exchange 2003.
ms:assetid: a115b182-cbd2-4d31-aa0e-375240939301
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/ms.exch.setupreadiness.exchange2000or2003presentinorg(v=EXCHG.150)
ms:contentKeyID: 50478926
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Impossible d'installer Exchange 2013 dans une forêt contenant des serveurs Exchange 2000 ou Exchange 2003.

 

_**Sapplique à :** Exchange Server_

_**Dernière rubrique modifiée :** 2016-12-09_

Microsoft Exchange Server 2013 ne peut pas poursuivre son exécution car un ou plusieurs ordinateurs exécutant Exchange 2000 Server ou Exchange Server 2003 ont été détectés dans la forêt Active Directory. Avant de pouvoir installer Exchange 2013, tous les serveurs Exchange 2000 et Exchange 2003 doivent être supprimés de la forêt. Les boîtes aux lettres, les dossiers publics et tous les autres objets ou composants Exchange doivent être mis à niveau vers Exchange Server 2007 ou Exchange Server 2010. Vous ne pouvez pas mettre à niveau d’Exchange 2000 ou Exchange 2003 directement vers Exchange 2013.

La procédure à suivre pour installer Exchange 2013 dans votre organisation dépend de la version d'Exchange qui est actuellement installée dans votre forêt. Pour plus d'informations, consultez le tableau suivant :


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Si cette version est installée dans votre organisation</th>
<th>Suivez cette procédure pour effectuer la mise à niveau vers Exchange 2013</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Exchange 2000</p></td>
<td><ol>
<li><p>Installez Exchange 2007 dans votre organisation Exchange 2000.</p></li>
<li><p>Configurez la coexistence entre Exchange 2007 et Exchange 2000.</p></li>
<li><p>Migrez les boîtes aux lettres, les dossiers publics et les autres composants Exchange 2000 vers Exchange 2007.</p></li>
<li><p>Désactivez et supprimez tous les serveurs Exchange 2000.</p></li>
<li><p>Installez Exchange 2013 dans votre organisation Exchange 2007.</p></li>
<li><p>Configurez la coexistence entre Exchange 2013 et Exchange 2007.</p></li>
<li><p>Migrez les boîtes aux lettres, les dossiers publics et les autres composants Exchange 2007 vers Exchange 2013.</p></li>
<li><p>Désactivez et supprimez tous les serveurs Exchange 2007.</p></li>
</ol>
<p>Pour plus d'informations, consultez les rubriques <a href="https://go.microsoft.com/fwlink/p/?linkid=103281">Mise à niveau vers Exchange 2007</a> et <a href="upgrade-from-exchange-2007-to-exchange-2013-exchange-2013-help.md">Mise à niveau d'Exchange 2007 vers Exchange 2013</a>.</p></td>
</tr>
<tr class="even">
<td><p>Exchange 2003</p></td>
<td><ol>
<li><p>Installez Exchange 2010 dans votre organisation Exchange 2003.</p></li>
<li><p>Configurez la coexistence entre Exchange 2010 et Exchange 2003.</p></li>
<li><p>Migrez les boîtes aux lettres, les dossiers publics et les autres composants Exchange 2003 vers Exchange 2010.</p></li>
<li><p>Désactivez et supprimez tous les serveurs Exchange 2003.</p></li>
<li><p>Installez Exchange 2013 dans votre organisation Exchange 2010.</p></li>
<li><p>Configurez la coexistence entre Exchange 2013 et Exchange 2010.</p></li>
<li><p>Migrez les boîtes aux lettres, les dossiers publics et les autres composants Exchange 2010 vers Exchange 2013.</p></li>
<li><p>Désactivez et supprimez tous les serveurs Exchange 2010.</p></li>
</ol>
<p>Pour plus d'informations, consultez les rubriques <a href="https://go.microsoft.com/fwlink/p/?linkid=268414">Exchange 2003 - Planification d'une feuille de route pour la mise à niveau et la coexistence</a> et <a href="upgrade-from-exchange-2010-to-exchange-2013-exchange-2013-help.md">Mise à niveau d'Exchange 2010 vers Exchange 2013</a>.</p></td>
</tr>
</tbody>
</table>


Lors de la mise à niveau vers Exchange 2010 ou Exchange 2013, vous pouvez utiliser l'Assistant Déploiement d'Exchange pour vous aider à effectuer votre déploiement. Pour plus d'informations, accédez aux liens suivants :

  - [Assistant Déploiement d'Exchange 2010](https://go.microsoft.com/fwlink/p/?linkid=171086)

  - [Assistant Déploiement d'Exchange 2013](https://go.microsoft.com/fwlink/p/?linkid=277105)

Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), et [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

Avez-vous trouvé ce que vous cherchez ? Veuillez prendre une minute pour [nous envoyer votre avis à l'adresse](mailto:exsetuphelpfeedback@microsoft.com?subject=exchange%202013%20setup%20help%20feedback) au sujet des informations que vous souhaitiez y trouver.

