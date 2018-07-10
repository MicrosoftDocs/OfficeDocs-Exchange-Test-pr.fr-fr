---
title: 'Gérer un standard automatique de messagerie unifiée: Exchange 2013 Help'
TOCTitle: Gérer un standard automatique de messagerie unifiée
ms:assetid: 4809ff56-ae34-4ce6-8e39-9193311c3f83
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Aa997867(v=EXCHG.150)
ms:contentKeyID: 50478024
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.OrganizationConfiguration.UnifiedMessaging.AutoAttendantGeneralPropertyPage
ms.translationtype: MT
---

# Gérer un standard automatique de messagerie unifiée

 

_**Sapplique à :** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2013-04-30_

Après avoir créé un standard automatique de messagerie unifiée, vous pouvez afficher ou configurer plusieurs paramètres. Par exemple, vous pouvez ajouter, supprimer et modifier les numéros de poste associés au standard automatique. Vous pouvez également activer ou désactiver la reconnaissance vocale du standard automatique et modifier les messages d'accueil utilisés pendant et en dehors des heures d'ouverture.

Pour les autres tâches de gestion relatives aux standards automatiques de messagerie unifiée, consultez la rubrique [Procédures relatives au standard automatique de messagerie unifiée](um-auto-attendant-procedures-exchange-2013-help.md).

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : 5 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l'entrée « Standards automatiques de messagerie unifiée » dans la rubrique [Autorisations de messagerie unifiée](unified-messaging-permissions-exchange-2013-help.md).

  - Avant d'exécuter ces procédures, vérifiez qu'un plan de numérotation de messagerie unifiée a été créé. Pour obtenir la procédure détaillée, consultez la rubrique [Créer un plan de numérotation de messagerie unifiée](create-a-um-dial-plan-exchange-2013-help.md).

  - Avant d'exécuter ces procédures, vérifiez qu'un standard automatique de messagerie unifiée a été créé. Pour obtenir la procédure détaillée, consultez la rubrique [Créer un standard automatique de messagerie unifiée](create-a-um-auto-attendant-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]  
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..


## Que souhaitez-vous faire ?

## Utiliser le CAE pour afficher ou configurer les paramètres du standard automatique de messagerie unifiée

1.  Dans le Centre d'administration Exchange, accédez à **Messagerie unifiée** \> **Plans de numérotation de messagerie unifiée**. Dans l'affichage Liste, sélectionnez le plan de numérotation de messagerie unifiée à modifier puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

2.  Dans la page **Plan de numérotation de messagerie unifiée**, sous **Standards automatiques de messagerie unifiée**, sélectionnez le standard automatique de messagerie unifiée à afficher ou configurer, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier") dans la barre d'outils.

