---
title: 'Installation des outils de gestion Exchange 2013: Exchange 2013 Help'
TOCTitle: Installation des outils de gestion Exchange 2013
ms:assetid: 71fcbe4c-783b-4f77-aabb-a21aa7a4ef23
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb232090(v=EXCHG.150)
ms:contentKeyID: 50555414
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Installation des outils de gestion Exchange 2013

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2013-01-28_

Les outils de gestion de Microsoft Exchange Server 2013 vous permettent de configurer et de gérer votre organisation Exchange à distance. Ils comprennent l'environnement de ligne de commande Exchange Management Shell et la boîte à outils Exchange. Cette rubrique explique comment utiliser Setup.exe ou l'installation sans assistance pour installer Exchange 2013 Management Tools.

> [!NOTE]
> Il n'est pas nécessaire d'exécuter cette procédure pour utiliser le Centre d'administration Exchange (CAE) à distance. Le Centre d'administration Exchange (CAE) est une console basée sur le web qui est hébergée sur des ordinateurs exécutant le rôle serveur d'accès au client d'Exchange 2013. Pour plus d'informations sur le CAE à distance, consultez la rubrique <a href="exchange-admin-center-in-exchange-2013-exchange-2013-help.md">Centre d’administration Exchange dans Exchange 2013</a>.


