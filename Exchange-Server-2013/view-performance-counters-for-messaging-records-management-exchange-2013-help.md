---
title: 'Afficher les compteurs de performances pour la gestion des enregistrements de messagerie: Exchange 2013 Help'
TOCTitle: Afficher les compteurs de performances pour la gestion des enregistrements de messagerie
ms:assetid: ec374d31-2797-4f8b-8c96-3839d01a662c
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb397227(v=EXCHG.150)
ms:contentKeyID: 51407249
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Afficher les compteurs de performances pour la gestion des enregistrements de messagerie

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2009-12-09_

Vous pouvez utiliser Windows la fiabilité et l'Analyseur de performances (Perfmon.exe) pour sélectionner et visualiser les compteurs de performances pour la messagerie (MRM) la gestion des enregistrements. À l'aide de compteurs de performances, vous pouvez surveiller l'Assistant dossier géré pendant son exécution des processus MRM beaucoup de ressources.

Pour obtenir une liste des compteurs de performances pour la gestion des enregistrements de messagerie, consultez la rubrique [Compteurs de performance pour la gestion des enregistrements de messagerie](performance-counters-for-messaging-records-management-exchange-2013-help.md).

Recherchez les autres tâches liées à la surveillance MRM ? Consultez la rubrique [Gestion des enregistrements de messagerie de la surveillance](monitoring-messaging-records-management-exchange-2013-help.md).

## Utilisation de l'Analyseur de fiabilité et de performances pour afficher les compteurs de performances pour la gestion des enregistrements de messagerie (MRM)

Pour réaliser cette procédure, vous devez utiliser un compte auquel l'appartenance au groupe Administrateurs local a été déléguée.

1.  Pour démarrer l'Analyseur de fiabilité et de performances de Windows, cliquez sur **Démarrer**, sur **Exécuter**, puis entrez **perfmon**.

2.  Dans l'arborescence de la console, accédez à **Outils d'analyse** \> **Analyseur de performances**.

3.  Cliquez sur le bouton signe plus (+) dans la barre d'outils. La boîte de dialogue **Ajouter des compteurs** s'affiche.

4.  Dans la liste **Choisir les compteurs sur**, activez l'une des options suivantes :
    
      - Si vous effectuez cette procédure sur un ordinateur local, sélectionnez **\< ordinateur Local \>**. Il s'agit de la sélection par défaut.
    
      - Si vous effectuez cette procédure à distance, sélectionnez le serveur à surveiller.

5.  Dans la liste des compteurs de performances, développez **Assistants MSExchange - Par base de données** ou l'**Assistant Dossier géré MSExchange**.

6.  Sélectionnez les compteurs de performances à surveiller.

7.  Compteurs de performance sous **Assistants MSExchange - par base de données**, pour afficher les compteurs de toutes les bases de données de boîtes aux lettres, dans **les Instances de l'objet sélectionné**, cliquez sur **toutes les instances**. Ou, pour spécifier une ou plusieurs bases de données de boîtes aux lettres, sélectionnez les instances de la liste.

8.  Pour ajouter les compteurs sélectionnés de sorte qu'ils figurent dans l'Analyseur de fiabilité et de performances de Windows et pour commencer à recueillir des données sur les performances, cliquez sur **Ajouter**.

