---
title: 'Outlook for iOS and Android: Exchange 2013 Help'
TOCTitle: Outlook for iOS and Android
ms:assetid: 3a66817c-30da-4965-a6db-2955b5365b0f
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Mt465744(v=EXCHG.150)
ms:contentKeyID: 70061277
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Outlook for iOS and Android

 

_**Sapplique à :**Exchange Server 2010, Exchange Server 2013_

_**Dernière rubrique modifiée :**2018-04-02_

**Résumé:** cet article contient une architecture et des informations de sécurité pour les administrateurs sur Outlook pour iOS et Android dans un Exchange 2013 environnement sur site.

L’application Outlook pour iOS et Android est conçue pour rassembler le courrier électronique, calendrier, contacts et autres fichiers, qui permet aux utilisateurs de votre organisation de faire plus à partir de leurs appareils mobiles. Cet article fournit une vue d’ensemble de l’architecture et la conception du stockage de l’application, afin que les administrateurs Exchange puissent déployer et mettre à jour d’Outlook pour iOS et Android dans leur organisation Exchange.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Les utilisateurs peuvent utiliser le <a href="https://support.office.com/fr-fr/article/outlook-for-ios-and-android-help-center-cd84214e-a5ac-4e95-9ea3-e07f78d0cde6">Centre d’aide sur Outlook pour iOS et Android</a>, ainsi que l’aide destinée à l’utilisation de l’application sur certains appareils et les informations relatives à la résolution des problèmes.</td>
</tr>
</tbody>
</table>


## Architecture d’Outlook pour iOS et Android

Outlook pour iOS et Android se compose d’une application frontale installée sur les appareils mobiles et d’un service cloud sécurisé et évolutif sur le serveur principal, appelé *service Outlook*. Le traitement des informations dans le service Outlook active des fonctionnalités avancées qui améliorent l’expérience Outlook, tout en offrant des performances accrues et une meilleure stabilité. Cette architecture s’appuie sur le service Outlook pour réaliser des tâches exigeantes, tout en limitant le nombre de ressources exigées des appareils des utilisateurs.

Voici quelques exemples des fonctionnalités proposées par le service Outlook :

  - Catégorisation pour la Boîte de réception triée.

  - Désabonnement en un clic des listes de diffusion.

  - Vitesse et efficacité accrues des recherches.

  - Transfert et envoi de fichiers volumineux sans téléchargement préalable sur un appareil mobile.

## Mise en cache des données

Pour améliorer les performances, un sous-ensemble de la messagerie, le calendrier et les données de fichier à partir de la boîte aux lettres de chaque utilisateur est mis en cache dans le service d’Outlook. Ce service s’exécute actuellement sur les Microsoft Azure. Nous déplacez le service Outlook vers Office 365 et prévoyez d’avoir ce déplacement terminé plus rapidement.

Les informations contenues dans le service d’Outlook sont actuellement mis en cache aux États-Unis ou en Europe, en fonction de l’adresse IP du client qui se connecte. À mesure que nous le service Outlook dans Office 365, nous s’aligne aux principes du Centre Office 365 confiance grâce à une stratégie de centre de données régionalisé. Dans Office 365 le pays ou la région, administrateur de ses entrées durant l’installation initiale des services, d’un client détermine l’emplacement de stockage principal pour les données de ce client. Pour plus d’informations, consultez [Le centre de confiance Office 365](https://go.microsoft.com/fwlink/p/?linkid=525776).

## FAQ sur la mise en cache des données

Vous trouverez ci-dessous les questions fréquemment posées sur le stockage des données dans Outlook pour iOS et Android.

## Quelle quantité de données de la boîte aux lettres d’un utilisateur est mise en cache dans le service Outlook ?

Environ un mois de données issues de la messagerie électronique, des calendriers et des contacts de l’utilisateur. Le processus de mise en cache est déterminé par un algorithme qui représente, entre autres facteurs, la taille d’une boîte aux lettres, l’importance relative d’un dossier de la boîte aux lettres (par exemple, le dossier Boîte de réception par défaut par rapport à un dossier créé par l’utilisateur) et la fréquence à laquelle un utilisateur accède à un dossier donné.

Le service Outlook stocke les données des pièces jointes comme suit : Lorsqu’un utilisateur demande à ouvrir une pièce jointe dans Outlook, le service récupère la pièce jointe à partir du serveur Exchange et la stocke temporairement. À ce stade, la pièce jointe est remise à l’application sur l’appareil mobile de l’utilisateur. Les données créées il y a plus d’un mois sont régulièrement effacées du service. À ce stade, la pièce jointe sera uniquement disponible sur le serveur Exchange.

## Comment supprimer mes informations du service Outlook ?

Vous disposez de trois options pour supprimer vos informations du service Outlook.

  - Option 1 : lancez une réinitialisation à distance pour chaque utilisateur ayant utilisé l’application Outlook pour iOS et Android afin de se connecter à Office 365 ou Exchange.

  - Option 2 : demandez à tous les utilisateurs de supprimer l’application Outlook. Toutes les données sont supprimées sous 3 à 7 jours environ.

  - Option 3 : demandez à chaque utilisateur de supprimer son compte de l’application Outlook, puis supprimez l’application de leurs appareils mobiles. Pour supprimer un compte, les utilisateurs doivent suivre les étapes suivantes :
    
    1.  Dans l’application Outlook, dans **Paramètres**, appuyez sur **Paramètres de compte**.
    
    2.  Appuyez sur **Sélectionner un compte**, puis, avec le compte sélectionné, appuyez sur **Supprimer le compte**.
    
    3.  Appuyez sur **Appareil et données distantes**.

## Comment sont sécurisées les données de boîte aux lettres temporairement mises en cache lorsqu’elles sont stockées dans le service Outlook ?

Vous pouvez découvrir comment nos données sont protégées dans le [Centre de confiance Azure](https://azure.microsoft.com/support/trust-center/). Comme mentionné précédemment, nous progressions dans Azure et Office 365. La sécurité de ces services est couvert dans [Le centre de confiance Office 365](https://go.microsoft.com/fwlink/p/?linkid=525776).

