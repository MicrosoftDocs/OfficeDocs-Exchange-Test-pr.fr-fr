---
title: 'Direct Push ;: Exchange 2013 Help'
TOCTitle: Direct Push ;
ms:assetid: 373c1629-3d4b-4828-b014-9e103de4ef25
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Aa997252(v=EXCHG.150)
ms:contentKeyID: 50477902
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Direct Push ;

 

_**Sapplique à :**Exchange Online, Exchange Server 2013_

_**Dernière rubrique modifiée :**2012-07-11_

Direct Push est une fonction intégrée à Microsoft Exchange Server 2013. Direct push conserve la fonction de périphérique mobile en cours via une connexion réseau cellulaire ou sans fil. Il informe le périphérique mobile lorsque de nouvelles informations sont prêtes à être synchronisées.

**Contenu de cette rubrique**

Vue d’ensemble

Topologie Direct Push

Configuration de la fonction Direct Push pour opérer à travers un pare-feu

## Vue d’ensemble

Pour que la fonction Direct Push fonctionne, le périphérique mobile doit être compatible Direct Push. Ces périphériques sont les suivants :

  - Toutes les versions de Windows Phone

  - Les téléphones mobiles qui sont produits par les détenteurs de licence Microsoft Exchange ActiveSync et qui sont spécialement conçus pour être compatibles avec la fonction Direct Push

Par défaut, la fonction Direct Push est activée dans Exchange 2013. Les périphériques mobiles qui prennent en charge la fonction Direct Push envoient une requête HTTPS à long terme au serveur Microsoft Exchange. Le serveur Exchange analyse l’activité de la boîte aux lettres de l’utilisateur et envoie une réponse à son périphérique mobile en cas de modifications telles que des messages électroniques ou des éléments de contact ou de tâche nouveaux ou modifiés. Si des modifications interviennent pendant la durée de vie de la demande HTTPS, le serveur Exchange adresse une réponse au périphérique qui indique que des modifications sont intervenues et que le périphérique doit lancer une synchronisation avec le serveur Exchange. Le périphérique envoie ensuite cette demande au serveur. Une fois la synchronisation terminée, une nouvelle demande HTTPS à long terme est générée pour relancer le processus. Cela garantit que les éléments de messagerie, de calendrier, de contact et de tâche sont remis rapidement au périphérique mobile et qu’il est toujours synchronisé avec le serveur Exchange.

## Topologie Direct Push

La fonction Direct Push opère comme suit :

1.  Un périphérique mobile configuré pour se synchroniser avec un serveur Exchange 2013 envoie une demande HTTPS au serveur. Cette demande est appelée « PING ». La demande donne pour instruction au serveur d’avertir le périphérique en cas de modification, au cours des 15 minutes suivantes, d’éléments figurant dans un dossier configuré pour la synchronisation. Autrement, le serveur doit retourner un message HTTP 200 OK. Ensuite, le périphérique mobile passe en mode attente. Le délai de 15 minutes est appelé *intervalle d’interrogation*.

2.  Si aucun élément ne change dans les 15 minutes, le serveur retourne une réponse HTTP 200 OK. Le périphérique mobile reçoit cette réponse, reprend son activité (*réveil*), puis renvoie la demande. Cette action relance le processus.

3.  Si des éléments changent ou si de nouveaux éléments sont reçus dans l’intervalle d’interrogation de 15 minutes, le serveur envoie une réponse informant le périphérique mobile de la présence d’un élément nouveau ou modifié et indiquant le nom du dossier dans lequel se trouve cet élément. Après que le périphérique mobile a reçu cette réponse, il émet une demande de synchronisation pour le dossier contenant l’élément nouveau ou modifié. Une fois la synchronisation terminée, le périphérique mobile émet une nouvelle demande PING et tout le processus recommence.

