---
title: 'Boîtes aux lettres déconnectées: Exchange 2013 Help'
TOCTitle: Boîtes aux lettres déconnectées
ms:assetid: 508ebe2b-387d-4867-bdb0-028ef351ce56
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb232039(v=EXCHG.150)
ms:contentKeyID: 50555397
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Boîtes aux lettres déconnectées

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2015-03-09_

Chaque boîte aux lettres Microsoft Exchange est constituée d’un compte d’utilisateur Active Directory et de données de boîte aux lettres stockées dans la base de données de boîtes aux lettres Exchange. Toutes les données de configuration d’une boîte aux lettres sont stockées dans les attributs d’Exchange de l’objet utilisateur Active Directory. La base de données de boîtes aux lettres contient les données de messagerie de la boîte aux lettres associée au compte d’utilisateur. La figure suivante illustre les composants d’une boîte aux lettres.

**Composants de boîte aux lettres**

![Composants d’une boîte aux lettres](images/Bb201680.5fcb5e6d-656e-42ae-871f-0eef8aea456b(EXCHG.150).gif "Composants d’une boîte aux lettres")

Une *boîte aux lettres déconnectée* est un objet boîte aux lettres de la base de données de boîtes aux lettres qui n’est pas associé à un compte d’utilisateur Active Directory. Il existe deux types de boîtes aux lettres déconnectées :

  - **Boîtes aux lettres désactivées**   Lorsqu’une boîte aux lettres est désactivée ou supprimée dans le Centre d’administration Exchange (CAE) ou à l’aide de la cmdlet **Disable-Mailbox** ou **Remove-Mailbox** de l’environnement de ligne de commande Exchange Management Shell, Exchange conserve la boîte aux lettres supprimée dans la base de données de boîtes aux lettres et fait basculer la boîte aux lettres à l’état désactivé. C’est la raison pour laquelle les boîtes aux lettres désactivées ou supprimées sont qualifiées de *boîtes aux lettres désactivées*. La seule différence est qu’en cas de désactivation d’une boîte aux lettres, les attributs d’Exchange sont supprimés du compte d’utilisateur Active Directory correspondant. Toutefois, le compte d’utilisateur est conservé. Lors de la suppression d’une boîte aux lettres, les attributs d’Exchange et le compte d’utilisateur Active Directory sont tous deux supprimés.
    
    Les boîtes aux lettres désactivées et supprimées sont conservées dans la base de données de boîtes aux lettres jusqu’à l’expiration de la période de rétention de la boîte aux lettres supprimée, qui est de 30 jours par défaut. À l’expiration de la période de rétention, la boîte aux lettres est définitivement supprimée (ou *vidée*). Si une boîte aux lettres est supprimée à l’aide de la cmdlet **Remove-Mailbox**, elle est également conservée pendant toute la durée de la période de rétention.
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ159813.important(EXCHG.150).gif" title="Important" alt="Important" />Important :</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Si une boîte aux lettres est supprimée à l’aide de la cmdlet <strong>Remove-Mailbox</strong> et du paramètre <em>Permanent</em> ou <em>StoreMailboxIdentity</em>, elle est immédiatement supprimée de la base de données de boîtes aux lettres.</td>
    </tr>
    </tbody>
    </table>
    
    Pour identifier les boîtes aux lettres désactivées de votre organisation, exécutez la commande suivante dans l’environnement de ligne de commande Exchange Management Shell :
    
        Get-MailboxDatabase | Get-MailboxStatistics | Where { $_.DisconnectReason -eq "Disabled" } | ft DisplayName,Database,DisconnectDate

  - **Boîtes aux lettres supprimées (récupérables)**   Lorsqu’une boîte aux lettres est déplacée vers une autre base de données de boîtes aux lettres, Exchange ne supprime pas entièrement la boîte aux lettres de la base de données de boîtes aux lettres source une fois le déplacement terminé. En revanche, la boîte aux lettres qui se trouve dans la base de données de boîtes aux lettres source passe à l’état *supprimé (récupérable)*. Tout comme les boîtes aux lettres désactivées, les boîtes aux lettres supprimées (récupérables) sont conservées dans la base de données source jusqu’à l’expiration de la période de rétention de la boîte aux lettres ou jusqu’au vidage de la boîte aux lettres à l’aide de la cmdlet **Remove-StoreMailbox**.
    
    Exécutez la commande suivante pour identifier les boîtes aux lettres supprimées (récupérables) dans votre organisation :
    
        Get-MailboxDatabase | Get-MailboxStatistics | Where { $_.DisconnectReason -eq "SoftDeleted" } | ft DisplayName,Database,DisconnectDate

