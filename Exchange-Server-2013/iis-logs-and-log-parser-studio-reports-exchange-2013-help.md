---
title: 'Journaux IIS et rapports Log Parser Studio: Exchange 2013 Help'
TOCTitle: Journaux IIS et rapports Log Parser Studio
ms:assetid: 01fa67d4-dc02-4c5f-93af-6da7b97d282f
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dn904092(v=EXCHG.150)
ms:contentKeyID: 63910999
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Journaux IIS et rapports Log Parser Studio

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2016-12-09_

## Analyse des rapports Log Parser Studio

Log Parser Studio est un utilitaire qui vous permet de parcourir et de créer des rapports à partir de plusieurs types de fichiers journaux, y compris ceux pour les Services IIS (Internet Information Services). Il se base sur Log Parser 2.2 et est doté d'une interface utilisateur complète pour faciliter la création et la gestion des requêtes SQL associées.

[Téléchargement de Log Parser Studio](https://go.microsoft.com/fwlink/p/?linkid=524244), puis consultez le billet de blog [Prise en main de Log Parser Studio](https://go.microsoft.com/fwlink/p/?linkid=524243).

Notez que dans Exchange 2013, tout le trafic doit passer par IIS. Cela signifie que l'analyse des journaux IIS est la meilleure façon d'obtenir une image complète du nombre de connexions atteignant un serveur, des informations propres au protocole sur les connexions et des utilisateurs qui ont le plus d'impact sur les performances. Plus de 20 nouveaux rapports ont été développés pour Log Parser Studio, à des fins de résolution des problèmes de performances d'Exchange 2013.

## Génération de rapports Log Parser Studio pour des problèmes de performances d'Exchange 2013

Pour une compréhension approfondie de la charge globale dans votre environnement Exchange 2013, utilisez les rapports suivants et comparez les nombres avec chaque serveur.

Un fichier .zip contenant les rapports Log Parser Studio répertoriés ici et des rapports supplémentaires sur la résolution des problèmes peuvent être [téléchargés ici](https://go.microsoft.com/fwlink/p/?linkid=524245).

  - **IIS : Demandes par heure**. Incorpore des flux de journaux IIS à partir du site web par défaut (répertoire W3SVC1) ou du site web principal (répertoire W3SVC2), mais pas des deux en même temps.

  - **ACTIVESYNC\_WP : Clients en pourcentage**. Calcule toutes les demandes ActiveSync, décomposées par agent utilisateur et pourcentage de chaque client pour le nombre total de demandes.

  - **ACTIVESYNC\_WP : Demandes par heure (CSV)**. Répertorie les demandes ActiveSync par heure et envoie les résultats dans un fichier CSV.

  - **ACTIVESYNC\_WP : Demandes par utilisateur (CSV)**. Répertorie les demandes ActiveSync par utilisateur et envoie les résultats dans un fichier CSV.

  - **ACTIVESYNC\_WP : Demandes par utilisateur (premiers 10 Ko)**. Répertorie les demandes ActiveSync par utilisateur pour les 10 000 premiers utilisateurs.

  - **ACTIVESYNC\_WP : Principaux interlocuteurs (CSV)**. Répertorie les principaux clients ActiveSync par ordre décroissant du nombre de demandes et envoie le résultat dans un fichier CSV.

  - **EWS\_WP : Clients en pourcentage**. Calcule toutes les demandes EWS, décomposées par agent utilisateur et pourcentage de chaque client pour le nombre total de demandes.

  - **EWS\_WP : Demandes par heure (CSV)**. Répertorie le nombre total de demandes EWS par heure.

  - **EWS\_WP : Demandes par utilisateur (CSV)**. Répertorie les demandes EWS par utilisateur et envoie les résultats dans un fichier CSV.

  - **EWS\_WP : Demandes par utilisateur (premiers 10 Ko)**. Répertorie les demandes EWS par utilisateur pour les 10 000 premiers utilisateurs.

  - **EWS\_WP : Principaux interlocuteurs (CSV)**. Répertorie les principaux clients EWS par ordre décroissant du nombre de demandes.

  - **OLA\_WP : Erreurs, par utilisateur, par heure, par jour**. Utilisateurs Outlook Anywhere par nombre de demandes.

  - **OLA\_WP : Demandes par heure**. Répertorie les demandes Outlook Anywhere par heure.

  - **OLA\_WP : Demandes par heure, par utilisateur**. Répertorie les demandes Outlook Anywhere par heure, par utilisateur.

  - **OLA\_WP : Demandes par utilisateur (CSV)**. Répertorie les demandes Outlook Anywhere par utilisateur.

  - **OLA\_WP : Demandes par utilisateur (premiers 10 Ko)**. Répertorie les demandes Outlook Anywhere par utilisateur pour les premiers 10 000 utilisateurs.

  - **OLA\_WP : Interlocuteurs principaux**. Répertorie les principaux clients Outlook Anywhere par ordre décroissant du nombre de demandes.

  - **OWA\_WP : Clients en pourcentage**. Calcule toutes les demandes OWA, décomposées par agent utilisateur et pourcentage de chaque client pour le nombre total de demandes.

  - **OWA\_WP : Demandes par heure (CSV)**. Répertorie les demandes OWA par heure et envoie les résultats dans un fichier CSV.

  - **OWA\_WP : Demandes par utilisateur (CSV)**. Répertorie les demandes OWA par utilisateur et envoie les résultats dans un fichier CSV.

  - **OWA\_WP : Demandes par utilisateur (premiers 10 Ko)**. Répertorie les demandes OWA par utilisateur pour les 10 000 premiers utilisateurs.

  - **OWA\_WP : Principaux interlocuteurs (CSV)**. Répertorie les principaux clients OWA par ordre décroissant du nombre de demandes et envoie le résultat dans un fichier CSV.

