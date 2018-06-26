---
title: 'Activation d’un message d’information automatique: Exchange 2013 Help'
TOCTitle: Activation d’un message d’information automatique
ms:assetid: 07f6c13e-3781-4127-9321-f0f85f054259
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb266918(v=EXCHG.150)
ms:contentKeyID: 50555340
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Activation d’un message d’information automatique

 

_**Sapplique à :**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :**2013-04-19_

Vous pouvez activer un message d'information automatique pour un standard automatique de messagerie unifiée. Lorsqu'il est activé, le message d'information automatique est lu immédiatement après le message d'accueil pendant les heures d'ouverture ou en dehors des heures d'ouverture. Par défaut, aucun message d'information automatique n'est configuré. Pour activer un message d'information automatique, créez un fichier .wav ou .wma à utiliser comme message, puis configurez le standard automatique pour utiliser ce fichier audio.

Pour les autres tâches de gestion relatives aux standards automatiques de messagerie unifiée, consultez la rubrique [Procédures relatives au standard automatique de messagerie unifiée](um-auto-attendant-procedures-exchange-2013-help.md).

## Ce qu’il faut savoir avant de commencer ?

  - Durée d'exécution estimée : Moins d’une minute.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Standards automatiques de messagerie unifiée » dans la rubrique [Autorisations de messagerie unifiée](unified-messaging-permissions-exchange-2013-help.md).

  - Avant d’exécuter ces procédures, vérifiez qu’un plan de numérotation de messagerie unifiée a été créé. Pour obtenir la procédure détaillée, consultez la rubrique [Créer un plan de numérotation de messagerie unifiée](create-a-um-dial-plan-exchange-2013-help.md).

  - Avant d'exécuter ces procédures, vérifiez qu'un standard automatique de messagerie unifiée a été créé. Pour obtenir la procédure détaillée, consultez la rubrique [Créer un standard automatique de messagerie unifiée](create-a-um-auto-attendant-exchange-2013-help.md).

  - Créez un fichier .wav ou .wma à utiliser pour le message d'information automatique.

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

## Utiliser le Centre d'administration Exchange (CAE) pour activer un message d'information automatique

1.  Dans le Centre d'administration Exchange, accédez à **Messagerie unifiée** \> **Plans de numérotation de messagerie unifiée**. Dans l'affichage Liste, sélectionnez le plan de numérotation de messagerie unifiée à modifier, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

2.  Dans la page **Plan de numérotation de messagerie unifiée**, sous **Standards automatiques de messagerie unifiée**, sélectionnez le standard automatique de messagerie unifiée pour lequel vous souhaitez activer un message d'information automatique, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

3.  Dans la page **Standard automatique de messagerie unifiée**, \> **Messages d'accueil**, sous **Message d'information automatique**, cliquez sur **Modifier**, puis sur **Parcourir** pour rechercher le fichier de message d'information automatique que vous avez créé avant d'initier cette procédure.
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ159813.important(EXCHG.150).gif" title="Important" alt="Important" />Important :</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Le fichier utilisé pour le message d'accueil doit être au format .wav ou .wma.</td>
    </tr>
    </tbody>
    </table>


4.  Après avoir localisé le fichier, cliquez sur **Ouvrir**, puis sur **Enregistrer**.

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour activer un message d'information automatique

Cet exemple montre comment activer un message d'information automatique utilisant le fichier `MyInfoAnnouncement.wav` sur un standard automatique de messagerie unifiée nommé `MyUMAutoAttendant`.

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -InfoAnnouncementEnabled $true -InfoAnnouncementFilename MyInfoAnnouncement.wav

