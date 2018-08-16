---
title: 'Fédération: Exchange 2013 Help'
TOCTitle: Fédération
ms:assetid: 0046e2eb-6940-4941-bd5b-cbe6bffa3b94
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dd335047(v=EXCHG.150)
ms:contentKeyID: 50477408
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Fédération

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2016-12-09_

Les professionnels de l’information ont souvent besoin de collaborer avec des destinataires, fournisseurs, partenaires et clients externes et de partager leurs informations de disponibilité (également appelées disponibilités de calendrier). La fédération dans Microsoft Exchange Server 2013 facilite ces efforts de collaboration. Le terme *fédération* désigne l’infrastructure d’approbation sous-jacente qui prend en charge le *partage fédéré*, un moyen facile pour les utilisateurs de partager des informations de calendrier avec les destinataires d’autres organisations fédérées externes. Pour en savoir plus sur le partage fédéré, voir [Partage](sharing-exchange-2013-help.md).

> [!NOTE]
> Cette fonctionnalité d’Exchange Server 2013 n’est pas entièrement compatible avec les systèmes Office 365 exécutés par 21Vianet en Chine et certaines limitations de fonctionnalités peuvent s’appliquer. Pour plus d’informations, voir <a href="https://go.microsoft.com/fwlink/?linkid=313640">En savoir plus sur Office 365 exécuté par 21Vianet</a>.


**Contenu de cette rubrique**

Terminologie clé

Système d’authentification Azure AD

Approbation de fédération

Identificateur d’organisation fédérée

Exemple de fédération

Configuration requise pour les certificats en vue de la fédération

Transition vers un nouveau certificat

Considérations relatives au pare-feu pour la fédération

## Terminologie clé

Le tableau suivant définit les principaux composants associés à la fédération dans Exchange 2013.

  - **identificateur d’application (AppID)**  
    Numéro unique généré par le système d'authentification Azure Active Directory pour identifier les organisations Exchange. L’AppID est généré automatiquement lorsque vous créez une approbation de fédération avec le système d'authentification Azure Active Directory.

<!-- end list -->

  - **jeton de délégation**  
    Jeton SAML (Security Assertion Markup Language) émis par le système d’authentification Azure Active Directory et permettant aux utilisateurs d’une organisation fédérée d’être approuvés par une autre organisation fédérée. Un jeton de délégation contient l’adresse de messagerie de l’utilisateur, un identificateur immuable et des informations associées à l’offre pour laquelle le jeton est émis.

<!-- end list -->

  - **organisation fédérée externe**  
    Organisation Exchange externe ayant établi une approbation de fédération avec le système d’authentification Azure Active Directory.

<!-- end list -->

  - **partage fédéré**  
    Groupe de fonctionnalités Exchange qui exploitent une approbation de fédération avec le système d’authentification Azure Active Directory pour la réutiliser dans toutes les organisations Exchange, y compris dans les déploiements Exchange entre différents locaux. Ensemble, ces fonctionnalités sont utilisées pour créer des demandes authentifiées entre les serveurs pour le compte d’utilisateurs de multiples organisations Exchange.

<!-- end list -->

  - **domaine fédéré**  
    Domaine accepté faisant autorité qui est ajouté à l’identificateur d’organisation (OrgID) d’une organisation Exchange.

<!-- end list -->

  - **chaîne de chiffrement de preuve de domaine**  
    Chaîne sécurisée de façon cryptographique utilisée par une organisation Exchange pour prouver que le domaine utilisé par le système d’authentification Azure Active Directory appartient à l’organisation. La chaîne est automatiquement générée lorsque vous utilisez l’Assistant **Activer l’approbation de fédération** ou peut être générée à l’aide de la cmdlet **Get-FederatedDomainProof**.

<!-- end list -->

  - **stratégie de partage fédéré**  
    Stratégie de niveau organisationnel qui active et contrôle le partage interpersonnel établi par l’utilisateur des informations de calendrier.

<!-- end list -->

  - **fédération**  
    Contrat de confiance entre deux organisations Exchange destiné à atteindre un objectif commun. Dans la fédération, les deux organisations veulent que les assertions d’authentification d’une organisation soient reconnues par l’autre.

