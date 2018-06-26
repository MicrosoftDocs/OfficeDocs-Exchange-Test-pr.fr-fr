---
title: "Simplification de l'URL d'Outlook Web App: Exchange 2013 Help"
TOCTitle: Simplification de l'URL d'Outlook Web App
ms:assetid: 5fb6a873-f3cf-4f82-87d1-2ff6e47a0080
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Aa998359(v=EXCHG.150)
ms:contentKeyID: 54652756
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Simplification de l'URL d'Outlook Web App

 

_**Sapplique à :**Exchange Server 2013_

_**Dernière rubrique modifiée :**2015-07-16_

**Résumé** : Utilisez les procédures décrites dans cet article pour simplifier l’URL que les utilisateurs de votre organisation utilisent pour accéder à OWA dans Exchange 2013.

Vous pouvez simplifier l’URL MicrosoftOutlook Web App que les utilisateurs utilisent pour accéder à leur boîte aux lettres Exchange Server 2013.

Pour simplifier l’accès à Outlook Web App pour vos utilisateurs, vous pouvez configurer la page web d’Outlook Web App, qui est généralement le site web par défaut dans IIS, afin de rediriger automatiquement les utilisateurs vers https. La procédure décrite dans la section « Utiliser le Gestionnaire des services Internet (IIS) pour simplifier l'URL d'Outlook Web App et forcer la redirection vers SSL » redirige une demande pour http://*serveur* vers https://*serveur*/owa. Pour sécuriser les informations envoyées entre le client et le serveur, le site web par défaut est défini pour exiger le protocole SSL (Secure Sockets Layer) lors de l’installation.

Lorsque vous configurez la redirection à partir d'un répertoire de premier niveau dans Windows Server 2008, les paramètres sont propagés vers les répertoires de bas niveau. Par exemple, quand vous configurez la redirection du site web par défaut vers le répertoire virtuel /owa, les paramètres que vous configurez apparaissent également dans la page Redirection HTTP de tous les répertoires virtuels, tels que /Autodiscover, /Exchange et /Public. Par conséquent, vous devez supprimer la redirection de tous les répertoires virtuels sauf celle du répertoire à rediriger.

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : 10 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l'entrée « Gestionnaire des services Internet » dans la section Autorisations Outlook Web App de la rubrique [Autorisations des clients et des périphériques mobiles](clients-and-mobile-devices-permissions-exchange-2013-help.md).

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


## Étape 1 : utiliser le Gestionnaire des services Internet (IIS) pour simplifier l’URL d’Outlook Web App et forcer la redirection vers SSL

1.  Démarrez le Gestionnaire des services Internet.

2.  Développez l'ordinateur local et **Sites**, puis cliquez sur **Site web par défaut**.

3.  En bas du volet Page d'accueil du site Web par défaut, cliquez sur **Affichage des fonctionnalités** si cette option n'est pas déjà activée.

4.  Dans la section **IIS**, double-cliquez sur **Redirection HTTP**.

5.  Activez la case à cocher **Rediriger les demandes vers cette destination**.

6.  Tapez le chemin d'accès absolu du répertoire virtuel /owa, par exemple, **https://mail.contoso.com/owa**.

7.  Sous **Rediriger le comportement**, activez la case à cocher **Rediriger unique. les dem. vers contenu de ce rép. (pas les sous-rép.)**.

8.  Dans la liste **Code d'état**, cliquez sur **Trouvé (302)**.

9.  Dans le volet Actions, cliquez sur **Appliquer**.

10. Cliquez sur **Site web par défaut**.

11. Dans le volet Page d'accueil du site web par défaut, cliquez sur **Paramètres SSL**.

12. Dans **paramètres SSL**, décochez la case **Exiger SSL**.
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Si vous ne décochez pas la case <strong>Exiger SSL</strong>, les utilisateurs ne seront pas redirigés lors de la saisie d’une URL non sécurisée. Une erreur d’accès refusé s’affichera à la place.</td>
    </tr>
    </tbody>
    </table>


## Étape 2 : supprimer la redirection des répertoires virtuels

Pour supprimer la redirection d'un répertoire virtuel, procédez comme suit :

1.  Ouvrez une fenêtre d'invite de commandes.

2.  Accédez au \<*répertoire Windows*\>\\System32\\Inetsrv.

3.  Exécutez les commandes suivantes :
    
    1.  `appcmd set config "Default Web Site/autodiscover" /section:httpredirect /enabled:false -commit:apphost`
    
    2.  `appcmd set config "Default Web Site/ecp" /section:httpredirect /enabled:false -commit:apphost`
    
    3.  `appcmd set config "Default Web Site/ews" /section:httpredirect /enabled:false -commit:apphost`
    
    4.  `appcmd set config "Default Web Site/owa" /section:httpredirect /enabled:false -commit:apphost`
    
    5.  `appcmd set config "Default Web Site/oab" /section:httpredirect /enabled:false -commit:apphost`
    
    6.  `appcmd set config "Default Web Site/powershell" /section:httpredirect /enabled:false -commit:apphost`
    
    7.  `appcmd set config "Default Web Site/rpc" /section:httpredirect /enabled:false -commit:apphost`
    
    8.  `appcmd set config "Default Web Site/rpcwithcert" /section:httpredirect /enabled:false -commit:apphost`
    
    9.  `appcmd set config "Default Web Site/Microsoft-Server-ActiveSync" /section:httpredirect /enabled:false -commit:apphost`

4.  Terminez la procédure en exécutant la commande `iisreset/noforce`.

Quand vous configurez la redirection à partir d'un répertoire de niveau supérieur, un fichier web.config peut être créé sous \<*lecteur*\>\\Program Files\\Microsoft\\Exchange Server\\\<*version*\>\\ClientAccess\\oab. Si cela s'est produit et que vous supprimez ultérieurement la redirection, Outlook peut se bloquer quand les utilisateurs cliquent sur **Envoyer et recevoir**. Pour éviter ce problème après la suppression de la redirection, supprimez le fichier web.config de \<*lecteur*\>\\Program Files\\Microsoft\\Exchange Server\\\<*version*\>\\ClientAccess\\oab.

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez bien simplifié l'URL d'Outlook Web App et redirigé celle-ci vers une connexion SSL, procédez comme suit :

1.  Ouvrez un navigateur web et entrez la nouvelle URL pour Outlook Web App en utilisant le format http://\<*URL*\>.

2.  Vous devriez être redirigé vers la page de connexion d'Outlook Web App via une connexion SSL.

