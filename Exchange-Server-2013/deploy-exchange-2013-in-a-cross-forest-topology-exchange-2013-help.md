---
title: 'Déploiement d’Exchange 2013 dans une topologie inter-forêts: Exchange 2013 Help'
TOCTitle: Déploiement d’Exchange 2013 dans une topologie inter-forêts
ms:assetid: 65be650f-d435-4f60-9ff0-5cb88a726abb
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Aa998597(v=EXCHG.150)
ms:contentKeyID: 51407197
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Déploiement d’Exchange 2013 dans une topologie inter-forêts

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2016-12-09_

Cette rubrique décrit la procédure de déploiement d'Exchange 2013 dans une topologie inter-forêts avec Microsoft Forefront Identity Manager 2010 R2 SP1. Pour déployer Exchange 2013 dans une topologie inter-forêts, vous devez commencer par installer Exchange 2013 dans chaque forêt, puis connecter les forêts de sorte que les utilisateurs puissent voir les données d'adresse et de disponibilité des forêts.

La figure suivante illustre la synchronisation utilisateur entre deux forêts Exchange 2013.

**Exemple de synchronisation inter-forêts Exchange 2013**

![Exemple de forêts Exchange 2010 multiples](images/Aa998597.df0ba5dd-cb96-4542-98bd-2a425defe317(EXCHG.150).gif "Exemple de forêts Exchange 2010 multiples")

Cette rubrique ne décrit *pas* la procédure de déploiement d'Exchange 2013 dans une topologie de forêt (ou forêt de ressources) Exchange dédiée. Pour plus d'informations sur le déploiement d'Exchange 2013 dans une topologie de forêt de ressources, consultez la rubrique [Déploiement d’Exchange 2013 dans une topologie de forêt ressource Exchange](deploy-exchange-2013-in-an-exchange-resource-forest-topology-exchange-2013-help.md).

## Ce qu'il faut savoir avant de commencer

