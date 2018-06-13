---
title: "Création d'un déploiement hybride avec l’assistant Configuration hybride: Exchange 2013 Help"
TOCTitle: Création d'un déploiement hybride avec l’assistant Configuration hybride
ms:assetid: 997a25d3-7fb3-4d4e-bb28-defcbf542c99
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ200787(v=EXCHG.150)
ms:contentKeyID: 50479670
ms.date: 03/14/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Création d'un déploiement hybride avec l’assistant Configuration hybride

Cette rubrique est en cours de rédaction.  

_**Sapplique à :**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :**2016-12-09_

Un déploiement hybride vous permet d'étendre l'éventail de fonctionnalités proposé et le contrôle administratif que vous exercez dans votre organisation Exchange Server locale vers le nuage. Un déploiement hybride sert également de support à une solution d'archivage en nuage pour vos boîtes aux lettres locales avec l'archivage Exchange Online et peut également servir d'étape intermédiaire à la migration définitive de vos boîtes aux lettres locales vers Exchange Online.

Cette rubrique couvre la configuration d’un déploiement hybride pour votre organisation Exchange locale et votre organisation Exchange Online dans Office 365 pour les entreprises utilisant l’Assistant Configuration hybride. Dans cette rubrique, un déploiement hybride est créé pour la configuration d’organisation suivante :

  - L’organisation locale est une organisation Exchange locale à forêt unique.

  - L’organisation locale n’utilise pas de service Microsoft Exchange Online Protection (EOP) existant pour la protection locale.

  - Aucun serveur de transport Edge n’est déployé dans l’organisation locale. L’assistant Configuration hybride prend en charge la configuration de serveurs de transport Edge dans le cadre d’un déploiement hybride, mais la configuration de serveurs de transport Edge dans l’Assistant n’est pas couverte par cette rubrique.

<table>
<thead>
<tr class="header">
<th><img src="images/Dn151301.important(EXCHG.150).gif" title="Important" alt="Important" />Important :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>La configuration d'un déploiement hybride avec l'Assistant Configuration hybride nécessite que l'Assistant remplisse plusieurs conditions préalables importantes et que les fonctions de déploiement hybride fonctionnent correctement. Vous devez remplir toutes les conditions préalables décrites dans <a href="hybrid-deployment-prerequisites-exchange-2013-help.md">Configuration requise pour un déploiement hybride</a> avant d'utiliser l'Assistant Configuration hybride pour créer et configurer votre déploiement hybride.<br />
En outre, l’<a href="http://technet.microsoft.com/exdeploy2013">Assistant de déploiement Exchange Server</a> est un outil web gratuit qui vous aide à configurer un déploiement hybride entre votre organisation locale et Office 365, ou à migrer complètement vers Office 365. L’outil vous pose une petite série de questions simples, puis, en fonction de vos réponses, crée une liste de contrôle personnalisée avec des instructions pour configurer votre déploiement hybride. Nous vous recommandons fortement d’utiliser l’Assistant de déploiement pour générer une liste de contrôle de déploiement hybride personnalisée selon les besoins spécifiques de votre organisation.</td>
</tr>
</tbody>
</table>


Si vous souhaitez rechercher des tâches de gestion supplémentaires relatives aux déploiements hybrides, consultez la rubrique [Procédures de déploiement hybride](hybrid-deployment-procedures-exchange-2013-help.md).

