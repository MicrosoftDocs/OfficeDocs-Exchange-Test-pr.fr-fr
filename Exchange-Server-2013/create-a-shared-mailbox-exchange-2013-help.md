---
title: 'Créer une boîte aux lettres partagée: Exchange 2013 Help'
TOCTitle: Créer une boîte aux lettres partagée
ms:assetid: d34bc827-1e83-4a7f-a219-8ba9c19fe24b
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ150570(v=EXCHG.150)
ms:contentKeyID: 50479236
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Créer une boîte aux lettres partagée

 

_**Sapplique à :** Exchange Online, Exchange Server 2013, Office 365 Enterprise_

_**Dernière rubrique modifiée :** 2016-12-09_

**Durée d’exécution estimée : 5 minutes**

Les boîtes aux lettres partagées permettent à un groupe de personnes dans votre entreprise de surveiller et d’envoyer en toute simplicité des messages électroniques à partir d’un compte commun, tel que info@contoso.com ou support@contoso.com. Lorsqu’une personne du groupe répond à un message envoyé à la boîte aux lettres partagée, le message semble avoir été envoyé à partir de la boîte aux lettres partagée, et non par l’utilisateur.

> [!IMPORTANT]
> Si vous utilisez Office 365 pour les entreprises, vous devez créer votre boîte aux lettres partagée dans le centre d’administration Office 365.
> <ul>
> <li><p><a href="http://go.microsoft.com/fwlink/p/?linkid=834766">Créer des boîtes aux lettres partagées dans Office 365</a></p></li></ul>

Si votre organisation utilise un environnement hybride Exchange, vous devez utiliser le Centre d’administration Exchange (CAE) local pour créer et gérer des boîtes aux lettres partagées. Pour en savoir plus sur les boîtes aux lettres partagées, consultez la rubrique [Boîtes aux lettres partagées](shared-mailboxes-exchange-2013-help.md).

## Utiliser le Centre d'administration Exchange (CAE) pour créer une boîte aux lettres partagée

Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l'entrée « Boîtes aux lettres utilisateur » dans la rubrique [Autorisations des destinataires](recipients-permissions-exchange-2013-help.md).

1.  Accédez à **Destinataires**\>**Partagés**\>**Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter").

2.  Remplissez les champs requis :
    
      - **Nom complet**
    
      - **Adresse de messagerie**

3.  Pour accorder des autorisations Accès total ou Envoyer en tant que, cliquez sur **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter"), puis sélectionnez les utilisateurs auxquels vous souhaitez accorder des autorisations. Vous pouvez utiliser la touche **CTRL** pour sélectionner plusieurs utilisateurs. Vous avez des doutes quant à l’autorisation à utiliser ? Consultez la section Quelles autorisations devez-vous utiliser ? plus loin dans cette rubrique.
    
    > [!NOTE]
    > L’autorisation Accès total permet aux utilisateurs d’ouvrir la boîte aux lettres, d’y créer des éléments et de les modifier. L’autorisation Envoyer en tant que permet à toute personne autre que le propriétaire de la boîte aux lettres d’envoyer des courriers électroniques à partir de cette boîte aux lettres partagée. Les deux autorisations sont requises pour que la boîte aux lettres partagée fonctionne.


4.  Cliquez sur **Enregistrer** pour enregistrer vos modifications et créer la boîte aux lettres partagée.

## Utiliser le CAE pour modifier la délégation de boîte aux lettres partagée

1.  Accédez à **Destinataires**\>**Partagés**\>**Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

2.  Cliquez sur **Délégation de boîte aux lettres**.