3.  Dans la page **Standard automatique de messagerie unifiée**, cliquez sur **Général** pour consulter des informations en affichage seul sur le standard automatique de messagerie unifiée et réaliser des tâches de gestion sur celui-ci, comme suit :
    
      - **Plan de numérotation de messagerie unifiée**   Cette zone montre le plan de numérotation de messagerie unifiée associé au standard automatique. Après la création d'un standard automatique, le plan de numérotation associé au standard automatique ne peut pas être modifié. Si vous devez associer un standard automatique à un plan de numérotation différent, vous devez supprimer le plan de numérotation, puis associer le standard automatique au plan de numérotation qui convient après sa recréation.
    
      - **Nom**   Cette zone affiche le nom affecté au standard automatique lors de sa création. C'est le nom qui apparaîtra dans le CAE.
    
      - **État**   Cette case indique si le standard automatique de messagerie unifiée est activé ou désactivé. Pour activer ou désactiver le standard automatique, fermez la page **Standard automatique de messagerie unifiée** et utilisez la barre d'outils sous **Standards automatiques de messagerie unifiée** dans la page **Plan de numérotation de messagerie unifiée**.
    
      - **Numéros d'accès**   Cette zone permet d'entrer un numéro de poste ou un numéro d'accès qui conduit les appelants sur le standard automatique. Par défaut, aucun numéro de poste ou d'accès n'est configuré lors de la création d'un standard automatique.
        
        Le nombre de chiffres des numéros d'accès ou des numéros de postes indiqués doit respecter le nombre de chiffres configuré pour un numéro de poste configurer sur le plan de numérotation de messagerie unifiée associé au standard automatique de messagerie unifiée. Dans cette case, vous pouvez également ajouter une adresse SIP (Session Initiation Protocol). Une adresse SIP est utilisée par certains PBX IP et PBX compatibles SIP, ainsi que par Microsoft Office Communications Server 2007 R2 ou Microsoft Lync Server.
        
        Vous pouvez créer un standard automatique sans numéro de poste ou numéro d'accès répertorié. Pour ajouter un numéro de poste, tapez le numéro dans cette zone, puis cliquez sur **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter"). Vous pouvez associer plus d'un numéro à un standard automatique. Vous pouvez également modifier ou supprimer un numéro d'accès existant. Pour le modifier, cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier"). Pour le supprimer de la liste, sélectionnez-le et cliquez sur **Supprimer**![Icône Suppression](images/Dd362328.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "Icône Suppression").
    
      - **Définir le standard automatique pour répondre aux commandes vocales**   Activez cette case à cocher pour permettre aux appelants de répondre oralement aux invites du standard automatique pour naviguer dans le système de menus. Par défaut, le standard automatique n'est pas à reconnaissance vocale au moment de sa création.
        
        Si vous décidez de créer un standard automatique de messagerie unifiée mais de ne pas en activer la reconnaissance vocale, vous pouvez utiliser le CAE ou l'environnement de ligne de commande Exchange Management Shell pour activer la reconnaissance vocale par la suite.
    
      - **Utilisez ce standard automatique de commandes vocales ne fonctionnent pas correctement**    Cliquez sur **Parcourir** pour sélectionner le standard automatique que vous souhaitez utiliser dans le cas où les commandes vocales ne fonctionnent pas. Il est également appelé un DTMF standard automatique de secours. Un standard de standard automatique de secours DTMF peut être utilisé uniquement si l'option **Set du standard automatique pour répondre aux commandes vocales ne fonctionnent pas correctement** est sélectionnée. Vous devez d'abord créer un standard de standard automatique de secours DTMF et puis cliquez sur **Parcourir** pour localiser le standard automatique de DTMF approprié.
        
        Un standard automatique de secours DTMF est utilisé lorsque le standard automatique de messagerie unifiée à reconnaissance vocale activée ne comprend pas ou ne reconnaît pas les entrées vocales de l'appelant. Si le standard automatique DTMF est utilisé, l'appelant doit utiliser des entrées DTMF pour naviguer dans le système de menus, épeler un nom d'utilisateur ou utiliser une invite de menu personnalisée. Un appelant ne peut pas utiliser de commandes vocales pour naviguer dans ce standard automatique.
        
        Si vous ne configurez pas de standard automatique de secours DTMF, nous vous recommandons que vous configuriez un numéro d'extension opérateur sur le standard automatique. Si vous ne configurez pas de numéro d'extension opérateur, lorsque les appelants utilisent un standard automatique à reconnaissance vocale activée, et que le système ne reconnaît pas leurs entrées vocales, ils ne peuvent pas naviguer dans le système ou être transférés vers un opérateur pour obtenir de l'aide.
        
        Bien que cela ne soit pas obligatoire, nous vous recommandons de configurer un standard automatique de secours DTMF pour disposer de la même configuration que le standard automatique à reconnaissance vocale activée. La reconnaissance vocale du standard automatique de secours DTMF ne doit pas être activée.
    
      - **Langue de l'interface vocale automatique**    Utilisez cette liste pour sélectionner la langue que les appelants entendront lorsqu'ils atteignent le standard automatique. La langue par défaut est déterminée lorsque vous installez Microsoft Exchange. Local et hybride déploiements, par défaut, anglais (États-Unis) est utilisé, car le standard automatique utilise le paramètre de langue sur le plan de numérotation de messagerie unifiée. Pour que les autres options de langue disponibles, vous devez installer les modules linguistiques de messagerie unifiée pour les langues que vous souhaitez inclure. Pour plus d'informations sur la façon d'installer un module linguistique de messagerie unifiée, consultez la rubrique [Installer un module linguistique de messagerie unifiée](install-a-um-language-pack-exchange-2013-help.md). Pour la messagerie unifiée dans Office 365, il n'est pas nécessaire d'installer les modules linguistiques de messagerie unifiée supplémentaires.
        
        Même si vous pouvez sélectionner une autre langue que celle définie dans le plan de numérotation de messagerie unifiée associé au standard automatique, nous vous recommandons d'utiliser les mêmes paramètres de langue pour le plan de numérotation et le standard automatique. Si les paramètres de langue diffèrent, lorsque des appelants composent un numéro de poste défini dans le plan de numérotation, ils voient des invites dans une langue différente de celle des invites affichées quand ils composent un numéro de poste associé à un standard automatique.
    
      - **Nom de l'entreprise**   Cette case sert à entrer le nom de l'entreprise. Aucun nom d'entreprise n'est entré par défaut. Si vous entrez un nom d'entreprise dans cette case, une invite portant le nom de l'entreprise sera lue aux appelants à la place du message d'accueil par défaut.
    
      - **Emplacement de l'entreprise**   Cette case sert à entrer l'emplacement de l'entreprise. Aucune adresse d'entreprise n'est entrée par défaut. En entrant l'emplacement de l'entreprise dans cette case, l'emplacement de l'entreprise sera lu aux appelants.

