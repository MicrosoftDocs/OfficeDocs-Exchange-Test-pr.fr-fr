---
title: 'Import entrées de réécriture d’adresses sur srv de transp. Edge: Exchange 2013'
TOCTitle: Importation d’entrées de réécriture d’adresses sur des serveurs de transport Edge
ms:assetid: bd0942c6-9c66-4b4c-b9bc-2f5f783def76
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb331966(v=EXCHG.150)
ms:contentKeyID: 61060523
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Importation d’entrées de réécriture d’adresses sur des serveurs de transport Edge

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2015-03-09_

Vous pouvez créer en bloc ou importer des informations de réécriture d’adresses dans un serveur de transport Edge à l’aide d’un fichier de valeurs séparées par des virgules (CSV). La liste suivante décrit les scénarios courants qui nécessitent une telle opération :

  - Vous remplacez une solution de réécriture d’adresses par un serveur de transport Edge.

  - Vous signez un accord avec un fournisseur de solutions tiers, ce qui vous oblige à réécrire leurs adresses de messagerie.

  - Vous acquérez une autre organisation et vous avez besoin de réécrire temporairement les adresses de messagerie de l’organisation acquise.

Vous pouvez utiliser un éditeur de texte, tel que le Bloc-notes, ou une application telle que Microsoft Excel pour créer le fichier CSV. Mettez en forme le fichier comme indiqué dans cette rubrique et enregistrez-le avec l’extension .csv.

La première ligne, ou *ligne d’en-tête*, du fichier CSV énumère les noms des paramètres. Les paramètres sont séparés par des virgules. Les paramètres obligatoires et facultatifs sont décrits dans le tableau suivant.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Paramètre</th>
<th>Obligatoire ou facultatif</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>Name</em></p></td>
<td><p>Obligatoire</p></td>
<td><p>Nom unique et descriptif de l’entrée de réécriture d’adresses.</p></td>
</tr>
<tr class="even">
<td><p><em>InternalAddress</em></p></td>
<td><p>Obligatoire</p></td>
<td><p>Adresse que vous souhaitez modifier. Vous pouvez utiliser les valeurs suivantes :</p>
<ul>
<li><p>une adresse de messagerie unique (chris@contoso.com) ;</p></li>
<li><p>un domaine ou sous-domaine unique (contoso.com ou sales.contoso.com) ;</p></li>
<li><p>un domaine et tous ses sous-domaines (*.contoso.com).</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p><em>ExternalAddress</em></p></td>
<td><p>Obligatoire</p></td>
<td><p>Adresse de messagerie finale de votre choix. Vous pouvez utiliser les valeurs suivantes :</p>
<ul>
<li><p>une adresse de messagerie unique si vous avez spécifié une adresse de messagerie unique pour <em>InternalAddress</em> ;</p></li>
<li><p>un domaine ou sous-domaine unique pour toutes les autres valeurs de <em>InternalAddress</em>.</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><em>ExceptionList</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Disponible uniquement lorsque vous réécrivez des adresses de messagerie dans un domaine et tous ses sous-domaines (*. contoso.com). Spécifie un ou plusieurs sous-domaines que vous souhaitez exclure de la réécriture d’adresses. Placez la valeur entre guillemets doubles et séparez les valeurs par des virgules. Par exemple, <code>&quot;marketing.contoso.com&quot;</code> ou <code>&quot;marketing.contoso.com,legal.contoso.com&quot;</code>.</p></td>
</tr>
<tr class="odd">
<td><p><em>OutboundOnly</em></p></td>
<td><p>Facultatif</p></td>
<td><p><code>False</code> signifie que les adresses sont écrites sur le courrier entrant et sortant. <code>True</code> signifie que les adresses sont réécrites sur le courrier sortant uniquement, et que vous devez configurer manuellement l’adresse de messagerie réécrite en tant qu’adresse proxy sur les destinataires concernés.</p>
<p>La valeur par défaut est <code>False</code>, mais vous devez la définir sur <code>True</code> si <em>InternalAddress</em> contient le caractère générique (*.contoso.com).</p>
<p>La valeur du paramètre <em>OutboundOnly</em> dans le fichier CSV est <code>True</code> ou <code>False</code>, et non pas <code>$True</code> ou <code>$False</code>.</p></td>
</tr>
</tbody>
</table>


Chaque ligne sous la ligne d’en-tête représente une entrée de réécriture d’adresses individuelle. Les valeurs de chaque ligne doivent respecter le même ordre que les noms de paramètres de la ligne d’en-tête. Les valeurs sont séparées par des virgules.

