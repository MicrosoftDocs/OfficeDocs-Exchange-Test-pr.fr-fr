---
title: 'Gestion des param. de messagerie vocale d’un utilisateur: Exchange 2013 Help'
TOCTitle: Gestion des paramètres de messagerie vocale d'un utilisateur
ms:assetid: 73957938-048a-4f9c-bd0f-a3c2c3dcd638
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Aa998851(v=EXCHG.150)
ms:contentKeyID: 50478453
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Gestion des paramètres de messagerie vocale d'un utilisateur

 

_**Sapplique à :** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2013-02-22_

Vous pouvez afficher ou définir les fonctions de messagerie unifiée et de messagerie vocale, ainsi que les paramètres de configuration d'un utilisateur activé pour la messagerie unifiée ou vocale. Par exemple, vous pouvez effectuer les opérations suivantes :

  - Réinitialiser son code confidentiel Outlook Voice Access.

  - Ajouter un numéro de poste opérateur personnel.

  - Ajouter d'autres numéros de poste.

  - Activer ou désactiver la reconnaissance vocale automatique (ASR).

  - Activer ou désactiver les règles de répondeur automatique.

  - Activer ou désactiver l'accès à son courrier électronique ou calendrier.

> [!NOTE]
> Certains paramètres et certaines fonctions peuvent uniquement être configurés via l'environnement de ligne de commande Exchange Management Shell.


