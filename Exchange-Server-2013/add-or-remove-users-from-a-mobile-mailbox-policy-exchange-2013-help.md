---
title: "Ajouter/supprimer des utlsr de strat. de BAL d’apprl mobiles: Exchange 2013 | Microsoft Docs"
TOCTitle: Ajouter ou supprimer des utilisateurs d'une stratégie de boîte aux lettres de périphériques mobiles
ms:assetid: 4ca8e395-c074-4165-b788-16fae3e2ccab
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Aa997929(v=EXCHG.150)
ms:contentKeyID: 50478137
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Ajouter ou supprimer des utilisateurs d'une stratégie de boîte aux lettres de périphériques mobiles

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2015-07-16_

Une stratégie de boîte aux lettres de périphérique mobile vous permet d’appliquer un ensemble commun de paramètres de sécurité et de périphériques mobiles à un groupe d’utilisateurs. Vous pouvez créer plusieurs stratégies de boîte aux lettres de périphérique mobile.

> [!CAUTION]
> Lorsque vous installez Microsoft Exchange Server 2013, une stratégie de boîtes aux lettres de périphérique mobile par défaut est créée et est automatiquement attribuée à tous les utilisateurs.


Pour d'autres tâches de gestion relatives aux stratégies de boîtes aux lettres de périphérique mobile, consultez la rubrique [Stratégies de boîte aux lettres d'appareil mobile](mobile-device-mailbox-policies-exchange-2013-help.md).

## Ce qu’il faut savoir avant de commencer ?

  - Durée d’exécution estimée de chaque procédure : 5 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Stratégie de boîte aux lettres de périphérique mobile » dans la rubrique [Autorisations des clients et des périphériques mobiles](clients-and-mobile-devices-permissions-exchange-2013-help.md).

  - Une stratégie de boîtes aux lettres de périphérique mobile doit être disponible dans l'EAC, dans **Mobile** \> **Stratégies de boîtes aux lettres de périphérique mobile**.

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..


## Que souhaitez-vous faire ?

## Modifier le stratégie de boîtes aux lettres de périphérique mobile d'un utilisateur

Vous pouvez utiliser l'EAC ou le Shell pour modifier une stratégie de boîtes aux lettres de périphérique mobile d'un utilisateur.

## Utilisez l'EAC pour modifier la stratégie de boîtes aux lettres de périphérique mobile d'un utilisateur

Modifiez la stratégie de boîtes aux lettres de périphérique mobile d'un seul utilisateur à l'aide de l'EAC.

1.  Dans le centre d’administration Exchange, cliquez sur **Destinataires** \> **Boîtes aux lettres**, puis sélectionnez une boîte aux lettres.

2.  Dans le volet d'informations, faites défiler la liste déroulante jusqu'à **Fonctions de téléphone et de voix** et sélectionnez **Afficher les détails** pour afficher l'écran **Détails des périphériques mobiles**.

3.  La stratégie de boîtes aux lettres de périphérique mobile actuellement attribuée s'affiche. Pour modifier la stratégie de boîtes aux lettres de périphérique mobile, cliquez sur **Parcourir**.

4.  Sélectionnez la stratégie de boîtes aux lettres de périphérique mobile appropriée dans la liste, puis cliquez sur **OK** et sur **Enregistrer**.

## Utilisez le Shell pour ajouter un utilisateur à la stratégie de boîtes aux lettres de périphérique mobile

Vous pouvez modifier la stratégie de boîtes aux lettres de périphérique mobile d'un seul utilisateur à l'aide de la cmdlet **Get-CASMailbox** dans le Shell.

1.  Dans l’environnement de ligne de commande Exchange Management Shell, exécutez la commande suivante.
    
        Get-CASMailbox -Identity tony@contoso.com -ActiveSyncMailboxPolicy "Sales" 

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez réussi à modifier une stratégie de boîte aux lettres de périphérique mobile, effectuez l’une des opérations suivantes :

1.  Dans le centre d’administration Exchange, cliquez sur **Destinataires** \> **Boîtes aux lettres**, puis sélectionnez un destinataire en particulier. Dans le volet d’informations, faites défiler le contenu vers le bas jusqu’à **Fonctionnalités téléphoniques et vocales** et cliquez sur **Voir les détails**.

2.  Dans l’environnement de ligne de commande Exchange Management Shell, exécutez la commande suivante.
    
        Get-CASMailbox -Identity tony@contoso.com 

## Modifier la stratégie de boîtes aux lettres de périphérique mobile pour plusieurs utilisateurs en même temps

Si vous souhaitez modifier la stratégie de boîtes aux lettres de périphérique mobile pour plusieurs utilisateurs en même temps, vous pouvez utiliser la fonction de modification en bloc dans l'EAC ou le Shell pour modifier la stratégie de boîtes aux lettres de périphérique mobile pour un groupe d'utilisateurs filtrés.

## Utilisez l'outil de modification en bloc dans l'EAC pour modifier la stratégie de boîtes aux lettres de périphérique mobile pour plusieurs utilisateurs

Vous pouvez mettre à jour la stratégie de boîtes aux lettres de périphérique mobile pour plusieurs utilisateurs en une seule fois au moyen de la fonction Modification en bloc.

1.  Dans le Centre d’administration Exchange, cliquez sur **Destinataires** \> **Boîtes aux lettres**.

2.  Sélectionnez plusieurs utilisateurs.

3.  Dans le volet d'informations, faites défiler la liste vers le bas jusqu'à **Exchange ActiveSync** et cliquez sur **Mettre à jour une stratégie**.

4.  Cliquez sur **Parcourir** pour choisir une stratégie de boîtes aux lettres de périphérique mobile.

5.  Cliquez sur **OK**, puis cliquez sur **Enregistrer**.

## Utilisez le Shell pour modifier la stratégie de boîtes aux lettres de périphérique mobile pour un groupe d'utilisateurs filtrés

Vous pouvez utiliser le Shell pour modifier la stratégie de boîtes aux lettres de périphérique mobile pour un groupe d'utilisateurs filtrés. Vous pouvez filtrer les utilisateurs sur une variété d'attributs.

1.  Dans l’environnement de ligne de commande Exchange Management Shell, exécutez la commande suivante.
    
        Get-Mailbox | where { $_.CustomAttribute1 -match "Manager"
         } | Set-CASMailbox -activesyncmailboxpolicy(Get-ActiveSyncMailboxPolicy "Contoso").Identity
    
    > [!NOTE]
    > Vous pouvez substituer <code>CustomAttribute1</code> à n’importe quelle propriété de l’objet <strong>Get-Mailbox</strong>. Pour afficher la liste complète, tapez : <code>Get-Mailbox username |fl</code>.


## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez réussi à modifier une stratégie de boîte aux lettres de périphérique mobile, effectuez l’une des opérations suivantes :

1.  Dans le centre d’administration Exchange, cliquez sur **Destinataires** \> **Boîtes aux lettres**, puis sélectionnez un destinataire en particulier. Dans le volet d’informations, faites défiler le contenu vers le bas jusqu’à **Fonctionnalités téléphoniques et vocales** et cliquez sur **Voir les détails**.

2.  Dans l’environnement de ligne de commande Exchange Management Shell, exécutez la commande suivante.
    
        Get-CASMailbox -Identity tony@contoso.com

