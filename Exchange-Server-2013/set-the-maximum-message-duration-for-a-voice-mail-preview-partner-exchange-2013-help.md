﻿---
title: "Définir la durée maximale des messages pour un partenaire de l'aperçu de messagerie vocale: Exchange 2013 Help"
TOCTitle: Définir la durée maximale des messages pour un partenaire de l'aperçu de messagerie vocale
ms:assetid: 18f928ff-f4cc-4eed-a466-de13388780b3
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Ff630912(v=EXCHG.150)
ms:contentKeyID: 51407162
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Définir la durée maximale des messages pour un partenaire de l'aperçu de messagerie vocale

 

_**Sapplique à :**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :**2013-02-13_

Vous pouvez définir la durée maximale d'un message pour un partenaire d'aperçu de messagerie vocale dans une stratégie de boîte aux lettres de messagerie unifiée. Une fois que vous avez défini la durée maximale du message, le paramètre s'applique à tous les utilisateurs à extension messagerie unifiée associés à cette stratégie de boîte aux lettres.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Vous devez utiliser l'environnement de ligne de commande Exchange Management Shell pour définir la durée maximale d'un message à un partenaire d'aperçu de messagerie vocale.</td>
</tr>
</tbody>
</table>


Pour plus d'informations sur le programme de partenariat d'aperçu de messagerie vocale, consultez la rubrique [Gestionnaire de l’aperçu de messagerie vocale](voice-mail-preview-advisor-exchange-2013-help.md).

Pour les autres tâches de gestion relatives à l'aperçu de messagerie vocale, consultez la rubrique [Procédures d'aperçu de messagerie vocale](voice-mail-preview-procedures-exchange-2013-help.md).

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : 1 minute.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l'entrée « Stratégies de boîte aux lettres de messagerie unifiée » dans la rubrique [Autorisations de messagerie unifiée](unified-messaging-permissions-exchange-2013-help.md).

  - Avant d'exécuter ces procédures, vérifiez qu'un plan de numérotation de messagerie unifiée a été créé. Pour obtenir la procédure détaillée, consultez la rubrique [Créer un plan de numérotation de messagerie unifiée](create-a-um-dial-plan-exchange-2013-help.md).

  - Avant d'exécuter ces procédures, vérifiez qu'un plan de numérotation de messagerie unifiée a été créé. Pour obtenir la procédure détaillée, consultez la rubrique [Créer une stratégie de boîte aux lettres de messagerie unifiée](create-a-um-mailbox-policy-exchange-2013-help.md).

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


## Utiliser l'environnement de ligne de commande Exchange Management Shell pour définir la durée maximale d'un message à un partenaire d'aperçu de messagerie vocale

Cet exemple établit à 300 secondes (5 minutes) la durée maximale d'un message à un partenaire d'aperçu de messagerie vocale dans une stratégie de boîte aux lettres de messagerie unifiée appelée *MyUMMailboxPolicy*.

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -VoiceMailPreviewPartnerMaxMessageDuration 300

