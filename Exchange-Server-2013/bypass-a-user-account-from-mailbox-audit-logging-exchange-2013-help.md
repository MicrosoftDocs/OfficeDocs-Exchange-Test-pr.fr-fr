---
title: "Contournement d'un compte d'utilisateur lors de la journalisation d'audit des boîtes aux lettres: Exchange 2013 Help"
TOCTitle: Contournement d'un compte d'utilisateur lors de la journalisation d'audit des boîtes aux lettres
ms:assetid: 98a87071-fe31-4b67-beb8-a73799e54df2
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Ff461934(v=EXCHG.150)
ms:contentKeyID: 50478767
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Contournement d'un compte d'utilisateur lors de la journalisation d'audit des boîtes aux lettres

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2013-05-21_

Lorsque vous activez la fonctionnalité d'enregistrement d'audit pour une boîte aux lettres, les événements d'accès à la boîte aux lettres spécifiée (par exemple, accès à un dossier ou un message, ou suppression permanente d'un message) sont enregistrés. Toutefois, l'accès par certains comptes autorisés, tels que les comptes utilisés par des outils tiers ou aux fins de surveillance licite, peut entraîner la création d'un grand nombre d'entrées de journal d'audit de boîte aux lettres et s'avérer être sans intérêt pour votre organisation.

Vous pouvez configurer un compte d'utilisateur ou d'ordinateur pour ignorer l'enregistrements d'audit de boîtes aux lettres afin que les actions de cet utilisateur ou de ce compte ne soient pas enregistrées pour l'ensemble des boîtes aux lettres. En ignorant des comptes d'utilisateur ou d'ordinateur approuvés nécessitant un accès fréquent aux boîtes aux lettres, vous pouvez réduire le bruit dans les journaux d'audit des boîtes aux lettres.

> [!CAUTION]
> Si vous utilisez l'enregistrement d'audit de boîte aux lettres pour auditer les accès aux boîtes aux lettres et les actions s'y rapportant, vous devez surveiller les associations de contournement d'audit de boîtes aux lettres à intervalles réguliers. Si une association de contournement d'audit de boîtes aux lettres est ajoutée à un compte, celui-ci peut accéder à n'importe quelle boîte aux lettres de l'organisation pour laquelle il a reçu des autorisations d'accès, sans que des entrées d'enregistrement d'audit de boîte aux lettres ne soient générées à chaque accès ou action entreprise (par exemple, suppression de messages).


Pour les autres tâches de gestion relatives à la journalisation d'audit des boîtes aux lettres, consultez la rubrique [Procédures d'enregistrement d’audit des boîtes aux lettres](mailbox-audit-logging-procedures-exchange-2013-help.md).

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : 1 minute.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l'entrée « Journalisation d'audit de boîte aux lettres » dans la rubrique [Stratégie de messagerie et autorisations de conformité](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

  - Lorsqu'un compte est configuré pour ignorer la journalisation d'audit de boîte aux lettres, l'accès à une quelconque boîte aux lettres par ce compte ne sera pas enregistré. Vous ne pouvez pas configurer un compte pour qu'il ignore l'enregistrement des accès à une boîte aux lettres spécifique.

  - Vous ne pouvez pas utiliser le Centre d'administration Exchange (CAE) pour activer ou désactiver le contournement de la journalisation d'audit de boîte aux lettres d'un compte. Vous devez utiliser l'environnement de ligne de commande Exchange Management Shell.

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.


## Utiliser l'environnement de ligne de commande Exchange Management Shell pour activer ou désactiver le contournement de la journalisation d'audit de boîte aux lettres d'un compte

Pour comprendre comment activer un contournement de journalisation d'audit de boîtes aux lettres pour un compte, consultez [Examples](https://technet.microsoft.com/fr-fr/ff696758\(exchg.150\)#examples) dans [Set-MailboxAuditBypassAssociation](https://technet.microsoft.com/fr-fr/library/ff696758\(v=exchg.150\)).

Pour comprendre comment désactiver un contournement d'enregistrement d'audit de boîtes aux lettres pour un compte, consultez l'[Examples](https://technet.microsoft.com/fr-fr/ff696758\(exchg.150\)#examples) de la rubrique [Set-MailboxAuditBypassAssociation](https://technet.microsoft.com/fr-fr/library/ff696758\(v=exchg.150\)).

## Comment savoir si cela a fonctionné ?

Après avoir contourné l'enregistrement d'audit de boîte aux lettres pour un compte d'utilisateur, vous pouvez vérifier les paramètres de contournement en exécutant la cmdlet [Get-MailboxAuditBypassAssociation](https://technet.microsoft.com/fr-fr/library/ff696741\(v=exchg.150\)).

Pour comprendre comment vérifier ldes associations de contournement d'audit de boîtes aux lettres, consultez les [Examples](https://technet.microsoft.com/fr-fr/ff696741\(exchg.150\)#examples) de la rubrique [Get-MailboxAuditBypassAssociation](https://technet.microsoft.com/fr-fr/library/ff696741\(v=exchg.150\)).

