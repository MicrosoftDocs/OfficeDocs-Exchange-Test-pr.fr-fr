---
title: 'Configuration de l’authentification OAuth avec SharePoint 2013 et Lync 2013: Exchange 2013 Help'
TOCTitle: Configuration de l’authentification OAuth avec SharePoint 2013 et Lync 2013
ms:assetid: ca3c78a3-80cc-4df2-859f-0106bbd57a07
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ649094(v=EXCHG.150)
ms:contentKeyID: 50479167
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configuration de l’authentification OAuth avec SharePoint 2013 et Lync 2013

 

_**Sapplique à :**Exchange Server 2013_

_**Dernière rubrique modifiée :**2014-03-03_

Exchange Server 2013 autorise les autres applications à utiliser OAuth pour s’authentifier à Exchange. Les applications doivent être configurées comme des applications partenaires dans Exchange 2013.

Dans Exchange 2013, la configuration OAuth avec des applications partenaires comme SharePoint 2013 et Lync Server 2013 est uniquement prise en charge par l’utilisation du script `Configure-EnterpriseApplication.ps1`. L’automatisation de la tâche facilite, pour le script, la configuration de l’authentification auprès des applications partenaires et diminue les erreurs de configuration. Le script exécute les tâches suivantes :

1.  Configure une application partenaire Entreprise qui auto-émet des jetons OAuth pour s’authentifier correctement auprès d’Exchange.

2.  Attribue des rôles RBAC (Role Based Access Control) à l’application partenaire pour l’autoriser à appeler des API de Services Web Exchange spécifiques.

## Ce qu’il faut savoir avant de commencer ?

  - Durée d’exécution estimée : 5 minutes.

  - L’application partenaire doit publier un document de métadonnées authentifié pour que Exchange 2013 puisse établir une approbation directe pour cette application et accepte les demandes d’authentification.

  - Les exemples de cette rubrique utilisent l’emplacement par défaut suivant dans le répertoire `\Scripts` : `C:\Program Files\Microsoft\Exchange Server\V15\Scripts`.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Applications partenaires - configurer » dans la rubrique [Autorisations de partage et de collaboration](sharing-and-collaboration-permissions-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

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


## Configurer l’authentification OAuth avec une application partenaire

Cette procédure utilise le script `Configure-EntepririseApplication.ps1` pour configurer l’authentification OAuth auprès d’applications partenaires. L’accès aux ressources dépend des autorisations attribuées à l’application partenaire et/ou à l’utilisateur RBAC dont il emprunte l’identité en utilisant RBAC.

Après la configuration de l’authentification OAuth à partir d’Exchange, l’application partenaire peut utiliser des ressources Exchange 2013. Si Exchange 2013 a également besoin d’accéder aux ressources proposées par l’application partenaire, vous devez aussi configurer l’authentification OAuth dans l’application partenaire.

Cet exemple configure l’authentification OAuth pour SharePoint 2013.

    Cd C:\Program Files\Microsoft\Exchange Server\V15\Scripts
    Configure-EnterprisePartnerApplication.ps1 -AuthMetaDataUrl https://sharepoint.contoso.com/_layouts/15/metadata/json/1 -ApplicationType SharePoint

Cet exemple configure l’authentification OAuth pour Lync Server 2013.

    Cd C:\Program Files\Microsoft\Exchange Server\V15\Scripts
    Configure-EnterprisePartnerApplication.ps1 -AuthMetaDataUrl https://lync.contoso.com/metadata/json/1 -ApplicationType Lync

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez bien configuré une application partenaire entreprise pour l’authentification auprès de Exchange 2013, exécutez la cmdlet [Get-PartnerApplication](https://technet.microsoft.com/fr-fr/library/jj218721\(v=exchg.150\)) dans l’environnement de ligne de commande Exchange Management Shell. Vous pouvez aussi exécuter la cmdlet [Test-OAuthConnectivity](https://technet.microsoft.com/fr-fr/library/jj218623\(v=exchg.150\)) pour tester la connectivité OAuth avec une application partenaire pour un utilisateur.

## Plus d’informations

  - Dans les déploiements hybrides, vous pouvez utiliser l’authentification OAuth entre votre organisation Exchange 2013 sur site et l’organisation Exchange Online. Pour plus d’informations, voir [Utilisation de l’authentification OAuth pour prendre en charge la découverte électronique dans un déploiement hybride Exchange](using-oauth-authentication-to-support-ediscovery-in-an-exchange-hybrid-deployment-exchange-2013-help.md).

  - Dans les déploiements sur site, vous pouvez configurer l’authentification de serveur à serveur entre Exchange 2013 et SharePoint 2013 afin que les administrateurs et les déontologues puissent utiliser le centre eDiscovery dans SharePoint 2013 pour la recherche de boîtes aux lettres Exchange 2013. Pour plus d’informations, voir [Configurer Exchange pour le Centre de découverte électronique SharePoint](configure-exchange-for-sharepoint-ediscovery-center-exchange-2013-help.md).