**Contenu de cette rubrique**

Utilisation de boîtes aux lettres désactivées

Utilisation de boîtes aux lettres d’archivage désactivées

Utilisation de boîtes aux lettres supprimées (récupérables)

Synthèse de l’utilisation de boîtes aux lettres déconnectées

Documentation de la boîte aux lettres déconnectée

## Utilisation de boîtes aux lettres désactivées

Vous pouvez réaliser plusieurs opérations sur une boîte aux lettres désactivée avant qu’elle ne soit vidée de la base de données de boîtes aux lettres :

  - Reconnectez-la au même compte d’utilisateur.

  - Connectez-la à un autre compte d’utilisateur ne disposant pas d’une messagerie, ce qui signifie que le compte d’utilisateur ne dispose pas d’une boîte aux lettres.

  - Restaurez-la dans un compte d’utilisateur possédant une boîte aux lettres existante. Par exemple, si un utilisateur dont la boîte aux lettres a été supprimée possède une nouvelle boîte aux lettres, vous pouvez restaurer sa boîte aux lettres désactivée dans sa nouvelle boîte aux lettres.

  - Supprimez-la définitivement de la base de données de boîtes aux lettres Exchange.

## Connexion ou restauration d’une boîte aux lettres désactivée

Voici quelques scénarios dans lesquels vous souhaiterez éventuellement connecter ou restaurer une boîte aux lettres désactivée avant l’expiration de la période de rétention de la boîte aux lettres ou sa suppression définitive :

  - Vous avez désactivé une boîte aux lettres et souhaitez à présent la reconnecter au même compte d’utilisateur Active Directory.

  - Vous avez supprimé une boîte aux lettres à l’aide du Centre d’administration Exchange ou de la cmdlet [Remove-Mailbox](https://technet.microsoft.com/fr-fr/library/aa995948\(v=exchg.150\)) et souhaitez à présent la reconnecter à un autre compte d’utilisateur Active Directory.

  - Vous avez supprimé une boîte aux lettres et souhaitez à présent la restaurer dans une boîte aux lettres existante. Par exemple, si un utilisateur dont la boîte aux lettres a été supprimée possède une nouvelle boîte aux lettres, vous pouvez restaurer sa boîte aux lettres désactivée dans celle-ci.

  - Vous voulez convertir une boîte aux lettres d’utilisateur en boîte aux lettres liée associée à un compte d’utilisateur externe à la forêt dans laquelle se trouve votre organisation Exchange. Le scénario de forêt ressource montre quand vous vous pouvez être amené à associer une boîte aux lettres à un compte externe. Dans ce scénario, les objets utilisateur de la forêt Exchange ont des boîtes aux lettres, mais sont désactivés pour l’ouverture de session. Vous devez associer une boîte aux lettres de la forêt Exchange à un compte d’utilisateur de la forêt de comptes externes.

Vous pouvez reconnecter ou restaurer une boîte aux lettres désactivée de deux manières : En utilisant le Centre d’administration Exchange ou la cmdlet **Connect-Mailbox** pour connecter une boîte aux lettres désactivée à un compte d’utilisateur. Pour connaître les procédures de reconnexion des boîtes aux lettres désactivées, consultez la rubrique [Connecter une boîte aux lettres déconnectée](connect-a-disabled-mailbox-exchange-2013-help.md).

En utilisant la cmdlet **New-MailboxRestoreRequest** pour fusionner le contenu de la boîte aux lettres désactivée avec une boîte aux lettres existante. Cette cmdlet utilise le service de réplication de boîte aux lettres (MRS) pour restaurer la boîte aux lettres. Pour connaître les procédures de restauration des boîtes aux lettres désactivées, consultez la rubrique [Connexion ou restauration d’une boîte aux lettres supprimée](connect-or-restore-a-deleted-mailbox-exchange-2013-help.md).

## Suppression définitive d’une boîte aux lettres désactivée

Comme indiqué précédemment, Exchange conserve les boîtes aux lettres désactivées dans la base de données de boîtes aux lettres en fonction des paramètres de rétention des boîtes aux lettres supprimées qui sont définis pour cette base de données de boîtes aux lettres. À l’issue de la période de rétention spécifiée, une boîte aux lettres désactivée est vidée de la base de données de boîtes aux lettres Exchange. Vous pouvez également supprimer définitivement une boîte aux lettres désactivée et l’intégralité du contenu de son message de la base de données de boîtes aux lettres à l’aide de la cmdlet **Remove-StoreMailbox**. Une fois qu’une boîte aux lettres désactivée est automatiquement vidée ou définitivement supprimée par un administrateur, la perte de données est permanente et la boîte aux lettres ne peut pas être récupérée.

Pour plus d’informations, consultez la rubrique [Supprimer définitivement une boîte aux lettres](permanently-delete-a-mailbox-exchange-2013-help.md).

Utilisation de boîtes aux lettres désactivées

## Utilisation de boîtes aux lettres d’archivage désactivées

Les boîtes aux lettres d’archivage sont déconnectées au moment de leur désactivation. Tout comme une boîte aux lettres principale désactivée, une boîte aux lettres d’archivage déconnectée peut être connectée en utilisant la cmdlet **Connect-Mailbox** avec le paramètre *Archive*.

La boîte aux lettres principale et la boîte aux lettres d’archivage partagent le même nom unique hérité. De fait, vous devez connecter la boîte aux lettres d’archivage à la même boîte aux lettres d’utilisateur à laquelle elle était préalablement connectée. Vous ne pouvez pas connecter la boîte aux lettres d’archivage à une autre boîte aux lettres d’utilisateur.

Deux opérations sont possibles sur une boîte aux lettres d’archivage déconnectée :

  - **La connecter à une boîte aux lettres principale existante**   Tout comme une boîte aux lettres principale déconnectée, une boîte aux lettres d’archivage déconnectée est conservée dans la base de données de boîtes aux lettres jusqu’à l’expiration de la période de rétention de la boîte aux lettres supprimée, qui est de 30 jours par défaut. Pendant ce temps, vous pouvez récupérer la boîte aux lettres d’archivage en la reconnectant au même compte d’utilisateur que celui auquel elle était connectée avant sa désactivation.
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Si vous désactivez une boîte aux lettres d’archivage pour une boîte aux lettres utilisateur, puis activez une boîte aux lettres d’archivage pour ce même utilisateur, une nouvelle boîte aux lettres d’archivage est octroyée à cette boîte aux lettres. Même si vous pouvez utiliser la cmdlet <strong>Connect-Mailbox</strong> pour connecter une boîte aux lettres principale à un utilisateur, vous devez utiliser la cmdlet <strong>Enable-Mailbox</strong> pour connecter une boîte aux lettres d’archivage désactivée à une boîte aux lettres existante.</td>
    </tr>
    </tbody>
    </table>
    
    Pour plus d’informations, consultez la rubrique [Gestion des archives permanentes dans Exchange 2013](manage-in-place-archives-in-exchange-2013-exchange-2013-help.md).

  - **La supprimer définitivement de la base de données de boîtes aux lettres Exchange**    Exchange conserve les boîtes aux lettres d’archivage déconnectées en fonction des paramètres de rétention des boîtes aux lettres supprimées qui sont configurés pour la base de données de boîtes aux lettres. Par défaut, la période de rétention est de 30 jours. À l’issue de la période de rétention de boîte aux lettres spécifiée, une boîte aux lettres d’archivage déconnectée est vidée de la base de données de boîtes aux lettres Exchange.
    
    Tout comme une boîte aux lettres principale désactivée, vous pouvez à tout moment supprimer définitivement une boîte aux lettres d’archivage désactivée à l’aide de la cmdlet **Remove-StoreMailbox**. Pour plus d’informations, consultez la rubrique [Supprimer définitivement une boîte aux lettres](permanently-delete-a-mailbox-exchange-2013-help.md).

Utilisation de boîtes aux lettres désactivées

## Utilisation de boîtes aux lettres supprimées (récupérables)

Une boîte aux lettres supprimée (récupérable) est créée lorsqu’une boîte aux lettres est déplacée d’une base de données de boîtes aux lettres Exchange vers n’importe quelle base de données de boîtes aux lettres. À la suite d’un déplacement, Exchange ne supprime pas complètement la boîte aux lettres de la base de données source si une erreur provoquant la défaillance de la boîte aux lettres dans la base de données de destination se produit pendant le déplacement. Vous pouvez toujours restaurer la boîte aux lettres source et renouveler votre essai. Exchange conserve la boîte aux lettres supprimée (récupérable) pendant toute la durée de la période de rétention de la boîte aux lettres.

Vous pouvez effectuer deux opérations sur une boîte aux lettres supprimée (récupérable) :

  - La restaurer dans une boîte aux lettres existante.

  - La supprimer définitivement de la base de données de boîtes aux lettres Exchange.

Les procédures de restauration et de suppression définitive d’une boîte aux lettres supprimée (récupérable) sont similaires à celles d’une boîte aux lettres désactivée. Pour plus d’informations, consultez les rubriques suivantes :

  - [Restaurer une boîte aux lettres supprimée (récupérable)](restore-a-soft-deleted-mailbox-exchange-2013-help.md)

  - [Supprimer définitivement une boîte aux lettres](permanently-delete-a-mailbox-exchange-2013-help.md)

Utilisation de boîtes aux lettres désactivées

## Synthèse de l’utilisation de boîtes aux lettres déconnectées

Le tableau suivant récapitule les informations relatives aux boîtes aux lettres déconnectées, notamment le mode de déconnexion de la boîte aux lettres, ce que devient le compte d’utilisateur Active Directory correspondant lorsqu’une boîte aux lettres est déconnectée, ainsi que les options et outils mis à votre disposition pour connecter ou restaurer des boîtes aux lettres déconnectées.


<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>Mode de désactivation de la boîte aux lettres</th>
<th>Valeur de la propriété <em>DisconnectReason</em></th>
<th>Le compte d’utilisateur Active Directory est-il conservé ?</th>
<th>Options de connexion ou de restauration</th>
<th>Outils</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><ul>
<li><p>Le Centre d’administration Exchange (CAE) : <strong>Destinataires</strong> &gt; <strong>Boîtes aux lettres</strong> &gt; <strong>Désactiver</strong></p></li>
<li><p>L’environnement de ligne de commande Exchange Management Shell : Cmdlet <strong>Disable-Mailbox</strong></p></li>
</ul></td>
<td><p>Désactivé</p></td>
<td><p>Oui</p></td>
<td><p>Connexion au même compte d’utilisateur</p></td>
<td><ul>
<li><p>Le Centre d’administration Exchange (CAE) : <strong>Destinataires</strong> &gt; <strong>Boîtes aux lettres</strong> &gt; <strong>Connecter une boîte aux lettres</strong></p></li>
<li><p>L’environnement de ligne de commande Exchange Management Shell : Cmdlet <strong>Connect-Mailbox</strong></p></li>
</ul></td>
</tr>
<tr class="even">
<td><ul>
<li><p>Le Centre d’administration Exchange (CAE) : <strong>Destinataires</strong> &gt; <strong>Boîtes aux lettres</strong> &gt; <strong>Supprimer</strong></p></li>
<li><p>L’environnement de ligne de commande Exchange Management Shell : Cmdlet <strong>Remove-Mailbox</strong></p></li>
</ul></td>
<td><p>Désactivé</p></td>
<td><p>Non</p></td>
<td><ul>
<li><p>Connexion à un autre compte d’utilisateur</p></li>
<li><p>Restauration dans une autre boîte aux lettres</p></li>
</ul></td>
<td><ul>
<li><p>Le Centre d’administration Exchange (CAE) : <strong>Destinataires</strong> &gt; <strong>Boîtes aux lettres</strong> &gt; <strong>Connecter une boîte aux lettres</strong></p></li>
<li><p>L’environnement de ligne de commande Exchange Management Shell : Cmdlet <strong>Connect-Mailbox</strong></p></li>
<li><p><strong>Enable-Mailbox</strong></p></li>
<li><p>L’environnement de ligne de commande Exchange Management Shell : Cmdlet <strong>New-MailboxRestore</strong></p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Déplacée vers une autre base de données de boîtes aux lettres</p></td>
<td><p>Supprimée (récupérable)</p></td>
<td><p>Oui</p></td>
<td><ul>
<li><p>Connexion à un autre compte d’utilisateur</p></li>
<li><p>Restauration dans une autre boîte aux lettres</p></li>
</ul></td>
<td><ul>
<li><p>Le Centre d’administration Exchange (CAE) : <strong>Destinataires</strong> &gt; <strong>Boîtes aux lettres</strong> &gt; <strong>Connecter une boîte aux lettres</strong></p></li>
<li><p>L’environnement de ligne de commande Exchange Management Shell : Cmdlet <strong>Connect-Mailbox</strong></p></li>
<li><p><strong>Enable-Mailbox</strong></p></li>
<li><p>L’environnement de ligne de commande Exchange Management Shell : Cmdlet <strong>New-MailboxRestore</strong></p></li>
</ul></td>
</tr>
</tbody>
</table>


Utilisation de boîtes aux lettres désactivées

## Documentation de la boîte aux lettres déconnectée

Le tableau suivant contient des liens renvoyant vers les rubriques qui vous permettront de gérer des boîtes aux lettres déconnectées. Cela inclut notamment la gestion des boîtes aux lettres d’utilisateur déconnectées, des boîtes aux lettres liées, des boîtes aux lettres de ressources et des boîtes aux lettres partagées.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Rubrique</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="disable-or-delete-a-mailbox-exchange-2013-help.md">Désactiver ou supprimer une boîte aux lettres</a></p></td>
<td><p>Apprenez à désactiver ou supprimer des boîtes aux lettres.</p></td>
</tr>
<tr class="even">
<td><p><a href="connect-a-disabled-mailbox-exchange-2013-help.md">Connecter une boîte aux lettres déconnectée</a></p></td>
<td><p>Apprenez à connecter une boîte aux lettres désactivée à un compte d’utilisateur existant.</p></td>
</tr>
<tr class="odd">
<td><p><a href="connect-or-restore-a-deleted-mailbox-exchange-2013-help.md">Connexion ou restauration d’une boîte aux lettres supprimée</a></p></td>
<td><p>Apprenez à connecter une boîte aux lettres supprimée à un compte d’utilisateur ou à restaurer le contenu d’une boîte aux lettres supprimée dans une boîte aux lettres existante.</p></td>
</tr>
<tr class="even">
<td><p><a href="restore-a-soft-deleted-mailbox-exchange-2013-help.md">Restaurer une boîte aux lettres supprimée (récupérable)</a></p></td>
<td><p>Apprenez à connecter une boîte aux lettres supprimée à un compte d’utilisateur ou à restaurer une boîte aux lettres supprimée (récupérable) dans une boîte aux lettres existante.</p></td>
</tr>
<tr class="odd">
<td><p><a href="manage-mailbox-restore-requests-exchange-2013-help.md">Gérer les demandes de restauration de boîte aux lettres</a></p></td>
<td><p>Apprenez à gérer les demandes de restauration de boîtes aux lettres à l’aide de l’environnement de ligne de commande Exchange Management Shell.</p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p><a href="permanently-delete-a-mailbox-exchange-2013-help.md">Supprimer définitivement une boîte aux lettres</a></p></td>
<td><p>Apprenez à supprimer définitivement une boîte aux lettres.</p></td>
</tr>
</tbody>
</table>


Utilisation de boîtes aux lettres désactivées

