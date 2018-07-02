﻿---
title: 'Autoriser les messages en attente indicateur (MWI) sur une passerelle IP de messagerie unifiée: Exchange 2013 Help'
TOCTitle: Autoriser les messages en attente indicateur (MWI) sur une passerelle IP de messagerie unifiée
ms:assetid: 5667e37c-48c6-4659-9dc9-94b1dd8ba232
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dd297995(v=EXCHG.150)
ms:contentKeyID: 50478227
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Autoriser les messages en attente indicateur (MWI) sur une passerelle IP de messagerie unifiée

 

_**Sapplique à :**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :**2013-02-23_

Vous pouvez autoriser ou empêcher les notifications de messagerie vocale auprès des utilisateurs pour les appels reçus par une passerelle IP de messagerie unifiée. Si vous activez ce paramètre, la passerelle IP de messagerie unifiée peut recevoir et envoyer des messages SIP NOTIFY pour les utilisateurs. L'indicateur de message en attente est activé par défaut. Il autorise l'envoi de notifications de message en attente aux utilisateurs, mais vous pouvez le désactiver en fonction de vos besoins.

Un indicateur de message en attente avertit un utilisateur en cas de nouveau message vocal ou en cas de message vocal non écouté. Il s'affiche dans la boîte de réception des clients tels qu'Outlook et Outlook Web App. Il peut aussi s'agir d'un message texte (SMS) envoyé à un téléphone mobile enregistré, d'un appel sortant effectué à partir d'un serveur Exchange vers un numéro configuré pour lire de nouveaux messages ou d'une lampe allumée sur le téléphone de bureau d'un utilisateur.

<table>
<thead>
<tr class="header">
<th><img src="images/Bb125224.tip(EXCHG.150).gif" title="Conseil" alt="Conseil" />Conseil :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Les notifications des indicateurs de message en attente peuvent aussi être activées et désactivées sur une stratégie de boîte aux lettres de messagerie unifiée pour un groupe d'utilisateurs.</td>
</tr>
</tbody>
</table>


Pour les autres tâches de gestion relatives aux passerelles IP de messagerie unifiée, consultez la rubrique [Procédures de passerelle IP de messagerie unifiée](um-ip-gateway-procedures-exchange-2013-help.md).

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : moins d'une minute.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l'entrée « Passerelles IP de messagerie unifiée » dans la rubrique [Autorisations de messagerie unifiée](unified-messaging-permissions-exchange-2013-help.md).

  - Avant d'exécuter ces procédures, vérifiez qu'un plan de numérotation de messagerie unifiée a été créé. Pour obtenir la procédure détaillée, consultez la rubrique [Créer un plan de numérotation de messagerie unifiée](create-a-um-dial-plan-exchange-2013-help.md).

  - Avant d'exécuter ces procédures, vérifiez qu'une passerelle IP de messagerie unifiée a été créée. Pour obtenir la procédure détaillée, consultez la rubrique [Créer une passerelle IP de messagerie unifiée](create-a-um-ip-gateway-exchange-2013-help.md).

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


## Que souhaitez-vous faire ?

## Utiliser le Centre d'administration Exchange (CAE) pour autoriser l'indicateur d'attente des messages

1.  Dans le CAE, accédez à **Messagerie unifiée** \> **Passerelles IP de messagerie unifiée**, sélectionnez la passerelle IP de messagerie unifiée à modifier, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

2.  Dans la page **Passerelle IP de messagerie unifiée**, cochez la case en regard de **Autoriser l'indicateur d'attente des messages**.

3.  Cliquez sur **Enregistrer**.

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour autoriser l'indicateur d'attente des messages

Cet exemple autorise l'affichage de l'indicateur de message en attente pour les utilisateurs associés à la passerelle IP de messagerie unifiée nommée `MyUMIPGateway` avec pour adresse IP 10.10.10.1.

    Set-UMIPGateway -Identity MyUMIPGateway -Address 10.10.10.1 -MessageWaitingIndicatorAllowed $true

