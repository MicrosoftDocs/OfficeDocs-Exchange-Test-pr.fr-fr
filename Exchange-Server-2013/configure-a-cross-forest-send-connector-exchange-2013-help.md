---
title: "Configuration d'un connecteur d'envoi inter-forêts: Exchange 2013 Help"
TOCTitle: Configuration d'un connecteur d'envoi inter-forêts
ms:assetid: 7840d172-071e-4f13-9379-2fe1eee1a7cc
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ945053(v=EXCHG.150)
ms:contentKeyID: 52062968
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configuration d'un connecteur d'envoi inter-forêts

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2013-02-21_

Dans Active Directory, la *forêt* représente la limite extérieure de votre service d'annuaire. Vous pouvez créer des connecteurs d'envoi pour activer la communication entre les forêts. Dans cet exemple, les connecteurs utilisent une authentification de base.

Pour découvrir d'autres tâches de gestion relatives à la configuration des connecteurs, consultez la rubrique [Connecteurs](connectors-exchange-2013-help.md).

Vou ssouhaitez découvrir des scénarios dans lesquels cette procédure est utilisée ? Consultez les rubriques suivantes :

  - [Déploiement d’Exchange 2013 dans une topologie inter-forêts](deploy-exchange-2013-in-a-cross-forest-topology-exchange-2013-help.md)

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : 20 minutes

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez les entrées « Connecteurs d'envoi » et « Connecteurs de réception » dans la rubrique [Autorisations de flux de messagerie](mail-flow-permissions-exchange-2013-help.md).

  - Consultez la rubrique [Déployer une nouvelle installation d’Exchange 2013](deploy-a-new-installation-of-exchange-2013-exchange-2013-help.md) si vous commencez votre installation. À l'issue de l'installation, vous pouvez utiliser les étapes décrites dans cette rubrique pour créer des connecteurs et configurer une topologie inter-forêts.

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


## Que souhaitez-vous faire ?

## Créer un compte d'utilisateur dans chaque forêt

Vous devez créer un compte d'utilisateur dans chaque forêt à utiliser pour l'authentification de base. Créez un compte dans chaque forêt et ajoutez-le au groupe universel de sécurité du serveur Exchange utilisé pour la communication. Le connecteur d'envoi utilise ce compte pour s'authentifier auprès du serveur qui reçoit le courrier dans l'autre forêt. Par exemple, fournissez comme informations d'identification un compte d'utilisateur dont le nom d'utilisateur principal (UPN) est FourthCoffee@Contoso.com à utiliser à des fins d'authentification par le serveur Exchange dans le domaine Fourth Coffee lors de l'envoi d'un message au serveur Exchange dans le domaine Contoso.

## Utiliser le Centre d'administration Exchange (CAE) pour créer un connecteur d'envoi afin d'acheminer le courrier électronique vers une autre forêt Exchange 2013

Établissez un flux de messagerie inter-forêts à l'aide de l'authentification de base.

1.  Dans le CAE, accédez à **Flux de messagerie** \> **Connecteurs de réception**. Cliquez sur **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter").

2.  Dans l'Assistant **Nouveau connecteur d'envoi**, spécifiez le nom du connecteur d'envoi, puis sélectionnez **Internet** en tant que **Type**. Cliquez sur **Suivant**.

3.  Sélectionnez **Acheminer tous les messages via les hôtes actifs**, puis cliquez sur **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter"). Dans la fenêtre **Ajouter un hôte actif**, spécifiez l'adresse IP du serveur cible dans la seconde forêt, par exemple 64.4.6.100. Cliquez sur **Enregistrer**, puis sur **Suivant**.
    
    Pour **Authentification d'un hôte actif**, sélectionnez **Authentification de base** et fournissez un nom d'utilisateur et un mot de passe. Vous pouvez alors choisir **Ne proposer l'authentification de base qu'après le démarrage de TLS** pour une communication sécurisée sur TLS.
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Si vous utilisez une authentification de base sur TLS, le serveur cible doit être configuré pour utiliser un certificat X.509.</td>
    </tr>
    </tbody>
    </table>


4.  Sous **Espace d'adressage**, cliquez sur **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter"). Dans la fenêtre **Ajouter un domaine**, vérifiez que SMTP apparaît dans la liste **Type**. Pour **Nom de domaine complet (FQDN)**, entrez le domaine de réception, par exemple fourthcoffee.com. Cliquez sur **Enregistrer**, puis sur **Suivant**.

5.  Pour **Serveur source**, cliquez sur **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter"). Dans la fenêtre **Sélectionner un serveur**, choisissez le serveur à utiliser et cliquez sur **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter"). Cliquez sur **OK**.

6.  Cliquez sur **Terminer**. Le connecteur apparaît dans la liste des connecteurs d'envoi.

Une fois votre connecteur d'envoi créé, créez un connecteur d'envoi dans la seconde forêt qui envoie le courrier à la forêt d'origine. Dans ce cas, le nom de domaine complet (FQDN) spécifié sera le nom de domaine de la première forêt. Par exemple, contoso.com.

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour définir des autorisations sur le connecteur d'envoi

Cet exemple utilise le script Enable-CrossForestConnector.ps1 dans l'environnement de ligne de commande Exchange Management Shell pour définir des autorisations sur le connecteur d'envoi à utiliser dans une topologie inter-forêts.

    .\Enable-CrossForestConnector.ps1 -Connector "Cross-Forest" -user "ANONYMOUS LOGON"

## Comment savoir si cela a fonctionné ?

Pour vérifier que des connecteurs d'envoi ont bien été créés pour acheminer le courrier électronique vers une seconde forêt, envoyez un message depuis un utilisateur de votre organisation (vous pouvez utiliser Outlook Web App) vers le domaine spécifié pour l'**Espace d'adressage**. Si le destinataire reçoit le message, vous avez correctement configuré le connecteur d'envoi.

## Pour plus d'informations

[Créer un connecteur d’envoi pour les messages électroniques envoyés vers Internet](create-a-send-connector-for-email-sent-to-the-internet-exchange-2013-help.md)

[Connecteurs d'envoi](send-connectors-exchange-2013-help.md)

