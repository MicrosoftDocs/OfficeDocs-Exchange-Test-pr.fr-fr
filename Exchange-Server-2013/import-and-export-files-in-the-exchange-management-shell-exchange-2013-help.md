---
title: 'Importation et exportation de fichiers dans l’environnement de ligne de commande Exchange Management Shell: Exchange 2013 Help'
TOCTitle: Importation et exportation de fichiers dans l’environnement de ligne de commande Exchange Management Shell
ms:assetid: b4b669e8-a3aa-4b0b-ad34-f1f15d9c9369
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dd638170(v=EXCHG.150)
ms:contentKeyID: 50555482
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Importation et exportation de fichiers dans l’environnement de ligne de commande Exchange Management Shell

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2015-03-09_

Microsoft Exchange Server 2013 utilise l’interface de ligne de commande Windows PowerShell à distance pour établir une connexion entre le serveur et la station de travail à partir de laquelle vous administrez Exchange et le serveur qui exécute Exchange 2013 que vous administrez. Dans Exchange 2013, ceci est appelé l’environnement de ligne de commande Exchange Management Shell distant. Même si vous administrez le serveur Exchange 2013 local, l'environnement de ligne de commande Exchange Management Shell distant permet d'établir la connexion. Pour plus d'informations sur l'environnement de ligne de commande Exchange Management Shell local et distant, voir [Utilisation de PowerShell avec Exchange 2013 (Exchange Management Shell)](https://technet.microsoft.com/fr-fr/library/bb123778\(v=exchg.150\)).

La manière dont vous importez ou exportez des fichiers vers ou à partir d’un serveur Exchange dans Exchange 2013 diffère de la manière avec laquelle vous aviez procédé dans Exchange Server 2007. Ceci est dû à l’utilisation de l’environnement de ligne de commande Exchange Management Shell distant dans Exchange 2013. Cette rubrique explique pourquoi ce nouveau processus est requis et comment importer et exporter des fichiers entre un serveur ou une station de travail locale et un serveur Exchange 2013.

## Sessions Windows PowerShell

Pour comprendre pourquoi vous avez besoin d'une syntaxe spéciale pour importer et exporter des fichiers dans l'environnement de ligne de commande Exchange Management Shell distant, vous devez savoir comment l'environnement est implémenté dans Exchange 2013. L'environnement distant utilise des sessions Windows PowerShell, qui sont les environnements dans lesquels les variables, cmdlets, et autres, peuvent partager des informations. Chaque fois que vous ouvrez une nouvelle fenêtre de l'environnement de ligne de commande Exchange Management Shell, vous créez une session. Les cmdlets qui sont exécutées dans chaque fenêtre peuvent accéder à des variables et à d'autres informations stockées dans cette fenêtre, mais elles ne peuvent pas accéder aux variables dans d'autres fenêtres ouvertes de l'environnement de ligne de commande Exchange Management Shell. Cela est dû au fait que les variables appartiennent chacune à une session Windows PowerShell qui leur est propre. Les sessions Windows PowerShell peuvent également être appelées instances d'exécution.

L'environnement de ligne de commande Exchange Management Shell distant dans Exchange 2013 comporte deux types de session, la session locale et la session distante. La session locale est la session Windows PowerShell qui est exécutée sur votre ordinateur local. Cette session contient toutes les cmdlets fournies avec Windows PowerShell. Elle a également accès à votre système de fichiers local.

La session distante est la session Windows PowerShell qui est exécutée sur le serveur Exchange distant. Cette session est celle où toutes les cmdlets Exchange sont exécutées. Elle a accès au système de fichiers du serveur Exchange.

Lorsque vous vous connectez à un serveur Exchange distant, une connexion est établie entre la session locale sur votre ordinateur et la session distante sur le serveur Exchange. Cette connexion vous permet d'exécuter les cmdlets Exchange sur le serveur Exchange distant dans votre session locale même si aucune cmdlet Exchange n'est installée sur votre ordinateur local. Bien que les cmdlets Exchange semblent s’exécuter sur votre ordinateur local, elles sont en réalité exécutées sur le serveur Exchange.

> [!NOTE]
> Même si vous ouvrez l'environnement de ligne de commande Exchange Management Shell sur un serveur Exchange 2013, le même processus de connexion a lieu et deux sessions sont créées. En d’autres termes, vous devez utiliser la même nouvelle syntaxe pour importer et exporter des fichiers lorsque vous ouvrez l’environnement de ligne de commande Exchange Management Shell sur un serveur Exchange 2013 ou à partir d’une station de travail client distante.


Les cmdlets Exchange qui sont exécutées dans la session distante sur le serveur Exchange distant n'ont pas accès à votre système de fichiers local. Vous ne pouvez donc pas utiliser les cmdlets Exchange seules pour importer ou exporter des fichiers depuis ou vers votre système de fichiers local. Vous devez utiliser une syntaxe supplémentaire pour cela. Ainsi les cmdlets Exchange exécutées sur le serveur Exchange distant pourront utiliser les données du système de fichiers. Pour plus d’informations sur la syntaxe requise, voir « Importation et exportation de fichiers dans l’environnement de ligne de commande Exchange Management Shell distant » plus loin dans cette rubrique.

## Importation et exportation de fichiers dans l’environnement de ligne de commande Exchange Management Shell distant

L’importation et l’exportation de fichiers nécessitent une syntaxe spécifique parce que les serveurs de boîtes aux lettres et d’accès au client utilisent l’environnement de ligne de commande Exchange Management Shell distant et ne disposent pas d’un accès au système de fichiers de l’ordinateur local.

## Importation de fichiers dans l’environnement de ligne de commande Exchange Management Shell distant

La syntaxe pour importer des fichiers dans Exchange 2013 est utilisée à chaque fois que vous voulez envoyer un fichier à une cmdlet exécutée sur un serveur Exchange 2013 à partir de votre ordinateur ou serveur local. Les cmdlets qui acceptent des données provenant d'un fichier sur un ordinateur local doivent comporter un paramètre appelé *FileData* (ou un paramètre similaire). Pour déterminer le paramètre approprié à utiliser, consultez les informations d'aide pour la cmdlet que vous utilisez.

L'environnement de ligne de commande Exchange Management Shell doit savoir quel fichier vous souhaitez envoyer à la cmdlet Exchange 2013 et quel paramètre acceptera les données. Pour cela, utilisez la syntaxe suivante :

    <Cmdlet> -FileData ([Byte[]]$(Get-Content -Path <local path to file> -Encoding Byte -ReadCount 0))

Par exemple, la commande suivante importe le fichier C:\\MyData.dat dans le paramètre *FileData* sur la cmdlet fictive **Import-SomeData**.

    Import-SomeData -FileData (Byte[]]$(Get-Content -Path "C:\MyData.dat" -Encoding Byte -ReadCount 0))

