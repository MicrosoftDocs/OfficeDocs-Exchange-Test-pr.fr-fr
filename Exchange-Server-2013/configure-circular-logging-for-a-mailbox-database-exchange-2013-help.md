---
title: 'Config. la journal. circulaire pour une BDD de BAL: Exchange 2013 Help'
TOCTitle: Configurer la journalisation circulaire pour une base de données de boîte aux lettres
ms:assetid: 29cbd7cd-382b-4e0d-8368-2e49e75df2fc
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dn756374(v=EXCHG.150)
ms:contentKeyID: 62524823
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configurer la journalisation circulaire pour une base de données de boîte aux lettres

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2014-06-24_

Lorsque vous activez la journalisation circulaire pour une base de données de boîtes aux lettres, le type de journalisation circulaire que vous obtenez dépend de l’utilisation ou non de la méthode de réplication continue pour la réplication de la base de données de boîte aux lettres :

  - Si la base de données de boîte aux lettres n’est pas répliquée, elle utilisera la journalisation circulaire de type JET. Dans ce cas, l’activation ou la désactivation de la journalisation circulaire de type JET exige le démontage et le remontage de la base de données.

  - Si la base de données de boîte aux lettres est répliquée, elle utilisera la journalisation circulaire à réplication continue (CRCL). Dans ce cas, l’activation ou la désactivation de l’enregistrement circulaire à réplication continue prend effet de manière dynamique. Il est inutile de démonter et de remonter la base de données.

Pour plus d’informations sur la journalisation circulaire et la CRCL, consultez la rubrique [Exchange Native Data Protection](backup-restore-and-disaster-recovery-exchange-2013-help.md).

## Ce qu’il faut savoir avant de commencer

  - Durée d’exécution estimée : 1 minute

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l’entrée « Autorisations de base de données de boîtes aux lettres » dans la rubrique [Autorisations des destinataires](recipients-permissions-exchange-2013-help.md).

## Utiliser le CAE pour configurer la journalisation circulaire pour une base de données

1.  Dans la CCE, accédez à **Serveurs** \> **Bases de données**.

2.  Sélectionnez la base de données de boîtes aux lettres que vous voulez configurer, puis cliquez sur ![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

3.  Activez ou désactivez la case **Activer la journalisation circulaire**, puis cliquez sur **Enregistrer**.

4.  Si des opérations de démontage et de montage sont nécessaires, un message d’avertissement s’affiche. Cliquez sur **OK** pour fermer le message d’avertissement.
    
    1.  Pour démonter la base de données, cliquez sur **Plus**![Icône Options supplémentaires](images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif "Icône Options supplémentaires"), puis cliquez sur **Démonter**. Cliquez sur **Oui** lorsque le message d’avertissement s’affiche.
    
    2.  Pour monter la base de données, cliquez sur **Plus**![Icône Options supplémentaires](images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif "Icône Options supplémentaires"), puis cliquez sur **Monter**. Cliquez sur **Oui** lorsque le message d’avertissement s’affiche.

## Utiliser l’environnement de ligne de commande Exchange Management Shell pour configurer la journalisation circulaire pour une base de données

Cet exemple active la journalisation circulaire de la base de données DB1.

```powershell
Set-MailboxDatabase DB1 -CircularLoggingEnabled $True
```

Cet exemple désactive la journalisation circulaire de la base de données DB1.

```powershell
Set-MailboxDatabase DB1 -CircularLoggingEnabled $False
```

Voir [Set-MailboxDatabase](https://technet.microsoft.com/fr-fr/library/bb123971\(v=exchg.150\)) pour découvrir les autres paramètres de base de données de boîte aux lettres que vous pouvez configurer.

