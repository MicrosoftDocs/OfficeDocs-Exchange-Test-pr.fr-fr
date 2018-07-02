---
title: "Réponse et routage automatique d'appels entrants: Exchange 2013 Help"
TOCTitle: Réponse et routage automatique d'appels entrants
ms:assetid: d3dcd488-bd57-44cc-bdd4-ddee42a69dde
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb124724(v=EXCHG.150)
ms:contentKeyID: 50479237
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Réponse et routage automatique d'appels entrants

 

_**Sapplique à :** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2013-08-26_

La messagerie unifiée Microsoft Exchange vous permet de créer un ou plusieurs standards automatiques de messagerie unifiée en fonction des besoins de votre organisation. Contrairement aux autres composants de messagerie unifiée, tels que les plans de numérotation et les passerelles IP de messagerie unifiée, vous n'êtes pas obligé de créer des standards automatiques de messagerie unifiée. Toutefois, les standards automatiques aident des appelants internes et externes à localiser des utilisateurs ou départements d'une organisation et à leur transférer des appels. Cette rubrique présente la fonctionnalité de standard automatique de la messagerie unifiée.

**Contenu de cette rubrique**

Les standards automatiques

Standards automatiques de messagerie unifiée

Standards automatiques en plusieurs langues

Messages d'accueil pour les heures d'ouverture et en dehors des heures d'ouverture

Entrées de navigation par menu

Exemples de standards automatiques

## Les standards automatiques

Dans des environnements de messagerie unifiée ou de téléphonie, un standard automatique ou un système de menus de standard automatique transfère les appelants vers le poste d'un utilisateur ou d'un département sans intervention d'un réceptionniste ou d'un opérateur. Dans de nombreux systèmes de standard automatique, vous pouvez joindre un réceptionniste ou un opérateur en appuyant sur la touche zéro ou en prononçant le mot zéro. Le standard automatique est une fonctionnalité disponible dans la plupart des autocommutateurs privés (PBX), PBX IP et solutions de messagerie unifiée actuelles.

Certains systèmes de standard automatique comportent des menus d'information uniquement pour les messages et des menus vocaux qui permettent à une organisation d'indiquer ses heures d'ouverture, l'itinéraire d'accès à ses locaux, les opportunités d'emploi et d'autres réponses à des questions fréquemment posées. Une fois le message lu, les appelants sont transférés vers le réceptionniste ou l'opérateur, ou peuvent revenir au menu principal.

Dans des systèmes de standard automatique plus complexes, le système de menus permet de rechercher d'autres menus de standard automatique, de localiser d'autres utilisateurs dans le système ou de transférer l'appel à une autre ligne téléphonique extérieure. Le système de menus permet aussi de laisser l'appelant interagir avec le système dans certaines situations, par exemple lorsqu'un étudiant s'inscrit à un cours à l'université, consulte ses résultats ou lorsque vous activez une carte de crédit par téléphone.

Bien que les standards automatiques puissent être très utiles, ils peuvent être une source de confusion et de frustration pour l'appelant s'ils ne sont pas conçus et configurés correctement. Par exemple, dans des organisations importantes, si un standard automatique n'est pas conçu correctement, les appelants peuvent être confrontés à une série interminable de questions et d'invites de menu avant d'être mis en relation avec la personne qui doit répondre à leur question.

## Standards automatiques de messagerie unifiée

La messagerie unifiée vous permet de créer un ou plusieurs standards automatiques de messagerie unifiée en fonction des besoins de votre organisation. Les standards automatiques de messagerie unifiée servent à créer un système de menus vocaux pour une organisation, qui permet aux appelants internes et externes de naviguer dans le système de menus du standard automatique de messagerie unifiée pour localiser, et passer ou transférer des appels à des utilisateurs ou départements d'une organisation.

