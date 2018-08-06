---
title: "Activer/désactiver l’envoi de messages vocaux aux utlsr: Exchange 2013 Help | Microsoft Docs"
TOCTitle: Activation ou désactivation de l'envoi de messages vocaux aux utilisateurs
ms:assetid: faa300d8-2534-40db-8ef9-428be8bb7934
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dd351277(v=EXCHG.150)
ms:contentKeyID: 52057195
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Activation ou désactivation de l'envoi de messages vocaux aux utilisateurs

 

_**Sapplique à :** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2012-12-13_

Vous pouvez permettre aux appelants d’envoyer des messages vocaux aux utilisateurs à partir d’un standard automatique de messagerie unifiée ou les empêcher de le faire. Par défaut, cette option est activée et permet aux appelants d’envoyer des messages vocaux aux utilisateurs d’un plan de numérotation de messagerie unifiée associé au standard automatique de messagerie unifiée. Si vous désactivez cette option, le standard automatique n’invitera pas les appelants à envoyer un message vocal via une invite du système.

Pour les autres tâches de gestion relatives aux standards automatiques de messagerie unifiée, consultez la rubrique [Procédures relatives au standard automatique de messagerie unifiée](um-auto-attendant-procedures-exchange-2013-help.md).

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : Moins d’une minute.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Standards automatiques de messagerie unifiée » dans la rubrique [Autorisations de messagerie unifiée](unified-messaging-permissions-exchange-2013-help.md).

  - Avant d’exécuter ces procédures, vérifiez qu’un plan de numérotation de messagerie unifiée a été créé. Pour obtenir la procédure détaillée, consultez la rubrique [Créer un plan de numérotation de messagerie unifiée](create-a-um-dial-plan-exchange-2013-help.md).

  - Avant d'exécuter ces procédures, vérifiez qu'un standard automatique de messagerie unifiée a été créé. Pour obtenir la procédure détaillée, consultez la rubrique [Créer un standard automatique de messagerie unifiée](create-a-um-auto-attendant-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..


## Que souhaitez-vous faire ?

## Utiliser le CAE pour permettre aux appelants d’envoyer des messages vocaux ou les en empêcher

1.  Dans le CAE, accédez à **Messagerie unifiée** \> **Plans de numérotation de messagerie unifiée**. Dans l'affichage Liste, sélectionnez le plan de numérotation de messagerie unifiée à modifier puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

2.  Dans la page **Plan de numérotation de messagerie unifiée**, sous **Standards automatiques de messagerie unifiée**, sélectionnez le standard à gérer, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

3.  Dans la page **Standard automatique de messagerie unifiée** \> **Accès au carnet d’adresses et à l’opérateur**, sous **Options de contact des utilisateurs**, activez la case à cocher en regard de l’option **Autoriser les appelants à laisser des messages vocaux aux utilisateurs** pour permettre aux appelants de laisser des messages vocaux. Pour empêcher les appelants de laisser des messages vocaux, désactivez la case à cocher.

4.  Cliquez sur **Enregistrer**.

> [!NOTE]
> Si vous désactivez cette option et l’option <strong>Autoriser les appelants à composer les numéros d’utilisateurs</strong>, les <strong>Options de recherche dans le carnet d’adresses</strong> sont également désactivées.


## Utiliser l’environnement de ligne de commande pour permettre aux appelants d’envoyer des messages vocaux ou les en empêcher

Cet exemple montre comment empêcher les appelants qui contactent un standard automatique de messagerie unifiée nommé `MyUMAutoAttendant` d’envoyer des messages vocaux.

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -SendVoiceMsgEnabled $false

Cet exemple montre comment permettre aux appelants qui contactent un standard automatique de messagerie unifiée nommé `MyUMAutoAttendant` d’envoyer des messages vocaux.

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -SendVoiceMsgEnabled $true

