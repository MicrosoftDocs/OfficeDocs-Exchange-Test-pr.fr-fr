---
title: 'Désactiver les fonctionnalités sélectionnées pour les utilisateurs Outlook Voice Access: Exchange 2013 Help'
TOCTitle: Désactiver les fonctionnalités sélectionnées pour les utilisateurs Outlook Voice Access
ms:assetid: 37421edf-af60-4ca9-9e8b-262b8b851607
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Gg602126(v=EXCHG.150)
ms:contentKeyID: 50555371
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Désactiver les fonctionnalités sélectionnées pour les utilisateurs Outlook Voice Access

 

_**Sapplique à :** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2013-02-22_

Outlook Voice Access contient deux interfaces : l'interface utilisateur téléphonique et l'interface utilisateur vocale. Par défaut, lorsque les utilisateurs se connectent à Outlook Voice Access, ils peuvent accéder à leur calendrier, leur messagerie électronique ainsi qu'à leurs contacts personnels, et effectuer des recherches dans le répertoire. Vous pouvez utiliser l'environnement de ligne de commande Exchange Management Shell pour interdire aux utilisateurs l'accès à une ou plusieurs de ces fonctionnalités quand ils utilisent Outlook Voice Access pour accéder à leur boîte aux lettres. Lorsque vous modifiez les fonctionnalités Outlook Voice Access sur une stratégie de boîte aux lettres de messagerie unifiée, vos modifications affectent tous les utilisateurs qui sont associés à cette stratégie.

Vous pouvez désactiver l'accès utilisateur aux fonctionnalités Outlook Voice Access suivantes sur une stratégie de boîte aux lettres de messagerie unifiée :

  - Calendrier

  - Répertoire

  - Email

  - Contacts personnels

Pour d'autres tâches de gestion relatives aux stratégies de boîte aux lettres de messagerie unifiée, consultez la rubrique [Procédures de stratégie de boîte aux lettres de messagerie unifiée](um-mailbox-policy-procedures-exchange-2013-help.md).

Vous pouvez également utiliser l'environnement de ligne de commande Exchange Management Shell pour désactiver les fonctionnalités Outlook Voice Access sur la boîte aux lettres d'un utilisateur à extension messagerie spécifique. Lors de cette opération, les fonctionnalités sont uniquement désactivées pour cet utilisateur. Même s'il est impossible de désactiver toutes les fonctionnalités d'Outlook Voice Access disponibles sur une stratégie de boîte aux lettres de messagerie unifiée pour un utilisateur unique, vous pouvez néanmoins désactiver l'accès à son calendrier et sa messagerie.

Pour d'autres tâches de gestion relatives aux serveurs de boîtes aux lettres de messagerie unifiée, consultez la rubrique [Messagerie vocale pour les utilisateurs](voice-mail-for-users-exchange-2013-help.md).

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>L'environnement de ligne de commande Exchange Management Shell permet uniquement de modifier les fonctionnalités d'Outlook Voice Access pour les utilisateurs de messagerie unifiée sur une stratégie de boîte aux lettres de messagerie unifiée ou sur la boîte aux lettres d'un utilisateur à extension messagerie spécifique.</td>
</tr>
</tbody>
</table>


## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée de chaque procédure : 5 minutes.

  - Les procédures décrites dans cette rubrique requièrent des autorisations spécifiques. Consultez chaque procédure pour savoir quelles autorisations sont nécessaires.

  - Avant d'exécuter ces procédures, vérifiez qu'un plan de numérotation de messagerie unifiée a été créé. Pour obtenir la procédure détaillée, consultez la rubrique [Créer un plan de numérotation de messagerie unifiée](create-a-um-dial-plan-exchange-2013-help.md).

  - Avant d'effectuer ces procédures, vérifiez qu'une stratégie de boîte aux lettres de messagerie unifiée a été créée. Pour obtenir la procédure détaillée, consultez la rubrique [Créer une stratégie de boîte aux lettres de messagerie unifiée](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Avant d'effectuer ces procédures, vérifiez qu'un utilisateur a été activé pour la messagerie unifiée. Pour obtenir la procédure détaillée, consultez la rubrique [Activation de la messagerie vocale pour un utilisateur](enable-a-user-for-voice-mail-exchange-2013-help.md).

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

## Désactiver les fonctionnalités Outlook Voice Access sélectionnées pour les utilisateurs de messagerie unifiée sur une stratégie de boîte aux lettres de messagerie unifiée via l'environnement de ligne de commande

Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l'entrée « Stratégies de boîte aux lettres de messagerie unifiée » dans la rubrique [Autorisations de messagerie unifiée](unified-messaging-permissions-exchange-2013-help.md).

Cet exemple empêche les utilisateurs associés à une stratégie de boîte aux lettres de messagerie unifiée nommée `MyUMMailboxPolicy` d'accéder à leur calendrier quand ils se connectent à Outlook Voice Access.

    Set-UMMailboxPolicy -id MyUMMailboxPolicy -AllowTUIAccessToCalendar $false

Cet exemple empêche les utilisateurs associés à une stratégie de boîte aux lettres de messagerie unifiée nommée `MyUMMailboxPolicy` d'accéder au répertoire quand ls se connectent à Outlook Voice Access.

    Set-UMMailboxPolicy -id MyUMMailboxPolicy -AllowTUIAccessToDirectory $false

Cet exemple empêche les utilisateurs associés à une stratégie de boîte aux lettres de messagerie unifiée nommée `MyUMMailboxPolicy` d'accéder au répertoire quand ils se connectent à Outlook Voice Access.

    Set-UMMailboxPolicy -id MyUMMailboxPolicy -AllowTUIAccessToEmail -$false

Cet exemple empêche les utilisateurs associés à une stratégie de boîte aux lettres de messagerie unifiée nommée `MyUMMailboxPolicy` d'accéder aux contacts personnels lorsqu'ils se connectent à Outlook Voice Access.

    Set-UMMailboxPolicy -id MyUMMailboxPolicy -AllowTUIAccessToPersonalContacts $false

## Désactiver les fonctionnalités Outlook Voice Access sélectionnées sur la boîte aux lettres d'un utilisateur de messagerie unifiée spécifique

Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Boîtes aux lettres de messagerie unifiée » dans la rubrique [Autorisations de messagerie unifiée](unified-messaging-permissions-exchange-2013-help.md).

Cet exemple permet de désactiver l'accès au calendrier de la boîte aux lettres de messagerie unifiée nommée tony@contoso.com lorsque l'utilisateur se connecte à Outlook Voice Access.

    Set-UMMailbox -id tony@contoso.com -TUIAccessToCalendarEnabled $false

Cet exemple montre comment désactiver l'accès à la messagerie de la boîte aux lettres de messagerie unifiée nommée tony@contoso.com lorsque l'utilisateur se connecte à Outlook Voice Access.

    Set-UMMailbox -id tony@contoso.com -TUIAccessToEmailEnabled $false

