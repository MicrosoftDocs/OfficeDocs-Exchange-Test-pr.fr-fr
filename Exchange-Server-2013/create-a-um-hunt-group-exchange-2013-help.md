---
title: 'Créer un groupement de postes de messagerie unifiée: Exchange 2013 Help'
TOCTitle: Créer un groupement de postes de messagerie unifiée
ms:assetid: 43ecb1ec-5f82-4516-9010-de8f954d3758
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Aa997679(v=EXCHG.150)
ms:contentKeyID: 50555386
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.Servers.UnifiedMessaging.CreateUMHuntGroupWizardForm.CreateUMHuntGroupWizardPage1
ms.translationtype: MT
---

# Créer un groupement de postes de messagerie unifiée

 

_**Sapplique à :** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2013-04-16_

Un groupement de postes de messagerie unifiée est une représentation logique d'un groupement de postes PBX (Private Branch eXchange) ou PBX IP. Un groupement de postes de messagerie unifiée sert de connexion ou de lien entre une passerelle IP de messagerie unifiée et un plan de numérotation de messagerie unifiée.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Si vous associez un plan de numérotation de messagerie unifiée à la passerelle IP de messagerie unifiée lorsque vous créez une passerelle IP de messagerie unifiée, un groupement de postes de messagerie unifiée est également créé.</td>
</tr>
</tbody>
</table>


<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Si vous voulez modifier les paramètres du groupement de postes de messagerie unifiée, vous devez d'abord supprimer ce dernier, puis en créer un autre doté des paramètres appropriés.</td>
</tr>
</tbody>
</table>


Pour d'autres tâches relatives aux regroupements de postes de messagerie unifiée, consultez la rubrique [Procédures de groupe postes de messagerie unifiée](um-hunt-group-procedures-exchange-2013-help.md).

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : 2 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l'entrée « Groupements de postes de messagerie unifiée » dans la rubrique [Autorisations de messagerie unifiée](unified-messaging-permissions-exchange-2013-help.md).

  - Avant d'exécuter ces procédures, vérifiez qu'un plan de numérotation de messagerie unifiée a été créé. Pour obtenir la procédure détaillée, consultez la rubrique [Créer un plan de numérotation de messagerie unifiée](create-a-um-dial-plan-exchange-2013-help.md).

  - Avant d'exécuter ces procédures, vérifiez qu'une passerelle IP de messagerie unifiée a été créée. Pour obtenir la procédure détaillée, consultez la rubrique [Créer une passerelle IP de messagerie unifiée](create-a-um-ip-gateway-exchange-2013-help.md).

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

## Utiliser le Centre d'administration Exchange (CAE) pour créer un groupement de postes de messagerie unifiée

1.  Dans le Centre d'administration Exchange, accédez à **Messagerie unifiée** \> **Plans de numérotation de messagerie unifiée**. Dans l'affichage Liste, sélectionnez le plan de numérotation de messagerie unifiée à modifier, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

2.  Dans la page **Plan de numérotation de messagerie unifiée**, sous **Groupements de postes de messagerie unifiée**, cliquez sur **Nouveau**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter").

3.  Dans la page **Nouveau groupement de postes de messagerie unifiée**, entrez les informations suivantes :
    
      - **Nom**   Ce champ permet de saisir le nom complet du groupement de postes de messagerie unifiée. Un nom de groupement de postes de messagerie unifiée est requis et doit être unique, mais il est uniquement utilisé à des fins d'affichage dans le CAE et l'environnement de ligne de commande Exchange Management Shell. Si vous voulez modifier le nom d’affichage du groupement de postes après sa création, vous devez d’abord supprimer le groupement de postes existant, puis en créer un autre avec le nom approprié.
        
        Si votre organisation utilise plusieurs groupements de postes, nous vous recommandons d'utiliser des noms significatifs pour ces derniers. La longueur maximale d'un nom de groupement de postes de messagerie unifiée est de 64 caractères pouvant contenir des espaces. Toutefois, il ne peut contenir aucun des caractères suivants : " / \\ \[ \] : ; | = , + \* ? \< \>.
    
      - **Passerelle IP de messagerie unifiée**   Ce champ permet d'indiquer la passerelle IP de messagerie unifiée à utiliser. Cliquez sur **Parcourir** pour sélectionner la passerelle IP de messagerie unifiée, puis sur **OK**.
    
      - **Identificateur de pilote**   Ce champ permet de spécifier une chaîne qui fournit une identification unique de l'identificateur de pilote configuré sur le PBX ou le PBX IP.
        
        Un numéro de poste ou un URI (Uniform Resource Identifier) du protocole SIP (Session Initiated Protocol) peut être utilisé dans ce champ. Les caractères alphanumériques sont acceptés dans ce champ. Pour les PBX hérités, une valeur numérique est utilisée comme identificateur pilote. Toutefois, certains PBX IP peuvent utiliser les URI du protocole SIP.

4.  
    
    Cliquez sur **Enregistrer**.

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour créer un groupement de postes de messagerie unifiée

Cet exemple crée un groupement de postes de messagerie unifiée nommé `MyUMHuntGroup` dont l'identificateur pilote est 12345.

    New-UMHuntGroup -Name MyUMHuntGroup -PilotIdentifier 12345 -UMDialplan MyUMDialPlan -UMIPGateway MyUMIPGateway

Cet exemple crée un groupement de postes de messagerie unifiée nommé `MyUMHuntGroup` ayant plusieurs identificateurs pilotes.

    New-UMHuntGroup -Name MyUMHuntGroup -PilotIdentifier 5551234,55555 -UMDialplan MyUMDialPlan -UMIPGateway MyUMIPGateway

