---
title: 'Configurer les services de partenaires d’aperçu de messagerie vocale pour les utilisateurs: Exchange 2013 Help'
TOCTitle: Configurer les services de partenaires d’aperçu de messagerie vocale pour les utilisateurs
ms:assetid: 7bb914ca-5502-4e64-bae5-555034138d8a
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Ff630920(v=EXCHG.150)
ms:contentKeyID: 51407205
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurer les services de partenaires d’aperçu de messagerie vocale pour les utilisateurs

 

_**Sapplique à :** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2016-12-09_

Vous pouvez configurer un partenaire d'aperçu de messagerie vocale dans une stratégie de boîte aux lettres de messagerie unifiée. Une fois que vous avez configuré les paramètres correspondants, tels que l'ID partenaire d'aperçu de messagerie vocale et Adresse du partenaire d'aperçu de messagerie vocale dans le cadre de la stratégie de boîte aux lettres de messagerie unifiée, ils s'appliquent à tous les utilisateurs à extension messagerie unifiée associés à cette stratégie.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Vous devez utiliser l'environnement de ligne de commande Exchange Management Shell pour configurer un partenaire d'aperçu de messagerie vocale.</td>
</tr>
</tbody>
</table>


Pour découvrir d'autres tâches de gestion relatives aux stratégies de boîte aux lettres de messagerie unifiée, consultez la rubrique [Procédures de stratégie de boîte aux lettres de messagerie unifiée](um-mailbox-policy-procedures-exchange-2013-help.md).

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : 5 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l'entrée « Stratégies de boîte aux lettres de messagerie unifiée » dans la rubrique [Autorisations de messagerie unifiée](unified-messaging-permissions-exchange-2013-help.md).

  - Avant d'exécuter ces procédures, vérifiez qu'un plan de numérotation de messagerie unifiée a été créé. Pour obtenir la procédure détaillée, consultez la rubrique [Créer un plan de numérotation de messagerie unifiée](create-a-um-dial-plan-exchange-2013-help.md).

  - Avant d'effectuer ces procédures, vérifiez qu'une stratégie de boîte aux lettres de messagerie unifiée a été créée. Pour obtenir la procédure détaillée, consultez la rubrique [Créer une stratégie de boîte aux lettres de messagerie unifiée](create-a-um-mailbox-policy-exchange-2013-help.md).

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


## Comment procéder ?

## Étape 1 : S'inscrire à un service partenaire

Pour trouver la liste des partenaires certifiés et des instructions détaillées sur la manière de s’inscrire, consultez le [Gestionnaire de l’aperçu de messagerie vocale](voice-mail-preview-advisor-exchange-2013-help.md) ou le site Web de [Microsoft PinPoint](https://go.microsoft.com/fwlink/p/?linkid=281966) . Une fois que vous avez souscrit, le partenaire de l’aperçu de messagerie vocale fournira vous un ID de partenaire et l’adresse SMTP à utiliser pour transférer les messages vocaux.

L'étape 2 consiste à appliquer l'ID partenaire et l'adresse SMTP acquis à l'étape précédente aux stratégies de boîte aux lettres de messagerie unifiée requises.

## Étape 2 : Définir l'ID et l'adresse du partenaire d'aperçu de messagerie vocale

Cet exemple définit l'adresse du partenaire d'aperçu de messagerie sur exumvmp@fabrikam.com et son sur ID CON123-2010 sur la stratégie de boîte aux lettres de messagerie unifiée *MyUMMailboxPolicy*.

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -VoiceMailPreviewPartnerAddress exumvmp@fabrikam.com
    -VoiceMailPreviewPartnerAssignedID CON123-2010

## Étape 3 : Configurer les paramètres avancés du partenaire d'aperçu de messagerie

Si le partenaire a besoin de paramètres personnalisés, vous pouvez définir les deux paramètres supplémentaires suivants :

  - *VoiceMailPreviewPartnerMaxMessageDuration*

  - *VoiceMailPreviewPartnerMaxDeliveryDelay*

Cet exemple définit la durée maximale d'un message sur 300 secondes (5 minutes) et le délai de remise maximal à 600 secondes (10 minutes) pour la stratégie de boîte aux lettres de messagerie unifiée *MyUMMailboxPolicy*.

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -VoiceMailPreviewPartnerMaxMessageDuration 300 -VoiceMailPreviewPartnerMaxDeliveryDelay 600

## Étape 4 : Associer un utilisateur à extension messagerie unifiée à la stratégie de boîte aux lettres de messagerie unifiée pour un partenaire d'aperçu de messagerie vocale

Pour configurer le service de partenaire d'aperçu de messagerie vocale pour certains utilisateurs à extension messagerie unifiée (mais pas tous) associés à un plan de numérotation de messagerie unifiée, vous devez créer une nouvelle stratégie et configurer le paramètres du partenaire. Une fois l'opération terminée, vous pouvez appliquer la nouvelle stratégie aux utilisateurs à extension messagerie unifiée sélectionnés. Pour plus d'informations sur la procédure d'attribution d'un utilisateur à extension messagerie unifiée à une stratégie de boîte aux lettres de messagerie unifiée, consultez les rubriques suivantes :

  - [Attribuer une stratégie de boîte aux lettres de messagerie unifiée](assign-a-um-mailbox-policy-exchange-2013-help.md)

  - [Set-UMMailbox](https://technet.microsoft.com/fr-fr/library/bb124893\(v=exchg.150\))

Pour plus d'informations sur le programme de partenariat d'aperçu de messagerie vocale, consultez la rubrique [Gestionnaire de l’aperçu de messagerie vocale](voice-mail-preview-advisor-exchange-2013-help.md).

