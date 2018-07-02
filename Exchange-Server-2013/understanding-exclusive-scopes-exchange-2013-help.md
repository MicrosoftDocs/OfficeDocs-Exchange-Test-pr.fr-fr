---
title: 'Présentation des étendues exclusives: Exchange 2013 Help'
TOCTitle: Présentation des étendues exclusives
ms:assetid: 32492622-3b01-4e3b-8288-ed39525eea75
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dd638110(v=EXCHG.150)
ms:contentKeyID: 50477845
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Présentation des étendues exclusives

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2015-03-09_

Les *étendues exclusives* constituent un type particulier d’étendue de gestion explicite qui peut être associée à des attributions de rôle de gestion. Les étendues exclusives permettent de gérer les situations où vous possédez un groupe d’objets très importants (comme la boîte aux lettres d’un PDG) et souhaitez contrôler précisément les personnes ayant accès à la gestion de ces objets.

Une attribution de rôle dotée d’une étendue exclusive est appelée *attribution de rôle exclusive*.

Lorsque vous créez une étendue exclusive, seules les personnes auxquelles cette étendue exclusive (ou une étendue exclusive équivalente) s’applique peuvent modifier les objets qui correspondent à l’étendue. Les personnes affectées au rôle qui ne bénéficient pas de cette étendue exclusive (ou d’une étendue exclusive équivalente) ne peuvent pas modifier les objets qui correspondent à l’étendue, même si leurs propres rôles bénéficient d’étendues qui, autrement, incluraient les objets. Les étendues exclusives remplacent les étendues normales qui ne sont pas exclusives. Ce comportement est similaire au fonctionnement d’une entrée de contrôle d’accès Refuser dans une liste de contrôle d’accès Active Directory.

Une *étendue exclusive équivalente* désigne une autre étendue exclusive incluant certains objets identiques à ceux d’une autre étendue exclusive. Une correspondance du même groupe d’objets complet n’est pas nécessaire dans les deux étendues. Les deux étendues peuvent être en mesure de modifier une partie ou l’intégralité des objets auxquels elles sont associées.

## Création d’étendues exclusives

Une étendue exclusive peut être créée de la même manière que n’importe quelle autre étendue explicite. Vous pouvez spécifier une étendue relative prédéfinie, un filtre de destinataire, de base de données ou de serveur, ou une liste de serveur ou de base de données. Contrairement aux étendues normales, qui ne prennent pas effet tant que vous n’avez pas associé une étendue à une attribution de rôle de gestion, le critère de refus d’une étendue exclusive prend effet immédiatement. Cela signifie que dès qu’une étendue exclusive est créée, les utilisateurs ne peuvent plus accéder aux objets contenus dans cette étendue tant que les attributions de rôles n’ont pas été créées.

Une fois que l’attribution a été créée, l’étendue exclusive autorise l’accès des utilisateurs associés à l’étendue et au rôle de gestion. Si une autre étendue exclusive équivalente correspond aux mêmes objets, l’attribution de rôle associée à cette étendue exclusive est toujours en mesure d’accéder aux objets.

Pour plus d’informations sur les filtres d’étendue de gestion, voir [Présentation des filtres d’attribution du rôle de gestion](understanding-management-role-scope-filters-exchange-2013-help.md).

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159813.important(EXCHG.150).gif" title="Important" alt="Important" />Important :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Les délais de réplication Active Directory doivent être pris en compte lorsque vous apportez des modifications à des composants de rôle de gestion, y compris aux étendues exclusives.</td>
</tr>
</tbody>
</table>


Si des objets sont contenus dans plusieurs étendues exclusives, le fait d’appartenir à l’une des étendues exclusives permet d’accéder aux objets. Pour plus d’informations, consultez la section Exclusive and regular scope interaction plus loin dans cette rubrique.

Les étendues exclusives déterminent uniquement la portée d’écriture de configuration ou de destinataire explicite d’une attribution de rôle. La portée de lecture de configuration ou de destinataire implicite du rôle attribué à un utilisateur ou un groupe continue de s’appliquer. Par conséquent, les conditions suivantes s’appliquent :

  - Les personnes auxquelles un rôle est attribué continuent de voir les objets qui correspondent à la portée de lecture implicite du rôle.

  - Les personnes dotées d’autres rôles peuvent voir les objets contenus dans une étendue exclusive, à condition que les portées de lecture des autres rôles incluent les objets. Cependant, les objets ne peuvent être modifiés que par les personnes dotées d’un rôle qui est associé à l’étendue exclusive.

Les étendues exclusives doivent être utilisées uniquement avec des rôles de spécialiste ou d’administrateur : elles ne peuvent pas être utilisées avec des rôles d’utilisateur final. Pour plus d’informations sur les rôles, voir [Présentation des rôles de gestion](understanding-management-roles-exchange-2013-help.md).

## Interaction des étendues exclusives et normales

