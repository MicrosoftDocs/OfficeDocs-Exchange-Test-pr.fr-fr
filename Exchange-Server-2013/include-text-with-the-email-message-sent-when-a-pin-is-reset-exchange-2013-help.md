---
title: "Inclure du texte avec le message électronique envoyé lors d'une réinitialisation du code confidentiel est: Exchange 2013 Help"
TOCTitle: Inclure du texte avec le message électronique envoyé lors d'une réinitialisation du code confidentiel est
ms:assetid: f7a4d775-a588-412f-ac2c-11ab1a5c67eb
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb201750(v=EXCHG.150)
ms:contentKeyID: 51407258
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Inclure du texte avec le message électronique envoyé lors d'une réinitialisation du code confidentiel est

 

_**Sapplique à :** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2013-02-22_

Vous pouvez inclure texte supplémentaire dans le message électronique qui est envoyé aux utilisateurs lorsque leur code confidentiel de la messagerie vocale ou de la messagerie unifiée (MU) est réinitialisée. Pour cela, en entrant un texte personnalisé dans la zone **lors Outlook Voice Access code confidentiel d'un utilisateur est réinitialisé** sur une stratégie de boîte aux lettres de messagerie unifiée. Le texte personnalisé peut inclure, par exemple, des informations relatives à la sécurité pour les utilisateurs à extension messagerie unifiée.

Par défaut, un code confidentiel utilisé pour Outlook Voice Access est réinitialisé par le système de messagerie vocale ou de la messagerie unifiée, si le nombre de tentatives de connexion ayant échoués est supérieur à 5. Les utilisateurs peuvent également réinitialiser leurs codes confidentiels utilisant les fonctionnalités de messagerie unifiée incluses avec Outlook Web App ou Outlook 2010 ou version ultérieures ou à l'aide de Outlook accès vocal à partir d'un téléphone.

> [!NOTE]
> Le texte que vous entrez dans ce champ ne peut pas comprendre plus de 512 caractères, et doit être un texte HTML simple.


Pour les autres tâches de gestion concernant la sécurité du code confidentiel d'Outlook Voice Access, consultez la rubrique [Procédures de sécurité de code confidentiel](pin-security-procedures-exchange-2013-help.md).

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : moins d'une minute.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Stratégies de boîte aux lettres de messagerie unifiée » dans la rubrique [Autorisations de messagerie unifiée](unified-messaging-permissions-exchange-2013-help.md).

  - Avant d'exécuter ces procédures, vérifiez qu'un plan de numérotation de messagerie unifiée a été créé. Pour obtenir la procédure détaillée, consultez la rubrique [Créer un plan de numérotation de messagerie unifiée](create-a-um-dial-plan-exchange-2013-help.md).

  - Avant d'effectuer ces procédures, vérifiez qu'une stratégie de boîte aux lettres de messagerie unifiée a été créée. Pour obtenir la procédure détaillée, consultez la rubrique [Créer une stratégie de boîte aux lettres de messagerie unifiée](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..


## Que souhaitez-vous faire ?

## Utiliser le CAE pour ajouter du texte au message électronique envoyé aux utilisateurs lors de la réinitialisation de leur code confidentiel

1.  Dans le CAE, accédez à **Messagerie unifiée** \> **Plans de numérotation de messagerie unifiée**. Dans l'affichage Liste, sélectionnez le plan de numérotation de messagerie unifiée à modifier puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

2.  Dans la page **Plan de numérotation de messagerie unifiée**, sous **Stratégies de boîte aux lettres de messagerie unifiée**, sélectionnez la stratégie de boîte aux lettres de messagerie unifiée à gérer, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

3.  Dans la page **Stratégie de boîte aux lettres de messagerie unifiée** \> **Texte du message**, dans la zone de texte **Lorsque le code confidentiel Outlook Voice Access d''un utilisateur est réinitialisé**, entrez le texte du message électronique envoyé lors de la réinitialisation du code confidentiel d'un utilisateur.

4.  Cliquez sur **Enregistrer**.

## Utiliser l'environnement de ligne de commande pour ajouter du texte au message électronique envoyé aux utilisateurs lors de la réinitialisation de leur code confidentiel

Cet exemple inclut le texte supplémentaire, « ne pas partager votre code confidentiel avec d'autres utilisateurs. Procéder ainsi peut entraîner disciplinaires », dans le message électronique envoyé aux utilisateurs qui sont associés à la de stratégie de boîte aux lettres de messagerie unifiée `MyUMMailboxPolicy` lors de leur code confidentiel est réinitialisé.

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -ResetPINText "Do not share your PIN with other users. Doing so may result in disciplinary action."

