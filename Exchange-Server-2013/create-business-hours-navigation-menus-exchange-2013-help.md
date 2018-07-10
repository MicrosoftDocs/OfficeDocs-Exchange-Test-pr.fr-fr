---
title: "Créer des heures d'ouverture des menus de navigation: Exchange 2013 Help"
TOCTitle: Créer des heures d'ouverture des menus de navigation
ms:assetid: f76472fd-aa1a-4cd8-8e26-cc674421d375
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb232203(v=EXCHG.150)
ms:contentKeyID: 50479580
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Créer des heures d'ouverture des menus de navigation

 

_**Sapplique à :** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2012-11-05_

Vous pouvez activer les mappages de touches heures pour un standard automatique de messagerie unifiée (MU). Après avoir créé un standard automatique de messagerie unifiée, une invite de commandes du système par défaut sera utilisé pour les heures ouvrées message d'accueil que les appelants entendront après que les heures ouvrées message de bienvenue de menu principal est émis. Les heures par défaut business indique de l'invite de commandes de menu principal, « Welcome to du standard automatique de Microsoft Exchange ». Car aucun mappage de clés n'est définis par défaut, aucune option de menu est disponible pour les appelants, et ils entendent uniquement l'invite du menu principal par défaut.

Lorsque vous configurez des mappages de touches, vous définissez les options et les opérations effectuées si un appelant prononce une phrase alors qu’il utilise un standard automatique à reconnaissance vocale, ou si l’appelant appuie sur la touche du clavier téléphonique alors qu’il utilise un standard automatique sans reconnaissance vocale.

