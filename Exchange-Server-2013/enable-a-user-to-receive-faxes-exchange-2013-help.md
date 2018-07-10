---
title: 'Permettent aux utilisateurs de recevoir des télécopies: Exchange 2013 Help'
TOCTitle: Permettent aux utilisateurs de recevoir des télécopies
ms:assetid: a0505001-aac0-41ef-824f-76e5e56d7675
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb201712(v=EXCHG.150)
ms:contentKeyID: 52057142
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Permettent aux utilisateurs de recevoir des télécopies

 

_**Sapplique à :** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2016-12-09_

Vous pouvez autoriser un utilisateur à extension messagerie unifiée à recevoir des télécopies. Par défaut, quand vous activez la messagerie unifiée pour un utilisateur, ce dernier peut recevoir des télécopies si vous activez la fonctionnalité de télécopie et si vous configurez l'URI d'un partenaire de télécopie sur la stratégie de boîte aux lettres de messagerie unifiée associée à l'utilisateur. La fonctionnalité de télécopie peut être activée ou désactivée sur les plans de numérotation de messagerie unifiée, les stratégies de boîte aux lettres de messagerie unifiée ou la boîte aux lettres d'un utilisateur à extension messagerie unifiée.

Par défaut, la boîte aux lettres de l'utilisateur et le plan de numérotation associé à l'utilisateur permettent d'autoriser les télécopies entrantes. Cependant, pour qu'un utilisateur reçoive des télécopies, vous devez tout d'abord activer les télécopies entrantes sur la stratégie de boîte aux lettres de messagerie unifiée qui est associée à l'utilisateur à extension messagerie unifiée, puis entrer l'URI du partenaire de télécopie.

> [!NOTE]
> Vous pouvez utiliser le Centre d'administration Exchange (CAE) pour configurer les paramètres de télécopie sur une stratégie de boîte aux lettres de messagerie unifiée. Vous devez cependant utiliser l'environnement de ligne de commande Exchange Management Shell pour configurer les paramètres de télécopie sur des plans de numérotation ou pour des utilisateurs individuels.


Pour plus d’informations sur les partenaires de télécopie, consultez [Microsoft PinPoint pour les partenaires de télécopie](https://go.microsoft.com/fwlink/?linkid=190238).

Pour les autres tâches de gestion relatives à la télécopie, consultez la rubrique [Procédures d'envoi de télécopie](faxing-procedures-exchange-2013-help.md).

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : 2 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l'entrée « Stratégies de boîte aux lettres de messagerie unifiée » dans la rubrique [Autorisations de messagerie unifiée](unified-messaging-permissions-exchange-2013-help.md).

  - Avant d'exécuter ces procédures, vérifiez qu'un plan de numérotation de messagerie unifiée a été créé. Pour obtenir la procédure détaillée, consultez la rubrique [Créer un plan de numérotation de messagerie unifiée](create-a-um-dial-plan-exchange-2013-help.md).

  - Avant d'effectuer ces procédures, vérifiez qu'une stratégie de boîte aux lettres de messagerie unifiée a été créée. Pour obtenir la procédure détaillée, consultez la rubrique [Créer une stratégie de boîte aux lettres de messagerie unifiée](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Avant de réaliser ces procédures, vérifiez que la fonctionnalité de télécopie est activée sur la stratégie de boîte aux lettres de messagerie unifiée attribuée à l'utilisateur et que l'URI du partenaire de télécopie est configuré correctement.

  - Avant d'effectuer ces procédures, vérifiez que la messagerie unifiée est activée pour l'utilisateur. Pour obtenir la procédure détaillée, consultez la rubrique [Activation de la messagerie vocale pour un utilisateur](enable-a-user-for-voice-mail-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..


## Utiliser l'environnement de ligne de commande Exchange Management Shell pour permettre à un utilisateur à extension messagerie unifiée de recevoir des télécopies

Cet exemple autorise Tony Smith à recevoir des télécopies.

    Set-UMMailbox -Identity tonysmith@contoso.com -FaxEnabled $true

