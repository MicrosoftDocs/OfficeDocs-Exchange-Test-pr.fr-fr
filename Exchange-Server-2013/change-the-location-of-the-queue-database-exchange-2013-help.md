---
title: 'Modif. l’emplacement de la BDD de file d’attente: Exchange 2013 Help'
TOCTitle: Modifier l'emplacement de la base de données de file d'attente
ms:assetid: f170cb0c-04a9-4fa7-b594-206e3a787e14
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb125177(v=EXCHG.150)
ms:contentKeyID: 51407253
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Modifier l'emplacement de la base de données de file d'attente

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2015-03-09_

Une *file d'attente* est un emplacement d'hébergement temporaire pour les messages attendant de passer à l'étape suivante du traitement. Chaque file d'attente représente un ensemble logique de messages traités par un serveur de transport dans un ordre spécifique.

Comme dans les versions précédentes d'Exchange, Microsoft Exchange Server 2013 utilise une base de données ESE (Extensible Storage Engine) pour le stockage des files d'attente. Les différentes files d'attente sont stockées dans une même base de données ESE. Les files d'attente se trouvent uniquement sur les serveurs de boîtes aux lettres et les serveurs de transport Edge.

L'emplacement de la base de données de files d'attente et de ses journaux de transactions est déterminé par des clés figurant dans le fichier de configuration de l'application XML `%ExchangeInstallPath%Bin\EdgeTransport.exe.config`. Ce fichier est associé au service de transport Microsoft Exchange. Le tableau suivant décrit chaque clé plus en détail.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Clé</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>QueueDatabasePath</em></p></td>
<td><p>Cette clé indique l'emplacement des fichiers de base de données de files d'attente. Les fichiers sont les suivants :</p>
<ul>
<li><p>Mail.que</p></li>
<li><p>Trn.chk</p></li>
</ul>
<p>L'emplacement par défaut est <code>%ExchangeInstallPath%TransportRoles\data\Queue</code>.</p></td>
</tr>
<tr class="even">
<td><p><em>QueueDatabaseLoggingPath</em></p></td>
<td><p>Cette clé indique l'emplacement des fichiers journaux de transactions d'une base de données de files d'attente. Les fichiers sont les suivants :</p>
<ul>
<li><p>Trn.log</p></li>
<li><p>Trntmp.log</p></li>
<li><p>Trn<em>nnn</em>.log</p></li>
<li><p>Trnres00001.jrs</p></li>
<li><p>Trnres00002.jrs</p></li>
<li><p>Temp.edb</p></li>
</ul>
<p>Notez que le fichier Temp.edb permet de vérifier le schéma de la base de données de files d'attente lors du démarrage du service de transport Microsoft Exchange. Bien que Temp.edb ne soit pas un fichier journal de transactions, il est conservé au même emplacement que les fichiers journaux de transactions.</p>
<p>L'emplacement par défaut est <code>%ExchangeInstallPath%TransportRoles\data\Queue</code>.</p></td>
</tr>
</tbody>
</table>


## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : 15 minutes.

  - Les autorisations Exchange ne s'appliquent pas aux procédures de cette rubrique. Ces procédures sont exécutées dans le système d'exploitation du serveur Exchange.

  - Quand vous arrêtez ou redémarrez le service de transport Microsoft Exchange, le flux de messagerie sur le serveur est interrompu.

  - Quand vous modifiez l'emplacement de la base de données de files d'attente ou des journaux de transactions, la base de données de files d'attente et les fichiers journaux de transactions existants ne sont pas déplacés. Une nouvelle base de données de files d'attente et de nouveaux journaux de transactions sont créés dans le nouvel emplacement. Les fichiers existants sont laissés à l'ancien emplacement. Elles ne sont toutefois plus utilisées. Si vous souhaitez réutiliser la base de données de files d'attente ou les fichiers journaux de transactions existants dans le nouvel emplacement, vous devez déplacer les fichiers existants vers le nouvel emplacement une fois le service de transport Microsoft Exchange arrêté, mais avant de le démarrer.

  - Si le dossier cible pour la base de données de files d'attente ou les fichiers journaux de transactions n'existe pas, il sera créé si le dossier parent dispose des autorisations suivantes :
    
      - Service réseau : Contrôle total
    
      - Système : Contrôle total
    
      - Administrateurs : Contrôle total

  - Les paramètres par serveur personnalisés de vos fichiers de configuration d’application XML Exchange, par exemple les fichiers web.config sur les serveurs d’accès au client ou le fichier EdgeTransport.exe.config sur les serveurs de boîtes aux lettres, seront remplacés lors de l’installation d’une mise à jour cumulative Exchange. Veuillez enregistrer ces informations pour configurer à nouveau votre serveur après l’installation. Vous devez reconfigurer ces paramètres après avoir installé une mise à jour cumulative Exchange.

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

## Que souhaitez-vous faire ?

## Utiliser l'invite de commandes pour créer une base de données de files d'attente et des journaux de transactions à un nouvel emplacement

1.  Créez les dossiers dans lesquels vous voulez conserver les bases de données de files d'attente et les journaux de transactions. Assurez-vous que les dossiers disposent des autorisations appropriées.

2.  Dans une fenêtre d'invite de commandes, ouvrez le fichier EdgeTransport.exe.config dans le Bloc-notes en exécutant la commande suivante :
    
    ```powershell
Notepad %ExchangeInstallPath%Bin\EdgeTransport.exe.config
```

