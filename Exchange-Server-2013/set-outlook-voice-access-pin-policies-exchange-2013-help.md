---
title: 'Définir des stratégies de code confidentiel de Outlook Voice Access: Exchange 2013 Help'
TOCTitle: Définir des stratégies de code confidentiel de Outlook Voice Access
ms:assetid: 5b2800b7-bfa6-4282-975c-0706ae25ad64
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Aa998285(v=EXCHG.150)
ms:contentKeyID: 50555398
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Définir des stratégies de code confidentiel de Outlook Voice Access

 

_**Sapplique à :**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :**2013-02-22_

Vous pouvez définir des stratégies de code confidentiel en relation avec une stratégie de boîte aux lettres de messagerie unifiée. Les stratégies de boîte aux lettres de messagerie unifiée peuvent être configurées pour augmenter le niveau de sécurité des utilisateurs à extension messagerie unifiée qui utilisent Outlook Voice Access en exigeant d'eux qu'ils se conforment aux stratégies de code confidentiel prédéfinies pour votre organisation.

Pour définir des stratégies de code confidentiel pour les utilisateurs d'Outlook Voice Access, vous pouvez soit créer une stratégie de boîte aux lettres de messagerie unifiée, soit modifier une stratégie de boîte aux lettres de messagerie unifiée existante. Après avoir créé une stratégie de boîte aux lettres de messagerie unifiée, vous pouvez configurer cette dernière en définissant les paramètres de code confidentiel suivants :

  - `MinPasswordLength`

  - `PINLifetime`

  - `LogonFailuresBeforePINReset`

  - `MaxLogonAttempts`

  - `AllowCommonPatterns`

  - `PINHistoryCount`

Il s'agit d'une pratique recommandée en matière de sécurité pour implémenter des contraintes de code confidentiel strictes pour des utilisateurs de messagerie unifiée. Cette pratique qui élève le niveau de sécurité de votre réseau peut être appliquée lors de la création de stratégies de code confidentiel de messagerie unifiée dont les codes confidentiels exigent 6 chiffres, voire davantage.

Lorsque vous modifiez la stratégie de code confidentiel, le nouveau paramétrage de code confidentiel est appliqué aux utilisateurs actuellement associés à la stratégie de boîte aux lettres de messagerie unifiée. Par exemple, si vous modifiez la stratégie de boîte aux lettres de messagerie unifiée en changeant la longueur minimale du code confidentiel de 7 chiffres en 10 chiffres, la prochaine fois que des utilisateurs se connectent, ils sont forcés de modifier leur code confidentiel pour se conformer à l'exigence de modification de code confidentiel.

Pour les autres tâches de gestion concernant la sécurité d'Outlook Voice Access par code confidentiel, consultez la rubrique [Procédures de sécurité de code confidentiel](pin-security-procedures-exchange-2013-help.md).

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : 5 minutes.

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

## Définir des stratégies de code confidentiel pour les utilisateurs d'Outlook Voice Access à l'aide du Centre d'administration Exchange (CAE)

1.  Dans le Centre d'administration Exchange, accédez à **Messagerie unifiée** \> **Plans de numérotation de messagerie unifiée**. Dans l'affichage Liste, cliquez sur le plan de numérotation de messagerie unifiée à modifier, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

2.  Dans la page **Plan de numérotation de messagerie unifiée**, sous **Stratégies de boîte aux lettres de messagerie unifiée**, sélectionnez la stratégie de boîte aux lettres de messagerie unifiée à modifier, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

3.  Cliquez sur **Propriétés**.

4.  Dans la page **Stratégie de boîte aux lettres de messagerie unifiée**, cliquez sur **Stratégies de code confidentiel**.

5.  Dans la page **Stratégies de code confidentiel**, configurez les paramètres de code confidentiel pour les utilisateurs d'Outlook Voice Access associés à cette stratégie de boîte aux lettres de messagerie unifiée, puis cliquez sur **Enregistrer**.

## Définir des stratégies de code confidentiel pour les utilisateurs d'Outlook Voice Access à l'aide de l'environnement de ligne de commande Exchange Management Shell

Cet exemple définit les paramètres de code confidentiel pour les utilisateurs disposant de la stratégie de boîte aux lettres de messagerie unifiée `MyUMMailboxPolicy`.

    Set-UMMailboxPolicy -Identity MyUMMailboxPolicy -LogonFailuresBeforePINReset 8 -MaxLogonAttempts 12 -MinPINLength 8 -PINHistoryCount 10 -PINLifetime 60 -ResetPINText "The PIN used to allow you access to your mailbox using Outlook Voice Access has been reset."

