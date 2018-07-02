---
title: 'Activer ou désactiver Exchange ActiveSync pour une boîte aux lettres: Exchange 2013 Help'
TOCTitle: Activer ou désactiver Exchange ActiveSync pour une boîte aux lettres
ms:assetid: dcf7c05b-b1b9-4b0f-800d-fec9f2ddc9e4
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb124809(v=EXCHG.150)
ms:contentKeyID: 50555502
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Activer ou désactiver Exchange ActiveSync pour une boîte aux lettres

 

_**Sapplique à :** Exchange Online, Exchange Server 2013_

_**Dernière rubrique modifiée :** 2012-11-13_

Vous pouvez utiliser le Centre d’administration Exchange ou l’environnement de ligne de commande Exchange Management Shell pour activer ou désactiver Microsoft Exchange ActiveSync pour une boîte aux lettres utilisateur. Exchange ActiveSync est un protocole client qui permet à des utilisateurs de synchroniser un appareil mobile avec sa boîte aux lettres Exchange. Exchange ActiveSync est activé par défaut lorsqu’une boîte aux lettres utilisateur est créée. Pour en savoir plus, consultez la rubrique [Exchange ActiveSync](exchange-activesync-exchange-2013-help.md).

## Ce qu’il faut savoir avant de commencer ?

  - Durée d'exécution estimée : 2 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Paramètres Exchange ActiveSync » dans la rubrique [Autorisations des clients et des périphériques mobiles](clients-and-mobile-devices-permissions-exchange-2013-help.md).

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

## Utiliser le Centre d’administration Exchange pour activer ou désactiver Exchange ActiveSync

1.  Dans le CAE, accédez à **Destinataires**  \> **Boîtes aux lettres**.

2.  Dans la liste des boîtes aux lettres utilisateur, cliquez sur la boîte aux lettres pour laquelle vous souhaitez activer ou désactiver Exchange ActiveSync, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

3.  Dans la page de propriétés de boîte aux lettres, cliquez sur **Fonctionnalités de boîte aux lettres**.

4.  Sous **Appareils mobiles**, sélectionnez l’une des options suivantes :
    
      - Pour désactiver Exchange ActiveSync cliquez sur **Désactiver ActiveSync Exchange**.
        
        Un message d’avertissement s’affiche pour vous demander de confirmer la désactivation de Exchange ActiveSync. Cliquez sur **Oui**.
    
      - Pour activer Exchange ActiveSync, cliquez **Activer Exchange ActiveSync**.

5.  Cliquez sur **Enregistrer** pour enregistrer votre modification.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Vous pouvez activer ou désactiver Exchange ActiveSync pour plusieurs boîtes aux lettres utilisateur à l’aide de la fonction de modification en bloc du Centre d’administration Exchange (EAC). Pour plus d’informations sur comment procéder, consultez la section « Modifier en bloc des boîtes aux lettres utilisateur » dans <a href="manage-user-mailboxes-exchange-2013-help.md">Gestion des boîtes aux lettres utilisateur</a>.</td>
</tr>
</tbody>
</table>


## Utiliser l’environnement de ligne de commande Exchange Management Shell pour activer ou désactiver Exchange ActiveSync

Dans cet exemple, nous désactivons Exchange ActiveSync pour la boîte aux lettres de Yan Li.

    Set-CASMailbox -Identity "Yan Li" -ActiveSyncEnabled $false

Dans cet exemple, nous activons Exchange ActiveSync pour la boîte aux lettres d’Elly Nkya.

    Set-CASMailbox -Identity Ellyn@contoso.com -ActiveSyncEnabled $true

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Set-CASMailbox](https://technet.microsoft.com/fr-fr/library/bb125264\(v=exchg.150\)).

## Comment savoir si cela a fonctionné ?

Pour vérifier que l’opération d’activation ou de désactivation de Exchange ActiveSync s’est effectuée correctement pour une boîte aux lettres utilisateur, exécutez l’une des actions suivantes :

  - Dans le Centre d’administration Exchange (EAC), accédez à **Destinataires** \> **Boîtes aux lettres**, cliquez sur la boîte aux lettres, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

  - Dans la page de propriétés de boîte aux lettres, cliquez sur **Fonctionnalités de boîte aux lettres**.

  - Sous **Appareils mobiles**, vérifiez si Exchange ActiveSync est activé ou désactivé.

Ou

  - Exécutez la commande suivante dans l’environnement de ligne de commande Exchange Management Shell.
    
        Get-CASMailbox <identity>
    
    Si Exchange ActiveSync est activé, la valeur pour la propriété *ActiveSyncEnabled* est `True`. Si Exchange ActiveSync est désactivé, la valeur est `False`.

