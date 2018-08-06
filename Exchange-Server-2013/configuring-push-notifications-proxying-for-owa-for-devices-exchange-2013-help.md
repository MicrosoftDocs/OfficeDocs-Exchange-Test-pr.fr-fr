---
title: 'Config. de l’envoi par proxy de noti. Push pour OWA pour les périphériques | Microsoft Docs'
TOCTitle: Configuration de l’envoi par proxy de notifications Push pour OWA pour les périphériques
ms:assetid: c0f4912d-8bd3-4a54-9097-03619c645c6a
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dn511017(v=EXCHG.150)
ms:contentKeyID: 59954723
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configuration de l’envoi par proxy de notifications Push pour OWA pour les périphériques

 

_**Sapplique à :** Exchange Online, Exchange Server 2013_

_**Dernière rubrique modifiée :** 2016-12-09_

L’activation des notifications Push pour OWA pour les périphériques (OWA pour iPhone et OWA pour iPad) pour un déploiement sur site de Microsoft Exchange 2013 permet à l’utilisateur de recevoir des mises à jour sur l’icône Outlook Web App sur son OWA pour iPhone et OWA pour iPad, qui indique le nombre de messages non vus dans sa boîte de réception. Si les notifications push ne sont ni configurées ni activées, un utilisateur disposant d’OWA pour les périphériques n’a aucun moyen de savoir si sa boîte de réception contient des messages non vus, sans lancer l’application. Quand un nouveau message est disponible, le badge OWA pour les périphériques est mis à jour sur le périphérique de l’utilisateur et ressemble au badge ci-après.

![Badge OWA pour les appareils](images/Dn511017.f399ba74-5395-4d24-ae7d-d16bf0ac7b35(EXCHG.150).png "Badge OWA pour les appareils")

## Comment activer les notifications Push ?

Pour activer les notifications Push, les serveurs Exchange 2013 sur site doivent se connecter au service de notifications Push Office 365 pour envoyer des notifications Push aux iPhones et aux iPads. Les serveurs Exchange 2013 sur site routent leurs notifications de mise à jour via les services de notifications Office 365. Il n’est alors plus nécessaire d’inscrire les comptes de développeur avec des services de notifications Push tiers. Le schéma suivant montre le processus par lequel les utilisateurs d’iPhone et d’iPad obtiennent des mises à jour de badge pour les messages non vus.

![Processus pour les notifications Push](images/Dn511017.36764ce6-7351-492f-a17e-c42b781e2781(EXCHG.150).jpg "Processus pour les notifications Push")

Pour activer les notifications Push, l’administrateur doit effecteur les actions suivantes :

1.  inscrire votre organisation dans Office 365 pour les entreprises ;

2.  mettre à jour tous les serveurs sur site vers la mise à jour cumulative 3 (CU3) d’Exchange Server 2013 ou une version ultérieure ;

3.  configurer Exchange 2013 sur site pour l’authentification d’Office 365 ;

4.  activer les notifications Push du serveur Exchange Server 2013 sur site vers Office 365 et vérifier que les notifications Push fonctionnent.

## Inscrire votre organisation dans Office 365 pour les entreprises

Office 365 est un service informatique destiné à répondre aux besoins de sécurité robuste, de fiabilité et de productivité de votre organisation. Office 365 se réfère à des plans d’abonnement qui comprennent l’accès aux applications Office ainsi que d’autres services de productivité qui sont activés via Internet (services en nuage), comme les conférences web de Lync et la messagerie hébergée Exchange Online pour les entreprises.

