---
title: "Exportation de messages de files d'attente: Exchange 2013 Help"
TOCTitle: Exportation de messages de files d'attente
ms:assetid: 688b342c-f380-4fe0-afce-7e38cf490627
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Aa998625(v=EXCHG.150)
ms:contentKeyID: 51407198
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Exportation de messages de files d'attente

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2014-05-05_

Lorsque vous exportez un message d'une file d'attente vers un fichier, le message n'est pas supprimé de la file d'attente. Une copie du message est faite dans la localisation spécifiée comme un fichier de texte en clair. Le fichier résultant peut être affiché dans une application, comme un éditeur de texte ou une application cliente de messagerie, ou le fichier de message peut être soumis de nouveau en utilisant le répertoire de relecture sur tout autre serveur de boîtes aux lettres ou serveur de transport Edge à l'intérieur ou à l'extérieur de l'organisation Exchange.

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée de chaque procédure : 15 minutes

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l'entrée « Files d'attente » dans la rubrique [Autorisations de flux de messagerie](mail-flow-permissions-exchange-2013-help.md).

  - Pour que le processus d'exportation réussisse, les messages doivent être dans un état Suspendu. Vous pouvez exporter des messages à partir de files d'attente de remise, de la file d'attente Inaccessible ou de la file d'attente de messages incohérents. Les messages se trouvant dans la file d'attente de messages incohérents sont déjà suspendus. Vous ne pouvez pas suspendre ou exporter des messages dans la file d'attente de soumission.

  - Vous ne pouvez pas utiliser l'Afficheur des files d'attente de la boîte à outils Exchange pour exporter des messages. Toutefois, vous pouvez utiliser l'Afficheur des files d'attente pour localiser, identifier et suspendre les messages avant de les exporter à l'aide de l'environnement de ligne de commande Exchange Management Shell.

  - Vérifiez les informations suivantes relatives à l'emplacement du répertoire cible des fichiers de messages :
    
      - Le répertoire cible doit exister avant d'exporter les messages. Le répertoire n'est pas créé automatiquement. Si aucun chemin absolu n'est spécifié, le répertoire de travail actuel de l'environnement de ligne de commande Exchange Management Shell est utilisé.
    
      - Le chemin peut être un chemin local du serveur Exchange ou un chemin UNC (Universal Naming Convention) d'un partage sur un serveur distant.
    
      - Votre compte doit disposer d'une autorisation en **écriture** sur le répertoire cible.
    
      - Quand vous spécifiez un nom de fichier pour les messages exportés, assurez-vous que vous incluez l'extension de nom du fichier .eml de sorte que les fichiers puissent être ouverts facilement par les applications clientes de messagerie ou correctement traités par le répertoire de relecture.

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

<table>
<thead>
<tr class="header">
<th><img src="images/Bb125224.tip(EXCHG.150).gif" title="Conseil" alt="Conseil" />Conseil :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.</td>
</tr>
</tbody>
</table>


## Que souhaitez-vous faire ?

## Utilisation du Shell pour exporter un message spécifique à partir d'une file d'attente spécifique

Pour exporter un message spécifique à partir d'une file d'attente précise, exécutez la commande suivante :

    Export-Message -Identity <MessageIdentity> | AssembleMessage -Path <FilePath>\<FileName>.eml

Cet exemple indique comment exporter une copie d'un message dont la valeur **InternalMessageID** est 1234 et qui est situé dans la file d'attente de remise contoso.com sur le serveur Mailbox01 vers le fichier intitulé export.eml avec le chemin d'accès D:\\Contoso Export.

    Export-Message -Identity Exchange01\Contoso.com\1234 | AssembleMessage -Path "D:\Contoso Export\export.eml"

## Utilisation du Shell pour exporter tous les messages à partir d'une file d'attente spécifique

La syntaxe suivante vous permet d'exporter tous les messages d'une file d'attente spécifique et d'utiliser la valeur **InternetMessageID** de chaque message comme nom de fichier :

    Get-Message -Queue <QueueIdentity> | ForEach-Object {$Temp=<Path>+$_.InternetMessageID+".eml";$Temp=$Temp.Replace("<","_");$Temp=$Temp.Replace(">","_");Export-Message $_.Identity | AssembleMessage -Path $Temp}

Notez que la valeur **InternetMessageID** contient des chevrons (\> et \<) qui doivent être supprimés dans la mesure où ils ne sont pas acceptés dans les noms de fichiers.

Cet exemple indique comment exporter une copie de tous les messages de la file d'attente de remise contoso.com sur le serveur Mailbox01 vers le répertoire local D:\\Contoso Export.

    Get-Message -Queue Mailbox01\Contoso.com | ForEach-Object {$Temp="D:\Contoso Export\"+$_.InternetMessageID+".eml";$Temp=$Temp.Replace("<","_");$Temp=$Temp.Replace(">","_");Export-Message $_.Identity | AssembleMessage -Path $Temp}

## Utilisation du Shell pour exporter des messages spécifiques à partir de toutes les files d'attente d'un serveur

La syntaxe suivante vous permet d'exporter des messages spécifiques de toutes les files d'attente d'un serveur et d'utiliser la valeur **InternetMessageID** de chaque message comme nom de fichier :

    Get-Message -Filter {<MessageFilter>} [-Server <ServerIdentity>] | ForEach-Object {$Temp=<Path>+$_.InternetMessageID+".eml";$Temp=$Temp.Replace("<","_");$Temp=$Temp.Replace(">","_");Export-Message $_.Identity | AssembleMessage -Path $Temp}

Notez que la valeur **InternetMessageID** contient des chevrons (\> et \<) qui doivent être supprimés dans la mesure où ils ne sont pas acceptés dans les noms de fichiers.

Cet exemple indique comment exporter une copie de tous les messages en provenance d'expéditeurs se trouvant dans le domaine contoso.com à partir de toutes les files d'attente sur le serveur Mailbox01 vers le répertoire local D:\\Contoso Export.

    Get-Message -Filter {FromAddress -like "*@contoso.com"} -Server Mailbox01 | ForEach-Object {$Temp="D:\Contoso Export\"+$_.InternetMessageID+".eml";$Temp=$Temp.Replace("<","_");$Temp=$Temp.Replace(">","_");Export-Message $_.Identity | AssembleMessage -Path $Temp}

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Si vous oubliez le paramètre <em>Server</em>, la commande est exécutée sur le serveur local.</td>
</tr>
</tbody>
</table>

