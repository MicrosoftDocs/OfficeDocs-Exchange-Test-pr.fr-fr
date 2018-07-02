---
title: 'Serveurs de transport Edge: Exchange 2013 Help'
TOCTitle: Serveurs de transport Edge
ms:assetid: cfff9f59-afac-447c-8297-afcebe49a52d
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb124701(v=EXCHG.150)
ms:contentKeyID: 61180548
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Serveurs de transport Edge

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2016-09-29_

Les serveurs de transport Edge réduisent la surface d’attaque en traitant tout le flux de messagerie Internet, ce qui fournit des services d’hôte actif et de relais SMTP (Simple Mail Transfer Protocol) pour votre organisation Exchange. Les agents exécutés sur le serveur de transport Edge fournissent des couches supplémentaires de sécurité et de protection des messages. Ces agents fournissent une protection contre le courrier indésirable et appliquent des règles de transport pour contrôler le flux de messagerie.

Comme le serveur de transport Edge est installé dans le réseau de périmètre, il n’est jamais membre de la forêt Active Directory interne de votre organisation et n’a pas accès aux informations Active Directory. Toutefois, le serveur de transport Edge requiert des données résidant dans Active Directory, par exemple des informations sur le connecteur pour le flux de messagerie et des informations sur le destinataire pour les tâches du blocage du courrier indésirable de recherche du destinataire. Ces données sont synchronisées avec le serveur de transport Edge par le service Microsoft Exchange EdgeSync (EdgeSync). EdgeSync est un ensemble de processus exécutés sur un serveur de boîtes aux lettres Exchange 2013 afin d’établir une réplication unidirectionnelle des informations de destinataire et de configuration à partir d’Active Directory vers l’instance Active Directory Lightweight Directory Services (AD LDS) sur le serveur de transport Edge. EdgeSync ne copie que les informations dont le serveur de transport Edge a besoin pour exécuter des tâches relatives à la configuration du blocage du courrier indésirable et pour activer un flux de messagerie de bout en bout. EdgeSync exécute des mises à jour planifiées de façon à ce que les informations disponibles dans AD LDS soient actualisées.

Vous pouvez installer plusieurs serveurs de transport Edge dans le réseau de périmètre. Le déploiement de plusieurs serveurs de transport Edge assure des capacités de redondance et de basculement pour le flux des messages entrants. Vous pouvez équilibrer la charge du trafic SMTP de votre organisation parmi des serveurs de transport Edge en définissant plusieurs enregistrements MX avec la même valeur de priorité pour votre domaine de messagerie. Vous pouvez obtenir une configuration cohérente parmi plusieurs serveurs de transport Edge en utilisant des scripts de configuration dupliquée.

Le rôle serveur de transport Edge permet de gérer les scénarios de traitement des messages suivants.

## Flux de messagerie Internet

Les serveurs de transport Edge acceptent des messages entrants dans l’organisation Exchange et provenant d’Internet. Une fois les messages traités par le serveur de transport Edge, ils sont routés en fonction de la configuration de vos serveurs Exchange internes :

  - Si le serveur d’accès au client et le serveur de boîtes aux lettres sont installés sur des ordinateurs distincts, le courrier est routé vers le service de transport sur le serveur de boîtes aux lettres. Le serveur d’accès au client est contourné pour le flux de messagerie SMTP entrant.

  - Si le serveur d’accès au client et le serveur de boîtes aux lettres sont installés sur le même ordinateur, le courrier est routé vers le service de transport frontal sur le serveur d’accès au client, puis vers le service de transport sur le serveur de boîtes aux lettres.

Tous les messages envoyés à Internet depuis l’organisation sont routés vers des serveurs de transport Edge après qu’ils ont été traités par le service de transport sur le serveur de boîtes aux lettres. Vous pouvez configurer le serveur de transport Edge pour qu'il utilise DNS pour résoudre des enregistrements de ressource MX pour des domaines SMTP externes, ou configurer le serveur de transport Edge pour qu'il transfère les messages à un hôte actif pour la résolution DNS.

## Protection contre le courrier indésirable

Dans Exchange 2013, les fonctionnalités de blocage du courrier indésirable offrent des services permettant de bloquer les messages publicitaires non sollicités (courrier indésirable) au niveau du périmètre de réseau.

Les spammeurs utilisent toutes sortes de techniques pour envoyer du courrier indésirable à votre organisation. Les serveurs de transport Edge empêchent que les utilisateurs reçoivent du courrier indésirable grâce à une série d’agents qui collaborent pour offrir différentes couches de filtrage et de protection. La définition d’intervalles de répulsion sur les connecteurs rend les tentatives de collecte d’adresses de messagerie inefficaces.

## Règles de transport Edge

Les règles de transport Edge sont utilisées pour contrôler le flux des messages échangés via Internet. Les règles de transport Edge sont configurées sur chaque serveur de transport Edge pour aider à protéger les ressources et les données du réseau d’entreprise en appliquant une action aux messages remplissant les conditions spécifiées. Les conditions des règles de transport Edge sont basées sur des données, telles que des mots ou des critères de texte spécifiques dans l’objet, le corps, l’en-tête du message, ou l’adresse de l’expéditeur, la valeur SCL ou le type de pièce jointe. Les actions déterminent le mode de traitement du message lorsqu'une condition spécifiée est vérifiée. Parmi les actions possibles, vous pouvez mettre un message en quarantaine, supprimer ou rejeter un message, ajouter des destinataires ou enregistrer un événement. Des exceptions facultatives permettent d'exempter certains messages de l'application d'une action.

## Réécriture d’adresses

La réécriture d’adresses présente une apparence cohérente des adresses de messagerie aux destinataires externes. Vous configurez la réécriture d’adresses sur les serveurs de transport Edge pour modifier les adresses SMTP sur les messages entrants et sortants. La réécriture d’adresses est particulièrement utile pour les organisations récemment fusionnées qui veulent présenter une apparence cohérente des adresses de messagerie.

Pour plus d’informations sur la réécriture d’adresses, voir [Réécriture d’adresses sur des serveurs de transport Edge](address-rewriting-on-edge-transport-servers-exchange-2013-help.md).

