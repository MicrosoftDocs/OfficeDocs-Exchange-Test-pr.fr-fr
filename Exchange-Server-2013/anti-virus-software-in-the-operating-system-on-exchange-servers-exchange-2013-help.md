---
title: "Logiciel anti-virus du système d'exploitation sur les serveurs Exchange: Exchange 2013 Help"
TOCTitle: Logiciel anti-virus du système d'exploitation sur les serveurs Exchange
ms:assetid: 7cef6017-7a55-41f3-a636-1ca4fce575b1
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb332342(v=EXCHG.150)
ms:contentKeyID: 50478551
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Logiciel anti-virus du système d'exploitation sur les serveurs Exchange

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2016-07-22_

Cette rubrique décrit les effets des antivirus au niveau fichier sur les ordinateurs qui exécutent Microsoft Exchange Server 2013. Les recommandations présentées dans cette rubrique permettent d’améliorer la sécurité et l’intégrité de votre organisation Exchange.

Les antivirus au niveau fichier sont fréquemment utilisés. Toutefois, s’ils sont mal configurés, ils peuvent causer des problèmes dans Exchange 2013. Il existe deux types d’antivirus au niveau fichier :

  - L’*analyse antivirus au niveau fichier résidant en mémoire* est une composante de l’antivirus au niveau fichier chargée en permanence dans la mémoire. Elle vérifie tous les fichiers utilisés sur le disque dur et dans la mémoire de l’ordinateur.

  - L’*analyse antivirus au niveau fichier à la demande* est une composante de l’antivirus au niveau fichier que vous pouvez configurer pour analyser les fichiers sur le disque dur manuellement ou selon une planification. Certaines versions de l’antivirus démarrent automatiquement l’analyse antivirus à la demande après la mise à jour des signatures de virus afin que tous les fichiers soient analysés avec les dernières signatures.

Les problèmes suivants peuvent survenir lorsque vous utilisez des antivirus au niveau fichier avec Exchange 2013 :

  - Les antivirus au niveau fichier peuvent analyser un fichier en cours d’utilisation ou à un intervalle planifié. Cela peut entraîner le verrouillage ou la mise en quarantaine par les antivirus d’un journal Exchange ou d’un fichier de base de données alors qu’Exchange 2013 tente d’utiliser le fichier. Ce comportement peut générer une erreur grave dans Exchange 2013 et générer également des erreurs -1018 dans le journal des événements.

  - Les analyseurs au niveau fichier n’offrent pas de protection contre les virus de messagerie comme le ver Storm Worm. Storm Worm était un virus de type cheval de Troie s’introduisant par une porte dérobée pour se propager via les messages électroniques. Le ver relie l’ordinateur infecté à un réseau zombie dans lequel l’ordinateur sert à envoyer des courriers indésirables par salves périodiques.

## Recommandations pour l’utilisation de l’analyse au niveau fichier avec Exchange 2013

Si vous déployez des antivirus au niveau fichier sur les serveurs Exchange 2013, assurez-vous que les exclusions adéquates, telles que les exclusions de répertoires, de processus et d’extensions de nom de fichier, sont mises en place pour l’analyse au niveau fichier résidant en mémoire. Cette section décrit les exclusions de répertoires, de processus et d’extensions de nom de fichier recommandées.

**Contenu de cette rubrique**

Exclusions de répertoires

Exclusions de processus

Exclusions d’extensions de nom de fichier

## Exclusions de répertoires

