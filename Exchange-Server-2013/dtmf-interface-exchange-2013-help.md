---
title: 'Interface DTMF: Exchange 2013 Help'
TOCTitle: Interface DTMF
ms:assetid: 2c7c9d8a-ed12-4dcf-a5b7-3cea0e785e49
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Aa996919(v=EXCHG.150)
ms:contentKeyID: 54652724
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Interface DTMF

 

_**Sapplique à :** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2016-12-09_

Dans la messagerie unifiée, les appelants peuvent utiliser des entrées DTMF (numérotation en fréquences vocales), également appelées numérotation multifréquence, et des entrées vocales pour interagir avec le système. La méthode utilisée par les appelants dépend de la configuration des standards automatiques et des plans de numérotation de messagerie unifiée.

L'interface DTMF permet aux appelants d'utiliser le clavier du téléphone pour localiser les utilisateurs et naviguer dans le système de menus de la messagerie vocale unifiée quand ils composent un numéro Outlook Voice Access configuré dans un plan de numérotation ou un numéro de téléphone configuré sur un standard automatique. Cette rubrique décrit l'interface DTMF et son utilisation par les appelants pour localiser des utilisateurs et naviguer dans le système de menus de la messagerie vocale unifiée.

**Contenu de cette rubrique**

Présentation de la numérotation en fréquences vocales (DTMF)

Plans de numérotation de messagerie unifiée et numérotation par nom

Plans DTMF

Plans DTMF pour les utilisateurs sans extension messagerie unifiée

Plans DTMF pour les utilisateurs à extension messagerie unifiée

Pour plus d'informations

## Présentation de la numérotation en fréquences vocales (DTMF)

La numérotation en fréquences vocales requiert qu'un appelant appuie sur une touche du clavier de téléphone correspondant à une option du menu de la messagerie unifiée ou entre le nom ou l'adresse de messagerie d'un utilisateur à l'aide des lettres figurant sur les touches pour épeler le nom ou l'alias. Les appelants peuvent utiliser la numérotation en fréquences vocales si la reconnaissance vocale (ASR) n'a pas été activée ou s'ils ont essayé sans succès d'utiliser les commandes vocales. Dans les deux cas, les entrées DTMF permettent de naviguer dans les menus et de rechercher des utilisateurs.

Par défaut, dans la messagerie unifiée, les entrées DTMF sont utilisées dans des plans de numérotation et constituent l'interface d'appelant par défaut des standards automatiques de messagerie unifiée.

Les appelants peuvent utiliser les entrées DTMF pour :

  - l'accès entrant au plan de numérotation via Outlook Voice Access ;

  - les recherches dans l'annuaire du plan de numérotation afin de localiser des utilisateurs ;

  - les standards automatiques qui ne sont pas à reconnaissance vocale ;

  - les standards automatiques à reconnaissance vocale pour lesquels un standard automatique de secours DTMF est configuré ou non ;

  - les standards automatiques de secours DTMF (non activés pour la reconnaissance vocale).

## Plans de numérotation de messagerie unifiée et numérotation par nom

Lors de la création d'un plan de numérotation de messagerie unifiée, vous pouvez configurer une méthode de saisie principale et secondaire que les appelants vont utiliser pour rechercher des noms afin de contacter un utilisateur. Ces paramètres sont situés dans la page **Paramètres** du plan de numérotation et s'intitulent **Premier moyen de rechercher des noms** et **Deuxième moyen de rechercher des noms**. Les options suivantes sont disponibles pour le premier et deuxième moyen de rechercher des noms :

  - Nom Prénom

  - Prénom Nom

  - Adresse SMTP

Par ailleurs, l'option **Aucun** est également disponible pour le deuxième moyen de rechercher des noms.

Par défaut, l'option **Nom Prénom** est sélectionnée comme premier moyen de rechercher des noms et l'option **Adresse SMTP** est sélectionnée comme deuxième moyen de rechercher des noms. Par conséquent, quand un appelant compose un numéro Outlook Voice Access configuré dans le plan de numérotation de messagerie unifiée, le message d'accueil est lu et l'opérateur lit un texte similaire à « Bienvenue dans Contoso Outlook Voice Access. Pour accéder à votre boîte aux lettres, entrez votre numéro de poste. Pour contacter une personne, appuyez sur la touche dièse ». Une fois que l'appelant a appuyé sur la touche dièse, le système répond « Épelez le nom puis le prénom de la personne que vous appelez ou, pour épeler l'alias de messagerie de la personne que vous appelez, appuyez deux fois sur la touche £ ». Dans ce scénario, en fonction de la configuration du plan de numérotation, le système invite l'appelant à entrer le nom et le prénom de l'utilisateur (Nom Prénom) ou à épeler l'alias de messagerie de l'utilisateur (nom de domaine exclu). Par exemple, si l'alias de messagerie de l'utilisateur est tsmith@contoso.com, l'appelant entre tsmith.

