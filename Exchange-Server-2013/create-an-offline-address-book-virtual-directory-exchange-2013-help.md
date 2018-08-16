---
title: 'Répertoire virtuel du carnet d’adresses hors connexion: Exchange 2013 Help'
TOCTitle: Créer un répertoire virtuel du carnet d’adresses en mode hors connexion
ms:assetid: 2c70e21f-2b12-414a-9e8c-65634a767c72
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Aa996917(v=EXCHG.150)
ms:contentKeyID: 50477808
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Créer un répertoire virtuel du carnet d’adresses en mode hors connexion

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2012-10-16_

Le répertoire virtuel OAB est la distribution de l’OAB. Par défaut, lors de l’installation de Microsoft Exchange Server 2013, un répertoire virtuel nommé carnet d’adresses en mode hors connexion est créé sur le site Web interne par défaut des services Internet (IIS). Si vous avez des utilisateurs côté client qui se connectent à Microsoft Outlook en dehors du pare-feu de votre organisation, vous pouvez ajouter un site Web externe. De la même façon, lorsque vous exécutez la cmdlet **New-OABVirtualDirectory** dans l’environnement de ligne de commande Exchange Management Shell, un répertoire virtuel nommé OAB est créé sur le site Web par défaut des services Internet (IIS) sur le serveur Exchange local.

La création d’un répertoire virtuel de carnet d’adresses en mode hors connexion n’est pas une tâche habituelle. Exchange autorise un seul répertoire virtuel de carnet d’adresses en mode hors connexion nommé OAB. Vous devez créer un répertoire virtuel de carnet d’adresses en mode hors connexion seulement s’il y a un problème avec le répertoire virtuel existant et si le répertoire précédent a été supprimé.

Pour les autres tâches de gestion relatives aux carnets d’adresses en mode hors connexion, voir [Procédures des carnets d’adresses en mode hors connexion](offline-address-book-procedures-exchange-2013-help.md).

> [!NOTE]
> Avant de créer un répertoire virtuel de carnet d’adresses en mode hors connexion, assurez-vous que les utilisateurs sont conscients des modifications que vous apportez. Cette procédure peut interrompre le processus de téléchargement du carnet d’adresses en mode hors connexion pour vos utilisateurs.


## Ce qu’il faut savoir avant de commencer ?

  - Durée d’exécution estimée de chaque procédure : 5 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Carnets d’adresses en mode hors connexion » dans la rubrique [Autorisations pour configurer les adresses de messagerie et les carnets d’adresses](email-address-and-address-book-permissions-exchange-2013-help.md).

  - Le rôle serveur d’accès au client doit être installé sur le serveur Exchange local.

  - Un site Web IIS par défaut doit exister (par exemple, /w3svc/1/root).

  - Un répertoire virtuel nommé OAB n’existe pas déjà.

  - Bien que la distribution Web soit activée par défaut et ne requiert pas de configuration supplémentaire, il est recommandé d’activer le protocole SSL (Secure Sockets Layer) pour le point de distribution de carnet d’adresses en mode hors connexion.

  - Vous ne pouvez pas utiliser le Centre d’administration Exchange (CAE) pour effectuer cette procédure. Vous devez utiliser l'environnement de ligne de commande Exchange Management Shell.

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.


## Utiliser l’environnement de ligne de commande Exchange Management Shell pour créer un répertoire virtuel de carnet d’adresses en mode hors connexion

Pour créer un répertoire virtuel de carnet d’adresses en mode hors connexion avec tous les paramètres par défaut, vous pouvez exécuter la cmdlet **New-OABVirtualDirectory** sans aucun paramètre. La procédure suivante permet de créer un répertoire virtuel de carnet d’adresses en mode hors connexion avec des paramètres personnalisés.

> [!NOTE]
> Lors de la création d’un répertoire virtuel de carnet d’adresses en mode hors connexion, il est recommandé d’activer le protocole SSL.


Cet exemple montre comment créer un répertoire virtuel de carnet d’adresses en mode hors connexion sur le serveur d’accès au client nommé CASServer01 sur lequel le protocole SSL est activé et qui dispose d’une URL externe.

    New-OABVirtualDirectory -Server CASServer01 -RequireSSL $true -ExternalURL "https://www.contoso.com/OAB"

Après avoir créé un répertoire virtuel de carnet d’adresses en mode hors connexion, vous devez modifier les paramètres sur chaque carnet d’adresses en mode hors connexion qui utilise la distribution Web pour les reconnecter au répertoire virtuel de carnet d’adresses en mode hors connexion. Pour plus d’informations, voir [Modifier la planification de génération du carnet d’adresses hors connexion](change-the-offline-address-book-generation-schedule-exchange-2013-help.md).

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [New-OabVirtualDirectory](https://technet.microsoft.com/fr-fr/library/bb123735\(v=exchg.150\)).

