---
title: 'Gestion des autorisations des destinataires: Exchange 2013 Help'
TOCTitle: Gestion des autorisations des destinataires
ms:assetid: 749cdfe3-496b-453f-96eb-20a0bf28fd52
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ919240(v=EXCHG.150)
ms:contentKeyID: 51407118
ms.date: 05/05/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Gestion des autorisations des destinataires

 

_**Sapplique à :** Exchange Online, Exchange Server 2013_

_**Dernière rubrique modifiée :** 2018-04-20_

Vous pouvez utiliser le CAE ou l'environnement de ligne de commande pour attribuer à des utilisateurs ou à des groupes (appelés *délégués*) des autorisations leur permettant d'ouvrir ou d'envoyer des messages à partir d'autres boîtes aux lettres. Des autorisations peuvent être attribuées à des boîtes aux lettres utilisateur, à des boîtes aux lettres associées, à des boîtes aux lettres de ressources et à des boîtes aux lettres partagées. Vous pouvez également attribuer des autorisations à des groupes de distribution, à des groupes de distribution dynamique et à des groupes de sécurité à extension messagerie pour permettre à des délégués d'envoyer des messages de la part de ces groupes. Vous pouvez attribuer à des délégués les autorisations suivantes pour accéder à des boîtes aux lettres ou envoyer des messages de la part de boîtes aux lettres ou de groupes :

  - **Accès total**   Cette autorisation permet à un délégué d’ouvrir la boîte aux lettres d’un utilisateur et d’accéder à son contenu. Toutefois, l'attribution de l'autorisation Accès total ne permet pas au délégué d'envoyer du courrier à partir de la boîte aux lettres. Pour permettre au délégué d'expédier du courrier, vous devez lui attribuer l'autorisation Envoyer en tant que ou Envoyer de la part de.
    
    L'autorisation Accès total n'est pas disponible lors de la configuration d'autorisations pour des groupes.

  - **Envoyer en tant que**   Cette autorisation permet aux délégués d'utiliser la boîte aux lettres pour envoyer des messages. Une fois cette autorisation attribuée à un délégué, tout message envoyé par un délégué à partir de la boîte aux lettres s'affiche comme s'il était envoyé par le propriétaire de la boîte aux lettres. Toutefois, cette autorisation ne permet pas à un délégué de se connecter à la boîte aux lettres de l’utilisateur. Elle permet uniquement aux utilisateurs d'ouvrir la boîte aux lettres. Si cette autorisation est attribuée à un groupe, un message envoyé par le délégué s'affiche comme s'il était envoyé par le groupe.

  - **Envoyer de la part de**   Cette autorisation permet également à un délégué d'utiliser la boîte aux lettres pour envoyer des messages. Lorsque cette autorisation est attribuée à un délégué, l'adresse **De** figurant dans tout message expédié par le délégué indique que ce message a été envoyé par le délégué de la part du propriétaire de la boîte aux lettres.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Si vous attribuez l’autorisation Accès total, Envoyer en tant que ou Envoyer de la part de pour accéder à une boîte aux lettres masquée dans les listes d’adresses, le délégué ne peut pas ouvrir cette boîte aux lettres ni envoyer de messages.</td>
</tr>
</tbody>
</table>


## Ce qu’il faut savoir avant de commencer ?

  - Durée d'exécution estimée de chaque procédure : 2 minutes.

  - Les procédures décrites dans cette rubrique requièrent des autorisations spécifiques. Consultez chaque procédure pour savoir quelles autorisations sont nécessaires.

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

## Attribuer des autorisations à une boîte aux lettres

Comme indiqué précédemment, vous pouvez attribuer des autorisations à des boîtes aux lettres utilisateur, à des boîtes aux lettres associées, à des boîtes aux lettres de ressources et à des boîtes aux lettres partagées. Vous pouvez également utiliser l'environnement de ligne de commande pour attribuer à des délégués des autorisations leur permettant d'accéder à une boîte aux lettres de découverte.

Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Autorisations et délégation » dans la section « Autorisations de configuration des destinataires » de la rubrique [Autorisations des destinataires](recipients-permissions-exchange-2013-help.md).

