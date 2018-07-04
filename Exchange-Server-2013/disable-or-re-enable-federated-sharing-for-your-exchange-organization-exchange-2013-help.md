---
title: 'Désactiver ou réactiver le partage fédéré de votre organisation Exchange: Exchange 2013 Help'
TOCTitle: Désactiver ou réactiver le partage fédéré de votre organisation Exchange
ms:assetid: d36490d8-0268-47b9-a6d4-e56427f1b02e
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ657497(v=EXCHG.150)
ms:contentKeyID: 50479238
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Désactiver ou réactiver le partage fédéré de votre organisation Exchange

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2014-02-17_

Il peut arriver que vous soyez amené à désactiver temporairement un partage fédéré pour votre organisation. Au lieu de supprimer l’approbation de fédération existante ou les relations d’organisation et les stratégies de partage dont vous pourriez avoir besoin a l’avenir, vous pouvez simplement désactiver l’identificateur d’organisation (OrgID) de l’approbation de fédération.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ673034.Caution(EXCHG.150).gif" title="Attention" alt="Attention" />Attention :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Pour les déploiements hybrides avec Office 365, la désactivation de l’approbation de fédération pour vos serveurs locaux entraîne la désactivation de fonctionnalités hybrides, telles que les informations de disponibilité du calendrier partagé, les infos-courrier et le suivi des messages. Cependant, le transport de messagerie sécurisé ne sera pas désactivé dans le déploiement hybride si l’approbation de fédération de l’organisation locale est désactivée.</td>
</tr>
</tbody>
</table>


Pour en savoir plus sur les approbations de fédération, consultez la rubrique [Fédération](federation-exchange-2013-help.md). Pour en savoir plus sur le partage fédéré, voir [Partage](sharing-exchange-2013-help.md).

Si vous souhaitez rechercher des tâches de gestion supplémentaires relatives au partage fédéré, consultez [Procédures de fédération](federation-procedures-exchange-2013-help.md).

> [!NOTE]
> Cette fonctionnalité d’Exchange Server 2013 n’est pas entièrement compatible avec les systèmes Office 365 exécutés par 21Vianet en Chine et certaines limitations de fonctionnalités peuvent s’appliquer. Pour plus d’informations, voir <a href="https://go.microsoft.com/fwlink/?linkid=313640">En savoir plus sur Office 365 exécuté par 21Vianet</a>.


## Ce qu’il faut savoir avant de commencer ?

  - Durée d'exécution estimée : 5 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez *Federation and certificates* Entrée d'autorisations dans la rubrique [Autorisations d’infrastructure Exchange et Shell](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md).

  - Toutes les relations organisationnelles et les stratégies de partage existantes d’autres organisations Exchange fédérées ne seront pas modifiées et ne fonctionneront pas. Les stratégies de partage qui sont configurées pour offrir aux destinataires Internet un accès aux informations de calendrier ne seront pas affectées.

  - Vous ne pouvez pas utiliser le Centre d’administration Exchange pour désactiver ou activer l’identificateur d’organisation fédérée d’une approbation de fédération. Vous devez utiliser l'environnement de ligne de commande Exchange Management Shell.

## Utilisation de l’environnement de ligne de commande Exchange Management Shell pour désactiver ou réactiver le partage fédéré

Cet exemple désactive l’identificateur d’organisation, ainsi que la fédération et le partage fédéré de l’organisation Exchange.

    Set-FederatedOrganizationIdentifier -Enabled $false

Cet exemple active l’identificateur d’organisation, et réactive la fédération et le partage fédéré de l’organisation Exchange.

    Set-FederatedOrganizationIdentifier -Enabled $true

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Set-FederatedOrganizationIdentifier](https://technet.microsoft.com/fr-fr/library/dd351037\(v=exchg.150\)).

## Comment savoir si cela a fonctionné ?

L’exécution réussie de la cmdlet **Set-OrganizationIdentifier** sera le premier indicateur de désactivation ou d’activation de l’identificateur d’organisation.

Pour confirmer que la réussite de l’opération, exécutez la commande de l’environnement de ligne de commande Exchange Management Shell et vérifiez la valeur renvoyée pour le paramètre *Enabled*

    Get-FederatedOrganizationIdentifier

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.