Pour plus d'informations sur les déploiements hybrides, consultez la rubrique [Déploiements hybrides Exchange Server](exchange-server-hybrid-deployments-exchange-2013-help.md). Pour plus d'informations sur Office 365, consultez la rubrique [Qu'est-ce qu'Office 365 ?](http://go.microsoft.com/fwlink/?linkid=266712).

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : 30 minutes
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Dn151301.important(EXCHG.150).gif" title="Important" alt="Important" />Important :</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>La durée de configuration des conditions préalables pour un déploiement hybride sera beaucoup plus longue que la durée d'exécution estimée des procédures de l'Assistant Configuration hybride décrites dans cette rubrique. Par exemple, l'inscription à Office 365 Entreprise, la configuration de la synchronisation Active Directory et l'affectation de licences Exchange Online requièrent un plus grand investissement en temps et peuvent également impliquer des changements de topologie réseau. Vous devez prévoir plus de temps que celui estimé pour réaliser cette procédure sur le temps global nécessaire à la configuration du déploiement de bout en bout.</td>
    </tr>
    </tbody>
    </table>


  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l'entrée « Déploiements hybrides » dans la rubrique [Autorisations d’infrastructure Exchange et Shell](https://technet.microsoft.com/fr-fr/library/dd638114\(v=exchg.150\)).

  - Vous devez lancer l’Assistant Configuration hybride sur un ordinateur exécutant la version prise en charge la plus récente du produit Exchange. Les dernières étapes de l’Assistant Configuration hybride pour la configuration de l’authentification OAuth Exchange exigent que les étapes soient réalisées à partir d’un serveur Exchange local ou à partir de tout serveur ou poste de travail appartenant au domaine. En outre, le processus d’authentification OAuth fonctionne mieux lors de l’utilisation de la version de bureau d’Internet Explorer 11 ou ultérieure.

  - Consultez [Déploiements hybrides Exchange Server](exchange-server-hybrid-deployments-exchange-2013-help.md) et assurez-vous de comprendre quels domaines seront affectés par la configuration d'un déploiement hybride.

  - Examinez et remplissez toutes les conditions préalables au déploiement hybride décrites dans [Configuration requise pour un déploiement hybride](hybrid-deployment-prerequisites-exchange-2013-help.md).

  - L’outil Analyseur de connectivité à distance de Microsoft vérifie la connectivité externe de votre organisation Exchange locale et s’assure que vous êtes prêt à configurer votre déploiement hybride. Nous vous recommandons vivement de vérifier votre organisation locale à l'aide de l'outil Analyseur de connectivité à distance avant de configurer votre déploiement hybride via l'Assistant Configuration hybride. Pour plus d'informations, consultez la rubrique [Outil Analyseur de connectivité à distance](http://go.microsoft.com/fwlink/p/?linkid=167905).

  - Nous vous recommandons vivement de configurer l’authentification unique à l’aide de la synchronisation de mot de passe Azure Active Directory Connect. L’authentification unique permet aux utilisateurs d’accéder à la fois à l’organisation locale et à l’organisation Exchange Online avec un nom d’utilisateur et un mot de passe uniques. L’authentification unique assure également que les utilisateurs ne sont pas invités à saisir leurs informations d’identification pour accéder au contenu archivé de l’organisation Exchange Online lorsqu’ils utilisent l’archivage Exchange Online. Pour plus d’informations sur la synchronisation de mot de passe, voir [Azure AD Connect Sync : implémenter la synchronisation de mot de passe](http://go.microsoft.com/fwlink/p/?linkid=723513)

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](https://technet.microsoft.com/fr-fr/library/jj150484\(v=exchg.150\)).

<table>
<thead>
<tr class="header">
<th><img src="images/Mt589761.tip(EXCHG.150).gif" title="Conseil" alt="Conseil" />Conseil :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.</td>
</tr>
</tbody>
</table>


## Utiliser le Centre d'administration Exchange et l'Assistant Configuration hybride pour créer un déploiement hybride

Utilisez la procédure suivante pour créer et configurer un déploiement hybride :

1.  Dans le CAE sur un serveur Exchange de votre organisation locale, accédez au nœud **Hybride**.

2.  Dans le nœud **Hybride**, cliquez sur **Configurer** pour saisir vos informations d’identification Office 365.
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Dn151301.important(EXCHG.150).gif" title="Important" alt="Important" />Important :</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Si votre organisation locale se trouve en Chine et que votre client Office 365 est hébergé par 21Vianet, vous devez cocher la case <strong>Mon organisation Office 365 est hébergée par 21Vianet</strong>. Si votre client Office 365 est hébergé par 21Vianet et que cette case n’est pas cochée, l’Assistant de configuration hybride ne se connectera pas au service 21Vianet, vos informations d’identification de compte Office 365 ne seront pas reconnues et l’Assistant ne se terminera pas correctement.</td>
    </tr>
    </tbody>
    </table>


3.  Lorsque vous êtes invité à vous connecter à Office 365, sélectionnez **Connexion à Office 365** et saisissez les informations d’identification du compte. Le compte auquel vous vous connectez doit être un administrateur global dans Office 365.

4.  Cliquez à nouveau sur **Configurer** pour démarrer l’Assistant Configuration hybride.

5.  Sur la page de **téléchargement de l’Assistant Configuration hybride de Microsoft Office 365**, cliquez sur **Cliquer ici** pour télécharger l’Assistant. Lorsque vous y êtes invité, cliquez sur **Installer** dans la boîte de dialogue **Installation de l’application**.

6.  Cliquez sur **Suivant**, puis, dans la section **Organisation de serveur Exchange local**, sélectionnez **Détecter un serveur exécutant Exchange 2013 CAS ou Exchange 2016**. L’Assistant va tenter de détecter un serveur Exchange local. Si l’Assistant ne détecte aucun serveur Exchange ou si vous souhaitez utiliser un autre serveur, sélectionnez **Spécifier un serveur exécutant Exchange 2013 CAS ou Exchange 2016**, puis indiquez le nom de domaine complet interne d’un serveur de boîtes aux lettres Exchange.

7.  Dans la section **Office 365 Exchange Online**, sélectionnez **Microsoft Office 365** et cliquez sur **Suivant**.

8.  Sur la page **Informations d’identification**, dans la section **Saisissez vos informations d’identification pour le compte local**, sélectionnez **Utiliser les informations d’identification Windows actuelles** pour que l’Assistant utilise le compte auquel vous êtes connecté pour accéder à vos serveurs Active Directory et Exchange locaux. Si vous souhaitez spécifier un autre ensemble d’informations d’identification, désactivez **Utiliser les informations d’identification Windows actuelles** et indiquez le nom d’utilisateur et le mot de passe d’un compte Active Directory que vous souhaitez utiliser. Quel que soit votre choix, le compte utilisé doit être membre du groupe de sécurité des administrateurs de l’entreprise.

9.  Dans la section **Saisissez vos informations d’identification pour Office 365**, spécifiez le nom d’utilisateur et le mot de passe d’un compte Office 365 disposant des droits d’accès d’administrateur général. Cliquez sur **Suivant**.

10. Sur la page **Validations des connexions et des informations d’identification**, l’Assistant se connecte à votre organisation locale et à votre organisation Office 365 pour valider les informations d’identification et examiner la configuration actuelle des deux organisations. Cliquez sur **Suivant** lorsqu’il a terminé.

11. Sur la page **Domaines hybrides**, sélectionnez les domaines que vous souhaitez inclure dans votre déploiement hybride. Dans la plupart des déploiements, vous pouvez laisser la colonne **Découverte automatique** définie sur **False** pour chaque domaine. Sélectionnez uniquement **True** en regard d’un domaine si vous devez obliger l’Assistant à utiliser les informations de découverte automatique à partir d’un domaine spécifique. Cliquez sur **Suivant**.
    
    <table>
    <colgroup>
    <col style="width: 100%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th><img src="images/Dn151301.important(EXCHG.150).gif" title="Important" alt="Important" />Important :</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Cette étape de sélection de domaine de l'Assistant Configuration hybride peut s'afficher ou non lorsque vous lancez l'Assistant.<br />
    Cette étape ne s’affichera pas si :
    <ul>
    <li><p>Vous avez seulement un domaine local accepté ajouté à votre organisation cliente Office 365. Ce domaine étant le seul disponible pour la configuration du déploiement hybride, le domaine est automatiquement sélectionné et l'étape est omise par l'Assistant.</p></li>
    <li><p>Aucun domaine local accepté n’a été ajouté à votre organisation cliente Office 365. Dans ce cas, un message d’erreur s’affiche et vous devez ajouter au moins un domaine à votre organisation cliente Office 365 avant de poursuivre. Vous pouvez le faire via le portail administratif Office 365, ou en configurant facultativement les services AD FS (Active Directory Federation Services) dans votre organisation locale.</p></li>
    </ul>
    Cette étape s'affichera si plus d'un domaine local accepté a été ajouté à votre organisation cliente Office 365.</td>
    </tr>
    </tbody>
    </table>


12. Sur la page **Approbation de fédération**, cliquez sur **Activer**, puis sur **Suivant**.

13. Sur la page **Propriété de domaine**, cliquez sur **Copier dans le Presse-papiers** pour copier les informations des jetons de preuve des domaines que vous avez choisis d’intégrer au déploiement hybride. Ouvrez un éditeur de texte comme le Bloc-notes et collez les informations des jetons pour ces domaines. Avant de continuer avec l’Assistant Configuration hybride, vous devez utiliser ces informations pour créer un enregistrement TXT pour chaque domaine dans votre DNS public. Reportez-vous à l’aide de l’hôte DNS pour plus d’informations sur l’ajout d’un enregistrement TXT à votre zone DNS. Cliquez sur **Suivant** après la création des enregistrements TXT et la réplication des enregistrements DNS.

14. Sur la page **Certificat de transport**, dans le champ **Sélectionner un serveur de référence**, sélectionnez le serveur Exchange disposant du certificat que vous avez configuré précédemment dans la liste de vérification.

15. Dans le champ **Sélectionner un certificat**, sélectionnez le certificat à utiliser pour le transport de messagerie sécurisée. Cette liste affiche les certificats numériques émis par une autorité de certification (CA) tierce installés sur le serveur de boîtes aux lettres sélectionné à l’étape précédente. Cliquez sur **Suivant**.

16. Sur la page **Nom de domaine complet de l’organisation**, saisissez le nom de domaine complet accessible de l’extérieur pour votre serveur Exchange accessible sur Internet. Office 365 utilise ce nom de domaine complet pour configurer les connecteurs de service pour le transport de messagerie sécurisée entre vos organisations Exchange. Par exemple, saisissez « mail.contoso.com ». Cliquez sur **Suivant**.

17. Les choix de configuration du déploiement hybride ayant été mis à jour, vous êtes désormais prêt à procéder à des changements au niveau des services Exchange et de la configuration du déploiement hybride. Cliquez sur **Mettre à jour** pour lancer le processus de configuration. Pendant l'exécution du processus de configuration hybride, l'Assistant affiche les fonctions et services configurés pour le déploiement hybride et mis à jour.

18. L’Assistant affiche un message de fin et le bouton **Fermer** s’affiche. Cliquez sur **Fermer** pour terminer le processus de configuration du déploiement hybride et pour fermer l’Assistant.

## Configurer l’authentification OAuth entre des organisations Exchange et Exchange Online

Pour les déploiements hybrides Exchange 2013/2010 et Exchange 2013/2007 mixtes, la nouvelle connexion d’authentification basée sur OAuth de déploiement hybride entre les organisations Office 365 et Exchange locales n’est pas configurée par l’Assistant de configuration hybride. Ces déploiements continuent à utiliser le processus d’approbation de fédération par défaut. Toutefois, certaines fonctionnalités d’Exchange 2013, telles que la gestion des enregistrements de messagerie (MRM), l’archivage inaltérable Exchange et la découverte électronique inaltérable sont totalement disponibles dans votre organisation seulement en utilisant le nouveau protocole d’authentification OAuth d’Exchange. Nous recommandons à toutes les organisations Exchange 2013/2010 et Exchange 2013/2007 mixtes qui veulent implémenter ces fonctionnalités dans le cadre d’un nouveau déploiement hybride avec Exchange Online de configurer l’authentification OAuth d’Exchange après la configuration de leur déploiement hybride avec l’Assistant de configuration hybride.

Pour obtenir la procédure de configuration détaillée, consultez la rubrique [Configurer l’authentification OAuth entre des organisations Exchange et Exchange Online](https://technet.microsoft.com/fr-fr/library/dn594521\(v=exchg.150\)).

Pour plus d’informations sur les fonctionnalités de sécurité et de conformité Exchange qui utilisent l’authentification OAuth, consultez les rubriques suivantes :

  - [Utilisation de l’authentification OAuth pour prendre en charge l’archivage dans un déploiement hybride Exchange](https://technet.microsoft.com/fr-fr/library/dn689104\(v=exchg.150\))

  - [Utilisation de l’authentification OAuth pour prendre en charge la découverte électronique dans un déploiement hybride Exchange](https://technet.microsoft.com/fr-fr/library/dn497703\(v=exchg.150\))

## Comment savoir si cela a fonctionné ?

Un message d'exécution réussie de l'Assistant Configuration hybride sera la première information vous indiquant que la procédure de configuration hybride s'est correctement déroulée.

Pour obtenir la confirmation que la création et la configuration de votre déploiement hybride se sont correctement déroulées, procédez comme suit :

  - Exécutez la commande suivante dans l'environnement de ligne de commande Exchange Management Shell pour l'organisation locale. Cette commande affiche les points de terminaison de transport, les fonctions hybrides et les valeurs et paramètres de configuration du déploiement hybride. Vérifiez que ces valeurs sont correctes.
    
        Get-HybridConfiguration

  - Confirmez que l'Assistant Configuration hybride a terminé toutes les étapes de configuration en consultant le journal de la configuration hybride. Par défaut, ce journal se situe sur le serveur de boîtes aux lettres local à l'emplacement suivant : C:\\Program Files\\Microsoft\\Exchange Server\\V15\\Logging\\Update-HybridConfiguration.

  - Déplacez une boîte aux lettres locale existante vers l'organisation Exchange Online pour tester la fonction de déplacement de boîte aux lettres, ou créez une nouvelle boîte aux lettres utilisateur dans l'organisation Exchange Online pour tester le partage de disponibilité du calendrier entre les deux organisations. Ces actions vous permettront également de tester la remise du courrier entre l'organisation locale et l'organisation Exchange Online et de confirmer qu'elle fonctionne correctement avec les boîtes aux lettres existantes, que la remise du courrier est sécurisée et que le courrier est traité comme des messages internes à destination de l'organisation Exchange.
    
      - Utilisez le CAE et accédez à **Entreprise** \> **Destinataires** \> **Boîtes aux lettres** pour créer une boîte aux lettres distante dans Exchange Online.
    
      - Utilisez le CAE et accédez à **Office 365** \> **Destinataires** \> **Migration** pour déplacer une boîte aux lettres existante vers Exchange Online.

