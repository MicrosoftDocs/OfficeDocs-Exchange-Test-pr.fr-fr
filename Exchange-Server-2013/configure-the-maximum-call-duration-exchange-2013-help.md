---
title: 'Configurer la durée d’appel maximale: Exchange 2013 Help'
TOCTitle: Configurer la durée d’appel maximale
ms:assetid: 01aa40d2-f918-472b-bace-158222143484
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Ee423535(v=EXCHG.150)
ms:contentKeyID: 50477422
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurer la durée d’appel maximale

 

_**Sapplique à :** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2012-11-09_

Vous pouvez spécifier le nombre maximal de minutes correspondant à la durée pendant laquelle un appel entrant peut être connecté au système sans être transféré à un numéro de poste valide avant qu’il ne soit mis fin à l’appel. Pour la plupart des organisations, cette valeur doit être définie par défaut sur:  30 minutes. Ce paramètre s’applique à tous les appels, y compris les appels entrants Outlook Voice Access, les appels vocaux internes à l’organisation, les appels vocaux transitant par les standards automatiques de messagerie unifiée et les appels de télécopie externes.

La valeur de ce paramètre est comprise entre 10 et 120. La définition d’une valeur trop basse peut entraîner la déconnexion des appels entrants avant que ceux-ci ne soient terminés. Par exemple, si votre organisation reçoit régulièrement des messages de télécopie volumineux, vous pouvez envisager de définir une valeur plus élevée que la valeur par défaut, de façon à recevoir toutes les pages des messages de télécopie.

Pour les autres tâches relatives aux plans de numérotation de messagerie unifiée, voir [Procédures de plan de numérotation de messagerie unifiée](um-dial-plan-procedures-exchange-2013-help.md).

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : moins d'une minute.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Plans de numérotation de messagerie unifiée » dans la rubrique [Autorisations de messagerie unifiée](unified-messaging-permissions-exchange-2013-help.md).

  - Avant d'exécuter ces procédures, vérifiez qu'un plan de numérotation de messagerie unifiée a été créé. Pour obtenir la procédure détaillée, consultez la rubrique [Créer un plan de numérotation de messagerie unifiée](https://docs.microsoft.com/fr-fr/exchange/voice-mail-unified-messaging/connect-voice-mail-system/create-um-dial-plan).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..


## Que souhaitez-vous faire ?

## Utiliser le Centre d’administration Exchange pour configurer la durée d’appel maximale

1.  Dans le Centre d’administration Exchange, accédez à **Messagerie unifiée** \> **Plans de numérotation de messagerie unifiée**.

2.  Dans l'affichage Liste, sélectionnez le plan de numérotation de messagerie unifiée à modifier, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

3.  Dans la page **Plan de numérotation de messagerie unifiée**, cliquez sur **Configurer**.

4.  Dans **Paramètres**, sous **Durée d’appel maximale (minutes)**, entrez un nombre en minutes.

5.  Cliquez sur **Enregistrer**.

## Utiliser l’environnement de ligne de commande Exchange Management Shell pour modifier la durée d’appel maximale

Cet exemple définit la durée d’appel maximale sur 10 minutes pour un plan de numérotation de messagerie unifiée appelé `MyUMDialPlan`.

    Set-UMDialPlan -identity MyUMDialPlan -MaxCallDuration 10

