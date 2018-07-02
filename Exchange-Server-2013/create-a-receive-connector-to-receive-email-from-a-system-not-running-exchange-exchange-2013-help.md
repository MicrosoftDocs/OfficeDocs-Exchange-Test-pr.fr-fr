---
title: "Créez un connecteur de réception pour recevoir des courriers électroniques depuis un système qui n'exécute pas Exchange: Exchange 2013 Help"
TOCTitle: Créez un connecteur de réception pour recevoir des courriers électroniques depuis un système qui n'exécute pas Exchange
ms:assetid: 85f0864a-6502-49db-8804-16755a7292b4
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ657467(v=EXCHG.150)
ms:contentKeyID: 50478614
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Créez un connecteur de réception pour recevoir des courriers électroniques depuis un système qui n'exécute pas Exchange

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2012-10-03_

Il peut exister une situation dans laquelle vous voulez recevoir des messages provenant d’un système n’exécutant pas Exchange. Par exemple, vous avez un dispositif Network Appliance qui effectue des contrôles de stratégies et vous acheminez des messages vers votre serveur Exchange. Dans ce cas, nous supposons que le dispositif utilise le protocole SMTP. Sinon, vous devez utiliser un connecteur étranger ou un connecteur d’agent de remise.

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


## Utilisez l’EAC pour créer un connecteur de réception pour recevoir des messages d’un dispositif de messagerie

1.  Dans la CCE, accédez à **Flux de messagerie** \> **Connecteurs de réception**. Cliquez sur **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter") pour créer un connecteur de réception.

2.  Sur la page **Nouveau connecteur de réception**, donnez un nom pour le connecteur de réception, puis sélectionnez **Transport Hub** pour le **Rôle**. Dans ce cas, vous voulez que votre serveur de boîte aux lettre exécute le service Transport pour recevoir des messages du dispositif.

3.  Sélectionnez le type **Personnalisé**, puisque le connecteur de réception doit recevoir du courrier d’un dispositif qui n’exécute pas Microsoft Exchange Server 2013.

4.  Pour la **Liaisons de carte réseau**, observez que **Toutes les IPv4 disponibles** est répertorié dans la liste **Adresses IP**. Cliquez sur **Suivant**.

5.  Pour **Paramètres du réseau à distance**, cliquez sur **Supprimer**![Icône Suppression](images/Dd362328.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "Icône Suppression") pour supprimer **0.0.0.0-255.255.255.255** de la liste des **adresses IP**, puisque vous souhaitez indiquer que le connecteur accepte du courrier provenant d’un dispositif spécifique. Cliquez sur **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter") pour ajouter une nouvelle adresse IP, puis dans la fenêtre **Ajouter une adresse IP**, ajoutez l’adresse IP de votre dispositif. Cliquez sur **Enregistrer**.

6.  Cliquez sur le bouton **Terminer** pour créer votre connecteur.

Une fois créé, le connecteur de réception apparaît dans la liste des connecteurs de réception. Pour voir un exemple de création d’un connecteur de réception avec une cmdlet, voir [New-ReceiveConnector](https://technet.microsoft.com/fr-fr/library/bb125139\(v=exchg.150\)).

## Comment savoir si cela a fonctionné ?

Pour vérifier que la création d’un connecteur de réception permettant de recevoir du courrier d’un dispositif de messagerie s’est correctement effectuée, faites un test de réception de courrier. Si vous pouvez recevoir du courrier, cela signifie que la configuration a bien fonctionné.

## Pour plus d'informations

[Créez un connecteur de réception pour recevoir des courriers électroniques depuis l'Internet](create-a-receive-connector-to-receive-email-from-the-internet-exchange-2013-help.md)

