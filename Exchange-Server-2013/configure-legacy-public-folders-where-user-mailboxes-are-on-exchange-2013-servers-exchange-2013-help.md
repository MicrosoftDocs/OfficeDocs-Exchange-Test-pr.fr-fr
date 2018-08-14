---
title: 'Config. dossiers publics hérités avec BAL utlsr sont s/ des srv Exchange 2013'
TOCTitle: Configuration des dossiers publics hérités où les boîtes aux lettres des utilisateurs résident sur des serveurs Exchange 2013
ms:assetid: 1d5ca19e-696e-4054-a634-15dd34d952b7
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dn690134(v=EXCHG.150)
ms:contentKeyID: 62281116
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configuration des dossiers publics hérités où les boîtes aux lettres des utilisateurs résident sur des serveurs Exchange 2013

 

_**Sapplique à :** Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2017-03-27_

Comment faire pour permettre aux utilisateurs d’Exchange 2013 ou Exchange 2016 à accès Exchange 2010 ou antérieures (également connu sous le nom dossiers publics hérités) des dossiers publics.

## Ce qu’il faut savoir avant de commencer

Les utilisateurs dont les boîtes aux lettres sont sur Exchange Server 2013 ou 2016 d’Exchange Server ne pourront pas accéder aux dossiers publics hérités à partir d’Outlook Web App, Outlook sur le web ou Outlook pour Mac. Les étapes décrites dans cet article fonctionnent pour Exchange 2013 et 2016 d’Exchange.

> [!NOTE]  
> Les utilisateurs d’Outlook 2016 pour Mac peuvent accéder aux dossiers publics hérités après avoir suivi les étapes décrites dans cet article. Si les clients de votre organisation utilisent Outlook 2016 pour Mac, assurez-vous qu’ils ont installé la mise à jour d’avril 2016. Dans le cas contraire, ces utilisateurs ne seront pas en mesure d’accéder aux dossiers publics dans une coexistence ou une topologie hybride. Pour plus d’informations, voir <a href="accessing-public-folders-with-outlook-2016-for-mac-exchange-2013-help.md">Accès aux dossiers publics avec Outlook 2016 pour Mac</a>.


## Étape 1 : rendre les dossiers publics Exchange 2010 détectables

1.  Si vos dossiers publics sont sur des serveurs Exchange 2010 ou version ultérieure, vous devez installer le rôle serveur d'accès au client sur tous les serveurs de boîtes aux lettres disposant d'une base de données de dossiers publics. Cela permet l'exécution du service RpcClientAccess de Microsoft Exchange qui permet à tous les clients d'accéder aux dossiers publics. Le rôle d’accès au client n’étant pas requis pour les serveurs de dossiers publics Exchange 2007, cette étape n’est pas nécessaire. Pour plus d'informations, consultez la rubrique [Installer Exchange Server 2010](install-exchange-2013-using-the-setup-wizard-exchange-2013-help.md).
    
    > [!NOTE]  
    > Il n’est pas utile que ce serveur prenne part à l’équilibrage de la charge d’accès au client. Pour plus d'informations, consultez la rubrique <a href="https://technet.microsoft.com/fr-fr/library/ff625247(v=exchg.141).aspx">Présentation de l'équilibrage de la charge dans Exchange 2010</a>.


2.  Créez une base de données de boîtes aux lettres vide sur chaque serveur de dossiers publics.
    
    Pour Exchange 2010, exécutez la commande suivante : Cette commande exclut la base de données de boîtes aux lettres du programme d’équilibrage de la charge pour l’ajout de boîtes aux lettres. Cela évite l'ajout automatique de nouvelles boîtes aux lettres à cette base de données.
    
        New-MailboxDatabase -Server <PFServerName_with_CASRole> -Name <NewMDBforPFs> -IsExcludedFromProvisioning $true 
    
    Pour Exchange 2007, exécutez la commande suivante :
    
        New-MailboxDatabase -StorageGroup "<PFServerName>\StorageGroup>" -Name <NewMDBforPFs>
    
    > [!NOTE]  
    > Nous vous recommandons d’ajouter à cette base de données uniquement la boîte aux lettres proxy que vous allez créer à l’étape 3. Aucune autre boîte aux lettres ne devrait être créée dans cette base de données de boîtes aux lettres.


