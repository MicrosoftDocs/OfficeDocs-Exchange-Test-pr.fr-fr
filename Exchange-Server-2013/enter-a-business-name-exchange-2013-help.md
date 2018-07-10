---
title: "Entrez un nom d'entreprise: Exchange 2013 Help"
TOCTitle: Entrez un nom d'entreprise
ms:assetid: a0e7cb24-0f55-442d-8ae2-21b177940b78
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Ee423549(v=EXCHG.150)
ms:contentKeyID: 50555459
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Entrez un nom d'entreprise

 

_**Sapplique à :** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2013-04-19_

Vous pouvez entrer le nom de votre entreprise dans la zone **Nom de l'entreprise** d'un standard automatique de messagerie unifiée. Par défaut, aucun nom d'entreprise n'est défini. Si vous entrez le nom d'une entreprise, un message d'accueil par défaut incluant le nom de l'entreprise est lu aux appelants quand ces derniers appellent le standard automatique de messagerie unifiée.

Pour d'autres tâches relatives aux standards automatiques de messagerie unifiée, consultez la rubrique [Procédures relatives au standard automatique de messagerie unifiée](um-auto-attendant-procedures-exchange-2013-help.md).

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : moins d'une minute.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Standards automatiques de messagerie unifiée » dans la rubrique [Autorisations de messagerie unifiée](unified-messaging-permissions-exchange-2013-help.md).

  - Avant d'exécuter ces procédures, vérifiez qu'un plan de numérotation de messagerie unifiée a été créé. Pour obtenir la procédure détaillée, consultez la rubrique [Créer un plan de numérotation de messagerie unifiée](create-a-um-dial-plan-exchange-2013-help.md).

  - Avant d'exécuter ces procédures, vérifiez qu'un standard automatique de messagerie unifiée a été créé. Pour obtenir la procédure détaillée, consultez la rubrique [Créer un standard automatique de messagerie unifiée](create-a-um-auto-attendant-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..


## Que souhaitez-vous faire ?

## Utiliser le Centre d'administration Exchange (CAE) pour configurer un nom d'une entreprise

1.  Dans le Centre d'administration Exchange, accédez à **Messagerie unifiée** \> **Plans de numérotation de messagerie unifiée**. Dans l'affichage Liste, sélectionnez le plan de numérotation de messagerie unifiée à modifier puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

2.  Dans la page **Plan de numérotation de messagerie unifiée**, sous **Standards automatiques de messagerie unifiée**, sélectionnez le standard automatique de messagerie unifiée pour lequel vous souhaitez définir un nom d'entreprise, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier") dans la barre d'outils.

3.  Dans la page **Standard automatique de messagerie unifiée** \> **Général**, sous **Nom de l'entreprise**, entrez le nom de l'entreprise.

4.  Cliquez sur **Enregistrer**.

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour configurer le nom d'une entreprise

Cet exemple définit le nom de l'entreprise sur un standard automatique de messagerie unifiée nommé `MyUMAutoAttendant`.

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -BusinessName "Northwind Traders"

