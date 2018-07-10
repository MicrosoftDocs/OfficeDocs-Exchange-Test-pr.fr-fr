---
title: 'Exchange ActiveSync: Exchange 2013 Help'
TOCTitle: Exchange ActiveSync
ms:assetid: 5fafaff3-eb37-4fdb-95f0-e56c45ea5884
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Aa998357(v=EXCHG.150)
ms:contentKeyID: 50478207
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange ActiveSync

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2016-12-09_

Découvrez le protocole client Exchange ActiveSync pour Exchange Server 2013. Cet article présente les fonctionnalités d’Exchange ActiveSync, notamment les fonctionnalités de sécurité, les éléments que vous pouvez gérer, la gestion de leur sécurité et la résolution des problèmes lors de la synchronisation vers Windows Phone 7.

> [!TIP]
> Cette rubrique est adressée aux administrateurs. Vous voulez configurer votre appareil Windows Phone, iOS ou Android afin de pouvoir accéder à votre boîte aux lettres Office 365 ou Exchange Server ? Consultez les rubriques suivantes.
> <ul>
> <li><p><a href="https://go.microsoft.com/fwlink/p/?linkid=615415">Configurer la messagerie sur Windows Phone</a></p></li>
> <li><p><a href="https://go.microsoft.com/fwlink/p/?linkid=615414">Configurer la messagerie sur Apple iPhone, iPad et iPod Touch</a></p></li>
> <li><p><a href="https://go.microsoft.com/fwlink/?linkid=615417">Configurer la messagerie électronique sur un téléphone ou une tablette Android</a></p></li></ul>

Exchange ActiveSync est un protocole client qui vous permet de synchroniser un périphérique mobile avec votre boîte aux lettres Exchange. Exchange ActiveSync est activé par défaut lorsque vous installez Microsoft Exchange 2013.

**Contenu de cette rubrique**

Vue d’ensemble d’Exchange ActiveSync

Fonctionnalités d’Exchange ActiveSync

Gestion d'Exchange ActiveSync

Synchronisation de Windows Phone 7

## Vue d’ensemble d’Exchange ActiveSync

Exchange ActiveSync est un protocole de synchronisation Microsoft Exchange optimisé pour fonctionner avec des réseaux à faible bande passante et latence élevée. Le protocole, basé sur HTTP et XML, permet à des téléphones mobiles d’accéder aux informations d’une organisation sur un serveur exécutant Microsoft Exchange. Exchange ActiveSync permet aux utilisateurs de téléphones mobiles d’accéder à leurs messages électroniques, calendrier, contacts et tâches et de continuer à avoir accès à ces informations lorsqu’ils travaillent hors connexion.

> [!NOTE]
> Exchange ActiveSync ne prend pas en charge les boîtes aux lettres partagées ou l’accès délégué.


> [!NOTE]
> Les téléphones mobiles Windows Phone 7 prennent uniquement en charge un sous-ensemble de tous les paramètres de la stratégie de boîtes aux lettres d’Exchange ActiveSync. Pour une liste complète, consultez la rubrique Synchronisation de Windows Phone 7.


## Fonctionnalités d’Exchange ActiveSync

Exchange ActiveSync présente les fonctionnalités suivantes :

  - prise en charge des messages HTML ;

  - prise en charge des indicateurs de suivi ;

  - regroupement de conversations par messages électroniques ;

  - Possibilité de synchroniser ou de ne pas synchroniser la totalité d’une conversation

  - Synchronisation de messages SMS avec la boîte aux lettres Exchange d’un utilisateur

  - Prise en charge de l’affichage de l’état de réponse du message

  - prise en charge de la récupération rapide des messages ;

  - informations des participants aux réunions ;

  - recherche Exchange optimisée ;

  - réinitialisation de code PIN ;

  - amélioration de la sécurité des appareils via des stratégies de mot de passe ;

  - service de découverte automatique pour mise en service directe ;

  - prise en charge du paramétrage de réponses automatiques lorsque vous êtes absent, en vacances ou hors de votre bureau ;

  - prise en charge de la synchronisation des tâches ;

  - Direct Push ;

  - prise en charge des informations de disponibilité des contacts.

## Gestion d'Exchange ActiveSync

Par défaut, Exchange ActiveSync est activé. Tous les utilisateurs disposant d'une boîte aux lettres Exchange peuvent synchroniser leur appareil mobile avec le serveur Microsoft Exchange.

Vous pouvez exécuter les tâches Exchange ActiveSync suivantes :

  - activer et désactiver Exchange ActiveSync pour des utilisateurs ;

  - définir des stratégies telles que la longueur de mot de passe minimale, le verrouillage d'appareils et le nombre maximal de tentatives d'entrée de mot de passe infructueuses ;

  - lancer une réinitialisation à distance pour supprimer toutes les données d'un téléphone mobile perdu ou volé ;

  - générer une série de rapports pour l'affichage et l'exportation sous plusieurs formats ;

  - contrôler les types de périphériques mobiles pouvant être synchronisés avec votre organisation via les règles d'accès aux périphériques

## Sécurité dans Exchange ActiveSync

Vous pouvez configurer Exchange ActiveSync pour utiliser un chiffrement SSL (Secure Sockets Layer) pour les communications entre le serveur Exchange et le périphérique mobile.

