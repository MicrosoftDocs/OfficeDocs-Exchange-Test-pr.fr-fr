---
title: 'Ajout de serveurs de BAL et accès au Client à un plan de num. URI SIP'
TOCTitle: Ajouter des serveurs de boîtes aux lettres et accès au Client à un plan de numérotation URI SIP
ms:assetid: 17fed308-ff0d-4e61-b9f9-e6680b6eccaa
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Aa996399(v=EXCHG.150)
ms:contentKeyID: 52062940
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Ajouter des serveurs de boîtes aux lettres et accès au Client à un plan de numérotation URI SIP

 

_**Sapplique à :** Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2013-04-16_

Vous pouvez ajouter des serveurs d'accès au client et des serveurs de boîtes aux lettres aux plans de numérotation URI SIP. Vous ne pouvez pas associer de serveurs d'accès au client et de serveurs de boîtes aux lettres à des plans de numérotation E.164 ou à numéro de poste, mais les serveurs répondront à tous les appels entrants.

Si vous déployez Microsoft Lync Server, pour permettre aux appels sortants de fonctionner correctement, vous devez ajouter manuellement tous les serveurs d'accès au client et tous les serveurs de boîtes aux lettres à tous les plans de numérotation URI SIP créés pour Lync Server.

Pour les autres tâches de gestion relatives aux plans de numérotation de messagerie unifiée, consultez la rubrique [Procédures de plan de numérotation de messagerie unifiée](um-dial-plan-procedures-exchange-2013-help.md).

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : Moins d’une minute.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l'entrée « Plans de numérotation de messagerie unifiée » dans la rubrique [Autorisations de messagerie unifiée](unified-messaging-permissions-exchange-2013-help.md).

  - Avant d'effectuer ces procédures, vérifiez qu'un plan de numérotation de messagerie unifiée SIP URI a été créé. Pour obtenir la procédure détaillée, consultez la rubrique [Créer un plan de numérotation de messagerie unifiée](https://docs.microsoft.com/fr-fr/exchange/voice-mail-unified-messaging/connect-voice-mail-system/create-um-dial-plan).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..


## Que souhaitez-vous faire ?

## Utiliser le Centre d'administration Exchange (CAE) pour ajouter un serveur de boîtes aux lettres à un plan de numérotation URI SIP

1.  Dans le CAE, accédez à **Serveurs** \> **Serveurs**.

2.  Dans l'affichage Liste, sélectionnez le serveur de boîtes aux lettres à modifier, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

3.  Dans la page **Exchange Server**, cliquez sur **Messagerie unifiée**.

4.  Sous **Paramètres de service de messagerie unifiée** \> **Plans de numérotation associés**, cliquez sur **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter").

5.  Dans la fenêtre **Sélectionner un plan de numérotation de messagerie unifiée**, sélectionnez le plan de numérotation URI SIP, cliquez sur **Ajouter**, sur **OK**, puis sur **Enregistrer**.

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour ajouter un serveur de boîtes aux lettres à un plan de numérotation URI SIP

Cet exemple ajoute le serveur de boîtes aux lettres `MyMailboxServer` à un plan de numérotation URI SIP nommé `MySIPDialPlan` et l'empêche d'accepter de nouveaux appels. Il montre également comment définir le mode de démarrage sur Double pour que le serveur de messagerie unifiée accepte les demandes TCP et TLS.

    Set-UMService -Identity MyMailboxServer -DialPlans MySIPDialPlan -Status Disabled -UMStartupMode Dual

Cet exemple ajoute le serveur de boîtes aux lettres `MyMailboxServer` à deux plans de numérotation SIP nommés `MySIPDialPlan` et `MySIPDialPlan2` et définit la configuration suivante :

  - Autorise les adresses IPv4 et IPv6.

  - Définit le nombre maximal d'appels entrants sur 50.

  - Configure le service d'accès SIP pour Lync Server.

<!-- end list -->

    Set-UMService -Identity MyMailboxServer -DialPlans MySIPDialPlan, MySIPDialPlan2 -IPAddressFamily Any -MaxCallsAllowed 50 -SipAccessService northamerica.lyncpoolna.contoso.com

## Utiliser le Centre d'administration Exchange (CAE) pour ajouter un serveur d'accès au client à un plan de numérotation URI SIP

1.  Dans le CAE, accédez à **Serveurs** \> **Serveurs**.

2.  Dans l'affichage Liste, sélectionnez le serveur d'accès au client à modifier, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

3.  Dans la page **Exchange Server**, cliquez sur **Messagerie unifiée**.

4.  Sous **Paramètres de routeur d'appels de messagerie unifiée** \> **Plans de numérotation associés**, cliquez sur **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter").

5.  Dans la fenêtre **Sélectionner un plan de numérotation de messagerie unifiée**, sélectionnez le plan de numérotation URI SIP, cliquez sur **Ajouter**, sur **OK**, puis sur **Enregistrer**.

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour ajouter un serveur d'accès au client à un plan de numérotation URI SIP

Cet exemple ajoute le serveur d'accès au client `MyClientAccessServer` à un plan de numérotation URI SIP nommé `MySIPDialPlan`. Il montre également comment définir le mode de démarrage sur Double pour que le serveur d'accès au client accepte les demandes TCP et TLS.

```powershell
Set-UMCallRouterSettings -DialPlans MySIPDialPlan -Server MyClientAccessServer -UMStartupMode Dual
```

Cet exemple ajoute le serveur d'accès au client `MyClientAccessServer` à deux plans de numérotation SIP nommés `MySIPDialPlan` et `MySIPDialPlan2`, et permet au serveur d'utiliser les adresses IPv4 et IPv6.

    Set-UMCallRouterSettings -DialPlans MySIPDialPlan, MySIPDialPlan2 -IPAddressFamily Any -Server MyClientAccessServer

