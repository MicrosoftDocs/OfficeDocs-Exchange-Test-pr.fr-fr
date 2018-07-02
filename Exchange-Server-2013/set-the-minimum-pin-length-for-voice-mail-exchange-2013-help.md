---
title: 'Définir la longueur minimale du code confidentiel pour la messagerie vocale: Exchange 2013 Help'
TOCTitle: Définir la longueur minimale du code confidentiel pour la messagerie vocale
ms:assetid: b2ecab54-42e6-45af-8322-615cc1f68dd9
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb124271(v=EXCHG.150)
ms:contentKeyID: 50555478
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Définir la longueur minimale du code confidentiel pour la messagerie vocale

 

_**Sapplique à :**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :**2013-02-22_

Vous pouvez configurer la longueur minimale du code confidentiel pour vos utilisateurs d'Outlook Voice Access à extension messagerie unifiée. Les paramètres de code confidentiel que vous configurez dans une stratégie de boîte aux lettres de messagerie unifiée sont appliqués à tous les utilisateurs à extension messagerie unifiée associés à la stratégie de boîte aux lettres de messagerie unifiée.

Outlook Voice Access permet aux utilisateurs à extension messagerie unifiée d'accéder à leurs informations de messagerie vocale et électronique, ainsi qu'à leurs informations de calendrier et de contact personnelles qui se trouvent dans leur boîte aux lettres. Toutefois, avant de pouvoir accéder à leur boîte aux lettres, ils doivent entrer un code confidentiel pour s'authentifier auprès du système de messagerie vocale.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Si vous modifiez la valeur de longueur minimale du code confidentiel, pour pouvoir continuer, les utilisateurs actuels d'Outlook Voice Access sont invités à entrer un nouveau code confidentiel respectant le nouveau nombre minimal de chiffres. La valeur par défaut est 6.</td>
</tr>
</tbody>
</table>


Pour découvrir d'autres tâches de gestion concernant la sécurité d'Outlook Voice Access par code confidentiel, consultez la rubrique [Procédures de sécurité de code confidentiel](pin-security-procedures-exchange-2013-help.md).

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : moins d'une minute.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l'entrée « Stratégies de boîte aux lettres de messagerie unifiée » dans la rubrique [Autorisations de messagerie unifiée](unified-messaging-permissions-exchange-2013-help.md).

  - Avant d'effectuer ces procédures, vérifiez qu'un plan de numérotation de messagerie unifiée a été créé. Pour obtenir la procédure détaillée, consultez la rubrique [Créer un plan de numérotation de messagerie unifiée](create-a-um-dial-plan-exchange-2013-help.md).

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

## Utiliser le Centre d'administration Exchange (CAE) pour configurer la longueur minimale du code confidentiel pour Outlook Voice Access

1.  Dans le Centre d'administration Exchange, accédez à **Messagerie unifiée** \> **Plans de numérotation de messagerie unifiée**.

2.  Dans l'affichage Liste, sélectionnez le plan de numérotation à modifier, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

3.  Dans la page **Plan de numérotation de messagerie unifiée**, sous **Stratégies de boîte aux lettres de messagerie unifiée**, sélectionnez la stratégie de boîte aux lettres de messagerie unifiée à modifier, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

4.  Cliquez sur **Stratégies de code confidentiel**, puis en regard de **Longueur minimale du code confidentiel**, entrez une valeur comprise entre 4 et 24.

5.  Cliquez sur **Enregistrer**.

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour configurer la longueur minimale du code confidentiel pour Outlook Voice Access

Cet exemple définit la longueur minimale du code confidentiel à 8 chiffres pour les utilisateurs d'Outlook Voice Access associés à la stratégie de boîte aux lettres de messagerie unifiée `MyUMMailboxPolicy`.

    Set-UMMailboxPolicy -Identity MyUMMailboxPolicy -MinPINLength 8

Cet exemple définit la longueur minimale du code confidentiel sur 8 chiffres et définit le nombre d'échecs de connexion sur 3 avant que le code confidentiel ne soit réinitialisé. Ceci s'applique aux utilisateurs à messagerie unifiée associés à la stratégie de boîte aux lettres de messagerie unifiée nommée `MyUMMailboxPolicy`.

    Set-UMMailboxPolicy -Identity MyUMMailboxPolicy -LogonFailuresBeforePINReset 3 -MinPINLength 8