4.  Utiliser des **messages d'accueil** sur le standard automatique pour gérer des messages d'accueil enregistrés. Vous pouvez sélectionner des messages d'accueil par défaut ou des messages d'accueil personnalisés enregistrés au préalable pendant et en dehors des heures d'ouverture. Vous pouvez configurer ce qui suit :
    
      - **Message d'accueil des heures d'ouverture**    Il s'agit du message d'accueil initial qui est émis lorsqu'un appelant appelle le standard automatique pendant les heures de bureau de votre organisation. Par défaut, les heures de bureau sont de 12:00 à 12:00 et aucune dehors des heures sont définies. Si vous ne spécifiez pas un fichier personnalisé salutation, une invite système indiquant, « Bienvenue pour le standard automatique de Exchange » est diffusé aux appelants. Les business et les heures creuses sont configurés dans le **heures d'ouverture** du standard automatique.
        
        Vous voudrez probablement personnaliser ce message d'accueil pour représenter votre société : « Merci d'avoir appelé Woodgrove Bank. » Vous pouvez configurer un message d'accueil personnalisé pendant les heures d'ouverture. Pour ce faire, cliquez sur **Modifier** afin de sélectionner un fichier de message d'accueil personnalisé précédemment enregistré. Le message d'accueil personnalisé doit avoir déjà été enregistré sous un fichier .wav ou .wma.
    
      - **Message d'accueil en dehors des heures d'ouverture**   Le message d'accueil initial est lu quand un appelant appelle le standard automatique en dehors des heures d'ouverture de votre organisation. Par défaut, aucune heure de fermeture n'est configurée. Par conséquent, il n'existe aucun message d'accueil en dehors des heures d'ouverture par défaut. L'option **Heures d'ouverture** du standard automatique permet de configurer les heures d'ouverture et de fermeture.
        
        Vous voudrez probablement personnaliser ce message d'accueil pour représenter votre société : « Merci d'avoir appelé Woodgrove Bank, mais nous sommes actuellement fermés. » ou « Vous appelez Contoso, Ltd. en dehors des heures d'ouverture. Nos heures d'ouverture sont de 8h00 à 17h00 du lundi au vendredi. » Vous pouvez configurer un message d'accueil personnalisé pendant les heures de fermeture. Pour ce faire, cliquez sur **Modifier** afin de sélectionner un fichier de message d'accueil personnalisé précédemment enregistré. Le message d'accueil personnalisé doit avoir déjà été enregistré sous un fichier .wav ou .wma.
    
      - **Message d'information automatique**   Lorsqu'il est activé, cet enregistrement facultatif est lu immédiatement après le message d'accueil pendant et en dehors des heures d'ouverture. Un message d'information automatique peut rappeler les heures d'ouverture de l'organisation, par exemple : « Nos heures d'ouverture sont de 8h30 à 17h30 du lundi au vendredi, et de 8h30 à 13h00 le samedi. » Un message d'information automatique peut également fournir les informations requises pour se conformer à la stratégie d'entreprise, par exemple : « Les appels peuvent être analysés à des fins de formation. » S'il est important que les appelants entendent le message d'information automatique dans son intégralité, celle-ci peut être configurée sur Interruption impossible, obligeant l'appelant à écouter l'annonce entière.
        
        Par défaut, aucun message d'information automatique n'est configuré dans les standards automatiques ou les plans de numérotation de messagerie unifiée. Si vous activez un message d'information automatique et utilisez un fichier audio personnalisé spécifique à votre organisation, l'option **Autoriser l'interruption de l'annonce** devient disponible. Les enregistrements doivent déjà être au format .wav ou wma. Cliquez sur **Modifier** pour localiser un fichier de message d'information automatique personnalisé précédemment enregistré.
        
        **Autoriser l'interruption du message**   Activez cette case à cocher pour permettre à l'appelant d'interrompre le message d'information automatique. Cette option doit être activée si vos messages d'information automatiques sont longs. Les appelants peuvent être incommodés si le message d'information automatique est trop long et qu'ils ne peuvent pas l'interrompre pour accéder aux options proposées par le standard automatique.

5.  Utilisez **Heures d'ouverture** pour définir les heures d'ouverture de l'organisation. Pendant les heures d'ouverture, les appelants entendent le message d'accueil par défaut ou un message d'accueil personnalisé et l'invite de menu principal correspondante si les mappages de touches appropriés sont configurés dans **Navigation de menu**. Vous pouvez configurer ce qui suit :
    
      - **Fuseau horaire**   Cette liste permet de sélectionner votre fuseau horaire. Vérifiez si le plan de numérotation associé au standard automatique couvre plus d'un fuseau horaire lorsque vous définissez votre planification.
        
        Pour les déploiements locaux et hybrides, le fuseau horaire est configuré par défaut par l'utilisation de l'heure système du serveur local lors de l'installation du serveur de boîtes aux lettres qui exécute le service de messagerie unifiée de Microsoft Exchange.
    
      - **Heures d'ouverture**    Cliquez sur **configurer les heures de bureau**, puis, dans la page **configurer les heures de bureau**, utilisez la grille pour configurer les heures de bureau de votre organisation.
    
      - **Planning des congés**   Permet de définir les jours, de 00h00 à 23h59, pendant lesquels votre organisation est fermée pour cause de congés. Les appelants qui accèdent au standard automatique pendant les heures spécifiées dans la page **Nouveau congé** entendent le fichier audio d'accueil pour les congés que vous définissez. Lors de la configuration du planning des congés, vous devez définir le nom du congé, le fichier audio d'accueil pour les congés ainsi que la **Date de début** et la **Date de fin**. Les messages d'accueil doivent déjà être enregistrés au format .wav ou wma.

