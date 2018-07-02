---
title: "Empêcher les appelants sans ID d'appelant de laisser un message vocal: Exchange 2013 Help"
TOCTitle: Empêcher les appelants sans ID d'appelant de laisser un message vocal
ms:assetid: dd5dad32-2f69-4bf4-8ff0-545c413d395a
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ673571(v=EXCHG.150)
ms:contentKeyID: 50479387
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Empêcher les appelants sans ID d'appelant de laisser un message vocal

 

_**Sapplique à :**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :**2013-02-22_

Vous pouvez également autoriser les utilisateurs à extension messagerie unifiée de recevoir des messages vocaux d'appelants anonymes ou les empêcher d'envoyer ce type de message. Par défaut, lorsque les utilisateurs sont activés pour la messagerie unifiée et la messagerie vocale, ils peuvent recevoir des appels anonymes sans informations d'ID d'appelant.

Dans la plupart des cas, les appels reçus par les serveurs Exchange contiennent un ID d'appelant permettant de déterminer la source de l'appel entrant. Toutefois, il peut arriver que les appels entrants n'incluent pas d'informations d'ID d'appelant pour les raisons suivantes :

  - L'équipement téléphonique de votre organisation est configuré pour ne pas inclure les informations d'ID d'appelant.

  - L'appel entrant provient d'un téléphone mobile ou externe.

  - L'appelant a désactivé l'ID de l'appelant sur son téléphone.

Étant donné que le paramètre *AnonymousCallersCanLeaveMessages* est activé par défaut, un utilisateur à extension messagerie unifiée peut recevoir un message vocal même si les informations sur l'ID d'appelant ne sont pas fournies. Si l'option *AnonymousCallersCanLeaveMessages* est désactivée et que l'utilisateur à extension messagerie unifiée reçoit un appel ne contenant pas d'ID d'appelant, l'appel est considéré comme anonyme et l'utilisateur à extension messagerie unifiée ne reçoit pas de message vocal.

Pour découvrir d'autres tâches de gestion relatives aux utilisateurs à extension messagerie vocale, consultez la rubrique [Voix des procédures de l'utilisateur à extension messagerie](voice-mail-enabled-user-procedures-exchange-2013-help.md).

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : 2 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l'entrée « Boîtes aux lettres de messagerie unifiée » dans la rubrique [Autorisations de messagerie unifiée](unified-messaging-permissions-exchange-2013-help.md).

  - Avant d'effectuer cette procédure, vérifiez qu'un plan de numérotation de messagerie unifiée a été créé. Pour obtenir la procédure détaillée, consultez la rubrique [Créer un plan de numérotation de messagerie unifiée](create-a-um-dial-plan-exchange-2013-help.md).

  - Avant d'effectuer cette procédure, vérifiez qu'une stratégie de boîte aux lettres de messagerie unifiée a été créée. Pour obtenir la procédure détaillée, consultez la rubrique [Créer une stratégie de boîte aux lettres de messagerie unifiée](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Avant d'effectuer cette procédure, vérifiez que la boîte aux lettres de l'utilisateur est à extension messagerie unifiée. Pour obtenir la procédure détaillée, consultez la rubrique [Activation de la messagerie vocale pour un utilisateur](enable-a-user-for-voice-mail-exchange-2013-help.md).

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


## Utilisation de l'environnement de ligne de commande Exchange Management Shell pour empêcher la réception de messages d'appelants anonymes

Cet exemple empêche l'utilisateur à extension messagerie unifiée tonysmith@contoso.com de recevoir des messages vocaux d'appels qui ne contiennent pas d'informations d'ID d'appelant.

    Set-UMMailbox -Identity tonysmith@contoso.com -AnonymousCallersCanLeaveMessages $false