Lorsque des utilisateurs anonymes ou non authentifiés appellent un numéro de téléphone externe ou lorsque des appelants internes composent un numéro de poste défini, ils accèdent à une série de messages d'assistance vocaux qui les aident à contacter un utilisateur ou à le localiser dans l'organisation, puis à l'appeler. Le standard automatique de messagerie unifiée est une série de messages d'assistance vocaux ou de fichiers .wav que les appelants entendent à la place d'un opérateur humain quand ils contactent une organisation disposant de la messagerie unifiée. Le standard automatique de messagerie unifiée permet aux appelants de naviguer dans le système de menus, de passer des appels ou de localiser des utilisateurs à l'aide des entrées DTMF (numérotation en fréquences vocales) ou vocales. Toutefois, pour la reconnaissance vocale (ASR) ou les entrées vocales à utiliser, vous devez activer l'ASR sur le standard automatique de messagerie unifiée.

Un standard automatique de messagerie unifiée offre les fonctions suivantes :

  - Il émet un message d'accueil professionnel ou informatif.

  - Il offre des menus professionnels personnalisés. Vous pouvez personnaliser ces menus afin d'obtenir plusieurs niveaux.

  - Il fournit une fonction de recherche d'annuaire qui permet à l'appelant de rechercher un nom dans l'annuaire de l'organisation.

  - Il permet à un appelant de se connecter au téléphone des membres de l'organisation ou de leur laisser des messages.

Il n'y a pas de limite au nombre de standards automatiques de messagerie unifiée pouvant être créés. Chaque standard automatique de messagerie unifiée peut prendre en charge un nombre illimité de postes. Un standard automatique de messagerie unifiée ne peut référencer qu'un seul plan de numérotation de messagerie unifiée. Les standards automatiques de messagerie unifiée peuvent également faire référence ou être liés à d'autres standards automatiques de messagerie unifiée.

Un appel entrant reçu depuis un numéro de téléphone externe ou un poste téléphonique interne est d'abord transmis entre des serveurs Exchange, puis envoyé à un standard automatique de messagerie unifiée. Le standard automatique de messagerie unifiée est configuré par l'administrateur système pour utiliser des fichiers vocaux pré-enregistrés (\*.wav) qui sont lus par téléphone à l'appelant, permettant à ce dernier de naviguer dans le système de menus de la messagerie unifiée. Vous pouvez personnaliser tous les fichiers \*.wav utilisés lorsque vous configurez un standard automatique de messagerie unifiée pour répondre aux besoins de votre organisation.

Retour au début

## Standards automatiques en plusieurs langues

Dans certaines situations, il se peut que vous deviez offrir aux appelants des standards automatiques en plusieurs langues. Le paramètre de langue disponible sur un standard automatique de messagerie unifiée vous permet de configurer la langue d'invite par défaut sur le standard automatique. Lorsque vous utilisez les invites système par défaut pour le standard automatique, il s'agit de la langue que l'appelant entend lorsque le standard automatique répond à l'appel entrant. Ce paramètre de langue affecte seulement les invites système par défaut fournies. Ce paramètre de langue n'a aucune incidence sur les messages personnalisés configurés sur un standard automatique.

Pour les déploiements locaux et hybrides, si vous installez la version anglaise (États-Unis), l'anglais É.U. est la seule langue qui peut être configurée sur les standards automatiques de messagerie unifiée. Si vous installez une version localisée, par exemple en japonais, vous pouvez configurer le standard automatique que vous créez pour utiliser le japonais ou l'anglais É.U. comme langue par défaut. Vous pouvez installer des modules linguistiques de messagerie unifiée supplémentaires sur un serveur de messagerie unifiée pour pouvoir utiliser d'autres langues par défaut sur un standard automatique.

Par exemple, si vous possédez une entreprise basée aux États-Unis mais qui requiert un système de menus proposant aux appelants des options en anglais É.U., en espagnol et en français, vous devez d'abord installer les modules linguistiques de messagerie unifiée dont vous avez besoin. Dans ce cas, si vous avez installé la version anglaise (É.U.), vous devez installer les modules linguistiques de messagerie unifiée en espagnol et français. Toutefois, comme il n'est possible de configurer qu'une seule langue à la fois pour un standard automatique de messagerie unifiée, vous devez créer quatre standards automatiques : un standard automatique principal configuré pour utiliser l'anglais É.U., puis un standard automatique pour chaque langue : anglais É.U., espagnol et français. Vous devez ensuite configurer le standard automatique principal pour qu'il dispose des mappages de touches ou d'une navigation par menu appropriés pour accéder aux autres standards automatiques que vous avez créés pour chaque langue. Dans cet exemple, le standard automatique principal répond à l'appel entrant et l'appelant entend le message : « Bienvenue chez Contoso, Ltd. Pour l'anglais, appuyez sur ou dites 1. Pour l'espagnol, appuyez sur ou dites 2. Pour le français , appuyez sur ou dites 3.»

