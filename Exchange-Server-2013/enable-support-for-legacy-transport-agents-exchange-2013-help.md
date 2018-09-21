---
title: 'Activer la prise en charge des agents de transport hérités: Exchange 2013 Help'
TOCTitle: Activer la prise en charge des agents de transport hérités
ms:assetid: 00617e87-7199-406e-b4a3-94378f657f1f
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ591524(v=EXCHG.150)
ms:contentKeyID: 50477407
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Activer la prise en charge des agents de transport hérités

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2015-03-09_

Dans Microsoft Exchange Server 2013, les agents de transport qui ont été créés à l'aide de la version 4.0 de Microsoft .NET Framework sont pris en charge par défaut. Exchange 2013 prend en charge les agents de transport créés à l'aide des versions antérieures de .NET Framework, mais leur prise en charge n'est pas activée par défaut. Pour activer la prise en charge des agents de transports hérités, vous devez modifier le fichier de configuration de l'application XML approprié. Les fichiers que vous devez modifier diffèrent selon l'emplacement d'installation de l'agent de transport :


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Serveur</th>
<th>Fichiers de configuration de l'application</th>
<th>Service Microsoft Windows</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Serveur d'accès au client</p></td>
<td><p>%ExchangeInstallPath%Bin\MSExchangeFrontendTransport.exe.config</p></td>
<td><p>Transport frontal Microsoft Exchange (MSExchangeFrontendTransport)</p></td>
</tr>
<tr class="even">
<td><p>Serveur de boîtes aux lettres</p></td>
<td><ul>
<li><p>%ExchangeInstallPath%Bin\EdgeTransport.exe.config</p></li>
<li><p>%ExchangeInstallPath%Bin\MSExchangeTransport.exe.config</p></li>
</ul></td>
<td><p>Transport Microsoft Exchange (MSExchangeTransport)</p></td>
</tr>
</tbody>
</table>


Des clés dans les fichiers de configuration de l'application permettent de contrôler la prise en charge des agents de transport hérités. Par défaut, aucune des clés requises ne figure dans les fichiers de configuration de l'application. Vous devez les ajouter manuellement. Le tableau suivant décrit chaque clé plus en détail.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Touche</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>useLegacyV2RuntimeActivationPolicy</em></p></td>
<td><p>Cette clé active ou désactive la prise en charge des agents de transport hérités. Les valeurs correctes pour cette clé sont <code>true</code> et <code>false</code>. Si cette clé n'est pas spécifiée, la valeur par défaut est <code>false</code>.</p></td>
</tr>
<tr class="even">
<td><p><em>supportedRuntime version</em></p></td>
<td><p>Cette clé spécifie la version de Microsoft .NET Framework dont l'agent a besoin. Les valeurs valides pour cette clé sont les suivantes :</p>
<ul>
<li><p><code>v4.0</code> ou <code>v4.0.30319</code></p></li>
<li><p><code>v3.5</code> ou <code>v3.5.21022</code></p></li>
<li><p><code>v3.0</code> ou <code>v3.0.4506</code></p></li>
<li><p><code>v2.0</code> ou <code>v2.0.50727</code></p></li>
</ul>
<p>Vous spécifiez plusieurs valeurs en utilisant plusieurs instances distinctes de la clé <em>supportedRuntime version</em>.</p>
<p>Lorsque vous activez la prise en charge de l'agent de transport hérité à l'aide de la clé <em>useLegacyV2RuntimeActivationPolicy</em>, vous devez toujours spécifier la valeur <code>v4.0</code> en plus des valeurs requises par l'agent de transport hérité.</p></td>
</tr>
</tbody>
</table>


## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : 15 minutes

  - Les autorisations Exchange ne s'appliquent pas aux procédures de cette rubrique. Ces procédures sont exécutées dans le système d'exploitation du serveur Exchange.

  - Les modifications que vous enregistrez dans un fichier de configuration de l'application sont prises en compte après le redémarrage du service correspondant.

  - Lorsque vous redémarrez un service associé aux fichiers de configuration de l'application, le flux de messagerie du serveur est temporairement interrompu.

  - Les paramètres par serveur personnalisés de vos fichiers de configuration d’application XML Exchange, par exemple les fichiers web.config sur les serveurs d’accès au client ou le fichier EdgeTransport.exe.config sur les serveurs de boîtes aux lettres, seront remplacés lors de l’installation d’une mise à jour cumulative Exchange. Veuillez enregistrer ces informations pour configurer à nouveau votre serveur après l’installation. Vous devez reconfigurer ces paramètres après avoir installé une mise à jour cumulative Exchange.

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.


## Utiliser l'invite de commandes pour configurer la prise en charge des agents de transport hérités

Utilisez la procédure suivante pour activer la prise en charge des agents de transport hérités :

1.  Dans une fenêtre d'invite de commandes, sur le serveur Exchange 2013 sur lequel vous souhaitez configurer la prise en charge de l'agent de transport hérité, ouvrez le fichier de configuration de l'application dans le Bloc-notes en exécutant la commande suivante :
    
    ```powershell
Notepad %ExchangeInstallPath%Bin\<AppConfigFile>
```
    
    Par exemple, pour ouvrir le fichier EdgeTransport.exe.config sur un serveur de boîtes aux lettres, exécutez la commande suivante :
    
    ```powershell
Notepad %ExchangeInstallPath%Bin\EdgeTransport.exe.config
```

2.  Localisez la clé *\</configuration\>* à la fin du fichier et collez les clés suivantes avant la clé *\</configuration\>* :
    
        <startup useLegacyV2RuntimeActivationPolicy="true">
           <supportedRuntime version="v4.0" />
           <supportedRuntime version="v3.5" />
           <supportedRuntime version="v3.0" />
           <supportedRuntime version="v2.0" />
        </startup>

3.  Quand vous avez terminé, enregistrez et fermez le fichier de configuration de l'application.

4.  Répétez les étapes 1 à 3 pour modifier les autres fichiers de configuration de l'application.

5.  Redémarrez le service Windows associé en exécutant la commande suivante :
    
        net stop <service> && net start <service>
    
    Par exemple, si vous avez modifié le fichier EdgeTransport.exe.config, vous devez redémarrer le service de transport Microsoft Exchange en exécutant la commande suivante :
    
        net stop MSExchangeTransport && net start MSExchangeTransport

6.  Répétez l'étape 5 pour redémarrer les services associés aux autres fichiers de configuration de l'application modifiés.

## Comment savoir si cela a fonctionné ?

Vous saurez que cette procédure fonctionne si l'agent de transport hérité s'installe correctement. Si vous essayez d'installer un agent de transport hérité sans suivre les procédures décrites dans cette rubrique, un message d'erreur similaire au suivant s'affiche :

    Mixed mode assembly is built against version '<version>' of the runtime and cannot be loaded in the 4.0 runtime without additional configuration information.

