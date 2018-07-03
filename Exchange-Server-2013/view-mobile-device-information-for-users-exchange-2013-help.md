---
title: 'Afficher les informations sur les périphériques mobiles des utilisateurs: Exchange 2013 Help'
TOCTitle: Afficher les informations sur les périphériques mobiles des utilisateurs
ms:assetid: 4fd263c0-ad61-416c-bd68-339bf66605cf
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Aa997974(v=EXCHG.150)
ms:contentKeyID: 50478107
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Afficher les informations sur les périphériques mobiles des utilisateurs

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2012-11-29_

Les utilisateurs peuvent configurer plusieurs périphériques mobiles pour la synchronisation avec Microsoft Exchange Server 2013. Vous pouvez utiliser l’EAC ou le Shell pour afficher la liste des téléphones mobiles associés à un utilisateur spécifique.

Si vous souhaitez rechercher des tâches de gestion supplémentaires relatives aux périphériques mobiles, consultez la rubrique [Exchange ActiveSync](exchange-activesync-exchange-2013-help.md).

## Ce qu’il faut savoir avant de commencer ?

  - Durée d’exécution estimée de chaque procédure : 5 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Stratégie de boîte aux lettres de périphérique mobile » dans la rubrique [Autorisations des clients et des périphériques mobiles](clients-and-mobile-devices-permissions-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..


## Utilisez l'EAC pour afficher les informations sur les périphériques mobiles pour les utilisateurs

Le Centre d'administration Exchange affiche une liste des périphériques mobiles actuellement en synchronisation avec une boîte aux lettres d'utilisateur. Vous pouvez afficher les périphériques mobiles par famille, modèle, numéro de téléphone ou état.

1.  Dans le centre d’administration Exchange, cliquez sur **Destinataires** \> **Boîtes aux lettres**, puis sélectionnez une boîte aux lettres.

2.  Dans le volet d'informations, faites défiler la liste déroulante jusqu'à **Fonctions de téléphone et de voix** et cliquez sur **Afficher les détails** pour afficher l'écran **Détails des périphériques mobiles**.

## Utilisez le Shell pour afficher les informations sur les périphériques mobiles pour les utilisateurs

Vous pouvez utiliser la cmdlet Get-MobileDevice pour afficher une liste des périphériques mobiles pour un utilisateur en particulier.

1.  Exécutez la commande suivante.
    
        Get-MobileDevice -Mailbox useralias

