---
title: 'Activer un message d’accueil en dehors des heures d’ouverture personnalisé: Exchange 2013 Help'
TOCTitle: Activer un message d’accueil en dehors des heures d’ouverture personnalisé
ms:assetid: d4743805-bab0-4735-a1e0-2cea4e088e8c
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb232183(v=EXCHG.150)
ms:contentKeyID: 50555497
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Activer un message d’accueil en dehors des heures d’ouverture personnalisé

 

_**Sapplique à :** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2012-11-30_

Vous pouvez activer un message d’accueil personnalisé en dehors des heures d’ouverture pour un standard automatique de messagerie unifiée. Le message d’accueil en dehors des heures d’ouverture est la première chose que l’appelant entend lorsqu’un standard automatique de messagerie unifiée répond à son appel en dehors des heures d’ouverture. Vous souhaitez certainement personnaliser le message d’accueil.

La messagerie unifiée inclut un message d'assistance vocal système par défaut à utiliser en dehors des heures d'ouverture. Bien que le message d’assistance vocal système par défaut ne doive être ni remplacé ni modifié, vous souhaitez peut-être offrir un accueil personnalisé. Vous pouvez créer un message d’accueil personnalisé au format de fichier .wav ou .wma à utiliser lorsque des appelants contactent le standard automatique de messagerie unifiée en dehors des heures d’ouverture. Par exemple, « Bienvenue chez Woodgrove Bank, nos bureaux sont actuellement fermés. ».

Pour inclure le nom de votre organisation ou entreprise dans le message d’accueil par défaut, entrez ce nom dans la zone **Nom de l’entreprise** sur le standard automatique de messagerie unifiée. Pour plus d’informations, consultez la rubrique [Entrez un nom d'entreprise](enter-a-business-name-exchange-2013-help.md).

Pour les autres tâches de gestion relatives aux standards automatiques de messagerie unifiée, voir [Procédures relatives au standard automatique de messagerie unifiée](um-auto-attendant-procedures-exchange-2013-help.md).

## Ce qu’il faut savoir avant de commencer ?

  - Durée d'exécution estimée : 5 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Standards automatiques de messagerie unifiée » dans la rubrique [Autorisations de messagerie unifiée](unified-messaging-permissions-exchange-2013-help.md).

  - Avant d’exécuter ces procédures, vérifiez qu’un plan de numérotation de messagerie unifiée a été créé. Pour obtenir la procédure détaillée, consultez la rubrique [Créer un plan de numérotation de messagerie unifiée](create-a-um-dial-plan-exchange-2013-help.md).

  - Avant d’exécuter ces procédures, vérifiez qu’un standard automatique de messagerie unifiée a été créé. Pour obtenir la procédure détaillée, consultez la rubrique [Créer un standard automatique de messagerie unifiée](create-a-um-auto-attendant-exchange-2013-help.md).

  - Créer un fichier .wav ou .wma à utiliser pour le message d’accueil.

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

<table>
<thead>
<tr class="header">
<th><img src="images/Bb125224.tip(EXCHG.150).gif" title="Conseil" alt="Conseil" />Conseil :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..</td>
</tr>
</tbody>
</table>


## Que souhaitez-vous faire ?

## Utiliser le Centre d’administration Exchange (EAC) pour activer un message d’accueil personnalisé en dehors des heures d’ouverture

1.  Dans le Centre d’administration Exchange, accédez à **Messagerie unifiée** \> **Plans de numérotation de messagerie unifiée**. Dans la liste affichée, sélectionnez le plan de numérotation de messagerie unifiée que vous souhaitez modifier puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

2.  Sur la page **Plan de numérotation de messagerie unifiée**, sous **Standards automatiques de messagerie unifiée**, sélectionnez le standard automatique de messagerie unifiée pour lequel vous voulez activer un message d’accueil personnalisé pour la période en dehors des heures d’ouverture, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

3.  Sur la page **Standard automatique de messagerie unifiée**, \> **Message d’accueil**, sous **Message d’accueil en dehors des heures d’ouverture**, cliquez sur **Modifier**, puis cliquez sur **Parcourir** pour rechercher le fichier de message d’accueil personnalisé pour la période en dehors des heures d’ouverture que vous avez créé avant de démarrer cette procédure.
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ159813.important(EXCHG.150).gif" title="Important" alt="Important" />Important :</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Le fichier que vous utilisez pour le message d’accueil doit être un fichier .wav ou .wma.</td>
    </tr>
    </tbody>
    </table>


4.  Après avoir localisé le fichier, cliquez sur **Ouvrir**, puis sur **Enregistrer**.

## Utiliser l’environnement de ligne de commande Exchange Management Shell pour activer un message d’accueil personnalisé en dehors des heures d’ouverture

Dans cet exemple, nous activons le message d’accueil en dehors des heures d’ouverture pour utiliser un message d’accueil personnalisé intitulé `GreetingFile.wav` pour le standard automatique de messagerie unifiée `MyUMAutoAttendant`.

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -AfterHoursWelcomeGreetingEnabled $true -AfterHoursWelcomeGreetingFilename GreetingFile.wav

Dans cet exemple, nous configurons un standard automatique de messagerie unifiée intitulé `MyUMAutoAttendant` dont les heures d’ouverture sont définies comme suit : de 10h45 à 13h15 le dimanche, de 9h à 17h le lundi et de 9h à 16h30 le samedi et les périodes de congés ; en outre, leurs messages d’accueil associés sont configurés pour être « `New Year` » le 2 janvier 2013 et « `Building Closed for Construction` » du 24 au 28 avril 2013.

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -BusinessHoursSchedule 0.10:45-0.13:15,1.09:00-1.17:00,6.09:00-6.16:30 -HolidaySchedule "New Year,newyrgrt.wav,1/2/2013","Building Closed for Construction,construction.wav,4/24/2013,4/28/2013"

Dans cet exemple, nous configurons un standard automatique de messagerie unifiée intitulé `MyAutoAttendant` et activons des mappages de touches pour la période en dehors des heures d’ouverture de manière à ce que les appelants, en appuyant sur la touche 1, soient transférés vers un autre standard automatique de messagerie unifiée nommé `SalesAutoAttendant`. S’ils appuient sur 2, leur transfert s’effectue vers le numéro de poste 12345 pour `Support` et s’ils appuient sur 3, ils sont dirigés vers un autre standard automatique qui diffuse un fichier audio.

    Set-UMAutoAttendant -Identity MyAutoAttendant - BusinessHoursKeyMappingEnabled $true -BusinessHoursKeyMapping "1,Sales,,SalesAutoAttendant","2,Support,12345","3,Directions,,,directions.wav"