## Utiliser le CAE pour attribuer des autorisations

La procédure suivante explique comment attribuer des autorisations à une boîte aux lettres utilisateur. Une procédure similaire permet d'attribuer des autorisations à des boîtes aux lettres de ressources ou partagées en accédant à la page **Ressources** ou **Partagées** dans le CAE, puis en sélectionnant la boîte aux lettres à laquelle attribuer les autorisations.

1.  Dans le CAE, accédez à **Destinataires**  \> **Boîtes aux lettres**.

2.  Dans la liste des boîtes aux lettres, cliquez sur celle pour laquelle vous voulez attribuer des autorisations, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

3.  Dans la page des propriétés de boîte aux lettres, cliquez sur **Délégation de boîte aux lettres**.

4.  Pour attribuer des autorisations à des délégués, cliquez sur **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter") sous l'autorisation voulue afin d'afficher une page qui présente la liste de tous les destinataires de votre organisation Exchange auxquels l'autorisation peut être attribuée. Sélectionnez les destinataires de votre choix, ajoutez-les à la liste, puis cliquez sur **OK**. Vous pouvez également rechercher un destinataire spécifique en tapant son nom dans la zone de recherche et en cliquant sur **Rechercher**![Icône Recherche](images/Dn750895.773574d0-9b92-4cab-9f6b-81532c7418b9(EXCHG.150).gif "Icône Recherche").
    
    Pour retirer une autorisation à un destinataire, sous l'autorisation en question, sélectionnez le destinataire, puis cliquez sur **Supprimer**![Icône Suppression](images/Dd362328.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "Icône Suppression").

5.  Cliquez sur **Enregistrer** pour enregistrer vos modifications.

## Utiliser le CAE pour attribuer des autorisations en bloc

Procédez comme suit pour attribuer des autorisations en bloc.

1.  Dans le CAE, accédez à **Destinataires**  \> **Boîtes aux lettres**.

2.  Sélectionnez les boîtes aux lettres auxquelles vous souhaitez attribuer des autorisations.

3.  Cliquez ou appuyez sur **Options supplémentaires** dans le volet droit, puis sous **Délégation de boîte aux lettres**, sélectionnez **Ajouter**.

4.  Sur la page **Délégation d’ajout en bloc**, cliquez ou appuyez sur **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter") sous l’autorisation appropriée pour afficher une page qui répertorie tous les destinataires de votre organisation Exchange auxquels l’autorisation peut être attribuée. Sélectionnez les destinataires que vous souhaitez, ajoutez-les à la liste, puis cliquez sur **OK**.
    
    Pour retirer une autorisation à des destinataires, sous l’autorisation en question, sélectionnez les destinataires, puis cliquez sur **Supprimer**![Icône Suppression](images/Dd362328.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "Icône Suppression").

## Utiliser le CAE pour attribuer une autorisation utilisateur afin d’envoyer un courrier électronique à partir de la boîte aux lettres d’un autre utilisateur

La procédure suivante montre comment attribuer une autorisation utilisateur pour envoyer un courrier électronique à partir de la boîte aux lettres d’un autre utilisateur.

1.  Dans le CAE, accédez à **Destinataires** \> **Boîtes aux lettres**.

2.  Dans la liste des boîtes aux lettres, cliquez sur celle pour laquelle vous voulez attribuer des autorisations Envoyer en tant que, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

3.  Dans la page des propriétés de boîte aux lettres, cliquez sur **Délégation de boîte aux lettres**.

