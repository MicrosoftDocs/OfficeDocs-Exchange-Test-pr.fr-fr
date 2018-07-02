---
title: 'Appliquer (ou supprimer) une stratégie de boîte aux lettres Outlook Web App à une boîte aux lettres: Exchange 2013 Help'
TOCTitle: Appliquer (ou supprimer) une stratégie de boîte aux lettres Outlook Web App à une boîte aux lettres
ms:assetid: 51d8e269-b0d5-4bc7-9b3d-0460871e54fa
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dd876884(v=EXCHG.150)
ms:contentKeyID: 50478186
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Appliquer (ou supprimer) une stratégie de boîte aux lettres Outlook Web App à une boîte aux lettres

 

_**Sapplique à :**Exchange Online, Exchange Server 2013_

_**Dernière rubrique modifiée :**2012-10-12_

Vous pouvez appliquer une stratégie de boîtes aux lettres Outlook Web App à une ou à plusieurs boîtes aux lettres ou en supprimer une en utilisant l'EAC ou le Shell.

## Ce qu’il faut savoir avant de commencer ?

  - Durée d’exécution estimée de chaque procédure : 10 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Stratégies de boîte aux lettres de messagerie unifiée Outlook Web App » dans la rubrique [Autorisations des clients et des périphériques mobiles](clients-and-mobile-devices-permissions-exchange-2013-help.md).

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

## Appliquer une stratégie de boîte aux lettres Outlook Web App

## Utilisez l'EAC pour appliquer une stratégie de boîte aux lettres Outlook Web App

1.  Dans le Centre d’administration Exchange, cliquez sur **Destinataires** \> **Boîtes aux lettres**.

2.  Dans le volet de travail, sélectionnez la boîte aux lettres à laquelle vous souhaitez appliquer une stratégie de boîte aux lettres Outlook Web App. Vous pouvez également sélectionner plusieurs boîtes aux lettres.

3.  **Si vous avez sélectionné une boîte aux lettres :**
    
    1.  Faites défiler le volet d'informations jusqu'à **Connectivité de messagerie** et cliquez sur **Afficher les détails**.
    
    2.  Cliquez sur **Parcourir** pour afficher et sélectionner l’une des stratégies de boîte aux lettres disponibles.
    
    3.  Cliquez sur **Enregistrer** pour attribuer la stratégie sélectionnée à la boîte aux lettres sélectionnée.
    
    **Si vous avez sélectionné plusieurs boîtes aux lettres :**
    
    1.  Faites défiler le volet d'informations jusqu'à **Outlook Web App** et cliquez sur **Attribuer une stratégie**.
    
    2.  Cliquez sur **Parcourir** pour afficher et sélectionner l’une des stratégies de boîte aux lettres disponibles.
    
    3.  Cliquez sur **Enregistrer** pour attribuer la stratégie sélectionnée pour les boîtes aux lettres sélectionnées.

## Utiliser l’environnement Shell pour appliquer une stratégie de boîte aux lettres Outlook Web App à une boîte aux lettres existante

Cet exemple montre comment appliquer la stratégie de boîte aux lettres Outlook Web App nommée « Calendrier » à la boîte aux lettres de l’utilisateur jean-charles@contoso.com.

    Set-CASMailbox -Identity tony@contoso.com -OwaMailboxPolicy:Calendar

Pour plus d’informations sur la syntaxe et les paramètres, voir [Set-CASMailbox](https://technet.microsoft.com/fr-fr/library/bb125264\(v=exchg.150\)).

## Supprimer une stratégie de boîte aux lettres Outlook Web App

## Utiliser le CAE pour supprimer une stratégie de boîte aux lettres Outlook Web App

1.  Dans le Centre d’administration Exchange, cliquez sur **Destinataires** \> **Boîtes aux lettres**.

2.  Dans le volet de travail, sélectionnez la boîte aux lettres à laquelle vous souhaitez supprimer une stratégie de boîte aux lettres Outlook Web App.

3.  Faites défiler le volet d'informations jusqu'à **Connectivité de messagerie** et cliquez sur **Afficher les détails**.
    
    Si la stratégie de boîte aux lettres a été attribuée, cliquez sur **Effacer** pour la supprimer de la boîte aux lettres.

4.  Cliquez sur **Enregistrer** pour enregistrer vos modifications.

## Utiliser l’environnement Shell pour supprimer une stratégie de boîte aux lettres Outlook Web App dans une boîte aux lettres existante.

Cet exemple montre comment supprimer la stratégie de boîte aux lettres Outlook Web App de la boîte aux lettres de l’utilisateur jean-charles@contoso.com.

    Set-CASMailbox -Identity tony@contoso.com -OwaMailboxPolicy:$null

Pour plus d’informations sur la syntaxe et les paramètres, voir [Set-CASMailbox](https://technet.microsoft.com/fr-fr/library/bb125264\(v=exchg.150\)).

