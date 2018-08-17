---
title: 'Configurer la taille du large public pour votre org.: Exchange 2013 Help'
TOCTitle: Configurer la taille du large public pour votre organisation
ms:assetid: 8a37911c-4339-4921-b5d3-0a5a774d4517
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ659068(v=EXCHG.150)
ms:contentKeyID: 50478638
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurer la taille du large public pour votre organisation

 

_**Sapplique à :** Exchange Online, Exchange Server 2013_

_**Dernière rubrique modifiée :** 2015-04-08_

Vous pouvez utiliser l’environnement de ligne de commande Exchange Management Shell pour configurer différents paramètres qui définissent l’utilisation des infos courrier dans votre organisation.

## Ce qu’il faut savoir avant de commencer ?

  - Durée d'exécution estimée : 5 minutes

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Infos-courrier » dans la rubrique [Autorisations de flux de messagerie](mail-flow-permissions-exchange-2013-help.md).

  - Vous pouvez uniquement utiliser l'environnement de ligne de commande Exchange Management Shell pour effectuer cette tâche.

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.


## Utiliser l’environnement Shell pour configurer la taille du large public dans votre organisation

Utilisez la cmdlet **Set-OrganizationConfig** pour configurer la taille du large public dans votre organisation. Lorsque les expéditeurs envoient des messages à un nombre de destinataires supérieur à la taille configurée, l’info-courrier sur le large public s’affiche. La taille du large public est définie sur 25 par défaut. Cet exemple montre comment configurer la taille du large public sur 50 dans votre organisation.

    Set-OrganizationConfig -MailTipsLargeAudienceThreshold 50

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Set-OrganizationConfig](https://technet.microsoft.com/fr-fr/library/aa997443\(v=exchg.150\)).

