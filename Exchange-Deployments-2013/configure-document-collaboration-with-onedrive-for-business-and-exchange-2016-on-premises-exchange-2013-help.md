---
title: 'Configuration des pièces jointes actuelles avec OneDrive Entreprise et Exchange 2016 en local: Exchange 2013 Help'
TOCTitle: Configuration des pièces jointes actuelles avec OneDrive Entreprise et Exchange 2016 en local
ms:assetid: 799518aa-7cfe-4708-92ee-98057ff168f5
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Mt589761(v=EXCHG.150)
ms:contentKeyID: 70319560
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configuration des pièces jointes actuelles avec OneDrive Entreprise et Exchange 2016 en local

 

_<strong>Sapplique à :</strong>Exchange Server 2016_

_<strong>Dernière rubrique modifiée :</strong>2016-12-09_

**Résumé** : Comment permettre à vos utilisateurs Exchange Server 2016 localement de tirer parti de l’utilisation de la collaboration sur des documents avec OneDrive Entreprise et SharePoint Online dans une configuration hybride.

Une nouvelle option de pièce jointe a récemment été rendue disponible dans Office 365. Dans Exchange 2016, cette option, appelée *collaboration sur les documents*, permet aux utilisateurs en local d’intégrer des pièces jointes stockées sur OneDrive Entreprise directement dans leurs clients Outlook sur le web.

> [!NOTE]
> À partir de la version de Exchange Server 2016, Outlook Web App s’appelle désormais Outlook sur le web.


En règle générale, un utilisateur envoie un fichier à d’autres personnes en pièce jointe dans un message. Un ou plusieurs destinataires apportent ensuite des modifications dans leurs copies respectives du fichier, qui doivent finalement être toutes fusionnées à un moment donné. En outre, ces fichiers joints occupent de l’espace de stockage dans la boîte aux lettres de chaque utilisateur. Avec la collaboration sur les documents, les utilisateurs insèrent plutôt un lien vers un fichier qui est stocké dans un compte OneDrive Entreprise, ce qui permet la modification du fichier par plusieurs personnes au même emplacement source, sans espace de stockage supplémentaire requis.

Avant la configuration correcte de l’environnement Exchange 2016 pour la collaboration sur des documents, la boîte de dialogue des pièces jointes par défaut d’un utilisateur d’Outlook sur le web sera semblable à ce qui suit :

![Boîte de dialogue de pièce jointe traditionnelle](images/Mt589761.f8c74d70-42f9-48c6-b263-ce6cef8591a8(EXCHG.150).png "Boîte de dialogue de pièce jointe traditionnelle")

Après avoir configuré votre environnement selon les instructions ci-dessous, les boîtes de dialogue de pièce jointe Outlook sur le web seront semblables à ce qui suit :

![Boîte de dialogue de pièce jointe avec activation des pièces jointes modernes](images/Mt589761.89eeae65-ce3a-4c47-b57e-db734a1de95b(EXCHG.150).png "Boîte de dialogue de pièce jointe avec activation des pièces jointes modernes")

Les utilisateurs de votre organisation avec des boîtes aux lettres locales et qui ont un compte professionnel OneDrive dans Office 365 sont autorisés à utiliser la méthode de pièce jointe moderne, qui leur permet de partager un document stocké dans OneDrive Entreprise avec plusieurs destinataires. L’emplacement des destinataires (en ligne ou local) n’a pas d’importance.

Pour en savoir plus sur les déploiements hybrides, voir [Déploiements hybrides Exchange Server](exchange-server-hybrid-deployments-exchange-2013-help.md).

