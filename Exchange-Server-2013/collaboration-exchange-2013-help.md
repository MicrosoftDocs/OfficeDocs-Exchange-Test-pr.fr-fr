---
title: 'Collaboration: Exchange 2013 Help'
TOCTitle: Collaboration
ms:assetid: f45c1be1-2a66-4610-a28d-4adc6d212769
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ218725(v=EXCHG.150)
ms:contentKeyID: 50479564
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Collaboration

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2015-03-09_

Exchange 2013 offre le large éventail suivant de fonctionnalités qui permet aux utilisateurs finaux de participer facilement à la messagerie électronique :

  - Boîtes aux lettres de site

  - Dossiers publics

  - Boîtes aux lettres partagées

  - Groupes de distribution

Chacune de ces fonctionnalités présente une expérience utilisateur et un ensemble de fonctions différentes et il convient de l’utilisateur selon les besoins spécifiques de l’utilisateur et ce que votre organisation peut proposer. Par exemple, les boîtes aux lettres de site offrent des fonctionnalités très intéressantes en termes de collaboration dans la documentation. Notez que les boîtes aux lettres de site s’appuient sur SharePoint Server 2013, et donc si vous ne prévoyez pas de déploiement SharePoint, vous devez utiliser des dossiers publics pour partager des documents.

Cette rubrique compare ces fonctionnalités de collaboration et vous permet ainsi de déterminer quelles fonctionnalités vous allez offrir à vos utilisateurs.

## Boîtes aux lettres de site

Une boîte aux lettres de site est une fonctionnalité composée d’une appartenance au site SharePoint 2013 (propriétaire et membres), d’un stockage partagé via une boîte aux lettres Exchange 2013 pour les messages électroniques et d’un site SharePoint 2013 destinée au stockage et au partage. Une boîte aux lettres de site consiste essentiellement à rassembler la messagerie électronique Exchange et les documents SharePoint. Pour les utilisateurs, une boîte aux lettres de site sert de classeur central pour un projet ; il s’agit d’un emplacement permettant de classer des courriers électroniques et des documents de projets uniquement accessibles et modifiables par les membres du site. En outre, les boîtes aux lettres de site ont une durée de vie déterminée et sont optimisées pour être utilisées avec des projets ayant une date de début et de fin définies. Pour mettre pleinement en œuvre les boîtes aux lettres de site, les utilisateurs finaux doivent utiliser Outlook 2013.

Pour plus d’informations, voir [Boîtes aux lettres de site](site-mailboxes-exchange-2013-help.md).

## Dossiers publics

Les dossiers publics sont conçus pour assurer un accès partagé et offrir une manière simple et efficace de collecter, d’organiser et de partager des informations avec d’autres personnes dans votre groupe de travail ou votre organisation.

Les dossiers publics organisent un contenu sous la forme d’une hiérarchique profonde, facile à parcourir. Les utilisateurs parcourent les branches de cette hiérarchie pour découvrir le contenu intéressant et pertinent pour eux-mêmes. Les utilisateurs voient toujours la hiérarchie complète dans l'affichage des dossiers Outlook. Les dossiers publics constituent une excellente technique d'archivage des groupes de distribution. Il est possible d'envoyer par messagerie électronique et d'ajouter un dossier public en tant que membre du groupe de distribution. Un message électronique envoyé au groupe de distribution est automatiquement ajouté au dossier public pour référence ultérieure. Les dossiers publics autorisent également un partage simple de documents et ne nécessitent pas l’installation de SharePoint Server 2013 dans votre organisation. Finalement, les utilisateurs finaux peuvent utiliser des dossiers publics avec les clients Outlook pris en charge suivants : Outlook 2007, Outlook 2010 et Outlook 2013.

Pour plus d’informations, voir [Dossiers publics](public-folders-exchange-2013-help.md).

## Boîtes aux lettres partagées

Une boîte aux lettres partagée est une boîte aux lettres accessible à plusieurs utilisateurs désignés pour lire et envoyer des messages électroniques et pour partager un calendrier commun. Elles peuvent fournir une adresse de messagerie générale (ex. info@contoso.com ou ventes@contoso.com) que les clients peuvent utiliser pour obtenir des renseignements sur votre société. Si l'autorisation Envoyer en tant que est affectée à la boîte aux lettres partagée lorsqu'un utilisateur délégué répond à un message électronique, elle peut apparaître comme si la boîte aux lettres (ex. ventes@contoso.com) répondait et non l'utilisateur réel.

