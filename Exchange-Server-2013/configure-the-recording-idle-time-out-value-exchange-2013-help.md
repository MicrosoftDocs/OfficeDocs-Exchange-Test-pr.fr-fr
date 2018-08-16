---
title: 'Configurer la durée d’inactivité d’enregistrement: Exchange 2013 Help'
TOCTitle: Configurez la valeur de délai d'inactivité d'enregistrement
ms:assetid: a7fb9a09-fde9-447d-ad2c-95598405e99b
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Ee423550(v=EXCHG.150)
ms:contentKeyID: 50478840
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurez la valeur de délai d'inactivité d'enregistrement

 

_**Sapplique à :** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2012-11-11_

Vous pouvez spécifier le nombre de secondes correspondant à la durée de silence autorisée par le système lors de l’enregistrement d’un message vocal avant qu’il ne soit mis fin à l’appel. Pour la plupart des organisations, cette valeur doit être définie par défaut sur 5 secondes.

Cette valeur peut être comprise entre 2 et 10. La définition d’une valeur trop basse peut entraîner la déconnexion des appelants par le système avant que ceux-ci n’aient eu le temps de laisser leur message vocal. La définition d’une valeur trop élevée autorise les silences relativement longs dans les messages vocaux.

Pour les autres tâches de gestion relatives aux plans de numérotation de messagerie unifiée, voir [Procédures de plan de numérotation de messagerie unifiée](um-dial-plan-procedures-exchange-2013-help.md).

## Ce qu’il faut savoir avant de commencer ?

  - Durée d'exécution estimée : moins d'une minute.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l'entrée « Plans de numérotation de messagerie unifiée » dans la rubrique [Autorisations de messagerie unifiée](unified-messaging-permissions-exchange-2013-help.md).

  - Avant d'effectuer ces procédures, vérifiez qu'un plan de numérotation de messagerie unifiée a été créé. Pour obtenir la procédure détaillée, consultez la rubrique [Créer un plan de numérotation de messagerie unifiée](create-a-um-dial-plan-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..


## Que souhaitez-vous faire ?

## Utiliser le CAE (Centre d’administration Exchange) pour configurer la valeur du délai d'inactivité d'enregistrement

1.  Dans le CAE, accédez à **Messagerie unifiée** \> **Plans de numérotation de messagerie unifiée**.

2.  Dans l'affichage de liste, sélectionnez le plan de numérotation de messagerie unifiée que vous souhaitez modifier, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

3.  Dans la page **Plan de numérotation de messagerie unifiée**, cliquez sur **Configurer**.

4.  Dans **Paramètres**, sous **Délai d’inactivité d’enregistrement (secondes)**, entrez le nombre voulu exprimé en secondes.

5.  Cliquez sur **Enregistrer**.

## Utiliser l’environnement de ligne de commande Exchange Management Shell pour configurer la valeur du délai d’inactivité d’enregistrement

Cet exemple illustre la définition de la valeur du délai d’inactivité d’enregistrement sur 10 pour un plan de numérotation de messagerie unifiée appelé `MyUMDialPlan`.

    Set-UMDialPlan -identity MyUMDialPlan -RecordingIdleTimeout 10

