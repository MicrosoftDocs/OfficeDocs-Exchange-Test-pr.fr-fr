---
title: 'Installation d’Exchange 2013 en mode sans assistance: Exchange 2013 Help'
TOCTitle: Installation d’Exchange 2013 en mode sans assistance
ms:assetid: 386465e9-41da-4e26-9816-b3b69be1f8bf
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Aa997281(v=EXCHG.150)
ms:contentKeyID: 50477923
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Installation d’Exchange 2013 en mode sans assistance

 

_**Sapplique à :**Exchange Server 2013_

_**Dernière rubrique modifiée :**2014-06-19_

Pour effectuer une installation sans assistance, vous devez installer Microsoft Exchange Server 2013 depuis l'invite de commandes. Pour de plus amples informations sur la planification et le déploiement d'Exchange 2013, consultez la rubrique [Planification et déploiement](planning-and-deployment-for-exchange-2013-installation-instructions.md).

Nous recommandons d’installer le rôle de transport Edge dans un réseau de périmètre extérieur à la forêt interne de votre organisation Active Directory. Bien que vous puissiez installer le rôle serveur de transport Edge sur un ordinateur joint à un domaine, cette configuration vous permettrait uniquement de gérer les fonctionnalités et les paramètres Windows. Le rôle de transport Edge n’utilise pas Active Directory. Par contre, il utilise la fonctionnalité Active Directory AD LDS (Lightweight Directory Services) Windows pour stocker la configuration et les informations de destinataire. Pour plus d’informations sur le rôle de transport Edge, consultez la rubrique [Serveurs de transport Edge](edge-transport-servers-exchange-2013-help.md).

<table>
<thead>
<tr class="header">
<th><img src="images/Bb125224.tip(EXCHG.150).gif" title="Conseil" alt="Conseil" />Conseil :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Avez-vous déjà entendu parler de l’Assistant de déploiement Exchange Server ? Il s’agit d’un outil en ligne gratuit qui vous permet de déployer rapidement Exchange 2013 dans votre organisation en répondant à quelques questions et en créant une liste de contrôle de déploiement personnalisée. Pour en savoir plus, consultez la page <a href="exchange-server-deployment-assistant-exchange-2013-help.md">Assistant de déploiement Exchange Server</a>.</td>
</tr>
</tbody>
</table>


<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Après avoir installé des rôles serveur sur un ordinateur exécutant Exchange 2013, il n'est plus possible d'utiliser l'Assistant Installation d'Exchange 2013 pour ajouter des rôles serveur à cet ordinateur. Pour ajouter des rôles serveur supplémentaires à un ordinateur, vous devez utiliser la fonctionnalité Ajout/Suppression de programmes du Panneau de configuration ou la commande Setup.exe depuis une fenêtre d'invite de commandes.<br />
Le rôle de transport Edge ne peut pas être installé sur le même ordinateur que les rôles serveur de boîtes aux lettres ou d’accès au client.</td>
</tr>
</tbody>
</table>


Pour plus d'informations sur les tâches postérieures à l'installation, consultez la rubrique [Tâches consécutives à l’installation d’Exchange 2013](exchange-2013-post-installation-tasks-exchange-2013-help.md).

## Ce qu'il faut savoir avant de commencer

