---
title: 'Configuration du déchargement SSL dans Exchange 2013: Exchange 2013 Help'
TOCTitle: Configuration du déchargement SSL dans Exchange 2013
ms:assetid: 654cc2c2-918b-48fc-9532-9c8e3012810d
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dn635115(v=EXCHG.150)
ms:contentKeyID: 61204572
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configuration du déchargement SSL dans Exchange 2013

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2016-08-22_

Les éléments suivants vous aident à configurer le déchargement SSL pour les protocoles et les services connexes sur les serveurs d’accès client Exchange 2013 avec le Service Pack 1 (SP1). Si vous avez plusieurs serveurs d’accès client, vous devez effectuer les étapes requises pour chaque protocole ou service sur tous les serveurs d’accès client avec SP1 de votre organisation locale. Cela ne veut pas dire que chaque serveur d’accès client de votre organisation doit être configuré de manière identique. Si vous mettez à niveau vers des mises à jour cumulatives ou des Service Packs plus récents et que vous souhaitez continuer à utiliser le déchargement SSL, vous devez effectuer les étapes suivantes de nouveau après la mise à niveau ou l’application de ces mises à jour sur les serveurs d’accès client Exchange 2013.

L’un des plus grands avantages au déchargement SSL est la possibilité de gérer plus facilement les certificats utilisés. Au lieu d’avoir des certificats SSL distincts pour chaque serveur d’accès client avec SP1, un certificat SSL unique est utilisé et importé pour tous les serveurs d’accès client. Il peut s’agir d’un certificat SSL existant ou nouvellement créé.

> [!CAUTION]
> Lorsque vous utilisez le Gestionnaire des services IIS (Internet Information Services), Exchange Management Shell ou une interface de ligne de commande pour configurer le déchargement SSL, notez qu’il existe un <strong>site web par défaut</strong> et un site <strong>Exchange Back End</strong>. Pour le déchargement SSL, configurez uniquement le <strong>site web par défaut</strong>. Ne modifiez pas le site <strong>Exchange Back End</strong>.


**Contenu de cette rubrique**

Configuration du déchargement SSL pour Outlook Web App

Configuration du déchargement SSL pour le Centre d’administration Exchange (CEA)

Configuration du déchargement SSL pour Outlook Anywhere

Configuration du déchargement SSL pour le carnet d’adresses en mode hors connexion (OAB)

Configuration du déchargement de SSL pour Exchange ActiveSync (EAS)

Configuration du déchargement de SSL pour les services web Exchange (EWS)

Configuration du déchargement SSL pour le service de découverte automatique

Configuration du déchargement SSL pour le service proxy de réplication de boîtes aux lettres Mailbox Replication Proxy Service (MRSProxy)

Configuration du déchargement SSL pour les clients Outlook (répertoire virtuel MAPI)

Utilisation d’un script pour activer le déchargement SSL pour tous les protocoles et services

Configuration de la coexistence avec Exchange 2007 et Exchange 2010

