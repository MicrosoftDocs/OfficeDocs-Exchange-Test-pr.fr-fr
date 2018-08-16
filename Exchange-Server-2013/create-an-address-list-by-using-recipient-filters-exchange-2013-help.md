---
title: 'Liste d’adresses: création avec filtres de destinataires: Exchange 2013 Help'
TOCTitle: Création d’une liste d’adresses à l’aide de filtres de destinataires
ms:assetid: 8eabea64-97c6-40af-b61c-9b6a125cbdf1
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb123718(v=EXCHG.150)
ms:contentKeyID: 50478685
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Création d’une liste d’adresses à l’aide de filtres de destinataires

 

_**Sapplique à :** Exchange Online, Exchange Server 2013_

_**Dernière rubrique modifiée :** 2014-12-16_

Cette rubrique décrit la création d'une liste d'adresses en utilisant des filtres de destinataires. Pour en savoir plus sur les listes d'adresses, consultez la rubrique [Listes d’adresses](address-lists-exchange-2013-help.md).

Pour les autres tâches de gestion relatives aux listes d'adresses, consultez la rubrique [Procédures des listes d'adresses](address-list-procedures-exchange-2013-help.md).

## Ce qu’il faut savoir avant de commencer ?

  - Durée d'exécution estimée de chaque procédure : 5 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l'entrée « Listes d'adresses » dans la rubrique [Autorisations pour configurer les adresses de messagerie et les carnets d’adresses](email-address-and-address-book-permissions-exchange-2013-help.md).

  - Par défaut dans Exchange Online, le rôle de liste d’adresses n’est affecté à aucun groupe de rôles. Pour utiliser les cmdlets nécessitant le rôle Liste d’adresses, vous devez ajouter ce dernier à un groupe de rôles. Pour plus d’informations, consultez la section « Ajouter un rôle à un groupe de rôles » de la rubrique [Gérer des groupes de rôles](manage-role-groups-exchange-2013-help.md).

  - Pour utiliser le paramètre *RecipientFilter* pour créer un filtre personnalisé, vous devez spécifier une chaîne pour le filtre. L'environnement de ligne de commande Exchange Management Shell utilise OPATH pour la syntaxe de filtrage. OPATH est un langage d'interrogation conçu pour rechercher les sources des données objet.

  - Vous ne pouvez pas utiliser le Centre d’administration Exchange (CAE) pour effectuer cette procédure. Vous devez utiliser l'environnement de ligne de commande Exchange Management Shell.

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.


## Utilisez l'environnement de ligne de commande Exchange Management Shell pour créer une liste d'adresses en utilisant des filtres de destinataires

Cet exemple crée une liste d'adresses pour tous les utilisateurs avec des boîtes aux lettres Exchange qui se trouvent à Washington ou dans l'Oregon.

    New-AddressList -Name "Pacific Northwest Mailboxes" -RecipientFilter {((RecipientType -eq 'UserMailbox') -and ((StateOrProvince -eq 'Washington') -or (StateOrProvince -eq 'Oregon')))}

Cet exemple crée une liste d'adresses pour tous les utilisateurs avec des boîtes aux lettres Exchange ayant `AgencyB` comme valeur pour le paramètre *CustomAttribute15*.

    New-AddressList -Name "AgencyB" -RecipientFilter {(RecipientType -eq 'UserMailbox') -and (CustomAttribute15 -like *AgencyB*)}

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, consultez la rubrique [New-AddressList](https://technet.microsoft.com/fr-fr/library/aa996912\(v=exchg.150\)).