Pour effectuer la procédure suivante dans Exchange 2013, vérifiez ce qui suit :

  - Vous avez correctement configuré un DNS (Domain Name System) pour la résolution de noms dans les forêts au sein de votre organisation. Pour vérifier que le DNS est configuré correctement, utilisez l'outil Ping pour tester la connectivité de chaque forêt à partir des autres forêts de votre organisation et à partir du serveur sur lequel vous voulez exécuter l'Agent GALSync.

  - L'agent de gestion GALSync communique avec la forêt Exchange 2013 par l'intermédiaire de Windows PowerShell V2.0 RTM. Vérifiez que Windows PowerShell v1.0 n'est pas installé sur cet ordinateur en accédant au Panneau de configuration, puis en cliquant sur Programmes et fonctionnalités.

  - Assurez-vous que l'administration à distance de Windows n'a pas été installée par Windows Update.

  - Installez Windows PowerShell et Administration à distance de Windows. Pour en savoir plus, consultez l'article 968930 de la Base de connaissances Microsoft, [Package de Windows Management Framework Core (Windows PowerShell 2.0 et WinRM 2.0)](http://go.microsoft.com/fwlink/p/?linkid=3052&kbid=968930).

  - Téléchargez Forefront Identity Manager 2010 R2 SP1. Consultez la page [Téléchargement de Microsoft Forefront Identity Manager 2010 R2 SP1](https://go.microsoft.com/fwlink/p/?linkid=279868).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.


## Déploiement d'Exchange 2013 dans une topologie inter-forêts avec Forefront Identity Manager 2010 R2 SP1

1.  Dans chaque forêt, installez Exchange 2013 séparément. Pour installer Exchange 2013, procédez comme vous le feriez pour l'installation d'Exchange 2013 dans une topologie de forêt unique. Pour obtenir la procédure détaillée, consultez l'une des rubriques suivantes :
    
      - [Déployer une nouvelle installation d’Exchange 2013](deploy-a-new-installation-of-exchange-2013-exchange-2013-help.md)
    
      - [Installer Exchange 2013 à l’aide de l’Assistant Installation](install-exchange-2013-using-the-setup-wizard-exchange-2013-help.md)
        
        > [!NOTE]
        > Cette rubrique est basée sur l'hypothèse que vous n'avez pas de topologie Exchange 2007 ou Exchange 2010 existante. Si vous avez une topologie Exchange existante et souhaitez procéder à une mise à niveau, consultez la rubrique <a href="upgrade-from-exchange-2010-to-exchange-2013-exchange-2013-help.md">Mise à niveau d'Exchange 2010 vers Exchange 2013</a> ou <a href="upgrade-from-exchange-2007-to-exchange-2013-exchange-2013-help.md">Mise à niveau d'Exchange 2007 vers Exchange 2013</a>.


2.  Dans chaque forêt, utilisez Utilisateurs et ordinateurs Active Directory pour créer un conteneur dans lequel Forefront Identity Manager 2010 R2 SP1 créera des contacts pour chaque boîte aux lettres à partir de l'autre forêt. Nous vous recommandons de nommer ce conteneur **FromFIM**. Pour créer le conteneur, sélectionnez le domaine dans lequel vous voulez le créer, cliquez avec le bouton droit sur le domaine, sélectionnez **Nouveau** \> **Unité d'organisation**. Dans **Nouvel objet - Unité d'organisation**, entrez **FromFIM**, puis cliquez sur **OK**.

3.  Créez un agent de gestion GALSync pour chaque forêt à l'aide de Forefront Identify Manager. Cela vous permet de synchroniser les utilisateurs de chaque forêt et de créer une LAG commune. Pour obtenir la procédure détaillée, consultez les ressources suivantes :
    
      - [Configuration de la synchronisation de liste d'adresses globale (LAG) avec Forefront Identity Manager (FIM) 2010](https://go.microsoft.com/fwlink/p/?linkid=279869)
    
      - [Utilisation des agents de gestion](https://go.microsoft.com/fwlink/p/?linkid=279870)
    
      - [Plan de la documentation sur Forefront Identity Manager 2010 R2](https://go.microsoft.com/fwlink/p/?linkid=279871)
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ159813.important(EXCHG.150).gif" title="Important" alt="Important" />Important :</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Bien que les ressources concernent Exchange 2010, FIM 2010 R2 SP1 prend en charge Exchange 2013. Assurez-vous de configurer les <strong>extensions</strong> dans FIM 2010 R2 SP1 pour Exchange 2013.</td>
    </tr>
    </tbody>
    </table>
    
    1.  Dans la page **Configuration des extensions**, sous **Configurer le(s) nom(s) de partition affiché(s)**, en regard de **Configurer pour**, sélectionnez **Exchange 2013**. Le champ **URI Exchange 2013 RPS** apparaît. Entrez l'URI d'un serveur d'accès au client Exchange 2013 pour vérifier le bon fonctionnement de la connexion Remote PowerShell. L'**URI Remote PowerShell d'Exchange 2013** doit être au format suivant : http://CAS\_Server\_FQDN/Powershell. Cliquez sur **OK**.
        
        > [!NOTE]
		> Vérifiez que les informations d'identification de l'administrateur, utilisées pour la connexion à la forêt d'Exchange 2013, permettent également les connexions Remote PowerShell à cette forêt.<br />
        > La figure suivante montre comment sélectionner la configuration pour Exchange 2013.
        
        **Configuration de l'agent de gestion GalSync pour Exchange 2013**
        
        ![Approvisionnement de l’Agent de gestion d’Exchange 2010](images/Aa998597.8f403cda-e5e4-4edf-887f-c1ed46cee3f5(EXCHG.150).gif "Approvisionnement de l’Agent de gestion d’Exchange 2010")  

4.  Créez un connecteur d'envoi SMTP dans chaque forêt. Pour obtenir la procédure détaillée, consultez la rubrique [Configuration d'un connecteur d'envoi inter-forêts](configure-a-cross-forest-send-connector-exchange-2013-help.md).

5.  Dans chaque forêt, activez le service de disponibilité de façon à ce que les utilisateurs de chaque forêt puissent consulter les données de disponibilité sur les utilisateurs dans l'autre forêt. Pour plus d'informations, consultez la rubrique [Service de disponibilité dans Exchange 2013](availability-service-in-exchange-2013-exchange-2013-help.md).

6.  Si vous souhaitez relayer des messages via une forêt dans votre organisation, vous devez configurer un domaine dans cette forêt comme domaine faisant autorité. Pour obtenir la procédure détaillée, consultez la rubrique [Configuration d’Exchange de manière à accepter des messages électroniques pour plusieurs domaines faisant autorité](configure-exchange-to-accept-mail-for-multiple-authoritative-domains-exchange-2013-help.md).

