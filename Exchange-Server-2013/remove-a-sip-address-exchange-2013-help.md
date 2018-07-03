---
title: 'Supprimer une adresse SIP: Exchange 2013 Help'
TOCTitle: Supprimer une adresse SIP
ms:assetid: eaaff0b0-7d85-4845-a7b8-ac22b42bc415
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ662761(v=EXCHG.150)
ms:contentKeyID: 50555513
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Supprimer une adresse SIP

 

_**Sapplique à :** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2012-11-14_

Lorsque vous activez un utilisateur pour la messagerie unifié et le liez à un plan de numérotation URI SIP, deux adresses proxy de messagerie unifiée Exchange sont créées. L'une contient le numéro de poste de l’utilisateur et l’autre contient une adresse SIP pour l’utilisateur. Le numéro de poste est utilisé lorsque l’utilisateur appelle en composant un numéro Outlook Voice Access.

Les plans de numérotation URI SIP et les adresses SIP sont utilisés lorsque vous intégrez une messagerie unifiée et Office Communications Server 2007 R2 ou Microsoft Lync Server. L’adresse SIP est utilisée par Communications Server ou Lync Server pour acheminer des appels entrants et envoyer des messages vocaux à l’utilisateur. Par défaut, l’adresse SIP qui est utilisée par la messagerie unifiée doit être celle que Communications Server ou Lync Server utilise.

Vous pouvez supprimer l’adresse SIP principale qui a été ajoutée lors de l’activation de l’utilisateur pour la messagerie unifiée ou une adresse SIP secondaire qui a été ajoutée par la suite pour l’utilisateur, avec l’adresse proxy de messagerie unifiée Exchange associée. L’adresse SIP principal que vous avez ajoutée lorsque que l’utilisateur a été activé pour la messagerie unifiée doit être répertoriée en tant qu’adresse proxy de messagerie unifiée Exchange principale. Toutes les adresses SIP supplémentaires que vous avez ajoutées doivent être répertoriées en tant qu’adresses proxy de messagerie unifiée Exchange secondaires. Lorsqu’une adresse SIP est supprimée, les appelants ne peuvent plus laisser de messages vocaux pour l’utilisateur à l’adresse SIP qui a été supprimée même si l’utilisateur s’est connecté avec l’adresse SIP attribuée à celui-ci dans Communications Server ou Lync Server.

Si vous supprimez l’adresse SIP principale, la messagerie unifiée n’est plus en mesure d’envoyer de messages vocaux dans la boîte aux lettres de l’utilisateur et les règles de répondeur automatique ne sont pas traitées. Après la suppression de l’adresse SIP principale, l’adresse proxy de messagerie unifiée Exchange de l’utilisateur doit être répertoriée comme **Null** au niveau de la boîte aux lettres de l’utilisateur dans le Centre d’administration Exchange (EAC) et lorsque vous exécutez la cmdlet **Get-Mailbox** dans l’environnement de ligne de commande Exchange Management Shell. De même, lorsque vous exécutez la cmdlet **Get-UMMailbox**, les paramètres *Extensions*, *PhoneNumber* et *CallAnsweringRulesExtensions* doivent être à blanc ou à la valeur « null ».

Vous pouvez utiliser le Centre d’administration Exchange (EAC) ou l’environnement de ligne de commande Exchange Management Shell pour supprimer une adresse SIP principale ou secondaire. La page **Adresse de messagerie** sur la boîte aux lettres de l’utilisateur du Centre d’administration Exchange (EAC) permet de supprimer une adresse SIP principale ou secondaire. En revanche, la page **Boîte aux lettres de messagerie unifiée** du Centre d’administration Exchange ne permet pas de supprimer une adresse SIP principale ou secondaire.

Vous pouvez afficher les adresses SIP principale et secondaires d’un utilisateur à l’aide de la cmdlet **Get-UMMailbox** ou de la cmdlet **Get-Mailbox** dans l’environnement de ligne de commande Exchange Management Shell.

Pour les autres tâches de gestion relatives aux utilisateurs qui sont activées pour la messagerie vocale, voir [Voix des procédures de l'utilisateur à extension messagerie](voice-mail-enabled-user-procedures-exchange-2013-help.md).

## Ce qu’il faut savoir avant de commencer ?

  - Durée d'exécution estimée : 3 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Boîtes aux lettres de messagerie unifiée » dans la rubrique [Autorisations de messagerie unifiée](unified-messaging-permissions-exchange-2013-help.md).

  - Avant d’effectuer cette procédure, vérifiez qu’une stratégie de boîte aux lettres de messagerie unifiée a été créée. Pour obtenir la procédure détaillée, consultez la rubrique [Créer une stratégie de boîte aux lettres de messagerie unifiée](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Avant d’exécuter ces procédures, vérifiez que la boîte aux lettres de l’utilisateur est activée pour la messagerie unifiée et qu’elle est liée à un plan de numérotation URI SIP. Pour obtenir la procédure détaillée, consultez la rubrique [Activation de la messagerie vocale pour un utilisateur](enable-a-user-for-voice-mail-exchange-2013-help.md).

  - Avant d’exécuter ces procédures, vérifiez que les adresses SIP principale et secondaires sont bien configurées pour l’utilisateur.

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..


## Que souhaitez-vous faire ?

## Utiliser le Centre d’administration Exchange (EAC) pour supprimer l’adresse SIP principale ou une adresse SIP secondaire

1.  Dans le CAE, accédez à **Destinataires**  \> **Boîtes aux lettres**.

2.  Dans l’affichage de liste, sélectionnez la boîte aux lettres dans laquelle vous voulez supprimer une adresse SIP, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

3.  Sur la page **Boîte aux lettres de l’utilisateur**, sous **Adresse de messagerie**, sélectionnez l’adresse SIP à supprimer de la liste, puis cliquez sur **Supprimer**![Icône Supprimer](images/Dd979797.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "Icône Supprimer"). L’adresse proxy de messagerie unifiée Exchange ou l’adresse SIP principale est répertoriée en caractères gras.

4.  Cliquez sur **Enregistrer**.

## Utiliser l’environnement de ligne de commande Exchange Management Shell pour supprimer l’adresse SIP principale ou une adresse SIP secondaire

Cet exemple illustre la suppression de l’adresse SIP tsmith@contoso.com de la boîte aux lettres de Tony Smith, un utilisateur à extension messagerie unifiée.

> [!NOTE]
> Avant de supprimer une adresse SIP à l’aide de l’environnement de ligne de commande Exchange Management Shell, vous devez déterminer la position de l’adresse proxy de messagerie unifiée Exchange que vous souhaitez modifier. Pour déterminer la position, utilisez la commande <strong>$mbx.EmailAddresses</strong>. La première adresse proxy de messagerie unifiée Exchange de la liste doit être 0.


    $mbx = Get-Mailbox tony.smith
    $mbx.EmailAddresses.Item(1) -="eum:tsmith@contoso.com;phone-context=MyDialPlan.contoso.com"
    Set-Mailbox tony.smith -EmailAddresses $mbx.EmailAddresses

