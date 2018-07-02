---
title: 'Tâches de gestion du répertoire virtuel Exchange ActiveSync: Exchange 2013 Help'
TOCTitle: Tâches de gestion du répertoire virtuel Exchange ActiveSync
ms:assetid: f0b339b7-e184-4392-a133-20523183459d
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb125170(v=EXCHG.150)
ms:contentKeyID: 50479509
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Tâches de gestion du répertoire virtuel Exchange ActiveSync

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2012-10-05_

Vous pouvez gérer plusieurs de ces paramètres d’application Exchange ActiveSync dans Exchange Server 2013 via le répertoire virtuel Exchange ActiveSync. Un répertoire virtuel est utilisé par Internet Information Services (IIS) pour autoriser l’accès à une application web, par exemple Exchange ActiveSync. Certains des paramètres du répertoire virtuel, que vous pouvez gérer pour Exchange ActiveSync incluent l’authentification, de sécurité et de création de rapports.

## Paramètres de répertoire virtuel Exchange ActiveSync

Vous pouvez modifier les propriétés et les paramètres sur le répertoire virtuel Exchange ActiveSync suivantes :

  - **InternalURL** Le InternalURL est l’URL que les clients internes peuvent utiliser pour accéder au répertoire virtuel. Il est généralement dans le format https://servername/Microsoft-Server-ActiveSync. Par exemple, si le nom NetBIOS du serveur est Sequoia, le InternalURL serait https://sequoia/Microsoft-Server-ActiveSync.

  - **ExternalURL** ExternalURL est l’URL que les clients externes peuvent utiliser pour accéder au répertoire virtuel. Cette URL doit être accessible depuis l’extérieur de votre réseau interne. Par exemple, votre ExternalURL pourrait être https://www.contoso.com/.

  - **Paramètres d’authentification** Les deux méthodes d’authentification que vous pouvez configurer pour le répertoire virtuel Exchange ActiveSync sont l’authentification de base et authentification par certificat Client.

