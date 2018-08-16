---
title: 'Modif. planif. de génér. du crnt d’adresses hors connexion: Exchange 2013 Help'
TOCTitle: Modifier la planification de génération du carnet d’adresses hors connexion
ms:assetid: d2b4d527-311e-442d-9f1f-54fac8371b80
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb124719(v=EXCHG.150)
ms:contentKeyID: 50479233
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.OrganizationConfiguration.Mailbox.OfflineAddressBookGeneralPage
ms.translationtype: MT
---

# Modifier la planification de génération du carnet d’adresses hors connexion

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2012-12-05_

Un carnet d’adresses en mode hors connexion est une copie de carnet d’adresses qui a été téléchargée de manière qu’un utilisateur Outlook puisse accéder aux informations qu’il contient tout en étant déconnecté du serveur. Vous pouvez configurer le carnet d’adresses en mode hors connexion à l’aide des paramètres *OABGeneratorWorkCycle* et *OABGeneratorWorkCycleCheckpoint* de la cmdlet Set-MailboxServer.

Pour les autres tâches de gestion relatives aux carnets d’adresses en mode hors connexion, voir [Procédures des carnets d’adresses en mode hors connexion](offline-address-book-procedures-exchange-2013-help.md).

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée de chaque procédure : 5 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Carnets d’adresses en mode hors connexion » dans la rubrique [Autorisations pour configurer les adresses de messagerie et les carnets d’adresses](email-address-and-address-book-permissions-exchange-2013-help.md).

  - Vous ne pouvez pas utiliser le Centre d’administration Exchange (CAE) pour effectuer cette procédure. Vous devez utiliser l'environnement de ligne de commande Exchange Management Shell.

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.


## Utiliser l'environnement de ligne de commande Exchange Management Shell pour configurer les propriétés du carnet d'adresses en mode hors connexion

Dans cet exemple, le carnet d’adresses en mode hors connexion est généré toutes les six heures tous les jours sur le serveur de boîtes aux lettres, MBXServer01.

    Set-MailboxServer -Identity MBXServer01 -OABGeneratorWorkCycle 01.00:00:00 -OABGeneratorWorkCycleCheckpoint 06:00:00 

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Set-OfflineAddressBook](https://technet.microsoft.com/fr-fr/library/aa996330\(v=exchg.150\)).

