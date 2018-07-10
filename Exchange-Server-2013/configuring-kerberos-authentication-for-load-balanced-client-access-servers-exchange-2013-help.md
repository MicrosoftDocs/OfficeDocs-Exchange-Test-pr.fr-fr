---
title: 'Configuration de l’authentification Kerberos pour les serveurs d’accès au client avec équilibrage de charge: Exchange 2013 Help'
TOCTitle: Configuration de l’authentification Kerberos pour les serveurs d’accès au client avec équilibrage de charge
ms:assetid: 8f4faeea-a825-438d-97dc-1c398ce7aba5
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Ff808312(v=EXCHG.150)
ms:contentKeyID: 62835952
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configuration de l’authentification Kerberos pour les serveurs d’accès au client avec équilibrage de charge

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2016-12-09_

**Résumé :**  Décrit comment utiliser l’authentification Kerberos à l’aide de serveurs d’accès au client avec équilibrage de charge dans Exchange 2013.

Afin d’utiliser l’authentification Kerberos avec des serveurs d’accès au client avec équilibrage de charge, vous devez suivre les étapes de configuration décrites dans cet article.

## Création du compte de service secondaire dans les services de domaine Active Directory

Tous les serveurs d'accès au client qui partagent les mêmes espaces de noms et URL doivent utiliser les mêmes informations d'identification de compte de service de substitution. En règle générale, il vous suffit de disposer d'un compte unique pour une forêt pour chaque version d'Exchange. *informations d'identification du compte de service de substitution* ou *informations d'identification ASA*.

> [!NOTE]
> Exchange 2010 et Exchange 2013 ne peuvent pas partager les mêmes informations d'identification ASA. Vous devez créer des informations d'identification ASA pour Exchange 2013.


> [!NOTE]
> Bien que les enregistrements CNAME soient pris en charge pour les espaces de noms partagés, Microsoft recommande d’utiliser des enregistrements A. Cela permet de s’assurer que le client émet correctement une demande de ticket Kerberos fondée sur le nom partagé et non sur le serveur FQDN.


Lorsque vous configurez le compte ASA, gardez ces recommandations à l’esprit :

  - **Type de compte.** Nous vous recommandons de créer un compte d’ordinateur plutôt qu’un compte d’utilisateur. Un compte d’ordinateur ne permet pas de connexion interactive et peut avoir des stratégies de sécurité plus simples que celles d’un compte d’utilisateur. Si vous créez un compte d’ordinateur, le mot de passe n’expire pas, mais nous vous recommandons de le mettre à jour régulièrement dans tous les cas. Vous pouvez utiliser la stratégie de groupe locale pour spécifier la durée de vie maximale du compte d’ordinateur et des scripts et ainsi supprimer régulièrement les comptes d’ordinateurs qui ne répondent pas aux exigences des stratégies actuelles. Votre stratégie de sécurité locale détermine également à quel moment vous devez modifier le mot de passe. Bien que nous vous recommandions d’utiliser un compte d’ordinateur, vous pouvez créer un compte d’utilisateur.

  - **Nom du compte.** Aucune exigence ne s’applique au nom du compte. Vous pouvez utiliser n’importe quel nom conforme à votre schéma d’affectation de noms.

  - **Groupe de comptes.** Le compte que vous utilisez pour les informations d'identification ASA n’ont pas besoin de privilège de sécurité particulier. Si vous utilisez un compte d’ordinateur, le compte doit simplement être membre du groupe de sécurité Ordinateurs du domaine. Si vous utilisez un compte d’utilisateur, il est simplement nécessaire que le compte soit un membre du groupe de sécurité Utilisateurs du domaine.

  - **Mot de passe du compte.** Le mot de passe que vous fournissez lorsque vous créez le compte sera utilisé. Ainsi, lorsque vous créez le compte, vous devez utiliser un mot de passe complexe et veiller à ce qu’il soit conforme aux exigences de mot de passe de votre organisation.

**Pour créer le compte ASA en tant que compte d’ordinateur, procédez comme suit :** 

1.  Sur un ordinateur avec jonction à un domaine, exécutez Windows PowerShell ou l’environnement de ligne de commande Exchange Management Shell.
    
    Utilisez la cmdlet **Import-Module** pour importer le module Active Directory.
    
        Import-Module ActiveDirectory

