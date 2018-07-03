---
title: 'Supprimer un plan de numérotation de messagerie unifiée: Exchange 2013 Help'
TOCTitle: Supprimer un plan de numérotation de messagerie unifiée
ms:assetid: c9b32ef6-432c-45ca-b94c-31bbcc973128
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb124546(v=EXCHG.150)
ms:contentKeyID: 50479219
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Supprimer un plan de numérotation de messagerie unifiée

 

_**Sapplique à :** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2012-11-11_

Vous pouvez supprimer un plan de numérotation de messagerie unifiée. Une fois que vous supprimez le plan de numérotation de messagerie unifiée, il ne sera plus disponible pour les passerelles IP de messagerie unifiée, les stratégies de boîte aux lettres de messagerie unifiée et les groupements de postes de messagerie unifiée. Vous ne pouvez pas supprimer un plan de numérotation de messagerie unifiée s’il est référencé par des stratégies de boîte aux lettres de messagerie unifiée, par des standards automatiques de messagerie unifiée, par des passerelles IP de messagerie unifiée ou par des groupements de postes de messagerie unifiée, ou s’il est associé à ces éléments.

Pour les autres tâches de gestion relatives aux plans de numérotation de messagerie unifiée, voir [Procédures de plan de numérotation de messagerie unifiée](um-dial-plan-procedures-exchange-2013-help.md).

## Ce qu’il faut savoir avant de commencer ?

  - Durée d'exécution estimée : moins d'une minute.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l'entrée « Plans de numérotation de messagerie unifiée » dans la rubrique [Autorisations de messagerie unifiée](unified-messaging-permissions-exchange-2013-help.md).

  - Avant d'effectuer ces procédures, vérifiez qu'un plan de numérotation de messagerie unifiée a été créé. Pour obtenir la procédure détaillée, consultez la rubrique [Créer un plan de numérotation de messagerie unifiée](create-a-um-dial-plan-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..


## Que souhaitez-vous faire ?

## Utiliser le CAE pour supprimer un plan de numérotation existant

1.  Dans le Centre d’administration Exchange, accédez à **Messagerie unifiée** \> **Plans de numérotation de messagerie unifiée**.

2.  Dans l’affichage de liste, sélectionnez le plan de numérotation de messagerie unifiée que vous voulez supprimer, puis cliquez sur **Modifier**![Icône Supprimer](images/Dd979797.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "Icône Supprimer").

3.  Sur la page Avertissement, cliquez sur **Oui**.

## Utiliser l’environnement de ligne de commande Exchange Management Shell pour supprimer un plan de numérotation existant

Cet exemple supprime un plan de numérotation de messagerie unifiée nommé `MyUMDialPlan`.

    RemoveUMDialplan -identity MyUMDialPlan