Les informations suivantes s’appliquent à tous les rôles serveur Exchange 2013.

  - Assurez-vous que vous avez lu les notes de publication avant d'installer Exchange 2013. Pour plus d'informations, consultez la rubrique [Notes de publication relatives à Exchange 2013](release-notes-for-exchange-2013-exchange-2013-help.md).

  - L’ordinateur sur lequel vous installez Exchange 2013 doit disposer d’un système d’exploitation compatible (tel que Windows Server 2008 R2 avec Service Pack 1 (SP1), Windows Server 2012 R2 ou Windows Server 2012), avoir suffisamment d’espace disque et respecter d’autres exigences. Pour plus d'informations sur la configuration système requise, consultez la rubrique [Configuration requise pour Exchange 2013](exchange-2013-system-requirements-exchange-2013-help.md).

  - Pour exécuter la configuration d’Exchange 2013, vous devez installer Microsoft .NET Framework 4.5, Windows Management Framework et d’autres logiciels requis. Pour connaître les conditions préalables pour tous les rôles de serveur, consultez la rubrique [Conditions préalables pour Exchange 2013](exchange-2013-prerequisites-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

<table>
<thead>
<tr class="header">
<th><img src="images/JJ673034.Caution(EXCHG.150).gif" title="Attention" alt="Attention" />Attention :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Après avoir installé Exchange sur un serveur, vous ne devez pas modifier le nom du serveur. La modification du nom d’un serveur après avoir installé un rôle de serveur Exchange n’est pas prise en charge.</td>
</tr>
</tbody>
</table>


Les informations suivantes s’appliquent aux rôles serveur de boîtes aux lettres et d’accès au client Exchange 2013.

  - Durée d'exécution estimée : 60 minutes

  - Chaque organisation demande au minimum un serveur d'accès au client et un serveur de boîtes aux lettres dans la forêt Active Directory. De plus, chaque site Active Directory qui contient un serveur de boîtes aux lettres doit également contenir au moins un serveur d'accès au client. Si vous séparez les rôles de vos serveurs, nous vous recommandons d'installer le serveur ayant le rôle de serveur de boîtes aux lettres en premier.

  - L’ordinateur sur lequel vous installez Exchange 2013 doit être membre d’un domaine Active Directory.

  - Vous devez vous assurer qu'une appartenance au groupe Administrateurs de schéma a été déléguée au compte utilisé si vous n'avez pas déjà préparé le schéma Active Directory. Si vous installez le premier serveur Exchange 2013 de l'organisation, vous devez utiliser un compte appartenant au groupe Administrateurs d'entreprise. Si vous avez déjà préparé le schéma mais que vous n'installez pas le premier serveur Exchange 2013 de l'organisation, vous devez utiliser un compte appartenant au groupe de rôles Gestion de l'organisation Exchange 2013.
    
    Les administrateurs membres du groupe de rôles Installation déléguée peuvent déployer des serveurs Exchange 2013 qui ont été précédemment mis en service par un membre du groupe de rôles Gestion de l'organisation.

Les informations suivantes s’appliquent au rôle serveur de transport Edge Exchange 2013.

  - Durée d’exécution estimée : 40 minutes

  - Le rôle de transport Edge est disponible avec Exchange 2013 SP1 ou version ultérieure.

  - Vous devez configurer le suffixe DNS principal sur l’ordinateur. Par exemple, si le nom de domaine complet de votre ordinateur est edge.contoso.com, le suffixe DNS de cet ordinateur est contoso.com. Pour plus d’informations, voir [Suffixe DNS principal manquant](primary-dns-suffix-is-missing-exchange-2013-help.md).

  - Les serveurs de transport Hub Exchange 2007 et Exchange 2010 doivent être mis à jour pour créer un abonnement EdgeSync entre eux et un serveur de transport Edge Exchange 2013. Si vous n’installez pas cette mise à jour, l’abonnement EdgeSync ne fonctionnera pas correctement. Pour plus d’informations, consultez la section « Scénarios de coexistence pris en charge » dans la rubrique [Configuration requise pour Exchange 2013](exchange-2013-system-requirements-exchange-2013-help.md).

  - Assurez-vous que le compte que vous utilisez est membre du groupe Administrateurs local sur l’ordinateur sur lequel vous installez le rôle de transport Edge.

## Utilisez Setup.exe pour installer Exchange 2013 en mode sans assistance

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Pour télécharger la dernière version d’Exchange 2013, voir <a href="updates-for-exchange-2013-exchange-2013-help.md">Mises à jour pour Exchange 2013</a></td>
</tr>
</tbody>
</table>


1.  Connectez-vous à l'ordinateur sur lequel vous voulez installer Exchange 2013.

2.  Accédez à l'emplacement réseau des fichiers d'installation d'Exchange 2013.

3.  À l'invite de commandes, exécutez la commande applicable à votre organisation.
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ159813.important(EXCHG.150).gif" title="Important" alt="Important" />Important :</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Si le contrôle de compte d'utilisateur est activé, vous devez exécuter <code>Setup.exe</code> à partir d'une invite de commandes élevée.</td>
    </tr>
    </tbody>
    </table>
    
        Setup.exe [/Mode:<setup mode>] [/IAcceptExchangeServerLicenseTerms]
        [/Roles:<server roles to install>] [/InstallWindowsComponents] 
        [/OrganizationName:<name for the new Exchange organization>] 
        [/TargetDir:<target directory>] [/SourceDir:<source directory>]
        [/UpdatesDir:<directory from which to install updates>] 
        [/DomainController:<FQDN of domain controller>] [/DisableAMFiltering]
        [/AnswerFile:<filename>] [/DoNotStartTransport] 
        [/EnableErrorReporting] [/CustomerFeedbackEnabled:<True | False>] 
        [/AddUmLanguagePack:<UM language pack name>] 
        [/RemoveUmLanguagePack:<UM language pack name>] 
        [/NewProvisionedServer:<server>] [/RemoveProvisionedServer:<server>] 
        [/MdbName:<mailbox database name>] [/DbFilePath:<Edb file path>] 
        [/LogFolderPath:<log folder path>] [/ActiveDirectorySplitPermissions:<True | False>]
        [/TenantOrganizationConfig:<path>]

4.  Le programme d'installation copie les fichiers d'installation localement sur l'ordinateur sur lequel vous installez Exchange 2013.

5.  Le programme d'installation vérifie les conditions préalables, notamment toutes les conditions spécifiques aux rôles serveur que vous installez. Si toutes les conditions préalables ne sont pas satisfaites, le programme d'installation échoue et renvoie un message d'erreur indiquant le motif de l'échec. Si toutes les conditions préalables sont remplies, le programme installe Exchange 2013.

6.  Redémarrez l'ordinateur une fois l'installation d'Exchange 2013 terminé.

7.  Terminez votre déploiement en exécutant les tâches fournies dans [Tâches consécutives à l’installation d’Exchange 2013](exchange-2013-post-installation-tasks-exchange-2013-help.md).

## Exemples

Voici des exemples d'utilisation de Setup.exe :

  - **Setup.exe /mode:Install /role:ClientAccess,Mailbox /OrganizationName:MyOrg /IAcceptExchangeServerLicenseTerms**
    
    Cette commande crée une organisation Exchange 2013 dans Active Directory appelée MyOrg, installe le rôle serveur d'accès au client, le rôle serveur de boîtes aux lettres et des outils de gestion. Elle accepte également le contrat de licence Exchange 2013.

  - **Setup.exe /mode:Install /role:ClientAccess,Mailbox /TargetDir:"C:\\Exchange Server" /IAcceptExchangeServerLicenseTerms**
    
    Cette commande installe le rôle serveur d'accès au client, le rôle serveur de boîtes aux lettres et les outils de gestion dans le répertoire « C:\\Exchange Server ». Cette commande suppose qu'une organisation Exchange 2013 a déjà été préparée.

  - **Setup.exe /mode:Install /r:CA,MB /IAcceptExchangeServerLicenseTerms**
    
    Cette commande installe le rôle serveur d'accès au client, le rôle serveur de boîtes aux lettres et les outils de gestion à l'emplacement d'installation par défaut.

  - **Setup.exe /mode:Install /r:EdgeTransport /IAcceptExchangeServerLicenseTerms**
    
    Cette commande installe le rôle serveur de transport Edge et les outils de gestion sur l’emplacement d’installation par défaut.

  - **Setup.exe /mode:Install /r:ET /IAcceptExchangeServerLicenseTerms**
    
    Cette commande installe le rôle serveur de transport Edge et les outils de gestion sur l’emplacement d’installation par défaut.

  - **Setup.exe /mode:Uninstall /IAcceptExchangeServerLicenseTerms**
    
    Cette commande supprime complètement Exchange 2013 du serveur ainsi que la configuration Exchange de ce serveur d'Active Directory.

  - **Setup.exe /PrepareAD /on:"My Org" /IAcceptExchangeServerLicenseTerms**
    
    Cette commande crée une organisation Exchange nommée My Org et prépare Active Directory pour Exchange 2013.

  - **C:\\ExchangeServer\\bin\\Setup.exe /m:Install /r:ClientAccess /SourceDir:d:\\amd64 /IAcceptExchangeServerLicenseTerms**
    
    Cette commande ajoute le rôle serveur d'accès au client à un serveur Exchange 2013 existant en utilisant D:\\amd64 comme répertoire source.

  - **Setup.exe /role:ClientAccess,Mailbox /UpdatesDir:"C:\\ExchangeServer\\New Patches" /IAcceptExchangeServerLicenseTerms**
    
    Cette commande met à jour ExchangeServer.msi avec des correctifs du répertoire spécifié, puis installe le rôle serveur d'accès au client, le rôle serveur de boîtes aux lettres et les outils de gestion. Si un lot de modules linguistiques est inclus dans ce répertoire, le module linguistique est également installé.

  - **Setup.exe /mode:Install /role:ClientAccess,Mailbox /DomainController:DC01 /IAcceptExchangeServerLicenseTerms**
    
    Cette commande utilise le contrôleur de domaine DC01 pour interroger et apporter des modifications à Active Directory tout en installant le rôle serveur d'accès au client, le rôle serveur de boîtes aux lettres et les outils de gestion.

  - **Setup.exe /mode:Install /role:ClientAccess /AnswerFile:c:\\ExchangeConfig.txt /IAcceptExchangeServerLicenseTerms**
    
    Cette commande installe le rôle serveur d'accès au client à l'aide des paramètres du fichier ExchangeConfig.txt.

  - **Setup.exe /rprs:Exchange03 /IAcceptExchangeServerLicenseTerms**
    
    Cette commande supprime l'objet Exchange03 d'Active Directory.

  - **Setup.exe /AddUmLanguagePack:ko-KR /IAcceptExchangeServerLicenseTerms**
    
    Cette commande installe le module linguistique de messagerie unifiée coréen à partir du répertoire %ExchangeSourceDir%\\ServerRoles\\UnifiedMessaging.

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez installé Exchange 2013 avec succès, consultez [Vérifier une installation d’Exchange 2013](verify-an-exchange-2013-installation-exchange-2013-help.md).

Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), et [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

Avez-vous trouvé ce que vous cherchez ? Veuillez prendre une minute pour [nous envoyer votre avis à l'adresse](mailto:exsetuphelpfeedback@microsoft.com?subject=exchange%202013%20setup%20help%20feedback) au sujet des informations que vous souhaitiez y trouver.

