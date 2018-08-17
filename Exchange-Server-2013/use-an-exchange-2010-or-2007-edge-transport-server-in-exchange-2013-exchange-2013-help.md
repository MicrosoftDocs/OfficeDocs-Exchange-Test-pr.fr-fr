---
title: 'Utilisation d’un srv de transp. Edge Exchange 2010 ou 2007 dans Exchange 2013'
TOCTitle: Utilisation d’un serveur de transport Edge Exchange 2010 ou 2007 dans Exchange 2013
ms:assetid: ce99b4bd-868c-4767-9009-e22c17ac0ac7
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ150569(v=EXCHG.150)
ms:contentKeyID: 50479195
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Utilisation d’un serveur de transport Edge Exchange 2010 ou 2007 dans Exchange 2013

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2016-12-09_

Le serveur de transport Edge est disponible dans Microsoft Exchange Server 2013 Service Pack 1 (SP1). Vous pouvez toutefois continuer à utiliser les serveurs de transport Edge Exchange Server 2007 ou Exchange Server 2010 que vous avez déployés dans votre réseau de périmètre. Vous pouvez aussi installer un nouveau serveur de transport Edge Exchange 2007 ou Exchange 2010 dans votre réseau de périmètre pour une organisation Exchange 2013 nouvellement créée ou mise à niveau.

Vous devez savoir ce qui suit :

  - Un serveur de transport Edge Exchange 2007 ou Exchange 2010 attend une connexion vers un serveur de transport Hub. Dans Exchange 2013, le service de transport existe sur le serveur de boîtes aux lettres. Par conséquent, il existe un flux de messagerie Internet entre le service de transport sur le serveur de boîtes aux lettres et le serveur de transport Edge, qui contourne efficacement le serveur d'accès au client Exchange 2013.

  - Vous pouvez abonner un serveur de transport Edge Exchange 2007 ou Exchange 2010 à un site Active Directory contenant uniquement des serveurs Exchange 2013. Vous pouvez importer le fichier d'abonnement Edge et exécuter EdgeSync sur un serveur de boîtes aux lettres Exchange 2013 autonome ou sur un serveur sur lequel les serveurs de boîtes aux lettres et d'accès au client sont installés sur le même ordinateur. Vous ne pouvez pas importer le fichier d'abonnement Edge ou exécuter EdgeSync sur un serveur d'accès au client Exchange 2013 autonome.

  - Les procédures de déploiement d'un nouveau serveur de transport Edge Exchange 2007 ou Exchange 2010 dans votre organisation Exchange 2013 sont, pour la plupart, identiques à celles des précédentes versions d'Exchange. Toutefois, toutes les procédures réalisées sur le serveur de transport Hub sont exécutées sur le serveur de boîtes aux lettres dans Exchange 2013. Les procédures sont les suivantes :
    
      - [Configurer le flux de messagerie Internet via un serveur de transport Edge abonné](https://go.microsoft.com/fwlink/p/?linkid=275859)
    
      - [Configurer le flux de messagerie entre un serveur de transport Edge et des serveurs de transport Hub sans utiliser EdgeSync](https://go.microsoft.com/fwlink/p/?linkid=276661)

