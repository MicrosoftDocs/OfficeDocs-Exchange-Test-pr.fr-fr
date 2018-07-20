---
title: 'Installer Exchange 2013 à l’aide de l’Assistant Installation: Exchange 2013 Help'
TOCTitle: Installer Exchange 2013 à l’aide de l’Assistant Installation
ms:assetid: da690d47-3384-4430-a69e-0cd4d3bf80a7
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb124778(v=EXCHG.150)
ms:contentKeyID: 50479360
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.ExSetupUI.SetupWizardForm.IntroductionPage
ms.translationtype: HT
---

# Installer Exchange 2013 à l’aide de l’Assistant Installation

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2014-06-19_

Cette rubrique explique comment utiliser l’Assistant Installation de Microsoft Exchange Server 2013 pour installer les rôles de boîte aux lettres et d’accès au client Exchange 2013 sur un ordinateur. Pour de plus amples informations sur la planification et le déploiement d'Exchange 2013, consultez la rubrique [Planification et déploiement](planning-and-deployment-for-exchange-2013-installation-instructions.md).

Si vous souhaitez installer le rôle de transport Edge Exchange 2013 sur un ordinateur, voir [Installer le rôle de transport Edge d’Exchange 2013 à l’aide de l’Assistant Installation](install-the-exchange-2013-edge-transport-role-using-the-setup-wizard-exchange-2013-help.md). Le rôle de transport Edge ne peut pas être installé sur le même ordinateur que les rôles serveur de boîtes aux lettres ou d’accès au client.

> [!TIP]  
> Avez-vous déjà entendu parler de l’Assistant de déploiement Exchange Server ? Il s’agit d’un outil en ligne gratuit qui vous permet de déployer rapidement Exchange 2013 dans votre organisation en répondant à quelques questions et en créant une liste de contrôle de déploiement personnalisée. Pour en savoir plus, consultez la page <a href="exchange-server-deployment-assistant-exchange-2013-help.md">Assistant de déploiement Exchange Server</a>.


> [!NOTE]  
> Après avoir installé des rôles serveur sur un ordinateur exécutant Exchange 2013, il n'est plus possible d'utiliser l'Assistant Installation d'Exchange 2013 pour ajouter des rôles serveur à cet ordinateur. Pour ajouter des rôles serveur supplémentaires à un ordinateur, vous devez utiliser la fonctionnalité Ajout/Suppression de programmes du Panneau de configuration ou la commande Setup.exe depuis une fenêtre d'invite de commandes.


Pour plus d'informations sur les tâches postérieures à l'installation, consultez la rubrique [Tâches consécutives à l’installation d’Exchange 2013](exchange-2013-post-installation-tasks-exchange-2013-help.md).

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : 60 minutes

  - Assurez-vous que vous avez lu les notes de publication avant d'installer Exchange 2013. Pour plus d'informations, consultez la rubrique [Notes de publication relatives à Exchange 2013](release-notes-for-exchange-2013-exchange-2013-help.md).

  - Chaque organisation demande au minimum un serveur d'accès au client et un serveur de boîtes aux lettres dans la forêt Active Directory. De plus, chaque site Active Directory qui contient un serveur de boîtes aux lettres doit également contenir au moins un serveur d'accès au client. Si vous séparez les rôles de vos serveurs, nous vous recommandons d'installer le serveur ayant le rôle de serveur de boîtes aux lettres en premier.

  - L’ordinateur sur lequel vous installez Exchange 2013 doit exécuter un système d’exploitation pris en charge (tel que Windows Server 2008 R2 avec le Service Pack 1 (SP1) ou Windows Server 2012), disposer de suffisamment d’espace disque, être membre d’un domaine Active Directory et respecter d’autres conditions préalables. Pour plus d'informations sur la configuration système requise, consultez la rubrique [Configuration requise pour Exchange 2013](exchange-2013-system-requirements-exchange-2013-help.md).

  - Pour exécuter l’installation d’Exchange 2013, vous devez installer Microsoft .NET Framework 4.5, Windows Management Framework 3.0 et les autres logiciels requis. Pour connaître les conditions préalables pour tous les rôles de serveur, consultez la rubrique [Conditions préalables pour Exchange 2013](exchange-2013-prerequisites-exchange-2013-help.md).

  - Vous devez vous assurer qu'une appartenance au groupe Administrateurs de schéma a été déléguée au compte utilisé si vous n'avez pas déjà préparé le schéma Active Directory. Si vous installez le premier serveur Exchange 2013 de l'organisation, vous devez utiliser un compte appartenant au groupe Administrateurs d'entreprise. Si vous avez déjà préparé le schéma mais que vous n'installez pas le premier serveur Exchange 2013 de l'organisation, vous devez utiliser un compte appartenant au groupe de rôles Gestion de l'organisation Exchange 2013.
    
    Les administrateurs membres du groupe de rôles Installation déléguée peuvent déployer des serveurs Exchange 2013 qui ont été précédemment mis en service par un membre du groupe de rôles de gestion Gestion de l'organisation.

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!CAUTION]  
> Après avoir installé Exchange sur un serveur, vous ne devez pas modifier le nom du serveur. La modification du nom d’un serveur après avoir installé un rôle de serveur Exchange n’est pas prise en charge.


