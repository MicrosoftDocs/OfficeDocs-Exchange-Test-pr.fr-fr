---
title: 'Afficher ou configurer des propriétés de stratégie de BAL Outlook Web App'
TOCTitle: Afficher ou configurer des propriétés de stratégie de boîte aux lettres Outlook Web App
ms:assetid: be012ffe-8fdb-4fb7-aebd-78b3a55593fa
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dd351097(v=EXCHG.150)
ms:contentKeyID: 50479093
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Afficher ou configurer des propriétés de stratégie de boîte aux lettres Outlook Web App

 

_**Sapplique à :** Exchange Online, Exchange Server 2013_

_**Dernière rubrique modifiée :** 2016-04-13_

Une fois que vous avez créé une stratégie de boîte aux lettres Outlook Web App, vous pouvez configurer diverses options pour contrôler les fonctionnalités dont disposent les utilisateurs dans Outlook Web App. Par exemple, vous pouvez activer ou désactiver des règles de boîte de réception, ou créer une liste de types de fichiers autorisés pour les pièces jointes.

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée de chaque procédure : 3 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l'entrée « Stratégies de boîte aux lettres de messagerie unifiée Outlook Web App » dans la rubrique [Autorisations des clients et des périphériques mobiles](clients-and-mobile-devices-permissions-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..


## Que souhaitez-vous faire ?

## Utiliser le CAE pour afficher ou configurer des stratégies de boîte aux lettres Outlook Web App

1.  Dans le CAE, cliquez sur **Autorisations**\>**Stratégies Outlook Web App**.

2.  Dans le volet des résultats, sélectionnez la stratégie de boîte aux lettres que vous voulez afficher ou configurer.

3.  Cliquez sur le bouton **Modifier**.

4.  
    
    Sous l'onglet **Général**, vous pouvez afficher et modifier le nom de la stratégie.

5.  
    
    Sous l'onglet **Fonctionnalités**, utilisez les cases à cocher pour activer ou désactiver des fonctionnalités. Par défaut, les fonctionnalités les plus courantes sont affichées. Pour afficher toutes les fonctionnalités pouvant être activées ou désactivées, cliquez sur **plus d'options**.
    
    > [!NOTE]
    > Présente les paramètres pour le remplacement par les stratégies de boîte aux lettres Outlook Web App par les paramètres de répertoire virtuel Outlook Web App. Vous pouvez modifier les paramètres de segmentation des utilisateurs à l'aide de la cmdlet <strong>Set-CASMailbox</strong> dans l'environnement Shell.


6.  
    
    Sous l’onglet **Accès au fichier**, utilisez les cases à cocher **Accès direct au fichier** pour configurer l’accès au fichier et les options d’affichage qui s’offrent aux utilisateurs. L’accès aux fichiers permet aux utilisateurs d’ouvrir ou d’afficher le contenu de fichiers envoyés sous forme de pièces jointes dans un message électronique.
    
    L'accès aux fichiers peut être contrôlé en fonction de la connexion de l'utilisateur sur un ordinateur public ou privé. L’option permettant aux utilisateurs de sélectionner un accès à un ordinateur privé ou public est disponible uniquement quand vous utilisez une authentification basée sur les formulaires. Toutes les autres authentifications se font par défaut par l'accès à un ordinateur privé.

7.  Sous l'onglet **Accès hors connexion**, utilisez les cases d'option pour configurer la disponibilité de l'accès hors ligne.

8.  Cliquez sur **Enregistrer** pour mettre à jour la stratégie.

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour configurer des stratégies de boîte aux lettres Outlook Web App

Cet exemple autorise l'accès au calendrier dans la stratégie de boîte aux lettres par défaut.

    Set-OwaMailboxPolicy -Identity Default -CalendarEnabled $true

Pour plus d'informations sur la syntaxe et les paramètres, consultez la rubrique [Set-OwaMailboxPolicy](https://technet.microsoft.com/fr-fr/library/dd297989\(v=exchg.150\)).

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour afficher des stratégies de boîte aux lettres Outlook Web App

Cet exemple récupère les propriétés de la stratégie de boîte aux lettres Outlook Web App`Executives` dans l'organisation `Fabrikam`.

    Get-OwaMailboxPolicy -Identity Fabrikam\Executives

Pour plus d'informations sur la syntaxe et les paramètres, consultez la rubrique [Get-OwaMailboxPolicy](https://technet.microsoft.com/fr-fr/library/dd351095\(v=exchg.150\)).

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez bien modifié une stratégie de boîte aux lettres Outlook Web App :

1.  Dans le CAE, cliquez sur **Autorisations**\>**Stratégies Outlook Web App**, puis choisissez une stratégie de boîte aux lettres Outlook Web App spécifique.

2.  Cliquez sur le bouton **Modifier** pour afficher les propriétés de la stratégie de boîte aux lettres.

3.  Cliquez sur **Enregistrer** ou sur **Annuler** pour fermer la page des propriétés.

