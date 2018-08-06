---
title: "Configurer des propriétés d’une liste d’adresses globale: Exchange 2013 Help | Microsoft Docs"
TOCTitle: Configuration des propriétés d'une liste d'adresses globale
ms:assetid: 5fd2c96f-fe93-4b5a-8495-70c450511a37
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb232068(v=EXCHG.150)
ms:contentKeyID: 50478298
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configuration des propriétés d'une liste d'adresses globale

 

_**Sapplique à :** Exchange Online, Exchange Server 2013_

_**Dernière rubrique modifiée :** 2014-12-16_

Cette rubrique explique comment modifier les paramètres d'une liste d'adresses globale (LAG).

Pour les autres tâches de gestion relatives aux listes d'adresses, consultez la rubrique [Procédures des listes d'adresses](address-list-procedures-exchange-2013-help.md).

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée de chaque procédure : 5 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l'entrée « Listes d'adresses » dans la rubrique [Autorisations pour configurer les adresses de messagerie et les carnets d’adresses](email-address-and-address-book-permissions-exchange-2013-help.md).

  - Par défaut dans Exchange Online, le rôle de liste d’adresses n’est affecté à aucun groupe de rôles. Pour utiliser les cmdlets nécessitant le rôle Liste d’adresses, vous devez ajouter ce dernier à un groupe de rôles. Pour plus d’informations, consultez la section « Ajouter un rôle à un groupe de rôles » de la rubrique [Gérer des groupes de rôles](manage-role-groups-exchange-2013-help.md).

  - Vous ne pouvez pas modifier les paramètres de la liste d'adresses globale par défaut.

  - Vous ne pouvez pas utiliser le Centre d’administration Exchange (CAE) pour effectuer cette procédure. Vous devez utiliser l'environnement de ligne de commande Exchange Management Shell.

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.


## Utiliser l'environnement de ligne de commande Exchange Management Shell pour configurer les propriétés de la liste d'adresses globale

Cet exemple attribue un nom nouveau, FourthCoffee, à la liste d'adresses globale dont le GUID est 96d0c505-eba8-4103-ad4f-577a1bf4ad7b.

    Set-GlobalAddressList -Identity 96d0c505-eba8-4103-ad4f-577a1bf4ad7b -Name FourthCoffee

> [!NOTE]
> Si vous utilisez des propriétés de filtrage conditionnel prédéfinies, la valeur du paramètre <em>IncludedRecipients</em> ne peut pas être vide.


Cet exemple modifie les destinataires qui seront inclus dans la ligne d'adresses globale Fourth Coffee à celles dont la société est définie à Fourth Coffee.

    Set-GlobalAddressList -Identity Fourth Coffee -RecipientFilter {Company -eq "Fourth Coffee"}

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, consultez la rubrique [Set-GlobalAddressList](https://technet.microsoft.com/fr-fr/library/bb123877\(v=exchg.150\)).

