---
title: 'Réduction de la taille d’une boîte aux lettres de découverte dans Exchange: Exchange 2013 Help'
TOCTitle: Réduction de la taille d’une boîte aux lettres de découverte dans Exchange
ms:assetid: fa762d14-f942-4728-8813-887d11441a68
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dn750895(v=EXCHG.150)
ms:contentKeyID: 62371334
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Réduction de la taille d’une boîte aux lettres de découverte dans Exchange

 

_**Sapplique à :** Exchange Online, Exchange Server 2013_

_**Dernière rubrique modifiée :** 2015-04-07_

Vous avez une boîte aux lettres de découverte qui a dépassé la limite de 50 Go ? Vous pouvez résoudre ce problème en créant des boîtes aux lettres de découverte et en copiant les résultats de la recherche de la grande boîte aux lettres de découverte dans les nouvelles.

## Pourquoi effectuer cette opération ?

Dans Exchange Server 2013 et Exchange Online, la taille maximale des boîtes aux lettres de découverte qui sont utilisées pour stocker les résultats de recherche de la découverte électronique sur place est de 50 Go. Avant la limite de taille actuelle, vous pouviez augmenter le quota de stockage à plus de 50 Go, ayant ainsi des boîtes aux lettres de découverte de plus de 50 Go. Il existe trois problèmes liés aux boîtes aux lettres de découverte qui sont supérieures à 50 Go :

  - Elles ne sont pas prises en charge.

  - Elles ne peuvent pas être migrées vers Office 365.

  - Si ce sont des boîtes aux lettres de découverte dans Exchange Server 2010, elles ne peuvent pas être mises à niveau vers Exchange Server 2013.

## Le processus en un clin d’œil

Voici un aperçu rapide de ce que vous devez faire pour réduire la taille d'une boîte aux lettres de découverte qui a dépassé la limite de 50 Go :

1.  Étape 1 : Création de boîtes aux lettres de découverte des boîtes aux lettres de découverte supplémentaires auxquelles distribuer les résultats de recherche.

2.  Étape 2 : Copie des résultats de la recherche dans une boîte aux lettres de découverte les résultats de la recherche de la boîte aux lettres de découverte existante vers une ou plusieurs des nouvelles boîtes aux lettres de découverte.

3.  Étape 3 : Suppression de recherches de découverte électronique des recherches de découverte électronique de la boîte aux lettres de découverte d'origine afin de réduire sa taille.

La stratégie présentée ici regroupe les résultats de la recherche de la boîte aux lettres de découverte d'origine dans des recherches de découverte électronique distinctes basées sur des plages de dates. Il s'agit d'un moyen rapide pour copier de nombreux résultats de recherche vers une nouvelle boîte aux lettres de découverte. Le graphique suivant illustre cette approche.

![Réduction de la taille d’une boîte aux lettres de découverte](images/Dn750895.4400df18-c7ed-4c62-b304-f9060ffbdba5(EXCHG.150).gif "Réduction de la taille d’une boîte aux lettres de découverte")

## Ce qu’il faut savoir avant de commencer

  - Durée d'exécution estimée de cette tâche : La durée variera en fonction de la quantité et de la taille des résultats de recherche qui seront copiés vers différentes boîtes aux lettres de découverte.

  - Exécutez la commande suivante pour déterminer la taille des boîtes aux lettres de découverte dans votre organisation.
    
        Get-Mailbox -RecipientTypeDetails DiscoveryMailbox | Get-MailboxStatistics | FL DisplayName,TotalItemSize

  - Déterminez si vous avez besoin de conserver une partie ou la totalité des résultats de la recherche de la boîte aux lettres de découverte qui a dépassé la limite de 50 Go. Suivez les étapes de cette rubrique pour conserver les résultats de la recherche en les copiant vers une boîte aux lettres de découverte différente. Si vous n'avez pas besoin de conserver les résultats d'une recherche de découverte électronique spécifique, vous pouvez supprimer la recherche, comme expliqué à l'étape 3. La suppression d'une recherche supprimera les résultats de la recherche de la boîte aux lettres de découverte.

  - Si vous n'avez pas besoin des résultats de la recherche d'une boîte aux lettres de découverte qui a dépassé la limite de 50 Go, vous pouvez la supprimer. S'il s'agit de la boîte aux lettres de découverte par défaut qui a été créée lorsque votre organisation Exchange a été mise en service, vous pouvez la recréer. Pour plus d’informations, voir [Suppression et recréation de la boîte aux lettres de découverte par défaut dans Exchange](delete-and-re-create-the-default-discovery-mailbox-in-exchange-exchange-2013-help.md).

  - Pour les conflits juridiques actuels, vous pouvez exporter les résultats de recherche de découverte électronique sélectionnés dans des fichiers .pst. Ainsi, les résultats d'une recherche spécifique sont intacts. En plus des fichiers .pst contenant les résultats de la recherche, un journal des résultats d'une recherche (format de fichier .csv) qui contient une entrée pour chaque message renvoyé dans les résultats de la recherche est également exporté. Chaque entrée du fichier identifie la boîte aux lettres source où se trouve le message. Pour plus d’informations, voir [Exporter les résultats de la recherche électronique vers un fichier PST](export-ediscovery-search-results-to-a-pst-file-exchange-2013-help.md).
    
    Après avoir exporté les résultats de la recherche dans des fichiers .pst, vous devrez utiliser Outlook si vous souhaitez les importer dans une nouvelle boîte aux lettres de découverte.

