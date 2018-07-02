---
title: 'Récupération des messages mis en quarantaine dans la boîte aux lettres de mise en quarantaine du courrier indésirable: Exchange 2013 Help'
TOCTitle: Récupération des messages mis en quarantaine dans la boîte aux lettres de mise en quarantaine du courrier indésirable
ms:assetid: 7a86bfde-f868-4689-bdec-5f01e52b510d
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Aa998920(v=EXCHG.150)
ms:contentKeyID: 50478522
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Récupération des messages mis en quarantaine dans la boîte aux lettres de mise en quarantaine du courrier indésirable

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2016-12-09_

Vous pouvez utiliser Microsoft Outlook pour récupérer un message mis en quarantaine à partir de la boîte aux lettres de mise en quarantaine du courrier indésirable.

La mise en quarantaine du courrier indésirable est une fonctionnalité de l’agent de filtrage du contenu qui réduit le risque de perte de messages légitimes. Lorsqu’un message atteint le seuil de mise en quarantaine du courrier indésirable, il est consigné dans une notification d’échec de remise et déposé dans la boîte aux lettres de mise en quarantaine du courrier indésirable. Pour plus d’informations sur la fonctionnalité de mise en quarantaine du courrier indésirable, voir [Mise en quarantaine du courrier indésirable](spam-quarantine-exchange-2013-help.md).

## Ce qu’il faut savoir avant de commencer ?

  - Durée d’exécution estimée de chaque procédure : 15 minutes

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Accès à la boîte aux lettres » dans la rubrique [Autorisations de flux de messagerie](mail-flow-permissions-exchange-2013-help.md).

  - Cette procédure nécessite d’avoir configuré la boîte aux lettres de mise en quarantaine antispam. Pour plus d’informations, consultez la rubrique [Configuration d’une boîte aux lettres de mise en quarantaine du courrier indésirable](configure-a-spam-quarantine-mailbox-exchange-2013-help.md).

  - Pour accéder à la boîte aux lettres de quarantaine, vous devez configurer un profil Outlook pour cette boîte aux lettres et puis ouvrez la boîte aux lettres à l’aide d’Outlook. Pour plus d’informations sur la configuration et l’utilisation de plusieurs profils Outlook, consultez [vue d’ensemble des e-mails profils Outlook](https://go.microsoft.com/fwlink/p/?linkid=178975).

  - Pour simplifier la recherche du message que vous souhaitez récupérer, vous pouvez créer un formulaire Outlook personnalisé et modifier la vue par défaut de façon à afficher l’adresse de l’expéditeur d’origine dans la liste des messages. Pour obtenir la procédure détaillée, voir [Configurer Outlook pour afficher l’expéditeur d’origine dans la boîte aux lettres de mise en quarantaine](configure-outlook-to-show-the-original-sender-in-the-quarantine-mailbox-exchange-2013-help.md).

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

## Utiliser Outlook 2010 ou Outlook 2013 pour récupérer un message à partir de la boîte aux lettres de mise en quarantaine du courrier indésirable

1.  Ouvrez la boîte aux lettres de mise en quarantaine via Outlook 2010 ou Outlook 2013 sur un ordinateur client.

2.  Dans la vue **Messagerie**, recherchez le message que vous souhaitez récupérer dans la **Boîte de réception**, puis double-cliquez sur le message pour l’ouvrir.

3.  Dans la section **Déplacer** du ruban, cliquez sur **Actions** \> **Renvoyer ce message**.

4.  Lorsque le message s’ouvre, cliquez sur **Envoyer** pour renvoyer le message au destinataire indiqué.

## Utiliser Outlook 2007 pour publier un message à partir de la boîte aux lettres de mise en quarantaine du courrier indésirable

1.  Ouvrez la boîte aux lettres de mise en quarantaine en utilisant Outlook 2007 sur un ordinateur client.

2.  Dans la vue **Dossiers Courrier**, recherchez le message que vous souhaitez récupérer dans la **Boîte de réception**, puis double-cliquez sur le message pour l’ouvrir.

3.  Dans le groupe **Répondre** de l’onglet **Rapport**, cliquez sur **Envoyer à nouveau**.

4.  Lorsque le message s’ouvre, cliquez sur **Envoyer** pour renvoyer le message au destinataire indiqué.

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez correctement récupéré le message à partir de la boîte aux lettres de mise en quarantaine du courrier indésirable, contactez le destinataire et assurez-vous qu’il a reçu le message.

