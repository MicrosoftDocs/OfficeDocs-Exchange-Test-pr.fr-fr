---
title: 'Utilisation de la sortie de la commande: Exchange 2013 Help'
TOCTitle: Utilisation de la sortie de la commande
ms:assetid: 8320e1a5-d3f5-4615-878d-b23e2aaa6b1e
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb123533(v=EXCHG.150)
ms:contentKeyID: 50478587
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Utilisation de la sortie de la commande

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2015-03-09_

Exchange Management Shell offre plusieurs méthodes que vous pouvez utiliser pour mettre en forme la sortie de la commande. Cette rubrique aborde les sujets suivants :

  - How to format data   Vous pouvez contrôler la mise en forme des données que vous consultez en utilisant les cmdlets **Format-List**, **Format-Table** et **Format-Wide**.

  - How to output data   Vous pouvez déterminer si la sortie des données doit se faire vers la fenêtre de la console du Shell ou vers un fichier à l’aide des cmdlets **Out-Host** et **Out-File**. Cette rubrique contient un modèle de script permettant d’envoyer des données vers Microsoft Internet Explorer.

  - How to filter data   Vous pouvez filtrer les données à l’aide de l’une des méthodes de filtrage suivantes :
    
      - Filtrage côté serveur, disponible sur certaines cmdlets.
    
      - Filtrage côté client, disponible sur toutes les cmdlets en canalisant les résultats d’une commande vers la cmdlet **Where-Object**.

