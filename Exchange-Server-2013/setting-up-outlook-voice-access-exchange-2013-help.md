---
title: 'Configuration d’Outlook Voice Access: Exchange 2013 Help'
TOCTitle: Configuration d’Outlook Voice Access
ms:assetid: 5ce8c877-35f3-4e55-a65e-5ca469aeae99
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dd298010(v=EXCHG.150)
ms:contentKeyID: 50555413
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configuration d’Outlook Voice Access

 

_**Sapplique à :** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2015-03-09_

Microsoft Outlook Voice Access permet aux utilisateurs à extension messagerie unifiée (MU) d’accéder à leurs boîtes aux lettres à l’aide d’un téléphone analogique, numérique ou mobile.

Un utilisateur Outlook Voice Access (également appelé *abonné*) est un utilisateur activé pour la messagerie unifiée au sein d’une organisation. Les abonnés utilisent Outlook Voice Access pour accéder à leurs boîtes aux lettres par téléphone pour extraire leur courrier électronique, messages vocaux, contacts personnels et informations de calendrier.

**Contenu de cette rubrique**

Vue d’ensemble d’Outlook Voice Access

Interfaces Outlook Voice Access

Scénarios Outlook Voice Access

Groupes de distribution et groupes de contacts

Choix d’une langue

Contrôle des fonctionnalités d’Outlook Voice Access

## Vue d’ensemble d’Outlook Voice Access

Dans la messagerie unifiée Exchange, un utilisateur à extension messagerie unifiée peut appeler un numéro de téléphone interne ou externe configuré sur un plan de numérotation de messagerie unifiée pour accéder à sa boîte aux lettres et utiliser le système de menus Outlook Voice Access. Grâce à ce menu, les utilisateurs à extension messagerie unifiée peuvent lire des messages électroniques, écouter des messages vocaux, interagir avec leur calendrier Outlook, accéder à leurs contacts personnels et effectuer des tâches, telles que la configuration de leur code confidentiel Outlook Voice Access et l’enregistrement de messages d’accueil vocaux.

Deux types d’utilisateurs, authentifiés et non authentifiés, peuvent appeler un numéro Outlook Voice Access. Lorsqu’un utilisateur non authentifié appelle un numéro Outlook Voice Access qui est défini sur un plan de numérotation de messagerie unifiée, il ne peut qu’effectuer des recherches dans l’annuaire des utilisateurs. Les utilisateurs authentifiés, ceux qui entrent leur code confidentiel, peuvent effectuer des recherches dans l’annuaire et se connecter à leur boîte aux lettres pour consulter les messages électroniques, les éléments de calendrier, la messagerie vocale, et rechercher des contacts personnels. Lorsqu’ils recherchent un utilisateur dans le répertoire ou les contacts personnels, une fois qu’ils ont trouvé l’utilisateur, ils peuvent transférer des appels vers un utilisateur ou appeler le poste de l’utilisateur.

## Interfaces Outlook Voice Access

Deux interfaces d’utilisateur de messagerie unifiée sont proposées aux utilisateurs d’Outlook Voice Access : l’interface utilisateur téléphonique et l’interface utilisateur vocale qui utilise la reconnaissance vocale automatique.

Avant que les utilisateurs puissent utiliser l’interface utilisateur vocale dans Outlook Voice Access, elle doit être activée sur le plan de numérotation de messagerie unifiée et sur la stratégie de boîte aux lettres de messagerie unifiée. Elle doit également être activée pour l’utilisateur. Par défaut, lorsque vous créez un plan de numérotation et une stratégie de boîte aux lettres de messagerie unifiée et que vous activez la messagerie vocale pour un utilisateur, l’utilisateur peut faire appel à la reconnaissance vocale ou à l’interface utilisateur vocale pour parcourir des menus, des messages et autres options. Cependant, même si l’utilisateur peut utiliser l’interface utilisateur vocale, il doit utiliser le pavé numérique du téléphone pour saisir son code confidentiel, explorer des options personnelles et effectuer des recherches dans l’annuaire. Les paramètres par défaut sont répertoriés dans le tableau suivant.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Composant de messagerie unifiée</th>
<th>Paramètre par défaut</th>
<th>Exemple d’environnement de ligne de commande Exchange Management Shell pour activer l’accès à l’interface utilisateur vocale</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Plan de numérotation de messagerie unifiée</p></td>
<td><p>Activé</p></td>
<td><p><code>Set-UMDialPlan -id MyUMDialPlan -AutomaticSpeechRecognitionEnabled  $true</code></p></td>
</tr>
<tr class="even">
<td><p>Stratégie de boîte aux lettres de messagerie unifiée</p></td>
<td><p>Activé</p></td>
<td><p><code>Set-UMMaiboxPolicy -id MyUMPolicy -AllowAutomaticSpeechRecognition  $true</code></p></td>
</tr>
<tr class="odd">
<td><p>Boîte aux lettres de l’utilisateur</p></td>
<td><p>Activé</p></td>
<td><p><code>Set-UMMailbox -id tonysmith -AutomaticSpeechRecognitionEnabled $true</code></p></td>
</tr>
</tbody>
</table>


