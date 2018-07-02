---
title: 'Définitions des fonctionnalités de boîte aux lettres pour des utilisateurs d’Outlook Voice Access: Exchange 2013 Help'
TOCTitle: Définitions des fonctionnalités de boîte aux lettres pour des utilisateurs d’Outlook Voice Access
ms:assetid: 10960bf0-65cf-4d0b-bae5-d203c53662db
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Aa996307(v=EXCHG.150)
ms:contentKeyID: 50555347
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Définitions des fonctionnalités de boîte aux lettres pour des utilisateurs d’Outlook Voice Access

 

_**Sapplique à :** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2013-02-22_

Outlook Voice Access contient deux interfaces : une interface utilisateur de téléphonie (TUI) et une interface utilisateur vocale (VUI). Vous pouvez configurer les paramètres de l'interface utilisateur de téléphonie à extension messagerie quand l'utilisateur accède à une boîte aux lettres à l'aide du système de messagerie unifiée d'Exchange 2013. Lorsque vous modifiez les paramètres de l'interface utilisateur téléphone à extension messagerie sur une stratégie de boîte aux lettres de messagerie unifiée. Les modifications affectent tous les utilisateurs qui sont associés à la stratégie de boîte aux lettres de messagerie unifiée. Vous pouvez modifier les paramètres d'interface utilisateur de téléphonie suivants sur une stratégie de boîte aux lettres de messagerie unifiée :

  - Accès sans code confidentiel à la messagerie vocale

  - Réponses vocales à d'autres messages

  - Accès TUI à leur calendrier

  - Accès TUI au répertoire

  - Accès TUI à leur messagerie

  - Accès TUI à leurs contacts personnels

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Vous pouvez uniquement utiliser l'environnement de ligne de commande Exchange Management Shell pour modifier les paramètres TUI d'Outlook Voice Access pour les utilisateurs à extension messagerie unifiée.</td>
</tr>
</tbody>
</table>


Pour les autres tâches de gestion relatives aux stratégies de boîte aux lettres de messagerie unifiée, consultez la rubrique [Procédures de stratégie de boîte aux lettres de messagerie unifiée](um-mailbox-policy-procedures-exchange-2013-help.md).

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : 5 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Stratégies de boîte aux lettres de messagerie unifiée » dans la rubrique [Autorisations de messagerie unifiée](unified-messaging-permissions-exchange-2013-help.md).

  - Avant d'effectuer cette procédure, vérifiez qu'un plan de numérotation de messagerie unifiée a été créé. Pour obtenir la procédure détaillée, consultez la rubrique [Créer un plan de numérotation de messagerie unifiée](create-a-um-dial-plan-exchange-2013-help.md).

  - Avant d'effectuer cette procédure, vérifiez qu'une stratégie de boîte aux lettres de messagerie unifiée a été créée. Pour obtenir la procédure détaillée, consultez la rubrique [Créer une stratégie de boîte aux lettres de messagerie unifiée](create-a-um-mailbox-policy-exchange-2013-help.md).

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


## Utiliser l'environnement de ligne de commande Exchange Management Shell pour modifier les paramètres de TUI sur une stratégie de boîte aux lettres de messagerie unifiée

Cet exemple montre comment définir les paramètres TUI sur une stratégie de boîte aux lettres de messagerie unifiée nommée `MyUMMailboxPolicy`.

    Set-UMMailbox -identity MyUMMailboxPolicy -AllowSubscriberAccess $true -AllowTUIAccessToCalendar $false -AllowTUIAccessToDirectory $false -AllowTUIAccessToEmail -$true -AllowTUIAccessToPersonalContacts $true