2.  Utilisez la cmdlet **New-ADComputer** pour créer un compte d’ordinateur Active Directory en suivant la syntaxe de cette cmdlet :
    
        New-ADComputer [-Name] <string> [-AccountPassword <SecureString>] [-AllowReversiblePasswordEncryption <System.Nullable[boolean]>] [-Description <string>] [-Enabled <System.Nullable[bool]>]
    
    **Exemple :** 
    
        New-ADComputer -Name EXCH2013ASA -AccountPassword (Read-Host 'Enter password' -AsSecureString) -Description 'Alternate Service Account credentials for Exchange' -Enabled:$True -SamAccountName EXCH2013ASA
    
    Lorsque *EXCH2013ASA* est le nom du compte, la description *Alternate Service Account credentials for Exchange* peut être ce que vous voulez et la valeur du paramètre *SamAccountName*, dans ce cas *EXCH2013ASA*, doit être unique dans votre répertoire.

3.  Utilisez la cmdlet **Set-ADComputer** pour activer le support de chiffrement AES 256 utilisé par Kerberos à l’aide de la syntaxe de cette cmdlet :
    
        Set-ADComputer [-Name] <string> [-add @{<attributename>="<value>"]
    
    **Exemple :** 
    
        Set-ADComputer EXCH2013ASA -add @{"msDS-SupportedEncryptionTypes"="28"}
    
    Où *EXCH2013ASA* est le nom du compte, et où l’attribut à modifier est *msDS-SupportedEncryptionTypes* avec une valeur décimale de 28, qui permet de réaliser les chiffrements suivants : RC4-HMAC, AES128-CTS-HMAC-SHA1-96, AES256-CTS-HMAC-SHA1-96.

Pour en savoir plus sur ces cmdlets, consultez les articles [Import-Module](https://technet.microsoft.com/library/hh849725.aspx) et [New-ADComputer](https://technet.microsoft.com/library/ee617245.aspx).

## Scénarios inter-forêts

Si votre déploiement est un déploiement inter-forêts ou de forêt de ressources et que certains utilisateurs se trouvent en dehors de la forêt Active Directory qui contient Exchange, vous devez configurer des relations d’approbation entre les forêts. Aussi, pour chaque forêt dans le déploiement, vous devez configurer une règle de routage qui permet d’établir une relation d’approbation entre tous les suffixes de noms dans la forêt et entre les forêts. Pour plus d’informations sur la gestion des approbations inter-forêts, consultez l’article [Gestion des approbations de forêt](https://technet.microsoft.com/library/cc772440.aspx).

## Identification des noms de principaux du service à associer au compte ASA

Une fois le compte ASA créé, vous devez associer les noms de principaux du service (SPN) Exchange aux informations d'identification ASA. La liste des SPN Exchange peut différer selon votre configuration, mais elle doit au moins comprendre les éléments suivants :

  - **http/**   Utilisez ce SPN pour Outlook Anywhere, MAPI sur HTTP, les services web Exchange, la découverte automatique et le carnet d’adresses en mode hors connexion.

Les valeurs de SPN doivent correspondre au nom de service sur l’équilibrage de la charge réseau et non sur des serveurs individuels. Pour vous aider à choisir les valeurs SPN appropriées, prenez en compte les scénarios suivants :

  - Site Active Directory unique

  - Sites Active Directory multiples

Chacun de ces scénarios part du principe que les noms de domaine complets (FQDN) avec équilibrage de charge ont été déployés pour les URL internes, les URL externes et l’URI interne de découverte automatique utilisées par les membres de serveurs d’accès au client. Pour plus d’informations, voir Présentation de la transmission par proxy et de la redirection.

## Site Active Directory unique

Si vous disposez d’un site Active Directory unique, votre environnement peut ressembler à celui représenté par le schéma ci-dessous :

![Objet CAS Array avec un seul site Active Directory et l’authentification Kerberos](images/Ff808312.97a1a926-f4ac-4498-bc6b-32e7fb1b70f1(EXCHG.150).jpg "Objet CAS Array avec un seul site Active Directory et l’authentification Kerberos")

En fonction des noms de domaine complets utilisés par les clients Outlook internes dans la figure précédente, vous devez associer les SPN suivants au compte ASA :

  - http/mail.corp.tailspintoys.com

  - http/autodiscover.corp.tailspintoys.com

## Sites Active Directory multiples

Si vous disposez de plusieurs sites Active Directory, votre environnement peut ressembler à celui représenté par le schéma ci-dessous :

![Objet CAS Array avec plusieurs sites AD et l’authentification Kerberos](images/Ff808312.95b52bd8-7074-4055-8bd2-e6bf1f112b42(EXCHG.150).jpg "Objet CAS Array avec plusieurs sites AD et l’authentification Kerberos")

En fonction des noms de domaine complets utilisés par les clients Outlook dans le schéma précédent, vous devez associer les SPN suivants au compte ASA utilisé par les serveurs d’accès au client dans ADSite 1 :

  - http/mail.corp.tailspintoys.com

  - http/autodiscover.corp.tailspintoys.com

Vous devez également associer les SPN suivants au compte ASA utilisé par les serveurs d’accès au client dans ADSite 2 :

  - http/mailsdc.corp.tailspintoys.com

  - http/autodiscoversdc.corp.tailspintoys.com

## Configuration et vérification de la configuration du compte ASA sur chaque serveur d’accès au client

Une fois le compte créé, vous devez vérifier qu’il a été répliqué sur tous les contrôleurs de domaine AD DS. Plus précisément, le compte doit être présent sur chaque serveur d’accès au client utilisant les informations d’identification du compte ASA. Ensuite, vous configurez le compte en tant que compte ASA sur chaque serveur d’accès au client dans votre déploiement.

Vous pouvez configurer le compte ASA en utilisant l’environnement de ligne de commande Exchange Management Shell, tel que décrit dans l’une de ces procédures :

  - Déployer les informations d'identification ASA sur le premier serveur d'accès client Exchange 2013

  - Déployer les informations d'identification ASA sur d'autres serveurs d'accès client Exchange 2013

La seule méthode prise en charge pour le déploiement des informations d'identification ASA consiste à utiliser le script RollAlternateServiceAcountPassword.ps1. Pour plus d'informations, voir [Utilisation du script RollAlternateserviceAccountCredential.ps1 dans l’environnement de ligne de commande Exchange Management Shell](using-the-rollalternateserviceaccountcredential-ps1-script-in-the-shell-exchange-2013-help.md). Une fois le script exécuté, il est recommandé de vérifier que tous les serveurs ciblés ont été mis à jour correctement.

## Déployer les informations d'identification ASA sur le premier serveur d'accès client Exchange 2013

1.  Ouvrez l’environnement de ligne de commande Exchange Management Shell sur un serveur Exchange 2013.

2.  Naviguez jusqu'aux répertoires *\<Exchange 2013 installation directory\>*\\V15\\Scripts.

3.  Exécutez la commande suivante pour déployer les informations d'identification ASA sur le premier serveur d'accès client Exchange 2013 :
    
        .\RollAlternateServiceAccountPassword.ps1 -ToSpecificServer cas-1.corp.tailspintoys.com -GenerateNewPasswordFor tailspin\EXCH2013ASA$

4.  Lorsque vous êtes invité à indiquer si vous souhaitez modifier le mot de passe pour le compte de service de substitution, répondez **Oui**.

Voici un exemple de sortie qui est affiché lorsque vous exécutez le script RollAlternateServiceAccountPassword.ps1.

    ========== Starting at 01/12/2015 10:17:47 ==========
    Creating a new session for implicit remoting of "Get-ExchangeServer" command...
    Destination servers that will be updated:
    
    Name                                                        PSComputerName
    ----                                                        --------------
    cas-1                                                   cas-1.corp.tailspintoys.com
    
    
    Credentials that will be pushed to every server in the specified scope (recent first):
    
    UserName                                                                                                        
    Password
    --------                                                                                                        
    --------
    tailspin\EXCH2013ASA$                                                                             
    System.Security.SecureString
    
    
    Prior to pushing new credentials, all existing credentials that are invalid or no longer work will be removed from  the destination servers.
    Pushing credentials to server cas-1
    Setting a new password on Alternate Serice Account in Active Directory
    
    Password change
    Do you want to change password for tailspin\EXCH2013ASA$ in Active Directory at this time?
    [Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"): y
    Preparing to update Active Directory with a new password for tailspin\EXCH2013ASA$ ...
    Resetting a password in the Active Directory for tailspin\EXCH2013ASA$ ...
    New password was successfully set to Active Directory.
    Retrieving the current Alternate Service Account configuration from servers in scope
    Alternate Service Account properties:
    
    StructuralObjectClass QualifiedUserName Last Pwd Update       SPNs
    --------------------- ----------------- ---------------       ----
    computer              tailspin\EXCH2013ASA$   1/12/2015 10:19:53 AM
    
    Per-server Alternate Service Account configuration as of the time of script completion:
    
    
       Array: {mail.corp.tailspintoys.com}
    
    Identity  AlternateServiceAccountConfiguration
    --------  ------------------------------------
    cas-1 Latest: 1/12/2015 10:19:22 AM, tailspin\EXCH2013ASA$
              ...
    
    ========== Finished at 01/12/2015 10:20:00 ==========
    
            THE SCRIPT HAS SUCCEEDED

## Déployer les informations d'identification ASA sur un autre serveur d'accès client Exchange 2013

1.  Ouvrez l’environnement de ligne de commande Exchange Management Shell sur un serveur Exchange 2013.

2.  Naviguez jusqu'aux répertoires *\<Exchange 2013 installation directory\>*\\V15\\Scripts.

3.  Exécutez la commande suivante pour déployer les informations d'identification ASA sur un autre serveur d'accès client Exchange 2013 :
    
        .\RollAlternateServiceAccountPassword.ps1 -ToSpecificServer cas-2.corp.tailspintoys.com -CopyFrom cas-1.corp.tailspintoys.com

4.  Répétez l'étape 3 pour chaque serveur d'accès client sur lequel vous souhaitez déployer les informations d'identification ASA.

Voici un exemple de sortie qui est affiché lorsque vous exécutez le script RollAlternateServiceAccountPassword.ps1.

    ========== Starting at 01/12/2015 10:34:35 ==========
    Destination servers that will be updated:
    
    Name                                                        PSComputerName
    ----                                                        --------------
    cas-2                                                   cas-2.corp.tailspintoys.com
    
    
    Credentials that will be pushed to every server in the specified scope (recent first):
    
    UserName                                                                                                        
    Password
    --------                                                                                                        
    --------
    tailspin\EXCH2013ASA$                                                                             
    System.Security.SecureString
    
    Prior to pushing new credentials, all existing credentials will be removed from the destination servers.
    Pushing credentials to server cas-2
    Retrieving the current Alternate Service Account configuration from servers in scope
    Alternate Service Account properties:
    
    StructuralObjectClass QualifiedUserName Last Pwd Update       SPNs
    --------------------- ----------------- ---------------       ----
    computer              tailspin\EXCH2013ASA$   1/12/2015 10:19:53 AM
    
    Per-server Alternate Service Account configuration as of the time of script completion:
    
    
       Array: cas-2.corp.tailspintoys.com
    
    Identity  AlternateServiceAccountConfiguration
    --------  ------------------------------------
    cas-2 Latest: 1/12/2015 10:37:59 AM, tailspin\EXCH2013ASA$
              ...
    
    
    ========== Finished at 01/12/2015 10:38:13 ==========
    
            THE SCRIPT HAS SUCCEEDED

## Vérifier le déploiement des informations d'identification ASA

  - Ouvrez l’environnement de ligne de commande Exchange Management Shell sur un serveur Exchange 2013.

  - Exécutez la commande suivante pour vérifier les paramètres sur un serveur d'accès client :
    
        Get-ClientAccessServer CAS-3 -IncludeAlternateServiceAccountCredentialStatus | Format-List Name, AlternateServiceAccountConfiguration

  - Répétez l'étape 2 sur chaque serveur d'accès client où vous souhaitez vérifier le déploiement des informations d'identification ASA.

Voici un exemple de la sortie qui est affichée lorsque vous exécutez la commande Get-ClientAccessServer ci-dessus et qu'aucune information d'identification ASA précédente n'a été définie.

    Name                                 : CAS-1
    AlternateServiceAccountConfiguration : Latest: 1/12/2015 10:19:22 AM, tailspin\EXCH2013ASA$
                                           Previous: <Not set>
                                               ...

Voici un exemple de la sortie qui est affichée lorsque vous exécutez la commande Get-ClientAccessServer ci-dessus et que des informations d'identification ASA ont été définies précédemment. Les informations d'identification ASA précédentes et la date et l'heure auxquelles elles ont été définies sont renvoyées.

    Name                                 : CAS-3
    AlternateServiceAccountConfiguration : Latest: 1/12/2015 10:19:22 AM, tailspin\EXCH2013ASA$
                                           Previous: 7/15/2014 12:58:35 PM, tailspin\oldSharedServiceAccountName$
                                               ...

## Association des noms de principaux du service (SPN) au compte ASA

> [!NOTE]
> N’associez pas les SPN avec des informations d’identification ASA jusqu’à ce que vous ayez déployé ces informations d’identification sur au moins un serveur Exchange, comme décrit précédemment dans la section Déployer les informations d'identification ASA sur le premier serveur d'accès client Exchange 2013. Dans le cas contraire, vous rencontrerez des erreurs d’authentification Kerberos.


Avant d’associer les SPN au compte ASA, vous devez vérifier que les SPN cibles ne sont pas déjà associés à un autre compte de la forêt. Les informations d’identification ASA doivent être le seul compte de la forêt auquel ces noms SPN sont associés. Vous pouvez vérifier qu’aucun autre compte de la forêt n’est associé aux noms de principaux du service en exécutant la commande **setspn** à partir de la ligne de commande.

**Pour vérifier qu’un SPN n’est pas déjà associé à un compte dans une forêt en exécutant la commande setspn, procédez comme suit :** 

1.  Appuyez sur **Démarrer**. Dans la zone **Recherche**, saisissez **Invite de commandes**, puis, dans la liste des résultats, sélectionnez **Invite de commandes**.

2.  Depuis l’invite de commandes, entrez la commande suivante :
    
        setspn -F -Q <SPN>
    
    Où \<SPN\> est le SPN que vous souhaitez associer au compte ASA. Par exemple :
    
        setspn -F -Q http/mail.corp.tailspintoys.com
    
    La commande ne doit retourner aucune donnée. Si elle renvoie des données, cela signifie qu’un autre compte est déjà associé au SPN. Répétez une fois cette étape pour chaque SPN que vous souhaitez associer au compte ASA.

**Pour associer un SPN à des informations d'identification ASA à l’aide de la commande setspn, procédez comme suit :** 

1.  Appuyez sur **Démarrer**. Dans la zone **Recherche**, saisissez **Invite de commandes**, puis, dans la liste des résultats, sélectionnez **Invite de commandes**.

2.  Depuis l’invite de commandes, entrez la commande suivante :
    
        setspn -S <SPN> <Account>$
    
    Où \<SPN\> est le SPN que vous souhaitez associer aux informations d’identification du compte ASA et \<Account\> est le compte associé aux informations d’identification du compte ASA. Par exemple :
    
        setspn -S http/mail.corp.tailspintoys.com tailspin\EXCH2013ASA$
    
    Exécutez une fois la commande suivante pour chaque SPN que vous souhaitez associer aux informations d’identification du compte ASA.

**Pour vérifier que vous avez associé les noms SPN aux informations d’identification ASA à l’aide de la commande setspn, procédez comme suit :** 

1.  Appuyez sur **Démarrer**. Dans la zone **Recherche**, saisissez **Invite de commandes**, puis, dans la liste des résultats, sélectionnez **Invite de commandes**.

2.  Depuis l’invite de commandes, entrez la commande suivante :
    
        setspn -L <Account>$
    
    Où \<Account\> est le compte associé au compte ASA. Par exemple :
    
        setspn -L tailspin\EXCH2013ASA$
    
    Vous ne devez exécuter cette commande qu’une seule fois.

## Activer l'authentification Kerberos pour les clients Outlook

1.  Ouvrez l’environnement de ligne de commande Exchange Management Shell sur un serveur Exchange 2013.

2.  Pour activer l'authentification Kerberos pour les clients Outlook Anywhere, exécutez la commande suivante sur votre serveur d'accès client :
    
        Get-OutlookAnywhere -server CAS-1 | Set-OutlookAnywhere -InternalClientAuthenticationMethod  Negotiate

3.  Pour activer l'authentification Kerberos pour le MAPI sur des clients HTTP, exécutez les opérations suivantes sur votre serveur d'accès client Exchange 2013 :
    
        Get-MapiVirtualDirectory -Server CAS-1 | Set-MapiVirtualDirectory -IISAuthenticationMethods Ntlm, Negotiate

4.  Répétez les étapes 2 et 3 pour chaque serveur d'accès client Exchange 2013 sur lequel vous souhaitez activer l'authentification Kerberos.

## Validation de l’authentification Kerberos de client Exchange

Après avoir correctement configuré Kerberos et le compte ASA, vérifiez que les clients peuvent s’authentifier, comme décrit dans ces tâches.

## Vérification de l’exécution du service d’hôte de service Microsoft Exchange

Le service d’hôte de service Microsoft Exchange (MSExchangeServiceHost) sur le serveur d’accès au client est chargé de la gestion des informations d’identification du compte ASA. Si ce service n’est pas en cours d’exécution, l’authentification Kerberos n’est pas possible. Par défaut, le service est configuré pour se lancer automatiquement au démarrage de l’ordinateur.

**Pour vérifier que le service d’hôte de service Microsoft Exchange est démarré, procédez comme suit :** 

1.  Cliquez sur **Démarrer**, entrez **services.msc** puis sélectionnez **services.msc** dans la liste.

2.  Dans la fenêtre **Services**, repérez le service **Hôte de services Microsoft Exchange** dans la liste des services.

3.  L’état du service doit être **En cours d’exécution**. Si l’état n’est pas **En cours d’exécution**, cliquez avec le bouton droit sur le service, puis sur **Démarrer**.

## Validation de Kerberos à partir du serveur d’accès au client

Lorsque vous avez configuré le compte ASA sur chaque serveur d’accès au client, vous avez exécuté la cmdlet **set-ClientAccessServer**. Une fois que vous avez exécuté cette cmdlet, vous pouvez utiliser les journaux pour connaître les connexions Kerberos ayant fonctionné.

**Pour vérifier que Kerberos fonctionne correctement à l’aide du fichier journal HttpProxy, procédez comme suit :** 

1.  Dans un éditeur de texte, accédez au dossier où est stocké le journal HttpProxy. Par défaut, le journal est stocké dans le dossier suivant :
    
    %ExchangeInstallPath%\\Logging\\HttpProxy\\RpcHttp

2.  Ouvrez le fichier journal le plus récent et recherchez le mot **Negotiate**. La ligne du fichier journal ressemble à l’exemple suivant :
    
        2014-02-19T13:30:49.219Z,e19d08f4-e04c-42da-a6be-b7484b396db0,15,0,775,22,,RpcHttp,mail.corp.tailspintoys.com,/rpc/rpcproxy.dll,,Negotiate,True,tailspin\Wendy,tailspintoys.com,MailboxGuid~ad44b1e0-e44f-4a16-9396-3a437f594f88,MSRPC,192.168.1.77,EXCH1,200,200,,RPC_OUT_DATA,Proxy,exch2.tailspintoys.com,15.00.0775.000,IntraForest,MailboxGuidWithDomain,,,,76,462,1,,1,1,,0,,0,,0,0,16272.3359,0,0,3,0,23,0,25,0,16280,1,16274,16230,16233,16234,16282,?ad44b1e0-e44f-4a16-9396-3a437f594f88@tailspintoys.com:6001,,BeginRequest=2014-02-19T13:30:32.946Z;BeginGetRequestStream=2014-02-19T13:30:32.946Z;OnRequestStreamReady=2014-02-19T13:30:32.946Z;BeginGetResponse=2014-02-19T13:30:32.946Z;OnResponseReady=2014-02-19T13:30:32.977Z;EndGetResponse=2014-02-19T13:30:32.977Z;,PossibleException=IOException;
    
    Si vous voyez que la valeur **AuthenticationType** est **Negotiate**, cela signifie que le serveur est en train de créer des connexions Kerberos authentifiées.

## Conservation des informations d’identification du compte ASA

Si vous devez mettre à jour le mot de passe du compte ASA régulièrement, suivez les étapes relatives à la configuration des informations d’identification du compte ASA contenues dans cet article. Envisagez la création d’une tâche planifiée pour effectuer une mise à jour régulière du mot de passe. Veillez à contrôler la tâche planifiée pour vérifier le changement en temps opportun du mot de passe et éviter toute erreur d’authentification.

## Désactivation de l’authentification Kerberos

Pour configurer votre serveur d’accès au client afin qu’il n’utilise pas Kerberos, dissociez ou supprimez les SPN des informations d’identification du compte ASA. Si les SPN sont supprimés, vos clients ne tenteront pas de procéder à une authentification Kerberos et les clients configurés pour utiliser l’authentification Negotiate utiliseront NTLM à la place. Les clients configurés pour utiliser uniquement Kerberos ne parviendront pas à se connecter. Une fois les SPN supprimés, vous devez également supprimer le compte.

**Pour supprimer les informations d'identification ASA**

1.  Ouvrez l'environnement de ligne de commande Exchange Management Shell sur un serveur Exchange 2013 et exécutez la commande suivante :
    
        Set-ClientAccessServer CAS-1 -RemoveAlternateServiceAccountCredentials

2.  Bien que vous n’ayez pas à le faire immédiatement, vous devrez dans tous les cas redémarrer tous les ordinateurs clients pour effacer le cache de ticket Kerberos de l’ordinateur.

