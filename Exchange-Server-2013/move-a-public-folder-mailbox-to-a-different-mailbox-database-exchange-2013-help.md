---
title: "Déplacement d'une boîte aux lettres de dossiers publics vers une autre base de données de boîtes aux lettres: Exchange 2013 Help"
TOCTitle: Déplacement d'une boîte aux lettres de dossiers publics vers une autre base de données de boîtes aux lettres
ms:assetid: 67601d45-4824-4ae6-9a7e-b645ec3af4d3
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ906434(v=EXCHG.150)
ms:contentKeyID: 51407192
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Déplacement d'une boîte aux lettres de dossiers publics vers une autre base de données de boîtes aux lettres

 

_**Sapplique à :** Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2015-07-21_

À des fins d'équilibrage de la charge ou de déplacement de ressources plus près de leur emplacement géographique, vous pouvez avoir besoin de déplacer une boîte aux lettres de dossiers publics vers une autre base de données de boîtes aux lettres. À l'instar du déplacement d'une boîte aux lettres normale, vous utilisez les cmdlets **MoveRequest** pour déplacer une boîte aux lettres de dossiers publics. Pour plus d'informations sur le déplacement des boîtes aux lettres, consultez la rubrique [Déplacements de boîtes aux lettres dans Exchange 2013](mailbox-moves-in-exchange-2013-exchange-2013-help.md).

Pour découvrir d'autres tâches de gestion associées aux dossiers publics, consultez la rubrique [Procédures relatives aux dossiers publics](public-folder-procedures-exchange-2013-help.md).

## Ce qu'il faut savoir avant de commencer

  - La durée d'exécution estimée dépend de la taille de la boîte aux lettres de dossiers publics.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez la section « Autorisations de migration et de déplacement de boîtes aux lettres » dans la rubrique [Autorisations des destinataires](recipients-permissions-exchange-2013-help.md).

  - Vous ne pouvez pas effectuer cette procédure dans le Centre d'administration Exchange (CAE). Vous pouvez uniquement utiliser l'environnement de ligne de commande Exchange Management Shell.

  - En fonction de la taille de la boîte aux lettres de dossiers publics, le déplacement peut prendre plusieurs heures. Pendant ce temps, les utilisateurs ne seront pas en mesure d'accéder aux dossiers publics. De plus, les utilisateurs ne pourront pas accéder aux dossiers publics pendant un court moment tant que le dossier se trouve dans l'état « Fin en cours ».

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.


## Que souhaitez-vous faire ?

## Créer une demande de déplacement

La cmdlet **New-MoveRequest** permet de mettre en file d'attente la boîte aux lettres de dossiers publics dans la file d'attente du service de réplication de boîtes aux lettres Microsoft Exchange. Lorsque le service de réplication de boîtes aux lettres Microsoft Exchange est disponible, celui-ci récupère la demande de déplacement et commence à déplacer la boîte aux lettres de dossiers publics. Il exécute l'intégralité de la demande, du début jusqu'à la fin.

Cet exemple commence la demande de déplacement pour la boîte aux lettres de dossiers publics PF\_SanFrancisco vers la base de données de boîtes aux lettres MBX\_DB01.

    New-MoveRequest -Identity "PF_SanFrancisco" -TargetDatabase MBX_DB01

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, consultez la rubrique [New-MoveRequest](https://technet.microsoft.com/fr-fr/library/dd351123\(v=exchg.150\)).

## Créer une demande de déplacement à terminer ultérieurement

Au cours de l'étape finale de la demande de déplacement, lors de la phase `CompletionInProgress`, la boîte aux lettres de dossiers publics est verrouillée aux utilisateurs. Le cas échéant, vous pouvez interrompre la demande de déplacement avant qu'elle n'atteigne cette phase et la reprendre plus tard, lorsqu'elle n'aura aucun impact sur les utilisateurs.

Cet exemple commence la demande de déplacement pour la boîte aux lettres de dossiers publics PF\_SanFrancisco vers la base de données de boîtes aux lettres MBX\_DB01, et l'interrompt lorsqu'elle est prête à être effectuée.

    New-MoveRequest -Identity "PF_SanFrancisco" -TargetDatabase MBX_DB01 -SuspendWhenReadyToComplete

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, consultez la rubrique [New-MoveRequest](https://technet.microsoft.com/fr-fr/library/dd351123\(v=exchg.150\)).

Cet exemple récupère l'état du déplacement de boîte aux lettres en cours pour la boîte aux lettres de dossiers publics PF\_SanFrancisco.

    Get-MoveRequest -Identity "PF_SanFrancisco"

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, consultez la rubrique [Get-MoveRequest](https://technet.microsoft.com/fr-fr/library/dd335227\(v=exchg.150\)).

Quand la demande de déplacement atteint l'état Suspendu, vous pouvez reprendre la demande. Cet exemple reprend la demande de déplacement associée à la boîte aux lettres de dossiers publics PF\_SanFrancisco.

    Resume-MoveRequest -Identity "PF_SanFrancisco"

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, consultez la rubrique [Resume-MoveRequest](https://technet.microsoft.com/fr-fr/library/ee332320\(v=exchg.150\)).

## Comment savoir si cela a fonctionné ?

Pour vérifier que la demande de déplacement a bien été créée, exécutez la commande suivante :

    Get-MoveRequestStatistics -Identity PF_SanFrancisco | Format-List Status

L'état `Completed` indique que la demande de déplacement a réussi.

Si le déplacement échoue, vous devrez peut-être restaurer le dossier public. Pour plus d'informations, consultez la rubrique [Restauration de dossiers publics et de boîtes aux lettres de dossiers publics à partir de déplacements ayant échoué](restore-public-folders-and-public-folder-mailboxes-from-failed-moves-exchange-2013-help.md).

