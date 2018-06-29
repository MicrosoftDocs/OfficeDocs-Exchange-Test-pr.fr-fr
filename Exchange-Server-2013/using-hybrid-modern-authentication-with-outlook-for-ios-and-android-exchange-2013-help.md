---
title: 'ITPro_R4_Stub_80: Exchange 2013 Help'
TOCTitle: ITPro_R4_Stub_80
ms:assetid: 0e701643-1f18-4cc3-8595-4fd4b15caf6c
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Mt846639(v=EXCHG.150)
ms:contentKeyID: 74520290
ms.date: 04/25/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# ITPro\_R4\_Stub\_80

 

_**Sapplique à :**Exchange Server 2013_

_**Dernière rubrique modifiée :**2018-04-19_

**Résumé** : Découvrez comment les administrations peuvent déployer les fonctionnalités de l’authentification moderne hybride et de la suite Enterprise Mobility + Security pour qu’elles soient prises en charge par les boîtes aux lettres Exchange locales dans Outlook pour iOS et Android.

L’application Outlook pour iOS et Android est conçue pour vous permettre de profiter du meilleur d’Office 365 sur votre appareil mobile en utilisant les services Microsoft pour vous aider à effectuer des recherches, à planifier et à organiser votre vie quotidienne et professionnelle. Outlook vous offre la sécurité, la confidentialité et l’accompagnement dont vous avez besoin, tout en protégeant vos données d’entreprise grâce à des fonctionnalités telles que les stratégies d’accès conditionnel Azure Active Directory et de protection des applications Intune. Les sections suivantes présentent l’architecture de l’authentification moderne hybride, les conditions préalables à son déploiement, et la procédure à suivre pour déployer en toute sécurité Outlook pour iOS et Android pour les boîtes aux lettres Exchange locales.

## Architecture Microsoft Cloud pour les clients Exchange Server hybrides

Outlook pour iOS et Android est une application cloud. En d’autres termes, l’application installée localement est optimisée par un service sécurisé et évolutif exécuté dans Microsoft Cloud.

