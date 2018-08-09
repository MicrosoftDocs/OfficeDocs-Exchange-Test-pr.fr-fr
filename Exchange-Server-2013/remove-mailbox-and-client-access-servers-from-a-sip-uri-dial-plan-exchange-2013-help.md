---
title: 'Supprimer des srv de BAL et accès au Client à partir d’un plan de num. URI SIP'
TOCTitle: Supprimer des serveurs de boîtes aux lettres et accès au Client à partir d'un plan de numérotation URI SIP
ms:assetid: 367441e1-1a0f-42c8-9fa8-8abe80b3d015
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Aa997238(v=EXCHG.150)
ms:contentKeyID: 54652752
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Supprimer des serveurs de boîtes aux lettres et accès au Client à partir d'un plan de numérotation URI SIP

 

_**Sapplique à :** Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2013-04-16_

Vous pouvez supprimer les serveurs d'accès au client et de boîtes aux lettres des plans de numérotation URI SIP. Lors du déploiement de Microsoft Lync Server, pour permettre aux appels sortants de fonctionner correctement, vous devez ajouter manuellement tous les serveurs d'accès au client et de boîtes aux lettres aux plans de numérotation URI SIP créés pour Lync Server. Cependant, il est possible que vous deviez supprimer un serveur d'accès au client ou de boîtes aux lettres de votre déploiement Lync, par exemple si vous effectuez une opération de maintenance ou si vous déconnectez le serveur.

Pour les autres tâches de gestion relatives aux plans de numérotation de messagerie unifiée, consultez la rubrique [Procédures de plan de numérotation de messagerie unifiée](um-dial-plan-procedures-exchange-2013-help.md).

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : moins d'une minute.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l'entrée « Plans de numérotation de messagerie unifiée » dans la rubrique [Autorisations de messagerie unifiée](unified-messaging-permissions-exchange-2013-help.md).

  - Avant d'effectuer ces procédures, vérifiez qu'un plan de numérotation de messagerie unifiée SIP URI a été créé. Pour obtenir la procédure détaillée, consultez la rubrique [Créer un plan de numérotation de messagerie unifiée](create-a-um-dial-plan-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..


## Que souhaitez-vous faire ?

## Utiliser le CAE pour supprimer un serveur de boîtes aux lettres d'un plan de numérotation URI SIP

1.  Dans le CAE, accédez à **Serveurs** \> **Serveurs**.

2.  Dans l'affichage Liste, sélectionnez le serveur de boîtes aux lettres à modifier, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

3.  Dans la page **Exchange Server**, cliquez sur **Messagerie unifiée**.

4.  Sous **Paramètres du service de messagerie unifiée** \> **Plans de numérotation associés**, localisez le plan de numérotation URI SIP à supprimer, cliquez sur **Supprimer**![Icône Suppression](images/Dd362328.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "Icône Suppression"), puis sur **Enregistrer**. Si vous voulez supprimer plusieurs plans de numérotation URI SIP, maintenez la touche Ctrl enfoncée, sélectionnez les plans de numérotation à supprimer, puis cliquez sur **Enregistrer**.

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour supprimer un serveur de boîtes aux lettres d'un plan de numérotation URI SIP

Cet exemple supprime le serveur de boîtes aux lettres nommé `MyMailboxServer` d'un plan de numérotation URI SIP nommé `MySIPDialPlan`.

    $dp= Get-UMDialPlan "MySIPDialPlan"
    $s=Get-UMService MyMailboxServer
    $s.dialplans-=$dp.identity
    Set-UMService -id MyMailboxServer -dialplans:$s.dialplans

Dans cet exemple figurent trois plans de numérotation URI SIP : SipDP1, SipDP2 et SipDP3. Cet exemple supprime le serveur de boîtes aux lettres nommé `MyMailboxServer` du plan de numérotation SipDP3.

    Set-UMService -id MyMailboxServer -DialPlans SipDP1,SipDP2

Dans cet exemple figurent deux plans de numérotation URI SIP : SipDP1 et SipDP2. Cet exemple supprime le serveur de boîtes aux lettres nommé `MyMailboxServer` du plan de numérotation SipDP2.

    Set-UMService -id MyMailboxServer -DialPlans SipDP1

Cet exemple supprime le serveur de boîtes aux lettres nommé `MyMailboxServer` de tous les plans de numérotation SIP.

    Set-UMService -id MyUMServer -DialPlans $null

## Utiliser le CAE pour supprimer un serveur d'accès au client d'un plan de numérotation URI SIP

1.  Dans le CAE, accédez à **Serveurs** \> **Serveurs**.

2.  Dans l'affichage Liste, sélectionnez le serveur d'accès au client à modifier, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

3.  Dans la page **Exchange Server**, cliquez sur **Messagerie unifiée**.

4.  Sous **Paramètres de routeur d'appels de messagerie unifiée** \> **Plans de numérotation associés**, localisez le plan de numérotation URI SIP à supprimer, cliquez sur **Supprimer**![Icône Suppression](images/Dd362328.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "Icône Suppression"), puis sur **Enregistrer**. Si vous voulez supprimer plusieurs plans de numérotation URI SIP, maintenez la touche Ctrl enfoncée, sélectionnez les plans de numérotation à supprimer, puis cliquez sur **Enregistrer**.

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour supprimer un serveur d'accès au client d'un plan de numérotation URI SIP

Cet exemple supprime le serveur d'accès au client nommé `MyClientAccessServer` d'un plan de numérotation URI SIP nommé `MySIPDialPlan`.

    $dp= Get-UMDialPlan "MySIPDialPlan"
    $s=Get-UMCallRouterSettings MyClientAccessServer
    $s.dialplans-=$dp.identity
    Set-UMCallRouterSettings -id MyClientAccessServer -dialplans:$s.dialplans

Dans cet exemple figurent trois plans de numérotation URI SIP : SipDP1, SipDP2 et SipDP3. Cet exemple supprime le serveur d'accès au client nommé `MyClientAccessServer` du plan de numérotation SipDP3.

    Set-UMCallRouterSettings -id MyClientAccessServer -DialPlans SipDP1,SipDP2

Dans cet exemple figurent deux plans de numérotation URI SIP : SipDP1 et SipDP2. Cet exemple supprime le serveur d'accès au client nommé `MyClientAccessServer` du plan de numérotation SipDP2.

    Set-UMCallRouterSettings -id MyClientAccessServer -DialPlans SipDP1

Cet exemple supprime le serveur d'accès au client nommé `MyClientAccessServer` de tous les plans de numérotation SIP.

    Set-UMCallRouterSettings -id MyClientAccessServer -DialPlans $null

