---
title: 'Empêcher les utlsr du même plan de num. à partir de la réception de télécopies | Microsoft Docs'
TOCTitle: Empêcher les utilisateurs dans le même plan de numérotation à partir de la réception de télécopies
ms:assetid: 4fc66414-c950-4bca-ac20-4e489f288d06
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb201688(v=EXCHG.150)
ms:contentKeyID: 52057075
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Empêcher les utilisateurs dans le même plan de numérotation à partir de la réception de télécopies

 

_**Sapplique à :** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2016-12-09_

Vous pouvez empêcher les utilisateurs à extension messagerie unifiée associés à un plan de numérotation de messagerie unifiée de recevoir des messages de télécopie. Par défaut, les utilisateurs à extension messagerie unifiée associés à un plan de numérotation de messagerie unifiée peuvent recevoir des messages de télécopie. Toutefois, il se peut que vous vouliez empêcher les utilisateurs associés à un plan de numérotation de messagerie unifiée particulier de recevoir des messages de télécopie.

Vous pouvez empêcher les utilisateurs à extension messagerie unifiée de recevoir des messages de télécopie en configurant le plan de numérotation de messagerie unifiée, la stratégie de boîte aux lettres de messagerie unifiée ou la boîte aux lettres de l'utilisateur à extension messagerie unifiée. Si vous désactivez la remise des messages de télécopie entrants sur un plan de numérotation de messagerie unifiée, les utilisateurs associés au plan de numérotation ne pourront pas recevoir de messages de télécopie. L'activation ou la désactivation de la télécopie sur un plan de numérotation de messagerie unifiée prime sur la configuration d'un utilisateur à extension messagerie unifiée individuel.

> [!NOTE]
> Vous pouvez utiliser le Centre d'administration Exchange (CAE) pour configurer les paramètres de télécopie sur une stratégie de boîte aux lettres de messagerie unifiée. Vous devez cependant utiliser l'environnement de ligne de commande Exchange Management Shell pour configurer les paramètres de télécopie sur des plans de numérotation ou pour des utilisateurs individuels.


Pour plus d’informations sur les partenaires de télécopie, consultez [Microsoft PinPoint pour les partenaires de télécopie](https://go.microsoft.com/fwlink/?linkid=190238).

Pour découvrir d'autres tâches de gestion relatives à la télécopie, consultez la rubrique [Procédures d'envoi de télécopie](faxing-procedures-exchange-2013-help.md).

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : moins d'une minute.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l'entrée « Plans de numérotation de messagerie unifiée » dans la rubrique [Autorisations de messagerie unifiée](unified-messaging-permissions-exchange-2013-help.md).

  - Avant d'exécuter ces procédures, vérifiez qu'un plan de numérotation de messagerie unifiée a été créé. Pour obtenir la procédure détaillée, consultez la rubrique [Créer un plan de numérotation de messagerie unifiée](create-a-um-dial-plan-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..


## Utiliser l'environnement de ligne de commande Exchange Management Shell pour empêcher les utilisateurs associés à un plan de numérotation de recevoir des messages de télécopie

Cet exemple empêche les utilisateurs à extension messagerie unifiée associés à un plan de numérotation de messagerie unifiée nommé `MyUMDialPlan` de recevoir des messages de télécopie.

    Set-UMDialPlan -Identity MyUMDialPlan -FaxEnabled $false

