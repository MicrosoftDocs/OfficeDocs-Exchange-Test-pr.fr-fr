---
title: 'Création d’un calendrier de vacances: Exchange 2013 Help'
TOCTitle: Création d’un calendrier de vacances
ms:assetid: 0c5c51e4-5b51-451b-ab93-2cebf644dc96
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb266921(v=EXCHG.150)
ms:contentKeyID: 50477496
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Création d’un calendrier de vacances

 

_**Sapplique à :**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :**2013-04-19_

Vous pouvez définir les date et heure de fermeture de votre organisation pour les vacances et d'autres occasions. Entre les dates de début et les dates de fin spécifiées, les appelants qui accèdent au standard automatique de messagerie unifiée entendent le message d'accueil pendant les congés spécifiés lors de la configuration du calendrier des vacances. Après avoir entendu le message d'accueil pendant les congés que vous avez spécifiés, l'appelant entend le message d'accueil et les invites de menu en dehors des heures d'ouverture.

Vous pouvez également créer un calendrier des vacances dans un calendrier des vacances existant. Lorsque vous créez plusieurs calendriers des vacances, la messagerie unifiée vous permet de faire chevaucher vos temps de congé planifiés. Par exemple, vous pouvez définir un calendrier des vacances du 15 au 31 décembre lorsque votre organisation est fermée pour travaux, et un autre calendrier des vacances du 24 au 26 décembre. Lorsque les appelants contactent le standard automatique entre le 15 et le 23 décembre, ainsi qu'entre le 27 et le 31 décembre, ils entendent le message d'accueil pendant les congés que vous avez spécifié pour ce calendrier. Par exemple, « Nous sommes actuellement fermés pour travaux. » Lorsque les appelants contactent le standard automatique entre le 24 et le 26 décembre, ils entendent un autre message d'accueil pendant les vacances, tel que « Nous sommes actuellement fermés pour que nos employés puissent passer leurs vacances en famille. »

Pour les autres tâches de gestion relatives aux standards automatiques de messagerie unifiée, consultez la rubrique [Procédures relatives au standard automatique de messagerie unifiée](um-auto-attendant-procedures-exchange-2013-help.md).

## Ce qu’il faut savoir avant de commencer ?

  - Durée d'exécution estimée : Moins d’une minute.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Standards automatiques de messagerie unifiée » dans la rubrique [Autorisations de messagerie unifiée](unified-messaging-permissions-exchange-2013-help.md).

  - Avant d’exécuter ces procédures, vérifiez qu’un plan de numérotation de messagerie unifiée a été créé. Pour obtenir la procédure détaillée, consultez la rubrique [Créer un plan de numérotation de messagerie unifiée](create-a-um-dial-plan-exchange-2013-help.md).

  - Avant d'exécuter ces procédures, vérifiez qu'un standard automatique de messagerie unifiée a été créé. Pour obtenir la procédure détaillée, consultez la rubrique [Créer un standard automatique de messagerie unifiée](create-a-um-auto-attendant-exchange-2013-help.md).

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

## Utiliser le Centre d'administration Exchange pour spécifier un calendrier des vacances pour un standard automatique de messagerie unifiée

1.  Dans le Centre d'administration Exchange, accédez à **Messagerie unifiée** \> **Plans de numérotation de messagerie unifiée**. Dans l'affichage Liste, sélectionnez le plan de numérotation de messagerie unifiée à modifier, puis, dans la barre d'outils, cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

2.  dans la page **Plan de numérotation de messagerie unifiée**, sous **Standards automatiques de messagerie unifiée**, sélectionnez le standard automatique de messagerie unifiée pour lequel vous souhaitez définir un calendrier de vacances. Dans la barre d'outils, cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

3.  Dans la page **Standards automatiques de messagerie unifiée**, \> **Heures de bureau**, sous **Calendrier des vacances**, cliquez sur **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter").

4.  Dans la page **Nouvelles vacances**, procédez comme suit :
    
      - **Nom**   Attribuez un nom à votre calendrier des vacances.
    
      - **Message d'accueil pendant les congés**   Sélectionnez le fichier .wav que vous voulez utiliser comme message d'accueil. Ce champ est obligatoire.
    
      - **Date de début**   Cette liste permet de sélectionner la date de votre choix pour le début des vacances. Le calendrier des vacances démarre à minuit, à la date spécifiée dans cette liste.
    
      - **Date de fin**   Cette liste permet de sélectionner la date de votre choix pour la fin des vacances. Le calendrier des vacances prend fin à 23 h 59, à la date spécifiée dans cette liste.

5.  Une fois votre calendrier des vacances configuré, cliquez sur **OK**, puis sur **Enregistrer**.

## Utiliser l'environnement de ligne de commande Exchange Management Shell afin de spécifier un calendrier des vacances pour un standard automatique de messagerie unifiée

Cet exemple montre comment configurer un standard automatique de messagerie unifiée nommé `MyUMAutoAttendant` dont les heures d'ouverture sont configurées pour être de 10h45 à 13h15 le dimanche, de 9h00 à 17h00 le lundi et de 9h00 à 16h30 le samedi, et dont les messages d'accueil associés aux périodes de vacances sont configurés pour être « Nouvelle année » le 2 janvier 2013 et « Bâtiment fermé pour travaux » du 24 au 28 avril 2013.

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -BusinessHoursSchedule 0.10:45-0.13:15,1.09:00-1.17:00,6.09:00-6.16:30 -HolidaySchedule "New Year,newyrgrt.wav,1/2/2013","Building Closed for Construction,construction.wav,4/24/2013,4/28/2013"

