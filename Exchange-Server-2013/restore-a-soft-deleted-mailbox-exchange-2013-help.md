---
title: 'Restaurer une boîte aux lettres supprimée (récupérable): Exchange 2013 Help'
TOCTitle: Restaurer une boîte aux lettres supprimée (récupérable)
ms:assetid: 4f3f5ce4-9d12-4ed8-9f70-d8a6aa8a1b2e
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ863435(v=EXCHG.150)
ms:contentKeyID: 50555395
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Restaurer une boîte aux lettres supprimée (récupérable)

 

_**Sapplique à :** Exchange Online, Exchange Server 2013_

_**Dernière rubrique modifiée :** 2012-11-29_

Connexion d’une boîte aux lettres supprimée (récupérable) à un compte d’utilisateur Active Directory à l’aide de l’environnement de ligne de commande Exchange Management Shell. Une boîte aux lettres est *supprimée (récupérable)* dans la base de données de boîtes aux lettres source lorsqu’elle est déplacée vers une autre base de données de boîtes aux lettres. Exchange ne supprime pas entièrement la boîte aux lettres de la base de données de boîtes aux lettres source une fois le déplacement terminé. Au lieu de cela, la boîte aux lettres qui se trouve dans la base de données de boîtes aux lettres source bascule vers l’état supprimé (récupérable). Il vous permet de restaurer la boîte aux lettres source si des erreurs provoquant une défaillance ou un endommagement de la boîte aux lettres sur la base de données de destination se produisent pendant le déplacement. Si cela se produit, vous pouvez restaurer la boîte aux lettres source et réessayer l’opération de déplacement.

Une boîte aux lettres supprimée (récupérable) est conservée dans la base de données source jusqu’à l’expiration de la période de rétention de la boîte aux lettres ou jusqu’au vidage de la boîte aux lettres supprimée à l’aide de la cmdlet **Remove-StoreMailbox**. Tant qu’une boîte aux lettres supprimée (récupérable) n’est pas définitivement supprimée de la base de données de boîtes aux lettres Exchange, vous pouvez utiliser l’environnement de ligne de commande Exchange Management Shell pour restaurer le contenu de la boîte aux lettres dans une boîte aux lettres existante ou une boîte aux lettres d’archivage.

Pour en savoir plus sur les boîtes aux lettres supprimées (récupérables) et exécuter d’autres tâches de gestion, consultez les rubriques suivantes :

  - [Boîtes aux lettres déconnectées](disconnected-mailboxes-exchange-2013-help.md)

  - [Connexion ou restauration d’une boîte aux lettres supprimée](connect-or-restore-a-deleted-mailbox-exchange-2013-help.md)

  - [Gérer les demandes de restauration de boîte aux lettres](manage-mailbox-restore-requests-exchange-2013-help.md)

  - [Supprimer définitivement une boîte aux lettres](permanently-delete-a-mailbox-exchange-2013-help.md)

## Ce qu’il faut savoir avant de commencer ?

  - Durée d'exécution estimée : 2 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Section « Autorisations de configuration des destinataires » dans la rubrique [Autorisations des destinataires](recipients-permissions-exchange-2013-help.md).

  - Les procédures décrites dans cette rubrique ne peuvent être effectuées dans l'environnement de ligne de commande Exchange Management Shell. Il n’est pas possible de restaurer des boîtes aux lettres supprimées (récupérables) à l’aide du Centre d’administration Exchange.

  - Exécutez la commande suivante pour vérifier que la boîte aux lettres supprimée (récupérable) à laquelle vous souhaitez connecter un compte d’utilisateur existe toujours dans la base de données de boîtes aux lettres et qu’elle n’est pas désactivée :
    
    ```powershell
    Get-MailboxDatabase | Get-MailboxStatistics | Where { $_.DisplayName -eq "<display name>" } | fl DisplayName,DisconnectReason,DisconnectDate
    ```
    
    La boîte aux lettres supprimée (récupérable) doit exister dans la base de données de boîtes aux lettres et la valeur de la propriété *DisconnectReason* doit être `SoftDeleted`. Si la boîte aux lettres a été purgée de la base de données, la commande ne renvoie aucun résultat.
    
    Vous pouvez également exécuter la commande suivante pour afficher toutes les boîtes aux lettres supprimées (récupérables) de votre organisation :
    
    ```powershell
    Get-MailboxDatabase | Get-MailboxStatistics | Where { $_.DisconnectReason -eq "SoftDeleted" } | fl DisplayName,DisconnectReason,DisconnectDate
    ```

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

  - Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), et [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)..