Si la configuration par défaut ne correspond pas à vos besoins, vous pouvez la modifier pour permettre aux appelants d'entrer d'abord l'alias de messagerie de l'utilisateur ou le prénom puis le nom de l'utilisateur. Dans ce cas, vous configurez l'option **Premier moyen de rechercher des noms** avec le paramètre **Adresse SMTP** et l'option **Deuxième moyen de rechercher des noms** avec le paramètre **Prénom Nom**. Les paramètres des méthodes de numérotation par nom s'appliquent également aux standards automatiques de messagerie unifiée associés au plan de numérotation. Pour que les appelants puissent saisir le nom de l’utilisateur à l’aide d’entrées DTMF ou des touches du clavier du téléphone, l’annuaire de votre organisation doit comporter un plan DTMF et des valeurs pour l’utilisateur.

Pour plus d'informations sur la modification des méthodes de numérotation par nom dans un plan de numérotation de messagerie unifiée, consultez les rubriques [Configurer le principal moyen pour les utilisateurs Outlook Voice Access pour la recherche](configure-the-primary-way-for-outlook-voice-access-users-to-search-exchange-2013-help.md) et [Configurer le deuxième moyen pour les utilisateurs Outlook Voice Access pour la recherche](configure-the-secondary-way-for-outlook-voice-access-users-to-search-exchange-2013-help.md).

Présentation de la numérotation en fréquences vocales (DTMF)

## Plans DTMF

Dans une organisation Exchange, un attribut nommé **msExchUMDtmfMap** est associé à chaque utilisateur créé dans l'annuaire. La messagerie unifiée utilise cet attribut pour mapper le prénom, le nom et l'alias de messagerie à un ensemble de chiffres. Ce mappage correspond au plan DTMF. Un plan DTMF permet aux appelants d'entrer les chiffres correspondant aux lettres du nom ou de l'alias de messagerie de l'utilisateur sur le clavier du téléphone. Cet attribut contient les valeurs nécessaires à la création d'un plan DTMF pour le prénom puis le nom de l'utilisateur, pour le nom puis le prénom de l'utilisateur et pour l'alias de messagerie de l'utilisateur.

Le tableau suivant montre les valeurs du plan DTMF qui seront enregistrées dans Active Directory sous l'attribut **msExchUMDtmfMap** pour un utilisateur à extension messagerie unifiée nommé Tony Smith dont l'alias est tsmith@contoso.com.

**Valeurs DTMF enregistrées pour un utilisateur à extension messagerie nommé Tony Smith**


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Entrée d'annuaire</th>
<th>Nom de l'utilisateur</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><ul>
<li><p>firstNameLastName:866976484</p></li>
</ul></td>
<td><p>tonysmith</p></td>
</tr>
<tr class="even">
<td><ul>
<li><p>lastNameFirstName:764848669</p></li>
</ul></td>
<td><p>smithtony</p></td>
</tr>
<tr class="odd">
<td><ul>
<li><p>emailAddress:876484</p></li>
</ul></td>
<td><p>tsmith</p></td>
</tr>
</tbody>
</table>


Les noms et alias de messagerie peuvent contenir des caractères non alphanumériques tels que les virgules, les traits d'union, les caractères de soulignement ou les points. Ces caractères ne sont pas utilisés dans un plan DTMF pour un utilisateur. Par exemple, si l'alias de messagerie de Tony Smith est tony-smith@contoso.com, la valeur du plan DTMF est 866976484 et le trait d'union n'est pas inclus. Toutefois, si l'alias de messagerie d'un utilisateur contient un ou plusieurs chiffres (par exemple, tonysmith123@contoso.com), les chiffres seront utilisés dans le plan DTMF créé. Le plan DTMF pour tonysmith123 serait 866976484123.

Un plan DTMF doit exister pour un utilisateur afin que les appelants puissent entrer le nom ou l'alias de messagerie de l'utilisateur. Toutefois, tous les utilisateurs n'ont pas de plan DTMF associé avec leur compte d'utilisateur.

Présentation de la numérotation en fréquences vocales (DTMF)

## Plans DTMF pour les utilisateurs sans extension messagerie unifiée

La messagerie unifiée n'est, par défaut, pas activée pour les utilisateurs, notamment les utilisateurs dotés d'une boîte aux lettres. L’attribut **msExchUMDtmfMap** est renseigné avec les valeurs nécessaires aux plans DTMF pour les utilisateurs sans extension messagerie unifiée. Par défaut, les plans DTMF suivants sont créés pour tous les utilisateurs lors de la création d'une boîte aux lettres à leur intention :

