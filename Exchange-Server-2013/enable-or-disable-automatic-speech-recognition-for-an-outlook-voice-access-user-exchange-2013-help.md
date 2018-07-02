---
title: 'Activer ou désactiver la reconnaissance vocale automatique pour un utilisateur Outlook Voice Access: Exchange 2013 Help'
TOCTitle: Activer ou désactiver la reconnaissance vocale automatique pour un utilisateur Outlook Voice Access
ms:assetid: 58f41016-e725-432b-953e-415d61e0664c
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb232062(v=EXCHG.150)
ms:contentKeyID: 50555406
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Activer ou désactiver la reconnaissance vocale automatique pour un utilisateur Outlook Voice Access

 

_**Sapplique à :** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2013-02-22_

Vous pouvez configurer la reconnaissance vocale automatique pour un utilisateur qui est activé pour la messagerie unifiée et la messagerie vocale. Lorsque la reconnaissance vocale est activée sur la boîte aux lettres d’un utilisateur d’Outlook Voice Access, celui-ci peut naviguer dans les menus de la boîte aux lettres via des commandes vocales. La reconnaissance vocale automatique est activée par défaut. Si la reconnaissance vocale est désactivée, l’utilisateur doit se servir d’entrées DTMF (numérotation en fréquences vocales), également appelées entrées à tonalité, pour naviguer dans les menus.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Vous ne pouvez pas utiliser le CAE pour configurer cette fonctionnalité. Vous devez utiliser l’environnement de ligne de commande Exchange Management Shell pour activer ou désactiver la reconnaissance vocale automatique pour un utilisateur de messagerie vocale.</td>
</tr>
</tbody>
</table>


Pour des tâches de gestion supplémentaires liés aux utilisateurs de messagerie unifiée ou vocale, voir [Gestion des paramètres de messagerie vocale d'un utilisateur](manage-voice-mail-settings-for-a-user-exchange-2013-help.md).

## Ce qu’il faut savoir avant de commencer ?

  - Durée d'exécution estimée : Moins d’une minute.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Boîtes aux lettres de messagerie unifiée » dans la rubrique [Autorisations de messagerie unifiée](unified-messaging-permissions-exchange-2013-help.md).

  - Avant d’exécuter ces procédures, vérifiez qu’un plan de numérotation de messagerie unifiée a été créé. Pour obtenir la procédure détaillée, consultez la rubrique [Créer un plan de numérotation de messagerie unifiée](create-a-um-dial-plan-exchange-2013-help.md).

  - Avant d’effectuer ces procédures, vérifiez qu’une stratégie de boîte aux lettres de messagerie unifiée a été créée. Pour obtenir la procédure détaillée, voir [Créer une stratégie de boîte aux lettres de messagerie unifiée](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Avant d’effectuer ces procédures, vérifiez que la boîte aux lettres de l’utilisateur a été activée pour la messagerie unifiée. Pour obtenir la procédure détaillée, consultez la rubrique [Activation de la messagerie vocale pour un utilisateur](enable-a-user-for-voice-mail-exchange-2013-help.md).

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


## Activation ou désactivation de la reconnaissance vocale automatique pour un utilisateur à extension messagerie unifiée à l’aide de l’environnement de ligne de commande Exchange Management Shell

Cet exemple montre comment activer la reconnaissance vocale automatique pour un utilisateur à extension messagerie unifiée nommé `tonysmith`.

    Set-UMMailbox -Identity tonysmith@contoso.com -AutomaticSpeechRecognitionEnabled $true

Cet exemple montre comment désactiver la reconnaissance vocale automatique pour un utilisateur à extension messagerie unifiée nommé `tonysmith`.

    Set-UMMailbox -Identity tonysmith@contoso.com -AutomaticSpeechRecognitionEnabled $false