Pour des informations supplémentaires sur la gestion d'Exchange 2013, consultez les rubriques [Centre d’administration Exchange dans Exchange 2013](exchange-admin-center-in-exchange-2013-exchange-2013-help.md) et [Utilisation de PowerShell avec Exchange 2013 (Exchange Management Shell)](https://technet.microsoft.com/fr-fr/library/bb123778\(v=exchg.150\)).

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : 10 minutes

  - Assurez-vous que vous avez lu les notes de publication avant d'installer Exchange 2013. Pour plus d'informations, consultez la rubrique [Notes de publication relatives à Exchange 2013](release-notes-for-exchange-2013-exchange-2013-help.md).

  - L'ordinateur sur lequel vous installez les outils de gestion doit exécuter un système d'exploitation pris en charge (comme Windows Server 2012 ou Windows 8), disposer d'un espace disque suffisant, être membre d'un domaine Active Directory et satisfaire d'autres exigences. Pour plus d'informations sur la configuration système requise, consultez la rubrique [Configuration requise pour Exchange 2013](exchange-2013-system-requirements-exchange-2013-help.md).

  - Pour exécuter le programme d'installation d'Exchange 2013, vous devez installer Microsoft .NET Framework 4.5, Windows Management Framework 3.0 et les autres logiciels requis. Pour connaître les conditions préalables pour tous les rôles de serveur, consultez la rubrique [Conditions préalables pour Exchange 2013](exchange-2013-prerequisites-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.


## Utilisation du programme d'installation pour installer les outils de gestion Exchange 2013

1.  Connectez-vous à l'ordinateur sur lequel vous voulez installer Exchange 2013.

2.  Accédez à l'emplacement réseau des fichiers d'installation d'Exchange 2013.

3.  Lancez le Programme d'installation de Exchange 2013 en double-cliquant sur `Setup.exe`
    
    > [!IMPORTANT]  
    > Si le contrôle d'accès des utilisateurs est activé, vous devez cliquer avec le bouton droit sur <code>Setup.exe</code> et sélectionner <strong>Exécuter en tant qu'administrateur</strong>.


4.  À la page **Vérifier les mises à jour**, indiquez si vous souhaitez que le Programme d'installation se connecte à Internet et télécharge les mises à jour du produit et de la sécurité pour Exchange 2013. Si vous sélectionnez **Se connecter à Internet et vérifier les mises à jour**, le Programme d'installation téléchargera les mises à jour et les appliquera avant de continuer. Si vous sélectionnez **Ne pas vérifier les mises à jour tout de suite**, vous pouvez télécharger et installer les mises à jour manuellement plus tard. Nous vous recommandons de télécharger et d'installer les mises à jour maintenant. Cliquez sur **Suivant** pour continuer.

5.  
    
    La page **Introduction** lance l'installation d'Exchange dans votre organisation. Il vous guide à travers l'installation. Plusieurs liens vers un contenu de déploiement utile sont répertoriés. nous vous recommandons de cliquer sur ces liens avant de poursuivre l'installation. Cliquez sur **Suivant** pour continuer.

6.  
    
    Dans la page **Contrat de licence**, lisez les termes du contrat de licence. Si vous acceptez les termes, sélectionnez **J'accepte les termes du contrat de licence**, puis cliquez sur **Suivant**.

7.  
    
    dans la page **Paramètres recommandés**, indiquez si vous souhaitez utiliser les paramètres recommandés. Si vous sélectionnez l'option **Utiliser les paramètres recommandés**, Exchange enverra automatiquement des rapports d'erreurs et des informations sur votre matériel informatique et l'utilisation de Microsoft Exchange. Si vous sélectionnez l'option **Ne pas utiliser les paramètres recommandés**, ces paramètres restent désactivés. Toutefois, vous pouvez les activer à tout moment une fois l'installation terminée. Pour plus d'informations sur ces paramètres et l'utilisation des informations envoyées à Microsoft, cliquez sur **?**.

8.  
    
    À la page **Sélection des rôles serveur**, vérifiez que **Outils de gestion** est sélectionné.
    
    Sélectionnez **Installer automatiquement les rôles et les fonctionnalités Windows Server requis pour Exchange Server** pour que l'Assistant Installation installe les composants requis de Windows. Il peut s'avérer nécessaire de redémarrer l'ordinateur pour terminer l'installation de certaines fonctionnalités de Windows. Si vous ne sélectionnez pas cette option, vous devez installer les fonctionnalités Windows manuellement.
    
    > [!NOTE]
    > Cette option installe uniquement les fonctionnalités Windows requises par Exchange. Vous devez installer manuellement les autres composants requis. Pour plus d'informations, consultez la rubrique <a href="exchange-2013-prerequisites-exchange-2013-help.md">Conditions préalables pour Exchange 2013</a>.
    
    Cliquez sur **Suivant** pour continuer.

9.  dans la page **Espace et emplacement d'installation**, acceptez l'emplacement d'installation par défaut ou cliquez sur **Parcourir** pour choisir un nouvel emplacement. Assurez-vous que l'emplacement sur lequel vous souhaitez installer Exchange dispose d'un espace disque suffisant. Cliquez sur **Suivant** pour continuer.

10. 
    
    Si vous exécutez le programme d'installation d'Exchange 2013 pour la première fois dans votre organisation, entrez le nom de votre organisation Exchange à la page **Organisation Exchange**. Un nom d'organisation Exchange ne peut contenir que les caractères suivants :
    
      - A à Z
    
      - a à z
    
      - 0 à 9
    
      - Espace (pas au début ni à la fin)
    
      - Trait d'union ou tiret
        
        > [!NOTE]
        > Un nom d'organisation ne peut pas contenir plus de 64 caractères. Le nom d'organisation ne peut pas être vide.
    
    Si vous souhaitez utiliser le modèle d'autorisations partagées Active Directory, sélectionnez l'option **Appliquer le modèle de sécurité des autorisations partagées Active Directory à l'organisation Exchange**.
    
    > [!CAUTION]
    > La plupart des organisations n'ont pas besoin d'appliquer le modèle d'autorisations partagées Active Directory. Si vous devez séparer la gestion des principaux de sécurité Active Directory et la configuration Exchange, les autorisations partagées du contrôle d'accès basé sur les rôles (RBAC) peuvent vous convenir. Pour plus d'informations, cliquez sur <strong>?</strong>.
    
    Cliquez sur **Suivant** pour continuer.

11. 
    
    Dans la page **Tests de préparation**, affichez l'état pour déterminer si les contrôles préalables de l'organisation et du rôle serveur ont été accomplis avec succès. Si ce n'est pas le cas, vous devez résoudre les erreurs signalées avant d'installer Exchange 2013. Il n'est pas nécessaire de quitter le programme d'installation lors de la résolution des erreurs relatives aux éléments requis. Une fois qu'une erreur signalée a été résolue, cliquez sur **Précédent**, puis sur **Suivant** pour exécuter à nouveau la vérification préalable. Veillez également à vérifier tous les avertissements signalés. Si tous les contrôles de préparation sont probants, cliquez sur **Suivant** pour installer Exchange 2013.

12. 
    
    Dans la page **Achèvement**, cliquez sur **Terminer**.

13. Redémarrez l'ordinateur une fois l'installation d'Exchange 2013 terminé.

## Utilisation du mode d'installation sans assistance pour installer les outils de gestion Exchange 2013

1.  Connectez-vous à l'ordinateur sur lequel vous voulez installer les outils de gestion d'Exchange 2013.

2.  Accédez à l'emplacement réseau des fichiers d'installation d'Exchange 2013.

3.  Depuis l'invite de commandes, exécutez la commande suivante :
    
    > [!IMPORTANT]  
    > Si le contrôle de compte d'utilisateur est activé, vous devez exécuter<code>Setup.exe</code> à partir d'une invite de commandes élevée.
    
    ```powershell
Setup.exe /Role:ManagementTools /IAcceptExchangeServerLicenseTerms
```

Pour plus d'informations, consultez la rubrique [Installation d’Exchange 2013 en mode sans assistance](install-exchange-2013-using-unattended-mode-exchange-2013-help.md).

