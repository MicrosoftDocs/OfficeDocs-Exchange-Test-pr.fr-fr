---
title: 'Config. des limites de taille de message propres au client: Exchange 2013 Help'
TOCTitle: Configuration des limites de taille de message propres au client
ms:assetid: fef9ca78-b68f-4342-ada0-881ab985ce3c
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Hh529949(v=EXCHG.150)
ms:contentKeyID: 52063035
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configuration des limites de taille de message propres au client

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2017-01-26_

Dans Microsoft Exchange Server 2013, différentes limites de taille s'appliquent aux messages circulant au sein votre organisation Exchange. Pour plus d'informations, consultez la rubrique [Tailles limites des messages](message-size-limits-exchange-2013-help.md).

Toutefois, vous pouvez configurer des limites de taille des messages spécifiques pour Outlook Web App et des clients de messagerie utilisant ActiveSync ou Services Web Exchange EWS. Si vous modifiez les limites de taille de message pour l’ensemble de l’organisation Exchange, vous devez vérifier qu’elles sont correctement définies pour Outlook Web App, ActiveSync et les services web Exchange. Vous configurez ces valeurs dans les fichiers web.config sur les serveurs d’accès au client et les serveurs de boîtes aux lettres. Ces limites sont décrites dans les tableaux suivants.

### ActiveSync

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Rôle serveur</th>
<th>Fichier de configuration</th>
<th>Clés et valeurs par défaut</th>
<th>Taille</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Accès client</p></td>
<td><p><code>%ExchangeInstallPath%FrontEnd\HttpProxy\Sync\web.config</code></p></td>
<td><p><code>maxAllowedContentLength=&quot;30000000 bytes&quot;</code>   Absent par défaut (voir les commentaires).</p></td>
<td><p>octets</p></td>
</tr>
<tr class="even">
<td><p>Accès client</p></td>
<td><p><code>%ExchangeInstallPath%FrontEnd\HttpProxy\Sync\web.config</code></p></td>
<td><p><code>maxRequestLength=&quot;10240&quot;</code></p></td>
<td><p>kilo-octets</p></td>
</tr>
<tr class="odd">
<td><p>Boîte aux lettres</p></td>
<td><p><code>%ExchangeInstallPath%ClientAccess\Sync\web.config</code></p></td>
<td><p><code>maxAllowedContentLength=&quot;30000000 bytes&quot;</code>   Absent par défaut (voir les commentaires).</p></td>
<td><p>octets</p></td>
</tr>
<tr class="even">
<td><p>Boîte aux lettres</p></td>
<td><p><code>%ExchangeInstallPath%ClientAccess\Sync\web.config</code></p></td>
<td><p><code>maxRequestLength=&quot;10240&quot;</code></p></td>
<td><p>kilo-octets</p></td>
</tr>
<tr class="odd">
<td><p>Boîte aux lettres</p></td>
<td><p><code>%ExchangeInstallPath%ClientAccess\Sync\web.config</code></p></td>
<td><p><code>&lt;add key=&quot;MaxDocumentDataSize&quot; value=&quot;10240000&quot;&gt;</code></p></td>
<td><p>octets</p></td>
</tr>
</tbody>
</table>


**Commentaires relatifs aux limites d’ActiveSync**

Par défaut, il n’existe pas de clé *maxAllowedContentLength* dans les fichiers `web.config` pour ActiveSync. Toutefois, la taille maximale de message pour ActiveSync est affectée par la valeur **maxAllowedContentLength** qui s’applique à tous les sites web sur le serveur. La valeur par défaut est 30 000 000 octets (30 Mo). Pour afficher ces valeurs pour ActiveSync sur les serveurs d’accès au client et les serveurs de boîtes aux lettres dans le Gestionnaire des services Internet, procédez comme suit :

1.  Effectuez l’une des étapes suivantes :
    
      - Sur les serveurs d’accès au client, ouvrez le **Gestionnaire des services Internet**, accédez à **Sites** \> **Site web par défaut** et sélectionnez **Microsoft-Server-ActiveSync**.
    
      - Sur les serveurs de boîte aux lettres, ouvrez le **Gestionnaire des services Internet**, accédez à **Sites** \> **Site principal Exchange**, puis sélectionnez **Microsoft-Server-ActiveSync**.

