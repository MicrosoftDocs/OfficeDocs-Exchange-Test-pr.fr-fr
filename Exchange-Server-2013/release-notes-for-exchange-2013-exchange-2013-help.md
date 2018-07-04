---
title: 'Notes de publication relatives à Exchange 2013: Exchange 2013 Help'
TOCTitle: Notes de publication relatives à Exchange 2013
ms:assetid: 1879fd5e-3d63-4264-9cc2-9c050c6ab3c5
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ150489(v=EXCHG.150)
ms:contentKeyID: 50477684
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Notes de publication relatives à Exchange 2013

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2018-04-16_

Bienvenue dans Microsoft Exchange Server 2013 \! Cette rubrique contient des informations importantes à connaître afin de déployer Exchange 2013. Veuillez lire entièrement cette rubrique avant de commencer votre déploiement.

Cette rubrique comprend les sections suivantes :

  - Installation et déploiement

  - Environnement de ligne de commande Exchange Management Shell

  - Boîte aux lettres

  - Dossiers publics

  - Flux de messagerie

  - Connectivité client

  - Coexistence avec Exchange 2010

## Installation et déploiement

  - **msExchProductId ne reflète pas la version d’Exchange 2013 installée** Une fois qu’Exchange étend votre schéma Active Directory et prépare Active Directory pour Exchange, plusieurs propriétés sont mises à jour pour indiquer que la préparation est terminée. Une de ces propriétés est *msExchangeProductId* sous le conteneur `CN=<your organization>, CN=Microsoft Exchange, CN=Services, CN=Configuration, DC=<domain>` dans le contexte d’appellation `Configuration`. Si aucune modification du schéma Active Directory n’est introduite dans la version d’Exchange 2013 que vous installez, cette propriété ne sera pas mise à jour ou pourra présenter une valeur inattendue. Cela pourrait porter à confusion si la valeur ne correspond pas à la version d’Exchange 2013 installée.
    
    Ce comportement est attendu car la valeur de *msExchProductId* ne reflète pas la version d’Exchange 2013 en cours d’installation. Cette propriété indique la dernière version d’Exchange 2013 qui a apporté des modifications au schéma Active Directory. Pour éviter toute confusion, il est recommandé de suivre les étapes de la section [How do you know this worked?](prepare-active-directory-and-domains-exchange-2013-help.md) de [Préparation d’Active Directory et des domaines](prepare-active-directory-and-domains-exchange-2013-help.md) pour vérifier que votre environnement Active Directory a été mis à jour et qu’il est prêt pour la version d’Exchange 2013 que vous installez.

  - **Le programme d’installation demande à tort .NET Framework 4.0**   Si vous tentez d’installer Exchange 2013 alors que .NET Framework n’est pas installé sur l’ordinateur, le programme d’installation demande à tort d’installer .NET Framework 4.0 alors qu’en fait, c’est .NET Framework 4.5 ou version ultérieure qui est nécessaire.
    
    Pour contourner ce problème, installez .NET Framework 4.5 ou version ultérieure. Il n’est pas nécessaire d’installer .NET Framework 4.0. Pour obtenir la liste complète des composants requis, consultez la rubrique [Conditions préalables pour Exchange 2013](exchange-2013-prerequisites-exchange-2013-help.md).

  - Les fichiers de configuration d’application XML **Exchange sont remplacés lors de l’installation de la mise à jour cumulative**   Les paramètres par serveur personnalisés de vos fichiers de configuration d’application XML Exchange, par exemple, les fichiers web.config sur les serveurs d’accès au client ou le fichier EdgeTransport.exe.config sur les serveurs de boîtes aux lettres, seront remplacés lors de l’installation d’un Service Pack ou d’une mise à jour cumulative Exchange. Veuillez enregistrer ces informations pour configurer à nouveau votre serveur après l'installation. Vous devez reconfigurer ces paramètres après avoir installé un Service Pack ou une mise à jour cumulative Exchange.

  - **L’installation d’Exchange à l’aide d’autorisations d’administration déléguée entraîne l’échec de la configuration** Lorsqu’un utilisateur membre du groupe de rôles Installation déléguée uniquement tente d’installer Exchange sur un serveur préconfiguré, l’installation échoue. Cela s’explique par le fait que le groupe Installation déléguée ne dispose pas des autorisations requises pour créer et configurer certains objets dans Active Directory.
    
    Pour contourner ce problème, effectuez l’une des opérations suivantes :
    
      - Ajoutez l’utilisateur installant Exchange au groupe de sécurité Administrateurs du domaine Active Directory.
    
      - Installez Exchange en vous servant d’un utilisateur membre du groupe de rôles Gestion de l’organisation.

