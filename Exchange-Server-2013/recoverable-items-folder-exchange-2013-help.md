---
title: 'Dossier Éléments récupérables: Exchange 2013 Help'
TOCTitle: Dossier Éléments récupérables
ms:assetid: efc48fb4-2ed8-4d05-93af-f3505fbc389d
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Ee364755(v=EXCHG.150)
ms:contentKeyID: 50479530
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Dossier Éléments récupérables

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2016-12-09_

Pour assurer une protection en cas de suppressions accidentelles ou malveillantes et pour faciliter les tâches de détection couramment effectuées avant ou pendant la période de litige ou d’enquête, Microsoft Exchange Server 2013 et Exchange Online utilisent le dossier Éléments récupérables. Le dossier Éléments récupérables remplace la fonctionnalité communément appelée *conteneur de dépôt* dans les versions précédentes d’Exchange. Le dossier Éléments récupérables est utilisé par les fonctionnalités Exchange suivantes :

  - Rétention des éléments supprimés

  - Récupération d’élément unique

  - Blocage local

  - Conservation pour litige

  - Enregistrement d’audit dans les boîtes aux lettres

  - Journalisation du calendrier

**Table des matières**

Terminologie

Dossier Éléments récupérables

  - Rétention des éléments supprimés

  - Récupération d’élément unique

  - Conservation inaltérable et conservation pour litige

  - Protection de page de copie sur écriture et éléments modifiés

Quotas de boîte aux lettres pour les éléments récupérables

## Terminologie

La connaissance des termes suivants vous permettra de comprendre le contenu de cette rubrique.

  - **Supprimer**  
    Décrit lorsqu’un élément est supprimé d’un dossier et placé dans le dossier par défaut Éléments supprimés.

<!-- end list -->

  - **Supprimer définitivement**  
    Décrit lorsqu’un élément est supprimé du dossier par défaut Éléments supprimés et placé dans le dossier Éléments récupérables. Décrit également lorsqu’un utilisateur Microsoft Outlook supprime un élément à l’aide des touches Maj+Suppr., action qui ignore le dossier Éléments supprimés et place l'élément directement dans le dossier Éléments récupérables.

<!-- end list -->

  - **Vidé**  
    Décrit lorsqu’un élément est marqué pour être purgé de la base de données de boîte aux lettres. On appelle également cela une *suppression réversible*.

Retour au début

## Dossier Éléments récupérables

Ce dossier réside dans la sous-arborescence non IPM de toutes les boîtes aux lettres. Cette sous-arborescence non IPM est une zone de stockage au sein de la boîte aux lettres qui contient des données opérationnelles relatives à la boîte en question. Elle n’est pas visible pour les utilisateurs utilisant Outlook, Microsoft OfficeOutlook Web App ou autres clients de messagerie.

Les principaux avantages de cette modification architecturale sont les suivants :

  - Lorsqu’une boîte aux lettres est déplacée dans une autre base de données de boîte aux lettres, le dossier Éléments récupérables est déplacé est même temps.

  - Le dossier Éléments récupérables est indexé à l’aide de Microsoft Exchange Search et peut être découvert en utilisant la découverte électronique sur place.

  - Le dossier Éléments récupérables possède son propre quota de stockage.

  - Exchange peut empêcher la purge des données du dossier Éléments récupérables.

  - Exchange peut suivre les modifications de certains contenus.

