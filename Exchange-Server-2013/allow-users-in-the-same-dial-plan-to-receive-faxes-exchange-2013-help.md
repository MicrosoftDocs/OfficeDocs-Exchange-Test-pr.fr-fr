---
title: 'Autoriser les utilisateurs dans le même plan de numérotation pour recevoir des télécopies: Exchange 2013 Help'
TOCTitle: Autoriser les utilisateurs dans le même plan de numérotation pour recevoir des télécopies
ms:assetid: cb245028-0b86-4171-879e-934dd35fa626
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb124557(v=EXCHG.150)
ms:contentKeyID: 52057182
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Autoriser les utilisateurs dans le même plan de numérotation pour recevoir des télécopies

 

_**Sapplique à :** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2016-12-09_

Vous pouvez autoriser tous les utilisateurs associés à un plan de numérotation de messagerie unifiée à recevoir des messages de télécopie dans leur boîte aux lettres. Par défaut, les utilisateurs à extension messagerie unifiée associés à un plan de numérotation de messagerie unifiée peuvent recevoir des messages de télécopie. Pour autoriser les utilisateurs à extension messagerie unifiée à recevoir des messages de télécopie dans leur boîte aux lettres, le plan de numérotation doit être configuré de manière à accepter les appels de télécopie entrants. Vous devez également activer la fonctionnalité de télécopie sur la stratégie de boîte aux lettres et pour l'utilisateur. Par défaut, cette fonctionnalité est activée sur les plans de numérotation et les stratégies de boîte aux lettres ainsi que pour les utilisateurs. Cependant, il peut arriver que ces paramètres par défaut changent et que les utilisateurs à extension messagerie unifiée ne puissent pas recevoir de messages de télécopie.

Si vous empêchez la réception des messages de télécopie sur un plan de numérotation, tous les utilisateurs associés au plan de numérotation ne pourront pas recevoir de messages de télécopie, même si vous configurez les propriétés d'un utilisateur individuel pour qu'il reçoive des messages de télécopie. L'activation ou la désactivation de la télécopie sur un plan de numérotation de messagerie unifiée prime sur les paramètres de télécopie d'une stratégie de boîte aux lettres ou d'un utilisateur à extension messagerie unifiée.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Vous pouvez utiliser le Centre d'administration Exchange (CAE) pour configurer les paramètres de télécopie sur une stratégie de boîte aux lettres de messagerie unifiée. Vous devez cependant utiliser l'environnement de ligne de commande Exchange Management Shell pour configurer les paramètres de télécopie sur des plans de numérotation ou pour des utilisateurs individuels.</td>
</tr>
</tbody>
</table>


Pour plus d’informations sur les partenaires de télécopie, consultez [Microsoft PinPoint pour les partenaires de télécopie](https://go.microsoft.com/fwlink/?linkid=190238).

Pour découvrir d'autres tâches de gestion relatives à la télécopie, consultez la rubrique [Procédures d'envoi de télécopie](faxing-procedures-exchange-2013-help.md).

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : moins d'une minute.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l'entrée « Plans de numérotation de messagerie unifiée » dans la rubrique [Autorisations de messagerie unifiée](unified-messaging-permissions-exchange-2013-help.md).

  - Avant d'effectuer ces procédures, vérifiez qu'un plan de numérotation de messagerie unifiée a été créé. Pour obtenir la procédure détaillée, consultez la rubrique [Créer un plan de numérotation de messagerie unifiée](create-a-um-dial-plan-exchange-2013-help.md).

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


## Utiliser l'environnement de ligne de commande Exchange Management Shell pour autoriser les utilisateurs associés à un plan de numérotation à recevoir des télécopies

Cet exemple autorise les utilisateurs à extension messagerie unifiée associés au plan de numérotation de messagerie unifiée `MyUMDialPlan` à recevoir des télécopies entrantes.

    Set-UMDialPlan -Identity MyUMDialPlan -FaxEnabled $true

