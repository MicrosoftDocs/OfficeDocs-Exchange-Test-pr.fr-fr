---
title: 'Affichage ou configuration des répertoires virtuels d’Outlook Web App: Exchange 2013 Help'
TOCTitle: Affichage ou configuration des répertoires virtuels d’Outlook Web App
ms:assetid: 90babcf6-4486-4e01-9819-6d3ca4ed756c
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dd298140(v=EXCHG.150)
ms:contentKeyID: 50478689
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Affichage ou configuration des répertoires virtuels d’Outlook Web App

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2013-08-12_

Le Centre d'administration Exchange (CAE) ou l'environnement de ligne de commande Exchange Management Shell permet d'afficher ou de configurer les propriétés d'un répertoire virtuel Outlook Web App.

<table>
<thead>
<tr class="header">
<th><img src="images/Bb125224.warning(EXCHG.150).gif" title="Avertissement" alt="Avertissement" />Avertissement :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Dans Exchange Online, les administrateurs ne peuvent pas afficher ou configurer les répertoires virtuels Outlook Web App.</td>
</tr>
</tbody>
</table>


Si vous utilisez l'environnement de ligne de commande Exchange Management Shell pour afficher les propriétés d'un répertoire virtuel Outlook Web App, les informations renvoyées représentent un sous-ensemble des informations disponibles. Par exemple, si vous utilisez la cmdlet **Get-OWAVirtualDirectory** pour afficher les propriétés, Exchange retourne les informations suivantes :

  - Nom du répertoire virtuel

  - Nom de serveur

  - Version du serveur Exchange

