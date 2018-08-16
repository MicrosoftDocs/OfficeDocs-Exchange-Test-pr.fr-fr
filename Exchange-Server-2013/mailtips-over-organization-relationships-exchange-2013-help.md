---
title: 'Infos-courrier sur les relations de l’organisation: Exchange 2013 Help'
TOCTitle: Infos-courrier sur les relations de l’organisation
ms:assetid: 1784256f-abe1-4503-b8c4-26d544b73452
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ670165(v=EXCHG.150)
ms:contentKeyID: 50477679
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Infos-courrier sur les relations de l’organisation

 

_**Sapplique à :** Exchange Online, Exchange Server 2013_

_**Dernière rubrique modifiée :** 2015-03-09_

Microsoft Exchange Server 2013 vous permet de configurer des relations organisationnelles avec Microsoft Exchange Online ou d’autres organisations Exchange. En établissant une relation organisationnelle, vous améliorez l’expérience de l’utilisateur qui traite avec l’autre organisation. Par exemple, vous pouvez partager des données de disponibilité, configurer des flux de messagerie sécurisés et activer le suivi des messages dans les deux organisations.

## Contrôle du niveau d’accès des infos-courrier

Vous pouvez limiter certains types d’infos-courrier. Vous pouvez autoriser le renvoi de toutes les infos-courrier ou uniquement d’un ensemble limité pour empêcher la notification d’échec de remise. Vous pouvez configurer cette option avec le paramètre *MailTipsAccessLevel* de la cmdlet **Set-OrganizationRelationship**. Le tableau suivant affiche les infos-courrier qui sont renvoyées dans la relation d’organisation.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Infos-courrier</th>
<th>Est-ce que l’info-courrier est disponible lorsque le niveau d’accès est défini sur Tous ?</th>
<th>Est-ce que l’info-courrier est disponible lorsque le niveau d’accès est défini sur Limité ?</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Large public</p></td>
<td><p>Oui</p></td>
<td><p>Non</p></td>
</tr>
<tr class="even">
<td><p>Réponses automatiques</p></td>
<td><p>Oui</p>
<p>Si le domaine distant du destinataire est spécifié comme étant interne, la réponse automatique interne s’affiche. Sinon, la réponse automatique externe s’affiche.</p></td>
<td><p>Oui</p>
<p>La réponse automatique externe s’affiche.</p></td>
</tr>
<tr class="odd">
<td><p>Destinataire modéré</p></td>
<td><p>Oui</p></td>
<td><p>Non</p></td>
</tr>
<tr class="even">
<td><p>Message dépassant la taille limite</p></td>
<td><p>Oui</p></td>
<td><p>Oui</p></td>
</tr>
<tr class="odd">
<td><p>Destinataire restreint</p></td>
<td><p>Oui</p></td>
<td><p>Oui</p></td>
</tr>
<tr class="even">
<td><p>Boîte aux lettres saturée</p></td>
<td><p>Oui</p></td>
<td><p>Non</p></td>
</tr>
<tr class="odd">
<td><p>Infos-courrier personnalisées</p></td>
<td><p>Oui</p></td>
<td><p>Non</p></td>
</tr>
<tr class="even">
<td><p>Destinataires externes</p></td>
<td><p>Oui</p>
<p>Si le domaine distant du destinataire est spécifié comme étant interne, cette info-courrier est supprimée. Sinon, l’info-courrier externe est renvoyée.</p></td>
<td><p>Oui</p>
<p>Si le domaine distant du destinataire est spécifié comme étant interne, cette info-courrier est supprimée. Sinon, l’info-courrier externe est renvoyée.</p></td>
</tr>
</tbody>
</table>


Pour obtenir la procédure détaillée de la configuration des niveaux d’accès des infos-courrier, voir [Gérer les infos-courrier pour les relations de l’organisation](manage-mailtips-for-organization-relationships-exchange-2013-help.md).

## Contrôle de l’étendue d’accès des infos-courrier

Lorsque vous activez les infos-courrier dans une relation d’organisation et que vous définissez le niveau d’accès sur `All`, les infos-courrier concernant les destinataires, la boîte aux lettres pleine, les réponses automatiques et les infos-courrier personnalisées sont renvoyées à tous les utilisateurs. Cependant, vous souhaiterez peut-être seulement autoriser ces infos-courrier pour un groupe d’utilisateurs spécifique. Par exemple, si vous définissez une relation d’organisation avec un partenaire, vous souhaiterez peut-être autoriser ces infos-courrier uniquement pour les utilisateurs travaillant avec ce partenaire.

Pour ce faire, vous devez d’abord créer un groupe et ajouter tous les utilisateurs pour lesquels vous souhaitez partager les infos-courrier concernant les destinataires de ce groupe. Vous pouvez ensuite spécifier ce groupe sur la relation d’organisation.

Après avoir mis en œuvre cette restriction, vos serveurs d’accès au client vérifieront d’abord si le destinataire dont ils ont reçu une requête d’info-courrier fait partie de ce groupe. Si le destinataire est membre de ce groupe, les serveurs d’accès au client transféreront par proxy toutes les infos-courrier, y compris les infos-courrier propres au destinataire. Dans le cas contraire, ils n’incluront pas les infos-courrier propres au destinataire dans leur réponse.

Pour obtenir la procédure détaillée de la configuration des niveaux d’accès des infos-courrier, voir [Gérer les infos-courrier pour les relations de l’organisation](manage-mailtips-for-organization-relationships-exchange-2013-help.md).

