---
title: 'Configuration de la journalisation de table de routage: Exchange 2013 Help'
TOCTitle: Configuration de la journalisation de table de routage
ms:assetid: 7184f8f7-4eb8-468a-aafe-b2d72868f820
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb201696(v=EXCHG.150)
ms:contentKeyID: 50478430
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configuration de la journalisation de table de routage

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2015-04-08_

La journalisation de table de routage enregistre régulièrement un instantané de la table de routage utilisée par Microsoft Exchange Server 2013 pour acheminer les messages vers leurs destinations.

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : 15 minutes

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez les entrées « Service de transport » et « Serveur de transport Edge » dans la rubrique [Autorisations de flux de messagerie](mail-flow-permissions-exchange-2013-help.md).

  - Vous pouvez uniquement utiliser l'environnement de ligne de commande Exchange Management Shell pour effectuer cette tâche.

  - Afin de configurer l'intervalle de temps pour le recalcul automatique de la table de routage, vous devez modifier le fichier de configuration d'application XML EdgeTransport.exe.config. Les modifications enregistrées dans ce fichier sont appliquées une fois que vous redémarrez le service de transport Microsoft Exchange. Quand vous redémarrez ce service, le flux de messagerie sur le serveur est temporairement interrompu.

  - Les paramètres par serveur personnalisés de vos fichiers de configuration d’application XML Exchange, par exemple les fichiers web.config sur les serveurs d’accès au client ou le fichier EdgeTransport.exe.config sur les serveurs de boîtes aux lettres, seront remplacés lors de l’installation d’une mise à jour cumulative Exchange. Veuillez enregistrer ces informations pour configurer à nouveau votre serveur après l’installation. Vous devez reconfigurer ces paramètres après avoir installé une mise à jour cumulative Exchange.

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

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour configurer la journalisation de table de routage

Exécutez la commande suivante :

    Set-TransportService <ServerIdentity> -RoutingTableLogMaxAge <dd.hh:mm:ss> -RoutingTableLogMaxDirectorySize <Size>  -RoutingTableLogPath <LocalFilePath>

Cet exemple définit les paramètres de journal de la table de routage suivants sur le serveur de boîtes aux lettres nommé Mailbox01 :

  - Définit l'emplacement des fichiers journaux de table de routage sur D:\\Routing Table Log. Notez bien que si le dossier n'existe pas, il sera créé pour vous.

  - Définit la taille maximale du dossier journal de table de routage sur 70 Mo.

  - Définit l'ancienneté maximale d'un fichier journal de table de routage sur 45 jours.

<!-- end list -->

    Set-TransportService Mailbox01 -RoutingTableLogPath "D:\Routing Table Log" -RoutingTableLogMaxDirectorySize 70MB -RoutingTableLogMaxAge 45.00:00:00

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>La définition du paramètre <em>RoutingTableLogMaxAge</em> sur la valeur <code>00:00:00</code> empêche la suppression automatique des fichiers journaux de table de routage en raison de leur ancienneté.</td>
</tr>
</tbody>
</table>


## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez correctement configuré la journalisation de table de routage, procédez comme suit :

1.  Dans l'environnement de ligne de commande Exchange Management Shell, exécutez la commande suivante :
    
        Get-TransportService <ServerIdentity> | Format-List RoutingTableLog*

2.  Vérifiez que les valeurs affichées sont les valeurs que vous avez configurées.

## Utiliser l'invite de commande pour configurer l'intervalle de recalcul automatique de la table de routage dans le fichier EdgeTransport.exe.config

1.  Dans une fenêtre d'invite de commandes, ouvrez le fichier de configuration d'application EdgeTransport.exe.config dans le Bloc-notes en exécutant la commande suivante :
    
        Notepad %ExchangeInstallPath%Bin\EdgeTransport.exe.config

2.  Modifiez la clé suivante dans la section `<appSettings>`.
    
        <add key="RoutingConfigReloadInterval" value="<hh:mm:ss>" />
    
    Par exemple, pour changer l'intervalle de recalcul automatique de la table de routage sur 10 heures, utilisez la valeur suivante :
    
        <add key="RoutingConfigReloadInterval" value="10:00:00" />

3.  Lorsque vous avez terminé, enregistrez et fermez le fichier EdgeTransport.exe.config.

4.  Redémarrez le service de transport Microsoft Exchange en exécutant la commande suivante :
    
        net stop MSExchangeTransport && net start MSExchangeTransport

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez correctement configuré l'intervalle de recalcul automatique de la table de routage, vérifiez que le journal de table de routage est mis à jour pendant l'intervalle de temps spécifié.

Notez que la table de routage est recalculée et journalisée avant la valeur spécifiée par la clé *RoutingConfigReloadInterval* si l'une des conditions suivantes est vraie :

  - Une modification de la configuration du routage est détectée. Par exemple, un connecteur d'envoi ou de réception est ajouté, supprimé ou modifié, ou le renouvellement du jeton Kerberos (valable 6 heures) a lieu.

  - Le service de transport Microsoft Exchange a démarré.

