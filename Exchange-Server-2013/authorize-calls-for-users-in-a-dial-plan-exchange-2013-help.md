---
title: 'Autoriser les appels destinés aux utilisateurs dans un plan de numérotation: Exchange 2013 Help'
TOCTitle: Autoriser les appels destinés aux utilisateurs dans un plan de numérotation
ms:assetid: 7c7fd0c4-4001-408e-b352-c49bac9f78cc
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb691175(v=EXCHG.150)
ms:contentKeyID: 51407207
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Autoriser les appels destinés aux utilisateurs dans un plan de numérotation

 

_**Sapplique à :** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2013-02-21_

Vous pouvez activer des autorisations de numérotation sur un plan de numérotation de messagerie unifiée. Les autorisations de numérotation sur un plan de numérotation permettent d'empêcher des utilisateurs Outlook Voice Access non authentifiés d'effectuer des appels téléphoniques nationaux/régionaux ou internationaux, c'est-à-dire de recourir à la *numérotation externe*. La numérotation externe intervient lorsque la messagerie unifiée effectue un appel sortant pour un utilisateur après qu'il a appelé un numéro de téléphone Outlook Voice Access configuré sur un plan de messagerie unifiée. Quand vous configurez un paramètre sur un plan de numérotation de messagerie unifiée, il s'applique à tous les utilisateurs non authentifiés qui appellent un numéro Outlook Voice Access.

Pour découvrir d'autres tâches de gestion relatives à la numérotation externe, consultez la rubrique [Ce qui permet aux utilisateurs d'effectuer les procédures d'appels](allowing-users-to-make-calls-procedures-exchange-2013-help.md).

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : moins d'une minute.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l'entrée « Plans de numérotation de messagerie unifiée » dans la rubrique [Autorisations de messagerie unifiée](unified-messaging-permissions-exchange-2013-help.md).

  - Avant d'exécuter ces procédures, vérifiez qu'un plan de numérotation de messagerie unifiée a été créé. Pour obtenir la procédure détaillée, consultez la rubrique [Créer un plan de numérotation de messagerie unifiée](create-a-um-dial-plan-exchange-2013-help.md).

  - Avant d'exécuter cette procédure, vérifiez que des règles de numérotation nationale/régionale et internationale ont été créées sur un plan de numérotation de messagerie unifiée. Pour obtenir la procédure détaillée, consultez la rubrique [Créer des règles de numérotation pour les utilisateurs](create-dialing-rules-for-users-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..


## Que souhaitez-vous faire ?

## Utiliser le Centre d'administration Exchange (CAE) pour activer des autorisations de numérotation dans un plan de numérotation de messagerie unifiée pour des groupes de règles de numérotation nationale/régionale

1.  Dans le CAE, accédez à **Messagerie unifiée** \> **Plans de numérotation de messagerie unifiée**. Dans l'affichage Liste, sélectionnez le plan de numérotation de messagerie unifiée à modifier puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

2.  Dans la page **Plan de numérotation de messagerie unifiée**, cliquez sur **Configurer**.

3.  Dans la page **Plan de numérotation de messagerie unifiée** \> **Autorisation de numérotation**, cliquez sur **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter") sous **Groupes de règles de numérotation nationale/régionale autorisés**.

4.  Dans la page **Sélectionner les groupes de règles de numérotation à autoriser**, sélectionnez le groupe de règles de numérotation et cliquez sur **OK**, puis **Enregistrer**.

## Utiliser le CAE pour activer des autorisations de numérotation dans un plan de numérotation de messagerie unifiée pour des groupes de règles de numérotation internationale

1.  Dans le CAE, accédez à **Messagerie unifiée** \> **Plans de numérotation de messagerie unifiée**. Dans l'affichage Liste, sélectionnez le plan de numérotation de messagerie unifiée à modifier puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

2.  Dans la page **Plan de numérotation de messagerie unifiée**, cliquez sur **Configurer**.

3.  Dans la page **Plan de numérotation de messagerie unifiée** \> **Autorisation de numérotation**, cliquez sur **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter") sous **Groupes de règles de numérotation internationale autorisés**.

4.  Dans la page **Sélectionner les groupes de règles de numérotation à autoriser**, sélectionnez le groupe de règles de numérotation et cliquez sur **OK**, puis **Enregistrer**.

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour activer les autorisations de numérotation nationale/régionale et internationale dans un plan de numérotation de messagerie unifiée

Cet exemple active les autorisations de numérotation InCountry/RegionGroup1, InCountry/RegionGroup2, InternationalGroup1 et InternationalGroup2 dans un plan de numérotation de messagerie unifiée nommé `MyUMDialPlan`.

    Set-UMDialPlan -Identity MyUMDialPlan -AllowedInCountryOrRegionGroups InCountry/RegionGroup1,InCountry/RegionGroup2 -AllowedInternationalGroups InternationalGroup1,InternationalGroup2