3.  Modifiez les clés suivantes dans la section `<appSettings>`.
    
        <add key="QueueDatabasePath" value="<LocalPath>" />
        <add key="QueueDatabaseLoggingPath" value="<LocalPath>" />
    
    Par exemple, pour créer une nouvelle base de données de files d'attente dans D:\\Queue\\QueueDB et de nouveaux journaux de transactions dans D:\\Queue\\QueueLogs, utilisez les valeurs suivantes :
    
        <add key="QueueDatabasePath" value="D:\Queue\QueueDB" />
        <add key="QueueDatabaseLoggingPath" value="D:\Queue\QueueLogs" />

4.  Quand vous avez terminé, enregistrez et fermez le fichier EdgeTransport.exe.config.

5.  Redémarrez le service de transport Microsoft Exchange en exécutant la commande suivante :
    
        net stop MSExchangeTransport && net start MSExchangeTransport

## Comment savoir si cela a fonctionné ?

Voici comment vérifier que vous avez correctement créé une base de données de files d'attente et des journaux de transactions au nouvel emplacement :

1.  Vérifiez les nouveaux fichiers de base de données Mail.que et Trn.chk figurent dans le nouvel emplacement.

2.  Vérifiez que les nouveaux fichiers journaux de transactions Trn.log, Trntmp.log, Trnres00001.jrs, Trnres00002.jrs et les fichiers Temp.edb figurent dans le nouvel emplacement.

3.  Si vous pouvez supprimer l'ancienne base de données de files d'attente et les anciens fichiers journaux de transactions de l'ancien emplacement une fois le service de transport Microsoft Exchange démarré, ces fichiers ne sont plus utilisés.

Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), et [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

Que souhaitez-vous faire ?

## Utiliser l'invite de commandes pour déplacer une base de données de files d'attente et des journaux de transactions existants vers un nouvel emplacement

Seuls les scénarios de récupération d'urgence dans lesquels le service de transport Microsoft Exchange n'a pas été arrêté correctement ou impliquant une panne du disque dur nécessitent la restauration et le déplacement d'une base de données de files d'attente existante et de ses journaux de transactions.

Dans des circonstances normales, vous ne devriez pas avoir à réutiliser des journaux de transactions existants. Un arrêt normal du service de transport Microsoft Exchange écrit toutes les entrées non validées du journal de transactions dans la base de données de files d'attente. En outre, la journalisation circulaire est utilisée, de sorte que les journaux de transactions contenant les modifications de la base de données précédemment validées ne sont pas conservés.

Utilisez la procédure suivante pour déplacer la base de données de files d'attente et les journaux de transactions existants vers un nouvel emplacement :

1.  Créez les dossiers dans lesquels vous voulez conserver les bases de données de files d'attente et les journaux de transactions. Assurez-vous que les dossiers disposent des autorisations appropriées.

2.  Dans une fenêtre d'invite de commandes, ouvrez le fichier EdgeTransport.exe.config dans le Bloc-notes en exécutant la commande suivante :
    
    ```powershell
Notepad %ExchangeInstallPath%Bin\EdgeTransport.exe.config
```

3.  Modifiez les clés suivantes dans la section `<appSettings>` :
    
        <add key="QueueDatabasePath" value="<LocalPath>" />
        <add key="QueueDatabaseLoggingPath" value="<LocalPath>" />
    
    Par exemple, pour modifier l'emplacement de la base de données de files d'attente pour D:\\Queue\\QueueDB et celui des journaux de transaction pour D:\\Queue\\QueueLogs, utilisez les valeurs suivantes :
    
        <add key="QueueDatabasePath" value="D:\Queue\QueueDB" />
        <add key="QueueDatabaseLoggingPath" value="D:\Queue\QueueLogs" />

4.  Quand vous avez terminé, enregistrez et fermez le fichier EdgeTransport.exe.config.

5.  Arrêtez le service de transport Microsoft Exchange en exécutant la commande suivante :
    
    ```powershell
net stop MSExchangeTransport
```

6.  Déplacez les fichiers de base de données existants Mail.que et Trn.chk de l'emplacement d'origine vers le nouvel emplacement.

7.  Déplacez les fichiers journaux de transactions existants Trn.log, Trntmp.log, Trn*nnnnn*.log, Trnres00001.jrs, Trnres00002.jrs et Temp.edb de l'ancien vers le nouvel emplacement.

8.  Démarrez le service de transport Microsoft Exchange en exécutant la commande suivante :
    
    ```powershell
net start MSExchangeTransport
```

## Comment savoir si cela a fonctionné ?

Voici comment vérifier que vous avez correctement déplacé la base de données de files d'attente et les journaux de transactions existants vers le nouvel emplacement :

1.  Vérifiez les fichiers de base de données de files d'attente Mail.que et Trn.chk figurent dans le nouvel emplacement.

2.  Vérifiez que les fichiers journaux de transactions Trn.log, Trntmp.log, Trnres00001.jrs, Trnres00002.jrs et les fichiers Temp.edb figurent dans le nouvel emplacement.

3.  Vérifiez que l'emplacement d'origine ne compte aucune base de données de files d'attente ni aucun fichier journal de transactions.

Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), et [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

Que souhaitez-vous faire ?

