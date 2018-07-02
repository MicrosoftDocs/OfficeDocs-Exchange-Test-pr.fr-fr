---
title: 'Configurer l’Assistant Dossier géré: Exchange 2013 Help'
TOCTitle: Configurer l’Assistant Dossier géré
ms:assetid: 9fcfb9b6-bd24-4218-a163-bc599cd5476a
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb123958(v=EXCHG.150)
ms:contentKeyID: 50478920
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurer l’Assistant Dossier géré

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2014-10-01_

L'*Assistant Dossier géré* est un Assistant de boîte aux lettres MicrosoftExchange qui applique les paramètres de rétention de messages configurés dans les stratégies de rétention.

Pour les autres tâches de gestion relatives à la gestion des enregistrements de messagerie (MRM), voir [Procédures de gestion des enregistrements de messagerie](messaging-records-management-procedures-exchange-2013-help.md).

## Ce qu’il faut savoir avant de commencer ?

  - Durée d'exécution : 1 minute.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l'entrée « Gestion des enregistrements de messagerie » à la rubrique [Stratégie de messagerie et autorisations de conformité](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

  - Vous ne pouvez pas utiliser le Centre d’administration Exchange pour configurer l'Assistant Dossier géré. Vous devez utiliser l’environnement de ligne de commande Exchange Management Shell

  - Dans Exchange 2013, l’Assistant Dossier géré est un assistant basé sur la limitation. Ces types d’assistant sont continuellement exécutés et n’ont pas besoin d’être planifiés. Les ressources système qu’ils peuvent consommer sont limitées. Vous pouvez configurer l’Assistant Dossier géré pour traiter toutes les boîtes aux lettres sur un serveur de boîtes aux lettres dans une certaine période (appelée *cycle de travail)*. Le cycle de travail est défini sur un jour par défaut.

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

## Utiliser l'environnement de ligne de commande pour configurer l'Assistant Dossier géré

Dans cet exemple, on configure l’Assistant Dossier géré pour traiter toutes les boîtes aux lettres en une journée.

    Set-MailboxServer MyMailboxServer -ManagedFolderWorkCycle 1

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Set-MailboxServer](https://technet.microsoft.com/fr-fr/library/aa998651\(v=exchg.150\)).

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez correctement configuré l'Assistant Dossier géré, utilisez la cmdlet [Get-MailboxServer](https://technet.microsoft.com/fr-fr/library/bb123539\(v=exchg.150\)) pour vérifier le paramètre *ManagedFolderWorkCycle*.

Cette commande récupère tous les serveurs de boîtes aux lettres de l'organisation et affiche les propriétés du cycle de travail de l'Assistant Dossier géré de chaque serveur dans un tableau. Le commutateur *Auto* permet d'ajuster automatiquement la largeur de colonne.

    Get-MailboxServer | Format-Table Name,ManagedFolderWorkCycle* -Auto

## Utiliser l'environnement de ligne de commande pour démarrer l'Assistant Dossier géré

Cet exemple déclenche l’Assistant Dossier géré pour traiter immédiatement la boîte aux lettres de Morris Cornejo.

    Start-ManagedFolderAssistant -Identity morris.cornejo@contoso.com

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Start-ManagedFolderAssistant](https://technet.microsoft.com/fr-fr/library/aa998864\(v=exchg.150\)).

