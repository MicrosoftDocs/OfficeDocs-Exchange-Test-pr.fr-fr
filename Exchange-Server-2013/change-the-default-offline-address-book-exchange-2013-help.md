---
title: "Modifiication du carnet d'adresses en mode hors connexion par défaut: Exchange 2013 Help"
TOCTitle: Modifiication du carnet d'adresses en mode hors connexion par défaut
ms:assetid: 61abf78e-2543-4431-acc8-839e3c7a4548
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Aa998569(v=EXCHG.150)
ms:contentKeyID: 50478311
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Modifiication du carnet d'adresses en mode hors connexion par défaut

 

_**Sapplique à :** Exchange Online, Exchange Server 2013_

_**Dernière rubrique modifiée :** 2014-12-16_

Par défaut, lorsque vous installez le rôle serveur de boîtes aux lettres, un carnet d'adresses en mode hors connexion par défaut basé sur le Web, nommé Carnet d'adresses en mode hors connexion par défaut, est créé. Vous pouvez définir n'importe quel carnet d'adresses en mode hors connexion dans votre organisation Exchange comme carnet d'adresses en mode hors connexion par défaut. Ce nouveau carnet d'adresses en mode hors connexion par défaut est associé à toutes les nouvelles bases de données de boîtes aux lettres. Vous ne pouvez avoir qu'un seul carnet d'adresses en mode hors connexion par défaut dans votre organisation. Si vous supprimez le carnet d'adresses en mode hors connexion par défaut, MicrosoftExchange n'affecte pas automatiquement un autre carnet d'adresses en mode hors connexion par défaut. Vous devez désigner manuellement un autre carnet d'adresses en mode hors connexion par défaut.

Pour les autres tâches de gestion relatives aux carnets d'adresses en mode hors connexion, consultez la rubrique [Procédures des carnets d’adresses en mode hors connexion](offline-address-book-procedures-exchange-2013-help.md).

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée de chaque procédure : 5 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Carnets d'adresses en mode hors connexion » dans la rubrique [Autorisations des destinataires](recipients-permissions-exchange-2013-help.md).

  - Par défaut dans Exchange Online, le rôle de liste d’adresses n’est affecté à aucun groupe de rôles. Pour utiliser les cmdlets nécessitant le rôle Liste d’adresses, vous devez ajouter ce dernier à un groupe de rôles. Pour plus d’informations, consultez la section « Ajouter un rôle à un groupe de rôles » de la rubrique [Gérer des groupes de rôles](manage-role-groups-exchange-2013-help.md).

  - Vous ne pouvez pas utiliser le Centre d’administration Exchange (CAE) pour effectuer cette procédure. Vous devez utiliser l'environnement de ligne de commande Exchange Management Shell.

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.


## Utiliser l'environnement de ligne de commande Exchange Management Shell pour modifier le carnet d'adresses en mode hors connexion par défaut

Cet exemple montre comment définir le carnet d'adresses en mode hors connexion nommé Mon carnet d'adresses en mode hors connexion comme carnet d'adresses en mode hors connexion par défaut.

    Set-OfflineAddressBook -Identity "My OAB" -IsDefault $true

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, consultez la rubrique [Set-OfflineAddressBook](https://technet.microsoft.com/fr-fr/library/aa996330\(v=exchg.150\)).

