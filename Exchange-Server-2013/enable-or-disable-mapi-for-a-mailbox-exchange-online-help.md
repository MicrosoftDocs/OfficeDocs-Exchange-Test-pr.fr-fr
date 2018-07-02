---
title: 'Activer ou désactiver MAPI pour une boîte aux lettres: Exchange 2013 Help'
TOCTitle: Activer ou désactiver MAPI pour une boîte aux lettres
ms:assetid: c2c6718c-a2c0-4ed2-b4ed-364c3cb1f592
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb124497(v=EXCHG.150)
ms:contentKeyID: 50555477
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Activer ou désactiver MAPI pour une boîte aux lettres

 

_**Sapplique à :**Exchange Online, Exchange Server 2013_

_**Dernière rubrique modifiée :**2017-12-31_

Le Centre d’administration Exchange ou l’Environnement de ligne de commande Exchange Management Shell vous permet d’activer ou de désactiver MAPI pour une boîte aux lettres utilisateur. Lorsque MAPI est activé, Outlook ou un autre client de messagerie électronique peut accéder à la boîte aux lettres d’un utilisateur. Lorsque MAPI est désactivé, ni Outlook ni un autre client de messagerie électronique ne peut y accéder. Cependant, la boîte aux lettres continue de recevoir des messages électroniques et, en supposant que la boîte aux lettres est configurée pour prendre en charge l’accès par ces clients, un utilisateur peut y accéder pour envoyer et recevoir des messages en utilisant Outlook Web App, un client de messagerie électronique POP ou IMAP.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>La prise en charge pour Outlook Web App et pour les clients de messagerie électronique MAPI, POP3 et IMAP4 est activée par défaut lors de la création d’une boîte aux lettres utilisateur.</td>
</tr>
</tbody>
</table>


Pour les tâches supplémentaires de gestion relatives à la gestion de l’accès aux clients de messagerie, consultez les rubriques suivantes :

  - [Activer ou désactiver Outlook Web App pour une boîte aux lettres](enable-or-disable-outlook-web-app-for-a-mailbox-exchange-2013-help.md)

  - [Activation ou désactivation de l'accès IMAP4 pour un utilisateur](enable-or-disable-imap4-access-for-a-user-exchange-2013-help.md)

  - [Activer ou désactiver l’accès POP3 pour un utilisateur](enable-or-disable-pop3-access-for-a-user-exchange-2013-help.md)

## Ce qu’il faut savoir avant de commencer ?

  - Durée d'exécution estimée : 2 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Paramètres utilisateur d’accès au client » dans la rubrique [Autorisations des clients et des périphériques mobiles](clients-and-mobile-devices-permissions-exchange-2013-help.md).

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


## Que souhaitez-vous faire ?

## Utiliser le Centre d’administration Exchange pour activer ou désactiver MAPI

1.  Dans le CAE, accédez à **Destinataires**  \> **Boîtes aux lettres**.

2.  Dans la liste des boîtes aux lettres utilisateur, cliquez sur la boîte aux lettres pour laquelle vous souhaitez activer ou désactiver MAPI, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

3.  Dans la page de propriétés de boîte aux lettres, cliquez sur **Fonctionnalités de boîte aux lettres**.

4.  Sous **Connectivité de messages électroniques**, sélectionnez l’une des options suivantes.
    
      - Pour désactiver MAPI, sous **MAPI : Activé**, cliquez sur **Désactiver**.
        
        Un message d’avertissement s’affiche pour vous demander de confirmer la désactivation de MAPI. Cliquez sur **Oui**.
    
      - Pour activer MAPI, sous **MAPI : Désactivé**, cliquez sur **Activer**.

5.  Cliquez sur **Enregistrer** pour enregistrer votre modification.

## Utilisation de l'environnement de ligne de commande Exchange Management Shell pour activer ou désactiver MAPI

Dans cet exemple, nous désactivons MAPI pour la boîte aux lettres de Ken Sanchez.

    Set-CASMailbox -Identity "Ken Sanchez" -MAPIEnabled $false

Dans cet exemple, nous activons MAPI pour la boîte aux lettres d’Esther Valle.

    Set-CASMailbox -Identity "Esther Valle" -MAPIEnabled $true

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, consultez la rubrique [Set-CASMailbox](https://technet.microsoft.com/fr-fr/library/bb125264\(v=exchg.150\)).

## Comment savoir si cela a fonctionné ?

Pour vérifier que l’opération d’activation ou de désactivation de MAPI s’est effectuée correctement pour une boîte aux lettres utilisateur, exécutez l’une des actions suivantes :

  - Dans le Centre d’administration Exchange (EAC), accédez à **Destinataires** \> **Boîtes aux lettres**, cliquez sur la boîte aux lettres, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

  - Dans la page de propriétés de boîte aux lettres, cliquez sur **Fonctionnalités de boîte aux lettres**.

  - Sous **Connectivité de messages électroniques**, vérifiez si MAPI est activé ou désactivé.

Ou

  - Exécutez la commande suivante dans l’Environnement de ligne de commande Exchange Management Shell.
    
        Get-CASMailbox <identity>
    
    Si MAPI est activé, la valeur de la propriété *MapiEnabled* est `True`. Si MAPI est désactivé, la valeur est `False`.

