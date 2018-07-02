---
title: 'Activer ou désactiver l’accès POP3 pour un utilisateur: Exchange 2013 Help'
TOCTitle: Activer ou désactiver l’accès POP3 pour un utilisateur
ms:assetid: 57e12f07-3b14-45bd-9a82-e6032d14214f
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb691018(v=EXCHG.150)
ms:contentKeyID: 50478136
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Activer ou désactiver l’accès POP3 pour un utilisateur

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2014-01-06_

Vous pouvez activer ou désactiver l’accès POP3 pour un utilisateur.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Après avoir activé ou désactivé l’accès POP3 pour un utilisateur, vous devez redémarrer le service Microsoft Exchange POP3 et le service de serveur principal Microsoft Exchange POP3. Pour plus d’informations sur le redémarrage du service POP3, consultez la rubrique <a href="start-and-stop-the-pop3-services-exchange-2013-help.md">Démarrage et arrêt des services POP3</a>.</td>
</tr>
</tbody>
</table>


Pour plus d’informations sur la gestion des boîtes aux lettres utilisateur, reportez-vous à la rubrique [Gestion des boîtes aux lettres utilisateur](manage-user-mailboxes-exchange-2013-help.md).

Pour plus d’informations sur POP3 et IMAP4, voir [POP3 et IMAP4 dans Exchange Server 2013](pop3-and-imap4-in-exchange-server-2013-exchange-2013-help.md).

## Ce qu’il faut savoir avant de commencer ?

  - Durée d'exécution estimée : 2 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez la section « Autorisations de configuration des destinataires » dans la rubrique [Autorisations des destinataires](recipients-permissions-exchange-2013-help.md).

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

## Utiliser le centre d'administration Exchange pour activer ou désactiver l’accès POP3 pour un utilisateur

1.  Dans le CAE, accédez à **Destinataires**  \> **Boîtes aux lettres**.

2.  Dans le volet Résultats, sélectionnez l’utilisateur pour lequel vous souhaitez activer ou désactiver l'accès POP3, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

3.  Dans la boîte de dialogue **Boîte aux lettres utilisateur**, dans l’arborescence de la console, cliquez sur **Fonctionnalités de boîte aux lettres**.
    
    Dans le volet Résultats, sous **Connectivité de messagerie**, effectuez l’une des opérations suivantes :
    
      - Pour désactiver l'accès POP3 pour l'utilisateur, sous **POP3 : Activé**, cliquez sur **Désactiver**.
    
      - Pour activer l'accès POP3 pour l'utilisateur, sous **POP3 : Désactivé**, cliquez sur **Activer**.

4.  Cliquez sur **Enregistrer**.

## Utiliser l’environnement Shell pour activer ou désactiver l’accès POP3 pour un utilisateur

Cet exemple montre comment activer l’accès POP3 pour l’utilisateur Patrick Colon.

    Set-CASMailbox -Identity "John Smith" -POPEnabled $true

Cet exemple montre comment désactiver l’accès POP3 pour l’utilisateur Patrick Colon.

    Set-CASMailbox -Identity "John Smith" -POPEnabled $false

## Comment savoir si cela a fonctionné ?

1.  Dans le CAE, accédez à **Destinataires**  \> **Boîtes aux lettres**.

2.  Dans le volet Résultats, sélectionnez l’utilisateur pour lequel vous souhaitez activer ou désactiver l’accès POP3, puis cliquez sur **Modifier**.

3.  Dans la boîte de dialogue **Boîte aux lettres utilisateur**, dans l’arborescence de la console, cliquez sur **Fonctionnalités de boîte aux lettres**.
    
    Dans le volet Résultats, examinez le champ **Connectivité de messagerie**.
    
      - Si POP3 est activé pour l'utilisateur, vous verrez **POP3 : Activé**.
    
      - Si POP3 est désactivé pour l’utilisateur, vous verrez **POP3 : Désactivé**.

4.  Cliquez sur **Enregistrer**.

