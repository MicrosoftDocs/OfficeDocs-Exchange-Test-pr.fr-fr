---
title: 'Tester la connectivité d’Outlook Anywhere: Exchange 2013 Help'
TOCTitle: Tester la connectivité d’Outlook Anywhere
ms:assetid: 0dc5b68f-2316-446a-84c9-5f1c50dc3776
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Ee633453(v=EXCHG.150)
ms:contentKeyID: 50555344
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Tester la connectivité d’Outlook Anywhere

 

_**Sapplique à :**Exchange Server 2013_

_**Dernière rubrique modifiée :**2016-12-09_

Vous pouvez tester la connectivité de bout en bout d’Outlook Anywhere du client à l’aide de l’environnement de ligne de commande Exchange Management Shell ou de l’analyseur de connectivité à distance Exchange (ExRCA). Il inclut des tests de connectivité via le service de découverte automatique, la création d’un profil utilisateur et la connexion à la boîte aux lettres utilisateur. Toutes les valeurs requises sont extraites du service de découverte automatique.

Pour d’autres tâches de gestion relatives à Outlook Anywhere, consultez la rubrique [Outlook Anywhere](outlook-anywhere-exchange-2013-help.md).

## Ce qu’il faut savoir avant de commencer ?

  - Durée d'exécution estimée : 10 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Outlook Anywhere » dans la rubrique [Autorisations des clients et des périphériques mobiles](clients-and-mobile-devices-permissions-exchange-2013-help.md).

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

## Utilisation de l’environnement de ligne de commande Exchange Management Shell pour tester la connectivité d’Outlook Anywhere

Pour utiliser l’environnement de ligne de commande Exchange Management Shell afin de tester la connectivité d’Outlook Anywhere, utilisez la cmdlet **Test-OutlookConnectivity**.

Exécutez la commande suivante.

    Test-OutlookConnectivity -ProbeIdentity 'OutlookMailboxDeepTestProbe' -MailboxId tony@contoso.com -Hostname contoso.com

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>La valeur du paramètre <em>OutlookMailboxDeepTestProbe</em> teste la connectivité à partir du serveur de boîtes aux lettres. Pour tester la connectivité à partir du serveur d’accès au client, utilisez <em>OutlookMailboxCTPProbe</em> pour la valeur du paramètre <em>ProbeIdentity</em>.</td>
</tr>
</tbody>
</table>


## Test de la connectivité d’Outlook Anywhere à l’aide de l’analyseur de connectivité à distance Exchange

L’analyseur de connectivité à distance Exchange (ExRCA) est un outil Web conçu pour tester la connectivité avec de nombreux protocoles Exchange. Vous pouvez accéder à l’ExRCA [ici](https://go.microsoft.com/fwlink/p/?linkid=167905).

1.  Sur le site Web de l’ExRCA, sous **Tests de connectivité de Microsoft Office Outlook**, sélectionnez **Outlook Anywhere**, puis Suivant au bas de la page.

2.  Saisissez les informations requises sur l’écran suivant, notamment l’adresse de messagerie, le domaine et le nom d’utilisateur, ainsi que le mot de passe.

3.  Indiquez si vous souhaitez utiliser le service de découverte automatique pour détecter les paramètres du serveur ou spécifier manuellement les paramètres du serveur.

4.  Acceptez le dédit de responsabilité, saisissez le code de vérification, puis sélectionnez **Vérifier**.

5.  Sélectionnez **Effectuer un test**.

## Comment savoir si cela a fonctionné ?

Une fois les tests ExRCA terminés, la sortie s’affiche sur la page Web. Tous les échecs sont répertoriés.

