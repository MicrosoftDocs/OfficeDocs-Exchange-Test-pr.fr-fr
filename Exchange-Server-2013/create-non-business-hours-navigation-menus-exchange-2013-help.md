---
title: 'Créer les heures creuses menus de navigation: Exchange 2013 Help'
TOCTitle: Créer les heures creuses menus de navigation
ms:assetid: bfe81ed6-9648-4882-8baf-ac93ea30a8ca
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb232175(v=EXCHG.150)
ms:contentKeyID: 50479121
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Créer les heures creuses menus de navigation

 

_**Sapplique à :**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :**2012-11-05_

Vous pouvez activer les mappages de touches en dehors des heures d’ouverture pour un standard automatique de messagerie unifiée. Une fois qu’un standard automatique de messagerie unifiée est créé, un message d’assistance vocale système par défaut est utilisé comme message d’accueil de menu principal en dehors des heures d’ouverture. Ce message est écouté par les appelants après le message d’accueil en dehors des heures d’ouverture. Le message d’assistance vocal par défaut du menu principal en dehors des heures d’ouverture est le suivant : « Bienvenue sur le standard automatique Microsoft Exchange en dehors des heures d’ouverture. » Puisque aucun mappage de touches n'est défini par défaut, aucune option de menu n'est disponible pour les appelants qui n'entendent que le message d'assistance vocal de menu principal par défaut en dehors des heures d'ouverture.

Lorsque vous configurez des mappages de touches, vous définissez les options et les opérations effectuées si un appelant prononce une phrase alors qu’il utilise un standard automatique à reconnaissance vocale, ou si l’appelant appuie sur la touche du clavier téléphonique alors qu’il utilise un standard automatique sans reconnaissance vocale.

Pour les autres tâches de gestion relatives aux standards automatiques de messagerie unifiée, consultez la rubrique [Procédures relatives au standard automatique de messagerie unifiée](um-auto-attendant-procedures-exchange-2013-help.md).

