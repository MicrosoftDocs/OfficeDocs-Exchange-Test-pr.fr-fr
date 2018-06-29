---
title: 'Gérer les demandes de restauration de boîte aux lettres: Exchange 2013 Help'
TOCTitle: Gérer les demandes de restauration de boîte aux lettres
ms:assetid: 8e668a52-c601-4d96-a51c-ab60267e1321
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ863437(v=EXCHG.150)
ms:contentKeyID: 50555436
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Gérer les demandes de restauration de boîte aux lettres

 

_**Sapplique à :**Exchange Server 2013_

_**Dernière rubrique modifiée :**2015-03-09_

Les demandes de restauration de boîte aux lettres sont utilisées pour restaurer les boîtes aux lettres déconnectées. Une boîte aux lettres déconnectée est une boîte aux lettres d'une base de données de boîtes aux lettres Exchange qui n'est associée à aucun compte d'utilisateur Active Directory. Les boîtes aux lettres sont déconnectées lorsqu’elles sont désactivées, supprimées ou déplacés vers une autre base de données. Pour plus d'informations, consultez la rubrique [Boîtes aux lettres déconnectées](disconnected-mailboxes-exchange-2013-help.md).

Les boîtes aux lettres déconnectées restent dans la base de données de boîtes aux lettres durant le temps spécifié dans les paramètres de rétention de boîtes aux lettres supprimées définis pour la base de données de boîtes aux lettres. Par défaut, les boîtes aux lettres déconnectées sont conservées pendant 30 jours. Pendant cette période de rétention, le contenu d'une boîte aux lettres supprimée peut être restauré (copié) dans une boîte aux lettres existante. Cette rubrique décrit comment gérer des demandes de restauration de boîtes aux lettres à l'aide de l'environnement de ligne de commande.

Pour les autres tâches relatives aux boîtes aux lettres déconnectées, consultez les rubriques suivantes :

[Désactiver ou supprimer une boîte aux lettres](disable-or-delete-a-mailbox-exchange-2013-help.md)

[Connecter une boîte aux lettres déconnectée](connect-a-disabled-mailbox-exchange-2013-help.md)

[Connexion ou restauration d’une boîte aux lettres supprimée](connect-or-restore-a-deleted-mailbox-exchange-2013-help.md)

[Restaurer une boîte aux lettres supprimée (récupérable)](restore-a-soft-deleted-mailbox-exchange-2013-help.md)

[Supprimer définitivement une boîte aux lettres](permanently-delete-a-mailbox-exchange-2013-help.md)

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée de chaque procédure : 2 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l'entrée « Demande de restauration de boîte aux lettres » dans la rubrique [Autorisations des destinataires](recipients-permissions-exchange-2013-help.md).

  - Les procédures décrites dans cette rubrique ne peuvent être effectuées dans l'environnement de ligne de commande Exchange Management Shell. Il n’est pas possible d’utiliser le Centre d’administration Exchange (EAC) pour gérer des demandes de restauration de boîte aux lettres.

  - Pour afficher la valeur de la propriété *Identity* pour toutes les demandes de restauration de boîtes aux lettres, exécutez la commande suivante.
    
        Get-MailboxRestoreRequest | Format-Table Identity
    
    Vous pouvez utiliser cette valeur d’identité pour spécifier une demande spécifique de restauration de boîte aux lettres, si vous exécutez les procédures de cette rubrique.

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

<table>
<thead>
<tr class="header">
<th><img src="images/Bb125224.tip(EXCHG.150).gif" title="Conseil" alt="Conseil" />Conseil :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..</td>
</tr>
</tbody>
</table>


## Que souhaitez-vous faire ?

## Utiliser l'environnement de ligne de commande pour afficher les propriétés d'une demande de restauration

L'affichage des propriétés d'une demande de restauration de boîte aux lettres vous permet d'accéder aux informations de base sur le statut d'une demande de restauration de boîte aux lettres.

Pour afficher la liste et la valeur de la propriété *Identity* pour toutes les demandes de restauration de boîtes aux lettres, exécutez la commande suivante.

    Get-MailboxRestoreRequest | Format-Table Identity

Vous pouvez utiliser l'identité pour obtenir des informations sur des demandes spécifiques de restauration de boîtes aux lettres.

