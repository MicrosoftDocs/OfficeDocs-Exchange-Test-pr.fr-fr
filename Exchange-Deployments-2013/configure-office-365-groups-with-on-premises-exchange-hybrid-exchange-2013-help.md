---
title: 'Configurer des groupes Office 365 avec un environnement Exchange hybride local: Exchange 2013 Help'
TOCTitle: Configurer des groupes Office 365 avec un environnement Exchange hybride local
ms:assetid: 184dfcfe-4b8e-450a-adc6-e647213b9501
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Mt668829(v=EXCHG.150)
ms:contentKeyID: 72515524
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configurer des groupes Office 365 avec un environnement Exchange hybride local

 

_<strong>Dernière rubrique modifiée :</strong>2016-12-06_

Découvrez comment permettre aux utilisateurs d’Exchange en local d’utiliser des Groupes Office 365 dans un déploiement hybride.

Groupes est un service d’Office 365 qui permet aux équipes de communiquer, de planifier des réunions et de collaborer sur des documents plus facilement. Toutes les informations partagées avec un groupe, à partir des messages électroniques envoyés au groupe, vers les fichiers stockés dans les bibliothèques OneDrive Entreprise ou SharePoint du groupe, sont disponibles pour tous les membres d’un groupe. Si vous avez configuré un déploiement hybride entre votre organisation Exchange locale et Office 365, vous pouvez mettre des groupes créés dans Office 365 à la disposition de vos utilisateurs en local en effectuant les étapes décrites dans cette rubrique.

>  [!IMPORTANT]  
> L’utilisation de Groupes Office 365 avec des utilisateurs locaux dans un déploiement Exchange hybride est une nouvelle fonctionnalité. Comme il s’agit d’une nouveauté, vous pouvez rencontrer des problèmes lors de la configuration. N’oubliez pas de consulter la section Problèmes connus à la fin de cette rubrique pour corriger les problèmes que vous pouvez rencontrer.</td>



## Conditions préalables

