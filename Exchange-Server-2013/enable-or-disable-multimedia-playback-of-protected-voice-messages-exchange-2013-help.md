---
title: 'Activer ou désactiver la lecture multimédia de messages vocaux protégés: Exchange 2013 Help'
TOCTitle: Activer ou désactiver la lecture multimédia de messages vocaux protégés
ms:assetid: 3c33370c-4262-42b1-8d83-d61fc7c426cd
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Ee423543(v=EXCHG.150)
ms:contentKeyID: 52057059
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Activer ou désactiver la lecture multimédia de messages vocaux protégés

 

_**Sapplique à :**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :**2013-02-22_

Vous pouvez obliger les utilisateurs qui reçoivent des messages vocaux protégés à recourir à la fonctionnalité Émettre au téléphone pour consulter leurs messages. Sinon, au cas où le logiciel client ne prend pas en charge la gestion des droits, les utilisateurs doivent utiliser Outlook Voice Access.

Pour consulter leurs messages vocaux, les utilisateurs à extension messagerie unifiée peuvent utiliser la fonctionnalité Émettre au téléphone ou un logiciel multimédia sur un ordinateur ou un appareil mobile. La reproduction multimédia permet aux utilisateurs à extension messagerie unifiée d'écouter leurs messages vocaux à l'aide d'un lecteur multimédia via les haut-parleurs de l'ordinateur ou sur un appareil mobile.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>La messagerie vocale protégée est disponible uniquement pour les clients qui utilisent une version d'Outlook prenant en charge la gestion des droits. Au cas où le logiciel client ne prend pas en charge la gestion des droits, les utilisateurs doivent utiliser Outlook Voice Access pour écouter leurs messages.</td>
</tr>
</tbody>
</table>


Par défaut, la valeur de la propriété **RequireProtectedPlayOnPhone** d'une stratégie de boîte aux lettres de messagerie unifiée est définie sur False. En d'autres termes, les utilisateurs à extension messagerie unifiée associés à cette stratégie de boîte aux lettres de messagerie unifiée peuvent écouter leurs messages vocaux protégés des manières suivantes :

  - en utilisant Outlook Voice Access ;

  - en utilisant le lecteur multimédia intégré ou le bouton Émettre au téléphone dans Outlook 2010 ou version ultérieure ;

  - en utilisant le lecteur multimédia intégré ou le bouton Émettre au téléphone dans Outlook Web App.

Si cette valeur est définie sur True, la reproduction multimédia des messages vocaux protégés n'est pas autorisée. Les utilisateurs à extension messagerie unifiée associés à une stratégie de boîte aux lettres de messagerie unifiée sur laquelle cette valeur est définie sur True peuvent écouter leurs messages vocaux protégés uniquement des manières suivantes :

  - en utilisant Outlook Voice Access ;

  - en utilisant le bouton Émettre au téléphone dans Outlook 2010 ou version ultérieure.

  - en utilisant le bouton Émettre au téléphone dans Outlook Web App.

Ce paramètre s'avère particulièrement utile lorsque des utilisateurs à extension messagerie unifiée utilisent des ordinateurs publics, des ordinateurs portables dans des lieux publics ou le lecteur multimédia de leur appareil mobile pour écouter les messages vocaux protégés contenant des informations privées.

Pour les autres tâches de gestion relatives aux procédures de la messagerie vocale protégée, consultez la rubrique [Procédures de la messagerie vocale protégées](protected-voice-mail-procedures-exchange-2013-help.md).

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

## Utiliser le CAE pour activer ou désactiver la reproduction multimédia de messages vocaux protégés

1.  Dans le CAE, accédez à **Messagerie unifiée** \> **Plans de numérotation de messagerie unifiée**. Dans l'affichage Liste, sélectionnez le plan de numérotation de messagerie unifiée à modifier puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

2.  Sous **Stratégies de boîte aux lettres de messagerie unifiée**, sélectionnez la stratégie de boîte aux lettres de messagerie unifiée à gérer, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

3.  Dans la page **Stratégie de boîte aux lettres de messagerie unifiée** \> **Messagerie vocale protégée**, cochez la case en regard du paramètre **Émettre au téléphone requis pour les messages vocaux protégés** afin de l'activer. Décochez la case pour désactiver ce paramètre.

4.  Cliquez sur **Enregistrer**.

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour activer ou désactiver la reproduction multimédia des messages vocaux protégés

Cet exemple permet aux utilisateurs associés à la stratégie de boîte aux lettres de messagerie unifiée nommée `MyUMMailboxPolicy` de lire des messages vocaux protégés à l'aide d'un lecteur multimédia.

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -RequireProtectedPlayOnPhone $false

Cet exemple empêche les utilisateurs associés à la stratégie de boîte aux lettres de messagerie unifiée nommée `MyUMMailboxPolicy` de lire des messages vocaux protégés à l'aide d'un lecteur multimédia.

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -RequireProtectedPlayOnPhone $true

