---
title: 'Désactivation de l’accès au Centre d’administration Exchange: Exchange 2013 Help'
TOCTitle: Désactivation de l’accès au Centre d’administration Exchange
ms:assetid: 49f4fa77-1722-4703-81c9-8724ae0334fb
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ218639(v=EXCHG.150)
ms:contentKeyID: 50478065
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Désactivation de l’accès au Centre d’administration Exchange

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2013-05-20_

Pour des questions de sécurité, certaines organisations peuvent souhaiter restreindre l'accès au centre d'administration Exchange (CAE) pour les utilisateurs provenant d'Internet. Cette procédure vous indique comment désactiver l'accès au CAE. Cette procédure n'empêche pas l'accès des utilisateurs aux options dans Outlook Web App.

> [!NOTE]
> Cette procédure désactive totalement l'accès administrateur au CAE sur le serveur d'accès au client où les étapes sont appliquées. Si vous voulez activez l'administrateur CAE pour les utilisateurs internes, nous vous conseillons d'installer un serveur d'accès au client distinct et de le configurer uniquement pour la gestion des requêtes internes à l'aide de la commande suivante :
> <code>Set-ECPVirtualDirectory -Identity &quot;InternalCAS\ecp (default web site)&quot; -AdminEnabled $True</code>


> [!CAUTION]
> La procédure s'applique uniquement aux déploiements locaux d'Exchange Server 2013.


## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : 5 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l'entrée « Connectivité du centre d'administration Exchange » dans la rubrique [Autorisations d’infrastructure Exchange et Shell](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md).

  - Vous ne pouvez pas utiliser le Centre d’administration Exchange pour effectuer cette procédure. Vous devez utiliser l'environnement de ligne de commande Exchange Management Shell.

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.


## Utilisation du Shell pour désactiver un accès Internet à l'EAC

Cet exemple désactive l'accès au CAE sur le serveur CAS01.

    Set-ECPVirtualDirectory -Identity "CAS01\ecp (default web site)" -AdminEnabled $false

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, consultez la rubrique [Set-EcpVirtualDirectory](https://technet.microsoft.com/fr-fr/library/dd297991\(v=exchg.150\)).

## Comment savoir si cela a fonctionné ?

Pour vérifier que l'accès au CAE a bien été désactivé, procédez comme suit :

1.  Dans votre navigateur Internet, tapez l'URL externe ou interne de votre organisation pour accéder à Outlook Web App, mais remplacez l'identificateur **/owa** par **/ecp**. Par exemple, si l'URL externe pour accéder à Outlook Web App est https://primary.tailspintoys.com/owa, utilisez https://primary.tailspintoys.com/ecp.

2.  Si l’accès est désactivé, un message d’erreur **404 – Site web introuvable** s’affiche.