<table>
<thead>
<tr class="header">
<th><img src="images/Bb125224.tip(EXCHG.150).gif" title="Conseil" alt="Conseil" />Conseil :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Dans la messagerie unifiée Exchange, les utilisateurs d’Outlook Voice Access authentifiés et non authentifiés ne peuvent pas rechercher des utilisateurs dans l’annuaire à l’aide de la saisie vocale, quelle que soit la langue. Toutefois, les appelants qui passent par un standard automatique peuvent utiliser la saisie vocale dans plusieurs langues pour parcourir les menus du standard et rechercher des utilisateurs dans l’annuaire.</td>
</tr>
</tbody>
</table>


Retour au début

## Messages d'accueil pour les heures d'ouverture et en dehors des heures d'ouverture

Une fois qu'un standard automatique de messagerie unifiée est créé, un message d'assistance vocale système par défaut est utilisé comme message d'accueil de menu principal en dehors des heures d'ouverture. Ce message est écouté par les appelants après le message d'accueil en dehors des heures d'ouverture. Bien que les messages d'assistance vocale du système ne doivent pas être remplacés ni modifiés, vous pouvez personnaliser les messages d'accueil et les messages d'assistance vocale de menu utilisés avec les standards automatiques de messagerie unifiée. Souvent, outre la configuration d'un message d'accueil personnalisé en dehors des heures d'ouverture, vous devez créer et configurer un message d'accueil personnalisé de menu principal en dehors des heures d'ouverture. Après avoir configuré un message d'accueil de menu principal en dehors des heures d'ouverture personnalisé, vous devez activer des mappages de touches sur le standard automatique de messagerie unifiée pour les heures de fermeture.

Un message d'accueil de menu principal en dehors des heures d'ouverture personnalisé est une liste d'options indiquée aux appelants en dehors des heures d'ouverture. Pour permettre aux appelants d'entendre un message d'accueil personnalisé de menu principal en dehors des heures d'ouverture, vous devez commencer par configurer le planning des heures d'ouverture et de fermeture à l'aide du Centre d'administration Exchange ou de la cmdlet **Set-UMAutoAttendant** de l'environnement de ligne de commande Exchange Management Shell. Par exemple, « Vous venez de contacter Trey Research en dehors des heures d'ouverture normales. Si vous êtes confronté à une urgence médicale, raccrochez et composez le 911. Pour laisser un message à l'adresse de l'un de nos médecins, appuyez sur la touche 1. Pour laisser un message à l'adresse de l'un de nos thérapeutes, appuyez sur la touche 2. Pour laisser un message général à l'adresse de l'un de nos coordinateurs, appuyez sur la touche 3. Pour être mis en communication avec l'un de nos opérateurs pendant les heures de fermeture, appuyez sur la touche 0. »

Par défaut, quand vous créez un standard automatique de messagerie unifiée, les messages d'assistance vocaux ou messages d'accueil pendant ou en dehors des heures d'ouverture ne sont pas configurés et aucune entrée de navigation par menu n'est définie pour les messages d'assistance vocaux de menu principal pendant ou en dehors des heures d'ouverture. Pour configurer correctement des messages d'accueil et des messages d'assistance vocaux de menu principal en dehors des heures d'ouverture :

1.  Configurez les heures d'ouverture et de fermeture dans la page **Heures d'ouverture**.

2.  Créez le fichier de message d'accueil qui sera utilisé en dehors des heures d'ouverture.

3.  Configurez le message d'accueil en dehors des heures d'ouverture dans la page **Messages d'accueil**.

4.  Créez le fichier de message d'accueil à utiliser pour le message d'accueil de menu principal en dehors des heures d'ouverture.

5.  Configurez le message d'accueil de menu principal en dehors des heures d'ouverture dans la page **Messages d'accueil**.

