---
title: 'Gérer une approbation de fédération: Exchange 2013 Help'
TOCTitle: Gérer une approbation de fédération
ms:assetid: 0439839f-2052-4bc9-9d30-aa6e7d51b733
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ673036(v=EXCHG.150)
ms:contentKeyID: 50477440
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Gérer une approbation de fédération

 

_**Sapplique à :**Exchange Server 2013_

_**Dernière rubrique modifiée :**2015-01-01_

Une approbation de fédération établit une relation d’approbation entre une organisation Microsoft Exchange 2013 et le système d’authentification Azure Active Directory et prend en charge le partage fédéré avec d’autres organisations Exchange fédérées. Normalement, vous ne devriez pas avoir à gérer ni à modifier l’approbation de fédération qui a été créée. Toutefois, dans certaines circonstances, il sera peut-être nécessaire d’ajouter ou de supprimer des domaines fédérés ou de redéfinir le domaine utilisé afin de configurer l’identificateur de l’organisation (OrgID) pour l’approbation de fédération.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>La modification d’une approbation de fédération, surtout le domaine partagé principal utilisé pour définir l’OrgID, peut perturber le partage fédéré entre les organisations Exchange fédérées ou pour les déploiements hybrides avec des organisations Office 365.</td>
</tr>
</tbody>
</table>


Pour connaître les autres tâches de gestion relatives à la fédération, consultez la rubrique [Procédures de fédération](federation-procedures-exchange-2013-help.md).

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159813.important(EXCHG.150).gif" title="Important" alt="Important" />Important :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Cette fonctionnalité d’Exchange Server 2013 n’est pas entièrement compatible avec les systèmes Office 365 exécutés par 21Vianet en Chine et certaines limitations de fonctionnalités peuvent s’appliquer. Pour plus d’informations, voir <a href="https://go.microsoft.com/fwlink/?linkid=313640">En savoir plus sur Office 365 exécuté par 21Vianet</a>.</td>
</tr>
</tbody>
</table>


## Ce qu’il faut savoir avant de commencer ?

  - Durée d'exécution estimée : 30 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez *Federation and certificates* Entrée d'autorisations dans la rubrique [Autorisations d’infrastructure Exchange et Shell](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md).

  - Vous devrez ajouter un enregistrement TXT à votre DNS public pour chaque nouveau domaine fédéré ajouté à l’approbation de fédération. Passez en revue les exigences pour l’ajout d’un enregistrement TXT avec l’organisation qui héberge vos enregistrements DNS publics.

  - Dans cette rubrique, nous avons configuré une approbation de fédération en utilisant les paramètres suivants :
    
      - **Contoso.com** est le domaine partagé principal pour l’approbation de fédération. (Ce domaine ne sera pas modifié.)
    
      - Les domaines fédérés **service.contoso.com** et **sales.contoso.com** sont inclus dans l’approbation de fédération existante.
    
      - **Marketing.contoso.com** est un domaine accepté dans l’organisation Exchange.

  - Cette rubrique traite également d’autres tâches de gestion relatives à la fédération, telles que l’affichage et la gestion de certificats utilisés pour l’approbation de fédération et l’affichage d’informations sur les paramètres d’approbation de fédération dans le Shell.

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

## Que souhaitez-vous faire ?

## Utiliser le Centre d’administration Exchange pour gérer une approbation de fédération

1.  Sur un serveur Exchange 2013 de votre organisation sur site, accédez à **Organisation** \> **Partage**.

2.  Dans la section **Approbation de fédération**, cliquez sur **Modifier**.

3.  Dans **Domaines activés pour le partage**, ignorez l’**étape 1**, car le domaine partagé principal ne change pas.

4.  À l’**étape 2**, sélectionnez le domaine **service.contoso.com**, puis cliquez sur **Supprimer**![Icône Suppression](images/Dd362328.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "Icône Suppression") pour supprimer le domaine de l’approbation fédérée.

5.  À l’**étape 2**, cliquez sur **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter").

6.  Dans **Sélectionner les domaines acceptés**, sélectionnez **marketing.contoso.com** dans la liste des domaines acceptés, puis cliquez sur **OK** pour ajouter le domaine à l’approbation fédérée.
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ159813.important(EXCHG.150).gif" title="Important" alt="Important" />Important :</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Une chaîne de vérification de domaine fédéré sera créée pour le domaine <strong>marketing.contoso.com</strong>. Vous devez créer un enregistrement TXT distinct sur votre DNS public pour ce domaine.</td>
    </tr>
    </tbody>
    </table>


7.  Utilisez la chaîne de vérification de domaine créée pour le domaine **marketing.contoso.com** pour créer un enregistrement TXT sur votre serveur DNS public. En fonction de la planification des mises à jour de votre hôte DNS public, la réplication des modifications DNS peut prendre au moins 15 minutes.

8.  Une fois l’enregistrement TXT créé et répliqué, cliquez sur **Mettre à jour**.

## Utiliser l’environnement Shell pour gérer une approbation de fédération