Vous devez exclure des répertoires spécifiques pour chaque serveur Exchange sur lequel vous exécutez une analyse antivirus au niveau fichier. Cette section décrit les répertoires que vous devez exclure de l’analyse au niveau fichier.

  - **serveurs de boîtes aux lettres**
    
      - **Bases de données de boîtes aux lettres**
        
          - Bases de données , fichiers de point de contrôle et fichiers journaux Exchange. Par défaut, ils sont accessibles dans les sous-dossiers du dossier %ExchangeInstallPath%Mailbox. Pour déterminer l’emplacement d’une base de données de boîtes aux lettres, d’un journal des transactions et d’un fichier de point de contrôle, exécutez la commande suivante : `Get-MailboxDatabase -Server <servername>| Format-List *path*`
        
          - Index du contenu des bases de données. Par défaut, ceux-ci se trouvent dans le même dossier que celui du fichier de la base de données.
        
          - Fichiers GroupMetrics. Par défaut, ils se trouvent dans le dossier %ExchangeInstallPath%GroupMetrics.
        
          - Fichiers journaux généraux, tels que les fichiers journaux de suivi des messages et de réparation du calendrier. Par défaut, ils se trouvent dans les sous-dossiers du dossier %ExchangeInstallPath%TransportRoles\\Logs et du dossier %ExchangeInstallPath%Logging. Pour déterminer les chemins d’accès aux journaux utilisés, exécutez la commande suivante dans l’environnement de ligne de commande Exchange Management Shell : `Get-MailboxServer <servername> | Format-List *path*`
        
          - Fichiers de carnet d’adresses en mode hors connexion. Par défaut, ils se trouvent dans les sous-dossiers du dossier %ExchangeInstallPath%ClientAccess\\OAB.
        
          - Fichiers système IIS du dossier %SystemRoot%\\System32\\Inetsrv.
        
          - Dossier temporaire de la base de données de boîtes aux lettres : %ExchangeInstallPath%Mailbox\\MDBTEMP
    
      - **Membres des groupes de disponibilité de base de données**
        
          - Tous les éléments répertoriées dans la liste **Bases de données de boîtes aux lettres** et la base de données quorum du cluster qui existe à %Windir%\\Cluster.
        
          - Fichiers du répertoire témoin. Ces fichiers se trouvent sur un autre serveur de l’environnement, en général un serveur d’accès au client qui n’est pas installé sur le même ordinateur que le serveur de boîtes aux lettres. Par défaut, les fichiers du répertoire témoin sont trouvent dans %SystemDrive%:\\DAGFileShareWitnesses\\\<DAGFQDN\>.
    
      - **service de transport**
        
          - Fichiers journaux comme les journaux de suivi des messages et de connectivité. Par défaut, ces fichiers se trouvent dans les sous-dossiers du dossier %ExchangeInstallPath%TransportRoles\\Logs. Pour déterminer les chemins d’accès aux journaux utilisés, exécutez la commande suivante dans l’environnement de ligne de commande Exchange Management Shell : `Get-TransportService <servername> | Format-List *logpath*,*tracingpath*`
        
          - Dossiers des répertoires de collecte et de relecture de message. Par défaut, ces dossiers se trouvent sous le dossier %ExchangeInstallPath%TransportRoles. Pour déterminer les chemins d’accès aux journaux utilisés, exécutez la commande suivante dans l’environnement de ligne de commande Exchange Management Shell : `Get-TransportService <servername>| Format-List *dir*path*`
        
          - Les fichiers de la base de données de file d’attente, les fichiers de points de contrôle et les fichiers journaux. Par défaut, ils se trouvent dans le dossier %ExchangeInstallPath%TransportRoles\\Data\\Queue.
        
          - Les fichiers de la base de données de réputation de l’expéditeur, les fichiers de points de contrôle et les fichiers journaux. Par défaut, ils se trouvent dans le dossier %ExchangeInstallPath%TransportRoles\\Data\\SenderReputation.
        
          - Dossiers temporaires utilisés pour effectuer des conversions :
            
              - Par défaut, les conversions de contenu sont effectuées dans le dossier %TMP% du serveur Exchange.
            
              - Par défaut, des conversions du format RTF en MIME/HTML sont effectuées dans le dossier %ExchangeInstallPath%\\Working\\OleConverter.
        
          - Le composant d’analyse du contenu est utilisé par l’agent de programmes malveillants et la stratégie de prévention de perte de données (DLP). Par défaut, ces fichiers se trouvent dans le dossier %ExchangeInstallPath%FIP-FS.
    
      - **Service de transport de boîtes aux lettres**
        
          - Fichiers journaux, comme les journaux de connectivité. Par défaut, ces fichiers se trouvent dans les sous-dossiers du dossier %ExchangeInstallPath%TransportRoles\\Logs\\Mailbox. Pour déterminer les chemins d’accès aux journaux utilisés, exécutez la commande suivante dans l’environnement de ligne de commande Exchange Management Shell : `Get-MailboxTransportService <servername> | Format-List *logpath*`
    
      - **Messagerie unifiée**
        
          - Fichiers de grammaire pour des langues différentes, par exemple fr-FR ou es-ES. Par défaut, ils sont stockés dans les sous-dossiers du dossier %ExchangeInstallPath%UnifiedMessaging\\grammars.
        
          - Fichiers d’invites vocales, de messages d’accueil et d’information. Par défaut, ils sont stockés dans les sous-dossiers du dossier %ExchangeInstallPath%UnifiedMessaging\\Prompts
        
          - Fichiers de messagerie vocale temporairement stockés dans le dossier %ExchangeInstallPath%UnifiedMessaging\\voicemail.
        
          - Fichiers temporaires générés par la messagerie unifiée. Par défaut, ceux-ci sont stockés dans le dossier %ExchangeInstallPath%UnifiedMessaging\\temp.
    
      - **Installation**
        
          - Fichiers d’installation temporaires Exchange Server. Ces fichiers sont généralement situés dans %SystemRoot%\\Temp\\ExchangeSetup.
    
      - **Service de recherche Exchange**
        
          - Fichiers temporaires utilisés par le service de recherche Exchange et Microsoft Filter Pack pour effectuer la conversion de fichier dans un environnement bac à sable. Ces fichiers sont trouvent dans %SystemRoot%\\Temp\\OICE\_*\<GUID\>*\\.

