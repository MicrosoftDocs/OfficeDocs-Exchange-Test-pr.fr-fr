---
title: 'Autoriser ou empêcher le transfert d’appels à partir d’Outlook Voice Access'
TOCTitle: Autoriser ou empêcher le transfert d'appels à partir d'Outlook Voice Access
ms:assetid: b80c57f1-394c-4608-8ad3-52a3e6d697db
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Ee423554(v=EXCHG.150)
ms:contentKeyID: 52057161
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Autoriser ou empêcher le transfert d'appels à partir d'Outlook Voice Access

 

_**Sapplique à :** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2013-02-22_

Vous pouvez autoriser les utilisateurs d'Outlook Voice Access à transférer des appels vers un utilisateur associé à un plan de numérotation de messagerie unifiée, ou les en empêcher. Par défaut, cette option et l'option **Laisser des messages vocaux sans faire sonner le téléphone de l'utilisateur**sont activées. Les utilisateurs Outlook Voice Access peuvent ainsi transférer des appels vers de utilisateurs du même plan de numérotation et leur laisser un message. Ce paramètre s'applique uniquement aux utilisateurs d'Outlook Voice Access qui ont entré leur code confidentiel et sont authentifiés.

Pour les autres tâches relatives aux plans de numérotation de messagerie unifiée, consultez la rubrique [Procédures de plan de numérotation de messagerie unifiée](um-dial-plan-procedures-exchange-2013-help.md).

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : moins d'une minute.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l'entrée « Plans de numérotation de messagerie unifiée » dans la rubrique [Autorisations de messagerie unifiée](unified-messaging-permissions-exchange-2013-help.md).

  - Avant d'effectuer ces procédures, vérifiez qu'un plan de numérotation de messagerie unifiée a été créé. Pour obtenir la procédure détaillée, consultez la rubrique [Créer un plan de numérotation de messagerie unifiée](create-a-um-dial-plan-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..


## Que souhaitez-vous faire ?

## Utiliser le Centre d'administration Exchange (CAE) pour empêcher les utilisateurs d'Outlook Voice Access de transférer des appels

1.  Dans le CAE, accédez à **Messagerie unifiée** \> **Plans de numérotation de messagerie unifiée**. Dans l'affichage Liste, sélectionnez le plan de numérotation de messagerie unifiée à modifier, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

2.  Dans la page **Plan de numérotation de messagerie unifiée**, cliquez sur **Configurer**.

3.  Dans **Transfert & recherche**, sous **Autoriser les appelants à**, cochez la case en regard de l'option **transférer aux utilisateurs** pour permettre aux appelants de transférer des appels à d'autres utilisateurs du même plan de numérotation. Si vous souhaitez empêcher les utilisateurs d'Outlook Voice Access à transférer des appels à d'autres utilisateurs, décochez cette case.

4.  Cliquez sur **Enregistrer**.

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour empêcher les utilisateurs d'Outlook Voice Access de transférer des appels

Cet exemple autorise les utilisateurs d'Outlook Voice Access à transférer des appels à d'autres utilisateurs du même plan de numérotation sur le plan de numérotation de messagerie unifiée `MyUMDialPlan`.

    Set-UMDialPlan -identity MyUMDialPlan -AllowDialPlanSubscribers $true

Cet exemple empêche les utilisateurs d'Outlook Voice Access de transférer des appels à d'autres utilisateurs du même plan de numérotation sur le plan de numérotation de messagerie unifiée `MyUMDialPlan`.

    Set-UMDialPlan -identity MyUMDialPlan -AllowDialPlanSubscribers $false