4.  Pour attribuer des autorisations aux délégués, cliquez sur **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter") sous **Envoyer en tant que** ou **Envoyer de la part de** afin d’afficher une page qui présente la liste de tous les destinataires de votre organisation Exchange auxquels l’autorisation peut être affectée. Sélectionnez les destinataires voulus, ajoutez-les à la liste, puis cliquez sur **OK**. Vous pouvez également rechercher un destinataire spécifique en tapant son nom dans la zone de recherche et en cliquant sur **Rechercher**![Icône Recherche](images/Dn750895.773574d0-9b92-4cab-9f6b-81532c7418b9(EXCHG.150).gif "Icône Recherche").
    
    L’autorisation **Envoyer en tant que** permet au délégué d’envoyer des courriers électroniques à partir de cette boîte aux lettres.
    
    L’autorisation **Envoyer de la part de** permet au délégué d’envoyer des courriers électroniques de la part de cette boîte aux lettres. La ligne **De** de tous les messages envoyés par un délégué indique que le message a été envoyé par le délégué, au nom du propriétaire de la boîte aux lettres.
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Si l’utilisateur doit également pouvoir ouvrir et afficher le contenu de cette boîte aux lettres, vous devez aussi lui attribuer l’autorisation <strong>Accès total</strong>.</td>
    </tr>
    </tbody>
    </table>


5.  Cliquez sur **Enregistrer** pour enregistrer vos modifications.

## Utiliser le CAE pour attribuer une autorisation utilisateur afin d’envoyer un courrier électronique à partir d’un groupe

La procédure suivante montre comment attribuer une autorisation utilisateur pour envoyer un courrier électronique à partir d’un groupe.

1.  Dans le CAE, accédez à **Destinataires** \> **Groupes**.

2.  Dans la liste des groupes, cliquez sur celui pour lequel vous voulez attribuer des autorisations Envoyer en tant que, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

3.  Dans la page des propriétés de groupe, cliquez sur **Délégation de groupe**.

4.  Pour attribuer des autorisations aux délégués, cliquez sur **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter") sous **Envoyer en tant que** ou **Envoyer de la part de** afin d’afficher une page qui présente la liste de tous les destinataires de votre organisation Exchange auxquels l’autorisation peut être affectée. Sélectionnez les destinataires voulus, ajoutez-les à la liste, puis cliquez sur **OK**. Vous pouvez également rechercher un destinataire spécifique en tapant son nom dans la zone de recherche et en cliquant sur **Rechercher**![Icône Recherche](images/Dn750895.773574d0-9b92-4cab-9f6b-81532c7418b9(EXCHG.150).gif "Icône Recherche").
    
    L’autorisation **Envoyer en tant que** permet au délégué d’envoyer des courriers électroniques à partir de ce groupe.
    
    L’autorisation **Envoyer de la part de** permet au délégué d’envoyer des courriers électroniques de la part de ce groupe. La ligne **De** de tous les messages envoyés par un délégué indique que le message a été envoyé par le délégué, au nom du groupe.

5.  Cliquez sur **Enregistrer** pour enregistrer vos modifications.

## Utiliser le CAE pour attribuer des autorisations d’accès total

La procédure suivante explique comment attribuer des autorisations d’accès total à une boîte aux lettres utilisateur.

1.  Dans le CAE, accédez à **Destinataires** \> **Boîtes aux lettres**.

2.  Dans la liste des boîtes aux lettres, cliquez sur celle pour laquelle vous voulez attribuer des autorisations d’accès total, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

3.  Dans la page des propriétés de boîte aux lettres, cliquez sur **Délégation de boîte aux lettres**.

4.  Pour attribuer des autorisations à des délégués, cliquez sur **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter") sous **Accès total** afin d’afficher une page qui présente la liste de tous les destinataires de votre organisation Exchange auxquels l’autorisation peut être attribuée. Sélectionnez les destinataires voulus, ajoutez-les à la liste, puis cliquez sur **OK**. Vous pouvez également rechercher un destinataire spécifique en tapant son nom dans la zone de recherche et en cliquant sur **Rechercher**![Icône Recherche](images/Dn750895.773574d0-9b92-4cab-9f6b-81532c7418b9(EXCHG.150).gif "Icône Recherche").
    
    L’autorisation **Accès total** permet à un délégué d’ouvrir la boîte aux lettres d’un utilisateur et d’accéder à son contenu.
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>L'attribution de l'autorisation <strong>Accès total</strong> ne permet pas au délégué d'envoyer du courrier à partir de la boîte aux lettres. Pour permettre au délégué d’expédier du courrier, vous devez lui attribuer l’autorisation <strong>Envoyer en tant que</strong> ou <strong>Envoyer de la part de</strong>.</td>
    </tr>
    </tbody>
    </table>