Le dossier Éléments récupérables contient les sous-dossiers suivants :

  - **Suppressions**   Ce sous-dossier contient tous les éléments supprimés du dossier Éléments supprimés. (Dans Outlook, un utilisateur peut définitivement supprimer un élément à l’aide des touches Maj+Suppr.) Les utilisateurs peuvent afficher ce sous-dossier via la fonctionnalité Récupérer des éléments supprimés dans Outlook et Outlook Web App.

  - **Versions**   Si la conservation inaltérable ou la conservation pour litige est activée, ce sous-dossier contient les copies originales et modifiées des éléments supprimés. Ce dossier n’est pas accessible aux utilisateurs finals.

  - **Purges**   Si la conservation pour litige ou la récupération d’élément unique est activée, ce sous-dossier contient tous les éléments vidés. Ce dossier n’est pas accessible aux utilisateurs finals.

  - **Audits**   Si l’enregistrement d’audit des boîtes aux lettres est activé pour une boîte aux lettres, ce sous-dossier contient les entrées du journal d’audit. Pour plus d’informations sur les enregistrements d’audit dans les boîtes aux lettres, voir [Enregistrement d’audit dans les boîtes aux lettres](mailbox-audit-logging-exchange-2013-help.md).

  - **DiscoveryHolds**   Si l’archive permanente est activée, ce sous-dossier contient tous les éléments qui satisfont les paramètres de demande de mise en attente et sont vidés.

  - **Journalisation du calendrier**   Ce sous-dossier contient les modifications du calendrier réalisées dans une boîte aux lettres. Les utilisateurs ne peuvent pas accéder à ce dossier.

L’illustration suivante montre les sous-dossiers des dossiers Éléments récupérables. Elle montre également les processus de rétention des éléments supprimés, de récupération d’élément unique et de flux de travail de conservation décrits dans les sections suivantes.

![Dossier Éléments récupérables](images/Ee364755.a1a08afc-3617-4adb-83ab-a6904516954e(EXCHG.150).gif "Dossier Éléments récupérables")

Retour au début

## Rétention des éléments supprimés

Un élément est considéré comme étant supprimé définitivement dans les cas suivants :

  - Un utilisateur supprime un élément ou vide tous les éléments du dossier Éléments supprimés.

  - Un utilisateur appuie sur les touches Maj+Suppr. pour supprimer un élément d’un autre dossier de la boîte aux lettres.

