---
title: 'Configurer les codes de numérotation: Exchange 2013 Help'
TOCTitle: Configurer les codes de numérotation
ms:assetid: e5b5efee-b734-4f70-8357-11be07b23bd0
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb124992(v=EXCHG.150)
ms:contentKeyID: 51407250
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurer les codes de numérotation

 

_**Sapplique à :**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :**2013-02-22_

Vous pouvez configurer des codes de numérotation, des préfixes de numéros et des formats de numéros que la messagerie unifiée utilise pour effectuer des appels entrants et sortants pour des utilisateurs à extension messagerie unifiée. Dans la plupart des cas, vous devrez configurer un plan de numérotation avec les codes de numérotation, les préfixes et les formats de numéros actuellement configurés dans votre réseau téléphonique.

Les codes de numérotation et les préfixes de numéros servent à déterminer le numéro correct à composer dans le cadre d'un appel sortant effectué par un utilisateur à extension messagerie unifiée. L'*automate d'appels* est le terme utilisé pour décrire le processus par lequel un utilisateur dans un plan de numérotation de messagerie unifiée émet un appel sortant. Les formats de numéros servent pour les appels entrants au sein d'un pays ou d'une région, les appels à l'international ou les appels effectués dans un plan de numérotation. Vous pouvez configurer un plan de numérotation de sorte qu'il utilise le format de numéro d'appel entrant pour les numéros nationaux/régionaux et internationaux. Quand vous configurez les formats de numéros nationaux/régionaux et internationaux, vous pouvez limiter les appels entrants pour des utilisateurs associés à un plan de numérotation.

Pour découvrir d'autres tâches de gestion relatives à l'automate d'appels, consultez la rubrique [Ce qui permet aux utilisateurs d'effectuer les procédures d'appels](allowing-users-to-make-calls-procedures-exchange-2013-help.md).

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : moins d'une minute.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l'entrée « Plans de numérotation de messagerie unifiée » dans la rubrique [Autorisations de messagerie unifiée](unified-messaging-permissions-exchange-2013-help.md).

  - Avant d'exécuter ces procédures, vérifiez qu'un plan de numérotation de messagerie unifiée a été créé. Pour obtenir la procédure détaillée, consultez la rubrique [Créer un plan de numérotation de messagerie unifiée](create-a-um-dial-plan-exchange-2013-help.md).

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

## Utiliser le Centre d'administration Exchange (CAE) pour configurer des codes de numérotation, des préfixes et des formats de numéros

1.  Dans le CAE, accédez à **Messagerie unifiée** \> **Plans de numérotation de messagerie unifiée**.

2.  Sélectionnez le plan de numérotation de messagerie unifiée à gérer, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

3.  Dans la page **Plan de numérotation de messagerie unifiée**, cliquez sur **Configurer**.

4.  Dans la page **Plan de numérotation de messagerie unifiée** \> **Codes de numérotation**, configurez les options suivantes :
    
      - **Code d'accès à une ligne extérieure**
    
      - **Code d'accès à l'international**
    
      - **Préfixe du numéro national**
    
      - **Code de pays/région**

5.  Sous **Formats de numéros pour la numérotation entre plans de numérotation**, configurez les options suivantes :
    
      - **Format de numéro de téléphone national**
    
      - **Format de numéro de téléphone international**
    
      - **Formats de numéros pour les appels entrants dans le même plan de numérotation**   Pour ajouter un format de numéro, cliquez sur **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter").

6.  Cliquez sur **Enregistrer** pour enregistrer vos modifications.

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour configurer des codes de numérotation, des préfixes et des formats de numéros

Cet exemple montre comment configurer le plan de numérotation de messagerie unifiée `MyUMDialPlan` avec un format de numéro de téléphone national, un format de numéro de téléphone international et les codes de numérotation suivants :

  - 9 pour le code d'accès à une ligne extérieure

  - 011 pour le code d'accès à l'international

  - 1 pour le préfixe du numéro national

  - 1 pour le code du pays ou de la région

<!-- end list -->

    Set-UMDialPlan -Identity MyUMDialPlan -OutsideLineAccessCode 9 -InternationalAccessCode 011 -NationalNumberPrefix 1 CountryorRegionCode 1 -InCountryOrRegionNumberFormat 1425xxxxxxx -InternationalNumberFormat 441425xxxxxxx

