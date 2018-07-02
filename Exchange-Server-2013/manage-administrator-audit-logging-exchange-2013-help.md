---
title: 'Gestion de la journalisation d’audit de l’administrateur: Exchange 2013 Help'
TOCTitle: Gestion de la journalisation d’audit de l’administrateur
ms:assetid: 15c284c0-b8e6-42ca-9913-7c59fdb6885d
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dd335109(v=EXCHG.150)
ms:contentKeyID: 50555350
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Gestion de la journalisation d’audit de l’administrateur

 

_**Sapplique à :**Exchange Server 2013_

_**Dernière rubrique modifiée :**2013-05-17_

La connexion au service d'audit administrateur dans Microsoft Exchange Server 2013 vous permet de créer une entrée de journal chaque fois qu'une cmdlet est exécutée. Les entrées de journal vous fournissent des informations sur la cmdlet qui a été exécutée, les paramètres utilisés, l'utilisateur qui a exécuté la cmdlet et les objets concernés. Pour plus d'informations sur l'enregistrement dans des journaux d'audit de l'administrateur, consultez la rubrique [Connexion au service d’audit administrateur](administrator-audit-logging-exchange-2013-help.md).

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée de chaque procédure : moins de 5 minutes

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Connexion au service d'audit administrateur » dans la rubrique [Autorisations d’infrastructure Exchange et Shell](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md).

  - La connexion au service d'audit administrateur s'appuie sur la réplication Active Directory pour répliquer les paramètres de configuration que vous spécifiez pour les contrôleurs de domaine de votre organisation. Selon vos paramètres de réplication, les modifications que vous apportez ne prendront peut-être pas immédiatement effet sur l'ensemble des serveurs Exchange 2013 de votre organisation.

  - Les modifications apportées à la configuration de l'enregistrement d'audit sont actualisées toutes les 60 minutes sur les ordinateurs ayant l'environnement de ligne de commande Exchange Management Shell ouvert au moment de la modification de la configuration. Si vous souhaitez appliquer les modifications immédiatement, fermez et rouvrez l'environnement de ligne de commande Exchange Management Shell sur chaque ordinateur.

  - 15 minutes peuvent être nécessaires pour qu'une commande apparaisse dans les résultats de la recherche du journal d'audit après son exécution, car les entrées du journal d'audit doivent être indexées avant que ces dernières ne puissent faire l'objet d'une recherche. Si une commande n'apparaît pas dans le journal d'audit de l'administrateur, patientez quelques minutes, puis réeffectuez la recherche.

  - Vous devez utiliser l'environnement de ligne de commande Exchange Management Shell pour effectuer ces procédures.

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

## Spécifier les cmdlets à auditer

Par défaut, la connexion au service d'audit crée une entrée de journal pour chaque cmdlet exécutée. Si vous activez la connexion au service d'audit pour la première fois et que ce comportement vous convient, il n'est pas nécessaire de changer la liste d'audit de cmdlet. Si vous avez indiqué préalablement les cmdlets à auditer et que vous souhaitez maintenant toutes les auditer, vous pouvez le faire en indiquant le caractère générique astérisque (\*) avec le paramètre *AdminAuditLogCmdlets* de la cmdlet **Set-AdminAuditLogConfig**, comme illustré dans la commande suivante :

    Set-AdminAuditLogConfig -AdminAuditLogCmdlets *

Vous pouvez désigner les cmdlets à auditer en fournissant une liste de cmdlets à l'aide du paramètre *AdminAuditLogCmdlets*. Dans cette liste, vous pouvez fournir des cmdlets uniques, des cmdlets avec le caractère générique astérisque (\*) ou un mélange des deux. Chaque entrée dans la liste est séparée par des virgules. Les valeurs suivantes sont toutes valides :

  - `New-Mailbox`

  - `*TransportRule`

  - `*Management*`

  - `Set-Transport*`

