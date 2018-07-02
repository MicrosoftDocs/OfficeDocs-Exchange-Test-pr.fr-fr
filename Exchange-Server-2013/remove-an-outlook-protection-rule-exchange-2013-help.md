---
title: 'Supprimer une règle de protection Outlook: Exchange 2013 Help'
TOCTitle: Supprimer une règle de protection Outlook
ms:assetid: 569fc3be-b269-43f5-8797-73ab0691e685
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Ee633467(v=EXCHG.150)
ms:contentKeyID: 50478233
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Supprimer une règle de protection Outlook

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2016-12-09_

À l'aide des règles de protection Microsoft Outlook, vous pouvez protéger des messages avec la Gestion des droits relatif à l'information (IRM) en appliquant un modèle de [Services AD RMS (Active Directory Rights Management Services)](https://technet.microsoft.com/fr-fr/library/hh831364.aspx) dans Outlook 2010 avant l'envoi des messages. Pour empêcher l'application d'une règle de protection Outlook, vous pouvez désactiver la règle. La suppression d'une règle de protection Outlook supprime la définition de la règle de Active Directory.

Si vous souhaitez rechercher des tâches de gestion supplémentaires relatives à IRM, consultez [Procédures de gestion des droits relatifs à l’information](information-rights-management-procedures-exchange-2013-help.md).

## Ce qu’il faut savoir avant de commencer ?

  - Durée d’exécution estimée : 1 minute.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l’entrée « Protection des droits » dans la rubrique [Stratégie de messagerie et autorisations de conformité](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

  - Vous ne pouvez pas utiliser le Centre d’administration Exchange (EAC) pour supprimer les règles de protection Outlook. Vous devez utiliser l'environnement de ligne de commande Exchange Management Shell.

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

## Utilisation de l’environnement de ligne de commande Exchange Management Shell pour supprimer une règle de protection Outlook

Cet exemple supprime la règle de protection Outlook OPR-DG-Finance.

    Remove-OutlookProtectionRule -Identity "OPR-DG-Finance"

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Remove-OutlookProtectionRule](https://technet.microsoft.com/fr-fr/library/dd297961\(v=exchg.150\)).

## Utilisation de l’environnement de ligne de commande Exchange Management Shell pour supprimer toutes les règles de protection Outlook

Cet exemple supprime toutes les règles de protection Outlook dans l’organisation Exchange.

    Get-OutlookProtectionRule | Remove-OutlookProtectionRule

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Get-OutlookProtectionRule](https://technet.microsoft.com/fr-fr/library/dd298004\(v=exchg.150\)) et [Remove-OutlookProtectionRule](https://technet.microsoft.com/fr-fr/library/dd297961\(v=exchg.150\)).

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez supprimé une règle de protection Outlook avec succès, utilisez la cmdlet [Get-OutlookProtectionRule](https://technet.microsoft.com/fr-fr/library/dd298004\(v=exchg.150\)) pour récupérer les règles de protection Outlook. Pour consulter un exemple de récupération de règles de protection Outlook, voir [Examples](https://technet.microsoft.com/fr-fr/dd298004\(exchg.150\)#examples) dans **Get-OutlookProtectionRule**.

