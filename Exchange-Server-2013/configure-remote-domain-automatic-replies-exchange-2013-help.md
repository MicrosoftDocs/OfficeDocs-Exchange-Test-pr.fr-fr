---
title: 'Configurer des réponses automatiques de domaine distant: Exchange 2013 Help'
TOCTitle: Configurer des réponses automatiques de domaine distant
ms:assetid: 3d88a1fb-4b62-419a-a50d-ffd868e229d0
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ657720(v=EXCHG.150)
ms:contentKeyID: 50477944
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configurer des réponses automatiques de domaine distant

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2015-04-08_

Vous pouvez utiliser Exchange Management Shell pour configurer la façon dont les courriers électroniques sont envoyés et reçus via des domaines distants. La démonstration suivante montre comment utiliser l’environnement de ligne de commande Exchange Management Shell pour configurer la manière dont Exchange gère les réponses automatiques.

## Ce qu’il faut savoir avant de commencer ?

  - Durée d'exécution estimée : 10 minutes

  - Vous pouvez uniquement utiliser l'environnement de ligne de commande Exchange Management Shell pour effectuer cette tâche.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez - Entrée « Domaine distant » dans la rubrique [Autorisations de flux de messagerie](mail-flow-permissions-exchange-2013-help.md).

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


## Utiliser l’environnement de ligne de commande Exchange Management Shell pour configurer les réponses automatiques

Vous pouvez utiliser la cmdlet **Set-RemoteDomain** pour configurer les propriétés d’un domaine distant.

Cet exemple permet l’envoi de réponses automatiques au domaine distant nommé Contoso. Ce paramètre est désactivé par défaut.

    Set-RemoteDomain Contoso -AutoReplyEnabled $true

Dans cet exemple les transferts automatiques vers le domaine distant sont autorisés. Ce paramètre est désactivé par défaut.

    Set-RemoteDomain Contoso -AutoForwardEnabled $true

