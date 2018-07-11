---
title: 'Gestion hybride dans les déploiements hybrides Exchange: Exchange 2013 Help'
TOCTitle: Gestion hybride dans les déploiements hybrides Exchange
ms:assetid: 233f9f34-3ff5-47e1-a9e8-3244ee868d6e
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ659048(v=EXCHG.150)
ms:contentKeyID: 50479663
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Gestion hybride dans les déploiements hybrides Exchange

 

_<strong>Sapplique à :</strong>Exchange Server 2013, Exchange Server 2016_

_<strong>Dernière rubrique modifiée :</strong>2016-12-09_

Quand vous installez un serveur Exchange, les outils de gestion Exchange sont automatiquement installés sur le serveur. Vous utiliserez les outils suivants pour configurer et gérer l’organisation Exchange locale et l’organisation Exchange Online :

  - **Centre d'administration Exchange**   Le CAE est une console de gestion web qui offre une grande facilité d'utilisation et qui est optimisée pour des déploiements Exchange hybrides, en ligne ou locaux. Le CAE remplace la Console de gestion Exchange (EMC) et le Panneau de configuration Exchange (ECP) qui étaient les interfaces utilisées pour gérer Exchange Server 2010.

  - **Exchange Management Shell**   L’Environnement de ligne de commande Exchange Management Shell est une interface de ligne de commande basée sur Windows PowerShell.

## Centre d’administration Exchange.

Le CAE vous permet d’effectuer de nombreuses tâches de déploiement et la plupart des tâches administratives quotidiennes les plus courantes sur les serveurs Exchange locaux et dans l’organisation Exchange Online. Il est installé par défaut sur chaque serveur Exchange 2013 ou serveur plus récent. Par ailleurs, dans la mesure où il s’agit d’une console de gestion basée sur le web, vous pouvez également y accéder à l’aide d’un navigateur web sur d’autres ordinateurs de votre réseau ou via Internet à l’aide de l’URL du répertoire virtuel de l’ECP.

Vous pouvez accéder à l’organisation Exchange Online dans le CAE en sélectionnant l’onglet de navigation entre différents locaux d’Office 365. La navigation entre différents locaux vous permet de basculer facilement de votre organisation Exchange Online à votre organisation Exchange locale. Si vous avez configuré un déploiement hybride, sélectionnez l’onglet Office 365 pour gérer des objets destinataires et l’organisation Exchange Online. Si vous n’avez pas d’organisation Exchange Online, sélectionnez le lien Office 365 pour être redirigé vers la page de connexion d’Office 365.

Pour plus d'informations sur le CAE, consultez la rubrique [Centre d’administration Exchange dans Exchange 2013](https://technet.microsoft.com/fr-fr/library/jj150562\(v=exchg.150\)).

## L’Environnement de ligne de commande Exchange Management Shell

L’Environnement de ligne de commande Exchange Management Shell vous permet de réaliser les mêmes tâches que le CAE, ainsi que d’autres tâches spécifiques pouvant uniquement être réalisées dans l’Environnement de ligne de commande Exchange Management Shell. L’Environnement de ligne de commande Exchange Management Shell est un ensemble de cmdlets et de scripts Windows PowerShell installés sur un ordinateur lors de l’installation des outils de gestion Exchange. Ces scripts et cmdlets ne sont chargés que si l’Environnement de ligne de commande Exchange Management Shell est ouvert au moyen de l’icône Environnement de ligne de commande Exchange Management Shell. Si vous ouvrez directement Windows PowerShell, les scripts et cmdlets Exchange ne sont pas chargés et vous ne pouvez pas gérer l’organisation locale.

> [!NOTE]
> Vous pouvez créer une connexion Windows PowerShell manuelle à votre organisation locale, de la même manière que pour une connexion à l’organisation Exchange Online ci-dessous. Toutefois, il est vivement recommandé d’utiliser l’icône Environnement de ligne de commande Exchange Management Shell pour ouvrir l’Environnement de ligne de commande Exchange Management Shell sur vos serveurs Exchange locaux.


Lorsque vous ouvrez l’Environnement de ligne de commande Exchange Management Shell via l’icône Environnement de ligne de commande Exchange Management Shell sur un ordinateur disposant des outils de gestion, vous pouvez gérer votre organisation locale. Cependant, vous ne pouvez pas gérer l’organisation Exchange Online si vous ouvrez l’Environnement de ligne de commande Exchange Management Shell via cette icône. En effet, l’ouverture de l’Environnement de ligne de commande Exchange Management Shell à l’aide de l’icône Environnement de ligne de commande Exchange Management Shell vous connecte automatiquement à un serveur Exchange local.

Si vous voulez gérer l’organisation Exchange Online à l’aide de Windows PowerShell, vous devez ouvrir Windows PowerShell directement, sans utiliser l’icône Environnement de ligne de commande Exchange Management Shell. Quand vous ouvrez Windows PowerShell, vous pouvez spécifier manuellement la connexion à établir. Quand vous créez une connexion manuelle, vous spécifiez un compte administrateur dans l’organisation cliente Office 365, puis exécutez une commande de connexion. Une fois la connexion établie, les cmdlets Exchange que vous êtes autorisé à exécuter sont mises à votre disposition. Pour plus d’informations, consultez la rubrique [Utiliser Windows PowerShell](http://go.microsoft.com/fwlink/p/?linkid=209660).

Si vous n’êtes pas familiarisé avec l’Environnement de ligne de commande Exchange Management Shell et que vous souhaitez obtenir des informations de base sur le fonctionnement, la syntaxe des commandes, etc., de l’Environnement de ligne de commande Exchange Management Shell, consultez la rubrique [Utilisation de PowerShell avec Exchange 2013 (Exchange Management Shell)](https://technet.microsoft.com/fr-fr/library/bb123778\(v=exchg.150\)).

