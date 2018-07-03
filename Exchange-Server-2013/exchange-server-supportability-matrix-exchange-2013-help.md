---
title: 'Exchange Server Supportability Matrix: Exchange 2013 Help'
TOCTitle: Exchange Server Supportability Matrix
ms:assetid: dbac2d40-da8b-469f-a265-1d1f948fe446
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Ff728623(v=EXCHG.150)
ms:contentKeyID: 54652780
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange Server Supportability Matrix

 

_**Sapplique à :** Exchange Server 2007, Exchange Server 2010, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2018-03-20_

La matrice de support d’Exchange Server offre aux administrateurs Microsoft Exchange une référence centrale permettant de localiser aisément les informations sur le niveau de support disponible pour les configurations ou les composants nécessaires, pour toutes les versions d’Microsoft Exchange prises en charge.

## Modèle de version

Le tableau suivant identifie le modèle de version pour chaque version prise en charge d’Exchange. Le modèle de version est indiqué par un X.

Pour les versions d’Exchange antérieures à Exchange 2013, chaque package de correctif de mise à jour est cumulatif par rapport au produit entier. Par conséquent, si vous appliquez un package de correctif cumulatif à Exchange Server 2010, vous appliquez tous les correctifs contenus dans ce package de correctif cumulatif. Il inclut également tous les correctifs contenus dans les packages de correctif cumulatif antérieurs. Lorsqu’une mise à jour ou un correctif est créé pour les versions d’Exchange, un ou plusieurs des fichiers binaires inclus dans la mise à jour ou dans le correctif sont cumulatifs. Autrement dit, ils sont cumulatifs par rapport au contenu des fichiers. Ils ne sont cependant pas cumulatifs par rapport au produit Exchange entier. Pour plus d’informations, consultez la page relative à la [maintenance d’Exchange 2010](https://go.microsoft.com/fwlink/p/?linkid=298627).

Dans Exchange 2013, nous avons modifié notre façon de fournir des correctifs et des Service Packs. Contrairement aux versions précédentes d’Exchange qui utilisaient un modèle de correctif cumulatif par ordre de priorité et de mises à jour cumulatives, Exchange 2013 et versions ultérieures adopte désormais un modèle de publication planifié. Dans ce modèle, des mises à jour cumulatives sont publiées tous les 3 mois. Une mise à jour cumulative publiée pour Exchange 2013 et versions ultérieures constitue une actualisation complète d’Exchange et est semblable à une mise à niveau de produit ou à la publication d’un Service Pack. Pour plus d’informations sur le nouveau modèle de service, consultez la rubrique [Mises à jour pour Exchange 2013](updates-for-exchange-2013-exchange-2013-help.md).


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Modèle de publication de service</th>
<th>Exchange 2016</th>
<th>Exchange 2013</th>
<th>Exchange 2010</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Mises à jour cumulatives</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p> </p></td>
</tr>
<tr class="even">
<td><p>Correctifs cumulatifs</p></td>
<td><p></p></td>
<td><p> </p></td>
<td><p>X</p></td>
</tr>
<tr class="odd">
<td><p>Correctifs de sécurité livrés séparément</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p> </p></td>
</tr>
</tbody>
</table>


## Politique de support

Pour plus d’informations sur la politique de prise en charge pour une version spécifique d’Exchange ou des systèmes d’exploitation client ou serveur MicrosoftWindows, consultez la page [Politique de support Microsoft](https://go.microsoft.com/fwlink/p/?linkid=55839). Pour plus d’informations sur la politique de support Microsoft, consultez la page [Forum aux questions sur la politique de support Microsoft](https://go.microsoft.com/fwlink/?linkid=158902).

## Fin de vie d’Exchange Server 2007

L’assistance pour Exchange 2007 a pris fin le 11 avril 2017, conformément à la [politique concernant le cycle de vie de Microsoft](https://go.microsoft.com/fwlink/p/?linkid=833210). Pour rappel, passée cette date, aucune nouvelle mise à jour de sécurité ou autre ne sera publiée, de même qu’aucune mise à jour du contenu technique en ligne, et les options de support gratuit ou payant ne seront plus disponibles. Par ailleurs, en raison de l’adoption accélérée d’Office 365 et de l’utilisation de plus en plus importante du cloud, les options de support personnalisé pour les produits Office ne seront plus disponibles. Cela inclut Exchange Server ainsi que les suites Office, SharePoint Server, Office Communications Server, Lync Server, Skype Entreprise Server, Visio et Project Server. L’assistance pour Exchange 2007 étant terminée, nous encourageons les utilisateurs à effectuer leur migration et à mettre à niveau leurs offres. Nous recommandons aux clients de profiter des avantages de déploiement fournis par Microsoft et ses partenaires certifiés, y compris les services [Microsoft FastTrack](https://go.microsoft.com/fwlink/p/?linkid=238431) pour les migrations dans le cloud et les [services de planification et de déploiement Software Assurance](https://go.microsoft.com/fwlink/p/?linkid=833211) pour les mises à niveau en local.

## Plateformes de système d’exploitation prises en charge

Le tableau suivant permet d’identifier les plateformes de système d’exploitation sur lesquelles les versions d’Exchange peuvent être exécutées. Les plateformes prises en charge sont indiquées par un X.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159813.important(EXCHG.150).gif" title="Important" alt="Important" />Important :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Les versions de Windows Server et du client Windows qui ne sont pas répertoriées dans le tableau ci-dessous ne sont pas prises en charge pour être utilisées avec une version d’Exchange.</td>
</tr>
</tbody>
</table>



<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>Plateforme de système d’exploitation</th>
<th>Exchange 2016 CU3 et version ultérieure</th>
<th>Exchange 2016 CU2 et versions antérieures</th>
<th>Exchange 2013 SP1 et versions ultérieures</th>
<th>Exchange 2010 SP3</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Windows Vista SP2</p></td>
<td><p></p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p>X1</p></td>
</tr>
<tr class="even">
<td><p>Windows Server 2008 SP2</p></td>
<td><p></p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p>X</p></td>
</tr>
<tr class="odd">
<td><p>Windows Server 2008 R2 SP1</p></td>
<td><p></p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p>Windows 7 SP1</p></td>
<td><p></p></td>
<td><p></p></td>
<td><p>X1</p></td>
<td><p>X1</p></td>
</tr>
<tr class="odd">
<td><p>Windows 8</p></td>
<td><p></p></td>
<td><p></p></td>
<td><p>X1</p></td>
<td><p>X1</p></td>
</tr>
<tr class="even">
<td><p>Windows 8.1</p></td>
<td><p>X1</p></td>
<td><p>X1</p></td>
<td><p>X1</p></td>
<td><p> </p></td>
</tr>
<tr class="odd">
<td><p>Windows 10</p></td>
<td><p>X1</p></td>
<td><p>X1</p></td>
<td><p></p></td>
<td><p> </p></td>
</tr>
<tr class="even">
<td><p>Windows Server 2012</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="odd">
<td><p>Windows Server 2012 R2</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p> </p></td>
</tr>
<tr class="even">
<td><p>Windows Server 2016</p></td>
<td><p>X</p></td>
<td><p></p></td>
<td><p></p></td>
<td><p> </p></td>
</tr>
</tbody>
</table>


1Uniquement pour les outils de gestion Exchange

## Environnements Active Directory pris en charge

Le tableau suivant permet d’identifier les environnements Active Directory avec lesquels chaque version d’Exchange peut communiquer. Les environnements pris en charge sont indiqués par un X. Un serveur Active Directory fait référence à la fois aux serveurs de catalogue global accessibles en écriture et aux contrôleurs de domaine accessibles en écriture. Les serveurs de catalogue global en lecture seule et les contrôleurs de domaine en lecture seule ne sont pas pris en charge.


<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>Environnement de système d’exploitation</th>
<th>Exchange 2016 CU3 et version ultérieure</th>
<th>Exchange 2016 CU2 et versions antérieures</th>
<th>Exchange 2013 SP1 et versions ultérieures</th>
<th>Exchange 2010 SP3 RU5 ou version ultérieure</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Serveurs Windows Server 2003 SP2 Active Directory</p></td>
<td><p></p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p>Serveurs Windows Server 2008 SP2 Active Directory</p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="odd">
<td><p>Serveurs Windows Server 2008 R2 SP1 Active Directory</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p>Serveurs Windows Server 2012 Active Directory</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="odd">
<td><p>Serveurs Windows Server 2012 R2 Active Directory</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p>Serveurs Windows Server 2016 Active Directory</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>



<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>Niveau fonctionnel de la forêt</th>
<th>Exchange 2016 CU3 et version ultérieure</th>
<th>Exchange 2016 CU2 et versions antérieures</th>
<th>Exchange 2013 SP1 et versions ultérieures</th>
<th>Exchange 2010 SP3 RU5 ou version ultérieure</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Niveau fonctionnel de la forêt Windows Server 2003</p></td>
<td><p></p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p>Niveau fonctionnel de la forêt Windows Server 2008</p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="odd">
<td><p>Niveau fonctionnel de la forêt Windows Server 2008 R2 SP1</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p>Niveau fonctionnel de la forêt Windows Server 2012</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="odd">
<td><p>Niveau fonctionnel de la forêt Windows Server 2012 R2</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p>Niveau fonctionnel de la forêt Windows Server 2016</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


## Navigateurs Web compatibles avec la version Premium d’Outlook Web App ou d’Outlook sur le web

Le tableau suivant identifie les navigateurs web pris en charge pour être utilisés avec la version Premium d’Outlook Web App ou d’Outlook sur le web. Les navigateurs pris en charge sont indiqués par un X.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Navigateur</th>
<th>Exchange 2016</th>
<th>Exchange 2013 SP1 et versions ultérieures</th>
<th>Exchange 2010 SP3</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Microsoft Edge</p></td>
<td><p>Version actuelle de Microsoft Edge</p></td>
<td><p>N/D</p></td>
<td><p>N/D</p></td>
</tr>
<tr class="even">
<td><p>Internet Explorer</p></td>
<td><p>Version actuelle ou immédiatement antérieure d’Internet Explorer</p></td>
<td><p>N/D</p></td>
<td><p>N/D</p></td>
</tr>
<tr class="odd">
<td><p>Internet Explorer 11</p></td>
<td><p> </p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p>Internet Explorer 10</p></td>
<td><p> </p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="odd">
<td><p>Internet Explorer 9</p></td>
<td><p> </p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p>Internet Explorer 8</p></td>
<td><p> </p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="odd">
<td><p>Internet Explorer 7</p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p>Firefox</p></td>
<td><p>Version actuelle ou immédiatement antérieure de Firefox</p></td>
<td><p>N/D</p></td>
<td><p>N/D</p></td>
</tr>
<tr class="odd">
<td><p>Firefox 3.0.1 ou version ultérieure</p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p>Firefox 12 ou version ultérieure</p></td>
<td><p> </p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="odd">
<td><p>Safari</p></td>
<td><p>Version actuelle de Safari</p></td>
<td><p>N/D</p></td>
<td><p>N/D</p></td>
</tr>
<tr class="even">
<td><p>Safari 3.1 ou version ultérieure</p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p>X</p></td>
</tr>
<tr class="odd">
<td><p>Safari 5.0 ou version ultérieure</p></td>
<td><p> </p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p>Chrome</p></td>
<td><p>Version actuelle de Chrome</p></td>
<td><p>N/D</p></td>
<td><p>N/D</p></td>
</tr>
<tr class="odd">
<td><p>Chrome 3.0.195 ou version ultérieure</p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p>Chrome 18 ou version ultérieure</p></td>
<td><p> </p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
</tbody>
</table>


## Navigateurs web compatibles avec la version de base d’Outlook Web App ou d’Outlook sur le web

Le tableau suivant identifie les navigateurs web pris en charge pour être utilisés avec la version allégée (basique) d’Outlook Web App ou d’Outlook sur le web. Les navigateurs pris en charge sont indiqués par un X.

> [!NOTE]
> Outlook Web App Basic (Outlook Web App Light) est pris en charge par les navigateurs mobiles. Toutefois, si des problèmes de rendu ou d'authentification surviennent dans un navigateur mobile, vérifiez si le problème se reproduit dans Outlook Web App Light dans le client complet d'un navigateur pris en charge. Par exemple, essayez d'utiliser Outlook Web App Light dans Safari, Chrome ou Internet Explorer. Si le problème ne se reproduit pas dans le client complet, nous vous conseillons de contacter le fabricant de l'appareil mobile pour obtenir de l'aide. Dans ces cas, nous collaborons avec le fournisseur, selon le cas.



<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Navigateur</th>
<th>Exchange 2016</th>
<th>Exchange 2013</th>
<th>Exchange 2010 SP3</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Microsoft Edge</p></td>
<td><p>Version actuelle de Microsoft Edge</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Internet Explorer</p></td>
<td><p>Version actuelle ou immédiatement antérieure d’Internet Explorer</p></td>
<td><p>N/D</p></td>
<td><p>N/D</p></td>
</tr>
<tr class="odd">
<td><p>Internet Explorer 11</p></td>
<td><p> </p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p>Internet Explorer 10</p></td>
<td><p> </p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="odd">
<td><p>Internet Explorer 9</p></td>
<td><p> </p></td>
<td><p>X</p></td>
<td><p>X<span></span></p></td>
</tr>
<tr class="even">
<td><p>Internet Explorer 8</p></td>
<td><p> </p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="odd">
<td><p>Internet Explorer 7</p></td>
<td><p> </p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p>Safari</p></td>
<td><p>Version actuelle de Safari</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="odd">
<td><p>Firefox</p></td>
<td><p>Version actuelle ou immédiatement antérieure de Firefox</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p>Chrome</p></td>
<td><p>Version actuelle de Chrome</p></td>
<td><p>N/D</p></td>
<td><p>N/D</p></td>
</tr>
<tr class="odd">
<td><p>Opera</p></td>
<td><p> </p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
</tbody>
</table>


## Navigateurs web pris en charge pour l’utilisation de S/MIME avec Outlook Web App ou Outlook sur le web

Le tableau suivant identifie les navigateurs web pris en charge pour l’utilisation de S/MIME avec Outlook Web App ou Outlook sur le web. Les navigateurs pris en charge sont indiqués par un X.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Navigateur</th>
<th>Exchange 2016</th>
<th>Exchange 2013 SP1 et versions ultérieures</th>
<th>Exchange 2010 SP3</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Microsoft Edge</p></td>
<td><p>Version actuelle de Microsoft Edge</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Internet Explorer</p></td>
<td><p>Version actuelle ou immédiatement antérieure d’Internet Explorer</p></td>
<td><p>N/D</p></td>
<td><p>N/D</p></td>
</tr>
<tr class="odd">
<td><p>Internet Explorer 11</p></td>
<td></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p>Internet Explorer 10</p></td>
<td></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="odd">
<td><p>Internet Explorer 9</p></td>
<td></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p>Internet Explorer 8</p></td>
<td></td>
<td><p> </p></td>
<td><p>X</p></td>
</tr>
<tr class="odd">
<td><p>Internet Explorer 7</p></td>
<td></td>
<td><p> </p></td>
<td><p>X</p></td>
</tr>
</tbody>
</table>


## Clients

Le tableau suivant permet d’identifier les clients de messagerie compatibles avec chaque version d’Exchange. Les clients pris en charge sont indiqués par un X.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Client</th>
<th>Exchange 2016</th>
<th>Exchange 2013 SP1 et versions ultérieures</th>
<th>Exchange 2010 SP3</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Outlook 2007</p></td>
<td><p></p></td>
<td><p>X1</p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p>Outlook 2010</p></td>
<td><p>X4</p></td>
<td><p>X2</p></td>
<td><p>X</p></td>
</tr>
<tr class="odd">
<td><p>Outlook 2013</p></td>
<td><p>X4</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p>Outlook 2016</p></td>
<td><p>X4</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="odd">
<td><p>Outlook pour Mac pour Office 365</p></td>
<td><p>X4</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p>Windows Phone 7</p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="odd">
<td><p>Windows Phone 7,5</p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p>Windows Phone 8</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="odd">
<td><p>Windows Phone 8.1</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p>Windows Mobile 10</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="odd">
<td><p>Entourage 2008 (EWS)</p></td>
<td><p>X3</p></td>
<td><p>X3</p></td>
<td><p>X3</p></td>
</tr>
</tbody>
</table>


1Requiert Outlook 2007 Service Pack 3 et la dernière mise à jour publique.

2Requiert Outlook 2010 Service Pack 1 et la dernière mise à jour publique.

3EWS uniquement. Il n’y a aucune prise en charge DAV pour Exchange 2010.

4Pris en charge avec le dernier Service Pack Office et les dernières mises à jour publiques.

## Outils

Le tableau suivant permet d’identifier la version d’Microsoft Exchange pouvant être utilisée avec l’outil de réplication inter-organisationnelle Microsoft Exchange (Exscfg.exe ; Exssrv.exe). L’outil permet de répliquer des informations de dossiers publics (y compris les informations de disponibilité) entre des organisations Exchange. Pour plus d’informations, consultez la page sur la [réplication inter-organisationnelle Microsoft Exchange Server](https://go.microsoft.com/fwlink/?linkid=22455). Les versions prises en charge sont indiquées par une croix (X).


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Outil</th>
<th>Exchange 2016</th>
<th>Exchange 2013 SP1 et versions ultérieures</th>
<th>Exchange 2010 SP3</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Outil de réplication inter-organisationnelle</p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p>X</p></td>
</tr>
</tbody>
</table>


## Microsoft .NET Framework

Le tableau suivant permet d’identifier la version de Microsoft.NET Framework compatible avec chaque version d’Exchange. Les versions prises en charge sont indiquées par un X.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159813.important(EXCHG.150).gif" title="Important" alt="Important" />Important :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><strong>Les versions de .NET Framework qui ne sont pas répertoriées dans le tableau ci-dessous ne sont prises en charge par aucune version d’Exchange.</strong> Cela inclut les versions mineures et de niveau de correctif logiciel de .NET Framework.</td>
</tr>
</tbody>
</table>


> [!NOTE]
> Quand vous mettez à niveau Exchange à partir d’une mise à jour cumulative (CU) non prise en charge vers la CU actuelle et qu’aucune CU intermédiaire n’est disponible, mettez d’abord à niveau Exchange vers la dernière version de .NET prise en charge par Exchange, puis mettez-le immédiatement à niveau vers la CU actuelle. Malgré tout, mettez régulièrement à jour vos serveurs Exchange en installant les mises à jour cumulatives prises en charge les plus récentes.
> Microsoft ne donne aucune garantie de la réussite de la mise à niveau en utilisant cette méthode. En cas de problème, contactez les services de support technique Microsoft.



<table style="width:100%;">
<colgroup>
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
</colgroup>
<thead>
<tr class="header">
<th>.NET Framework</th>
<th>CU8 Exchange 2016</th>
<th>CU5 - CU7 Exchange 2016</th>
<th>CU19 Exchange 2013</th>
<th>CU16 - CU18 Exchange 2013</th>
<th>Exchange 2010 SP3</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>.NET Framework 3.5</p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p>X1</p></td>
</tr>
<tr class="even">
<td><p>.NET Framework 3.5 SP1</p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p>X</p></td>
</tr>
<tr class="odd">
<td><p>.NET Framework 4.0</p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p>X1,2</p></td>
</tr>
<tr class="even">
<td><p>.NET Framework 4.5</p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p>X1,2 </p></td>
</tr>
<tr class="odd">
<td><p>.NET Framework 4.6.2</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p> </p></td>
</tr>
<tr class="even">
<td><p>.NET Framework 4.7.1</p></td>
<td><p>X</p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


1 Si vous utilisez Windows Server 2012, .NET Framework 3.5 doit être installé pour pouvoir utiliser Exchange 2010 SP3.

2Exchange 2010 utilise uniquement les bibliothèques .NET .NET Framework 3.5 et .NET .NET Framework 3.5 SP1. Il n’utilise pas les bibliothèques .NET .NET Framework 4.5 si elles sont installées sur l’ordinateur. Nous prenons en charge l’installation de toutes les versions majeures ou mineures de .NET .NET Framework 4.5 (par exemple, .NET .NET Framework 4.5.1, .NET .NET Framework 4.5.2, etc.) pour peu que .NET .NET Framework 3.5 ou .NET .NET Framework 3.5 SP1 soit également installé sur l’ordinateur.

## Windows Management Framework

Le tableau suivant permet d’identifier la version de Windows Management Framework, qui contient l’interface de ligne de commande Windows PowerShell compatible avec chaque version d’Exchange. Les versions prises en charge sont indiquées par un X.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Windows PowerShell</th>
<th>Exchange 2016</th>
<th>Exchange 2013</th>
<th>Exchange 2010</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Windows PowerShell 2.0</p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p>Windows Management Framework</p></td>
<td><p>Version de Windows Management Framework intégrée à la version de Windows Server sur laquelle vous installez Exchange.</p></td>
<td><p>Version de Windows Management Framework intégrée à la version de Windows Server sur laquelle vous installez Exchange.</p></td>
<td><p>Version de Windows Management Framework intégrée à la version de Windows Server sur laquelle vous installez Exchange.1</p></td>
</tr>
</tbody>
</table>


1Windows Management Framework 3.0 et Windows Management Framework 4.0 peuvent être utilisés pour effectuer des tâches de gestion relatives au système d’exploitation sur des ordinateurs exécutant Exchange 2010 SP3 RU5 ou version ultérieure. Toutefois, les cmdlets Exchange 2010 et les scripts Exchange 2010 requièrent Windows PowerShell 2.0. L’utilisation des cmdlets et des scripts Exchange 2010 avec Windows Management Framework 3.0 ou Windows Management Framework 4.0 n’est pas prise en charge.

## Microsoft Management Console

Le tableau suivant permet d'identifier la version de Microsoft Management Console (MMC) compatible avec chaque version d'Exchange. Les versions prises en charge sont indiquées par un X.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>MMC</th>
<th>Exchange 2016</th>
<th>Exchange 2013 SP1 ou version ultérieure</th>
<th>Exchange 2010 SP3</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>MMC 3.0</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
</tbody>
</table>


## Windows Installer

Le tableau suivant permet d’identifier la version de Windows Installer compatible avec chaque version d’Exchange. Les versions prises en charge sont indiquées par un X.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Windows Installer</th>
<th>Exchange 2016</th>
<th>Exchange 2013 SP1 et versions ultérieures</th>
<th>Exchange 2010 SP3</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Windows Installer 4.5</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p>Windows Installer 5.0</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p> </p></td>
</tr>
</tbody>
</table>