<!-- end list -->

  - **approbation de fédération**  
    Relation avec le système d’authentification Azure Active Directory qui définit les composants suivants pour votre organisation Exchange :
    
      - Espace de noms de compte
    
      - Identificateur d’application (AppID)
    
      - Identificateur d’organisation (OrgID)
    
      - Domaines fédérés
    
    Pour configurer le partage fédéré avec d’autres organisations Exchange fédérées, une approbation de fédération doit être établie avec le système d’authentification Azure Active Directory.

<!-- end list -->

  - **organisation non fédérée**  
    Organisations ne disposant pas d’approbation de fédération établie avec le système d’authentification Azure Active Directory.

<!-- end list -->

  - **identificateur d’organisation (OrgID)**  
    Identifie les domaines acceptés de référence configurés dans une organisation qui sont activés pour la fédération. Seuls les destinataires ayant des adresses de messagerie avec des domaines fédérés configurés dans l’OrgID sont reconnus par le système d’authentification Azure Active Directory et peuvent utiliser des fonctionnalités de partage fédéré. L’OrgID est constitué d’une chaîne prédéfinie et du premier domaine accepté qui est sélectionné pour la fédération dans l’Assistant **Activer l’approbation de fédération**. Par exemple, si vous spécifiez le domaine fédéré contoso.com comme domaine SMTP principal de votre organisation, l’espace de noms de compte FYDIBOHF25SPDLT.contoso.com sera créé automatiquement comme OrgID pour l’approbation de fédération.

<!-- end list -->

  - **relation organisationnelle**  
    Relation un-à-un entre deux organisations Exchange fédérées qui permet aux destinataires d’échanger des informations de disponibilité (disponibilité de calendrier). Une relation organisationnelle requiert une approbation de fédération avec le système d’authentification Azure Active Directory et rend inutile l’utilisation d’approbations de forêt ou de domaine Active Directory entre organisations Exchange.

