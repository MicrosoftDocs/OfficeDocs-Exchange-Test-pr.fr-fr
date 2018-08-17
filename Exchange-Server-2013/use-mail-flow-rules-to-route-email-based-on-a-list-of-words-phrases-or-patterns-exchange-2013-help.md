---
title: 'Rgl de flux de messag. pr achem. e-mails p/r à 1 liste de mots, exprs ou mod.'
TOCTitle: Utiliser des règles de flux de messagerie pour acheminer le courrier électronique en fonction d’une liste de mots, d’expressions ou de modèles
ms:assetid: 4c5bee1b-58b5-4152-baef-86fa103050ae
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dn951131(v=EXCHG.150)
ms:contentKeyID: 65218856
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Utiliser des règles de flux de messagerie pour acheminer le courrier électronique en fonction d’une liste de mots, d’expressions ou de modèles

 

_**Sapplique à :** Exchange Online, Exchange Online Protection, Exchange Server 2013_

_**Dernière rubrique modifiée :** 2017-10-30_

Pour aider vos utilisateurs à se conformer aux stratégies de messagerie de votre organisation, vous pouvez utiliser des règles de transport Exchange pour déterminer le mode d’acheminement du courrier électronique contenant des mots ou modèles spécifiques. Pour consulter la liste courte de mots ou d’expressions, vous pouvez utiliser le Centre d’administration Exchange. Pour une liste plus longue, vous pouvez utiliser le module Exchange pour Windows PowerShell pour lire la liste à partir d’un fichier texte.

  - Exemple 1 : Utiliser une courte liste de mots interdits

  - Exemple 2 : Utilisez une longue liste de mots interdits

Si votre organisation utilise la protection contre la perte de données (DLP), consultez [Protection contre la perte de données](technical-overview-of-dlp-data-loss-prevention-in-exchange.md) pour découvrir des options supplémentaires permettant d’identifier et d’acheminer le courrier électronique qui contient des informations sensibles.

## Exemple 1 : Utiliser une courte liste de mots interdits

Si votre liste de mots ou expressions est courte, vous pouvez créer une règle à l’aide du Centre d’administration Exchange. Par exemple, si vous voulez vous assurer que personne n’envoie de courrier électronique contenant des mots incorrects ou des fautes d’orthographe dans le nom de votre société, les acronymes internes ou les noms de produit, vous pouvez créer une règle pour bloquer le message et avertir l’expéditeur. Notez que les mots, phrases et modèles ne respectent pas la casse.

Cet exemple bloque les messages contenant des fautes de frappe courantes.

![Règle affichant le blocage d’un message en fonction de critères de texte](images/Dn951131.a8489cbb-be59-4890-ae30-1431703eeb88(EXCHG.150).png "Règle affichant le blocage d’un message en fonction de critères de texte")

## Exemple 2 : Utilisez une longue liste de mots interdits

Si votre liste de mots, d’expressions ou de modèles est longue, vous pouvez placer chacun des éléments sur une ligne différente dans un fichier texte. Utilisez le module Exchange pour Windows PowerShell pour lire la liste des mots-clés dans une variable, créez une règle de transport et affectez la variable avec les mots-clés à la condition de règle de transport. Par exemple, le script suivant tire une liste de fautes d’orthographe d’un fichier nommé misspelled\_companyname.txt.

    $keywords=Import-Content  .\misspelled_companyname.txt
    New-TransportRule -Name "Block messages with unacceptable words" -SubjectOrBodyContainsWords $keywords -SentToScope "NotInOrganization" -RejectMessageReasonText "Do not use internal acronyms, product names, or misspellings in external communications."

## À l’aide d’expressions et de modèles dans le fichier texte

Le fichier texte peut contenir des expressions régulières pour les modèles. Ces expressions ne respectent pas la casse. Voici quelques exemples d’expressions régulières courantes :


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>Expression</strong></p></td>
<td><p><strong>Correspond à</strong></p></td>
</tr>
<tr class="even">
<td><p><strong>.</strong></p></td>
<td><p>Tout caractère unique</p></td>
</tr>
<tr class="odd">
<td><p><strong>*</strong></p></td>
<td><p>Tout caractère supplémentaire</p></td>
</tr>
<tr class="even">
<td><p><strong>\d</strong></p></td>
<td><p>Tout chiffre décimal</p></td>
</tr>
<tr class="odd">
<td><p>[<em>character_group</em>]</p></td>
<td><p>Tout caractère unique dans <em>character_group</em>.</p></td>
</tr>
</tbody>
</table>


Par exemple, ce fichier texte contient des fautes d’orthographe courantes dans le nom Microsoft.

    [mn]sft
    [mn]icrosft
    [mn]icro soft
    [mn].crosoft

Pour découvrir comment spécifier des modèles à l’aide d’expressions régulières, consultez la rubrique [Langage des expressions régulières - Aide-mémoire](https://go.microsoft.com/fwlink/p/?linkid=532394).