Pour découvrir d'autres tâches de gestion relatives aux utilisateurs à extension messagerie vocale, consultez la rubrique [Voix des procédures de l'utilisateur à extension messagerie](voice-mail-enabled-user-procedures-exchange-2013-help.md).

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : 5 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l'entrée « Boîtes aux lettres de messagerie unifiée » dans la rubrique [Autorisations de messagerie unifiée](unified-messaging-permissions-exchange-2013-help.md).

  - Avant d'exécuter ces procédures, vérifiez qu'un plan de numérotation de messagerie unifiée a été créé. Pour obtenir la procédure détaillée, consultez la rubrique [Créer un plan de numérotation de messagerie unifiée](create-a-um-dial-plan-exchange-2013-help.md).

  - Avant d'effectuer ces procédures, vérifiez qu'une stratégie de boîte aux lettres de messagerie unifiée a été créée. Pour obtenir la procédure détaillée, consultez la rubrique [Créer une stratégie de boîte aux lettres de messagerie unifiée](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Avant d'effectuer ces procédures, vérifiez que l'utilisateur existant est actuellement activé pour la messagerie unifiée. Pour obtenir la procédure détaillée, consultez la rubrique [Activation de la messagerie vocale pour un utilisateur](enable-a-user-for-voice-mail-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..


## Que souhaitez-vous faire ?

## Utiliser le Centre d'administration Exchange (CAE) pour afficher ou configurer les propriétés d'un utilisateur à extension messagerie unifiée

1.  Dans le CAE, accédez à **Destinataires**  \> **Boîtes aux lettres**.

2.  Dans l'affichage Liste, sélectionnez la boîte aux lettres pour laquelle vous voulez modifier la stratégie de boîte aux lettres de messagerie unifiée.

3.  Dans le volet d'informations, sous **Fonctions de téléphone et de voix** \> **Messagerie unifiée**, cliquez sur**Afficher les détails**.

4.  Dans la page **Boîte aux lettres de messagerie unifiée**, cliquez sur **Paramètres des boîtes aux lettres de messagerie unifiée** afin d'afficher ou de modifier les propriétés de messagerie unifiée suivantes pour un utilisateur à extension messagerie unifiée existant :
    
      - **État du code confidentiel**   Ce champ en affichage seul indique l'état de la boîte aux lettres de l'utilisateur. Par défaut, quand un utilisateur est activé pour la messagerie unifiée, l'état du code confidentiel est **Non verrouillé**. Toutefois, si l'utilisateur a entré un code confidentiel Outlook Voice Access incorrect à plusieurs reprises, l'état est **Verrouillé**.
    
      - **Stratégie de boîte aux lettres de messagerie unifiée**   Cette zone affiche le nom de la stratégie de boîte aux lettres de messagerie unifiée associée à l'utilisateur à extension messagerie unifiée. Vous pouvez cliquer sur **Parcourir** pour rechercher et spécifier la stratégie de boîte aux lettres de messagerie unifiée devant être associée à cette boîte aux lettres de messagerie unifiée.
    
      - **Extension opérateur personnel**   Cette zone permet de spécifier le numéro de poste opérateur de l'utilisateur. Par défaut, le numéro de poste n'est pas configuré. Le numéro de poste peut contenir de 1 à 20 caractères. Les appels entrants destinés à l'utilisateur à extension messagerie unifiée peuvent ainsi être transférés au numéro de poste que vous spécifiez dans cette zone.
        
        Vous pouvez configurer d'autres types de numéros de poste d'opérateur dans les plans de numérotation et les standards automatiques. Toutefois, ces postes sont généralement utilisés par les réceptionnistes ou les opérateurs à l'échelle de la société. Le paramètre de poste d'opérateur personnel peut être utilisé lorsqu'un administrateur adjoint ou un Assistant répond aux appels entrants avant que ceux-ci ne soient réceptionnés par un utilisateur particulier.

5.  Dans la page **Boîte aux lettres de messagerie unifiée**, sous **Extensions supplémentaires**, vous pouvez ajouter, changer et afficher des numéros de poste pour l'utilisateur.
    
      - Pour ajouter un numéro de poste, cliquez sur **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter"). Dans la page **Ajouter une autre extension**, utilisez **Parcourir** pour sélectionner le plan de numérotation de messagerie unifiée, puis saisissez le numéro de poste dans la zone **Numéro d'extension**.
    
      - Pour supprimer un numéro de poste, sélectionnez-le, puis cliquez sur **Supprimer**![Icône Suppression](images/Dd362328.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "Icône Suppression").

6.  Si vous effectuez des modifications, cliquez sur **Enregistrer**.

## Utiliser l'environnement de ligne de commande Exchange Management Shell afin de configurer des fonctionnalités pour un utilisateur à extension messagerie unifiée

Cet exemple désactive les appels d'émission au téléphone et les notifications d'appels en absence, mais il active les notifications de message texte (SMS).

> [!NOTE]
> Pour les déploiements locaux et hybrides, lors de l'intégration de la messagerie unifiée et de Lync Server, les notifications d'appels en absence ne sont pas disponibles pour les utilisateurs qui ont une boîte aux lettres située sur un serveur de boîtes aux lettres Exchange 2007 ou Exchange 2010. Une notification d'appel en absence est générée lorsqu'un utilisateur se déconnecte avant l'envoi de l'appel vers un serveur de boîtes aux lettres.


    Set-UMMailbox -Identity tony@contoso.com -UMEnabled $true -UMMailboxPolicy AdminPolicy -MissedCallNotificationEnabled $false -PlayonPhoneEnabled $false -SMSMessageWaitingNotificationEnabled $true

Cet exemple empêche un utilisateur d'accéder à son calendrier, mais lui permet d'accéder à ses messages électroniques quand il utilise Outlook Voice Access.

    Set-UMMailbox -Identity tony@contoso.com -UMEnabled $true -UMMailboxPolicy AdminPolicy -Extension 523456 -FAXEnabled $true -TUIAccessToCal $false -TUIAccessToEmail True

Cet exemple empêche un utilisateur d'accéder à son calendrier et à ses messages électroniques quand il utilise Outlook Voice Access.

    Set-UMMailbox -Identity tony@contoso.com -TUIAccessToCalendarEnabled $false -TUIAccessToEmailEnabled $false

Cet exemple empêche un utilisateur de créer des règles de répondeur automatique, de recevoir des télécopies entrantes et d'utiliser Outlook Voice Access, mais lui permet d'utiliser la reconnaissance vocale automatique (Automatic Speech Recognition, ASR).

    Set-UMMailbox -Identity tony@contoso.com -AutomaticSpeechRecognitionEnabled $true -CallAnsweringRulesEnabled $false -FaxEnabled $false -SubscriberAccessEnabled $false 

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour afficher les propriétés d'un utilisateur à messagerie unifiée

Cet exemple affiche la liste de toutes les boîtes aux lettres à extension messagerie unifiée de la forêt dans une liste mise en forme.

    Get-UMMailbox | Format-List

Cet exemple affiche les propriétés de la boîte aux lettres de messagerie unifiée de jccolon@contoso.com.

    Get-UMMailbox -Identity tonysmith@contoso.com

> [!NOTE]
> Quand vous exécutez Exchange 2007 et Exchange 2013 et que la boîte aux lettres de l'utilisateur est située sur un serveur de boîtes aux lettres Exchange 2007, l'exécution de la cmdlet <strong>Get-UMMailbox</strong> ne fonctionne pas correctement. Pour résoudre ce problème, exécutez la cmdlet <strong>Get-UMMailbox</strong> à partir d'un serveur Exchange 2007 ou d'un ordinateur exécutant les outils d'administration Exchange 2007.

