---
title: 'Activation de la récupération d’élément unique pour une boîte aux lettres: Exchange 2013 Help'
TOCTitle: Activation de la récupération d’élément unique pour une boîte aux lettres
ms:assetid: 2e7f1bcd-8395-45ad-86ce-22868bd46af0
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Ee633460(v=EXCHG.150)
ms:contentKeyID: 54652726
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Activation de la récupération d’élément unique pour une boîte aux lettres

 

_**Sapplique à :**Exchange Online, Exchange Server 2013_

_**Dernière rubrique modifiée :**2015-03-13_

Vous pouvez utiliser l’environnement de ligne de commande Exchange Management Shell pour activer ou désactiver la fonctionnalité de récupération d’élément unique sur une boîte aux lettres. Dans Exchange Online, la récupération d’élément unique est activée par défaut lors de la création d’une boîte aux lettres. Dans Exchange 2013, la récupération d’élément unique est désactivée lors de la création d’une boîte aux lettres. Quand cette fonctionnalité est activée, les messages que l’utilisateur a supprimés définitivement (purgés) sont conservés dans le dossier Éléments récupérables de la boîte aux lettres jusqu’à l’expiration de la période de rétention des éléments supprimés. Cela permet aux administrateurs de récupérer les messages supprimés définitivement par l’utilisateur avant l’expiration de la période de rétention des éléments supprimés. En outre, si un message est modifié par un utilisateur ou un processus, des copies de l’élément d’origine sont également conservées lorsque la fonctionnalité de récupération d’élément unique est activée.

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : 2 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l'entrée « Rétention et suspens pour raisons juridiques » dans la rubrique [Autorisations des destinataires](recipients-permissions-exchange-2013-help.md).

  - Vous ne pouvez pas utiliser le Centre d’administration Exchange (CAE) pour activer ou désactiver la fonctionnalité de récupération d’élément unique.

  - Dans Exchange Online, la période de rétention des éléments supprimés est par défaut définie sur 14 jours. Vous pouvez augmenter la valeur de ce paramètre jusqu'à 30 jours au maximum. Pour plus d’informations, consultez la rubrique [Modifier la durée de conservation des éléments supprimés définitivement pour une boîte aux lettres Exchange Online](https://technet.microsoft.com/fr-fr/library/dn163584\(v=exchg.150\))

  - Dans Exchange 2013, la boîte aux lettres utilise les paramètres de rétention des éléments supprimés de la base de données de boîtes aux lettres, par défaut. La période de rétention des éléments supprimés dans une base de données de boîtes aux lettres est définie sur 14 jours, mais vous pouvez remplacer la valeur par défaut en configurant ce paramètre pour chaque boîte aux lettres. Pour plus d'informations, consultez la rubrique [Configurer la rétention des éléments supprimés et les quotas d’éléments récupérables](configure-deleted-item-retention-and-recoverable-items-quotas-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), et [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)..

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour activer la fonctionnalité de récupération d'élément unique

Cet exemple permet d'activer la fonctionnalité de récupération d'élément unique pour la boîte aux lettres d'April Summers.

    Set-Mailbox -Identity "April Summers" -SingleItemRecoveryEnabled $true

Cet exemple permet d'activer la fonctionnalité de récupération d'élément unique pour la boîte aux lettres de Pilar Pinilla et de définir la période de rétention des éléments supprimés sur 30 jours.

    Set-Mailbox -Identity "Pilar Pinilla" -SingleItemRecoveryEnabled $true -RetainDeletedItemsFor 30

Cet exemple permet d'activer la fonctionnalité de récupération d'élément unique pour toutes les boîtes aux lettres d'utilisateurs au sein de l'organisation.

    Get-Mailbox -ResultSize unlimited -Filter {(RecipientTypeDetails -eq 'UserMailbox')} | Set-Mailbox -SingleItemRecoveryEnabled $true

Cet exemple active la fonctionnalité de récupération d’élément unique pour toutes les boîtes aux lettres d’utilisateur dans l’organisation et définit le nombre de jours pendant lesquels les éléments supprimés sont conservés sur 30 jours

    Get-Mailbox -ResultSize unlimited -Filter {(RecipientTypeDetails -eq 'UserMailbox')} | Set-Mailbox -SingleItemRecoveryEnabled $true -RetainDeletedItemsFor 30

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, consultez la rubrique [Set-Mailbox](https://technet.microsoft.com/fr-fr/library/bb123981\(v=exchg.150\)).

## Utiliser l’environnement de ligne de commande Exchange Management Shell pour désactiver la fonctionnalité de récupération d’élément unique

Vous devrez peut-être désactiver la récupération d’élément unique pour la boîte aux lettres d’un utilisateur. Par exemple, pour pouvoir utiliser **Search-Mailbox –DeleteContent** pour supprimer définitivement le contenu d’une boîte aux lettres, vous devez désactiver la récupération d’élément unique. Pour plus d’informations, voir [Recherche et suppression de messages - Aide de l’administrateur](search-for-and-delete-messages-admin-help-exchange-2013-help.md).

Cet exemple permet de désactiver la fonctionnalité de récupération d’élément unique pour la boîte aux lettres d’Ayla Kol.

    Set-Mailbox -Identity "Ayla Kol" -SingleItemRecoveryEnabled $false

## Comment savoir si cela a fonctionné ?

Exécutez la commande suivante pour vérifier que vous avez bien activé la fonctionnalité de récupération d’élément unique sur une boîte aux lettres et afficher la période de rétention des éléments supprimés (en jours) :

    Get-Mailbox <Name> | FL SingleItemRecoveryEnabled,RetainDeletedItemsFor

Vous pouvez utiliser cette même commande pour vérifier que la récupération d’élément unique est désactivée sur une boîte aux lettres.

## Plus d’informations

  - Pour en savoir plus sur la fonctionnalité de récupération d'élément unique, consultez la rubrique [Dossier Éléments récupérables](recoverable-items-folder-exchange-2013-help.md). Pour récupérer des messages que l’utilisateur a supprimés définitivement avant l’expiration de la période de rétention des éléments supprimés, consultez la rubrique [Récupérer des messages supprimés dans la boîte aux lettres d’un utilisateur](recover-deleted-messages-in-a-user-s-mailbox-exchange-2013-help.md).

  - Si une boîte aux lettres est placée sur Conservation inaltérable ou Conservation pour litige, les messages du dossier Éléments récupérables sont conservés jusqu’à l’expiration de la durée de la conservation. Si la durée de la conservation est illimitée, les éléments sont conservés jusqu’à la suppression de la conservation ou la modification de la durée de la conservation.

