---
title: 'Supprimer un numéro de poste: Exchange 2013 Help'
TOCTitle: Supprimer un numéro de poste
ms:assetid: c2b896cf-21f7-4453-a4e6-b23d236a6dd3
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dd351124(v=EXCHG.150)
ms:contentKeyID: 50555490
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Supprimer un numéro de poste

 

_**Sapplique à :** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2016-07-21_

Lorsque vous activez un utilisateur pour la messagerie unifiée et l’associez à un plan de numérotation de postes téléphoniques, une adresse proxy EUM contenant le numéro de poste de l’utilisateur est créée pour ce dernier. Vous devez définir au moins un numéro de poste pour la messagerie unifiée à utiliser afin que la messagerie vocale puisse être transférée vers la boîte aux lettres de l’utilisateur. Le numéro de poste est également utilisé lorsque l’utilisateur appelle un numéro Outlook Voice Access.

Vous pouvez supprimer le numéro de poste principal qui a été ajouté lors de l’activation de l’utilisateur pour la messagerie unifiée ou un numéro de poste secondaire qui a été ajouté par la suite pour l’utilisateur, avec les adresses proxy de messagerie unifiée Exchange associées. Le numéro de poste principal que vous avez ajouté lorsque que l’utilisateur a été activé pour la messagerie unifiée doit être répertorié en tant qu’adresse proxy principale de messagerie unifiée Exchange. Tous les numéros de poste supplémentaires que vous avez ajoutés doivent être répertoriés en tant qu’adresses proxy de messagerie unifiée Exchange secondaires. Lorsqu’un numéro de poste est supprimé, les appelants ne peuvent plus laisser de message vocal à l’utilisateur pour lequel le numéro de poste a été supprimé.

Si vous supprimez le numéro de poste principal, la messagerie unifiée n’est plus en mesure d’envoyer de messages vocaux dans la boîte aux lettres de l’utilisateur et les règles de répondeur automatique ne sont pas traitées. Après la suppression du numéro de poste principal, l’adresse proxy de messagerie unifiée Exchange de l’utilisateur doit être répertoriée comme **Null** au niveau de la boîte aux lettres de l’utilisateur dans le Centre d’administration Exchange (EAC) et lorsque vous exécutez la cmdlet **Get-Mailbox** dans l’environnement de ligne de commande Exchange Management Shell. De même, lorsque vous exécutez la cmdlet **Get-UMMailbox**, les paramètres *Extensions*, *PhoneNumber* et *CallAnsweringRulesExtensions* doivent être à blanc ou à la valeur « null ».

Vous pouvez utiliser le Centre d’administration Exchange (EAC) ou l’environnement de ligne de commande Exchange Management Shell pour supprimer un numéro de poste principal ou secondaire. Vous pouvez utiliser la page **Adresse de messagerie** de la boîte aux lettres de l’utilisateur dans le Centre d’administration Exchange (EAC) pour supprimer un numéro de poste principal ou secondaire. Vous ne pouvez pas utiliser la page **Boîte aux lettres de messagerie unifiée** du Centre d’administration Exchange (EAC) pour supprimer un numéro de poste principal, en revanche vous pouvez l’utiliser pour supprimer un numéro de poste secondaire.

Vous pouvez afficher le numéro de poste principal et le numéro de poste secondaire d’un utilisateur à l’aide de la cmdlet **Get-UMMailbox** ou de la cmdlet **Get-Mailbox** dans l’environnement de ligne de commande Exchange Management Shell.

Pour les autres tâches de gestion relatives aux utilisateurs qui sont activées pour la messagerie vocale, voir [Voix des procédures de l'utilisateur à extension messagerie](voice-mail-enabled-user-procedures-exchange-2013-help.md).

## Ce qu’il faut savoir avant de commencer ?

  - Durée d'exécution estimée : 3 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Boîtes aux lettres de messagerie unifiée » dans la rubrique [Autorisations de messagerie unifiée](unified-messaging-permissions-exchange-2013-help.md).

  - Avant d'effectuer cette procédure, vérifiez qu'un plan de numérotation de messagerie unifiée a été créé. Pour obtenir la procédure détaillée, consultez la rubrique [Créer un plan de numérotation de messagerie unifiée](create-a-um-dial-plan-exchange-2013-help.md).

  - Avant d’effectuer cette procédure, vérifiez qu’une stratégie de boîte aux lettres de messagerie unifiée a été créée. Pour obtenir la procédure détaillée, consultez la rubrique [Créer une stratégie de boîte aux lettres de messagerie unifiée](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Avant d’exécuter ces procédures, vérifiez que la boîte aux lettres de l’utilisateur est activée pour la messagerie unifiée et qu’elle est liée à un plan de numérotation de numéro de poste. Pour obtenir la procédure détaillée, consultez la rubrique [Activation de la messagerie vocale pour un utilisateur](enable-a-user-for-voice-mail-exchange-2013-help.md).

  - Avant d’exécuter ces procédures, vérifiez que le numéro de poste principal et le numéro de poste secondaire sont bien configurés pour l’utilisateur.

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

## Utiliser le Centre d’administration Exchange pour supprimer le numéro de poste principal ou secondaire

1.  Dans le CAE, accédez à **Destinataires**  \> **Boîtes aux lettres**.

2.  Dans l’affichage de liste, sélectionnez la boîte aux lettres dans laquelle vous voulez supprimer un numéro de poste, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

3.  Sur la page **Boîte aux lettres de l’utilisateur**, sous **Adresse de messagerie**, sélectionnez le numéro de poste à supprimer de la liste, puis cliquez sur **Supprimer**![Icône Supprimer](images/Dd979797.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "Icône Supprimer"). L’adresse proxy de messagerie unifiée Exchange ou le numéro de poste principal est répertorié en caractères gras.

4.  Cliquez sur **Enregistrer**.

## Utiliser le Centre d’administration Exchange pour supprimer un numéro de poste secondaire

1.  Dans le CAE, accédez à **Destinataires**  \> **Boîtes aux lettres**.

2.  Dans l’affichage de liste, sélectionnez l’utilisateur pour lequel vous voulez supprimer un numéro de poste dans la boîte aux lettres.

3.  Dans le volet d’informations, sous **Fonctions de téléphone et de voix** \> **Messagerie unifiée**, cliquez sur**Afficher les détails**.

4.  Sur la page **Autres postes**, dans la zone **Numéro de poste**, sélectionnez le numéro de poste que vous voulez supprimer, puis cliquez sur **Supprimer**![Icône Supprimer](images/Dd979797.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "Icône Supprimer").

5.  Cliquez sur **Enregistrer**.

## Utiliser l’environnement de ligne de commande Exchange Management Shell pour supprimer un numéro de poste

Cet exemple supprime le numéro de poste 12345 de la boîte aux lettres de Jean-Charles Colon, un utilisateur à messagerie unifiée.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Avant de supprimer un numéro de poste à l’aide de l’environnement de ligne de commande Exchange Management Shell, vous devez déterminer la position de l’adresse proxy de messagerie unifiée Exchange que vous souhaitez modifier. Pour déterminer la position, utilisez la commande <strong>$mbx.EmailAddresses</strong>. La première adresse proxy de messagerie unifiée Exchange de la liste doit être 0.</td>
</tr>
</tbody>
</table>


    $mbx = Get-Mailbox tony.smith
    $mbx.EmailAddresses.remove("eum:22222;phone-context=MyDialPlan.contoso.com") 
    Set-Mailbox tony.smith -EmailAddresses $mbx.EmailAddresses

