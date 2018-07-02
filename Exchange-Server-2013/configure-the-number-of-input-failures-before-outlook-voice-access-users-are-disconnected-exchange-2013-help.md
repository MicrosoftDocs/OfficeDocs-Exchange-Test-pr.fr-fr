---
title: "Configurer le nombre d'échecs d'entrée avant que les utilisateurs Outlook Voice Access sont déconnectés.: Exchange 2013 Help"
TOCTitle: Configurer le nombre d'échecs d'entrée avant que les utilisateurs Outlook Voice Access sont déconnectés.
ms:assetid: 64c13d17-a26a-4c9b-b495-bd69c716456a
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Ee423547(v=EXCHG.150)
ms:contentKeyID: 50478288
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurer le nombre d'échecs d'entrée avant que les utilisateurs Outlook Voice Access sont déconnectés.

 

_**Sapplique à :** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2012-11-09_

Vous pouvez configurer combien de données incorrectes des utilisateurs qui appellent un numéro Outlook Voice Access peuvent entrer avant d'être déconnectés. Ce paramètre s'applique aux utilisateurs d'Outlook Voice Access et aux appelants non authentifiés qui utilisent la recherche dans l'annuaire.

Voici des exemples de types de données qui sont considérés comme incorrects :

  - Un appelant demande un numéro de poste qui n'est pas trouvé dans le système.

  - Le système ne peut pas localiser le numéro de poste de l'utilisateur pour transférer l'appel.

  - Un appelant appuie sur une option de menu qui n'est pas valide.

La valeur de ce paramètre peut se situer entre 1 et 20. Pour la plupart des organisations, cette valeur doit être définie par défaut sur trois tentatives. Choisir une valeur trop basse peut déconnecter les appelants de façon anticipée.

Pour les autres tâches de gestion relatives aux plans de numérotation de messagerie unifiée, consultez la rubrique [Procédures de plan de numérotation de messagerie unifiée](um-dial-plan-procedures-exchange-2013-help.md).

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : moins d'une minute.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l'entrée « Plans de numérotation de messagerie unifiée » dans la rubrique [Autorisations de messagerie unifiée](unified-messaging-permissions-exchange-2013-help.md).

  - Avant d'exécuter ces procédures, vérifiez qu'un plan de numérotation de messagerie unifiée a été créé. Pour obtenir la procédure détaillée, consultez la rubrique [Créer un plan de numérotation de messagerie unifiée](create-a-um-dial-plan-exchange-2013-help.md).

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

## Utiliser le CAE pour configurer le nombre d'échecs d'entrée avant de déconnecter

1.  Dans le Centre d'administration Exchange, accédez à **Messagerie unifiée** \> **Plans de numérotation de messagerie unifiée**.

2.  Dans l'affichage Liste, sélectionnez le plan de numérotation de messagerie unifiée à modifier, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

3.  Dans la page **Plan de numérotation de messagerie unifiée**, cliquez sur **Configurer**.

4.  Dans **Paramètres**, sous **Nombre d'échecs d'entrées avant la déconnexion**, entrez un nombre d'échecs d'entrées.

5.  Cliquez sur **Enregistrer**.

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour configurer les erreurs de saisie avant déconnexion

Cet exemple définit le nombre d'erreurs de saisie avant déconnexion sur 5 pour un plan de numérotation de messagerie unifiée appelé `MyUMDialPlan`.

    Set-UMDialPlan -identity MyUMDialPlan -InputFailuresBeforeDisconnect 5

