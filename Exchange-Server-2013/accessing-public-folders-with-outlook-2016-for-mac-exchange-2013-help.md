---
title: 'Accès aux dossiers publics avec Outlook 2016 pour Mac: Exchange 2013 Help'
TOCTitle: Accès aux dossiers publics avec Outlook 2016 pour Mac
ms:assetid: bc9b8226-bd8b-4edc-882b-4f19cfe118eb
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Mt788631(v=EXCHG.150)
ms:contentKeyID: 74115360
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Accès aux dossiers publics avec Outlook 2016 pour Mac

 

_**Sapplique à :**Exchange Online, Exchange Server 2013, Exchange Server 2016, Office 365_

_**Dernière rubrique modifiée :**2017-05-19_

**Résumé** : Topologies Exchange les plus récentes prises en charge permettant aux utilisateurs d’accéder aux dossiers publics avec Outlook 2016 pour Mac.

Avec les versions de la [mise à jour de 2016 d’avril](https://go.microsoft.com/fwlink/?linkid=829202) pour 2016 de Outlook pour les clients Mac, [mise à jour Cumulative 14 (CU14)](https://go.microsoft.com/fwlink/p/?linkid=849432) pour Exchange 2013 et [mise à jour Cumulative 2 (CU 2)](https://go.microsoft.com/fwlink/p/?linkid=849793) pour 2016 Exchange, les utilisateurs de 2016 d’Outlook pour Mac peuvent maintenant accéder aux dossiers publics dans plusieurs types de topologies de qu’il a pu avant.

## Limitations d'Outlook pour Mac

Toutes les versions d’Outlook pour Mac peuvent accéder aux dossiers publics Exchange, mais jusqu’à récemment, ces clients ne pouvaient pas accéder aux dossiers publics dans les scénarios de déploiement suivants :

  - **Coexistence avec les dossiers publics hérités.** Lorsque la boîte aux lettres d’un utilisateur est sur un serveur Exchange 2013 ou 2016 d’Exchange, l’utilisateur peut utiliser pas Outlook pour Mac pour accéder aux dossiers publics déployés sur les serveurs exécutant Exchange 2010 SP3 ou une version ultérieures. Autres clients peuvent accéder à ces dossiers publics hérités dans ce scénario.

  - **Topologies hybrides.** Les utilisateurs locaux avec une boîte aux lettres dans Exchange Online peuvent utilisez pas Outlook pour Mac pour accéder aux dossiers publics modernes de locaux. De même, les utilisateurs avec des boîtes aux lettres Exchange 2016 sur-locaux ou un 2013 Exchange n’a pas peuvent utiliser Outlook pour Mac pour accéder aux dossiers publics déployés dans Exchange en ligne.

## Outlook 2016 pour Mac

Avril 2016 la mise à jour pour 2016 d’Outlook pour Mac, ainsi que CU14 pour Exchange 2013 et CU2 pour Exchange 2016, les scénarios ci-dessus maintenant fonctionnera pour 2016 de Outlook pour les clients Mac.

Le tableau ci-dessous récapitule les topologies prises en charge pour les utilisateurs avec les clients Outlook 2016 pour Mac qui tentent d’accéder aux dossiers publics dans Exchange 2013, Exchange 2016 et Exchange Online.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Les scénarios indiqués dans le tableau suivant supposent que la mise à jour d’avril 2016 pour Outlook 2016 pour Mac a été appliquée à tous les clients.</td>
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
<th>Dossiers publics déployés sur...</th>
<th>Boîte aux lettres utilisateur sur Exchange 2010 SP3 ou version ultérieure</th>
<th>Boîte aux lettres utilisateur sur Exchange 2013 CU13 ou version ultérieure</th>
<th>Boîte aux lettres utilisateur sur Exchange 2016 CU2 ou version ultérieure</th>
<th>Boîte aux lettres utilisateur sur Office 365 / Exchange Online</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Exchange Server 2010 SP3 ou version ultérieure</p></td>
<td><p>Pris en charge</p></td>
<td><p>Pris en charge</p></td>
<td><p>Pris en charge</p></td>
<td><p>Non pris en charge</p></td>
</tr>
<tr class="even">
<td><p>Exchange Server 2013 CU13 ou version ultérieure</p></td>
<td><p>Non pris en charge</p></td>
<td><p>Pris en charge</p></td>
<td><p>Pris en charge</p></td>
<td><p>Pris en charge</p></td>
</tr>
<tr class="odd">
<td><p>Exchange Server 2016 CU2 ou version ultérieure</p></td>
<td><p>Non pris en charge</p></td>
<td><p>Pris en charge</p></td>
<td><p>Pris en charge</p></td>
<td><p>Pris en charge</p></td>
</tr>
<tr class="even">
<td><p>Office 365 / Exchange Online</p></td>
<td><p>Non pris en charge</p></td>
<td><p>Pris en charge</p></td>
<td><p>Pris en charge</p></td>
<td><p>Pris en charge</p></td>
</tr>
</tbody>
</table>


Les articles suivants expliquent comment déployer des dossiers publics dans votre organisation Exchange dans une topologie hybride ou une coexistence. Si vos clients Outlook 2016 pour Mac ont installé la mise à jour d’avril 2016, ils seront en mesure d’accéder aux dossiers publics dans les configurations détaillées dans les articles suivants :

  - [Configuration des dossiers publics hérités où les boîtes aux lettres des utilisateurs résident sur des serveurs Exchange 2013](configure-legacy-public-folders-where-user-mailboxes-are-on-exchange-2013-servers-exchange-2013-help.md)

  - [Configurer les dossiers publics Exchange 2013 pour un déploiement hybride](configure-exchange-2013-public-folders-for-a-hybrid-deployment-exchange-2013-help.md)

  - [Configurer les dossiers publics Exchange Online pour un déploiement hybride](configure-exchange-online-public-folders-for-a-hybrid-deployment-exchange-2013-help.md)

