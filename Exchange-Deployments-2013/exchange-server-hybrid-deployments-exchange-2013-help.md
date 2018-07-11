---
title: 'Déploiements hybrides Exchange Server: Exchange 2013 Help'
TOCTitle: '@NoTitle'
ms:assetid: 59e32000-4fcf-417f-a491-f1d8f9aeef9b
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ200581(v=EXCHG.150)
ms:contentKeyID: 50479665
ms.date: 04/27/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Déploiements hybrides Exchange Server

 

_<strong>Sapplique à :</strong>Exchange Online, Exchange Server 2013, Exchange Server 2016_

_<strong>Dernière rubrique modifiée :</strong>2018-04-16_

**Résumé** : Ce que vous devez savoir pour planifier un déploiement Exchange hybride.

Un déploiement hybride offre aux entreprises la possibilité d'étendre l'éventail de fonctionnalités proposé et le contrôle administratif qu'elles exercent dans leur organisation Microsoft Exchange locale vers le nuage. Le déploiement hybride offre l'apparence homogène d'une organisation Exchange unique entre une organisation Exchange locale et Exchange Online dans Microsoft Office 365. De plus, il peut servir d'étape intermédiaire à la migration définitive vers une organisation Exchange Online.

**Table des matières**

Fonctions de déploiement hybride Exchange

Éléments à prendre en compte pour le déploiement hybride Exchange

Composants d'un déploiement hybride Exchange

Exemple de déploiement hybride Exchange

Points à considérer avant de configurer un déploiement hybride Exchange

Terminologie clé

Documentation sur le déploiement hybride Exchange

## Fonctions de déploiement hybride Exchange

