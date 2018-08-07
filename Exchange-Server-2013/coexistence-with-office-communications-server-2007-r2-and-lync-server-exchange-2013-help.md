---
title: 'Coexistence avec Office Communications Server 2007 R2 et Lync Server'
TOCTitle: Coexistence avec Office Communications Server 2007 R2 et Lync Server
ms:assetid: f12d65c7-0b2c-46a1-a14a-802a76296fa1
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ851069(v=EXCHG.150)
ms:contentKeyID: 50555512
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Coexistence avec Office Communications Server 2007 R2 et Lync Server

 

_**Sapplique à :** Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2015-03-09_

Communications Server 2007 R2 et Lync Server offrent de nombreuses fonctions aux utilisateurs finaux, notamment la messagerie instantanée, la présence, la messagerie instantanée à plusieurs, et leurs fonctionnalités de messagerie vocale peuvent être intégrées à la messagerie unifiée d’Exchange. S’il s’agit de déploiements qui intègrent Lync Server 2010 ou 2013, les utilisateurs peuvent être activés pour Enterprise Voice, ce qui permet à ceux activés pour la messagerie vocale d’accéder à leur messagerie vocale via les composants de Lync Server.

Lorsque vous intégrez la messagerie unifiée à des versions antérieures d’Office Communications Server ou de Lync Server, vous n’avez pas accès à toutes les fonctions. Pour que des utilisateurs puissent profiter pleinement des nouvelles fonctions avancées destinées aux utilisateurs finaux comme les photos en mode haute résolution, le magasin de contacts unifié et l’intégration de l’archivage Lync, ils doivent posséder des comptes utilisateur sous Lync Server 2013 et Exchange Server 2013, et doivent utiliser la version la plus récente du logiciel client Lync 2013. Par exemple, le magasin de contacts unifié n’est pas accessible aux utilisateurs qui ont été activés pour Enterprise Voice sous Lync Server 2010. De même, les photos en haute résolution ne peuvent pas être affichées sous Lync 2010.

Lorsque vous intégrez la messagerie unifiée Exchange à Office Communications Server 2007 R2 ou Lync Server 2010, vous devrez peut-être installer des correctifs, des correctifs cumulatifs, des mises à jour cumulatives et des services packs supplémentaires sur les serveurs Office Communications Server 2007 R2 ou Lync 2010 qui ont été déployés dans votre organisation. Ce que vous avez à installer va dépendre la topologie de votre déploiement et des versions des produits que vous intégrez à la messagerie unifiée Exchange.

## Correctifs, correctifs cumulatifs, mises à jour cumulatives et services packs requis

Le tableau suivant dresse la liste des correctifs qui sont requis pour chaque version des produits destinés à être intégrés à la messagerie unifiée.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Office Communications Server 2007 R2</p></td>
<td><p>Office Communications Server 2007 R2 - Mise à jour cumulative 10 ou ultérieure.</p></td>
</tr>
<tr class="even">
<td><p>Lync Server 2010</p></td>
<td><p>Lync Server 2010 - Mise à jour cumulative 3 ou ultérieure.</p></td>
</tr>
<tr class="odd">
<td><p>Lync Server 2013</p></td>
<td><p>Aucune mise à jour n’est requise.</p></td>
</tr>
</tbody>
</table>

