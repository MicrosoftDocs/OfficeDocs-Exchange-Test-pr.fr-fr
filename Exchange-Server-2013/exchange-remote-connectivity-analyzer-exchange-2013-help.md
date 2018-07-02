---
title: 'Analyseur de connectivité à distance Exchange: Exchange 2013 Help'
TOCTitle: Analyseur de connectivité à distance Exchange
ms:assetid: dd26698e-d00c-47f5-a7aa-c3894fe86c75
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Ff701693(v=EXCHG.150)
ms:contentKeyID: 50479347
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Analyseur de connectivité à distance Exchange

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2014-09-22_

L’analyseur de connectivité à distance Microsoft Exchange (ExRCA) vous permet de vous assurer que la connectivité de vos serveurs Exchange est correctement configurée. Si vous rencontrez des problèmes, il peut aussi vous aider à les résoudre. Le site web de l’ExRCA peut tester la connectivité de Microsoft Exchange ActiveSync, des services web Exchange, de MicrosoftOutlook et de la messagerie Internet.

## Tests de l’Analyseur de connectivité à distance

Vous pouvez effectuer plusieurs tests avec l’ExRCA. Ces tests fonctionnent sur Exchange 2007 et versions ultérieures pour les fonctionnalités suivantes :

  - Exchange ActiveSync

  - Services Web Exchange

  - Outlook

  - Messagerie Internet

## Tests Exchange ActiveSync

Vous pouvez effectuer les tests suivants pour Exchange ActiveSync :

  - **Exchange ActiveSync :**  ce test simule les étapes qu’utilise un périphérique mobile pour se connecter à un serveur Exchange à l’aide d’Exchange ActiveSync.

  - **Découverte automatique d’Exchange ActiveSync** : ce test effectue les étapes suivies par un appareil Exchange ActiveSync pour obtenir des paramètres via le service de découverte automatique.

## Tests de connectivité des services web Exchange

Les tests des services web Exchange permettent de vérifier les paramètres de la plupart des services web Exchange. Vous pouvez effectuer les tests suivants pour les services web Exchange :

  - **Synchronisation, notification, disponibilité et réponses automatiques** : ces tests explorent plusieurs tâches de base des services web Exchange pour confirmer qu’ils fonctionnent correctement. Ils sont notamment utiles pour les administrateurs informatiques devant résoudre des problèmes d’accès externe à l’aide d’Entourage EWS ou d’autres clients de services web.

  - **Accès au compte de service (développeurs) :**  ce test vérifie si un compte de service peut accéder à une boîte aux lettres donnée, créer et supprimer les éléments qui y figurent et y accéder via l’emprunt d’identité Exchange. Il est principalement utilisé par les développeurs d’applications pour vérifier s’il est possible d’accéder à des boîtes aux lettres avec d’autres informations d’identification.

## Tests de connectivité Microsoft Office Outlook

Vous pouvez effectuer les tests suivants pour évaluer la connectivité d’Outlook :

  - **Outlook Anywhere (RPC sur HTTP)** : ce test effectue les étapes suivies par Outlook pour se connecter via Outlook Anywhere (RPC sur HTTP).

  - **Découverte automatique Outlook** : ce test effectue les étapes suivies par Outlook pour obtenir les paramètres via le service de découverte automatique. Ce test ne se connecte pas réellement à une boîte aux lettres.

## Tests de messagerie Internet

Vous pouvez effectuer les tests suivants pour vérifier la messagerie Internet :

  - **Messagerie électronique** **SMTP entrante** : ce test effectue les étapes suivies par un serveur de messagerie Internet pour envoyer des messages SMTP entrants vers votre domaine.

  - **Messagerie électronique SMTP sortante** : ce test vérifie certaines caractéristiques de votre adresse IP sortante. Il effectue notamment une vérification des DNS inversés, des ID d’expéditeur et des listes rouges en temps réel.

  - **Boîte aux lettres POP :**  ce test effectue les étapes suivies par un client de messagerie pour se connecter à une boîte aux lettres via le service POP3.

  - **Boîte aux lettres IMAP :**  ce test effectue les étapes suivies par un client de messagerie pour se connecter à une boîte aux lettres via le service IMAP.

