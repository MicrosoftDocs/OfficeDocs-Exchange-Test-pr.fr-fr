---
title: 'Relations des organisations: Exchange 2013 Help'
TOCTitle: Relations des organisations
ms:assetid: 4c48db61-3370-462b-a3f8-2a6311c6e4ee
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ657445(v=EXCHG.150)
ms:contentKeyID: 50478133
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Relations des organisations

 

_**Sapplique à :**Exchange Server 2013_

_**Dernière rubrique modifiée :**2014-02-20_

Configurez une relation organisationnelle pour partager des informations de calendrier avec un partenaire commercial externe. Les administrateurs Exchange peuvent configurer une relation organisationnelle avec une organisation Office 365 ou avec une autre organisation Exchange sur site. Si vous souhaitez partager des calendriers avec une autre organisation Exchange sur site, les deux administrateurs Exchange sur site doivent configurer une relation d’authentification avec le nuage (également appelée « fédération ») et satisfaire à la configuration logicielle requise minimale.

Une relation organisationnelle est une relation un-à-un entre des entreprises pour permettre aux utilisateurs de chaque organisation d’afficher les informations de disponibilité de calendrier. Lors de la configuration de la relation organisationnelle, vous configurez votre côté de la relation et indiquez le niveau d’information visible par les utilisateurs de l’organisation externe. L’organisation externe peut configurer des paramètres identiques ou différents de son côté. Par exemple, si Contoso crée une relation organisationnelle avec Tailspin Toys, les utilisateurs de Tailspin Toys pourront planifier des réunions avec des utilisateurs de Contoso en ajoutant les adresses de messagerie de ces derniers dans l’invitation à la réunion. L’utilisateur Tailspin Toys pourra afficher la disponibilité de l’utilisateur Contoso invité. Toutefois, avant que Contoso puisse également voir la disponibilité des utilisateurs chez Tailspin Toys, l’administrateur de ces derniers doit configurer une relation organisationnelle avec Contoso.

Il existe trois niveaux d’accès que vous pouvez indiquer :

  - Pas d’accès

  - Accès aux horaires de disponibilité uniquement

  - Accès à la disponibilité, y compris aux horaires, objets et emplacements

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Si les utilisateurs ne veulent pas partager leurs informations de disponibilité avec d’autres utilisateurs, ils peuvent modifier l’entrée d’autorisation par défaut dans Outlook. Pour ce faire, les utilisateurs doivent accéder aux <strong>Propriétés du calendrier</strong> &gt; onglet <strong>Autorisations</strong>, sélectionner l’autorisation <strong>Par défaut</strong>, puis choisir <strong>Aucun</strong> dans la liste <strong>Niveau d’autorisation</strong>. Leurs informations de disponibilité ne seront pas visibles par les utilisateurs internes ou externes, même si une relation organisationnelle existe. Les autorisations définies par l’utilisateur s’appliqueront.</td>
</tr>
</tbody>
</table>


Les rubriques suivantes vous permettront de configurer et de gérer les relations organisationnelles dans le cadre du partage pour votre organisation :

[Créer une relation d’organisation](create-an-organization-relationship-exchange-2013-help.md)

[Modifier une relation organisationnelle](modify-an-organization-relationship-exchange-2013-help.md)

[Suppression d'une relation d'organisation](remove-an-organization-relationship-exchange-2013-help.md)

Vous recherchez des informations complémentaires sur le partage fédéré ? Voir [Partage](sharing-exchange-2013-help.md).

