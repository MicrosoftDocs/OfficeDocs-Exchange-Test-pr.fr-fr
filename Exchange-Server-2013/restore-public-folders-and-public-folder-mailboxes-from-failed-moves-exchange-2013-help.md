---
title: 'Restauration de dossiers publics et de boîtes aux lettres de dossiers publics à partir de déplacements ayant échoué: Exchange 2013 Help'
TOCTitle: Restauration de dossiers publics et de boîtes aux lettres de dossiers publics à partir de déplacements ayant échoué
ms:assetid: 2ade83c9-5f9b-4945-bf32-48fa8185b515
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ983802(v=EXCHG.150)
ms:contentKeyID: 52062955
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Restauration de dossiers publics et de boîtes aux lettres de dossiers publics à partir de déplacements ayant échoué

 

_**Sapplique à :** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2013-02-13_

Si une demande de déplacement pour un dossier public ou une boîte aux lettres de dossiers publics échoue, vous pouvez restaurer le dossier ou la boîte aux lettres du moment que les conditions suivantes soient remplies :

  - **Déplacement de dossier public en échec**   Une copie du dossier public supprimé (récupérable) existe toujours dans la boîte aux lettres de dossiers publics source et se trouve encore dans la période de rétention.

  - **Déplacement de boîte aux lettres de dossiers publics en échec**   Une copie de la boîte aux lettres de dossiers publics supprimée (récupérable) existe toujours dans la base de données de boîtes aux lettres source et se trouve encore dans la période de rétention de la boîte aux lettres.

Si la période de rétention de la boîte aux lettres est écoulée, vous pouvez récupérer une boîte aux lettres de dossiers publics d'après une sauvegarde. Vous pouvez ensuite extraire les données de la boîte aux lettres restaurée et les copier dans un dossier cible ou les fusionner avec les données d'une autre boîte aux lettres. Pour plus d'informations, consultez la rubrique [Restaurer des données à l’aide d’une base de données de récupération](restore-data-using-a-recovery-database-exchange-2013-help.md).

Pour les autres tâches de gestion relatives aux dossiers publics, consultez la rubrique [Procédures relatives aux dossiers publics](public-folder-procedures-exchange-2013-help.md).

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : 5 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l'entrée « Demande de restauration de boîte aux lettres » dans la rubrique [Autorisations des destinataires](recipients-permissions-exchange-2013-help.md).

  - Vous ne pouvez pas utiliser le Centre d’administration Exchange pour effectuer cette procédure. Vous devez utiliser l'environnement de ligne de commande Exchange Management Shell.

  - Pour créer une demande de restauration, vous devez renseigner les valeurs des paramètres *DisplayName*, *LegacyDN* ou *MailboxGUID* pour la boîte aux lettres de dossiers publics supprimée (récupérable).

  - Par défaut, les dossiers conteneur de dépôt sont restaurés avec des dossiers normaux. Ce comportement peut être désactivé à l'aide du paramètre *ExcludeDumpster*.

  - La restauration de boîtes aux lettres de dossiers publics et la restauration de boîtes aux lettres classiques sont différentes dans le sens où les dossiers ne sont pas créés s'ils n'existent pas dans la boîte aux lettres cible. Les dossiers manquants sont affichés dans un message d'avertissement à la fin de la demande de restauration.

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.


## Que souhaitez-vous faire ?

## Restaurer un dossier public supprimé (récupérable)

Cet exemple permet de restaurer le dossier public \\Dev\\CustomerEnagagements vers la boîte aux lettres de dossiers publics cibles Development01.

    New-MailboxRestoreRequest -SourceStoreMailbox Development -SourceDatabase MBX_DB01 -TargetMailbox Development01 -AllowLegacyDNMismatch -IncludeFolders \Dev\CustomerEngagements

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, consultez la rubrique [New-MailboxRestoreRequest](https://technet.microsoft.com/fr-fr/library/ff829875\(v=exchg.150\)).

## Restaurer une boîte aux lettres de dossiers publics supprimée (récupérable)

Cet exemple permet de restaurer la boîte aux lettres de dossiers publics PF\_Singapore vers la nouvelle boîte aux lettres de dossiers publics PF\_Singapore\_Restore.

    New-MailboxRestoreRequest -SourceStoreMailbox PF_Singapore -SourceDatabase MBX_DB01 -TargetMailbox PF_Singapore_Restore -AllowLegacyDNMismatch

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, consultez la rubrique [New-MailboxRestoreRequest](https://technet.microsoft.com/fr-fr/library/ff829875\(v=exchg.150\)).

