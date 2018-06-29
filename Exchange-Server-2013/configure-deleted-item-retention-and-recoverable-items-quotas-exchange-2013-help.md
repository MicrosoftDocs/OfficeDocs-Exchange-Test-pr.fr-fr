---
title: 'Configurer la rétention des éléments supprimés et les quotas d’éléments récupérables: Exchange 2013 Help'
TOCTitle: Configurer la rétention des éléments supprimés et les quotas d’éléments récupérables
ms:assetid: de7d667a-1c93-4364-a4f9-2aa5e3678b12
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Ee364752(v=EXCHG.150)
ms:contentKeyID: 50555506
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configurer la rétention des éléments supprimés et les quotas d’éléments récupérables

 

_**Sapplique à :**Exchange Server 2013_

_**Dernière rubrique modifiée :**2016-12-09_

Lorsqu’un utilisateur supprime des éléments du dossier par défaut Éléments supprimés à l’aide des touches Suppr., Maj+Suppr. ou de l’action **Vider le dossier Éléments supprimés**, les éléments sont déplacés vers le dossier **Éléments récupérables/Suppressions**. La durée pendant laquelle les éléments supprimés sont conservés dans ce dossier est basée sur les paramètres de rétention des éléments supprimés configurés pour la base de données de boîtes aux lettres ou la boîte aux lettres. Par défaut, une base de données de boîtes aux lettres est configurée pour conserver des éléments supprimés pendant 14 jours. Le quota d’avertissements des éléments récupérables et le quota d’éléments récupérables sont respectivement définis à 20 Go et 30 Go.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Avant l’expiration du délai de rétention des éléments supprimés, les utilisateurs de Microsoft Outlook et Microsoft Office Outlook Web App peuvent récupérer les éléments supprimés à l’aide de la fonctionnalité Récupérer les éléments supprimés. Pour en savoir plus sur ces fonctionnalités, consultez la rubrique « Restaurer les éléments supprimés » pour <a href="https://go.microsoft.com/fwlink/p/?linkid=198206">Outlook</a> ou <a href="https://go.microsoft.com/fwlink/p/?linkid=198207">Outlook Web App</a>.</td>
</tr>
</tbody>
</table>


L’environnement de ligne de commande Exchange Management Shell vous permet de configurer des paramètres de rétention des éléments supprimés et des quotas d’éléments récupérables pour une boîte aux lettres ou une base de données de boîtes aux lettres. Les paramètres de rétention des éléments supprimés sont ignorés si l’état d’une boîte aux lettres est défini à « blocage sur place » ou « suspension pour litige ».

Pour plus d’informations sur la rétention des éléments supprimés, le dossier Éléments récupérables, le blocage sur place et la suspension pour litige, consultez [Dossier Éléments récupérables](recoverable-items-folder-exchange-2013-help.md).

