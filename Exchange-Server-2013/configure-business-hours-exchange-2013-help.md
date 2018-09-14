---
title: "Configurer les heures d'ouverture: Exchange 2013 Help"
TOCTitle: Configurer les heures d'ouverture
ms:assetid: 96b4be99-af94-4fa4-959a-48413387a044
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb232133(v=EXCHG.150)
ms:contentKeyID: 50478746
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurer les heures d'ouverture

 

_**Sapplique à :** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2013-04-19_

Lors de la configuration des heures d'ouverture pour un standard automatique de messagerie unifiée, vous devez définir les heures d'ouverture de votre organisation ainsi que les messages d'accueil et les messages d'assistance vocaux pendant les heures d'ouverture que les appelants entent quand ils appellent un numéro de poste configuré sur le standard automatique. Si l'appelant contacte le standard automatique en dehors des heures d'ouverture que vous définissez, il entend les messages d'accueil et les messages d'assistance vocaux en dehors des heures d'ouverture.

Plusieurs options de planification par défaut sont disponibles dans le Centre d'administration Exchange (CAE). Par exemple, la plupart des sociétés sont ouvertes de 8h00 à 17h00 du lundi au vendredi. Parfois, les options par défaut ne correspondent pas à vos besoins et vous souhaiterez peut-être personnaliser le planning. Si vos heures d'ouverture ne coïncident pas avec les horaires de planning définis par le système, vous pouvez définir un planning personnalisé pour le standard automatique.

Par défaut, le standard automatique de la messagerie unifiée lit les invites et les messages d'accueil des heures d'ouverture, quelle que soit l'heure à laquelle les appelants joignent le standard automatique.

> [!NOTE]
> Lors de la configuration du planning des heures d'ouverture et de fermeture sur un standard automatique de messagerie unifiée, assurez-vous que le fuseau horaire est correctement défini.


Pour les autres tâches de gestion relatives aux standards automatiques de messagerie unifiée, consultez la rubrique [Procédures relatives au standard automatique de messagerie unifiée](https://docs.microsoft.com/fr-fr/exchange/voice-mail-unified-messaging/automatically-answer-and-route-calls/um-auto-attendant-procedures).

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : 3 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l'entrée « Standards automatiques de messagerie unifiée » dans la rubrique [Autorisations de messagerie unifiée](unified-messaging-permissions-exchange-2013-help.md).

  - Avant d'exécuter ces procédures, vérifiez qu'un plan de numérotation de messagerie unifiée a été créé. Pour obtenir la procédure détaillée, consultez la rubrique [Créer un plan de numérotation de messagerie unifiée](https://docs.microsoft.com/fr-fr/exchange/voice-mail-unified-messaging/connect-voice-mail-system/create-um-dial-plan).

  - Avant d'exécuter ces procédures, vérifiez qu'un standard automatique de messagerie unifiée a été créé. Pour obtenir la procédure détaillée, consultez la rubrique [Créer un standard automatique de messagerie unifiée](create-a-um-auto-attendant-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..


## Que souhaitez-vous faire ?

## Utiliser le Centre d'administration Exchange (CAE) pour spécifier les heures d'ouverture pour un standard automatique de messagerie unifiée

1.  Dans le Centre d'administration Exchange, accédez à **Messagerie unifiée** \> **Plans de numérotation de messagerie unifiée**. Dans l'affichage Liste, sélectionnez le plan de numérotation de messagerie unifiée à modifier puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

2.  Dans la page **Plan de numérotation de messagerie unifiée**, sous **Standards automatiques de messagerie unifiée**, sélectionnez le standard automatique pour lequel vous souhaitez définir les heures d'ouverture, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

3.  Dans la page **Standard automatique de messagerie unifiée**, \> **Heures d'ouverture**, sous **Heures d'ouverture**, cliquez sur **Configurer les heures d'ouverture**.

4.  Dans la page **Configurer les heures d'ouverture**, sélectionnez les heures que vous voulez utiliser comme heures d'ouverture pour chaque jour de la semaine.

5.  Cliquez sur **OK**, puis sur **Enregistrer**.

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour spécifier les heures d'ouverture pour un standard automatique de messagerie unifiée

Cet exemple montre comment définir les heures d'ouverture pour un standard automatique de messagerie unifiée nommé `MyUMAutoAttendant`.

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -BusinessHoursSchedule 0.10:45-0.13:15,1.09:00-1.17:00,6.09:00-6.16:30