Les éléments supprimés définitivement sont déplacés dans le sous-dossier Suppressions du dossier Éléments récupérables. Cette méthode fournit une couche supplémentaire de protection grâce à laquelle les utilisateurs peuvent récupérer des éléments supprimés définitivement sans avoir à demander l’intervention de l’assistance. Les utilisateurs peuvent utiliser la fonctionnalité Récupérer des éléments supprimés d’Outlook ou d’Outlook Web App pour récupérer un élément supprimé. Les utilisateurs peuvent également utiliser cette fonctionnalité pour supprimer définitivement un élément. Pour plus d’informations, consultez les rubriques suivantes :

  - [Restaurer les éléments supprimés dans Outlook](https://go.microsoft.com/fwlink/p/?linkid=524923)

  - [Récupérer des éléments ou des messages supprimés dans Outlook Web App](https://go.microsoft.com/fwlink/p/?linkid=524924)

Les éléments restent dans le sous-dossier Suppressions jusqu’à la fin de la période de rétention des éléments supprimés. La période de rétention par défaut des éléments supprimés d’une base de données de boîte aux lettres est de 14 jours. Vous pouvez modifier cette période pour une base de données de boîte aux lettres ou pour une boîte aux lettres spécifique. Outre une période de rétention des éléments supprimés, le dossier Éléments récupérables est également soumis à des quotas. Pour plus d’informations, voir Quotas de boîte aux lettres pour les éléments récupérables plus loin dans cette rubrique.

À la fin de la période de rétention des éléments supprimés, l’élément est déplacé dans le dossier Purges et l’utilisateur ne peut plus le voir. Lorsque l’Assistant Dossier géré traite la boîte aux lettres, les éléments du sous-dossier Purges sont vidés de la base de données de boîtes aux lettres et ne peuvent être récupérés.

Retour au début

## Récupération d’élément unique

Si un élément est supprimé du sous-dossier Suppressions, soit par un utilisateur qui purge l’élément à l’aide de la fonctionnalité Récupérer les éléments supprimés ou par un processus automatisé tel que l’Assistant Dossier géré, l’élément ne peut pas être récupéré par l’utilisateur. Dans les précédentes versions d’Exchange, l’administrateur devait restaurer la base de données des boîtes aux lettres ou une boîte aux lettres à partir des copies de sauvegarde pour pouvoir récupérer ces éléments. Ce processus retardait généralement la récupération de quelques minutes voire heures, selon le mécanisme de sauvegarde utilisé.

Dans Exchange 2013, vous pouvez utiliser la *récupération d’élément unique* pour récupérer des éléments sans avoir à restaurer les bases de données de boîte aux lettres à l’aide d’un support de sauvegarde. Cela permet de réduire considérablement les périodes de récupération. Lorsque l’Assistant Dossier géré traite le dossier Éléments récupérables d’une boîte aux lettres pour laquelle la récupération d’élément unique est activée, tout élément du sous-dossier Purges n’est pas purgé si la période de rétention des éléments supprimés de cet élément n’est pas écoulée.

Le tableau suivant dresse la liste des contenus et actions pouvant être exécutées dans le dossier Éléments récupérables si la récupération d’élément unique est activée.

### Dossier Éléments récupérables et récupération d’élément unique

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>État de la récupération d’élément unique</th>
<th>Le dossier Éléments récupérables contient des éléments supprimés définitivement</th>
<th>Le dossier Éléments récupérables contient des éléments vidés</th>
<th>Les utilisateurs peuvent purger des éléments du dossier Éléments récupérables</th>
<th>L’Assistant Dossier géré purge automatiquement les éléments du dossier Éléments récupérables</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Activé</p></td>
<td><p>Oui</p></td>
<td><p>Oui</p></td>
<td><p>Oui. Les utilisateurs peuvent vider les éléments à l’aide de la fonctionnalité Récupérer les éléments supprimés dans Outlook ou Outlook Web App. Toutefois, les éléments vidés ne sont pas définitivement supprimés de la base de données de boîte aux lettres avant l’expiration de la période de rétention des éléments supprimés.</p></td>
<td><p>Oui. Par défaut, tous les éléments sont purgés passé un délai de 14 jours, à l’exception des éléments de calendrier qui sont purgés au bout de 31 jours.</p></td>
</tr>
<tr class="even">
<td><p>Désactivé</p></td>
<td><p>Oui</p></td>
<td><p>Non</p></td>
<td><p>Oui. Dans ce cas, les éléments vidés sont marqués pour être définitivement supprimés de la base de données de boîte aux lettres et ne peuvent pas être récupérés.</p></td>
<td><p>Oui. Par défaut, tous les éléments sont purgés passé un délai de 14 jours, à l’exception des éléments de calendrier qui sont purgés au bout de 31 jours. Si le quota d’avertissement des éléments récupérables est atteint avant la fin de la période de rétention des éléments supprimés, les messages sont supprimés dans l’ordre d’arrivée.</p></td>
</tr>
</tbody>
</table>


Dans Exchange 2013, la récupération d’élément unique n’est pas activée par défaut pour les nouvelles boîtes aux lettres ou les boîtes aux lettres déplacées à partir d’une version précédente d’Exchange. Vous devez utiliser l’environnement de ligne de commande Exchange Management Shell pour activer la récupération d’élément unique d’une boîte aux lettres, puis configurer ou modifier la période de rétention des éléments supprimés. Pour plus d’informations sur comment effectuer la récupération d’un élément unique, consultez la rubrique [Récupérer des messages supprimés dans la boîte aux lettres d’un utilisateur](recover-deleted-messages-in-a-user-s-mailbox-exchange-2013-help.md).

Retour au début

## Conservation inaltérable et conservation pour litige

Dans Exchange 2013 et Exchange Online, les gestionnaires de découverte peuvent utiliser la découverte électronique sur place avec autorisations [Gestion de la détection](discovery-management-exchange-2013-help.md) déléguées pour réaliser des recherches de découverte électroniques dans le contenu des boîtes aux lettres. Exchange 2013 et Exchange Online ont également introduit l’archive permanente, que vous pouvez utiliser pour conserver les éléments de boîte aux lettres qui correspondent aux paramètres de demande et protègent les éléments contre la suppression par les utilisateurs ou les processus automatisés. Vous pouvez également utiliser la conservation pour litige pour préserver tous les éléments des boîtes aux lettres des utilisateurs et protéger les éléments contre la suppression par les utilisateurs ou les processus automatisés.

Lorsque vous placez une boîte aux lettres en conservation pour litige ou inaltérable, l’Assistant Dossier géré arrête de purger automatiquement les messages des sous-dossiers Purges et DiscoveryHolds. Par ailleurs, la protection de page de copie sur écriture est également activée pour la boîte aux lettres. Cette fonctionnalité crée une copie de l’élément original avant que des modifications ne soient écrites dans la banque Exchange. Une fois que la boîte aux lettres ne fait plus l’objet d’une conservation, l’Assistant Dossier géré reprend la purge automatique.

Le tableau suivant dresse la liste des contenus et des actions pouvant être exécutées dans le dossier Éléments récupérables si la conservation pour litige est activée.

### Dossier Éléments récupérables et mises en attente

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>État de mise en attente</th>
<th>Le dossier Éléments récupérables contient les éléments supprimés définitivement</th>
<th>Le dossier Éléments récupérables contient des éléments modifiés et vidés</th>
<th>Les utilisateurs peuvent purger des éléments du dossier Éléments récupérables</th>
<th>L’Assistant Dossier géré purge automatiquement les éléments du dossier Éléments récupérables</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Activé</p></td>
<td><p>Oui</p></td>
<td><p>Oui</p></td>
<td><p>Oui. Les utilisateurs peuvent vider les éléments à l’aide de la fonctionnalité Récupérer les éléments supprimés dans Outlook ou Outlook Web App. Toutefois, l’Assistant Dossier géré ne les supprime pas définitivement de la base de données de boîte aux lettres si la boîte aux lettres est en attente.</p></td>
<td><p>Non</p></td>
</tr>
<tr class="even">
<td><p>Désactivé</p></td>
<td><p>Oui</p></td>
<td><p>Non</p></td>
<td><p>Oui</p></td>
<td><p>Oui</p></td>
</tr>
</tbody>
</table>


Pour plus d’informations sur la découverte électronique inaltérable, la conservation inaltérable et la conservation pour litige, consultez les rubriques suivantes :

  - [Découverte électronique locale](in-place-ediscovery-exchange-2013-help.md)

  - [Conservation inaltérable et conservation pour litige](in-place-hold-and-litigation-hold-exchange-2013-help.md)

Retour au début

## Protection de page de copie sur écriture et éléments modifiés

Si un utilisateur avec conservation inaltérable ou conservation pour litige modifie des propriétés spécifiques d’un élément de boîte aux lettres, une copie de l’élément de boîte aux lettres original est créée avant l’écriture de l’élément modifié. La copie d’origine est enregistrée dans le sous-dossier Versions. Ce processus est également appelé *protection de page de copie sur écriture*. La protection de page de copie sur écriture s’applique aux éléments résidant dans n’importe quel dossier de boîte aux lettres. Les utilisateurs ne peuvent pas voir le sous-dossier Versions.

Le tableau suivant dresse la liste des propriétés de message qui déclenchent une opération de protection de page de copie sur écriture.

### Propriétés qui déclenchent la protection de page de copie sur écriture

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Type d’élément</th>
<th>Propriétés qui déclenchent la protection de page de copie sur écriture</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Messages (IPM.Note*)</p>
<p>Publications (IPM.Post*)</p></td>
<td><ul>
<li><p>Objet</p></li>
<li><p>Body</p></li>
<li><p>Pièces jointes</p></li>
<li><p>Expéditeurs et destinataires</p></li>
<li><p>Dates d'envoi et de réception</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Éléments autres que les messages et les publications</p></td>
<td><p>Toute modification apportée à une propriété visible, à l’exception des éléments suivants :</p>
<ul>
<li><p>Emplacement d’un élément (lorsqu’un élément fait l’objet de déplacements entre des dossiers)</p></li>
<li><p>Modification de l’état d’un élément (lu ou non lu)</p></li>
<li><p>Modifications apportées à la balise de rétention appliquée à un élément</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Éléments du dossier par défaut Brouillons</p></td>
<td><p>Aucun. La protection de page de copie sur écriture ne s’applique pas aux éléments du dossier Brouillons.</p></td>
</tr>
</tbody>
</table>


<table>
<thead>
<tr class="header">
<th><img src="images/JJ159813.important(EXCHG.150).gif" title="Important" alt="Important" />Important :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>La protection de page de copie sur écriture n’enregistre pas de version de la réunion lorsque l’organisateur d’une réunion reçoit des réponses des participants et que les informations de suivi de la réunion sont mises jour. En outre, les changements apportés aux flux RSS ne sont pas pris en compte par la protection de page de copie sur écriture.</td>
</tr>
</tbody>
</table>


Lorsqu’une boîte aux lettres n’est plus bloquée sur place ou mise en attente pour litige, les copies des éléments modifiés enregistrées dans le dossier Versions sont supprimées.

Retour au début

## Quotas de boîte aux lettres pour les éléments récupérables

Lorsqu’un élément est déplacé dans le dossier Éléments récupérables, sa taille est déduite du quota de la boîte aux lettres et ajoutée à la taille du dossier Éléments récupérables. Dans Exchange 2013, les bases de données de boîtes aux lettres ont un quota d’avertissement des éléments récupérables configurable (*limite logicielle*) de 20 Go et un quota d’éléments récupérables (*limite matérielle*) de 30 Go. Par défaut, ces limites sont héritées par toutes les boîtes aux lettres de la base de données. Cependant, vous pouvez configurer des boîtes aux lettres individuelles avec des quotas différents. Pour en savoir plus, consultez la rubrique [Configurer la rétention des éléments supprimés et les quotas d’éléments récupérables](configure-deleted-item-retention-and-recoverable-items-quotas-exchange-2013-help.md).

Dans Exchange Online, les limites par défaut pour le quota d’éléments récupérables sont les mêmes que dans Exchange 2013 ; une limite logicielle de 20 Go et une limite matérielle de 30 Go. Toutefois, les quotas pour le dossier Éléments récupérables sont automatiquement augmentés à 90 et 100 Go, respectivement, lorsque vous placez une boîte aux lettres en conservation pour litige ou en conservation inaltérable.

Lorsque le dossier Éléments récupérables d’une boîte aux lettres atteint le quota des éléments récupérables, aucun élément supplémentaire ne peut être stocké dans le dossier. Cela impacte la fonctionnalité de boîte aux lettres des façons suivantes :

  - Les utilisateurs de boîte aux lettres ne peuvent pas supprimer des éléments.

  - L’Assistant Dossier géré ne peut pas supprimer des éléments en fonction de la balise de rétention ou des paramètres de dossiers gérés.

  - Pour les boîtes aux lettres pour lesquelles la récupération d’élément unique, la conservation inaltérable ou la conservation pour litige est activée, le processus de protection de page de copie sur écriture ne peut pas conserver les versions des éléments modifiés par l’utilisateur.

  - Pour les boîtes aux lettres pour lesquelles l’enregistrement d’audit des boîtes aux lettres est activé, aucune entrée d’audit de boîtes aux lettres ne peut être enregistrée dans le sous-dossier Audits.

Pour les boîtes aux lettres sans conservation inaltérable ou conservation pour litige, l’Assistant Dossier géré purge automatiquement les éléments du dossier Éléments récupérables à la fin de la période de rétention des éléments supprimés. Si le dossier atteint le quota d’avertissement des éléments récupérables, l’assistant purge automatiquement les éléments dans l’ordre d’arrivée.

Lorsque le dossier Éléments récupérables atteint les limites logicielle et matérielle par défaut, vous êtes notifié au moyen d’un journal des événements et d’une alerte Microsoft System Center Operations Manager. Cette alerte ne fonctionne que lorsque le dossier Éléments récupérables atteint une première fois les limites logicielle et matérielle par défaut, puis une fois par jour par la suite.

Le tableau suivant dresse la liste des événements journalisés lorsque le dossier Éléments récupérables atteint les limites logicielle et matérielle par défaut.

### Erreurs et avertissements de quota des éléments récupérables

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>ID d’évènement</th>
<th>Type</th>
<th>Source</th>
<th>Message</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>10024</p></td>
<td><p>Avertissement</p></td>
<td><p>MSExchangeIS Mailbox Store</p></td>
<td><p>La boîte aux lettres pour &lt;<em>utilisateur de boîte aux lettres</em>&gt; (<em>GUID</em>) a dépassé le quota d’avertissement des éléments récupérables. Veuillez supprimer des éléments du dossier Éléments récupérables ou augmenter le quota d’avertissements des éléments récupérables et le quota des éléments récupérables. En cas de dépassement du quota des éléments récupérables, l’utilisateur ne pourra pas supprimer d’éléments de la boîte aux lettres.</p></td>
</tr>
<tr class="even">
<td><p>10023</p></td>
<td><p>Erreur</p></td>
<td><p>MSExchangeIS Mailbox Store</p></td>
<td><p>La boîte aux lettres pour &lt;<em>utilisateur de boîte aux lettres</em>&gt; (<em>GUID</em>) a dépassé le quota maximal des éléments récupérables. Les éléments ne peuvent pas être supprimés de cette boîte aux lettres. Le propriétaire de la boîte aux lettres devrait être informé de la situation de la boîte aux lettres dès que possible. Veuillez supprimer des éléments du dossier Éléments récupérables ou augmenter le quota des éléments récupérables pour restaurer les fonctionnalités.</p></td>
</tr>
<tr class="odd">
<td><p>10023</p></td>
<td><p>Avertissement</p></td>
<td><p>MSExchangeMailboxAssistants</p></td>
<td><p>La taille des éléments récupérables de la boîte aux lettres &lt;<em>utilisateur de boîte aux lettres</em>&gt; a dépassé la limite de quota d’avertissement. Les éléments ont été supprimés des dossiers Éléments récupérables pour éviter une défaillance de la boîte aux lettres. Quota d’avertissement des éléments récupérables : 20 Go (21,474,836,480 octets) taille d’origine des éléments récupérables : 21475005311 taille actuelle des éléments récupérables : 21474823820 Statistiques du dossier : - Dossiers traités : RecoverableItemsRoot, RecoverableItemsVersions, RecoverableItemsPurges, RecoverableItemsDeletions - tailles d’origine des dossiers : 21391661934, 55190914, 1987247, 26157788 (nombres d’éléments : 276828, 400, 84, 646) - tailles actuelles des dossiers : 21391480443, 55190914, 1987247, 26157788 (nombres d’éléments : 276817, 400, 84, 646)</p></td>
</tr>
</tbody>
</table>


Si la boîte aux lettres est en conservation inaltérable ou en conservation pour litige, la protection de page de copie sur écriture ne peut pas conserver les versions des éléments modifiés. Pour conserver des versions des éléments modifiés, vous devez réduire la taille du dossier Éléments récupérables. La cmdlet [Search-Mailbox](https://technet.microsoft.com/fr-fr/library/dd298173\(v=exchg.150\)) permet de copier des messages du dossier Éléments récupérables depuis une boîte aux lettres vers une boîte aux lettres de découverte, puis de supprimer les éléments de la boîte aux lettres. Vous pouvez également augmenter le quota des éléments récupérables de la boîte aux lettres. Pour plus d’informations, consultez la rubrique [Nettoyer le dossier Éléments récupérables](clean-up-the-recoverable-items-folder-exchange-2013-help.md).

Retour au début

## Plus d’informations

  - La copie sur écriture est activée uniquement lorsqu’une boîte aux lettres est en conservation inaltérable ou en conservation pour litige.

  - Si les utilisateurs ont besoin de récupérer des éléments supprimés du dossier Éléments récupérables, dirigez-les vers les rubriques suivantes :
    
      - [Restaurer les éléments supprimés dans Outlook](https://go.microsoft.com/fwlink/p/?linkid=524923)
    
      - [Récupérer des éléments ou des messages supprimés dans Outlook Web App](https://go.microsoft.com/fwlink/p/?linkid=524924)

Retour au début