2.  Vérifiez que l’option **Affichage des fonctionnalités** est sélectionnée, et double-cliquez sur **Éditeur de configuration** dans la section **Gestion**.

3.  Cliquez sur la flèche déroulante dans le champ **Section**, accédez à **system.webServer** \> **sécurité** et sélectionnez **requestFiltering**.

4.  Dans les résultats, développez **requestLimits** et vous verrez **maxAllowedContentLength** et la valeur par défaut 30 000 000 (octets).

Pour modifier la valeur **maxAllowedContentLength**, saisissez une nouvelle valeur en octets, puis cliquez sur **Appliquer**. Vous devez modifier la valeur sur les serveurs d’accès au client et les serveurs de boîtes aux lettres. Une fois que vous avez modifié la valeur dans le Gestionnaire des services Internet, une nouvelle clé *maxAllowedContentLength* est écrite dans le fichier `web.config` correspondant (`%ExchangeInstallPath%FrontEnd\HttpProxy\Sync\web.config` sur les serveurs d’accès au client et `%ExchangeInstallPath%ClientAccess\Sync\web.config` sur les serveurs de boîte aux lettres).

Pour modifier la taille maximale des messages des clients ActiveSync, vous devez modifier la valeur de *maxRequestLength* dans le fichier `web.config` sur les serveurs d’accès au client et les serveurs de boîte aux lettres, *MaxDocumentDataSize* dans le fichier `web.config` sur les serveurs de boîte aux lettres et *maxAllowedContentLength* dans le Gestionnaire des services Internet sur les serveurs d’accès au client et les serveurs de boîte aux lettres.

### Services Web Exchange

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Rôle serveur</th>
<th>Fichier de configuration</th>
<th>Clés et valeurs par défaut</th>
<th>Taille</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Accès client</p></td>
<td><p><code>%ExchangeInstallPath%FrontEnd\HttpProxy\ews\web.config</code></p></td>
<td><p><code>maxAllowedContentLength=&quot;67108864&quot;</code></p></td>
<td><p>octets</p></td>
</tr>
<tr class="even">
<td><p>Boîte aux lettres</p></td>
<td><p><code>%ExchangeInstallPath%ClientAccess\exchweb\ews\web.config</code></p></td>
<td><p><code>maxAllowedContentLength=&quot;67108864&quot;</code></p></td>
<td><p>octets</p></td>
</tr>
<tr class="odd">
<td><p>Boîte aux lettres</p></td>
<td><p><code>%ExchangeInstallPath%ClientAccess\exchweb\ews\web.config</code></p></td>
<td><p>14 instances de <code>maxReceivedMessageSize=&quot;67108864&quot;</code></p></td>
<td><p>octets</p></td>
</tr>
</tbody>
</table>


**Commentaires relatifs aux limites des services web Exchange**

  - Il existe 14 instances distinctes de la valeur `maxReceivedMessageSize="67108864"` correspondant aux différentes combinaisons de liaisons (http et https) et de méthodes d’authentification.

  - Pour modifier la taille maximale des messages pour les clients des services web Exchange, vous devez modifier la valeur de *maxAllowedContentLength* dans les deux fichiers `web.config`, ainsi que les 14 instances `maxReceivedMessageSize="67108864"` dans le fichier `web.config` sur les serveurs de boîte aux lettres.

  - Dans le fichier `web.config` sur les serveurs de boîte aux lettres figurent également deux instances de la valeur `maxReceivedMessageSize="1048576"` pour les liaisons **UMLegacyMessageEncoderSoap11Element** que vous n’avez pas besoin de modifier.

  - *maxRequestLength* est un paramètre ASP.NET présent dans les deux fichiers web.config, mais non utilisé par les services web Exchange, afin que vous n’ayez pas besoin de le modifier.