3.  Créez une boîte aux lettres proxy à l'intérieur de la nouvelle base de données de boîtes aux lettres, puis masquez-la dans le carnet d'adresses. Le SMTP de cette boîte aux lettres sera renvoyé par la découverte automatique comme SMTP *DefaultPublicFolderMailbox*, de sorte qu'en résolvant ce SMTP, le client pourrait atteindre le serveur Exchange hérité pour l'accès aux dossiers publics.
    ```
        New-Mailbox -Name <PFMailbox1> -Database <NewMDBforPFs> 
    ```
    ```
        Set-Mailbox -Identity <PFMailbox1> -HiddenFromAddressListsEnabled $true
    ```

4.  Pour Exchange 2010, activez la découverte automatique de façon à ce qu’elle renvoie les boîtes aux lettres de dossiers publics proxy. Cette étape n’est pas nécessaire pour Exchange 2007.
    
        Set-MailboxDatabase <NewMDBforPFs> -RPCClientAccessServer <PFServerName_with_CASRole>

5.  Répétez les étapes précédentes pour chaque serveur de dossiers publics au sein de votre organisation.

## Étape 2 : configurer des boîtes aux lettres d’utilisateurs pour accéder aux dossiers publics hérités

La dernière étape de cette procédure consiste à configurer les boîtes aux lettres des utilisateurs afin d'autoriser l'accès aux dossiers publics locaux hérités.

Autorisez les utilisateurs sur site d’Exchange Server 2013 à accéder aux dossiers publics hérités. Vous allez pointer vers toutes les boîtes aux lettres de dossiers publics proxy que vous avez créées à l'[Step 2: Make remote public folders discoverable](configure-legacy-on-premises-public-folders-for-a-hybrid-deployment-exchange-2013-help.md). Exécutez la commande suivante à partir d’un serveur Exchange 2013 disposant de la mise à jour cumulative 5 ou d’une mise à jour ultérieure.

    Set-OrganizationConfig -PublicFoldersEnabled Remote -RemotePublicFolderMailboxes ProxyMailbox1,ProxyMailbox2,ProxyMailbox3

> [!NOTE]  
> Pour voir les modifications, vous devez attendre que la synchronisation ActiveDirectory soit terminée. Ce processus peut prendre plusieurs heures.


## Comment savoir si cela a fonctionné ?

Connectez-vous à Outlook pour un utilisateur dont la boîte aux lettres se trouve sur un serveur Exchange Server 2013 avec mise à jour cumulative 5 ou ultérieur, et effectuez les tests de dossier public suivants :

1.  Assurez-vous que le client Outlook est en cours d'exécution.

2.  Maintenez enfoncée la touche CTRL, puis cliquez avec le bouton droit sur l’icône Outlook dans la zone de notification sur le côté droit de la barre des tâches de Windows.

3.  Sélectionnez **Tester la configuration automatique du courrier électronique...**

4.  Assurez-vous que l’outil Tester la configuration automatique du courrier électronique renvoie les informations suivantes dans l’onglet XML :
    
      - \<PublicFolderInformation\>
    
      - \<SmtpAddress\>\<Adresse SMTP pour la boîte aux lettres de dossier public\</SmtpAddress\>
    
      - \</PublicFolderInformation\>

5.  Dans le client Outlook, effectuez les tâches suivantes :
    
      - Affichez la hiérarchie de dossiers publics.
    
      - Vérifiez les autorisations.
    
      - Créez et supprimez des dossiers publics.
    
      - Publiez ou effacez du contenu dans un dossier public.