Un déploiement hybride active les fonctions suivantes :

  - Sécurisation du routage des messages entre l'organisation locale et l'organisation Exchange Online.

  - Routage des messages avec espace de noms de domaine partagé. Par exemple, l'organisation locale et l'organisation Exchange Online utilisent le domaine SMTP @contoso.com.

  - Liste d’adresses globale (LAG) unifiée, également appelée « carnet d’adresses partagé »

  - Partage de calendrier et de disponibilité entre l'organisation locale et l'organisation Exchange Online.

  - Contrôle centralisé du flux des messages entrants et sortants. Vous pouvez configurer tous les messages Exchange Online entrants et sortants pour qu'ils soient acheminés via l'organisation Exchange locale.

  - URL Outlook sur le web unique pour les organisations Exchange Online et locale

  - Possibilité de déplacer des boîtes aux lettres locales existantes vers l'organisation Exchange Online. Les boîtes aux lettres Exchange Online peuvent être redéplacées vers l'organisation locale si nécessaire.

  - Gestion centralisée des boîtes aux lettres à l'aide du Centre d'administration Exchange (CAE) local.

  - Suivi des messages, infos-courrier et recherche dans plusieurs boîtes aux lettres entre l'organisation locale et l'organisation Exchange Online.

  - Archivage dans le cloud des messages pour les boîtes aux lettres Exchange locales. L’archivage Exchange Online peut être utilisé en association avec un déploiement hybride. Pour plus d’informations sur l’archivage Exchange Online, consultez la rubrique [Services supplémentaires de Microsoft Office 365](http://go.microsoft.com/fwlink/p/?linkid=233231).

## Éléments à prendre en compte pour le déploiement hybride Exchange

Vous devez tenir compte des aspects suivants avant d’implémenter un déploiement hybride Exchange :

  - **Exigences de déploiement hybride** : avant de configurer un déploiement hybride, vous devez vous assurer que votre organisation en local remplit toutes les conditions préalables requises pour réussir un déploiement. Pour plus d’informations, voir [Configuration requise pour un déploiement hybride](hybrid-deployment-prerequisites-exchange-2013-help.md).

  - **Clients Exchange ActiveSync** : lorsque vous déplacez une boîte aux lettres de votre organisation Exchange locale vers Exchange Online, tous les clients qui accèdent à la boîte aux lettres doivent être mis à jour pour utiliser Exchange Online ; cela inclut les périphériques Exchange ActiveSync. La plupart des clients Exchange ActiveSync sont désormais automatiquement reconfigurés lorsque la boîte aux lettres est déplacée vers Exchange Online. Cependant, il est possible que certains périphériques plus anciens ne se mettent pas à jour correctement. Pour plus d’informations, voir [Paramètres du périphérique Exchange ActiveSync avec des déploiements hybrides Exchange](exchange-activesync-device-settings-with-exchange-hybrid-deployments-exchange-2013-help.md).

  - **Migration d’autorisations de boîtes aux lettres** : les autorisations sur les boîtes aux lettres locales (par exemple, Envoyer en tant que, Accès complet, Envoyer de la part de et les autorisations de dossier) qui sont explicitement appliquées sur la boîte aux lettres, sont migrées vers Exchange Online. Les autorisations de boîte aux lettres héritées (non explicites) et les autorisations accordées sur des objets qui ne disposent pas d’une extension messagerie dans Exchange Online ne sont pas migrées. Avant la migration, vous devez vérifier que toutes les autorisations sont accordées explicitement et que tous les objets disposent de l’extension messagerie. Par conséquent, vous devez planifier la configuration de ces autorisations dans Office 365 pour votre organisation, le cas échéant. Dans le cas des autorisations Envoyer en tant que, si l’utilisateur et la ressource requérant l’autorisation ne sont pas déplacés en même temps, vous devez ajouter explicitement l’autorisation Envoyer en tant que dans Exchange Online à l’aide de la cmdlet **Add-RecipientPermission**.

  - **Prise en charge des autorisations de boîtes aux lettres entre différents locaux** Les déploiements hybrides Exchange prennent en charge l’utilisation des autorisations « Accès total » et « Envoyer pour le compte de » entre les boîtes aux lettres situées dans une organisation Exchange sur site et des boîtes aux lettres dans Office 365. Des étapes supplémentaires sont requises pour les autorisations « Envoyer en tant que ». En outre, une configuration supplémentaire peut être nécessaire pour prendre en charge les autorisations de boîtes aux lettres entre différents locaux, en fonction de la version d’Exchange installée dans votre organisation sur site. Pour plus d’informations, reportez-vous à la section [Octroi d'autorisations de boîte aux lettres à des délégués](permissions-in-exchange-hybrid-deployments-exchange-2013-help.md) dans la rubrique [Autorisations dans les déploiements hybrides Exchange](permissions-in-exchange-hybrid-deployments-exchange-2013-help.md), ainsi qu’à la rubrique [Configurer Exchange pour prendre en charge des autorisations de boîtes aux lettres déléguées dans un déploiement hybride](configure-exchange-to-support-delegated-mailbox-permissions-in-a-hybrid-deployment-exchange-2013-help.md).
    
    > [!NOTE]
    > Le déploiement de la fonctionnalité prenant en charge les droits Accès total, Envoyer pour le compte de et les droits sur les dossiers inter-forêts commencera en février 2018 et se terminera en avril 2018.


  - **Gestion des déplacements** : dans le cadre de la gestion continue des destinataires, vous pouvez avoir à replacer les boîtes aux lettres Exchange Online dans votre environnement local.
    
    Pour plus d’informations sur le déplacement de boîtes aux lettres dans un déploiement hybride Exchange 2010, voir [Déplacer une boîte aux lettres Exchange Online vers l’organisation locale](https://technet.microsoft.com/fr-fr/library/hh882527\(v=exchg.150\)).
    
    Pour plus d’informations sur le déplacement des boîtes aux lettres dans les déploiements hybrides basés sur Exchange 2013 ou version ultérieure, voir [Déplacement de boîtes aux lettres entre des organisations locales et Exchange Online dans des déploiements hybrides](move-mailboxes-between-on-premises-and-exchange-online-organizations-in-hybrid-deployments-exchange-2013-help.md).

  - **Paramètres de transfert de boîtes aux lettres** Les boîtes aux lettres peuvent être configurées pour transférer automatiquement le courrier qui leur est envoyé à une autre boîte aux lettres. Tandis que le transfert de boîtes aux lettres est pris en charge dans Exchange Online, la configuration du transfert n’est pas copiée dans Exchange Online quand la boîte aux lettres y est déplacée. Avant de migrer une boîte aux lettres vers Exchange Online, veillez à exporter la configuration de transfert pour chaque boîte aux lettres. La configuration du transfert est stockée dans les propriétés `DeliverToMailboxAndForward`, `ForwardingAddress` et `ForwardingSmtpAddress` de chaque boîte aux lettres.

## Composants d’un déploiement hybride Exchange

Un déploiement hybride implique différents services et composants :

  - **Serveurs Exchange** : au moins un serveur Exchange doit être configuré dans votre organisation locale si vous souhaitez configurer un déploiement hybride. Si vous exécutez Exchange 2013 ou version antérieure, vous devez installer au moins un serveur exécutant les rôles de boîte aux lettres et d’accès client. Si vous exécutez Exchange 2016 ou version ultérieure, au moins un serveur exécutant le rôle de boîte aux lettres doit être installé. Si nécessaire, les serveurs de transport Edge Exchange peuvent également être installés dans un réseau de périmètre et prendre en charge un flux de messagerie sécurisé avec Office 365.
    
    > [!NOTE]
    > Nous ne prenons pas en charge l’installation des serveurs Exchange exécutant les rôles de serveur de boîte aux lettres ou d’accès client dans un réseau de périmètre.


  - **Microsoft Office 365** : le service Office 365 comprend une organisation Exchange Online dans le cadre de son service d’abonnement. Les organisations configurant un déploiement hybride doivent acheter une licence pour chaque boîte aux lettres migrée vers ou créée dans l’organisation Exchange Online.

  - **Assistant Configuration hybride**Exchange inclut l'Assistant Configuration hybride qui vous propose un processus rationalisé pour configurer un déploiement hybride entre une organisation Exchange locale et une organisation Exchange Online.
    
    Pour plus d'informations, consultez la rubrique [Assistant de configuration hybride](hybrid-configuration-wizard-exchange-2013-help.md).

  - **Système d’authentification Azure AD** : le système d’authentification Azure Active Directory (AD) est un service informatique gratuit qui agit en tant que courtier d’approbation entre votre organisation Exchange 2016 locale et l’organisation Exchange Online. Les organisations locales qui configurent un déploiement hybride doivent disposer d’une approbation de fédération avec le système d’authentification d’Azure AD. L’approbation de fédération peut être créée manuellement, soit dans le cadre de la configuration des fonctions de partage fédéré entre une organisation Exchange locale et d’autres organisations Exchange fédérées, soit dans le cadre de la configuration d’un déploiement hybride avec l’Assistant Configuration hybride. Une approbation de fédération avec le système d’authentification d’Azure AD pour votre client Office 365 est automatiquement configurée lorsque vous activez votre compte de service Office 365.
    
    Pour plus d’informations, consultez la rubrique [Système d’authentification Azure AD](https://go.microsoft.com/fwlink/p/?linkid=135986).

  - **Synchronisation Azure Active Directory** : la synchronisation Azure AD utilise Azure AD Connect pour répliquer les informations Active Directory locales pour les objets à extension messagerie vers l’organisation Office 365 afin de prendre en charge la liste d’adresses globale unifiée (LAG) et l’authentification des utilisateurs. Les organisations configurant un déploiement hybride doivent déployer Azure AD Connect sur un serveur local distinct afin de synchroniser Active Directory en local avec Office 365.
    
    Pour plus d’informations, consultez la rubrique suivante : [Azure AD Connect - Présentation](https://go.microsoft.com/fwlink/p/?linkid=203007)

Terminologie clé

## Exemple de déploiement hybride

Étudiez le scénario suivant. Il s’agit d’un exemple de topologie qui présente un déploiement Exchange 2016 type. Contoso, Ltd. est une organisation dotée d’une seule forêt, d’un seul domaine avec deux contrôleurs de domaine et un serveur Exchange 2016 installé. Les utilisateurs Contoso distants se servent d’Outlook sur le web pour se connecter à Exchange 2016 via Internet pour vérifier leurs boîtes aux lettres et accéder à leur calendrier Outlook.

![Le déploiement d’Exchange local avant le déploiement hybride avec Office 365 est configuré](images/JJ200581.dad133ae-d18a-42ec-8f0a-dd1de391200e(EXCHG.150).png "Le déploiement d’Exchange local avant le déploiement hybride avec Office 365 est configuré")

Supposons que vous êtes l’administrateur réseau de Contoso et que vous envisagez de configurer un déploiement hybride. Vous déployez et configurez un serveur Azure AD Connect obligatoire et vous décidez également d’utiliser la fonctionnalité de synchronisation de mot de passe Azure AD Connect pour permettre aux utilisateurs d’utiliser les mêmes informations d’identification pour leur compte de réseau local et leur compte Office 365. Après avoir satisfait les conditions préalables d’un déploiement hybride et utilisé l’Assistant Configuration hybride pour sélectionner les options du déploiement hybride, votre nouvelle topologie présente la configuration suivante :

  - Les utilisateurs se servent du même nom d’utilisateur et du même mot de passe pour se connecter à l’organisation locale et à l’organisation Exchange Online (« authentification unique »).

  - Les boîtes aux lettres utilisateur situées dans l'organisation locale et l'organisation Exchange Online utiliseront le même domaine d'adresse de messagerie. Par exemple, les boîtes aux lettres situées localement et celles situées dans l'organisation Exchange Online utiliseront les adresses de messagerie utilisateur @contoso.com.

  - Tous les messages sortants sont remis à Internet par l’organisation locale. L’organisation locale contrôle le transport de tous les messages et sert de relais à l’organisation Exchange Online (« transport de courrier centralisé »).

  - Les utilisateurs de l'organisation locale et de l'organisation Exchange Online peuvent partager leurs informations de disponibilité du calendrier les uns avec les autres. Les relations des organisations configurées pour les deux organisations autorisent également le suivi des messages, les info-courriers et la recherche de messages intersite.

  - Les utilisateurs de l’organisation locale et de l’organisation Exchange Online utilisent la même URL pour se connecter à leurs boîtes aux lettres via Internet.

![Le déploiement d’Exchange local après le déploiement hybride avec Office 365 est configuré](images/JJ200581.e8681849-f15d-4d0e-b77e-6105b6096c4b(EXCHG.150).png "Le déploiement d’Exchange local après le déploiement hybride avec Office 365 est configuré")

Si vous comparez la configuration de l’organisation existante de Contoso avec celle d’un déploiement hybride, vous constaterez que la configuration d’un déploiement hybride a permis d’ajouter des serveurs et des services qui prennent en charge des fonctions et des échanges supplémentaires partagés entre l’organisation locale et l’organisation Exchange Online. Voici un aperçu des modifications qu’un déploiement hybride apporte à l’organisation Exchange locale initiale.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Configuration</th>
<th>Avant de déploiement hybride</th>
<th>Après le déploiement hybride</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Emplacement des boîtes aux lettres</p></td>
<td><p>Boîtes aux lettres locales uniquement.</p></td>
<td><p>Boîtes aux lettres locales et dans Office 365.</p></td>
</tr>
<tr class="even">
<td><p>Transport des messages</p></td>
<td><p>Les serveurs de boîtes aux lettres locaux gèrent l’acheminement de tous les messages entrants et sortants.</p></td>
<td><p>Les serveurs de boîtes aux lettres locaux gèrent le routage de message interne entre l’organisation locale et l’organisation Office 365.</p></td>
</tr>
<tr class="odd">
<td><p>Outlook sur le web</p></td>
<td><p>Les serveurs de boîtes aux lettres locaux reçoivent toutes les demandes Outlook sur le web et affichent les informations de boîte aux lettres.</p></td>
<td><p>Les serveurs de boîtes aux lettres locaux redirigent les demandes Outlook sur le web vers des serveurs de boîtes aux lettres Exchange 2016 locaux ou fournissent un lien pour se connecter à Office 365.</p></td>
</tr>
<tr class="even">
<td><p>Liste d'adresses globale unifiée pour les deux organisations</p></td>
<td><p>Non applicable ; une seule organisation uniquement.</p></td>
<td><p>Le serveur de synchronisation Active Directory local réplique les informations Active Directory des objets à extension messagerie dans Office 365.</p></td>
</tr>
<tr class="odd">
<td><p>Authentification unique utilisée pour les deux organisations</p></td>
<td><p>Non applicable ; une seule organisation uniquement.</p></td>
<td><p>Active Directory en local et Office 365 utilisent les mêmes nom d’utilisateur et mot de passe pour les boîtes aux lettres situées en local ou dans Office 365.</p></td>
</tr>
<tr class="even">
<td><p>Relation d’organisation établie et approbation de fédération avec le système d’authentification Azure AD</p></td>
<td><p>Une relation d’approbation avec le système d’authentification Azure AD et des relations d’organisation avec d’autres organisations Exchange fédérées peuvent être configurées.</p></td>
<td><p>Une relation d’approbation avec le système d’authentification Azure AD est exigée. Les relations des organisations sont établies entre l’organisation locale et Office 365.</p></td>
</tr>
<tr class="odd">
<td><p>Partage de disponibilité</p></td>
<td><p>Partage de disponibilité entre utilisateurs locaux uniquement.</p></td>
<td><p>Partage des informations de disponibilité entre les utilisateurs locaux et ceux de l’organisation Office 365.</p></td>
</tr>
</tbody>
</table>


## Points à considérer avant de configurer un déploiement hybride

Maintenant que vous savez un peu mieux ce qu'est un déploiement hybride, vous devez considérer certains aspects importants. La configuration d'un déploiement hybride pourrait affecter plusieurs zones de votre réseau actuel et de votre organisation Exchange.

## Synchronisation d’annuaires et authentification unique

La synchronisation Active Directory entre l’organisation locale et l’organisation Office 365, qui est réalisée toutes les trois heures par un serveur exécutant Azure Active Directory Connect, est une configuration requise pour la configuration d’un déploiement hybride. La synchronisation d’annuaires permet aux destinataires des deux organisations de se voir dans la liste d’adresses globale. Elle synchronise également les noms d’utilisateur et les mots de passe, ce qui permet aux utilisateurs de se connecter avec les mêmes informations d’identification dans l’organisation locale et Office 365.

> [!NOTE]
> Si vous choisissez de configurer Azure AD Connect avec AD FS, les noms d’utilisateur et les mots de passe des utilisateurs locaux seront toujours synchronisés avec Office 365 par défaut. Toutefois, les utilisateurs s’authentifieront auprès de votre organisation Active Directory locale avec AD FS comme principale méthode d’authentification. Si AD FS ne peut pas se connecter à votre organisation Active Directory locale pour quelque raison que ce soit, les clients tentent de s’authentifier avec les noms d’utilisateur et les mots de passe synchronisés avec Office 365.


Tous les clients Azure Active Directory et Office 365 sont limités à 50 000 objets (utilisateurs, contacts à extension messagerie et groupes). Cette limite détermine le nombre d’objets que vous pouvez créer dans votre organisation Office 365. Lorsque vous vérifiez votre premier domaine, cette limite d’objets est automatiquement élevée à 300 000 objets. Si vous avez vérifié un domaine et que vous devez synchroniser plus de 300 000 objets, ou si vous n’avez aucun domaine à vérifier et que vous devez synchroniser plus de 50 000 objets, vous devez contacter le support Azure Active Directory pour demander une augmentation de votre quota d’objets.

En plus d’un serveur exécutant Azure AD Connect, vous devez également déployer un serveur proxy d’application web si vous choisissez de configurer AD FS. Ce serveur doit être placé dans votre réseau de périmètre et agit comme un intermédiaire entre votre server Azure AD Connect interne et Internet. Le serveur proxy d’application web doit accepter les connexions provenant de clients et de serveurs sur Internet à l’aide du port TCP 443.

## Gestion d'un déploiement hybride

Vous gérez un déploiement hybride dans Exchange 2016 via une console de gestion unifiée unique qui permet de gérer à la fois votre organisation locale et votre organisation Exchange Online. Le *Centre d’administration Exchange* (CAE), qui remplace la console de gestion Exchange et le Panneau de configuration Exchange, vous permet de vous connecter et de configurer des fonctionnalités pour les deux organisations. Lorsque vous exécutez l’Assistant Configuration hybride pour la première fois, vous êtes invité à vous connecter à votre organisation Exchange Online. Vous devez utiliser un compte Office 365 membre du groupe de rôles Gestion de l’organisation pour connecter le CAE à votre organisation Exchange Online.

## Certificats

Les certificats numériques SSL (Secure Sockets Layer) jouent un rôle important dans la configuration d'un déploiement hybride. Ils contribuent à la sécurisation des échanges entre le serveur hybride local et l'organisation Exchange Online. Les certificats sont une condition préalable à la configuration de plusieurs types de services. Si vous utilisez déjà des certificats numériques dans votre organisation Exchange, vous devrez peut-être les modifier afin d'inclure des domaines supplémentaires ou acheter d'autres certificats auprès d'une autorité de certification approuvée (CA). Si vous n'utilisez pas encore de certificats, vous devrez en acheter un ou plusieurs auprès d'une autorité de certification approuvée.

Pour plus d'informations, consultez la rubrique suivante : [Conditions requises pour les certificats dans le cadre de déploiements hybrides](certificate-requirements-for-hybrid-deployments-exchange-2013-help.md)

## Bande passante

Votre connexion réseau à Internet a un impact direct sur les performances de la communication entre votre organisation locale et l’organisation Office 365. Cela se vérifie plus particulièrement lorsque vous déplacez des boîtes aux lettres depuis votre serveur Exchange 2016 local vers l’organisation Office 365. La quantité de bande passante réseau disponible, combinée à la taille et au nombre de boîtes aux lettres déplacées, entraîne des variations au niveau de la durée du déplacement. Par ailleurs, d’autres services Office 365, tels que SharePoint Server 2016 et Skype Entreprise, peuvent également affecter la bande passante disponible pour les services de messagerie.

Avant de déplacer des boîtes aux lettres vers Office 365, vous devez réaliser les opérations suivantes :

  - déterminer la taille moyenne des boîtes aux lettres qui seront transférées vers Office 365.

  - déterminer la vitesse moyenne de connexion et de débit de votre connexion à Internet depuis votre organisation locale.

  - calculer la vitesse moyenne de transfert attendue et planifier vos déplacements de boîtes aux lettres en conséquence.

Pour plus d’informations, voir : [Mise en réseau](https://go.microsoft.com/fwlink/p/?linkid=280178)

## Messagerie unifiée

La messagerie unifiée est prise en charge dans un déploiement hybride entre votre organisation locale et votre organisation Office 365. Votre solution de téléphonie locale doit pouvoir communiquer avec Office 365. Vous devrez donc peut-être acheter un logiciel ou du matériel supplémentaire.

Si vous souhaitez déplacer les boîtes aux lettres de votre organisation locale vers Office 365 et que ces boîtes aux lettres sont configurées pour une messagerie unifiée, vous devrez configurer la messagerie unifiée dans votre déploiement hybride avant de les déplacer. Si vous déplacez les boîtes aux lettres avant de configurer la messagerie unifiée dans votre déploiement hybride, ces boîtes aux lettres n’auront plus accès à la fonctionnalité de messagerie unifiée.

Pour plus d’informations, consultez la rubrique suivante : [Configurer la coexistence de messagerie unifiée](https://go.microsoft.com/fwlink/p/?linkid=842271)

## Gestion des droits relatifs à l’information

La gestion des droits relatifs à l'information (IRM) permet aux utilisateurs d'appliquer des modèles de service Active Directory RMS (Active Directory Rights Management Services) aux messages qu'ils envoient. Les modèles AD RMS permettent de contribuer à la prévention des fuites d'informations en permettant aux utilisateurs d'avoir le contrôle des personnes qui peuvent ouvrir un message protégé et sur ce qu'elles peuvent faire avec ce message après son ouverture.

La technologie IRM dans un déploiement hybride nécessite la planification, la configuration manuelle de l’organisation Office 365 et une certaine compréhension de la manière dont les clients utilisent les serveurs AD RMS selon que leur boîte aux lettres se trouve dans l’organisation locale ou l’organisation Exchange Online.

Pour plus d’informations, voir : [Gestion des droits relatifs à l’information (IRM) dans des déploiements hybrides Exchange](irm-in-exchange-hybrid-deployments-exchange-2013-help.md)

## Appareils mobiles

Les périphériques mobiles sont pris en charge dans le cadre d’un déploiement hybride. Si Exchange ActiveSync est déjà activé sur vos serveurs existants, il continuera à rediriger les demandes provenant de périphériques mobiles vers les boîtes aux lettres se trouvant sur le serveur de boîtes aux lettres local. Pour les périphériques mobiles qui se connectent à des boîtes aux lettres existantes déplacées de l’organisation locale vers Office 365, les profils Exchange ActiveSync sont automatiquement mis à jour pour se connecter à Office 365 sur la plupart des téléphones. Tous les périphériques mobiles prenant en charge Exchange ActiveSync doivent être compatibles avec un déploiement hybride.

Pour plus d’informations, voir : [Téléphones mobiles](https://go.microsoft.com/fwlink/p/?linkid=206387)

## Configuration requise du client

Nous recommandons à vos clients d’utiliser Outlook 2016 ou Outlook 2013 pour une expérience et des performances optimales dans le déploiement hybride. Les clients de versions d’Outlook 2010 antérieures ne sont pas pris en charge dans les déploiements hybrides ou avec Office 365.

## Licence pour Office 365

Pour créer des boîtes aux lettres dans Office 365 ou pour y déplacer des boîtes aux lettres, vous devez vous inscrire à Office 365 Entreprise et disposer de licences. Lorsque vous vous inscrivez à Office 365, vous recevez un nombre déterminé de licences que vous pouvez attribuer à de nouvelles boîtes aux lettres ou à celles déplacées depuis l’organisation locale. Chaque boîte aux lettres d’Office 365 doit posséder une licence.

## Services de blocage du courrier indésirable et antivirus

Les boîtes aux lettres déplacées vers Office 365 disposent automatiquement d’une protection antivirus et de blocage du courrier indésirable fournie par Exchange Online Protection (EOP), un service Office 365. Vous pouvez avoir besoin d’acheter des licences EOP supplémentaires pour vos utilisateurs locaux si vous avez choisi d’acheminer tous les messages Internet entrants via le service EOP. Nous vous recommandons d’évaluer avec soin si la protection EOP de votre organisation Office 365 est appropriée pour couvrir les besoins en protection antivirus et blocage du courrier indésirable de votre organisation locale. Si une protection est déjà mise en œuvre dans votre organisation locale, vous serez peut-être amené à mettre à niveau ou à configurer vos solutions antivirus et de blocage du courrier indésirable locales pour offrir une protection maximale dans toute l’organisation.

Pour plus d'informations, consultez la rubrique suivante : [Protection anti-courrier indésirable et anti-programme malveillant](https://technet.microsoft.com/fr-fr/library/jj200731\(v=exchg.150\))

## Dossiers publics

Les dossiers publics sont désormais pris en charge dans Office 365 et les dossiers publics locaux peuvent être migrés vers Office 365. En outre, les dossiers publics sur Office 365 peuvent être déplacés vers l’organisation Exchange 2016 locale. Les utilisateurs locaux comme les utilisateurs Office 365 peuvent accéder à des dossiers publics situés dans l’une ou l’autre organisation à l’aide d’Outlook sur Internet, Outlook 2016, Outlook 2013 ou Outlook 2010 SP2 ou version ultérieure. La configuration des dossiers publics locaux existants et l’accès pour les boîtes aux lettres locales ne se trouvent pas modifiés par la configuration d’un déploiement hybride.

Pour plus d’informations, voir : [Dossiers publics](https://technet.microsoft.com/fr-fr/library/jj150538\(v=exchg.150\))

## Accessibilité

Pour des informations sur les raccourcis clavier applicables aux procédures de la liste de contrôle, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](https://technet.microsoft.com/fr-fr/library/jj150484\(v=exchg.150\)).

## Terminologie clé

La liste suivante vous fournit les définitions des composants principaux associés aux déploiements hybrides dans Exchange 2013.

  - **transport de messagerie centralisé**  
    Il s'agit de l'option de configuration hybride dans laquelle tous les messages Internet Exchange Online entrants et sortants sont acheminés via l'organisation Exchange locale. Cette option de routage est configurée dans l'Assistant Configuration hybride. Pour plus d'informations, consultez la rubrique [Options de transport dans les déploiements hybrides Exchange](transport-options-in-exchange-hybrid-deployments-exchange-2013-help.md).

<!-- end list -->

  - **domaine de coexistence**  
    Il s'agit d'un domaine accepté ajouté à l'organisation locale pour le flux de messagerie hybride et les demandes de découverte automatique pour le service Office 365. Ce domaine est ajouté en tant que domaine de proxy secondaire à toutes les stratégies d'adresse de messagerie dont les modèles de domaine *PrimarySmtpAddress* sont sélectionnés dans l'Assistant Configuration hybride. Par défaut, ce domaine est \<domaine\>.mail.onmicrosoft.com.

<!-- end list -->

  - ***HybridConfiguration* Objet Active Directory**  
    Il s'agit de l'objet Active Directory dans l'organisation locale contenant les paramètres de configuration de déploiement hybride souhaités définis via les sélections effectuées dans l'Assistant Configuration hybride. Le moteur de configuration hybride utilise ces paramètres lors de la configuration des paramètres Exchange Online locaux pour activer les fonctionnalités hybrides. Le contenu de l'objet *HybridConfiguration* est réinitialisé à chaque exécution de l'Assistant Configuration hybride.

<!-- end list -->

  - **Moteur de configuration hybride**  
    Le moteur de configuration hybride exécute les actions essentielles et nécessaires à la configuration et à la mise à jour d’un déploiement hybride. Le HCE compare l’état de l’objet Active Directory *HybridConfiguration* aux paramètres de configuration actuels de l’organisation Exchange locale et Exchange Online et exécute certaines tâches pour synchroniser les paramètres de configuration du déploiement avec les paramètres définis dans l’objet Active Directory *HybridConfiguration*. Pour plus d’informations, consultez la rubrique [Hybrid Configuration Engine](hybrid-configuration-wizard-exchange-2013-help.md).

<!-- end list -->

  - **Assistant Configuration hybride (HCW)**  
    Il s’agit d’un outil adaptable proposé dans Exchange qui guide les administrateurs pendant la configuration d’un déploiement hybride entre leurs organisations locales et Exchange Online. L’Assistant définit les paramètres de configuration du déploiement hybride dans l’objet *HybridConfiguration* et ordonne au moteur de configuration hybride d’exécuter les tâches de configuration nécessaires pour activer les fonctionnalités hybrides définies. Pour plus d’informations, consultez la rubrique [Assistant de configuration hybride](hybrid-configuration-wizard-exchange-2013-help.md).

<!-- end list -->

  - **déploiement hybride d'Exchange 2010**  
    Il s’agit d’un déploiement hybride qui est configuré à l’aide du Service Pack 3 (SP3) pour les serveurs Exchange Server 2010 locaux en tant que point de terminaison de connexion pour les services Office 365 et Exchange Online. Cette option de déploiement hybride est proposée pour les organisations Exchange 2010, Exchange Server 2007 et Exchange Server 2003 locales.

<!-- end list -->

  - **déploiement hybride d'Exchange 2013**  
    Il s’agit d’un déploiement hybride qui est configuré à l’aide de serveurs Exchange 2013 locaux en tant que point de terminaison de connexion pour les services Office 365 et Exchange Online. Cette option de déploiement hybride est proposée pour les organisations Exchange 2013, Exchange 2010 et Exchange 2007 locales.

<!-- end list -->

  - **Déploiement hybride d’Exchange 2016**  
    Il s’agit d’un déploiement hybride qui est configuré à l’aide de serveurs Exchange 2016 locaux en tant que point de terminaison de connexion pour les services Office 365 et Exchange Online. Cette option de déploiement hybride est proposée pour les organisations Exchange 2016, Exchange 2013 et Exchange 2010 locales.

<!-- end list -->

  - **transport de messagerie sécurisé**  
    Il s’agit d’une fonctionnalité de déploiement hybride configurée automatiquement qui permet un transport de messagerie sécurisé entre les organisations locales et Exchange Online. Les messages sont chiffrés et authentifiés à l’aide du protocole TLS (Transport Layer Security) avec un certificat sélectionné dans l’Assistant Configuration hybride. Office 365 est le point de terminaison pour les connexions de transport hybride provenant de l’organisation locale et il s’agit de la source pour les connexions de transport hybride à destination de l’organisation locale à partir d’Exchange Online.

Terminologie clé

## Documentation sur le déploiement hybride Exchange

Le tableau suivant contient des liens à des rubriques qui vous permettront d'en savoir plus sur les déploiements hybrides et leur gestion dans Microsoft Exchange.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Rubrique</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="hybrid-configuration-wizard-exchange-2013-help.md">Assistant de configuration hybride</a></p></td>
<td><p>En savoir plus sur la configuration d'un déploiement hybride par l'Assistant Configuration hybride et le moteur de configuration hybride.</p></td>
</tr>
<tr class="even">
<td><p><a href="hybrid-deployment-prerequisites-exchange-2013-help.md">Configuration requise pour un déploiement hybride</a></p></td>
<td><p>En savoir plus sur les conditions préalables à un déploiement hybride, notamment les organisations Exchange Server compatibles, la configuration Office 365 requise et autres conditions préalables de configuration locale.</p></td>
</tr>
<tr class="odd">
<td><p><a href="certificate-requirements-for-hybrid-deployments-exchange-2013-help.md">Conditions requises pour les certificats dans le cadre de déploiements hybrides</a></p></td>
<td><p>En savoir plus sur la configuration requise pour les certificats numériques dans des déploiements hybrides.</p></td>
</tr>
<tr class="even">
<td><p><a href="transport-options-in-exchange-hybrid-deployments-exchange-2013-help.md">Options de transport dans les déploiements hybrides Exchange</a></p></td>
<td><p>En savoir plus sur les options de transport des messages entrants et sortants dans des déploiements hybrides.</p></td>
</tr>
<tr class="odd">
<td><p><a href="transport-routing-in-exchange-hybrid-deployments-exchange-2013-help.md">Routage de transport dans les déploiements hybrides Exchange</a></p></td>
<td><p>En savoir plus sur les options de routage des messages entrants et sortants dans un déploiement hybride.</p></td>
</tr>
<tr class="even">
<td><p><a href="hybrid-management-in-exchange-hybrid-deployments-exchange-2013-help.md">Gestion hybride dans les déploiements hybrides Exchange</a></p></td>
<td><p>En savoir plus sur la gestion de votre déploiement hybride avec le Centre d'administration Exchange et l'environnement de ligne de commande Exchange Management Shell.</p></td>
</tr>
<tr class="odd">
<td><p><a href="shared-free-busy-in-exchange-hybrid-deployments-exchange-2013-help.md">Partage des disponibilités dans des déploiements hybrides Exchange</a></p></td>
<td><p>En savoir plus le partage de disponibilité du calendrier entre une organisation locale et une organisation Exchange Online dans un déploiement hybride.</p></td>
</tr>
<tr class="even">
<td><p><a href="server-roles-in-exchange-hybrid-deployments-exchange-2013-help.md">Rôles serveur dans les déploiements hybrides Exchange</a></p></td>
<td><p>En savoir plus sur le fonctionnement des rôles de serveur Exchange dans un déploiement hybride.</p></td>
</tr>
<tr class="odd">
<td><p><a href="irm-in-exchange-hybrid-deployments-exchange-2013-help.md">Gestion des droits relatifs à l’information (IRM) dans des déploiements hybrides Exchange</a></p></td>
<td><p>En savoir plus sur le fonctionnement de la Gestion des droits relatifs à l'information dans un déploiement hybride.</p></td>
</tr>
<tr class="even">
<td><p><a href="permissions-in-exchange-hybrid-deployments-exchange-2013-help.md">Autorisations dans les déploiements hybrides Exchange</a></p></td>
<td><p>En savoir plus sur la manière dont un déploiement hybride utilise le contrôle d'accès en fonction du rôle (RBAC) pour contrôler les autorisations.</p></td>
</tr>
<tr class="odd">
<td><p><a href="edge-transport-servers-with-hybrid-deployments-exchange-2013-help.md">Serveurs de transport Edge avec déploiements hybrides</a></p></td>
<td><p>En savoir plus sur les serveurs de transport Edge Exchange, ainsi que sur leur déploiement et leur fonctionnement dans un déploiement hybride.</p></td>
</tr>
<tr class="even">
<td><p><a href="single-sign-on-with-hybrid-deployments-exchange-2013-help.md">Authentification unique avec les déploiements hybrides</a></p></td>
<td><p>En savoir plus sur le fonctionnement de l’authentification unique à l’aide de la synchronisation de mot de passe et d’AD FS dans un déploiement hybride.</p></td>
</tr>
<tr class="odd">
<td><p><a href="hybrid-deployment-procedures-exchange-2013-help.md">Procédures de déploiement hybride</a></p></td>
<td><p>Découvrez des procédures permettant de créer et de modifier des déploiements hybrides pour votre organisation Exchange locale et votre organisation Exchange Online.</p></td>
</tr>
<tr class="even">
<td><p><a href="hybrid-deployments-with-exchange-2013-and-exchange-2010-exchange-2013-help.md">Déploiements hybrides avec Exchange 2013 et Exchange 2010</a></p></td>
<td><p>En savoir plus sur les déploiements hybrides Exchange 2013 avec des organisations Exchange 2010.</p></td>
</tr>
<tr class="odd">
<td><p><a href="hybrid-deployments-with-exchange-2013-and-exchange-2007-exchange-2013-help.md">Déploiements hybrides avec Exchange 2013 et Exchange 2007</a></p></td>
<td><p>En savoir plus sur les déploiements hybrides Exchange 2013 avec des organisations Exchange 2007.</p></td>
</tr>
</tbody>
</table>


## Vous débutez avec Office 365 ?


<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><img src="images/JJ200581.eac8a413-9498-4220-8544-1e37d1aaea13(EXCHG.150).png" title="Icône rapide pour LinkedIn Learning" alt="Icône rapide pour LinkedIn Learning" /> <strong>Vous débutez avec Office 365 ?</strong><br />
Découvrez les cours vidéo gratuits pour <a href="https://support.office.com/fr-fr/article/office-365-admin-and-it-pro-courses-68cc9b95-0bdc-491e-a81f-ee70b3ec63c5">Office 365 admins and IT pros</a> proposés par LinkedIn Learning.</p></td>
</tr>
</tbody>
</table>