Pour plus d'informations sur l'installation d'Exchange 2013, consultez la rubrique [Planification et déploiement](planning-and-deployment-for-exchange-2013-installation-instructions.md).

## Environnement de ligne de commande Exchange Management Shell

  - **L’environnement de ligne de commande charge les cmdlets Exchange 2007 ou Exchange 2010 de manière inattendue** Auparavant, l’ouverture de l’environnement de ligne de commande sur un serveur Exchange 2013 entraînait l’ouverture d’une connexion au serveur local ou à un autre serveur exécutant Exchange 2013 par l’environnement de ligne de commande. Lorsque la connexion est établie, les cmdlets Exchange 2013 sont chargées. À partir d’Exchange 2013 CU11, l’environnement de ligne de commande se connecte au serveur Exchange à l’emplacement où se trouve la boîte aux lettres de l’utilisateur connecté. Si l’utilisateur connecté ne possède pas de boîte aux lettres, l’environnement de ligne de commande se connecte au serveur, à l’emplacement de la boîte aux lettres d’arbitrage SystemMailbox{bb558c35-97f1-4cb9-8ff7-d53741dc928c}. Le serveur cible peut être n’importe quelle version d’Exchange prise en charge. Cela signifie que si la boîte aux lettres de l’utilisateur connecté (ou la boîte aux lettres d’arbitrage si l’utilisateur ne possède pas de boîte aux lettres) se trouve sur un serveur Exchange 2010, l’environnement de ligne de commande se connectera à ce serveur et chargera les cmdlets Exchange 2010. Cela peut vous empêcher d’effectuer certaines tâches, car les cmdlets Exchange 2010 ne peuvent pas gérer les serveurs ou la configuration Exchange 2013.
    
    À partir d’Exchange 2013 CU11, il s’agit du comportement par défaut. Pour vous assurer que l’environnement de ligne de commande charge les cmdlets Exchange 2013, déplacez la boîte aux lettres de l’utilisateur connecté vers Exchange 2013. Si l’utilisateur connecté ne possède pas de boîte aux lettres, déplacez la boîte aux lettres d’arbitrage SystemMailbox{bb558c35-97f1-4cb9-8ff7-d53741dc928c} sur un serveur Exchange 2013.
    
    Pour plus de détails et d’informations sur le déplacement de la boîte aux lettres d’arbitrage, consultez l’article relatif à l’[ancrage des boîtes aux lettres et de l’environnement de ligne de commande Exchange Management Shell](https://go.microsoft.com/fwlink/?linkid=717722) sur le blog de l’équipe Exchange.

## Boîte aux lettres

  - **Des serveurs de boîtes aux lettres exécutant différentes versions d’Exchange peuvent être ajoutés au même groupe de disponibilité de base de données** La cmdlet **Add-DatabaseAvailabilityGroupServer** et le Centre d’administration Exchange autorisent à tort qu’un serveur Exchange 2013 soit ajouté à un groupe de disponibilité de base de données (DAG) Exchange 2016, et inversement. Exchange prend en charge uniquement l’ajout de serveurs de boîte aux lettres exécutant la même version (Exchange 2013 et Exchange 2016, par exemple) à un DAG. En outre, le Centre d’administration Exchange affiche les serveurs Exchange 2013 et Exchange 2016 dans la liste des serveurs disponibles pour être ajoutés à un DAG. Cela pourrait permettre à un administrateur d’ajouter par inadvertance un serveur exécutant une version incompatible d’Exchange à un DAG (par exemple, d’ajouter un serveur Exchange 2013 à un DAG Exchange 2016).
    
    Il n’existe actuellement aucune solution pour contourner ce problème. Les administrateurs doivent faire preuve de vigilance lors de l’ajout d’un serveur de boîte aux lettres à un DAG. Ajoutez uniquement des serveurs Exchange 2013 à des DAG Exchange 2013, et uniquement des serveurs Exchange 2016 à des DAG Exchange 2016. Vous pouvez différencier chaque version d’Exchange en consultant la colonne **Version** dans la liste des serveurs du Centre d’administration Exchange. Voici les versions de serveur pour Exchange 2013 et Exchange 2016 :
    
      - **Exchange 2013** 15.0 (Build xxx.xx)
    
      - **Exchange 2016** 15.1 (Build xxx.xx)

  - **La taille de la boîte aux lettres augmente lors d’une migration à partir de versions précédentes d’Exchange**   Lorsque vous déplacez une boîte aux lettres d’une version précédente d’Exchange vers Exchange 2013, la taille signalée de la boîte aux lettres peut augmenter de 30 à 40 %. Ce n'est pas l'espace disque utilisé par la base de données de boîtes aux lettres qui a augmenté, mais l'attribution de l'espace utilisé par chaque boîte aux lettres. L'augmentation de la taille de la boîte aux lettres résulte de l'inclusion de toutes les propriétés des éléments dans le calcul du quota, ce qui produit un calcul plus précis de l'espace utilisé par des éléments dans leur boîte aux lettres. Pour certains utilisateurs, cette augmentation risque de provoquer un dépassement des quotas de taille de leur boîte aux lettres lorsqu'elles sont transférées vers Exchange 2013.
    
    Pour empêcher ce dépassement, augmentez les valeurs de quota des bases de données ou des boîtes aux lettres pour permettre le calcul du nouveau quota. Pour configurer les valeurs de quota des bases de données ou des boîtes aux lettres, utilisez les paramètres *IssueWarningQuota*, *ProhibitSendQuota* et *ProhibitSendReceiveQuota* des cmdlets **Set-MailboxDatabase** et **Set-Mailbox**, respectivement.

  - Il est possible que les clients **Outlook 2007 et Outlook 2010 ne puissent pas télécharger le carnet d’adresses en mode hors connexion**   Si l’URL interne du carnet d’adresses en mode hors connexion n’est pas accessible à partir d’Internet, les clients Outlook 2007 et Outlook 2010 ne pourront peut-être pas télécharger le carnet d’adresses en mode hors connexion.
    
    Pour contourner ce problème pour les clients Outlook 2007 et Outlook 2010, faites en sorte que l’URL interne du carnet d’adresses en mode hors connexion soit accessible à partir d’Internet. Outlook 2013 n’est pas concerné par ce problème.

  - **L’installation d’Exchange 2013 dans une organisation Exchange existante peut provoquer le téléchargement du carnet d’adresses en mode hors connexion par tous les clients**   L’installation du premier serveur Exchange 2013 dans une organisation Exchange 2007 ou Exchange 2010 existante peut provoquer le téléchargement d’une nouvelle copie du carnet d’adresses en mode hors connexion par tous les clients de l’organisation, ce qui peut entraîner une saturation du réseau et réduire les performances des serveurs. Ce problème vient du fait qu'Exchange 2013 crée un carnet d'adresses en mode hors connexion par défaut dans l'organisation, lequel remplace le carnet d'adresses en mode hors connexion d'Exchange 2007 ou d'Exchange 2010. Les boîtes aux lettres pour lesquelles un carnet d’adresses en mode hors connexion spécifique n’a pas été attribué, ou celles se trouvant sur une base de données de boîtes aux lettres pour lesquelles un carnet d’adresses en mode hors connexion spécifique n’a pas été attribué, téléchargent le nouveau carnet d’adresses en mode hors connexion par défaut.
    
    Pour empêcher les clients de télécharger une nouvelle copie du carnet d'adresses en mode hors connexion lors de l'installation d'Exchange 2013, attribuez un carnet d'adresses en mode hors connexion à chaque boîte aux lettres ou à la base de données dans laquelle se trouvent les boîtes aux lettres. Cette opération doit réalisée avant l'installation d'Exchange 2013 dans l'organisation.

  - **Les utilisateurs peuvent être acheminés vers une boîte aux lettres de génération du carnet d’adresses en mode hors connexion (OAB) qui n’est pas responsable du carnet d’adresses en mode hors connexion (OAB) demandé**   La mise à jour cumulative 5 et les mises à jour cumulatives ultérieures d’Exchange 2013 modifient le mode de liaison des carnets d’adresses en mode hors connexion (OAB) aux boîtes aux lettres de génération de ces derniers. Cette modification permet à un utilisateur d’être acheminé vers une boîte aux lettres de génération de carnet d’adresses en mode hors connexion qui n’est pas responsable du carnet d’adresses en mode hors connexion demandé par l’utilisateur. Cette situation peut se produire si toutes les conditions suivantes sont remplies :
    
      - Vous avez plusieurs boîtes aux lettres de génération de carnet d’adresses en mode hors connexion dans votre organisation.
    
      - Vous mettez à niveau les serveurs de boîtes aux lettres qui hébergent les boîtes aux lettres de génération de carnet d’adresses en mode hors connexion avant de mettre à niveau les serveurs d’accès au client.
    
      - Vous mettez à niveau vos serveurs Exchange 2013 à partir d’une version antérieure à la mise à jour cumulative 5 vers une version ultérieure (par exemple, vous effectuez une mise à niveau à partir de la mise à jour cumulative 3 d’Exchange 2013 vers la mise à jour cumulative 6 d’Exchange 2013).
    
      - Vos serveurs d’accès au client exécutent une version antérieure à la mise à jour cumulative 5.
    
    Pour contourner ce problème, veillez à mettre à niveau vos serveurs d’accès au client vers la mise à jour cumulative 6 ou version ultérieure d’Exchange 2013 avant de mettre à niveau vos serveurs de boîtes aux lettres. Cela permettra de s’assurer que les serveurs d’accès au client savent comment rediriger via proxy les demandes vers la boîte aux lettres de génération de carnet d’adresses en mode hors connexion chargée de la génération du carnet d’adresses en mode hors connexion de l’utilisateur.
    
    Pour en savoir plus sur les modifications relatives au carnet d’adresses en mode hors connexion dans la mise à jour cumulative 5 d’Exchange 2013, consultez l’article relatif aux [améliorations du carnet d’adresses en mode hors connexion dans la mise à jour cumulative 5 d’Exchange 2013](https://go.microsoft.com/fwlink/p/?linkid=400642).

## Dossiers publics

  - **Les expéditeurs non autorisés ne peuvent plus envoyer des messages vers des dossiers publics à extension messagerie**   Avant la mise à jour cumulative 6 d’Exchange 2013, les expéditeurs non autorisés pouvaient envoyer des messages vers des dossiers publics à extension messagerie. Les expéditeurs externes avaient ainsi la possibilité d’envoyer des messages vers des dossiers publics à extension messagerie, quelles que soient les autorisations définies pour le dossier public.
    
    À compter de la mise à jour cumulative 6 d’Exchange 2013, si vous souhaitez que les expéditeurs externes puissent envoyer des messages vers des dossiers publics à extension messagerie, l’utilisateur **Anonyme** doit disposer au minimum de l’autorisation **Création d’éléments**. Si vous avez configuré des dossiers publics à extension messagerie et que vous n’avez pas effectué l’étape précédente, les expéditeurs externes recevront une notification d’échec de remise et les messages ne seront pas transmis au dossier public à extension messagerie.
    
    Vous pouvez utiliser l’environnement de ligne de commande Exchange Management Shell ou Outlook pour définir les autorisations de l’utilisateur Anonyme. Pour en savoir plus sur la définition des autorisations de l’utilisateur Anonyme, consultez la rubrique [Activation ou désactivation de la messagerie pour un dossier public](mail-enable-or-mail-disable-a-public-folder-exchange-2013-help.md).

  - Le nombre maximal de dossiers publics pouvant être migrés vers Exchange 2013 à partir de serveurs Exchange hérités est de 500 000. Pour plus d’informations sur la migration de dossiers publics, voir [Utiliser la migration par lots pour migrer les dossiers publics vers Exchange 2013 à partir de versions antérieures](use-batch-migration-to-migrate-public-folders-to-exchange-2013-from-previous-versions-exchange-2013-help.md).

## Flux de messagerie

  - **Les cmdlets TransportAgent sur les serveurs d’accès au client nécessitent Windows PowerShell local**   Il existe un problème avec les cmdlets **\*-TransportAgent** qui empêche ces cmdlets d’installer, de désinstaller et de gérer les agents de transport sur les serveurs d’accès au client à l’aide de l’environnement de ligne de commande Exchange Management Shell. Pour installer, désinstaller et gérer les agents de transport sur des serveurs d’accès au client, vous devez charger manuellement le composant logiciel enfichable Windows PowerShell Exchange, puis exécuter les cmdlets **\*-TransportAgent**. Si vous essayez d’installer, de désinstaller ou de gérer des agents de transport à l’aide de l’environnement de ligne de commande Exchange Management Shell, vos modifications seront appliquées au serveur de boîtes aux lettres Exchange 2013 auquel vous êtes connecté.
    
    Pour installer, désinstaller ou gérer des agents de transport sur des serveurs d'accès au client, procédez comme suit sur le serveur d'accès au client à gérer :
    
    > [!CAUTION]
    > Ne chargez pas le composant logiciel enfichable Windows PowerShell <code>Microsoft.Exchange.Management.PowerShell.SnapIn</code> et n’exécutez pas de cmdlets autres que <strong>*-TransportAgent</strong> au risque de provoquer des dommages irréparables à votre déploiement Exchange.
    > Vous devez être un administrateur local sur le serveur d'accès au client sur lequel vous souhaitez installer, désinstaller ou gérer des agents de transport. Nous n’autorisons pas la modification des listes de contrôle d’accès (ACL) dans les répertoires et les fichiers Exchange ou les objets Active Directory.
    
    > [!NOTE]
    > Exécutez les opérations suivantes sur les serveurs d'accès au client uniquement. Il n’est pas nécessaire de charger le composant logiciel enfichable Windows PowerShell Exchange pour gérer des agents de transport sur des serveurs de boîtes aux lettres.
    
    1.  Ouvrez une nouvelle fenêtre Windows PowerShell.
    
    2.  Exécutez la commande suivante.
        
            Add-PSSnapin Microsoft.Exchange.Management.PowerShell.SnapIn
    
    3.  Exécutez les tâches de gestion des agents de transport comme vous procédez habituellement.
    
    4.  Répétez cette procédure sur chaque serveur d'accès au client à gérer.

## Connectivité client

  - **L’authentification NTLM échoue pour les clients non liés à un domaine**   L’authentification entre un client, tel que Windows Live Mail, et Exchange 2013 peut échouer lorsque les conditions suivantes sont remplies :
    
      - La méthode d’authentification utilisée par le client est NTLM.
    
      - L’ordinateur n’est pas lié au domaine.
    
    Pour contourner ce problème, vous pouvez effectuer l’une des actions suivantes :
    
      - Liez l’ordinateur sur lequel le client est en cours d’exécution au domaine.
    
      - Changez le type d’authentification utilisé par le client, de NTLM à l’authentification de base sur TLS.

  - **L’authentification GSSAPI échoue lorsqu’elle est utilisée avec la cmdlet Send-MailMessage**   L’authentification GSSAPI (Generic Security Service Application Program Interface) peut échouer lorsque la cmdlet **Send-MailMessage**, qui est incluse avec les installations par défaut de PowerShell Windows, est utilisée pour envoyer du courrier authentifié à Exchange 2013. Lorsque cela se produit, une entrée s’affiche dans le journal des événements **Application** sur le serveur d’accès au client Exchange 2013 qui a reçu la connexion, avec les informations suivantes :
    
      - **Source**   MSExchangeFrontEndTransport
    
      - **ID d’événement**   1035
    
      - **Description**   L’authentification entrante a échoué avec l’erreur `IllegalMessage` pour le connecteur de réception client frontal \<*nom du serveur*\>. Le mécanisme d’authentification est Gssapi. L’adresse IP source du client qui a essayé de s’authentifier auprès de Exchange est \[\<*adresse IP du client*\>\].
    
    Pour contourner ce problème, vous devez supprimer la méthode d’authentification `Integrated` du connecteur de réception client sur vos serveurs d’accès au client Exchange 2013. Pour supprimer la méthode d’authentification `Integrated` d’un connecteur de réception client, exécutez la commande suivante sur chaque serveur d’accès au client Exchange 2013 qui pourrait recevoir des connexions à partir d’ordinateurs exécutant la cmdlet **Send-MailMessage** :
    
        Set-ReceiveConnector "<server name>\Client Frontend <server name>" -AuthMechanism Tls, BasicAuth, BasicAuthRequireTLS

  - **Le protocole MAPI sur HTTP peut rencontrer des problèmes de performances lors de la mise à niveau vers Exchange 2013 SP1**   Si vous effectuez une mise à niveau à partir d’une mise à jour cumulative Exchange 2013 vers Exchange 2013 SP1 et que vous activez MAPI sur HTTP, les clients qui se connectent à un serveur Exchange 2013 SP1 à l’aide de ce protocole peuvent rencontrer des problèmes de performances. En effet, les paramètres requis ne sont pas configurés lors d’une mise à niveau à partir d’une mise à jour cumulative vers Exchange 2013 SP1. Ce problème ne se produit pas si vous effectuez une mise à niveau vers Exchange 2013 SP1 depuis Exchange 2013 RTM ou si vous installez un nouveau serveur Exchange 2013 SP1 ou versions ultérieures.
    
    > [!NOTE]
    > Ce problème n’est observé que si le protocole MAPI sur HTTP est activé sur vos serveurs d’accès au client. Il est désactivé par défaut. Si le protocole MAPI sur HTTP est désactivé, les clients utilisent le protocole RPC sur HTTP à la place.
    
    Pour contourner ce problème, procédez comme suit :
    
    1.  Sur les serveurs exécutant le rôle serveur d’accès au client, exécutez les commandes suivantes dans une invite de commandes Windows :
        
            set AppCmdLocation=%windir%\System32\inetsrv
            set ExchangeLocation=%ProgramFiles%\Microsoft\Exchange Server\V15
            
            %AppCmdLocation%\appcmd.exe SET AppPool "MSExchangeMapiFrontEndAppPool" /CLRConfigFile:"%ExchangeLocation%\bin\MSExchangeMapiFrontEndAppPool_CLRConfig.config"
            %AppCmdLocation%\appcmd.exe RECYCLE AppPool "MSExchangeMapiFrontEndAppPool"
    
    2.  Sur les serveurs exécutant le rôle serveur de boîtes aux lettres, exécutez les commandes suivantes dans une invite de commandes Windows :
        
            set AppCmdLocation=%windir%\System32\inetsrv
            set ExchangeLocation=%ProgramFiles%\Microsoft\Exchange Server\V15
            
            %AppCmdLocation%\appcmd.exe SET AppPool "MSExchangeMapiMailboxAppPool" /CLRConfigFile:"%ExchangeLocation%\bin\MSExchangeMapiMailboxAppPool_CLRConfig.config"
            %AppCmdLocation%\appcmd.exe RECYCLE AppPool "MSExchangeMapiMailboxAppPool"
            
            %AppCmdLocation%\appcmd.exe SET AppPool "MSExchangeMapiAddressBookAppPool" /CLRConfigFile:"%ExchangeLocation%\bin\MSExchangeMapiAddressBookAppPool_CLRConfig.config"
            %AppCmdLocation%\appcmd.exe RECYCLE AppPool "MSExchangeMapiAddressBookAppPool"

## Coexistence avec Exchange 2010

  - **Les demandes d’accès aux boîtes aux lettres Exchange 2010 peuvent ne pas fonctionner lorsqu’elles sont transférées par proxy via les serveurs d’accès au client Exchange 2013**   Dans certaines situations, la requête proxy entre les serveurs d’accès au client Exchange 2013 et Exchange 2010 Service Pack 3 (SP3) sans correctif cumulatif peut ne pas fonctionner correctement et une erreur s’affiche. Cette situation peut se produire si les conditions suivantes sont remplies :
    
      - Un utilisateur disposant d’une boîte aux lettres Exchange 2013 essaie d’ouvrir une boîte aux lettres Exchange 2010 à l’aide d’une des méthodes suivantes :
        
          - L’option **Ouvrir une autre boîte aux lettres** dans Outlook Web App**OU**
        
          - L’option **Un autre utilisateur** dans le Centre d’administration Exchange (CAE)
    
      - Le serveur d’accès au client auquel s’est connecté l’utilisateur exécute Exchange 2013.
    
      - Le serveur d’accès au client Exchange 2010 a été mis à niveau vers Exchange 2010 SP3 à partir de la version finalisée (RTM) d’Exchange 2010 ou d’un Service Pack Exchange 2010 précédent.
    
    Si toutes les conditions ci-dessus sont remplies, l’utilisateur ne pourra pas accéder aux options Outlook Web AppExchange 2010 de l’autre utilisateur et une page vierge risque de s’afficher.
    
    Pour contourner ce problème, installez le correctif cumulatif 1 d’Exchange 2010 SP3 ou une version ultérieure sur chaque serveur Exchange 2010.

