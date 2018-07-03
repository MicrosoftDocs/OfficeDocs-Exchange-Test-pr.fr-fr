---
title: 'Désactiver ou supprimer une boîte aux lettres: Exchange 2013 Help'
TOCTitle: Désactiver ou supprimer une boîte aux lettres
ms:assetid: 31ad25d6-2942-4fd9-aecb-cdf9654163d2
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ863434(v=EXCHG.150)
ms:contentKeyID: 50555374
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Désactiver ou supprimer une boîte aux lettres

 

_**Sapplique à :** Exchange Server 2013 SP1_

_**Dernière rubrique modifiée :** 2015-03-09_

Vous pouvez utiliser le CAE ou l’environnement de ligne de commande Exchange Management Shell pour désactiver ou supprimer une boîte aux lettres dans Exchange 2013. Lorsqu’une boîte aux lettres est désactivée ou supprimée, Exchange la conserve dans la base de données de boîtes aux lettres et change son état en désactivé. Les boîtes aux lettres désactivées et supprimées sont conservées dans la base de données de boîtes aux lettres jusqu’à l’expiration de la période de rétention de la boîte aux lettres supprimée, qui est de 30 jours par défaut. À l’expiration de la période de rétention, la boîte aux lettres est définitivement supprimée ou *vidée*.