Vous pouvez également extraire des informations pour un répertoire virtuel spécifique sur un serveur spécifique à l'aide des paramètres disponibles. Pour plus d'informations sur les paramètres de la cmdlet **Get-OWAVirtualDirectory**, consultez la rubrique [Get-OwaVirtualDirectory](https://technet.microsoft.com/fr-fr/library/aa998588\(v=exchg.150\)).

Si vous utilisez le CAE pour afficher les propriétés d’un répertoire virtuel Outlook Web App, vous pourrez afficher la plupart des propriétés relatives au répertoire virtuel que vous visualisez.

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée de chaque procédure : 10 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l'entrée « Répertoires virtuels Outlook Web App » de la rubrique [Autorisations des clients et des périphériques mobiles](clients-and-mobile-devices-permissions-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

<table>
<thead>
<tr class="header">
<th><img src="images/Bb125224.tip(EXCHG.150).gif" title="Conseil" alt="Conseil" />Conseil :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..</td>
</tr>
</tbody>
</table>


## Que souhaitez-vous faire ?

## Utiliser le CAE pour afficher ou configurer les propriétés d'un répertoire virtuel Outlook Web App

1.  Dans le CAE, cliquez sur **Serveurs** \> **Répertoires virtuels**.
    
    Utilisez les listes déroulantes pour sélectionner le serveur et le type de répertoire virtuel. Par défaut, tous les serveurs et répertoires virtuels sont affichés.

2.  Dans le volet Résultats, sélectionnez le répertoire virtuel que vous souhaitez afficher ou modifier, puis cliquez sur **Modifier**.

3.  L'onglet **Général** vous permet d'afficher les propriétés du site web par défaut Outlook Web App et de spécifier une URL externe et une URL interne. Affichez ou sélectionnez les options suivantes :
    
      - **Serveur**   (Lecture seule.) Le champ **Serveur** affiche le nom du serveur qui héberge le répertoire virtuel d'Outlook Web App.
    
      - **Version**   (Lecture seule.) Le champ **Version** affiche la version du serveur Exchange sur lequel réside le répertoire virtuel.
    
      - **Site Web**   (Lecture seule.) Le champ **Site web** affiche le nom du site web.
    
      - **Version d'Outlook Web App**   (Lecture seule.) Le champ **Version Outlook Web App** affiche la version du serveur Exchange.
    
      - **Modifié**   (Lecture seule.) Le champ **Modifié** affiche la date et l'heure auxquelles le répertoire virtuel a été modifié pour la dernière fois.
    
      - **URL interne**   Cette zone de texte permet de spécifier l'URL utilisée pour accéder à ce site web à partir d'un réseau interne. Une adresse URL interne est configurée automatiquement lors de l'installation d'Exchange 2013. La configuration de l'URL interne par défaut pour un serveur connecté ou non à Internet est https://\<Nom de l'ordinateur\>/owa.
    
      - **URL externe**   Cette zone de texte permet de spécifier l'URL utilisée pour accéder à ce site web à partir d'Internet. Par défaut, le paramètre **URL externe** est vide. Pour les serveurs d'accès au client connectés à Internet, la propriété **URL externe** doit être définie sur la valeur publiée dans le DNS de ce site Active Directory. Pour les serveurs Exchange 2013 n'ayant pas de présence Internet, le paramètre **URL externe** doit rester vide.

4.  L'onglet **Authentification** permet de spécifier les méthodes d'authentification, le format de connexion et le domaine de connexion.
    
      - **Utiliser une ou plusieurs méthodes d'authentification standard**   Activez cette option pour utiliser une ou plusieurs des méthodes d'authentification standard suivantes :
        
        **Authentification Windows intégrée**   Cette méthode requiert que les utilisateurs disposent d'un nom de compte et d'un mot de passe d'utilisateur Windows Server 2008 ou Windows Server 2012 valides pour accéder aux informations. Les utilisateurs ne sont pas invités à entrer leurs noms de compte et mots de passe. En revanche, le serveur négocie avec les modules de sécurité Windows installés sur l'ordinateur client. L'authentification Windows intégrée active le serveur pour authentifier les utilisateurs sans leur demander d'informations et sans transmettre d'informations non chiffrées sur le réseau. Pour que cette méthode fonctionne, l'ordinateur client doit être membre du même domaine que les serveurs exécutant Exchange ou d'un domaine approuvé par le domaine dans lequel se trouve le serveur Exchange.
        
        **Authentification Digest pour les serveurs de domaine Windows**   Cette méthode transmet les mots de passe sur le réseau en tant que valeur de hachage pour plus de sécurité. L'authentification Digest ne peut s'utiliser que dans des domaines Windows Server 2008 et Windows Server 2012 pour des utilisateurs possédant un compte enregistré dans Active Directory. Pour plus d'informations sur l'authentification Digest, consultez la documentation Windows Server.
        
        **Authentification de base (mot de passe envoyé en texte clair)**   Cette méthode est un mécanisme d'authentification simple défini par la spécification HTTP qui code le nom et le mot de passe de connexion d'un utilisateur avant d'envoyer les informations d'identification de l'utilisateur au serveur. Pour vous assurer que le mot de passe est aussi sécurisé que possible, vous devez utiliser le chiffrement SSL (Secure Sockets Layer) entre les ordinateurs clients et le serveur sur lequel le rôle serveur d'accès au client est installé.
    
      - **Utiliser l'authentification basée sur des formulaires**   L'authentification basée sur des formulaires fournit une sécurité optimisée pour les répertoires virtuels Outlook Web App. L'authentification basée sur des formulaires crée une page de connexion pour Outlook Web App. Vous pouvez configurer le type d'invite de connexion utilisé par l'authentification basée sur des formulaires. Par exemple, vous pouvez configurer une authentification basée sur des formulaires pour demander aux utilisateurs qu'ils fournissent leurs informations de nom d'utilisateur et de domaine, au format domaine\\nom d'utilisateur dans la page de connexion d'Outlook Web App.
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/JJ159813.important(EXCHG.150).gif" title="Important" alt="Important" />Important :</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>L'authentification basée sur des formulaires ne sera pas sécurisée tant que la SSL ne sera pas activée.</td>
        </tr>
        </tbody>
        </table>
        
        Activez l'une des options suivantes :
        
        **Domaine\\Nom d'utilisateur**   L'utilisateur doit entrer le domaine et le nom de l'utilisateur selon le format domaine\\nom d'utilisateur. Par exemple, pour un utilisateur nommé Kweku dans le domaine Contoso, la connexion serait contoso\\kweku.
        
        **Nom d'utilisateur principal (UPN)** Si le format de connexion du nom d'utilisateur principal (UPN) est spécifié, la zone **Nom d'utilisateur** de la page de connexion d'Outlook Web App permet aux utilisateurs d'entrer leur adresse de messagerie, par exemple : kweku@contoso.com. Si l'UPN d'un utilisateur diffère de son adresse de messagerie, l'utilisateur ne peut pas accéder à Outlook Web App via l'invite de connexion **PrincipalName**. Il est préférable d'utiliser l'invite de connexion **PrincipalName** uniquement si l'UPN des utilisateurs est identique à leur adresse de messagerie.
        
        **Nom d'utilisateur uniquement** L'utilisateur n'entre que le nom d'utilisateur, sans le nom de domaine, par exemple, Kweku. Si vous utilisez l'invite de connexion **Nom d'utilisateur uniquement** pour une authentification basée sur des formulaires, vous devez également spécifier la propriété **Domaine de connexion**. La propriété **Domaine de connexion** détermine le domaine par défaut à utiliser lorsqu'un utilisateur tente de se connecter à Outlook Web App. Par exemple, si le domaine par défaut est Contoso et qu'un utilisateur de domaine nommé Kweku se connecte à Outlook Web App, seul le nom d'utilisateur Kweku doit être entré. Le serveur utilisera le domaine par défaut Contoso. Si l'utilisateur n'est pas membre du domaine Contoso, le nom d'utilisateur et le domaine doivent être entrés.

5.  L'onglet **Fonctionnalités** permet de spécifier les fonctionnalités que vous souhaitez activer ou désactiver pour les utilisateurs d'Outlook Web App sur un répertoire virtuel.
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Les paramètres de fonctionnalités pour des utilisateurs individuels remplacent les paramètres de répertoire virtuel. Vous pouvez modifier les paramètres de fonctionnalités pour des utilisateurs individuels à l'aide de la cmdlet <strong>Set-CASMailbox</strong> ou des stratégies de boîte aux lettres Outlook Web App. Pour plus d'informations, consultez la rubrique <a href="outlook-web-app-mailbox-policies-exchange-2013-help.md">Stratégies de boîte aux lettres de Outlook Web App</a>.</td>
    </tr>
    </tbody>
    </table>
    
    Utilisez les cases à cocher pour activer ou désactiver des fonctionnalités. Par défaut, les fonctionnalités les plus courantes sont affichées. Pour afficher toutes les fonctionnalités pouvant être activées ou désactivées, cliquez sur **plus d'options**.
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>L'option d'activation ou de désactivation de la version standard d'Outlook Web App à l'aide de la case à cocher <strong>Client premium</strong> est obsolète et sera supprimée des paramètres. La version standard d'Outlook Web App est toujours activée.</td>
    </tr>
    </tbody>
    </table>


6.  Sous l'onglet **Accès au fichier**, utilisez les cases à cocher pour configurer l'accès au fichier et afficher les options offertes aux utilisateurs. L'accès aux fichiers permet aux utilisateurs d'ouvrir ou d'afficher le contenu de fichiers envoyés sous forme de pièces jointes dans un message électronique.
    
    L'accès aux fichiers peut être contrôlé en fonction de la connexion de l'utilisateur sur un ordinateur public ou privé. La possibilité offerte aux utilisateurs de sélectionner un accès à un ordinateur privé ou public n’est proposée que si vous utilisez une authentification basée sur des formulaires. Toutes les autres authentifications se font par défaut par l'accès à un ordinateur privé.
    
      - **Accès direct aux fichiers**   Cochez cette case si vous souhaitez activer l'accès direct aux fichiers. L'accès direct aux fichiers permet aux utilisateurs d'ouvrir des fichiers joints aux messages électroniques.
    
      - **WebReady Document Viewing**   Cochez cette case si vous souhaitez activer la conversion au format HTML et l'affichage dans un navigateur web des documents pris en charge.
    
      - **Forcer WebReady Document Viewing lorsqu'un convertisseur est disponible**   Cochez cette case si vous souhaitez forcer la conversion au format HTML et l'affichage dans un navigateur Web des documents avant que les utilisateurs ne puissent les ouvrir dans une application d'affichage. Les documents peuvent être ouverts dans l'application d'affichage uniquement si l'accès au fichier direct a été activé.

7.  Cliquez sur **Enregistrer** pour mettre à jour la stratégie.

## Utilisez l'environnement de ligne de commande Exchange Management Shell pour configurer les propriétés d'un répertoire virtuel d'Outlook Web App

Cet exemple active l'authentification basée sur des formulaires pour le répertoire virtuel Outlook Web App par défaut sur le serveur nommé Contoso.

    set-OwaVirtualDirectory -Identity "Contoso\owa (default web site)" -FormsAuthentication $true

Pour plus d'informations sur la syntaxe et les paramètres, consultez la rubrique [Set-OwaVirtualDirectory](https://technet.microsoft.com/fr-fr/library/bb123515\(v=exchg.150\)).

## Utilisez l'environnement pour afficher les propriétés d'un répertoire virtuel d'Outlook Web App

Cet exemple permet d'afficher les propriétés de tous les répertoires virtuels Outlook Web App de tous les sites web IIS (Internet Information Services) sur tous les ordinateurs dans lesquels le rôle serveur d'accès au client est installé pour une organisation Exchange.

    Get-OWAVirtualDirectory

Cet exemple affiche les propriétés d'un répertoire virtuel Outlook Web App sur le site web IIS par défaut sur le serveur Exchange local.

    Get-OWAVirtualDirectory -identity "<Exchange Server Name>\owa (default web site)"

Cet exemple affiche les propriétés de tous les répertoires virtuels Outlook Web App d'un site web IIS sur un serveur Exchange spécifique.

    Get-OWAVirtualDirectory -server <Exchange Server Name>

Cet exemple affiche les valeurs des propriétés de chaque répertoire virtuel Outlook Web App de tous les sites web IIS sur tous les serveurs d'accès au client d'une organisation Exchange.

    Get-OWAVirtualDirectory | format-list

Pour plus d'informations sur la syntaxe et les paramètres, consultez la rubrique [Get-OwaVirtualDirectory](https://technet.microsoft.com/fr-fr/library/aa998588\(v=exchg.150\)).

## Comment savoir si cela a fonctionné ?

Pour vérifier qu’un répertoire virtuel Outlook Web App a été modifié correctement, procédez comme suit :

1.  Dans le CAE, cliquez sur **Serveurs** \> **Répertoires virtuels**, puis sélectionnez un répertoire virtuel Outlook Web App spécifique.

2.  Cliquez que le bouton **Modifier** pour afficher les propriétés d'un répertoire virtuel.

3.  Cliquez sur **Enregistrer** ou sur **Annuler** pour fermer la page des propriétés.

