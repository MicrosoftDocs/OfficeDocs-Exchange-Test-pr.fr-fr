---
title: 'Désactiver pour un groupe d’utilisateurs de télécopie: Exchange 2013 Help'
TOCTitle: Désactiver pour un groupe d’utilisateurs de télécopie
ms:assetid: 1c57c3ba-2b0e-43dd-9b28-43bada1592c5
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ650864(v=EXCHG.150)
ms:contentKeyID: 52057043
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Désactiver pour un groupe d’utilisateurs de télécopie

 

_**Sapplique à :**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :**2016-12-09_

Vous pouvez désactiver les télécopies entrantes pour des utilisateurs associés à une stratégie de boîte aux lettres de messagerie unifiée. Par défaut, quand vous activez la messagerie unifiée pour des utilisateurs, ces derniers ne peuvent pas recevoir de messages de télécopie tant que vous n'avez pas spécifié l'URI du serveur de partenaire de télécopie, déployé un serveur de partenaire de télécopie et activé la fonctionnalité de télécopie sur une stratégie de boîte aux lettres de messagerie unifiée. Si l'option autorisant les télécopies entrantes est désactivée dans le plan de numérotation de messagerie unifiée, les utilisateurs associés à la stratégie de boîte aux lettres de messagerie unifiée ne pourront pas recevoir de télécopies. De même, si l'option autorisant les télécopies entrantes est désactivée sur un utilisateur individuel, celui-ci ne pourra pas recevoir de télécopies.

Pour plus d’informations sur les partenaires de télécopie, consultez [Microsoft PinPoint pour les partenaires de télécopie](https://go.microsoft.com/fwlink/?linkid=190238).

Pour les autres tâches de gestion relatives à la télécopie, consultez la rubrique [Procédures d'envoi de télécopie](faxing-procedures-exchange-2013-help.md).

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : moins d'une minute.

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


## Que souhaitez-vous faire ?

## Utiliser le Centre d'administration Exchange (CAE) pour désactiver les télécopies entrantes

1.  Dans le CAE, accédez à **Messagerie unifiée** \> **Plans de numérotation de messagerie unifiée**. Dans l'affichage Liste, sélectionnez le plan de numérotation de messagerie unifiée à modifier, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

2.  Dans la page **Plan de numérotation de messagerie unifiée**, sous **Stratégies de boîte aux lettres de messagerie unifiée**, sélectionnez la stratégie de boîte aux lettres de messagerie unifiée à modifier, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

3.  Dans la page **Stratégie de boîte aux lettres de messagerie unifiée** \> **Général**, décochez la case en regard de l'option **Autoriser les télécopies entrantes**.

4.  Cliquez sur **Enregistrer** pour enregistrer vos modifications.

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour désactiver les télécopies entrantes

Cet exemple empêche les utilisateurs associés à la stratégie de boîte aux lettres de messagerie unifiée intitulée `MyUMMailboxPolicy` d'utiliser les télécopies entrantes.

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -AllowFax $false

