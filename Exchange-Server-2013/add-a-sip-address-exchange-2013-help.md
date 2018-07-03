---
title: 'Ajouter une adresse SIP: Exchange 2013 Help'
TOCTitle: Ajouter une adresse SIP
ms:assetid: 40295bcf-c62b-4f26-95ca-a8c4bd210fb3
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ662760(v=EXCHG.150)
ms:contentKeyID: 50555375
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Ajouter une adresse SIP

 

_**Sapplique à :** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2012-11-14_

Lorsque vous activez un utilisateur pour la messagerie unifiée et l’associez à un plan de numérotation SIP URI, deux adresses proxy EUM sont créées : l’une contient le numéro de poste de l’utilisateur et l’autre, une adresse SIP pour l’utilisateur. Le numéro de poste est utilisé lorsque l’utilisateur appelle un numéro Outlook Voice Access.

Les plans de numérotation SIP URI et les adresses SIP sont utilisés lorsque vous intégrez la messagerie unifiée et Microsoft Office Communications Server 2007 R2 ou Microsoft Lync Server. L’adresse SIP est utilisée par Communications Server ou Lync Server pour acheminer les appels entrants et envoyer des messages vocaux à l’utilisateur. Par défaut, l’adresse SIP qui est utilisée par la messagerie unifiée est celle qui est utilisée par Communications Server ou Lync Server.

L’adresse SIP principale que vous avez ajoutée lorsque l’utilisateur a été activé pour la messagerie unifiée est répertoriée en tant qu’adresse proxy EUM principale. Si l’adresse SIP principale a été supprimée, la première adresse proxy EUM ajoutée qui contient l’adresse SIP de l’utilisateur est répertoriée en tant qu’adresse proxy EUM principale. Toutes les adresses SIP supplémentaires que vous ajoutez sont répertoriées en tant qu’adresses proxy EUM secondaires. Lorsque des adresses SIP secondaires sont ajoutées, les appelants peuvent laisser des messages vocaux à l’utilisateur sur tous les points de terminaison SIP auxquels il est connecté à l’aide des adresses SIP. Tous les messages vocaux sont remis dans la même boîte aux lettres de l’utilisateur.

Vous pouvez ajouter une adresse SIP principale ou secondaire pour un utilisateur à l’aide du Centre d’administration Exchange ou de l’environnement de ligne de commande Exchange Management Shell. Vous pouvez utiliser la page **Adresse de messagerie** sur la boîte aux lettres de l’utilisateur dans le CAE pour ajouter une adresse SIP principale ou secondaire. Il n’est pas possible d’utiliser la page **Boîte aux lettres de messagerie unifiée** du CAE pour ajouter une adresse SIP principale ou secondaire.

Vous pouvez afficher les adresses SIP principales ou secondaires d’un utilisateur à l’aide de la cmdlet **Get-UMMailbox** ou de la cmdlet **Get-Mailbox** de l’environnement de ligne de commande Exchange Management Shell.

Pour d’autres tâches de gestion relatives aux utilisateurs activés pour la messagerie vocale, consultez la rubrique [Voix des procédures de l'utilisateur à extension messagerie](voice-mail-enabled-user-procedures-exchange-2013-help.md).

## Ce qu’il faut savoir avant de commencer ?

  - Durée d'exécution estimée : 3 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Boîtes aux lettres de messagerie unifiée » dans la rubrique [Autorisations de messagerie unifiée](unified-messaging-permissions-exchange-2013-help.md).

  - Avant d’effectuer ces procédures, vérifiez qu’un plan de numérotation de messagerie unifiée SIP URI a été créé. Pour obtenir la procédure détaillée, consultez la rubrique [Créer un plan de numérotation de messagerie unifiée](create-a-um-dial-plan-exchange-2013-help.md).

  - Avant d’effectuer ces procédures, vérifiez qu’une stratégie de boîte aux lettres de messagerie unifiée a été créée. Pour obtenir la procédure détaillée, consultez la rubrique [Créer une stratégie de boîte aux lettres de messagerie unifiée](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Avant d’effectuer ces procédures, vérifiez que l’utilisateur existant est activé pour la messagerie unifiée et associé à un plan de numérotation SIP URI. Pour obtenir la procédure détaillée, consultez la rubrique [Activation de la messagerie vocale pour un utilisateur](enable-a-user-for-voice-mail-exchange-2013-help.md).

  - Avant d’effectuer ces procédures, vérifiez que l’adresse SIP qui sera attribuée à l’utilisateur est valide et correctement formatée.

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..


## Que souhaitez-vous faire ?

## Ajout d’une adresse SIP principale ou secondaire à l’aide du Centre d’administration Exchange (CAE)

1.  Dans le CAE, accédez à **Destinataires**  \> **Boîtes aux lettres**.

2.  Dans la liste affichée, sélectionnez la boîte aux lettres pour laquelle vous souhaitez ajouter une adresse SIP, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

3.  Sur la page **Boîte aux lettres de l’utilisateur**, sous **Adresse de messagerie**, cliquez sur **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter").

4.  Sur la page **Nouvelle adresse de messagerie**, sélectionnez **EUM**, puis dans le champ **Adresse/Poste**, saisissez la nouvelle adresse SIP de l’utilisateur.

5.  Sur la page **Nouvelle adresse de messagerie**, sous **Plan de numérotation**, cliquez sur **Parcourir** pour sélectionner le plan de numérotation SIP URI, puis cliquez sur **OK**.

6.  Cliquez sur **Enregistrer**.

## Ajout d’une adresse SIP à l’aide de l’environnement de ligne de commande Exchange Management Shell

Cet exemple montre comment ajouter une adresse SIP pour Tony Smith, un utilisateur à extension messagerie unifiée.

> [!NOTE]
> Avant d’ajouter une adresse SIP à l’aide de l’environnement de ligne de commande Exchange Management Shell, vous devez déterminer la position de l’adresse proxy EUM que vous souhaitez ajouter. Pour cela, exécutez la commande <strong>$mbx.EmailAddresses</strong>. La première adresse proxy dans la liste est 0.


    $mbx=Get-Mailbox tony.smith
    $mbx.EmailAddresses +="eum:tsmit@contoso.com;phone-context=MyDialPlan.contoso.com"
    Set-Mailbox tony.smith -EmailAddresses $mbx.EmailAddresses