### Outlook Web App

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Rôle serveur</th>
<th>Fichier de configuration</th>
<th>Clés et valeurs par défaut</th>
<th>Taille</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Accès client</p></td>
<td><p><code>%ExchangeInstallPath%FrontEnd\HttpProxy\owa\web.config</code></p></td>
<td><p><code>maxAllowedContentLength=&quot;35000000&quot;</code></p></td>
<td><p>octets</p></td>
</tr>
<tr class="even">
<td><p>Accès client</p></td>
<td><p><code>%ExchangeInstallPath%FrontEnd\HttpProxy\owa\web.config</code></p></td>
<td><p><code>maxRequestLength=&quot;35000&quot;</code></p></td>
<td><p>kilo-octets</p></td>
</tr>
<tr class="odd">
<td><p>Boîte aux lettres</p></td>
<td><p><code>%ExchangeInstallPath%ClientAccess\Owa\web.config</code></p></td>
<td><p><code>maxAllowedContentLength=&quot;35000000&quot;</code></p></td>
<td><p>octets</p></td>
</tr>
<tr class="even">
<td><p>Boîte aux lettres</p></td>
<td><p><code>%ExchangeInstallPath%ClientAccess\Owa\web.config</code></p></td>
<td><p><code>maxRequestLength=&quot;35000&quot;</code></p></td>
<td><p>kilo-octets</p></td>
</tr>
<tr class="odd">
<td><p>Boîte aux lettres</p></td>
<td><p><code>%ExchangeInstallPath%ClientAccess\Owa\web.config</code></p></td>
<td><p>2 instances de <code>maxReceivedMessageSize=&quot;35000000&quot;</code></p></td>
<td><p>octets</p></td>
</tr>
<tr class="even">
<td><p>Boîte aux lettres</p></td>
<td><p><code>%ExchangeInstallPath%ClientAccess\Owa\web.config</code></p></td>
<td><p>2 instances de <code>maxStringContentLength=&quot;35000000&quot;</code></p></td>
<td><p>octets</p></td>
</tr>
</tbody>
</table>


**Commentaires relatifs aux limites d’Outlook Web App**

  - Dans le fichier `web.config` sur les serveurs de boîte aux lettres, il existe deux instances distinctes des valeurs `maxReceivedMessageSize="35000000"` et `maxStringContentLength="35000000"` qui correspondent à des liaisons http et https.

  - Pour modifier la taille maximale des messages pour les clients Outlook Web App, vous devez modifier toutes ces valeurs dans les deux fichiers, y compris les deux instances de *maxReceivedMessageSize* et *maxStringContentLength* dans le fichier `web.config` sur les serveurs de boîte aux lettres.

  - Dans le fichier `web.config` sur les serveurs de boîte aux lettres, il existe également une instance de la valeur `maxStringContentLength="102400"` pour la liaison **MsOnlineShellService** que vous n’avez pas besoin de modifier.

Pour toutes les limites de taille de message, vous devez définir des valeurs supérieures aux tailles réelles que vous voulez appliquer. Cette augmentation des valeurs est nécessaire pour tenir compte de l'augmentation inévitable de la taille des messages suite à l'ajout de pièces jointes et à la présence de données binaires en codage Base64. Le codage Base64 augmentant la taille des messages d'environ 33 %, les valeurs que vous spécifiez pour les limites de taille de message doivent être d'environ 33 % supérieures aux tailles réelles de message utilisables. Par exemple, si vous spécifiez une valeur maximale de taille de message de 64 Mo, vous pouvez vous attendre à une valeur maximale réelle de taille de message d'environ 48 Mo.

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : 15 minutes

  - Les autorisations Exchange ne s'appliquent pas aux procédures de cette rubrique. Ces procédures sont exécutées dans le système d'exploitation du serveur Exchange.

  - Les modifications que vous enregistrez dans le fichier de configuration Web.config s'appliquent après le redémarrage des services Internet (IIS).

  - Pour autoriser une augmentation de 33 % de la taille en raison du codage Base64, multipliez par 4/3 la nouvelle valeur de taille maximale souhaitée en mégaoctets. Pour convertir la valeur en kilo-octets, multipliez-la par 1024. Pour la convertir en octets, multipliez-la par 1048756 (1024\*1024). Notez que l'augmentation de taille due au codage Base64 peut être supérieure à 33 %, et qu'elle dépend de plusieurs facteurs tels que la taille, le type et le niveau de compression des pièces jointes, ainsi que le client de messagerie utilisé pour composer et envoyer le message.

  - Les paramètres par serveur personnalisés de vos fichiers de configuration d’application XML Exchange, par exemple les fichiers web.config sur les serveurs d’accès au client ou le fichier EdgeTransport.exe.config sur les serveurs de boîtes aux lettres, seront remplacés lors de l’installation d’une mise à jour cumulative Exchange. Veuillez enregistrer ces informations pour configurer à nouveau votre serveur après l’installation. Vous devez reconfigurer ces paramètres après avoir installé une mise à jour cumulative Exchange.

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.