## Restaurer une boîte aux lettres supprimée (récupérable) via l’environnement de ligne de commande Exchange Management Shell

Vous pouvez utiliser l’environnement de ligne de commande Exchange Management Shell pour restaurer une boîte aux lettres supprimée (récupérable) dans une boîte aux lettres existante à l’aide de la cmdlet **New-MailboxRestoreRequest**. Lorsque vous restaurez une boîte aux lettres supprimée (récupérable), son contenu est copié dans une boîte aux lettres existante appelée *boîte aux lettres cible*. Une fois qu’une demande de restauration de boîte aux lettres a été correctement traitée, elle est conservée par défaut pendant 30 jours avant d’être supprimée. Vous pouvez la supprimer plus tôt à l’aide de la cmdlet **Remove-MailboxRestoreRequest**.

Une fois que vous avez restauré une boîte aux lettres supprimée (récupérable), celle-ci est conservée dans la base de données de boîtes aux lettres jusqu’à sa suppression définitive par un administrateur ou sa purge à l’expiration de la période de rétention de la boîte aux lettres supprimée.

Pour créer une demande de restauration de boîte aux lettres, vous devez utiliser le nom complet, le GUID de la boîte aux lettres ou le nom unique hérité de la boîte aux lettres supprimée (récupérable). Utilisez la cmdlet **Get-MailboxStatistics** pour afficher les valeurs des propriétés **DisplayName**, **MailboxGuid** et **LegacyDN** de la boîte aux lettres supprimée (récupérable) à restaurer. Par exemple, exécutez la commande suivante pour renvoyer ces informations sur toutes les boîtes aux lettres désactivées et supprimées (récupérables) de votre organisation :

```powershell
Get-MailboxDatabase | Get-MailboxStatistics | Where {$_.DisconnectReason -eq "SoftDeleted"} | fl DisplayName,MailboxGuid,LegacyDN,Database
```

Cet exemple montre comment restaurer une boîte aux lettres supprimée (récupérable), qui est identifiée par le nom complet dans le paramètre *SourceStoreMailbox* et située dans la base de données de boîtes aux lettres MBXDB01, dans la boîte aux lettres cible appelée Debra Garcia. Le paramètre *AllowLegacyDNMismatch* est utilisé de sorte à pouvoir restaurer la boîte aux lettres source dans une boîte aux lettres ne possédant pas la même valeur de nom unique hérité que celle de la boîte aux lettres supprimée (récupérable).

```powershell
New-MailboxRestoreRequest -SourceStoreMailbox "Debra Garcia" -SourceDatabase MBXDB01 -TargetMailbox "Debra Garcia" -AllowLegacyDNMismatch
```

Cet exemple montre comment restaurer la boîte aux lettres d’archivage supprimée (récupérable) de Pilar Pinilla, identifiée par le GUID de boîte aux lettres, dans sa boîte aux lettres d’archivage actuelle. Le paramètre *AllowLegacyDNMismatch* n’est pas nécessaire, car une boîte aux lettres principale et sa boîte aux lettres d’archivage correspondante comportent le même nom unique hérité.

```powershell
New-MailboxRestoreRequest -SourceStoreMailbox dc35895a-a628-4bba-9aa9-650f5cdb9ae7 -SourceDatabase MBXDB02 -TargetMailbox pilarp@contoso.com -TargetIsArchive
```

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [New-MailboxRestoreRequest](https://technet.microsoft.com/fr-fr/library/ff829875\(v=exchg.150\)).

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez bien restauré une boîte aux lettres supprimée (récupérable) dans la boîte aux lettres cible, exécutez la cmdlet **Get-MailboxRestoreRequest** ou la cmdlet **Get-MailboxRestoreRequestStatistics** pour afficher les informations sur la demande de restauration. Si la demande de restauration a été correctement créée, la propriété *Status* aura la valeur **Queued**, **InProgress** ou **Completed**. Une fois la demande de restauration traitée, le contenu de la boîte aux lettres supprimée (récupérable) apparaît dans la boîte aux lettres cible.

Pour plus d’informations, voir :

  - [Gérer les demandes de restauration de boîte aux lettres](manage-mailbox-restore-requests-exchange-2013-help.md)

  - [Get-MailboxRestoreRequest](https://technet.microsoft.com/fr-fr/library/ff829907\(v=exchg.150\))

  - [Get-MailboxRestoreRequestStatistics](https://technet.microsoft.com/fr-fr/library/ff829912\(v=exchg.150\))

