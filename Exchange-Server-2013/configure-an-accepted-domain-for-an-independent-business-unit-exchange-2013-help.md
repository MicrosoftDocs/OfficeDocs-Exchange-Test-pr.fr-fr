---
title: 'Configurer un domaine accepté pour une division indépendante: Exchange 2013 Help'
TOCTitle: Configurer un domaine accepté pour une division indépendante
ms:assetid: bc95dbdc-3669-4c06-ab94-90093bc0dbfd
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ657491(v=EXCHG.150)
ms:contentKeyID: 50479018
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configurer un domaine accepté pour une division indépendante

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2014-02-17_

Il peut vous arriver de devoir configurer un domaine accepté pour une division indépendante avec des serveurs de messagerie externes à votre organisation Exchange. Dans ce type de situations, vous pouvez configurer le domaine accepté en tant que domaine de relais externe.

## Ce qu’il faut savoir avant de commencer ?

  - Durée d'exécution estimée : 5 minutes

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez entrée « Domaines acceptés » dans la rubrique [Autorisations de flux de messagerie](mail-flow-permissions-exchange-2013-help.md).

  - Si vous disposez d’un serveur de transport Edge abonné dans votre réseau de périmètre, vous configurez les domaines acceptés sur un serveur de boîtes aux lettres dans votre organisation Exchange. La configuration des domaines acceptés est répliquée sur le serveur de transport Edge lors de la synchronisation EdgeSync. Pour plus d’informations, consultez la rubrique [Abonnements Edge](edge-subscriptions-exchange-2013-help.md).

  - Vous ne pouvez pas créer de domaine accepté portant le même nom qu'un domaine distant déjà configuré. Par exemple, si fabrikam.com est configuré en tant que domaine distant, vous ne pouvez pas créer le domaine accepté fabrikam.com.

  - Avant de configurer un domaine accepté, vous devez vérifier qu'un enregistrement de ressource MX DNS (Domain Name System) public existe pour cet espace de noms SMTP et que l'enregistrement de ressource MX fait référence à un nom de serveur et une adresse IP associés à l'organisation .

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


## Utiliser le CAE pour configurer un domaine accepté en tant que domaine de relais externe

Il peut vous arriver de devoir configurer un domaine accepté pour une division avec des serveurs de messagerie externes à votre organisation Exchange.

1.  Dans le CAE, rendez-vous sur **Flux de messagerie** \> **Domaines acceptés**, sélectionnez le domaine à configurer, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

2.  Dans le champ **Nom**, saisissez le nom d'affichage pour le domaine accepté. Chaque domaine accepté de votre organisation doit avoir un nom complet unique. Il peut être différent du domaine accepté. Par exemple, le domaine Contoso.com pourrait avoir un nom d'affichage de Contoso Local Accepted Domain.

3.  Sélectionnez **Domaine de relais externe**. Cette option permet de relayer les messages électroniques vers un serveur externe à votre organisation Exchange.

4.  Cliquez sur **Enregistrer**.

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez bien configuré un domaine accepté en tant que domaine de relais externe, envoyez un message depuis le domaine accepté que vous avez configuré en tant que domaine de relais externe, et vérifiez qu’il est bien reçu.

