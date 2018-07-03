---
title: 'Spécifiez le texte à afficher pour les clients de messagerie qui ne prennent pas en charge Windows Rights Management: Exchange 2013 Help'
TOCTitle: Spécifiez le texte à afficher pour les clients de messagerie qui ne prennent pas en charge Windows Rights Management
ms:assetid: a9b2238a-b534-469c-a0c3-2768bc3d005b
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Ee423552(v=EXCHG.150)
ms:contentKeyID: 52057153
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Spécifiez le texte à afficher pour les clients de messagerie qui ne prennent pas en charge Windows Rights Management

 

_**Sapplique à :** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2013-02-22_

Vous pouvez spécifier le texte envoyé à un utilisateur quand ce dernier reçoit un message vocal protégé, mais que son client ne prend pas en charge la Gestion des droits relatifs à l'information (IRM) ou la Gestion des droits Windows.

La messagerie vocale protégée est uniquement accessible aux clients de messagerie qui prennent en charge la Gestion des droits Windows ou quand un utilisateur à extension messagerie unifiée fait appel à Outlook Voice Access pour accéder à un message vocal protégé.

La messagerie vocale protégée est chiffrée. Quand un message vocal est protégé :

  - Le message est marqué comme Privé dans Microsoft Outlook et Outlook Web App.

  - Le message vocal peut être ouvert uniquement par le destinataire approprié.

  - Le destinataire peut répondre au message vocal, mais ne peut pas le transmettre à une personne non incluse dans le message vocal d'origine.

Si un message vocal protégé est envoyé à une personne dont le client de messagerie ne prend pas en charge la Gestion des droits Windows et que celle-ci ne parvient pas à accéder au message à l'aide d'Outlook Voice Access, un message électronique incluant le texte que vous avez spécifié lui est envoyé. Ce texte doit inclure des instructions sur la procédure que le destinataire doit suivre pour pouvoir recevoir le message vocal protégé.

Pour les autres tâches de gestion relatives aux procédures de la messagerie vocale protégée, consultez la rubrique [Procédures de la messagerie vocale protégées](protected-voice-mail-procedures-exchange-2013-help.md).

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : moins d'une minute.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l'entrée « Stratégies de boîte aux lettres de messagerie unifiée » dans la rubrique [Autorisations de messagerie unifiée](unified-messaging-permissions-exchange-2013-help.md).

  - Avant d'effectuer ces procédures, vérifiez qu'un plan de numérotation de messagerie unifiée a été créé. Pour obtenir la procédure détaillée, consultez la rubrique [Créer un plan de numérotation de messagerie unifiée](create-a-um-dial-plan-exchange-2013-help.md).

  - Avant d'effectuer ces procédures, vérifiez qu'une stratégie de boîte aux lettres de messagerie unifiée a été créée. Pour obtenir la procédure détaillée, consultez la rubrique [Créer une stratégie de boîte aux lettres de messagerie unifiée](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..


## Que souhaitez-vous faire ?

## Utiliser le Centre d'administration Exchange (CAE) pour spécifier le texte à afficher aux clients de messagerie qui ne prennent pas en charge la Gestion des droits Windows

1.  Dans le CAE, accédez à **Messagerie unifiée** \> **Plans de numérotation de messagerie unifiée**. Dans l'affichage Liste, sélectionnez le plan de numérotation de messagerie unifiée à modifier puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

2.  Dans la page **Plan de numérotation de messagerie unifiée**, sous **Stratégies de boîte aux lettres de messagerie unifiée**, sélectionnez la stratégie de boîte aux lettres de messagerie unifiée à gérer, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

3.  Dans la page **Stratégie de boîte aux lettres de messagerie unifiée** \> **Messagerie vocale protégée**, sous **Message à envoyer aux utilisateurs ne disposant pas de la prise en charge de la gestion des droits Windows**, tapez le texte du message dans la zone de texte.

4.  Cliquez sur **Enregistrer**.

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour spécifier le texte à afficher aux clients de messagerie qui ne prennent pas en charge la Gestion des droits Windows

Cet exemple montre comment spécifier le texte à présenter aux utilisateurs associés à la stratégie de boîte aux lettres de messagerie unifiée `MyUMMailboxPolicy` qui possèdent des clients de messagerie ne prenant pas en charge la Gestion des droits Windows.

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -ProtectedVoiceMailText "Your email client software does not support Protected Voice Mail. Please contact the Help Desk."