La section suivante comprend des scénarios qui décrivent la fonctionnalité d’interface utilisateur vocale.

Vue d’ensemble d’Outlook Voice Access

## Scénarios Outlook Voice Access

Voici quelques exemples d’utilisation d’Outlook Voice Access sur un téléphone :

  - **Accès à la messagerie**   Un utilisateur Outlook Voice Access appelle un numéro Outlook Voice Access à partir d’un téléphone et souhaite accéder à sa messagerie. L’invite vocale dit : « Bienvenue vous êtes connecté à Microsoft Exchange. Pour accéder à votre boîte aux lettres, entrez votre numéro de poste. Pour contacter une personne, appuyez sur la touche dièse. » Après que l’utilisateur ait saisi un numéro de poste, le message d’assistance vocale dit : « Entrez votre code confidentiel, puis appuyez sur la touche dièse. » Après que l’utilisateur ait saisit son code confidentiel, le message d’assistance vocale dit : « Vous avez deux nouveaux messages vocaux, 10 nouveaux messages électroniques et votre prochaine réunion est prévue à 10h00. Dites messagerie vocale, messagerie électronique, calendrier, contacts personnels, annuaire ou options personnelles. » Lorsque l’utilisateur prononce « Messagerie électronique », le système de messagerie vocale lit l’en-tête du message, puis le nom, l’objet, l’heure et l’importance des messages contenus dans la boîte aux lettres de l’utilisateur.

  - **Accès au calendrier**   Un utilisateur Outlook Voice Access appelle un numéro Outlook Voice Access à partir d’un téléphone et souhaite accéder à son calendrier. Le message d'assistance vocale dit : « Bienvenue, vous êtes connecté à Microsoft Exchange. Pour accéder à votre boîte aux lettres, entrez votre numéro de poste. Pour contacter une personne, appuyez sur la touche dièse. » Après que l’utilisateur ait saisi un numéro de poste, le message d’assistance vocale dit : « Entrez votre code confidentiel, puis appuyez sur la touche dièse. » Après que l’utilisateur ait saisit son code confidentiel, le message d’assistance vocale dit : « Vous avez deux nouveaux messages vocaux, 10 nouveaux messages électroniques et votre prochaine réunion est prévue à 10h00. Dites messagerie vocale, messagerie électronique, calendrier, contacts personnels, annuaire ou options personnelles. » Lorsque l’utilisateur dit « Calendrier », le système de messagerie vocale répond : « D’accord et quel jour dois-je ouvrir ? » L’utilisateur dit : « Aujourd’hui ». Le système de messagerie vocale répond en disant : « Ouverture du calendrier du jour ». Le système de messagerie vocale lit à l’utilisateur tous les rendez-vous de cette journée du calendrier.
    
    > [!NOTE]
    > Si un serveur de boîtes aux lettres exécutant le service de messagerie unifiée Microsoft Exchange rencontre un élément de calendrier endommagé dans la boîte aux lettres d’un utilisateur, il ne pourra pas lire l’élément, mais renverra l’appelant au menu principal d’Outlook Voice Access, et ne lira pas les autres réunions planifiées pour le reste de la journée.


  - **Accès à la messagerie vocale**   Un utilisateur Outlook Voice Access appelle un numéro Outlook Voice Access à partir d’un téléphone et souhaite accéder à sa messagerie vocale. Le message d'assistance vocale dit : « Bienvenue, vous êtes connecté à Microsoft Exchange. Pour accéder à votre boîte aux lettres, entrez votre numéro de poste. Pour contacter une personne, appuyez sur la touche dièse. » Après que l’utilisateur ait saisi un numéro de poste, le message d’assistance vocale dit : « Entrez votre code confidentiel, puis appuyez sur la touche dièse ». Après que l’utilisateur ait saisit son code confidentiel, le message d’assistance vocale dit : « Vous avez deux nouveaux messages vocaux, 10 nouveaux messages électroniques et votre prochaine réunion est prévue à 10h00. Dites messagerie vocale, messagerie électronique, calendrier, contacts personnels, annuaire ou options personnelles ». L’utilisateur prononce « Messagerie vocale », et la messagerie unifiée lit l’en-tête du message, puis le nom, l’objet, l’heure et l’importance des messages vocaux contenus dans la boîte aux lettres de l’utilisateur.
    
    > [!NOTE]
    > Si la reconnaissance vocale est activée, les utilisateurs peuvent accéder à leur boîte aux lettres à extension messagerie unifiée à l’aide d’instructions vocales. Les abonnés peuvent également utiliser un système à tonalité, également appelé DTMF (multifréquence bi-tonalité), en appuyant sur 0. La reconnaissance vocale n’est pas activée pour l’entrée de code confidentiel.


  - **Rechercher un utilisateur dans l’annuaire**   Un utilisateur Outlook Voice Access appelle un numéro Outlook Voice Access à partir d’un téléphone et souhaite rechercher une personne dans l’annuaire en épelant son alias de messagerie. Le message d'assistance vocale dit : « Bienvenue, vous êtes connecté à Microsoft Exchange. Pour contacter une personne, appuyez sur la touche dièse. » L’utilisateur appuie sur la touche dièse, pus utilise les entrées à tonalité pour épeler l’adresse SMTP de la personne.
    
    > [!NOTE]
    > La fonction de recherche dans l’annuaire avec un numéro Outlook Voice Access n’est pas activée pour la reconnaissance vocale. Les utilisateurs peuvent épeler le nom de la personne qu’ils souhaitent contacter uniquement en utilisant des entrées à tonalité.
    
    > [!IMPORTANT]
    > Dans certaines sociétés (en particulier en Asie orientale), aucune lettre n’est inscrite sur les touches du clavier téléphonique. Cela rend l’utilisation de la fonctionnalité d’écriture du nom à l’aide de l’interface à tonalité pratiquement impossible sans une connaissance approfondie du mappage des touches. Par défaut, la messagerie unifiée utilise le mappage de touches E.161. Par exemple, 2=ABC, 3=DEF, 4=GHI, 5=JKL, 6=MNO, 7=PQRS, 8=TUV, 9=WXYZ.
    
    Lors de l’entrée de la combinaison de lettres et de chiffres, par exemple Mike1092, les caractères numériques sont mappés sur eux-mêmes. Pour que l’alias de messagerie Mike1092 soit saisi correctement, l’utilisateur doit appuyer sur les touches 64531092. De même, pour des caractères autres que les lettres de A à Z et les chiffres de 0 à 9, il n’y a pas d’équivalent au niveau des touches téléphoniques. Il ne faut donc pas utiliser ces caractères. Par exemple, pour entrer l’alias de messagerie jim.wilson, il faut appuyer sur les touches 546945766. Même s’il y a 10 chiffres à entrer, l’utilisateur n’entre que 9 chiffres parce que le point (.) n’a pas d’équivalent numérique.