6.  Utilisez la **Navigation de menu** pour spécifier les options de menu proposées aux appelants pendant les heures d'ouverture et de fermeture. Si vous souhaitez activer la navigation de menu, vous devez le faire séparément pour les heures d'ouverture et de fermeture. Par exemple, si vous souhaitez activer la navigation pour les heures d'ouverture, vous devez ajouter un enregistrement audio d'invite de menu. Cochez la case **Activer la navigation de menu pendant les heures d'ouverture**, cliquez sur **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter"), puis définissez les options dans la page **Nouvelle entrée de navigation de menu**.
    
      - **Navigation de menu pendant les heures d'ouverture**   Il s'agit de la liste des options que les appelants entendent pendant les heures d'ouverture définies dans la page **Heures d'ouverture**. Par exemple : « Pour le support technique, appuyez sur ou dites 1. Pour les bureaux d'entreprise et l'administration, appuyez sur ou dites 2. Pour les ventes, appuyez sur ou dites 3. »
        
        Pour activer la navigation de menu pendant les heures d'ouverture, procédez comme suit :
        
        1.  **Invite de menu**   Cette option permet de spécifier un fichier audio d'invite de menu personnalisé. Pour utiliser un message d'accueil de menu pour les heures d'ouverture personnalisé ou préalablement enregistré, cliquez sur **Modifier**, puis sur **Parcourir** pour indiquer l'emplacement du fichier audio du message d'accueil.
        
        2.  **Activer la navigation de menu pendant les heures d'ouverture**   Cochez cette case pour activer des options pour la navigation de menu qui sera utilisée pendant les heures d'ouverture. Lorsque vous activez la navigation de menu pour les heures d'ouverture, vous pouvez ajouter de nouvelles entrées de navigation de menu pour les heures d'ouverture.
        
        3.  Cliquez sur **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter") pour créer une nouvelle entrée de navigation par menu. Dans la page **Nouvelle entrée de navigation de menu**, utilisez les options suivantes pour créer une nouvelle entrée de navigation de menu :
            
              - **Invite**   Cette zone permet de saisir le nom du nouveau menu de navigation. Le nom du menu de navigation est uniquement utilisé à des fins d'affichage. Ce champ est obligatoire.
                
                Comme vous pouvez spécifier plusieurs nouveaux menus de navigation, nous vous recommandons d'utiliser des noms significatifs pour vos mappages de touches. Ce nom doit contenir au maximum 64 caractères et peut comporter des espaces. Toutefois, il ne peut contenir aucun des caractères suivants : " / \\ \[ \] : ; | = , + \* ? \< \>.
            
              - **Lorsque cette touche est enfoncée**   Utilisez cette liste pour activer le mappage de touches. Le mappage de touches est le numéro de la touche qu'un appelant doit enfoncer pour que le standard automatique effectue une opération spécifique, telle que le transfert d'un appelant vers un autre standard automatique ou un opérateur. Par défaut, aucune entrée n'est définie.
                
                La liste déroulante permet de taper la touche numérique (de 1 à 9) que l'appelant doit enfoncer. Zéro (0) est réservé pour l'opérateur de standard automatique.
                
                L'option **Délai d'attente** de la liste déroulante permet d'activer les appelants à transférer vers un numéro de poste ou un autre standard automatique s'ils n'enfoncent pas une touche du clavier du téléphone. Par exemple, «Veuillez patienter, un agent va bientôt vous répondre.» Le paramètre par défaut est 5 secondes. Si vous activez cette option, un mappage de touches vide est créé.
            
              - **Lire le fichier audio suivant**   Utilisez cette option pour sélectionner un fichier audio précédemment enregistré pour les appelants. Cliquez sur **Modifier** puis sur **Parcourir** pour accéder au fichier audio. Si vous laissez le fichier audio sur l'option par défaut \<Aucun\>, le moteur de conversion de texte par synthèse vocale (TTS) de messagerie unifiée synthétisera un message d'accueil de menu principal dans les heures d'ouverture. D'autre part, vous pouvez créer un fichier audio personnalisé pouvant être utilisé pour le message d'accueil du menu principal dans les heures d'ouverture pour un standard automatique à reconnaissance vocale. Le message peut être le suivant : « Pour laisser un message vocale pour les ventes, dites 1. Pour laisser un message vocal pour l'assistance technique, dites 2. Pour laisser un message vocal pour l'administration, dites 3. »
            
              - **Effectuer cette action supplémentaire**   Sélectionnez l'une des actions suivantes pour définir l'action que vous souhaitez que le standard automatique effectue pour le compte de l'appelant :
                
                  - **Aucun**   Si vous ne voulez pas que le standard automatique transfert l'appel vers un poste ou un autre standard automatique, ni ne laisse de message pour un utilisateur, utilisez cette option.
                
                  - **Transférer vers cette extension**   Activez cette option pour activer le transfert des appels vers une extension. Si vous activez cette option, utilisez cette zone pour saisir le numéro de l'extension vers lequel l'appel sera transféré. Ce champ ne peut contenir que des caractères numériques. Il ne peut contenir aucun des caractères suivants : " / \\ \[ \] : ; | = , + \* ? \< \>.
                
                  - **Transférer vers ce standard automatique de messagerie unifiée**   Activez cette option pour transférer l'appel vers un standard automatique. Cliquez sur **Parcourir** pour localiser le standard automatique que vous voulez utiliser. Avant d'activer cette option, vous devez créer et configurer le standard automatique. Cette option est utilisée lorsque vous créez une structure parent/enfant de standards automatiques de messagerie unifiée.
                
                  - **Laisser un message vocal pour cet utilisateur**   Activez cette option pour permettre à un appelant de laisser un message vocal à un utilisateur qui appartient au même plan de numérotation que le standard automatique de messagerie unifiée que vous configurez. Lorsqu'un appelant choisit cette option dans un menu de standard automatique, il est invité à laisser un message vocal à l'utilisateur qui a été sélectionné. Cliquez sur **Parcourir** pour accéder à l'utilisateur à extension messagerie unifiée.
                
                  - **Annoncer l'adresse de l'entreprise**   Activez cette option pour permettre à un appelant de choisir une option de menu de standard automatique pour écouter l'adresse de l'entreprise qui a été configurée sur le standard automatique de messagerie unifiée. Pour que ce service fonctionne correctement, vous devez d'abord saisir l'adresse de l'entreprise dans la zone **Adresse de l'entreprise** de la page **Général** dudit standard.
                
                  - **Annoncer les heures d'ouverture**   Activez cette option pour permettre à un appelant de choisir une option de menu de standard automatique pour écouter les heures d'ouverture de l'entreprise qui a été configurée sur le standard automatique de messagerie unifiée. Pour que ce service fonctionne correctement, vous devez d'abord configurer les heures d'ouverture dans la page **Heures d'ouverture** du standard automatique de messagerie unifiée.
    
      - **Navigation de menu en dehors des heures d'ouverture**   Il s'agit de la liste des options que les appelants entendent en dehors des heures d'ouverture définies dans la page **Heures d'ouverture**. Par exemple : « Votre appel est important. Toutefois, vous joignez Woodgrove Bank après les heures d'ouverture normales. Si vous voulez laisser un message, dites ou appuyez sur 1 et nous vous rappellerons dès que possible. »
        
        Pour activer la navigation de menu en dehors des heures d'ouverture, procédez comme suit :
        
        1.  **Invite de menu** Cette option permet de spécifier un fichier audio d'invite de menu personnalisé. Pour utiliser une invite de menu personnalisée ou préalablement enregistrée en dehors des heures d'ouverture, cliquez sur **Parcourir**.
        
        2.  **Activer la navigation de menu en dehors des heures d'ouverture**   Cochez cette case pour activer des options pour la navigation de menu qui sera utilisée en dehors des heures d'ouverture. Quand vous activez la navigation de menu en dehors des heures d'ouverture, vous pouvez ajouter de nouvelles entrées de navigation de menu en dehors des heures d'ouverture.
        
        3.  Cliquez sur **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter") pour créer une nouvelle entrée de navigation par menu. Dans la page **Nouvelle entrée de navigation de menu**, utilisez les options suivantes pour créer une nouvelle entrée de navigation de menu :
            
              - **Invite**   Cette zone permet de saisir le nom du nouveau menu de navigation. Le nom du menu de navigation est uniquement utilisé à des fins d'affichage. Ce champ est obligatoire.
                
                Comme vous pouvez spécifier plusieurs nouveaux menus de navigation, nous vous recommandons d'utiliser des noms significatifs pour vos mappages de touches. Ce nom doit contenir au maximum 64 caractères et peut comporter des espaces. Toutefois, il ne peut contenir aucun des caractères suivants : " / \\ \[ \] : ; | = , + \* ? \< \>.
            
              - **Lorsque cette touche est enfoncée**   Utilisez cette liste pour activer le mappage de touches. Le mappage de touches est le numéro de la touche qu'un appelant doit enfoncer pour que le standard automatique effectue une opération spécifique, telle que le transfert d'un appelant vers un autre standard automatique ou un opérateur. Par défaut, aucune entrée n'est définie.
                
                La liste déroulante permet de taper la touche numérique (de 1 à 9) que l'appelant doit enfoncer. Zéro (0) est réservé pour l'opérateur de standard automatique.
                
                L'option **Délai d'attente** de la liste déroulante permet d'activer les appelants à transférer vers un numéro de poste ou un autre standard automatique s'ils n'enfoncent pas une touche du clavier du téléphone. Par exemple, «Veuillez patienter, un agent va bientôt vous répondre.» Le paramètre par défaut est 5 secondes. Si vous activez cette option, un mappage de touches vide est créé.
            
              - **Lire le fichier audio suivant**   Utilisez cette option pour sélectionner un fichier audio précédemment enregistré pour les appelants. Cliquez sur **Modifier** puis sur **Parcourir** pour accéder au fichier audio. Si vous laissez le fichier audio sur l'option par défaut \<Aucun\>, le moteur de conversion de texte par synthèse vocale (TTS) de messagerie unifiée synthétisera un message d'accueil de menu principal hors des heures d'ouverture. Par contre, vous pouvez créer un fichier audio personnalisé qui peut être utilisé pour le message d'accueil du menu principal hors des heures d'ouverture pour un standard automatique à reconnaissance vocale, dont le message pourra être, par exemple, « Vous avez contacté Contoso hors des heures d'ouverture. Pour laisser un message vocal pour les ventes, dites 1. Pour laisser un message vocal pour l'assistance technique, dites 2. Pour laisser un message vocal pour l'administration, dites 3. Pour atteindre un opérateur après les heures d'ouverture, appuyez sur zéro. "
            
              - **Effectuer cette action supplémentaire**   Sélectionnez l'une des actions suivantes pour définir l'action que vous souhaitez que le standard automatique effectue pour le compte de l'appelant :
                
                  - **Aucun**   Si vous ne voulez pas que le standard automatique transfert l'appel vers un poste ou un autre standard automatique, ni ne laisse de message pour un utilisateur, utilisez cette option.
                
                  - **Transférer vers cette extension**   Activez cette option pour activer le transfert des appels vers une extension. Si vous activez cette action, utilisez la zone pour entrer le numéro de poste vers lequel l'appel sera transféré. Ce champ ne peut contenir que des caractères numériques. Il ne peut contenir aucun des caractères suivants : " / \\ \[ \] : ; | = , + \* ? \< \>.
                
                  - **Transférer vers ce standard automatique de messagerie unifiée**   Activez cette option pour transférer l'appel vers un standard automatique existant. Cliquez sur **Parcourir** pour localiser le standard automatique que vous voulez utiliser. Avant d'activer cette option, vous devez créer et configurer le standard automatique. Cette option est utilisée lorsque vous créez une structure parent/enfant de standards automatiques de messagerie unifiée.
                
                  - **Laisser un message vocal pour cet utilisateur**   Activez cette option pour permettre à un appelant de laisser un message vocal à un utilisateur qui appartient au même plan de numérotation que le standard automatique de messagerie unifiée que vous configurez. Lorsqu'un appelant choisit cette option dans un menu de standard automatique, il est invité à laisser un message vocal à l'utilisateur qui a été sélectionné. Cliquez sur **Parcourir** pour accéder à l'utilisateur à extension messagerie unifiée.
                
                  - **Annoncer l'adresse de l'entreprise**   Activez cette option pour permettre à un appelant de choisir une option de menu de standard automatique pour écouter l'adresse de l'entreprise qui a été configurée sur le standard automatique de messagerie unifiée. Pour que ce service fonctionne correctement, vous devez d'abord saisir l'adresse de l'entreprise dans la zone **Adresse de l'entreprise** de la page **Général** dudit standard.
                
                  - **Annoncer les heures d'ouverture**   Activez cette option pour permettre à un appelant de choisir une option de menu de standard automatique pour écouter les heures d'ouverture de l'entreprise qui a été configurée sur le standard automatique de messagerie unifiée. Pour que ce service fonctionne correctement, vous devez d'abord configurer les heures d'ouverture dans la page **Heures d'ouverture** du standard automatique de messagerie unifiée.

