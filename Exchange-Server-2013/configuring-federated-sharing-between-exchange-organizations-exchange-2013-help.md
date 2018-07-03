---
title: 'Configuration du partage fédéré entre des organisations Exchange: Exchange 2013 Help'
TOCTitle: Configuration du partage fédéré entre des organisations Exchange
ms:assetid: 94e31454-b027-4757-b52f-d3c2ead6d916
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ657473(v=EXCHG.150)
ms:contentKeyID: 50478757
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configuration du partage fédéré entre des organisations Exchange

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2016-12-09_

Le partage fédéré permet aux utilisateurs de votre organisation Exchange locale de partager des informations de disponibilité du calendrier (disponible/occupé) avec des destinataires d'autres organisations Exchange également configurées pour le partage fédéré. Le partage de disponibilités peut être activé entre deux organisations qui exécutent Exchange 2013, ainsi qu'entre des organisations à déploiement Exchange mixte. Pour en savoir plus sur le partage fédéré, consultez la rubrique [Partage](sharing-exchange-2013-help.md).

Cette rubrique fournit un résumé des exigences et des étapes de configuration nécessaires pour activer le partage des disponibilités entre différents types des déploiements Exchange communs suivants :

  - Deux organisations Exchange 2013.

  - Une organisation Exchange 2013 et une organisation Exchange 2010 SP2.

  - Une organisation Exchange 2007 (ou une organisation mixte Exchange 2007 et Exchange 2010 SP2) et une organisation Exchange 2013.

  - Une organisation Exchange 2003 (ou une organisation mixte Exchange 2003 et Exchange 2010 SP2) et une organisation Exchange 2013.

Si vous souhaitez rechercher des tâches de gestion supplémentaires relatives au partage fédéré, consultez [Procédures de fédération](federation-procedures-exchange-2013-help.md).

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159813.important(EXCHG.150).gif" title="Important" alt="Important" />Important :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Cette fonctionnalité d’Exchange Server 2013 n’est pas entièrement compatible avec les systèmes Office 365 exécutés par 21Vianet en Chine et certaines limitations de fonctionnalités peuvent s’appliquer. Pour plus d’informations, voir <a href="https://go.microsoft.com/fwlink/?linkid=313640">En savoir plus sur Office 365 exécuté par 21Vianet</a>.</td>
</tr>
</tbody>
</table>


## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée de chaque procédure : 2 heures.

  - Les procédures décrites dans cette rubrique requièrent des autorisations spécifiques. Consultez chaque procédure pour savoir quelles autorisations sont nécessaires.

  - Préalablement à l'exécution des procédures de cette rubrique, assurez-vous d'avoir bien compris les limitations qui sont associées au partage des informations de disponibilités sur des organisations Exchange. Pour plus d'informations, consultez la rubrique [Limitations of free/busy sharing](sharing-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

## Que souhaitez-vous faire ?

## Configurer le partage des disponibilités entre des organisations Exchange 2013

Exécutez les étapes de [Configurer le partage fédéré](configure-federated-sharing-exchange-2013-help.md) pour les deux organisations.

