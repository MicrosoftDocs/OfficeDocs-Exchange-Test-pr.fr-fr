---
title: 'Autoriser des appels utilisant des règles de numérotation: Exchange 2013 Help'
TOCTitle: Autorisation des appels utilisant des règles de numérotation
ms:assetid: 4c18bc07-f55c-42b7-81c1-729878aa93aa
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ898499(v=EXCHG.150)
ms:contentKeyID: 51407182
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Autorisation des appels utilisant des règles de numérotation

 

_**Sapplique à :** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2015-03-09_

Par défaut, les utilisateurs ne peuvent pas passer d’appels sortants. Pour spécifier les types d'appels que les utilisateurs peuvent effectuer, commencez par créer des règles de numérotation, puis autorisez les groupes de ces règles sur les plans de numérotation, les stratégies de boîte aux lettres et les standards automatiques de messagerie unifiée. Avant de pouvoir autoriser des groupes de règles de numérotation, vous devez d'abord définir des règles de numérotation sur un plan de numérotation de messagerie unifiée. Pour plus d'informations, consultez la rubrique [Créer des règles de numérotation pour les utilisateurs](create-dialing-rules-for-users-exchange-2013-help.md).

Toutes les règles de numérotation que vous créez contiennent les types d'appels ou les modèles de numéros auxquels vous voulez que les utilisateurs aient accès. Vous pouvez autoriser différents types d'utilisateurs à effectuer différents types d'appels. Les appels que vous autorisez peuvent être nationaux, régionaux ou internationaux.

Pour autoriser ou restreindre la numérotation, les paramètres suivants doivent être configurés correctement :

  - **Règles de numérotation**   Les règles de numérotation définissent le numéro composé par les utilisateurs à extension messagerie unifiée ainsi que le numéro envoyé à partir de la messagerie unifiée et composé par le PBX ou PBX IP. Créez un groupe de règles de numérotation en ajoutant une règle de numérotation. Une fois le groupe créé, ajoutez-le à la liste des appels autorisés pour un groupe de règles de numérotation national/régional ou international.

  - **Groupes de règles de numérotation**   Les groupes de règles de numérotation déterminent les types d'appels que les utilisateurs au sein du groupe peuvent effectuer.

  - **Autorisations de numérotation**   Les autorisations de numérotation permettent de déterminer les restrictions appliquées afin d'empêcher les utilisateurs d'engager des frais de communications téléphoniques superflus ou de passer des appels longue distance.

## Comment autoriser un groupe de règles de numérotation ?

La manière d'autoriser les groupes de règles de numérotation dépend du type d'appelant que vous voulez autoriser à effectuer des appels sortants. Par exemple, si vous voulez que seuls les utilisateurs d'Outlook Voice Access puissent effectuer des appels sortants, vous allez créer vos règles de numérotation, puis autoriser ces groupes de numérotation sur la stratégie de boîte aux lettres de messagerie unifiée à laquelle les utilisateurs d'Outlook Voice Access sont associés. Le tableau suivant montre comment autoriser les appels pour différents types d'appelants.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Type d'appelant</th>
<th>Autoriser des groupes de règles de numérotation ici</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Appelants non authentifiés qui appellent un numéro Outlook Voice Access et n’entrent pas de code confidentiel</p></td>
<td><p>Plan de numérotation de messagerie unifiée. Pour plus d'informations, consultez la rubrique <a href="authorize-calls-for-users-in-a-dial-plan-exchange-2013-help.md">Autoriser les appels destinés aux utilisateurs dans un plan de numérotation</a>.</p></td>
</tr>
<tr class="even">
<td><p>Appelants authentifiés qui appellent un numéro Outlook Voice Access et indiquent un code confidentiel.</p></td>
<td><p>Stratégie de boîte aux lettres de messagerie unifiée pour l'appelant. Pour plus d'informations, consultez la rubrique <a href="authorize-calls-for-a-group-of-users-exchange-2013-help.md">Autoriser les appels pour un groupe d'utilisateurs</a>.</p></td>
</tr>
<tr class="odd">
<td><p>Appelants non authentifiés qui appellent un numéro de téléphone configuré sur un standard automatique de messagerie unifiée</p></td>
<td><p>Standard automatique de messagerie unifiée. Pour plus d'informations, consultez la rubrique <a href="authorize-calls-for-auto-attendant-callers-exchange-2013-help.md">Autoriser les appels d'appelants de standard automatique</a>.</p></td>
</tr>
</tbody>
</table>


En fonction des utilisateurs que vous autorisez à effectuer des appels sortants, utilisez la page **Autorisation de numérotation** du Centre d’administration Exchange (CAE) pour le plan de numérotation, le standard automatique ou la stratégie de boîte aux lettres de messagerie unifiée.

