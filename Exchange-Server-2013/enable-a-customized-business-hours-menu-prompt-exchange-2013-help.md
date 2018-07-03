---
title: 'Activer une invite de menu personnalisé les heures de bureau: Exchange 2013 Help'
TOCTitle: Activer une invite de menu personnalisé les heures de bureau
ms:assetid: 89053e84-3490-4dc6-ade3-9b6c5dbf4020
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb232116(v=EXCHG.150)
ms:contentKeyID: 50555438
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Activer une invite de menu personnalisé les heures de bureau

 

_**Sapplique à :** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2013-04-19_

Vous pouvez personnaliser l'invite de menu qu'un standard automatique de messagerie unifiée va utiliser pendant les heures d'ouverture. Après avoir créé un standard automatique de messagerie unifiée, une invite du système par défaut (« Bienvenue dans la messagerie unifiée ») est utilisée comme invite du menu principal à l'intention des appelants après le message d'accueil utilisé pendant les heures d'ouverture. Même si l'invite du système ne doit pas être remplacée ni modifiée, vous pouvez personnaliser les messages d'accueil et les invites de menu qui sont utilisés avec les standards automatiques de messagerie unifiée. Après avoir personnalisé un fichier audio d'invite de menu pour les heures d'ouverture, vous devez activer les entrées de navigation par menu sur le standard automatique de messagerie unifiée pour les heures d'ouverture.

Si vous voulez inclure uniquement le nom de votre organisation ou société dans l'invite du système par défaut, vous pouvez le saisir dans le champ **Nom de l'entreprise** sur le standard automatique de messagerie unifiée. Pour plus d'informations, consultez la rubrique [Entrez un nom d'entreprise](enter-a-business-name-exchange-2013-help.md).

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159813.important(EXCHG.150).gif" title="Important" alt="Important" />Important :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Vous devez configurer les heures d'ouverture sur le standard automatique. Pour plus d'informations, consultez la rubrique <a href="configure-business-hours-exchange-2013-help.md">Configurer les heures d'ouverture</a>.</td>
</tr>
</tbody>
</table>


Pour les autres tâches de gestion relatives aux standards automatiques de messagerie unifiée, consultez la rubrique [Procédures relatives au standard automatique de messagerie unifiée](um-auto-attendant-procedures-exchange-2013-help.md).

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : 5 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Standards automatiques de messagerie unifiée » dans la rubrique [Autorisations de messagerie unifiée](unified-messaging-permissions-exchange-2013-help.md).

  - Avant d'exécuter ces procédures, vérifiez qu'un plan de numérotation de messagerie unifiée a été créé. Pour obtenir la procédure détaillée, consultez la rubrique [Créer un plan de numérotation de messagerie unifiée](create-a-um-dial-plan-exchange-2013-help.md).

  - Avant d'exécuter ces procédures, vérifiez qu'un standard automatique de messagerie unifiée a été créé. Pour obtenir la procédure détaillée, consultez la rubrique [Créer un standard automatique de messagerie unifiée](create-a-um-auto-attendant-exchange-2013-help.md).

  - Créez un fichier .wav ou .wma à utiliser pour l'invite de menu.

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..


## Que souhaitez-vous faire ?

## Utiliser le Centre d'administration Exchange (CAE) pour activer une invite du menu personnalisée pendant les heures d'ouverture

1.  Dans le Centre d'administration Exchange, accédez à **Messagerie unifiée** \> **Plans de numérotation de messagerie unifiée**. Dans l'affichage Liste, sélectionnez le plan de numérotation de messagerie unifiée à modifier, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

2.  Dans la page **Plan de numérotation de messagerie unifiée**, sous **Standards automatiques de messagerie unifiée**, sélectionnez le standard automatique de messagerie unifiée pour lequel vous voulez activer une invite du menu personnalisée pour les heures d'ouverture, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

3.  Dans la page **Standard automatique de messagerie unifiée**, \> **Navigation par menu**, sous **Navigation dans le menu des heures d'ouverture**, cliquez sur **Modifier**, puis sur **Parcourir** pour rechercher le fichier des invites du menu personnalisées pour les heures d'ouverture.
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ159813.important(EXCHG.150).gif" title="Important" alt="Important" />Important :</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Le fichier que vous utilisez pour l'invite de menu doit être au format .wav ou .wma.</td>
    </tr>
    </tbody>
    </table>


4.  Après avoir localisé le fichier, cliquez sur **Ouvrir**, puis sur **Enregistrer**.

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour activer une invite du menu personnalisée pendant les heures d'ouverture

Cet exemple active une invite du menu principal des heures d'ouverture et utilise une invite personnalisée intitulée `businesshoursprompts.wav` sur le standard automatique de messagerie unifiée `MyUMAutoAttendant`.

    Command Set-UMAutoAttendant -Identity MyUMAutoAttendant -BusinessHoursMainMenuCustomPromptEnabled $true -BusinessHoursMainMenuCustomPromptFilename BusinessHoursPrompts.wav

Dans cet exemple, nous configurons le standard automatique de messagerie unifiée `MyUMAutoAttendant` dont les heures d'ouverture sont définies comme suit : de 10h45 à 13h15 le dimanche, de 9h à 17h le lundi et de 9h à 16h30 le samedi et les périodes de congés. Par ailleurs, leur message d'accueil associé est configuré pour être « `New Year` » le 2 janvier 2013 et « `Building Closed for Construction` » du 24 au 28 avril 2013.

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -BusinessHoursSchedule 0.10:45-0.13:15,1.09:00-1.17:00,6.09:00-6.16:30 -HolidaySchedule "New Year,newyrgrt.wav,1/2/2013","Building Closed for Construction,construction.wav,4/24/2013,4/28/2013"

Cet exemple permet de configurer le standard automatique de messagerie unifiée `MyAutoAttendant` et d'activer les menus de navigation pour les heures d'ouverture de manière à ce que les appelants soient transférés vers un autre standard automatique de messagerie unifiée intitulé `SalesAutoAttendant` quand ils appuient sur la touche 1. S'ils appuient sur 2, le transfert s'effectue vers le numéro de poste 12345 pour `Support` et s'ils appuient sur la touche 3, ils sont dirigés vers un autre standard automatique qui diffuse un fichier audio.

    Set-UMAutoAttendant -Identity MyAutoAttendant - BusinessHoursKeyMappingEnabled $true -BusinessHoursKeyMapping "1,Sales,,SalesAutoAttendant","2,Support,12345","3,Directions,,,directions.wav"

