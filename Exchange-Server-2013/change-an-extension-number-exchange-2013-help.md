---
title: 'Modifier un numéro de poste: Exchange 2013 Help'
TOCTitle: Modifier un numéro de poste
ms:assetid: ff22b366-3bfb-4bf7-9f11-62fba48f1caf
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb232208(v=EXCHG.150)
ms:contentKeyID: 50555522
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Modifier un numéro de poste

 

_**Sapplique à :** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2012-11-14_

Lorsque vous activez un utilisateur pour la messagerie unifiée et l’associez à un plan de numérotation de postes téléphoniques, une adresse proxy EUM contenant le numéro de poste de l’utilisateur est créée pour ce dernier. Vous devez définir au moins un numéro de poste pour la messagerie unifiée à utiliser afin que la messagerie vocale puisse être transférée vers la boîte aux lettres de l’utilisateur. Le numéro de poste est également utilisé lorsque l’utilisateur appelle un numéro Outlook Voice Access.

Vous pouvez modifier le numéro de poste principal qui a été ajouté lorsque l’utilisateur a été activé pour la messagerie unifiée ou un numéro de poste secondaire ajouté ultérieurement, ainsi que les adresses proxy EUM associées de l’utilisateur. Le numéro de poste principal que vous avez ajouté lorsque l’utilisateur a été activé pour la messagerie unifiée sera répertorié en tant qu’adresse proxy EUM principale. Tous les numéros d’extension secondaires supplémentaires que vous avez ajoutés sont répertoriés en tant qu’adresses proxy EUM secondaires. Lorsque les numéros d’extension ont été modifiés, les appelants peuvent laisser des messages vocaux à l’utilisateur sur tous les nouveaux numéros d’extension qui ont été définis. Tous les messages vocaux sont remis dans la même boîte aux lettres de l’utilisateur.

Vous pouvez utiliser le Centre d’administration Exchange (EAC) ou l’environnement de ligne de commande Exchange Management Shell pour modifier un numéro de poste principal ou secondaire pour un utilisateur. La page **Adresse de messagerie** de la boîte aux lettres de l’utilisateur dans le Centre d’administration Exchange (EAC) vous permet de modifier un numéro de poste principal ou secondaire. Vous ne pouvez pas utiliser la page **Boîte aux lettres de messagerie unifiée** du Centre d’administration Exchange (EAC) pour modifier un numéro de poste principal, en revanche vous pouvez l’utiliser pour modifier un numéro de poste secondaire. Pour modifier un numéro de poste secondaire, vous devez commencer par supprimer le numéro de poste secondaire existant et ajouter ensuite le numéro de poste secondaire correct pour l’utilisateur.

Vous pouvez afficher le numéro de poste principal et le numéro de poste secondaire d’un utilisateur à l’aide de la cmdlet **Get-UMMailbox** ou de la cmdlet **Get-Mailbox** dans l’environnement de ligne de commande Exchange Management Shell.

Pour d’autres tâches de gestion relatives aux utilisateurs activés pour la messagerie vocale, consultez la rubrique [Voix des procédures de l'utilisateur à extension messagerie](voice-mail-enabled-user-procedures-exchange-2013-help.md).

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : 3 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Boîtes aux lettres de messagerie unifiée » dans la rubrique [Autorisations de messagerie unifiée](unified-messaging-permissions-exchange-2013-help.md).

  - Avant d’effectuer ces procédures, vérifiez qu’un plan de numérotation de MU de postes téléphoniques a été créé. Pour obtenir la procédure détaillée, consultez la rubrique [Créer un plan de numérotation de messagerie unifiée](create-a-um-dial-plan-exchange-2013-help.md).

  - Avant d’effectuer ces procédures, vérifiez qu’une stratégie de boîte aux lettres de messagerie unifiée a été créée. Pour obtenir la procédure détaillée, consultez la rubrique [Créer une stratégie de boîte aux lettres de messagerie unifiée](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Avant d’effectuer ces procédures, vérifiez que la boîte aux lettres de l’utilisateur a été activée pour la messagerie unifiée et qu’elle est associée à un plan de numérotation de postes téléphoniques. Pour obtenir la procédure détaillée, consultez la rubrique [Activation de la messagerie vocale pour un utilisateur](enable-a-user-for-voice-mail-exchange-2013-help.md).

  - Avant d’effectuer ces procédures, vérifiez que le numéro de poste qui sera attribué à l’utilisateur contient le nombre correct de chiffres définis sur le plan de numérotation de messagerie unifiée.

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..


## Que souhaitez-vous faire ?

## Utiliser le Centre d’administration Exchange pour modifier le numéro de poste principal ou secondaire

1.  Dans le CAE, accédez à **Destinataires**  \> **Boîtes aux lettres**.

2.  Dans l’affichage de liste, sélectionnez la boîte aux lettres pour laquelle vous voulez modifier un numéro de poste, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

3.  Sur la page **Boîte aux lettres de l’utilisateur**, sous **Adresse de messagerie**, sélectionnez le numéro de poste à modifier, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier"). Le numéro de poste principal est répertorié en caractères gras.

4.  Sur la page **Adresse de messagerie**, dans le champ **Adresse/Poste**, entrez le nouveau numéro de poste de l’utilisateur. Pour sélectionner un nouveau plan de numérotation de messagerie unifiée, vous pouvez cliquer sur **Parcourir**.

5.  Cliquez sur **Enregistrer**.

## Utiliser l’environnement de ligne de commande Exchange Management Shell pour modifier le numéro de poste principal ou secondaire

Cet exemple modifie et redéfinit le numéro d’extension à 22222 pour un utilisateur à messagerie unifiée du nom de Jean-Charles Colon.

> [!NOTE]
> Avant de modifier un numéro de poste à l’aide de l’environnement de ligne de commande Exchange Management Shell, vous devez déterminer la position de l’adresse proxy EUM à modifier. Pour déterminer la position, exécutez la commande <strong>$mbx.EmailAddresses</strong>. La première adresse proxy EUM est le numéro de poste (principal) par défaut et est désignée par le chiffre 0 dans la liste.


    $mbx=Get-Mailbox tony.smith
    $mbx.EmailAddresses.Item(0)="eum:22222;phone-context=MyDialPlan.contoso.com"
    Set-Mailbox tony.smith -EmailAddresses $mbx.EmailAddresses