Pour les autres tâches de gestion relatives aux standards automatiques de messagerie unifiée, consultez la rubrique [Procédures relatives au standard automatique de messagerie unifiée](um-auto-attendant-procedures-exchange-2013-help.md).

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : moins d'une minute.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l'entrée « Standards automatiques de messagerie unifiée » dans la rubrique [Autorisations de messagerie unifiée](unified-messaging-permissions-exchange-2013-help.md).

  - Avant d'exécuter ces procédures, vérifiez qu'un plan de numérotation de messagerie unifiée a été créé. Pour obtenir la procédure détaillée, consultez la rubrique [Créer un plan de numérotation de messagerie unifiée](create-a-um-dial-plan-exchange-2013-help.md).

  - Avant d'exécuter ces procédures, vérifiez qu'un standard automatique de messagerie unifiée a été créé. Pour obtenir la procédure détaillée, consultez la rubrique [Créer un standard automatique de messagerie unifiée](create-a-um-auto-attendant-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..


## Que souhaitez-vous faire ?

## Utiliser le CAE pour activer les heures de bureau standard automatiquement des mappages de touches sur une messagerie unifiée

1.  Dans le CAE, accédez à **Messagerie unifiée** \> **Plans de numérotation de messagerie unifiée**. Dans l'affichage Liste, sélectionnez le plan de numérotation de messagerie unifiée à modifier puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

2.  Dans la page **Plan de numérotation de messagerie unifiée**, sous **Standards automatiques de messagerie unifiée**, sélectionnez le standard automatique de messagerie unifiée pour lequel vous souhaitez créer un menu de navigation des heures ouvrées. Dans la barre d'outils, cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

3.  Dans la page de **Standard automatique de messagerie unifiée**, cliquez sur **navigation de Menu**, sous **navigation de menu des heures d'ouverture**, sélectionnez **Activer la navigation de menu les heures de bureau**, puis cliquez sur **Add**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter").

4.  Dans la page **nouvelle entrée de navigation de menu**, utilisez les options suivantes pour créer une nouvelle entrée de navigation :
    
      - **Invite**   Cette zone permet de saisir le nom du nouveau menu de navigation. Le nom du menu de navigation est uniquement utilisé à des fins d’affichage. Ce champ est obligatoire.
        
        Comme vous pouvez spécifier plusieurs nouveaux menus de navigation, nous vous recommandons d’utiliser des noms significatifs pour vos mappages de touches. La longueur maximale de ce nom est de 64 caractères et il peut contenir des espaces. Toutefois, il ne peut pas contenir les caractères suivants : " / \\ \[ \] : ; | = , + \* ? \< \>.
    
      - **Lorsque cette touche est enfoncée**   Utilisez cette liste pour activer le mappage de touches. Le mappage de touches est le numéro de la touche qu’un appelant doit enfoncer pour que le standard automatique effectue une opération spécifique, telle que le transfert d’un appelant vers un autre standard automatique ou un opérateur. Par défaut, aucune entrée n’est définie.
        
        La liste déroulante permet de taper la touche numérique (de 1 à 9) que l’appelant doit enfoncer. Zéro (0) est réservé pour l’opérateur de standard automatique.
        
        L'option **Délai d'attente** de la liste déroulante permet d'activer les appelants à transférer vers un numéro de poste ou un autre standard automatique s'ils n'enfoncent pas une touche du clavier du téléphone. Par exemple, «Veuillez patienter, un agent va bientôt vous répondre.» Le paramètre par défaut est 5 secondes. Si vous activez cette option, un mappage de touches vide est créé.
    
      - **Lire le fichier audio suivant**   Utilisez cette option pour sélectionner un fichier audio précédemment enregistré pour les appelants. Cliquez sur **Modifier** puis sur **Parcourir** pour accéder au fichier audio. Si vous laissez le fichier audio sur l'option par défaut \<Aucun\>, le moteur de conversion de texte par synthèse vocale (TTS) de messagerie unifiée synthétisera un message d'accueil de menu principal dans les heures d'ouverture. D'autre part, vous pouvez créer un fichier audio personnalisé pouvant être utilisé pour le message d'accueil du menu principal dans les heures d'ouverture pour un standard automatique à reconnaissance vocale. Le message peut être le suivant : « Pour laisser un message vocale pour les ventes, dites 1. Pour laisser un message vocal pour l'assistance technique, dites 2. Pour laisser un message vocal pour l'administration, dites 3. »
    
      - **Effectuer cette action supplémentaire**   Sélectionnez l’une des actions suivantes pour définir l’action que vous souhaitez que le standard automatique effectue pour le compte de l’appelant:
        
          - **Aucun**   Si vous ne voulez pas que le standard automatique transfert l'appel vers un poste ou un autre standard automatique, ni ne laisse de message pour un utilisateur, utilisez cette option.
        
          - **Transférer vers cette extension**   Sélectionnez cette option pour activer le transfert des appels vers une extension. Si vous activez cette action, utilisez la zone pour entrer le numéro de poste vers lequel l'appel sera transféré. Ce champ ne peut contenir que des caractères numériques. Il ne peut pas contenir les caractères suivants : " / \\ \[ \] : ; | = , + \* ? \< \>.
        
          - **Transférer vers ce standard automatique de messagerie unifiée**   Activez cette option pour transférer l'appel vers un standard automatique. Cliquez sur **Parcourir** pour localiser le standard automatique que vous voulez utiliser. Avant d'activer cette option, vous devez créer et configurer le standard automatique. Cette option est utilisée lorsque vous créez une structure parent/enfant de standards automatiques de messagerie unifiée.
        
          - **Laisser un message vocal pour cet utilisateur**   Activez cette option pour permettre à un appelant de laisser un message vocal à un utilisateur qui appartient au même plan de numérotation que le standard automatique de messagerie unifiée que vous configurez. Lorsqu'un appelant choisit cette option dans un menu de standard automatique, il est invité à laisser un message vocal à l'utilisateur qui a été sélectionné. Cliquez sur **Parcourir** pour accéder à l'utilisateur à extension messagerie unifiée.
        
          - **Annoncer l’adresse de l’entreprise**   Sélectionnez cette option pour permettre à un appelant de choisir une option de menu de standard automatique pour écouter l’adresse de l’entreprise qui a été configurée sur le standard automatique de messagerie unifiée. Pour que ce service fonctionne correctement, vous devez d’abord saisir l’adresse de l’entreprise dans la zone **Adresse de l’entreprise** de la page **Général** dudit standard.
        
          - **Annoncer les heures d’ouverture**   Sélectionnez cette option pour permettre à un appelant de choisir une option de menu de standard automatique pour écouter les heures d’ouverture de l’entreprise qui a été configurée sur le standard automatique de messagerie unifiée. Pour que ce service fonctionne correctement, vous devez d’abord configurer les heures d’ouverture dans la page **Heures d’ouverture** du standard automatique de messagerie unifiée.

5.  Cliquez sur **OK** pour créer le nouveau menu de navigation.

6.  Dans la page **Standard automatique de messagerie unifiée**, cliquez sur **Enregistrer** pour enregistrer vos modifications.

## Utiliser le Shell pour activer les heures de bureau standard automatiquement des mappages de touches sur une messagerie unifiée

Cet exemple configure un standard automatique de messagerie unifiée nommé `MyAutoAttendant` et Active les mappages de touches heures ouvrées afin que lorsque les appelants appuyez sur 1, sont transférés vers un autre standard automatique de messagerie unifiée nommé `SalesAutoAttendant`. Lorsqu'il clique sur 2, sont transférés vers le numéro de poste 12345 pour la prise en charge, et lorsqu'il clique sur 3, ils sont envoyés vers un autre standard automatique qui lit un fichier audio.

    Set-UMAutoAttendant -Identity MyAutoAttendant - BusinessHoursKeyMappingEnabled $true -BusinessHoursKeyMapping "1,Sales,,SalesAutoAttendant","2,Support,12345","3,Directions,,,directions.wav"

