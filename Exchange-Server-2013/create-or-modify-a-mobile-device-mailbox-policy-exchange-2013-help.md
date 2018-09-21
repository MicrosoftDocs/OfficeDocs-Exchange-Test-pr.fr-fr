---
title: 'Créer ou modifier une stratégie de BAL de périph. mobiles: Exchange 2013 Help'
TOCTitle: Créer ou modifier une stratégie de boîte aux lettres de périphériques mobiles
ms:assetid: b4a37a81-25e3-40ff-a18a-a62ae4493635
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb124315(v=EXCHG.150)
ms:contentKeyID: 50479032
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Créer ou modifier une stratégie de boîte aux lettres de périphériques mobiles

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2012-10-16_

Une stratégie de boîte aux lettres de périphérique mobile vous permet d’appliquer un ensemble commun de paramètres de sécurité et de périphériques mobiles à un groupe d’utilisateurs. Vous pouvez créer plusieurs stratégies de boîte aux lettres de périphérique mobile. Une stratégie de boîte aux lettres d'appareils mobiles doit être attribuée à chaque destinataire de votre organisation. Quand vous installez Microsoft Exchange Server 2013, une stratégie de boîte aux lettres d'appareils mobiles par défaut est créée et est automatiquement attribuée aux nouveaux utilisateurs. Pour attribuer une stratégie de boîte aux lettres d'appareils mobiles à des utilisateurs spécifiques, voir [Ajouter ou supprimer des utilisateurs d'une stratégie de boîte aux lettres de périphériques mobiles](add-or-remove-users-from-a-mobile-mailbox-policy-exchange-2013-help.md).