## Ce qu’il faut savoir avant de commencer ?

  - Durée d'exécution estimée : 15 minutes

  - Consultez [Déploiements hybrides Exchange Server](exchange-server-hybrid-deployments-exchange-2013-help.md) et assurez-vous de comprendre quels domaines seront affectés par la configuration d'un déploiement hybride.

  - Examinez et remplissez toutes les conditions préalables au déploiement hybride décrites dans [Configuration requise pour un déploiement hybride](hybrid-deployment-prerequisites-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](https://technet.microsoft.com/fr-fr/library/jj150484\(v=exchg.150\)).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.


## Configurer Exchange 2016 pour activer la collaboration sur les documents dans un environnement hybride

Vérifiez que les étapes préalables suivantes ont été effectuées, puis utilisez la procédure suivante pour activer la collaboration sur les documents.

**Conditions préalables**

  - Configurez votre environnement hybride Exchange à l’aide de l’[Assistant de configuration hybride](hybrid-configuration-wizard-exchange-2013-help.md) (HCW).

  - Exchange 2016 doit être installé dans votre organisation en local. Exchange 2016 peut coexister avec les versions antérieures d’Exchange, mais la collaboration sur les documents fonctionne uniquement pour les boîtes aux lettres sur un serveur Exchange 2016.

  - Le serveur d’authentification doit être installé avec tous les utilisateurs synchronisés. Vous pouvez utiliser l’applet de commande [Get-AuthServer](https://technet.microsoft.com/fr-fr/library/jj218613\(v=exchg.150\)) pour trouver votre serveur d’authentification. Nous recommandons l’utilisation du HCW d’un serveur Exchange 2016 pour effectuer les configurations OAuth nécessaires.
    
    > [!IMPORTANT]
    > OAuth doit être configuré correctement entre Exchange 2016 et Office 365. Pour plus d’informations, voir <a href="https://technet.microsoft.com/fr-fr/library/dn594521(v=exchg.150)">Configurer l’authentification OAuth entre des organisations Exchange et Exchange Online</a>.


  - Les utilisateurs doivent disposer des licences appropriées. Les utilisateurs avec un compte professionnel OneDrive doivent avoir une licence pour SharePoint Online ou OneDrive Entreprise. Vous pouvez vérifier la licence d’un utilisateur en sélectionnant l’utilisateur dans le portail Office 365 et en sélectionnant le bouton **Modifier**.
    
    > [!NOTE]
    > Voir <a href="http://go.microsoft.com/fwlink/p/?linkid=627455">Configurer OneDrive Entreprise dans Office 365</a> pour plus d’informations.


Procédez comme suit :

1.  Configurez la stratégie de boîte aux lettres Outlook sur le web par défaut pour définir l’URL hôte de OneDrive Entreprise.
    
    > [!NOTE]
    > Vous pouvez accéder à l’administration du client Office 365 SharePoint Online pour récupérer l’URL hôte de OneDrive Entreprise. Par exemple, https://contoso-my.sharepoint.com est une URL hôte Mon site dans le client O365 de Contoso.<br />
    > Bien que la stratégie de boîte aux lettres d’Outlook sur le web fournie avec Exchange 2016 soit appelée « Par défaut », elle n’est pas appliquée automatiquement aux boîtes aux lettres, sauf si vous définissez la stratégie par défaut, ou l’attribuez directement à une boîte aux lettres.
    
    En utilisant l’exemple suivant comme base, utilisez le Environnement de ligne de commande Exchange Management Shell pour configurer l’URL Mon site interne et externe sur la stratégie de boîte aux lettres d’Outlook sur le web par défaut :
    
        Set-OwaMailboxPolicy Default -InternalSPMySiteHostURL https://Contoso-my.sharepoint.com -ExternalSPMySiteHostURL https://Contoso-my.sharepoint.com

2.  Ensuite, définissez la stratégie que vous venez de configurer comme stratégie par défaut, afin qu’elle soit appliquée à toutes les boîtes aux lettres, ou affectez la stratégie à des utilisateurs individuels.
    
    Pour que la stratégie soit la stratégie de boîte aux lettres d’Outlook sur le web par défaut, tapez la commande suivante dans le Environnement de ligne de commande Exchange Management Shell :
    
        Set-OwaMailboxPolicy Default -IsDefault 
    
    Pour affecter la stratégie à la boîte aux lettres d’une personne, tapez la commande suivante dans le Environnement de ligne de commande Exchange Management Shell:
    
        Set-CASMailbox <user mailbox> -OwaMailboxPolicy Default

3.  (Facultatif) Sur chaque serveur Exchange 2016, redémarrez **OWAApplicationPool** pour que la configuration fonctionne immédiatement. Si vous n’exécutez cette commande, il faudra quelques minutes pour que vos serveurs Exchange 2016 appliquent la stratégie de boîte aux lettres mise à jour. Dans l’exécution de Environnement de ligne de commande Exchange Management Shell :
    
        Restart-WebAppPool MSExchangeOWAAppPool

Une fois la configuration terminée, les utilisateurs d’Outlook sur le web se verront proposer de choisir le type de pièce jointe qu’ils souhaitent appliquer à leurs messages : traditionnel ou moderne.

![Boîte de dialogue d’options de pièces jointes, Partager avec OneDrive ou Envoyer en tant que pièce jointe](images/Mt589761.7d2f27c2-3638-479a-a577-029ac61e7d95(EXCHG.150).png "Boîte de dialogue d’options de pièces jointes, Partager avec OneDrive ou Envoyer en tant que pièce jointe")

