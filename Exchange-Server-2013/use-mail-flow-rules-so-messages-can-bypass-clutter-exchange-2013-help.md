---
title: 'Utiliser des règles de flux de messagerie afin que les messages puissent contourner le courrier non trié: Exchange 2013 Help'
TOCTitle: Utiliser des règles de flux de messagerie afin que les messages puissent contourner le courrier non trié
ms:assetid: 58e413f0-aa27-4307-bffd-4df03090a15e
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dn896639(v=EXCHG.150)
ms:contentKeyID: 64141267
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Utiliser des règles de flux de messagerie afin que les messages puissent contourner le courrier non trié

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2016-12-09_

Si vous voulez être sûr de recevoir des messages spécifiques, vous pouvez créer une règle de transport Exchange qui garantit que ces messages contournent votre dossier de courrier non trié. Consultez la rubrique [Utiliser l’encombrement pour trier les messages à priorité basse dans Outlook Web App](https://go.microsoft.com/fwlink/p/?linkid=528411) pour plus d’informations sur la fonction Courrier non trié.

Pour les autres tâches de gestion relatives aux règles de transport, consultez [Règles de flux de messagerie (règles de transport) dans Exchange Online](https://technet.microsoft.com/fr-fr/library/jj919238\(v=exchg.150\)) et la rubrique PowerShell [New-TransportRule](https://technet.microsoft.com/fr-fr/library/bb125138\(v=exchg.150\)). Si vous débutez avec PowerShell, consultez les rubriques suivantes pour obtenir de l’aide sur l’utilisation de Powershell :

  - [Connexion à Exchange Online à l'aide de Remote PowerShell](https://technet.microsoft.com/fr-fr/library/jj984289\(v=exchg.150\))

  - [Se connecter à Exchange à l’aide de l’environnement de ligne de commande Exchange Management Shell distant](https://technet.microsoft.com/fr-fr/library/dd335083\(v=exchg.150\))

## Ce qu’il faut savoir avant de commencer

  - Durée d’exécution estimée : 5 minutes

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l’entrée « Règles de transport » dans la rubrique [Stratégie de messagerie et autorisations de conformité](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

## Utiliser l’interface utilisateur pour créer une règle de transport pour contourner le dossier de courrier pêle-mêle

Cet exemple permet à tous les messages dont le titre est « Meeting » de contourner le courrier non trié.

1.  Dans le centre d’administration Exchange, accédez à **flux de messagerie**\>**Règles**. Cliquez sur ![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter"), puis sélectionnez **Créer une règle...**.

2.  Une fois que vous avez créé la règle, cliquez sur **enregistrer** pour démarrer la règle.

![Exemple d’image : Si l’objet contient le mot « meeting », contourner le Courrier pêle-mêle](images/Dn896639.75957aa4-4b2a-4142-92ff-07f8ccc64d82(EXCHG.150).png "Exemple d’image : Si l’objet contient le mot « meeting », contourner le Courrier pêle-mêle")

## Utiliser l’environnement de ligne de commande Exchange Management Shell pour créer une règle de transport pour contourner le dossier de courrier non trié

Cet exemple permet à tous les messages dont le titre est « Meeting » de contourner le courrier non trié.

    New-TransportRule -Name <name_of_the_rule> -SubjectContainsWords "Meeting" -SetHeaderName "X-MS-Exchange-Organization-BypassClutter" -SetHeaderValue "true"

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159813.important(EXCHG.150).gif" title="Important" alt="Important" />Important :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Dans cet exemple, « X-MS-Exchange-Organization-BypassClutter » et « true » respectent tous deux la casse.</td>
</tr>
</tbody>
</table>


Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [New-TransportRule](https://technet.microsoft.com/fr-fr/library/bb125138\(v=exchg.150\)).

## Comment savoir si cela a fonctionné ?

Vous pouvez vérifier les en-têtes des messages électroniques pour voir si les messages arrivent dans la boîte de réception en raison du contournement de la règle de transport de courrier non trié. Sélectionnez un message électronique dans une boîte aux lettres de votre organisation à laquelle la règle de transport de contournement du courrier non trié est appliquée. Examinez les en-têtes marqués sur le message et vous devriez voir l’en-tête **X-MS-Exchange-Organization-BypassClutter: true**. Cela signifie que le contournement fonctionne. Consultez la rubrique [Afficher les informations d’en-tête Internet des messages électroniques](https://go.microsoft.com/fwlink/p/?linkid=822530) pour plus d’informations sur la façon de rechercher les informations d’en-tête.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Les éléments de calendrier, tels que les réunions acceptées, envoyées ou refusées, ne possèdent pas ces en-têtes. Nous nous efforçons d’étendre les fonctionnalités de courrier non trié à ces éléments de calendrier le plus rapidement possible.</td>
</tr>
</tbody>
</table>

