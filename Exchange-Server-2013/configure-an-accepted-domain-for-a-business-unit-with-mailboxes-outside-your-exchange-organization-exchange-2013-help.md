---
title: 'Config. domaine accepté pr 1 unité cciale avec BAL à l’ext. de l’org. Exchange'
TOCTitle: Configurer un domaine accepté pour une unité commerciale avec des boîtes aux lettres à l’extérieur de votre organisation Exchange
ms:assetid: ff46310b-5392-4eac-97bc-d39d397e1ce1
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ657737(v=EXCHG.150)
ms:contentKeyID: 50479640
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configurer un domaine accepté pour une unité commerciale avec des boîtes aux lettres à l’extérieur de votre organisation Exchange

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2014-08-06_

Dans certaines instances, vous voudrez peut-être configurer un domaine accepté pour une division dans laquelle certains destinataires, ou tous, dans le domaine ne disposent pas de boîtes aux lettres dans votre organisation Exchange. Cela peut se produire, par exemple, lorsqu'une organisation partage le même espace d’adressage SMTP avec plusieurs systèmes de messagerie différents. Dans ces cas, vous pouvez configurer un domaine accepté en tant que domaine de relais interne.

## Ce qu’il faut savoir avant de commencer ?

  - Durée d'exécution estimée : 5 minutes

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez entrée « Domaines acceptés » dans la rubrique [Autorisations de flux de messagerie](mail-flow-permissions-exchange-2013-help.md).

  - Si vous disposez d’un serveur de transport Edge abonné dans votre réseau de périmètre, vous configurez les domaines acceptés sur un serveur de boîtes aux lettres dans votre organisation Exchange. La configuration des domaines acceptés est répliquée sur le serveur de transport Edge lors de la synchronisation EdgeSync. Pour plus d’informations, consultez la rubrique [Abonnements Edge](edge-subscriptions-exchange-2013-help.md).

  - Avant de configurer un domaine accepté, vous devez vérifier qu'un enregistrement de ressource MX DNS (Domain Name System) public existe pour cet espace de noms SMTP et que l'enregistrement de ressource MX fait référence à un nom de serveur et une adresse IP associés à l'organisation .

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.


## Utiliser le Centre d’administration Exchange (CAE) pour configurer un domaine accepté comme domaine de relais interne

1.  Dans le Centre d’administration Exchange (CAE), accédez à **Flux de messagerie** \> **Domaines acceptés**, sélectionnez le domaine à configurer, puis cliquez sur **Modifier** ![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

2.  Dans le champ **Nom**, saisissez le nom d'affichage pour le domaine accepté. Chaque domaine accepté de votre organisation doit avoir un nom complet unique. Il peut être différent du domaine accepté. Par exemple, le domaine Contoso.com pourrait avoir un nom d'affichage de Contoso Local Accepted Domain.

3.  Sélectionnez **Domaine de relais interne**.

4.  Cliquez sur **Enregistrer**.

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez configuré sans problème un domaine accepté comme domaine de relais interne, envoyez un message à partir du domaine de relais interne à une boîte aux lettres de votre organisation Exchange et vérifiez qu'il est bien reçu.

