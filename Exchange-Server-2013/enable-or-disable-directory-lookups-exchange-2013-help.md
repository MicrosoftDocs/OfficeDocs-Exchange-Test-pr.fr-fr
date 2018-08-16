---
title: "Activer ou désactiver les recherches dans l'annuaire: Exchange 2013 Help"
TOCTitle: Activer ou désactiver les recherches dans l'annuaire
ms:assetid: c0768815-8578-4385-8d4c-7d1e40304cec
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Ee423557(v=EXCHG.150)
ms:contentKeyID: 52057145
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Activer ou désactiver les recherches dans l'annuaire

 

_**Sapplique à :** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2016-05-10_

Vous pouvez activer les recherches dans l'annuaire afin que les personnes qui appellent un standard automatique de messagerie unifiée puissent rechercher des noms dans l'annuaire uniquement l'aide du clavier de leur téléphone (les entrées vocales ne sont pas prises en charge). Ce paramètre est activé par défaut. Si ce paramètre est désactivé, les appelants ne pourront pas rechercher une personne spécifique dans l'annuaire à l'aide du système de numérotation multifréquence ou de commandes vocales.

Pour les autres tâches de gestion relatives aux standards automatiques de messagerie unifiée, consultez la rubrique [Procédures relatives au standard automatique de messagerie unifiée](um-auto-attendant-procedures-exchange-2013-help.md).

> [!NOTE]
> Outlook les utilisateurs Voice Access ne peut pas utiliser la saisie vocale ou reconnaissance vocale automatique (ASR) pour localiser des utilisateurs dans le répertoire, ils peuvent uniquement utiliser DTMF ou des entrées à tonalité.


## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : moins d'une minute.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l'entrée « Standards automatiques de messagerie unifiée » dans la rubrique [Autorisations de messagerie unifiée](unified-messaging-permissions-exchange-2013-help.md).

  - Avant d'exécuter ces procédures, vérifiez qu'un plan de numérotation de messagerie unifiée a été créé. Pour obtenir la procédure détaillée, consultez la rubrique [Créer un plan de numérotation de messagerie unifiée](create-a-um-dial-plan-exchange-2013-help.md).

  - Avant d'exécuter ces procédures, vérifiez qu'un standard automatique de messagerie unifiée a été créé. Pour obtenir la procédure détaillée, consultez la rubrique [Créer un standard automatique de messagerie unifiée](create-a-um-auto-attendant-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..


## Que souhaitez-vous faire ?

## Utiliser le Centre d'administration Exchange (CAE) pour activer ou désactiver les recherches dans l'annuaire

1.  Dans le CAE, accédez à **Messagerie unifiée** \> **Plans de numérotation de messagerie unifiée**. Dans l'affichage Liste, sélectionnez le plan de numérotation de messagerie unifiée à modifier puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

2.  Dans la page **Plan de numérotation de messagerie unifiée**, sous **Standards automatiques de messagerie unifiée**, sélectionnez le standard automatique de messagerie unifiée pour lequel vous souhaitez activer ou désactiver les recherches dans l'annuaire, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

3.  Dans la page **Standard automatique de messagerie unifiée** \> **Accès au carnet d'adresses et à l'opérateur**, sous **Options de recherche dans le carnet d'adresses**, cochez la case en regard de **Autoriser les appelants à rechercher des utilisateurs par nom ou alias** pour permettre aux utilisateurs de rechercher des utilisateurs. Décochez la case pour empêcher la recherche d'appelants par des utilisateurs.

4.  Cliquez sur **Enregistrer**.

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour activer ou désactiver les recherches dans l'annuaire

Cet exemple désactive les recherches dans l'annuaire pour le standard automatique de messagerie unifiée `MyUMAutoAttendant`.

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -NameLookupEnabled $false