Pour plus d’informations, voir [Boîtes aux lettres partagées](shared-mailboxes-exchange-2013-help.md).

## Groupes

Les groupes (également appelés « groupe de distribution ») rassemblent deux ou davantage de destinataires qui apparaissent dans le carnet d’adresses partagé. Lorsqu’un message électronique est envoyé à un groupe, tous ses membres le reçoivent. Les groupes de distribution peuvent s’organiser autour d’un sujet de discussion particulier (comme les « amis des chiens ») ou autour d’utilisateurs qui partagent une structure de travail commune nécessitant de fréquentes communications.

Pour plus d’informations, voir [Recipients](recipients-exchange-2013-help.md).

## Laquelle utiliser ?

Le tableau suivant donne un aperçu de chaque fonctionnalité de collaboration afin de vous aider à décider laquelle utiliser.


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
<th></th>
<th>Boîtes aux lettres de site</th>
<th>Dossiers publics</th>
<th>Boîtes aux lettres partagées</th>
<th>Groupes</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Type de groupe</strong></p></td>
<td><p>Les utilisateurs qui travaillent ensemble, sont en équipe sur un projet donné avec des dates de début et de fin arrêtées.</p></td>
<td><p>Munie des autorisations appropriées, chaque personne de votre organisation peut accéder et consulter des dossiers publics. Les dossiers publics sont parfaits pour maintenir un historique ou des conversations de groupes de distribution.</p></td>
<td><p>Délègue le travail pour le compte d’une identité virtuelle et peuvent répondre aux messages électroniques partagés par l’identité de la boîte aux lettres partagée. Exemple : support@tailspintoys.com</p></td>
<td><p>Utilisateurs devant envoyer un message électronique à un groupe de destinataires partageant des intérêts ou des caractéristiques communs.</p></td>
</tr>
<tr class="even">
<td><p><strong>Taille idéale d'un groupe</strong></p></td>
<td><p>Petit</p></td>
<td><p>Grande</p></td>
<td><p>Petit</p></td>
<td><p>Grande</p></td>
</tr>
<tr class="odd">
<td><p><strong>Accès</strong></p></td>
<td><p>Membres et propriétaires de boîte aux lettres de site.</p></td>
<td><p>Accessible à tous dans votre organisation.</p></td>
<td><p>Les utilisateurs peuvent avoir les autorisations Accès total et/ou Envoyer en tant que. S'ils ont l'autorisation Accès total, les utilisateurs doivent également ajouter la boîte aux lettres partagée à leur profil Outlook pour y accéder.</p></td>
<td><p>Pour les groupes de distribution, il faut ajouter les membres manuellement. Pour les groupes de distribution dynamiques, les membres sont ajoutés d'après des critères de filtrage.</p></td>
</tr>
<tr class="even">
<td><p><strong>Calendrier partagé ?</strong></p></td>
<td><p>Non</p></td>
<td><p>Oui</p></td>
<td><p>Oui</p></td>
<td><p>Non</p></td>
</tr>
<tr class="odd">
<td><p><strong>Un message électronique arrive-t-il dans la boîte de réception personnelle de l’utilisateur ?</strong></p></td>
<td><p>Non, les messages électroniques arrivent dans la boîte aux lettres de site.</p></td>
<td><p>Non, le message électronique arrive dans le dossier public.</p></td>
<td><p>Non, le message électronique arrive dans la boîte de réception de la boîte aux lettres partagée.</p></td>
<td><p>Oui. Le message électronique arrive dans la boîte de réception d’un membre du groupe de distribution.</p></td>
</tr>
<tr class="even">
<td><p><strong>Clients pris en charge</strong></p></td>
<td><ul>
<li><p>Outlook 2013</p></li>
<li><p>SharePoint 2013</p></li>
</ul></td>
<td><ul>
<li><p>Outlook 2013</p></li>
<li><p>Outlook 2010</p></li>
<li><p>Outlook 2007</p></li>
</ul></td>
<td><ul>
<li><p>Outlook 2013</p></li>
<li><p>Outlook Web App</p></li>
<li><p>Outlook 2010</p></li>
<li><p>Outlook 2007</p></li>
</ul></td>
<td><ul>
<li><p>Outlook 2013</p></li>
<li><p>Outlook Web App</p></li>
<li><p>Outlook 2010</p></li>
<li><p>Outlook 2007</p></li>
</ul></td>
</tr>
</tbody>
</table>

