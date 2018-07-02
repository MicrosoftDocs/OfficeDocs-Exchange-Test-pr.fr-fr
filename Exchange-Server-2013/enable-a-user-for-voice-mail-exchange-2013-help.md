---
title: 'Activation de la messagerie vocale pour un utilisateur: Exchange 2013 Help'
TOCTitle: Activation de la messagerie vocale pour un utilisateur
ms:assetid: ad027767-5e14-4cb1-9f8a-0791d9188db5
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb124147(v=EXCHG.150)
ms:contentKeyID: 50478862
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.Recipients.EnableUnifiedMessagingWizardForm.EnableUnifiedMessagingWizardPage
ms.translationtype: HT
---

# Activation de la messagerie vocale pour un utilisateur

 

_**Sapplique à :**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :**2013-02-22_

Quand vous activez la messagerie unifiée pour un utilisateur, un ensemble par défaut de propriétés est appliqué à l'utilisateur pour lui permettre d'utiliser les fonctionnalités de messagerie vocale incluses dans la messagerie unifiée. Après avoir activé la messagerie vocale pour un utilisateur, vous avez la possibilité d'ajouter une adresse SIP (Session Initiation Protocol) pour l'utilisateur si une stratégie de boîte aux lettres de messagerie unifiée liée à un plan de numérotation URI SIP lui a été attribuée. Vous pouvez aussi ajouter un numéro E.164 pour l'utilisateur si une stratégie de boîte aux lettres de messagerie unifiée liée à un plan de numérotation E.164 lui a été attribuée. Dans les deux cas, un numéro de poste doit être configuré pour l'utilisateur.

Un numéro de poste est requis pour chaque utilisateur associé à un plan de numérotation de numéro de poste, URI (Uniform Resource Identifier) SIP ou E.164. Le numéro de poste doit comporter le nombre correct de chiffres, conformément aux spécifications du plan de numérotation de messagerie unifiée pour la stratégie de boîte aux lettres de messagerie unifiée.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Vous devez ajouter, supprimer ou modifier des numéros de poste pour tous les utilisateurs à extension messagerie unifiée via le CAE ou l'environnement de ligne de commande Exchange Management Shell, même s'ils sont associés à un URI SIP ou à un plan de numérotation E.164. Pour ajouter, supprimer ou modifier des adresses SIP ou des numéros E.164 pour des utilisateurs, vous devez utiliser l'environnement de ligne de commande Exchange Management Shell, car ces options ne sont pas disponibles dans le CAE.</td>
</tr>
</tbody>
</table>