6.  Activez la navigation par menu et ajoutez des entrées de navigation dans la page **Navigation par menu**.

Retour au début

## Entrées de navigation par menu

Si vous utilisez le message d'accueil de menu principal par défaut et définissez une ou plusieurs entrées de navigation par menu, le moteur TTS (conversion de texte par synthèse vocale) de la messagerie unifiée synthétise un message d'assistance vocal de menu principal. Toutefois, le moteur TTS ne synthétise le message d'assistance vocal de menu principal que si le message d'accueil par défaut est configuré et qu'au moins une entrée de navigation par menu a été définie. Le moteur TTS ne synthétise pas une invite du menu principal si vous utilisez un message personnalisé, tel que « Pour le service commercial, appuyez sur 1. Pour le service d'assistance, appuyez sur 2. » Pour créer cette invite du menu principal, vous devez créer deux entrées de navigation par menu : l'un nommé « Département des ventes » et l'autre « Service après vente », puis configurer l'entrée de mappage de touches pour lire un fichier audio, effectuer un transfert vers un numéro de poste ou transférer l'appelant vers un autre standard automatique.

Lorsque vous configurez des entrées de navigation par menu, vous définissez les options et les opérations qui seront effectuées si un appelant prononce une phrase alors qu'il utilise un standard automatique à reconnaissance vocale, ou s'il appuie sur une touche du clavier téléphonique alors qu'il utilise un standard automatique sans reconnaissance vocale. Pour configurer des entrées de navigation par menu pour un standard automatique, vous devez :

  - activer la navigation de menu en dehors des heures d'ouverture ;

  - ajouter des entrées de navigation par menu ;

  - saisir le nom de l'entrée de navigation de menu.

  - Sélectionnez une option dans la liste **Lorsque cette touche est enfoncée**, et télécharger le fichier audio à lire dans le champ **Lire le fichier audio suivant**.

  - Configurer l'action à exécuter :
    
      - Transférer vers ce poste
    
      - Transférer vers ce standard automatique de messagerie unifiée
    
      - Laisser un message vocal à cet utilisateur
    
      - Annoncer l'adresse de l'entreprise
    
      - Annoncer les heures d'ouverture

Retour au début

## Exemples de standards automatiques

Les exemples suivants montrent comment utiliser des standards automatiques de messagerie unifiée avec la messagerie unifiée :

  - **Exemple 1**   Les clients externes de la société Contoso, Ltd peuvent utiliser trois numéros de téléphones externes : 425-555-0111 (Bureaux), 425-555-0122 (Support technique) et 425-555-0133 (Ventes). Les départements Ressources humaines, Administration et Comptabilité ont des postes téléphoniques internes et ne sont accessibles que via le standard automatique de messagerie unifiée des bureaux.
    
    Pour créer une structure de standard automatique de messagerie unifiée qui prend en charge ce scénario, créez et configurez trois standards automatiques de messagerie unifiée, chacun avec les numéros de téléphone externes appropriés. Créez trois autres standards automatiques de messagerie unifiée pour chaque service des bureaux de l'entreprise. Vous configurez ensuite chaque standard automatique de messagerie unifiée en fonction de vos besoins, par exemple en choisissant un type de message d'accueil ou en introduisant d'autres informations de navigation.

  - **Exemple 2**   Les clients externes de la société Contoso, Ltd appellent le numéro principal de l'entreprise, à savoir le 425-555-0100. Quand un appelant externe compose le numéro externe, le standard automatique de messagerie unifiée répond en disant « Bienvenue chez Contoso, Ltd. Appuyez sur la touche 1 ou dites « Un » pour être transféré au service Administration. Appuyez sur la touche 2 ou dites « Deux » pour être transféré au service Support technique. Appuyez sur la touche 3 ou dites « Trois » pour être transféré au service Informations sur l'entreprise. Appuyez sur la touche 0 ou dites « Zéro » pour être transféré vers l'opérateur. » Pour créer une structure de standard automatique de messagerie unifiée qui prend en charge ce scénario, vous créez un standard automatique de messagerie unifiée avec des postes personnalisés qui acheminent l'appel vers le numéro de poste approprié.

Retour au début