7.  Utilisez **Accès au carnet d'adresses et à l'opérateur** pour définir les fonctionnalités proposées aux appelants qui appellent le standard automatique de messagerie unifiée. Vous pouvez configurer les fonctionnalités du standard automatique, telles que la langue utilisée lorsque des appelants contactent le standard automatique et la possibilité de transfert des appelants vers le numéro de poste d'un opérateur. Vous pouvez configurer ce qui suit :
    
      - **Options de contact des utilisateurs**   Utilisez ces options pour déterminer comment les appelants peuvent contacter des utilisateurs avec messagerie vocale quand ils appellent un standard automatique de messagerie unifiée
        
          - **Autoriser les appelants à composer les numéros d'utilisateurs**   Activez cette case à cocher pour permettre aux appelants de transférer les appels à des utilisateurs. Par défaut, cette option est activée et permet aux utilisateurs associés au plan de numérotation de transférer les appels aux utilisateurs dans le même plan de numérotation de messagerie unifiée. Une fois cette case cochée, vous pouvez définir le groupe d'utilisateurs auxquels les appelants peuvent transférer des appels en sélectionnant l'option appropriée sous la section **Options de recherche dans le carnet d'adresses** de cette page.
            
            Si vous désactivez cette option et l'option **Autoriser les appelants à laisser des messages vocaux aux utilisateurs**, les options sous **Options de recherche dans le carnet d'adresses** sont également désactivées.
        
          - **Autoriser les appelants à laisser des messages vocaux aux utilisateurs**   Cochez cette case pour permettre aux appelants d'envoyer des messages vocaux à des utilisateurs. Par défaut, cette option est activée et permet aux utilisateurs associés au plan de numérotation d'envoyer des messages vocaux aux utilisateurs dans le même plan de numérotation de messagerie unifiée. Une fois cette case cochée, vous pouvez définir le groupe d'utilisateurs auxquels les appelants peuvent envoyer des messages vocaux en sélectionnant l'option appropriée sous la section **Options de recherche dans le carnet d'adresses** de cette page.
            
            Si vous désactivez cette option et l'option **Autoriser les appelants à composer les numéros d'utilisateurs**, les options sous **Options de recherche dans le carnet d'adresses** sont également désactivées.
            
            Si vous désactivez cette option, le standard automatique ne permettra pas aux appelants d'envoyer un message vocal via une invite du système.
    
      - **Options de recherche dans le carnet d'adresses**   Utilisez ces options pour déterminer un groupe d'utilisateurs. Par défaut, l'option **Autoriser les appelants à rechercher des utilisateurs par nom ou alias** est sélectionnée, de même que l'option **Dans ce plan de numérotation uniquement**. Toutefois, vous pouvez modifier le regroupement d'utilisateurs afin de permettre aux appelants de transférer des appels ou d'envoyer des messages vocaux à des utilisateurs présents dans la liste d'adresses globale (GAL) d'une organisation. Vous pouvez choisir l'une des options suivantes :
        
          - **Autoriser les appelants à rechercher des utilisateurs par nom ou alias**   Par défaut, cette option est sélectionnée. Elle permet aux appelants qui appellent ce standard automatique de rechercher des utilisateurs par nom ou par alias dans l'annuaire. Un alias est affecté à chaque utilisateur pour lequel une boîte aux lettres est créée. L'alias est la première partie d'une adresse SMTP, par exemple, jeanmartin@contoso.com. L'adresse SMTP est jeanmartin@contoso.com, tandis que l'alias est jeanmartin. La sélection de cette option affecte uniquement les appelants qui utilisent ce standard automatique et non pas ceux qui utilisent Outlook Voice Access.
            
              - **Dans ce plan de numérotation seulement**   Activez cette option pour permettre aux appelants qui se connectent au standard automatique de messagerie unifiée de localiser et de contacter des utilisateurs dans le même plan de numérotation associé à ce standard automatique de messagerie unifiée. Par défaut, cette option est activée sur le plan de numérotation et sur le standard automatique. Cela signifie que les utilisateurs d'Outlook Voice Access et les appelants qui se connectent au standard automatique sont en mesure de rechercher des utilisateurs dans le même plan de numérotation.
            
              - **Dans l'ensemble de l'organisation**    Sélectionnez cette option pour autoriser les appelants qui appellent à ce standard automatique de messagerie unifiée pour rechercher et contacter une personne répertoriée dans la liste d'adresses globale pour l'organisation. Cela inclut non seulement les utilisateurs à extension messagerie unifiée, mais tous les utilisateurs qui sont à extension boîte aux lettres. Cette option permet aux appelants de contacts des utilisateurs dans plusieurs plans de numérotation. Il n'est pas activé par défaut. Ce paramètre est également disponible sur un plan de numérotation pour les utilisateurs Outlook Voice Access.
        
          - **Informations à inclure pour des noms similaires**   Utilisez cette liste déroulante pour sélectionner l'option utilisée par le standard automatique de messagerie unifiée lorsque des utilisateurs portent des noms identiques ou similaires. Ce paramètre est utilisé lorsque deux ou plusieurs utilisateurs dans l'annuaire portent le même nom. Il est également appelé champ Levée d'ambiguïté ou Nom correspondant. Vous pouvez configurer ce paramètre ou vous pouvez conserver le paramètre par défaut sur le standard automatique. Par défaut, le standard automatique hérite de ce paramètre à partir de celui défini sur le plan de numérotation associé au standard automatique. Voici un exemple de standard automatique à reconnaissance vocale :
            
            1.  Système : « Bienvenue chez Contoso. Si vous connaissez le nom de la personne que vous appelez, veuillez indiquer son nom à tout moment. »
            
            2.  L'appelant dit « Tony Smith ».
            
            3.  Plusieurs personnes portent ce nom. Veuillez sélectionner l'une de ces options : Pour Tony Smith du service de recherche, appuyez sur 1. Pour Tony Smith de la direction, appuyez sur 2. Pour Tony Smith du support technique, appuyez sur 3. »
            
            4.  L'appelant appuie sur la touche correspondante sur le clavier numérique et l'appel est transféré à l'utilisateur.
                
                > [!NOTE]  
				> Sur un standard automatique sans reconnaissance, le système indiquera l'appelant d'utiliser le clavier pour saisir le nom d'utilisateur (nom tout d'abord) puis effectuez une recherche de l'utilisateur. S'il existe plusieurs personnes dans le répertoire portant le même nom, l'appelant est invité à appuyer sur la clé appropriée à transférer à l'utilisateur. Vous pouvez éventuellement créer un standard automatique de secours DTMF qui utilise uniquement le clavier pour entrer un nom ou un alias.
                            
            Pour utiliser ces paramètres, vous devez ajouter les informations appropriées à l'utilisateur. Par exemple, si vous souhaitez que le standard automatique à utiliser un titre pour deux utilisateurs avec le même nom, vous devez ajouter ces informations pour le compte d'utilisateur. Sélectionnez une des méthodes suivantes qui fournissent des informations supplémentaires pour vous aider à la sélection de l'appelant l'utilisateur correct dans l'organisation :
            
              - **Hériter du plan de commutation des appels**   Activez cette option afin que le standard automatique utilise le paramètre par défaut du plan de numérotation associé au standard automatique.
            
              - **Titre**   Activez cette option afin que le standard automatique inclue le titre de chaque utilisateur lors du relevé des correspondances.
            
              - **Service**   Activez cette option afin que le standard automatique inclue le service de chaque utilisateur lors du relevé des correspondances.
            
              - **Emplacement**   Activez cette option afin que le standard automatique inclue l'emplacement de chaque utilisateur lors du relevé des correspondances.
            
              - **Aucune**   Activez cette option afin qu'aucune information supplémentaire ne soit transmise lors du relevé des correspondances.
            
              - **Demander un alias**   Activez cette option afin que le standard automatique invite l'appelant à indiquer l'alias de l'utilisateur.

