---
title: 'Configurer Get-QueueDigest: Exchange 2013 Help'
TOCTitle: Configurer Get-QueueDigest
ms:assetid: f730c520-4ba5-4a15-8846-132bff500bb8
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dn505733(v=EXCHG.150)
ms:contentKeyID: 59634348
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurer Get-QueueDigest

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2014-12-16_

La cmdlet **Get-QueueDigest** vous permet d’afficher des informations concernant une partie ou la totalité des files d’attente au sein de votre organisation Exchange à l’aide d’une seule commande.

Par défaut, les résultats renvoyés par la cmdlet **Get-QueueDigest** datent d’une à deux minutes. Ces valeurs sont contrôlées par les paramètres suivants :

  - **Clé QueueLoggingInterval dans EdgeTransport.exe.config**   Cette clé spécifie la fréquence à laquelle les données de file d’attente sont enregistrées et disponibles dans **Get-QueueDigest**. La valeur par défaut est `00:01:00` (une minute). Pour spécifier une valeur, entrez-la sous forme de période : *hh:mm:ss* où *h* = heures, *m* = minutes et *s* = secondes. Par défaut, cette clé n’est pas présente dans le fichier EdgeTransport.exe.config.

  - **Paramètre QueueDiagnosticsAggregationInterval sur Set-TransportConfig**   Ce paramètre définit la fréquence à laquelle les données de file d’attente sont partagées entre les serveurs de boîtes aux lettres. La valeur par défaut est `00:01:00` (une minute). Pour spécifier une valeur, entrez-la sous forme de période : *hh:mm:ss* où *h* = heures, *m* = minutes et *s* = secondes.

La somme des valeurs de la clé **QueueLoggingInterval** et du paramètre *QueueDiagnosticsAggregationInterval* détermine l’âge maximal des résultats renvoyés par **Get-QueueDigest**.

En outre, **Get-QueueDigest** renvoie des résultats différemment en fonction du type de file d’attente et de l’état de la file d’attente. Par exemple, les files d’attente suivantes sont affichées dans les résultats tant qu’elles contiennent au moins un message :

  - la file d’attente de soumission, la file d’attente inaccessible et la file d’attente des messages incohérents (files d’attente permanentes) ;

  - les files d’attente de remise ayant l’état suspendu (files d’attente suspendues manuellement par un administrateur).

Par défaut, les files d’attente de remise ayant l’état Actif, Connexion, Prêt ou Nouvelle tentative sont renvoyées dans les résultats seulement si elles contiennent au moins 10 messages. Cette valeur est contrôlée par la clé **QueueLoggingThreshold** dans le fichier EdgeTransport.exe.config. Vous pouvez spécifier une valeur entière inférieure ou supérieure. Par défaut, cette clé n’est pas présente dans le fichier EdgeTransport.exe.config.

## Ce qu’il faut savoir avant de commencer

  - Durée d’exécution estimée : 15 minutes

  - Pour voir les autorisations Exchange dont vous avez besoin pour exécuter **Set-TransportConfig** dans l’environnement de ligne de commande Exchange Management Shell, consultez l’entrée « Configuration du transport » dans la rubrique [Autorisations de flux de messagerie](mail-flow-permissions-exchange-2013-help.md).

  - Les autorisations Exchange ne s’appliquent pas à la modification du fichier EdgeTransport.exe.config et au redémarrage du service de transport Microsoft Exchange. Ces procédures sont exécutées dans le système d’exploitation du serveur Exchange.

  - Les modifications que vous enregistrez dans le fichier EdgeTransport.exe.config sont appliquées après le redémarrage du service de transport de Microsoft Exchange. Lorsque vous redémarrez le service, le flux de messagerie sur le serveur est temporairement interrompu.

  - Les paramètres par serveur personnalisés de vos fichiers de configuration d’application XML Exchange, par exemple les fichiers web.config sur les serveurs d’accès au client ou le fichier EdgeTransport.exe.config sur les serveurs de boîtes aux lettres, seront remplacés lors de l’installation d’une mise à jour cumulative Exchange. Veuillez enregistrer ces informations pour configurer à nouveau votre serveur après l’installation. Vous devez reconfigurer ces paramètres après avoir installé une mise à jour cumulative Exchange.

  - Les modifications apportées à l’aide de **Set-TransportConfig** affectent tous les serveurs de boîtes aux lettres dans votre organisation. Les modifications que vous apportez au fichier EdgeTransport.exe.config affectent uniquement le serveur de boîtes aux lettres local.

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


## Configurer Get-QueueDigest

1.  Dans une fenêtre d’invite de commandes, ouvrez le fichier EdgeTransport.exe.config dans le Bloc-notes en exécutant la commande suivante :
    
        Notepad %ExchangeInstallPath%Bin\EdgeTransport.exe.config

2.  Ajoutez l’une ou les deux clés suivantes dans la section `<appSettings>`.
    
        <add key="QueueLoggingThreshold" value="<integer>" />
        <add key="QueueLoggingInterval" value="<hh:mm:ss>" />
    
    Par exemple, pour définir la valeur de **QueueLoggingThreshold** sur 1 et la valeur de **QueueLoggingInterval** sur 30 secondes, utilisez les valeurs suivantes :
    
        <add key="QueueLoggingThreshold" value="1" />
        <add key="QueueLoggingInterval" value="00:00:30" />

3.  Lorsque vous avez terminé, enregistrez et fermez le fichier EdgeTransport.exe.config.

4.  Redémarrez le service de transport Microsoft Exchange en exécutant la commande suivante :
    
        net stop MSExchangeTransport && net start MSExchangeTransport

5.  Pour modifier la valeur du paramètre *QueueDiagnosticsAggregationInterval* dans l’environnement de ligne de commande Exchange Management Shell, utilisez la syntaxe suivante :
    
        Set-TransportConfig -QueueDiagnosticsAggregationInterval <hh:mm:ss>
    
    Par exemple, pour modifier la valeur sur 30 secondes, exécutez la commande suivante :
    
        Set-TransportConfig -QueueDiagnosticsAggregationInterval 00:00:30

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez correctement configuré **Get-QueueDigest**, procédez comme suit :

1.  Vérifiez les valeurs des clés **QueueLoggingThreshold** et **QueueLoggingInterval** dans le fichier EdgeTransport.exe.config. Si les clés ne sont pas présentes, les valeurs par défaut sont utilisées.

2.  Vérifiez que la valeur du paramètre *QueueDiagnosticsAggregationInterval* en exécutant la commande suivante :
    
        Get-TransportConfig | Format-List *queue*

