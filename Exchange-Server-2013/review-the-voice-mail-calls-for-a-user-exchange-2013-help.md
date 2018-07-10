---
title: 'Passez en revue les appels de messagerie vocale pour un utilisateur: Exchange 2013 Help'
TOCTitle: Passez en revue les appels de messagerie vocale pour un utilisateur
ms:assetid: 95768fe3-3ae2-43bd-9cbf-18c3b85c4592
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ659070(v=EXCHG.150)
ms:contentKeyID: 50555455
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Passez en revue les appels de messagerie vocale pour un utilisateur

 

_**Sapplique à :** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2013-02-22_

Les journaux des appels des utilisateurs permettent de consulter les informations suivantes concernant des utilisateurs spécifiques de la messagerie unifiée :

  - Détails sur les appels de messagerie unifiée pour un utilisateur au cours des 90 derniers jours.

  - Qualité audio de chaque appel. Les mesures de qualité audio peuvent ne pas être disponibles pour tous les appels, parce que ces mesures dépendent de plusieurs facteurs, tels que le type et la durée de l'appel.

Pour d'autres tâches relatives aux rapports de messagerie unifiée, consultez la rubrique [Procédures de rapports de messagerie unifiée](um-reports-procedures-exchange-2013-help.md).

## Comment recevoir des journaux d'appel pour un utilisateur à extension messagerie unifiée ?

1.  Dans le Centre d’administration Exchange (EAC), sélectionnez **Messagerie unifiée**\> **Autres options**![Icône Options supplémentaires](images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif "Icône Options supplémentaires") \> **Journaux des appels des utilisateurs**.

2.  Cliquez sur **Sélectionner un utilisateur**, puis sélectionnez l’utilisateur pour lequel vous voulez les données.

3.  Pour obtenir plus de détails sur la qualité audio pour une ligne du rapport, sélectionnez la ligne et cliquez sur **Détails de la qualité audio**. Pour plus d'informations sur l'interprétation de la qualité audio, consultez la rubrique [Étude de la qualité audio des appels vocaux pour un utilisateur](investigate-the-audio-quality-of-voice-calls-for-a-user-exchange-2013-help.md).

4.  Pour copier le rapport dans le Presse-papiers, cliquez sur **Copier toutes les lignes dans le Presse-papiers.**

## Comment interpréter le journal des appels d'utilisateur de messagerie unifiée ?

Le journal d'appels de l'utilisateur inclut les informations suivantes pour chaque appel:

  - **DATE ET HEURE** Les date et heure de l’appel, dans le fuseau horaire que l’utilisateur sélectionné a défini dans Microsoft Outlook Web App.

  - **DURÉE** Durée de l’appel, en minutes (MM) et secondes (SS) dans le format suivant : MM:SS.

  - **TYPE D’APPEL   **Le type d’appel :
    
      - **Répondeur automatique**   L’appel n’a pas obtenu de réponse et a été transféré aux serveurs de boîtes aux lettres, et l’appelant a laissé un message vocal.
    
      - **Appel manqué du répondeur automatique**   L’appel n’a pas obtenu de réponse et a été transféré aux serveurs de boîtes aux lettres, sans que l’appelant ne laisse de message vocal.
    
      - **Accès abonné**   Un appel a été effectué vers le numéro d’accès abonné. L’appelant s’est connecté et a été authentifié auprès de la messagerie unifiée grâce à son poste et son mot de passe pour accéder aux messages électroniques, aux calendriers et aux messages vocaux par le téléphone.
    
      - **Standard automatique**   L’appel a abouti sur un standard automatique de messagerie unifiée. Ces appels sont en général des appels pour lesquels l'appelant a composé le numéro de téléphone principal de votre organisation.
    
      - **Télécopie**   Appel pour lequel une tonalité de télécopie a été détectée. Si vous avez configuré des partenaires de télécopie, cet appel a été transféré au partenaire.
    
      - **Émettre au téléphone**   Appel passé par la messagerie unifiée parce que l’utilisateur a cliqué sur le bouton Émettre au téléphone dans un message vocal de Microsoft Outlook Web App ou Outlook.
    
      - **Me localiser**   Appel sortant passé par la messagerie unifiée comme résultat d’une règle Me localiser dans une règle de répondeur automatique aux appels.
    
      - **Numéro pilote non authentifié**   Appel effectué vers le numéro Outlook Voice Access. L'appelant ne s'est pas connecté et n'a pas été authentifié.
    
      - **Enregistrement des messages d'accueil**   Appel passé par la messagerie unifiée pour enregistrer des messages d'accueil personnels pour un utilisateur.
    
      - **Aucun**   Appel passé mais dont le type n'a pas été défini.

  - **NUMÉRO APPELANT** Le numéro de téléphone ou l’adresse SIP de l’appelant.

  - L’appel **NUMÉRO APPELÉ** Le numéro de téléphone ou l’adresse SIP (pour les utilisateurs figurant dans des plans de numérotation SIP, comme les utilisateurs de Microsoft Office Communications Server 2007 R2 ou de Microsoft Lync Server) du destinataire visé par l’appel.

  - **PASSERELLE IP DE MESSAGERIE UNIFIÉE** La passerelle IP de messagerie unifiée qui a pris l’appel.

  - **QUALITÉ AUDIO** La qualité audio globale de l’appel. Pour plus d’informations sur la qualité audio, sélectionnez la ligne et cliquez sur **Détails de la qualité audio**.

