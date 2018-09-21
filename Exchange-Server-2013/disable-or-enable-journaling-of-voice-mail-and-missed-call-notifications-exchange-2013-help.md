---
title: 'Désactiver/activer journ. des notif. d’appel en absence et de la messag. voc.'
TOCTitle: Désactiver ou activer la journalisation des notifications d’appel en absence et de la messagerie vocale
ms:assetid: 5164a92e-69e6-4339-b80c-0cfbf0dc0198
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb201690(v=EXCHG.150)
ms:contentKeyID: 50478185
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Désactiver ou activer la journalisation des notifications d’appel en absence et de la messagerie vocale

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2015-04-08_

Dans Microsoft Exchange Server 2013, lorsque vous créez une règle de journal sur les messages électroniques échangés entre des destinataires et des expéditeurs dans une organisation Exchange, les notifications d’appel en absence ou de la messagerie vocale générées par le service de messagerie unifiée sont incluses. Utilisez les procédures de la présente rubrique pour activer ou désactiver cette fonction pour votre organisation en entier.

Souhaitez-vous rechercher les autres tâches de gestion relatives à la journalisation ? Consultez la rubrique [Gérer la journalisation](https://docs.microsoft.com/fr-fr/exchange/security-and-compliance/journaling/manage-journaling).

## Ce qu’il faut savoir avant de commencer ?

  - Durée d'exécution estimée : 5 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Journalisation » dans la rubrique [Stratégie de messagerie et autorisations de conformité](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

  - Vous pouvez uniquement utiliser l'environnement de ligne de commande Exchange Management Shell pour effectuer cette tâche.

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.


## Utilisez le Shell pour désactiver ou activer la journalisation des messages vocaux et des notifications d’appel en absence

Cet exemple illustre la désactivation de la journalisation des messages vocaux et des notifications d’appel en absence via le réglage du paramètre *VoicemailJournalingEnabled* sur la valeur `$false`.

    Set-TransportConfig -VoicemailJournalingEnabled $false

Cet exemple illustre l’activation de la journalisation des messages vocaux et des notifications d’appel en absence via le réglage du même paramètre sur `$true`.

    Set-TransportConfig -VoicemailJournalingEnabled $true

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Set-TransportConfig](https://technet.microsoft.com/fr-fr/library/bb124151\(v=exchg.150\)).

## Pour plus d’informations

[Journalisation](journaling-exchange-2013-help.md)

[Gérer la journalisation](https://docs.microsoft.com/fr-fr/exchange/security-and-compliance/journaling/manage-journaling)