Voici ce qui se produit lorsque la commande est exécutée :

1.  La commande est acceptée par l'environnement de ligne de commande Exchange Management Shell distant.

2.  L'environnement de ligne de commande Exchange Management Shell distant évalue la commande et détermine qu'une commande est incorporée à la valeur fournie au paramètre *FileData*.

3.  L'environnement de ligne de commande Exchange Management Shell distant interrompt l'évaluation de la commande **Import-SomeData** et exécute la commande **Get-Content**. La commande **Get-Content** lit les données du fichier MyData.dat.

4.  L'environnement de ligne de commande Exchange Management Shell distant stocke temporairement les données de la commande **Get-Content** sous forme d'objet `Byte[]` pour les transférer à la cmdlet **Import-SomeData**.

5.  L'exécution de la commande **Import-SomeData** reprend. L'environnement de ligne de commande Exchange Management Shell distant envoie la demande d'exécution de la cmdlet **Import-SomeData** au serveur Exchange 2013 distant ainsi que l'objet créé par la cmdlet **Get-Content**.

6.  La cmdlet **Import-SomeData** est exécutée sur le serveur Exchange 2013 distant et les données stockées dans l'objet temporaire créé par la cmdlet **Get-Content** sont transmises au paramètre *FileData*. La cmdlet **Import-SomeData** traite ces données et effectue les actions requises.