Pour les boîtes aux lettres Exchange Server, la conception de la nouvelle architecture Outlook pour iOS et Android est semblable à celle de son architecture héritée. Toutefois, comme le service est désormais intégré directement dans Microsoft Cloud (à l’aide d’Office 365 et de Microsoft Azure) les clients peuvent profiter de la sécurité, de la protection de la vie privée, de la conformité et de la transparence promises par Microsoft dans le [Centre de gestion de la confidentialité Office 365](https://products.office.com/business/office-365-trust-center-welcome) et le [Centre de confidentialité Azure](https://www.microsoft.com/trustcenter/cloudservices/azure).

![Diagramme de l’architecture de l’authentification moderne hybride dans Outlook pour iOS et Android](images/Mt846639.20a7e963-916d-47e0-bffb-4d86c4777bea(EXCHG.150).png "Diagramme de l’architecture de l’authentification moderne hybride dans Outlook pour iOS et Android")

Les données sont transmises d’Exchange Online à l’application Outlook via une connexion sécurisée TLS. Le traducteur de protocole exécuté sur Azure achemine les données, les commandes et les notifications, mais il ne peut pas lire les données.

La connexion Exchange ActiveSync entre l’environnement local et Exchange Online facilite la synchronisation des données des utilisateurs situées dans l’environnement local. Elle comporte quatre semaines de données liées au courrier, au calendrier, aux contacts et aux statuts d’absence du bureau dans votre client Exchange Online. Ces données seront automatiquement supprimées d’Exchange Online 30 jours après la suppression du compte dans Azure Active Directory.

La synchronisation des données entre l’environnement local et Exchange Online se produit indépendamment du comportement de l’utilisateur. Ainsi, nous pouvons envoyer de nouveaux messages aux appareils très rapidement.

Le traitement des informations dans Microsoft Cloud offre des fonctionnalités avancées, comme la classification des e-mails dans la boîte de réception Prioritaire, une expérience personnalisée avec les applications Voyage et Calendrier et une vitesse de recherche améliorée. En traitant vos informations de manière intensive dans le cloud et en limitant les ressources requises des appareils des utilisateurs, vous profitez d’une application plus performante et plus stable. Enfin, Outlook peut créer des fonctionnalités qui fonctionnent sur tous les comptes de courrier, quelles que soient les fonctionnalités technologiques des serveurs sous-jacents (en cas de versions différentes d’Exchange Server ou d’Office 365, par exemple).

Plus précisément, cette nouvelle architecture confère les améliorations suivantes :

1.  **Prise en charge de la suite Enterprise Mobility + Security** : les clients peuvent utiliser Microsoft Enterprise Mobility + Security (EMS), y compris Microsoft Intune et Azure Active Directory Premium, pour activer les stratégies d’accès conditionnel et de protection des applications Intune, qui contrôlent et protègent les données d’entreprise dans les messages de l’appareil mobile.

2.  **Activation totale par Microsoft Cloud** : les données de boîte aux lettres locales sont synchronisées dans Exchange Online, garantissant ainsi la sécurité, la protection de la vie privée, la conformité et la transparence promises par Microsoft dans le [Centre de gestion de la confidentialité d’Office 365](https://products.office.com/business/office-365-trust-center-welcome).

3.  **Protection des mots de passe des utilisateurs par OAuth** : Outlook utilise l’authentification moderne hybride (OAuth) pour protéger les informations d’identification des utilisateurs. L’authentification moderne hybride permet à Outlook d’accéder de manière sécurisée aux données Exchange sans toucher aux informations d’identification d’un utilisateur, ni les enregistrer. Au moment de se connecter, l’utilisateur s’authentifie directement sur une plateforme d’identité (Azure Active Directory ou un fournisseur d’identité local comme ADFS) et reçoit en retour un jeton d’accès qui autorise Outlook à accéder à la boîte aux lettres ou aux fichiers de l’utilisateur. À aucun moment le service n’a accès au mot de passe de l’utilisateur.

4.  **ID d’appareil uniques fournis** : chaque connexion à Outlook est inscrite de façon unique dans Microsoft Intune et peut ainsi être gérée comme une connexion unique.

5.  **Nouvelles fonctionnalités sur iOS et Android** : cette mise à jour permet à l’application Outlook d’utiliser des fonctionnalités Office 365 natives qui ne sont, pour l’instant, pas prises en charge dans l’environnement Exchange local (par exemple, la recherche complète Exchange Online et la boîte de réception Prioritaire). Ces fonctionnalités sont uniquement disponibles quand vous utilisez Outlook pour iOS et Android.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Il est impossible de gérer des appareils via le Centre d’administration Exchange local. Pour cela, utilisez Intune.</td>
</tr>
</tbody>
</table>


## Sécurité des données, accès et contrôles d’audit

Les clients se posent des questions concernant la protection des données synchronisées dans Exchange Online. Le livre blanc sur le [chiffrement des données dans le Microsoft Cloud](http://aka.ms/office365ce) explique comment les données sont chiffrées par volume avec BitLocker. Comme l’explique le livre blanc, le chiffrement des données de service avec l’option Clé client est pris en charge dans l’architecture d’Outlook pour iOS et Android. Cependant, l’utilisateur doit disposer d’une licence Office 365 Entreprise E5 (ou les versions correspondantes de ces plans pour le secteur public ou l’éducation) pour qu’une stratégie de chiffrement lui soit affectée.

Par défaut, les ingénieurs Microsoft ne disposent d’aucun privilège administratif permanent et d’aucun accès permanent au contenu du client dans Office 365. Le livre blanc sur les [contrôles d’accès administratifs d’Office 365](http://aka.ms/office365aac) traite notamment du filtrage, des vérifications des antécédents du personnel, du référentiel sécurisé et du référentiel sécurisé du client.

Le document relatif aux [contrôles audités ISO sur la certification de Service](https://sip.protection.office.com/) fournit l’état des contrôles audités au regard des normes et des réglementations appliquées par Office 365 dans le domaine de la sécurité des informations.

## Flux de connexion

Quand Outlook pour iOS et Android est activé avec l’authentification moderne hybride, le flux de connexion se met en place de la manière suivante.

![Flux d’authentification dans l’authentification moderne hybride](images/Mt846639.d6e20ddb-cf8e-4154-8a17-95657ef696d1(EXCHG.150).png "Flux d’authentification dans l’authentification moderne hybride")

1.  Quand l’utilisateur a entré son adresse e-mail, Outlook pour iOS et Android se connecte au service AutoDetect. Ce service détermine le type de boîte aux lettres en envoyant une requête de découverte automatique à Exchange Online. Exchange Online détermine que la boîte aux lettres de l’utilisateur est locale et renvoie une redirection 302 à AutoDetect avec l’URL de découverte automatique locale. AutoDetect envoie une requête auprès du service de découverte automatique local pour déterminer le point de terminaison ActiveSync pour l’adresse e-mail. L’URL tentée en local est semblable à l’URL suivante : https://autodiscover.contoso.com/autodiscover/autodiscover.json?Email=test%40contoso.com\&Protocol=activesync\&RedirectCount=3.

2.  AutoDetect établit une connexion à l’URL ActiveSync locale renvoyée à l’étape 1 précédente avec un défi de porteur vide. Le défi de porteur vide indique à l’environnement ActiveSync local que le client prend en charge l’authentification moderne. L’environnement ActiveSync local renvoie une réponse de stimulation 401 et inclut l’en-tête *WWW-Authenticate: Bearer*. Dans cet en-tête figure la valeur authorization\_uri qui identifie le point de terminaison Azure Active Directory (AAD) à utiliser pour obtenir un jeton OAuth.

3.  AutoDetect renvoie le point de terminaison AAD au client. Le client démarre le flux de connexion et l’utilisateur voit s’afficher un formulaire web (ou il est redirigé vers l’application Microsoft Authenticator) dans lequel il peut entrer ses informations d’identification. Selon la configuration de l’identité, cela peut entraîner la redirection du point de terminaison fédéré vers un fournisseur d’identité local. Enfin, le client obtient une paire de jetons d’accès-actualisation, intitulée AT1/RT1. Ce jeton d’accès est étendu au client Outlook pour iOS et Android avec une audience du point de terminaison Exchange Online.

4.  Outlook pour iOS et Android établit une connexion au traducteur de protocole sans état où le protocole de l’appareil propriétaire du client est traduit en un protocole que comprend Exchange Online.

5.  Une demande d’attribution de privilèges d’accès est transmise à Exchange Online. Elle comprend le jeton d’accès de l’utilisateur (AT1) et le point de terminaison ActiveSync local.

6.  L’API d’attribution de privilèges d’accès MRS dans Exchange Online utilise AT1 comme entrée et obtient une deuxième paire de jetons d’accès-actualisation (appelée AT2/RT2) pour accéder à la boîte aux lettres locale via un appel « de la part de » à Azure Active Directory. Ce deuxième jeton d’accès est étendu au client Exchange Online et à une audience du point de terminaison d’espace de noms ActiveSync local.

7.  Si la boîte aux lettres n’est pas configurée, l’API d’attribution de privilèges d’accès crée une boîte aux lettres.

8.  L’API d’attribution de privilèges d’accès MRS établit une connexion sécurisée au point de terminaison ActiveSync local et synchronise les données de messagerie de l’utilisateur à l’aide du jeton d’accès AT2 comme mécanisme d’authentification. Ce jeton d’accès est étendu au client Outlook pour iOS et Android avec une audience du point de terminaison Exchange Online. RT2 est régulièrement utilisé pour générer un nouvel AT2 afin que les données puissent être synchronisées en arrière-plan sans intervention de l’utilisateur. Ce jeton d’accès est étendu au client Outlook pour iOS et Android avec une audience du point de terminaison Exchange Online.

## Exigences techniques et critères de licence

L’architecture de l’authentification moderne hybride comporte les exigences techniques suivantes :

1.  **Configuration de l’environnement Exchange local** :
    
      - la mise à jour cumulative doit être au minimum déployée sur tous les serveurs Exchange d’Exchange Server 2016 CU8 ou d’Exchange Server 2013 CU19. Notez que les clients qui possèdent des déploiements hybrides où Exchange est déployé dans l’environnement local et dans le cloud, ou qui utilisent l’Archivage Exchange Online avec leur déploiement Exchange local, doivent déployer la mise à jour cumulative la plus récente ou la mise à jour précédente.
    
      - Tous les serveurs Exchange 2007 ou Exchange 2010 doivent être supprimés de l’environnement. Exchange Server 2010 SP3 n’est pas pris en charge et ne fonctionnera pas avec Outlook pour iOS et Android géré dans Intune. Dans cette architecture, Outlook pour iOS et Android utilise OAuth comme mécanisme d’authentification. L’un des changements de configuration effectué en local active le point de terminaison OAuth dans le Microsoft Cloud comme point de terminaison d’autorisation par défaut. Lorsque ce changement est effectué, les clients peuvent commencer à négocier l’utilisation de OAuth. Comme il s’agit d’un changement réalisé à l’échelle de l’organisation, les boîtes aux lettres Exchange 2010 affichées par Exchange 2013 ou 2016 considèrent à tort qu’elles peuvent exécuter OAuth et finissent par se déconnecter, car Exchange 2010 ne prend pas en charge OAuth comme mécanisme d’authentification.

2.  **Synchronisation Active Directory** : la synchronisation Active Directory synchronise tout le répertoire local avec Azure Active Directory via Azure AD Connect. Vérifiez que les attributs suivants sont synchronisés :
    
      - Office 365 ProPlus
    
      - Exchange Online
    
      - Écriture différée hybride Exchange
    
      - Azure RMS
    
      - Intune

3.  **Configuration hybride d’Exchange** : une relation hybride complète doit exister entre l’environnement Exchange local et Exchange Online.
    
      - Le client Office 365 hybride doit être configuré en mode de configuration hybride complète selon les explications fournies dans l’[Assistant de déploiement Exchange Server](http://technet.microsoft.com/exdeploy).
    
      - Un client Office 365 Entreprise, Business ou Éducation est requis.
    
      - Les données de la boîte aux lettres locale sont synchronisées dans la même région de centre de données que celle où ce client Office 365 est configuré. Pour en savoir plus sur l’emplacement des données Office 365, consultez la section [Emplacement de vos données](http://o365datacentermap.azurewebsites.net/) dans le Centre de gestion de la confidentialité Office 365.
    
      - L’utilisation de clients Office 365 pour le gouvernement américain (Défense et communauté), de clients Office 365 allemands et de clients Office 365 chinois gérés par des clients 21Vianet n’est pas prise en charge.
    
      - Les noms d’hôte d’URL externe pour Exchange ActiveSync et le service de découverte automatique doivent être publiés en tant que principaux de service sur Azure Active Directory via l’Assistant Configuration hybride.
    
      - Les espaces de noms d’Exchange ActiveSync et du service de découverte automatique doivent être accessibles sur Internet et ne peuvent pas être affichés par une solution de pré-authentification.
    
      - Vérifiez que le déchargement SSL ou TLS n’est pas utilisé entre l’équilibreur de charge et vos serveurs Exchange, car cela aurait une incidence sur l’utilisation du jeton OAuth. Le pontage SSL et TLS (arrêt et rechiffrement) est pris en charge.

4.  **Configuration d’Intune** : les déploiements cloud et hybrides d’Intune sont pris en charge. (La gestion des périphériques mobiles pour Office 365 n’est pas prise en charge.)

5.  **Gestion des licences Office 365\*** : chaque utilisateur doit disposer de l’une des licences Office 365 suivantes :
    
      - Commercial : licences Entreprise E3, Entreprise E5, ProPlus ou Business
    
      - Administration : Informations d’identification personnelle Communauté Office 365 pour le gouvernement américain G3 Communauté Office 365 pour le gouvernement américain G5
    
      - Éducation : Office 365 Éducation E3, Office 365 Éducation E5
    
    Par ailleurs, les licences doivent inclure les applications clientes Office requises pour utiliser Outlook pour iOS et Android à des fins commerciales.

6.  **Gestion des licences EMS\*** : chaque utilisateur de l’environnement local doit disposer de l’une des licences suivantes :
    
      - Intune autonome + Azure Active Directory Premium autonome
    
      - Enterprise Mobility + Security E3, Enterprise Mobility + Security E5

**\*** Microsoft Secure Productive Enterprise (SPE) inclut toutes les licences requises pour Office 365 et EMS.

## Étapes d’implémentation

Pour implémenter l’authentification moderne hybride dans votre organisation, suivez les procédures détaillées dans les sections suivantes :

1.  Créer une stratégie d’accès conditionnel

2.  Créer une stratégie de protection des applications Intune

3.  Activer l’authentification moderne hybride

4.  Contacter Microsoft

## Créer une stratégie d’accès conditionnel

Quand une organisation décide de standardiser les méthodes d’accès aux données Exchange (avec Outlook pour iOS et Android comme seule application de messagerie utilisée par les utilisateurs finaux), les administrateurs peuvent configurer une stratégie d’accès conditionnel qui bloque les autres méthodes d’accès mobile. Outlook pour iOS et Android authentifie via l’objet d’identité Azure Active Directory, puis se connecte à Exchange Online. Par conséquent, nous vous recommandons de créer des stratégies d’accès conditionnel Azure Active Directory pour limiter l’accès des appareils mobiles à Exchange Online. Pour cela, vous avez besoin de deux stratégies d’accès conditionnel, qui ciblent chacune tous les utilisateurs potentiels. Pour savoir comment créer ces stratégies, consultez l’article [Accès conditionnel basé sur les applications Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-mam#exchange-online-policy).

1.  La première stratégie autorise Outlook pour iOS et Android à se connecter à Exchange Online et empêche les clients Exchange ActiveSync compatibles OAuth de le faire. Consultez l’« Étape 1 : configurer une stratégie d’accès conditionnel Azure AD pour Exchange Online ».

2.  La deuxième stratégie empêche les clients Exchange ActiveSync qui utilisent l’authentification de base de se connecter à Exchange Online. Consultez l’« Étape 2 : configurer une stratégie d’accès conditionnel Azure AD pour Exchange Online avec Exchange Active Sync (EAS) ».

Les stratégies utilisent le contrôle d’autorisation [Nécessite une application cliente approuvée](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-technical-reference). Il garantit que seules les applications Microsoft qui ont intégré le Kit de développement logiciel (SDK) Intune bénéficient de droits d’accès.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159813.important(EXCHG.150).gif" title="Important" alt="Important" />Important :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Pour recourir à des stratégies d’accès conditionnel basées sur l’application, l’application Microsoft Authenticator doit être installée sur les appareils iOS. Pour les appareils Android, c’est le Portail d’entreprise Intune qui est utilisé. Pour en savoir plus, consultez l’article <a href="https://docs.microsoft.com/intune/app-based-conditional-access-intune">Accès conditionnel basé sur l’application avec Intune</a>.</td>
</tr>
</tbody>
</table>


Pour empêcher d’autres clients de l’appareil mobile (par exemple, le client de messagerie native inclus dans le système d’exploitation mobile) de se connecter à votre environnement local (qui s’authentifie via l’authentification de base auprès d’Active Directory local), deux options s’offrent à vous :

1.  Vous pouvez utiliser les règles d’accès des appareils mobiles Exchange intégrées et empêcher tous les appareils mobiles de se connecter en définissant la commande suivante dans l’environnement de ligne de commande Exchange Management Shell :
    
        Set-ActiveSyncOrganizationSettings -DefaultAccessLevel Block

2.  Vous pouvez utiliser une stratégie d’accès conditionnel local dans Intune après avoir installé le connecteur Exchange local. Pour en savoir plus, consultez l’article [Créer une stratégie d’accès conditionnel pour Exchange sur site et Exchange Online Dedicated hérité](https://docs.microsoft.com/intune/conditional-access-exchange-create#configure-exchange-on-premises-access).

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Au moment d’implémenter l’une de ces options dans l’environnement local, n’oubliez pas que cela peut affecter les utilisateurs qui se connectent à Exchange sur leurs appareils mobiles.</td>
</tr>
</tbody>
</table>


## Créer une stratégie de protection des applications Intune

Une fois l’authentification moderne hybride activée, tous les utilisateurs d’appareils mobiles dans l’environnement local peuvent utiliser Outlook pour iOS et Android à l’aide de l’architecture Office 365. Par conséquent, il est important de protéger les données d’entreprise à l’aide d’une stratégie de protection des applications Intune.

Créez des stratégies de protection des applications Intune pour iOS et Android en suivant les étapes décrites dans l’article [Guide pratique de gestion et affectation des stratégies de protection des applications](https://docs.microsoft.com/intune/app-protection-policies). Chaque stratégie doit au minimum remplir les conditions suivantes :

1.  Elles doivent inclure toutes les applications mobiles Microsoft, telles que Word, Excel ou PowerPoint, pour que les utilisateurs puissent accéder aux données d’entreprise et les manipuler de manière sécurisée dans toutes les applications Microsoft.

2.  Elles doivent imiter les fonctionnalités de sécurité fournies par Exchange pour les appareils mobiles, notamment :
    
      - Demande du code confidentiel d’accès (avec les paramètres Sélectionner le type, Longueur du code PIN, Autoriser un code PIN simple, Autoriser une empreinte digitale)
    
      - Chiffrement des données de l’application
    
      - Blocage des applications gérées sur les appareils « jailbreakés » et rootés

3.  Elles doivent être affectées à tous les utilisateurs. Cela permet de garantir la protection de tous les utilisateurs, qu’ils utilisent Outlook pour iOS et Android ou non.

Par ailleurs, songez à déployer des paramètres de stratégie de protection avancée, tels que **Restreindre les opérations Couper, copier et coller avec d’autres applications** pour prévenir les fuites des données d’entreprise. Pour en savoir plus sur les paramètres disponibles, consultez les articles [Paramètres de la stratégie de protection des applications Android dans Microsoft Intune](https://docs.microsoft.com/intune/app-protection-policy-settings-android) et [Paramètres de stratégie de protection d’application iOS](https://docs.microsoft.com/intune/app-protection-policy-settings-ios).

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159813.important(EXCHG.150).gif" title="Important" alt="Important" />Important :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Pour appliquer les stratégies de protection des applications Intune pour les applications des appareils Android non inscrits dans Intune, l’utilisateur doit également installer le portail d’entreprise Intune. Pour en savoir plus, consultez l’article <a href="https://docs.microsoft.com/fr-fr/intune/app-protection-enabled-apps-android">Ce qui se passe quand votre application Android est gérée par des stratégies de protection d’application</a>.</td>
</tr>
</tbody>
</table>


## Activer l’authentification moderne hybride

Si vous n’avez pas activé l’authentification moderne hybride, consultez et suivez les étapes décrites dans l’article sur [l’authentification moderne hybride et les conditions préalables pour l’utiliser avec Skype en local pour les entreprises et les serveurs Exchange](https://support.office.com/article/hybrid-modern-authentication-overview-and-prerequisites-for-using-it-with-on-premises-skype-for-business-and-exchange-servers-ef753b32-7251-4c9e-b442-1a5aec14e58d?).

Si vous avez déjà activé l’authentification moderne hybride pour prendre en charge d’autres versions d’Outlook, y compris Outlook pour Mac, pour vos utilisateurs locaux, en suivant les étapes décrites dans l’article [Comment configurer Exchange Server en local pour utiliser l’authentification moderne hybride](https://support.office.com/article/how-to-configure-exchange-server-on-premises-to-use-hybrid-modern-authentication-cef3044d-d4cb-4586-8e82-ee97bd3b14ad?), quelques étapes supplémentaires sont nécessaires :

1.  Créez une règle d’autorisation d’accès des appareils Exchange pour autoriser Exchange Online à se connecter à votre environnement local à l’aide du protocole ActiveSync :
    
        If ((Get-ActiveSyncOrganizationSettings).DefaultAccessLevel -ne "Allow") {New-ActiveSyncDeviceAccessRule -Characteristic DeviceType -QueryString "OutlookService" -AccessLevel Allow}
    
    Notez qu’il n’est pas possible de gérer les appareils via le Centre d’administration Exchange local. Pour cela, utilisez Intune.

2.  Créez une règle d’accès des appareils Exchange qui empêche les utilisateurs de se connecter à l’environnement local avec Outlook pour iOS et Android avec l’authentification de base via le protocole Exchange ActiveSync :
    
        New-ActiveSyncDeviceAccessRule -Characteristic DeviceModel -QueryString "Outlook for iOS and Android" -AccessLevel Block
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Une fois cette règle créée, les utilisateurs qui utilisent Outlook pour iOS et Android avec l’authentification de base sont bloqués.</td>
    </tr>
    </tbody>
    </table>


3.  Vérifiez que la propriété maxRequestLength d’EAS correspond à la propriété MaxSendSize/MaxReceiveSize de votre configuration de transport :
    
      - Chemin : `%ExchangeInstallPath%FrontEnd\HttpProxy\Sync\web.config`
    
      - Propriété : `maxRequestLength`
    
      - Valeur : définie en Ko (10 Mo est 10 240, par exemple)

## Contacter Microsoft

Pour qu’Outlook pour iOS et Android prenne en charge l’authentification moderne hybride, contactez l’équipe des comptes Microsoft, votre interlocuteur du service client ou votre responsable technique de compte. Vous devrez fournir tous les domaines SMTP (et les domaines UPN si vos domaines UPN ne correspondent pas à l’adresse SMTP). Une fois les domaines fournis et activés, l’authentification moderne hybride sera prise en charge pour les boîtes aux lettres locales qui utilisent Outlook pour iOS et Android.

## Fonctionnalités clientes non prises en charge

Les fonctionnalités suivantes ne sont pas prises en charge pour les boîtes aux lettres locales qui utilisent l’authentification moderne hybride avec Outlook pour iOS et Android.

  - Synchronisation du dossier Brouillons et des Brouillons

  - Accès partagé et accès délégué au calendrier

  - Notifications Heure du départ de Cortana

  - Pièces jointes de calendrier

  - Gestion des tâches avec Microsoft To-Do

## FAQ sur le flux de connexion

**Q** : La stratégie de sécurité de mon organisation exige que les connexions entrantes Internet soient limitées aux adresses IP ou aux noms de domaine complets (FQDN) approuvés. Est-ce possible avec cette architecture ?

**R** : Microsoft recommande que les points de terminaison locaux pour les protocoles ActiveSync et découverte automatique soient ouverts et accessibles sur Internet sans aucune restriction. Ce n’est pas toujours possible dans certains cas. Par exemple, si votre environnement coexiste avec une autre solution de gestion des périphériques mobiles, nous vous recommandons d’imposer des restrictions au protocole ActiveSync pour empêcher les utilisateurs de contourner la solution de gestion des périphériques mobiles tierce pendant que vous migrez vers Intune et Outlook pour iOS et Android. Si des restrictions doivent être imposées à votre pare-feu local ou à vos appareils de passerelle Edge, Microsoft vous recommande de filtrer les points de terminaison des FQDN. Si vous ne pouvez pas utiliser les points de terminaison des FQDN, filtrez les adresses IP. Vérifiez que les sous-réseaux IP et les FQDN suivants figurent dans la liste verte :

  - Toutes les plages de sous-réseaux IP et les URL d’Exchange Online figurant dans l’article [URL et plages d’adresses IP Office 365](https://support.office.com/article/office-365-urls-and-ip-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2).

  - Tous les FQDN de l’application Outlook iOS et Android figurant dans l’article [Requêtes réseau dans Office 365 ProPlus et Mobile](https://support.office.com/article/network-requests-in-office-365-proplus-and-mobile-eb73fcd1-ca88-4d02-a74b-2dd3a9f3364d?).

  - Tous les sous-réseaux IP des centres de données américains et européens figurant dans l’article relatif aux [plages d’adresses IP du centre de données Microsoft Azure](https://www.microsoft.com/download/details.aspx?id=41653). Le service de détection automatique établit des connexions à l’infrastructure locale, comme décrit dans la section Flux de connexion. Pour l’instant, le service de détection automatique n’utilise pas les réservations IP dans Azure.

**Q** : Mon organisation utilise une solution de gestion des périphériques mobiles tierce pour contrôler l’accès des appareils mobiles. Si j’expose l’espace de noms Exchange ActiveSync sur Internet, les utilisateurs pourront contourner la solution de gestion des périphériques mobiles tierce pendant la période de co-existence. Comment l’éviter ?

**R** : Il existe trois solutions possibles pour résoudre ce problème :

1.  Implémentez des règles d’accès des appareils mobiles Exchange pour contrôler les appareils qui sont autorisés à se connecter.

2.  Certaines solutions de gestion des périphériques mobiles tierces s’intègrent aux règles d’accès des appareils mobiles Exchange, et bloquent les accès non approuvés, tout en ajoutant les appareils approuvés dans la propriété ActiveSyncAllowedDeviceIDs de l’utilisateur.

3.  Implémentez les restrictions IP à l’espace de noms Exchange ActiveSync.

**Q** : Puis-je utiliser Azure ExpressRoute pour gérer le trafic entre Microsoft Cloud et mon environnement local ?

**R** : Pour vous connecter à Microsoft Cloud, vous avez besoin d’une connexion Internet. Toutefois, un sous-ensemble du trafic réseau Office 365 peut être acheminé via Azure ExpressRoute. Pour en savoir plus, consultez l’article [Azure ExpressRoute pour Office 365](https://support.office.com/article/azure-expressroute-for-office-365-6d2534a2-c19c-4a99-be5e-33a0cee5d3bd).

Avec ExpressRoute, il n’existe aucun espace IP privé pour les connexions ExpressRoute, ni aucune résolution DNS « privée ». En d’autres termes, les points de terminaison que votre entreprise souhaite utiliser via ExpressRoute doivent être résolus en DNS publics. Si ce point de terminaison est résolu en adresse IP présente dans les préfixes publiés associés au circuit ExpressRoute (votre entreprise doit configurer ces préfixes dans le portail Azure quand vous activez l’appairage Microsoft sur la connexion ExpressRoute), la connexion sortante entre Exchange Online et votre environnement local est acheminée via le circuit ExpressRoute. Votre entreprise doit s’assurer que le trafic de retour associé à ces connexions est acheminé via le circuit ExpressRoute (en évitant un routage asymétrique).

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Comme votre entreprise ajoute l’espace de noms Exchange ActiveSync aux préfixes publiés dans le circuit ExpressRoute, la seule façon d’atteindre le point de terminaison Exchange ActiveSync est de passer par ExpressRoute. En d’autres termes, Outlook pour iOS et Android est le seul appareil mobile qui peut se connecter à l’environnement local via l’espace de noms ActiveSync. Tous les autres clients ActiveSync (par exemple, les clients de messagerie natifs des appareils mobiles) ne peuvent pas se connecter à l’environnement local car la connexion n’est pas établie à partir du Microsoft Cloud. En effet, l’espace IP public publié sur Microsoft sur le circuit ExpressRoute et l’espace IP public publié sur votre ou vos circuit(s) Internet ne peuvent pas se chevaucher.</td>
</tr>
</tbody>
</table>


**Q** : Si seules quatre semaines de données de courrier sont synchronisées vers Exchange Online, est-ce que les requêtes de recherche exécutées dans Outlook pour iOS et Android peuvent renvoyer d’autres informations en plus des données disponibles sur l’appareil local ?

**R** : Quand une requête de recherche est exécutée dans Outlook pour iOS et Android, les éléments correspondant à la requête de recherche sont renvoyés s’ils se trouvent sur l’appareil. Par ailleurs, la requête de recherche est transmise à l’environnement Exchange local via Exchange Online. L’environnement Exchange local exécute la requête de recherche auprès de la boîte aux lettres locale et renvoie le résultat à Exchange Online, qui relaie les résultats au client. Les résultats de la requête locale sont stockés dans Exchange Online pendant un jour avant d’être supprimés.

**Q** : Comment savoir si le compte de courrier est correctement ajouté dans Outlook pour iOS et Android ?

**R** : Les boîtes aux lettres locales ajoutées via l’authentification moderne hybride sont étiquetées **Exchange (hybride)** dans les paramètres du compte Outlook pour iOS et Android, comme dans l’exemple suivant :

![Exemple d’un compte Outlook pour iOS et Android configuré pour l’authentification moderne hybride](images/Mt846639.79887a65-e5e1-4501-a274-008393dbb6c9(EXCHG.150).png "Exemple d’un compte Outlook pour iOS et Android configuré pour l’authentification moderne hybride")

## FAQ sur l’authentification

**Q** : Quelles sont les configurations d’identité prises en charge avec l’authentification moderne hybride et Outlook pour iOS et Android ?

**R** : Les configurations d’identité suivantes, réalisées avec Azure Active Directory, sont prises en charge avec l’authentification moderne hybride :

  - Identité fédérée avec un fournisseur d’identité local pris en charge par Azure Active Directory

  - Synchronisation de hachage du mot de passe via Azure Active Directory Connect

  - Authentification directe via Azure Active Directory Connect

**Q** : Quel mécanisme d’authentification est utilisé pour Outlook pour iOS et Android ? Les informations d’identification sont-elles stockées dans Office 365 ?

**R** : Outlook pour iOS et Android utilise l’authentification basée sur la bibliothèque d’authentification Active Directory (ADAL) pour accéder aux données des boîtes aux lettres locales synchronisées avec Exchange Online. L’authentification ADAL, utilisée par les applications Office de bureau et mobiles, demande aux utilisateurs de se connecter directement à Azure Active Directory, fournisseur d’identité Office 365, au lieu de fournir des informations d’identification à Outlook.

La connexion basée sur la bibliothèque d’authentification Active Directory permet d’accéder aux comptes hybrides de l’environnement Exchange local via OAuth, et offre à Outlook pour iOS et Android un mécanisme sécurisé pour accéder au courrier électronique sans demander l’accès aux informations d’identification de l’utilisateur. Pour se connecter, l’utilisateur s’authentifie directement auprès du Cloud de Microsoft et reçoit en retour un jeton d’accès. Le jeton permet à Outlook pour iOS et Android d’accéder à la boîte aux lettres appropriée. OAuth fournit à Outlook un mécanisme sécurisé pour accéder à Office 365 et au service cloud Outlook sans demander ou enregistrer les informations d’identification d’un utilisateur.

Pour en savoir plus, consultez le billet de blog d’Office sur les [nouveaux contrôles d’accès et de sécurité pour Outlook pour iOS et Android](https://blogs.office.com/2015/06/10/new-access-and-security-controls-for-outlook-for-ios-and-android/).

**Q** : Est-ce qu’Outlook pour iOS et Android et d’autres applications mobiles Microsoft Office prennent en charge l’authentification unique ?

**R** : Toutes les applications Microsoft qui exploitent la Bibliothèque d’authentification Azure Active Directory (ADAL) prennent en charge l’authentification unique. Par ailleurs, l’authentification unique est également prise en charge quand les applications sont utilisées avec les applications Microsoft Authenticator ou Portail d’entreprise Microsoft.

Les jetons peuvent être partagés et réutilisés par d’autres applications Microsoft (par exemple, Word Mobile) dans les scénarios suivants :

1.  Lorsque les applications sont signées par le même certificat de signature et utilisent la même URL d’audience ou de point de terminaison (par exemple, l’URL Office 365). Dans ce cas, le jeton est conservé dans le stockage partagé de l’application.

2.  Lorsque les applications exploitent ou prennent en charge l’authentification unique avec une application Broker. Les jetons sont stockés dans l’application Broker. Microsoft Authenticator est un exemple d’application Broker. Dans le scénario de l’application Broker, une fois que vous aurez essayé de vous connecter à Outlook pour iOS et Android, ADAL lancera l’application Microsoft Authenticator, qui se connectera à Azure Active Directory pour obtenir le jeton. Elle conservera ensuite le jeton et le ré-utilisera pour les demandes d’authentification d’autres applications, tant que la durée de vie configurée du jeton le permettra.

Pour en savoir plus, consultez l’article [Activation d’une authentification unique entre applications sur iOS à l’aide de la bibliothèque ADAL](https://docs.microsoft.com/azure/active-directory/develop/active-directory-sso-ios).

**Q** : Quelle est la durée de vie des jetons générés et utilisés par la bibliothèque ADAL dans Outlook pour iOS et Android ?

**R** : Quand un utilisateur s’authentifie via les applications compatibles avec ADAL, comme Outlook pour iOS et Android, l’application Authenticator ou l’application Portail d’entreprise, plusieurs jetons sont générés. La première paire de jetons d’accès et d’actualisation sert à accéder aux données synchronisées dans Exchange Online ; la deuxième paire de jetons d’accès et d’actualisation est utilisée par Exchange Online pour accéder à la boîte aux lettres locale via le protocole Exchange ActiveSync. Le jeton d’accès permet d’accéder à la ressource (les données du message Exchange, par exemple), tandis que le jeton d’actualisation sert à obtenir une nouvelle paire de jetons d’accès ou d’actualisation à l’expiration du jeton d’accès en cours.

Par défaut, la durée de vie du jeton d’accès est d’une heure et celle du jeton d’actualisation est de 14 jours. Ces valeurs peuvent être ajustées. Pour en savoir plus, consultez l’article [Durées de vie des jetons configurables dans Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-configurable-token-lifetimes). Notez que si vous choisissez de réduire ces durées de vie, vous pouvez aussi réduire les performances d’Outlook pour iOS et Android, car une durée de vie plus courte augmente le nombre de demandes de remplacement du jeton d’accès.

**Q** : Qu’advient-il du jeton d’accès quand le mot de passe d’un utilisateur est modifié ?

**R** : Un jeton d’accès précédemment accordé est valide jusqu’à son expiration. Le modèle d’identité que vous utilisez pour l’authentification a également un impact sur la gestion de l’expiration du mot de passe. Il existe trois scénarios :

1.  Pour un modèle d’identité fédérée, vérifiez que votre fournisseur d’identité local envoie des revendications d’expiration du mot de passe à Azure Active Directory. Dans le cas contraire, Azure Active Directory ne peut pas modifier la date d’expiration du mot de passe. Pour en savoir plus, consultez l’article [Configurer ADFS pour envoyer des revendications d’expiration de mot de passe](https://docs.microsoft.com/windows-server/identity/ad-fs/operations/configure-ad-fs-to-send-password-expiry-claims).

2.  La synchronisation de hachage du mot de passe ne prend pas en charge l’expiration du mot de passe. En d’autres termes, les applications qui avaient précédemment obtenu une paire de jetons d’accès et d’actualisation continuent de fonctionner jusqu’à ce que la durée de vie de la paire de jetons expire ou que l’utilisateur modifie son mot de passe. Pour en savoir plus, consultez [Implémenter la synchronisation de hachage de mot de passe avec la synchronisation Azure AD Connect](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnectsync-implement-password-hash-synchronization#how-password-synchronization-works).

3.  L’authentification directe nécessite l’activation de l’écriture différée du mot de passe dans AAD Connect. Pour en savoir plus, consultez l’article [Authentification directe Azure Active Directory : forum aux questions](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-pass-through-authentication-faq#what-happens-if-my-users-password-has-expired-and-they-try-to-sign-in-by-using-pass-through-authentication).

Jusqu’à l’expiration du jeton, le client peut essayer d’utiliser le jeton d’actualisation pour obtenir un nouveau jeton d’accès, mais, puisque le mot de passe de l’utilisateur a changé, le jeton d’actualisation sera invalidé (à condition que les répertoires locaux et Azure Active Directory aient été synchronisés). Le jeton d’actualisation invalidé oblige l’utilisateur à se ré-authentifier pour obtenir une nouvelle paire de jetons d’accès et d’actualisation.

**Q** : L’utilisateur peut-il contourner la détection automatique quand il ajoute son compte à Outlook pour iOS et Android ?

**R** : Oui, un utilisateur peut contourner la détection automatique à tout moment et configurer manuellement la connexion à l’aide de l’authentification de base via le protocole Exchange ActiveSync. Pour vous assurer que l’utilisateur ne se connecte pas à votre environnement local via un mécanisme qui ne prend pas en charge les stratégies d’accès conditionnel Azure Active Directory ou de protection des applications Intune, l’administrateur Exchange local doit configurer une règle d’accès des appareils Exchange qui bloque la connexion ActiveSync. Pour cela, exécutez la commande suivante dans l’environnement de ligne de commande Exchange Management Shell :

``` 
 New-ActiveSyncDeviceAccessRule -Characteristic DeviceModel -QueryString "Outlook for iOS and Android" -AccessLevel Block
```