8.  Sous **Accès à l'opérateur**, vous pouvez spécifier les paramètres d'opérateur de standard automatique, notamment :
    
      - **Extension opérateur**   Cette case permet de taper le numéro de poste utilisé pour appeler un opérateur. Ce numéro de poste peut connecter l'appelant à un opérateur humain ou une boîte aux lettres à extension messagerie unifiée, ou peut être configuré pour appeler un numéro de téléphone externe. Par défaut, aucune extension opérateur n'est incluse dans cette case.
    
      - **Autoriser le transfert à l'opérateur pendant les heures d'ouverture**   Cochez cette case pour autoriser le transfert des appelants vers un opérateur humain pendant les heures d'ouverture à l'aide du numéro de poste configuré dans la zone **Poste opérateur**. Par défaut, cette option est désactivée.
        
        Il est utile d'activer cette option de façon à ce que, lorsqu'un appelant ne parvient pas à localiser une personne à l'aide des invites du menu ou de la recherche dans l'annuaire pendant les heures d'ouverture, il puisse laisser un message vocal ou être mis en relation avec un opérateur humain. Après avoir activé cette option, vous pouvez configurer le numéro de poste de l'opérateur sur une boîte aux lettres à extension messagerie unifiée qui est analysée. L'appelant peut laisser un message vocal ou obtenir de l'aide d'un opérateur correspondant au numéro de poste.
    
      - **Autoriser le transfert à l'opérateur en dehors des heures d'ouverture**   Cochez cette case pour autoriser le transfert des appelants vers un opérateur humain après les heures d'ouverture à l'aide du numéro de poste configuré dans la zone **Poste opérateur**. Par défaut, cette option est désactivée.
        
        Il est utile d'activer cette option de façon à ce que, lorsqu'un appelant ne parvient pas à localiser une personne à l'aide des invites du menu ou de la recherche dans l'annuaire après les heures d'ouverture, il puisse laisser un message vocal ou être mis en relation avec un opérateur humain. Après avoir activé cette option, vous pouvez configurer le numéro de poste de l'opérateur configuré sur une boîte aux lettres à extension messagerie unifiée qui est analysée. L'appelant peut laisser un message vocal ou obtenir de l'aide d'un opérateur correspondant au numéro de poste.

