---
title: 'Ajouter un numéro E.164: Exchange 2013 Help'
TOCTitle: Ajouter un numéro E.164
ms:assetid: fab86207-be03-40ef-9fea-045a50f3d122
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ662762(v=EXCHG.150)
ms:contentKeyID: 50555517
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Ajouter un numéro E.164

 

_**Sapplique à :** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2012-11-14_

Lorsque vous activez un utilisateur pour la messagerie unifiée et l’associez à un plan de numérotation E.164, deux adresses proxy EUM sont créées : l’une contient le numéro de poste de l’utilisateur et l’autre, le numéro E.164 de l’utilisateur. Le numéro de poste est utilisé lorsque l’utilisateur appelle un numéro Outlook Voice Access.

Le numéro E.164 principal que vous avez ajouté lorsque l’utilisateur a été activé pour la messagerie unifiée sera répertorié en tant qu’adresse proxy EUM principale. Si le numéro E.164 principal a été supprimé, la première adresse proxy EUM ajoutée qui contient le numéro E.164 de l’utilisateur est répertoriée comme adresse proxy EUM principale. Tous les numéros E.164 supplémentaires que vous ajoutez sont répertoriés en tant qu’adresses proxy EUM secondaires. Lorsque des numéros E.164 secondaires supplémentaires sont ajoutés, les appelants peuvent laisser des messages vocaux à tous les numéros E.164 de l’utilisateur qui ont été définis. Tous les messages vocaux sont remis dans la même boîte aux lettres de l’utilisateur.

Vous pouvez ajouter un numéro E.164 principal ou secondaire pour un utilisateur à l’aide du Centre d’administration Exchange ou de l’environnement de ligne de commande Exchange Management Shell. Vous pouvez utiliser la page **Adresse de messagerie** sur la boîte aux lettres de l’utilisateur dans le CAE pour ajouter un numéro E.164 principal ou secondaire. Il n’est pas possible d’utiliser la page **Boîte aux lettres de messagerie unifiée** du CAE pour ajouter un numéro E.164 principal ou secondaire.

Vous pouvez afficher les numéros E.164 principaux ou secondaires d’un utilisateur à l’aide de la cmdlet **Get-UMMailbox** ou de la cmdlet **Get-Mailbox** de l’environnement de ligne de commande Exchange Management Shell.

Pour d’autres tâches de gestion relatives aux utilisateurs activés pour la messagerie vocale, consultez la rubrique [Voix des procédures de l'utilisateur à extension messagerie](voice-mail-enabled-user-procedures-exchange-2013-help.md).

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : 3 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Boîtes aux lettres de messagerie unifiée » dans la rubrique [Autorisations de messagerie unifiée](unified-messaging-permissions-exchange-2013-help.md).

  - Avant d’effectuer ces procédures, vérifiez qu’un plan de numérotation de messagerie unifiée E.164 a été créé. Pour obtenir la procédure détaillée, consultez la rubrique [Créer un plan de numérotation de messagerie unifiée](create-a-um-dial-plan-exchange-2013-help.md).

  - Avant d’effectuer ces procédures, vérifiez qu’une stratégie de boîte aux lettres de messagerie unifiée a été créée. Pour obtenir la procédure détaillée, consultez la rubrique [Créer une stratégie de boîte aux lettres de messagerie unifiée](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Avant d’effectuer ces procédures, vérifiez que la boîte aux lettres de l’utilisateur a été activée pour la messagerie unifiée et qu’elle est associée à un plan de numérotation E.164. Pour obtenir la procédure détaillée, consultez la rubrique [Activation de la messagerie vocale pour un utilisateur](enable-a-user-for-voice-mail-exchange-2013-help.md).

  - Avant d’exécuter ces procédures, vérifiez que le numéro E.164 qui doit être affecté à l’utilisateur est valide et formaté correctement.

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

## Utiliser le Centre d’administration Exchange pour ajouter un numéro E.164 principal ou secondaire

1.  Dans le CAE, accédez à **Destinataires**  \> **Boîtes aux lettres**.

2.  Dans l’affichage de liste, sélectionnez la boîte aux lettres pour laquelle vous voulez ajouter un numéro E.164, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

3.  Sur la page **Boîte aux lettres de l’utilisateur**, sous **Adresse de messagerie**, cliquez sur **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter").

4.  Sur la page **Nouvelle adresse de messagerie**, sélectionnez **EUM** (messagerie unifiée Exchange), puis dans la zone **Adresse/Poste**, entrez le nouveau numéro E.164 pour l’utilisateur.

5.  Sur la page **Nouvelle adresse de messagerie**, sous **Plan de numérotation**, cliquez sur **Parcourir** pour sélectionner le plan de numérotation E.164, puis cliquez sur **OK**.

6.  Cliquez sur **Enregistrer**.

## Utiliser l’environnement de ligne de commande Exchange Management Shell pour ajouter un numéro E.164

Cet exemple illustre l’ajout d’un numéro E.164 pour Tony Smith, un utilisateur à extension messagerie unifiée.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Avant d’ajouter un numéro E.164 à l’aide de l’environnement de ligne de commande Exchange Management Shell, vous devez déterminer la position de l’adresse proxy EUM à ajouter. Pour cela, exécutez la commande <strong>$mbx.EmailAddresses</strong>. La première adresse proxy dans la liste est 0.</td>
</tr>
</tbody>
</table>


    $mbx=Get-Mailbox tony.smith
    $mbx.EmailAddresses.Item(2)="eum:+14255550123;phone-context=MyDialPlan.contoso.com"
    Set-Mailbox tony.smith -EmailAddresses $mbx.EmailAddresses

