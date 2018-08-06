---
title: 'Installer le rôle de transport Edge d’Exchange 2013 à l’aide de l’Assistant | Microsoft Docs'
TOCTitle: Installer le rôle de transport Edge d’Exchange 2013 à l’aide de l’Assistant Installation
ms:assetid: b8e51b0b-201e-4c64-92c8-3ac0db04b6e2
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dn635117(v=EXCHG.150)
ms:contentKeyID: 61204574
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Installer le rôle de transport Edge d’Exchange 2013 à l’aide de l’Assistant Installation

 

_**Sapplique à :** Exchange Server, Exchange Server 2013_

_**Dernière rubrique modifiée :** 2014-06-19_

Cette rubrique explique comment utiliser l’Assistant Installation de Microsoft Exchange Server 2013 pour installer le rôle serveur de transport Edge Exchange 2013 sur un ordinateur. Le rôle de transport Edge est disponible avec Exchange 2013 Service Pack 1 (SP1) ou version ultérieure. Pour de plus amples informations sur la planification et le déploiement d’Exchange 2013, consultez la rubrique [Planification et déploiement](planning-and-deployment-for-exchange-2013-installation-instructions.md).

Nous recommandons d’installer le rôle de transport Edge dans un réseau de périmètre extérieur à la forêt interne de votre organisation Active Directory. Bien que vous puissiez installer le rôle serveur de transport Edge sur un ordinateur joint à un domaine, cette configuration vous permettrait uniquement de gérer les fonctionnalités et les paramètres Windows. Le rôle de transport Edge n’utilise pas Active Directory. Par contre, il utilise la fonctionnalité Active Directory AD LDS (Lightweight Directory Services) Windows pour stocker la configuration et les informations de destinataire. Pour plus d’informations sur le rôle de transport Edge, consultez la rubrique [Serveurs de transport Edge](edge-transport-servers-exchange-2013-help.md).

Si vous souhaitez installer les rôles de boîtes aux lettres ou d’accès au client Exchange 2013 sur un ordinateur, consultez la rubrique [Installer Exchange 2013 à l’aide de l’Assistant Installation](install-exchange-2013-using-the-setup-wizard-exchange-2013-help.md). Le rôle de transport Edge ne peut pas être installé sur le même ordinateur que les rôles serveur de boîtes aux lettres ou d’accès au client.

> [!TIP]
> Avez-vous déjà entendu parler de l’Assistant de déploiement Exchange Server ? Il s’agit d’un outil en ligne gratuit qui vous permet de déployer rapidement Exchange 2013 dans votre organisation en répondant à quelques questions et en créant une liste de contrôle de déploiement personnalisée. Pour en savoir plus, consultez la page <a href="exchange-server-deployment-assistant-exchange-2013-help.md">Assistant de déploiement Exchange Server</a>.


Pour plus d’informations sur les tâches postérieures à l’installation, consultez la rubrique [Tâches consécutives à l’installation d’Exchange 2013](exchange-2013-post-installation-tasks-exchange-2013-help.md).

## Ce qu’il faut savoir avant de commencer

  - Durée d’exécution estimée : 40 minutes

  - Assurez-vous que vous avez lu les notes de publication avant d’installer Exchange 2013. Pour plus d’informations, voir [Notes de publication relatives à Exchange 2013](release-notes-for-exchange-2013-exchange-2013-help.md).

  - L’ordinateur sur lequel vous installez Exchange 2013 doit disposer d’un système d’exploitation compatible (tel que Windows Server 2008 R2 avec SP1, Windows Server 2012 R2 ou Windows Server 2012), avoir suffisamment d’espace disque et satisfaire à d’autres exigences. Pour obtenir plus d’informations sur la configuration système requise, consultez la rubrique [Configuration requise pour Exchange 2013](exchange-2013-system-requirements-exchange-2013-help.md).

  - Pour exécuter la configuration d’Exchange 2013, vous devez installer Microsoft .NET Framework 4.5, Windows Management Framework et d’autres logiciels requis. Pour connaître les conditions préalables pour tous les rôles de serveur, consultez la rubrique [Conditions préalables pour Exchange 2013](exchange-2013-prerequisites-exchange-2013-help.md).

  - Vous devez configurer le suffixe DNS principal sur l’ordinateur. Par exemple, si le nom de domaine complet de votre ordinateur est edge.contoso.com, le suffixe DNS de cet ordinateur est contoso.com. Pour plus d’informations, voir [Suffixe DNS principal manquant](primary-dns-suffix-is-missing-exchange-2013-help.md).

  - Les serveurs de transport Hub Exchange 2007 et Exchange 2010 doivent être mis à jour pour créer un abonnement EdgeSync entre eux et un serveur de transport Edge Exchange 2013. Si vous n’installez pas cette mise à jour, l’abonnement EdgeSync ne fonctionnera pas correctement. Pour plus d’informations, consultez la section « Scénarios de coexistence pris en charge » dans la rubrique [Configuration requise pour Exchange 2013](exchange-2013-system-requirements-exchange-2013-help.md).

  - Assurez-vous que le compte que vous utilisez est membre du groupe Administrateurs local sur l’ordinateur sur lequel vous installez le rôle de transport Edge.

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!CAUTION]
> Après avoir installé Exchange sur un serveur, vous ne devez pas modifier le nom du serveur. La modification du nom d’un serveur après avoir installé un rôle de serveur Exchange n’est pas prise en charge.


## Installer Exchange Server 2013

