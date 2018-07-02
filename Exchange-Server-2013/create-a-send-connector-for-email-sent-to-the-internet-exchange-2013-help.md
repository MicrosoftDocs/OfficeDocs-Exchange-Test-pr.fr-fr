---
title: 'Créer un connecteur d’envoi pour les messages électroniques envoyés vers Internet: Exchange 2013 Help'
TOCTitle: Créer un connecteur d’envoi pour les messages électroniques envoyés vers Internet
ms:assetid: 6deaefa8-1152-40d9-b1ba-9c19bdf8a928
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ657457(v=EXCHG.150)
ms:contentKeyID: 50478399
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Créer un connecteur d’envoi pour les messages électroniques envoyés vers Internet

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2015-01-23_

Par défaut, Microsoft Exchange Server 2013 ne vous permet pas d’envoyer des messages électroniques en dehors de votre domaine. Pour envoyer des messages électroniques en dehors de votre domaine, vous devez créer un connecteur d’envoi. La figure suivante illustre le flux de messagerie lorsque vous créez un connecteur d’envoi pour envoyer les messages électroniques vers Internet.

![connector\_send\_onprem\_internet](images/JJ657457.e8963e4f-7dce-461f-bbcf-660278cefa35(EXCHG.150).gif "connector_send_onprem_internet")

Intéressé par des scénarios où cette procédure est utilisée ? Consultez les rubriques suivantes :

  - [Configuration du flux de messagerie et de l’accès au client](configure-mail-flow-and-client-access-exchange-2013-help.md)

## Ce qu’il faut savoir avant de commencer ?

  - Durée d'exécution estimée : 15 minutes

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l’entrée « Connecteurs d’envoi » dans la rubrique [Autorisations de flux de messagerie](mail-flow-permissions-exchange-2013-help.md).

  - Voir [Déployer une nouvelle installation d’Exchange 2013](deploy-a-new-installation-of-exchange-2013-exchange-2013-help.md) si vous commencez votre installation. À l’issue de l’installation, vous pouvez utiliser les étapes de cette rubrique pour créer votre connecteur d’envoi.

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

## Utiliser le Centre d’administration Exchange (EAC) pour créer un connecteur d’envoi pour les messages électroniques envoyés vers Internet

1.  Dans le Centre d’administration Exchange, accédez à **Flux de messagerie**\>**Connecteurs d’envoi**, puis cliquez sur **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter").

2.  Dans l’Assistant **Nouveau connecteur d’envoi**, spécifiez le nom du connecteur d’envoi, puis sélectionnez **Internet** en tant que **Type**. Cliquez sur **Suivant**.

3.  Vérifiez si **Enregistrement MX associé au domaine du destinataire** est sélectionné, ce qui spécifie que ce connecteur utilise le système DNS (Domain Name System) pour acheminer les messages. Cliquez sur **Suivant**.

4.  Sous **Espace d’adressage**, cliquez sur **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter"). Dans la fenêtre **Ajouter un domaine**, vérifiez que SMTP apparaît dans la liste **Type**. Pour **Nom de domaine complet (FQDN)**, entrez \* pour indiquer que ce connecteur d’envoi s’applique aux messages destinés à n’importe quel domaine. Cliquez sur **Enregistrer**.

5.  Assurez-vous que la case à cocher **Connecteur d’envoi délimité** est désactivée, puis cliquez sur **Suivant**.

6.  Pour **Serveur source**, cliquez sur **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter"). Dans la fenêtre **Sélectionner un serveur**, sélectionnez un serveur de boîtes aux lettres qui sera utilisé pour envoyer des messages à l’Internet via le serveur d’accès au client puis cliquez sur **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter"). Après avoir sélectionné le serveur, cliquez sur **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter"). Cliquez sur **OK**.

7.  Cliquez sur **Terminer**.

Une fois créé, le connecteur d’envoi apparaît dans la liste des connecteurs d’envoi.

## Utiliser l’environnement de ligne de commande Exchange Management Shell pour router les messages électroniques via le serveur d’accès au client

Dans Exchange 2013, vous pouvez utiliser le paramètre *FrontendProxyEnabled* de la cmdlet **Set-SendConnector** pour router les messages sortants via le serveur d’accès au client. Ce paramètre n’est pas défini sur `$true` par défaut, mais il peut dans de nombreux cas consolider et simplifier le flux de messagerie, notamment si vous utilisez un environnement comportant un grand nombre de serveurs de messagerie.

Cet exemple définit le paramètre *FrontendProxyEnabled* sur `$true` sur un connecteur d’envoi.

    Set-SendConnector "Contoso.com Send Connector" -FrontendProxyEnabled $true

## Comment savoir si cela a fonctionné ?

Afin de contrôler que vous avez correctement créé un connecteur d’envoi pour les messages électroniques envoyés vers Internet, envoyez un message depuis l’un de vos utilisateurs vers un destinataire externe, puis vérifiez que le message est bien arrivé.

## Pour plus d'informations

[Connecteurs d'envoi](send-connectors-exchange-2013-help.md)

[Créer un connecteur d’envoi pour router le courrier sortant via un hôte actif](create-a-send-connector-to-route-outbound-email-through-a-smart-host-exchange-2013-help.md)

