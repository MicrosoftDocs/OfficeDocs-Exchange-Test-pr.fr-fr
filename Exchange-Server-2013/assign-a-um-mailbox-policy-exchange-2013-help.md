---
title: 'Attribuer une stratégie de boîte aux lettres de messagerie unifiée: Exchange 2013 Help'
TOCTitle: Attribuer une stratégie de boîte aux lettres de messagerie unifiée
ms:assetid: c8da6cbe-3d22-4fff-8b5a-416b1c8adb6c
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb201728(v=EXCHG.150)
ms:contentKeyID: 50479161
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Attribuer une stratégie de boîte aux lettres de messagerie unifiée

 

_**Sapplique à :** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2012-11-30_

Lorsque vous activez un utilisateur pour la messagerie unifiée et la messagerie vocale, vous devez sélectionner une stratégie de boîte aux lettres de messagerie unifiée qui sera associée à la boîte aux lettres de l’utilisateur. Vous pouvez modifier la stratégie de boîte aux lettres de messagerie unifiée associée à la boîte aux lettres de l’utilisateur, une fois qu’il a été activé pour la messagerie unifiée.

Vous créez des stratégies de boîte aux lettres de messagerie unifiée pour appliquer un ensemble commun de stratégies ou de paramètres de sécurité à une série de boîtes aux lettres d’utilisateurs à messagerie unifiée. Vous pouvez utiliser les stratégies de boîte aux lettres de messagerie unifiée pour appliquer les paramètres suivants :

  - Stratégies de code confidentiel

  - Restrictions de numérotation

  - Autres propriétés générales de stratégies de boîte aux lettres de messagerie unifiée

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Une stratégie de boîte aux lettres de messagerie unifiée par défaut est créée chaque fois que vous créez un plan de numérotation de messagerie unifiée. Vous pouvez supprimer les stratégies de boîte aux lettres de messagerie unifiée par défaut ou créer d’autres stratégies de boîte aux lettres de messagerie unifiée selon les besoins de votre organisation.</td>
</tr>
</tbody>
</table>


Pour découvrir d'autres tâches de gestion relatives aux utilisateurs à extension messagerie vocale, consultez la rubrique [Voix des procédures de l'utilisateur à extension messagerie](voice-mail-enabled-user-procedures-exchange-2013-help.md).

## Ce qu’il faut savoir avant de commencer ?

  - Durée d’exécution estimée : 2 minutes.

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


## Que souhaitez-vous faire ?

## Utiliser le CAE pour modifier la stratégie de boîte aux lettres de messagerie unifiée attribuée à un utilisateur à messagerie unifiée

1.  Dans le CAE, accédez à **Destinataires**  \> **Boîtes aux lettres**.

2.  Dans l’affichage liste, sélectionnez la boîte aux lettres pour laquelle vous voulez changer la stratégie de messagerie unifiée.

3.  Dans le volet d’informations, sous **Fonctions de téléphone et de voix** \> **Messagerie unifiée**, cliquez sur**Afficher les détails**.

4.  Sur la page **Boîte aux lettres de messagerie unifiée**, cliquez sur **Paramètres de la boîte aux lettres de messagerie unifiée**, puis sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

5.  Sur la page **Boîte aux lettres de messagerie unifiée** \> en regard de **Stratégie de boîte aux lettres de MU**, cliquez sur **Parcourir** pour localiser la stratégie de boîte aux lettres de messagerie unifiée pour l’utilisateur.

6.  Cliquez sur **Enregistrer**.

## Utiliser l’environnement de ligne de commande Exchange Management Shell pour modifier la stratégie de boîte aux lettres de messagerie unifiée attribuée à un utilisateur à messagerie unifiée

Cet exemple associe l’utilisateur à messagerie unifiée Jean-Charles Colon à une stratégie de boîte aux lettres de messagerie unifiée nommée `MyUMMailboxPolicy`.

    Set-UMMailbox -Identity tonysmith@contoso.com -UMMailboxPolicy MyUMMailboxPolicy