## Ce qu’il faut savoir avant de commencer ?

  - Durée d'exécution estimée : Moins d’une minute.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Standards automatiques de messagerie unifiée » dans la rubrique [Autorisations de messagerie unifiée](unified-messaging-permissions-exchange-2013-help.md).

  - Avant d’exécuter ces procédures, vérifiez qu’un plan de numérotation de messagerie unifiée a été créé. Pour obtenir la procédure détaillée, consultez la rubrique [Créer un plan de numérotation de messagerie unifiée](create-a-um-dial-plan-exchange-2013-help.md).

  - Avant d'exécuter ces procédures, vérifiez qu'un standard automatique de messagerie unifiée a été créé. Pour obtenir la procédure détaillée, consultez la rubrique [Créer un standard automatique de messagerie unifiée](create-a-um-auto-attendant-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

<table>
<thead>
<tr class="header">
<th><img src="images/Bb125224.tip(EXCHG.150).gif" title="Conseil" alt="Conseil" />Conseil :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..</td>
</tr>
</tbody>
</table>


## Que souhaitez-vous faire ?

## Utiliser le CAE pour activer les mappages de touches en dehors des heures d’ouverture sur un standard automatique de messagerie unifiée

1.  Dans le Centre d’administration Exchange, accédez à **Messagerie unifiée** \> **Plans de numérotation de messagerie unifiée**. Dans la liste affichée, sélectionnez le plan de numérotation de messagerie unifiée que vous souhaitez modifier puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

2.  Sur la page **Plan de numérotation de messagerie unifiée**, sous **Standards automatiques de messagerie unifiée**, sélectionnez le standard automatique de messagerie unifiée pour lequel créer un menu de navigation en dehors des heures d’ouverture. Dans la barre d’outils, cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

3.  Sur la page **Standard automatique de messagerie unifiée**, cliquez sur **Navigation par menu**. Sous **Navigation de menu en dehors des heures d’ouverture**, sélectionnez **Activer la navigation de menu en dehors des heures d’ouverture**, puis cliquez sur **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter").

4.  Dans la page **Nouvelle entrée de navigation par menu**, utilisez les options suivantes pour créer une nouvelle entrée de navigation par menu:
    
      - **Invite**   Cette zone permet de saisir le nom du nouveau menu de navigation. Le nom du menu de navigation est uniquement utilisé à des fins d’affichage. Ce champ est obligatoire.
        
        Comme vous pouvez spécifier plusieurs nouveaux menus de navigation, nous vous recommandons d’utiliser des noms significatifs pour vos mappages de touches. La longueur maximale de ce nom est de 64 caractères et il peut contenir des espaces. Toutefois, il ne peut pas contenir les caractères suivants : " / \\ \[ \] : ; | = , + \* ? \< \>.
    
      - **Lorsque cette touche est enfoncée**   Utilisez cette liste pour activer le mappage de touches. Le mappage de touches est le numéro de la touche qu’un appelant doit enfoncer pour que le standard automatique effectue une opération spécifique, telle que le transfert d’un appelant vers un autre standard automatique ou un opérateur. Par défaut, aucune entrée n’est définie.
        
        La liste déroulante permet de taper la touche numérique (de 1 à 9) que l’appelant doit enfoncer. Zéro (0) est réservé pour l’opérateur de standard automatique.
        
        L’option **Délai d’attente** de la liste déroulante permet d’activer les appelants à transférer vers un numéro de poste ou un autre standard automatique s’ils n’enfoncent pas une touche du clavier du téléphone. Par exemple, « Veuillez patienter, un agent va bientôt vous répondre. » Le paramètre par défaut est 5 secondes. Si vous activez cette option, un mappage de touches vide est créé.
    
      - **Lire le fichier audio suivant**   Utilisez cette option pour sélectionner un fichier audio précédemment enregistré pour les appelants. Cliquez sur **Modifier** puis sur **Parcourir** pour accéder au fichier audio. Si vous laissez le fichier audio sur l'option par défaut \<Aucun\>, le moteur de conversion de texte par synthèse vocale (TTS) de messagerie unifiée synthétisera un message d'accueil de menu principal hors des heures d'ouverture. Par contre, vous pouvez créer un fichier audio personnalisé qui peut être utilisé pour le message d'accueil du menu principal hors des heures d'ouverture pour un standard automatique à reconnaissance vocale, dont le message pourra être, par exemple, « Vous avez contacté Contoso hors des heures d'ouverture. Pour laisser un message vocal pour les ventes, dites 1. Pour laisser un message vocal pour l'assistance technique, dites 2. Pour laisser un message vocal pour l'administration, dites 3. Pour atteindre un opérateur après les heures d'ouverture, appuyez sur zéro. "
    
      - **Effectuer cette action supplémentaire**   Sélectionnez l’une des actions suivantes pour définir l’action que vous souhaitez que le standard automatique effectue pour le compte de l’appelant:
        
          - **Aucun**   Si vous ne voulez pas que le standard automatique transfert l'appel vers un poste ou un autre standard automatique, ni ne laisse de message pour un utilisateur, utilisez cette option.
        
          - **Transférer vers cette extension**   Sélectionnez cette option pour activer le transfert des appels vers une extension. Si vous activez cette action, utilisez la zone pour entrer le numéro de poste vers lequel l'appel sera transféré. Ce champ ne peut contenir que des caractères numériques. Il ne peut pas contenir les caractères suivants : " / \\ \[ \] : ; | = , + \* ? \< \>.
        
          - **Transférer vers ce standard automatique de messagerie unifiée**   Sélectionnez cette option pour transférer l'appel vers un standard automatique existant. Cliquez sur **Parcourir** pour localiser le standard automatique que vous voulez utiliser. Avant d’activer cette option, vous devez créer et configurer le standard automatique. Cette option est utilisée lorsque vous créez une structure parent/enfant de standards automatiques de messagerie unifiée.
        
          - **Laisser un message vocal pour cet utilisateur**   Sélectionnez cette option pour permettre à un appelant de laisser un message vocal à un utilisateur qui appartient au même plan de numérotation que le standard automatique de messagerie unifiée que vous configurez. Lorsqu’un appelant choisit cette option dans un menu de standard automatique, il est invité à laisser un message vocal à l’utilisateur qui a été sélectionné. Cliquez sur **Parcourir** pour accéder à l’utilisateur à extension messagerie unifiée.
        
          - **Annoncer l’adresse de l’entreprise**   Sélectionnez cette option pour permettre à un appelant de choisir une option de menu de standard automatique pour écouter l’adresse de l’entreprise qui a été configurée sur le standard automatique de messagerie unifiée. Pour que ce service fonctionne correctement, vous devez d’abord saisir l’adresse de l’entreprise dans la zone **Adresse de l’entreprise** de la page **Général** dudit standard.
        
          - **Annoncer les heures d’ouverture**   Sélectionnez cette option pour permettre à un appelant de choisir une option de menu de standard automatique pour écouter les heures d’ouverture de l’entreprise qui a été configurée sur le standard automatique de messagerie unifiée. Pour que ce service fonctionne correctement, vous devez d’abord configurer les heures d’ouverture dans la page **Heures d’ouverture** du standard automatique de messagerie unifiée.

5.  Cliquez sur **OK** pour créer le nouveau menu de navigation.

6.  Dans la page **Standard automatique de messagerie unifiée**, cliquez sur **Enregistrer** pour enregistrer vos modifications.

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour activer les mappages de touches en dehors des heures d'ouverture sur un standard automatique de messagerie unifiée

Cet exemple configure un standard automatique de messagerie unifiée nommé `MyAutoAttendant` et active les mappages de touches en dehors des heures d'ouverture de manière à ce que lorsque les appelants disent « After hours » ils soient dirigées vers le poste 12345 et s'ils disent « Directions », ils soient dirigés vers le poste 23456.

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -AfterHoursKeyMappingEnabled $true -AfterHoursKeyMapping "AfterhoursOperator,12345","Directions,23456"

