---
title: "Configurer la durée maximale d'enregistrement: Exchange 2013 Help"
TOCTitle: Configurer la durée maximale d'enregistrement
ms:assetid: 18eeb567-1048-4c82-93cf-612cb12ec5e3
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Ee423539(v=EXCHG.150)
ms:contentKeyID: 50477692
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurer la durée maximale d'enregistrement

 

_**Sapplique à :**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :**2012-11-09_

Vous pouvez spécifier le nombre maximal de minutes autorisé pour chaque enregistrement vocal lorsqu’un appelant laisse un message vocal. Cette valeur peut être définie sur un nombre compris entre 1 et 100. Pour la plupart des organisations, cette valeur doit être définie à la valeur par défaut de 20 minutes. La définition d’une valeur trop basse risque de provoquer la déconnexion de longs messages vocaux avant qu’ils ne soient terminés. La définition d’une valeur trop élevée permet aux utilisateurs d’enregistrer des messages vocaux relativement longs dans leur boîte de réception.

Il s’agit d’un paramètre important si vous avez mis en place des quotas de disque stricts pour les utilisateurs. Elle doit être inférieure à celle définie pour **Durée d’appel maximale (minutes)**.

Pour les autres tâches relatives aux plans de numérotation de messagerie unifiée, voir [Procédures de plan de numérotation de messagerie unifiée](um-dial-plan-procedures-exchange-2013-help.md).

## Ce qu’il faut savoir avant de commencer ?

  - Durée d'exécution estimée : Moins d’une minute.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Plans de numérotation de messagerie unifiée » dans la rubrique [Autorisations de messagerie unifiée](unified-messaging-permissions-exchange-2013-help.md).

  - Avant d’exécuter ces procédures, vérifiez qu’un plan de numérotation de messagerie unifiée a été créé. Pour obtenir la procédure détaillée, consultez la rubrique [Créer un plan de numérotation de messagerie unifiée](create-a-um-dial-plan-exchange-2013-help.md).

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


## Que souhaitez-vous faire ?

## Utiliser le Centre d’administration Exchange pour configurer la durée d’enregistrement maximale

1.  Dans le Centre d’administration Exchange, accédez à **Messagerie unifiée** \> **Plans de numérotation de messagerie unifiée**.

2.  Dans la liste affichée, sélectionnez le plan de numérotation de messagerie unifiée que vous souhaitez modifier, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

3.  Dans la page **Plan de numérotation de messagerie unifiée**, cliquez sur **Configurer**.

4.  Dans **Paramètres**, sous **Durée d’enregistrement maximale (minutes)**, entrez un nombre en minutes.

5.  Cliquez sur **Enregistrer**.

## Utiliser l’environnement de ligne de commande Exchange Management Shell pour configurer la durée d’enregistrement maximale

Cet exemple définit la durée d’appel maximale sur 10 minutes pour un plan de numérotation de messagerie unifiée appelé `MyUMDialPlan`.

    Set-UMDialPlan -identity MyUMDialPlan -MaxRecordingDuration 10

