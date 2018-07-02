---
title: 'Comment et quand désaffecter vos serveurs Exchange locaux dans un déploiement hybride: Exchange 2013 Help'
TOCTitle: Comment et quand désaffecter vos serveurs Exchange locaux dans un déploiement hybride
ms:assetid: 4f884b7a-3b8a-4207-8843-65d3141731dc
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dn931280(v=EXCHG.150)
ms:contentKeyID: 64965199
ms.date: 03/26/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Comment et quand désaffecter vos serveurs Exchange locaux dans un déploiement hybride

 

_<strong>Sapplique à :</strong>Exchange Online, Exchange Server, Exchange Server 2013, Exchange Server 2016_

_<strong>Dernière rubrique modifiée :</strong>2017-07-27_

Lisez cet article si vous êtes prêt à passer d’un déploiement Exchange hybride à une mise en œuvre cloud complète.

Pour convaincre une société d’adopter Exchange Online, l’une des meilleures options est d’utiliser l’approche de déploiement hybride décrite dans la rubrique [Planifier un déploiement hybride Exchange Online dans Office 365](https://msdn.microsoft.com/fr-fr/library/ff633682\(v=exchsrvcs.149\).aspx). Il s’agit de la seule option qui vous permet de facilement intégrer des boîtes aux lettres et d’annuler leur intégration (toutes les autres options natives ne permettent que l’intégration). En plus d’annuler l’intégration, une configuration hybride propose les options clés suivantes.

Cette rubrique vous aidera à comprendre les options de désaffectation de l’instance Exchange hybride, et à déterminer quand chacune de ces options doit être mise en œuvre. La désaffectation des serveurs Exchange hybrides peut être effectuée à différents moments et de différentes façons. Il est important de prendre le temps d’en comprendre les tenants et les aboutissants et de planifier correctement la désaffectation complète ou partielle des serveurs locaux.

  - **Disponibilité entre différents locaux**. Ceci vous permet de consulter les informations de disponibilité d’un utilisateur pendant la planification d’une réunion, quel que soit le site de sa boîte aux lettres.

  - **Archivage entre différents locaux**. Ceci permet à un client de déplacer uniquement la boîte aux lettres d’archivage d’un utilisateur dans le cloud. Il s’agit souvent de la première étape lorsque les clients essaient Office 365 et, plus spécifiquement, Exchange Online.

  - **Recherche de découverte entre différents locaux**. Ceci permet à un client d’effectuer une recherche de découverte électronique qui analysera les boîtes aux lettres et les archives dans les deux locaux (pour ce faire, vous devez configurer l’authentification OAuth).

  - **Outlook Web AppRedirection d’URL**. Ceci permet de rediriger les utilisateurs vers le bon local pour l’accès à Outlook Web App.

  - **Aucune recréation de profil après déplacement**. Contrairement à d’autres options de migration, le GUID de boîte aux lettres ne change pas. Cela signifie que vous n’avez pas besoin de recréer votre profil ou de retélécharger l’OST après le déplacement d’une boîte aux lettres.

En fonction des besoins de votre organisation, un déploiement hybride est la meilleure solution pour fournir l’expérience utilisateur et de coexistence la plus transparente possible.

## Autres méthodes de migration vers Exchange Online

Un déploiement hybride ne convient pas à tout le monde, en fait il existe généralement de meilleures options. Un grand nombre de clients ayant choisi de déployer une configuration hybride comptent moins de 50 utilisateurs. Si la liste des avantages offerts par un déploiement hybride peut sembler attrayante, le prix à payer est lourd en ce qui concerne sa complexité. Certains des plus petits clients ont besoin des fonctionnalités d’un déploiement hybride mais, pour la plupart d’entre eux, l’expérience serait bien meilleure avec une option de migration à basculement, intermédiaire ou IMAP. Pour choisir l’option de migration à adopter, vous pouvez utiliser le programme FastTrack. Pour en savoir plus, consultez la page de [FastTrack](https://go.microsoft.com/fwlink/?linkid=846696).

Le tableau suivant vous aide à choisir le type de migration le mieux adapté à votre organisation. (Pour obtenir plus d’informations, consultez l’article [Méthodes de migration des comptes de courrier vers Office 365](https://support.office.com/fr-fr/article/m%c3%a9thodes-de-migration-des-comptes-de-courrier-vers-office-365-0a4913fe-60fb-498f-9155-a86516418842?ui=fr-fr%26rs=fr-fr%26ad=fr).)


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Organisation existante</th>
<th>Nombre de boîtes aux lettres à migrer</th>
<th>Souhaitez-vous gérer des comptes d'utilisateur dans votre organisation locale ?</th>
<th>Type de migration</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Exchange 2013, Exchange 2010, Exchange 2007 ou Exchange 2003</p></td>
<td><p>Moins de 2 000 boîtes aux lettres</p></td>
<td><p>Non</p></td>
<td><p>Migration Exchange à basculement</p></td>
</tr>
<tr class="even">
<td><p>Exchange 2007 ou Exchange 2003</p></td>
<td><p>Moins de 2 000 boîtes aux lettres</p></td>
<td><p>Non</p></td>
<td><p>Migration Exchange intermédiaire</p></td>
</tr>
<tr class="odd">
<td><p>Exchange 2007 ou Exchange 2003</p></td>
<td><p>Plus de 2 000 boîtes aux lettres*</p></td>
<td><p>Oui</p></td>
<td><p>Migration Exchange intermédiaire ou migration à distance dans un déploiement hybride Exchange</p></td>
</tr>
<tr class="even">
<td><p>Exchange 2013 ou Exchange 2010</p></td>
<td><p>Plus de 2 000 boîtes aux lettres*</p></td>
<td><p>Oui</p></td>
<td><p>Migration à distance dans un déploiement hybride Exchange</p></td>
</tr>
<tr class="odd">
<td><p>Exchange 2000 Server ou versions antérieures</p></td>
<td><p>Pas de maximum</p></td>
<td><p>Oui</p></td>
<td><p>Migration IMAP</p></td>
</tr>
<tr class="even">
<td><p>Système de messagerie local non-Exchange</p></td>
<td><p>Pas de maximum</p></td>
<td><p>Oui</p></td>
<td><p>Migration IMAP</p></td>
</tr>
</tbody>
</table>


\*Certaines organisations avec moins de 2 000 boîtes aux lettres peuvent tirer parti des fonctions et des fonctionnalités qui ne sont disponibles qu’avec un déploiement hybride. Il est important d’examiner attentivement les avantages d’un déploiement hybride en tenant compte de la complexité qu’il induit. Nous recommandons vivement aux clients avec moins de 2 000 boîtes aux lettres d’envisager une migration intermédiaire ou à basculement avant de procéder à un déploiement hybride.

## Raison pour laquelle vous pouvez ne pas souhaiter désaffecter les serveurs Exchange en local

Au bout d’un certain temps, les clients avec une configuration hybride se rendent souvent compte que toutes leurs boîtes aux lettres ont été déplacées vers Exchange Online. À ce stade, ils peuvent décider de supprimer les serveurs Exchange en local. Cependant, ils découvrent qu’ils ne peuvent plus gérer leurs boîtes aux lettres cloud.

Lorsque la synchronisation d’annuaires est activée pour un client et qu’un utilisateur est synchronisé à partir de l’environnement local, la plupart des attributs ne peuvent être gérés depuis Exchange Online et doivent être gérés en local. Ce n’est pas dû à la configuration hybride, mais cela se produit en raison de la synchronisation d’annuaires. En outre, même si vous avez mis en place la synchronisation d’annuaires sans exécuter l’Assistant Configuration hybride, vous ne pouvez toujours pas gérer la plupart des tâches de destinataires à partir du cloud. Pour plus d’informations, consultez ce [blog TechNet](http://blogs.technet.com/b/exchange/archive/2012/12/05/decommissioning-your-exchange-2010-servers-in-a-hybrid-deployment.aspx).

## Des outils de gestion tiers peuvent-ils être utilisés ?

La possibilité d’utiliser un outil de gestion tiers ou ADSIEDIT est une question fréquemment posée. La réponse est que vous pouvez les utiliser, mais qu’ils ne sont pas pris en charge. La console de gestion Exchange, le Centre d’administration Exchange (CAE) et l’environnement Exchange Management Shell sont les seuls outils pris en charge qui sont disponibles pour gérer les destinataires et objets Exchange. Si vous décidez d’utiliser les outils de gestion tiers, cela sera à vos propres risques. Les outils de gestion tiers fonctionnent souvent correctement, mais Microsoft ne les valide pas.

## Scénarios courants

Il n’est pas simple de passer d’une configuration hybride à une configuration dans le cloud. Nous avons mis beaucoup de temps à établir un processus de passage à une configuration hybride fonctionnant correctement. Bien qu’il existe des problèmes, nous pensons que nous avons fait du bon travail en faisant d’une tâche presque impossible à réaliser un processus basé sur un assistant relativement simple.

Toutefois, nous avons consacré peu d’efforts dans la définition d’un processus vous permettent de passer d’une configuration hybride à une configuration dans le cloud uniquement. En fonction de vos objectifs immédiats, ce processus peut être relativement simple si vous suivez nos conseils. Ci-dessous figurent trois scénarios hybrides courants ainsi que nos recommandations pour atteindre correctement l’objectif final du client.

La base de clients hybride étant très diversifiée, il est difficile d’essayer de tous les intégrer dans des scénarios « courants ». Nous avons tenté de fournir ci-après des scénarios de haut niveau pour la désaffectation d’Exchange Server en local ; par conséquent, tandis que vous lisez ces scénarios et formez un plan de désaffectation, vous devrez déterminer le scénario qui convient le mieux à vos besoins.

## Scénario 1

**Problème** : mon organisation utilise une configuration hybride et toutes mes boîtes aux lettres sont dans Exchange Online. Je n’ai pas besoin de gérer mes utilisateurs en local et je n’ai plus besoin de la synchronisation d’annuaires ou de la synchronisation de mots de passe.

**Solution** : comme tous les utilisateurs seront gérés dans Office 365 et qu’aucune synchronisation d’annuaires supplémentaire n’est requise, vous pouvez en toute sécurité désactiver la synchronisation d’annuaires et retirer Exchange de l’environnement local.

![Supprimer Exchange de l’environnement local](images/Dn931280.f9c2a2cb-4c16-4ca3-8244-b89c1cdf0744(EXCHG.150).jpg "Supprimer Exchange de l’environnement local") **Pour désactiver la synchronisation d’annuaires et désinstaller l’instance d’Exchange hybride**

1.  Exécutez `Get-OrganizationConfig |fl PublicFoldersEnabled` et vérifiez qu’il n’est pas défini sur À distance. S’il est défini sur À distance et que vous souhaitez continuer à accéder aux dossiers publics, vous devez les migrer vers Exchange Online. Pour plus d’informations, consultez la rubrique [Use batch migration to migrate legacy public folders to Office 365 and Exchange Online](https://technet.microsoft.com/fr-fr/library/dn874017\(v=exchg.150\)).

2.  En supposant que vous avez déjà déplacé toutes les boîtes aux lettres vers Exchange Online, vous pouvez pointer les enregistrements DNS de découverte automatique et MX vers Exchange Online, plutôt que vers l’environnement local. Pour plus d’informations, consultez la rubrique [Référence : Enregistrements DNS externes pour Office 365](http://technet.microsoft.com/fr-fr/library/hh852557.aspx).
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Dn151301.important(EXCHG.150).gif" title="Important" alt="Important" />Important :</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Veillez à mettre à jour les DNS interne et externe, ou vous rencontrerez peut-être un comportement de connectivité client incohérent.</td>
    </tr>
    </tbody>
    </table>


3.  Ensuite, vous devez supprimer les valeurs de point de connexion de service sur vos serveurs Exchange. Cela garantit qu’aucun point de connexion de service n’est renvoyé, et que le client utilisera à la place la méthode DNS pour la découverte automatique. Voici un exemple :
    
        Get-ClientAccessServer | Set-ClientAccessServer -AutoDiscoverServiceInternalUri $Null
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Dn986544.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Si votre environnement comporte des serveurs Exchange 2007, vous devrez exécuter une commande similaire sur vos serveurs Exchange 2007 pour annuler les paramètres.</td>
    </tr>
    </tbody>
    </table>


4.  Il y a des connecteurs entrants et sortants créés par l’Assistant Configuration hybride que vous souhaiterez supprimer. Pour ce faire, procédez comme suit :
    
    1.  Connectez-vous au [portail d’administration d’Office 365](http://portal.office.com) et ouvrez une session en tant qu’administrateur client.
    
    2.  Sélectionnez l’option de gestion d’**Exchange**.
    
    3.  Accédez à **Flux de messagerie** -\> **Connexion**.
    
    4.  Vous pouvez désormais désactiver ou supprimer les connecteurs entrants et sortants. L’Assistant Configuration hybride crée des connecteurs avec l’espace de noms unique **Réception depuis \<identificateur unique\>** et **Émission vers \<identificateur unique\>** comme indiqué dans l’illustration ci-dessous.
        
        ![L’Assistant Configuration hybride crée des connecteurs avec l’espace de noms unique](images/Dn931280.7b1b6f0b-43d6-4407-8cd7-7dd52e016697(EXCHG.150).jpg "L’Assistant Configuration hybride crée des connecteurs avec l’espace de noms unique")  

5.  Supprimez la relation d’organisation créée par l’Assistant Configuration hybride. Pour ce faire, procédez comme suit :
    
    1.  Connectez-vous au [portail d’administration d’Office 365](http://portal.office.com) et ouvrez une session en tant qu’administrateur client.
    
    2.  Sélectionnez l’option de gestion d’Exchange.
    
    3.  Accédez à **Organisation**.
    
    4.  Sous **Partage de l’organisation**, supprimez l’organisation nommée **O365 vers local – \<identificateur unique\>**, comme indiqué dans l’illustration ci-dessous.
        
        ![Supprimer la relation d’organisation créée par l’Assistant Configuration hybride](images/Dn931280.2f0c1077-8785-487a-87a5-a75f0a4f0fea(EXCHG.150).jpg "Supprimer la relation d’organisation créée par l’Assistant Configuration hybride")  

6.  Si OAuth est configuré pour un déploiement hybride Exchange, vous devez désactiver la configuration à la fois en local et dans Office 365. Dans la plupart des environnements, ces étapes peuvent être ignorées car seul un petit sous-ensemble de nos clients a configuré OAuth.
    
    Pour désactiver la configuration en local, procédez comme suit :
    
    1.  À partir d’un serveur Exchange 2013, ouvrez l’environnement Exchange Management Shell.
    
    2.  Exécutez la commande suivante :
        
            Get-IntraorganizationConnector -Identity ExchangeHybridOnPremisesToOnline | Set-IntraOrganizationConnector -Enabled $False
    
    Pour désactiver la configuration Exchange Online, procédez comme suit :
    
    1.  Connectez Windows PowerShell à Exchange Online.
    
    2.  Exécutez la commande suivante :
        
            Run Get-IntraorganizationConnector -Identity ExchangeHybridOnlineToOnPremises | Set-IntraOrganizationConnector -Enabled $False
        
        Le paramètre *Identity* part du principe que vous avez utilisé l’Assistant Configuration hybride pour configurer OAuth. Si ce n’est pas le cas, vous devrez ajuster la valeur que vous avez spécifiée pour l’identité des connecteurs.

7.  Désactivez la synchronisation d’annuaires pour vos clients. Une fois cette étape terminée, toutes les tâches de gestion des utilisateurs seront effectuées à partir des outils de gestion Office 365. Cela signifie que vous n’utiliserez plus la console de gestion Exchange ou le Centre d’administration Exchange (CAE). Pour plus d’informations sur la procédure de désactivation de la synchronisation d’annuaires, consultez la rubrique [Désactiver la synchronisation d’annuaires](https://technet.microsoft.com/fr-fr/library/dn144760.aspx).

8.  Vous pouvez désormais désinstaller Exchange des serveurs locaux en toute sécurité.

## Scénario 2

**Problème** : mon organisation est exécutée dans une configuration hybride depuis environ un an et a enfin déplacé ma dernière boîte aux lettres dans le cloud. Je prévois de conserver les services ADFS (Active Directory Federation Services) pour l’authentification des utilisateurs de mes boîtes aux lettres Exchange Online. (Ce scénario s’appliquerait à tous les clients qui prévoient de conserver la synchronisation d’annuaires.)

**Solution** : comme le client prévoit de conserver ADFS, il devra également conserver la synchronisation d’annuaires, car il s’agit d’une condition préalable. Pour cette raison, il ne peut pas supprimer entièrement les serveurs Exchange de l’environnement local. Cependant, il peut désaffecter la plupart des serveurs Exchange, mais il en laisse quelques-uns pour la gestion des utilisateurs. N’oubliez pas que les serveurs qui continuent de fonctionner peuvent être exécutés sur des machines virtuelles car la charge de travail est presque totalement basculée vers Exchange Online.

L’illustration ci-dessous décrit l’état final souhaité :

![Désaffecter les serveurs Exchange avec des éléments restants](images/Dn931280.d7734579-6999-45b2-9a0f-a23f18353a49(EXCHG.150).jpg "Désaffecter les serveurs Exchange avec des éléments restants")

L’illustration ci-dessous décrit l’état final réel :

![État avant la désaffectation de serveurs Exchange](images/Dn931280.c692f0af-6536-4bc9-950d-58a1e486525f(EXCHG.150).jpg "État avant la désaffectation de serveurs Exchange") **Pour conserver ADFS et la synchronisation d’annuaires et désaffecter la plupart des serveurs Exchange**

1.  Exécutez `Get-OrganizationConfig |fl PublicFoldersEnabled` et assurez-vous qu’il n’est pas défini sur À distance. S’il est défini sur À distance et que vous souhaitez continuer à accéder aux dossiers publics, vous devez les migrer vers Exchange Online. Pour plus d’informations sur la façon de procéder, consultez la rubrique [Use batch migration to migrate legacy public folders to Office 365 and Exchange Online](https://technet.microsoft.com/fr-fr/library/dn874017\(v=exchg.150\)).
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Dn151301.important(EXCHG.150).gif" title="Important" alt="Important" />Important :</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Si la migration des dossiers publics vers Exchange Online n’est pas une option et que vous en avez toujours besoin pour vos utilisateurs, vous ne devez pas poursuivre.</td>
    </tr>
    </tbody>
    </table>


2.  Après avoir déplacé toutes les boîtes aux lettres vers Exchange Online, la première chose que vous pouvez faire pour désaffecter la plupart des serveurs Exchange est de pointer les enregistrements DNS de découverte automatique et MX vers Exchange Online, plutôt que vers l’environnement local. Pour plus d’informations, consultez la rubrique [Référence : Enregistrements DNS externes pour Office 365](http://technet.microsoft.com/fr-fr/library/hh852557.aspx).
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Dn151301.important(EXCHG.150).gif" title="Important" alt="Important" />Important :</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Veillez à mettre à jour les DNS interne et externe, ou vous rencontrerez peut-être des comportements de connectivité client et de flux de messagerie incohérents.</td>
    </tr>
    </tbody>
    </table>


3.  Ensuite, vous devez supprimer les valeurs de point de connexion de service sur vos serveurs Exchange. Cela garantit qu’aucun point de connexion de service n’est renvoyé, et que le client utilisera à la place la méthode DNS pour la découverte automatique. Voici un exemple :
    
        Get-ClientAccessServer | Set-ClientAccessServer -AutoDiscoverServiceInternalUri $Null
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Dn986544.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Si votre environnement comporte des serveurs Exchange 2007, vous devrez exécuter une commande similaire sur vos serveurs Exchange 2007 pour annuler les paramètres.</td>
    </tr>
    </tbody>
    </table>


4.  Pour éviter que les objets de configuration hybride soient recréés à l’avenir, vous devez supprimer l’objet de configuration hybride d’Active Directory. Pour ce faire, ouvrez l’environnement Exchange Management Shell et exécutez la commande suivante :
    
        Remove-HybridConfiguration

5.  Supprimez tous les serveurs Exchange à l’exception de ceux que vous conserverez pour la création et la gestion des utilisateurs. Deux serveurs devraient suffire pour la gestion des utilisateurs, même si vous devriez pouvoir vous en sortir avec un seul. En outre, il est inutile de disposer d’un groupe de disponibilité de base de données ou d’autres options de haute disponibilité.

6.  Si OAuth est configuré pour un déploiement hybride Exchange, vous devez désactiver la configuration à la fois en local et dans Office 365. Dans la plupart des environnements, ces étapes peuvent être ignorées car seul un petit sous-ensemble de nos clients a configuré OAuth.
    
    Pour désactiver la configuration en local, procédez comme suit :
    
    1.  Ouvrez l’environnement Exchange Management Shell à partir d’un serveur Exchange 2013.
    
    2.  Exécutez la commande suivante :
        
            Get-IntraorganizationConnector -Identity ExchangeHybridOnPremisesToOnline | Set-IntraOrganizationConnector -Enabled $False
    
    Pour désactiver la configuration Exchange Online, procédez comme suit :
    
    1.  Connectez Windows PowerShell à Exchange Online.
    
    2.  Exécutez la commande suivante :
        
            Run Get-IntraorganizationConnector -Identity ExchangeHybridOnlineToOnPremises | Set-IntraOrganizationConnector -Enabled $False
        
        Le paramètre Identity part du principe que vous avez utilisé l’Assistant Configuration hybride pour configurer OAuth. Si ce n’est pas le cas, vous devrez ajuster la valeur que vous avez spécifiée pour l’identité des connecteurs.

7.  Il y a des connecteurs entrants et sortants créés par l’Assistant Configuration hybride que vous souhaiterez supprimer. Pour ce faire, procédez comme suit :
    
    1.  Connectez-vous au [portail d’administration d’Office 365](http://portal.office.com) et ouvrez une session en tant qu’administrateur client.
    
    2.  Sélectionnez l’option de gestion d’**Exchange**.
    
    3.  Accédez à **Flux de messagerie** -\> **Connecteurs**.
    
    4.  Vous pouvez désormais désactiver ou supprimer les connecteurs entrants et sortants. L’Assistant Configuration hybride crée des connecteurs avec l’espace de noms unique **Réception depuis \<identificateur unique\>** et **Émission vers \<identificateur unique\>** comme indiqué dans l’illustration ci-dessous.
        
        ![L’Assistant Configuration hybride crée des connecteurs avec l’espace de noms unique](images/Dn931280.7b1b6f0b-43d6-4407-8cd7-7dd52e016697(EXCHG.150).jpg "L’Assistant Configuration hybride crée des connecteurs avec l’espace de noms unique")  

8.  Supprimez la relation d’organisation créée par l’Assistant Configuration hybride. Pour ce faire, procédez comme suit :
    
    1.  Connectez-vous au [portail d’administration d’Office 365](http://portal.office.com) et ouvrez une session en tant qu’administrateur client.
    
    2.  Sélectionnez l’option de gestion d’**Exchange**.
    
    3.  Accédez à **Organisation**.
    
    4.  Sous **Partage de l’organisation**, supprimez l’organisation nommée **O365 vers local – \<identificateur unique\>**, comme indiqué dans l’illustration ci-dessous.
        
        ![Supprimer la relation d’organisation créée par l’Assistant Configuration hybride](images/Dn931280.2f0c1077-8785-487a-87a5-a75f0a4f0fea(EXCHG.150).jpg "Supprimer la relation d’organisation créée par l’Assistant Configuration hybride")  

## Scénario 3

**Problème** : je veux supprimer mes serveurs Exchange locaux après avoir déplacé toutes mes boîtes aux lettres vers Exchange Online. Toutefois, nous avons découvert qu’ils utilisent Exchange à d’autres fins, par exemple pour un relais SMTP (Simple Mail Transfer Protocol) pour une application ou pour l’accès aux dossiers publics. Si vous avez besoin de serveurs Exchange locaux afin de répondre aux besoins actuels de votre organisation, il n’est peut-être pas dans votre intérêt de supprimer les serveurs locaux.

**Solution** : Nous vous déconseillons de supprimer Exchange et la configuration hybride à ce stade. Si vous deviez démarrer le processus en pointant les enregistrements de découverte automatique vers Exchange Online, vous interrompriez immédiatement certaines fonctionnalités comme l’accès aux dossiers publics hybrides. Vous pourriez modifier l’enregistrement MX afin qu’il pointe vers Exchange Online Protection si ce n’est pas déjà le cas, vous pourriez même supprimer certains des serveurs Exchange locaux. Toutefois, vous devriez en conserver suffisamment en place pour gérer les fonctions hybride restantes. En règle générale, cela entraînerait un encombrement très faible en local.