Vue d’ensemble d’Outlook Voice Access

## Groupes de distribution et groupes de contacts

Les utilisateurs peuvent utiliser Outlook Voice Access pour envoyer ou transférer un message vocal, un message électronique ou une demande de réunion. Vous pouvez envoyer ou transférer le message ou la demande de réunion à l’une des personnes suivantes :

  - Une personne de son dossier Contacts personnels

  - Une personne du carnet d’adresses partagé de son organisation

  - Un groupe de contacts qu’il a créé dans son dossier Contacts

  - Un groupe de distribution inclus dans le carnet d’adresses partagé de son organisation

Ils peuvent envoyer des messages et des demandes de réunion à l’aide de l’interface utilisateur vocale (si la reconnaissance vocale a été activée) ou à l’aide des entrées à tonalité sur le pavé numérique de son téléphone. Ils peuvent également utiliser Outlook Voice Access pour écouter les détails relatifs à un groupe, y compris les membres qui le composent.

> [!NOTE]
> Si un utilisateur essaie d’envoyer un message à un groupe (soit un groupe de distribution de son carnet d’adresses partagé, soit un groupe de contacts de son dossier Contacts personnels) qui ne comporte pas de membres, le système de messagerie vocale ne vous donne pas la possibilité d’envoyer ou de transférer le message ou la demande de réunion. S’ils essaient d’ajouter un groupe sans membre comme l’un des destinataires d’un message ou d’une demande de réunion qu’ils ont créé sur le téléphone, le système de messagerie vocale n’ajoutera pas le groupe au message et dira « Le message n’a pas pu être envoyé car le contact ne semble pas avoir d’adresse de messagerie valide. »


