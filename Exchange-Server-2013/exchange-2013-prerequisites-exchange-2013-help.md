---
title: 'Conditions préalables pour Exchange 2013: Exchange 2013 Help'
TOCTitle: Conditions préalables pour Exchange 2013
ms:assetid: e21cf744-7813-48b3-9293-5cecd89a6c25
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb691354(v=EXCHG.150)
ms:contentKeyID: 50479424
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Conditions préalables pour Exchange 2013

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2017-03-20_

Cette rubrique présente les étapes d’installation des prérequis des systèmes d’exploitation Windows Server 2012 R2, Windows Server 2012 et Windows Server 2008 R2 avec le Service Pack 1 (SP1) pour les rôles serveur d'accès au client, de boîte aux lettres Microsoft Exchange 2013 et de transport Edge Elle indique également les conditions préalables nécessaires à l'installation des outils de gestion Exchange 2013 sur les ordinateurs clients Windows 8, Windows 8.1 et Windows 7.

  - Ce qu'il faut savoir avant de commencer

  - Préparation d'Active Directory

  - Conditions préalables pour Windows Server 2012 R2 et Windows Server 2012
    
      - Rôles serveur de boîte aux lettres ou d’accès au client
    
      - Rôle serveur de transport Edge

  - Composants préalables de Windows Server 2008 R2 SP1
    
      - Rôles serveur de boîte aux lettres ou d’accès au client
    
      - Rôle serveur de transport Edge

  - Configuration requise pour Windows 7 (outils d’administration uniquement) (outils d’administration uniquement)

  - Configuration requise pour Windows 8 et Windows 8.1 (outils d’administration uniquement) (outils d’administration uniquement)

## Ce qu'il faut savoir avant de commencer

  - Les informations contenues dans cette rubrique s’appliquent au Service Pack 1 et versions ultérieures d’Exchange 2013.

  - Le rôle serveur de transport Edge est disponible à partir d’Exchange 2013 SP1.

  - Assurez-vous que le niveau fonctionnel de votre forêt est au moins Windows Server 2003 et que le contrôleur de schéma exécute Windows Server 2003 avec le Service Pack 2 ou une version ultérieure. Pour plus d'informations sur le niveau fonctionnel de Windows, consultez la rubrique [Gestion des domaines et des forêts](https://go.microsoft.com/fwlink/p/?linkid=137037).

  - L’option d’installation complète de Windows Server 2012, Windows Server 2012 et Windows Server 2008 R2 SP1 doit être utilisée pour tous les serveurs exécutant des rôles serveur ou outils de gestion Exchange 2013.

  - Vous devez d'abord relier l'ordinateur à la forêt et au domaine Active Directory appropriés.

  - Certaines conditions préalables requièrent de redémarrer le serveur pour terminer l'installation.

  - Installez les dernières mises à jour de Windows sur votre ordinateur. Pour plus d'informations, consultez la rubrique [Liste de vérification pour la sécurité du pré-déploiement](deployment-security-checklist-exchange-2013-help.md).
    
    > [!NOTE]
    > Si vous installez le rôle serveur de boîtes aux lettres et souhaitez que le serveur soit membre d’un groupe de disponibilité de base de données (DAG), vous devez exécuter l’édition Standard ou Datacenter de Windows Server 2012 R2, l’édition Standard ou Datacenter de Windows Server 2012 ou l’édition Enterprise de Windows Server 2008 R2 SP1. L'édition Standard de Windows Server 2008 R2 SP1 ne prend pas en charge les fonctionnalités nécessaires pour les groupes de disponibilité de base de données.
    > Vous ne pouvez pas mettre à niveau Windows quand Exchange est installé sur le serveur.
    > Pour installer la mise à niveau vers Microsoft Unified Communications Managed API (UCMA) 4.0, vous devez d'abord désinstaller les versions antérieures d'UCMA à l'aide de <strong>Ajout/Suppression de programmes</strong>.



> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.


## Préparation d'Active Directory

L'ordinateur que vous souhaitez utiliser pour préparer Active Directory à Exchange 2013 présente des conditions préalables qu'il vous faut satisfaire.

Installez les logiciels suivants, en respectant l’ordre indiqué, sur l’ordinateur que vous allez utiliser pour préparer Active Directory :

