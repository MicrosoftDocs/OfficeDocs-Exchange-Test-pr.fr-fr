---
title: 'Messagerie unifiée: Exchange 2013 Help'
TOCTitle: Messagerie unifiée
ms:assetid: 004b5d1a-cae8-4034-ab65-db41bd2f7b97
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ150478(v=EXCHG.150)
ms:contentKeyID: 50477409
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Messagerie unifiée

 

_**Sapplique à :**Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :**2016-12-09_

La messagerie unifiée permet aux utilisateurs d'utiliser la messagerie vocale, ainsi que d'autres fonctionnalités, telles que Outlook Voice Access et les règles de répondeur automatique. La messagerie unifiée combine la messagerie vocale et la messagerie électronique dans une boîte aux lettres accessible à partir de nombreux types d'appareils. Les utilisateurs peuvent écouter leurs messages à partir de leur boîte de réception de messagerie ou en utilisant Outlook Voice Access à partir d'un téléphone. Vous avez le contrôle sur la façon dont les utilisateurs passent des appels sortants à partir de la messagerie unifiée, et ce qu'ils entendent quand ils appellent votre organisation.

Actuellement, les administrateurs informatiques gèrent fréquemment les réseaux de messagerie vocale ou de téléphonie, ainsi que les systèmes de messagerie électronique ou les réseaux de données pour leurs organisations comme des systèmes distincts. Les messageries vocale et électronique se trouvent dans des boîtes de réception séparées. Elles sont hébergées sur des serveurs distincts accessibles via le bureau pour la messagerie électronique et via le téléphone pour la messagerie vocale.

La messagerie unifiée permet aux administrateurs Exchange de regrouper la messagerie vocale et la messagerie électronique dans une boîte aux lettres pour que les utilisateurs puissent écouter leurs messages vocaux dans leur boîte de réception ou via Outlook Voice Access à partir d'un téléphone. Elle utilise la banque d'informations Exchange pour les messages électroniques et vocaux.

**Contenu de cette rubrique**

Fonctionnalités nouvelles

Fonctionnalités de messagerie unifiée

Planification et déploiement de la messagerie unifiée

Gestion de la messagerie unifiée via le Centre d'administration Exchange (CAE) et l'environnement de ligne de commande Exchange Management Shell

Documentation de la messagerie unifiée

## Fonctionnalités nouvelles

D'abord introduite dans Microsoft Exchange Server 2007, la messagerie unifiée était également disponible dans Exchange 2010. La fonctionnalité de messagerie unifiée définie dans Exchange 2013 est similaire à celle des versions précédentes d'Exchange. Toutefois, certaines nouveautés ont été introduites et quelques modifications architecturales ont été apportées. La messagerie unifiée est maintenant considérée comme un composant ou une sous-fonction des fonctionnalités vocales proposées dans Exchange 2013. Le terme *Messagerie unifiée* est toujours très utilisé dans les cmdlets de l'environnement de ligne de commande Exchange Management Shell et les services de messagerie unifiée. En outre, tous les composants de messagerie unifiée, tels que les plans de numérotation, les standards automatiques, les stratégies de boîte aux lettres de messagerie unifiée ou les passerelles IP de messagerie unifiée, ainsi que la fonctionnalité permettant de les gérer, se trouvent à l'intérieur du nœud de messagerie unifiée dans le volet de navigation du Centre d'administration Exchange.