1.  emailAddress

2.  firstNameLastName

3.  lastNameFirstName

Si un utilisateur n’a pas de valeurs de plan DTMF définies pour son compte, les appelants ne peuvent pas le contacter quand ils appuient sur une touche du clavier du téléphone depuis un menu de standard automatique de messagerie unifiée ou quand ils effectuent une recherche dans l’annuaire. Par ailleurs, les utilisateurs à extension messagerie unifiée ne peuvent pas envoyer de messages ou transférer des appels aux utilisateurs sans plan DTMF, sauf s’ils peuvent avoir recours à la reconnaissance vocale. Pour permettre aux appelants de transférer des appels ou de contacter des utilisateurs sans extension messagerie unifiée à l'aide du clavier du téléphone, vous devez créer les valeurs nécessaires pour le plan DTMF associé à ces utilisateurs. Vous pouvez utiliser la cmdlet **Set-User** avec le paramètre *-CreateDtmfMap* pour créer et mettre à jour le plan DTMF d'un utilisateur ou mettre à jour un plan DTMF pour un utilisateur si le nom de ce dernier a été modifié après la création du plan DTMF. Par ailleurs, vous pouvez créer un script dans l'environnement de ligne de commande Exchange Management Shell en utilisant cette cmdlet pour mettre à jour les valeurs du plan DTMF associé à plusieurs utilisateurs.

Pour plus d'informations sur la cmdlet **Set-User**, consultez la rubrique [Set-User](https://technet.microsoft.com/fr-fr/library/aa998221\(v=exchg.150\)).

Présentation de la numérotation en fréquences vocales (DTMF)

## Plans DTMF pour les utilisateurs à extension messagerie unifiée

Par défaut, un plan DTMF est créé pour un utilisateur quand la messagerie unifiée est activée pour ce dernier. Cela permet de transférer les appels d'appelants externes, d'utilisateurs sans extension messagerie unifiée et d'autres utilisateurs à extension messagerie unifiée qui utilisent le clavier du téléphone pour épeler le nom ou l'alias de messagerie de l'utilisateur vers un utilisateur à extension messagerie unifiée.

Une fois les valeurs du plan DTMF créées pour un utilisateur à extension messagerie unifiée, les appelants peuvent utiliser la fonctionnalité de recherche dans l'annuaire. Les appelants utilisent cette fonctionnalité quand ils utilisent le clavier du téléphone dans les situations suivantes :

  - pour identifier ou rechercher un utilisateur quand ils appellent un numéro Outlook Voice Access ;

  - pour localiser ou transférer des appels à un utilisateur à extension messagerie unifiée quand ils appellent un standard automatique de messagerie unifiée.

Pour plus d'informations sur l'activation de la messagerie unifiée pour un utilisateur, consultez la rubrique [Activation de la messagerie vocale pour un utilisateur](enable-a-user-for-voice-mail-exchange-2013-help.md).

Parfois, le prénom, le nom ou l'alias de messagerie d'un utilisateur est modifié après que la messagerie unifiée a été activée pour celui-ci. Les valeurs du plan DTMF de l'utilisateur ne sont pas automatiquement mises à jour dans. Si un appelant entre le nouveau nom ou le nouvel alias de messagerie de l’utilisateur et que le plan DTMF de l’utilisateur n’a pas été mis à jour afin de répercuter la modification, l’appelant ne peut pas localiser l’utilisateur dans l’annuaire, lui envoyer un message ou lui transférer des appels. Si vous devez mettre à jour le plan DTMF d'un utilisateur après que la messagerie unifiée a été activée pour celui-ci , vous pouvez utiliser la cmdlet **Set-User** avec le paramètre *-CreateDtmfMap*. Par ailleurs, vous pouvez créer un script dans l'environnement de ligne de commande Exchange Management Shell en utilisant cette cmdlet si vous voulez mettre à jour les valeurs du plan DTMF pour plusieurs utilisateurs à extension messagerie unifiée.

> [!CAUTION]
> Nous vous déconseillons de modifier manuellement les valeurs DTMF pour les utilisateurs à l'aide d'un outil tel que l'Éditeur ADSI, car cela peut entraîner des configurations incohérentes ou d'autres erreurs. Nous vous recommandons d'utiliser uniquement la cmdlet <strong>Set-UMService</strong> ou <strong>Set-User</strong> pour créer ou mettre à jour des plans DTMF associés à des utilisateurs.


## Pour plus d'informations

[Éditeur ADSI](https://go.microsoft.com/fwlink/p/?linkid=73175)

