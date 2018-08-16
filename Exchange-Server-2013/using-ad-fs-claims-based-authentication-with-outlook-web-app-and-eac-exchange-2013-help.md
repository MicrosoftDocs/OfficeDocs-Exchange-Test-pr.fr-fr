---
title: 'Authentification basée sur les revendications AD FS avec OWA et le CAE'
TOCTitle: Utiliser l'authentification basée sur les revendications AD FS avec Outlook Web App et le CAE
ms:assetid: 919a9bfb-c6df-490a-b2c4-51796b0f0596
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dn635116(v=EXCHG.150)
ms:contentKeyID: 61204573
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Utiliser l'authentification basée sur les revendications AD FS avec Outlook Web App et le CAE

 

_**Sapplique à :** Exchange Server 2013 SP1_

_**Dernière rubrique modifiée :** 2017-04-14_

**Résumé** :

Pour les déploiements d’Exchange 2013 Service Pack 1 (SP1) sur site, une fois les services Active Directory Federation Services (AD FS) installés et configurés, vous pouvez utiliser l’authentification basée sur les revendications AD FS pour vous connecter à Outlook Web App et au CAE. Vous pouvez intégrer AD FS et l’authentification basée sur les revendications à Exchange 2013 SP1. L’authentification basée sur les revendications remplace les méthodes d’authentification traditionnelles, y compris les suivantes :

  - Authentification Windows

  - Authentification par formulaires

  - Authentification Digest

  - Authentification de base

  - Authentification de certificats clients Active Directory

L’authentification est le processus visant à confirmer l’identité d’un utilisateur. Elle vérifie que l’utilisateur est bien la personne qu’il prétend être. L’identité basée sur les revendications est une autre approche de l’authentification. L’authentification basée sur les revendications supprime la gestion de l’authentification de l’application (en l’occurrence, Outlook Web App et le CAE) pour faciliter la gestion des comptes en centralisant l’authentification. Outlook Web App et le CAE ne sont pas en charge de l’authentification des utilisateurs, du stockage des comptes et des mots de passe d’utilisateurs, de la recherche de détails sur l’identité de l’utilisateur, ni de l’intégration à d’autres systèmes d’identité. La centralisation de l’authentification permet de simplifier la mise à niveau vers les méthodes d’authentification à venir.

> [!NOTE]
> OWA pour les périphériques ne prend pas en charge l’authentification basée sur les revendications AD FS.


Plusieurs versions d’AD FS peuvent être utilisées, comme le résume le tableau suivant.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Version d’Windows Server</th>
<th>Installation</th>
<th>Version d’AD FS</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Windows Server 2008 R2</p></td>
<td><p><strong>Téléchargez et installez</strong> AD FS 2.0, qui est un module complémentaire Windows.</p></td>
<td><p>AD FS 2.0</p></td>
</tr>
<tr class="even">
<td><p>Windows Server 2012</p></td>
<td><p>Installez le rôle de serveur AD FS <strong>intégré</strong>.</p></td>
<td><p>AD FS 2.1</p></td>
</tr>
<tr class="odd">
<td><p>Windows Server 2012 R2</p></td>
<td><p>Installez le rôle de serveur AD FS <strong>intégré</strong>.</p></td>
<td><p>AD FS 3.0</p></td>
</tr>
</tbody>
</table>


Les tâches que vous aurez à effectuer ici sont basées sur Windows Server 2012 R2 avec le service de rôle AD FS.

**Vue d’ensemble des étapes requises**

Step 1 - Review the certificate requirements for AD FS

Step 2 - Install and configure Active Directory Federation Services (AD FS)

Étape 3 - Créer une approbation de partie de confiance et des règles de revendication personnalisées pour Outlook Web App et le CAE

Étape 4 - Installer le service de rôle de proxy d'application web (facultatif)

Étape 5 - Configurer le service de rôle de proxy d'application web (facultatif)

Étape 6 - Publier Outlook Web App et le CAE à l'aide du proxy d'application web (facultatif)

Étape 7 - Configurer Exchange 2013 pour utiliser l'authentification AD FS

Étape 8 - Activer l'authentification AD FS sur les répertoires virtuels OWA et ECP

Étape 9 - Redémarrer ou recycler Internet Information Services (IIS)

Étape 10 - Tester les revendications AD FS pour Outlook Web App et le CAE

Additional information you might want to know