Pour plus d'informations sur les stratégies de boîte aux lettres d'appareils mobiles, voir [Stratégies de boîte aux lettres d'appareil mobile](mobile-device-mailbox-policies-exchange-2013-help.md).

## Ce qu’il faut savoir avant de commencer ?

  - Durée d’exécution estimée de chaque procédure : 10 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Stratégie de boîte aux lettres de périphérique mobile » dans la rubrique [Autorisations des clients et des périphériques mobiles](clients-and-mobile-devices-permissions-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..


## Que souhaitez-vous faire ?

## Créer une stratégie de boîte aux lettres d'appareils mobiles

Vous pouvez utiliser le CAE ou l'environnement de ligne de commande Exchange Management Shell pour créer une stratégie de boîte aux lettres d'appareils mobiles.

Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Stratégie de boîte aux lettres de périphérique mobile » dans la rubrique [Autorisations des clients et des périphériques mobiles](clients-and-mobile-devices-permissions-exchange-2013-help.md).

## Utiliser le CAE pour créer une stratégie de boîte aux lettres d'appareils mobiles

Vous pouvez créer une stratégie de boîte aux lettres d'appareils mobiles via le CAE.

> [!NOTE]
> Vous pouvez uniquement définir un sous-ensemble de paramètres de stratégie de boîte aux lettres d'appareils mobiles dans le CAE. Pour configurer tous les paramètres de stratégie de boîte aux lettres d'appareils mobiles, vous devez utiliser l'environnement de ligne de commande Exchange Management Shell.


1.  Dans le CAE, cliquez sur **Mobile** \> **Stratégies de boîte aux lettres d'appareils mobiles**, puis sur **Nouveau**.

2.  Utilisez les différentes cases à cocher et listes déroulantes pour configurer les paramètres de la stratégie de boîte aux lettres d'appareils mobiles.
    
    > [!WARNING]
    > Sélectionnez <strong>Il s'agit de la stratégie par défaut</strong> pour que la stratégie de boîte aux lettres d'appareils mobiles soit celle par défaut. Après avoir fait d'une stratégie de boîte aux lettres d'appareils mobiles celle par défaut, tous les nouveaux utilisateurs se verront attribuer automatiquement cette stratégie au moment de leur création.


3.  Cliquez sur **Enregistrer**.

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour créer une stratégie de boîte aux lettres d'appareils mobiles

Vous créez une stratégie de boîte aux lettres d'appareils mobiles à l'aide de la cmdlet New-MobileDeviceMailboxPolicy.

> [!WARNING]
> Deux cmdlets peuvent vous permettre de créer une stratégie de boîte aux lettres d'appareils mobiles. Les cmdlets <strong>New-ActiveSyncMailboxPolicy</strong> et <strong>New-MobileDeviceMailboxPolicy</strong> effectuent des tâches identiques. Dans une version future de Microsoft Exchange Server, la cmdlet <strong>New-ActiveSyncMailboxPolicy</strong> sera supprimée. Nous vous recommandons de mettre à jour vos scripts et procédures pour utiliser la cmdlet <strong>New-MobileDeviceMailboxPolicy</strong>.


1.  Dans l’environnement de ligne de commande Exchange Management Shell, exécutez la commande suivante.
    
        New-MobileDeviceMailboxPolicy -Name:"Management" -AllowBluetooth:$true -AllowBrowser:$true -AllowCamera:$true -AllowPOPIMAPEmail:$false -PasswordEnabled:$true -AlphanumericPasswordRequired:$true -PasswordRecoveryEnabled:$true -MaxEmailAgeFilter:10 -AllowWiFi:$true -AllowStorageCard:$true -AllowPOPIMAPEmail:$false

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez bien créé une stratégie de boîte aux lettres d'appareils mobiles, choisissez l'une des options suivantes :

1.  Dans le CAE, cliquez sur **Mobile** \> **Stratégies de boîte aux lettres d'appareils mobiles** et vérifiez que votre nouvelle stratégie apparaît dans l'affichage liste.

2.  Dans l’environnement de ligne de commande Exchange Management Shell, exécutez la commande suivante.
    
        Get-MobileDeviceMailboxPolicy -Identity <PolicyName> 

## Modifier une stratégie existante de boîte aux lettres d'appareils mobiles

Pour modifier une stratégie de boîte aux lettres d'appareils mobiles, vous pouvez utiliser le CAE ou l'environnement de ligne de commande Exchange Management Shell.

Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Stratégie de boîte aux lettres de périphérique mobile » dans la rubrique [Autorisations des clients et des périphériques mobiles](clients-and-mobile-devices-permissions-exchange-2013-help.md).

## Utiliser le CAE pour modifier une stratégie de boîte aux lettres d'appareils mobiles

Vous pouvez modifier une stratégie de boîte aux lettres d'appareils mobiles via le CAE.

> [!NOTE]
> Vous pouvez uniquement modifier un sous-ensemble de paramètres de stratégie de boîte aux lettres d'appareils mobiles dans le CAE. Pour modifier tous les paramètres de stratégie de boîte aux lettres d'appareils mobiles, vous devez utiliser l'environnement de ligne de commande Exchange Management Shell.


1.  Dans le CAE, cliquez sur **Mobile** \> **Stratégies de boîte aux lettres d'appareils mobiles**.

2.  Sélectionnez une stratégie dans l'affichage liste, puis cliquez sur le bouton **Modifier**.

3.  Utilisez les onglets **Général** et **Sécurité** pour modifier les paramètres de la stratégie de boîte aux lettres d'appareils mobiles.

4.  Cliquez sur **Enregistrer** pour mettre à jour la stratégie.

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour modifier les paramètres d'une stratégie de boîte aux lettres d'appareils mobiles

Vous pouvez utiliser l'environnement de ligne de commande Exchange Management Shell pour modifier une stratégie de boîte aux lettres d'appareils mobiles.

> [!WARNING]
> Deux cmdlets peuvent vous permettre de modifier une stratégie de boîte aux lettres d'appareils mobiles. Les cmdlets Set-ActiveSyncMailboxPolicy et Set-MobileDeviceMailboxPolicy effectuent des tâches identiques. Dans une version future de Microsoft Exchange Server, la cmdlet <strong>Set-ActiveSyncMailboxPolicy</strong> sera supprimée. Nous vous recommandons de mettre à jour vos scripts et procédures pour utiliser la cmdlet <strong>Set-MobileDeviceMailboxPolicy</strong>.


1.  Dans l’environnement de ligne de commande Exchange Management Shell, exécutez la commande suivante.
    
        Set-MobileDeviceMailboxPolicy -Identity:Default -DevicePasswordEnabled:$true -AlphanumericDevicePasswordRequired:$true -PasswordRecoveryEnabled:$true -MaxEmailAgeFilter:ThreeDays -AllowWiFi:$false -AllowStorageCard:$true -AllowPOPIMAPEmail:$false -IsDefault:$true -AllowTextMessaging:$true -Confirm:$true

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez bien modifié une stratégie de boîte aux lettres d'appareils mobiles, choisissez l'une des options suivantes :

1.  Dans le CAE, cliquez sur **Mobile** \> **Stratégie de boîte aux lettres d'appareils mobiles**, puis choisissez une stratégie spécifique. Dans le volet d'informations, vous verrez le nombre de paramètres de stratégie répertoriés.

2.  Dans l’environnement de ligne de commande Exchange Management Shell, exécutez la commande suivante.
    
    ```powershell
Get-MobileDeviceMailboxPolicy -Identity <PolicyName>
```