## Utiliser le bloc-notes pour configurer des limites de taille de message spécifiques pour les clients

1.  Ouvrez les fichiers web.config appropriés dans le bloc-notes. Par exemple, pour ouvrir les fichiers web.config pour les clients Services Web Exchange, exécutez les commandes suivantes :
    
        Notepad %ExchangeInstallPath%ClientAccess\exchweb\ews\web.config
        Notepad %ExchangeInstallPath%FrontEnd\HttpProxy\ews\web.config

2.  Recherchez les clés pertinentes dans les fichiers web.config appropriés, comme décrit dans les tableaux présentés plus haut dans la rubrique. Par exemple, pour les clients Services Web Exchange, recherchez la clé *maxAllowedContentLength* dans les deux fichiers, ainsi que les 14 instances de la valeur `maxReceivedMessageSize="67108864"` dans le fichier `web.config` sur les serveurs de boîte aux lettres.
    
        <requestLimits maxAllowedContentLength="67108864" />
        ...maxReceivedMessageSize="67108864"...
    
    Par exemple, pour autoriser une taille maximale des messages codés en Base64 d’environ 64 Mo, changez toutes les instances de `67108864` en `89478486` (64\*4/3\*1048756) :
    
        <requestLimits maxAllowedContentLength="89478486" />
        ...maxReceivedMessageSize="89478486"...

3.  Quand vous avez terminé, enregistrez et fermez les fichiers web.config.

4.  Redémarrez les services Internet (IIS) en exécutant la commande suivante :
    
    ```powershell
IISReset /noforce
```

## Configurer des limites de taille de message spécifiques pour les clients à partir de la ligne de commande

Au lieu d’utiliser le bloc-notes, vous pouvez configurer les limites de taille de message spécifiques pour les clients à partir de la ligne de commande. Ouvrez une invite de commandes avec des privilèges élevés sur le serveur Exchange (la fenêtre d’invite de commandes s’ouvre lorsque vous sélectionnez **Exécuter en tant qu’administrateur**) et exécutez les commandes appropriées pour les limites à configurer.

**Remarques** :

  - Les valeurs de taille dans les commandes sont celles par défaut, vous devez donc les modifier.

  - N’oubliez pas de vérifier si la valeur est en octets ou en kilo-octets.

**ActiveSync**

    %windir%\system32\inetsrv\appcmd.exe set config "Default Web Site/Microsoft-Server-ActiveSync/" -section:system.webServer/security/requestFiltering /requestLimits.maxAllowedContentLength:30000000
    %windir%\system32\inetsrv\appcmd.exe set config "Default Web Site/Microsoft-Server-ActiveSync/" -section:system.web/httpRuntime /maxRequestLength:10240
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/Microsoft-Server-ActiveSync/" -section:system.webServer/security/requestFiltering /requestLimits.maxAllowedContentLength:30000000
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/Microsoft-Server-ActiveSync/" -section:system.web/httpRuntime /maxRequestLength:10240
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/Microsoft-Server-ActiveSync/" -section:appSettings /[key='MaxDocumentDataSize'].value:10240000