De nombreux plans Office 365 comprennent également la version de bureau des dernières applications Office, que les utilisateurs peuvent installer sur plusieurs ordinateurs et périphériques. Tous les plans Office 365 sont payés sur la base d’un abonnement mensuel ou annuel. Pour en savoir plus ou pour vous inscrire dans Office 365 pour votre organisation, voir [Présentation d’Office 365 pour les entreprises](http://go.microsoft.com/fwlink/?linkid=335705). Pour en savoir plus sur les services offerts par Office 365, voir [Description du service Office 365](http://go.microsoft.com/fwlink/?linkid=335704).

## Effectuer une mise à jour vers CU3 ou version ultérieure

La mise à jour cumulative 3 (CU3) pour Exchange Server 2013 résout les problèmes détectés dans Exchange Server 2013 puisque le logiciel a été publié depuis la version de publication (RTM). Elle contient tous les problèmes et correctifs déjà présents dans CU1 et CU2, ainsi que d’autres correctifs et mises à jour postérieurs à la publication de CU2. Cette mise à jour est fortement recommandée pour tous les clients Exchange Server 2013 sur site, mais elle est obligatoire pour les notifications Push. Pour en savoir plus sur les mises à jour cumulatives, y compris CU3, voir [Mises à jour pour Exchange 2013](updates-for-exchange-2013-exchange-2013-help.md).

## Configurer Exchange 2013 sur site pour l’authentification d’Office 365

L’approche utilisée par Exchange Server 2013 consiste à utiliser une seule méthode standardisée pour l’authentification de serveur à serveur. [Exchange Server 2013](http://go.microsoft.com/fwlink/?linkid=290946) (ainsi que [Lync Server 2013](http://go.microsoft.com/fwlink/?linkid=273796) et [SharePoint 2013](http://go.microsoft.com/fwlink/?linkid=335701)) et [Office 2013](http://go.microsoft.com/fwlink/?linkid=335696) prennent en charge le protocole OAuth (Open Authorization) pour l’autorisation et l’authentification de serveur à serveur. Avec OAuth, un protocole d’autorisation standard utilisé par un certain nombre de sites web majeurs, les informations d’identification et les mots de passe des utilisateurs ne sont pas passés d’un ordinateur à un autre. Au lieu de cela, l’authentification et l’autorisation reposent sur les jetons de sécurité OAuth. Ces jetons donnent accès à un ensemble de ressources spécifique, pour une période donnée.

L’authentification OAuth implique généralement trois composants : un serveur d’autorisation unique et deux domaines qui doivent communiquer entre eux. Les jetons de sécurité sont émis par le serveur d’autorisation (également appelé serveur de jeton de sécurité) pour les deux domaines qui doivent communiquer entre eux. Ces jetons vérifient que les communications provenant d’un domaine doivent être approuvées par l’autre domaine. Par exemple, le serveur d’autorisation peut émettre des jetons qui vérifient que les utilisateurs d’un domaine Lync Server 2013 spécifique peuvent accéder à un domaine Exchange 2013 donné, et vice versa.

> [!TIP]  
> Un domaine est un conteneur de sécurité.


Toutefois, pour l’authentification de serveur à serveur sur site, il est inutile d’utiliser un serveur de jeton tiers. Les produits serveur tels que Lync Server 2013 et Exchange 2013 disposent chacun d’un serveur de jeton intégré qui peut être utilisé à des fins d’authentification avec d’autres serveurs Microsoft (tels que SharePoint Server) qui prennent en charge l’authentification de serveur à serveur. Par exemple, Lync Server 2013 peut émettre et signer un jeton de sécurité par lui-même, puis utiliser ce jeton pour communiquer avec Exchange 2013. Dans un cas comme celui-ci, aucun serveur de jeton tiers n’est nécessaire.

Pour configurer l’authentification de serveur à serveur pour une implémentation sur site d’Exchange Server 2013 sur Office 365, vous devez suivre les deux étapes suivantes :

  - **Étape 1 - Attribuer un certificat à l’émetteur de jeton intégré du serveur Exchange sur site.** Tout d’abord, si aucun certificat n’a été créé auparavant, un administrateur Exchange sur site doit utiliser le script d’environnement de ligne de commande Exchange Management Shell suivant pour en créer un et pour l’attribuer à l’émetteur de jeton intégré du serveur Exchange sur site. Il s’agit d’un processus unique. Une fois le certificat créé, celui-ci doit être réutilisé pour d’autres scénarios d’authentification et ne doit pas être remplacé. Assurez-vous que vous mettez à jour la valeur de *$tenantDomain* pour qu’elle corresponde au nom de votre domaine. Pour ce faire, copiez et collez le code suivant.
    
    > [!WARNING]  
    > Copiez et collez le code dans un éditeur de texte comme le Bloc-notes, puis enregistrez-le avec une extension .ps1. Cela facilite l’exécution des scripts Shell.
    
        # Make sure to update the following $tenantDomain with your Office 365 tenant domain.
        
        $tenantDomain = "Fabrikam.com"
        
        # Check whether the cert returned from Get-AuthConfig is valid and keysize must be >= 2048
        
        $c = Get-ExchangeCertificate | ?{$_.CertificateDomains -eq $env:USERDNSDOMAIN -and $_.Services -ge "SMTP" -and $_.PublicKeySize -ge 2048 -and $_.FriendlyName -match "OAuth"}
        If ($c.Count -eq 0)
        {
            Write-Host "Creating certificate for oAuth..."
            $ski = [System.Guid]::NewGuid().ToString("N")
            $friendlyName = "Exchange S2S OAuth"
            New-ExchangeCertificate -FriendlyName $friendlyName -DomainName $env:USERDNSDOMAIN -Services Federation -KeySize 2048 -PrivateKeyExportable $true -SubjectKeyIdentifier $ski
            $c = Get-ExchangeCertificate | ?{$_.friendlyname -eq $friendlyName}
        }
        ElseIf ($c.Count -gt 1)
        {
            $c = $c[0]
        }
        
        $a = $c | ?{$_.Thumbprint -eq (get-authconfig).CurrentCertificateThumbprint}
        If ($a.Count -eq 0)
        {
            Set-AuthConfig -CertificateThumbprint $c.Thumbprint
        }
        Write-Host "Configured Certificate Thumbprint is:"(get-authconfig).CurrentCertificateThumbprint
        
        # Export the certificate
        
        Write-Host "Exporting certificate..."
        if((test-path $env:SYSTEMDRIVE\OAuthConfig) -eq $false)
        {
            md $env:SYSTEMDRIVE\OAuthConfig
        }
        cd $env:SYSTEMDRIVE\OAuthConfig
        
        $oAuthCert = (dir Cert:\LocalMachine\My) | where {$_.FriendlyName -match "OAuth"}
        $certType = [System.Security.Cryptography.X509Certificates.X509ContentType]::Cert
        $certBytes = $oAuthCert.Export($certType)
        $CertFile = "$env:SYSTEMDRIVE\OAuthConfig\OAuthCert.cer"
        [System.IO.File]::WriteAllBytes($CertFile, $certBytes)
        
        # Set AuthServer
        $authServer = Get-AuthServer MicrosoftSts;
        if ($authServer.Length -eq 0)
        {
            Write-Host "Creating AuthServer Config..."
            New-AuthServer MicrosoftSts -AuthMetadataUrl https://accounts.accesscontrol.windows.net/metadata/json/1/?realm=$tenantDomain
        }
        elseif ($authServer.AuthMetadataUrl -ne "https://accounts.accesscontrol.windows.net/metadata/json/1/?realm=$tenantDomain")
        {
            Write-Warning "AuthServer config already exists but the AuthMetdataUrl doesn't match the appropriate value. Updating..."
            Set-AuthServer MicrosoftSts -AuthMetadataUrl https://accounts.accesscontrol.windows.net/metadata/json/1/?realm=$tenantDomain
        }
        else
        {
            Write-Host "AuthServer Config already exists."
        }
        Write-Host "Complete."
    
    Le résultat attendu devrait être semblable à la sortie suivante.
    
        Configured Certificate Thumbprint is: 7595DBDEA83DACB5757441D44899BCDB9911253C
        Exporting certificate...
        Complete.
    
    > [!WARNING]  
    > Avant de poursuivre, la cmdlet Module Azure Active Directory pour Windows PowerShell est requise. Si la cmdlet Module Azure Active Directory pour Windows PowerShell (précédemment appelée le module Microsoft Online Services pour Windows PowerShell) n'a pas été installée, vous pouvez l'installer à partir de <a href="http://aka.ms/aadposh">Gérer Azure Active Directory à l’aide de Windows PowerShell</a>.


  - **Étape 2 - Configurer Office 365 pour qu’il communique avec Exchange 2013 sur site.** Configurez le serveur Office 365 qui communiquera avec Exchange Server 2013 en tant qu’application partenaire. Par exemple, si Exchange Server 2013 sur site doit communiquer avec Office 365, vous devez configurer Exchange sur site en tant qu’application partenaire. Une application partenaire est une application avec laquelle Exchange 2013 peut directement échanger des jetons de sécurité, sans avoir à passer par un serveur de jeton de sécurité tiers. Un administrateur Exchange 2103 sur site doit utiliser le script d’environnement de ligne de commande Exchange Management Shell suivant pour configurer le client Office 365 avec lequel Exchange 2013 communiquera en tant qu’application partenaire. Lors de l’exécution, vous serez invité à entrer le nom d’utilisateur et le mot de passe de l’administrateur du domaine client Office 365 (par exemple, administrateur@fabrikam.com). Assurez-vous que vous mettez à jour la valeur de *$CertFile* sur l’emplacement du certificat, si ce dernier n’a pas été créé à partir du script précédent. Pour ce faire, copiez et collez le code suivant.
    
        # Make sure to update the following $CertFile with the path to the cert if not using the previous script.
        
        $CertFile = "$env:SYSTEMDRIVE\OAuthConfig\OAuthCert.cer"
        
        If (Test-Path $CertFile)
        {
            $ServiceName = "00000002-0000-0ff1-ce00-000000000000";
        
            $objFSO = New-Object -ComObject Scripting.FileSystemObject;
            $CertFile = $objFSO.GetAbsolutePathName($CertFile);
        
            $cer = New-Object System.Security.Cryptography.X509Certificates.X509Certificate
            $cer.Import($CertFile);
            $binCert = $cer.GetRawCertData();
            $credValue = [System.Convert]::ToBase64String($binCert);
        
            Write-Host "Please enter the administrator user name and password of the Office 365 tenant domain..."
        
            Connect-MsolService;
            Import-Module msonlineextended;
        
            Write-Host "Adding a key to Service Principal..."
        
            $p = Get-MsolServicePrincipal -ServicePrincipalName $ServiceName
            New-MsolServicePrincipalCredential -AppPrincipalId $p.AppPrincipalId -Type asymmetric -Usage Verify -Value $credValue -StartDate $cer.GetEffectiveDateString() -EndDate $cer.GetExpirationDateString()
        }
        Else
        {
            Write-Error "Cannot find certificate."
        } 
    
    Le résultat attendu doit être comme suit.
    
        Please enter the administrator user name and password of the Office 365 tenant domain...
        Adding a key to Service Principal...
        Complete.

## Activer l’envoi par proxy de notifications Push

Une fois l’authentification OAuth correctement configurée grâce aux étapes précédentes, un administrateur sur site doit activer l’envoi par proxy de notifications Push à l’aide du script suivant. Assurez-vous que vous mettez à jour la valeur de *$tenantDomain* pour qu’elle corresponde au nom de votre domaine. Pour ce faire, copiez et collez le code suivant.

    $tenantDomain = "Fabrikam.com"
    Enable-PushNotificationProxy -Organization:$tenantDomain

Le résultat attendu doit être semblable à la sortie suivante.

    RunspaceId        : 4f2eb5cc-b696-482f-92bb-5b254cd19d60
    DisplayName       : On Premises Proxy app
    Enabled           : True
    Organization      : fabrikam.com
    Uri               : https://outlook.office365.com/PushNotifications
    Identity          : OnPrem-Proxy
    IsValid           : True
    ExchangeVersion   : 0.20 (15.0.0.0)
    Name              : OnPrem-Proxy
    DistinguishedName : CN=OnPrem-Proxy,CN=Push Notifications Settings,CN=First Organization,CN=Microsoft
                        Exchange,CN=Services,CN=Configuration,DC=Domain,DC=extest,DC=microsoft,DC=com
    Guid              : 8b567958-58a4-403c-a8f0-524d7f1e9279
    ObjectCategory    : fabrikam.com/Configuration/Schema/ms-Exch-Push-Notifications-App
    ObjectClass       : {top, msExchPushNotificationsApp}
    WhenChanged       : 8/27/2013 7:23:47 PM
    WhenCreated       : 8/14/2013 1:30:27 PM
    WhenChangedUTC    : 8/28/2013 2:23:47 AM
    WhenCreatedUTC    : 8/14/2013 8:30:27 PM
    OrganizationId    :
    OriginatingServer : server.fabrikam.com
    ObjectState       : Unchanged

## Vérifier le fonctionnement des notifications Push

Une fois les étapes précédentes effectuées, les notifications Push peuvent être testées par l’une des opérations suivantes :

  - **Envoi d’un message électronique de test à la boîte aux lettres de l’utilisateur :** 
    
    1.  Configurez un compte sur un périphérique mobile dans OWA pour les périphériques afin de vous abonner aux notifications.
    
    2.  Revenez à l’écran d’accueil du périphérique, qui place OWA pour les périphériques en arrière-plan.
    
    3.  Envoyez un message électronique à partir d’un autre périphérique, comme un PC, à la boîte de réception du compte configuré sur le périphérique mobile.
    
    4.  Après quelques minutes, l’icône de l’application doit indiquer le nombre de message non vus.

  - **Activation du contrôle.** Une autre méthode de test des notifications Push ou de recherche de la raison de l’échec des notifications consiste à activer le contrôle sur un serveur de boîtes aux lettres de votre organisation. Un administrateur du serveur Exchange 2013 sur site doit appeler le contrôle par proxy des notifications Push à l’aide du script suivant. Pour ce faire, copiez et collez le code suivant.
    
        # Send a push notification to verify connectivity.
        
        $s = Get-ExchangeServer | ?{$_.ServerRole -match "Mailbox"}
        If ($s.Count -gt 1)
        {
            $s = $s[0]
        }
        If ($s.Count -ne 0)
        {
            # Restart the monitoring service to clear the cache from when push was previously disabled.
            Restart-Service MSExchangeHM
        
            # Give the monitoring service enough time to load.
            Start-Sleep -Seconds:120
        
            Invoke-MonitoringProbe PushNotifications.Proxy\PushNotificationsEnterpriseConnectivityProbe -Server:$s.Fqdn | fl ResultType, Error, Exception
        }
        Else
        {
            Write-Error "Cannot find a Mailbox server in the current site."
        }
    
    Le résultat attendu doit être semblable à la sortie suivante.
    
        ResultType : Succeeded
        Error      :
        Exception  :

