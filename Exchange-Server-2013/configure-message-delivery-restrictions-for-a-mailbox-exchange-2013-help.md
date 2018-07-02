---
title: 'Configurer les restrictions de remise de message pour une boîte aux lettres: Exchange 2013 Help'
TOCTitle: Configurer les restrictions de remise de message pour une boîte aux lettres
ms:assetid: c4b8b89f-3dbe-4cb8-8839-9a4e8067e00c
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb397214(v=EXCHG.150)
ms:contentKeyID: 50555486
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configurer les restrictions de remise de message pour une boîte aux lettres

 

_**Sapplique à :** Exchange Online, Exchange Server 2013_

_**Dernière rubrique modifiée :** 2012-11-29_

Le Centre d’administration Exchange ou l’environnement de ligne de commande Exchange Management Shell vous permet d’appliquer des restrictions sur la manière dont les messages sont remis à des destinataires individuels. Les restrictions de remise de messages sont utiles pour établir qui peut envoyer des messages aux utilisateurs de votre organisation. Par exemple, vous pouvez configurer une boîte aux lettres pour accepter ou refuser des messages envoyés par un utilisateur spécifique ou pour accepter des messages provenant uniquement des utilisateurs de votre organisation.

Les restrictions de remise de message présentées dans cette rubrique s’appliquent à tous les types de destinataire. Pour plus d’informations sur les différents types de destinataires, voir [Recipients](recipients-exchange-2013-help.md).

Pour les tâches supplémentaires relatives aux destinataires, consultez les rubriques suivantes :

  - [Gestion des boîtes aux lettres utilisateur](manage-user-mailboxes-exchange-2013-help.md)

  - [Création et gestion de groupes de distribution](create-and-manage-distribution-groups-exchange-2013-help.md)

  - [Gérer des groupes de distribution dynamiques](manage-dynamic-distribution-groups-exchange-2013-help.md)

  - [Gérer les utilisateurs de messagerie](manage-mail-users-exchange-2013-help.md)

  - [Gérer les contacts de messagerie](manage-mail-contacts-exchange-2013-help.md)

## Ce qu’il faut savoir avant de commencer ?

  - Durée d'exécution estimée : 5 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Section « Autorisations de configuration des destinataires » dans la rubrique [Autorisations des destinataires](recipients-permissions-exchange-2013-help.md).

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

## Utiliser le Centre d’administration Exchange pour configurer des restrictions de remise

1.  Dans le CAE, accédez à **Destinataires**  \> **Boîtes aux lettres**.

2.  Dans la liste des boîtes aux lettres utilisateurs, cliquez sur la boîte aux lettres pour laquelle vous souhaitez configurer des restrictions de remise de messages, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

3.  Dans la page de propriétés de boîte aux lettres, cliquez sur **Fonctionnalités de boîte aux lettres**.

4.  Sous **Restrictions de remise de messages**, cliquez sur **Afficher les détails** pour afficher et modifier les restrictions de remise suivantes :
    
      - **Accepter les messages provenant de**   Cette section permet de spécifier qui peut envoyer des messages à cet utilisateur.
        
          - **Tous les expéditeurs**   Cette option spécifie que l’utilisateur peut accepter des messages de tous les expéditeurs. Sont inclus à la fois les expéditeurs de votre organisation Exchange et les expéditeurs externes. Il s’agit de l’option par défaut. Elle inclut les utilisateurs externes uniquement si vous désactivez la case à cocher **Exiger l’authentification de tous les expéditeurs**. Si cette case à cocher est activée, les messages des utilisateurs externes seront rejetés.
        
          - **Uniquement les expéditeurs de la liste suivante**   Cette option spécifie que l’utilisateur ne peut accepter que des messages provenant d’un ensemble spécifique d’expéditeurs de votre organisation Exchange. Cliquez sur **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter") pour afficher la liste de tous les destinataires de votre organisation Exchange. Sélectionnez les destinataires voulus, ajoutez-les à la liste, puis cliquez sur **OK**. Vous pouvez également rechercher un destinataire spécifique en tapant son nom dans la zone de recherche et en cliquant sur **Rechercher**![Icône Recherche](images/Dn750895.773574d0-9b92-4cab-9f6b-81532c7418b9(EXCHG.150).gif "Icône Recherche").
        
          - **Exiger l’authentification de tous les expéditeurs**   Cette option empêche les utilisateurs anonymes d’envoyer des messages à l’utilisateur. Ceci inclut les utilisateurs externes qui ne font pas partie de votre organisation Exchange.
    
      - **Rejeter les messages de**   Cette section permet d’empêcher des personnes d’envoyer des messages à cet utilisateur.
        
          - **Aucun expéditeur**   Cette option spécifie que la boîte aux lettres ne doit pas refuser les messages des expéditeurs de l’organisation Exchange. Il s’agit de l’option par défaut.
        
          - **Expéditeurs de la liste suivante**   Cette option spécifie que la boîte aux lettres doit refuser les messages provenant d’un ensemble spécifique d’expéditeurs de votre organisation Exchange. Cliquez sur **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter") pour afficher la liste de tous les destinataires de votre organisation Exchange. Sélectionnez les destinataires voulus, ajoutez-les à la liste, puis cliquez sur **OK**. Vous pouvez également rechercher un destinataire spécifique en tapant son nom dans la zone de recherche et en cliquant sur **Rechercher**![Icône Recherche](images/Dn750895.773574d0-9b92-4cab-9f6b-81532c7418b9(EXCHG.150).gif "Icône Recherche").