<!-- end list -->

  - **serveurs d’accès au client**
    
      - **Composants Web**
        
          - Pour les serveurs utilisant les services IIS 7.0 (Internet Information Services), dossier de compression utilisé avec Microsoft Outlook Web App. Par défaut, le dossier de compression des services IIS 7.0 se trouve dans %systemroot%\\IIS Temporary Compressed Files.
        
          - Fichiers système IIS dans le dossier %SystemRoot%\\System32\\Inetsrv
        
          - Inetpub\\logs\\logfiles\\w3svc
        
          - Sous-dossiers dans %SystemRoot%\\Microsoft.NET\\Framework64\\v4.0.30319\\Temporary ASP.NET Files
    
      - **Journalisation des protocoles POP3 et IMAP4**
        
          - Dossier POP3 : %ExchangeInstallPath%Logging\\POP3
        
          - Dossier IMAP4 : %ExchangeInstallPath%Logging\\IMAP4
    
      - **Service de transport frontal**
        
          - Fichiers journaux, comme les journaux de connectivité et les journaux de protocole. Par défaut, ces fichiers se trouvent dans les sous-dossiers du dossier %ExchangeInstallPath%TransportRoles\\Logs\\FrontEnd. Pour déterminer les chemins d’accès aux journaux utilisés, exécutez la commande suivante dans l’environnement de ligne de commande Exchange Management Shell : `Get-FrontEndTransportService <servername> | Format-List *logpath*`
    
      - **Installation**
        
          - Fichiers temporaires d’installation d’Exchange Server. Ces fichiers sont généralement situés dans %SystemRoot%\\Temp\\ExchangeSetup.

Recommandations pour l’utilisation de l’analyse au niveau fichier avec Exchange 2013

## Exclusions de processus

