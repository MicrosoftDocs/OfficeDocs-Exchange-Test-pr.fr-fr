---
title: 'Activer ou désactiver le cryptage de rapport de journal: Exchange 2013 Help'
TOCTitle: Activer ou désactiver le cryptage de rapport de journal
ms:assetid: 1dedbe73-2c1a-4b14-8799-5091aaec7965
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dd638092(v=EXCHG.150)
ms:contentKeyID: 50477618
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Activer ou désactiver le cryptage de rapport de journal

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2016-12-09_

Décryptage de rapport de journal l’activation permet de joindre une copie de décryptage d’un message protégé par des droits à l’état du journal de l’agent de journalisation. Avant d’activer le déchiffrement de rapport de journal, vous devez ajouter la boîte aux lettres fédéré de remise pour le groupe de super utilisateurs configuré sur votre serveur de [Services AD RMS (Active Directory Rights Management Services) (AD RMS)](https://technet.microsoft.com/en-us/library/hh831364.aspx) .

Pour les autres tâches de gestion liées à la Gestion des droits relatifs à l’information (IRM), voir [Procédures de gestion des droits relatifs à l’information](information-rights-management-procedures-exchange-2013-help.md).

## Ce qu’il faut savoir avant de commencer ?

  - Durée d'exécution estimée : 1 minute

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l’entrée « Protection des droits » dans la rubrique [Stratégie de messagerie et autorisations de conformité](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

  - Une licence d’utilisation propriétaire est accordée aux membres du groupe de super utilisateurs lorsque ces derniers en font la demande à partir du cluster AD RMS. Cela leur permet de déchiffrer tout le contenu protégé par IRM qui a été créé par ce cluster.

  - Un cluster AD RMS doit être installé dans la forêt Active Directory.

  - La boîte aux lettres de remise fédérée a été ajoutée au groupe de super utilisateurs AD RMS. Pour plus d’informations, voir [Ajouter la boîte aux lettres de fédération au groupe de super utilisateurs AD RMS](add-the-federation-mailbox-to-the-ad-rms-super-users-group-exchange-2013-help.md).

  - Vous ne pouvez pas utiliser le Centre d’administration Exchange (CAE) pour activer le chiffrement du rapport du journal. Vous devez utiliser l'environnement de ligne de commande Exchange Management Shell.

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.


## Que souhaitez-vous faire ?

## Utiliser l’environnement de ligne de commande Exchange Management Shell pour activer le déchiffrement du rapport du journal

Cet exemple montre comment activer le déchiffrement du rapport du journal pour l’organisation Exchange.

```powershell
Set-IRMConfiguration -JournalReportDecryptionEnabled $true
```

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, consultez la rubrique [Set-IRMConfiguration](https://technet.microsoft.com/fr-fr/library/dd979792\(v=exchg.150\)).

## Utiliser l’environnement de ligne de commande Exchange Management Shell pour désactiver le déchiffrement du rapport du journal

Cet exemple montre comment désactiver le déchiffrement du rapport du journal pour l’organisation Exchange.

```powershell
Set-IRMConfiguration -JournalReportDecryptionEnabled $false
```

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Set-IRMConfiguration](https://technet.microsoft.com/fr-fr/library/dd979792\(v=exchg.150\)).

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez activé ou désactivé le chiffrement du rapport du journal, exécutez la cmdlet **Get-IRMConfiguration** et vérifiez la valeur de la propriété *JournalDecryptionEnabled*.

Exemples