Cet exemple audite les cmdlets spécifiées dans la liste précédente.

    Set-AdminAuditLogConfig -AdminAuditLogCmdlets New-Mailbox, *TransportRule, *Management*, Set-Transport*

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, consultez la rubrique [Set-AdminAuditLogConfig](https://technet.microsoft.com/fr-fr/library/dd298169\(v=exchg.150\)).

## Spécifier les paramètres à auditer

Par défaut, la connexion au service d'audit crée une entrée de journal pour chaque cmdlet exécutée, quels que soient les paramètres spécifiés. Si vous activez la connexion au service d'audit pour la première fois et que ce comportement vous convient, il n'est pas nécessaire de changer la liste d'audit des paramètres. Si vous avez indiqué préalablement les paramètres à auditer et que vous souhaitez maintenant tous les auditer, vous pouvez le faire en indiquant le caractère générique astérisque (\*) avec le paramètre *AdminAuditLogParameters* de la cmdlet **Set-AdminAuditLogConfig**, comme illustré dans la commande suivante :

    Set-AdminAuditLogConfig -AdminAuditLogParameters *

Vous pouvez indiquer les paramètres que vous souhaitez auditer en utilisant le paramètre *AdminAuditLogParameters*. Dans la liste des paramètres à auditer, vous pouvez fournir des paramètres uniques, des paramètres avec le caractère générique astérisque (\*) ou un mélange des deux. Chaque entrée dans la liste est séparée par des virgules. Les valeurs suivantes sont toutes valides :

  - `Database`

  - `*Address*`

  - `Custom*`

  - `*Region`

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Pour la création d'une entrée de journal d'audit lors de l'exécution d'une commande, cette dernière doit inclure au moins un ou plusieurs paramètres qui existent sur au moins une ou plusieurs cmdlets spécifiées avec le paramètre <em>AdminAuditLogCmdlets</em>.</td>
</tr>
</tbody>
</table>


Cet exemple audite les paramètres spécifiés dans la liste précédente.

    Set-AdminAuditLogConfig -AdminAuditLogParameters Database, *Address*, Custom*, *Region

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, consultez la rubrique [Set-AdminAuditLogConfig](https://technet.microsoft.com/fr-fr/library/dd298169\(v=exchg.150\)).

## Spécifier la durée de vie du journal d'audit

La durée de vie du journal d'audit détermine la durée de conservation des entrées du journal. Lorsqu'une entrée dépasse la durée de vie définie, elle est supprimée. La valeur par défaut est 90 jours.

Vous pouvez spécifier le nombre de jours, d'heures, de minutes et de secondes pendant lesquels les entrées du journal d'audit doivent être conservées. Pour spécifier une valeur, utilisez le format jj.hh.mm:ss :

  - **jj**   Nombre de jours de conservation de l'entrée du journal d'audit

  - **hh**   Nombre d'heures de conservation de l'entrée de journal d'audit

  - **mm**   Nombre de minutes de conservation de l'entrée du journal d'audit

  - **ss**   Nombre de secondes de conservation de l'entrée du journal d'audit

<table>
<thead>
<tr class="header">
<th><img src="images/JJ673034.Caution(EXCHG.150).gif" title="Attention" alt="Attention" />Attention :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Vous pouvez définir une durée de vie du journal d'audit inférieure à la durée de vie actuellement paramétrée. Dans ce cas, seront supprimées toutes les entrées du journal d'audit dont la durée de vie dépasse la nouvelle durée fixée.<br />
Si vous définissez la durée de vie sur 0, Exchange supprimera toutes les entrées dans le journal d'audit.<br />
Nous vous recommandons d'accorder les autorisations de configuration de la durée de vie du journal d'audit uniquement à des utilisateurs en qui vous avez toute confiance.</td>
</tr>
</tbody>
</table>


Cet exemple spécifie une durée de vie de deux ans et six mois.

    Set-AdminAuditLogConfig -AdminAuditLogAgeLimit 913.00:00:00

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, consultez la rubrique [Set-AdminAuditLogConfig](https://technet.microsoft.com/fr-fr/library/dd298169\(v=exchg.150\)).

## Activer ou désactiver l'enregistrement des cmdlets de test

Les cmdlets qui commencent par le verbe **Test** ne sont pas enregistrées par défaut. parce que ces cmdlets de **Test** peuvent générer une quantité importante de données en peu de temps. Activez uniquement l'enregistrement des cmdlets de **Test** pour de courtes périodes.

Cette commande active l'enregistrement des cmdlets de **Test**.

    Set-AdminAuditLogConfig -TestCmdletLoggingEnabled $True

Cette commande désactive l'enregistrement des cmdlets de **Test**.

    Set-AdminAuditLogConfig -TestCmdletLoggingEnabled $False

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, consultez la rubrique [Set-AdminAuditLogConfig](https://technet.microsoft.com/fr-fr/library/dd298169\(v=exchg.150\)).

## Désactivation de la journalisation d'audit de l'administrateur

Pour désactiver la journalisation d'audit de l'administrateur, exécutez la commande suivante :

    Set-AdminAuditLogConfig -AdminAuditLogEnabled $False

## Activer l'enregistrement d'audit administrateur

Pour activer la journalisation d'audit de l'administrateur, exécutez la commande suivante :

    Set-AdminAuditLogConfig -AdminAuditLogEnabled $True

## Affichage des paramètres de journalisation d'audit de l'administrateur

Pour afficher les paramètres de journalisation d'audit de l'administrateur que vous avez configurés pour votre organisation, exécutez la commande suivante :

    Get-AdminAuditLogConfig