De nombreux antivirus au niveau fichier prennent désormais en charge l’analyse de processus pouvant nuire à Microsoft Exchange en cas d’analyse des processus erronés. Par conséquent, vous devez exclure les processus suivants des antivirus au niveau fichier.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Processus</th>
<th>Chemin</th>
<th>Commentaires</th>
<th>Serveurs</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Dsamain.exe</p></td>
<td><p>%SystemRoot%\System32</p></td>
<td><p>Services AD LDS (Active Directory Lightweight Directory Services) sur les serveurs de transport Edge abonnés.</p></td>
<td><p>Serveurs de transport Edge</p></td>
</tr>
<tr class="even">
<td><p>EdgeTransport.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Processus de travail du service de transport Microsoft Exchange</p></td>
<td><p>Serveurs de boîtes aux lettres</p>
<p>Serveurs de transport Edge</p></td>
</tr>
<tr class="odd">
<td><p>fms.exe</p></td>
<td><p>%ExchangeInstallPath%FIP-FS\Bin</p></td>
<td><p>Composant d’analyse de contenu utilisé par l’agent anti-programme malveillant et dans la protection contre la perte de données (stratégie DLP).</p></td>
<td><p>Serveurs de boîtes aux lettres</p></td>
</tr>
<tr class="even">
<td><p>hostcontrollerservice.exe</p></td>
<td><p>%ExchangeInstallPath%Bin\Search\Ceres\HostController</p></td>
<td><p>Service de contrôleur d’hôte Microsoft Exchange Search (HostControllerService)</p></td>
<td><p>Serveurs de boîtes aux lettres</p>
<p>Serveurs d’accès au client</p></td>
</tr>
<tr class="odd">
<td><p>inetinfo.exe</p></td>
<td><p>%SystemRoot%\System32\inetsrv</p></td>
<td><p>Internet Information Services (IIS)</p></td>
<td><p>Serveurs de boîtes aux lettres</p>
<p>Serveurs d’accès au client</p></td>
</tr>
<tr class="even">
<td><p>Microsoft.Exchange.AntispamUpdateSvc.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Service de mise à jour anti-courrier indésirable Microsoft Exchange (MSExchangeAntispamUpdate)</p></td>
<td><p>Serveurs de boîtes aux lettres</p>
<p>Serveurs de transport Edge</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft.Exchange.ContentFilter.Wrapper.exe</p></td>
<td><p>%ExchangeInstallPath%TransportRoles\agents\Hygiene</p></td>
<td><p>Agent de filtrage du contenu</p></td>
<td><p>Serveurs de boîtes aux lettres</p>
<p>Serveurs de transport Edge</p></td>
</tr>
<tr class="even">
<td><p>Microsoft.Exchange.Diagnostics.Service.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Service de diagnostics Microsoft Exchange (MSExchangeDiagnostics)</p></td>
<td><p>Serveurs de boîtes aux lettres</p>
<p>Serveurs d’accès au client</p>
<p>Serveurs de transport Edge</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft.Exchange.Directory.TopologyService.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Service de topologie Active Directory de Microsoft Exchange (MSExchangeADTopology)</p></td>
<td><p>Serveurs de boîtes aux lettres</p>
<p>Serveurs d’accès au client</p></td>
</tr>
<tr class="even">
<td><p>Microsoft.Exchange.EdgeCredentialSvc.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Service d’informations d’identification Microsoft Exchange (MSExchangeEdgeCredential)</p></td>
<td><p>Serveurs de transport Edge</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft.Exchange.EdgeSyncSvc.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Service Microsoft Exchange EdgeSync (MSExchangeEdgeSync)</p></td>
<td><p>Serveurs de boîtes aux lettres</p></td>
</tr>
<tr class="even">
<td><p>Microsoft.Exchange.Imap4.exe</p></td>
<td><p>ExchangeInstallPath%FrontEnd\PopImap</p></td>
<td><p>Service Microsoft Exchange IMAP4 (MSExchangeImap4)</p></td>
<td><p>Serveurs d’accès au client</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft.Exchange.Imap4service.exe</p></td>
<td><p>%ExchangeInstallPath%ClientAccess\PopImap</p></td>
<td><p>Service principal Microsoft Exchange IMAP4 (MSExchangeIMAP4BE)</p></td>
<td><p>Serveurs de boîtes aux lettres</p></td>
</tr>
<tr class="even">
<td><p>Microsoft.Exchange.Pop3.exe</p></td>
<td><p>%ExchangeInstallPath%FrontEnd\PopImap</p></td>
<td><p>Service Microsoft Exchange POP3 (MSExchangePOP3)</p></td>
<td><p>Serveurs d’accès au client</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft.Exchange.Pop3service.exe</p></td>
<td><p>%ExchangeInstallPath%ClientAccess\PopImap</p></td>
<td><p>Service principal Microsoft Exchange POP3 (MSExchangePOP3BE)</p></td>
<td><p>Serveurs de boîtes aux lettres</p></td>
</tr>
<tr class="even">
<td><p>Microsoft.Exchange.ProtectedServiceHost.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Service d’hôte de service Microsoft Exchange (MSExchangeServiceHost)</p></td>
<td><p>Serveurs de boîtes aux lettres</p>
<p>Serveurs d’accès au client</p>
<p>Serveurs de transport Edge</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft.Exchange.RPCClientAccess.Service.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Service d’accès au client RPC Microsoft Exchange (MSExchangeRPC)</p></td>
<td><p>Serveurs de boîtes aux lettres</p></td>
</tr>
<tr class="even">
<td><p>Microsoft.Exchange.Search.Service.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Service Microsoft Exchange Search (MSExchangeFastSearch)</p></td>
<td><p>Serveurs de boîtes aux lettres</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft.Exchange.Servicehost.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Service d’hôte de service Microsoft Exchange (MSExchangeServiceHost)</p></td>
<td><p>Serveurs de boîtes aux lettres</p>
<p>Serveurs d’accès au client</p>
<p>Serveurs de transport Edge</p></td>
</tr>
<tr class="even">
<td><p>Microsoft.Exchange.Store.Service.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Service Banque d’informations de Microsoft Exchange (MSExchangeIS)</p></td>
<td><p>Serveurs de boîtes aux lettres</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft.Exchange.Store.Worker.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Processus de travail du service Banque d’informations de Microsoft Exchange</p></td>
<td><p>Serveurs de boîtes aux lettres</p></td>
</tr>
<tr class="even">
<td><p>Microsoft.Exchange.UM.CallRouter.exe</p></td>
<td><p>%ExchangeInstallPath%FrontEnd\CallRouter</p></td>
<td><p>Service de routeur d’appel de messagerie unifiée Microsoft Exchange (MSExchangeUMCR)</p></td>
<td><p>Serveurs d’accès au client</p></td>
</tr>
<tr class="odd">
<td><p>MSExchangeDagMgmt.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Service de gestion de groupe de disponibilité de base de données (DAG) Microsoft Exchange (MSExchangeDagMgmt)</p></td>
<td><p>Serveurs de boîtes aux lettres</p></td>
</tr>
<tr class="even">
<td><p>MSExchangeDelivery.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Service de remise de transport de boîte aux lettres Microsoft Exchange (MSExchangeDelivery)</p></td>
<td><p>Serveurs de boîtes aux lettres</p></td>
</tr>
<tr class="odd">
<td><p>MSExchangeFrontendTransport.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Service de transport frontal Microsoft Exchange (MSExchangeFrontEndTransport)</p></td>
<td><p>Serveurs d’accès au client</p></td>
</tr>
<tr class="even">
<td><p>MSExchangeHMHost.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Service de gestionnaire de contrôle d’intégrité Microsoft Exchange (MSExchangeHM)</p></td>
<td><p>Serveurs de boîtes aux lettres</p>
<p>Serveurs d’accès au client</p>
<p>Serveurs de transport Edge</p></td>
</tr>
<tr class="odd">
<td><p>MSExchangeHMWorker.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Processus de travail de service de gestionnaire de contrôle d’intégrité Microsoft Exchange</p></td>
<td><p>Serveurs de boîtes aux lettres</p>
<p>Serveurs d’accès au client</p>
<p>Serveurs de transport Edge</p></td>
</tr>
<tr class="even">
<td><p>MSExchangeMailboxAssistants.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Service Assistants de boîte aux lettres Microsoft Exchange (MSExchangeMailboxAssistants)</p></td>
<td><p>Serveurs de boîtes aux lettres</p></td>
</tr>
<tr class="odd">
<td><p>MSExchangeMailboxReplication.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Service de réplication de boîte aux lettres Microsoft Exchange (MSExchangeMailboxReplication)</p></td>
<td><p>Serveurs de boîtes aux lettres</p></td>
</tr>
<tr class="even">
<td><p>MSExchangeMigrationWorkflow.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Service de flux de travail de migration Microsoft Exchange (MSExchangeMigrationWorkflow)</p></td>
<td><p>Serveurs de boîtes aux lettres</p></td>
</tr>
<tr class="odd">
<td><p>MSExchangeRepl.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Service de réplication Microsoft Exchange (MSExchangeRepl)</p></td>
<td><p>Serveurs de boîtes aux lettres</p></td>
</tr>
<tr class="even">
<td><p>MSExchangeSubmission.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Service de dépôt de transport de boîte aux lettres Microsoft Exchange (MSExchangeSubmission)</p></td>
<td><p>Serveurs de boîtes aux lettres</p></td>
</tr>
<tr class="odd">
<td><p>MSExchangeTransport.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Service de transport Microsoft Exchange (MSExchangeTransport)</p></td>
<td><p>Serveurs de boîtes aux lettres</p>
<p>Serveurs de transport Edge</p></td>
</tr>
<tr class="even">
<td><p>MSExchangeTransportLogSearch.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Service de recherche de journal de transport Microsoft Exchange (MSExchangeTransportLogSearch)</p></td>
<td><p>Serveurs de boîtes aux lettres</p>
<p>Serveurs de transport Edge</p></td>
</tr>
<tr class="odd">
<td><p>MSExchangeThrottling.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Service de limitation Microsoft Exchange (MSExchangeThrottling)</p></td>
<td><p>Serveurs de boîtes aux lettres</p></td>
</tr>
<tr class="even">
<td><p>Noderunner.exe</p></td>
<td><p>%ExchangeInstallPath%Bin\Search\Ceres\Runtime\1.0</p></td>
<td><p>Service Microsoft Exchange Search (MSExchangeFastSearch)</p></td>
<td><p>Serveurs de boîtes aux lettres</p></td>
</tr>
<tr class="odd">
<td><p>OleConverter.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Convertit les messages RTF au format MIME/HTML pour les destinataires externes.</p></td>
<td><p>Serveurs de boîtes aux lettres</p></td>
</tr>
<tr class="even">
<td><p>ParserServer.exe</p></td>
<td><p>%ExchangeInstallPath%Bin\Search\Ceres\ParserServer</p></td>
<td><p>Service Microsoft Exchange Search (MSExchangeFastSearch)</p></td>
<td><p>Serveurs de boîtes aux lettres</p></td>
</tr>
<tr class="odd">
<td><p>Powershell.exe</p></td>
<td><p>C:\Windows\System32\WindowsPowerShell\v1.0</p></td>
<td><p>Environnement de ligne de commande Exchange Management Shell</p></td>
<td><p>Serveurs de boîtes aux lettres</p>
<p>Serveurs d’accès au client</p>
<p>Serveurs de transport Edge</p></td>
</tr>
<tr class="even">
<td><p>ScanEngineTest.exe</p></td>
<td><p>%ExchangeInstallPath%FIP-FS\Bin</p></td>
<td><p>Composant d’analyse de contenu utilisé par l’agent anti-programme malveillant et dans la protection contre la perte de données (stratégie DLP).</p></td>
<td><p>Serveurs de boîtes aux lettres</p></td>
</tr>
<tr class="odd">
<td><p>ScanningProcess.exe</p></td>
<td><p>%ExchangeInstallPath%FIP-FS\Bin</p></td>
<td><p>Composant d’analyse de contenu utilisé par l’agent anti-programme malveillant et dans la protection contre la perte de données (stratégie DLP).</p></td>
<td><p>Serveurs de boîtes aux lettres</p></td>
</tr>
<tr class="even">
<td><p>TranscodingService.exe</p></td>
<td><p>%ExchangeInstallPath%ClientAccess\Owa\Bin\DocumentViewing</p></td>
<td><p>Affichage de document WebReady dans Outlook Web App.</p></td>
<td><p>Serveurs de boîtes aux lettres</p></td>
</tr>
<tr class="odd">
<td><p>UmService.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Service de messagerie unifiée Microsoft Exchange (MSExchangeUM)</p></td>
<td><p>Serveurs de boîtes aux lettres</p></td>
</tr>
<tr class="even">
<td><p>UmWorkerProcess.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Processus de travail de service de messagerie unifiée Microsoft Exchange</p></td>
<td><p>Serveurs de boîtes aux lettres</p></td>
</tr>
<tr class="odd">
<td><p>UpdateService.exe</p></td>
<td><p>%ExchangeInstallPath%FIP-FS\Bin</p></td>
<td><p>Composant d’analyse de contenu utilisé par l’agent anti-programme malveillant et dans la protection contre la perte de données (stratégie DLP).</p></td>
<td><p>Serveurs de boîtes aux lettres</p></td>
</tr>
<tr class="even">
<td><p>W3wp.exe</p></td>
<td><p>%SystemRoot%\System32\inetsrv</p></td>
<td><p>Internet Information Services (IIS)</p></td>
<td><p>Serveurs de boîtes aux lettres</p>
<p>Serveurs d’accès au client</p></td>
</tr>
</tbody>
</table>


