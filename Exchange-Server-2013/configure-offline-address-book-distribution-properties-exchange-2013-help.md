---
title: 'Config. les propriétés de distrib. du carnet d’adresses en mode hors connexion | Microsoft Docs'
TOCTitle: Configurer les propriétés de la distribution du carnet d’adresses en mode hors connexion
ms:assetid: 8df985e9-75ba-47ea-9cc3-aa98a5d8acf4
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb123710(v=EXCHG.150)
ms:contentKeyID: 50478659
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.Servers.ClientAccess.OabDistributionGeneralPage
ms.translationtype: HT
---

# Configurer les propriétés de la distribution du carnet d’adresses en mode hors connexion

 

_**Sapplique à :** Exchange Online, Exchange Server 2013_

_**Dernière rubrique modifiée :** 2012-10-14_

Pour chaque point de distribution de carnet d’adresses en mode hors connexion dans Exchange, vous pouvez configurer deux adresses URL : une adresse URL interne accessible uniquement depuis votre réseau d’entreprise interne et une adresse URL externe accessible depuis Internet.

Pour les autres tâches de gestion relatives aux carnets d’adresses en mode hors connexion, voir [Procédures des carnets d’adresses en mode hors connexion](offline-address-book-procedures-exchange-2013-help.md).

## Ce qu’il faut savoir avant de commencer ?

  - Durée d’exécution estimée de chaque procédure : 5 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Carnets d’adresses en mode hors connexion » dans la rubrique [Autorisations pour configurer les adresses de messagerie et les carnets d’adresses](email-address-and-address-book-permissions-exchange-2013-help.md).

  - Vous ne pouvez pas utiliser le Centre d’administration Exchange (CAE) pour effectuer cette procédure. Vous devez utiliser l'environnement de ligne de commande Exchange Management Shell.

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.


## Utiliser le shell pour configurer les propriétés de distribution du carnet d’adresses en mode hors connexion

Cet exemple définit sur six heures l’intervalle entre deux interrogation pour la distribution du carnet d’adresses en mode hors connexion sur le répertoire virtuel OAB du carnet d’adresses en mode hors connexion (site Web par défaut).

    Set-OABVirtualDirectory "OAB (Default Web Site)" -PollInterval 360

Cet exemple définit le point distribution externe sur https://contoso.com/OAB pour le répertoire virtuel par défaut du carnet d’adresses en mode hors connexion (site Web par défaut).

    Set-OABVirtualDirectory "OAB (Default Web Site)" -ExternalUrl https://contoso.com/OAB

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Set-OabVirtualDirectory](https://technet.microsoft.com/fr-fr/library/bb124707\(v=exchg.150\)).

## Pour plus d’informations

[Carnets d’adresses en mode hors connexion](offline-address-books-exchange-2013-help.md)