## Installer Exchange Server 2013

Si vous installez le premier serveur Exchange 2013 de l’organisation et n’avez pas suivi les étapes de préparation Active Directory, vous devez utiliser un compte appartenant au groupe Administrateurs de l’entreprise. Si vous n’avez pas préparé le schéma Active Directory en amont, le compte doit également être membre du groupe Administrateurs du schéma. Pour plus d’informations sur la préparation d’Active Directory pour Exchange 2013, voir [Préparation d’Active Directory et des domaines](prepare-active-directory-and-domains-exchange-2013-help.md). Si vous avez déjà réalisé les étapes de préparation Active Directory et de schéma, vous devez utiliser un compte appartenant au groupe de rôles de gestion Installation déléguée ou au groupe de rôles Gestion de l’organisation.

> [!NOTE]  
> Pour télécharger la dernière version d’Exchange 2013, voir <a href="updates-for-exchange-2013-exchange-2013-help.md">Mises à jour pour Exchange 2013</a>


1.  Connectez-vous à l'ordinateur sur lequel vous voulez installer Exchange 2013.

2.  Accédez à l'emplacement réseau des fichiers d'installation d'Exchange 2013.

3.  Lancez le Programme d'installation de Exchange 2013 en double-cliquant sur `Setup.exe`
    
    > [!NOTE]  
    > Si le contrôle d’accès d’utilisateur est activé, vous devez cliquer avec le bouton droit de la souris sur <code>Setup.exe</code> et sélectionner <strong>Exécuter en tant qu’administrateur</strong>.


4.  dans la page **Vérifier les mises à jour ?**, indiquez si vous souhaitez que le Programme d'installation se connecte à Internet et télécharge les mises à jour du produit et de la sécurité pour Exchange 2013. Si vous sélectionnez **Se connecter à Internet et vérifier les mises à jour**, le Programme d'installation téléchargera les mises à jour et les appliquera avant de continuer. Si vous sélectionnez **Ne pas vérifier les mises à jour tout de suite**, vous pouvez télécharger et installer les mises à jour manuellement plus tard. Nous vous recommandons de télécharger et d'installer les mises à jour maintenant. Cliquez sur **Suivant** pour continuer.

5.  La page **Introduction** lance l'installation d'Exchange dans votre organisation. Il vous guide à travers l'installation. Plusieurs liens vers un contenu de déploiement utile sont répertoriés. nous vous recommandons de cliquer sur ces liens avant de poursuivre l'installation. Cliquez sur **Suivant** pour continuer.

6.  Dans la page **Contrat de licence**, lisez les termes du contrat de licence. Si vous acceptez les termes, sélectionnez **J'accepte les termes du contrat de licence**, puis cliquez sur **Suivant**.

7.  dans la page **Paramètres recommandés**, indiquez si vous souhaitez utiliser les paramètres recommandés. Si vous sélectionnez l’option **Utiliser les paramètres recommandés**, Exchange enverra automatiquement à Microsoft des rapports d’erreurs et des informations sur votre matériel informatique et l’utilisation d’Exchange. Si vous sélectionnez l'option **Ne pas utiliser les paramètres recommandés**, ces paramètres restent désactivés. Toutefois, vous pouvez les activer à tout moment une fois l'installation terminée. Pour plus d'informations sur ces paramètres et l'utilisation des informations envoyées à Microsoft, cliquez sur **?**.