L’exemple présenté à la fin de cette section illustre les interactions au sein des étendues exclusives, ainsi que les interactions entre les étendues exclusives et les étendues normales. Les utilisateurs mentionnés dans l’exemple sont dotés des attributs suivants.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>User</th>
<th>Ville</th>
<th>Poste</th>
<th>Service</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Terry</p></td>
<td><p>Vancouver</p></td>
<td><p>Comptable</p></td>
<td><p>Comptabilité</p></td>
</tr>
<tr class="even">
<td><p>David</p></td>
<td><p>Vancouver</p></td>
<td><p>Rédacteur</p></td>
<td><p>Marketing</p></td>
</tr>
<tr class="odd">
<td><p>Walter</p></td>
<td><p>Vancouver</p></td>
<td><p>Directeur</p></td>
<td><p>Marketing</p></td>
</tr>
<tr class="even">
<td><p>Bob</p></td>
<td><p>Vancouver</p></td>
<td><p>PDG</p></td>
<td><p>Direction</p></td>
</tr>
<tr class="odd">
<td><p>Christine</p></td>
<td><p>Vancouver</p></td>
<td><p>Président</p></td>
<td><p>Direction</p></td>
</tr>
<tr class="even">
<td><p>Fred</p></td>
<td><p>Vancouver</p></td>
<td><p>Directeur financier</p></td>
<td><p>Cadre</p></td>
</tr>
<tr class="odd">
<td><p>Martin</p></td>
<td><p>Vancouver</p></td>
<td><p>Directeur informatique</p></td>
<td><p>Cadre</p></td>
</tr>
<tr class="even">
<td><p>Kim</p></td>
<td><p>Vancouver</p></td>
<td><p>Vice-président de l’exploitation</p></td>
<td><p>Cadre</p></td>
</tr>
<tr class="odd">
<td><p>Jennifer</p></td>
<td><p>Vancouver</p></td>
<td><p>Vice-président des technologies</p></td>
<td><p>Cadre</p></td>
</tr>
</tbody>
</table>


Les trois attributions de rôle de gestion suivantes gèrent les utilisateurs du tableau précédent. Chaque attribution possède une entendue associée, qui est parfois une étendue exclusive.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Attribution de rôle</th>
<th>Filtre d’étendue</th>
<th>Exclusive ou normale</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Administrateurs des destinataires</p></td>
<td><p>Ville = Vancouver</p></td>
<td><p>Normale</p></td>
</tr>
<tr class="even">
<td><p>Administrateurs des VIP</p></td>
<td><p>Poste = PDG, directeur financier, directeur informatique ou président</p></td>
<td><p>Exclusif</p></td>
</tr>
<tr class="odd">
<td><p>Administrateurs des cadres</p></td>
<td><p>Service = Cadre</p></td>
<td><p>Exclusif</p></td>
</tr>
</tbody>
</table>


L’attribution de rôle Administrateurs des destinataires possède une étendue qui correspond à tous les utilisateurs, car chaque utilisateur est situé à Vancouver. S’il n’existait aucune étendue exclusive, l’attribution de rôle Administrateurs des destinataires pourrait ainsi gérer n’importe quel utilisateur. Toutefois, cette organisation a créé deux étendues exclusives : Administrateurs des VIP et Administrateurs des cadres. Ces étendues exclusives limitent les personnes habilitées à gérer les utilisateurs qui correspondent à leur filtre d’étendue respective. L’attribution de rôle Administrateurs des VIP possède un filtre d’étendue qui correspond à tout utilisateur dont le poste est PDG, directeur financier, directeur informatique ou président. L’attribution de rôle Administrateurs des cadres possède un filtre d’étendue qui correspond à tout utilisateur appartenant au service Cadre.

Lorsque les étendues exclusives et normales sont évaluées, le résultat est le suivant :

  - L’attribution de rôle Administrateurs des destinataires peut gérer les utilisateurs Terry, David et Walter. Cette attribution de rôle ne peut gérer aucun autre utilisateur, car les autres utilisateurs correspondent aux filtres d’étendue exclusive des attributions de rôle Administrateurs des VIP et Administrateurs des cadres.

  - L’attribution de rôle Administrateurs des VIP peut gérer les utilisateurs Bob, Christine, Fred et Martin. De fait, le filtre d’étendue exclusif associé à l’attribution de rôle correspond aux attributs sur ces objets. Cette attribution de rôle ne peut pas gérer les utilisateurs Kim et Jennifer, car leurs attributs ne correspondent pas à cette étendue exclusive.

  - L’attribution de rôle Administrateurs des cadres peut gérer les utilisateurs Kim, Jennifer, Fred et Martin. De fait, le filtre d’étendue exclusif associé à l’attribution de rôle correspond aux attributs sur ces objets. Cette attribution de rôle ne peut pas gérer les utilisateurs Bob et Christine, car leurs attributs ne correspondent pas à cette étendue exclusive.

Notez que les deux étendues exclusives peuvent accéder à Fred et Martin. En effet, les attributs de ces utilisateurs correspondent aux filtres des deux étendues exclusives.

**Interactions entre les étendues exclusives et les étendues normales**

![Interaction des étendues exclusives et normales](images/Dd638110.0aa26d1d-1fa6-44d8-802d-83d75cd2624c(EXCHG.150).jpg "Interaction des étendues exclusives et normales")

Pour plus d’informations sur les étendues de gestion, voir [Présentation des portées du rôle de gestion](understanding-management-role-scopes-exchange-2013-help.md).

