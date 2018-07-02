---
title: 'Déléguer l’installation d’un serveur Exchange 2013: Exchange 2013 Help'
TOCTitle: Déléguer l’installation d’un serveur Exchange 2013
ms:assetid: f2fc8680-0c7c-4a29-b8f5-d77404fec280
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb201741(v=EXCHG.150)
ms:contentKeyID: 62615206
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Déléguer l’installation d’un serveur Exchange 2013

 

_**Sapplique à :** Exchange Online, Exchange Server, Exchange Server 2013_

_**Dernière rubrique modifiée :** 2014-07-31_

Exchange Server 2013 vous permet de déléguer l’installation des serveurs Exchange à des personnes qui ne sont pas membres du groupe de rôles Gestion de l’organisation Exchange 2013. Ceci est souvent utile dans les grandes entreprises où les personnes qui installent et configurent les serveurs ne sont pas celles qui gèrent les services, comme Exchange. Si vous voulez déléguer l’installation de serveurs, cette rubrique devrait vous intéresser.

Normalement, les personnes qui procèdent à l’installation d’Exchange doivent être des membres du groupe de rôles [Gestion de l’organisation](organization-management-exchange-2013-help.md). En effet, lors de l’installation d’Exchange, des modifications sont apportées à Active Directory, et seuls les administrateurs Exchange, qui sont membres du groupe de rôles Gestion de l’organisation, peuvent effectuer ces changements. La liste suivante répertorie les modifications apportées :

  - Un objet serveur est créé dans la partition de configuration **CN=Servers,CN=Exchange Administrative Group (FYDIBOHF23SPDLT),CN=Administrative Groups,CN=\<Organization Name\>,CN=Microsoft Exchange,CN=Services,CN=Configuration,DC=\<Root Domain\>**.

  - Les entrées de contrôle d’accès (ACE) suivantes sont ajoutées à l’objet serveur dans la partition de configuration du groupe de rôles Installation déléguée :
    
      - contrôle total sur l’objet serveur et ses objets enfants ;
    
      - entrée de contrôle d’accès refusée pour le droit étendu Envoyer en tant que ;
    
      - entrée de contrôle d’accès refusée pour le droit étendu Recevoir en tant que.
    
      - autorisations CreateChild et DeleteChild refusées pour les objets de banque de dossiers publics Exchange.
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Les dossiers publics sont administrés au niveau de l’organisation. Par conséquent, la création et la suppression des banques de dossiers publics est limitée aux administrateurs Exchange.</td>
    </tr>
    </tbody>
    </table>


  - Le compte d’ordinateur Active Directory du serveur est ajouté au groupe de serveurs Exchange.

  - Le serveur est ajouté en tant que serveur configuré dans le Centre d’administration Exchange.

Dans les grandes entreprises, les personnes qui installent et configurent les nouveaux serveurs sont rarement des administrateurs Exchange. Pour leur permettre d’installer Exchange, un administrateur Exchange peut *configurer* le serveur dans Active Directory. Lorsqu’un serveur est configuré, toutes les modifications nécessaires pour le fonctionnement du nouveau serveur Exchange sont effectuées sur Active Directory séparément de l’installation réelle de Exchange sur un ordinateur. Un administrateur Exchange peut configurer un nouveau serveur dans Active Directory plusieurs heures, voire plusieurs jours avant l’installation d’Exchange sur le nouvel ordinateur. Une fois qu’un serveur a été configuré, la personne qui procède à l’installation doit seulement appartenir au groupe de rôles [Installation déléguée](delegated-setup-exchange-2013-help.md) pour installer Exchange. Le groupe de rôles Installation déléguée autorise uniquement les membres à installer les serveurs configurés.

Gardez à l’esprit les éléments suivants lorsque vous envisagez l’installation déléguée :

  - Au moins un serveur Exchange 2013 doit déjà être installé pour que vous puissiez déléguer l’installation de serveurs supplémentaires. La personne qui installe le premier serveur doit être un administrateur Exchange. Pour plus d’informations, voir [Liste de contrôle : Effectuer une nouvelle installation d’Exchange 2013](checklist-perform-a-new-installation-of-exchange-2013-exchange-2013-help.md).

  - Un utilisateur délégué ne peut pas désinstaller un serveur Exchange. Pour désinstaller un serveur Exchange, vous devez être un administrateur Exchange.

