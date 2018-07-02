---
title: 'Modification de propriétés à valeurs multiples: Exchange 2013 Help'
TOCTitle: Modification de propriétés à valeurs multiples
ms:assetid: dc2c1062-ad79-404b-8da3-5b5798dbb73b
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb684908(v=EXCHG.150)
ms:contentKeyID: 50479377
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Modification de propriétés à valeurs multiples

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2015-03-09_

Une propriété à valeurs multiples est une propriété qui peut contenir plusieurs valeurs. Par exemple, la propriété **BlockedRecipients** sur l’objet **RecipientFilterConfig** peut accepter plusieurs adresses de destinataire, par exemple :

  - john@contoso.com

  - kim@northwindtraders.com

  - david@adatum.com

Étant donné que la propriété **BlockedRecipients** peut accepter plusieurs valeurs, elle est appelée propriété à valeurs multiples. Cette rubrique explique comment utiliser l’environnement de ligne de commande Exchange Management Shell pour ajouter et supprimer des valeurs d’une propriété à valeurs multiples sur un objet.

Pour plus d’informations sur les objets, voir [Données structurées](https://technet.microsoft.com/fr-fr/library/aa996386\(v=exchg.150\)). Pour plus d’informations sur l’environnement de ligne de commande Exchange Management Shell, consultez la rubrique [Utilisation de PowerShell avec Exchange 2013 (Exchange Management Shell)](https://technet.microsoft.com/fr-fr/library/bb123778\(v=exchg.150\)).

## Modification d’une propriété à valeurs multiples et d’une propriété n’acceptant qu’une seule valeur

La procédure de modification d’une propriété à valeurs multiples diffère légèrement de la procédure de modification d’une propriété n’acceptant qu’une valeur. Lorsque vous modifiez une propriété qui n’accepte qu’une valeur, vous pouvez lui affecter directement une valeur, comme dans la commande suivante.

    Set-TransportConfig -MaxSendSize 12MB

Lorsque vous utilisez cette commande pour fournir une nouvelle valeur à la propriété **MaxSendSize**, la valeur stockée est remplacée. Cela ne pose aucun problème avec les propriétés n’acceptant qu’une valeur, ce n’est, en revanche, pas le cas avec les propriétés à valeurs multiples. Supposons par exemple que la propriété **BlockedRecipients** de l’objet **RecipientFilterConfig** est configurée pour recevoir les trois valeurs indiquées dans la section précédente. Lorsque vous exécutez la commande `Get-RecipientFilterConfig | Format-List BlockedRecipients`, le résultat suivant s’affiche.

    BlockedRecipients : {david@adatum.com, kim@northwindtraders.com, john@contoso.com}

Supposons maintenant que vous avez reçu une demande pour ajouter une nouvelle adresse SMTP à la liste des destinataires bloqués. Vous devez exécuter la commande suivante pour ajouter la nouvelle adresse SMTP.

    Set-RecipientFilterConfig -BlockedRecipients chris@contoso.com

Lorsque vous exécutez de nouveau la commande `Get-RecipientFilterConfig | Format-List BlockedRecipients`, vous obtenez ce qui suit.

    BlockedRecipients : {chris@contoso.com}

Ce n’est pas ce que vous attendiez. Vous souhaitiez ajouter la nouvelle adresse SMTP à la liste existante de destinataires bloqués, mais celle-ci a été remplacée par la nouvelle adresse SMTP. Ce résultat inattendu montre à titre d’exemple comment la modification de propriétés à valeurs multiples diffère de celle des propriétés qui n’acceptent qu’une seule valeur. Lorsque vous modifiez une propriété à valeurs multiples, vous devez veiller à ajouter ou supprimer les valeurs et non pas remplacer l’ensemble de la liste de valeurs. Les sections suivantes vous indiquent comment procéder.

## Modification de propriétés à valeurs multiples

La modification des propriétés à valeurs multiples suit le même processus que si vous modifiiez des propriétés à valeur unique. Il vous suffit d’ajouter une syntaxe supplémentaire pour indiquer à l’environnement de ligne de commande Exchange Management Shell que vous souhaitez ajouter ou supprimer des valeurs vers ou à partir de la propriété à valeurs multiples plutôt que de remplacer tout le contenu stocké dans la propriété. Tout comme la ou les valeurs à ajouter dans la propriété ou à supprimer de celle-ci, la syntaxe est incluse et apparaît sous la forme d’une valeur dans un paramètre lorsque vous exécutez une cmdlet. Le tableau qui suit présente la syntaxe que vous devez ajouter à un paramètre dans une cmdlet pour modifier les propriétés à valeurs multiples.

### Syntaxe des propriétés à valeurs multiples

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Action</th>
<th>Syntaxe</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Ajouter une ou plusieurs valeurs à une propriété à valeurs multiples</p></td>
<td><pre><code>@{Add=&quot;&lt;value1&gt;&quot;, &quot;&lt;value2&gt;&quot;, &quot;&lt;value3&gt;&quot;}</code></pre></td>
</tr>
<tr class="even">
<td><p>Supprimer une ou plusieurs valeurs d’une propriété à valeurs multiples</p></td>
<td><pre><code>@{Remove=&quot;&lt;value1&gt;&quot;, &quot;&lt;value2&gt;&quot;, &quot;&lt;value3&gt;&quot;}</code></pre></td>
</tr>
</tbody>
</table>


La syntaxe que vous choisissez dans le tableau de syntaxe des propriétés à valeurs multiples est précisée sous la forme d’une valeur de paramètre dans une cmdlet. Par exemple, la commande suivante ajoute plusieurs valeurs à une propriété à valeurs multiples :

    Set-ExampleCmdlet -Parameter @{Add="Red", "Blue", "Green"}

Lorsque vous utilisez cette syntaxe, les valeurs que vous spécifiez sont ajoutées ou supprimées de la liste des valeurs déjà présentes dans la propriété. Prenons l’exemple **BlockedRecipients** présenté plus haut dans cette rubrique : nous pouvons désormais ajouter l’utilisateur chris@contoso.com sans remplacer les valeurs restantes dans cette propriété à l’aide de la commande suivante :

    Set-RecipientFilterConfig -BlockedRecipients @{Add="chris@contoso.com"}

Si vous souhaitiez supprimer david@adatum.com de la liste des valeurs, vous utiliseriez cette commande :

    Set-RecipientFilterConfig -BlockedRecipients @{Remove="david@adatum.com"}

Des combinaisons plus complexes peuvent être utilisées, notamment en ajoutant ou en supprimant simultanément des éléments dans une propriété. Pour ce faire, insérez un point-virgule (`;`) entre les actions `Add` et `Remove`. Par exemple :

    Set-RecipientFilterConfig -BlockedRecipients @{Add="carter@contoso.com", "sam@northwindtraders.com", "brian@adatum.com"; Remove="john@contoso.com"}

Si vous réutilisez la commande `Get-RecipientFilterConfig | Format-List BlockedRecipients`, on constate que les adresses de messagerie de Carter, Sam et Brian ont été ajoutées alors que l’adresse de John a été supprimée.

    BlockedRecipients : {brian@adatum.com, sam@northwindtraders.com, carter@contoso.com, chris@contoso.com, kim@northwindtraders.com}