## Étape 1 : Création de boîtes aux lettres de découverte

La première étape consiste à créer des boîtes aux lettres de découverte supplémentaires pour copier les résultats de la recherche de la boîte aux lettres de découverte qui a dépassé la limite de taille. Sur la base de la limite de taille de 50 Go pour les boîtes aux lettres de découverte, déterminez le nombre de boîtes aux lettres de découverte supplémentaires dont vous aurez besoin et créez-les. Vous devrez ensuite attribuer aux utilisateurs ou aux groupes des autorisations nécessaires pour ouvrir ces nouvelles boîtes aux lettres de découverte.

1.  Exécutez la commande suivante pour créer une boîte aux lettres de découverte.
    
        New-Mailbox -Name <discovery mailbox name> -Discovery

2.  Exécutez la commande suivante pour attribuer des autorisations à un utilisateur ou à un groupe afin qu’ils puissent ouvrir une boîte aux lettres de découverte et visualiser les résultats de la recherche.
    
        Add-MailboxPermission <discovery mailbox name> -User <name of user or group> -AccessRights FullAccess -InheritanceType all

## Étape 2 : Copie des résultats de la recherche dans une boîte aux lettres de découverte

L'étape suivante consiste à utiliser l'applet de commande **New-MailboxSearch** pour copier les résultats de la recherche de la boîte aux lettres de découverte existante dans une nouvelle boîte aux lettres de découverte que vous avez créée à l'étape précédente. Cette procédure utilise les paramètres *StartDate* et *EndDate* pour limiter les résultats de la recherche à des lots dont la taille ne dépasse pas 50 Go. Cela peut nécessiter quelques tests (en estimant les résultats de la recherche) pour dimensionner correctement les résultats de la recherche.

1.  Exécutez la commande suivante pour créer une recherche de découverte électronique.
    
        New-MailboxSearch -Name "Search results from 2010" -SourceMailboxes "Discovery Search Mailbox" -StartDate "01/01/2010" -EndDate "12/31/2010" -TargetMailbox "Discovery Mailbox Backup 01" -EstimateOnly -StatusMailRecipients admin@contoso.com
    
    Cet exemple utilise les paramètres suivants :
    
      - *Name*   Ce paramètre spécifie le nom de la nouvelle recherche de la découverte électronique. Étant donné que la recherche est limitée par des dates d'envoi et de réception, il est utile que le nom de la recherche comprenne la plage de dates.
    
      - *SourceMailboxes*   Ce paramètre spécifie la boîte aux lettres de découverte par défaut. Vous pouvez également spécifier le nom d'une autre boîte aux lettres de découverte qui a dépassé la limite de taille.
    
      - *StartDate* et *EndDate*   Ces paramètres permettent de spécifier la plage de dates des résultats de la recherche dans la boîte aux lettres de découverte par défaut à inclure dans les résultats de la recherche.
        
        > [!NOTE]
        > Pour les dates, utilisez le format de date courte, mm/jj/aaaa, même si les options régionales de l’ordinateur local sont configurées avec un format différent, comme jj/mm/aaaa. Par exemple, utilisez <strong>03/01/2014</strong> pour spécifier le 1er mars 2014.
    
      - *TargetMailbox*   Ce paramètre spécifie que les résultats de la recherche doivent être copiés dans la boîte aux lettres de découverte nommée « Discovery Mailbox Backup 01 ».
    
      - *EstimateOnly*   Ce commutateur précise que seule une estimation du nombre d'éléments à retourner est fournie au démarrage de la recherche. Si vous n'incluez pas ce commutateur, les messages sont copiés dans la boîte aux lettres cible au démarrage de la recherche. Ce commutateur vous permet de régler les plages de dates si nécessaire pour augmenter ou diminuer le nombre de résultats de la recherche.
    
      - *StatusMailRecipients*   Ce paramètre indique que le message d'état doit être envoyé au destinataire spécifié.

