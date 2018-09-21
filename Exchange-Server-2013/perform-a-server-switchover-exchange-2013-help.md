---
title: 'Effectuer un basculement de serveur: Exchange 2013 Help'
TOCTitle: Effectuer un basculement de serveur
ms:assetid: ffcefd56-b0a0-4229-9011-fff4197b7c74
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dd298187(v=EXCHG.150)
ms:contentKeyID: 62523889
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Effectuer un basculement de serveur

 

_**Sapplique à :** Exchange Server 2013 SP1_

_**Dernière rubrique modifiée :** 2014-06-23_

Un basculement de serveur est une opération effectuée dans le but de déplacer toutes les copies de base de données de boîtes aux lettres actives du serveur de boîtes aux lettres actuel vers un ou plusieurs autres serveurs de boîtes aux lettres au sein d'un groupe de disponibilité de base de données. Cette tâche est effectuée dans le cadre de la préparation d’une interruption programmée pour le serveur de boîtes aux lettres actuel.

## Ce que vous devez savoir avant de commencer

  - Durée d’exécution estimée : 30 secondes par base de données

  - l’entrée Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez « Groupes de disponibilité de base de données » dans la rubrique [Autorisations de haute disponibilité et de résilience des sites](high-availability-and-site-resilience-permissions-exchange-2013-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..


## Utiliser le Centre d’administration Exchange (CAE) pour effectuer un basculement de serveur

l’entrée Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez « Copies de bases de données de boîtes aux lettres » dans la rubrique [Autorisations de haute disponibilité et de résilience des sites](high-availability-and-site-resilience-permissions-exchange-2013-help.md).

1.  Dans le CAE, accédez à **Serveurs** \> **serveurs**.

2.  Sélectionnez le serveur de boîtes de données à faire basculer.

3.  Dans le volet d’informations, sélectionnez **Basculement du serveur**.

4.  Sur la page **Basculement du serveur**, effectuez l’une des opérations suivantes :
    
    1.  Acceptez le paramètre par défaut **Choisir automatiquement un serveur cible** (dans ce cas, le système sélectionne automatiquement le serveur de boîtes aux lettres le mieux adapté à chaque base de données basculée), puis cliquez sur **OK**.
    
    2.  Cliquez sur **Utilisez le serveur spécifié en tant que cible pour le basculement**, sur **Parcourir** pour choisir un serveur de boîtes aux lettres, puis sur **enregistrer**.

5.  Une fois le basculement terminé, cliquez sur **fermer** pour quitter la page **Basculement du serveur**.

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour effectuer un basculement de serveur

Cet exemple effectue un basculement de serveur pour le serveur MBX1. Le système sélectionne automatiquement le serveur de boîtes aux lettres le mieux adapté à chaque base de données active sur MBX1.

```powershell
Move-ActiveMailboxDatabase -Server MBX1
```

Cet exemple effectue un basculement de serveur pour le serveur de boîtes aux lettres MBX4. Une fois la commande exécutée, MBX5 héberge la copie active des bases de données précédemment actives sur MBX4.

```powershell
Move-ActiveMailboxDatabase -Server MBX4 -ActivateOnServer MBX5
```

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Move-ActiveMailboxDatabase](https://technet.microsoft.com/fr-fr/library/dd298068\(v=exchg.150\)).