5.  Cliquez sur **OK** pour fermer la page **Restrictions de remise de messages**, puis cliquer sur **Enregistrer** pour enregistrer vos modifications.

## Utiliser l’environnement de ligne de commande Exchange Management Shell pour configurer des restrictions de remise de message

L’exemple suivant décrit comment utiliser l’environnement de ligne de commande Exchange Management Shell pour configurer des restrictions de remise de messages pour une boîte aux lettres. Pour les autres types de destinataires, utilisez la cmdlet **Set-** correspondante avec les mêmes paramètres.

Dans cet exemple, nous configurons la boîte aux lettres de Robin Wood pour accepter uniquement les messages provenant des utilisateurs Lori Penor, Jeff Phillips et des membres du groupe de distribution Legal Team 1.

    Set-Mailbox -Identity "Robin Wood" -AcceptMessagesOnlyFrom "Lori Penor","Jeff Phillips" -AcceptMessagesOnlyFromDLMembers "Legal Team 1"

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Si vous configurez une boîte aux lettres pour qu’elle accepte uniquement des messages provenant d’expéditeurs individuels, vous devez utiliser le paramètre <em>AcceptMessagesOnlyFrom</em>. Si vous configurez une boîte aux lettres pour qu’elle accepte uniquement des messages provenant d’expéditeurs membres d’un groupe de distribution spécifique, utilisez le paramètre <em>AcceptMessagesOnlyFromDLMembers</em>.</td>
</tr>
</tbody>
</table>


Dans cet exemple, nous ajoutons l’utilisateur David Pelton à la liste des utilisateurs dont les messages doivent être acceptés par la boîte aux lettres de Robin Wood.

    Set-Mailbox -Identity "Robin Wood" -AcceptMessagesOnlyFrom @{add="David Pelton"}

Dans cet exemple, nous configurons la boîte aux lettres de Robin Wood pour exiger que tous les expéditeurs soient authentifiés. En d’autres termes, la boîte aux lettres ne doit accepter que des messages envoyés par d’autres utilisateurs de votre organisation Exchange.

    Set-Mailbox -Identity "Robin Wood" -RequireSenderAuthenticationEnabled $true

Dans cet exemple, nous configurons la boîte aux lettres de Robin Wood pour refuser les messages provenant des utilisateurs Joe Healy, Terry Adams et des membres du groupe de distribution Legal Team 2.

    Set-Mailbox -Identity "Robin Wood" -RejectMessagesFrom "Joe Healy","Terry Adams" -RejectMessagesFromDLMembers "Legal Team 2"

Dans cet exemple, nous configurons la boîte aux lettres de Robin Wood pour refuser également des messages envoyés par des membres du groupe Legal Team 3.

    Set-Mailbox -Identity "Robin Wood" -RejectMessagesFromDLMembers @{add="Legal Team 3"}

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Si vous configurez une boîte aux lettres pour qu’elle refuse des messages provenant d’expéditeurs individuels, vous devez utiliser le paramètre <em>RejectMessagesFrom</em>. Si vous configurez une boîte aux lettres pour qu’elle refuse des messages provenant d’expéditeurs membres d’un groupe de distribution spécifique, utilisez le paramètre <em>RejectMessagesFromDLMembers</em>.</td>
</tr>
</tbody>
</table>


Pour plus d’informations sur la syntaxe et les paramètres relatifs à la configuration des restrictions de remise pour différents types de destinataires, consultez les rubriques suivantes :

  - [Set-DistributionGroup](https://technet.microsoft.com/fr-fr/library/bb124955\(v=exchg.150\))

  - [Set-DynamicDistributionGroup](https://technet.microsoft.com/fr-fr/library/bb123796\(v=exchg.150\))

  - [Set-Mailbox](https://technet.microsoft.com/fr-fr/library/bb123981\(v=exchg.150\))

  - [Set-MailContact](https://technet.microsoft.com/fr-fr/library/aa995950\(v=exchg.150\))

  - [Set-MailUser](https://technet.microsoft.com/fr-fr/library/aa995971\(v=exchg.150\))

## Comment savoir si cela a fonctionné ?

Pour vérifier que la configuration des restrictions de remise de messages a été correctement effectuée pour une boîte aux lettres utilisateur, effectuez l’une des opérations suivantes :

1.  Dans le CAE, accédez à **Destinataires**  \> **Boîtes aux lettres**.

2.  Dans la liste des boîtes aux lettres utilisateurs, cliquez sur la boîte aux lettres pour laquelle vous souhaitez vérifier les restrictions de remise de messages, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

3.  Dans la page de propriétés de boîte aux lettres, cliquez sur **Fonctionnalités de boîte aux lettres**.

4.  Sous **Restrictions de remise de messages**, cliquez sur **Afficher les détails** pour vérifier les restrictions de remise pour la boîte aux lettres :

Ou

Exécutez la commande suivante dans l’environnement de ligne de commande Exchange Management Shell.

    Get-Mailbox <identity> | fl AcceptMessagesOnlyFrom,AcceptMessagesOnlyFromDLMembers,RejectMessagesFrom,RejectMessagesFromDLMembers,RequireSenderAuthenticationEnabled

