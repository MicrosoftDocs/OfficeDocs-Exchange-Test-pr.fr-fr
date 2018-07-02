---
title: "Création d'une stratégie de boîte aux lettres Outlook Web App: Exchange 2013 Help"
TOCTitle: Création d'une stratégie de boîte aux lettres Outlook Web App
ms:assetid: 347207fa-cfb7-40a6-b19a-831dcdb54ad5
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dd335191(v=EXCHG.150)
ms:contentKeyID: 50477850
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Création d'une stratégie de boîte aux lettres Outlook Web App

 

_**Sapplique à :** Exchange Online, Exchange Server 2013_

_**Dernière rubrique modifiée :** 2013-05-30_

Vous créez une stratégie de boîte aux lettres Outlook Web App pour appliquer un ensemble courant de paramètres de stratégies. Les stratégies de boîte aux lettres Outlook Web App sont utiles pour l'application et la normalisation des paramètres, par exemple les paramètres de pièces jointes, pour des groupes spécifiques d'utilisateurs.

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée de chaque procédure : 5 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette cmdlet. Bien que tous les paramètres de cette cmdlet soient répertoriés dans cette rubrique, il est possible que vous n’ayez pas accès à certains paramètres s’ils ne sont pas inclus dans les autorisations qui vous ont été attribuées. Pour voir les autorisations qui vous sont nécessaires, voir l'entrée « Stratégies de boîte aux lettres de messagerie unifiée Outlook Web App » dans la rubrique [Autorisations des clients et des périphériques mobiles](clients-and-mobile-devices-permissions-exchange-2013-help.md).

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

## Utiliser le CAE pour créer une stratégie de boîte aux lettres Outlook Web App

1.  Dans le CAE, cliquez sur **Autorisations** \> **Stratégies Outlook Web App**.

2.  Cliquez sur le bouton **Nouveau**.

3.  
    
    Entrez un nom pour votre stratégie.

4.  
    
    Utilisez les cases à cocher pour activer ou désactiver des fonctionnalités. Par défaut, les fonctionnalités les plus courantes sont affichées. Pour afficher toutes les fonctionnalités pouvant être activées ou désactivées, cliquez sur **plus d'options**.
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Présente les paramètres pour le remplacement par les stratégies de boîte au lettres Outlook Web App par les paramètres de répertoire virtuel Outlook Web App. Vous pouvez modifier les paramètres de segmentation des utilisateurs à l'aide de la cmdlet <strong>Set-CASMailbox</strong> dans l'environnement Shell.</td>
    </tr>
    </tbody>
    </table>


5.  Cliquez sur **Enregistrer** pour enregistrer la stratégie.

## Utiliser l'environnement Shell pour créer une stratégie de boîte aux lettres de Outlook Web App

Cet exemple crée une stratégie de boîte aux lettres Outlook Web App appelée `Policy1`.

  - Dans l'environnement de ligne de commande Exchange Management Shell, exécutez la commande suivante.
    
        New-OwaMailboxPolicy -Name Policy1

Pour plus d'informations sur la syntaxe et les paramètres, consultez la rubrique [New-OwaMailboxPolicy](https://technet.microsoft.com/fr-fr/library/dd351067\(v=exchg.150\)). Pour plus d'informations sur l'utilisation de l'environnement de ligne de commande Exchange Management Shell pour configurer une stratégie de boîte aux lettres Outlook Web App, consultez la rubrique [Set-OwaMailboxPolicy](https://technet.microsoft.com/fr-fr/library/dd297989\(v=exchg.150\)).

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez correctement créé une stratégie de boîte aux lettres Outlook Web App :

  - Dans le CAE, cliquez sur **Autorisations** \> **Stratégies Outlook Web App** et recherchez votre nouvelle stratégie de boîte aux lettres.