**Services Web Exchange**

    %windir%\system32\inetsrv\appcmd.exe set config "Default Web Site/ews/" -section:system.webServer/security/requestFiltering /requestLimits.maxAllowedContentLength:67108864
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/ews/" -section:system.webServer/security/requestFiltering /requestLimits.maxAllowedContentLength:67108864
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/ews/" -section:system.serviceModel/bindings /customBinding.[name='EWSAnonymousHttpsBinding'].httpsTransport.maxReceivedMessageSize:67108864
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/ews/" -section:system.serviceModel/bindings /customBinding.[name='EWSAnonymousHttpBinding'].httpTransport.maxReceivedMessageSize:67108864
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/ews/" -section:system.serviceModel/bindings /customBinding.[name='EWSBasicHttpsBinding'].httpsTransport.maxReceivedMessageSize:67108864
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/ews/" -section:system.serviceModel/bindings /customBinding.[name='EWSBasicHttpBinding'].httpTransport.maxReceivedMessageSize:67108864
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/ews/" -section:system.serviceModel/bindings /customBinding.[name='EWSNegotiateHttpsBinding'].httpsTransport.maxReceivedMessageSize:67108864
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/ews/" -section:system.serviceModel/bindings /customBinding.[name='EWSNegotiateHttpBinding'].httpTransport.maxReceivedMessageSize:67108864
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/ews/" -section:system.serviceModel/bindings /customBinding.[name='EWSWSSecurityHttpsBinding'].httpsTransport.maxReceivedMessageSize:67108864
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/ews/" -section:system.serviceModel/bindings /customBinding.[name='EWSWSSecurityHttpBinding'].httpTransport.maxReceivedMessageSize:67108864
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/ews/" -section:system.serviceModel/bindings /customBinding.[name='EWSWSSecuritySymmetricKeyHttpsBinding'].httpsTransport.maxReceivedMessageSize:67108864
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/ews/" -section:system.serviceModel/bindings /customBinding.[name='EWSWSSecuritySymmetricKeyHttpBinding'].httpTransport.maxReceivedMessageSize:67108864
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/ews/" -section:system.serviceModel/bindings /customBinding.[name='EWSWSSecurityX509CertHttpsBinding'].httpsTransport.maxReceivedMessageSize:67108864
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/ews/" -section:system.serviceModel/bindings /customBinding.[name='EWSWSSecurityX509CertHttpBinding'].httpTransport.maxReceivedMessageSize:67108864
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/ews/" -section:system.serviceModel/bindings /webHttpBinding.[name='EWSStreamingNegotiateHttpsBinding'].maxReceivedMessageSize:67108864
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/ews/" -section:system.serviceModel/bindings /webHttpBinding.[name='EWSStreamingNegotiateHttpBinding'].maxReceivedMessageSize:67108864

**Outlook Web App**

    %windir%\system32\inetsrv\appcmd.exe set config "Default Web Site/owa/" -section:system.webServer/security/requestFiltering /requestLimits.maxAllowedContentLength:35000000
    %windir%\system32\inetsrv\appcmd.exe set config "Default Web Site/owa/" -section:system.web/httpRuntime /maxRequestLength:35000
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/owa/" -section:system.webServer/security/requestFiltering /requestLimits.maxAllowedContentLength:35000000
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/owa/" -section:system.web/httpRuntime /maxRequestLength:35000
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/owa/" -section:system.serviceModel/bindings /webHttpBinding.[name='httpsBinding'].maxReceivedMessageSize:35000000
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/owa/" -section:system.serviceModel/bindings /webHttpBinding.[name='httpBinding'].maxReceivedMessageSize:35000000
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/owa/" -section:system.serviceModel/bindings /webHttpBinding.[name='httpsBinding'].readerQuotas.maxStringContentLength:35000000
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/owa/" -section:system.serviceModel/bindings /webHttpBinding.[name='httpBinding'].readerQuotas.maxStringContentLength:35000000

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez correctement configuré la limite de taille de message spécifique des clients, vous devez envoyer un message de test à destination et en provenance d’une boîte aux lettres utilisée par le client concerné. Vous pouvez tenter d'utiliser quelques pièces jointes de plus petite taille ou une pièce jointe de grande taille de façon à ce que la taille des messages de test soit d'environ 33 % inférieure à la valeur que vous avez configurée. Par exemple, une valeur configurée de 85 Mo correspond à une taille maximale réelle de message d'environ 64 Mo.