Les rubriques suivantes vous donnent accès à des informations sur les fonctionnalités nouvelles ou améliorées de la messagerie unifiée Exchange 2013 :

  - [Modifications de l’architecture vocale](voice-architecture-changes-exchange-2013-help.md)

  - [Prise en charge d’IPv6 dans la messagerie unifiée](ipv6-support-in-unified-messaging-exchange-2013-help.md)

  - [Améliorations d'aperçu de messagerie vocale](voice-mail-preview-enhancements-exchange-2013-help.md)

  - [Mises à jour des cmdlets de messagerie unifiée](unified-messaging-cmdlet-updates-exchange-2013-help.md)

Retour au début

## Fonctionnalités de messagerie unifiée

Les fonctionnalités de messagerie vocale disponibles dans la messagerie unifiée offrent des avantages aux utilisateurs et aux administrateurs informatiques.

## Fonctionnalités pour les utilisateurs

Quand vous déployez la messagerie unifiée, les utilisateurs peuvent accéder aux messages vocaux et électroniques, ainsi qu'aux informations de calendrier qui se trouvent dans leur boîte aux lettres, à partir d'un client de messagerie, comme Outlook ou MicrosoftOutlook Web App, d'un téléphone mobile où Microsoft Exchange ActiveSync est configuré, tel qu'un Windows Phone, ou encore d'un téléphone fixe. En outre, les utilisateurs peuvent utiliser les fonctionnalités suivantes :

  - **Accès aux informations Exchange   **Les utilisateurs à extension messagerie unifiée peuvent accéder à un ensemble complet de fonctionnalités de messagerie vocale à partir de téléphones mobiles compatibles Internet, d'MicrosoftOffice Outlook 2007 ou versions ultérieures et d'Outlook Web App. Ces fonctionnalités incluent de nombreuses options de configuration de messagerie vocale, ainsi que la possibilité d'écouter un message vocal, soit à partir du volet de lecture à l'aide d'un lecteur Windows Media intégré, soit à partir de la liste des messages en utilisant les haut-parleurs de l'ordinateur.

  - **Émettre au téléphone**   La fonctionnalité Émettre au téléphone permet aux utilisateurs à messagerie unifiée d'écouter des messages vocaux au téléphone. Il peut cependant arriver que les utilisateurs ne souhaitent pas ou ne puissent pas écouter un message vocal dans les haut-parleurs de leur ordinateur, par exemple s'ils travaillent dans un environnement de travail organisé en box, s'ils utilisent un ordinateur public, si leur ordinateur ne permet pas de lire des fichiers multimédias ou si le message est confidentiel. Dans ce cas, ils peuvent écouter les messages vocaux en utilisant un téléphone fixe (privé ou professionnel) ou mobile.

  - **Écran de messagerie vocale**   L'écran de messagerie vocale ressemble au formulaire de courrier électronique par défaut. Il offre aux utilisateurs une interface permettant d'exécuter des actions telles que écouter, arrêter ou suspendre l'écoute des messages vocaux, écouter des messages vocaux au téléphone, ainsi que d'ajouter et de modifier des notes.
    
    L'écran de messagerie vocale comprend le lecteur Windows Media intégré et un champ Notes audio. Le lecteur Windows Media intégré et le champ Notes s'affichent soit dans le volet de lecture lorsque les utilisateurs visualisent un message vocal, soit dans une fenêtre indépendante quand ils l'ouvrent. Si la messagerie unifiée n'est pas activée ou si aucun client de messagerie pris en charge n'est installé sur l'ordinateur client, les messages vocaux sont présentés en tant que pièces jointes, et l'écran de messagerie vocale n'est pas disponible.

  - **Configuration utilisateur**   Un utilisateur disposant de la messagerie unifiée peut configurer plusieurs options de messagerie vocale pour la messagerie unifiée à l'aide d'Outlook Web App. Par exemple, l'utilisateur peut configurer des numéros d'accès téléphonique, le numéro de messagerie vocale « Émettre au téléphone » et réinitialiser un code confidentiel d'accès à la messagerie vocale.

  - **Répondeur automatique   **Le répondeur automatique permet de répondre à des appels entrants à la place des utilisateurs, de diffuser leur message d'accueil personnel, d'enregistrer des messages et de les envoyer à leur boîte de réception sous forme de message électronique.

  - **Règles de répondeur automatique**   Les règles de répondeur automatique permettent aux utilisateurs dont la messagerie vocale est activée de déterminer comment les appels entrants du répondeur automatique doivent être traités. Les règles de répondeur automatique et les règles de boîte de réception sont appliquées pratiquement de la même manière aux appels entrants et aux messages électroniques entrants, respectivement. Par défaut, aucune règle de répondeur automatique n'est configurée. Si un serveur de boîtes aux lettres répond à un appel entrant, l'appelant est invité à laisser un message vocal à la personne appelée. Grâce aux règles de répondeur automatique, un appelant peut effectuer les opérations suivantes :
    
      - laisser un message vocal à l'attention de l'utilisateur à messagerie unifiée ;
    
      - transférer son appel à un autre contact de l'utilisateur à messagerie unifiée ;
    
      - procéder à un transfert vers la messagerie vocale de cet autre contact ;
    
      - transférer son appel vers d'autres numéros de téléphone configurés par l'utilisateur à extension messagerie unifiée ;
    
      - utiliser la fonctionnalité de recherche ou localiser un utilisateur à extension messagerie unifiée via un transfert d'un opérateur.

  - **Aperçu de messagerie vocale**   Le serveur de boîtes aux lettres applique la reconnaissance vocale automatique aux nouveaux messages vocaux créés. Lorsque les utilisateurs reçoivent des messages vocaux, ces messages contiennent à la fois des données enregistrées et un texte créé à partir de l'enregistrement vocal. Les utilisateurs voient le texte du message vocal s'afficher dans un courrier électronique depuis Outlook Web App ou tout autre client de messagerie pris en charge.

  - **Indicateur de message en attente**   L'indicateur de message en attente est une fonctionnalité présente dans la plupart des systèmes de messagerie vocale hérités et peut désigner un mécanisme dont la fonction est d'indiquer l'existence d'un nouveau message. Dans Exchange 2007, cette fonctionnalité provenait d'une application tierce qui signalait la réception d'un nouveau message vocal par l'allumage d'un voyant sur le téléphone fixe. Cette fonctionnalité a été ajoutée à Exchange 2010 ; plus aucun logiciel tiers n'est nécessaire. L'activation ou désactivation de l'indicateur de message en attente a lieu dans la boîte aux lettres de l'utilisateur ou dans une stratégie de boîte aux lettres de messagerie unifiée.

  - **Notifications d'appels manqués et de messages vocaux par SMS**   Dans le cadre d'un déploiement hybride ou Office 365, si les utilisateurs configurent le transfert d'appels ainsi que les paramètres de messagerie vocale avec leur numéro de téléphone mobile, ils peuvent recevoir des notifications d'appels manqués et de nouveaux messages vocaux sur leurs téléphones mobiles, sous la forme d'un message texte transmis par SMS (Short Messaging Service). Cependant, pour recevoir ce type de notifications, les utilisateurs doivent avant tout configurer la messagerie texte et activer les notifications sur leur compte.

  - **Messagerie vocale protégée**   La messagerie vocale protégée est une fonctionnalité de la messagerie unifiée qui permet aux utilisateurs d'envoyer des messages privés. Ces messages sont protégés par les services AD RMS (Active Directory Rights Management Services), et les utilisateurs ne peuvent pas transférer, copier ni récupérer les fichiers vocaux à partir de leur messagerie électronique. La messagerie vocale protégée accroît la confidentialité de la messagerie unifiée et permet aux utilisateurs d'adresser leurs messages vocaux à un public restreint. Cette fonctionnalité traite les messages électroniques privés pratiquement de la même manière que dans Exchange 2007, mais elle s'applique maintenant aussi aux messages vocaux.

  - **Outlook Voice Access   **Les utilisateurs à messagerie unifiée peuvent accéder à deux interfaces utilisateur de messagerie unifiée : l'interface utilisateur téléphonique et l'interface utilisateur vocale. La combinaison de ces deux interfaces constitue Outlook Voice Access. Les utilisateurs Outlook Voice Access peuvent utiliser Outlook Voice Access quand ils accèdent au système de messagerie vocale à partir d'un téléphone interne ou externe. Les utilisateurs à extension messagerie unifiée qui accèdent à distance au système de messagerie vocale peuvent accéder à leur boîte aux lettres à l'aide d'Outlook Voice Access. À partir d'un téléphone, un utilisateur à messagerie unifiée peut :
    
      - accéder à sa messagerie vocale ;
    
      - écouter ses messages électroniques, les transférer ou y répondre ;
    
      - écouter les informations de calendrier ;
    
      - afficher ou appeler les contacts stockés dans l’annuaire de l’organisation ou bien un contact ou un groupe de contacts répertorié dans sa liste de contacts personnels.
    
      - accepter ou annuler des demandes de réunion ;
    
      - activer un message vocal d'absence ;
    
      - configurer des préférences de sécurité et des options personnelles.

  - **Envoi de messages à un groupe à l'aide d'Outlook Voice Access**   Dans Exchange 2007, les utilisateurs pouvaient au choix utiliser l'interface utilisateur téléphonique ou l'interface utilisateur vocale d'Outlook Voice Access pour envoyer des messages électroniques et des messages vocaux quand ils se connectaient à leur boîte aux lettres. En revanche, ils ne pouvaient envoyer un message électronique qu'à un seul contact de leur liste de contacts personnels. Pour en inclure plusieurs, ils devaient ajouter chaque destinataire individuellement ou ajouter le nom d'une liste de distribution à partir de l'annuaire de l'organisation. Dans Exchange 2013, quand un utilisateur se connecte à sa boîte aux lettres via Outlook Voice Access, il peut également envoyer des messages électroniques et vocaux aux utilisateurs d'un groupe stocké dans sa liste de contacts personnels.

Retour au début

## Fonctionnalités d'administration

Actuellement, la plupart des utilisateurs et des services informatiques gèrent séparément les messages vocaux et les messages électroniques. Les messageries vocale et électronique sont des boîtes de réception séparées, hébergées sur des serveurs distincts accessibles via le bureau pour la messagerie électronique et via le téléphone pour la messagerie vocale. La messagerie unifiée comporte une banque intégrée pour tous les messages et un accès au contenu via l'ordinateur et le téléphone.

Les administrateurs Exchange peuvent gérer la messagerie unifiée avec la même interface qu'ils utilisent pour gérer les autres fonctionnalités d'Exchange, à l'aide du Centre d'administration Exchange (CAE) et de l'environnement de ligne de commande Exchange Management Shell. Ils peuvent :

  - gérer les messageries vocale et électronique à partir d'une seule plateforme ;

  - gérer la messagerie unifiée à l'aide de commandes contenant des scripts ;

  - construire des infrastructures de messagerie unifiée hautement fiables et disponibles.

Exchange 2013 La messagerie unifiée offre aux administrateurs ce qui suit :

  - **Système de messagerie unifiée complet**   La messagerie unifiée offre une solution de messagerie vocale complète s'appuyant sur une infrastructure unique de stockage, de transport et d'annuaire. Le stockage est assuré par un serveur de boîtes aux lettres et le transfert des appels entrants à partir d'une passerelle voix sur IP ou d'un PBX IP est géré par un serveur d'accès au client. Tous les messages électroniques et vocaux peuvent être gérés à partir d'un seul point de gestion, grâce à une interface d'administration et à un jeu d'outils.

  - **Modèle de sécurité Exchange   **Le service de messagerie unifiée MicrosoftExchange sur un serveur de boîtes aux lettres et le service de routeur d'appels de messagerie unifiée MicrosoftExchange sur un serveur d'accès au client s'exécutent comme un compte de serveur Exchange unique.

  - **Regroupement des systèmes de messagerie vocale**   Actuellement, la plupart des systèmes de messagerie vocale requièrent que tous les composants du système soient installés dans chaque bureau physique d'une organisation. Dans ce type de configuration, les systèmes de messagerie vocale des succursales sont situés à l'extérieur du site central et doivent être administrés sur site. Cela augmente en général les coûts d'administration et rend celle-ci plus complexe. La messagerie unifiée vous permet de gérer votre système de messagerie vocale à partir d'un emplacement central. Pour créer un système de gestion centralisé pour la messagerie unifiée, placez quelques serveurs Exchange dans un centre de données ou à un autre emplacement, et le reste localement. Ensuite, déployez les passerelles voix sur IP, les PBX IP ou les contrôleurs SBC dans chacune des succursales en remplacement du système de messagerie vocale de celles-ci. De cette manière, vous pourrez réduire considérablement les coûts d'administration et de matériel.

  - **Rôles administratifs de messagerie unifiée intégrés**   Parmi les rôles administratifs propres à la messagerie unifiée destinés à gérer les fonctionnalités de messagerie unifiée et de messagerie vocale, on compte les suivants :
    
      - Boîtes aux lettres de messagerie unifiée
    
      - Messages de messagerie unifiée
    
      - Messagerie unifiée

  - **Prise en charge des télécopies entrantes**Exchange 2013 permet aux utilisateurs disposant d'une boîte aux lettres à extension messagerie unifiée de recevoir des télécopies. Ils peuvent recevoir des messages de télécopie en cas d'appel de leur numéro de poste.
    
    Les clients à la recherche d'une solution de télécopie devront déployer une solution de télécopie partenaire. Des solutions de télécopie sont disponibles auprès de plusieurs partenaires. Les solutions partenaires sont conçues pour être étroitement intégrées à Exchange et permettent aux utilisateurs à extension messagerie unifiée de recevoir des messages de télécopie entrants. Vous pouvez rechercher une solution de télécopie partenaire en consultant le site [Microsoft Pinpoint](https://go.microsoft.com/fwlink/?linkid=190238).

  - **Prise en charge de plusieurs langues   **   Tous les modules linguistiques disponibles sont pourvus du moteur de synthèse vocale (TTS) et de messages d'assistance vocaux préenregistrés pour chaque langue. Ils prennent également en charge la reconnaissance vocale. En revanche, la fonctionnalité d'aperçu des messages vocaux n'est disponible que pour certaines langues. Le module linguistique Français (fr-FR) est disponible sur le support d'installation et d'autres modules linguistiques de messagerie unifiée peuvent être téléchargés à partir du [Centre de téléchargement Microsoft](https://go.microsoft.com/fwlink/p/?linkid=266542).

  - **Standard automatique**   Un standard automatique est un ensemble de messages d'assistance vocale qui permet aux utilisateurs externes et internes d'accéder au système de messagerie vocale. Les utilisateurs peuvent utiliser le clavier du téléphone ou la saisie vocale pour naviguer dans le menu du standard automatique, appeler un utilisateur ou localiser un utilisateur de l'organisation puis l'appeler. Le standard automatique permet à l'administrateur de :
    
      - créer un menu personnalisé pour des utilisateurs externes ;
    
      - définir les messages d'accueil ayant valeur d'informations, les messages d'accueil pendant les heures d'ouverture et les messages d'accueil en dehors des heures d'ouverture ;
    
      - définir les plannings de congés ;
    
      - décrire la procédure de recherche dans l'annuaire de l'organisation ;
    
      - décrire la procédure permettant de contacter un utilisateur en indiquant son poste ;
    
      - décrire la procédure permettant d'appeler un utilisateur en le recherchant dans l'annuaire de l'organisation ;
    
      - autoriser les utilisateurs externes à appeler l'opérateur.

Retour au début

## Planification et déploiement de la messagerie unifiée

La messagerie unifiée nécessite d'intégrer le déploiement d'Exchange Server avec le système de téléphonie existant pour votre organisation. Un déploiement réussi nécessite une analyse attentive de votre infrastructure de téléphonie et l'exécution des étapes de planification appropriées pour déployer et gérer la messagerie vocale dans la messagerie unifiée.

Lorsque vous planifiez le déploiement de votre messagerie unifiée, vous devez tenir compte de sa conception et d'autres problèmes qui pourraient vous empêcher d'atteindre vos objectifs d'organisation pendant son déploiement. Généralement, plus la topologie de messagerie unifiée est simple, plus son déploiement et sa maintenance sont aisés. Installez le moins de serveurs d'accès au client et de boîtes aux lettres possible et créez uniquement les composants de messagerie unifiée qui vous permettront d'atteindre les objectifs de l'organisation, comme les plans de numérotation de messagerie unifiée, les standards automatiques et les stratégies de boîte aux lettres de messagerie unifiée. Les grandes entreprises disposant d'environnements de réseau et de téléphonie complexes, de plusieurs divisions autonomes ou d'autres systèmes complexes nécessitent davantage de planification que les petites organisations avec des besoins de messagerie relativement simples.

Vous devez tenir compte de nombreux facteurs et les évaluer pour garantir un déploiement réussi de la messagerie unifiée. Vous devez connaître les différents aspects de la messagerie unifiée, ainsi que chaque composant et fonction, de façon à pouvoir planifier correctement l'infrastructure et le déploiement de la messagerie unifiée. Consacrez le temps nécessaire à la planification et à la résolution de ces problèmes pour garantir la réussite du déploiement de la messagerie unifiée au sein de votre organisation. Parmi les facteurs que vous devez prendre en compte et évaluer lorsque vous envisagez de déployer la messagerie unifiée dans votre organisation, on compte les suivants :

  - les besoins de votre organisation ;

  - les exigences de sécurité de votre organisation ;

  - vos infrastructures de téléphonie, réseau avec commutation de circuits et système de messagerie vocale actuels ;

  - la conception actuelle de votre réseau IP à commutations de paquets (y compris vos dispositifs et points de connectivité de réseau local et de réseau étendu) ;

  - votre environnement Active Directory actuel ;

  - le nombre d’utilisateurs à prendre en charge.

  - le nombre de serveurs d’accès au client et de boîtes aux lettres dont vous aurez besoin.

  - l’intégration ou non de la messagerie unifiée avec Microsoft Lync Server pour activer Enterprise Voice.

  - l'installation de passerelles voix sur IP, d'équipements de téléphonie et de serveurs d'accès au client et de boîtes aux lettres ;

  - le type de déploiement de messagerie unifiée, à savoir local ou hybride ;

  - les besoins de stockage des utilisateurs de la messagerie vocale.

Retour au début

## Gestion de la messagerie unifiée via le Centre d'administration Exchange (CAE) et l'environnement de ligne de commande Exchange Management Shell

**Gestion via le CAE**

Exchange 2013 fournit à votre organisation une console de gestion unifiée qui inclut tous les composants et fonctionnalités de messagerie unifiée. Le CAE propose une interface rationalisée optimisée pour la gestion des déploiements locaux, en ligne ou hybrides. Le CAE disponible dans Exchange 2013 remplace la console de gestion Exchange et le Panneau de configuration Exchange (ECP) d'Exchange 2010. Parmi les fonctionnalités du CAE, on compte les suivantes :

  - **Affichage Liste**   L'affichage Liste du CAE a permis de supprimer certaines restrictions qui existaient dans le Panneau de configuration Exchange. L’ECP ne pouvait afficher que 500 objets au maximum et, si vous souhaitiez afficher des objets qui n’étaient pas répertoriés dans le volet d’informations, vous deviez utiliser les fonctions de recherche et de filtrage pour trouver ces objets spécifiques. Dans Exchange 2013, la limite d'affichage de la liste du CAE est environ de 20 000 objets. D'autre part, la fonction de pagination a été ajoutée afin de pouvoir paginer les résultats. Vous pouvez également configurer la taille de page et exporter vers un fichier CSV.

  - **Ajout/suppression de colonnes dans la liste des destinataires**   Vous pouvez choisir les colonnes à afficher et enregistrer des listes personnalisées.

  - **Sécurisation du répertoire virtuel du Panneau de configuration Exchange**   Vous pouvez partitionner l'accès à partir d'Internet et d'intranets dans le répertoire virtuel IIS du Panneau de configuration Exchange pour autoriser ou interdire les fonctionnalités de gestion. Grâce à cette fonctionnalité, vous pouvez autoriser ou refuser l’accès des utilisateurs qui essaient d’accéder au Centre d’administration Exchange via Internet à l’extérieur de l’environnement de votre organisation tout en autorisant l’accès aux options Outlook Web App d’un utilisateur final.

  - **Gestion des dossiers publics**   Dans Exchange 2010 et Exchange 2007, les dossiers publics étaient gérés via la console d'administration des dossiers publics. Les dossiers publics se trouvent désormais dans le Centre d'administration Exchange et vous n'avez pas besoin d'aucun outil supplémentaire pour les gérer.

  - **Notifications**   Dans Exchange 2013, le Centre d'administration Exchange dispose désormais un afficheur de notifications qui permet de connaître l'état de processus de longue durée et, si vous le souhaitez, de recevoir une notification via un message électronique une fois le processus terminé.

  - **Éditeur des utilisateurs RBAC (contrôle d'accès basé sur un rôle)**   Dans Exchange 2010, vous pouviez utiliser l'Éditeur des utilisateurs RBAC pour ajouter des utilisateurs à des groupes de rôles de gestion. Dans Exchange 2013, la fonctionnalité Éditeur des utilisateurs RBAC se trouve maintenant dans le CAE. Vous n'avez pas besoin d'un outil distinct pour gérer le contrôle d'accès basé sur un rôle.

  - **Outils de messagerie unifiée**   Dans Exchange 2010, vous pouviez utiliser les outils Statistiques d'appel et Journaux des appels des utilisateurs pour fournir des statistiques de messagerie unifiée et des informations sur des appels spécifiques correspondant à un utilisateur à extension messagerie unifiée. Dans Exchange 2013, les outils Statistiques d'appel et Journaux des appels des utilisateurs se trouvent maintenant dans le CAE. Vous n'avez pas besoin d'un outil distinct pour les gérer.

**Gestion du Shell**

L'environnement de ligne de commande Exchange Management Shell, basé sur la technologie Windows PowerShell, est une interface de ligne de commande puissante qui permet d'automatiser les tâches d'administration. Avec le Shell, vous pouvez gérer tous les aspects d'Exchange. Vous pouvez activer de nouveaux comptes de messagerie, créer des connecteurs d'envoi et de réception, configurer les propriétés de base de données, gérer tous les aspects de la messagerie unifiée, et bien plus encore. Le shell peut effectuer chaque tâche exécutable par le CAE, et bien d'autres encore. En fait, lorsque vous faites quelque chose dans le Centre d'administration Exchange, c'est l'environnement de ligne de commande Exchange Management Shell qui travaille en arrière-plan.

Retour au début

## Documentation de la messagerie unifiée

Le tableau suivant contient des liens vers des rubriques qui vous aideront à découvrir et à gérer la messagerie unifiée Exchange.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Rubrique</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="new-voice-mail-features-exchange-2013-help.md">Nouvelles fonctionnalités de messagerie vocale</a></p></td>
<td><p>Découvrez les nouvelles fonctionnalités de Microsoft Exchange 2013.</p></td>
</tr>
<tr class="even">
<td><p><a href="planning-for-unified-messaging-exchange-2013-help.md">Planification de la messagerie unifiée</a></p></td>
<td><p>Découvrez les concepts et les informations dont vous aurez besoin pour planifier le déploiement de la messagerie unifiée.</p></td>
</tr>
<tr class="odd">
<td><p><a href="deploying-voice-mail-and-um-exchange-2013-help.md">Déploiement de la messagerie vocale et la messagerie unifiée</a></p></td>
<td><p>Découvrez les exigences et les étapes de déploiement de la messagerie vocale et de la messagerie unifiée.</p></td>
</tr>
<tr class="even">
<td><p><a href="um-languages-prompts-and-greetings-exchange-2013-help.md">Langues de messagerie unifiée, invites et messages d’accueil</a></p></td>
<td><p>Découvrez les modules linguistiques de messagerie unifiée et les paramètres de langue.</p></td>
</tr>
<tr class="odd">
<td><p><a href="telephone-system-integration-with-um-exchange-2013-help.md">Intégration des systèmes téléphoniques à la messagerie unifiée</a></p></td>
<td><p>Obtenez plus d'informations sur l'intégration de votre réseau de téléphonie à la messagerie unifiée.</p></td>
</tr>
<tr class="even">
<td><p><a href="connect-your-voice-mail-system-to-your-telephone-network-exchange-2013-help.md">Connexion de votre système de messagerie vocale à votre réseau téléphonique</a></p></td>
<td><p>Apprenez à utiliser et à configurer les composants de messagerie unifiée pour connecter votre réseau de téléphonie à la messagerie unifiée Exchange.</p></td>
</tr>
<tr class="odd">
<td><p><a href="automatically-answer-and-route-incoming-calls-exchange-2013-help.md">Réponse et routage automatique d'appels entrants</a></p></td>
<td><p>Apprenez à créer des standards automatiques de messagerie unifiée et à gérer les paramètres des menus de navigation et des messages d'accueil pendant les heures d'ouverture ou en dehors de ces heures.</p></td>
</tr>
<tr class="even">
<td><p><a href="set-up-voice-mail-for-users-exchange-2013-help.md">Configurer la messagerie vocale pour les utilisateurs</a></p></td>
<td><p>Apprenez à créer et gérer des stratégies de boîte aux lettres de messagerie unifiée et à activer la messagerie unifiée pour des utilisateurs.</p></td>
</tr>
<tr class="odd">
<td><p><a href="set-up-client-voice-mail-features-exchange-2013-help.md">Configurer les fonctionnalités de messagerie vocale cliente</a></p></td>
<td><p>Apprenez à définir des fonctionnalités client pour autoriser les utilisateurs à accéder et à gérer leurs messages vocaux.</p></td>
</tr>
<tr class="even">
<td><p><a href="set-outlook-voice-access-pin-security-exchange-2013-help.md">Définition de la sécurité des codes confidentiels d'Outlook Voice Access</a></p></td>
<td><p>Apprenez à définir des codes confidentiels pour les utilisateurs Outlook Voice Access.</p></td>
</tr>
<tr class="odd">
<td><p><a href="protect-voice-mail-exchange-2013-help.md">Protéger la messagerie vocale</a></p></td>
<td><p>Apprenez à utiliser la messagerie unifiée pour protéger les messages vocaux.</p></td>
</tr>
<tr class="even">
<td><p><a href="run-reports-for-voice-mail-calls-exchange-2013-help.md">Pour exécuter des rapports pour les appels de messagerie vocale</a></p></td>
<td><p>Découvrez les rapports d'appels de la messagerie unifiée.</p></td>
</tr>
</tbody>
</table>