Certaines cmdlets utilisent la syntaxe alternative suivante qui accomplit la même chose que la syntaxe précédente.

    [Byte[]]$Data = Get-Content -Path <local path to file> -Encoding Byte -ReadCount 0
    Import-SomeData -FileData $Data

Le même processus se produit avec cette syntaxe. La seule différence étant qu'au lieu d'effectuer l'opération entière immédiatement, les données récupérées du fichier local sont stockées dans une variable créée à cet effet qui peut ensuite être référencée. La variable est alors utilisée dans la commande d'importation pour transmettre le contenu du fichier local à la cmdlet **Import-SomeData**. Ce processus à deux étapes est utile lorsque vous voulez utiliser les données du fichier local dans plusieurs commandes.

Vous devez tenir compte d'un certain nombre de limites lors de l'importation de fichiers. Pour plus d’informations, consultez la section « Limites relatives à l’importation de fichiers » plus loin dans cette rubrique.

Pour des informations spécifiques sur l'importation de données dans Exchange 2013, voir les rubriques d'aide pour la fonctionnalité que vous gérez.

## Limites relatives à l’importation de fichiers

Des limites peuvent être définies lors de l'importation de données dans l'environnement de ligne de commande Exchange Management Shell distant pour préserver l'intégrité des données transférées. Les transferts en cours ne peuvent pas reprendre s'ils ont été interrompus. En outre, étant donné que les données transférées sont stockées dans la mémoire du serveur distant, celui-ci doit être préservé d'un épuisement possible de la mémoire causé par des volumes de données trop importants.

Pour ces raisons, le volume des données transférées à un serveur Exchange 2013 distant depuis un serveur ou un ordinateur local est limité comme suit :

  - 500 mégaoctets (Mo) pour chaque cmdlet exécutée

  - 75 Mo pour chaque objet transféré à une cmdlet

Si vous dépassez l'une de ces limites, l'exécution de la cmdlet et de son pipeline associé s'arrêtera et vous recevrez un message d'erreur. Les exemples dans le tableau suivant vous aideront à comprendre le fonctionnement de ces limites.

### Exemples de limite d'importation de données

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Nombre d'objets</th>
<th>Taille par objet (Mo)</th>
<th>Taille totale (Mo)</th>
<th>Résultat de l'opération</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>10</p></td>
<td><p>40</p></td>
<td><p>400</p></td>
<td><p>L'opération a réussi, car ni la taille de chaque objet, ni le volume total des données transmises à la cmdlet ne dépasse leur limite respective de 75 Mo et 500 Mo.</p></td>
</tr>
<tr class="even">
<td><p>5</p></td>
<td><p>80</p></td>
<td><p>400</p></td>
<td><p>L'opération échoue, car bien que le volume total des données transmises à la cmdlet ne soit que de 400 Mo, la taille de chaque objet dépasse la limite autorisée de 75 Mo.</p></td>
</tr>
<tr class="odd">
<td><p>120</p></td>
<td><p>5</p></td>
<td><p>600</p></td>
<td><p>L'opération échoue car, bien que la taille de chaque objet soit seulement 5 Mo, le volume total des données transmises à la cmdlet dépasse la limite autorisée de 500 Mo.</p></td>
</tr>
</tbody>
</table>


En raison des limites de taille appliquées au volume des données pouvant être transférées entre un serveur Exchange 2013 distant et un ordinateur local, toutes les cmdlets ne prennent plus en charge l'importation de données. Pour déterminer si une cmdlet spécifique prend en charge l'importation de données, consultez les informations d'aide de cette cmdlet.

