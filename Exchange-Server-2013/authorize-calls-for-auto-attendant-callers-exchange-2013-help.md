---
title: "Autoriser les appels d'appelants de standard automatique: Exchange 2013 Help"
TOCTitle: Autoriser les appels d'appelants de standard automatique
ms:assetid: c6c94fad-64df-44aa-a198-980f017ef716
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb691238(v=EXCHG.150)
ms:contentKeyID: 51407236
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Autoriser les appels d'appelants de standard automatique

 

_**Sapplique à :** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2013-02-21_

Vous pouvez activer des autorisations de numérotation sur un standard automatique de messagerie unifiée. Les autorisations de numérotation sur un standard automatique permettent d'empêcher des utilisateurs qui appellent le standard automatique d'effectuer des appels téléphoniques nationaux/régionaux ou internationaux, c'est-à-dire de recourir à un *automate d'appels*. L'automate d'appels intervient quand la messagerie unifiée effectue un appel sortant pour un utilisateur après que celui-ci a appelé un numéro de téléphone configuré sur un standard automatique de messagerie unifiée.

Pour découvrir d'autres tâches de gestion relatives à la numérotation externe, consultez la rubrique [Ce qui permet aux utilisateurs d'effectuer les procédures d'appels](allowing-users-to-make-calls-procedures-exchange-2013-help.md).

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : moins d'une minute.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l'entrée « Standards automatiques de messagerie unifiée » dans la rubrique [Autorisations de messagerie unifiée](unified-messaging-permissions-exchange-2013-help.md).

  - Avant d’exécuter ces procédures, vérifiez qu’un plan de numérotation de messagerie unifiée a été créé. Pour obtenir la procédure détaillée, consultez la rubrique [Créer un plan de numérotation de messagerie unifiée](create-a-um-dial-plan-exchange-2013-help.md).

  - Avant d'exécuter ces procédures, vérifiez qu'un standard automatique de messagerie unifiée a été créé. Pour obtenir la procédure détaillée, consultez la rubrique [Créer un standard automatique de messagerie unifiée](create-a-um-auto-attendant-exchange-2013-help.md).

  - Avant d'exécuter ces procédures, vérifiez que des règles de numérotation nationale/régionale et internationale ont été créées sur un plan de numérotation de messagerie unifiée. Pour obtenir la procédure détaillée, consultez la rubrique [Créer des règles de numérotation pour les utilisateurs](create-dialing-rules-for-users-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..


## Que souhaitez-vous faire ?

## Utiliser le Centre d'administration Exchange (CAE) pour activer des autorisations de numérotation sur un standard automatique de messagerie unifiée pour des groupes de règles d'appels nationaux/régionaux

1.  Dans le CAE, accédez à **Messagerie unifiée** \> **Plans de numérotation de messagerie unifiée**. Dans l'affichage Liste, sélectionnez le plan de numérotation de messagerie unifiée à modifier puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

2.  Dans la page **Plan de numérotation de messagerie unifiée**, sous **Standards automatiques de messagerie unifiée**, sélectionnez le standard automatique de messagerie unifiée pour lequel créer une autorisation de numérotation, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

3.  Dans la page **Standard automatique de messagerie unifiée** \> **Autorisation de numérotation**, cliquez sur **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter") sous **Groupes de règles de numérotation nationale/régionale autorisés**.

4.  Dans la page **Sélectionner les groupes de règles de numérotation à autoriser**, sélectionnez le groupe de règles de numérotation et cliquez sur **OK**, puis sur **Enregistrer**.

## Utiliser le Centre d'administration Exchange (CAE) pour activer des autorisations de numérotation sur un standard automatique de messagerie unifiée pour des groupes de règles d'appels à l'international

1.  Dans le CAE, accédez à **Messagerie unifiée** \> **Plans de numérotation de messagerie unifiée**. Dans l'affichage Liste, sélectionnez le plan de numérotation de messagerie unifiée à modifier puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

2.  Dans la page **Plan de numérotation de messagerie unifiée**, sous **Standards automatiques de messagerie unifiée**, sélectionnez le standard automatique de messagerie unifiée pour lequel créer une autorisation de numérotation, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

3.  Dans la page **Standard automatique de messagerie unifiée** \> **Autorisation de numérotation**, cliquez sur **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter") sous **Groupes de règles de numérotation internationale autorisés**.

4.  Dans la page **Sélectionner les groupes de règles de numérotation à autoriser**, sélectionnez le groupe de règles de numérotation et cliquez sur **OK**, puis sur **Enregistrer**.

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour activer des autorisations de numérotation internationale et nationale/régionale sur un standard automatique de messagerie unifiée

Cet exemple active les autorisations de numérotation InCountry/RegionGroup1, InCountry/RegionGroup2, InternationalGroup1 et InternationalGroup2 sur le standard automatique de messagerie unifiée `MyUMAutoAttendant`.

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -AllowedInCountryOrRegionGroups InCountry/RegionGroup1,InCountry/RegionGroup2 -AllowedInternationalGroups InternationalGroup1,InternationalGroup2

