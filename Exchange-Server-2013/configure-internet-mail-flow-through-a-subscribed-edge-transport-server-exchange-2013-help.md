---
title: 'Configurer le flux de messagerie Internet via un serveur de transport Edge abonné: Exchange 2013 Help'
TOCTitle: Configurer le flux de messagerie Internet via un serveur de transport Edge abonné
ms:assetid: d12ea770-99ce-4ab4-a373-96f2554641fa
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb738158(v=EXCHG.150)
ms:contentKeyID: 61180549
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configurer le flux de messagerie Internet via un serveur de transport Edge abonné

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2015-04-08_

Pour établir la messagerie Internet via un serveur de transport Edge, abonnez le serveur de transport Edge à un site Active Directory. Ceci crée automatiquement les deux connecteurs d’envoi requis pour le flux de messagerie Internet :

  - un connecteur d’envoi configuré pour envoyer des messages électroniques sortants à tous les domaines Internet ;

  - un connecteur d’envoi configuré pour envoyer des messages électroniques entrants depuis le serveur de transport Edge à un serveur de boîtes aux lettres Exchange 2013.

Si vous ne souhaitez pas abonner le serveur de transport Edge à un site Active Directory, il est possible de créer manuellement des connecteurs d’envoi requis pour établir le flux de messagerie entre le serveur de boîtes aux lettres et le serveur de transport Edge. Pour plus d'informations, voir [Configurer le flux de messagerie Internet via un serveur de transport Edge sans utiliser EdgeSync](configure-internet-mail-flow-through-an-edge-transport-server-without-using-edgesync-exchange-2013-help.md). Toutefois, nous vous recommandons d’abonner le serveur de transport Edge au site Active Directory dès que possible.

## Avant de commencer

  - Durée d’exécution estimée : 20 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l’entrée « EdgeSync » et les « serveurs de transport Edge » dans la rubrique [Autorisations de flux de messagerie](mail-flow-permissions-exchange-2013-help.md).

  - Avant d’abonner un serveur de transport Edge à votre organisation, vous devez d’abord configurer les stratégies d’adresses de messagerie et les domaines faisant autorité pour votre organisation Exchange.

  - Activez le port LDAP 50636/TCP sécurisé à travers le pare-feu qui sépare votre réseau de périmètre de l’organisation Exchange. Le serveur de transport Edge doit être en mesure de communiquer avec tous les serveurs de boîtes aux lettres Exchange 2013 dans le site Active Directory abonné.

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


## Configurer le flux de messagerie Internet via un serveur de transport Edge abonné

1.  Sur le serveur de transport Edge, créez le fichier d’abonnement Edge à l’aide de la syntaxe suivante.
    
        New-EdgeSubscription -FileName <FileName>.xml [-Force]
    
    L’exemple suivant crée un fichier d’abonnement Edge nommé EdgeSubscriptionInfo.xml dans le dossier C:\\My Documents. Le paramètre *Force* supprime les invites confirmant que les commandes seront désactivées, ainsi que les avertissements indiquant que les données de configuration seront remplacées sur le serveur de transport Edge.
    
        New-EdgeSubscription -FileName "C:\My Documents\EdgeSubscriptionInfo.xml" -Force

2.  Copiez le fichier d’abonnement Edge créé vers un serveur de boîtes aux lettres dans le site Active Directory auquel vous abonnez le serveur de transport Edge.

3.  Sur le serveur de boîtes aux lettres, pour importer le fichier d’abonnement Edge, utilisez la syntaxe ci-après.
    
        New-EdgeSubscription -FileData ([byte[]]$(Get-Content -Path "<FileName>.xml" -Encoding Byte -ReadCount 0)) -Site <SiteName>
    
    Cet exemple importe le fichier d’abonnement Edge nommé EdgeSubscriptionInfo.xml à partir du dossier D:\\Data, et abonne le serveur de transport Edge au site Active Directory nommé « Default-First-Site-Name ».
    
        New-EdgeSubscription -FileData ([byte[]]$(Get-Content -Path "D:\Data\EdgeSubscriptionInfo.xml" -Encoding Byte -ReadCount 0)) -Site "Default-First-Site-Name"
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Vous pouvez utiliser les paramètres <em>CreateInternetSendConnector</em> ou <em>CreateInboundSendConnector</em> pour empêcher la création automatique d’un seul ou des deux connecteurs d’envoi requis. Pour plus d’informations, voir <a href="edge-subscriptions-exchange-2013-help.md">Abonnements Edge</a>.</td>
    </tr>
    </tbody>
    </table>


4.  Sur le serveur de boîtes aux lettres, exécutez la commande suivante pour démarrer la première synchronisation EdgeSync.
    
        Start-EdgeSynchronization

5.  Une fois que vous avez terminé, nous vous recommandons vivement de supprimer le fichier d’abonnement Edge à la fois du serveur de transport Edge et du serveur de boîtes aux lettres. Le fichier d’abonnement Edge contient des informations sur les informations d’identification utilisées lors du processus de communication LDAP.