Cet exemple renvoie l'état de la demande de restauration « Pilar Pinilla \\MailboxRestore» à l'aide du paramètre *Identity*.

    Get-MailboxRestoreRequest -Identity "Pilar Pinilla\MailboxRestore"

Cet exemple renvoie toutes les informations concernant la deuxième demande de restauration pour la boîte aux lettres cible de Pilar Pinilla.

    Get-MailboxRestoreRequest -Identity "Pilar Pinilla\MailboxRestore1" | Format-List

Cet exemple renvoie l'état des demandes de restauration en cours de traitement à partir de la base de données source MBD01.

    Get-MailboxRestoreRequest -SourceDatabase MBD01

Cet exemple renvoie toutes les demandes de restauration actuellement en cours.

    Get-MailboxRestoreRequest -Status InProgress

D'autres états utiles sont `Queued`, `Completed`, `Suspended` et `Failed`.

Cet exemple renvoie toutes les demandes de restauration suspendues.

    Get-MailboxRestoreRequest -Suspend $true

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, consultez la rubrique [Get-MailboxRestoreRequest](https://technet.microsoft.com/fr-fr/library/ff829907\(v=exchg.150\)).

## Sortie de la cmdlet Get-MailboxRestoreRequest

Par défaut, la cmdlet **Get-MailboxRestoreRequest** renvoie le nom de la demande, la boîte aux lettres cible dans laquelle les données sont restaurées et l'état de la demande. Le tableau suivant répertorie des informations utiles renvoyées si vous canalisez la commande vers la cmdlet **Format-List**.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Valeur</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>SourceDatabase</code></p></td>
<td><p>Spécifie la base de données contenant la boîte aux lettres déconnectée en cours de restauration.</p></td>
</tr>
<tr class="even">
<td><p><code>TargetMailbox</code></p></td>
<td><p>Indique la boîte aux lettres dans laquelle les données sont restaurées.</p></td>
</tr>
<tr class="odd">
<td><p><code>Name</code></p></td>
<td><p>Indique le nom de la demande.</p></td>
</tr>
<tr class="even">
<td><p><code>RequestQueue</code></p></td>
<td><p>Indique la base de données sur laquelle le service de réplication de boîte aux lettres Exchange (MRS) enregistre l'état détaillé de la demande.</p></td>
</tr>
<tr class="odd">
<td><p><code>Status</code></p></td>
<td><p>Indique l'état de la demande.</p></td>
</tr>
<tr class="even">
<td><p><code>Suspend</code></p></td>
<td><p>Indique si la demande est suspendue. Une restauration de boîte aux lettres peut être suspendue si vous l’avez créée à l’aide de la cmdlet <strong>New-MailboxRestoreRequest</strong> avec le paramètre <em>Suspend</em>. Elle peut également être suspendue par un administrateur à l'aide de la cmdlet <strong>Suspend-MailboxRestoreRequest</strong> ou en cas d'échec de l'opération de restauration de boîte aux lettres.</p></td>
</tr>
<tr class="odd">
<td><p><code>Identity</code></p></td>
<td><p>Indique l'identité de la demande. Cette identité est une combinaison du nom de la boîte aux lettres cible et du nom de la demande.</p></td>
</tr>
</tbody>
</table>


## Comment savoir si cela a fonctionné ?

Exécutez la cmdlet **Get-MailboxRestoreRequest** pour vérifier que vous pouvez afficher les propriétés relatives aux demandes de restauration de boîtes aux lettres. Si la cmdlet renvoie une erreur, vérifiez que vous utilisez la syntaxe et l’identité correctes. Dans certains cas, l'exécution de la cmdlet peut réussir sans renvoyer de résultats. Par exemple, si vous avez soumis une demande de restauration de boîte aux lettres, puis exécuté la commande `Get-MailboxRestoreRequest -Status InProgress` et qu’aucun résultat n’est renvoyé, cela indique qu’aucune des demandes de restauration n’est actuellement exécutée.

## Utiliser l'environnement de ligne de commande pour afficher les statistiques d'une demande de restauration

L'affichage des statistiques d'une demande de restauration de boîte aux lettres vous permet de consulter des informations détaillées que vous pouvez utiliser à des fins de dépannage.

Cet exemple renvoie les statistiques par défaut de la demande de restauration danp\\MailboxRestore1. Par défaut, les informations renvoyées incluent le nom, la boîte aux lettres, l'état et le pourcentage d'exécution.

    Get-MailboxRestoreRequestStatistics -Identity danp\MailboxRestore1

Cet exemple renvoie les statistiques relatives à la boîte aux lettres de Dan Park et exporte le rapport dans un fichier .csv.

    Get-MailboxRestoreRequestStatistics -Identity "Dan Park\MailboxRestore" | Export-CSV \\SERVER01\RestoreRequest_Reports\DanPark_Restorestats.csv

Cet exemple renvoie des informations supplémentaires sur la demande de restauration de la boîte aux lettres de Pilar Pinilla à l’aide du paramètre *IncludeReport* et canalise les résultats vers la cmdlet **Format-List**.

    Get-MailboxRestoreRequestStatistics -Identity "Pilar Pinilla\MailboxRestore" -IncludeReport | Format-List 

Cet exemple renvoie des informations supplémentaires sur toutes les demandes de restauration dont l'état est `Failed` à l'aide du paramètre *IncludeReport*, puis enregistre les informations dans le fichier AllRestoreReports.txt à l'emplacement d'exécution de la commande.

    Get-MailboxRestoreRequest -Status Failed | Get-MailboxRestoreRequestStatistics -IncludeReport | Format-List > AllRestoreReports.txt

Pour des informations détaillées sur la syntaxe et les paramètres, consultez les rubriques [Get-MailboxRestoreRequestStatistics](https://technet.microsoft.com/fr-fr/library/ff829912\(v=exchg.150\)) et [Get-MailboxRestoreRequest](https://technet.microsoft.com/fr-fr/library/ff829907\(v=exchg.150\)).

## Sortie de la cmdlet Get-MailboxRestoreRequestStatistics

Par défaut, la cmdlet [Get-MailboxRestoreRequestStatistics](https://technet.microsoft.com/fr-fr/library/ff829912\(v=exchg.150\)) renvoie le nom et l'état de la demande, l'alias de la boîte aux lettres cible et le pourcentage d'exécution. Le tableau suivant répertorie d'autres informations utiles renvoyées si vous canalisez la cmdlet vers la cmdlet **Format-List**.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Valeur</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>Name</code></p></td>
<td><p>Indique le nom de la demande.</p></td>
</tr>
<tr class="even">
<td><p><code>Status</code></p></td>
<td><p>Indique l'état de la demande.</p></td>
</tr>
<tr class="odd">
<td><p><code>StatusDetail</code></p></td>
<td><p>Fournit des informations détaillées sur l'état de la demande. Par exemple, si la valeur <code>Status</code> renvoie <code>InProgress</code>, la valeur <code>StatusDetail</code> renverra les étapes spécifiques de l'état <code>InProgress</code>, telles que <code>CreatingFolderHierarchy</code> et <code>CopyingMessages</code>.</p></td>
</tr>
<tr class="even">
<td><p><code>SyncStage</code></p></td>
<td><p>Indique le pourcentage de traitement de la demande au cours du processus de restauration.</p></td>
</tr>
<tr class="odd">
<td><p><code>Suspend</code></p></td>
<td><p>Indique si la demande de restauration est suspendue. Cette valeur est <code>true</code> dans les cas suivants :</p>
<ul>
<li><p>MRS a interrompu ou est en train d'interrompre la demande en raison d'un échec.</p></li>
<li><p>Un administrateur a suspendu la demande.</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><code>SourceExchangeGuid</code></p></td>
<td><p>Indique le GUID de la boîte aux lettres source à partir de laquelle les données sont restaurées.</p></td>
</tr>
<tr class="odd">
<td><p><code>SourceRootFolder</code></p></td>
<td><p>Spécifie le nom du dossier racine dans la hiérarchie de boîtes aux lettres source à partir de laquelle les données sont restaurées. Si cette valeur n'est pas renseignée, les données sont restaurées à partir du dossier « Partie supérieure de la banque d'informations ».</p></td>
</tr>
<tr class="even">
<td><p><code>SourceDatabase</code></p></td>
<td><p>Indique le nom de la base de données dans laquelle se trouve la boîte aux lettres source.</p></td>
</tr>
<tr class="odd">
<td><p><code>MailboxRestoreFlags</code></p></td>
<td><p>Indique que la boîte aux lettres en cours de restauration est <code>Disabled</code> ou <code>Soft-Deleted</code>.</p></td>
</tr>
<tr class="even">
<td><p><code>TargetAlias</code></p></td>
<td><p>Indique l'alias de la boîte aux lettres cible.</p></td>
</tr>
<tr class="odd">
<td><p><code>TargetIsArchive</code></p></td>
<td><p>Indique si la boîte aux lettres est restaurée dans une archive.</p></td>
</tr>
<tr class="even">
<td><p><code>TargetExchangeGuid</code></p></td>
<td><p>Indique le GUID de la boîte aux lettres cible.</p></td>
</tr>
<tr class="odd">
<td><p><code>TargetRootFolder</code></p></td>
<td><p>Indique le nom du dossier racine dans la hiérarchie de boîtes aux lettres cible vers laquelle les données sont restaurées. Si la valeur n'est pas renseignée, les données sont restaurées dans le dossier « Partie supérieure de la banque d'informations ».</p></td>
</tr>
<tr class="even">
<td><p><code>TargetDatabase</code></p></td>
<td><p>Indique le nom de la base de données dans laquelle se trouve la boîte aux lettres cible.</p></td>
</tr>
<tr class="odd">
<td><p><code>TargetMailboxIdentity</code></p></td>
<td><p>Indique l'identité de la boîte aux lettres cible.</p></td>
</tr>
<tr class="even">
<td><p><code>IncludeFolders</code></p></td>
<td><p>Indique la liste des dossiers à inclure pendant la restauration. Si cette valeur n'est pas renseignée, cela signifie qu'aucun dossier n'a été spécifié lors de la création de la demande et que tous les dossiers sont restaurés dans la boîte aux lettres (sauf si le paramètre <em>ExcludeFolders</em> est utilisé pour exclure des dossiers spécifiques).</p></td>
</tr>
<tr class="odd">
<td><p><code>ExcludeFolders</code></p></td>
<td><p>Indique la liste des dossiers à exclure pendant la restauration. Si cette valeur n'est pas renseignée, cela signifie qu'aucun dossier n'a été spécifié lors de la création de la demande et que tous les dossiers sont restaurés dans la boîte aux lettres (sauf si le paramètre <em>IncludeFolders</em> est utilisé pour inclure des dossiers spécifiques).</p></td>
</tr>
<tr class="even">
<td><p><code>ExcludeDumpster</code></p></td>
<td><p>Indique si le dossier Éléments récupérables a été exclu au moment de la création de la demande.</p></td>
</tr>
<tr class="odd">
<td><p><code>ConflictResolutionOption</code></p></td>
<td><p>Indique l'action que MRS doit entreprendre s'il existe des messages correspondants dans les dossiers cible et source.</p></td>
</tr>
<tr class="even">
<td><p><code>AssociatedMessagesCopyOption</code></p></td>
<td><p>Indique si les messages associés sont copiés lors du traitement de la demande. Des messages associés constituent des messages spéciaux qui contiennent des données masquées avec des informations sur les règles, les écrans et les formulaires.</p></td>
</tr>
<tr class="odd">
<td><p><code>BadItemLimit</code></p></td>
<td><p>Indique le nombre d'éléments incorrects que MRS ignorera si la demande rencontre des messages endommagés.</p></td>
</tr>
<tr class="even">
<td><p><code>BadItemsEncountered</code></p></td>
<td><p>Indique le nombre de messages endommagés rencontrés par la commande. Si la valeur <em>BadItemsEncountered</em> est supérieure à la valeur <em>BadItemLimit</em> , la demande échoue.</p></td>
</tr>
<tr class="odd">
<td><p><code>QueuedTimeStamp</code></p></td>
<td><p>Indique la date et l'heure auxquelles la demande a été transmise au service MRS.</p></td>
</tr>
<tr class="even">
<td><p><code>StartTimeStamp</code></p></td>
<td><p>Indique les date et heure auxquelles le service de réplication de boîte aux lettres (MRS) a démarré le traitement de la demande de restauration.</p></td>
</tr>
<tr class="odd">
<td><p><code>LastUpdateTimeStamp</code></p></td>
<td><p>Indique la date et l'heure de la dernière modification apportée à la demande. La modification a pu être effectuée par un administrateur ou par MRS.</p></td>
</tr>
<tr class="even">
<td><p><code>SuspendTimeStamp</code></p></td>
<td><p>Indique la date et l'heure auxquelles la demande a été suspendue.</p></td>
</tr>
<tr class="odd">
<td><p><code>OverallDuration</code></p></td>
<td><p>Indique le temps qu'il a fallu pour traiter la demande. Si la demande est à l'état <code>Failed</code>, cette valeur indique la durée écoulée entre l'envoi de la demande et l'échec de son traitement. Si la demande n'est pas terminée, cette valeur indique la durée écoulée entre l'envoi de la demande et l'exécution de la cmdlet <strong>Get-MailboxRestoreRequestStatistics</strong>.</p></td>
</tr>
<tr class="even">
<td><p><code>TotalSuspendedDuration</code></p></td>
<td><p>Indique la durée pendant laquelle la demande était à l'état <code>Suspended</code>.</p></td>
</tr>
<tr class="odd">
<td><p><code>TotalFailedDuration</code></p></td>
<td><p>Indique la durée pendant laquelle la demande était à l'état <code>Failed</code>.</p></td>
</tr>
<tr class="even">
<td><p><code>TotalQueuedDuration</code></p></td>
<td><p>Indique la durée pendant laquelle la demande était à l'état <code>Queued</code>.</p></td>
</tr>
<tr class="odd">
<td><p><code>TotalInProgressDuration</code></p></td>
<td><p>Indique la durée pendant laquelle la demande était à l'état <code>In Progress</code>.</p></td>
</tr>
<tr class="even">
<td><p><code>TotalStalledDueToHADuration</code></p></td>
<td><p>Indique la durée pendant laquelle la demande a été bloquée pour cause de haute disponibilité.</p></td>
</tr>
<tr class="odd">
<td><p><code>MRSServerName</code></p></td>
<td><p>Indique le nom du serveur d'accès au client qui a traité la demande.</p></td>
</tr>
<tr class="even">
<td><p><code>EstimatedTransferSize</code></p></td>
<td><p>Indique la taille totale du fichier qui a été restauré ou que le service MRS prévoit de restaurer si l'état de la demande est <code>In Progress</code>.</p></td>
</tr>
<tr class="odd">
<td><p><code>EstimatedTransferItemCount</code></p></td>
<td><p>Indique le nombre d'éléments qui ont été restaurés ou que le service MRS prévoit de restaurer si la demande est à l'état <code>In Progress</code>.</p></td>
</tr>
<tr class="even">
<td><p><code>BytesTransferredPerMinute</code></p></td>
<td><p>Indique le nombre moyen d'octets qui ont été transférés par minute.</p></td>
</tr>
<tr class="odd">
<td><p><code>ItemsTransferred</code></p></td>
<td><p>Indique le nombre d'éléments qui ont été transférés.</p></td>
</tr>
<tr class="even">
<td><p><code>PercentComplete</code></p></td>
<td><p>Indique le pourcentage de traitement de la demande.</p></td>
</tr>
<tr class="odd">
<td><p><code>CompletedRequestAgeLimit</code></p></td>
<td><p>Indique le temps qu’une demande de restauration terminée doit être conservée avant d’être supprimée. La valeur par défaut est 30 jours.</p></td>
</tr>
<tr class="even">
<td><p><code>PositionInQueue</code></p></td>
<td><p>Si le traitement de la demande n'a pas commencé, cette valeur spécifie la position de la demande dans la file d'attente.</p></td>
</tr>
<tr class="odd">
<td><p><code>FailureCode</code></p></td>
<td><p>En cas de défaillance, cette valeur indique le code correspondant.</p></td>
</tr>
<tr class="even">
<td><p><code>FailureType</code></p></td>
<td><p>En cas de défaillance, cette valeur indique le type correspondant.</p></td>
</tr>
<tr class="odd">
<td><p><code>FailureSide</code></p></td>
<td><p>En cas de défaillance, cette valeur indique si la défaillance s'est produite sur la boîte aux lettres cible ou sur la boîte aux lettres source.</p></td>
</tr>
<tr class="even">
<td><p><code>Message</code></p></td>
<td><p>En cas de défaillance, cette valeur indique le message correspondant. Cette valeur peut également spécifier le commentaire de suspension.</p></td>
</tr>
<tr class="odd">
<td><p><code>FailureTimestamp</code></p></td>
<td><p>Si la demande a échoué, cette valeur spécifie la date et l'heure de l'échec de la demande.</p></td>
</tr>
<tr class="even">
<td><p><code>FailureContext</code></p></td>
<td><p>En cas d'échec de la demande, cette valeur fournit des informations sur l'opération effectuée au moment de l'échec.</p></td>
</tr>
<tr class="odd">
<td><p><code>ValidationMessage</code></p></td>
<td><p>Si la demande n'était pas valide, cette valeur en indique le motif.</p></td>
</tr>
<tr class="even">
<td><p><code>RequestQueue</code></p></td>
<td><p>Indique la base de données dans laquelle MRS enregistre l'état détaillé de la demande.</p></td>
</tr>
<tr class="odd">
<td><p><code>Identity</code></p></td>
<td><p>Indique l'identité de la demande.</p></td>
</tr>
<tr class="even">
<td><p><code>Report</code></p></td>
<td><p>Si vous avez utilisé le paramètre <em>IncludeReport</em>, cette valeur fournit des informations permettant de résoudre des problèmes liés à la demande.</p></td>
</tr>
</tbody>
</table>


## Comment savoir si cela a fonctionné ?

Exécutez la cmdlet **Get-MailboxRestoreRequestStatistics** pour vérifier que vous pouvez afficher les statistiques relatives aux demandes de restauration de boîtes aux lettres. Si la cmdlet renvoie une erreur, vérifiez que vous utilisez l’identité correcte pour la demande de restauration.

## Utiliser l'environnement de ligne de commande pour modifier les propriétés d'une demande de restauration

Si une demande de restauration de boîte aux lettres échoue, utilisez la cmdlet **Set-MailboxRestoreRequest** pour modifier les propriétés de la demande et tenter une récupération après défaillance.

Dans cet exemple, il est spécifié que la demande de restauration MailboxRestore1 pour la boîte aux lettres de Debra Garcia doit ignorer 10 éléments de boîte aux lettres endommagés.

    Set-MailboxRestoreRequest -Identity "Debra Garcia\MailboxRestore1" -BadItemLimit 10

Cet exemple montre que la demande de restauration MailboxRestore1 pour la boîte aux lettres de Florence Flipo ignore 100 éléments endommagés. Puisque la valeur de *BadItemLimit* est supérieure à 50, le paramètre *AcceptLargeDataLoss* doit être spécifié.

    Set-MailboxRestoreRequest -Identity "Florence Flipo\MailboxRestore1" -BadItemLimit 100 -AcceptLargeDataLoss

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, consultez la rubrique [Set-MailboxRestoreRequest](https://technet.microsoft.com/fr-fr/library/ff829909\(v=exchg.150\)).

## Comment savoir si cela a fonctionné ?

Pour vérifier que les propriétés d’une demande de restauration ont été correctement modifiées, exécutez la cmdlet **Get-MailboxRestoreRequestStatistics** afin d’afficher les propriétés révisées pour la demande de restauration. Si la demande de restauration a bien été créée, la valeur de la propriété *Status* doit être `Queued`, `InProgress` ou `Completed`. Une fois la demande de restauration exécutée, le contenu de la boîte aux lettres supprimée (récupérable) doit apparaître dans la boîte aux lettres cible.

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, consultez la rubrique [Get-MailboxRestoreRequestStatistics](https://technet.microsoft.com/fr-fr/library/ff829912\(v=exchg.150\)).

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour interrompre une demande de restauration

Vous pouvez interrompre une demande de restauration à tout moment après avoir créé la demande, mais avant que la demande atteigne l'état `Completed`. Pour la syntaxe de la commande permettant de reprendre la demande de restauration à l'aide de la cmdlet [Resume-MailboxRestoreRequest](https://technet.microsoft.com/fr-fr/library/ff829908\(v=exchg.150\)), consultez la section Reprendre une demande de restauration via l'environnement de ligne de commande Exchange Management Shell plus loin dans cette rubrique .

Dans cet exemple, nous interrompons la demande de restauration MailboxRestore1 de la boîte aux lettres de Pilar Pinilla.

    Suspend-MailboxRestoreRequest -Identity "Pilar Pinilla\MailboxRestore1"

Cet exemple montre comment suspendre toutes les demandes de restauration en cours en extrayant toutes les demandes dont l'état est `InProgress`, puis en canalisant la sortie vers la cmdlet **Suspend-MailboxRestoreRequest** tout en ajoutant le commentaire « Resume after FY13Q2 Maintenance » (Reprendre après la maintenance FY13Q2).

    Get-MailboxRestoreRequest -Status InProgress | Suspend-MailboxRestoreRequest -SuspendComment "Resume after FY13Q2 Maintenance"

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, consultez la rubrique [Suspend-MailboxRestoreRequest](https://technet.microsoft.com/fr-fr/library/ff829906\(v=exchg.150\)).

## Comment savoir si cela a fonctionné ?

Pour vérifier que la suspension d’une demande de restauration de boîte aux lettres s’est correctement effectuée, exécutez la commande suivante :

    Get-MailboxRestoreRequest <identity> | Format-List Suspend,Status

Si la valeur de la propriété *Suspend* est égale à `True`, la demande de restauration a bien été suspendue. De même, une valeur de `Suspended` pour la propriété *Status* indique que la demande de restauration a bien été suspendue.

## Reprendre une demande de restauration via l'environnement de ligne de commande Exchange Management Shell

La cmdlet **Resume-MailboxRestoreRequest** permet de reprendre une demande de restauration ayant échoué ou ayant été suspendue.

Cet exemple montre comment reprendre la demande de restauration Pilar Pinilla\\MailboxRestore1.

    Resume-MailboxRestoreRequest -Identity "Pilar Pinilla\MailboxRestore1"

Cet exemple montre comment reprendre toutes les demandes de restauration dont l'état est Échec.

    Get-MailboxRestoreRequest -Status Failed | Resume-MailboxRestoreRequest

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, consultez la rubrique [Resume-MailboxRestoreRequest](https://technet.microsoft.com/fr-fr/library/ff829908\(v=exchg.150\)).

## Comment savoir si cela a fonctionné ?

Pour vérifier qu'une demande de restauration a bien repris, exécutez la commande suivante.

    Get-MailboxRestoreRequest <identity> | Format-List Suspend,Status

Si la valeur de la propriété *Suspend* est égale à `False`, ce la signifie que la demande de restauration a bien été reprise. De même, une valeur de `InProgress` pour la propriété *Status* indique que la demande de restauration a bien été reprise.

## Supprimer une demande de restauration via l'environnement de ligne de commande Exchange Management Shell

La cmdlet **Remove-MailboxRestoreRequest** vous permet de supprimer des demandes de restauration de boîtes aux lettres. Si vous supprimez une demande de restauration après l’échec de la copie des données de boîte aux lettres vers la boîte aux lettres cible, la boîte aux lettres cible conserve les données copiées.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Comme indiqué précédemment, les demandes de restauration exécutées sont conservées pendant 30 jours par défaut avant leur suppression automatique.</td>
</tr>
</tbody>
</table>


Cet exemple montre comment supprimer la demande de restauration Pilar Pinilla\\MailboxRestore1.

    Remove-MailboxRestoreRequest -Identity "Pilar Pinilla\MailboxRestore1"

Cet exemple supprime toutes les demandes de restauration dont l'état est Terminé (Completed).

    Get-MailboxRestoreRequest -Status Completed | Remove-MailboxRestoreRequest

Cet exemple annule la demande de restauration en utilisant le paramètre *RequestGuid* pour une demande stockée sur MBXDB01. Le jeu de paramètres exigeant les paramètres *RequestGuid* et *RequestQueue* n'est utilisé que pour les besoins de débogage du service de réplication Microsoft. N'utilisez ce jeu que sur instruction du service de support technique Microsoft.

    Remove-MailboxRestoreRequest -RequestQueue MBXDB01 -RequestGuid 25e0eaf2-6cc2-4353-b83e-5cb7b72d441f

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, consultez la rubrique [Remove-MailboxRestoreRequest](https://technet.microsoft.com/fr-fr/library/ff829910\(v=exchg.150\)).

## Comment savoir si cela a fonctionné ?

Pour vérifier que la suppression d’une demande de restauration de boîte aux lettres s’est correctement effectuée, exécutez la commande suivante :

    Get-MailboxRestoreRequest -Identity <identity of removed restore request>

La commande renvoie une erreur indiquant que la demande de restauration n'existe pas.

Vous pouvez également exécuter la cmdlet **Get-MailboxRestoreRequest**. Si une demande de restauration a bien été supprimée, cette dernière figure pas dans les résultats.

