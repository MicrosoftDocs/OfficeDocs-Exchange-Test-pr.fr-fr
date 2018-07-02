---
title: 'Configurer l’authentification OAuth entre des organisations Exchange et Exchange Online: Exchange 2013 Help'
TOCTitle: Configurer l’authentification OAuth entre des organisations Exchange et Exchange Online
ms:assetid: f703e153-98e2-4268-8a6e-07a86b0a1d22
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dn594521(v=EXCHG.150)
ms:contentKeyID: 61170769
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configurer l’authentification OAuth entre des organisations Exchange et Exchange Online

 

_**Sapplique à :** Exchange Online, Exchange Server 2013_

_**Dernière rubrique modifiée :** 2016-12-09_

Les déploiements hybrides Exchange 2013 uniquement configurent l’authentification OAuth lors de l’utilisation de l’Assistant Configuration hybride. Pour les déploiements hybrides Exchange 2013/2010 et Exchange 2013/2007 mixtes, la nouvelle connexion d’authentification basée sur OAuth de déploiement hybride entre les organisations Office 365 et Exchange locales n’est pas configurée par l’Assistant Configuration hybride. Ces déploiements continuent à utiliser le processus d’approbation de fédération par défaut. Toutefois, certaines fonctionnalités d’Exchange 2013 sont totalement disponibles dans votre organisation uniquement en utilisant le nouveau protocole d’authentification OAuth d’Exchange.

Le nouveau processus d’authentification OAuth d’Exchange permet actuellement d’activer les fonctionnalités Exchange suivantes :

  - Gestion des enregistrements de messagerie (MRM)

  - Découverte électronique locale Exchange

  - Archivage local Exchange

Nous recommandons à toutes les organisations Exchange mixtes qui implémentent un déploiement hybride avec Exchange 2013 et Exchange Online de configurer l’authentification OAuth Exchange après la configuration de leur déploiement hybride avec l’Assistant Configuration hybride.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159813.important(EXCHG.150).gif" title="Important" alt="Important" />Important :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Si votre organisation sur site utilise uniquement des serveurs Exchange 2013 avec la mise à jour cumulative 5 ou version ultérieure installée, exécutez l’assistant de déploiement hybride au lieu de suivre les étapes décrites dans cette rubrique.<br />
Cette fonctionnalité d’Exchange Server 2013 n’est pas entièrement compatible avec les systèmes Office 365 exécutés par 21Vianet en Chine et certaines limitations de fonctionnalités peuvent s’appliquer. Pour plus d’informations, voir <a href="https://go.microsoft.com/fwlink/?linkid=313640">En savoir plus sur Office 365 exécuté par 21Vianet</a>.</td>
</tr>
</tbody>
</table>