## Que dois-je savoir avant de commencer ?

  - Vous devez au moins installer des serveurs Windows Server 2012 R2 séparés : un en tant que contrôleur de domaine qui utilise les services de domaine Active Directory (AD DS), un serveur Exchange 2013, un serveur proxy d’application web et un serveur Active Directory Federation Services (AD FS). Vérifiez que toutes les mises à jour sont installées.

  - Installez les services AD DS sur le nombre approprié de serveurs Windows Server 2012 R2 dans votre organisation. Vous pouvez également utiliser l’option **Notifications** dans **Gestionnaire de serveur**\>**Tableau de bord** pour **promouvoir ce serveur en contrôleur de domaine**.

  - Installez le nombre approprié de serveurs d’accès au client et de boîte aux lettres pour votre organisation. Vérifiez que toutes les mises à jour sont installées, y compris SP1, sur tous les serveurs Exchange 2013 de votre organisation. Pour télécharger le SP1, consultez la rubrique [Mises à jour pour Exchange 2013](updates-for-exchange-2013-exchange-2013-help.md).

  - Le déploiement du proxy d’application web sur un serveur requiert des autorisations d’administrateur local. Pour pouvoir déployer un proxy d’application web, vous devez déployer AD FS sur un serveur exécutant Windows Server 2012 R2 dans votre organisation.

  - Installez et configurez le rôle AD FS, puis créez des règles de revendications et des approbations de partie de confiance sur Windows Server 2012 R2. Pour ce faire, connectez-vous avec un compte d’utilisateur qui est membre du groupe Administrateurs de domaine, Administrateurs d’entreprise ou Administrateurs locaux.

  - Déterminez les autorisations requises pour Exchange 2013 en consultant la rubrique [Autorisations des fonctionnalités](feature-permissions-exchange-2013-help.md).

  - Vous devez posséder les autorisations de gestion d’Outlook Web App. Pour connaître les autorisations dont vous avez besoin, consultez l’entrée « Autorisations Outlook Web App » dans la rubrique [Autorisations des clients et des périphériques mobiles](clients-and-mobile-devices-permissions-exchange-2013-help.md).

  - Vous devez posséder les autorisations de gestion du CAE. Pour connaître les autorisations nécessaires, consultez l’entrée « Connectivité du Centre d’administration Exchange » dans la rubrique [Autorisations d’infrastructure Exchange et Shell](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md).

  - Pour effectuer certaines procédures, vous pouvez utiliser uniquement le Shell. Pour en savoir plus sur l’ouverture de l’environnement de ligne de commande Exchange Management Shell dans votre organisation Exchange sur site, consultez la rubrique [Ouvrir le Shell](https://technet.microsoft.com/fr-fr/library/dd638134\(v=exchg.150\)).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.


## Étape 1 – Vérifier les exigences de certificats pour AD FS

Les certificats jouent un rôle crucial dans la sécurisation des communications entre les serveurs Exchange 2013 SP1, les clients web tels qu’Outlook Web App et le CAE, les serveurs Windows Server 2012 R2, y compris les serveurs Active Directory Federation Services (AD FS) et les serveurs proxy d’application web. Les exigences pour les certificats varient selon que vous configurez un serveur AD FS, un proxy AD FS ou un serveur proxy d’application web. Les certificats qui sont utilisés pour les services AD FS, y compris les certificats SSL et de signature de jetons, doivent être importés dans le magasin Autorités de certification racine de confiance sur tous les serveurs Exchange, AD FS et proxy d’application web. L’empreinte du certificat importé est également utilisée sur les serveurs Exchange 2013 SP1 lorsque vous utilisez la cmdlet [Set-OrganizationConfig](https://technet.microsoft.com/fr-fr/library/aa997443\(v=exchg.150\)).

Dans toute conception AD FS, divers certificats doivent être utilisés pour sécuriser la communication entre les utilisateurs sur Internet et les serveurs AD FS. Chaque serveur de fédération doit disposer d’un certificat de communication de service ou d’un certificat SSL (Secure Socket Layer), et d’un certificat de signature de jetons pour que les serveurs AD FS, les contrôleurs de domaine Active Directory, et les serveurs Exchange 2013 puissent communiquer et procéder à l’authentification. En fonction de vos exigences de sécurité et de votre budget, définissez attentivement ceux de vos certificats qui seront obtenus par une autorité de certification publique ou une autorité de certification d’entreprise. Si vous voulez installer et configurer une autorité de certification racine ou subordonnée d’entreprise, vous pouvez utiliser les services de certificats Active Directory (AD CS). Pour en savoir plus sur les services AD CS, consultez la rubrique [Vue d’ensemble des services de certificats Active Directory](https://go.microsoft.com/fwlink/?linkid=392697).

Bien que les services AD FS ne nécessitent pas de certificats émis par une autorité de certification, le certificat SSL (qui est également utilisé par défaut comme certificat de communications de service) doit être approuvé par les clients AD FS. Nous vous recommandons de ne pas utiliser de certificats auto-signés. Les serveurs de fédération utilisent un certificat SSL pour sécuriser le trafic de services web pour la communication SSL avec les clients web et les proxys de serveur de fédération. Étant donné que le certificat SSL doit être approuvé par les ordinateurs clients, nous vous recommandons d’utiliser un certificat signé par une autorité de certification approuvée. Tous les certificats que vous sélectionnez doivent posséder une clé privée correspondante. Après avoir reçu un certificat d’une autorité de certification (d’entreprise ou publique), assurez-vous que tous les certificats sont importés dans le magasin Autorités de certification racine de confiance sur tous les serveurs. Vous pouvez importer des certificats dans le magasin avec le composant logiciel enfichable MMC **Certificats** ou distribuer les certificats à l’aide des services de certificats Active Directory. Si le certificat que vous avez importé expire, vous devez importer manuellement un autre certificat valide.

> [!NOTE]
> Si vous utilisez le certificat de signature de jetons auto-signé d’AD FS, vous devez l’importer dans le magasin Autorités de certification racine sur tous vos serveurs Exchange 2013. Si le certificat de signature de jetons auto-signé n’est pas utilisé et que le proxy d’application web est déployé, vous devez mettre à jour la clé publique dans la configuration du proxy d’application web et toutes les approbations de partie de confiance AD FS.


Lorsque vous configurez Exchange 2013 SP1, AD FS et le proxy d’application web, suivez ces recommandations de certificat :

  - **Serveurs de boîte aux lettres**   Les certificats qui sont utilisés sur les serveurs de boîte aux lettres sont des certificats auto-signés car ils sont créés lors de l’installation d’Exchange 2013. Comme tous les clients se connectent à un serveur de boîte aux lettres Exchange 2013 via un serveur d’accès au client Exchange 2013, les seuls certificats que vous devez gérer sont ceux des serveurs d’accès au client.

  - **Serveurs d’accès au client**   Un certificat SSL utilisé pour les communications de service est requis. Si votre certificat SSL existant comprend déjà le nom de domaine complet (FQDN) que vous utilisez pour configurer le point de terminaison d’approbation de partie de confiance, aucun certificat supplémentaire n’est nécessaire.

  - **AD FS**   Deux types de certificats sont requis par AD FS :
    
      - Certificat SSL utilisé pour les communications de service
        
          - Nom de l’objet : **adfs.contoso.com** (nom de déploiement AD FS)
        
          - Autre nom de l’objet (SAN) : aucun
    
      - Certificat de signature de jetons
        
          - Nom de l’objet : **tokensigning.contoso.com**
        
          - Autre nom de l’objet (SAN) : aucun
        
        > [!NOTE]
        > Lorsque vous remplacez le certificat de signature de jetons sur AD FS, les approbations de partie de confiance existantes doivent être mises à jour pour utiliser le nouveau certificat de signature de jetons.


  - **Proxy d’application web**
    
      - Certificat SSL utilisé pour les communications de service
        
          - Nom de l’objet : **owa.contoso.com**
        
          - Autre nom de l’objet (SAN) : aucun
        
        > [!NOTE]
        > Si votre URL externe de proxy d’application web est identique à votre URL interne, vous pouvez réutiliser le certificat SSL Exchange.
    
      - Certificat SSL de proxy AD FS
        
          - Nom de l’objet : **adfs.contoso.com** (nom de déploiement AD FS)
        
          - Autre nom de l’objet (SAN) : aucun
    
      - Certificat de signature de jetons - Ce certificat sera automatiquement copié à partir d’AD FS au cours des étapes suivantes. Si ce certificat est utilisé, il doit être approuvé par les serveurs Exchange 2013 de votre organisation.

Pour plus d’informations sur les certificats, consultez la section relative aux exigences de certificats dans [Vérifier les conditions requises pour le déploiement d’AD FS](https://go.microsoft.com/fwlink/?linkid=392699).

> [!NOTE]
> Un certificat de chiffrement SSL est toujours nécessaire pour Outlook Web App et le CAE, même si vous disposez d’un certificat SSL pour AD FS. Le certificat SSL est utilisé sur les répertoires virtuels OWA et ECP.


## Étape 2 – Installer et configurer les services AD FS (Active Directory Federation Services)

Dans Windows Server 2012 R2, AD FS offre une fédération des identités sécurisée et simplifiée, ainsi que des fonctions d’authentification unique (SSO) web. AD FS comprend un service de fédération qui active l’authentification SSO web basée sur le navigateur, multifacteur et basée sur les revendications. AD FS simplifie l’accès aux systèmes et aux applications à l’aide de l’authentification basée sur les revendications et du mécanisme d’autorisation d’accès, ce qui permet de maintenir la sécurité d’application.

Pour installer AD FS sur Windows Server 2012 R2 :

1.  Ouvrez le **Gestionnaire de serveur** sur l’écran **Démarrer** ou sur la barre des tâches du bureau. Cliquez sur **Ajouter des rôles et des fonctionnalités** dans le menu **Gérer**.

2.  Sur la page **Avant de commencer**, cliquez sur **Suivant**.

3.  Sur la page **Sélectionner le type d’installation**, cliquez sur **Installation basée sur un rôle ou une fonctionnalité**, puis sur **Suivant**.

4.  Sur la page **Sélectionner le serveur de destination**, cliquez sur **Sélectionner un serveur du pool de serveurs**, vérifiez que l’ordinateur local est sélectionné, puis cliquez sur **Suivant**.

5.  Sur la page **Sélectionner des rôles de serveurs**, cliquez sur **Services AD FS (Active Directory Federation Services)**, puis cliquez sur **Suivant**.
    
    Sur la page **Sélectionner des fonctionnalités**, cliquez sur **Suivant**. Les fonctionnalités ou conditions préalables requises sont déjà sélectionnées pour vous. Vous n’avez pas besoin de sélectionner d’autres fonctionnalités.

6.  Sur la page **Services AD FS (Active Directory Federation Services)**, cliquez sur **Suivant**.

7.  Sur la page **Confirmer les sélections d’installation**, sélectionnez **Redémarrer automatiquement le serveur de destination, si nécessaire**, puis cliquez sur **Installer**.
    
    > [!NOTE]
    > Ne fermez pas l’Assistant pendant le processus d’installation.


Après avoir installé les serveurs AD FS requis et généré les certificats requis, vous devez configurer AD FS, puis vérifier que les services AD FS fonctionnent correctement. Vous pouvez également utiliser la liste de contrôle ci-après pour vous aider à installer et configurer AD FS : [Liste de contrôle : Configuration d’un serveur de fédération](https://go.microsoft.com/fwlink/?linkid=392700).

Pour configurer Active Directory Federation Services :

1.  Sur la page **Progression de l’installation**, dans la fenêtre sous **Services AD FS (Active Directory Federation Services)**, cliquez sur **Configurer le service FS (Federation Service) sur ce serveur**. L’Assistant Configuration d’Active Directory Federation Service s’ouvre.

2.  Sur la page **Bienvenue**, cliquez sur **Créer le premier serveur de fédération dans une batterie de serveurs de fédération**, puis cliquez sur **Suivant**.

3.  Sur la page **Connexion à AD DS**, spécifiez un compte avec des droits d’administrateur de domaine pour le domaine Active Directory auquel cet ordinateur est associé, puis cliquez sur **Suivant**. Si vous devez sélectionner un autre utilisateur, cliquez sur **Modifier**.

4.  Sur la page **Spécifier les propriétés de service**, effectuez les actions suivantes, puis cliquez sur **Suivant** :
    
      - Importez le certificat SSL que vous avez obtenu précédemment à partir des services AD CS ou d’une autorité de certification publique. Ce certificat est le certificat d’authentification de service requis. Accédez à l’emplacement de votre certificat SSL. Pour plus de détails sur la création et l’importation de certificats SSL, consultez la rubrique [Certificats de serveur](https://go.microsoft.com/fwlink/?linkid=392703).
    
      - Entrez un nom pour votre service de fédération, par exemple, **adfs.contoso.com**.
    
      - Pour indiquer un nom d’affichage pour votre service de fédération, tapez le nom de votre organisation, par exemple, **Contoso, Ltd.**.

5.  Sur la page **Spécifier un compte de service**, sélectionnez **Utiliser un compte d’utilisateur de domaine ou de service administré de type groupe existant**, puis spécifiez le compte GMSA (FsGmsa) que vous avez créé lors de la création du contrôleur de domaine. Incluez les paramètres de compte, puis cliquez sur **Suivant**.
    
    > [!NOTE]
    > Le compte de service géré globalement (GMSA) est un compte qui doit être créé lors de la configuration d’un contrôleur de domaine. Le compte GMSA est obligatoire lors de l’installation et la configuration d’AD FS. Si vous n’avez pas encore créé ce compte, exécutez la commande Windows PowerShell suivante. Elle crée le compte pour le domaine contoso.com et le serveur AD FS :


6.  Exécutez la commande suivante.
    
        Add-KdsRootKey -EffectiveTime (Get-Date).AddHours(-10)

7.  Cet exemple crée un nouveau compte de GMSA nommé FsGmsa pour le Service de fédération nommé adfs.contoso.com. Le nom du Service de fédération est la valeur qui est visible pour les clients.
    
        New-ADServiceAccount FsGmsa -DNSHostName adfs.contoso.com -ServicePrincipalNames http/adfs.contoso.com

8.  Sur la page **Spécifier une base de données de configuration**, sélectionnez **Créer une base de données sur ce serveur à l’aide de la base de données interne Windows**, puis cliquez sur **Suivant**.

9.  Sur la page **Examiner les options**, vérifiez vos sélections de configuration. Vous pouvez éventuellement utiliser le bouton **Afficher le script** pour automatiser des installations AD FS supplémentaires. Cliquez sur **Suivant**.

10. Sur la page **Vérification des conditions préalables**, vérifiez que toutes les vérifications préalables ont été correctement effectuées, puis cliquez sur **Configurer**.

11. Sur la page **Progression de l’installation**, vérifiez que tout est correctement installé, puis cliquez sur **Fermer**.

12. Sur la page **Résultats**, vérifiez les résultats, vérifiez que la configuration s’est déroulée correctement, puis cliquez sur **Étapes ultérieures requises pour le déploiement de votre service FS (Federation Service)**.

Les commandes de PowerShell suivantes Windows font la même chose que les étapes précédentes.
```
    Import-Module ADFS
```
```
    Install-AdfsFarm -CertificateThumbprint 0E0C205D252002D535F6D32026B6AB074FB840E7 -FederationServiceDisplayName "Contoso Corporation" -FederationServiceName adfs.contoso.com -GroupServiceAccountIdentifier "contoso\FSgmsa`$"
```

Pour plus de détails et d’informations sur la syntaxe, consultez la page relative à [Install-AdfsFarm](https://go.microsoft.com/fwlink/?linkid=392704).

Pour vérifier l’installation : Sur le serveur AD FS, ouvrez votre navigateur web, puis accédez à l’URL des métadonnées de fédération, par exemple, **https://adfs.contoso.com/federationmetadata/2007-06/federationmetadata.xml**.

## Étape 3 - Créer une approbation de partie de confiance et des règles de revendication personnalisées pour Outlook Web App et le CAE

Pour toutes les applications et tous les services que vous souhaitez publier via le proxy d’application web, vous devez configurer une approbation de partie de confiance sur le serveur AD FS. Pour les déploiements avec plusieurs sites Active Directory qui utilisent des espaces de noms distincts, une approbation de partie de confiance pour Outlook Web App et le CAE doit être ajoutée pour chaque espace de noms.

Le CAE utilise le répertoire virtuel ECP. Vous pouvez afficher ou configurer les paramètres du CAE à l’aide des cmdlets [Get-EcpVirtualDirectory](https://technet.microsoft.com/fr-fr/library/dd351058\(v=exchg.150\)) et [Set-EcpVirtualDirectory](https://technet.microsoft.com/fr-fr/library/dd297991\(v=exchg.150\)). Pour accéder au CAE, vous devez utiliser un navigateur web et accéder à **http://server1.contoso.com/ecp**.

> [!NOTE]
> L’inclusion de la barre oblique finale <strong>/</strong> dans les exemples d’URL ci-dessous est intentionnelle. Il est important de s’assurer que les approbations de partie de confiance AD FS et les URI d’audience Exchange <strong>sont identiques</strong>. Cela signifie que les approbations de partie de confiance AD FS et les URI d’audience Exchange doivent <strong>avoir</strong> ou <strong>générer</strong> des barres obliques finales dans leur URL. Les exemples de cette section contiennent la barre oblique finale <strong>/</strong> à la fin de chaque URL se terminant par « owa » ( /owa/) ou « ecp » ( /ecp/).


Pour Outlook Web App, pour créer des approbations de partie de confiance à l’aide du composant logiciel enfichable de gestion d’AD FS dans Windows Server 2012 R2 :

1.  Dans **Gestionnaire de serveur**, cliquez sur **Outils**, puis sélectionnez **Gestion AD FS**.

2.  Dans le **composant logiciel enfichable AD FS**, sous **Relations AD FS/d’approbation**, cliquez avec le bouton droit sur **Approbations de partie de confiance**, puis cliquez sur **Ajouter une approbation de partie de confiance** pour ouvrir l’Assistant **Ajout d’une approbation de partie de confiance**.

3.  Sur la page **Bienvenue**, cliquez sur **Démarrer**.

4.  Sur la page **Sélectionner la source de données**, cliquez sur **Entrer les données relatives à la partie de confiance manuellement**, puis cliquez sur **Suivant**.

5.  Sur la page **Spécifier le nom d’affichage**, dans la zone **Nom d’affichage**, tapez **Outlook Web App**, puis sous **Notes**, tapez une description de cette approbation de partie de confiance (comme **This is a trust for https://mail.contoso.com/owa**) et cliquez sur **Suivant**.

6.  Sur la page **Choix d’un profil**, cliquez sur **Profil AD FS**, puis sur **Suivant**.

7.  Sur la page **Configurer le certificat**, cliquez sur **Suivant**.

8.  Sur la page **Configurer l’URL**, cliquez sur **Activer la prise en charge pour le protocole WS-Federation Passive**, sous **URL de protocole WS-Federation Passive de partie de confiance**, **type https://mail.contoso.com/owa**, puis cliquez sur **Suivant**.

9.  Sur la page **Configurer les identificateurs**, indiquez un ou plusieurs identificateurs pour cette partie de confiance, cliquez sur **Ajouter** pour les ajouter à la liste, puis cliquez sur **Suivant**.

10. Sur la page **Configurer l’authentification multifacteur maintenant ?**, sélectionnez **Configurer les paramètres d’authentification multifacteur pour cette approbation de partie de confiance**.

11. Sur la page **Configurer l’authentification multifacteur**, vérifiez que l’option **Je ne veux pas configurer les paramètres d’authentification multifacteur pour cette approbation de partie de confiance pour le moment** est sélectionnée, puis cliquez sur **Suivant**.

12. Sur la page **Choisir les règles d’autorisation d’émission**, sélectionnez **Autoriser tous les utilisateurs à accéder à cette partie de confiance**, puis cliquez sur **Suivant**.

13. Sur la page **Prêt à ajouter l’approbation**, vérifiez les paramètres, puis cliquez sur **Suivant** pour enregistrer les informations relatives à votre approbation de partie de confiance.

14. Sur la page **Terminer**, vérifiez que l’option **Ouvrir la boîte de dialogue Modifier les règles de revendication pour cette approbation de partie de confiance à la fermeture de l’Assistant** n’est pas sélectionnée, puis cliquez sur **Fermer**.

Pour créer une approbation de partie de confiance pour le CAE, vous devez répéter ces étapes et créer une seconde approbation de partie de confiance, mais au lieu d’entrer **Outlook Web App** pour le nom d’affichage, saisissez **EAC**. Pour la description, entrez **This is a trust for the Exchange Admin Center**, et l’option **URL de protocole WS-Federation Passive de partie de confiance** doit être définie sur **https://mail.contoso.com/ecp**.

Dans un modèle d’identité basée sur les revendications, la fonction d’Active Directory Federation Services (ADFS) en tant que service de fédération est d’émettre un jeton contenant un ensemble de revendications. Les règles de revendication régissent les décisions relatives aux revendications émises par AD FS. Les règles de revendication et toutes les données de configuration de serveur sont stockées dans la base de données de configuration AD FS.

Vous devez créer deux règles de revendication :

  - SID d’utilisateur Active Directory

  - Active Directory UPN

Pour ajouter les règles de revendication requises :

1.  Dans **Gestionnaire de serveur**, cliquez sur **Outils**, puis sur **Gestion AD FS**.

2.  Dans l’arborescence de la console, sous **Relations AD FS/d’approbation**, cliquez sur **Approbations de fournisseur de revendications** ou **Approbations de partie de confiance**, puis cliquez sur l’approbation de partie de confiance pour Outlook Web App.

3.  Dans la fenêtre **Approbations de partie de confiance**, cliquez avec le bouton droit sur l’approbation Outlook Web App, puis cliquez sur **Modifier les règles de revendication**.

4.  Dans la fenêtre **Modifier les règles de revendication**, sur l’onglet **Règles de transformation d’émission**, cliquez sur **Ajouter une règle** pour lancer l’Assistant Ajout de règle de revendication de transformation.

5.  Sur la page **Sélectionner un modèle de règle**, sous **Modèle de règle de revendication**, sélectionnez **Envoyer des revendications à l’aide d’une règle personnalisée** dans la liste, puis cliquez sur **Suivant**.

6.  Sur la page **Configurer la règle**, à l’étape **Choisir le type de règle**, sous **Nom de la règle de revendication**, entrez le nom de la règle de revendication. Utilisez un nom descriptif pour la règle de revendication, par exemple, **ActiveDirectoryUserSID**. Sous **Règle personnalisée**, entrez la syntaxe de langage de règle de revendication suivante pour cette règle :
    
        c:[Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname", Issuer == "AD AUTHORITY"] => issue(store = "Active Directory", types = ("http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid"), query = ";objectSID;{0}", param = c.Value);

7.  Sur la page **Configurer la règle**, cliquez sur **Terminer**.

8.  Dans la fenêtre **Modifier les règles de revendication**, sur l’onglet **Règles de transformation d’émission**, cliquez sur **Ajouter une règle** pour lancer l’Assistant Ajout de règle de revendication de transformation.

9.  Sur la page **Sélectionner un modèle de règle**, sous **Modèle de règle de revendication**, sélectionnez **Envoyer des revendications à l’aide d’une règle personnalisée** dans la liste, puis cliquez sur **Suivant**.

10. Sur la page **Configurer la règle**, à l’étape **Choisir le type de règle**, sous **Nom de la règle de revendication**, entrez le nom de la règle de revendication. Utilisez un nom descriptif pour la règle de revendication, par exemple, **ActiveDirectoryUPN**. Sous **Règle personnalisée**, entrez la syntaxe de langage de règle de revendication suivante pour cette règle :
    
        c:[Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname", Issuer == "AD AUTHORITY"] => issue(store = "Active Directory", types = ("http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn"), query = ";userPrincipalName;{0}", param = c.Value);

11. Cliquez sur **Terminer**.

12. Dans la fenêtre **Modifier les règles de revendication**, cliquez sur **Appliquer**, puis sur **OK**.

13. Répétez les étapes 3 à 12 de cette procédure pour l’approbation de partie de confiance du CAE.

Vous pouvez également créer des approbations de partie de confiance et des règles de revendication à l’aide de Windows PowerShell :

1.  Créez deux fichiers .txt : IssuanceAuthorizationRules.txt et IssuanceTransformRules.txt.

2.  Importez leur contenu dans deux variables.

3.  Exécutez les deux cmdlets suivantes pour créer les approbations de partie de confiance. Dans cet exemple, les règles de revendication seront également configurées.

**IssuanceAuthorizationRules.txt contient :** 

    @RuleTemplate = "AllowAllAuthzRule" => issue(Type = "http://schemas.microsoft.com/authorization/claims/permit", Value = "true");

**IssuanceTransformRules.txt contient :** 
```
    @RuleName = "ActiveDirectoryUserSID" c:[Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname", Issuer == "AD AUTHORITY"] => issue(store = "Active Directory", types = ("http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid"), query = ";objectSID;{0}", param = c.Value); 
 
    @RuleName = "ActiveDirectoryUPN" c:[Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname", Issuer == "AD AUTHORITY"] => issue(store = "Active Directory", types = ("http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn"), query = ";userPrincipalName;{0}", param = c.Value);
```

**Exécutez les commandes suivantes :** 
```
    [string]$IssuanceAuthorizationRules=Get-Content -Path C:\IssuanceAuthorizationRules.txt
   
    [string]$IssuanceTransformRules=Get-Content -Path c:\IssuanceTransformRules.txt
 
    Add-ADFSRelyingPartyTrust -Name "Outlook Web App" -Enabled $true -Notes "This is a trust for https://mail.contoso.com/owa/" -WSFedEndpoint https://mail.contoso.com/owa/ -Identifier https://mail.contoso.com/owa/ -IssuanceTransformRules $IssuanceTransformRules -IssuanceAuthorizationRules $IssuanceAuthorizationRules
 
    Add-ADFSRelyingPartyTrust -Name "Exchange Admin Center (EAC)" -Enabled $true -Notes "This is a trust for https://mail.contoso.com/ecp/" -WSFedEndpoint https://mail.contoso.com/ecp/ -Identifier https://mail.contoso.com/ecp/ -IssuanceTransformRules $IssuanceTransformRules -IssuanceAuthorizationRules $IssuanceAuthorizationRules
```

## Étape 4 – Installer le service de rôle de proxy d’application web (facultatif)

> [!NOTE]
> Les étapes 4, 5 et 6 sont destinées aux utilisateurs qui veulent publier ECP et OWA pour Exchange à l’aide du proxy d’application web, et que ce dernier effectue l’authentification AD FS. Toutefois, la publication d’Exchange avec le proxy d’application web n’étant pas obligatoire, vous pouvez passer à l’étape 7 si vous n’utilisez pas le proxy d’application web et ne voulez pas qu’Exchange effectue l’authentification AD FS lui-même.


Le proxy d’application web est un nouveau service de rôle d’accès à distance dans Windows Server 2012 R2. Le proxy d’application web offre une fonctionnalité de proxy inverse pour les applications web de votre réseau d’entreprise, pour permettre aux utilisateurs d’accéder aux différents appareils qu’ils utilisent depuis l’extérieur du réseau d’entreprise. Le proxy d’application web authentifie au préalable l’accès aux applications web à l’aide des services Active Directory Federation Services (AD FS) et fonctionne également en tant que proxy AD FS. Même si le proxy d’application web n’est pas obligatoire, il est recommandé lorsque des clients externes peuvent accéder à AD FS. Toutefois, l’accès hors connexion à Outlook Web App n’est pas pris en charge lorsque l’authentification AD FS est utilisée via le proxy d’application web. Pour plus d’informations sur l’intégration avec le proxy d’application web, consultez la rubrique [Installation et configuration du proxy d’application web pour les applications internes de publication](https://go.microsoft.com/fwlink/?linkid=392705)

> [!WARNING]
> Vous ne pouvez pas installer le proxy d’application web sur le serveur où AD FS est installé.


Pour déployer le proxy d’application web, vous devez installer le rôle de serveur d’accès à distance avec le service de rôle de proxy d’application web sur un serveur qui fera office de serveur proxy d’application web. Pour installer le service de rôle de proxy d’application web :

1.  Sur le serveur proxy d’application web, dans **Gestionnaire de serveur**, cliquez sur **Gérer**, puis sur **Ajouter des rôles et des fonctionnalités**.

2.  Dans l’Assistant Ajout de rôles et de foncitonnalités, cliquez sur **Suivant** trois fois pour accéder à la page **Rôles de serveur**.

3.  Sur la page **Rôles de serveur**, sélectionnez **Accès à distance** dans la liste, puis cliquez sur **Suivant**.

4.  Sur la page **Foncitonnalités**, cliquez sur **Suivant**.

5.  Sur la page **Accès à distance**, consultez les informations, puis cliquez sur **Suivant** :

6.  Sur la page **Services de rôle**, sélectionnez **Proxy d’application web**. Ensuite, dans la fenêtre **Assistant Ajout de rôles et de fonctionnalités**, cliquez sur **Ajouter des fonctionnalités**, puis cliquez sur **Suivant**.

7.  Dans la fenêtre **Confirmation**, cliquez sur **Installer**. Vous pouvez également sélectionner **Redémarrer automatiquement le serveur de destination, si nécessaire**.

8.  Dans la boîte de dialogue **Progression de l’installation**, vérifiez que l’installation s’est correctement déroulée, puis cliquez sur **Fermer**.

La cmdlet Windows PowerShell suivante effectue les mêmes actions que les étapes précédentes.

    Install-WindowsFeature Web-Application-Proxy -IncludeManagementTools

## Étape 5 – Configurer le service de rôle de proxy d’application web (facultatif)

Pour vous connecter au serveur AD FS, vous devez configurer le proxy d’application web. Répétez cette procédure pour tous les serveurs que vous souhaitez déployer en tant que serveurs proxy d’application web.

Pour configurer le service de rôle d’application web :

1.  Sur le serveur proxy d’application web, dans **Gestionnaire de serveur**, cliquez sur **Outils**, puis cliquez sur **Gestion de l’accès à distance**.

2.  Dans le volet **Configuration**, cliquez sur **Proxy d’application web**.

3.  Dans la console **Gestion de l’accès à distance**, dans le volet central, cliquez sur **Exécuter l’Assistant Configuration de proxy d’application web**.

4.  Dans l’Assistant Configuration de proxy d’application web, dans la boîte de dialogue **Bienvenue**, cliquez sur **Suivant**.

5.  Sur la page **Serveur de fédération**, effectuez les actions suivantes, puis cliquez sur **Suivant** :
    
      - Dans la zone **Nom du service FS (Federation Service)**, entrez le nom de domaine complet (FQDN) du serveur AD FS, par exemple, **adfs.contoso.com**.
    
      - Dans les zones **Nom d’utilisateur** et **Mot de passe**, entrez les informations d’identification d’un compte d’administrateur local sur les serveurs AD FS.

6.  Dans la boîte de dialogue **Certificat de proxy AD FS**, dans la liste des certificats actuellement installés sur le serveur proxy d’application web, sélectionnez le certificat que le proxy d’application web doit utiliser pour la fonctionnalité de proxy AD FS, puis cliquez sur **Suivant**. Le certificat que vous choisissez ici doit être celui dont l’objet est le nom du service de fédération, par exemple, **adfs.contoso.com**.

7.  Dans la boîte de dialogue **Confirmation** vérifiez les paramètres. Si nécessaire, vous pouvez copier la cmdlet Windows PowerShell pour automatiser des installations supplémentaires. Cliquez sur **Configurer**.

8.  Dans la boîte de dialogue **Résultats**, vérifiez que la configuration s’est correctement déroulée, puis cliquez sur **Fermer**.

La cmdlet Windows PowerShell suivante effectue les mêmes actions que les étapes précédentes.

    Install-WebApplicationProxy -CertificateThumprint 1a2b3c4d5e6f1a2b3c4d5e6f1a2b3c4d5e6f1a2b -FederationServiceName adfs.contoso.com

## Étape 6 – Publier Outlook Web App et le CAE à l’aide du proxy d’application web (facultatif)

À l’étape 3, vous avez créé des approbations de partie reposant sur les revendications pour Outlook Web App et le CAE, et vous devez désormais publier ces deux applications. Mais avant cela, vérifiez qu’une approbation de partie de confiance a bien été créée pour ces deux applications, que vous disposez d’un certificat sur le serveur proxy d’application web et qu’il est compatible avec Outlook Web App et le CAE. Dans la console de gestion AD FS, vous devez définir chaque point de terminaison AD FS qui doit être publié par le proxy d’application web sur **Proxy activé**.

Suivez les étapes pour publier Outlook Web App à l’aide du proxy d’application web. Pour le CAE, répétez ces étapes. Lorsque vous publiez le CAE, vous devez changer le nom, l’URL externe, le certificat externe et l’URL principale.

Pour publier Outlook Web App et le CAE à l’aide du proxy d’application web :

1.  Sur le serveur proxy d’application web, dans la console **Gestion de l’accès à distance**, dans le volet **Navigation**, cliquez sur **Proxy d’application web**, puis dans le volet **Tâches**, cliquez sur **Publier**.

2.  Dans l’Assistant Publication d’une nouvelle application, sur la page **Bienvenue**, cliquez sur **Suivant**.

3.  Sur la page **Pré-authentification**, cliquez sur **Services AD FS (Active Directory Federation Services)**, puis cliquez sur **Suivant**.

4.  Sur la page **Partie de confiance**, dans la liste des parties de confiance, sélectionnez-en une pour l’application que vous souhaitez publier, puis cliquez sur **Suivant**.

5.  Sur la page **Paramètres de publication**, effectuez les opérations suivantes et cliquez sur **Suivant** :
    
    1.  Dans la zone **Nom**, entrez un nom convivial pour l’application. Ce nom est utilisé uniquement dans la liste des applications publiées dans la **console Gestion de l’accès à distance**. Vous pouvez utiliser **OWA** et **EAC** pour les noms.
    
    2.  Dans la zone **URL externe**, entrez l’URL externe pour cette application, par exemple, **https://external.contoso.com/owa** pour Outlook Web App et **https://external.contoso.com/ecp** pour le CAE.
    
    3.  Dans la liste **Certificat externe**, sélectionnez un certificat dont le nom d’objet correspond au nom d’hôte de l’URL externe.
    
    4.  Dans la zone **URL du serveur principal**, entrez l’URL du serveur principal. Notez que cette valeur est saisie automatiquement lorsque vous entrez l’URL externe et que vous devez la modifier uniquement si l’URL du serveur principal est différente, par exemple, **https://mail.contoso.com/owa** pour Outlook Web App et **https://mail.contoso.com/ecp** pour le CAE.
    
    > [!NOTE]
    > Le proxy d’application web peut convertir des noms d’hôte en URL, mais ne peut pas convertir les chemins d’accès. Par conséquent, vous pouvez entrer des noms d’hôte différents, mais vous devez entrer le même chemin. Par exemple, vous pouvez entrer l’URL externe <em>https://external.contoso.com/app1/</em> et l’URL de serveur principal <em>https://mail.contoso.com/app1/</em>. Cependant, vous ne pouvez pas entrer l’URL externe <em>https://external.contoso.com/app1/</em> et l’URL de serveur principal <em>https://mail.contoso.com/internal-app1/</em>.


6.  Sur la page **Confirmation**, vérifiez les paramètres, puis cliquez sur **Publier**. Vous pouvez copier la commande Windows PowerShell pour configurer des applications publiées supplémentaires.

7.  Sur la page **Résultats**, assurez-vous que l’application a été correctement publiée, puis cliquez sur **Fermer**.

La cmdlet Windows PowerShell suivante effectue les mêmes tâches que la procédure précédente pour Outlook Web App.

    Add-WebApplicationProxyApplication -BackendServerUrl 'https://mail.contoso.com/owa/' -ExternalCertificateThumbprint 'E9D5F6CDEA243E6E62090B96EC6DE873AF821983' -ExternalUrl 'https://external.contoso.com/owa/' -Name 'OWA' -ExternalPreAuthentication ADFS -ADFSRelyingPartyName 'Outlook Web App'

La cmdlet Windows PowerShell suivante effectue les mêmes tâches que la procédure précédente pour le CAE.

    Add-WebApplicationProxyApplication -BackendServerUrl 'https://mail.contoso.com/ecp/' -ExternalCertificateThumbprint 'E9D5F6CDEA243E6E62090B96EC6DE873AF821983' -ExternalUrl 'https://external.contoso.com/ecp/' -Name 'EAC' -ExternalPreAuthentication ADFS -ADFSRelyingPartyName 'Exchange Admin Center'

Une fois ces étapes effectuées, le proxy d’application web effectue l’authentification AD FS pour les clients Outlook Web App et du CAE, et sert également de proxy pour les connexions à Exchange pour leur compte. Vous n’avez pas besoin de configurer Exchange pour l’authentification AD FS ; passez à l’étape 10 pour tester votre configuration.

## Étape 7 – Configurer Exchange 2013 pour utiliser l’authentification AD FS

Lorsque vous configurez AD FS pour l’authentification basée sur les revendications avec Outlook Web App et le CAE dans Exchange 2013, vous devez activer AD FS pour votre organisation Exchange. Vous devez utiliser la cmdlet [Set-OrganizationConfig](https://technet.microsoft.com/fr-fr/library/aa997443\(v=exchg.150\)) pour configurer les paramètres AD FS pour votre organisation :

  - Définissez l’émetteur AD FS sur **https://adfs.contoso.com/adfs/ls/**.

  - Définissez les URI AD FS sur **https://mail.contoso.com/owa/** et **https://mail.contoso.com/ecp/**.

  - Recherchez le jeton AD FS empreinte numérique du certificat de signature à l’aide de la Windows PowerShell sur le serveur AD FS et saisie de `Get-ADFSCertificate -CertificateType "Token-signing"`. Ensuite, affectez l’empreinte de certificat de signature de jetons que vous avez trouvé. Si le certificat de signature de jetons AD FS a expiré, l’empreinte à partir du nouveau certificat de signature de jetons AD FS doit être mis à jour à l’aide de l’applet de commande [Set-OrganizationConfig](https://technet.microsoft.com/fr-fr/library/aa997443\(v=exchg.150\)) .

Dans Exchange Management Shell, exécutez les commandes suivantes.

    $uris = @(" https://mail.contoso.com/owa/","https://mail.contoso.com/ecp/")
    Set-OrganizationConfig -AdfsIssuer "https://adfs.contoso.com/adfs/ls/" -AdfsAudienceUris $uris -AdfsSignCertificateThumbprint "88970C64278A15D642934DC2961D9CCA5E28DA6B"

> [!NOTE]
> Le paramètre <em>-AdfsEncryptCertificateThumbprint</em> n’est pas pris en charge pour ces scénarios.


Pour plus de détails et d’informations sur la syntaxe, consultez les rubriques [Set-OrganizationConfig](https://technet.microsoft.com/fr-fr/library/aa997443\(v=exchg.150\)) et [Get-ADFSCertificate](https://go.microsoft.com/fwlink/?linkid=392706).

## Étape 8 – Activer l’authentification AD FS sur les répertoires virtuels OWA et ECP

Pour les répertoires virtuels OWA et ECP, activez l’authentification AD FS comme seule méthode d’authentification et désactivez toutes les autres formes d’authentification.

> [!CAUTION]
> Vous devez configurer le répertoire virtuel ECP avant le répertoire virtuel OWA.


Configurer le répertoire virtuel ECP à l’aide d’Exchange Management Shell. Dans la fenêtre de Shell, exécutez la commande suivante.

    Get-EcpVirtualDirectory | Set-EcpVirtualDirectory -AdfsAuthentication $true -BasicAuthentication $false -DigestAuthentication $false -FormsAuthentication $false -WindowsAuthentication $false

Configurer le répertoire virtuel OWA à l’aide d’Exchange Management Shell. Dans la fenêtre de Shell, exécutez la commande suivante.

    Get-OwaVirtualDirectory | Set-OwaVirtualDirectory -AdfsAuthentication $true -BasicAuthentication $false -DigestAuthentication $false -FormsAuthentication $false -WindowsAuthentication $false -OAuthAuthentication $false

> [!NOTE]
> Les commandes Exchange Management Shell précédentes configurer les répertoires virtuels OWA et ECP sur chaque serveur d’accès Client de votre organisation. Si vous ne souhaitez pas appliquer ces paramètres à tous les serveurs d’accès Client, utilisez le paramètre <em>-Identity</em> et spécifiez le serveur d’accès Client. Il est probable que vous souhaitez appliquer ces paramètres uniquement vers les serveurs d’accès Client de votre organisation qui sont Internet en vis-à-vis.


Pour plus de détails et d’informations sur la syntaxe, reportez-vous aux rubriques [Get-OwaVirtualDirectory](https://technet.microsoft.com/fr-fr/library/aa998588\(v=exchg.150\)) et [Set-OwaVirtualDirectory](https://technet.microsoft.com/fr-fr/library/bb123515\(v=exchg.150\)) ou [Get-EcpVirtualDirectory](https://technet.microsoft.com/fr-fr/library/dd351058\(v=exchg.150\)) et [Set-EcpVirtualDirectory](https://technet.microsoft.com/fr-fr/library/dd297991\(v=exchg.150\)).

## Étape 9 – Redémarrer ou recycler Internet Information Services (IIS)

Une fois toutes les étapes requises terminées, y compris les modifications sur les répertoires virtuels Exchange, vous devez redémarrer IIS. Pour ce faire, utilisez l’une des méthodes suivantes :

  - À l’aide de Windows PowerShell :
    
        Restart-Service W3SVC,WAS -noforce

  - À l’aide d’une ligne de commande : Cliquez sur **Démarrer**, sur **Exécuter**, entrez `IISReset /noforce`, puis cliquez sur **OK**.

  - À l’aide du Gestionnaire des services IIS : Dans **Gestionnaire de serveur**\>**IIS**, cliquez sur **Outils**, puis sur **Gestionnaire des services IIS**. Dans la fenêtre **Gestionnaire des services IIS**, dans le volet Actions sous **Gérer le serveur**, cliquez sur **Redémarrer**.

## Étape 10 - Tester les revendications AD FS pour Outlook Web App et le CAE

Pour tester les revendications AD FS pour Outlook Web App :

  - Dans votre navigateur web, connectez-vous à Outlook Web App, par exemple, **https://mail.contoso.com/owa**

  - Dans la fenêtre du navigateur, si vous obtenez une erreur de certificat, continuez simplement sur le site web Outlook Web App. Vous devez être redirigé vers la page de connexion AD FS ou l’invite AD FS des informations d’identification.

  - Tapez votre nom d’utilisateur (domaine\\utilisateur) et votre mot de passe, puis cliquez sur **Connexion**.

Outlook Web App est chargé dans la fenêtre.

Pour tester les revendications AD FS pour le CAE :

1.  Dans votre navigateur web, accédez à **https://mail.contoso.com/ecp**.

2.  Dans la fenêtre du navigateur, si vous obtenez une erreur de certificat, continuez simplement sur le site web d’ECP. Vous devez être redirigé vers la page de connexion AD FS ou l’invite AD FS des informations d’identification.

3.  Tapez votre nom d’utilisateur (domaine\\utilisateur) et votre mot de passe, puis cliquez sur **Connexion**.

4.  Le CAE doit être chargé dans la fenêtre.

## Informations supplémentaires utiles

**Authentification multifacteur**

Pour les déploiements Exchange 2013 SP1 sur site, le déploiement et la configuration des services Active Directory Federation Services (AD FS) 2.0 à l’aide des revendications signifient qu’Outlook Web App et le CAE dans Exchange 2013 SP1 peuvent prendre en charge les méthodes d’authentification multifacteur, telles que l’authentification basée sur des certificats, les jetons d’authentification ou de sécurité et l’authentification par empreinte. L’authentification à deux facteurs est souvent confondue avec d’autres formes d’authentification. L’authentification multifacteur requiert l’utilisation de deux des trois facteurs d’authentification. Ces facteurs sont les suivants :

  - Un élément que seul l’utilisateur connait (par exemple, le mot de passe, le code PIN ou le modèle)

  - Un élément que seul l’utilisateur possède (par exemple, une carte de crédit, un jeton de sécurité, une carte à puce ou un téléphone mobile)

  - Un élément propre à l’utilisateur (par exemple, une caractéristique biométrique, comme une empreinte digitale)

Pour plus de détails sur l’authentification multifacteur dans Windows Server 2012 R2, consultez la rubrique [Vue d’ensemble : gérer les risques avec une authentification multifacteur supplémentaire pour les applications sensibles](https://go.microsoft.com/fwlink/?linkid=392707) et [Guide pas à pas : gérer les risques avec une authentification multifacteur supplémentaire pour les applications sensibles](https://go.microsoft.com/fwlink/?linkid=392708).

Dans le service de rôle Windows Server 2012 R2 AD FS, le service de fédération fonctionne comme un service de jetons de sécurité, fournit les jetons de sécurité qui sont utilisés avec les revendications et vous permet de prendre en charge l’authentification multifacteur. Le service de fédération émet des jetons à partir des informations d’identification présentées. Une fois que le magasin de comptes a vérifié les informations d’identification de l’utilisateur, les revendications concernant l’utilisateur sont générées selon les règles de la stratégie d’approbation, puis ajoutées à un jeton de sécurité qui est remis au client. Pour plus d’informations sur les revendications, consultez la rubrique [Présentation des revendications](https://go.microsoft.com/fwlink/?linkid=392709).

**Coexistence avec d’autres versions d’Exchange**

Il est possible d’utiliser l’authentification AD FS pour Outlook Web App et le CAE lorsque plusieurs versions d’Exchange sont déployées dans votre organisation. Ce scénario est uniquement pris en charge pour les déploiements d’Exchange 2010 et Exchange 2013, et uniquement si tous les clients se connectent via les serveurs Exchange 2013 **et** que ces serveurs Exchange 2013 ont été configurés pour l’authentification AD FS.

Les utilisateurs disposant d’une boîte aux lettres sur un serveur Exchange 2010 peuvent accéder à leurs boîtes aux lettres via un serveur Exchange 2013 configuré pour l’authentification AD FS. La connexion cliente initiale au serveur Exchange 2013 utilisera l’authentification AD FS. En revanche, la connexion avec proxy au serveur Exchange 2010 utilisera Kerberos. Il n’existe aucun moyen pris en charge de configurer Exchange Server 2010 pour l’authentification AD FS directe.