## Configurer le partage des disponibilités entre des organisations Exchange 2013 et Exchange 2010 SP2

  - Configurer le partage fédéré pour l'organisation Exchange 2013. Exécutez les étapes décrites dans la rubrique [Configurer le partage fédéré](configure-federated-sharing-exchange-2013-help.md).

  - Configurer une délégation fédérée (ancien nom du partage fédéré) pour l’organisation Exchange 2010 SP2. Exécutez les étapes de [Configurer la délégation fédérée](https://go.microsoft.com/fwlink/p/?linkid=268410).

## Configurer le partage des disponibilités entre des organisations Exchange 2013 et Exchange 2007

  - Configurer le partage fédéré pour l'organisation Exchange 2013. Exécutez les étapes décrites dans la rubrique [Configurer le partage fédéré](configure-federated-sharing-exchange-2013-help.md).

  - Dans l'organisation Exchange 2007, procédez comme suit :
    
    1.  **Ajouter un serveur Exchange 2010 SP2**
        
        Un serveur Exchange 2010 SP2 avec le rôle serveur d’accès au client doit être installé dans l’organisation Exchange 2007. Si vous avez d’autres serveurs Exchange 2010 existants, ces derniers devraient être mis à jour vers Exchange 2010 SP2. Pour plus d’informations sur l’installation d’Exchange 2010 au sein d’une organisation Exchange 2007, consultez l’article [Exchange 2007 - Planification de la feuille de route de mise à niveau et de coexistence](https://go.microsoft.com/fwlink/p/?linkid=268411).
    
    2.  **Configurer la délégation fédérée**
        
        Configurer la délégation fédérée pour l’organisation Exchange 2007. Sur un serveur Exchange 2010 SP2 dans l’organisation Exchange 2007, suivez les étapes décrites dans [Configurer la délégation fédérée](https://go.microsoft.com/fwlink/p/?linkid=268410).
    
    3.  **Configurer la synchronisation Active Directory**
        
        La synchronisation Active Directory doit être configurée pour tous les utilisateurs qui ont besoin de partager des informations de disponibilité entre les organisations. Vous pouvez configurer la synchronisation Active Directory manuellement ou utiliser un service de synchronisation automatique Active Directory. Pour configurer la synchronisation Active Directory, reportez-vous aux étapes ci-dessous :
        
          - **Conditions préalables**   Assurez-vous que votre organisation réponde aux conditions d'installation de la synchronisation Active Directory.
            
            Pour en savoir plus, consultez la rubrique [Préparer la synchronisation Active Directory](https://go.microsoft.com/fwlink/p/?linkid=247302)
        
          - **Plan**   Comprendre l'outil de synchronisation d'annuaires Microsoft Online Services et le plan d'installation.
            
            Pour en savoir plus, consultez la rubrique [Synchronisation Active Directory : feuille de route](http://go.microsoft.com/fwlink/p/?linkid=203007)
        
          - **Installation et configuration**   Configurer la synchronisation Active Directory entre votre organisation locale et l'organisation du service client Office 365.
            
            Pour en savoir plus, consultez la rubrique [Installer et mettre à jour l’outil de synchronisation d’annuaires Microsoft Online Services](https://go.microsoft.com/fwlink/p/?linkid=247303)
    
    4.  **Créer un espace d'adressage de disponibilité**
        
        Créer un espace d'adressage de disponibilité pour l'organisation Exchange 2013 distante qui dirige les requêtes de disponibilité des utilisateurs de boîtes aux lettres d'Exchange 2007 vers le serveur d'accès au client Exchange 2010 SP2 au sein de l'organisation Exchange 2007. Ce paramètre permet de rediriger via un proxy des demandes de disponibilité des utilisateurs provenant d'utilisateurs Exchange 2007 et destinées à des utilisateurs de l'organisation Exchange 2013 distante par le biais du serveur d'accès au client Exchange 2010 au sein de l'organisation Exchange 2007. Le serveur d'accès au client Exchange 2010 de l'organisation Exchange 2007 utilise l'approbation de fédération et la relation d'organisation pour envoyer les demandes de disponibilité au point de terminaison de disponibilité de la forêt d'organisation distante Exchange 2013.
        
        Pour configurer l'espace d'adressage de disponibilité, sur le serveur d'accès au client Exchange 2010 de l'organisation Exchange 2007, exécutez la commande suivante dans l'environnement Exchange Management Shell :
        
            Add-AvailabilityAddressSpace -AccessMethod InternalProxy -ProxyUrl https://<Exchange 2010 CAS server name>/ews/exchange.asmx -ForestName <SMTP domain of the remote Exchange organization> -UseServiceAccount $True
        
        Pour une syntaxe détaillée et des informations sur les paramètres, voir [Add-AvailabilityAddressSpace](https://go.microsoft.com/fwlink/p/?linkid=268413)

## Configurer le partage de disponibilité entre des organisations Exchange 2013 et Exchange 2003

  - Configurer le partage fédéré pour l'organisation Exchange 2013. Exécutez les étapes décrites dans la rubrique [Configurer le partage fédéré](configure-federated-sharing-exchange-2013-help.md).

  - Dans l'organisation Exchange 2003, procédez comme suit :
    
    1.  **Ajouter un serveur Exchange 2010 SP2**.
        
        Un serveur Exchange 2010 SP2 avec le rôle serveur d’accès au client doit être installé dans l’organisation Exchange 2003. Si vous avez d’autres serveurs Exchange 2010 existants, ces derniers devraient être mis à jour vers Exchange 2010 SP2. Pour plus d’informations sur l’installation d’Exchange 2010 au sein d’une organisation Exchange 2003, consultez l’article [Exchange 2003 - Planification de la feuille de route de mise à niveau et de coexistence](https://go.microsoft.com/fwlink/?linkid=268414).
        
        > [!WARNING]
		> Pour qu'un partage de disponibilités fonctionne correctement entre des organisations Exchange 2013 et Exchange 2003, le dossier public <strong>OU=EXTERNAL (FYDIBOHF25SPDLT)</strong> doit exister dans la hiérarchie des dossiers publics. Ce dossier est créé automatiquement sur le serveur de boîtes aux lettres Exchange 2010 de l'organisation Exchange 2003 seulement si vous sélectionnez l'option de création des dossiers publics comme partie intégrante de la configuration des paramètres client pour la prise en charge de Microsoft Outlook 2003 lors de l'installation de Microsoft Exchange 2010. En outre, cette option n'est accessible durant le processus d'installation que si le serveur de boîtes aux lettres Exchange 2010 est le premier serveur de boîtes aux lettres installé dans l'organisation. Si le dossier public <strong>OU=EXTERNAL (FYDIBOHF25SPDLT)</strong> n’a pas été créé lors de l’installation, vous devez le créer manuellement. Pour plus d'informations sur la création de ce dossier public, consultez la rubrique <a href="http://go.microsoft.com/fwlink/p/?linkid=3052&kbid=2555008">Comment résoudre les problèmes de disponibilité lorsque vous utilisez Exchange Federation dans l'environnement Microsoft Office 365 pour les entreprises</a>.
    
    2.  **Configurer la délégation fédérée**.
        
        Configurer la délégation fédérée pour l’organisation Exchange 2003. Sur un serveur Exchange 2010 SP2 dans l’organisation Exchange 2003, suivez les étapes décrites dans [Configurer la délégation fédérée](https://go.microsoft.com/fwlink/p/?linkid=268410).
    
    3.  **Configurer la synchronisation Active Directory**.
        
        La synchronisation Active Directory doit être configurée pour tous les utilisateurs qui ont besoin de partager des informations de disponibilité entre les organisations. Vous pouvez configurer la synchronisation Active Directory manuellement ou utiliser un service de synchronisation automatique Active Directory. Pour en savoir plus sur la synchronisation Active Directory, consultez la rubrique [Forefront Identity Management](https://go.microsoft.com/fwlink/?linkid=294645).
        
          - **Conditions préalables**   Assurez-vous que votre organisation réponde aux conditions d'installation de la synchronisation Active Directory.
            
            Pour en savoir plus, consultez la rubrique [Préparer la synchronisation Active Directory](https://go.microsoft.com/fwlink/p/?linkid=247302)
        
          - **Plan**   Comprendre l'outil de synchronisation d'annuaires Microsoft Online Services et le plan d'installation.
            
            Pour en savoir plus, consultez la rubrique [Synchronisation Active Directory : feuille de route](http://go.microsoft.com/fwlink/p/?linkid=203007)
        
          - **Installation et configuration**   Configurer la synchronisation Active Directory entre votre organisation locale et l'organisation du service client Office 365.
            
            Pour en savoir plus, consultez la rubrique [Installer et mettre à jour l’outil de synchronisation d’annuaires Microsoft Online Services](https://go.microsoft.com/fwlink/p/?linkid=247303)
    
    4.  **Configurer des dossiers publics pour le partage de disponibilités dans votre organisation Exchange 2003.**
        
        Sur un serveur Exchange 2003, procédez comme suit :
        
          - Dans le Gestionnaire système Exchange, dans l'arborescence de la console, accédez à **Groupes d'administration**\>**Premier groupe d'administration**\>**Serveurs**.
        
          - Sélectionnez votre serveur Exchange 2003, puis accédez à **Premier groupe de stockage**\>**Banque de dossiers publics**\>**Dossiers publics**\>**Schedule+ LIBRE/OCCUPÉ**.
        
          - Dans le volet Actions, sélectionnez le dossier **OU=EXTERNAL (FYDIBOHF25SPDLT)** pour le **Premier groupe d'administration**.
        
          - Cliquez avec le bouton droit sur le dossier **OU=EXTERNAL (FYDIBOHF25SPDLT)**, puis cliquez sur **Propriétés**.
        
          - Dans **Propriétés OU=EXTERNAL (FYDIBOHF25SPDLT)**, sélectionnez l'onglet **Réplication**.
        
          - Pour répliquer le dossier **OU=EXTERNAL (FYDIBOHF25SPDLT)** sur le serveur d'accès au client/de boîtes aux lettres Exchange 2010, cliquez sur **Ajouter**.
        
          - Dans **Sélectionner une banque de dossier public**, sélectionnez la **Base de données de dossiers publics** du serveur d'accès au client/de boîtes aux lettres Exchange 2010, puis cliquez sur **OK**.
            
            > [!NOTE]
            > Par défaut, Exchange utilise la planification de la réplication définie dans la base de données de dossiers publics.
        
          - Cliquez sur **OK** pour fermer **Propriétés OU=EXTERNAL (FYDIBOHF25SPDLT)** et enregistrer vos modifications.
        
          - Effectuez les mêmes étapes pour le dossier **OU=Exchange Administrative Group (FYDIBOHF23SPDLT)**.
            
            > [!WARNING]
			> Selon la taille des dossiers publics, il est possible que la réplication prenne plusieurs heures.
                    
          - Après la réplication des dossiers publics **OU=EXTERNAL (FYDIBOHF25SPDLT)** et **OU=Exchange Administrative Group (FYDIBOHF23SPDLT)** sur le serveur d'accès au client/de boîtes aux lettres Exchange 2010, vous devez supprimer les réplicas de ces dossiers publics sur le serveur Exchange 2003.
    
    5.  **Modifier le paramètre LegacyExchangeDN**
        
        Modifier le paramètre *LegacyExchangeDN* sur tous les objets à extension messagerie de l'organisation Exchange 2003 qui référencent l'organisation Exchange 2013 distante. Changer la valeur de l'unité d'organisation existante pour l'objet à extension messagerie en **Externe (FYDIBOHF25SPDLT)**. Par exemple, **LegacyExchangeDN = / o = première organisation/ou = Externe (FYDIBOHF25SPDLT) / cn = destinataires/cn = nom d'utilisateur**.
        
        Pour modifier les objets à extension messagerie dans l’organisation Exchange 2003, vous pouvez utiliser soit l’[outil ADSI Edit (Active Directory Service Interfaces Editor)](https://go.microsoft.com/fwlink/?linkid=294644), soit l’[utilitaire Microsoft Exchange Server LegacyDN](http://go.microsoft.com/fwlink/?linkid=294643).

