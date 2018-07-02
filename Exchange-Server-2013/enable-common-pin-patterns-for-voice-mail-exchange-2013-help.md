---
title: 'Activer les modèles communs de code confidentiel pour la messagerie vocale: Exchange 2013 Help'
TOCTitle: Activer les modèles communs de code confidentiel pour la messagerie vocale
ms:assetid: 9940a8c2-f576-4089-ab96-8b318ad3da0f
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ673546(v=EXCHG.150)
ms:contentKeyID: 50555449
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Activer les modèles communs de code confidentiel pour la messagerie vocale

 

_**Sapplique à :** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2013-02-22_

Vous pouvez activer ou désactiver des modèles courants de codes confidentiels de messagerie unifiée pour des utilisateurs d'Outlook Voice Access. Si vous activez ou désactivez des paramètres de modèles courants de codes confidentiels dans une stratégie de boîte aux lettres de messagerie unifiée, la configuration qui en résulte s'applique à tous les utilisateurs à messagerie unifiée associés à cette stratégie. Par défaut, les utilisateurs à extension messagerie unifiée ne peuvent pas utiliser les modèles courants lorsqu'ils créent un code confidentiel.

Vous pouvez configurer plusieurs paramètres de code confidentiel dans une stratégie de boîte aux lettres de messagerie unifiée. Le paramètre **Autoriser les modèles courants de codes confidentiels** permet d'autoriser ou d'interdire l'utilisation de modèles numériques courants lors de la création d'un code confidentiel par les utilisateurs. Par défaut, ce paramètre est désactivé et empêche les utilisateurs de se servir des modèles numériques suivants :

  - Exemples

  - Exemples

  - **Suffixe d'une extension de boîte aux lettres**   Valeurs de code confidentiel qui incluent le suffixe de l'extension de boîte aux lettres d'un utilisateur. Par exemple, si l'extension de boîte aux lettres d'un utilisateur est 36697, le code confidentiel de l'utilisateur ne peut pas être 3669712.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Si l'option <strong>Autoriser les modèles courants de codes confidentiels</strong> est activée, seul le suffixe de l'extension de boîte aux lettres est rejeté.</td>
</tr>
</tbody>
</table>


Pour les autres tâches de gestion concernant la sécurité d'Outlook Voice Access par code confidentiel, consultez la rubrique [Procédures de sécurité de code confidentiel](pin-security-procedures-exchange-2013-help.md).

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

## Utiliser le Centre d'administration Exchange (CAE) pour activer les modèles courants de codes confidentiels

1.  Dans le Centre d'administration Exchange, accédez à **Messagerie unifiée** \> **Plans de numérotation de messagerie unifiée**. Dans l'affichage Liste, sélectionnez le plan de numérotation de messagerie unifiée à modifier, puis, dans la barre d'outils, cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

2.  Dans la page **Plan de numérotation de messagerie unifiée**, sous **Stratégies de boîte aux lettres de messagerie unifiée**, sélectionnez la stratégie de boîte aux lettres de messagerie unifiée que vous souhaitez gérer, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

3.  Dans la page **Stratégie de boîte aux lettres de messagerie unifiée**, sous **Stratégies de code confidentiel** cochez la case située en regard de l'option **Autoriser les modèles courants de codes confidentiels**.

4.  Cliquez sur **Enregistrer**.

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour activer les modèles courants de codes confidentiels

Dans cet exemple, nous autorisons des utilisateurs associés à la stratégie de boîte aux lettres de messagerie unifiée `MyUMMailboxPolicy` d'utiliser des codes confidentiels contenant des modèles courants.

    Set-UMMailboxPolicy -Identity MyUMMailboxPolicy -AllowCommonPatterns $true