1.  [.NET Framework 4.6.2](https://go.microsoft.com/fwlink/p/?linkid=808659)

2.  [Windows Management Framework 4.0](https://go.microsoft.com/fwlink/p/?linkid=390234) (inclus avec Windows Server 2012 R2)

Après avoir installé les logiciels indiqués ci-dessus, suivez les étapes suivantes pour installer le pack d'administration des outils à distance. Une fois ce pack installé, vous êtes en mesure d'utiliser l'ordinateur pour préparer Active Directory. Pour plus d'informations sur la préparation d’Active Directory, consultez la rubrique [Préparation d’Active Directory et des domaines](prepare-active-directory-and-domains-exchange-2013-help.md).

1.  Ouvrez Windows PowerShell.

2.  Installez le pack d'administration des outils à distance.
    
      - Sur un ordinateur Windows Server 2012 R2 ou Windows Server 2012, exécutez la commande suivante.
        
        ```powershell
        Install-WindowsFeature RSAT-ADDS
        ```
    
      - Sur un ordinateur Windows Server 2008 R2 SP1, exécutez la commande suivante.
        
        ```powershell
        Add-WindowsFeature RSAT-ADDS
        ```

## Conditions préalables pour Windows Server 2012 R2 et Windows Server 2012

Les prérequis nécessaires pour installer Exchange 2013 sur un ordinateur Windows Server 2012 R2 ou Windows Server 2012 dépendent des rôles Exchange que vous voulez installer. Lire la section ci-dessous qui correspond à des rôles que vous voulez installer.

## Rôles serveur de boîte aux lettres ou d’accès au client

Suivez les instructions de la présente section pour installer les composants préalables sur les ordinateurs Windows Server 2012 R2 ou Windows Server 2012 sur lesquels vous souhaitez réaliser l'une des actions suivantes :

  - Installez uniquement le rôle serveur de boîtes aux lettres sur un ordinateur.

  - Installez uniquement le rôle serveur d’accès au client sur un ordinateur.

  - Installez les deux boîtes aux lettres et les rôles serveur d'accès au client sur ​​le même ordinateur.

Procédez comme suit pour installer les rôles Windows requis et les fonctionnalités :

1.  Ouvrez Windows PowerShell.

2.  Exécutez la commande suivante pour installer les composants Windows requis.
    
    ```powershell
    Install-WindowsFeature AS-HTTP-Activation, Desktop-Experience, NET-Framework-45-Features, RPC-over-HTTP-proxy, RSAT-Clustering, RSAT-Clustering-CmdInterface, RSAT-Clustering-Mgmt, RSAT-Clustering-PowerShell, Web-Mgmt-Console, WAS-Process-Model, Web-Asp-Net45, Web-Basic-Auth, Web-Client-Auth, Web-Digest-Auth, Web-Dir-Browsing, Web-Dyn-Compression, Web-Http-Errors, Web-Http-Logging, Web-Http-Redirect, Web-Http-Tracing, Web-ISAPI-Ext, Web-ISAPI-Filter, Web-Lgcy-Mgmt-Console, Web-Metabase, Web-Mgmt-Console, Web-Mgmt-Service, Web-Net-Ext45, Web-Request-Monitor, Web-Server, Web-Stat-Compression, Web-Static-Content, Web-Windows-Auth, Web-WMI, Windows-Identity-Foundation, RSAT-ADDS
    ```

Une fois que vous avez installé les rôles et les fonctions du système d'exploitation, installez les logiciels suivants dans l'ordre indiqué :

1.  [.NET Framework 4.6.2](https://go.microsoft.com/fwlink/p/?linkid=808659)
    
    > [!IMPORTANT]
    > Exchange 2013 CU16 et versions ultérieures <strong>nécessitent</strong> .NET Framework 4.6.2. Mettez à niveau vos serveurs vers .NET Framework 4.6.2 avant d’installer Exchange 2013 CU16, ou vous recevrez une erreur. Si .NET Framework 4.5.2 est installé sur vos serveurs Exchange, mettez à niveau vos serveurs Exchange 2013 CU15 avant d’installer .NET Framework 4.6.2.


2.  [Windows Management Framework 4.0](https://go.microsoft.com/fwlink/p/?linkid=390234) (inclus avec Windows Server 2012 R2)

3.  [Microsoft Unified Communications Managed API 4.0, Core Runtime 64 bits](https://go.microsoft.com/fwlink/p/?linkid=258269)

## Rôle serveur de transport Edge

Suivez les instructions de la présente section pour installer les composants préalables sur les ordinateurs Windows Server 2012 R2 ou Windows Server 2012 sur lesquels vous souhaitez installer le rôle serveur de transport Edge.

Procédez comme suit pour installer les rôles Windows requis et les fonctionnalités :

1.  Ouvrez Windows PowerShell.

2.  Exécutez la commande suivante pour installer les composants Windows requis.
    
    ```powershell
    Install-WindowsFeature ADLDS
    ```

Installez la version de Microsoft .NET Framework qui correspond à la version d’Exchange 2013 que vous installez :

1.  [.NET Framework 4.6.2](https://go.microsoft.com/fwlink/p/?linkid=808659)
    
    > [!IMPORTANT]
    > Exchange 2013 CU16 et versions ultérieures <strong>nécessitent</strong> .NET Framework 4.6.2. Mettez à niveau vos serveurs vers .NET Framework 4.6.2 avant d’installer Exchange 2013 CU16, ou vous recevrez une erreur. Si .NET Framework 4.5.2 est installé sur vos serveurs Exchange, mettez à niveau vos serveurs Exchange 2013 CU15 avant d’installer .NET Framework 4.6.2.


2.  [Windows Management Framework 4.0](https://go.microsoft.com/fwlink/p/?linkid=390234) (inclus avec Windows Server 2012 R2)

## Composants préalables de Windows Server 2008 R2 SP1

Les conditions préalables à satisfaire pour installer Exchange 2013 sur un ordinateur Windows Server 2008 R2 SP1 dépendent des rôles Exchange que vous souhaitez installer. Lire la section ci-dessous qui correspond à des rôles que vous voulez installer.

## Rôles serveur de boîte aux lettres ou d’accès au client

Suivez les instructions de la présente section pour installer les composants préalables sur les ordinateurs Windows Server 2008 R2 SP1 sur lesquels vous souhaitez réaliser l'une des actions suivantes :

  - Installez uniquement le rôle serveur de boîtes aux lettres sur un ordinateur.

  - Installez uniquement le rôle serveur d’accès au client sur un ordinateur.

  - Installez les deux boîtes aux lettres et les rôles serveur d'accès au client sur ​​le même ordinateur.

Procédez comme suit pour installer les rôles Windows requis et les fonctionnalités :

1.  Ouvrez Windows PowerShell.

2.  Exécutez la commande suivante pour charger le module Gestionnaire de serveur.
    
    ```powershell
    Import-Module ServerManager
    ```

3.  Exécutez la commande suivante pour installer les composants Windows requis.
    
    ```powershell
    Add-WindowsFeature Desktop-Experience, NET-Framework, NET-HTTP-Activation, RPC-over-HTTP-proxy, RSAT-Clustering, RSAT-Web-Server, WAS-Process-Model, Web-Asp-Net, Web-Basic-Auth, Web-Client-Auth, Web-Digest-Auth, Web-Dir-Browsing, Web-Dyn-Compression, Web-Http-Errors, Web-Http-Logging, Web-Http-Redirect, Web-Http-Tracing, Web-ISAPI-Ext, Web-ISAPI-Filter, Web-Lgcy-Mgmt-Console, Web-Metabase, Web-Mgmt-Console, Web-Mgmt-Service, Web-Net-Ext, Web-Request-Monitor, Web-Server, Web-Stat-Compression, Web-Static-Content, Web-Windows-Auth, Web-WMI, RSAT-ADDS
    ```

Une fois que vous avez installé les rôles et les fonctions du système d'exploitation, installez les logiciels suivants dans l'ordre indiqué :

1.  [.NET Framework 4.6.2](https://go.microsoft.com/fwlink/p/?linkid=808659)
    
    > [!IMPORTANT]
    > Exchange 2013 CU16 et versions ultérieures <strong>nécessitent</strong> .NET Framework 4.6.2. Mettez à niveau vos serveurs vers .NET Framework 4.6.2 avant d’installer Exchange 2013 CU16, ou vous recevrez une erreur. Si .NET Framework 4.5.2 est installé sur vos serveurs Exchange, mettez à niveau vos serveurs Exchange 2013 CU15 avant d’installer .NET Framework 4.6.2.


2.  [Windows Management Framework 4.0](https://go.microsoft.com/fwlink/p/?linkid=390234)

3.  [Microsoft Unified Communications Managed API 4.0, Core Runtime 64 bits](https://go.microsoft.com/fwlink/p/?linkid=258269)

4.  [Article de la base de connaissances Microsoft KB974405 (Windows Identity Foundation)](http://go.microsoft.com/fwlink/?linkid=3052&kbid=974405)

5.  [Article de la base de connaissances KB2619234 (Permettre les témoins de l'association/GUID utilisé par RPC sur HTTP pour être aussi utilisé dans la couche RPC dans Windows 7 et Windows Server 2008 R2)](http://go.microsoft.com/fwlink/?linkid=3052&kbid=2619234)

6.  [Article de la base de connaissances KB2533623 (Chargement de bibliothèque non sécurisé pourrait permettre l'exécution de code à distance)](http://go.microsoft.com/fwlink/?linkid=3052&kbid=2533623)
    
    > [!NOTE]
    > Ce correctif peut déjà être installé si vous avez configuré Windows Update pour installer les mises à jour de sécurité sur votre ordinateur.


## Rôle serveur de transport Edge

Suivez les instructions de la présente section pour installer les composants préalables sur les ordinateurs Windows Server 2008 R2 SP1 sur lesquels vous souhaitez installer le rôle serveur de transport Edge.

Procédez comme suit pour installer les rôles Windows requis et les fonctionnalités :

1.  Ouvrez Windows PowerShell.

2.  Exécutez la commande suivante pour charger le module Gestionnaire de serveur.
    
    ```powershell
    Import-Module ServerManager
    ```

3.  Exécutez la commande suivante pour installer les composants Windows requis.
    
    ```powershell
    Add-WindowsFeature NET-Framework, ADLDS
    ```

Une fois que vous avez installé les rôles et les fonctions du système d'exploitation, installez les logiciels suivants dans l'ordre indiqué :

1.  [.NET Framework 4.6.2](https://go.microsoft.com/fwlink/p/?linkid=808659)
    
    > [!IMPORTANT]
    > Exchange 2013 CU16 et versions ultérieures <strong>nécessitent</strong> .NET Framework 4.6.2. Mettez à niveau vos serveurs vers .NET Framework 4.6.2 avant d’installer Exchange 2013 CU16, ou vous recevrez une erreur. Si .NET Framework 4.5.2 est installé sur vos serveurs Exchange, mettez à niveau vos serveurs Exchange 2013 CU15 avant d’installer .NET Framework 4.6.2.


2.  [Windows Management Framework 4.0](https://go.microsoft.com/fwlink/p/?linkid=390234)

3.  [Microsoft Unified Communications Managed API 4.0, Core Runtime 64 bits](https://go.microsoft.com/fwlink/p/?linkid=258269)

## Configuration requise pour Windows 7 (outils d’administration uniquement)

Suivez les instructions de la présente section pour installer les composants préalables sur les ordinateurs Windows 7 64 bits liés à un domaine sur lesquels vous souhaitez installer les outils de gestion Exchange.

1.  Ouvrez le **Panneau de configuration** et sélectionnez **Programmes**.

2.  Cliquez sur **Activer ou désactiver les fonctionnalités Windows**.

3.  Accédez à **Services Internet (IIS)** \>**Outils d’administration web** \>**Compatibilité avec la gestion IIS 6**.

4.  Activez la case à cocher **Console de gestion IIS 6**, puis cliquez sur **OK**.

Après avoir installé les fonctionnalités du système d'exploitation, installez les logiciels suivants dans l'ordre indiqué :

1.  [.NET Framework 4.6.2](https://go.microsoft.com/fwlink/p/?linkid=808659)

2.  [Windows Management Framework 4.0](https://go.microsoft.com/fwlink/p/?linkid=390234)

3.  [Article de la base de connaissances KB974405 (Windows Identity Foundation)](http://go.microsoft.com/fwlink/?linkid=3052&kbid=974405)

## Configuration requise pour Windows 8 et Windows 8.1 (outils d’administration uniquement)

[.NET Framework 4.6.2](https://go.microsoft.com/fwlink/p/?linkid=808659)

