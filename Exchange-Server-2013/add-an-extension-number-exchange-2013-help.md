---
title: 'Ajouter un numéro de poste: Exchange 2013 Help'
TOCTitle: Ajouter un numéro de poste
ms:assetid: 1a73c9c8-cb50-4bd7-a101-dadd20e28031
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dd335124(v=EXCHG.150)
ms:contentKeyID: 50555354
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Ajouter un numéro de poste

 

_**Sapplique à :** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2012-11-14_

Lorsque vous activez un utilisateur pour la messagerie unifiée et l’associez à un plan de numérotation de postes téléphoniques, une adresse proxy EUM contenant le numéro de poste de l’utilisateur est créée pour ce dernier. Vous devez définir au moins un numéro de poste pour la messagerie unifiée à utiliser afin que la messagerie vocale puisse être transférée vers la boîte aux lettres de l’utilisateur. Le numéro de poste est également utilisé lorsque l’utilisateur appelle un numéro Outlook Voice Access.

Le numéro de poste principal que vous avez ajouté lorsque l’utilisateur a été activé pour la messagerie unifiée sera répertorié en tant qu’adresse proxy EUM principale. Si le numéro de poste principal a été supprimé, la première adresse proxy EUM ajoutée qui contient le numéro de poste de l’utilisateur devient l’adresse proxy EUM principale. Tous les numéros de postes supplémentaires que vous ajoutez sont répertoriés en tant qu’adresses proxy EUM secondaires. Lorsque des numéros de postes secondaires supplémentaires sont ajoutés, les appelants peuvent laisser des messages vocaux à tous les numéros de postes de l’utilisateur qui ont été définis. Tous les messages vocaux sont remis dans la même boîte aux lettres de l’utilisateur.

Vous pouvez ajouter un numéro de poste principal ou secondaire pour un utilisateur à l’aide du Centre d’administration Exchange ou de l’environnement de ligne de commande Exchange Management Shell. Vous pouvez utiliser la page **Adresse de messagerie** sur la boîte aux lettres de l’utilisateur dans le Centre d’administration Exchange pour ajouter un numéro de poste principal ou secondaire. Vous ne pouvez pas utiliser la page **Boîte aux lettres de messagerie unifiée** du CAE pour ajouter un numéro de poste principal. Toutefois, vous pouvez utiliser cette page pour ajouter des numéros de postes secondaires.

Vous pouvez afficher les numéros de postes principaux ou secondaires d’un utilisateur à l’aide de la cmdlet **Get-UMMailbox** ou de la cmdlet **Get-Mailbox** de l’environnement de ligne de commande Exchange Management Shell.

Pour d’autres tâches de gestion relatives aux utilisateurs activés pour la messagerie vocale, consultez la rubrique [Voix des procédures de l'utilisateur à extension messagerie](https://docs.microsoft.com/fr-fr/exchange/voice-mail-unified-messaging/set-up-voice-mail/voice-mail-enabled-user-procedures).

## Ce qu’il faut savoir avant de commencer ?

  - Durée d'exécution estimée : 3 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Boîtes aux lettres de messagerie unifiée » dans la rubrique [Autorisations de messagerie unifiée](unified-messaging-permissions-exchange-2013-help.md).

  - Avant d’effectuer ces procédures, vérifiez qu’un plan de numérotation de MU de postes téléphoniques a été créé. Pour obtenir la procédure détaillée, consultez la rubrique [Créer un plan de numérotation de messagerie unifiée](https://docs.microsoft.com/fr-fr/exchange/voice-mail-unified-messaging/connect-voice-mail-system/create-um-dial-plan).

  - Avant d’effectuer ces procédures, vérifiez qu’une stratégie de boîte aux lettres de messagerie unifiée a été créée. Pour obtenir la procédure détaillée, consultez la rubrique [Créer une stratégie de boîte aux lettres de messagerie unifiée](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Avant d’effectuer ces procédures, vérifiez que la boîte aux lettres de l’utilisateur a été activée pour la messagerie unifiée et qu’elle est associée à un plan de numérotation de postes téléphoniques. Pour obtenir la procédure détaillée, consultez la rubrique [Activation de la messagerie vocale pour un utilisateur](https://docs.microsoft.com/fr-fr/exchange/voice-mail-unified-messaging/set-up-voice-mail/enable-a-user-for-voice-mail).

  - Avant d’effectuer ces procédures, vérifiez que le numéro de poste qui sera attribué à l’utilisateur contient le nombre correct de chiffres définis sur le plan de numérotation de messagerie unifiée.

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..


## Que souhaitez-vous faire ?

## Ajout d’un numéro de poste secondaire à l’aide du Centre d’administration Exchange

1.  Dans le CAE, accédez à **Destinataires**  \> **Boîtes aux lettres**.

2.  Dans la liste affichée, sélectionnez la boîte aux lettres pour laquelle vous souhaitez ajouter un numéro de poste.

3.  Dans le volet d’informations, sous **Fonctions de téléphone et de voix** \> **Messagerie unifiée**, cliquez sur **Afficher les détails**.

4.  Sur la page **Boîte aux lettres de messagerie unifiée**, cliquez sur **Autres postes**, puis sur **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter").

5.  Sur la page **Autres postes**, en regard de la zone **Plan de numérotation de messagerie unifiée**, cliquez sur **Parcourir** et recherchez le plan de numérotation de l’utilisateur.

6.  Sur la page **Autres postes**, dans la zone **Numéro de poste**, saisissez le numéro de poste, puis cliquez sur **OK**.

7.  Cliquez sur **Enregistrer**.

## Ajout d’un numéro de poste principal ou secondaire à l’aide du Centre d’administration Exchange

1.  Dans le CAE, accédez à **Destinataires**  \> **Boîtes aux lettres**.

2.  Dans la liste affichée, sélectionnez la boîte aux lettres à laquelle vous souhaitez ajouter le numéro de poste, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

3.  Sur la page **Boîte aux lettres de l’utilisateur**, sous **Adresse de messagerie**, cliquez sur **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter").

4.  Sur la page **Nouvelle adresse de messagerie**, sélectionnez **EUM** et, dans la zone **Adresse/Poste**, saisissez le numéro de poste de l’utilisateur.

5.  Sur la page **Nouvelle adresse de messagerie**, sous **Plan de numérotation**, cliquez sur **Parcourir** pour sélectionner le plan de numérotation de postes téléphoniques, puis cliquez sur **OK**.

6.  Cliquez sur **Enregistrer**.

## Ajout d’un numéro de poste à l’aide de l’environnement de ligne de commande Exchange Management Shell

Cet exemple montre comment ajouter le numéro de poste 22222 pour Tony Smith, un utilisateur à extension messagerie unifiée.

> [!NOTE]
> Avant d’ajouter un numéro de poste à l’aide de l’environnement de ligne de commande Exchange Management Shell, vous devez déterminer la position de l’adresse proxy EUM à ajouter. Pour cela, exécutez la commande <strong>$mbx.EmailAddresses</strong>. La première adresse proxy dans la liste est 0.


    $mbx=Get-Mailbox tony.smith
    $mbx.EmailAddresses +="eum:22222;phone-context=MyDialPlan.contoso.com"
    Set-Mailbox tony.smith -EmailAddresses $mbx.EmailAddresses

