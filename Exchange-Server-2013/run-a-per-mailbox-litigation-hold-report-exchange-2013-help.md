---
title: 'Exécuter un rapport de suspension pour litige par BAL: Exchange 2013 Help'
TOCTitle: Exécuter un rapport de suspension pour litige par boîte aux lettres
ms:assetid: 98c46226-2f48-42c6-a741-34bb5944f519
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ150542(v=EXCHG.150)
ms:contentKeyID: 50477290
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exécuter un rapport de suspension pour litige par boîte aux lettres

 

_**Sapplique à :** Exchange Online, Exchange Server 2013_

_**Dernière rubrique modifiée :** 2012-10-13_

Si votre organisation est impliquée dans une action légale, vous devrez peut-être prendre des mesures pour conserver des données pertinentes, telles que les messages électroniques, qui peuvent être utilisées comme preuves. Dans de telles situations, vous pouvez utiliser la suspension pour litige pour conserver tous les messages électroniques envoyés et reçus par des personnes spécifiques ou conserver tous les messages électroniques envoyés et reçus dans votre organisation pour une période donnée. Pour plus d'informations sur ce qui se passe lorsqu'une boîte aux lettres est en suspension pour litige et sur la façon d'activer et de désactiver cette suspension, consultez la section « Fonctionnalités des boîtes aux lettres », à la rubrique [Gestion des boîtes aux lettres utilisateur](manage-user-mailboxes-exchange-2013-help.md).

Utilisez le rapport de suspension pour litige pour effectuer le suivi des types suivants de modifications apportées à une boîte aux lettres sur une période donnée :

  - La suspension pour litige a été activée.

  - La suspension pour litige a été désactivée.

Pour chacun de ces types de modifications, le rapport inclut l'utilisateur qui l'a apportée et l'heure et la date de la modification.

## Ce qu’il faut savoir avant de commencer ?

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l’entrée « Enregistrement d’audit d’administrateur en affichage seul » dans la rubrique [Autorisations d’infrastructure Exchange et Shell](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..


## Utiliser le Centre d'administration Exchange pour exécuter un rapport de suspension pour litige

1.  Dans le Centre d’administration Exchange, rendez-vous sur **Gestion de la conformité** \> **Audit**.

2.  Cliquez sur **Exécuter un rapport de suspension pour litige par boîte aux lettres**.
    
    Microsoft Exchange exécute le rapport pour toutes les modifications de suspension pour litige apportées à une boîte aux lettres au cours des deux semaines passées.

3.  Pour consulter les modifications apportées à une boîte aux lettres spécifique, dans le volet des résultats de la recherche, sélectionnez la boîte aux lettres. Consultez les résultats de la recherche dans le volet d’informations.

> [!TIP]
> Souhaitez-vous affiner les résultats de la recherche ? Sélectionnez la date de début, la date de fin, ou les deux, et sélectionnez des boîtes aux lettres spécifiques dans lesquelles effectuer la recherche. Cliquez sur <strong>Rechercher</strong> pour réexécuter le rapport.


## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez correctement exécuté un rapport de suspension pour litige, voyez si les boîtes aux lettres auxquelles des modifications de suspension pour litige ont été apportées dans la plage de dates sont affichées dans le volet des résultats de la recherche. Si le volet ne contient aucun résultat, cela signifie qu'aucune modification de suspension pour litige n'a été apportée dans la plage de dates ou que les modifications récentes n'ont pas encore pris effet.

> [!NOTE]
> Lorsqu'une boîte aux lettres est placée en suspension pour litige, il peut falloir jusqu'à 60 minutes pour que cette dernière prenne effet.

