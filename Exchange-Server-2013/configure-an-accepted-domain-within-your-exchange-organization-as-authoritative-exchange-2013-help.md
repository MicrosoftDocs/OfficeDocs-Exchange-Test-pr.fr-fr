---
title: 'Configurer un domaine accepté dans votre organisation Exchange comme autorité: Exchange 2013 Help'
TOCTitle: Configurer un domaine accepté dans votre organisation Exchange comme autorité
ms:assetid: e182d54f-e58a-47ba-a5c1-28c0dfa86eed
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ657734(v=EXCHG.150)
ms:contentKeyID: 50479397
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configurer un domaine accepté dans votre organisation Exchange comme autorité

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2014-02-17_

Si un domaine appartenant à votre organisation héberge des boîtes aux lettres pour tous les destinataires dans un espace de noms SMTP, ce domaine est considéré comme faisant autorité. Par défaut, un domaine accepté est configuré comme faisant autorité pour l’organisation Exchange. Si votre organisation dispose de plusieurs espaces de noms SMTP, vous pouvez configurer plusieurs domaines acceptés faisant autorité.

## Ce qu’il faut savoir avant de commencer ?

  - Durée d'exécution estimée : 5 minutes

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez entrée « Domaines acceptés » dans la rubrique [Autorisations de flux de messagerie](mail-flow-permissions-exchange-2013-help.md).

  - Si vous disposez d’un serveur de transport Edge abonné dans votre réseau de périmètre, vous configurez les domaines acceptés sur un serveur de boîtes aux lettres dans votre organisation Exchange. La configuration des domaines acceptés est répliquée sur le serveur de transport Edge lors de la synchronisation EdgeSync. Pour plus d’informations, consultez la rubrique [Abonnements Edge](edge-subscriptions-exchange-2013-help.md).

  - Vous ne pouvez pas créer de domaine accepté portant le même nom qu'un domaine distant déjà configuré. Par exemple, si fabrikam.com est configuré en tant que domaine distant, vous ne pouvez pas créer le domaine accepté fabrikam.com.

  - Avant de configurer un domaine accepté, vous devez vérifier qu'un enregistrement de ressource MX DNS (Domain Name System) public existe pour cet espace de noms SMTP et que l'enregistrement de ressource MX fait référence à un nom de serveur et une adresse IP associés à l'organisation Exchange.

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


## Utiliser le CAE pour configurer un domaine accepté faisant autorité

Si un domaine accepté pour votre organisation Exchange héberge toutes les boîtes aux lettres des destinataires dans un espace de noms SMTP, vous souhaitez peut-être le configurer comme domaine faisant autorité.

1.  Dans le Centre d’administration Exchange, accédez à **Flux de messagerie** \> **Domaines acceptés**, puis cliquez sur **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter").

2.  Dans le champ **Nom**, saisissez le nom d'affichage pour le domaine accepté. Chaque domaine accepté de votre organisation doit avoir un nom complet unique, qui peut différer du nom de domaine accepté. Par exemple, le domaine contoso.com pourrait avoir un nom d'affichage de Contoso Local Accepted Domain.

3.  Dans le champ **Domaine accepté**, saisissez le domaine accepté. Spécifiez un espace de noms SMTP pour lequel votre organisation accepte les messages électroniques. (par exemple, contoso.com).

4.  Sélectionnez **Domaine faisant autorité**. Cette option concerne les messages électroniques relayés vers des serveurs au sein de votre organisation Exchange pour un domaine accepté qui héberge les boîtes aux lettres de tous les destinataires dans un espace de noms SMTP.

5.  Cliquez sur **Enregistrer**.

<table>
<thead>
<tr class="header">
<th><img src="images/Bb125224.tip(EXCHG.150).gif" title="Conseil" alt="Conseil" />Conseil :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Pour configurer un domaine accepté créé antérieurement, sélectionnez-en un dans la liste des domaines acceptés, puis cliquez sur <strong>Modifier</strong><img src="images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif" title="Icône Modifier" alt="Icône Modifier" />. Vous pouvez configurer plusieurs domaines faisant autorité.</td>
</tr>
</tbody>
</table>


## Comment savoir si cela a fonctionné ?

Votre nouveau domaine accepté apparaîtra dans la liste des domaines acceptés du CAE. Pour vérifier que vous avez configuré correctement le domaine accepté faisant autorité, envoyez un message au domaine et assurez-vous de sa réception.