Si vous devez supprimer une boîte aux lettres dans Exchange Online, consultez la rubrique [Suppression ou restauration de boîtes aux lettres utilisateur dans Exchange Online](https://technet.microsoft.com/fr-fr/library/dn186233\(v=exchg.150\)).

> [!NOTE]
> Les boîtes aux lettres désactivés ou supprimées sont qualifiées de <em>boîtes aux lettres déconnectées</em>.


La principale différence entre la suppression et la désactivation d’une boîte aux lettres est que lors d’une désactivation, les attributs d’Exchange sont supprimés du compte d’utilisateur Active Directory correspondant, mais le compte d’utilisateur est conservé. Lors de la suppression d’une boîte aux lettres, les attributs d’Exchange et le compte d’utilisateur Active Directory sont tous deux supprimés. Cette différence détermine également vos options pour reconnecter ou restaurer des boîtes aux lettres désactivées et supprimées.

Le tableau suivant décrit les types de boîtes aux lettres Exchange pouvant être désactivés et supprimés.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Type de boîte aux lettres</th>
<th>Désactiver ?</th>
<th>Supprimer ?</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Boîte aux lettres d’archivage</p></td>
<td><p>Oui</p></td>
<td><p>Non *</p></td>
</tr>
<tr class="even">
<td><p>Boîte aux lettres liée</p></td>
<td><p>Oui</p></td>
<td><p>Oui</p></td>
</tr>
<tr class="odd">
<td><p>Boîte aux lettres de ressources (salle ou équipement)</p></td>
<td><p>Non</p></td>
<td><p>Oui</p></td>
</tr>
<tr class="even">
<td><p>Boîte aux lettres partagée</p></td>
<td><p>Oui</p></td>
<td><p>Oui</p></td>
</tr>
<tr class="odd">
<td><p>Boîte aux lettres d’utilisateur</p></td>
<td><p>Oui</p></td>
<td><p>Oui</p></td>
</tr>
</tbody>
</table>


\* Si une boîte aux lettres d’archivage est activée, elle sera supprimée en même temps que la boîte aux lettres principale. Pour plus d’informations sur la désactivation de boîtes aux lettres d’archivage, consultez la rubrique [Gestion des archives permanentes dans Exchange 2013](manage-in-place-archives-in-exchange-2013-exchange-2013-help.md).

Si un administrateur supprime un compte d’utilisateur qui comporte une boîte aux lettres, la banque d’informations Exchange détectera que la boîte aux lettres n’est plus connectée à un compte d’utilisateur et la marquera pour suppression, même si elle est en attente. Pour conserver la boîte aux lettres, procédez comme suit :

1.  Au lieu de supprimer le compte d’utilisateur, désactivez-le.

2.  Modifiez les propriétés de la boîte aux lettres pour en restreindre l’utilisation et l’accès. Par exemple, la définition de quotas d’envoi/de réception sur 1 permet de bloquer les personnes pouvant envoyer des messages à la boîte aux lettres et de restreindre l’accès à cette dernière.

3.  Conservez la boîte aux lettres jusqu’à ce que toutes les données aient pu être vidées ou jusqu’à ce que le blocage ne soit plus nécessaire.

Pour d’autres tâches de gestion relatives aux boîtes aux lettres déconnectées, consultez les rubriques suivantes :

  - [Boîtes aux lettres déconnectées](disconnected-mailboxes-exchange-2013-help.md)

  - [Connecter une boîte aux lettres déconnectée](connect-a-disabled-mailbox-exchange-2013-help.md)

  - [Connexion ou restauration d’une boîte aux lettres supprimée](connect-or-restore-a-deleted-mailbox-exchange-2013-help.md)

  - [Supprimer définitivement une boîte aux lettres](permanently-delete-a-mailbox-exchange-2013-help.md)

## Ce qu’il faut savoir avant de commencer ?

  - Durée d’exécution estimée de chaque procédure : 2 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Section « Autorisations de configuration des destinataires » dans la rubrique [Autorisations des destinataires](recipients-permissions-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..


## Que souhaitez-vous faire ?

## Désactiver une boîte aux lettres

Comme indiqué précédemment, lorsque vous désactivez une boîte aux lettres, les attributs d’Exchange sont supprimés du compte d’utilisateur Active Directory correspondant, mais le compte d’utilisateur est conservé.

## Désactivation d’une boîte aux lettres à l’aide du Centre d’administration Exchange (CAE)

La procédure suivante explique comment désactiver une boîte aux lettres utilisateur. Suivez la même procédure pour désactiver d’autres types de boîtes aux lettres après avoir accédé à la page appropriée dans le CAE.

1.  Dans le CAE, accédez à **Destinataires**  \> **Boîtes aux lettres**.

2.  Dans la liste des boîtes aux lettres utilisateur, cliquez sur la boîte aux lettres que vous souhaitez désactiver.

3.  Cliquez sur **Autre**![Icône Options supplémentaires](images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif "Icône Options supplémentaires"), puis cliquez sur **Désactiver**.

4.  Un message d’avertissement vous demande de confirmer la désactivation de la base de données. Cliquez sur **Oui** pour désactiver la boîte aux lettres.

La boîte aux lettres est supprimée de la liste de boîtes aux lettres.

## Utiliser l’environnement de ligne de commande Exchange Management Shell pour désactiver une boîte aux lettres

Utilisez la commande suivante pour désactiver les boîtes aux lettres utilisateur, les boîtes aux lettres associées, les boîtes aux lettres de ressources et les boîtes aux lettres partagées :

    Disable-Mailbox <identity>

Lorsque vous exécutez cette commande, un message s’affiche pour vous demander de confirmer la désactivation de la boîte aux lettres.

Voici quelques exemples de commandes permettant de désactiver les boîtes aux lettres.

    Disable-Mailbox danj

    Disable-Mailbox "Conf Room 31/1234 (12)"

    Disable-Mailbox sharedmbx@contoso.com

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez bien désactivé une boîte aux lettres, procédez de l’une des manières suivantes :

  - Dans le CAE, cliquez sur **Destinataires**, accédez à la page correspondant au type de boîte aux lettres que vous avez désactivé, puis vérifiez que la boîte aux lettres n’est plus répertoriée.

  - Dans Utilisateurs et ordinateurs Active Directory, cliquez avec le bouton droit sur le compte d’utilisateur dont vous souhaitez désactiver la boîte aux lettres, puis cliquez sur **Propriétés**. Dans l’onglet **Général**, remarquez que le champ **Courrier électronique** est vide. Ceci indique que la boîte aux lettres est désactivée, mais que le compte d’utilisateur existe toujours.

  - Dans l’environnement de ligne de commande Exchange Management Shell, exécutez la commande suivante.
    
        Get-MailboxDatabase | Get-MailboxStatistics | Where { $_.DisplayName -eq "<display name>" } | fl DisconnectReason,DisconnectDate
    
    La valeur `Disabled` de la propriété *DisconnectReason* indique que la boîte aux lettres est désactivée.
    
    > [!NOTE]
    > Lorsque vous supprimez une boîte aux lettres, la valeur de la propriété <em>DisconnectReason</em> est également <code>Disabled</code>. Cependant, le compte d’utilisateur Active Directory correspondant est supprimé.


  - Dans l’environnement de ligne de commande Exchange Management Shell, exécutez la commande suivante.
    
        Get-User <identity>
    
    Notez que la valeur de la propriété *RecipientType* est `User` et non pas `UserMailbox`, qui est la valeur attribuée aux utilisateurs dont les boîtes aux lettres sont activées. Ceci indique également que la boîte aux lettres est désactivée, mais que le compte d’utilisateur est conservé.

## Suppression d’une boîte aux lettres

Comme indiqué précédemment, lors de la suppression d’une boîte aux lettres, les attributs d’Exchange et le compte d’utilisateur Active Directory sont tous deux supprimés. La boîte aux lettres (et la boîte aux lettres d’archivage si celle-ci est activée) est définitivement supprimée de la base de données de boîtes aux lettres à l’expiration de la période de rétention de la boîte aux lettres.

## Suppression d’une boîte aux lettres à l’aide du Centre d’administration Exchange (CAE)

La procédure suivante explique comment supprimer une boîte aux lettres utilisateur. Suivez la même procédure pour supprimer d’autres types de boîtes aux lettres après avoir accédé à la page appropriée dans le CAE.

1.  Dans le CAE, accédez à **Destinataires**  \> **Boîtes aux lettres**.

2.  Dans la liste des boîtes aux lettres utilisateur, cliquez sur la boîte aux lettres que vous souhaitez supprimer, puis sur **Supprimer**![Icône Supprimer](images/Dd979797.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "Icône Supprimer").

3.  Un message d’avertissement vous demande de confirmer la suppression de la boîte aux lettres. Cliquez sur **Oui** pour supprimer la boîte aux lettres.

La boîte aux lettres est supprimée de la liste de boîtes aux lettres.

## Suppression d’une boîte aux lettres à l’aide de l’environnement de ligne de commande Exchange Management Shell

Utilisez la commande suivante pour supprimer les boîtes aux lettres utilisateur, les boîtes aux lettres associées, les boîtes aux lettres de ressources et les boîtes aux lettres partagées :

    Remove-Mailbox <identity>

Lorsque vous exécutez cette commande, un message vous demande de confirmer la suppression de la boîte aux lettres et du compte d’utilisateur Active Directory correspondant.

Voici quelques exemples de commandes permettant de supprimer des boîtes aux lettres.

    Remove-Mailbox pilarp@contoso.com

    Remove-Mailbox "Fleet Van (16)"

    Remove-Mailbox corpprint

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez bien supprimé une boîte aux lettres, exécutez l’un des ensembles de procédures de vérification suivants :

1.  Dans le CAE, cliquez sur **Destinataires**, puis accédez à la page correspondant au type de boîte aux lettres que vous avez supprimé, puis vérifiez que la boîte aux lettres n’est plus répertoriée.

2.  Dans Utilisateurs et ordinateurs Active Directory, vérifiez que le compte d’utilisateur correspondant n’est plus répertorié.

Ou

1.  Exécutez la commande suivante pour vérifier que la boîte aux lettres a été supprimée :
    
        Get-MailboxDatabase | Get-MailboxStatistics | Where { $_.DisplayName -eq "<display name>" } | fl DisconnectReason,DisconnectDate
    
    La valeur `Disabled` de la propriété *DisconnectReason* indique que la boîte aux lettres a été supprimée.
    
    > [!NOTE]
    > Lorsque vous désactivez une boîte aux lettres, la valeur de la propriété <em>DisconnectReason</em> est également <code>Disabled</code>. Cependant, le compte d’utilisateur Active Directory correspondant est conservé.


2.  Exécutez la commande suivante pour vérifier que le compte d’utilisateur Active Directory a été supprimé :
    
        Get-User <identity>
    
    La commande renvoie une erreur indiquant que l’utilisateur est introuvable, en s’assurant que le compte a bien été supprimé.

