---
title: "Créez un connecteur de réception pour recevoir des courriers électroniques depuis l'Internet: Exchange 2013 Help"
TOCTitle: Créez un connecteur de réception pour recevoir des courriers électroniques depuis l'Internet
ms:assetid: 534bbd32-a0db-4d50-9579-4933b156d7b3
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ657447(v=EXCHG.150)
ms:contentKeyID: 50478206
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Créez un connecteur de réception pour recevoir des courriers électroniques depuis l'Internet

 

_**Sapplique à :**Exchange Server 2013_

_**Dernière rubrique modifiée :**2012-10-15_

Cette procédure illustre comment configurer un connecteur de réception pour recevoir des messages électroniques depuis Internet.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Dans la plupart des cas, vous n'aurez pas besoin de configurer un connecteur de réception pour recevoir des messages électroniques depuis Internet, car, pour accepter des messages électroniques depuis Internet, un connecteur de réception est implicitement créé au moment de l'installation de Exchange. Voir <a href="receive-connectors-exchange-2013-help.md">Connecteurs de réception</a> pour plus d'informations.</td>
</tr>
</tbody>
</table>


Intéressé par des scénarios où cette procédure est utilisée ? Consultez les rubriques suivantes :

  - [Configuration du flux de messagerie et de l’accès au client](configure-mail-flow-and-client-access-exchange-2013-help.md)

## Ce qu’il faut savoir avant de commencer ?

  - Durée d'exécution estimée : 15 minutes

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Connecteurs de réception » dans la rubrique [Autorisations de flux de messagerie](mail-flow-permissions-exchange-2013-help.md).

  - Voir [Déployer une nouvelle installation d’Exchange 2013](deploy-a-new-installation-of-exchange-2013-exchange-2013-help.md) si vous commencez votre installation. Après l’installation, vous pouvez utiliser la procédure présentée dans cette rubrique pour créer votre connecteur de réception.

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


## Utilisez l'EAC pour créer un connecteur de réception afin de recevoir des messages depuis Internet

1.  Dans la CCE, accédez à **Flux de messagerie** \> **Connecteurs de réception**. Cliquez sur **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter") pour créer un connecteur de réception.

2.  Dans la page **Nouveau connecteur de réception**, spécifiez un nom pour le connecteur de réception, puis sélectionnez **Transport Frontend** pour le **Rôle**. Puisque dans ce cas, vous recevez du courrier depuis Internet, nous vous recommandons de router initialement les messages vers votre ou vos serveurs Frontend.

3.  Choisissez **Internet** pour le type. Le connecteur de réception recevra le courrier provenant d'expéditeurs Internet.

4.  En ce qui concerne les **liaisons de cartes réseau**, vous pouvez observer que l'option **Toutes les IPv4 disponibles** se trouve dans la liste des **adresses IP** et que le **Port** est 25. (le protocole SMTP (Simple Mail Transfer Protocol) utilise le port 25.) Cela indique que le connecteur écoute les connexions sur toutes les adresses IP attribuées aux cartes réseau sur le serveur local.
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Si vous avez plusieurs cartes réseau, ajoutez dans cette page une adresse IP attribuée à une carte réseau spécifique sur le serveur local. Cela n'est cependant pas obligatoire.</td>
    </tr>
    </tbody>
    </table>


5.  Cliquez sur le bouton **Terminer** pour créer votre connecteur.

Une fois créé, le connecteur de réception apparaît dans la liste des connecteurs de réception. Pour voir un exemple de création d’un connecteur de réception avec une cmdlet, voir [New-ReceiveConnector](https://technet.microsoft.com/fr-fr/library/bb125139\(v=exchg.150\)).

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez créé un connecteur de réception avec succès pour recevoir des messages depuis Internet, essayez d'envoyer un message depuis une source extérieure et vérifiez qu'un de vos utilisateurs peut le recevoir. Si vous pouvez recevoir du courrier, cela signifie que la configuration a bien fonctionné.

## Pour plus d'informations

[Créer un connecteur de réception sécurisé pour recevoir le message électronique d’un partenaire](create-a-secure-receive-connector-to-receive-email-from-a-partner-exchange-2013-help.md)

[Créez un connecteur de réception pour recevoir des courriers électroniques depuis un système qui n'exécute pas Exchange](create-a-receive-connector-to-receive-email-from-a-system-not-running-exchange-exchange-2013-help.md)