## Ce qu’il faut savoir avant de commencer

  - Durée d’exécution estimée de cette tâche : 15 minutes

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l’entrée d’autorisations « Fédération et certificats » dans la rubrique [Autorisations d’infrastructure Exchange et Shell](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md).

  - La configuration de votre déploiement hybride à l’aide de l’Assistant Déploiement hybride est terminée. Pour plus d’informations, consultez la rubrique [Déploiements hybrides Exchange Server](https://technet.microsoft.com/fr-fr/library/jj200581\(v=exchg.150\)).

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


## Comment configurer l’authentification OAuth entre vos organisations Exchange Online et Exchange locale ?

## Étape 1 : créer un objet serveur d’autorisation pour votre organisation Exchange Online

Pour cette procédure, vous devez spécifier un domaine vérifié pour votre organisation Exchange Online. Ce domaine doit être le même domaine que celui utilisé comme domaine SMTP principal pour les comptes de messagerie informatiques. Ce domaine est appelé *\<votre domaine vérifié\>* dans la procédure suivante.

Exécutez la commande suivante dans l’environnement de ligne de commande Exchange Management Shell (Exchange PowerShell) dans votre organisation Exchange locale.

    New-AuthServer -Name "WindowsAzureACS" -AuthMetadataUrl https://accounts.accesscontrol.windows.net/<your verified domain>/metadata/json/1

## Étape 2 : activer l’application partenaire pour votre organisation Exchange Online

Exécutez la commande suivante dans Exchange PowerShell dans votre organisation Exchange locale.

    Get-PartnerApplication |  ?{$_.ApplicationIdentifier -eq "00000002-0000-0ff1-ce00-000000000000" -and $_.Realm -eq ""} | Set-PartnerApplication -Enabled $true

## Étape 3 : exporter le certificat d’autorisation local

Dans cette étape, vous devez exécuter un script PowerShell pour exporter le certificat d’autorisation local, qui sera importé dans votre organisation Exchange Online à l’étape suivante.

1.  Enregistrez le texte suivant dans un fichier de script PowerShell nommé, par exemple, **ExportAuthCert.ps1**.
    
        $thumbprint = (Get-AuthConfig).CurrentCertificateThumbprint
         
        if((test-path $env:SYSTEMDRIVE\OAuthConfig) -eq $false)
        {
            md $env:SYSTEMDRIVE\OAuthConfig
        }
        cd $env:SYSTEMDRIVE\OAuthConfig
         
        $oAuthCert = (dir Cert:\LocalMachine\My) | where {$_.Thumbprint -match $thumbprint}
        $certType = [System.Security.Cryptography.X509Certificates.X509ContentType]::Cert
        $certBytes = $oAuthCert.Export($certType)
        $CertFile = "$env:SYSTEMDRIVE\OAuthConfig\OAuthCert.cer"
        [System.IO.File]::WriteAllBytes($CertFile, $certBytes)

2.  Dans Exchange PowerShell dans votre organisation Exchange locale, exécutez le script PowerShell que vous avez créé à l’étape précédente. Par exemple :
    
        .\ExportAuthCert.ps1

## Étape 4 : télécharger le certificat d’autorisation local vers le service ACS de Windows Azure Active Directory

Ensuite, vous devez utiliser Windows PowerShell pour télécharger le certificat d'autorisation local que vous avez exporté à l'étape précédente dans Services de contrôle d’accès Azure Active Directory (ACS). Pour ce faire, la cmdlet Module Azure Active Directory pour Windows PowerShell doit être installée. Si elle n'est pas installée, accédez à <https://aka.ms/aadposh> pour installer la cmdlet Module Azure Active Directory pour Windows PowerShell. Effectuez les étapes suivantes une fois que la cmdlet Module Azure Active Directory pour Windows PowerShell est installée.

1.  Cliquez sur le raccourci **Module Windows Azure Active Directory pour Windows PowerShell** afin d’ouvrir un espace de travail Windows PowerShell pour lequel les cmdlets Azure AD sont installées. Dans cette étape, toutes les commandes seront exécutées à l’aide de la console Windows PowerShell pour Azure Active Directory.

2.  Enregistrez le texte suivant dans un fichier de script PowerShell nommé, par exemple, **UploadAuthCert.ps1**.
    
        Connect-MsolService;
        Import-Module msonlineextended;
        
        $CertFile = "$env:SYSTEMDRIVE\OAuthConfig\OAuthCert.cer"
        
        $objFSO = New-Object -ComObject Scripting.FileSystemObject;
        $CertFile = $objFSO.GetAbsolutePathName($CertFile);
        
        $cer = New-Object System.Security.Cryptography.X509Certificates.X509Certificate
        $cer.Import($CertFile);
        $binCert = $cer.GetRawCertData();
        $credValue = [System.Convert]::ToBase64String($binCert);
        
        $ServiceName = "00000002-0000-0ff1-ce00-000000000000";
        
        $p = Get-MsolServicePrincipal -ServicePrincipalName $ServiceName
        New-MsolServicePrincipalCredential -AppPrincipalId $p.AppPrincipalId -Type asymmetric -Usage Verify -Value $credValue

3.  Exécutez le script PowerShell que vous avez créé à l’étape précédente. Par exemple :
    
        .\UploadAuthCert.ps1

4.  Une fois le script lancé, une boîte de dialogue d’informations d’identification s’affiche. Entrez les informations d’identification du compte d’administrateur client de votre organisation Microsoft Online Azure AD. Après avoir exécuté le script, laissez la session Windows PowerShell pour Azure AD ouverte. Vous l’utiliserez pour exécuter un script PowerShell à l’étape suivante.

## Étape 5 : enregistrer toutes les autorités de nom d’hôte pour vos points de terminaison HTTP Exchange locaux externes auprès de Windows Azure Active Directory

Dans cette étape, vous devez exécuter le script pour chaque point de terminaison de votre organisation Exchange locale qui est accessible publiquement. Nous vous recommandons d’utiliser des caractères génériques, si possible. Par exemple, supposons qu’Exchange est disponible en externe sur **https://mail.contoso.com/ews/exchange.asmx**. Dans ce cas, un seul caractère générique peut être utilisé : **\*.contoso.com**. Il couvre les points de terminaison autodiscover.contoso.com et mail.contoso.com. Toutefois, il ne couvre pas le domaine de niveau supérieur, soit **contoso.com**. Dans le cas où vos serveurs d’accès au client Exchange 2013 sont accessibles en externe avec l’autorité de nom d’hôte de niveau supérieur, celle-ci doit également être enregistrée en tant que **contoso.com**. Il n’y a pas de limite concernant l’enregistrement d’autorités de nom d’hôte externes supplémentaires.

Si vous avez des doutes concernant les points de terminaison Exchange externes de votre organisation Exchange locale, vous pouvez obtenir une liste des points de terminaison de services web configurés externes en exécutant la commande suivante dans Exchange PowerShell, dans votre organisation Exchange locale :

    Get-WebServicesVirtualDirectory | FL ExternalUrl

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Pour que le script suivant soit correctement exécuté, Windows PowerShell pour Azure Active Directory doit être connecté à votre client Azure AD, comme expliqué à l’étape 4 de la section précédente.</td>
</tr>
</tbody>
</table>


1.  Enregistrez le texte suivant dans un fichier de script PowerShell nommé, par exemple, **RegisterEndpoints.ps1**. Cet exemple utilise un caractère générique pour enregistrer tous les points de terminaison pour contoso.com. Remplacez **contoso.com** par une autorité de nom d’hôte pour votre organisation Exchange locale.
    
        $externalAuthority="*.contoso.com"
         
        $ServiceName = "00000002-0000-0ff1-ce00-000000000000";
         
        $p = Get-MsolServicePrincipal -ServicePrincipalName $ServiceName;
         
        $spn = [string]::Format("{0}/{1}", $ServiceName, $externalAuthority);
        $p.ServicePrincipalNames.Add($spn);
         
        Set-MsolServicePrincipal -ObjectID $p.ObjectId -ServicePrincipalNames $p.ServicePrincipalNames;

2.  Dans Windows PowerShell pour Azure Active Directory, exécutez le script Windows PowerShell que vous avez créé à l’étape précédente. Par exemple :
    
        .\RegisterEndpoints.ps1

## Étape 6 : créer un connecteur intra-organisationnel à partir de votre organisation locale vers Office 365

Vous devez définir une adresse cible pour vos boîtes aux lettres hébergées dans Exchange Online. Cette adresse cible est créée automatiquement lors de la création de votre client Office 365. Par exemple, si le domaine de votre organisation hébergé dans le client Office 365 est « contoso.com », votre adresse de service cible sera « contoso.mail.onmicrosoft.com ».

Avec Exchange PowerShell, exécutez la cmdlet suivante dans votre organisation locale :

    New-IntraOrganizationConnector -name ExchangeHybridOnPremisesToOnline -DiscoveryEndpoint https://outlook.office365.com/autodiscover/autodiscover.svc -TargetAddressDomains <your service target address>

## Étape 7 : créer un connecteur intra-organisationnel à partir de votre client Office 365 vers votre organisation Exchange locale

Vous devez définir une adresse cible pour vos boîtes aux lettres hébergées dans votre organisation locale. Si l’adresse SMTP principale de votre organisation est « contoso.com », il s’agira de « contoso.com ».

Vous devez également définir le point de terminaison de découverte automatique externe de votre organisation locale. Si votre société est « contoso.com », il s’agit généralement de l’un des éléments suivants :

  - https://autodiscover.\<votre domaine SMTP principal\>/autodiscover/autodiscover.svc

  - https://\<votre domaine SMTP principal\>/autodiscover/autodiscover.svc

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Vous pouvez utiliser la cmdlet <a href="https://technet.microsoft.com/fr-fr/library/dn551183(v=exchg.150)">Get-IntraOrganizationConfiguration</a> pour vos clients locaux et Office 365 afin de déterminer les valeurs des points de terminaison requises par la cmdlet <a href="https://technet.microsoft.com/fr-fr/library/dn551178(v=exchg.150)">New-IntraOrganizationConnector</a>.</td>
</tr>
</tbody>
</table>


À l’aide de Windows PowerShell, exécutez la cmdlet suivante :

    $UserCredential = Get-Credential
    
    $Session = New-PSSession -ConfigurationName Microsoft.Exchange -ConnectionUri https://outlook.office365.com/powershell-liveid/ -Credential $UserCredential -Authentication Basic -AllowRedirection
    
    Import-PSSession $Session
    
    New-IntraOrganizationConnector -name ExchangeHybridOnlineToOnPremises -DiscoveryEndpoint <your on-premises Autodiscover endpoint> -TargetAddressDomains <your on-premises SMTP domain>

## Étape 8 : configurer un objet AvailabilityAddressSpace pour tous les serveurs Exchange de version antérieure à 2013 SP1

Lors de la configuration d’un déploiement hybride dans une organisation antérieure à Exchange 2013, vous devez installer au moins un serveur Exchange 2013 SP1 ou ultérieur avec les rôles serveur d’accès au client et serveur de boîtes aux lettres dans votre organisation Exchange existante. Les serveurs d’accès au client et de boîtes aux lettres Exchange 2013 sont utilisés comme serveurs frontaux et coordonnent les communications entre votre organisation Exchange locale existante et l’organisation Exchange Online. Cette communication englobe le transport des messages et les caractéristiques de messagerie entre l’organisation sur site et l’organisation Exchange Online. Nous recommandons vivement d’installer plusieurs serveurs Exchange 2013 dans votre organisation locale pour renforcer la fiabilité et la disponibilité des fonctionnalités de déploiement hybride.

Dans un déploiement mixte avec Exchange 2013/2010 ou Exchange 2013/2007, nous vous recommandons d’utiliser des serveurs d’accès au client exécutant Exchange 2013 SP1 ou version ultérieure en tant que serveurs frontaux Internet pour votre organisation locale. Toutes les demandes de services web Exchange (EWS) provenant d’Office 365 et d’Exchange Online doivent se connecter à un serveur d’accès au client Exchange 2013 dans votre déploiement local. En outre, toutes les demandes EWS provenant de vos organisations Exchange locales pour Exchange Online doivent être redirigées via proxy par l’intermédiaire d’un serveur d’accès au client exécutant Exchange 2013 SP1 ou version ultérieure. Puisque ces serveurs d’accès au client Exchange 2013 doivent gérer des demandes EWS entrantes et sortantes supplémentaires, il est important qu’un nombre suffisant de serveurs d’accès au client Exchange 2013 soit disponible pour gérer la charge de travail et fournir une redondance de connexion. Le nombre de serveurs d’accès au client nécessaire dépendra de la quantité moyenne de demandes EWS et varie en fonction de l’organisation.

Avant d’effectuer l’étape suivante, vérifiez que :

  - La version des serveurs hybrides frontaux est Exchange 2013 SP1 ou ultérieure

  - Vous disposez d’une URL EWS externe unique pour les serveurs Exchange 2013. Le client Office 365 doit se connecter à ces serveurs pour que les demandes informatiques de fonctionnalités hybrides fonctionnent correctement.

  - Les serveurs ont les rôles serveur de boîtes aux lettres et serveur d’accès au client

  - Tout serveur de boîtes aux lettres et d’accès au client Exchange 2010/2007 existant dispose de la dernière mise à jour cumulative ou du dernier Service Pack (SP).
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Les serveurs de boîtes aux lettres Exchange 2010/2007 peuvent continuer à utiliser des serveurs d’accès au client Exchange 2010/2007 pour les serveurs frontaux pour des connexions de fonctionnalités non hybrides. Les demandes de fonctionnalité de déploiement hybride du client Office 365 doivent se connecter aux serveurs Exchange 2013.</td>
    </tr>
    </tbody>
    </table>


Un paramètre *AvailabilityAddressSpace* doit être configuré sur les serveurs d’accès au client antérieurs à Exchange 2013 pointant vers le point de terminaison des services web Exchange de vos serveurs d’accès au client Exchange 2013 SP1 locaux. Ce point de terminaison est le même que celui précédemment décrit à l’étape 5 ou peut être déterminé par l’exécution de la cmdlet suivante sur votre serveur d’accès au client Exchange 2013 SP1 local :

    Get-WebServicesVirtualDirectory | FL AdminDisplayVersion,ExternalUrl

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Si des informations de répertoire virtuel sont renvoyées par plusieurs serveurs, assurez-vous que vous utilisez le point de terminaison renvoyé pour le serveur d’accès au client Exchange 2013 SP1. Cela affichera une valeur égale ou supérieure à 15.0 (build 847.32) pour le paramètre <em>AdminDisplayVersion</em>.</td>
</tr>
</tbody>
</table>


Pour configurer l’objet *AvailabilityAddressSpace*, utilisez Exchange PowerShell et exécutez l’applet de commande suivante dans votre organisation locale :

    Add-AvailabilityAddressSpace -AccessMethod InternalProxy -ProxyUrl <your on-premises External Web Services URL> -ForestName <your Office 365 service target address> -UseServiceAccount $True

## Comment savoir si cela a fonctionné ?

Vous pouvez vérifier que l’authentification OAuth est correcte à l’aide de la cmdlet [Test-OAuthConnectivity](https://technet.microsoft.com/fr-fr/library/jj218623\(v=exchg.150\)). Cette cmdlet vérifie que les points de terminaison Exchange et Exchange Online locaux peuvent authentifier correctement les demandes l’un de l’autre.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159813.important(EXCHG.150).gif" title="Important" alt="Important" />Important :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Lors de la connexion à votre organisation Exchange Online avec Remote PowerShell, il se peut que vous deviez utiliser le paramètre <em>AllowClobber</em> avec la cmdlet <strong>Import-PSSession</strong> pour importer les dernières commandes dans la session PowerShell locale.</td>
</tr>
</tbody>
</table>


Pour vérifier que votre organisation Exchange locale peut se connecter correctement à Exchange Online, exécutez la commande suivante dans Exchange PowerShell dans votre organisation locale :

    Test-OAuthConnectivity -Service EWS -TargetUri https://outlook.office365.com/ews/exchange.asmx -Mailbox <On-Premises Mailbox> -Verbose | fl

Pour vérifier que votre organisation Exchange Online peut se connecter correctement à votre organisation Exchange locale, utilisez [Remote PowerShell](https://technet.microsoft.com/fr-fr/library/jj984289\(v=exchg.150\)) pour vous connecter à votre organisation Exchange Online et exécutez la commande suivante :

    Test-OAuthConnectivity -Service EWS -TargetUri <external hostname authority of your Exchange On-Premises deployment>/metadata/json/1 -Mailbox <Exchange Online Mailbox> -Verbose | fl

Par exemple, Test-OAuthConnectivity -Service EWS -TargetUri https://lync.contoso.com/metadata/json/1 -Mailbox ExchangeOnlineBox1 -Verbose | fl

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159813.important(EXCHG.150).gif" title="Important" alt="Important" />Important :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Vous pouvez ignorer l’erreur « Aucune boîte aux lettres n’est associée à l’adresse SMTP ». Ce qui importe, c’est que la valeur renvoyée par le paramètre <em>ResultTask</em> soit <strong>Réussite</strong>. Par exemple, la dernière section de la sortie de test doit être :<br />
<code>ResultType: Success</code><br />
<code>Identity: Microsoft.Exchange.Security.OAuth.ValidationResultNodeId</code><br />
<code>IsValid: True</code><br />
<code>ObjectState: New</code></td>
</tr>
</tbody>
</table>


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

