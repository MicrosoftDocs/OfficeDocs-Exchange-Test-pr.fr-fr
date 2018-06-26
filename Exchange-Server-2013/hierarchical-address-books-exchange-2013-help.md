---
title: 'Carnets d’adresses hiérarchiques: Exchange 2013 Help'
TOCTitle: Carnets d’adresses hiérarchiques
ms:assetid: a1d277a0-5437-40af-aade-e4730a0d1308
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Ff629379(v=EXCHG.150)
ms:contentKeyID: 50478933
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Carnets d’adresses hiérarchiques

 

_**Sapplique à :**Exchange Server 2013_

_**Dernière rubrique modifiée :**2014-03-26_

Le carnet d’adresses hiérarchique permet aux utilisateurs de rechercher des destinataires dans leur carnet d’adresses à l’aide d’une hiérarchie d’organisation. Normalement, les utilisateurs sont limités à la LAG par défaut et à ses propriétés de destinataire, et la structure de la LAG ne reflète pas souvent les relations hiérarchiques ou d’ancienneté des destinataires de votre organisation. Le fait de pouvoir personnaliser un carnet d’adresses hiérarchique reflétant la structure métier propre à votre organisation permet à vos utilisateurs de trouver efficacement les destinataires internes.

## Utilisation des carnets d’adresses hiérarchiques

Dans un carnet d’adresses hiérarchique, votre organisation racine (par exemple, Contoso, Ltd.) est utilisée au niveau supérieur. Sous ce niveau supérieur, vous pouvez ajouter plusieurs niveaux enfants pour créer un carnet d’adresses hiérarchique personnalisé, découpé par division, service ou toute autre unité organisationnelle que vous spécifiez. L’image ci-dessous illustre un carnet d’adresses hiérarchique pour Contoso, Ltd. avec la structure suivante :

  - Le niveau supérieur représente l’organisation racine Contoso, Ltd.

  - Les niveaux enfants du deuxième niveau représentent les divisions métiers de Contoso, Ltd. : Corporate Office (Siège), Product Support Organization (Support produit) et Sales & Marketing Organization (Ventes et marketing).

  - Les niveaux enfants du troisième niveau représentent les services de la division Corporate Office (Siège) : Human Resources (Ressources humaines), Accounting Group (Comptabilité) et Administration Group (Administration).

**Exemple de carnet d’adresses hiérarchique pour Contoso, Ltd**

![Boîte de dialogue Carnet d’adresses hiérarchique](images/Ff607473.d8cc782f-61cd-44c4-9c74-432ebea0c3db(EXCHG.150).gif "Boîte de dialogue Carnet d’adresses hiérarchique")

Vous pouvez ajouter un niveau supplémentaire de hiérarchie en utilisant le paramètre *SeniorityIndex*. Lorsque vous créez un carnet d’adresses hiérarchique, utilisez le paramètre *SeniorityIndex* pour classer les destinataires individuels ou les groupes organisationnels par ancienneté au sein des niveaux organisationnels. Ce classement spécifie l’ordre dans lequel les destinataires ou les groupes apparaissent dans le carnet d’adresses hiérarchique. Par exemple, pour l’image ci-dessus, le paramètre *SeniorityIndex* pour les destinataires de la division Corporate Office (Siège) est défini comme suit :

  - `100` pour David Hamilton

  - `50` pour Rajesh M. Patel

  - `25` pour Amy Alberts

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Si le paramètre <em>SeniorityIndex</em> n’est pas défini ou équivaut à deux ou plusieurs utilisateurs, le mode de tri du carnet d’adresses hiérarchique utilise le paramètre <em>PhoneticDisplayName</em> pour répertorier les utilisateurs dans l’ordre alphabétique croissant. Si le paramètre <em>PhoneticDisplayName</em> n’est pas défini, l’ordre de tri du carnet d’adresses hiérarchique est défini par défaut avec la valeur <em>DisplayName</em> et affiche les utilisateurs par ordre alphabétique croissant.</td>
</tr>
</tbody>
</table>


## Configuration des carnets d’adresses hiérarchiques

Les instructions détaillées concernant la création de carnets d’adresses hiérarchiques sont incluses dans la rubrique [Activation ou désactivation des carnets d’adresses hiérarchiques](enable-or-disable-hierarchical-address-books-exchange-2013-help.md). Les étapes générales sont les suivantes :

1.  Créer un groupe de distribution qui sera utilisé pour l’organisation racine (niveau supérieur). Si vous le souhaitez, vous pouvez utiliser une unité organisationnelle existante de votre forêt Exchange pour le groupe de distribution.

2.  Créer des groupes de distribution pour les niveaux enfants et les désigner membres du carnet d’adresses hiérarchique. Modifiez le paramètre *SeniorityIndex* de ces groupes pour qu’ils apparaissent dans l’ordre hiérarchique approprié au sein de l’organisation racine.

3.  Ajouter des membres d’organisation. Modifiez le paramètre *SeniorityIndex* des membres pour qu’ils apparaissent dans l’ordre hiérarchique approprié au sein des niveaux enfants.

4.  Pour des raisons d’accessibilité, vous pouvez utiliser le paramètre *PhoneticDisplayName*, qui spécifie une prononciation phonétique du paramètre *DisplayName*.