3.  Pour accorder ou supprimer les autorisations Accès total et Envoyer en tant que, cliquez sur **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter") ou **Supprimer**, ![Icône Suppression](images/Dd362328.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "Icône Suppression"), puis sélectionnez les utilisateurs auxquels vous souhaitez accorder des autorisations.
    
    > [!NOTE]
    > L’autorisation Accès total permet aux utilisateurs d’ouvrir la boîte aux lettres, d’y créer des éléments et de les modifier. L’autorisation Envoyer en tant que permet à toute personne autre que le propriétaire de la boîte aux lettres d’envoyer des courriers électroniques à partir de cette boîte aux lettres partagée. Les deux autorisations sont requises pour que la boîte aux lettres partagée fonctionne.


4.  Cliquez sur **Enregistrer** pour enregistrer vos modifications.

## Utiliser une boîte aux lettres partagée

Pour savoir comment les utilisateurs peuvent accéder aux boîtes aux lettres partagées et les utiliser, consultez les rubriques suivantes :

  - [Ouvrir et utiliser une boîte aux lettres partagée dans Outlook 2016 et Outlook 2013](https://go.microsoft.com/fwlink/p/?linkid=834764)

  - [Ouvrir et utiliser une boîte aux lettres partagée dans Outlook sur le Web Entreprise](https://go.microsoft.com/fwlink/p/?linkid=834766)

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour créer une boîte aux lettres partagée

Cet exemple crée la boîte aux lettres partagée Sales Department et octroie les autorisations Full Access (Accès total) et Send on Behalf (Envoyer de la part de) au groupe de sécurité MarketingSG. Les autorisations d'accès à la boîte aux lettres seront accordées aux utilisateurs membres du groupe de sécurité.

> [!NOTE]
> Cet exemple suppose que vous avez déjà créé le groupe de sécurité MarketingSG et que ce dernier est à extension messagerie. Consultez la rubrique <a href="manage-mail-enabled-security-groups-exchange-2013-help.md">Gérer les groupes de sécurité à extension de messagerie</a>.


    New-Mailbox -Shared -Name "Sales Department" -DisplayName "Sales Department" -Alias Sales | Set-Mailbox -GrantSendOnBehalfTo MarketingSG | Add-MailboxPermission -User MarketingSG -AccessRights FullAccess -InheritanceType All

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, consultez la rubrique [New-Mailbox](https://technet.microsoft.com/fr-fr/library/aa997663\(v=exchg.150\)).

## Quelles autorisations devez-vous utiliser ?

Vous pouvez utiliser les autorisations suivantes avec une boîte aux lettres partagée.

  - **Accès total**   L’autorisation Accès total permet à un utilisateur d’ouvrir la boîte aux lettres partagée et d’agir comme le propriétaire de cette boîte aux lettres. Une fois qu’il a accédé à la boîte aux lettres partagée, l’utilisateur peut créer des éléments de calendrier, lire, afficher, supprimer et modifier des courriers électroniques, créer des tâches et contacts de calendrier. Toutefois, un utilisateur doté d’une autorisation Accès total ne peut pas envoyer de messages à partir de la boîte aux lettres partagée à moins de disposer de l’autorisation Envoyer en tant que ou Envoyer de la part de.

  - **Envoyer en tant que**   L’autorisation Envoyer en tant que permet à un utilisateur d’emprunter l’identité du propriétaire de la boîte aux lettres partagée pour envoyer des messages. Par exemple, si Kweku se connecte à la boîte aux lettres partagée du service Marketing et envoie un message, le service Marketing semblera en être l’expéditeur.

  - **Envoyer de la part de**   L’autorisation Envoyer de la part de permet à l’utilisateur d’envoyer des messages de la part de la boîte aux lettres partagée. Par exemple, si John se connecte à la boîte aux lettres partagée Reception Building 32 et envoie un message, ce dernier semblera avoir été envoyé par « John de la part de Reception Building 32 ». Vous ne pouvez pas utiliser le CAE pour accorder des autorisations Envoyer de la part de ; vous devez utiliser la cmdlet [Set-Mailbox](https://technet.microsoft.com/fr-fr/library/bb123981\(v=exchg.150\)) avec le paramètre *GrantSendonBehalf*.

## Plus d’informations

Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.