Recommandations pour l’utilisation de l’analyse au niveau fichier avec Exchange 2013

## Exclusions d’extensions de nom de fichier

Outre l’exclusion de répertoires et de processus spécifiques, en cas d’échec des exclusions de répertoires ou de déplacement de fichiers hors de leurs emplacements par défaut, vous devez exclure les extensions de nom de fichier spécifiques à Exchange.

  - Extensions relatives aux applications :
    
      - .config
    
      - .dia
    
      - .wsb

<!-- end list -->

  - Extensions relatives aux bases de données :
    
      - .chk
    
      - .edb
    
      - .jrs
    
      - .jsl
    
      - .log
    
      - .que

<!-- end list -->

  - Extensions relatives au carnet d’adresses en mode hors connexion :
    
      - .lzx

<!-- end list -->

  - Extensions relatives à l’index de contenu :
    
      - .ci
    
      - .dir
    
      - .wid
    
      - .000
    
      - .001
    
      - .002

<!-- end list -->

  - Extensions relatives à la messagerie unifiée :
    
      - .cfg
    
      - .grxml

<!-- end list -->

  - Extensions relatives aux mesures de groupe :
    
      - .dsc
    
      - .txt

Recommandations pour l’utilisation de l’analyse au niveau fichier avec Exchange 2013

