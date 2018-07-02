---
title: "Réinitialisation d'un code confidentiel de messagerie vocale: Exchange 2013 Help"
TOCTitle: Réinitialisation d'un code confidentiel de messagerie vocale
ms:assetid: bf07e6e7-01d2-4933-bff5-c615cc21a480
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb124404(v=EXCHG.150)
ms:contentKeyID: 50555475
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.Recipients.ResetUnifiedMessagingPinPropertyControl
ms.translationtype: HT
---

# Réinitialisation d'un code confidentiel de messagerie vocale

 

_**Sapplique à :** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2013-02-22_

Lorsqu'un utilisateur de messagerie vocale à extension messagerie unifiée voit sa boîte aux lettres verrouillée sous Outlook Voice Access parce qu'il a tenté plusieurs fois de se connecter à l'aide d'un code confidentiel incorrect ou qu'il l'a oublié, vous pouvez utiliser l'une des procédures suivantes pour réinitialiser le code confidentiel de l'utilisateur. Lors de la réinitialisation du code confidentiel Outlook Voice Access d'un utilisateur, vous pouvez configurer la messagerie unifiée de manière à ce qu'elle génère automatiquement un code confidentiel, ou le spécifier manuellement. Le nouveau code confidentiel est envoyé à l'utilisateur par courrier électronique. Vous pouvez spécifier des options de code confidentiel supplémentaires, comme exiger que l'utilisateur définisse un nouveau code confidentiel lors de la première connexion. Les utilisateurs peuvent également réinitialiser leur code confidentiel de messagerie unifiée à l'aide de Outlook ou Outlook Web App.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Pour accéder à leur boîte aux lettres à extension messagerie unifiée, les utilisateurs d'Outlook Voice Access doivent utiliser un système de numérotation multifréquence, également appelé entrées DTMF (numérotation en fréquences vocales). La reconnaissance vocale n'est pas disponible pour l'entrée de code confidentiel.</td>
</tr>
</tbody>
</table>


Pour découvrir d'autres tâches de gestion concernant la sécurité d'Outlook Voice Access par code confidentiel, consultez la rubrique [Procédures de sécurité de code confidentiel](pin-security-procedures-exchange-2013-help.md).

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : moins d'une minute.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l'entrée « Boîtes aux lettres de messagerie unifiée » dans la rubrique [Autorisations de messagerie unifiée](unified-messaging-permissions-exchange-2013-help.md).

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

## Utiliser le Centre d'administration Exchange (CAE) pour réinitialiser un code confidentiel de messagerie unifiée

1.  Dans le CAE, accédez à **Destinataires**. Dans l'affichage Liste, sélectionnez la boîte aux lettres utilisateur à afficher.

2.  Dans le volet d'informations, sous **Fonctions de téléphone et de voix**, sous **Messagerie unifiée**, cliquez sur **Afficher les détails**.

3.  Dans la page **Boîte aux lettres de messagerie unifiée**, sous **Paramètres de la boîte aux lettres de messagerie unifiée**, cliquez sur **Réinitialiser le code confidentiel**.

4.  Dans la page **Réinitialiser le code confidentiel de boîte aux lettres de messagerie unifiée**, utilisez les options suivantes pour réinitialiser le code confidentiel de l'utilisateur à extension messagerie unifiée :
    
      - **Générer automatiquement un code confidentiel**   Utilisez cette option pour générer automatiquement le code confidentiel entré par l'utilisateur pour accéder à sa boîte aux lettres à l'aide d'Outlook Voice Access. Par défaut, ce paramètre est activé.
        
        Le code confidentiel généré automatiquement est envoyé par message électronique dans la boîte aux lettres de l'utilisateur. Après avoir reçu le code confidentiel et s'être connecté à sa boîte aux lettres, l'utilisateur est invité à modifier le code confidentiel par un code confidentiel plus facile à retenir.
        
        Outlook Web App et Microsoft Outlook permettent également aux utilisateurs de redéfinir leur code confidentiel. Le code confidentiel est généré automatiquement en fonction des stratégies de code confidentiel configurées dans la stratégie de boîte aux lettres de messagerie unifiée associée à la boîte aux lettres de l'utilisateur. nous vous recommandons de générer automatiquement les codes confidentiels pour les utilisateurs Outlook Voice Access.
    
      - **Taper un code confidentiel**   Utilisez cette option pour spécifier manuellement un code confidentiel pour un utilisateur d'Outlook Voice Access. Par défaut, ce paramètre est désactivé.
        
        Si vous spécifiez un code confidentiel pour un utilisateur, il est envoyé par message électronique dans la boîte aux lettres de l'utilisateur. Après avoir reçu le code confidentiel et s'être connecté à sa boîte aux lettres, l'utilisateur peut modifier le code confidentiel en configurant des options personnelles dans Outlook Voice Access. Toutefois, dans Outlook Web App et Microsoft Outlook, aucune option ne permet de spécifier un code confidentiel manuellement.
    
      - **Exiger que l'utilisateur réinitialise son code confidentiel la première fois qu'il se connecte**   Utilisez cette option pour exiger de l'utilisateur qu'il réinitialise son code confidentiel lors de sa première connexion à Outlook Voice Access. Par défaut, cette option est activée.
        
        Si vous sélectionnez l'option de génération automatique d'un code confidentiel pour l'utilisateur, vous pouvez activer cette option pour exiger des utilisateurs qu'ils changent leur code confidentiel lorsqu'ils se connectent à Outlook Voice Access pour la première fois. Ceci contribue à protéger le code confidentiel des utilisateurs.

5.  Cliquez sur **Enregistrer**.

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour redéfinir un code confidentiel de messagerie unifiée

Cet exemple redéfinit le code confidentiel de la messagerie vocale de Tony Smith sur 1985848. Cependant, ce code confidentiel devra être modifié lors de la première connexion de l'utilisateur à Outlook Voice Access.

    Set-UMMailboxPIN -Identity tonysmith@contoso.com -PIN 1985848 -PinExpired $true