9.  Utilisez l'option **Autorisation de numérotation** pour configurer les règles de numérotation pour les appelants qui appellent un standard automatique de messagerie unifiée. Ces paramètres permettent de contrôler les numéros de poste accessibles à partir d'un standard automatique ou de contrôler les numéros de téléphone que peuvent composer les appelants qui ont contacté le standard automatique. Vous pouvez configurer ce qui suit :
    
      - **Appels dans le même plan de numérotation de messagerie unifiée**   Cochez cette case pour autoriser les utilisateurs qui appellent un standard automatique à effectuer ou à transférer des appels vers un numéro de poste associé à un utilisateur à extension messagerie unifiée qui est associé au même plan de numérotation que le standard automatique. Par défaut, ce paramètre est activé.
        
        Lorsque vous désactivez ce paramètre, les utilisateurs qui appellent un standard automatique peuvent établir ou transférer des appels vers des utilisateurs qui ne sont pas à extension messagerie unifiée ou vers d'autres numéros de postes qui ne sont pas associés à un utilisateur à extension messagerie unifiée. Les utilisateurs ne peuvent pas transférer d'appels vers des utilisateurs à extension messagerie unifiée qui sont associés au même plan de numérotation que le standard automatique. Cela est dû au fait que le paramètre **Autoriser les appels à tous les postes** est activé par défaut.
    
      - **Autoriser les appels à tous les postes**   Quand ce paramètre est désactivé, les utilisateurs qui appellent un standard automatique ne peuvent pas effectuer d'appels vers des utilisateurs qui ne sont pas à extension messagerie unifiée ou vers d'autres numéros de postes qui ne sont pas associés à un utilisateur à extension messagerie unifiée. Toutefois, ils peuvent établir ou transférer des appels vers des numéros de poste associés à des utilisateurs à extension messagerie unifiée. Cela est dû au fait que le paramètre **Appels appartenant au même plan de numérotation de messagerie unifiée** est activé par défaut. Le paramètre **Autoriser les appels à tous les postes** est activé par défaut.
        
        Lorsque ce paramètre est activé, les utilisateurs qui appellent un standard automatique peuvent établir des appels vers des utilisateurs sans extension messagerie unifiée, d'autres numéros de poste non associés à un utilisateur à extension messagerie unifiée et des utilisateurs à extension messagerie unifiée. Cela est dû au fait que le paramètre **Appels appartenant au même plan de numérotation de messagerie unifiée** est activé par défaut.
        
        Vous pouvez activer ce paramètre dans un environnement où tous les utilisateurs ne sont pas activés pour la messagerie unifiée. Ce paramètre est également utile si vous voulez autoriser des utilisateurs qui appellent un numéro de téléphone configuré sur un standard automatique à appeler des numéros de poste associés à un utilisateur à extension messagerie unifiée.
    
      - **Groupes de règles de numérotation nationales/régionales autorisés**   Cette section permet d'ajouter ou de supprimer des groupes de règles de numérotation dans le pays/la région autorisés. Par défaut, aucun groupe de règles de numérotation nationale/régionale n'est configuré pour les standards automatiques de messagerie unifiée.
        
        Des groupes de règles de numérotation nationales/régionales sont utilisés pour autoriser ou limiter les numéros de téléphone, dans un pays ou une région, qu'un utilisateur ayant appelé le standard automatique de messagerie unifiée peut composer. Cela permet d'empêcher des appels et frais téléphoniques superflus ou non autorisés.
        
        Pour ajouter des groupes de règles de numérotation nationale/régionale, vous devez commencer par créer les groupes de règles de numérotation nationales/régionales appropriés dans le plan de numérotation associé au standard automatique de messagerie unifiée, puis ajouter le groupe de règles de numérotation approprié.
        
        La messagerie unifiée peut utiliser des groupes de règles de numérotation nationale/régionale pour autoriser ou bloquer l'accès à des numéros de téléphone à l'intérieur d'un pays ou d'une région. Cela s'applique à tout utilisateur ayant appelé un standard automatique. Pour plus d'informations sur l'automate d'appels, consultez la rubrique [Autoriser les utilisateurs à effectuer des appels](allow-users-to-make-calls-exchange-2013-help.md).
    
      - **Groupes autorisés de règles de numérotation à l'international**   Cette section permet d'ajouter ou de supprimer des groupes autorisés de règles de numérotation à l'international. Par défaut, aucun groupe de règles de numérotation internationales n'est configuré sur les standards automatiques de messagerie unifiée.
        
        Des groupes de règles de numérotation internationales sont utilisés pour autoriser ou limiter les numéros de téléphone, extérieurs à un pays ou une région, qu'un utilisateur ayant appelé le standard automatique de messagerie unifiée peut composer. Cela permet d'empêcher des appels et frais téléphoniques superflus ou non autorisés.
        
        Pour ajouter des groupes de règles de numérotation à l'international, vous devez commencer par créer les groupes de règles de numérotation à l'internationale appropriés dans le plan de numérotation associé au standard automatique de messagerie unifiée. Après avoir créé les groupes de règles de numérotation requis pour le plan de numérotation, vous devez les ajouter à la liste des groupes de règles de numérotation autorisés sur le standard automatique de messagerie unifiée.
        
        La messagerie unifiée peut utiliser des groupes de règles de numérotation internationale pour autoriser ou bloquer l'accès à des numéros de téléphone à l'extérieur d'un pays ou d'une région. Cela s'applique à tout utilisateur ayant appelé un standard automatique. Pour plus d'informations sur l'automate d'appels, consultez la rubrique [Autoriser les utilisateurs à effectuer des appels](allow-users-to-make-calls-exchange-2013-help.md).

