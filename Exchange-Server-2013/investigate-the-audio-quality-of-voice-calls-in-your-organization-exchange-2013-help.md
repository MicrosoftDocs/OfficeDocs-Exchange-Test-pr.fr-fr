---
title: "Examiner la qualité audio d'appels vocaux au sein de votre organisation: Exchange 2013 Help"
TOCTitle: Examiner la qualité audio d'appels vocaux au sein de votre organisation
ms:assetid: 8a87694b-1678-4a01-859f-5ad3b2c73db5
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ659069(v=EXCHG.150)
ms:contentKeyID: 50555430
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Examiner la qualité audio d'appels vocaux au sein de votre organisation

 

_**Sapplique à :** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2013-02-21_

Si votre organisation rencontre des problèmes avec la qualité audio des appels de messagerie unifiée et des messages vocaux, utilisez le rapport Statistiques d'appels pour vous aider à comprendre ce qui provoque les problèmes.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>La qualité audio d'un appel peut être affectée par des facteurs qui ne sont pas couverts dans les rapports. Par exemple, si vos serveurs Exchange rencontrent une charge élevée de mémoire ou d'unité centrale, les utilisateurs peuvent signaler une qualité d'appel médiocre même si les rapports indiquent une qualité audio excellente.</td>
</tr>
</tbody>
</table>


Pour les tâches supplémentaires relatives aux statistiques d'appels, consultez la rubrique [Procédures de rapports de messagerie unifiée](um-reports-procedures-exchange-2013-help.md).

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : 3 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l'entrée « Données d'appel de messagerie unifiée et cmdlets de rapport de synthèse » dans la rubrique [Autorisations de messagerie unifiée](unified-messaging-permissions-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

<table>
<thead>
<tr class="header">
<th><img src="images/Bb125224.tip(EXCHG.150).gif" title="Conseil" alt="Conseil" />Conseil :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..</td>
</tr>
</tbody>
</table>


## Utiliser le Centre d'administration Exchange (CAE) pour récupérer des statistiques relatives à la qualité audio pour votre organisation

1.  Dans le CAE, accédez à **Messagerie unifiée **\> **Autres options**![Icône Options supplémentaires](images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif "Icône Options supplémentaires") \> **Statistiques d'appels**.

2.  Sélectionnez les statistiques d'appels à inclure dans le rapport. Le rapport se met à jour automatiquement lorsque vous activez une des options suivantes.
    
      - **Afficher **  Choisissez le type de statistiques d'appels à afficher :
        
          - **Quotidiennement (90 jours)** Sélectionnez Quotidiennement pour consulter les détails de tous les appels traités au cours des 90 derniers jours.
        
          - **Mensuellement (12 mois)**   Sélectionnez Mensuellement pour consulter un résumé d'appels par mois pour les 12 derniers mois.
        
          - **Tout**   Sélectionnez Tout pour consulter les statistiques combinées de tous les appels reçus depuis que la messagerie unifiée a commencé à gérer les appels.
    
      - **Plan de numérotation de messagerie unifiée**   Si vous souhaitez limiter les données dans le rapport aux appels dans un plan de numérotation de messagerie unifiée spécifique, sélectionnez ce plan de numérotation.
    
      - **Passerelle IP de messagerie unifiée**   Si vous souhaitez limiter les données dans le rapport aux appels dans une passerelle IP de messagerie unifiée spécifique, sélectionnez cette passerelle IP de messagerie unifiée. Si vous sélectionnez d'abord un plan de numérotation de messagerie unifiée, seules les passerelles IP de messagerie unifiée associées au plan de numérotation de messagerie unifiée sélectionné sont disponibles dans la liste.

3.  Pour obtenir plus de détails sur la qualité audio pour une ligne du rapport, sélectionnez la ligne et cliquez sur **Détails de la qualité audio**. Les informations suivantes sont disponibles :
    
      - **DATE ET HEURE**   Date et heure, au format de temps universel coordonné, de capture des statistiques d'appels.
    
      - **PLAN DE NUMÉROTATION DE MESSAGERIE UNIFIÉE**   Plan de numérotation pour les appels inclus dans les statistiques.
    
      - **PASSERELLE IP DE MESSAGERIE UNIFIÉE**   Passerelle IP de messagerie unifiée qui a pris les appels inclus dans les statistiques.
    
      - **NMOS**   Note moyenne d'opinion de réseau NMOS pour cet appel. Le score NMOS évalue la qualité audio de l'appel, sur une échelle de 1 à 5, 5 indiquant une excellente qualité.
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>La note NMOS maximale pour un appel dépend du codec audio utilisé. Il est possible que le score NMOS ne soit pas disponible pour des appels très courts d'une durée inférieure à 10 secondes.</td>
        </tr>
        </tbody>
        </table>
    
      - **DÉGRADATION NMOS**   Niveau de dégradation audio du score NMOS, à partir de la valeur la plus élevée possible pour le codec audio utilisé. Par exemple, si la valeur de dégradation NMOS d'un appel est égale à 1,2 et que le score NMOS signalé de l'appel est égal à 3,3, le score NMOS maximal de cet appel en particulier est de 4,5 (1,2 + 3,3).
    
      - **INSTABILITÉ**   Variation moyenne de l'arrivée des paquets de données pour un appel.
    
      - **PERTE DE PAQUETS**   Pourcentage moyen de la perte de paquets de données pour l'appel sélectionné. La perte de paquets est une indication de la fiabilité de la connexion.
    
      - **ALLER-RETOUR**   Durée moyenne d'aller-retour, en millisecondes, de l'audio pour l'appel sélectionné. Le score d'aller-retour mesure la latence de la connexion.
    
      - **DURÉE DE PERTE DE TRANSMISSION EN RAFALE**   Durée moyenne de perte de paquets pendant les rafales de pertes pour l'appel sélectionné.
    
      - **NOMBRE D'EXEMPLES**   Nombre d'appels échantillonnés pour calculer les moyennes.

4.  Pour des mesures détaillées de la qualité audio concernant des appels spécifiques, consultez la rubrique [Étude de la qualité audio des appels vocaux pour un utilisateur](investigate-the-audio-quality-of-voice-calls-for-a-user-exchange-2013-help.md).