## Ce qu’il faut savoir avant de commencer ?

  - Durée d’exécution estimée : 5 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Gestion des enregistrements de messagerie » dans la rubrique [Stratégie de messagerie et autorisations de conformité](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

<table>
<thead>
<tr class="header">
<th><img src="images/Bb125224.tip(EXCHG.150).gif" title="Conseil" alt="Conseil" />Conseil :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.</td>
</tr>
</tbody>
</table>


## Que souhaitez-vous faire ?

## Configurer la rétention d’éléments supprimés pour une boite aux lettres

**Utiliser le Centre d’administration Exchange pour configurer la rétention des éléments supprimés pour une boîte aux lettres**

1.  Accédez à **Destinataires**\>**Boîtes aux lettres**.

2.  Dans l’affichage de liste, sélectionnez une boîte aux lettres, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

3.  Dans la page des propriétés de boîte aux lettres, cliquez sur **Utilisation des boîtes aux lettres**, cliquez sur **Plus d’options**, puis sélectionnez l’une des options suivantes
    
      - **Utiliser les paramètres de rétention par défaut de la base de données de boîtes aux lettres**   Ce paramètre permet d’utiliser le paramètre de rétention des éléments supprimés configuré pour la base de données de boîtes aux lettres.
    
      - **Personnaliser les paramètres de cette boîte aux lettres**   Utilisez ce paramètre pour configurer des paramètres de rétention d’éléments supprimés pour la boîte aux lettres.
        
        **Conserver les éléments supprimés pendant (jours)**   Ce champ affiche la durée pendant laquelle les éléments supprimés sont conservés avant leur suppression définitive sans récupération possible par l’utilisateur. Lors de la création de la boîte aux lettres, cette valeur est basée sur les paramètres de rétention des articles supprimés configurés pour la base de données de la boîte aux lettres. Par défaut, une base de données de boîtes aux lettres est configurée pour conserver les éléments supprimés pendant 14 jours. La plage de valeurs de cette propriété s’étend de 0 à 24 855 jours.
    
      - **Ne pas supprimer définitivement les éléments tant que la base de données n’a pas été sauvegardée**   Activez cette case à cocher pour empêcher la suppression des éléments jusqu’à la sauvegarde de la base de données de boîtes aux lettres sur laquelle la boîte aux lettres est située.

**Utiliser l’environnement de ligne de commande Exchange Management Shell pour configurer la rétention des éléments supprimés d’une boîte aux lettres**

Cet exemple illustre la configuration de la boîte aux lettres d’April Stewart pour conserver les éléments supprimés pendant 30 jours.

    Set-Mailbox -Identity - "April Stewart" -RetainDeletedItemsFor 30

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, consultez la rubrique [Set-Mailbox](https://technet.microsoft.com/fr-fr/library/bb123981\(v=exchg.150\)).

## Utiliser l’environnement de ligne de commande Exchange Management Shell pour configurer les quotas des éléments récupérables pour une boîte aux lettres

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Vous ne pouvez pas utiliser le Centre d’administration Exchange pour configurer les quotas d’éléments récupérables pour une boîte aux lettres.</td>
</tr>
</tbody>
</table>


Cet exemple illustre la configuration d’un quota d’avertissement des éléments récupérables de 12 Go et d’un quota d’éléments récupérables de 15 Go pour la boîte aux lettres d’April Stewart.

    Set-Mailbox -Identity "April Stewart" -RecoverableItemsWarningQuota 12GB -RecoverableItemsQuota 15GB -UseDatabaseQuotaDefaults $false

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Pour configurer une boîte aux lettres pour qu’elle utilise des quotas d’éléments récupérables différents de la base de données de boîtes aux lettres dans laquelle elle réside, vous devez définir le paramètre <em>UseDatabaseQuotaDefaults</em> à <code>$false</code>.</td>
</tr>
</tbody>
</table>


Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Set-Mailbox](https://technet.microsoft.com/fr-fr/library/bb123981\(v=exchg.150\)).

## Utiliser l’environnement de ligne de commande Exchange Management Shell pour configurer la rétention des éléments supprimés d’une base de données de boîtes aux lettres

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Vous ne pouvez pas utiliser le Centre d’administration Exchange pour configurer une rétention d’éléments supprimés pour une boîte aux lettres.</td>
</tr>
</tbody>
</table>


Cet exemple configure une période de rétention d’éléments supprimés de 10 jours pour la base de données de boîtes aux lettres MDB2.

    Set-MailboxDatabase -Identity MDB2 -DeletedItemRetention 10

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, consultez la rubrique [Set-MailboxDatabase](https://technet.microsoft.com/fr-fr/library/bb123971\(v=exchg.150\)).

## Utiliser l’environnement de ligne de commande Exchange Management Shell pour configurer des quotas d’éléments récupérables pour une base de données de boîtes aux lettres

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Vous ne pouvez pas utiliser le Centre d’administration Exchange pour configurer des quotas d’éléments récupérables pour une base de données de boîtes aux lettres</td>
</tr>
</tbody>
</table>


Cet exemple illustre la configuration d’un quota d’avertissements des éléments récupérables de 15 Go et d’un quota d’éléments récupérables de 20 Go sur la base de données de boîtes aux lettres MDB2.

    Set-MailboxDatabase -Identity MDB2 -RecoverableItemsWarningQuota 15GB -RecoverableItemsQuota 20GB

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Set-MailboxDatabase](https://technet.microsoft.com/fr-fr/library/bb123971\(v=exchg.150\)).

