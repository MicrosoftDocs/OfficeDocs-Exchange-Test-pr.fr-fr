---
title: 'Activ. une invite de menu perso. hors des heures d’ouvt: Exchange 2013 Help'
TOCTitle: Activation d’une invite de menu personnalisée en dehors des heures d’ouverture
ms:assetid: 094c50b2-072b-4929-aaf8-f7db5b19e9b6
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb266919(v=EXCHG.150)
ms:contentKeyID: 50555341
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Activation d’une invite de menu personnalisée en dehors des heures d’ouverture

 

_**Sapplique à :** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2013-03-22_

Vous pouvez personnaliser l'invite de menu qui sera utilisée par un standard automatique de messagerie unifiée en dehors des heures d'ouverture. Après avoir créé un standard automatique de messagerie unifiée, une invite du système par défaut (« Bienvenue dans la messagerie unifiée ») est l'invite de menu qu'entendent les appelants une fois que le message d'accueil en dehors des heures d'ouverture est lu. Même si l'invite du système ne doit pas être remplacée ni modifiée, vous pouvez personnaliser les messages d'accueil et les invites de menu qui sont utilisés avec les standards automatiques de messagerie unifiée. Après avoir créé un fichier audio d'invite de menu en dehors des heures d'ouverture personnalisé, vous devez activer les entrées de navigation du menu sur le standard automatique de messagerie unifiée en dehors des heures d'ouverture.

Si vous voulez inclure uniquement le nom de votre organisation ou société dans l'invite du système par défaut, vous pouvez le saisir dans le champ **Nom de l'entreprise** sur le standard automatique de messagerie unifiée. Pour plus d'informations, consultez la rubrique [Entrez un nom d'entreprise](enter-a-business-name-exchange-2013-help.md).

> [!NOTE]
> Vous devez configurer les heures d'ouverture sur le standard automatique. Lorsque vous configurez les heures d'ouverture, les heures de fermeture sont définies automatiquement. Pour plus d'informations, consultez la rubrique <a href="configure-business-hours-exchange-2013-help.md">Configurer les heures d'ouverture</a>.


Pour les autres tâches de gestion relatives aux standards automatiques de messagerie unifiée, consultez la rubrique [Procédures relatives au standard automatique de messagerie unifiée](https://docs.microsoft.com/fr-fr/exchange/voice-mail-unified-messaging/automatically-answer-and-route-calls/um-auto-attendant-procedures).

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : 5 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l'entrée « Standards automatiques de messagerie unifiée » dans la rubrique [Autorisations de messagerie unifiée](unified-messaging-permissions-exchange-2013-help.md).

  - Avant d’exécuter ces procédures, vérifiez qu’un plan de numérotation de messagerie unifiée a été créé. Pour obtenir la procédure détaillée, consultez la rubrique [Créer un plan de numérotation de messagerie unifiée](https://docs.microsoft.com/fr-fr/exchange/voice-mail-unified-messaging/connect-voice-mail-system/create-um-dial-plan).

  - Avant d'exécuter ces procédures, vérifiez qu'un standard automatique de messagerie unifiée a été créé. Pour obtenir la procédure détaillée, consultez la rubrique [Créer un standard automatique de messagerie unifiée](create-a-um-auto-attendant-exchange-2013-help.md).

  - Créez un fichier .wav ou .wma à utiliser pour l'invite de menu.

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..


## Que souhaitez-vous faire ?

## Utiliser le Centre d'administration Exchange (CAE) pour active une invite de menu en dehors des heures d'ouverture personnalisée

1.  Dans le Centre d'administration Exchange, accédez à **Messagerie unifiée** \> **Plans de numérotation de messagerie unifiée**. Dans l'affichage Liste, sélectionnez le plan de numérotation de messagerie unifiée à modifier, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

2.  dans la page **Plan de numérotation de messagerie unifiée**, sous **Standards automatiques de messagerie unifiée**, sélectionnez le standard automatique pour lequel vous souhaitez activer une invite de menu en dehors des heures d'ouverture personnalisée, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

3.  dans la page **Standard automatique de messagerie unifiée**, \> **Navigation de menu**, sous **Navigation de menu en dehors des heures d'ouverture**, cliquez sur **Modifier**, puis sur **Parcourir** pour localiser le fichier d'invite de menu en dehors des heures d'ouverture personnalisé.
    
    > [!NOTE]
    > Le fichier que vous utilisez pour l'invite de menu doit être au format .wav ou .wma.


4.  Après avoir localisé le fichier, cliquez sur **Ouvrir**, puis sur **Enregistrer**.

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour activer une invite de menu en dehors des heures d'ouverture personnalisée

Cet exemple montre comment activer un standard automatique de messagerie unifiée nommé `MyUMAutoAttendant` dont les heures d'ouverture sont configurées pour être de 10h45 à 13h15 le dimanche, de 9h00 à 17h00 le lundi et de 9h00 à 16h30 le samedi, et dont les messages d'accueil associés aux périodes de congés sont configurés pour être « `New Year` » le 1er janvier 2013 et « `Building Closed for Construction` » du 24 au 28 avril 2013.

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -BusinessHoursSchedule 0.10:45-0.13:15,1.09:00-1.17:00,6.09:00-6.16:30 -HolidaySchedule "New Year,newyrgrt.wav,1/2/2013","Building Closed for Construction,construction.wav,4/24/2013,4/28/2013"

Cet exemple montre comment configurer un standard automatique de messagerie unifiée nommé `MyAutoAttendant` et activer des menus de navigation en dehors des heures d'ouverture afin que les appelants qui appuient sur 1 soient transférés vers un autre standard automatique de messagerie unifiée nommé `SalesAutoAttendant`. Quand les appelants appuient sur 2, ils sont transférés vers le numéro de poste 12345 pour `Support`, et quand ils appuient sur 3, ils sont transférés vers un autre standard automatique qui lit un fichier audio.

    Set-UMAutoAttendant -Identity MyAutoAttendant - 
    AfterHoursKeyMappingEnabled $true -
    AfterHoursKeyMapping "1,Sales,,SalesAutoAttendant","2,Support,12345","3,Directions,,,directions.wav"

