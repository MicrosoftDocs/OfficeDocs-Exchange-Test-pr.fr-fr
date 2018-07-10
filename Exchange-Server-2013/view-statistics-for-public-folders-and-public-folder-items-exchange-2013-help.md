---
title: 'Affichage des statistiques des dossiers publics et des éléments des dossiers publics: Exchange 2013 Help'
TOCTitle: Affichage des statistiques des dossiers publics et des éléments des dossiers publics
ms:assetid: 4e412710-9a74-4649-ab01-502e969a7eda
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Aa997949(v=EXCHG.150)
ms:contentKeyID: 50478155
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Affichage des statistiques des dossiers publics et des éléments des dossiers publics

 

_**Sapplique à :** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2013-02-14_

Cette rubrique explique comment obtenir des statistiques sur un dossier public, telles que le nom complet, l'heure de création, l'heure de la dernière modification par l'utilisateur, le dernier accès de l'utilisateur et la taille de l'élément. Vous pouvez utiliser ces informations pour décider de supprimer ou de conserver des dossiers publics.

> [!NOTE]
> Dans le centre d'administration Exchange (CAE), vous pouvez afficher certaines informations de quota et d'utilisation des dossiers publics en accédant à <strong>Dossiers publics</strong> &gt; <strong>Modifier</strong><img src="images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif" title="Icône Modifier" alt="Icône Modifier" /> &gt; <strong>Utilisation de la boîte aux lettres</strong>. Ces informations sont toutefois incomplètes. Nous vous recommandons d'utiliser l'environnement de commande Exchange Power Shell pour voir les statistiques de dossier public.


Pour découvrir d'autres tâches de gestion associées à la gestion des dossiers publics, consultez la rubrique [Procédures relatives aux dossiers publics](public-folder-procedures-exchange-2013-help.md).

Pour découvrir d'autres tâches de gestion associées aux dossiers publics, consultez la rubrique [Procédures de dossiers publics dans Office 365 et Exchange Online](https://technet.microsoft.com/fr-fr/library/jj966272\(v=exchg.150\)).

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : 1 minute.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l'entrée « Dossiers publics » dans la rubrique [Autorisations de partage et de collaboration](sharing-and-collaboration-permissions-exchange-2013-help.md).

  - Vous ne pouvez pas utiliser le CAE pour extraire des statistiques de dossier public.

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.


## Que souhaitez-vous faire ?

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour obtenir les statistiques de dossiers publics

Cet exemple renvoie les statistiques du dossier public Marketing avec une commande redirigée pour formater la liste.

    Get-PublicFolderStatistics -Identity \Marketing | Format-List

> [!NOTE]
> La valeur du paramètre <em>Identity</em> doit inclure le chemin d'accès au dossier public. Par exemple, si le dossier public nommé Marketing existait sous un dossier parent nommé Business, vous devez indiquer la valeur suivante : <code>\Business\Marketing</code>


Pour obtenir des informations détaillées sur la syntaxe et les paramètres, consultez la rubrique [Get-PublicFolderStatistics](https://technet.microsoft.com/fr-fr/library/aa998663\(v=exchg.150\)).

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour afficher des statistiques sur les éléments de dossier public

Vous pouvez afficher les informations suivantes sur les éléments d'un dossier public :

  - Type de l'élément

  - Objet

  - Date de la dernière modification utilisateur

  - Date du dernier accès utilisateur

  - Date de création

  - Pièces jointes

  - Taille des messages

Vous pouvez utiliser ces informations pour prendre des décisions relatives aux actions à mettre en place pour vos dossiers publics, tels que les dossiers publics à supprimer. Par exemple, vous pouvez vouloir supprimer un dossier public s'il n'y a eu aucun accès aux éléments pendant plus de deux ans. Ou bien, vous pouvez vouloir convertir un dossier public utilisé comme référentiel de document vers une autre application d'accès au client.

Cet exemple renvoie des statistiques par défaut sur tous les éléments du dossier public Pamphlets, sous le chemin d'accès \\Marketing\\2013. Les informations par défaut incluent l'identité de l'élément, l'heure de création et l'objet.

    Get-PublicFolderItemStatistics -Identity "\Marketing\2013\Pamphlets"

Cet exemple renvoie des informations supplémentaires sur les éléments du dossier public Pamphlets, telles que l'objet, l'heure de la dernière modification, l'heure de création, les pièces jointes, la taille des messages et le type d'élément. Il inclut également une commande redirigée qui permet de formater la liste.

    Get-PublicFolderItemStatistics -Identity "\Marketing\2010\Pamphlets" | Format-List

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, consultez la rubrique [Get-PublicFolderItemStatistics](https://technet.microsoft.com/fr-fr/library/ee332344\(v=exchg.150\)).

## Utiliser le Shell pour exporter le résultat de la cmdlet Get-PublicFolderItemStatistics vers un fichier .csv

Cet exemple exporte la sortie de la cmdlet vers le fichier PFItemStats.csv contenant les informations suivantes sur tous les éléments figurant dans le dossier public \\Marketing\\Reports :

  - Objet du message (`Subject`)

  - Date et heure de dernière modification de l'élément (`LastModificationTime`)

  - Pièces jointes éventuelles (`HasAttachments`)

  - Type d'élément (`ItemType)`)

  - Taille de l'élément (`MessageSize`)

<!-- end list -->

    Get-PublicFolderItemStatistics -Identity "\Marketing\Reports" | Select Subject,LastModificationTime,HasAttachments,ItemType,MessageSize | Export-CSV C:\PFItemStats.csv

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, consultez la rubrique [Get-PublicFolderItemStatistics](https://technet.microsoft.com/fr-fr/library/ee332344\(v=exchg.150\)).