## Choix d’une langue

Les utilisateurs ne peuvent pas modifier la langue qu’Outlook Voice Access utilise pour s’adresser à eux et y répondre. Le système de messagerie vocale tente de rechercher et d’utiliser la meilleure correspondance pour la langue que l’utilisateur a choisie lorsqu’il s’est connecté à MicrosoftOutlook Web App ou la langue qu’il a choisie dans les paramètres régionaux d’Outlook Web App. Si la langue qu’il a choisie n’est pas prise en charge par Outlook Voice Access, le système de messagerie vocale utilise la même langue que celle entendue par les appelants lorsqu’ils sont invités à laisser un message vocal.

Vue d’ensemble d’Outlook Voice Access

## Contrôle des fonctionnalités d’Outlook Voice Access

Par défaut, lorsque les utilisateurs se connectent à Outlook Voice Access, ils peuvent utiliser le téléphone pour accéder à leur calendrier, leur messagerie et leurs contacts personnels, et effectuer des recherches dans l’annuaire. Vous pouvez utiliser l’environnement de ligne de commande Exchange Management Shell pour empêcher les utilisateurs d’accéder à une ou plusieurs de ces fonctionnalités lorsqu’ils utilisent Outlook Voice Access pour accéder à leur boîte aux lettres. Lorsque vous modifiez les fonctionnalités d’Outlook Voice Access sur une stratégie de boîte aux lettres de messagerie unifiée, vos modifications concernent tous les utilisateurs qui sont associés à la stratégie de boîte aux lettres de messagerie unifiée. Vous pouvez également désactiver certaines fonctionnalités sur une boîte aux lettres d’utilisateur unique, même si d’autres fonctionnalités peuvent être uniquement désactivées sur une stratégie de boîte aux lettres de MU et qu’elles ne sont pas disponibles sur une boîte aux lettres individuelle.

> [!NOTE]
> Vous pouvez uniquement utiliser l’environnement de ligne de commande Exchange Management Shell pour modifier les paramètres TUI d’Outlook Voice Access pour les utilisateurs à extension messagerie unifiée ou les stratégies de boîtes aux lettres de MU.


**Paramètres de stratégie de boîte aux lettres de MU**   Vous pouvez désactiver l’accès utilisateur aux fonctionnalités d’Outlook Voice Access suivantes sur une stratégie de boîte aux lettres de MU :

  - Reconnaissance vocale

  - Accès sans code confidentiel à la messagerie vocale

  - Réponses vocales à d’autres messages

  - Accès TUI à leur calendrier

  - Accès TUI au répertoire

  - Accès TUI à leur messagerie

  - Accès TUI à leurs contacts personnels

**Paramètres de boîte aux lettres à extension messagerie unifiée**   Vous pouvez désactiver l’accès d’un utilisateur aux fonctionnalités d’Outlook Voice Access suivantes sur la boîte aux lettres de l’utilisateur :

  - Accès TUI au calendrier

  - Accès TUI à la messagerie électronique

  - Reconnaissance vocale

Vous pouvez empêcher des utilisateurs de recevoir des messages vocaux, mais leur laisser la possibilité d’accéder à leur boîte aux lettres à l’aide d’Outlook Voice Access. Vous pouvez activer un utilisateur pour la messagerie unifiée et configurer sa boîte aux lettres avec un numéro de poste qui n’est pas attribué à un autre utilisateur de l’organisation.

Vue d’ensemble d’Outlook Voice Access