Ces limites doivent convenir à la majorité des opérations normales pouvant être effectuées sur un serveur Exchange 2013. Si les limites sont abaissées, certaines opérations normales risquent d'échouer, car elles dépasseront les nouvelles limites. Si les limites sont élevées, le transfert des données pourra prendre plus de temps et aura plus de chance d'être interrompu dû à un certain nombre de conditions temporaires. En outre, vous risquez d'épuiser la mémoire sur le serveur distant si vous n'avez pas installé suffisamment de mémoire sur ce serveur pour lui permettre de stocker le bloc de données entier au cours du transfert. Chaque possibilité peut entraîner la perte de données. Par conséquent, nous vous conseillons de ne pas changer les limites par défaut.

## Exportation de fichiers dans l’environnement de ligne de commande Exchange Management Shell distant

La syntaxe pour exporter les fichiers dans Exchange 2013 est utilisée à chaque fois que vous voulez accepter les données d'une cmdlet exécutée sur un serveur Exchange 2013 distant et stocker les données sur votre ordinateur ou serveur local. Les cmdlets qui fournissent des données que vous pouvez enregistrer dans un fichier local produisent un objet qui contient la propriété **FileData** (ou une propriété similaire). En fonction de la cmdlet, la propriété **FileData** est uniquement renseignée sur l'objet qui est produit dans certaines situations. Pour déterminer la propriété appropriée à utiliser et dans quelle situation, consultez les informations d'aide pour la cmdlet que vous utilisez.

L'environnement de ligne de commande Exchange Management Shell doit savoir que vous souhaitez enregistrer les données stockées dans la propriété **FileData** sur votre ordinateur local. Pour cela, utilisez la syntaxe suivante :

    <cmdlet> | ForEach { $_.FileData | Add-Content <local path to file> -Encoding Byte }

Par exemple, la commande suivante exporte les données stockées dans la propriété **FileData** sur l'objet créé par la cmdlet fictive **Export-SomeData**. Les données exportées sont stockées dans un fichier que vous spécifiez sur l'ordinateur local, dans ce cas MyData.dat.

> [!NOTE]
> Cette procédure utilise la cmdlet <strong>ForEach</strong>, des objets et le traitement en pipeline. Pour plus d’informations, consultez les rubriques <a href="https://technet.microsoft.com/fr-fr/library/aa998260(v=exchg.150)">Traitement en pipeline</a> et <a href="https://technet.microsoft.com/fr-fr/library/aa996386(v=exchg.150)">Données structurées</a>.


    Export-SomeData | ForEach { $_.FileData | Add-Content C:\MyData.dat -Encoding Byte }

Voici ce qui se produit lorsque la commande est exécutée :

1.  La commande est acceptée par l'environnement de ligne de commande Exchange Management Shell distant.

2.  L'environnement de ligne de commande Exchange Management Shell distant appelle la cmdlet **Export-SomeData** sur le serveur Exchange 2013 distant.

3.  L'objet créé par la cmdlet **Export-SomeData** est retransmis à la session locale de l'environnement de ligne de commande Exchange Management Shell via the pipeline.

4.  L'objet est ensuite transmis via le pipeline à la cmdlet **ForEach** qui dispose d'un bloc de script.

5.  Dans ce bloc de script, la propriété **FileData** sur l'objet actuel dans le pipeline est sélectionnée. Les données contenues dans la propriété **FileData** sont transmises à la cmdlet **Add-Content** via le pipeline.

6.  La cmdlet **Add-Content** enregistre les données transmises de la propriété **FileData** au fichier MyData.dat sur le système de fichiers local.

Pour des informations spécifiques sur l'exportation de données depuis Exchange 2013, voir les rubriques d'aide pour la fonctionnalité que vous gérez.

