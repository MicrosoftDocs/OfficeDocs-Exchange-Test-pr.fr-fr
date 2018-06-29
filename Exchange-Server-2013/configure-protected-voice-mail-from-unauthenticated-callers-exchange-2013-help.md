---
title: 'Configuration de la messagerie vocale protégée contre les appelants non authentifiés: Exchange 2013 Help'
TOCTitle: Configuration de la messagerie vocale protégée contre les appelants non authentifiés
ms:assetid: 106bfa0a-a0fa-4a1b-bd59-4b6df1d0d61d
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dd335098(v=EXCHG.150)
ms:contentKeyID: 52057035
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configuration de la messagerie vocale protégée contre les appelants non authentifiés

 

_**Sapplique à :**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :**2013-02-22_

Vous pouvez configurer la messagerie unifiée pour répondre à un appel entrant, puis déterminer si celle-ci appliquera une protection par chiffrement aux messages vocaux. Quand un message vocal est protégé :

  - Le message est marqué comme Privé dans Microsoft Outlook et Outlook Web App.

  - Le message vocal peut être ouvert uniquement par le destinataire approprié.

  - Le destinataire peut répondre au message vocal, mais ne peut pas le transmettre à une personne non incluse dans le message vocal d'origine.

Ce paramètre s'applique aux messages vocaux envoyés aux utilisateurs à extension messagerie unifiée quand ils ne répondent pas à leur téléphone. Ce paramètre s'applique également aux messages vocaux envoyés directement aux utilisateurs à extension messagerie unifiée quand l'appelant utilise un standard automatique de messagerie unifiée.

Pour les autres tâches de gestion relatives aux procédures de la messagerie vocale protégée, consultez la rubrique [Procédures de la messagerie vocale protégées](protected-voice-mail-procedures-exchange-2013-help.md).

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : moins d'une minute.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Stratégies de boîte aux lettres de messagerie unifiée » dans la rubrique [Autorisations de messagerie unifiée](unified-messaging-permissions-exchange-2013-help.md).

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


## Que souhaitez-vous faire ?

## Utiliser le Centre d'administration Exchange (CAE) pour configurer la messagerie vocale protégée contre les appelants non authentifiés

1.  Dans le CAE, accédez à **Messagerie unifiée** \> **Plans de numérotation de messagerie unifiée**. Dans l'affichage Liste, sélectionnez le plan de numérotation de messagerie unifiée à modifier, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

2.  Dans la page **Plan de numérotation de messagerie unifiée**, sous **Stratégies de boîte aux lettres de messagerie unifiée**, sélectionnez la stratégie de boîte aux lettres de messagerie unifiée que vous souhaitez gérer, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

3.  Dans la page **Stratégie de boîte aux lettres de messagerie unifiée** \> **Messagerie vocale protégée**, sous **Protéger les messages vocaux provenant des appelants non authentifiés**, activez l'une des options suivantes :
    
      - **Aucun**   Quand vous définissez ce paramètre, aucune protection n'est appliquée aux messages vocaux envoyés aux utilisateurs à extension messagerie.
    
      - **Privé**   Quand ce paramètre est défini, la messagerie unifiée applique une protection uniquement aux messages vocaux qui ont été marqués comme Privé par l'appelant.
    
      - **Tous**   Quand ce paramètre est défini, la messagerie unifiée applique une protection à tous les messages vocaux, y compris à ceux qui ne sont pas marqués comme étant privés.

4.  Cliquez sur **Enregistrer**.

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour configurer la messagerie vocale protégée contre les appelants non authentifiés

Cet exemple permet de protéger tous les messages vocaux contre les appelants non authentifiés sur la stratégie de boîte aux lettres de messagerie unifiée `MyUMMailboxPolicy`.

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -ProtectUnauthenticatedVoiceMail -All

