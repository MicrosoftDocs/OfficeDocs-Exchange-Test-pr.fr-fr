---
title: 'Activation du point de terminaison du proxy MRS pour les déplacements distants: Exchange 2013 Help'
TOCTitle: Activation du point de terminaison du proxy MRS pour les déplacements distants
ms:assetid: 9840f712-127e-4c2d-bfe5-1b35cdb2a31b
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dn155787(v=EXCHG.150)
ms:contentKeyID: 54652766
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Activation du point de terminaison du proxy MRS pour les déplacements distants

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2013-07-02_

Le serveur proxy du service de réplication de boîtes aux lettres (proxy MRS) facilite les déplacements de boîtes aux lettres inter-forêts et les migrations de déplacement à distance entre votre organisation Exchange locale et Exchange Online. Dans Exchange 2013, le proxy MRS est inclus dans le rôle serveur de boîtes aux lettres (également appelé *Serveur de boîtes aux lettres*). Durant les migrations de déplacement à distance et inter-forêts, un serveur d'accès au client agit en tant que proxy pour les demandes de déplacement entrantes pour le serveur de boîtes aux lettres. Par défaut, la capacité d'un serveur d'accès au client d'accepter ces demandes est désactivée. Pour permettre au serveur d'accès au client d'accepter des demandes de déplacement entrantes, vous devez activer le point de terminaison du proxy MRS.

Le choix du serveur d'accès au client sur lequel activer le point de terminaison du proxy MRS dépend du type et de la direction du déplacement de boîte aux lettres.

  - **Déplacements d'entreprise inter-forêts**   Pour les déplacements inter-forêts opérés à partir de l'environnement cible (dits de type *pull*), vous devez activer le point de terminaison du proxy MRS sur les serveurs d'accès au client dans l'environnement source. Pour les déplacements inter-forêts opérés à partir de l'environnement source (dits de type *push*), vous devez activer le point de terminaison du proxy MRS sur les serveurs d'accès au client dans l'environnement cible.

  - **Migrations de déplacement à distance entre une organisation Exchange locale et Exchange Online**   Pour les migrations de déplacement à distance, tant par embarquement que par débarquement, vous devez activer le point de terminaison du proxy MRS sur les serveurs d'accès au client au sein de votre organisation locale.

> [!NOTE]
> Si vous utilisez le CAE pour déplacer des boîtes aux lettres, les déplacements inter-forêts et les migrations de déplacement à distance par embarquement sont des déplacements de type pull parce que la demande provient de l'environnement cible. Les migrations de déplacement à distance par débarquement sont des déplacements de type push parce que la demande provient de l'environnement source.


## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : 2 minutes par serveur.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Autorisations des services web Exchange » dans la rubrique [Autorisations des clients et des périphériques mobiles](clients-and-mobile-devices-permissions-exchange-2013-help.md).

  - Si vous avez déployé plusieurs serveurs d'accès au client dans votre organisation Exchange, vous devez activer le point de terminaison du proxy MRS sur chacun d'eux. Si vous ajoutez des serveurs d'accès au client, veillez à activer le point de terminaison du proxy MRS sur les nouveaux serveurs. Les déplacements inter-forêts et les migrations de déplacement à distance peuvent échouer si le point de terminaison du proxy MRS n'est pas activé sur tous les serveurs d'accès au client.

  - Si vous n'effectuez pas de déplacements inter-forêts ou de migrations de déplacement à distance, veillez à ce que les points de terminaison du proxy MRS soient désactivés afin de réduire la surface d'attaque de votre organisation.

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..


## Que souhaitez-vous faire ?

## Utiliser le CAE pour activer le point de terminaison du proxy MRS

1.  Dans le CAE, accédez à **Destinataires** \> **Serveurs** \> **Répertoires virtuels**.

2.  Dans la liste déroulante **Sélectionner le serveur**, sélectionnez le nom du serveur d'accès au client sur lequel vous voulez activer le point de terminaison du proxy MRS. Vous pouvez également sélectionner **Tous les serveurs** pour afficher les répertoires virtuels sur tous les serveurs d'accès au client de votre organisation.

3.  Dans la liste déroulante **Sélectionner le type**, sélectionnez **EWS** pour afficher le répertoire virtuel du service web Exchange (EWS) pour le serveur sélectionné.

4.  Dans la liste des répertoires virtuels, cliquez sur **EWS (site web par défaut)** pour le serveur d'accès au client à configurer, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

5.  Dans la page de propriétés **EWS (site web par défaut)**, activez la case à cocher **Proxy MRS activé**, puis cliquez sur **Enregistrer**.

## Utiliser l'environnement de ligne de commande pour activer le point de terminaison du proxy MRS

La commande suivante active le point de terminaison du proxy MRS sur un serveur d'accès au client nommé EXCH-SRV-01.

    Set-WebServicesVirtualDirectory -Identity "EXCH-SRV-01\EWS (Default Web Site)" -MRSProxyEnabled $true

La commande suivante active le point de terminaison du proxy MRS sur tous les serveurs d'accès au client au sein de votre organisation Exchange.

    Get-WebServicesVirtualDirectory | Set-WebServicesVirtualDirectory -MRSProxyEnabled $true

> [!NOTE]
> Comme indiqué précédemment, le point de terminaison du proxy MRS doit être activé sur chaque serveur d'accès au client au sein de votre organisation. Après avoir ajouté un serveur d'accès au client à votre organisation, exécutez la commande précédente.


## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez bien activé le point de terminaison du proxy MRS, procédez comme suit :

1.  Dans le CAE, accédez à **Destinataires** \> **Serveurs** \> **Répertoires virtuels**.

2.  Dans la liste des répertoires virtuels, cliquez sur **EWS (site web par défaut)**, puis vérifiez dans le volet des détails que le point de terminaison du proxy MRS est activé.
    
    Vous pouvez également cliquer sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier") pour afficher la page de propriétés **EWS (site web par défaut)** et vérifier que la case à cocher **Proxy MRS activé** est sélectionnée.

Ou

Exécutez la commande suivante dans l'environnement de ligne de commande :

    Get-WebServicesVirtualDirectory | FL Identity,MRSProxyEnabled

Vérifiez que le paramètre *MRSProxyEnabled* est défini sur `True`.

Une autre manière de vérifier que le point de terminaison du proxy MRS est activé consiste à utiliser la cmdlet **Test-MigrationServerAvailability** pour tester la capacité de communiquer avec le serveur distant hébergeant les boîtes aux lettres à déplacer ou, en cas de débarquement de boîtes aux lettres Exchange Online dans votre organisation locale, avec un serveur au sein de votre organisation locale. Pour plus d'informations, consultez la rubrique [Test-MigrationServerAvailability](https://technet.microsoft.com/fr-fr/library/jj219169\(v=exchg.150\)).

L'exemple suivant montre comment tester la connexion au serveur dans la forêt corp.contoso.com.

    $Credentials = Get-Credential

    Test-MigrationServerAvailability -ExchangeRemoteMove -Autodiscover -EmailAddress administrator@corp.contoso.com -Credentials $Credentials

Pour que l'exécution de cette commande réussisse, le point de terminaison du proxy MRS soit être activé.

