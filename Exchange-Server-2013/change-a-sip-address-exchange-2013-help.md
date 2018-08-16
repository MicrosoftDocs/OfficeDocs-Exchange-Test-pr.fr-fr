﻿---
title: 'Modifier une adresse SIP: Exchange 2013 Help'
TOCTitle: Modifier une adresse SIP
ms:assetid: 33f4f464-9baa-48af-bf5e-a0d55bb45f60
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dd335189(v=EXCHG.150)
ms:contentKeyID: 50555367
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Modifier une adresse SIP

 

_**Sapplique à :** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2012-11-14_

Lorsque vous activez un utilisateur pour la messagerie unifiée et l’associez à un plan de numérotation SIP URI, deux adresses proxy EUM sont créées : L’une contient le numéro de poste de l’utilisateur et l’autre, une adresse SIP pour l’utilisateur. Le numéro de poste est utilisé lorsque l’utilisateur appelle un numéro Outlook Voice Access.

Les plans de numérotation SIP URI et les adresses SIP sont utilisés lorsque vous intégrez la messagerie unifiée et Microsoft Office Communications Server 2007 R2 ou Microsoft Lync Server. L’adresse SIP est utilisée par Communications Server ou Lync Server pour acheminer les appels entrants et envoyer des messages vocaux à l’utilisateur. Par défaut, l’adresse SIP qui est utilisée par la messagerie unifiée est celle qui est utilisée par Communications Server ou Lync Server.

Vous pouvez modifier l’adresse SIP principale qui a été ajoutée lorsque l’utilisateur a été activé pour la messagerie unifiée ou une adresse SIP secondaire ajoutée ultérieurement, ainsi que les adresses proxy EUM de l’utilisateur. L’adresse SIP principale que vous avez ajoutée lorsque l’utilisateur a été activé pour la messagerie unifiée est répertoriée en tant qu’adresse proxy EUM principale. Toutes les adresses SIP secondaires supplémentaires que vous avez ajoutées sont répertoriées en tant qu’adresses proxy EUM secondaires. Lorsque des adresses SIP secondaires sont modifiées, les appelants peuvent laisser des messages vocaux à l’utilisateur sur tous les points de terminaison SIP auxquels l’utilisateur est connecté à l’aide des nouvelles adresses SIP. Tous les messages vocaux sont remis dans la même boîte aux lettres de l’utilisateur.

Vous pouvez utiliser le Centre d’administration Exchange ou l’environnement de ligne de commande Exchange Management Shell pour modifier une adresse SIP principale ou secondaire. Vous pouvez utiliser la page **Adresse de messagerie** sur la boîte aux lettres de l’utilisateur dans le CAE pour modifier une adresse SIP principale ou secondaire. Il n’est pas possible d’utiliser la page **Boîte aux lettres de messagerie unifiée** du CAE pour modifier une adresse SIP principale ou secondaire.

Vous pouvez afficher les adresses SIP principales ou secondaires d’un utilisateur à l’aide de la cmdlet **Get-UMMailbox** ou de la cmdlet **Get-Mailbox** de l’environnement de ligne de commande Exchange Management Shell.

Pour d’autres tâches de gestion relatives aux utilisateurs activés pour la messagerie vocale, consultez la rubrique [Voix des procédures de l'utilisateur à extension messagerie](voice-mail-enabled-user-procedures-exchange-2013-help.md).

## Ce qu’il faut savoir avant de commencer ?

  - Durée d'exécution estimée : 3 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Boîtes aux lettres de messagerie unifiée » dans la rubrique [Autorisations de messagerie unifiée](unified-messaging-permissions-exchange-2013-help.md).

  - Avant d’effectuer ces procédures, vérifiez qu’un plan de numérotation de messagerie unifiée SIP URI a été créé. Pour obtenir la procédure détaillée, consultez la rubrique [Créer un plan de numérotation de messagerie unifiée](create-a-um-dial-plan-exchange-2013-help.md).

  - Avant d’effectuer ces procédures, vérifiez qu’une stratégie de boîte aux lettres de messagerie unifiée a été créée. Pour obtenir la procédure détaillée, consultez la rubrique [Créer une stratégie de boîte aux lettres de messagerie unifiée](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Avant d’effectuer ces procédures, vérifiez que l’utilisateur existant est activé pour la messagerie unifiée et qu’il est associé à un plan de numérotation SIP URI. Pour obtenir la procédure détaillée, consultez la rubrique [Activation de la messagerie vocale pour un utilisateur](enable-a-user-for-voice-mail-exchange-2013-help.md).

  - Avant d’effectuer ces procédures, vérifiez que l’adresse SIP qui sera attribuée à l’utilisateur est valide et correctement formatée.

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..


## Que souhaitez-vous faire ?

## Modification de l’adresse SIP principale ou d’une adresse SIP secondaire à l’aide du Centre d’administration Exchange (CAE)

1.  Dans le CAE, accédez à **Destinataires**  \> **Boîtes aux lettres**.

2.  Dans la liste affichée, sélectionnez la boîte aux lettres pour laquelle vous souhaitez modifier une adresse SIP, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

3.  Sur la page **Boîte aux lettres utilisateur**, sous **Adresse de messagerie**, sélectionnez l’adresse SIP que vous souhaitez modifier, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier"). L’adresse SIP principale apparaît en chiffres et en lettres gras.

4.  Sur la page **Adresse de messagerie**, dans le champ **Adresse/Poste**, entrez la nouvelle adresse SIP de l’utilisateur, puis cliquez sur **OK**. Pour sélectionner un nouveau plan de numérotation de messagerie unifiée, vous pouvez cliquer sur **Parcourir**.

5.  Cliquez sur **Enregistrer**.

## Modification de l’adresse SIP principale ou d’une adresse SIP secondaire à l’aide de l’environnement de ligne de commande Exchange Management Shell

Cet exemple montre comment modifier une adresse SIP pour Tony Smith.

> [!NOTE]
> Avant de modifier une adresse SIP à l’aide de l’environnement de ligne de commande Exchange Management Shell, vous devez déterminer la position de l’adresse proxy EUM à modifier. Pour cela, exécutez la commande <strong>$mbx.EmailAddresses</strong>. La première adresse proxy EUM est l’adresse SIP (principale) par défaut et est désignée par le chiffre 0 dans la liste.


    $mbx=Get-Mailbox tony.smith
    $mbx.EmailAddresses.Item(1)="eum:tsmith@contoso.com;phone-context=MySIPDialPlan.contoso.com"
    Set-Mailbox tony.smith -EmailAddresses $mbx.EmailAddresses

