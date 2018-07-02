---
title: 'Passez en revue les appels de messagerie vocale dans votre organisation: Exchange 2013 Help'
TOCTitle: Passez en revue les appels de messagerie vocale dans votre organisation
ms:assetid: f6fdbe17-d1d2-442a-aa13-06b908d9c33a
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ659073(v=EXCHG.150)
ms:contentKeyID: 50555521
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Passez en revue les appels de messagerie vocale dans votre organisation

 

_**Sapplique à :** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2013-02-22_

Vous pouvez utiliser le rapport statistiques d'appel pour afficher des informations sur le type et le statut des appels entrants gérés par les serveurs Exchange de votre organisation. Le rapport fournit des informations statistiques sur les appels transférés vers ou passés par la messagerie unifiée (MU) pour votre organisation. Vous pouvez utiliser ces informations pour effectuer le suivi de l'utilisation pour la planification de la capacité, surveiller et dépanner la disponibilité et la qualité audio de la messagerie unifiée et à résoudre les problèmes d'appels ayant échoué.

Cette rubrique répond à ces questions :

  - How do I get call statistics for UM?

  - How do I interpret UM call statistics?

Pour d'autres tâches relatives aux rapports de messagerie unifiée, consultez la rubrique [Procédures de rapports de messagerie unifiée](um-reports-procedures-exchange-2013-help.md).

## Comment obtenir des statistiques d'appels pour la messagerie unifiée ?

1.  Dans le Centre d'administration Exchange (CAE), cliquez sur **Messagerie unifiée** \> **Plus d'options**![Icône Options supplémentaires](images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif "Icône Options supplémentaires") \> **Statistiques d'appels**.

2.  Choisissez les informations que vous souhaitez inclure dans le rapport. Le rapport se met à jour automatiquement lorsque vous sélectionnez une des options suivantes :
    
      - **Afficher**  Choisissez le type de statistiques d'appels à afficher :
        
          - **Quotidiennement (90 jours)**   Sélectionnez Quotidiennement pour consulter les détails de tous les appels traités au cours des 90 derniers jours.
        
          - **Mensuellement (12 mois)**   Sélectionnez Mensuellement pour consulter un résumé d'appels par mois pour les 12 derniers mois.
        
          - **Tout**   Sélectionnez Tout pour consulter les statistiques combinées de tous les appels reçus depuis que la messagerie unifiée a commencé à gérer les appels.
    
      - **Plan de numérotation de messagerie unifiée**   Si vous souhaitez limiter les données dans le rapport aux appels dans un plan de numérotation de messagerie unifiée spécifique, sélectionnez ce plan de numérotation.
    
      - **Passerelle IP de messagerie unifiée**   Si vous souhaitez limiter les données dans le rapport aux appels dans une passerelle IP de messagerie unifiée spécifique, sélectionnez cette passerelle. Si vous sélectionnez d'abord un plan de numérotation de messagerie unifiée, seules les passerelles IP de messagerie unifiée associées au plan de numérotation de messagerie unifiée sélectionné sont disponibles dans la liste.

3.  Pour obtenir plus d'informations sur la qualité audio d'une ligne dans le rapport, sélectionnez la ligne, puis cliquez sur **Détails de la qualité Audio**. Pour plus d'informations sur la façon d'interpréter la qualité audio, voir [Examiner la qualité audio d'appels vocaux au sein de votre organisation](investigate-the-audio-quality-of-voice-calls-in-your-organization-exchange-2013-help.md).

4.  Pour copier le rapport vers le Presse-papiers, cliquez sur **Copier**.

5.  Pour des rapports quotidiens, vous pouvez exporter les détails pour un jour spécifique vers un fichier .csv.
    
    1.  Sélectionnez le jour, puis cliquez sur **Jour d'exportation**.
    
    2.  Dans la zone de confirmation **Téléchargement de fichier**, cliquez sur **Ouvrir** ou **Enregistrer**.
    
    Le fichier exporté sera nommé um\_cdr\_*YYYY-MM-DD*.csv, où *YYYY-MM-DD* est l'année, mois et jour que le rapport a été exécuté. Pour plus d'informations, voir [Interpréter les enregistrements d'appel de messagerie vocale](interpret-voice-mail-call-records-exchange-2013-help.md).
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Dans la page du rapport, vous pouvez télécharger un modèle Microsoft Excel qui vous servira à importer le fichier .csv d'un jour spécifique.</td>
    </tr>
    </tbody>
    </table>


Retour au début

## Comment interpréter les statistiques d'appels de messagerie unifiée ?

Le rapport des statistiques d'appels de messagerie unifiée inclut les informations suivantes :

  - **DATE**   La date au format UTC pour les données d'appel. Le format de date dépend du type de rapport que vous avez choisi et vos paramètres régionaux. Vous pouvez choisir parmi les options suivantes :
    
      - **--- **  Tous les appels sont affichés.
    
      - **MMM/AA**   Le mois des appels. Par exemple, Jan/13.
    
      - **MM/jj/aa**   Le jour des appels. Par exemple, 13/23/6.

  - **TOTAL**   Le nombre total d'appels pour le plan de numérotation de messagerie unifiée ou la passerelle IP de messagerie unifiée sélectionnée pour cette date.

  - **MESSAGE VOCAL**   Le pourcentage d'appels entrants répondus par la messagerie unifiée pour le compte des utilisateurs et au cours desquels les appelants ont laissé un message vocal.

  - **MANQUÉS**   Le pourcentage d'appels entrants auxquels la messagerie unifiée a répondu pour le compte des utilisateurs et pour lesquels les appelants n'ont laissé aucun message, ce qui a abouti à une notification d'appel en absence.

  - **OUTLOOK VOICE ACCESS**   Le pourcentage d'appels entrants au cours desquels les utilisateurs se sont connectés à la messagerie unifiée (et ont été authentifiés) pour accéder à leurs messagerie électronique, calendriers et messages vocaux.

  - **Sortant**   Pourcentage d'appels qui ont été placés ou transférés par la messagerie unifiée pour le compte d'utilisateurs authentifiés ou non authentifiés. Cette statistique inclut trouver Me, émettre au téléphone et lire sur les types d'appels téléphoniques le message d'accueil.

  - **STANDARD AUTOMATIQUE**   Le pourcentage des appels entrants traités par les standards automatiques de messagerie unifiée.

  - **TÉLÉCOPIE**   Le pourcentage des appels entrants qui ont été redirigés vers un partenaire de télécopie.

  - **Autres**   Pourcentage de n'importe quel autres appels entrants ou placés qui ne rentrent pas dans une des catégories définies ci-dessus. Ces appels sont les appels passés aux numéros d'Outlook Voice Access où les utilisateurs n'a pas se connecter et n'ont pas été authentifiées.

  - **Échec ou rejeté**   Pourcentage d'appels qui a échoué ou qui ont été rejetés par la messagerie unifiée. Notez que les appels ayant échoué ne sont pas comptées deux fois. Par exemple, si un appel à Outlook Voice Access échoue, elle est comptabilisée uniquement sous la forme d'un appel a échoué et pas également un appel d'Outlook Voice Access.

  - **QUALITÉ AUDIO**   Une représentation graphique de la qualité audio globale pour la période sélectionnée de l'organisation.

Retour au début

## Pour plus d'informations

[Examiner la qualité audio d'appels vocaux au sein de votre organisation](investigate-the-audio-quality-of-voice-calls-in-your-organization-exchange-2013-help.md)

[Interpréter les enregistrements d'appel de messagerie vocale](interpret-voice-mail-call-records-exchange-2013-help.md)

