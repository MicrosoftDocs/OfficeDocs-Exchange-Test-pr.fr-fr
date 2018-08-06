---
title: "Déf. l’adresse du partenaire d’aperçu de messagerie vocale: Exchange 2013 Help | Microsoft Docs"
TOCTitle: Définir l'adresse du partenaire aperçu de messagerie vocale
ms:assetid: 57fbed1e-1b14-4939-95e6-ef7c072f32a9
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Ff630917(v=EXCHG.150)
ms:contentKeyID: 51407193
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Définir l'adresse du partenaire aperçu de messagerie vocale

 

_**Sapplique à :** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2013-02-13_

Vous pouvez définir l'adresse d'un partenaire d'aperçu de messagerie vocale dans une stratégie de boîte aux lettres de messagerie unifiée. Une fois que vous avez défini l'adresse du partenaire d'aperçu de messagerie vocale sur une stratégie de boîte aux lettres de messagerie unifiée, le paramètre s'applique à tous les utilisateurs à extension messagerie unifiée liés à cette stratégie de boîte aux lettres.

> [!NOTE]
> Vous devez utiliser l'environnement de ligne de commande Exchange Management Shell pour définir l'adresse du partenaire d'aperçu de messagerie vocale.


Pour plus d'informations sur le programme de partenariat d'aperçu de messagerie vocale, consultez la rubrique [Gestionnaire de l’aperçu de messagerie vocale](voice-mail-preview-advisor-exchange-2013-help.md).

Pour les autres tâches de gestion relatives à l'aperçu de messagerie vocale, consultez la rubrique [Procédures d'aperçu de messagerie vocale](voice-mail-preview-procedures-exchange-2013-help.md).

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : 1 minute.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l'entrée « Stratégies de boîte aux lettres de messagerie unifiée » dans la rubrique [Autorisations de messagerie unifiée](unified-messaging-permissions-exchange-2013-help.md).

  - Avant d'exécuter ces procédures, vérifiez qu'un plan de numérotation de messagerie unifiée a été créé. Pour obtenir la procédure détaillée, consultez la rubrique [Créer un plan de numérotation de messagerie unifiée](create-a-um-dial-plan-exchange-2013-help.md).

  - Avant d'exécuter ces procédures, vérifiez qu'un plan de numérotation de messagerie unifiée a été créé. Pour obtenir la procédure détaillée, consultez la rubrique [Créer une stratégie de boîte aux lettres de messagerie unifiée](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..


## Utiliser l'environnement de ligne de commande Exchange Management Shell pour définir l'adresse du partenaire d'aperçu de messagerie vocale sur une stratégie de boîte aux lettres de messagerie unifiée

Cet exemple définit l'adresse du partenaire d'aperçu de messagerie vocale comme étant exumvmp@fabrikam.com dans une stratégie de boîte aux lettres de messagerie unifiée portant le nom *MyUMMailboxPolicy*.

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -VoiceMailPreviewPartnerAddress exumvmp@fabrikam.com

