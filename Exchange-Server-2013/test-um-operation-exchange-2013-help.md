---
title: 'Tester le fonctionnement de la messagerie unifiée: Exchange 2013 Help'
TOCTitle: Tester le fonctionnement de la messagerie unifiée
ms:assetid: 06c9ab4e-8272-47b1-a217-e366f7e9dbaa
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Aa995957(v=EXCHG.150)
ms:contentKeyID: 56269360
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Tester le fonctionnement de la messagerie unifiée

 

_**Sapplique à :** Exchange Server 2010 Service Pack 2 (SP2), Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2013-06-25_

Cette rubrique explique comment utiliser l’environnement Shell pour tester le fonctionnement de votre système de messagerie vocale. Lorsque vous exécutez la procédure suivante, le serveur de boîtes aux lettres exécutant le service de messagerie unifiée de Microsoft Exchange lance un appel SIP (Session Initiation Protocol) de diagnostic, puis retourne une variable d’état d’intégrité des services de messagerie unifiée.

Le test de diagnostic peut être exécuté uniquement sur un serveur de boîtes aux lettres local et vous ne pouvez pas tester le fonctionnement du serveur de boîtes aux lettres à l’aide du CAE.

Pour d’autres tâches de gestion relatives aux serveurs d’accès au client et aux serveurs de boîtes aux lettres, consultez la rubrique [Procédures de services de messagerie unifiée](um-services-procedures-exchange-2013-help.md).

## Ce qu’il faut savoir avant de commencer

  - Durée d’exécution estimée : 3 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrées « Serveur de boîtes aux lettres (service de messagerie unifiée) » et « Serveur d’accès au client (service de routeur d’appel de messagerie unifiée) » dans la rubrique [Autorisations de messagerie unifiée](unified-messaging-permissions-exchange-2013-help.md).

  - Pour exécuter les procédures suivantes, vous devez vous connecter au serveur de boîtes aux lettres à l’aide d’un compte appartenant au groupe Administrateurs local.

  - Vérifiez que le serveur de boîtes aux lettres est installé sur le même ordinateur que le serveur d’accès au client ou sur un ordinateur séparé.

  - Vérifiez que le serveur d’accès au client est installé sur le même ordinateur que le serveur de boîtes aux lettres ou sur un ordinateur séparé.

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..


## Utiliser l’environnement Shell pour tester le fonctionnement des services de messagerie unifiée

Cet exemple exécute des tests de connectivité et de fonctionnement sur le serveur de boîtes aux lettres local, puis affiche les informations de connectivité VoIP (Voice over IP).

    Test-UMConnectivity

Cet exemple indique comment tester la capacité d’un serveur d’accès au client local à écouter les requêtes SIP entrantes non chiffrées sur le port TCP 5060.

    Test-UMConnectivity -ListenPort 5060

Cet exemple indique comment tester la capacité d’un serveur d’accès au client local à écouter les requêtes SIP entrantes chiffrées sur le port TCP 5061.

    Test-UMConnectivity -ListenPort 5061

> [!NOTE]
> Utilisez le mode 1 lorsque le paramètre <code>-UMIPGateway</code> n’est pas spécifié.


> [!NOTE]
> Vous pouvez définir ce paramètre <code>-Timeout</code> avec une valeur inférieure à 5 secondes. Il est toutefois recommandé de toujours configurer ce paramètre avec une valeur minimale de 5 secondes.

