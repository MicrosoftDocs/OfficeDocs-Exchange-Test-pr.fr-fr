---
title: 'Créer un connecteur de réception sécurisé pour recevoir le message électronique d’un partenaire: Exchange 2013 Help'
TOCTitle: Créer un connecteur de réception sécurisé pour recevoir le message électronique d’un partenaire
ms:assetid: 06aa692c-7940-4a14-a722-058c47440f85
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ673037(v=EXCHG.150)
ms:contentKeyID: 50477461
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Créer un connecteur de réception sécurisé pour recevoir le message électronique d’un partenaire

 

_**Sapplique à :**Exchange Server 2013_

_**Dernière rubrique modifiée :**2012-10-03_

Cette procédure indique comment configurer un connecteur de réception pour recevoir des courriers électroniques sécurisés d’un partenaire. Utilisez cette procédure lorsque vous devez chiffrer les messages que vous échangez avec un partenaire approuvé. Le connecteur est configuré pour accepter uniquement les connexions des serveurs qui s’authentifient avec le protocole TLS (Transport Layer Security).

Intéressé par des scénarios où cette procédure est utilisée ? Consultez les rubriques suivantes :

  - [Configuration du flux de messagerie et de l’accès au client](configure-mail-flow-and-client-access-exchange-2013-help.md)

## Ce qu’il faut savoir avant de commencer

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


## Utiliser le Centre d’administration Exchange pour créer un connecteur en vue de recevoir des messages sécurisés d’un partenaire

1.  Dans la CCE, accédez à **Flux de messagerie** \> **Connecteurs de réception**. Cliquez sur **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter") pour créer un connecteur de réception.

2.  Sur la page **Nouveau connecteur de réception**, spécifiez le nom du connecteur de réception et sélectionnez le **RôleTransport frontal**. Dans ce cas, comme vous recevez les messages envoyés par un partenaire, nous vous recommandons de les acheminer initialement vers votre serveur frontal pour simplifier et consolider votre flux de messagerie.

3.  Choisissez le type **Partenaire**. Le connecteur de réception recevra les messages envoyés par un tiers approuvé.

4.  Pour les **Liaisons de carte réseau**, vous remarquerez que l’option **Toutes les adresses IPV4 disponibles** figure dans la liste **Adresses IP** et que le **Port** est 25. (port utilisé par le protocole SMTP.) Cela indique que le connecteur écoute les connexions sur toutes les adresses IP attribuées aux cartes réseau sur le serveur local. Cliquez sur **Suivant**.

5.  Si la page Paramètres du réseau distant indique 0.0.0.0-255.255.255.255, ce qui signifie que le connecteur de réception reçoit des connexions de l’ensemble des adresses IP, cliquez sur **Supprimer**![Icône Suppression](images/Dd362328.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "Icône Suppression") pour le supprimer. Cliquez sur **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter"), ajoutez l’adresse IP du serveur de votre partenaire, puis cliquez sur **Enregistrer**.
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Vous pouvez également spécifier une plage d’adresses IP avec une notation CIDR, comme 64.4.6.100/24.</td>
    </tr>
    </tbody>
    </table>


6.  Cliquez sur **Terminer** pour créer le connecteur.

Une fois créé, le connecteur de réception apparaît dans la liste des connecteurs de réception. Pour voir un exemple de création d’un connecteur de réception avec une cmdlet, voir [New-ReceiveConnector](https://technet.microsoft.com/fr-fr/library/bb125139\(v=exchg.150\)).

## Comment savoir si cela a fonctionné ?

Pour vous assurer que le connecteur de réception a été correctement créé et que vous pouvez recevoir des messages d’un partenaire, faites un test en demandant au partenaire d’envoyer un message à l’un des vos utilisateurs et vérifiez qu’il a bien été reçu. Si vous pouvez recevoir des messages chiffrés (vérifiez dans l’en-tête du message que TLS est bien utilisé), vous savez que la configuration est correcte.

## Pour plus d'informations

[Connecteurs de réception](receive-connectors-exchange-2013-help.md)

