---
title: "Définir le nombre d'échecs de connexion avant une réinitialisation du code PIN de la messagerie vocale: Exchange 2013 Help"
TOCTitle: Définir le nombre d'échecs de connexion avant une réinitialisation du code PIN de la messagerie vocale
ms:assetid: 4de38499-0a6f-4f00-8697-eeff805d7266
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Aa997939(v=EXCHG.150)
ms:contentKeyID: 50555389
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Définir le nombre d'échecs de connexion avant une réinitialisation du code PIN de la messagerie vocale

 

_**Sapplique à :** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2013-02-22_

Vous pouvez configurer le nombre d'échecs de connexion autorisés avant la réinitialisation du code confidentiel pour un utilisateur d'Outlook Voice Access sur une valeur comprise entre 1 et 998. La valeur par défaut est 5. Le nombre d'échecs de connexion autorisés avant la réinitialisation d'un code confidentiel est configuré pour une stratégie de boîte aux lettres de messagerie unifiée et s'applique à tous les utilisateurs d'Outlook Voice Access associés à cette stratégie.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Vous pouvez optimiser la sécurité en configurant le paramètre <strong>Nombre d'échecs de connexion avant réinitialisation du code confidentiel</strong> sur un nombre inférieur à 5. La sécurité est diminuée si le nombre est supérieur à 5.</td>
</tr>
</tbody>
</table>


Pour les tâches supplémentaires concernant la sécurité du code confidentiel Outlook Voice Access, consultez la rubrique [Procédures de sécurité de code confidentiel](pin-security-procedures-exchange-2013-help.md).

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : 3 minutes.

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

## Utiliser le Centre d'administration Exchange (CAE) pour configurer le nombre d'échecs de connexion avant la réinitialisation d'un code confidentiel

1.  Dans le Centre d'administration Exchange, accédez à **Messagerie unifiée** \> **Plans de numérotation de messagerie unifiée**.

2.  Dans l'affichage Liste, sélectionnez le plan de numérotation de messagerie unifiée à modifier puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

3.  dans la page **Plan de numérotation de messagerie unifiée**, sous **Stratégies de boîte aux lettres de messagerie unifiée**, sélectionnez la stratégie de boîte aux lettres de messagerie unifiée à modifier, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

4.  Cliquez sur **Stratégies de code confidentiel**, puis en regard du paramètre **Nombre d'échecs de connexion avant réinitialisation du code confidentiel**, entrez une valeur comprise entre 0 et 999.

5.  Cliquez sur **Enregistrer**.

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour configurer le nombre d'échecs de connexion avant la réinitialisation d'un code confidentiel

Cet exemple définit le nombre d'échecs de connexion avant la réinitialisation du code confidentiel de l'utilisateur sur 3 pour les utilisateurs à extension messagerie unifiée associés à une stratégie de boîte aux lettres de messagerie unifiée nommée `MyUMMailboxPolicy`.

    Set-UMMailboxPolicy -Identity MyUMMailboxPolicy -LogonFailuresBeforePINReset 3

Cet exemple définit le nombre d'échecs de connexion avant la réinitialisation du code confidentiel de l'utilisateur sur 3, le nombre maximal de tentatives de connexions sur 5 et la longueur minimale du code confidentiel sur 9 caractères pour les utilisateurs à extension messagerie unifiée sont associés à la stratégie de boîte aux lettres de messagerie unifiée nommée `MyUMMailboxPolicy`.

    Set-UMMailboxPolicy -Identity MyUMMailboxPolicy -LogonFailuresBeforePINReset 3 -MaxLogonAttempts 5 -MinPINLength 9