## Ce qu'il faut savoir avant de commencer

  - Installez tous les serveurs de boîtes aux lettres et d’accès client requis dans votre organisation.

  - Installez le Service Pack 1 (SP1) sur chaque serveur de boîtes aux lettres et d’accès client de votre organisation. Pour télécharger le SP1, consultez la rubrique [Mises à jour pour Exchange 2013](updates-for-exchange-2013-exchange-2013-help.md).

  - Déterminez les autorisations requises pour Exchange 2013 en consultant la rubrique [Autorisations des fonctionnalités](feature-permissions-exchange-2013-help.md).

  - Pour voir les autorisations dont vous avez besoin pour les serveurs d’accès client, consultez la section « Autorisations du serveur d’accès au client » dans [Autorisations des clients et des périphériques mobiles](clients-and-mobile-devices-permissions-exchange-2013-help.md).

  - Pour voir les autorisations dont vous avez besoin pour les serveurs d’accès client, consultez la section « Autorisations Outlook Web App » dans [Autorisations des clients et des périphériques mobiles](clients-and-mobile-devices-permissions-exchange-2013-help.md).

  - Pour effectuer certaines procédures, vous pouvez utiliser uniquement le Shell. Pour en savoir plus sur l’ouverture de l’environnement de ligne de commande Exchange Management Shell dans votre organisation Exchange locale, consultez la rubrique [Ouvrir le Shell](https://technet.microsoft.com/fr-fr/library/dd638134\(v=exchg.150\)).

  - Pour utiliser un certificat existant sur vos serveurs d’accès client et sur l’appareil dont vous mettez fin aux connexions SSL, exportez le certificat avec la clé privée sur un serveur d’accès client et importez-le ou installez-le sur l’appareil. Pour plus d’informations, consultez la rubrique [Export-ExchangeCertificate](https://technet.microsoft.com/fr-fr/library/aa996305\(v=exchg.150\)).

  - Pour utiliser un nouveau certificat, vous devez utiliser le CAE ou le Shell afin de créer, d’importer et d’activer le nouveau certificat. Pour plus d’informations, consultez la rubrique [Interface utilisateur de la gestion de certificats Exchange 2013](exchange-2013-certificate-management-ui-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.


## Configuration du déchargement SSL pour Outlook Web App

Pour activer le déchargement SSL pour Outlook Web App, vous devez supprimer l’exigence SSL dans le répertoire virtuel **owa** du **site web par défaut** :

  - **Étape 1** Vous pouvez utiliser le Gestionnaire des services IIS ou une ligne de commande pour désactiver SSL dans le répertoire virtuel **owa** :
    
      - À l’aide du Gestionnaire des services IIS, développez **Sites** \> **Site Web par défaut**, puis sélectionnez le répertoire virtuel **owa**. Dans le volet Résultats, sous **IIS**, double-cliquez sur **Paramètres SSL**. Dans le volet des résultats **Paramètres SSL**, décochez la case **Requérir SSL**, puis cliquez sur **Appliquer** dans le volet **Actions**.
    
      - Via la ligne de commande, entrez la commande suivante, puis appuyez sur Entrée.
        
        ```powershell
        appcmd set config "Default Web Site/owa" /section:access /sslFlags:None /commit:APPHOST
        ```

  - **Étape 2** Vous devez recycler le pool d’applications correct ou redémarrer Internet Information Services en utilisant l’une des méthodes suivantes :
    
      - À l’aide d’une ligne de commande : cliquez sur **Démarrer** \> **Exécuter**, entrez **cmd**, puis appuyez sur Entrée. Dans la fenêtre d’invite de commandes, entrez la commande suivante et appuyez sur Entrée.
        
        ```powershell
        appcmd Recycle AppPool MSExchangeOWAAppPool
        ```
    
      - À l’aide d’une cmdlet Windows PowerShell, entrez la commande suivante et appuyez sur Entrée.
        
        ```powershell
        IIS:\>Restart-WebAppPool MSExchangeOWAAppPool
        ```
    
      - À l’aide d’une ligne de commande : cliquez sur **Démarrer** \> **Exécuter**, entrez **cmd**, puis appuyez sur Entrée. Dans la fenêtre d’invite de commandes, entrez la commande suivante et appuyez sur Entrée.
        
        ```powershell
        iisreset /noforce
        ```
    
      - À l’aide du Gestionnaire des services IIS : dans le Gestionnaires des services IIS, dans le volet **Actions**, cliquez sur **Redémarrer**.

Revenir en haut

## Configuration du déchargement SSL pour le Centre d’administration Exchange (CEA)

Pour activer le déchargement SSL pour le CEA, vous devez supprimer l’exigence SSL dans le répertoire virtuel **ecp** du **site web par défaut** :

  - **Étape 1** Vous pouvez utiliser le Gestionnaire des services IIS ou une ligne de commande pour désactiver SSL dans le répertoire virtuel **ecp** :
    
      - À l’aide du Gestionnaire des services IIS, développez **Sites** \> **Site Web par défaut**, puis sélectionnez le répertoire virtuel **ecp**. Dans le volet Résultats, sous **IIS**, double-cliquez sur **Paramètres SSL**. Dans le volet des résultats **Paramètres SSL**, décochez la case **Requérir SSL**, puis cliquez sur **Appliquer** dans le volet **Actions**.
    
      - Via la ligne de commande, entrez la commande suivante, puis appuyez sur Entrée.
        
        ```powershell
        appcmd set config "Default Web Site/ecp" /section:access /sslFlags:None /commit:APPHOST
        ```


  - **Étape 2** Vous devez recycler le pool d’applications correct ou redémarrer Internet Information Services en utilisant l’une des méthodes suivantes :
    
      - À l’aide d’une ligne de commande : cliquez sur **Démarrer** \> **Exécuter**, entrez **cmd**, puis appuyez sur Entrée. Dans la fenêtre d’invite de commandes, entrez la commande suivante et appuyez sur Entrée.
        
        ```powershell
        appcmd Recycle AppPool MSExchangeECPAppPool
        ```
    
      - À l’aide d’une cmdlet Windows PowerShell, entrez la commande suivante et appuyez sur Entrée.
        
        ```powershell
        IIS:\>Restart-WebAppPool MSExchangeECPAppPool
        ```
    
      - À l’aide d’une ligne de commande : cliquez sur **Démarrer** \> **Exécuter**, entrez **cmd**, puis appuyez sur Entrée. Dans la fenêtre d’invite de commandes, entrez la commande suivante et appuyez sur Entrée.
        
        ```powershell
        iisreset /noforce
        ```
    
      - À l’aide du Gestionnaire des services IIS : dans le Gestionnaires des services IIS, dans le volet **Actions**, cliquez sur **Redémarrer**.

Revenir en haut

## Configuration du déchargement SSL pour Outlook Anywhere

Le déchargement SSL pour Outlook Anywhere est activé par défaut. Les clients Outlook Anywhere peuvent recevoir des e-mails provenant d’un réseau privé ou public. Par défaut, le nom d’hôte interne ou le nom de domaine complet du serveur est utilisé pour permettre aux clients Outlook internes de se connecter. Toutefois, si Outlook Anywhere n’est pas utilisé en interne, vous devez supprimer le nom d’hôte interne. Afin d’autoriser un accès interne et externe pour les clients Outlook, vous devez configurer les noms d’hôte interne et externe, définir la méthode d’authentification de chacun, et définir les clients internes et externes afin qu’ils requièrent SSL. Pour configurer la méthode d’authentification pour les clients externes, vous pouvez utiliser le CAE ou Exchange Management Shell. Pour les clients internes, vous devez utiliser le Shell :

  - **Étape 1** Vous pouvez utiliser le CAE ou le Shell si vous n’avez pas ajouté de nom d’hôte externe pour Outlook Anywhere :
    
      - Dans le CAE, accédez à **Serveurs**, sélectionnez le nom du serveur d’accès client dans la liste, puis cliquez sur **Modifier**. Dans la fenêtre **Serveur Exchange**, cliquez sur **Outlook Anywhere**, puis dans la zone **Indiquez le nom d’hôte externe (par exemple, contoso.com) que les utilisateurs utiliseront pour se connecter à votre organisation**, entrez le nom d’hôte externe. Vérifiez que l’option **Autoriser le déchargement SSL** est sélectionnée, puis cliquez sur **Enregistrer**.
    
      - Avec Exchange Management Shell, cliquez sur **Démarrer**, puis, dans le menu **Démarrer**, cliquez sur **Exchange Management Shell**. Dans la fenêtre, entrez la commande suivante et appuyez sur Entrée :
        
        ```powershell
        Set-OutlookAnywhere -Identity ClientAccessServer1\Rpc* -Externalhostname ClientAccessServer1.contoso.com -ExternalClientsRequireSsl:$True -ExternalClientAuthenticationMethod Basic
        ```

  - **Étape 2** Le déchargement SSL est activé par défaut. Cependant, vous pouvez utiliser le CAE ou Exchange Management Shell si le déchargement SSL a été désactivé et que vous voulez l’activer :
    
      - Dans le CAE, accédez à **Serveurs**, sélectionnez le nom du serveur d’accès client dans la liste, puis cliquez sur **Modifier**. Dans la fenêtre **Serveur Exchange**, cliquez sur **Outlook Anywhere**, sur l’option **Autoriser le déchargement SSL**, puis sur **Enregistrer**.
    
      - Dans le Shell, entrez la commande suivante et appuyez sur Entrée :
        
        ```powershell
        Set-OutlookAnywhere -Identity ClientAccessServer1\Rpc* -SSLOffloading $true
        ```

  - **Étape 3** Par défaut, l’option **Requérir SSL** n’est pas sélectionnée dans le répertoire virtuel **Rpc**, mais si vous voulez vérifier que SSL est désactivé, vous pouvez utiliser le Gestionnaire des services IIS.
    
      - À l’aide du Gestionnaire des services IIS, développez **Sites** \> **Site Web par défaut**, puis sélectionnez le répertoire virtuel **Rpc**. Dans le volet Résultats, sous **IIS**, double-cliquez sur **Paramètres SSL**. Dans le volet des résultats **Paramètres SSL**, vérifiez que la case **Requérir SSL** est décochée, puis cliquez sur **Appliquer** dans le volet **Actions**.

  - **Étape 4** Vous devez recycler le pool d’applications correct ou redémarrer Internet Information Services en utilisant l’une des méthodes suivantes :
    
      - À l’aide d’une ligne de commande : cliquez sur **Démarrer** \> **Exécuter**, entrez **cmd**, puis appuyez sur Entrée. Dans la fenêtre d’invite de commandes, entrez la commande suivante et appuyez sur Entrée.
        
        ```powershell
        appcmd Recycle AppPool MSExchangeRpcProxyFrontEndAppPool
        ```
    
      - À l’aide d’une cmdlet Windows PowerShell, entrez la commande suivante et appuyez sur Entrée.
        
        ```powershell
        IIS:\>Restart-WebAppPool MSExchangeRpcProxyFrontEndAppPool
        ```
    
      - À l’aide d’une ligne de commande : cliquez sur **Démarrer** \> **Exécuter**, entrez **cmd**, puis appuyez sur Entrée. Dans la fenêtre d’invite de commandes, entrez la commande suivante et appuyez sur Entrée.
        
        ```powershell
        iisreset /noforce
        ```
    
      - À l’aide du Gestionnaire des services IIS : dans le Gestionnaires des services IIS, dans le volet **Actions**, cliquez sur **Redémarrer**.

> [!NOTE]
> Vous devez attendre l’application (toutes les 15 minutes) par le processus hôte de service des éventuelles modifications d’Active Directory à IIS, même si vous redémarrez IIS sur un serveur d’accès client.


Revenir en haut

## Configuration du déchargement SSL pour le carnet d’adresses en mode hors connexion (OAB)

Pour activer le déchargement SSL pour le carnet d’adresses en mode hors connexion (OAB), vous devez supprimer l’exigence SSL dans le répertoire virtuel **OAB** du **site web par défaut** :

  - **Étape 1** Vous pouvez utiliser le Gestionnaire des services IIS ou une ligne de commande pour désactiver SSL dans le répertoire virtuel **OAB** :
    
      - À l’aide du Gestionnaire des services IIS, développez **Sites** \> **Site Web par défaut**, puis sélectionnez le répertoire virtuel **OAB**. Dans le volet Résultats, sous **IIS**, double-cliquez sur **Paramètres SSL**. Dans le volet des résultats **Paramètres SSL**, décochez la case **Requérir SSL**, puis cliquez sur **Appliquer** dans le volet **Actions**.
    
      - Via la ligne de commande, entrez la commande suivante, puis appuyez sur Entrée.
        
        ```powershell
        appcmd set config "Default Web Site/OAB" /section:access /sslFlags:None /commit:APPHOST
        ```

  - **Étape 2** Vous devez recycler le pool d’applications correct ou redémarrer Internet Information Services en utilisant l’une des méthodes suivantes :
    
      - À l’aide d’une ligne de commande : cliquez sur **Démarrer** \> **Exécuter**, entrez **cmd**, puis appuyez sur Entrée. Dans la fenêtre d’invite de commandes, entrez la commande suivante et appuyez sur Entrée.
        
        ```powershell
        appcmd Recycle AppPool MSExchangeOABAppPool
        ```
    
      - À l’aide d’une cmdlet Windows PowerShell, entrez la commande suivante et appuyez sur Entrée.
        
        ```powershell
        IIS:\>Restart-WebAppPool MSExchangeOABAppPool
        ```
    
      - À l’aide d’une ligne de commande : cliquez sur **Démarrer** \> **Exécuter**, entrez **cmd**, puis appuyez sur Entrée. Dans la fenêtre d’invite de commandes, entrez la commande suivante et appuyez sur Entrée.
        
        ```powershell
        iisreset /noforce
        ```
    
      - À l’aide du Gestionnaire des services IIS : dans le Gestionnaires des services IIS, dans le volet **Actions**, cliquez sur **Redémarrer**.

Revenir en haut

## Configuration du déchargement de SSL pour Exchange ActiveSync (EAS)

Pour activer le déchargement SSL pour Exchange ActiveSync (EAS), vous devez supprimer l’exigence SSL dans le répertoire virtuel **Microsoft-Server-ActiveSync** du **site web par défaut** :

  - **Étape 1** Vous pouvez utiliser le Gestionnaire des services IIS ou une ligne de commande pour désactiver SSL dans le répertoire virtuel **Microsoft-Server-ActiveSync** :
    
      - À l’aide du Gestionnaire des services IIS, développez **Sites** \> **Site Web par défaut**, puis sélectionnez le répertoire virtuel **Microsoft-Server-ActiveSync**. Dans le volet Résultats, sous **IIS**, double-cliquez sur **Paramètres SSL**. Dans le volet des résultats **Paramètres SSL**, décochez la case **Requérir SSL**, puis cliquez sur **Appliquer** dans le volet **Actions**.
    
      - Via la ligne de commande, entrez la commande suivante, puis appuyez sur Entrée.
        
        ```powershell
        appcmd set config "Default Web Site/MSExchangeSyncAppPool" /section:access /sslFlags:None /commit:APPHOST
        ```

  - **Étape 2** Vous devez recycler le pool d’applications correct ou redémarrer Internet Information Services en utilisant l’une des méthodes suivantes :
    
      - À l’aide d’une ligne de commande : cliquez sur **Démarrer** \> **Exécuter**, entrez **cmd**, puis appuyez sur Entrée. Dans la fenêtre d’invite de commandes, entrez la commande suivante et appuyez sur Entrée.
        
        ```powershell
        appcmd Recycle AppPool MSExchangeSyncAppPool
        ```
    
      - À l’aide d’une cmdlet Windows PowerShell, entrez la commande suivante et appuyez sur Entrée.
        
        ```powershell
        IIS:\>Restart-WebAppPool MSExchangeSyncAppPool
        ```
    
      - À l’aide d’une ligne de commande : cliquez sur **Démarrer** \> **Exécuter**, entrez **cmd**, puis appuyez sur Entrée. Dans la fenêtre d’invite de commandes, entrez la commande suivante et appuyez sur Entrée.
        
        ```powershell
        iisreset /noforce
        ```
    
      - À l’aide du Gestionnaire des services IIS : dans le Gestionnaires des services IIS, dans le volet **Actions**, cliquez sur **Redémarrer**.

Revenir en haut

## Configuration du déchargement de SSL pour les services web Exchange (EWS)

Pour activer le déchargement SSL pour les services web Exchange (EWS), vous devez supprimer l’exigence SSL dans le répertoire virtuel **EWS** du **site web par défaut** :

  - **Étape 1** Vous pouvez utiliser le Gestionnaire des services IIS ou une ligne de commande pour désactiver SSL dans le répertoire virtuel **EWS** :
    
      - À l’aide du Gestionnaire des services IIS, développez **Sites** \> **Site Web par défaut**, puis sélectionnez le répertoire virtuel **EWS**. Dans le volet Résultats, sous **IIS**, double-cliquez sur **Paramètres SSL**. Dans le volet des résultats **Paramètres SSL**, décochez la case **Requérir SSL**, puis cliquez sur **Appliquer** dans le volet **Actions**.
    
      - Via la ligne de commande, entrez la commande suivante, puis appuyez sur Entrée.
        
        ```powershell
        appcmd set config "Default Web Site/EWS" /section:access /sslFlags:None /commit:APPHOST
        ```

  - **Étape 2** Vous devez recycler le pool d’applications correct ou redémarrer Internet Information Services en utilisant l’une des méthodes suivantes :
    
      - À l’aide d’une ligne de commande : cliquez sur **Démarrer** \> **Exécuter**, entrez **cmd**, puis appuyez sur Entrée. Dans la fenêtre d’invite de commandes, entrez la commande suivante et appuyez sur Entrée.
        
        ```powershell
        appcmd Recycle AppPool MSExchangeServicesAppPool
        ```
    
      - À l’aide d’une cmdlet Windows PowerShell, entrez la commande suivante et appuyez sur Entrée.
        
        ```powershell
        IIS:\>Restart-WebAppPool MSExchangeServicesAppPool
        ```
    
      - À l’aide d’une ligne de commande : cliquez sur **Démarrer** \> **Exécuter**, entrez **cmd**, puis appuyez sur Entrée. Dans la fenêtre d’invite de commandes, entrez la commande suivante et appuyez sur Entrée.
        
        ```powershell
        iisreset /noforce
        ```
    
      - À l’aide du Gestionnaire des services IIS : dans le Gestionnaires des services IIS, dans le volet **Actions**, cliquez sur **Redémarrer**.

Revenir en haut

## Configuration du déchargement SSL pour le service de découverte automatique

Pour activer le déchargement SSL pour le service de découverte automatique, vous devez supprimer l’exigence SSL dans le répertoire virtuel **Autodiscover** du **site web par défaut** :

  - **Étape 1** Vous pouvez utiliser le Gestionnaire des services IIS ou une ligne de commande pour désactiver SSL dans le répertoire virtuel **Autodiscover** :
    
      - À l’aide du Gestionnaire des services IIS, développez **Sites** \> **Site Web par défaut**, puis sélectionnez le répertoire virtuel **Autodiscover**. Dans le volet Résultats, sous **IIS**, double-cliquez sur **Paramètres SSL**. Dans le volet des résultats **Paramètres SSL**, décochez la case **Requérir SSL**, puis cliquez sur **Appliquer** dans le volet **Actions**.
    
      - Via la ligne de commande, entrez la commande suivante, puis appuyez sur Entrée.
        
        ```powershell
        appcmd set config "Default Web Site/autodiscover" /section:access /sslFlags:None /commit:APPHOST
        ```

  - **Étape 2** Vous devez recycler le pool d’applications correct ou redémarrer Internet Information Services en utilisant l’une des méthodes suivantes :
    
      - À l’aide d’une ligne de commande : cliquez sur **Démarrer** \> **Exécuter**, entrez **cmd**, puis appuyez sur Entrée. Dans la fenêtre d’invite de commandes, entrez la commande suivante et appuyez sur Entrée.
        
        ```powershell
        appcmd Recycle AppPool MSExchangeAutodiscoverAppPool
        ```
    
      - À l’aide d’une cmdlet Windows PowerShell, entrez la commande suivante et appuyez sur Entrée.
        
        ```powershell
        IIS:\>Restart-WebAppPool MSExchangeAutodiscoverAppPool
        ```
    
      - À l’aide d’une ligne de commande : cliquez sur **Démarrer** \> **Exécuter**, entrez **cmd**, puis appuyez sur Entrée. Dans la fenêtre d’invite de commandes, entrez la commande suivante et appuyez sur Entrée.
        
        ```powershell
        iisreset /noforce
        ```
    
      - À l’aide du Gestionnaire des services IIS : dans le Gestionnaires des services IIS, dans le volet **Actions**, cliquez sur **Redémarrer**.

Revenir en haut

## Configuration du déchargement SSL pour le service proxy de réplication de boîtes aux lettres Mailbox Replication Proxy Service (MRSProxy)

Le service MRSProxy (Mailbox Replication Proxy) est installé sur chaque serveur d’accès client Exchange 2013. MRSProxy vous aide à faire des demandes de déplacement inter-forêts sur site, ainsi qu’à déplacer des boîtes aux lettres locales vers Office 365. Cependant, par défaut, MRSProxy est désactivé. Si vous l’activez, vous devez l’activer dans la forêt Exchange distante pour les déplacements de boîtes aux lettres locales inter-forêts ou dans la forêt Exchange locale pour déplacer une boîte aux lettres vers Office 365. Bien que le service MRSProxy fonctionne sous EWS (services web Exchange), il n’est pas pris en charge pour la configuration du déchargement SSL.

La raison en est que le service MRSProxy exige que le trafic soit signé/chiffré. Un programme d’équilibrage de la charge matérielle ou un pare-feu doit rechiffrer le trafic MRSProxy avant de l’envoyer à des serveurs d’accès client. Il est alors recommandé de configurer le pontage SSL pour que le déchargement fonctionne.

**SSL inverse ou pontage SSL**   Si vous activez le SSL inverse ou le pontage SSL sur les programmes d’équilibrage de la charge matérielle, vous n’avez pas besoin d’effectuer les étapes précédentes sur chaque serveur CAS. Cependant, l’activation du SSL inverse sur les programmes d’équilibrage de la charge matérielle signifie que le chiffrement et le déchiffrement SSL restent sur les serveurs d’accès client. Dans ce cas, le chiffrement et le déchiffrement SSL se produisent à la fois sur les programmes d’équilibrage de la charge matérielle et sur les serveurs d’accès client. Choisir d’utiliser le SSL inverse (pontage SSL) ou le déchargement SSL Exchange 2013 dépend des objectifs de l’organisation et des principes de sécurité à mettre en œuvre. L’illustration suivante montre la connectivité client avec pontage SSL (SSL inverse) activé.

![Pontage SSL](images/Dn635115.a08aacc1-0ab4-46b3-bdae-b9518a3f5748(EXCHG.150).jpg "Pontage SSL")

## Configuration du déchargement SSL pour les clients Outlook (répertoire virtuel MAPI)

Pour activer le déchargement SSL pour les clients Outlook, vous devez supprimer l’exigence SSL dans le répertoire virtuel **MAPI** du **site web par défaut** :

  - **Étape 1** Vous pouvez utiliser le Gestionnaire des services IIS ou une ligne de commande pour désactiver SSL dans le répertoire virtuel **MAPI** :
    
      - À l’aide du Gestionnaire des services IIS, développez **Sites** \> **Site Web par défaut**, puis sélectionnez le répertoire virtuel **MAPI**. Dans le volet Résultats, sous **IIS**, double-cliquez sur **Paramètres SSL**. Dans le volet des résultats **Paramètres SSL**, décochez la case **Requérir SSL**, puis cliquez sur **Appliquer** dans le volet **Actions**.
    
      - Via la ligne de commande, entrez la commande suivante, puis appuyez sur Entrée.
        
        ```powershell
        appcmd set config "Default Web Site/MAPI" /section:access /sslFlags:None /commit:APPHOST
        ```

  - **Étape 2** Vous devez recycler le pool d’applications correct ou redémarrer Internet Information Services en utilisant l’une des méthodes suivantes :
    
      - À l’aide d’une ligne de commande : cliquez sur **Démarrer** \> **Exécuter**, entrez **cmd**, puis appuyez sur Entrée. Dans la fenêtre d’invite de commandes, entrez la commande suivante et appuyez sur Entrée.
        
        ```powershell
        appcmd Recycle AppPool MSExchangeMapiFrontEndAppPool
        ```
    
      - À l’aide d’une cmdlet Windows PowerShell, entrez la commande suivante et appuyez sur Entrée.
        
        ```powershell
        IIS:\>Restart-WebAppPool MSExchangeMapiFrontEndAppPool
        ```
    
      - À l’aide d’une ligne de commande : cliquez sur **Démarrer** \> **Exécuter**, entrez **cmd**, puis appuyez sur Entrée. Dans la fenêtre d’invite de commandes, entrez la commande suivante et appuyez sur Entrée.
        
        ```powershell
        iisreset /noforce
        ```
    
      - À l’aide du Gestionnaire des services IIS : dans le Gestionnaires des services IIS, dans le volet **Actions**, cliquez sur **Redémarrer**.

Revenir en haut

## Utilisation d’un script pour activer le déchargement SSL pour tous les protocoles et services

Si vous travaillez dans une grande organisation avec plusieurs serveurs d’accès client Exchange 2013, vous souhaitez peut-être accélérer les étapes que vous venez d’effectuer. Vous pouvez copier et coller les commandes de n’importe lequel des scripts suivants dans le Bloc-notes, effectuer les modifications requises, enregistrer le fichier avec une extension .ps1, puis l’exécuter à partir d’Exchange Management Shell. Selon vos besoins, ces deux scripts peuvent être utilisés afin de configurer le déchargement SSL pour tous les protocoles et services d’un seul ou de plusieurs serveurs d’accès client.

> [!NOTE]
> Pour les entrées de la cmdlet <strong>Set-OutlookAnywhere</strong>, remplacez « MyServer » par le nom du ou des serveur(s) d’accès au client.


**Utilisation de Set-WebConfigurationProperty**

```powershell
Set-OutlookAnywhere -Identity MyServer\Rpc* -Externalhostname MyServer.mail.contoso.com -ExternalClientsRequireSsl $True -ExternalClientAuthenticationMethod Basic
Set-OutlookAnywhere -Identity MyServer\Rpc* -SSLOffloading $true
Set-WebConfigurationProperty -Filter //security/access -name sslflags -Value "None" -PSPath IIS:  -Location "Default Web Site/OWA"
Set-WebConfigurationProperty -Filter //security/access -name sslflags -Value "None" -PSPath IIS: -Location "Default Web Site/ecp"
Set-WebConfigurationProperty -Filter //security/access -name sslflags -Value "None" -PSPath IIS: -Location "Default Web Site/EWS"
Set-WebConfigurationProperty -Filter //security/access -name sslflags -Value "None" -PSPath IIS: -Location "Default Web Site/Autodiscover"
Set-WebConfigurationProperty -Filter //security/access -name sslflags -Value "None" -PSPath IIS: -Location "Default Web Site/Microsoft-Server-ActiveSync"
Set-WebConfigurationProperty -Filter //security/access -name sslflags -Value "None" -PSPath IIS: -Location "Default Web Site/OAB"
Set-WebConfigurationProperty -Filter //security/access -name sslflags -Value "None" -PSPath IIS: -Location "Default Web Site/MAPI"
iisreset /noforce
```

**Utilisation d’appcmd**

> [!NOTE]
> Pour les entrées de la cmdlet <strong>Set-OutlookAnywhere</strong>, remplacez « MyServer » par le nom du ou des serveur(s) d’accès au client.


```powershell
Set-OutlookAnywhere -Identity MyServer\Rpc* -Externalhostname MyServer.mail.contoso.com -ExternalClientsRequireSsl $True -ExternalClientAuthenticationMethod Basic
Set-OutlookAnywhere -Identity MyServer\Rpc* -SSLOffloading $true
&$env:systemroot\system32\inetsrv\appcmd set config "Default Web Site/owa" /section:access /sslFlags:None /commit:APPHOST
&$env:systemroot\system32\inetsrv\appcmd set config "Default Web Site/ecp" /section:access /sslFlags:None /commit:APPHOST
&$env:systemroot\system32\inetsrv\appcmd set config "Default Web Site/EWS" /section:access /sslFlags:None /commit:APPHOST
&$env:systemroot\system32\inetsrv\appcmd set config "Default Web Site/Autodiscover" /section:access /sslFlags:None /commit:APPHOST
&$env:systemroot\system32\inetsrv\appcmd set config "Default Web Site/Microsoft-Server-ActiveSync" /section:access /sslFlags:None /commit:APPHOST
&$env:systemroot\system32\inetsrv\appcmd set config "Default Web Site/OAB" /section:access /sslFlags:None /commit:APPHOST
&$env:systemroot\system32\inetsrv\appcmd set config "Default Web Site/MAPI" /section:access /sslFlags:None /commit:APPHOST
iisreset /noforce
```

Revenir en haut

## Configuration de la coexistence avec Exchange 2007 et Exchange 2010

Dans le cas d’un scénario de coexistence où vous avez un mélange de serveurs Exchange 2003 et Exchange 2010 dans l’organisation, l’une des premières étapes que vous devez effectuer après le déploiement des serveurs d’accès client Exchange 2010 est de modifier le DNS de sorte que les utilisateurs Exchange 2003 accèdent à leurs boîtes aux lettres à partir d’un groupe de serveurs d’accès client Exchange 2010. Dans un tel scénario, l’activation du déchargement SSL sur le programme d’équilibrage de charge utilisé pour distribuer le trafic client parmi les serveurs d’accès client est entièrement prise en charge.

**Coexistence avec d’autres versions d’Outlook Web App**

Lorsque le déchargement SSL est configuré sur les serveurs d’accès client Exchange 2013, la coexistence fonctionne avec Exchange 2007 et Exchange 2010 :

  - En vue de la coexistence avec Exchange 2007, un espace de noms antérieur est requis. La redirection vers cet espace de noms n’a lieu que pour Outlook Web App et les services web Exchange. La découverte automatique, Outlook Anywhere et Exchange ActiveSync utilisent un proxy vers les versions antérieures.

  - En vue de la coexistence avec Exchange 2010, si l’URL externe est définie, une redirection est effectuée. Si ce n’est pas le cas, un proxy est utilisé.

Revenir en haut

