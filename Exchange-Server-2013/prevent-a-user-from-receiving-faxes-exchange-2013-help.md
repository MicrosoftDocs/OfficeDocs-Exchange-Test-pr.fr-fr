---
title: 'Empêcher un utilisateur de recevoir des télécopies: Exchange 2013 Help'
TOCTitle: Empêcher un utilisateur de recevoir des télécopies
ms:assetid: b5d022b9-043a-4324-87fb-074d5e2c2ca3
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb201722(v=EXCHG.150)
ms:contentKeyID: 52057140
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Empêcher un utilisateur de recevoir des télécopies

 

_**Sapplique à :**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :**2016-12-09_

Empêcher un utilisateur de messagerie unifiée (MU) de recevoir des télécopies. Découvrez comment modifier les paramètres de télécopie pour les utilisateurs de MU nouveaux et existants.

Par défaut, lorsque vous activez un utilisateur pour la messagerie unifiée, ils seront en mesure de recevoir des télécopies si vous activez l’envoi de télécopies et configurez les URI d’un partenaire de télécopie sur la stratégie de boîte aux lettres de messagerie UNIFIÉE qui est liée à l’utilisateur. Envoi de télécopies peut être activé ou désactivé sur MU composer des plans, des stratégies de boîte aux lettres de MU ou boîte aux lettres de l’utilisateur activé pour la MU.

Par défaut, la boîte aux lettres utilisateur et le plan de numérotation associé à l'utilisateur autorisent les télécopies entrantes. Cependant, pour qu'un utilisateur reçoive les télécopies, vous devez d'abord activer les télécopies entrantes sur la stratégie de boîte aux lettres de messagerie unifiée associée à l'utilisateur à extension messagerie unifiée, puis entrer l'URI du partenaire de télécopie.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Vous pouvez utiliser la FAC pour configurer les paramètres de télécopie sur une stratégie de boîte aux lettres de messagerie unifiée. Toutefois, vous devez utiliser l’interpréteur de commandes pour configurer les paramètres de télécopie sur les plans de numérotation ou pour des utilisateurs individuels.</td>
</tr>
</tbody>
</table>


Pour plus d’informations sur les partenaires de télécopie, consultez [Microsoft PinPoint pour les partenaires de télécopie](https://go.microsoft.com/fwlink/?linkid=190238).

Pour découvrir d'autres tâches de gestion relatives à la télécopie, consultez la rubrique [Procédures d'envoi de télécopie](faxing-procedures-exchange-2013-help.md).

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : 2 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Stratégies de boîte aux lettres de messagerie unifiée » dans la rubrique [Autorisations de messagerie unifiée](unified-messaging-permissions-exchange-2013-help.md).

  - Avant d'exécuter ces procédures, vérifiez qu'un plan de numérotation de messagerie unifiée a été créé. Pour obtenir la procédure détaillée, consultez la rubrique [Créer un plan de numérotation de messagerie unifiée](create-a-um-dial-plan-exchange-2013-help.md).

  - Avant d'effectuer ces procédures, vérifiez qu'une stratégie de boîte aux lettres de messagerie unifiée a été créée. Pour obtenir la procédure détaillée, consultez la rubrique [Créer une stratégie de boîte aux lettres de messagerie unifiée](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Avant d'effectuer ces procédures, vérifiez que la messagerie unifiée est activée pour l'utilisateur. Pour obtenir la procédure détaillée, consultez la rubrique [Activation de la messagerie vocale pour un utilisateur](enable-a-user-for-voice-mail-exchange-2013-help.md).

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


## Utiliser l’interpréteur de commandes pour empêcher un utilisateur de messagerie UNIFIÉE à partir de la réception de télécopies

Cet exemple empêche l'utilisateur à extension messagerie unifiée Tony de recevoir des télécopies dans sa boîte aux lettres.

    Set-UMMailbox -Identity tony@contoso.com -FaxEnabled $false