2.  Une fois que la recherche a été créée, démarrez-la en utilisant l'environnement de ligne de commande Exchange Management Shell ou le Centre d'administration Exchange (CAE).
    
      - **Utilisation de l'environnement de ligne de commande Exchange Management Shell** : Exécutez la commande suivante pour lancer la recherche créée à l'étape précédente. Étant donné que le commutateur *EstimateOnly* a été inclus lors de la création de la recherche, les résultats de la recherche ne seront pas copiés dans la boîte aux lettres de découverte cible.
        
            Start-MailboxSearch "Search results from 2010"
    
      - **Utilisation du CAE** : Accédez à **Gestion de la conformité** \> **Découverte électronique et blocage sur place**. Sélectionnez la recherche créée à l'étape précédente, cliquez sur **Rechercher**![Icône Recherche](images/Dn750895.773574d0-9b92-4cab-9f6b-81532c7418b9(EXCHG.150).gif "Icône Recherche"), puis cliquez sur **Estimation des résultats de recherche**.

3.  Si nécessaire, réglez la plage de dates pour augmenter ou diminuer le nombre de résultats de recherche qui sont renvoyés. Si vous modifiez la plage de dates, exécutez de nouveau la recherche pour obtenir une nouvelle estimation des résultats. Envisagez de modifier le nom de la recherche afin de refléter la nouvelle plage de dates.

4.  Lorsque vous avez terminé de tester la recherche, utilisez l'environnement de ligne de commande Exchange Management Shell ou le CAE pour copier les résultats de la recherche dans la boîte aux lettres de découverte cible.
    
      - **Utiliser l'environnement de ligne de commande Exchange Management Shell** : Exécutez les commandes suivantes pour copier les résultats de la recherche. Vous devez supprimer le commutateur *EstimateOnly* avant de copier les résultats de la recherche.
        
            Set-MailboxSearch "Search results from 2010" -EstimateOnly $false
        
            Start-MailboxSearch "Search results from 2010"
    
      - **Utilisation du CAE** : Accédez à **Gestion de la conformité** \> **Découverte électronique et blocage sur place**. Sélectionnez la recherche, cliquez sur **Rechercher**![Icône Recherche](images/Dn750895.773574d0-9b92-4cab-9f6b-81532c7418b9(EXCHG.150).gif "Icône Recherche"), puis cliquez sur **Copier les résultats de recherche**.
    
    Pour plus d’informations, voir [Copier les résultats de la recherche de découverte automatique dans une boîte aux lettres de découverte](copy-ediscovery-search-results-to-a-discovery-mailbox-exchange-2013-help.md).

5.  Répétez les étapes 1 à 4 pour créer des recherches de plages de dates supplémentaires. Incluez la plage de dates dans le nom de la nouvelle recherche pour indiquer la plage des résultats. Pour vérifier qu'aucune des boîtes aux lettres de découverte ne dépasse la limite de 50 Go, utilisez des boîtes aux lettres de découverte différentes de la boîte aux lettres cible.

## Étape 3 : Suppression de recherches de découverte électronique

Après avoir copié les résultats de recherche de la boîte aux lettres de découverte d'origine vers une autre boîte aux lettres de découverte, vous pouvez supprimer les recherches de découverte électronique d'origine. La suppression d'une recherche de découverte électronique supprimera les résultats de recherche de la boîte aux lettres de découverte où les résultats de la recherche sont stockés.

Avant de supprimer une recherche, vous pouvez exécuter la commande suivante pour identifier la taille des résultats de recherche qui ont été copiés dans une boîte aux lettres de découverte pour toutes les recherches dans votre organisation.

    Get-MailboxSearch | FL Name,TargetMailbox,ResultSizeCopied

Vous pouvez utiliser l'environnement de ligne de commande Exchange Management Shell ou le CAE pour supprimer une recherche de découverte électronique.

  - **Utiliser l'environnement de ligne de commande Exchange Management Shell** : Exécutez la commande suivante.
    
        Remove-MailboxSearch -Identity <name of search>

  - **Utilisation du CAE** : Accédez à **Gestion de la conformité** \> **Découverte électronique et blocage sur place**. Sélectionnez la recherche à supprimer, puis cliquez sur **Supprimer**![Icône Supprimer](images/Dd979797.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "Icône Supprimer").

## Comment savoir si cela a fonctionné ?

Après avoir supprimé les recherches de découverte électronique pour supprimer les résultats de la boîte aux lettres de découverte où ils étaient stockés, exécutez la commande suivante pour afficher la taille d'une boîte aux lettres de découverte sélectionnée.

    Get-Mailbox <name of discovery mailbox> | Get-MailboxStatistics | FL TotalItemSize

