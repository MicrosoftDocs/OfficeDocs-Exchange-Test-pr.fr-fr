---
title: 'Configuration d’un numéro Outlook Voice Access: Exchange 2013 Help'
TOCTitle: Configuration d’un numéro Outlook Voice Access
ms:assetid: 443c838e-f266-4893-b6b2-e5fc96579b55
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Aa997680(v=EXCHG.150)
ms:contentKeyID: 50555387
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configuration d’un numéro Outlook Voice Access

 

_**Sapplique à :** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2016-12-09_

Un numéro Outlook Voice Access permet à un utilisateur activé pour la messagerie unifiée et la messagerie vocale d'accéder à sa boîte aux lettres à l'aide d'Outlook Voice Access. Lorsque vous configurez un numéro Outlook Voice Access ou un numéro d'accès d'abonné dans un plan de numérotation, les utilisateurs à extension messagerie unifiée peuvent appeler le numéro, se connecter à leur boîte aux lettres et accéder à leurs informations personnelles de messagerie électronique, de messagerie vocale, de calendrier et de contact.

Par défaut, lorsque vous créez un plan de numérotation de messagerie unifiée, aucun numéro Outlook Voice Access n'est configuré. Pour configurer un numéro Outlook Voice Access, vous devez d'abord créer un plan de numérotation, puis configurer un numéro Outlook Voice Access sous l'option **Outlook Voice Access** du plan de numérotation. Bien qu'un numéro Outlook Voice Access ne soit pas nécessaire, vous devez configurer au moins un numéro Outlook Voice Access pour permettre à un utilisateur à extension messagerie d'utiliser Outlook Voice Access pour accéder à sa boîte aux lettres. Vous pouvez configurer plusieurs numéros Outlook Voice Access pour un plan de numérotation unique.

Les numéros Outlook Voice Access peuvent contenir des caractères alphabétiques, numériques et spéciaux, des séparateurs et des espaces. Par exemple :

  - \+14255551010

  - \+1-425-555-1010

  - 4255551010

  - \+1 425 555 1010

  - 1-800-555-CALL

Pour plus d'informations sur les options de menu disponibles pour les utilisateurs d'Outlook Voice Access, consultez le guide de référence rapide pour Outlook Voice Access disponible dans le [Centre de téléchargement Microsoft](https://go.microsoft.com/fwlink/p/?linkid=64645).

Pour les autres tâches de gestion relatives aux plans de numérotation de messagerie unifiée, consultez la rubrique [Procédures de plan de numérotation de messagerie unifiée](um-dial-plan-procedures-exchange-2013-help.md).

## Ce qu’il faut savoir avant de commencer ?

  - Durée d'exécution estimée : moins d'une minute.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l'entrée « Plans de numérotation de messagerie unifiée » dans la rubrique [Autorisations de messagerie unifiée](unified-messaging-permissions-exchange-2013-help.md).

  - Avant d'exécuter ces procédures, vérifiez qu'un plan de numérotation de messagerie unifiée a été créé. Pour obtenir la procédure détaillée, consultez la rubrique [Créer un plan de numérotation de messagerie unifiée](create-a-um-dial-plan-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..


## Que souhaitez-vous faire ?

## Utiliser le Centre d'administration Exchange (CAE) pour configurer un numéro Outlook Voice Access

1.  Dans le Centre d'administration Exchange, accédez à **Messagerie unifiée** \> **Plans de numérotation de messagerie unifiée**.

2.  Dans l'affichage Liste, sélectionnez le plan de numérotation de messagerie unifiée à modifier puis, dans la barre d'outils, cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

3.  Dans la page **Plan de numérotation de messagerie unifiée**, cliquez sur **Configurer**.

4.  Dans **Outlook Voice Access**, sous **numéros Outlook Voice Access**, saisissez le nombre à utiliser dans le champ, puis cliquez sur **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter").

5.  Cliquez sur **Enregistrer**.

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour configurer un numéro Outlook Voice Access

Cet exemple définit le numéro Outlook Voice Access sur 4255550100 pour un plan de numérotation de messagerie unifiée nommé `MyUMDialPlan`.

    Set-UMDialPlan -identity MyUMDialPlan -AccessTelephoneNumbers 4255550100