## Configuration d’un serveur Exchange 2013

Pour configurer un serveur Exchange, vous devez utiliser l’installation par ligne de commande Exchange 2013. Si vous ne connaissez pas l’invite de commandes Windows, ne vous inquiétez pas. Cette rubrique vous indique la marche à suivre. Avant de commencer, voici quelques éléments que vous devez garder à l’esprit :

  - Vous devez être membre du groupe de rôles Gestion de l’organisation pour configurer un serveur.

  - Vous devez disposer de la dernière version d’Exchange 2013. Vous pouvez obtenir le lien de téléchargement dans la rubrique [Mises à jour pour Exchange 2013](updates-for-exchange-2013-exchange-2013-help.md).

La commande à utiliser pour configurer le serveur dépend de si vous exécutez l’installation à partir de l’ordinateur que vous configurez ou si vous l’exécutez sur un autre ordinateur. Dans les étapes suivantes, choisissez la commande correspondant à l’emplacement où vous exécutez l’installation :

1.  Appuyez sur les touches Windows+R pour ouvrir la fenêtre **Exécuter**.

2.  Dans **Ouvrir**, saisissez **cmd.exe**, puis appuyez sur Entrée pour ouvrir une **invite de commandes Windows**.

3.  Modifiez les répertoires à l’emplacement où vous avez téléchargé et développé les fichiers d’installation Exchange 2013. Si ces fichiers se trouvent dans `C:\Downloads\Exchange 2013`, utilisez la commande suivante.
    
        CD "C:\Downloads\Exchange 2013"

4.  Choisissez la commande qui correspond à l’emplacement où vous exécutez l’installation :
    
      - **Si vous procédez à l’installation sur l’ordinateur en cours de configuration**, exécutez la commande suivante :
        
            Setup.exe /NewProvisionedServer /IAcceptExchangeServerLicenseTerms
    
      - **Si vous procédez à l’installation sur un autre ordinateur**, exécutez la commande suivante :
        
            Setup.exe /NewProvisionedServer:<ComputerName> /IAcceptExchangeServerLicenseTerms

5.  Après avoir configuré le serveur, vérifiez que vous avez ajouté les utilisateurs qui doivent pouvoir installer Exchange sur les serveurs configurés au groupe de rôles Installation déléguée. Pour savoir comment ajouter des utilisateurs à un groupe de rôles, voir [Add members to a role group](manage-role-group-members-exchange-2013-help.md).

Lorsque vous avez terminé ces étapes, l’ordinateur est prêt pour l’installation d’Exchange. Exchange 2013 peut être installé sur un serveur configuré à l’aide des étapes décrites dans la rubrique [Installer Exchange 2013 à l’aide de l’Assistant Installation](install-exchange-2013-using-the-setup-wizard-exchange-2013-help.md).

## Comment savoir si cela a fonctionné ?

Pour vous assurer que le serveur a été configuré correctement pour Exchange, procédez comme suit :

1.  Accédez à **Démarrer** \> **Outils d’administration**, puis ouvrez **Utilisateurs et ordinateurs Active Directory**.

2.  Sélectionnez **Groupes de sécurité Microsoft Exchange**, double-cliquez sur **Serveurs Exchange**, puis affichez l’onglet **Membres**.

3.  Dans l’onglet **Membres**, vérifiez si le serveur que vous venez de configurer est répertorié en tant que membre du groupe de sécurité.

Si votre serveur fait partie du groupe de sécurité des serveurs Exchange, il a été configuré correctement. Un membre du groupe de rôles Installation déléguée peut maintenant installer Exchange sur ce serveur.

Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), et [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

Avez-vous trouvé ce que vous cherchez ? Veuillez prendre une minute pour [nous envoyer votre avis à l'adresse](mailto:exsetuphelpfeedback@microsoft.com?subject=exchange%202013%20setup%20help%20feedback) au sujet des informations que vous souhaitiez y trouver.