1.  Cet exemple permet de supprimer le domaine service.contoso.com de l’approbation de fédération.
    
        Remove-FederatedDomain -DomainName service.contoso.com

2.  Cet exemple permet d’ajouter le domaine marketing.contoso.com à l’approbation de fédération.
    
        Add-FederatedDomain -DomainName marketing.contoso.com

Pour des informations détaillées sur la syntaxe et les paramètres, consultez les rubriques [Remove-FederatedDomain](https://technet.microsoft.com/fr-fr/library/dd298128\(v=exchg.150\)) et [Add-FederatedDomain](https://technet.microsoft.com/fr-fr/library/dd351208\(v=exchg.150\)).

Exécutez les commandes d’environnement suivantes pour gérer d’autres aspects relatifs à une approbation de fédération :

1.  **Afficher l’OrgID fédéré et les domaines fédérés**
    
    Cet exemple affiche l’OrgID fédéré de l’organisation Exchange et les informations connexes, comme les domaines fédérés et l’état.
    
        Get-FederatedOrganizationIdentifier

2.  **Afficher les certificats de l’approbation de fédération**
    
    Cet exemple affiche les certificats précédent, actuel et suivant utilisés par l’approbation de fédération « Authentification Azure AD ».
    
        Get-FederationTrust "Azure AD authentication" | Select Org*certificate

3.  **Vérifier l’état des certificats de fédération**
    
    Cet exemple affiche l’état des certificats de fédération sur tous les serveurs de boîtes aux lettres et d’accès au client dans l’organisation.
    
        Test-FederationTrustCertificate

4.  **Configurer l'approbation de fédération pour utiliser un certificat comme certificat suivant**
    
    Cet exemple configure l’approbation de fédération « Authentification Azure AD » de sorte qu’elle utilise le certificat doté d’une empreinte comme certificat suivant. Une fois le certificat déployé sur l’ensemble des serveurs Exchange de l’organisation, vous pouvez utiliser le commutateur *PublishCertificate* pour configurer l’approbation de fédération afin qu’elle utilise ce certificat comme certificat actuel.
    
        Set-FederationTrust "Azure AD authentication" -Thumbprint AC00F35CBA8359953F4126E0984B5CCAFA2F4F17

5.  **Configurer l'approbation de fédération pour utiliser le certificat suivant comme certificat actuel**
    
    Cet exemple configure l’approbation de fédération « Authentification Azure AD » de sorte qu’elle utilise le certificat suivant comme certificat actuel et la publie dans le système d’authentification Azure AD.
    
        Set-FederationTrust "Azure AD authentication" -PublishFederationCertificate
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ673034.Caution(EXCHG.150).gif" title="Attention" alt="Attention" />Attention :</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Avant de configurer l’approbation de fédération afin qu’elle utilise le certificat suivant comme certificat de fédération actuel, assurez-vous que le certificat est déployé sur tous les serveurs Exchange de votre organisation. Utilisez la cmdlet <a href="https://technet.microsoft.com/fr-fr/library/dd335228(v=exchg.150)">Test-FederationTrustCertificate</a> pour vérifier l’état de déploiement du certificat.</td>
    </tr>
    </tbody>
    </table>


6.  **Actualisez le certificat et les métadonnées de fédération à partir du système d'authentification Azure AD**
    
    Cet exemple actualise le certificat et les métadonnées de fédération du système d’authentification Azure AD pour l’approbation de fédération « Authentification Azure AD ».
    
        Set-FederationTrust "Azure AD authentication" -RefreshMetadata

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, consultez les rubriques suivantes :

  - [Get-FederatedOrganizationIdentifier](https://technet.microsoft.com/fr-fr/library/dd298149\(v=exchg.150\))

  - [Get-FederationTrust](https://technet.microsoft.com/fr-fr/library/dd351262\(v=exchg.150\))

  - [Test-FederationTrustCertificate](https://technet.microsoft.com/fr-fr/library/dd335228\(v=exchg.150\))

  - [Set-FederationTrust](https://technet.microsoft.com/fr-fr/library/dd298034\(v=exchg.150\))

## Comment savoir si cela a fonctionné ?

Si vous avez réussi à exécuter toutes les étapes de l’Assistant **Domaines activés pour le partage**, l’approbation de fédération devrait être correctement configurée.

Pour le vérifier, procédez comme suit :

1.  Exécutez la commande de l’environnement de ligne de commande suivante pour vérifier les informations d’approbation de la fédération.
    
        Get-FederationTrust | format-list

2.  Exécutez la commande de l’environnement de ligne de commande suivante pour vérifier si les informations de la fédération peuvent être récupérées à partir de votre organisation. Par exemple, vérifiez que les domaines sales.contoso.com et marketing.contoso.com sont renvoyés dans le paramètre *DomainNames*.
    
        Get-FederationInformation -DomainName <your primary sharing domain>

<table>
<thead>
<tr class="header">
<th><img src="images/Bb125224.tip(EXCHG.150).gif" title="Conseil" alt="Conseil" />Conseil :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.</td>
</tr>
</tbody>
</table>