5.  Cliquez sur **Enregistrer** pour enregistrer vos modifications.

## Utiliser l'environnement de ligne de commande pour attribuer des autorisations

Les sections suivantes montrent comment utiliser l'environnement de ligne de commande pour gérer les autorisations Accès total, Envoyer en tant que et Envoyer de la part de pour des boîtes aux lettres.

## Gérer l'autorisation Accès total

Les exemples suivants montrent comment utiliser les cmdlets **Add-MailboxPermission** et **Remove-MailboxPermission** pour gérer les autorisations Accès total.

Cet exemple attribue au délégué Raymond Sam l'autorisation Accès total pour la boîte aux lettres de Terry Adams.

    Add-MailboxPermission -Identity "Terry Adams" -User raymonds -AccessRights FullAccess -InheritanceType all

Cet exemple attribue à Esther Valle l'autorisation Accès total pour la boîte aux lettres de découverte de l'organisation.

    Add-MailboxPermission -Identity "DiscoverySearchMailbox{D919BA05-46A6-415f-80AD-7E09334BB852}" -User estherv -AccessRights FullAccess -InheritanceType all

Cet exemple attribue aux membres du groupe de distribution Helpdesk l'autorisation Accès total pour la boîte aux lettres partagée Helpdesk Tickets.

    Add-MailboxPermission "HelpdeskTickets" -User helpdesk -AccessRights FullAccess -InheritanceType all