Pour les autres tâches de gestion relatives aux utilisateurs à extension messagerie vocale, consultez la rubrique [Voix des procédures de l'utilisateur à extension messagerie](voice-mail-enabled-user-procedures-exchange-2013-help.md).

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : 5 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Boîtes aux lettres de messagerie unifiée » dans la rubrique [Autorisations de messagerie unifiée](unified-messaging-permissions-exchange-2013-help.md).

  - Avant d'exécuter ces procédures, vérifiez qu'un plan de numérotation de messagerie unifiée a été créé. Pour obtenir la procédure détaillée, consultez la rubrique [Créer un plan de numérotation de messagerie unifiée](create-a-um-dial-plan-exchange-2013-help.md).

  - Avant d'effectuer ces procédures, vérifiez qu'une stratégie de boîte aux lettres de messagerie unifiée a été créée. Pour obtenir la procédure détaillée, consultez la rubrique [Créer une stratégie de boîte aux lettres de messagerie unifiée](create-a-um-mailbox-policy-exchange-2013-help.md).

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

## Utiliser le CAE afin d'activer la messagerie vocale pour un utilisateur

1.  Dans le CAE, cliquez sur **Destinataires**.

2.  Dans l'affichage Liste, sélectionnez l'utilisateur possédant la boîte aux lettres pour laquelle vous souhaitez activer la messagerie unifiée.

3.  Dans le volet d'informations, sous **Fonctionnalités téléphoniques et vocales**, cliquez sur **Activer**.

4.  Dans la page **Activer la boîte aux lettres de messagerie unifiée**, cliquez sur le bouton **Parcourir** à côté de **Stratégie de boîte aux lettres de messagerie unifiée**, localisez la stratégie à attribuer à l'utilisateur dans la liste, puis cliquez sur **OK**.

5.  Dans la page **Activer la boîte aux lettres de messagerie unifiée**, complétez les champs suivants :
    
      - **Adresse SIP** ou **Numéro E.164**   Dans la zone de texte **Adresse SIP** ou **Numéro E.164**, entrez l'adresse SIP ou le numéro E.164 pour l'utilisateur. Ces options sont disponibles si l'utilisateur pour lequel vous activez la messagerie unifiée est associé à une stratégie de boîte aux lettres de messagerie unifiée liée à un URI SIP ou à un plan de numérotation E.164. Vous ne pouvez pas ajouter d'adresse SIP ou de numéro E.164 à un utilisateur si ce dernier est associé à plan de numérotation de poste téléphonique.
        
        Lorsque vous associez l'utilisateur à une stratégie de boîte aux lettres de messagerie unifiée liée à un URI SIP ou à un plan de numérotation E.164, vous devez entrer un numéro de poste pour l'utilisateur. L'utilisateur utilise ce numéro de poste lorsqu'il accède à sa boîte aux lettres via Outlook Voice Access. Le nombre de chiffres que vous configurez dans ce champ doit correspondre au nombre de chiffres configurés pour l'URI SIP ou le plan de numérotation E.164.
    
      - **Numéro de poste**   Cette zone de texte vous permet d'entrer manuellement le numéro de poste de l'utilisateur dont vous activez la messagerie unifiée.
        
        Vous devez indiquer un numéro de poste valide pour l'utilisateur, c'est-à-dire que le numéro doit comporter le nombre de chiffres indiqué dans le plan de numérotation. Vous pouvez entrer uniquement des chiffres compris entre 1 et 20. Un numéro de poste classique compte entre 3 et 7 chiffres. Le nombre de chiffres du poste est défini dans le plan de numérotation associé à la stratégie de boîte aux lettres de messagerie unifiée attribuée à l'utilisateur.
    
      - Sous **Paramètres du code confidentiel**, procédez comme suit :
        
          - **Générer automatiquement un code confidentiel**   Cliquez sur ce bouton pour générer automatiquement un code confidentiel pour l'utilisateur à extension messagerie unifiée, qu'il utilisera pour accéder à la messagerie vocale via Outlook Voice Access. Il s'agit du paramètre par défaut. Le code confidentiel est automatiquement généré d'après les stratégies de code confidentiel configurées dans la stratégie de boîte aux lettres de messagerie unifiée attribuée à l'utilisateur. L'utilisation de ce paramètre permet de protéger le code confidentiel de l'utilisateur. Le code confidentiel est envoyé à l'utilisateur dans le message d'accueil qu'il reçoit après avoir été activé pour la messagerie unifiée. Par défaut, il devra modifier ce code confidentiel lorsqu'il se connecte pour la première fois à sa boîte aux lettres pour accéder à sa messagerie vocale.
        
          - **Taper un code confidentiel**   Cliquez sur ce bouton pour entrer un code confidentiel dont se servira l'utilisateur pour accéder au système de messagerie vocale. Le code confidentiel doit être conforme aux paramètres de stratégie de code confidentiel configurés dans la stratégie de boîte aux lettres de messagerie unifiée associée à cet utilisateur à extension messagerie. Par exemple, si la stratégie de boîte aux lettres de messagerie unifiée est configurée pour accepter uniquement les codes confidentiels contenant au moins sept chiffres, le code confidentiel entré dans ce champ doit comporter au moins sept chiffres.
        
          - **Exiger que l'utilisateur réinitialise son code confidentiel à sa première connexion**   Activez cette case à cocher pour obliger l'utilisateur à réinitialiser son code confidentiel de messagerie vocale quand il accède pour la première fois au système de messagerie vocale à partir d'un téléphone via Outlook Voice Access. Il sera invité à saisir un code confidentiel avec lequel il est davantage familiarisé. Cette recommandation en matière de sécurité contraint les utilisateurs à extension messagerie unifiée à modifier leur code confidentiel lorsqu'ils se connectent pour la première fois pour se protéger contre les accès autorisés à leurs données et à leur boîte de réception. Cette case à cocher est activée par défaut.

6.  Dans la page **Activer la boîte aux lettres de messagerie unifiée**, révisez vos paramètres. Pour activer la messagerie vocale pour l'utilisateur, cliquez sur **Terminer**. Cliquez sur **Précédent** pour apporter des modifications de configuration.

## Utiliser l'environnement de ligne de commande Exchange Management Shell afin d'activer la messagerie vocale pour un utilisateur

Dans cet exemple, la messagerie unifiée est activée sur la boîte aux lettres de tonysmith@contoso.com, le numéro de poste est défini (51234), le code confidentiel est défini pour l'utilisateur (5643892) et la stratégie de boîte aux lettres de messagerie unifiée `MyUMMailboxPolicy` est attribuée à l'utilisateur.

    Enable-UMMailbox -Identity tonysmith@contoso.com -UMMailboxPolicy MyUMMailboxPolicy -Extensions 51234 -PIN 5643892 -PINExpired $true

Dans cet exemple, la messagerie unifiée est activée sur la boîte aux lettres tonysmith@contoso.com, une stratégie de boîte aux lettres de messagerie unifiée `MyUMMailboxPolicy` est attribuée à l'utilisateur et le numéro de poste, l'adresse SIP et le code confidentiel sont définis pour l'utilisateur.

    Enable-UMMailbox -Identity tonysmith@contoso.com -UMMailboxPolicy MyUMMailboxPolicy -Extensions 51234 -PIN 5643892 -SIPResourceIdentifier "tonysmith@contoso.com" -PINExpired $true