10. Cliquez sur **OK** pour créer le nouveau menu de navigation.

11. Dans la page **Standard automatique de messagerie unifiée**, cliquez sur **Enregistrer** pour enregistrer vos modifications.

## Utilisation de l'environnement Shell pour configurer les propriétés du standard automatique de messagerie unifiée

Cet exemple configure un standard automatique de messagerie unifiée nommé `MySpeechEnabledAA` pour basculer vers le standard automatique de `MyDTMFAA` , définit l'extension de l'opérateur à 50100 et permet à ce numéro de poste, les transferts après les heures de bureau.

    Set-UMAutoAttendant -Identity MySpeechEnabledAA -DTMFFallbackAutoAttendant MyDTMFAA -OperatorExtension 50100 -AfterHoursTransferToOperatorEnabled $true

Cet exemple montre comment configurer un standard automatique de messagerie unifiée nommé `MyUMAutoAttendant` qui présente les propriétés suivantes : Heures d'ouverture configurées de 10h45 à 13h15 le dimanche, de 9h00 à 17h00 le lundi et de 9h00 à 16h30 le samedi ; les congés et les messages d'accueil associés configurés sur « Nouvelle année » le 02.01.13 ; et « Bâtiment fermé pour construction » configuré du 24 avril au 28.04.13.

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -BusinessHoursSchedule 0.10:45-0.13:15,1.09:00-1.17:00,6.09:00-6.16:30 -HolidaySchedule "New Year,newyrgrt.wav,1/2/2013","Building Closed for Construction,construction.wav,4/24/2013,4/28/2013"

## Utilisation de l'environnement Shell pour afficher les propriétés du standard automatique de messagerie unifiée

Cet exemple montre comment renvoyer une liste mise en forme de tous les standards automatiques de messagerie unifiée.

    Get-UMAutoAttendant | Format-List

Cet exemple montre comment afficher les propriétés d'un standard automatique de messagerie unifiée nommé MyUMAutoAttendant.

    Get-UMAutoAttendant -Identity MyUMAutoAttendant

