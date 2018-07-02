---
title: 'Créez un connecteur de réception pour recevoir des messages depuis un serveur Exchange interne: Exchange 2013 Help'
TOCTitle: Créez un connecteur de réception pour recevoir des messages depuis un serveur Exchange interne
ms:assetid: 546cead9-7a2d-4332-a5f6-35343d56c619
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ657448(v=EXCHG.150)
ms:contentKeyID: 50478216
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Créez un connecteur de réception pour recevoir des messages depuis un serveur Exchange interne

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2012-10-03_

Vous créez un connecteur de réception de type **Interne** lorsque vous voulez recevoir du courrier depuis un serveur Exchange. Utilisez ce type de connecteur pour contrôler le routage du courrier au sein de votre organisation : par exemple, lorsque vous voulez router du courrier depuis le service de transport d'un serveur de boîtes aux lettres vers un serveur de transport Edge ou depuis un serveur de boîtes aux lettres vers un autre.

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


## Créez un connecteur de réception pour recevoir des messages depuis un serveur Exchange interne

1.  Dans la CCE, accédez à **Flux de messagerie** \> **Connecteurs de réception**. Cliquez sur **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter") pour créer un connecteur de réception.

2.  Dans la page **Nouveau connecteur de réception**, spécifiez un nom pour le connecteur de réception, puis sélectionnez **Transport Hub** pour le **Rôle**. Dans ce cas, nous supposons que vous voulez router le courrier à l'intérieur de votre réseau et non à l'intérieur et à l'extérieur de l'organisation.

3.  Choisissez **interne** pour le type. Le connecteur est configuré avec l'authentification du serveur Exchange.

4.  Si la page Paramètres du réseau distant indique 0.0.0.0-255.255.255.255, ce qui signifie que le connecteur de réception reçoit des connexions de l’ensemble des adresses IP, cliquez sur **Supprimer**![Icône Suppression](images/Dd362328.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "Icône Suppression") pour le supprimer. Cliquez sur **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter"), ajoutez l'adresse IP du serveur depuis lequel vous voulez recevoir le courrier, par exemple 192.168.1.1, et cliquez sur **Enregistrer**.

5.  Cliquez sur **Terminer** pour créer le connecteur.

Une fois créé, le connecteur de réception apparaît dans la liste des connecteurs de réception. Pour voir un exemple de création d’un connecteur de réception avec une cmdlet, voir [New-ReceiveConnector](https://technet.microsoft.com/fr-fr/library/bb125139\(v=exchg.150\)).

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez créé un connecteur de réception avec succès pour recevoir des messages depuis un serveur interne, vérifiez que les messages envoyés depuis le serveur d'envoi voyagent correctement vers le serveur destinataire. Pour ce faire, utilisez l'environnement Exchange Management Shell pour définir le paramètre *ProtocolLoggingLevel* pour le connecteur de réception créé pour `Verbose`, au moyen de la cmdlet [Set-ReceiveConnector](https://technet.microsoft.com/fr-fr/library/bb125140\(v=exchg.150\)), et vérifiez les journaux pour garantir la bonne livraison des messages.

## Pour plus d'informations

[Créez un connecteur de réception pour recevoir des courriers électroniques depuis l'Internet](create-a-receive-connector-to-receive-email-from-the-internet-exchange-2013-help.md)

[Créer un connecteur de réception sécurisé pour recevoir le message électronique d’un partenaire](create-a-secure-receive-connector-to-receive-email-from-a-partner-exchange-2013-help.md)

