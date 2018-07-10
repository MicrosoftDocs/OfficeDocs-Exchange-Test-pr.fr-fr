---
title: 'Activation ou désactivation de la messagerie pour un dossier public: Exchange 2013 Help'
TOCTitle: Activation ou désactivation de la messagerie pour un dossier public
ms:assetid: 3d69f76d-ff3c-46c1-b962-6a1baa425d8a
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Aa997560(v=EXCHG.150)
ms:contentKeyID: 50477967
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Activation ou désactivation de la messagerie pour un dossier public

 

_**Sapplique à :** Exchange Online, Exchange Server 2013_

_**Dernière rubrique modifiée :** 2016-06-15_

Les dossiers publics sont conçus pour assurer un accès partagé et offrir une manière simple et efficace de collecter, d'organiser et de partager des informations avec d'autres personnes dans votre groupe de travail ou votre organisation. Activer la messagerie d'un dossier public permet aux utilisateurs de publier dans le dossier public en y envoyant un message électronique. Quand la messagerie est activée pour un dossier public, des paramètres supplémentaires sont disponibles pour ce dossier public dans le Centre d’administration Exchange (CAE), tels que les adresses de messagerie et les quotas de messagerie. Dans l'environnement de ligne de commande Exchange Management Shell, avant d'activer la messagerie d'un dossier public, vous utilisez la cmdlet **Set-PublicFolder** pour gérer tous ses paramètres. Une fois la messagerie activée pour le dossier public, vous utilisez les cmdlets **Set-PublicFolder** et **Set-MailPublicFolder** pour gérer les paramètres.

Si vous souhaitez que les utilisateurs d’Internet envoient des messages à un dossier public à extension messagerie, vous devez définir les autorisations d’ajout à l’aide de la cmdlet **Add-PublicFolderClientPermission**.

Pour d'autres tâches de gestion relatives à la gestion des dossiers publics, consultez la rubrique [Procédures relatives aux dossiers publics](public-folder-procedures-exchange-2013-help.md).

Pour découvrir d'autres tâches de gestion associées aux dossiers publics, consultez la rubrique [Procédures de dossiers publics dans Office 365 et Exchange Online](https://technet.microsoft.com/fr-fr/library/jj966272\(v=exchg.150\)).

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : 5 minutes

  - Pour garantir que les utilisateurs d’Internet peuvent envoyer des messages électroniques vers un dossier public à extension messagerie, le dossier public doit disposer au minimum du droit d’accès *CreateItems* accordé au compte Anonyme. Pour connaître la procédure à suivre, consultez la section Autoriser les utilisateurs anonymes à envoyer des messages vers un dossier public à extension messagerie .

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l'entrée « Dossiers publics » dans la rubrique [Autorisations de partage et de collaboration](sharing-and-collaboration-permissions-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.


## Que souhaitez-vous faire ?

## Utiliser le CAE pour activer ou désactiver la messagerie d'un dossier public

1.  Accédez à **Dossiers publics**\>**Dossiers publics**.

2.  Dans l'affichage Liste, sélectionnez le dossier public pour lequel vous voulez activer ou désactiver la messagerie.

3.  Dans le volet d'informations, sous **Paramètres de la messagerie**, cliquez sur **Activer** ou **Désactiver**.

4.  Un message d'avertissement vous demande de confirmer l'activation ou la désactivation de la messagerie du dossier public. Cliquez sur **Oui** pour continuer.

Si vous souhaitez que des utilisateurs externes puissent envoyer des messages à ce dossier public, suivez les étapes de la section Autoriser les utilisateurs anonymes à envoyer des messages vers un dossier public à extension messagerie.

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour activer la messagerie d'un dossier public

Cet exemple active la messagerie du dossier public Support technique.

    Enable-MailPublicFolder -Identity "\Help Desk"

Cet exemple active la messagerie du dossier public Reports sous le dossier public Marketing, mais il masque le dossier de la liste d'adresses.

    Enable-MailPublicFolder -Identity "\Marketing\Reports" -HiddenFromAddressListsEnabled $True

Si vous souhaitez que des utilisateurs externes puissent envoyer des messages à ce dossier public, suivez les étapes de la section Autoriser les utilisateurs anonymes à envoyer des messages vers un dossier public à extension messagerie.

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, consultez la rubrique [Enable-MailPublicFolder](https://technet.microsoft.com/fr-fr/library/aa998824\(v=exchg.150\)).

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour désactiver la messagerie d'un dossier public

Cet exemple désactive la messagerie du dossier public Marketing\\Reports.

    Disable-MailPublicFolder -Identity "\Marketing\Reports"

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, consultez la rubrique [Disable-MailPublicFolder](https://technet.microsoft.com/fr-fr/library/bb123781\(v=exchg.150\)).

## Autoriser les utilisateurs anonymes à envoyer des messages vers un dossier public à extension messagerie

Vous pouvez utiliser Outlook ou l’environnement de ligne de commande Exchange Management Shell pour définir les autorisations du compte Anonyme d’un dossier public. Vous ne pouvez pas utiliser le CAE pour définir des autorisations sur le compte Anonyme.

**Utiliser Outlook pour définir des autorisations pour le compte Anonyme**

1.  Ouvrez Outlook à l’aide d’un compte disposant des autorisations Propriétaire pour le dossier public à extension messagerie auquel vous souhaitez que les utilisateurs anonymes puissent envoyer des messages.

2.  Accédez à **Dossiers publics - \<nom de l’utilisateur\>**.

3.  Accédez au dossier public que vous souhaitez modifier.

4.  Cliquez avec le bouton droit sur le dossier public, cliquez sur **Propriétés**, puis sélectionnez l’onglet **Autorisations**.

5.  Sélectionnez le compte **Anonyme**, sélectionnez **Créer des éléments** sous **Écriture**, puis cliquez sur **OK**.

**Utiliser l’environnement de ligne de commande Exchange Management Shell pour définir des autorisations pour le compte Anonyme**

Cet exemple définit l’autorisation `CreateItems` pour le compte Anonyme sur le dossier public à extension messagerie « Commentaires des clients ».

    Add-PublicFolderClientPermission "\Customer Feedback" -AccessRights CreateItems -User Anonymous

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, consultez la rubrique [Add-PublicFolderClientPermission](https://technet.microsoft.com/fr-fr/library/bb124743\(v=exchg.150\)).