8.  dans la page **Sélection du rôle de serveur**, indiquez si vous souhaitez installer le **rôle Boîte aux lettres**, le **rôle Accès au client**, les deux rôles ou uniquement les **outils de gestion** sur cet ordinateur. Vous pourrez ajouter des rôles serveur supplémentaires ultérieurement si vous décidez de ne pas les installer au cours de cette installation. Au moins une règle Boîte aux lettres et un rôle serveur d'accès au client doivent être installés dans une organisation. Ils peuvent être installés sur un même ordinateur ou sur des ordinateurs distincts. Les outils de gestion sont installés automatiquement si vous installez un rôle serveur.
    
    Sélectionnez **Installer automatiquement les rôles et les fonctionnalités Windows Server requis pour Exchange Server** pour que l’Assistant Installation installe les composants Windows requis. Il peut s’avérer nécessaire de redémarrer l’ordinateur pour terminer l’installation de certaines fonctionnalités Windows. Si vous ne sélectionnez pas cette option, vous devez installer les fonctionnalités Windows manuellement.
    
    > [!NOTE]
    > Cette option installe uniquement les fonctionnalités Windows requises par Exchange. Vous devez installer manuellement les autres composants requis. Pour plus d'informations, consultez la rubrique <a href="exchange-2013-prerequisites-exchange-2013-help.md">Conditions préalables pour Exchange 2013</a>.
    
    Cliquez sur **Suivant** pour continuer.

9.  Sur la page **Espace et emplacement d’installation**, acceptez l’emplacement d’installation par défaut ou cliquez sur **Parcourir** pour choisir un nouvel emplacement. Assurez-vous que l’emplacement sur lequel vous souhaitez installer Exchange dispose d’un espace disque suffisant. Cliquez sur **Suivant** pour continuer.

10. S'il s'agit du premier serveur Exchange de votre organisation, dans la page **Organisation Exchange**, entrez le nom de votre organisation Exchange. Un nom d'organisation Exchange ne peut contenir que les caractères suivants :
    
      - A à Z
    
      - a à z
    
      - 0 à 9
    
      - Espace (pas au début ni à la fin)
    
      - Trait d’union ou tiret
        
        > [!NOTE]
        > Un nom d'organisation ne doit pas contenir plus de 64 caractères. Le nom de l'organisation ne peut pas être vide.
    
    Si vous souhaitez utiliser le modèle d’autorisations partagées Active Directory, sélectionnez l’option **Appliquer le modèle de sécurité des autorisations partagées Active Directory à l’organisation Exchange**.
    
    > [!CAUTION]
    > La plupart des organisations n’ont pas besoin d’appliquer le modèle d’autorisations partagées Active Directory. Si vous devez séparer la gestion des principaux de sécurité Active Directory et la configuration Exchange, les autorisations partagées du contrôle d’accès basé sur les rôles (RBAC) peuvent vous convenir. Pour plus d'informations, cliquez sur <strong>?</strong>.
    
    Cliquez sur **Suivant** pour continuer.

11. Si vous installez le rôle Boîte aux lettres, dans la page **Paramètres de la protection anti-programme malveillant**, indiquez si vous souhaitez activer ou désactiver la recherche de programmes malveillants. Si vous désactivez la recherche de programmes malveillants, elle peut être activée à l'avenir. Cliquez sur **Suivant** pour continuer.

12. 
    
    Dans la page **Tests de préparation**, affichez l'état pour déterminer si les contrôles préalables de l'organisation et du rôle serveur ont été accomplis avec succès. Si ce n'est pas le cas, vous devez résoudre les erreurs signalées avant d'installer Exchange 2013. Vous n'avez pas besoin de quitter le programme d'installation pour résoudre certaines de ces erreurs. Une fois qu'une erreur signalée a été résolue, cliquez sur **Précédent**, puis sur **Suivant** pour exécuter à nouveau la vérification préalable. Veillez également à vérifier tous les avertissements signalés. Si tous les contrôles de préparation sont probants, cliquez sur **Suivant** pour installer Exchange 2013.

13. 
    
    Dans la page **Achèvement**, cliquez sur **Terminer**.

14. Redémarrez l'ordinateur une fois l'installation d'Exchange 2013 terminé.

15. Terminez votre déploiement en exécutant les tâches fournies dans [Tâches consécutives à l’installation d’Exchange 2013](exchange-2013-post-installation-tasks-exchange-2013-help.md).

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez installé Exchange 2013 avec succès, consultez [Vérifier une installation d’Exchange 2013](verify-an-exchange-2013-installation-exchange-2013-help.md).

Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), et [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

Avez-vous trouvé ce que vous cherchez ? Veuillez prendre une minute pour [nous envoyer votre avis à l'adresse](mailto:exsetuphelpfeedback@microsoft.com?subject=exchange%202013%20setup%20help%20feedback) au sujet des informations que vous souhaitiez y trouver.