<!-- end list -->

  - **Azure Active Directory système d'authentification**  
    Service d’identité en nuage gratuit qui agit comme un courtier d’approbation entre vos organisations Microsoft Exchange fédérées. Il est responsable de l’envoi de jetons de délégation aux destinataires Exchange qui demandent des informations aux destinataires d’autres organisations Exchange fédérées. Pour en savoir plus, consultez la rubrique [Azure Active Directory](https://go.microsoft.com/fwlink/?linkid=392500).

## Système d’authentification Azure AD

Le système d’authentification Azure Active Directory, un service informatique gratuit basé sur le nuage proposé par Microsoft, intervient comme un courtier d’approbation entre votre organisation Exchange 2013 locale et d’autres organisations Exchange 2010 et Exchange 2013 fédérées. Si vous souhaitez configurer la fédération dans votre organisation Exchange, vous devez établir une approbation de fédération unique avec le système d’authentification Azure Active Directory, afin qu’elle puisse devenir partenaire de fédération de votre organisation. Une fois cette approbation en place, les utilisateurs authentifiés par Active Directory (appelés *fournisseurs d’identité*) obtiennent des jetons de délégation SAML (Security Assertion Markup Language) du système d’authentification Azure AD. Ces jetons permettent aux utilisateurs d’une organisation Exchange fédérée d’être approuvés par une autre organisation Exchange fédérée. Lorsque le système d’authentification Azure AD intervient comme courtier d’approbation, les organisations ne sont pas tenues d’établir plusieurs relations d’approbation individuelles avec d’autres organisations, et les utilisateurs peuvent accéder à des ressources externes à l’aide de l’authentification unique. Pour plus d’informations, consultez la rubrique [Azure Active Directory](https://go.microsoft.com/fwlink/?linkid=392500).

Terminologie clé

## Approbation de fédération

Pour utiliser les fonctionnalités de partage fédéré Exchange 2013, vous devez établir une approbation de fédération entre votre organisation Exchange 2013 et le système d’authentification Azure AD. L'établissement d'une approbation de fédération avec le système d’authentification Azure AD permet d'échanger le certificat de sécurité numérique de votre organisation avec le système d’authentification Azure AD et récupère les métadonnées de fédération et le certificat du système d'authentification Azure AD. Vous pouvez établir une approbation de fédération à l’aide de l’Assistant **Activer l’approbation de fédération** dans le Centre d’administration Exchange ou de la cmdlet **New-FederationTrust** dans l’environnement de ligne de commande Exchange Management Shell. Un certificat auto-signé est automatiquement créé par l’Assistant **Activer l’approbation de fédération** et utilisé pour la signature et le chiffrement des jetons de délégation du système d’authentification Azure AD qui permettent aux utilisateurs d’être approuvés par des organisations fédérées externes. Pour plus d’informations sur la configuration requise pour les certificats, consultez la section Configuration requise pour les certificats en vue de la fédération plus loin dans cette rubrique.

Lorsque vous créez une approbation de fédération avec le système d’authentification Azure AD, un *identificateur d’application* (AppID) est généré automatiquement pour votre organisation Exchange et indiqué dans la sortie de la cmdlet **Get-FederationTrust**. L’AppID est utilisé par le système d’authentification Azure AD pour identifier de manière unique votre organisation Exchange. Il est également utilisé par l’organisation Exchange pour prouver que votre organisation contrôle le domaine à utiliser avec le système d’authentification Azure AD. Cette opération est effectuée en créant un enregistrement de texte (TXT) dans la zone DNS (Domain Name System) publique pour chaque domaine fédéré.

Terminologie clé

## Identificateur d’organisation fédérée

L’*identificateur d’organisation fédérée* détermine, parmi les domaines acceptés faisant autorité configurés dans votre organisation, quels sont ceux qui sont activés pour la fédération. Seuls les destinataires possédant des adresses de messagerie avec des domaines acceptés configurés dans l’OrgID sont reconnus par le système d’authentification Azure AD et peuvent utiliser les fonctionnalités de partage fédéré. Lorsque vous créez une approbation de fédération, un OrgID est créé automatiquement dans le système d’authentification Azure AD. Cet OrgID est constitué d’une chaîne prédéfinie et du domaine accepté qui est sélectionné comme domaine partagé principal dans l’Assistant. Par exemple, dans l’Assistant Modifier les domaines activés pour le partage, si vous spécifiez le domaine fédéré **contoso.com** comme domaine partagé principal de votre organisation, l’espace de noms de compte **FYDIBOHF25SPDLT.contoso.com** sera créé automatiquement comme OrgID pour l’approbation de fédération de votre organisation Exchange.

Bien qu’il s’agisse généralement du domaine SMTP principal de l’organisation Exchange, ce domaine n’est pas obligatoirement un domaine accepté dans votre organisation Exchange et ne requiert pas d’enregistrement TXT de preuve d’appartenance du DNS. La seule exigence est la limitation des domaines acceptés qui sont sélectionnés pour être fédérés à un nombre maximal de 32 caractères. Ce sous-domaine a pour seul objet de servir d’espace de noms fédéré pour le système d’authentification Azure AD afin de pouvoir gérer des identificateurs uniques pour des destinataires demandant des jetons de délégation SAML (Security Assertions Markup Language). Pour de plus amples informations sur les jetons SAML, consultez la rubrique [Jetons SAML et revendications](https://go.microsoft.com/fwlink/?linkid=198561)

Vous pouvez à tout moment ajouter des domaines acceptés à l’approbation de fédération ou en supprimer. Si vous souhaitez activer ou désactiver toutes les fonctionnalités de partage de fédération dans votre organisation, il vous suffit d’activer ou de désactiver l’OrgID pour l’approbation de fédération.

> [!NOTE]
> Si vous modifiez l’OrgID, les domaines acceptés ou l’identificateur d’application pour l’approbation de fédération, toutes les fonctionnalités de partage de fédération sont affectées dans votre organisation. Toute organisation Exchange fédérée externe, notamment Exchange Online et les configurations de déploiement hybride, est également affectée. Nous vous recommandons d’informer tous vos partenaires fédérés externes si vous modifiez ces paramètres de configuration de l’approbation de fédération.


Terminologie clé

## Exemple de fédération

Deux organisations Exchange, Contoso, Ltd. et Fabrikam, Inc., souhaitent permettre à leurs utilisateurs d’échanger leurs informations de disponibilité de calendrier. Chaque organisation crée une approbation de fédération avec le système d’authentification Azure AD et configure son espace de noms de compte afin d’inclure le domaine utilisé pour le domaine d’adresse de messagerie de ses utilisateurs.

Les employés de Contoso utilisent l’un des domaines d’adresse de messagerie suivants : contoso.com, contoso.co.uk ou contoso.ca. Les employés de Fabrikam utilisent l’un des domaines d’adresse de messagerie suivants : fabrikam.com, fabrikam.org ou fabrikam.net. Les deux organisations s’assurent que tous les domaines de messagerie acceptés sont inclus dans l’espace de noms de compte pour leur approbation de fédération avec le système d’authentification Azure AD. Au lieu d’exiger une configuration d’approbation de forêt ou de domaine Active Directory complexe entre elles, les deux organisations configurent une relation organisationnelle afin de permettre le partage des disponibilités de calendrier.

La figure suivante illustre la configuration de la fédération entre Contoso, Ltd. et Fabrikam, Inc.

**Exemple de partage fédéré**

![Approbations de fédération et partage fédéré](images/Dd335047.310f0698-b67d-4b0e-91e4-231c6e9db952(EXCHG.150).gif "Approbations de fédération et partage fédéré")

## Configuration requise pour les certificats en vue de la fédération

Pour établir une approbation de fédération avec le système d’authentification Azure AD, un certificat auto-signé ou un certificat X.509 signé par une autorité de certification doit être créé et installé sur le serveur Exchange 2013 utilisé pour créer l’approbation. Il est vivement conseillé d’utiliser un certificat auto-signé, que vous pouvez créer et installer automatiquement à l’aide de l’Assistant **Activer l’approbation de fédération** dans le Centre d’administration Exchange. Ce certificat sert uniquement à signer et chiffrer les jetons de délégation utilisés pour le partage fédéré ; un seul certificat est nécessaire pour l’approbation de fédération. Exchange 2013 distribue automatiquement le certificat à tous les autres serveurs Exchange 2013 de l’organisation.

Si vous souhaitez utiliser un certificat X.509 signé par une Autorité de certification externe, il doit réunir les conditions suivantes :

  - **Trusted CA**   Si possible, le certificat SSL (Secure Sockets Layer) X.509 doit être émis par une Autorité de certification approuvée par Windows Live. Cependant, vous pouvez utiliser les certificats utilisés par des autorités de certification qui ne sont pas actuellement certifiées par Microsoft. Pour obtenir une liste actualisée des autorités de certification approuvées, voir [Autorités de certification racine de confiance pour les approbations de fédération](trusted-root-certification-authorities-for-federation-trusts-exchange-2013-help.md).

  - **Identificateur de clé de l’objet**   Le certificat doit posséder un champ d’identificateur de clé de l’objet. La plupart des certificats X.509 émis par des autorités de certification commerciales comportent cet identificateur.

  - **Fournisseur de services de chiffrement CryptoAPI**   Le certificat doit utiliser un fournisseur de services de chiffrement CryptoAPI. Certificats utilisant un API de cryptographie : les fournisseurs CNG (Cryptography Next Generation) ne sont pas pris en charge pour la fédération. Si vous vous servez d’Exchange pour créer une demande de certificat, un fournisseur CryptoAPI est utilisé. Pour de plus amples informations, consultez la page [API Cryptography : Next Generation](https://go.microsoft.com/fwlink/?linkid=187890).

  - **Algorithme de signature RSA**   Le certificat doit utiliser RSA comme algorithme de signature.

  - **Clé privée exportable**   La clé privée utilisée pour générer le certificat doit être exportable. Vous pouvez demander à ce que la clé privée soit exportable lors de la création de la demande de certificat à l’aide de l’Assistant **Nouveau certificat Exchange** dans le Centre d’administration Exchange ou de la cmdlet [New-ExchangeCertificate](https://technet.microsoft.com/fr-fr/library/aa998327\(v=exchg.150\)) dans l’environnement Exchange Management Shell.

  - **Certificat actuel**   Le certificat doit être en cours. Vous ne pouvez pas utiliser de certificat expiré ou révoqué pour créer une approbation de fédération.

  - **Utilisation améliorée de la clé**   Le certificat doit inclure le type d’utilisation améliorée de la clé (EKU) **Authentification du client (1.3.6.1.5.5.7.3.2)**. Ce type d’utilisation permet de prouver votre identité sur un ordinateur distant. Si vous utilisez le Centre d’administration Exchange ou l’environnement Exchange Management Shell pour générer une demande de certificat, ce type d’utilisation est inclus par défaut.

> [!NOTE]
> Étant donné que le certificat n’est pas utilisé pour l’authentification, il n’y a aucune exigence en matière de nom d’objet ou d’autre nom d’objet. Vous pouvez utiliser un certificat dont le nom d’objet est identique au nom d’hôte, au nom de domaine ou à tout autre nom.


Terminologie clé

## Transition vers un nouveau certificat

Le certificat utilisé pour créer l’approbation de fédération est désigné comme certificat actuel. Cependant, vous devrez peut-être installer et utiliser régulièrement un nouveau certificat pour l’approbation de fédération. Par exemple, vous devrez éventuellement utiliser un nouveau certificat si le certificat actuel expire ou pour répondre à un nouveau besoin de l’entreprise ou à un impératif de sécurité. Pour assurer une transition transparente vers un nouveau certificat, vous devez installer le nouveau certificat sur votre serveur Exchange 2013 et configurer l’approbation de fédération pour le désigner comme nouveau certificat. Exchange 2013 distribue automatiquement le nouveau certificat à tous les autres serveurs Exchange 2013 de l’organisation. Selon votre topologie Active Directory, la distribution du certificat peut prendre un certain temps. Vous pouvez vérifier l’état du certificat à l’aide de la cmdlet [Test-FederationTrustCertificate](https://technet.microsoft.com/fr-fr/library/dd335228\(v=exchg.150\)) dans l’environnement Exchange Management Shell.

Une fois l’état de distribution du certificat vérifié, vous pouvez configurer l’approbation afin qu’elle utilise le nouveau certificat. Après avoir changé de certificat, le certificat actuel est désigné comme certificat précédent, et le nouveau certificat comme certificat actuel. Le nouveau certificat est publié dans le système d’authentification Azure AD et tous les nouveaux jetons remplacés par le système d’authentification Azure AD sont chiffrés à l’aide du nouveau certificat.

> [!NOTE]
> Ce processus de transition de certificat est uniquement utilisé par la fédération. Si vous utilisez le même certificat pour d’autres fonctions d’Exchange 2013 exigeant des certificats, vous devez prendre en compte les fonctionnalités requises lorsque vous envisagez d’obtenir, d’installer ou d’adopter un nouveau certificat.


Terminologie clé

## Considérations relatives au pare-feu pour la fédération

Les fonctionnalités de fédération exigent que les serveurs d’accès au client et de boîtes aux lettres de votre organisation aient un accès sortant à Internet via HTTPS. Vous devez autoriser un accès HTTPS sortant (port 443 pour TCP) à tous les serveurs d’accès au client et de boîtes aux lettres Exchange 2013 de l’organisation.

Pour qu’une organisation externe ait accès aux informations de disponibilité de votre organisation, vous devez publier un serveur d’accès au client sur Internet. Un accès HTTPS entrant depuis Internet vers le serveur d’accès au client est nécessaire. Les serveurs d’accès au client dans les sites Active Directory n’ayant pas de serveur d’accès au client publié sur Internet peuvent utiliser les serveurs d’accès au client dans d’autres sites Active Directory accessibles depuis Internet. Les serveurs d’accès au client qui ne sont pas publiés sur Internet doivent avoir l’URL externe du répertoire virtuel des services web définie avec l’URL accessible aux organisations externes.

[Retour au début](sharing-exchange-2013-help.md)

