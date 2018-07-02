---
title: 'Supprimer une stratégie de carnet d’adresses: Exchange 2013 Help'
TOCTitle: Supprimer une stratégie de carnet d’adresses
ms:assetid: c20c6f82-2f75-4116-9be1-c5af10113f71
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Hh529946(v=EXCHG.150)
ms:contentKeyID: 50479105
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Supprimer une stratégie de carnet d’adresses

 

_**Sapplique à :**Exchange Online, Exchange Server 2013_

_**Dernière rubrique modifiée :**2014-03-25_

Utilisez cette procédure pour supprimer une stratégie de carnet d’adresses (ABP).

Si vous souhaitez rechercher des tâches de gestion supplémentaires relatives aux stratégies de carnet d’adresses, consultez la rubrique [Procédures des stratégies de carnet d’adresses](address-book-policy-procedures-exchange-2013-help.md).

## Ce qu’il faut savoir avant de commencer ?

  - Durée d’exécution estimée : Moins de 5 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Stratégies de carnet d’adresses » dans la rubrique [Autorisations pour configurer les adresses de messagerie et les carnets d’adresses](email-address-and-address-book-permissions-exchange-2013-help.md).

  - Vous ne pouvez pas supprimer une stratégie de carnet d’adresses si elle est toujours attribuée à la boîte aux lettres d’un utilisateur ou à une boîte aux lettres ayant subi une suppression logicielle. Pour déterminer si une stratégie de carnet d’adresses est affectée à un utilisateur, exécutez la commande suivante dans l’environnement de ligne de commande Exchange Management Shell :
    
    `Get-Mailbox | Where $._AddressBookPolicy -eq <AddressBookPolicyName>`
    
    Pour déterminer si une stratégie de carnet d’adresses est affectée à une boîte aux lettres ayant subi une suppression logicielle, exécutez la commande suivante :
    
    `Get-Mailbox -SoftDeletedMailbox | Where $._AddressBookPolicy -eq <AddressBookPolicyName>`

  - Pour supprimer une stratégie de carnet d’adresses de la boîte aux lettres d’un utilisateur, vous pouvez utiliser la page **Fonctionnalités de boîte aux lettres** des propriétés de la boîte aux lettres ou la cmdlet **Set-Mailbox**.

  - Vous ne pouvez pas utiliser le Centre d’administration Exchange (CAE) pour supprimer une stratégie de carnet d’adresses. Vous devez utiliser l’environnement de ligne de commande Exchange Management Shell.

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

<table>
<thead>
<tr class="header">
<th><img src="images/Bb125224.tip(EXCHG.150).gif" title="Conseil" alt="Conseil" />Conseil :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.</td>
</tr>
</tbody>
</table>


## Utilisation du Shell pour supprimer une stratégie de carnet d’adresses

Cet exemple concerne la suppression de la stratégie de carnet d’adresses (ABP) nommée ABP\_TailspinToys.

    Remove-AddressBookPolicy -Identity "ABP_TailspinToys"

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Remove-AddressBookPolicy](https://technet.microsoft.com/fr-fr/library/hh529929\(v=exchg.150\)).