## Ce qu’il faut savoir avant de commencer

  - Durée d’exécution estimée de cette tâche : 30 minutes

  - Assurez-vous que vous comprenez ce qu’implique la réécriture d’adresses. Par exemple, l’adresse de messagerie réécrite doit être unique dans votre organisation Exchange, et il se peut que vous deviez configurer les adresses proxy sur les destinataires concernés. Pour plus d’informations, voir [Réécriture d’adresses sur des serveurs de transport Edge](address-rewriting-on-edge-transport-servers-exchange-2013-help.md) et [Gestion de la réécriture d’adresses sur les serveurs de transport Edge](manage-address-rewriting-on-edge-transport-servers-exchange-2013-help.md).

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l’entrée « Agent de réécriture d’adresses » dans la rubrique [Autorisations de flux de messagerie](mail-flow-permissions-exchange-2013-help.md).

  - Si vous disposez de plusieurs serveurs de transport Edge, nous vous recommandons d’utiliser les procédures décrites dans cette rubrique pour importer les entrées de réécriture d’adresses sur un serveur de transport Edge, puis de dupliquer la configuration de ce serveur de transport Edge sur les autres serveurs de transport Edge dans votre organisation. Pour plus d’informations sur la duplication d’un serveur de transport Edge, consultez la rubrique [Configuration clonée de serveur de transport Edge](edge-transport-server-cloned-configuration-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.


## Comment procéder ?

## Étape 1 : Créer le fichier CSV

Lorsque vous créez le fichier CSV, prenez en compte les éléments suivants :

  - Si vous spécifiez des valeurs pour les paramètres facultatifs du fichier CSV, chaque ligne doit inclure une valeur dans cette colonne. Si vous souhaitez créer plusieurs entrées de réécriture d’adresses où certaines entrées comportent des paramètres facultatifs et d’autres pas, vous devez les séparer dans deux fichiers CSV distincts, puis importer chacun d’eux séparément.

  - Si le fichier CSV contient des caractères non ASCII, veillez à l’enregistrer avec l’encodage UTF-8 ou un autre encodage Unicode. Selon l’application, l’enregistrement du fichier CSV avec l’encodage UTF-8 ou un autre encodage Unicode peut être facilité lorsque les paramètres régionaux système de l’ordinateur correspondent à la langue utilisée dans le fichier CSV.

L’exemple suivant montre comment renseigner un fichier CSV avec les paramètres *ExceptionList* et *OutboundOnly* facultatifs :

    Name,InternalAddress,ExternalAddress,ExceptionList,OutboundOnly
    "Wingtip UK",*.wingtiptoys.co.uk,tailspintoys.com,"legal.wingtiptoys.co.uk,finance.wingtiptoys.co.uk,support.wingtiptoys.co.uk",True
    "Wingtip USA",*.wingtiptoys.com,tailspintoys.com,"legal.wingtiptoys.com,finance.wingtiptoys.com,support.wingtiptoys.com,corp.wingtiptoys.com",True
    "Wingtip Canada",*.wingtiptoys.ca,tailspintoys.com,"legal.wingtiptoys.ca,finance.wingtiptoys.ca,support.wingtiptoys.ca",True

## Étape 2 : Importer le fichier CSV

Pour importer le fichier CSV, utilisez la syntaxe suivante :

    Import-Csv <FileNameAndPath> | ForEach {New-AddressRewriteEntry -Name $_.Name -InternalAddress $_.InternalAddress -ExternalAddress $_.ExternalAddress -OutboundOnly ([Bool]::Parse($_.OutboundOnly)) -ExceptionList $_.ExceptionList}

Cet exemple importe les entrées de réécriture d’adresses à partir de C:\\My Documents\\ImportAddressRewriteEntries.csv.

    Import-Csv "C:\My Documents\ImportAddressRewriteEntries.csv" | ForEach {New-AddressRewriteEntry -Name $_.Name -InternalAddress $_.InternalAddress -ExternalAddress $_.ExternalAddress -OutboundOnly ([Bool]::Parse($_.OutboundOnly)) -ExceptionList $_.ExceptionList}

## Comment savoir si cette étape a fonctionné ?

Pour vérifier que vous avez importé les entrées de réécriture d’adresses à partir d’un fichier CSV, procédez comme suit :

1.  Pour afficher toutes les entrées de réécriture d’adresses, exécutez la commande `Get-AddressRewriteEntry`.

2.  Pour voir plus de détails sur une entrée de réécriture d’adresses spécifique, exécutez la commande `Get-AddressRewriteEntry <AddressRewriteIdentity> | Format-List`