> [!NOTE]
> Pour télécharger la dernière version d’Exchange 2013, voir <a href="updates-for-exchange-2013-exchange-2013-help.md">Mises à jour pour Exchange 2013</a>


1.  Connectez-vous à l’ordinateur sur lequel vous voulez installer Exchange 2013.

2.  Accédez à l’emplacement réseau des fichiers d’installation d’Exchange 2013.

3.  Lancez le programme d’installation d’Exchange 2013 en double-cliquant sur `Setup.exe`
    
    > [!NOTE]
    > Si le contrôle d’accès d’utilisateur est activé, vous devez cliquer avec le bouton droit de la souris sur <code>Setup.exe</code> et sélectionner <strong>Exécuter en tant qu’administrateur</strong>.


4.  Sur la page **Vérifier les mises à jour ?**, indiquez si vous souhaitez que le programme d’installation se connecte à Internet et télécharge les mises à jour de produit et de sécurité pour Exchange 2013. Si vous sélectionnez **Se connecter à Internet et vérifier les mises à jour**, le programme d’installation télécharge les mises à jour et les applique avant de continuer. Si vous sélectionnez **Ne pas vérifier les mises à jour maintenant**, vous pouvez télécharger et installer les mises à jour manuellement plus tard. Nous vous recommandons de télécharger et d’installer les mises à jour maintenant. Cliquez sur **Suivant** pour continuer.

5.  
    
    La page **Introduction** lance l’installation d’Exchange dans votre organisation. Elle vous guide au fil de l’installation. Plusieurs liens vers du contenu utile sur le déploiement sont répertoriés. Nous vous recommandons de cliquer sur ces liens avant de poursuivre l’installation. Cliquez sur **Suivant** pour continuer.

6.  
    
    Sur la page **Contrat de licence**, lisez les termes du contrat de licence logiciel. Si vous acceptez les termes, sélectionnez **J’accepte les termes du contrat de licence**, puis cliquez sur **Suivant**.

7.  
    
    Dans la page **Paramètres recommandés**, indiquez si vous souhaitez utiliser les paramètres recommandés. Si vous sélectionnez l’option **Utiliser les paramètres recommandés**, Exchange enverra automatiquement à Microsoft des rapports d’erreurs et des informations sur votre matériel informatique et l’utilisation d’Exchange. Si vous sélectionnez **Ne pas utiliser les paramètres recommandés**, ces paramètres restent désactivés. Toutefois, vous pouvez les activer à tout moment une fois l’installation terminée. Pour plus d’informations sur ces paramètres et l’utilisation des informations envoyées à Microsoft, cliquez sur **?**.

8.  
    
    Sur la page **Sélection du rôle de serveur**, sélectionnez **Transport Edge**. N’oubliez pas que vous ne pouvez pas ajouter les rôles serveur de boîte aux lettres ou serveur d’accès au client à un ordinateur sur lequel le rôle de transport Edge est installé. Les outils de gestion sont installés automatiquement si vous installez un rôle serveur.
    
    Sélectionnez **Installer automatiquement les rôles et les fonctionnalités Windows Server requis pour Exchange Server** pour que l’Assistant Installation installe les composants Windows requis. Il peut s’avérer nécessaire de redémarrer l’ordinateur pour terminer l’installation de certaines fonctionnalités Windows. Si vous ne sélectionnez pas cette option, vous devez installer les fonctionnalités Windows manuellement.
    
    > [!NOTE]
    > Cette option installe uniquement les fonctionnalités Windows requises par Exchange. Vous devez installer manuellement les autres composants requis. Pour plus d’informations, voir <a href="exchange-2013-prerequisites-exchange-2013-help.md">Conditions préalables pour Exchange 2013</a>.
    
    Cliquez sur **Suivant** pour continuer.

9.  Sur la page **Espace et emplacement d’installation**, acceptez l’emplacement d’installation par défaut ou cliquez sur **Parcourir** pour choisir un nouvel emplacement. Assurez-vous que l’emplacement sur lequel vous souhaitez installer Exchange dispose d’un espace disque suffisant. Cliquez sur **Suivant** pour continuer.

10. 
    
    Sur la page **Tests de préparation**, affichez l’état pour déterminer si les vérifications préalables de l’organisation et du rôle serveur ont été accomplies avec succès. Si ce n’est pas le cas, vous devez corriger les erreurs signalées avant d’installer Exchange 2013. Vous n’avez pas besoin de quitter le programme d’installation pour résoudre certaines de ces erreurs. Une fois qu’une erreur signalée a été résolue, cliquez sur **Retour**, puis sur **Suivant** pour exécuter à nouveau la vérification des conditions préalables. Veillez également à vérifier tous les avertissements signalés. Si tous les tests de préparation sont probants, cliquez sur **Suivant** pour installer Exchange 2013.

11. 
    
    Dans la page **Achèvement**, cliquez sur **Terminer**.

12. Redémarrez l’ordinateur une fois l’installation d’Exchange 2013 terminée.

13. Terminez votre déploiement en exécutant les tâches indiquées dans [Tâches consécutives à l’installation d’Exchange 2013](exchange-2013-post-installation-tasks-exchange-2013-help.md).

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez installé Exchange 2013 avec succès, consultez [Vérifier une installation d’Exchange 2013](verify-an-exchange-2013-installation-exchange-2013-help.md).

Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), et [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

Avez-vous trouvé ce que vous cherchez ? Veuillez prendre une minute pour [nous envoyer votre avis à l'adresse](mailto:exsetuphelpfeedback@microsoft.com?subject=exchange%202013%20setup%20help%20feedback) au sujet des informations que vous souhaitiez y trouver.

