---
title: 'Supprimer définitivement une boîte aux lettres: Exchange 2013 Help'
TOCTitle: Supprimer définitivement une boîte aux lettres
ms:assetid: df35765a-0bef-4561-9846-d91d69c0269c
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ863440(v=EXCHG.150)
ms:contentKeyID: 50555507
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Supprimer définitivement une boîte aux lettres

 

_**Sapplique à :** Exchange Online, Exchange Server 2013_

_**Dernière rubrique modifiée :** 2012-11-16_

Lorsque vous supprimez définitivement des boîtes aux lettres actives et des boîtes aux lettres déconnectées, tous les contenus des boîtes aux lettres sont purgés de la base de données des boîtes aux lettres Exchange, et la perte des données est définitive. Lorsque vous supprimez définitivement une boîte aux lettres active, le compte utilisateur Active Directory associé est également supprimé.

Une alternative à la suppression définitive d’une boîte aux lettres consiste à la déconnecter. Après avoir déconnecté une boîte aux lettres, par défaut, celle-ci est maintenue pendant 30 jours dans la base de données de boîtes aux lettres. Ainsi, vous avez encore l’opportunité de reconnecter ou de restaurer une boîte aux lettres avant qu’elle ne soit purgée de la base de données.

Pour plus d’informations sur les boîtes aux lettres déconnectées et sur l’exécution des autres tâches de gestion associées, consultez les rubriques suivantes :

  - [Boîtes aux lettres déconnectées](disconnected-mailboxes-exchange-2013-help.md)

  - [Désactiver ou supprimer une boîte aux lettres](disable-or-delete-a-mailbox-exchange-2013-help.md)

  - [Connecter une boîte aux lettres déconnectée](connect-a-disabled-mailbox-exchange-2013-help.md)

  - [Connexion ou restauration d’une boîte aux lettres supprimée](connect-or-restore-a-deleted-mailbox-exchange-2013-help.md)

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Vous ne pouvez pas utiliser le Centre d’administration Exchange (EAC) pour supprimer définitivement une boîte aux lettres active ou déconnectée.</td>
</tr>
</tbody>
</table>


## Ce qu’il faut savoir avant de commencer ?

  - Durée d'exécution estimée : 2 minutes.

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

## Supprimer définitivement une boîte aux lettres active

## Utiliser l’environnement de ligne de commande Exchange Management Shell pour supprimer définitivement une boîte aux lettres active

Exécuter la commande suivante pour supprimer définitivement une boîte aux lettres active et le compte utilisateur Active Directory associé.

    Remove-Mailbox -Identity <identity> -Permanent $true

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Si vous n’incluez pas le paramètre <em>Permanent</em>, la boîte aux lettres est conservée dans la base de données de boîtes aux lettres pendant 30 jours, par défaut, avant d’être supprimée définitivement.</td>
</tr>
</tbody>
</table>


Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Remove-Mailbox](https://technet.microsoft.com/fr-fr/library/aa995948\(v=exchg.150\)).

## Comment savoir si cela a fonctionné ?

Pour vérifier qu’une boîte aux lettres active a été définitivement supprimée, procédez comme suit :

1.  Vérifiez que la boîte aux lettres n’est plus répertoriée dans le Centre d’administration Exchange (EAC).

2.  Vérifiez que le compte utilisateur associé n’apparaît plus dans le composant Utilisateurs et ordinateurs Active Directory.

3.  Exécutez la commande suivante pour vérifier que la boîte aux lettres a bien été purgée de la base de données de boîtes aux lettres Exchange.
    
        Get-MailboxDatabase | Get-MailboxStatistics | Where { $_.DisplayName -eq "<display name>" }
    
    Si la boîte aux lettres a bien été purgée, la commande ne doit renvoyé aucun résultat. Sinon, la commande renvoie des informations sur la boîte aux lettres.

## Suppression définitive d’une boîte aux lettres déconnectée

## Utiliser l’environnement de ligne de commande Exchange Management Shell pour supprimer définitivement une boîte aux lettres déconnectée

Il existe deux types de boîtes aux lettres déconnectées : désactivé et supprimé (récupérable). Vous devez spécifier l’un de ces types lorsque vous exécutez la cmdlet pour supprimer définitivement la boîte aux lettres. Si le type que vous spécifiez ne correspond pas au type réel de la boîte aux lettres déconnectée, la commande échoue.

Exécutez la commande suivante pour déterminer si une boîte aux lettres déconnectée est de type désactivé ou supprimé (récupérable).

    Get-MailboxDatabase | Get-MailboxStatistics | Where { $_.DisplayName -eq "<display name>" } | fl DisplayName,MailboxGuid,Database,DisconnectReason

La valeur de la propriété *DisconnectReason* pour des boîtes aux lettres déconnectées doit être `Disabled` ou `SoftDeleted`.

Exécuter la commande suivante pour afficher le type de toutes les boîtes aux lettres déconnectées de votre organisation.

    Get-MailboxDatabase | Get-MailboxStatistics | Where { $_.DisconnectReason -ne $null } | fl DisplayName,MailboxGuid,Database,DisconnectReason

<table>
<thead>
<tr class="header">
<th><img src="images/Bb125224.warning(EXCHG.150).gif" title="Avertissement" alt="Avertissement" />Avertissement :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Lorsque vous utilisez la cmdlet <strong>Remove-StoreMailbox</strong> pour supprimer définitivement une boîte aux lettres déconnectée, tout son contenu est purgé de la base de données de boîtes aux lettres et la perte des données est définitive.</td>
</tr>
</tbody>
</table>


Cet exemple supprime définitivement la boîte aux lettres désactivée portant le GUID 2ab32ce3-fae1-4402-9489-c67e3ae173d3 de la base de données de boîtes aux lettres MBD01.

    Remove-StoreMailbox -Database MBD01 -Identity "2ab32ce3-fae1-4402-9489-c67e3ae173d3" -MailboxState Disabled

Cet exemple illustre la suppression définitive de la boîte aux lettres supprimée (récupérable) de Dan Jump de la base de données de boîtes aux lettres MBD01.

    Remove-StoreMailbox -Database MBD01 -Identity "Dan Jump" -MailboxState SoftDeleted

Cet exemple supprime définitivement toutes les boîtes aux lettres supprimées (récupérables) de la base de données de boîtes aux lettres MBD01.

    Get-MailboxStatistics -Database MBD01 | where {$_.DisconnectReason -eq "SoftDeleted"} | ForEach {Remove-StoreMailbox -Database $_.Database -Identity $_.MailboxGuid -MailboxState SoftDeleted}

Pour des informations détaillées sur la syntaxe et les paramètres, consultez les rubriques [Remove-StoreMailbox](https://technet.microsoft.com/fr-fr/library/ff829913\(v=exchg.150\)) et [Get-MailboxStatistics](https://technet.microsoft.com/fr-fr/library/bb124612\(v=exchg.150\)).

## Comment savoir si cela a fonctionné ?

Pour vérifier que la suppression de la boîte aux lettres déconnectée est définitive et qu’elle a bien été purgée de la base de données de boîtes aux lettres Exchange, exécutez la commande suivante.

    Get-MailboxDatabase | Get-MailboxStatistics | Where { $_.DisplayName -eq "<display name>" }

Si la boîte aux lettres a bien été purgée, la commande ne doit renvoyé aucun résultat. Sinon, la commande renvoie des informations sur la boîte aux lettres.