Avant de commencer, vérifiez que vous avez effectué les opérations suivantes :

  - Achat de licences Azure Active Directory Premium pour votre client. Cela est nécessaire pour activer la fonctionnalité d’écriture différée de Groupes dans Azure Active Directory Connect.

  - Configuration d’un déploiement hybride entre votre organisation Exchange locale et Office 365 et vérification du bon fonctionnement. Pour plus d’informations sur le déploiement hybride Exchange, consultez les rubriques suivantes :
    
      - [Déploiements hybrides Exchange Server](exchange-server-hybrid-deployments-exchange-2013-help.md)
    
      - [Configuration requise pour un déploiement hybride](hybrid-deployment-prerequisites-exchange-2013-help.md)

  - Installation d’une version prise en charge de l’intégration d’Exchange en local avec Groupes Office 365 est disponible dans CU1 et les versions plus récentes d’Exchange 2016, et CU11 et les versions plus récentes d’Exchange 2013. Toutefois, Exchange hybride nécessite que la dernière mise à jour cumulative (CU) Exchange 2016 ou Exchange 2013 soit installée sur les serveurs Exchange locaux. Si vous ne pouvez pas installer la dernière CU, vous pouvez utiliser la mise à jour publiée immédiatement avant la CU actuelle.

  - Configuration de l’authentification unique à l’aide d’Azure Active Directory Connect (Azure AD Connect). Cela est nécessaire pour permettre aux utilisateurs de cliquer sur le lien **Afficher des fichiers de groupe** ou les liens de pièces jointes dans le cloud dans les messages électroniques du groupe.
    
    Lorsque vous configurez Azure AD Connect pour l’authentification unique dans un déploiement Exchange hybride, nous vous recommandons d’utiliser la synchronisation de mot de passe. Les services de fédération Active Directory (AD FS) ne doivent être utilisés que si vous appartenez à une grande entreprise ; si vous disposez d’un déploiement Active Directory complexe en local (par exemple, plusieurs forêts Active Directory) ; si un autre produit Microsoft nécessite AD FS pour fonctionner avec Office 365 ; ou si, en raison des stratégies de conformité, vous n’êtes pas en mesure de synchroniser les mots de passe en dehors de votre réseau local. Pour plus d’informations sur l’authentification unique, consultez la rubrique [Intégration de vos identités locales avec Azure Active Directory](http://go.microsoft.com/fwlink/p/?linkid=723513).

## Activer l’écriture différée de groupe dans Azure AD Connect

1.  Dans l’Assistant Azure AD Connect, sélectionnez **Personnaliser les options de synchronisation**, puis cliquez sur **Suivant**.

2.  Sur la page **Connexion à Azure AD**, entrez vos identifiants Office 365 et locaux. Cliquez sur **Suivant**.

3.  Sur la page **Fonctionnalités facultatives**, vérifiez que les options que vous avez configurées précédemment sont toujours sélectionnées. Les options les plus fréquemment sélectionnées sont **Exchange hybride** et **Synchronisation de hachage de mot de passe**.

4.  Sélectionnez **Écriture différée de groupe** puis cliquez sur **Suivant**.

5.  Sur la page **Écriture différée**, sélectionnez une unité d’organisation dans Active Directory pour stocker des objets qui sont synchronisés depuis Office 365 sur votre organisation en local, puis cliquez sur **Suivant**.

6.  Sur la page **Prêt à configurer**, cliquez sur **Configurer**.

7.  Une fois l’Assistant terminé, cliquez sur **Quitter** sur la page **Configuration terminée**.

8.  Ouvrez Utilisateurs et ordinateurs Active Directory sur un contrôleur de domaine Active Directory et recherchez le compte d’utilisateur qui commence par **AAD\_**. Notez le nom de ce compte.

9.  Ouvrez l’environnement de ligne de commande Exchange Management Shell sur un serveur Exchange local et exécutez les commandes suivantes.
    
        $AzureADConnectSWritebackAccount = <AAD_ account name from step 8>
        
        $GroupsOU = <writeback Active Directory OU selected in step 5>
        
        Import-Module "C:\Program Files\Microsoft Azure Active Directory Connect\AdPrep\AdSyncPrep.psm1"
        
        Initialize-ADSyncGroupWriteBack -ADConnectorAccount $AzureADConnectSWritebackAccount -GroupWriteBackContainerDN $GroupsOU

## Configurer un domaine de groupe

Le domaine SMTP principal d’un Groupe Office 365 est appelé un *domaine de groupe*. Par défaut, le domaine accepté par défaut dans votre organisation est choisi comme domaine de groupe. Si vous souhaitez ajouter un domaine de groupe dédié, vous pouvez ajouter un domaine à l’aide de la procédure suivante. Pour plus d’informations sur la prise en charge de plusieurs domaines pour les Groupes Office 365, consultez l’article [Prise en charge de plusieurs domaines pour les Groupes Office 365](https://support.office.com/fr-fr/article/multi-domain-support-for-office-365-groups-admin-help-7cf5655d-e523-4bc3-a93b-3ccebf44a01a).

1.  Ajoutez votre nouveau domaine à votre organisation Office 365. Si vous avez besoin d’aide pour ajouter un domaine à Office 365, consultez l’article [Ajouter des utilisateurs et un domaine à Office 365](https://support.office.com/fr-fr/article/add-users-and-domain-to-office-365-6383f56d-3d09-4dcb-9b41-b5f5a5efd611?ui=en-us%26rs=en-us%26ad=us).

2.  Ajoutez le domaine de groupe sous la forme d’un domaine accepté dans votre organisation Exchange en local à l’aide de la commande suivante. Cela est nécessaire pour que le connecteur d’envoi hybride puisse être utilisé pour la remise de courrier sortant au domaine de groupe dans Office 365.
    
        New-AcceptedDomain -Name groups.contoso.com -DomainName groups.contoso.com -DomainType InternalRelay

3.  Créez les enregistrements DNS publics suivants auprès de votre fournisseur DNS.
    
    
    <table>
    <colgroup>
    <col style="width: 33%" />
    <col style="width: 33%" />
    <col style="width: 33%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th><p>Nom d’enregistrement DNS</p></th>
    <th><p>Type d’enregistrement DNS</p></th>
    <th><p>Valeur d’enregistrement DNS</p></th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p>groups.contoso.com</p></td>
    <td><p>MX</p></td>
    <td><p>groups-contoso-com.mail.protection.outlook.com</p>
    
    > [!NOTE]  
    > Le format de cette valeur d’enregistrement DNS est <em>&lt;domain key&gt;</em>.mail.protection.outlook.com. Pour connaître votre clé de domaine, consultez l’article <a href="https://support.office.microsoft.com/fr-fr/article/gather-the-information-you-need-to-create-office-365-dns-records-77f90d4a-dc7f-4f09-8972-c1b03ea85a67?ui=en-us%26rs=en-us%26ad=us">Recueillez les informations nécessaires pour créer des enregistrements DNS Office 365</a>.
    

</td>
    </tr>
    <tr class="even">
    <td><p>autodiscover.groups.contoso.com</p></td>
    <td><p>CNAME</p></td>
    <td><p>autodiscover.outlook.com</p></td>
    </tr>
    </tbody>
    </table>
    
   > [!CAUTION]  
   > Si l’enregistrement DNS MX pour le domaine de groupe est défini sur le serveur Exchange local, le flux de messagerie ne fonctionne pas correctement entre les utilisateurs de l’organisation Exchange en local et le Groupe Office 365.


4.  Ajoutez le domaine de groupe au connecteur d’envoi hybride, créé par l’Assistant Configuration hybride dans votre organisation Exchange en local, à l’aide de la commande suivante.
    
        Set-SendConnector -Identity "Outbound to Office 365" -AddressSpaces "contoso.mail.onmicrosoft.com","groups.contoso.com"
    
    > [!NOTE]  
    > Si le connecteur d’envoi n’est pas mis à jour, ou si le domaine de groupe n’est pas ajouté sous la forme d’un domaine accepté dans l’organisation Exchange en local, le courrier électronique envoyé à partir d’une boîte aux lettres en local ne sera pas remis au groupe, sauf si le groupe est configuré pour recevoir du courrier provenant d’expéditeurs externes.
    

## Comment savoir si cela a fonctionné ?

Pour vous assurer que les groupes fonctionnent avec votre déploiement Exchange hybride, vous devez les tester à l’aide d’une boîte aux lettres locale et à l’aide d’une boîte aux lettres déplacée à partir de votre organisation en local vers Office 365. Suivez les étapes présentées dans les sections suivantes pour réaliser chaque test.

## Test à l’aide d’une boîte aux lettres locale

1.  Ajoutez une boîte aux lettres locale à un Groupe Office 365.

2.  Ajoutez une boîte aux lettres Office 365 au même Groupe Office 365.

3.  Connectez-vous à la boîte aux lettres Office 365 à l’aide d’Outlook sur le web.

4.  Publiez un message dans le groupe à l’aide de la boîte aux lettres Office 365.

5.  Ouvrez la boîte aux lettres locale à l’aide d’Outlook 2016 ou d’Outlook sur le web.

6.  Vérifiez que la boîte aux lettres a reçu un message électronique contenant le billet envoyé au Groupe Office 365.

7.  Dans la même boîte aux lettres, rédigez une réponse au message et envoyez-la au groupe.

8.  Vérifiez que le message peut être affiché par tous les membres du groupe.

## Test à l’aide d’une boîte aux lettres déplacée vers Office 365

1.  Déplacez une boîte aux lettres de votre organisation d’Exchange locale vers Office 365.

2.  Ajoutez la boîte aux lettres à un Groupe Office 365.

3.  Dans une nouvelle session de navigateur, connectez-vous à la boîte aux lettres qui a été déplacée vers Office 365.

4.  Dans Outlook sur le web, vérifiez que le groupe est répertorié dans la barre de navigation gauche.

5.  Publiez un message destiné au groupe.

6.  Vérifiez que le message peut être affiché par tous les membres du groupe.

## Problèmes connus

  - **Les Groupes n’apparaissent pas pour les boîtes aux lettres déplacées vers Office 365** Lorsqu’un utilisateur est déplacé de votre organisation Exchange locale vers Office 365, les groupes ne s’affichent pas dans le volet de navigation gauche dans Outlook ou Outlook sur le web. Pour résoudre le problème, supprimez la boîte aux lettres à partir de n’importe quel groupe dont elle est membre et rajoutez-la à chaque groupe.

  - **Les nouveaux groupes n’apparaissent pas dans la liste d’adresses globale (LAG) Exchange en local** Lorsqu’un groupe est créé dans Office 365, il n’apparaîtra pas automatiquement dans les LAG locales. Pour résoudre ce problème, ouvrez l’environnement de ligne de commande Exchange Management Shell sur un serveur Exchange et exécutez la commande suivante.
    
        Update-Recipient "<group name>"

  - **Les groupes ne reçoivent pas les messages des utilisateurs locaux** Un utilisateur local ne peut pas envoyer de messages électroniques à un Groupe d’Office 365 lorsque les conditions suivantes sont vraies :
    
      - Le domaine de groupe est configuré comme un domaine faisant autorité de votre organisation Exchange locale.
    
      - Le groupe a été créé récemment et ses informations n’ont pas encore été réécrites dans Active Directory en local.
    
    Ce problème se résoudra de lui-même lors de la prochaine synchronisation d’Azure AD Connect entre Office 365 et votre organisation locale. La synchronisation Azure AD Connect se produit toutes les trente minutes.

  - **Les utilisateurs locaux ne peuvent pas utiliser les liens inclus dans les pieds de page de message de groupe** Les utilisateurs locaux ne peuvent pas utiliser les liens **Afficher les conversations de groupe** ou **Annuler l’abonnement** qui sont inclus dans le pied de page de chaque message de groupe envoyé. Pour annuler un abonnement d’un groupe, les utilisateurs locaux doivent contacter un administrateur de groupe.

  - **Le courrier envoyé à l’adresse SMTP secondaire d’un groupe ne peut pas être remis** Lorsque plusieurs adresses de messagerie sont ajoutées à un groupe, seule l’adresse SMTP principale est réécrite dans Active Directory en local. Si un utilisateur local essaie d’envoyer un message à l’adresse SMTP secondaire d’un groupe, le message ne pourra pas être remis. Pour éviter ce problème, configurez une seule adresse SMTP sur chaque groupe.

  - **Les utilisateurs locaux ne peuvent pas devenir un administrateur d’un groupe en local** Les utilisateurs locaux ne peuvent pas accéder directement à l’espace de groupe. Pour cette raison, ils ne peuvent pas être ajoutés en tant qu’administrateur d’un groupe.

  - **La remise du courrier externe à un groupe peut échouer si vous avez activé le flux de messagerie centralisé** Si le flux de messagerie centralisé est activé, les messages envoyés par un utilisateur externe à un groupe ne sont pas remis, même si le groupe accepte les messages électroniques provenant d’expéditeurs externes.

  - **Les utilisateurs locaux ne peuvent pas envoyer de courrier en tant que groupe** Un utilisateur local qui essaie d’envoyer un message en tant que Groupe Office 365 reçoit une erreur d’autorisation refusée même s’il a obtenu des autorisations « Envoyer en tant que » sur le groupe. Les autorisations « Envoyer en tant que » sur un groupe fonctionnent uniquement pour les utilisateurs de boîte aux lettres Exchange Online.

  - **La sélection d’un groupe dans le volet de navigation gauche d’Outlook n’entraîne pas l’ouverture de la boîte aux lettres du groupe** Outlook utilise l’URL de découverte automatique pour ouvrir une boîte aux lettres de groupe. Si l’adresse de messagerie principale d’un groupe se trouve dans un domaine qui ne pointe pas vers une URL de découverte automatique d’Office 365 (autodiscover.outlook.com), Outlook ne peut pas ouvrir la boîte aux lettres du groupe. Pour résoudre le problème, les groupes peuvent être configurés avec une adresse principale dans un domaine qui pointe vers l’URL de découverte automatique d’Office 365. Vous pouvez configurer une stratégie d’adresse de messagerie pour ajouter une adresse de messagerie principale sur chaque boîte aux lettres de groupe qui pointe vers l’URL de découverte automatique d’Office 365. Consultez l’article [Prise en charge de plusieurs domaines pour les Groupes Office 365](https://support.office.com/fr-fr/article/multi-domain-support-for-office-365-groups-admin-help-7cf5655d-e523-4bc3-a93b-3ccebf44a01a) pour plus d’informations.

