---
title: 'Obtenir les stat. sur le dossier Éléments récupérables: Exchange 2013 Help'
TOCTitle: Obtenir les statistiques sur le dossier Éléments récupérables
ms:assetid: dee77958-ee87-4908-85e4-ad053bacd8b0
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Ff714343(v=EXCHG.150)
ms:contentKeyID: 52063012
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Obtenir les statistiques sur le dossier Éléments récupérables

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2015-01-22_

Le dossier Éléments récupérables contient des éléments supprimés par les utilisateurs de Microsoft Outlook et Microsoft OfficeOutlook Web App ou par l'Assistant Boîte aux lettres. La durée pendant laquelle les éléments supprimés sont conservés dans ce dossier est basée sur les paramètres de rétention des éléments supprimés configurés pour la base de données de boîtes aux lettres ou la boîte aux lettres. Par défaut, une base de données de boîtes aux lettres est configurée pour conserver les éléments supprimés pendant 14 jours. Les quotas d'éléments récupérables et d'avertissements des éléments récupérables sont définis respectivement sur 20 Go et 30 Go. Cependant, si une conservation pour litige ou inaltérable est activée pour la boîte aux lettres, le dossier Éléments récupérables peut accumuler les éléments supprimés au-delà de la période de rétention spécifiée et conserver également différentes versions des éléments de boîte aux lettres modifiés.

Lorsque le dossier Éléments récupérables atteint la limite de quota d'avertissements des éléments récupérables, un événement d'avertissement est enregistré dans le journal des événements de l'application. Si la boîte aux lettres n’est pas en conservation pour litige, les éléments sont supprimés sur la base du premier entré, premier sorti (FIFO). Toutefois, si la boîte aux lettres est en conservation pour litige, elle n’est jamais vidée, ce qui a pour effet de perturber son fonctionnement lorsque le quota d’éléments récupérables est atteint.

Par conséquent, il est important de surveiller le journal des événements pour d'éventuelles alertes générées quand les boîtes aux lettres atteignent les quotas d'éléments récupérables. Vous pouvez également utiliser cette procédure afin de créer des rapports de statistiques pour le dossier Éléments récupérables, en particulier pour les boîtes aux lettres placées en conservation pour litige.

Pour plus d'informations, consultez les rubriques suivantes :

  - [Dossier Éléments récupérables](recoverable-items-folder-exchange-2013-help.md)

  - [Conservation inaltérable et conservation pour litige](https://docs.microsoft.com/fr-fr/exchange/security-and-compliance/in-place-and-litigation-holds)

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : 1 minute

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l'entrée « Dossiers de boîte aux lettres » dans la rubrique [Autorisations des destinataires](recipients-permissions-exchange-2013-help.md).

  - Vous ne pouvez pas utiliser le Centre d'administration Exchange (CAE) pour obtenir des statistiques du dossier Éléments récupérables d'une boîte aux lettres.

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), et [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

## Que souhaitez-vous faire ?

## Obtenir des statistiques du dossier Éléments récupérables d'une boîte aux lettres

Cet exemple obtient des statistiques de dossiers du dossier Éléments récupérables de Soumya Singhi et affiche le résultat sous forme de liste.

```powershell
Get-MailboxFolderStatistics -Identity "Soumya Singhi" -FolderScope RecoverableItems | Format-List
```

Cet exemple obtient les statistiques de dossiers du dossier Éléments récupérables de 'oumya Singhi et affiche le nom et le chemin d'accès du dossier, le nombre d'éléments qu'il contient et sa taille sous forme de tableau.

```powershell
Get-MailboxFolderStatistics -Identity "Soumya Singhi" -FolderScope RecoverableItems | Format-Table Name,FolderPath,ItemsInFolder,FolderAndSubfolderSize
```

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, consultez la rubrique [Get-MailboxFolderStatistics](https://technet.microsoft.com/fr-fr/library/aa996762\(v=exchg.150\)).

## Obtenir les statistiques du dossier Éléments récupérables pour toutes les boîtes aux lettres en conservation pour litige

Cet exemple récupère une liste de toutes les boîtes aux lettres en conservation pour litige, ainsi que les statistiques des dossiers des boîtes aux lettres pour le dossier Éléments récupérables et ses sous-dossiers pour chaque boîte aux lettres. Les propriétés **Identity** (identité du dossier de boîte aux lettres) et **FolderAndSubfolderSize** s'affichent sous forme de tableau.

```powershell
Get-Mailbox -ResultSize Unlimited -Filter {LitigationHoldEnabled -eq $true} | Get-MailboxFolderStatistics | Format-Table Identity,FolderAndSubfolderSize
```

Pour des informations détaillées sur la syntaxe et les paramètres, consultez les rubriques [Get-Mailbox](https://technet.microsoft.com/fr-fr/library/bb123685\(v=exchg.150\)) et [Get-MailboxFolderStatistics](https://technet.microsoft.com/fr-fr/library/aa996762\(v=exchg.150\)).

## Obtenir le quota des éléments récupérables pour une boîte aux lettres

Cet exemple affiche le quota et le quota d’avertissement pour le dossier Éléments récupérables de la boîte aux lettres d’un utilisateur. Il récupère également les informations indiquant si une conservation pour litige ou inaltérable est placée sur la boîte aux lettres.

```powershell
Get-Mailbox -Identity <identity of mailbox> | Format-List RecoverableItems*,LitigationHoldEnabled,InPlaceHolds
```

Cet exemple affiche le quota et le quota d’avertissement pour le dossier Éléments récupérables de toutes les boîtes aux lettres des utilisateurs au sein de votre organisation. L’exemple récupère également les informations de conservation.

```powershell
Get-Mailbox -ResultSize Unlimited -Filter {RecipientTypeDetails -eq "UserMailbox"} | Format-List Name,RecoverableItems*,LitigationHoldEnabled,InPlaceHolds
```

