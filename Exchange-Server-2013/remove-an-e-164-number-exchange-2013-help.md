---
title: 'Supprimer un numéro E.164: Exchange 2013 Help'
TOCTitle: Supprimer un numéro E.164
ms:assetid: 17941918-7dc5-41a0-b540-09f2f907362b
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ662759(v=EXCHG.150)
ms:contentKeyID: 50555351
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Supprimer un numéro E.164

 

_**Sapplique à :** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2012-11-14_

Lorsque vous activez un utilisateur pour la messagerie unifiée et l’associez à un plan de numérotation E.164, deux adresses proxy EUM sont créées : l’une contient le numéro de poste de l’utilisateur et l’autre, le numéro E.164 de l’utilisateur. Le numéro de poste est utilisé lorsque l’utilisateur appelle un numéro Outlook Voice Access.

Vous pouvez supprimer le numéro E.164 principal qui a été ajouté lorsque l’utilisateur a été activé pour la messagerie unifiée ou un numéro E.164 secondaire ajouté ultérieurement, ainsi que les adresses proxy EUM de l’utilisateur. Le numéro E.164 principal que vous avez ajouté lorsque l’utilisateur a été activé pour la messagerie unifiée est répertorié en tant qu’adresse proxy EUM principale. Tous les numéros E.164 supplémentaires que vous avez ajoutés sont répertoriés en tant qu’adresses proxy EUM secondaires. Lorsqu’un numéro E.164 est supprimé, les appelants ne peuvent plus laisser de messages vocaux à l’utilisateur au numéro E.164 qui a été supprimé.

Si vous supprimez le numéro E.164 principal, la messagerie unifiée ne peut pas transférer de messages vocaux vers la boîte aux lettres de l’utilisateur et les règles de répondeur automatique ne sont pas traitées. Après avoir supprimé le numéro E.164 principal, l’adresse proxy EUM de l’utilisateur apparaît comme **Nulle** dans la boîte aux lettres de l’utilisateur dans le CAE et lors de l’exécution de la cmdlet **Get-Mailbox** de l’environnement de ligne de commande Exchange Management Shell. Aussi, lorsque vous exécutez la cmdlet **Get-UMMailbox**, les paramètres *Extensions*, *PhoneNumber* et *CallAnsweringRulesExtensions* sont vides ou nuls.

Vous pouvez supprimer un numéro E.164 principal ou secondaire pour un utilisateur à l’aide du Centre d’administration Exchange ou de l’environnement de ligne de commande Exchange Management Shell. Vous pouvez utiliser la page **Adresse de messagerie** sur la boîte aux lettres de l’utilisateur dans le CAE pour supprimer un numéro E.164 principal ou secondaire. Il n’est pas possible d’utiliser la page **Boîte aux lettres de messagerie unifiée** du CAE pour supprimer un numéro E.164 principal ou secondaire.

Vous pouvez afficher les numéros E.164 principaux ou secondaires d’un utilisateur à l’aide de la cmdlet **Get-UMMailbox** ou de la cmdlet **Get-Mailbox** de l’environnement de ligne de commande Exchange Management Shell.

Pour d’autres tâches de gestion relatives aux utilisateurs activés pour la messagerie vocale, consultez la rubrique [Voix des procédures de l'utilisateur à extension messagerie](voice-mail-enabled-user-procedures-exchange-2013-help.md).

## Ce qu’il faut savoir avant de commencer ?

  - Durée d'exécution estimée : 3 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Boîtes aux lettres de messagerie unifiée » dans la rubrique [Autorisations de messagerie unifiée](unified-messaging-permissions-exchange-2013-help.md).

  - Avant d’effectuer cette procédure, vérifiez qu’un plan de numérotation de messagerie unifiée E.164 a été créé. Pour obtenir la procédure détaillée, consultez la rubrique [Créer un plan de numérotation de messagerie unifiée](create-a-um-dial-plan-exchange-2013-help.md).

  - Avant d’effectuer cette procédure, vérifiez qu’une stratégie de boîte aux lettres de messagerie unifiée a été créée. Pour obtenir la procédure détaillée, consultez la rubrique [Créer une stratégie de boîte aux lettres de messagerie unifiée](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Avant d’effectuer ces procédures, vérifiez que la boîte aux lettres de l’utilisateur a été activée pour la messagerie unifiée et qu’elle est associée à un plan de numérotation E.164. Pour obtenir la procédure détaillée, consultez la rubrique [Activation de la messagerie vocale pour un utilisateur](enable-a-user-for-voice-mail-exchange-2013-help.md).

  - Avant d’effectuer ces procédures, vérifiez que les numéros E.164 principaux et secondaires sont configurés pour l’utilisateur.

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

## Suppression du numéro E.164 principal ou d’un numéro E.164 secondaire à l’aide du Centre d’administration Exchange (CAE)

1.  Dans le CAE, accédez à **Destinataires**  \> **Boîtes aux lettres**.

2.  Dans la liste affichée, sélectionnez la boîte aux lettres dont vous souhaitez supprimer un numéro E.164, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

3.  Sur la page **Boîte aux lettres utilisateur**, sous **Adresse de messagerie**, sélectionnez le numéro E.164 que vous souhaitez supprimer de la liste, puis cliquez sur **Supprimer**![Icône Supprimer](images/Dd979797.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "Icône Supprimer"). L’adresse proxy EUM principale ou le numéro E.164 apparaît en chiffres et en lettres gras.

4.  Cliquez sur **Enregistrer**.

## Suppression du numéro E.164 principal ou d’un numéro E.164 secondaire à l’aide de l’environnement de ligne de commande Exchange Management Shell

Cet exemple montre comment supprimer le numéro E.164 +14255551010 de la boîte aux lettres de Tony Smith, un utilisateur à extension messagerie unifiée.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Avant de supprimer un numéro E.164 à l’aide de l’environnement de ligne de commande Exchange Management Shell, vous devez déterminer la position de l’adresse proxy EUM que vous souhaitez modifier. Pour cela, exécutez la commande <strong>$mbx.EmailAddresses</strong>. La première adresse proxy EUM de la liste est 0.</td>
</tr>
</tbody>
</table>


    $mbx = Get-Mailbox tony.smith
    $mbx.EmailAddresses.Item(1) -="eum:+14255551010;phone-context=MyDialPlan.contoso.com"
    Set-Mailbox tony.smith -EmailAddresses $mbx.EmailAddresses