La fonction Direct Push dépend des conditions de fonctionnement du réseau qui prennent en charge une demande HTTPS à long terme. Si le réseau opérateur pour le périphérique mobile ou le pare-feu ne prend pas en charge les demandes HTTPS à long terme, la demande HTTPS est interrompue. Les étapes suivantes décrivent la manière dont la fonction Direct Push opère quand un réseau opérateur de périphérique mobile a une valeur de délai d’expiration définie sur 13 minutes.

1.  Un périphérique mobile envoie une demande HTTPS au serveur. La demande donne pour instruction au serveur d’avertir le périphérique en cas de modification, au cours des 15 minutes suivantes, d’éléments figurant dans un dossier configuré pour la synchronisation. Autrement, le serveur doit retourner un message HTTP 200 OK. Ensuite, le périphérique mobile passe en mode attente.

2.  Si le serveur ne répond pas après 15 minutes, le périphérique mobile s’éveille et conclut que la connexion au serveur a été interrompue par le réseau à l’issue du délai d’expiration. Le périphérique renvoie la demande HTTPS mais en utilisant un intervalle d’interrogation de huit minutes.

3.  Après huit minutes, le serveur envoie un message HTTP 200 OK. Le périphérique tente alors d’établir une connexion plus longue en envoyant une nouvelle demande HTTPS au serveur, avec un intervalle d’interrogation de 12 minutes.

4.  Après quatre minutes, un nouveau message électronique est reçu et le serveur réagit en envoyant une demande HTTPS invitant le périphérique à se synchroniser. Le périphérique se synchronise et renvoie la demande HTTPS avec l’intervalle d’interrogation de 12 minutes.

5.  Après 12 minutes, à défaut d’élément nouveau ou modifié, le serveur répond en envoyant un message HTTP 200 OK. Le périphérique s’éveille et conclut que les conditions de fonctionnement du réseau prennent en charge un intervalle d’interrogation de 12 minutes. Le périphérique tente alors d’établir une connexion plus longue en renvoyant une demande HTTPS avec un intervalle d’interrogation de 16 minutes.

6.  Après 16 minutes, aucune réponse n’est reçue du serveur. Le périphérique s’éveille et conclut que les conditions de fonctionnement du réseau ne peuvent pas prendre en charge un intervalle d’interrogation de 16 minutes. Comme cette défaillance s’est produite juste après que le périphérique a tenté d’allonger l’intervalle d’interrogation, le périphérique conclut que l’intervalle d’interrogation a atteint sa limite maximale. Le périphérique envoie ensuite une demande HTTPS avec un intervalle d’interrogation de 12 minutes parce que c’était le dernier intervalle d’interrogation correctement établi.

Le périphérique mobile tente d'utiliser l'intervalle d'interrogation le plus long pris en charge par le réseau. Cela permet de prolonger la durée de vie de la batterie sur le périphérique et réduit la quantité de données transférées sur le réseau. Les opérateurs mobiles peuvent spécifier une valeur d'intervalle d'interrogation maximale, minimale et initiale pour le périphérique mobile dans les paramètres de registre.

## Configuration de la fonction Direct Push pour opérer à travers un pare-feu

Pour que la fonction Direct Push fonctionne via votre pare-feu, vous devez ouvrir le port TCP 443. Ce port est nécessaire pour les SSL (Secure Sockets Layer) et doit être ouvert entre Internet et le serveur d’accès au client.

Outre l’ouverture de ports sur votre pare-feu, pour optimiser des performances de la fonction Direct Push, il est recommandé d’augmenter la valeur de délai d’expiration sur le pare-feu en modifiant la valeur par défaut de 15 à 30 minutes. La longueur maximale de la demande HTTPS est déterminée par les paramètres suivants :

  - La valeur de délai maximale définie sur les pare-feu qui contrôlent le trafic depuis Internet vers le serveur d’accès au client

  - Les valeurs de délai de pare-feu qui sont définies par l’opérateur mobile