## Gestion des accès aux périphériques mobiles dans Exchange ActiveSync

Vous pouvez contrôler les périphériques mobiles pouvant être synchronisés. Pour ce faire, vous pouvez contrôler les périphériques mobiles au moment de leur connexion à votre organisation ou vous pouvez définir les règles qui déterminent les types de périphériques mobiles autorisés à se connecter. Quelle que soit la méthode utilisée pour spécifier les périphériques mobiles pouvant être synchronisés, vous pouvez approuver ou refuser l'accès de tout périphérique mobile pour un utilisateur spécifique, à tout moment

## Fonctionnalités de sécurité des périphériques dans Exchange ActiveSync

Outre la possibilité de configurer des options de sécurité pour les communications entre le serveur Exchange et vos appareils mobiles, Exchange ActiveSync offre les fonctionnalités suivantes permettant d'accroître la sécurité des appareils mobiles :

  - **Effacement à distance**   Si votre périphérique mobile est perdu, volé ou compromis de quelque manière que se soit, vous pouvez émettre une commande d’effacement à distance depuis l’ordinateur Exchange Server ou depuis tout navigateur Web à l’aide d’Outlook Web App. Cette commande efface toutes les données de votre périphérique mobile.

  - **Stratégies de mot de passe de périphérique **  Exchange ActiveSync permet de configurer plusieurs options pour les mots de passe de périphérique.
    
    > [!WARNING]
    > La technologie de lecture d’empreintes digitales d’iOS7 ne peut pas faire office de mot de passe sur un appareil. Si vous choisissez d’utiliser le lecteur d’empreintes digitales d’iOS7, vous devrez tout de même créer et entrer un mot de passe sur l’appareil si la stratégie de boîte aux lettres d’appareil mobile de votre organisation en exige un.
    
    Les options disponibles pour les mots de passe d’appareil sont les suivantes :
    
      - **Longueur minimale du mot de passe (caractères) **  Cette option spécifie la longueur du mot de passe du périphérique mobile. La longueur par défaut est de 4 caractères mais le mot de passe peut en contenir jusqu’à 18.
    
      - **Nombre minimal de jeux de caractères**   Utilisez cette zone de texte pour indiquer la complexité du mot de passe alphanumérique et obliger les utilisateurs à utiliser des types de caractères différents parmi les suivants : lettres minuscules, lettres majuscules, symboles et nombres.
    
      - **Exiger un mot de passe alphanumérique**   Cette option détermine la force du mot de passe. Vous pouvez appliquer l'utilisation d'un caractère ou d'un symbole dans le mot de passe en plus des chiffres.
    
      - **Inactivité (secondes)**   Cette option détermine le temps pendant lequel l'appareil mobile doit être inactif avant que l'utilisateur ne soit invité à entrer un mot de passe pour le déverrouiller.
    
      - **Activer l’historique du mot de passe**   Activez cette case à cocher pour obliger le téléphone mobile à empêcher l’utilisateur de réutiliser ses mots de passe précédents. Le nombre que vous définissez détermine le nombre d’anciens mots de passe que l’utilisateur ne pourra pas réutiliser.
    
      - **Activer la récupération du mot de passe**   Cochez cette case pour activer la récupération du mot de passe sur appareil mobile.  Les administrateurs peuvent utiliser la cmdlet **Get-ActiveSyncDeviceStatistics** pour rechercher le mot de passe de récupération de l’utilisateur.
    
      - **Effacer l’appareil après un échec (tentatives)**   Cette option permet de spécifier si vous voulez que la mémoire du téléphone soit effacée après plusieurs tentatives d’entrée de mot de passe infructueuses.

  - **Stratégies de chiffrement d'appareil**   Il existe des stratégies de chiffrement d'appareil mobile que vous pouvez appliquer pour un groupe d'utilisateurs. Ces stratégies sont les suivantes :
    
      - **Exiger le chiffrement sur l'appareil**   Cochez cette case pour exiger le chiffrement de l'appareil mobile. Cela augmente la sécurité en chiffrant toutes les informations sur l'appareil mobile.
    
      - **Exiger le chiffrement sur la carte de stockage**   Cochez cette case pour exiger le chiffrement de la carte de stockage amovible du périphérique mobile. Cela augmente la sécurité en chiffrant toutes les informations des cartes de stockage du périphérique mobile.

## Synchronisation de Windows Phone 7

Si votre organisation utilise des périphériques mobiles Phone 7, des problèmes de synchronisation se produiront si certaines propriétés de la stratégie de boîte aux lettres des périphérique mobiles sont configurées. Pour permettre la synchronisation des téléphones mobiles Windows Phone 7 avec une boîte aux lettres Exchange, définissez la propriété **AllowNonProvisionableDevices** sur True ou configurez seulement les propriétés de la stratégie de boîte aux lettres des périphériques mobiles :

  - PasswordRequired

  - MinPasswordLength

  - IdleTimeoutFrequencyValue

  - DeviceWipeThreshold

  - AllowSimplePassword

  - PasswordExpiration

  - PasswordHistory

  - DisableRemovableStorage

  - DisableIrDA

  - DisableDesktopSync

  - BlockRemoteDesktop

  - BlockInternetSharing