Pour utiliser les fonctionnalités décrites dans cette rubrique, vous devez maîtriser les concepts suivants :

  - [Traitement en pipeline](https://technet.microsoft.com/fr-fr/library/aa998260\(v=exchg.150\))

  - [Variables de l’environnement Shell](https://technet.microsoft.com/fr-fr/library/bb124036\(v=exchg.150\))

  - [Opérateurs de comparaison](https://technet.microsoft.com/fr-fr/library/bb125229\(v=exchg.150\))

## Mise en forme des données

Si vous appelez des cmdlets de mise en forme à la fin du pipeline, vous pouvez remplacer la mise en forme par défaut pour contrôler les données qui s’affichent et leur mode d’affichage. Les cmdlets de mise en forme sont **Format-List**, **Format-Table** et **Format-Wide**. Chaque cmdlet de mise en forme a un style de sortie distinct.

## Format-List

La cmdlet **Format-List** prend l’entrée dans le pipeline et produit une liste de colonnes verticale de toutes les propriétés spécifiées pour chaque objet. Vous pouvez spécifier la propriété que vous souhaitez afficher en utilisant le paramètre *Property*. Si la cmdlet **Format-List** est appelée sans spécification d’aucun paramètre, toutes les propriétés sont produites. La cmdlet **Format-List** insère des retours automatiques dans les lignes au lieu de les tronquer. L’une des meilleures utilisations de la cmdlet **Format-List** est la réécriture de la sortie par défaut d’une cmdlet afin que vous puissiez extraire des informations supplémentaires et plus spécifiques.

Par exemple, lorsque vous appelez la cmdlet **Get-Mailbox**, vous ne pouvez consulter qu’un nombre limité d’informations en format de tableau. Si vous canalisez la sortie de la cmdlet **Get-Mailbox** vers la cmdlet **Format-List** et ajoutez des paramètres pour obtenir les informations supplémentaires ou plus spécifiques que vous voulez consulter, vous pouvez extraire la sortie souhaitée.

Vous pouvez également spécifier un caractère générique « \* » avec un nom de propriété partiel. Si vous incluez un caractère générique, vous pouvez établir la correspondance entre des propriétés multiples sans devoir taper chaque nom de propriété individuellement. Par exemple, `Get-Mailbox | Format-List -Property Email* ` renvoie toutes les propriétés commençant par `Email`.

Les exemples suivants montrent les différentes manières dont vous pouvez consulter les mêmes données renvoyées par la cmdlet **Get-Mailbox** .

```powershell
Get-Mailbox TestUser1
    
Name                      Alias                ServerName       ProhibitSendQuo
                                                                    ta
----                      -----                ----------       ---------------
TestUser1                 TestUser1            mbx              unlimited
```

Dans ce premier exemple, la cmdlet **Get-Mailbox** est appelée sans mise en forme spécifique pour que la sortie par défaut soit au format tableau et qu’elle contienne un ensemble de propriétés prédéterminées.

```powershell
Get-Mailbox TestUser1 | Format-List -Property Name,Alias,EmailAddresses
```
    
```powershell
Name           : TestUser1
Alias          : TestUser1
EmailAddresses : {SMTP:TestUser1@contoso.com}
```

Dans le deuxième exemple, la sortie de la cmdlet **Get-Mailbox** est canalisée vers la cmdlet **Format-List**, avec des propriétés spécifiques. Comme vous pouvez le constater, la mise en forme et le contenu de la sortie sont sensiblement différents.

```powershell
Get-Mailbox TestUser1 | Format-List -Property Name, Alias, Email*

Name                      : Test User
Alias                     : TestUser1
EmailAddresses            : {SMTP:TestUser1@contoso.com}
EmailAddressPolicyEnabled : True
```

Dans le dernier exemple, la sortie de la cmdlet **Get-Mailbox** est canalisée vers le cmdlet **Format-List**, comme dans le deuxième exemple. Cependant, dans le dernier exemple, un caractère générique est utilisé pour faire correspondre toutes les propriétés commençant par `Email`.

Si plusieurs objets sont transmis à la cmdlet **Format-List**, toutes les propriétés spécifiées pour un objet sont affichées et regroupées par objet. L’ordre d’affichage dépend du paramètre par défaut de la cmdlet. Le paramètre par défaut est généralement *Name* ou *Identity*. Par exemple, lors de l’appel de la cmdlet **Get-Childitem**, l’ordre d’affichage par défaut est l’ordre alphabétique des noms de fichier. Pour modifier ce comportement, vous devez appeler la cmdlet **Format-List** avec le paramètre *GroupBy* et le nom d’une valeur de propriété en fonction de laquelle vous souhaitez regrouper la sortie. Par exemple, la commande suivante affiche la liste de tous les fichiers dans un répertoire et regroupe ces fichiers par extension.

```powershell
Get-Childitem | Format-List Name,Length -GroupBy Extension

    
    Extension: .xml
    
Name   : Config_01.xml
Length : 5627
    
Name   : Config_02.xml
Length : 3901
    
    
    Extension: .bmp
    
Name   : Image_01.bmp
Length : 746550
    
Name   : Image_02.bmp
Length : 746550
    
    
    Extension: .txt
    
Name   : Text_01.txt
Length : 16822
    
Name   : Text_02.txt
Length : 9835
```

Dans cet exemple, la cmdlet **Format-List** a regroupé les éléments par la propriété *Extension* spécifiée par le paramètre *GroupBy*. Vous pouvez utiliser le paramètre *GroupBy* avec n’importe quelle propriété valide pour les objets dans le flux du pipeline.

## Format-Table

La cmdlet **Format-Table** permet d’afficher des éléments dans un format tableau avec des en-têtes libellés et des colonnes de données de propriété. Par défaut, de nombreuses cmdlets, telles que **Get-Process** et **Get-Service**, utilisent le format tableau pour la sortie. Les paramètres de la cmdlet **Format-Table** incluent les paramètres *Properties* et *GroupBy*. Ces paramètres fonctionnent exactement comme avec la cmdlet **Format-List**.

La cmdlet **Format-Table** utilise également le paramètre *Wrap*. Ce paramètre permet l’affichage complet de longues lignes d’informations de propriété plutôt que de les tronquer à la fin de la ligne. Pour voir comment le paramètre *Wrap* est utilisé pour afficher les informations renvoyées, comparez la sortie de la commande **Get-Command** dans les deux exemples ci-après.

Dans le premier exemple, lorsque la cmdlet **Get-Command** est utilisée pour afficher les informations de la commande sur la cmdlet **Get-Process**, les informations de la propriété *Definition* sont tronquées.

```powershell
Get-Command Get-Process | Format-Table Name,Definition

    
    Name                                    Definition
    ----                                    ----------
```powershell
get-process                             get-process [[-ProcessName] String[]...
```

Dans le deuxième exemple, le paramètre *Wrap* est ajouté à la commande pour forcer l’affichage du contenu complet de la propriété *Definition*.

```powershell
Get-Command Get-Process | Format-Table Name,Definition -Wrap
    
Get-Process                             Get-Process [[-Name] <String[]>] [-Comp

                                            uterName <String[]>] [-Module] [-FileVe
                                            rsionInfo] [-Verbose] [-Debug] [-ErrorA
                                            ction <ActionPreference>] [-WarningActi
                                            on <ActionPreference>] [-ErrorVariable
                                            <String>] [-WarningVariable <String>] [
                                            -OutVariable <String>] [-OutBuffer <Int
                                            32>]
                                            Get-Process -Id <Int32[]> [-ComputerNam

                                            e <String[]>] [-Module] [-FileVersionIn
                                            fo] [-Verbose] [-Debug] [-ErrorAction <
                                            ActionPreference>] [-WarningAction <Act
                                            ionPreference>] [-ErrorVariable <String
                                            >] [-WarningVariable <String>] [-OutVar
                                            iable <String>] [-OutBuffer <Int32>]
                                            Get-Process [-ComputerName <String[]>]
                                            [-Module] [-FileVersionInfo] -InputObje
                                            ct <Process[]> [-Verbose] [-Debug] [-Er
                                            rorAction <ActionPreference>] [-Warning
                                            Action <ActionPreference>] [-ErrorVaria
                                            ble <String>] [-WarningVariable <String
                                            >] [-OutVariable <String>] [-OutBuffer
                                            <Int32>]
```

Tout comme avec la cmdlet **Format-List** vous pouvez spécifier un caractère générique « `*` » avec un nom de propriété partiel. En incluant un caractère générique, vous pouvez mettre en correspondance plusieurs propriétés sans taper chaque nom individuellement.

## Format-Wide

La cmdlet **Format-Wide** offre un contrôle de sortie plus simple que les autres cmdlets de format. Par défaut, la cmdlet **Format-Wide** tente d’afficher un maximum de valeurs de propriété dans une ligne de sortie. En ajoutant des paramètres, vous pouvez contrôler le nombre de colonnes et l’utilisation de l’espace de sortie.

Dans l’utilisation la plus élémentaire, l’appel de la cmdlet **Format-Wide** sans aucun paramètre dispose la sortie dans le nombre maximal de colonnes que la page peut accueillir. Par exemple, si vous exécutez la cmdlet **Get-Childitem** en canalisant sa sortie vers la cmdlet **Format-Wide**, les informations suivantes s’affichent :

```powershell
Get-ChildItem | Format-Wide
    
        Directory: FileSystem::C:\WorkingFolder
    
    Config_01.xml                           Config_02.xml
    Config_03.xml                           Config_04.xml
    Config_05.xml                           Config_06.xml
    Config_07.xml                           Config_08.xml
    Config_09.xml                           Image_01.bmp
    Image_02.bmp                            Image_03.bmp
    Image_04.bmp                            Image_05.bmp
    Image_06.bmp                            Text_01.txt
    Text_02.txt                             Text_03.txt
    Text_04.txt                             Text_05.txt
    Text_06.txt                             Text_07.txt
    Text_08.txt                             Text_09.txt
    Text_10.txt                             Text_11.txt
    Text_12.txt
```

Généralement, l’appel de la cmdlet **Get-Childitem** sans aucun paramètre affiche les noms de tous les fichiers du répertoire dans un tableau de propriétés. Dans cet exemple, en canalisant la sortie de la cmdlet **Get-Childitem** vers la cmdlet **Format-Wide**, la sortie a été affichée dans deux colonnes de noms. Notez qu’un seul type de propriété peut être affiché à la fois, spécifié par un nom de la propriété qui suit la cmdlet **Format-Wide**. Si vous ajoutez le paramètre *Autosize*, la sortie passe de deux colonnes à autant de colonnes que le permet la largeur de l’écran.

```powershell
Get-ChildItem | Format-Wide -AutoSize
    
        Directory: FileSystem::C:\WorkingFolder
    
    Config_01.xml   Config_02.xml   Config_03.xml   Config_04.xml   Config_05.xml
    Config_06.xml   Config_07.xml   Config_08.xml   Config_09.xml   Image_01.bmp
    Image_02.bmp    Image_03.bmp    Image_04.bmp    Image_05.bmp    Image_06.bmp
    Text_01.txt     Text_02.txt     Text_03.txt     Text_04.txt     Text_05.txt
    Text_06.txt     Text_07.txt     Text_08.txt     Text_09.txt     Text_10.txt
    Text_11.txt     Text_12.txt
```

Dans cet exemple, le tableau contient cinq colonnes au lieu de deux. Le paramètre *Column* offre un contrôle supplémentaire en vous permettant de spécifier le nombre maximal de colonnes pour afficher les informations comme suit :

```powershell
Get-ChildItem | Format-Wide -Column 4
    
        Directory: FileSystem::C:\WorkingFolder
    
    Config_01.xml       Config_02.xml       Config_03.xml       Config_04.xml
    Config_05.xml       Config_06.xml       Config_07.xml       Config_08.xml
    Config_09.xml       Image_01.bmp        Image_02.bmp        Image_03.bmp
    Image_04.bmp        Image_05.bmp        Image_06.bmp        Text_01.txt
    Text_02.txt         Text_03.txt         Text_04.txt         Text_05.txt
    Text_06.txt         Text_07.txt         Text_08.txt         Text_09.txt
    Text_10.txt         Text_11.txt         Text_12.txt
```

Dans cet exemple, le nombre de colonnes est fixé à quatre à l’aide du paramètre *Column*.

## Sortie des données

## Cmdlets Out-Host et Out-File

La cmdlet **Out-Host** est une cmdlet invisible par défaut à la fin du pipeline. Après l’application de toute mise en forme, la cmdlet **Out-Host** envoie la sortie finale à la fenêtre de la console pour affichage. Il n’est pas nécessaire d’appeler explicitement la cmdlet **Out-Host** car il s’agit de la sortie par défaut. Vous pouvez réécrire l’envoi de la sortie vers la fenêtre de la console en appelant la cmdlet **Out-File** comme dernière cmdlet de la commande. La cmdlet **Out-File** écrit alors la sortie dans le fichier que vous spécifiez dans la commande, comme dans l’exemple suivant :

```powershell
Get-ChildItem | Format-Wide -Column 4 | Out-File c:\OutputFile.txt
```

Dans cet exemple, la cmdlet **Out-File** écrit les informations affichées dans la commande **Get-ChildItem | Format-Wide -Column 4** dans un fichier nommé `OutputFile.txt`. Vous pouvez également rediriger la sortie du pipeline vers un fichier en utilisant l’opérateur de redirection, à savoir le signe plus grand que ( `>` ). Pour ajouter la sortie du pipeline d’une commande à un fichier existant sans remplacer le fichier original, utilisez deux signes plus grand que ( `>>` ), comme dans l’exemple suivant :

```powershell
Get-ChildItem | Format-Wide -Column 4 >> C:\OutputFile.txt
```

Dans cet exemple, la sortie de la cmdlet **Get-Childitem** est canalisée vers la cmdlet **Format-Wide** à des fins de mise en forme, puis écrit dans le fichier `OutputFile.txt`. Notez que si le fichier `OutputFile.txt` n’existait pas, l’utilisation des deux signes plus grand que ( `>>` ) entraîne la création du fichier.

Pour plus d’informations sur les pipelines, consultez la rubrique [Traitement en pipeline](https://technet.microsoft.com/fr-fr/library/aa998260\(v=exchg.150\)).

Pour plus d’informations sur la syntaxe utilisée dans les exemples précédents, consultez la [Syntaxe](https://technet.microsoft.com/fr-fr/library/bb123552\(v=exchg.150\)).

## Affichage de données dans Internet Explorer

Étant donné la flexibilité et la facilité de script dans Exchange Management Shell, vous pouvez prendre les données renvoyées par les commandes, les mettre en forme et les sortir d’un nombre de façons quasiment illimité.

L’exemple suivant montre comment vous pouvez utiliser un script unique pour sortir les données renvoyées par une commande et les afficher dans Internet Explorer. Ce script prend les objets transmis via le pipeline, ouvre une fenêtre Internet Explorer, puis affiche les données dans Internet Explorer :

```powershell
$Ie = New-Object -Com InternetExplorer.Application
$Ie.Navigate("about:blank")
While ($Ie.Busy) { Sleep 1 }
$Ie.Visible = $True
$Ie.Document.Write("$Input")
# If the previous line doesn't work on your system, uncomment the line below.
# $Ie.Document.IHtmlDocument2_Write("$Input")
$Ie
```

Pour utiliser ce script, sauvegardez-le dans le répertoire `C:\Program Files\Microsoft\Exchange Server\V15\Scripts` sur l’ordinateur sur lequel le script est exécuté. Nommez le fichier `Out-Ie.ps1`. Une fois le fichier enregistré, vous pouvez utiliser le script comme une cmdlet ordinaire.

> [!NOTE]
> Pour exécuter des scripts dans Exchange 2013, ceux-ci doivent faire partie d’un rôle de gestion non délimité et ce rôle doit vous être attribué directement ou via un groupe de rôles de gestion. Pour plus d’informations, voir <a href="understanding-management-roles-exchange-2013-help.md">Présentation des rôles de gestion</a>.


Le script `Out-Ie` suppose que les données reçues sont dans un code HTML valide. Pour convertir les données à afficher en HTML, vous devez canaliser les résultats de votre commande vers la cmdlet **ConvertTo-Html**. Vous pouvez alors canaliser les résultats de cette commande vers le script `Out-Ie`. L’exemple suivant montre comment afficher une liste de répertoires dans une fenêtre d’Internet Explorer :

```powershell
Get-ChildItem | Select Name,Length | ConvertTo-Html | Out-Ie
```

## Procédure de filtrage de données

L’environnement Shell vous donne accès à un volume important d’informations sur vos serveurs, vos boîtes aux lettres, Active Directory et d’autres objets de votre organisation. Bien que l’accès à ces informations vous permette de mieux comprendre votre environnement, ce volume d’informations risque de vous submerger. Le Shell permet de contrôler ces informations et de ne renvoyer que les données que vous souhaitez en utilisant un filtrage. Les types de filtrage ci-après sont disponibles :

  - **Filtrage côté serveur**   Le filtrage côté serveur prend le filtre que vous spécifiez dans la ligne de commande et le soumet au serveur Exchange que vous interrogez. Ce serveur traite la requête et ne renvoie que les données correspondant au filtre que vous avez spécifié.
    
    Le filtrage côté serveur n’est appliqué qu’à des objets pour lequels des dizaines voire des centaines de milliers de résultats pourraient être retournés. Ainsi, seules les cmdlets de gestion des destinataires, telles que la cmdlet **Get-Mailbox**, et les cmdlets de gestion de file d’attente, telles que la cmdlet **Get-Queue**, prennent en charge le filtrage coté serveur. Ces cmdlets prennent en charge le paramètre *Filter*. Ce paramètre prend l’expression de filtrage que vous spécifiez et la soumet au serveur pour traitement.

  - **Filtrage côte client**   Le filtrage côté client s’effectue sur les objets de la fenêtre de console locale dans laquelle vous travaillez. Lorsque vous utilisez le filtrage côté client, la cmdlet extrait tous les objets correspondant à la tâche que vous effectuez vers la fenêtre de console locale. Le Shell prend alors tous les résultats retournés, applique le filtrage coté client à ces résultats, puis ne renvoie que les résultats correspondant à votre filtre. Toutes les cmdlets prennent en charge le filtrage côté client. Ce filtrage est appelé en canalisant les résultats d’une commande vers la cmdlet **Where-Object**.

## Filtrage côté serveur

La mise en œuvre du filtrage côté serveur est spécifique à la cmdlet qui le prend en charge. Le filtrage côté serveur n’est activé que pour des propriétés spécifiques des objets retournés. Pour plus d’informations, consultez l'aide pour les cmdlets suivantes :


<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Get-ActiveSyncDevice</p></td>
<td><p>Get-ActiveSyncDeviceClass</p></td>
<td><p>Get-CASMailbox</p></td>
<td><p>Get-Contact</p></td>
<td><p>Get-DistributionGroup</p></td>
</tr>
<tr class="even">
<td><p>Get-DynamicDistributionGroup</p></td>
<td><p>Get-Group</p></td>
<td><p>Get-Mailbox</p></td>
<td><p>Get-MailboxStatistics</p></td>
<td><p>Get-MailContact</p></td>
</tr>
<tr class="odd">
<td><p>Get-MailPublicFolder</p></td>
<td><p>Get-MailUser</p></td>
<td><p>Get-Message</p></td>
<td><p>Get-MobileDevice</p></td>
<td><p>Get-Queue</p></td>
</tr>
<tr class="even">
<td><p>Get-QueueDigest</p></td>
<td><p>Get-Recipient</p></td>
<td><p>Get-RemoteMailbox</p></td>
<td><p>Get-RoleGroup</p></td>
<td><p>Get-SecurityPrincipal</p></td>
</tr>
<tr class="odd">
<td><p>Get-StoreUsageStatistics</p></td>
<td><p>Get-UMMailbox</p></td>
<td><p>Get-User</p></td>
<td><p>Get-UserPhoto</p></td>
<td><p>Remove-Message</p></td>
</tr>
<tr class="even">
<td><p>Resume-Message</p></td>
<td><p>Resume-Queue</p></td>
<td><p>Retry-Queue</p></td>
<td><p>Suspend-Message</p></td>
<td><p>Suspend-Queue</p></td>
</tr>
</tbody>
</table>


## Filtrage côté client

Le filtrage côté client peut être utilisé avec n’importe quelle cmdlet. Cette fonction comprend les cmdlets qui prennent également en charge le filtrage côté serveur. Comme décrit ci-avant dans cette rubrique, le filtrage côté client accepte toutes les données renvoyées par une commande précédente dans le pipeline, puis renvoie uniquement les résultats correspondant au filtre que vous spécifiez. La cmdlet **Where-Object** exécute ce filtrage. Vous pouvez l’abréger en **Where**.

Lorsque les données transitent dans le pipeline, la cmdlet **Where** reçoit les données de l’objet précédent, puis les filtre avant de les transmettre à l’objet suivant. Le filtrage est basé sur un bloc de scripts défini dans la commande **Where**. Le bloc de scripts filtre les données sur la base des propriétés et des valeurs de l’objet.

La cmdlet **Clear-Host** permet de nettoyer la fenêtre de la console. Dans cet exemple, vous trouvez tous les alias définis pour la cmdlet **Clear-Host** en exécutant la commande suivante :

```powershell
Get-Alias | Where {$_.Definition -eq "Clear-Host"}
 
    CommandType     Name                            Definition
    -----------     ----                            ----------
    Alias           clear                           clear-host
    Alias           cls                             clear-host
```

La cmdlet **Get-Alias** et la commande **Where** fonctionnent conjointement pour renvoyer la liste des alias définis pour la cmdlet **Clear-Host** et pour aucune autre cmdlet. Le tableau suivant décrit brièvement chaque élément de la commande **Where** utilisée dans l’exemple.

### Éléments de la commande Where

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Éléments</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>{ }</code></p></td>
<td><p>Les accolades entourent le bloc de scripts qui définit le filtre.</p></td>
</tr>
<tr class="even">
<td><p><code>$_</code></p></td>
<td><p>Cette variable spéciale se lie automatiquement aux objets dans le pipeline.</p></td>
</tr>
<tr class="odd">
<td><p><code>Definition</code></p></td>
<td><p>La propriété <code>Definition</code> est la propriété des objets figurant dans le pipeline en cours qui stocke le nom de la définition de l’alias. En cas d’utilisation de <code>Definition</code> avec la variable <code>$_</code>, un point est placé devant le nom de la propriété.</p></td>
</tr>
<tr class="even">
<td><p><code>-eq</code></p></td>
<td><p>Cet opérateur de comparaison « égal à » permet de spécifier que les résultats doivent correspondre précisément à la valeur de propriété indiquée dans l’expression.</p></td>
</tr>
<tr class="odd">
<td><p>&quot;<strong>Clear-Host</strong>&quot;</p></td>
<td><p>Dans cet exemple, « <strong>Clear-Host</strong> » est la valeur que la commande analyse.</p></td>
</tr>
</tbody>
</table>


Dans l’exemple, les objets retournés par la cmdlet **Get-Alias** représentent tous les alias définis dans le système. Bien qu’ils soient invisibles depuis la ligne de commandes, les alias sont collectés et transmis à la cmdlet **Where** à travers le pipeline. La cmdlet **Where** utilise les informations du bloc de scripts pour appliquer un filtre aux alias d’objets.

La variable spéciale `$`\_ représente les objets qui sont transmis. La variable `$_` est automatiquement initiée par le Shell et est liée à l’objet pipeline actuel. Pour plus d’informations sur cette variable spéciale, consultez la rubrique [Variables de l’environnement Shell](https://technet.microsoft.com/fr-fr/library/bb124036\(v=exchg.150\)).

Avec la notation « point » (objet.propriété.) standard, la propriété `Definition` est ajoutée pour définir la propriété exacte de l’objet à évaluer. L’opérateur de comparaison `-eq` compare ensuite la valeur de cette propriété à `"Clear-Host"`. Seuls les objets ayant la propriété `Definition` correspondant à ce critère sont transmis à la fenêtre de la console pour la sortie. Pour plus d’informations sur les opérateurs de comparaison, consultez la rubrique [Opérateurs de comparaison](https://technet.microsoft.com/fr-fr/library/bb125229\(v=exchg.150\)).

Après que la commande **Where** a filtré les objets retournés par la cmdlet **Get-Alias**, vous pouvez canaliser les objets filtrés vers une autre commande. La commande suivante traite uniquement les objets filtrés retournés par la commande Where.

