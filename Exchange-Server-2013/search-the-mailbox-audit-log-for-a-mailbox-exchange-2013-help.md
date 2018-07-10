---
title: 'Rechercher une boîte aux lettres dans le journal d’audit de boîte aux lettres: Exchange 2013 Help'
TOCTitle: Rechercher une boîte aux lettres dans le journal d’audit de boîte aux lettres
ms:assetid: 5b518a08-3b51-4ba3-bfbd-0e35cc5ff374
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Ff461930(v=EXCHG.150)
ms:contentKeyID: 50478268
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Rechercher une boîte aux lettres dans le journal d’audit de boîte aux lettres

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2012-10-03_

Vous pouvez effectuer des recherches de manière synchrone sur les entrées de journaux d’audit de boîte aux lettres d’une boîte aux lettres et afficher les résultats de la recherche dans l’environnement de ligne de commande Exchange Management Shell.

Si vous voulez effectuer des recherches sur les journaux d’audits de boîtes aux lettres de plusieurs boîtes aux lettres et envoyer les résultats par courrier électronique à une adresse spécifiée, vous devez créer à la place une recherche de journal d’audit de boîtes aux lettres. Pour plus d’informations, consultez la rubrique [Créer une recherche dans le journal d’audit de la boîte aux lettres](create-a-mailbox-audit-log-search-exchange-2013-help.md).

Pour les autres tâches de gestion relatives à l’enregistrement d’audit des boîtes aux lettres, voir [Procédures d'enregistrement d’audit des boîtes aux lettres](mailbox-audit-logging-procedures-exchange-2013-help.md).

## Ce qu’il faut savoir avant de commencer ?

  - Durée d'exécution estimée : 1 minute.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l’entrée « Journaux d’audit de boîtes aux lettres » dans la rubrique [Stratégie de messagerie et autorisations de conformité](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

  - Par défaut, l’enregistrement d’audit de boîte aux lettres est désactivé pour toutes les boîtes aux lettres. Pour chaque boîte aux lettres que vous souhaitez auditer, vous devez activer l’enregistrement d’audit et spécifier les actions du propriétaire, délégué ou administrateur de la boîte aux lettres que vous voulez auditer. Pour plus d’informations, consultez la rubrique [Activer ou désactiver l’enregistrement d’audit pour une boîte aux lettres](enable-or-disable-mailbox-audit-logging-for-a-mailbox-exchange-2013-help.md).

  - Vous ne pouvez pas utiliser l’EAC pour effectuer des recherches dans un journal d’audit de boîtes aux lettres d’une boîte aux lettres. Cependant, vous pouvez utiliser l'EAC pour l'exécution ou la recherche et exporter un rapport d'accès à la boîte aux lettres non propriétaire.

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.


## Utilisation de l’environnement de ligne de commande Exchange Management Shell pour effectuer des recherches dans le journal d’audit de boîte aux lettres d’une boîte aux lettres

Pour obtenir des exemples sur comment utiliser le Shell pour la recherche du journal d'audit de boîtes aux lettres d'une boîte aux lettres, consultez [Examples](https://technet.microsoft.com/fr-fr/ff522360\(exchg.150\)#examples) dans [Search-MailboxAuditLog](https://technet.microsoft.com/fr-fr/library/ff522360\(v=exchg.150\)).