Cet exemple retire à Jim Hance l’autorisation Accès total pour la boîte aux lettres d’Ayla Kol.

    Remove-MailboxPermission -Identity ayla -User "Jim Hance" -AccessRights FullAccess -Inheritance

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, consultez les rubriques suivantes :

  - [Add-MailboxPermission](https://technet.microsoft.com/fr-fr/library/bb124097\(v=exchg.150\))

  - [Remove-MailboxPermission](https://technet.microsoft.com/fr-fr/library/bb125153\(v=exchg.150\))

## Gérer l'autorisation Envoyer en tant que

Les exemples suivants montrent comment gérer les autorisations Envoyer en tant que dans Exchange Server 2013 et dans Exchange Online. Dans Exchange 2013, vous devez utiliser les cmdlets **Add-ADPermission** et **Remove-ADPermission**, tandis que dans Exchange Online, vous devez utiliser les cmdlets **Add-RecipientPermission** et **Remove-RecipientPermission**. Dans les deux cas, le paramètre *Identity* permet de spécifier le nom de la boîte aux lettres pour laquelle l'autorisation Envoyer en tant que doit être ajoutée ou supprimée, et le paramètre *User* ou *Trustee* permet de spécifier le délégué (par exemple, un utilisateur ou un groupe) auquel l'autorisation Envoyer en tant que doit être attribuée ou retirée.

<table>
<thead>
<tr class="header">
<th><img src="images/Bb125224.tip(EXCHG.150).gif" title="Conseil" alt="Conseil" />Conseil :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Utilisez la cmdlet <strong>Get-Recipient</strong> pour récupérer la propriété <em>Name</em> pour la boîte aux lettres et le délégué. Utilisez ces valeurs pour attribuer l'autorisation Envoyer en tant que.</td>
</tr>
</tbody>
</table>


## Exchange Server 2013

Cet exemple attribue au groupe Helpdesk l'autorisation Envoyer en tant que pour la boîte aux lettres partagée Helpdesk Support Team.

    Add-ADPermission -Identity helpdesksupport -User helpdeskgroup -ExtendedRights "Send As"

Cet exemple retire à l'utilisateur Pilar Pinilla l'autorisation Envoyer en tant que pour la boîte aux lettres de James Alvord.

    Remove-ADPermission -Identity "James Alvord" -User pilarp -ExtendedRights "Send As"

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, consultez les rubriques suivantes :

  - [Add-ADPermission](https://technet.microsoft.com/fr-fr/library/bb124403\(v=exchg.150\))

  - [Remove-ADPermission](https://technet.microsoft.com/fr-fr/library/aa996048\(v=exchg.150\))

## Exchange Online

Cet exemple attribue au groupe Printer Support l'autorisation Envoyer en tant que pour la boîte aux lettres partagée Contoso Printer Support.

    Add-RecipientPermission -Identity "Contoso Printer Support" -Trustee "Printer Support" -AccessRights SendAs

Cet exemple retire à l'utilisateur Karen Toh l'autorisation Envoyer en tant pour la boîte aux lettres d'Yan Li.

    Remove-RecipientPermission -Identity "Yan Li" -Trustee "Karen Toh" -ExtendedRights SendAs

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, consultez les rubriques suivantes :

  - [Add-RecipientPermission](https://technet.microsoft.com/fr-fr/library/ff935839\(v=exchg.150\))

  - [Remove-RecipientPermission](https://technet.microsoft.com/fr-fr/library/ff945794\(v=exchg.150\))

## Gérer l'autorisation Envoyer de la part de

Les exemples suivants montrent comme utiliser la cmdlet **Set-Mailbox** pour gérer les autorisations Envoyer de la part de.

Cet exemple attribue au délégué Holly Holt l'autorisation Envoyer de la part de pour la boîte aux lettres de Sean Chai.

    Set-Mailbox -Identity seanc@contoso.com -GrantSendOnBehalfTo hollyh

Cet exemple retire au groupe Temporary Executive Assistants l'autorisation Envoyer de la part de pour la boîte aux lettres partagée Contoso Executives.

    Set-Mailbox "Contoso Executives" -GrantSendOnBehalfTo @{remove="tempassistants@contoso.com"}

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, consultez la rubrique [Set-Mailbox](https://technet.microsoft.com/fr-fr/library/bb123981\(v=exchg.150\)).

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez correctement attribué des autorisations à une boîte aux lettres ou à une boîte aux lettres partagée, procédez de l'une des manières suivantes :

  - Dans le CAE :
    
    1.  Accédez à **Destinataires** \> **Boîte aux lettres** ou **Partagées**, cliquez sur la boîte aux lettres, puis sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").
    
    2.  Dans la page des propriétés de boîte aux lettres, cliquez sur **Délégation de boîte aux lettres**.
    
    3.  Si vous avez attribué une autorisation à un destinataire, vérifiez que l'utilisateur ou le groupe figure dans la liste sous l'autorisation en question. Si vous avez retiré une autorisation, vérifiez que le destinataire ne figure pas dans la liste sous l'autorisation en question.

Ou

  - Dans l'environnement de ligne de commande, exécutez l'une des commandes suivantes, selon l'autorisation que vous voulez gérer.
    
      - **Accès total**
        
            Get-MailboxPermission -Identity <mailbox>
        
        Pour vérifier si l'autorisation Accès total est attribuée à un délégué spécifique pour une boîte aux lettres, exécutez la commande suivante.
        
            Get-MailboxPermission -Identity <mailbox> -User <delegate>
    
      - **Envoyer en tant que**
        
        Dans Exchange Server 2013, exécutez la commande suivante.
        
            Get-ADPermission -Identity <name of mailbox> -User <delegate>
        
        Dans Exchange Online, exécutez la commande suivante.
        
            Get-RecipientPermission -Identity <mailbox> -Trustee <delegate>
    
      - **Envoyer de la part de**
        
            Get-Mailbox -Identity <mailbox> | FL GrantSendOnBehalfTo

## Attribuer des autorisations à un groupe

Comme indiqué précédemment, vous pouvez attribuer des autorisations Envoyer en tant que et Envoyer de la part de à des groupes de distribution, à des groupes de distribution dynamique et à des groupes de sécurité à extension messagerie, pour permettre à des délégués d'envoyer des messages en tant que ce groupe ou de la part de ce groupe.

Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrées « Groupes de distribution » et « Groupes de distribution dynamique » dans la section « Autorisations de configuration des destinataires » de la rubrique [Autorisations des destinataires](recipients-permissions-exchange-2013-help.md).

## Utiliser le CAE pour attribuer des autorisations

1.  Dans le CAE, accédez à **Destinataires** \> **Groupes**.

2.  Dans la liste des groupes, cliquez sur celui pour lequel vous voulez attribuer des autorisations, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

3.  Dans la page des propriétés de groupe, cliquez sur **Délégation de groupe**.

4.  Pour attribuer une autorisation à des délégués, cliquez sur **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter") sous l'autorisation en question afin d'afficher une page présentant la liste de tous les destinataires de votre organisation Exchange auxquels l'autorisation peut être attribuée. Sélectionnez les destinataires de votre choix, ajoutez-les à la liste, puis cliquez sur **OK**. Vous pouvez également rechercher un destinataire spécifique en tapant son nom dans la zone de recherche et en cliquant sur **Rechercher**![Icône Recherche](images/Dn750895.773574d0-9b92-4cab-9f6b-81532c7418b9(EXCHG.150).gif "Icône Recherche").
    
    Pour retirer une autorisation à un destinataire, sous l'autorisation en question, sélectionnez le destinataire, puis cliquez sur **Supprimer**![Icône Suppression](images/Dd362328.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "Icône Suppression").

5.  Cliquez sur **Enregistrer** pour enregistrer vos modifications.

## Utiliser l'environnement de ligne de commande pour attribuer des autorisations

Les sections suivantes montrent comment utiliser l'environnement de ligne de commande pour gérer les autorisations Envoyer en tant que et Envoyer de la part de pour des groupes.

## Gérer l'autorisation Envoyer en tant que

Les exemples suivants montrent comment gérer les autorisations Envoyer en tant que pour des groupes dans Exchange Server 2013 et dans Exchange Online. Dans Exchange 2013, vous devez utiliser les cmdlets **Add-ADPermission** et **Remove-ADPermission**. Dans Exchange Online, vous devez utiliser les cmdlets **Add-RecipientPermission** et **Remove-RecipientPermission**. Dans les deux cas, le paramètre *Identity* permet de spécifier le nom du groupe pour lequel l'autorisation Envoyer en tant que doit être ajoutée ou supprimée, et le paramètre *User* ou *Trustee* permet de spécifier le délégué (par exemple, un utilisateur ou un groupe) auquel l'autorisation Envoyer en tant que doit être attribuée ou retirée.

<table>
<thead>
<tr class="header">
<th><img src="images/Bb125224.tip(EXCHG.150).gif" title="Conseil" alt="Conseil" />Conseil :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Utilisez la cmdlet <strong>Get-Recipient</strong> pour récupérer la propriété <em>Name</em> pour le groupe et le délégué. Utilisez ces valeurs pour attribuer l'autorisation Envoyer en tant que.</td>
</tr>
</tbody>
</table>


## Exchange Server 2013

Cet exemple attribue au groupe Sales Admins l'autorisation Envoyer en tant que pour le groupe Contoso Sales Info. Cela permet aux membres du groupe Sales Admins d'envoyer des messages en tant que groupe Contoso Sales Info.

    Add-ADPermission -Identity "Contoso Sales Info" -User "Sales Admins" -ExtendedRights "Send As"

Cet exemple retire à l'utilisateur Alan Shen l'autorisation Envoyer en tant que pour le groupe Corporate IT Admins.

    Remove-ADPermission -Identity "Corporate IT Admins" -User contoso\alans -ExtendedRights "Send As"

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, consultez les rubriques suivantes :

  - [Add-ADPermission](https://technet.microsoft.com/fr-fr/library/bb124403\(v=exchg.150\))

  - [Remove-ADPermission](https://technet.microsoft.com/fr-fr/library/aa996048\(v=exchg.150\))

## Exchange Online

Cet exemple attribue au groupe Contoso Admins l'autorisation Envoyer en tant que pour le groupe de distribution dynamique Emergency Broadcast Messages.

    Add-RecipientPermission -Identity emergencybroadcast@contoso.com -Trustee "Contoso Admins" -AccessRights SendAs

Cet exemple retire à l'utilisateur Walter Harp l'autorisation Envoyer en tant que pour le groupe de sécurité Printer Resources.

    Remove-RecipientPermission -Identity "Printer Resources" -Trustee walterh@contoso.com ExtendedRights SendAs

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, consultez les rubriques suivantes :

  - [Add-RecipientPermission](https://technet.microsoft.com/fr-fr/library/ff935839\(v=exchg.150\))

  - [Remove-RecipientPermission](https://technet.microsoft.com/fr-fr/library/ff945794\(v=exchg.150\))

## Gérer l'autorisation Envoyer de la part de

Les exemples suivants montrent comme utiliser les cmdlets **Set-DistributionGroup** et **Set-DynamicDistributionGroup** pour gérer les autorisations Envoyer de la part de pour des groupes.

Cet exemple attribue au délégué Sara Davis l'autorisation Envoyer de la part de pour le groupe de distribution Printer Support.

    Set-DistributionGroup -Identity printersupport@contoso.com -GrantSendOnBehalfTo sarad

Cet exemple attribue au délégué Administrator l'autorisation Envoyer de la part de pour le groupe de distribution dynamique All Employees.

    Set-DynamicDistributionGroup -Identity "All Employees" -GrantSendOnBehalfTo administrator

Cet exemple retire au délégué Administrator l'autorisation Envoyer de la part de pour le groupe de distribution dynamique All Employees.

    Set-DynamicDistributionGroup "All Employees" -GrantSendOnBehalfTo @{remove="administrator"}

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, consultez les rubriques suivantes :

  - [Set-DistributionGroup](https://technet.microsoft.com/fr-fr/library/bb124955\(v=exchg.150\))

  - [Set-DynamicDistributionGroup](https://technet.microsoft.com/fr-fr/library/bb123796\(v=exchg.150\))

## Comment savoir si cela a fonctionné ?

Pour vérifier si vous avez correctement attribué des autorisations à un groupe, procédez comme suit :

  - Dans le CAE :
    
    1.  Accédez à **Destinataires** \> **Groupes**, cliquez sur le groupe, puis sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").
    
    2.  Dans la page des propriétés de groupe, cliquez sur **Délégation de groupe**.
    
    3.  Si vous avez attribué une autorisation à un destinataire, vérifiez que l'utilisateur ou le groupe figure dans la liste sous l'autorisation en question. Si vous avez retiré une autorisation, vérifiez que le destinataire ne figure pas dans la liste sous l'autorisation en question.

Ou

  - Dans l'environnement de ligne de commande, exécutez l'une des commandes suivantes, selon l'autorisation que vous voulez gérer.
    
      - **Envoyer en tant que**
        
        Dans Exchange Server 2013, exécutez la commande suivante.
        
            Get-ADPermission -Identity <name of group> -User <delegate>
        
        Dans Exchange Online, exécutez la commande suivante.
        
            Get-RecipientPermission -Identity <group> -Trustee <delegate>
    
      - **Envoyer de la part de**
        
            Get-DistributionGroup -Identity <group> | FL GrantSendOnBehalfTo
        
        Ou
        
            Get-DynamicDistributionGroup -Identity <group> | FL GrantSendOnBehalfTo

