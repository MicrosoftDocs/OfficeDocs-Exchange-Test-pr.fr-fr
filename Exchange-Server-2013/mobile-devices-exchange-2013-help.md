---
title: 'Appareils mobiles: Exchange 2013 Help'
TOCTitle: Appareils mobiles
ms:assetid: 93a949e7-b3ef-43ea-ae0c-6698826fc8d2
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb232129(v=EXCHG.150)
ms:contentKeyID: 50478740
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Appareils mobiles

 

_**Sapplique à :**Exchange Server 2013_

_**Dernière rubrique modifiée :**2012-09-24_

Les appareils mobiles activés pour MicrosoftExchange ActiveSync permettent aux utilisateurs d’accéder à la plupart de leurs données de boîte aux lettres Microsoft Exchange à toute heure et quel que soit l’endroit. De nombreux et différents appareils et téléphones mobiles sont compatibles avec Exchange ActiveSync. notamment, les téléphones Windows, téléphones mobiles Nokia, téléphones et tablettes Android et les appareils iPhone, iPod et iPad d’Apple.

Bien que les appareils mobiles qu’il s'agisse d’un téléphone ou non, prennent en charge Exchange ActiveSync, dans la majeure partie de la documentation de Microsoft Exchange ActiveSync, nous les désignons sous le terme *appareil mobile*. Sauf si la ou les fonctionnalités abordées nécessitent un signal de téléphone mobile, comme une notification de message par SMS, le terme « appareil mobile » s’applique à la fois aux téléphones et autres périphériques mobiles comme les tablettes.

## Exchange ActiveSync

Exchange ActiveSync est un protocole de communication qui permet un accès mobile direct aux messages électroniques, données de planification, contacts et tâches. Exchange ActiveSync est accessible sur les téléphones Windows et les téléphones tiers activés pour Exchange ActiveSync.

Exchange ActiveSync intègre la technologie Direct Push. Celle-ci utilise une connexion HTTPS chiffrée établie et maintenue entre l’appareil mobile et le serveur pour transmettre des nouveaux messages électroniques et autres données Exchange à l’appareil.

Pour utiliser la technologie Direct Push avec MicrosoftExchange Server 2013, vos utilisateurs doivent posséder un appareil mobile compatible avec Direct Push.

## Fonctionnalités d’Exchange ActiveSync

Exchange ActiveSync offre un accès à de nombreuses fonctionnalités différentes qui vous permettent d'appliquer des stratégies de sécurité sur des appareils mobiles. Exchange 2013 permet de configurer de nombreuses stratégies de boîte aux lettres d’appareil mobile et de contrôler les appareils mobiles qui peuvent se synchroniser avec votre serveur Exchange. Exchange ActiveSync vous permet d’envoyer une commande de réinitialisation à distance qui efface toutes les données d’un appareil mobile en cas de perte ou de vol de celui-ci. Les utilisateurs peuvent également lancer une réinitialisation à distance depuis Outlook Web App.

Exchange ActiveSync permet aux utilisateurs de générer un mot de passe de récupération. Ce mot de passe de récupération est enregistré sur l’appareil mobile et il est activé lorsqu’un utilisateur oublie son mot de passe. L’utilisateur génère le mot de passe de récupération en même temps qu’il génère le code confidentiel ou le mot de passe du périphérique. Ce mot de passe de récupération peut être utilisé pour déverrouiller l’appareil mobile. Immédiatement après utilisation du mot de passe de récupération, l’utilisateur devra créer un nouveau code confidentiel.

## POP3 et IMAP4

Si votre appareil mobile ne prend pas en charge Exchange ActiveSync ou ne nécessite pas l’ensemble étendu de fonctionnalités proposé par Exchange ActiveSync, vous pouvez utiliser POP3 ou IMAP4 pour accéder à votre messagerie électronique sur votre appareil mobile. Pour plus d’informations sur l’accès à POP3 et IMAP4 pour votre boîte aux lettres, consultez la rubrique [POP3 et IMAP4 dans Exchange Server 2013](pop3-and-imap4-in-exchange-server-2013-exchange-2013-help.md).

