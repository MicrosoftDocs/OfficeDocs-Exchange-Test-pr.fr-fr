---
title: 'Déploiement de la messagerie unifiée Exchange 2013: Exchange 2013 Help'
TOCTitle: Déploiement de la messagerie unifiée Exchange 2013
ms:assetid: d147d4b1-32d7-476b-b76f-ee3c0b35ba49
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ673564(v=EXCHG.150)
ms:contentKeyID: 50479223
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Déploiement de la messagerie unifiée Exchange 2013

 

_**Sapplique à :** Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2016-12-09_

La messagerie unifiée requiert l'intégration de votre déploiement Exchange Server au système de téléphonie existant de votre organisation. Un déploiement réussi nécessite une analyse attentive de votre infrastructure de téléphonie existante et d'effectuer les étapes de planification appropriées pour déployer et gérer la messagerie vocale dans la messagerie unifiée.

**Contenu de cette rubrique**

Avant le déploiement

Déploiement de la messagerie unifiée

Tâches consécutives au déploiement pour la messagerie unifiée

## Avant le déploiement

Avant de déployer la messagerie unifiée, nous vous conseillons de vous familiariser avec les concepts des rubriques suivantes :

  - [Plans de numérotation de messagerie unifiée](um-dial-plans-exchange-2013-help.md)

  - [Passerelles IP de messagerie unifiée](um-ip-gateways-exchange-2013-help.md)

  - [Services de messagerie unifiée](um-services-exchange-2013-help.md)

  - [Groupes de recherche de messagerie unifiée](um-hunt-groups-exchange-2013-help.md)

  - [Réponse et routage automatique d'appels entrants](automatically-answer-and-route-incoming-calls-exchange-2013-help.md)

  - [Stratégies de boîte aux lettres de messagerie unifiée](um-mailbox-policies-exchange-2013-help.md)

  - [Messagerie vocale pour les utilisateurs](voice-mail-for-users-exchange-2013-help.md)

## Déploiement de la messagerie unifiée

Que vous déployiez la messagerie unifiée à l’aide de PBX IP (Private Branch eXchange), de passerelles VoIP ou de Microsoft Lync Server, toutes les options de déploiement pour la messagerie unifiée ont plusieurs étapes en commun. Ces étapes sont nécessaires pour créer un système hautement disponible et évolutif pour la prise en charge d'un grand nombre d'utilisateurs de la messagerie unifiée. Ces étapes sont les suivantes :

1.  Déployez et configurez vos composants de téléphonie pour la messagerie unifiée.

2.  Vérifiez que vous avez correctement installé le serveur d'accès au client exécutant le service routeur des appels de messagerie unifiée Microsoft Exchange et le serveur de boîtes aux lettres exécutant le service de messagerie unifiée Microsoft Exchange.

3.  Créez et configurez les composants de messagerie unifiée requis.

4.  Effectuez toutes les tâches consécutives au déploiement pour la messagerie unifiée.

## Déploiement et configuration des composants de téléphonie

Pour déployer correctement la messagerie unifiée dans une organisation Exchange, l'administrateur Exchange doit maîtriser les concepts de réseau de données ainsi que les concepts et la terminologie de la téléphonie et être en mesure de configurer correctement les composants de téléphonie nécessaires à la messagerie unifiée. L'exécution d'un nouveau déploiement ou la mise à niveau d'un système de messagerie vocale hérité requièrent une solide connaissance des réseaux de téléphonie et de la messagerie unifiée.

Vous devez généralement réaliser trois tâches pour configurer les composants de téléphonie requis par la messagerie unifiée :

1.  **Fourniture de lignes PBX**   La première étape du déploiement d'une solution de messagerie unifiée hautement évolutive consiste à fournir des lignes PBX.

2.  **Organisation de canaux**   Après avoir fourni des canaux vocaux PBX, vous pouvez les organiser dans des groupements de postes.

3.  **Déploiement de passerelles VoIP**   Après avoir organisé vos canaux vocaux en groupements de postes, vous devez les terminer au niveau des passerelles VoIP. Les passerelles VoIP sont utilisées avec un PBX hérité pour convertir les protocoles de commutation par circuit présents sur un réseau téléphonique en protocoles IP à commutation par paquets.

Lorsque vous intégrez les réseaux de données et téléphonique de votre organisation lors du déploiement de la messagerie unifiée, vous devez configurer correctement les composants de réseau téléphonique et de données. Vous devez également configurer les composants ou interfaces suivants pour déployer correctement la messagerie unifiée :

  - **Configurez la connexion des PBX de votre organisation afin qu'ils puissent communiquer avec vos passerelles VoIP.**   Pour obtenir des informations détaillées, consultez la rubrique [Connecter une passerelle voix sur IP pour communiquer avec un PBX](connect-a-voip-gateway-to-communicate-with-a-pbx-exchange-2013-help.md).

  - **Configurez la connexion de votre interface de passerelle VoIP au PBX.**   Pour plus d'informations sur la configuration de votre interface PBX pour qu'elle communique avec votre passerelle VoIP prise en charge, consultez la documentation produit spécifique à votre PBX ou la rubrique [Connecter une passerelle voix sur IP pour communiquer avec un PBX](connect-a-voip-gateway-to-communicate-with-a-pbx-exchange-2013-help.md).

  - **Configurez la connexion de l'interface de passerelle VoIP aux serveurs d'accès au client et de boîtes aux lettres..**   Pour obtenir des informations détaillées, consultez la rubrique [Connexion d’une passerelle VoIP, d’un IP PBX ou d’un contrôleur SBC à la messagerie unifiée](connect-a-voip-gateway-ip-pbx-or-session-border-controller-to-um-exchange-2013-help.md).

  - **Configurez la connexion à partir des serveurs d'accès au client et de boîtes aux lettes vers l'interface de passerelle VoIP.**   Pour obtenir des informations détaillées, consultez la rubrique [Connecter la messagerie unifiée à une passerelle VoIP pris en charge](connect-um-to-a-supported-voip-gateway-exchange-2013-help.md).

Avant le déploiement

## Installer les serveurs de boîtes aux lettres et d'accès au client

Différents chemins de déploiement sont disponibles pour les organisations qui envisagent de déployer la messagerie unifiée Exchange. Bien qu'ils aboutissent tous au même résultat final (un déploiement réussi de la messagerie unifiée), chaque chemin est légèrement différent, car les besoins et les points de départ de chaque client sont différents. Toutefois, des points de départ et des chemins communs couvrent généralement tous les scénarios de déploiement pris en charge, y compris les nouvelles installations et mises à niveau. Pour déployer vos serveurs d'accès au client et de boîtes aux lettres, procédez comme suit :

1.  Vérifiez que votre infrastructure existante répond à certaines conditions préalables. Pour plus d'informations, consultez la rubrique [Conditions préalables pour Exchange 2013](exchange-2013-prerequisites-exchange-2013-help.md).

2.  Déployez votre nouvelle organisation Exchange 2013. Pour plus d'informations, consultez la rubrique [Installer Exchange 2013 à l’aide de l’Assistant Installation](install-exchange-2013-using-the-setup-wizard-exchange-2013-help.md).
    
    > [!WARNING]
    > Vous devez déployer au moins un serveur de boîtes aux lettres Exchange 2013 dans votre organisation avant de configurer les passerelles VoIP ou les PBX IP pour envoyer le trafic SIP ou RTP de messagerie unifiée vers les serveurs d’accès client Exchange 2013.


3.  Vérifiez que vous avez correctement installé les serveurs d'accès au client et de boîtes aux lettres. Après avoir installé les serveurs, nous vous recommandons de vérifier l'installation et de consulter les journaux d'installation du serveur. Pour plus d'informations, consultez la rubrique [Vérifier une installation d’Exchange 2013](verify-an-exchange-2013-installation-exchange-2013-help.md).

## Ajout des modules linguistiques de messagerie unifiée requis

Les modules linguistiques de messagerie unifiée permettent aux appelants et aux utilisateurs d'Outlook Voice Access d'interagir avec le système de messagerie unifiée dans plusieurs langues. Après que vous avez installé un module linguistique supplémentaire sur un serveur de boîtes aux lettres, les appelants et les utilisateurs d'Outlook Voice Access ont la possibilité d'écouter les messages électroniques et d'interagir avec le système de messagerie vocale dans cette langue.

Lorsque vous installez , l'anglais (É.U.) est la langue par défaut et la seule option de langue disponible pour votre plan de numérotation. Après que vous avez installé un module linguistique sur un serveur de messagerie unifiée, la langue associée au module linguistique est aussi répertoriée comme une option disponible lorsque vous configurez la langue par défaut du plan de numérotation. Par défaut, comme les standards automatiques de messagerie unifiée sont associés à un plan de numérotation de messagerie unifiée lors de leur création, ils utilisent le paramètre de langue par défaut de ce plan. Cependant, ce paramètre peut être modifié après la création du standard automatique de messagerie unifiée.

Vous pouvez ajouter des modules linguistiques de messagerie unifiée à l'aide de la commande Setup.exe ou en exécutant le programme d'installation *\<UMLanguagePack\>*.exe après avoir téléchargé le module linguistique de messagerie unifiée à partir de la page [Exchange Server 2013 UM Language Packs - Français](https://go.microsoft.com/fwlink/p/?linkid=266542). Cependant, vous devez utiliser la commande Setup.exe pour supprimer un module linguistique de messagerie unifiée. Il n'existe aucune cmdlet de l'environnement de ligne de commande Exchange Management Shell permettant d'ajouter ou de supprimer des modules linguistiques d'un serveur de boîte aux lettres. Pour plus d'informations sur l'installation d'un module linguistique de messagerie unifiée, consultez la rubrique [Installer un module linguistique de messagerie unifiée](install-a-um-language-pack-exchange-2013-help.md).

> [!NOTE]
> Par défaut, lorsque vous installez un serveur de boîtes aux lettres, l'anglais (États-Unis) est installé. Il ne peut pas être retiré, sauf si vous supprimez le serveur de boîtes aux lettres à partir de l'ordinateur.


Avant le déploiement

## Créer et configurer des composants de messagerie unifiée

Il existe plusieurs composants de messagerie unifiée nécessaires au déploiement et au fonctionnement de la messagerie unifiée. Les composants de messagerie unifiée connectent l'infrastructure téléphonique à l'environnement de messagerie unifiée. Après avoir correctement installé les serveurs d'accès au client et de boîtes aux lettres, procédez comme suit.

## Étape 1 : Création et configuration des plans de numérotation de messagerie unifiée

Les plans de numérotation de messagerie unifiée jouent un rôle essentiel dans le fonctionnement de la messagerie unifiée et sont nécessaires pour déployer correctement la messagerie unifiée sur votre réseau. Après avoir installé correctement vos serveurs d'accès au client et de boîtes aux lettres, un plan de numérotation de messagerie unifiée sera le premier composant à créer.

Par défaut, les plans de numérotation de messagerie unifiée et les serveurs d'accès au client et de boîtes aux lettres qui sont associés au plan de numérotation envoient et reçoivent les données sans utiliser de chiffrement. En mode non sécurisé, les trafics VoIP et SIP ne sont pas chiffrés. Lorsque vous créez le plan de numérotation ou après l'avoir créé, vous pouvez le configurer pour chiffrer les trafics VoIP et SIP à l'aide de l'authentification TLS (Transport Layer Security) mutuelle. Pour utiliser le protocole TLS mutuel, vous devez définir le plan de numérotation sur le mode Sécurisé ou Sécurisé SIP, définir le mode de démarrage de messagerie unifiée sur TLS ou Double, et créer et distribuer un certificat approuvé entre les serveurs Exchange et les passerelles VoIP, les PBX IP ou les contrôleurs de limite de session (SBC). Après avoir configuré le paramètre de sécurité VoIP, vous devrez configurer le mode de démarrage des serveurs d'accès au client et de boîtes aux lettres. Pour plus d'informations, consultez la rubrique [Configuration du mode de démarrage sur un serveur de boîtes aux lettres](configure-the-startup-mode-on-a-mailbox-server-exchange-2013-help.md) ou [Configurer le mode de démarrage sur un serveur d'accès au Client](configure-the-startup-mode-on-a-client-access-server-exchange-2013-help.md).

Effectuez la procédure suivante pour créer un plan de numérotation de messagerie unifiée.

## Créer un plan de numérotation de messagerie unifiée

1.  Dans le Centre d'administration Exchange (CAE), accédez à **Messagerie unifiée** \> **Plans de numérotation de messagerie unifiée**, puis cliquez sur **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter").

2.  Dans la page **Nouveau plan de numérotation de messagerie unifiée**, complétez les champs suivants :
    
      - **Nom**   Tapez le nom du plan de numérotation. Un nom de plan de numérotation de messagerie unifiée est obligatoire et doit être unique. Le nom entré est utilisé uniquement à des fins d'affichage dans le CAE et l'environnement de ligne de commande Exchange Management Shell. La longueur maximale d'un nom de plan de numérotation de messagerie unifiée est de 64 caractères pouvant contenir des espaces. Toutefois, il ne peut contenir aucun des caractères suivants : " / \\ \[ \] : ; | = , + \* ? \< \>.
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/JJ159813.important(EXCHG.150).gif" title="Important" alt="Important" />Important :</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>Bien que le champ destiné au nom du plan de numérotation puisse accepter 64 caractères, la longueur du nom du plan de numérotation ne peut pas être supérieure à 49 caractères. En effet, lorsque vous créez un plan de numérotation, une stratégie de boîte aux lettres de messagerie unifiée par défaut est également créée avec le nom de stratégie par défaut <em>&lt;DialPlanName&gt;</em>. Le paramètre <em>name</em> du plan de numérotation de messagerie unifiée et de la stratégie de boîte aux lettres de messagerie unifiée peut comporter jusqu'à 64 caractères.</td>
        </tr>
        </tbody>
        </table>
    
      - **Longueur des numéros de poste (chiffres)**   Entrez le nombre de chiffres pour les numéros de poste dans le plan de numérotation. Le nombre de chiffres des numéros de poste repose sur le plan de numérotation des appels téléphoniques créé sur un PBX. Par exemple, si un utilisateur associé à un plan de numérotation téléphonique compose un poste à 4 chiffres pour appeler un autre utilisateur du même plan de numérotation téléphonique, sélectionnez 4 pour le nombre de chiffres du poste.
        
        Ce champ est obligatoire et la plage de valeurs est comprise entre 1 et 20. En règle générale, le numéro de poste comprend entre 3 et 7 chiffres. Si votre environnement téléphonique existant inclut des numéros de poste, vous devez spécifier un nombre de chiffres correspondant au nombre de chiffres que comportent ces numéros de poste.
        
        Lorsque vous créez un plan de numérotation de numéro de poste, vous devez saisir un numéro de poste pour l’utilisateur lié à ce plan. Un numéro de poste est également nécessaire avec les plans de numérotation SIP (Session Initiation Protocol) ou les plans de numérotation E.164 lorsqu'un utilisateur à extension messagerie unifiée est lié à un plan de numérotation URI SIP ou E.164. Ce numéro de poste est utilisé par des utilisateurs d'Outlook Voice Access pour accéder à leur boîte aux lettres Exchange.
    
      - UNRESOLVED\_TOKENBLOCK\_VAL(Type UI\_URI)
    
      - UNRESOLVED\_TOKENBLOCK\_VAL(Sécurité UI\_VoIP)
    
      - **Code de pays/région**   Ce champ permet de saisir le code numérique du pays/de la région à utiliser pour les appels sortants. Ce numéro est automatiquement ajouté devant le numéro de téléphone composé. Ce champ peut recevoir 1 à 4 chiffres. Par exemple, aux États-Unis, le code du pays/de la région est 1. Au Royaume-Uni, ce code est 44.

3.  Cliquez sur **Enregistrer**.
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ159813.important(EXCHG.150).gif" title="Important" alt="Important" />Important :</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Dans les versions antérieures d'Exchange, le serveur de messagerie unifiée devait être ajouté à un plan de numérotation de messagerie unifiée. Dans Exchange 2013, les serveurs d’accès au client et de boîtes aux lettres ne peuvent pas être associés à un plan de numérotation de numéro de poste ou E.164. Les serveurs d'accès au client et de boîtes aux lettres répondront à tous les appels entrants pour tous les types de plans de numérotation. Cependant, si vous intégrez la messagerie unifiée à Microsoft Lync Server, vous devez ajouter tous les serveurs d’accès au client et de boîtes aux lettres à l’ensemble des plans de numérotation URI SIP afin de permettre un fonctionnement parfait d’acheminement des appels avec Lync Server.</td>
    </tr>
    </tbody>
    </table>


Avant le déploiement

## Étape 2 : Création et configuration d'une passerelle IP de messagerie unifiée

Une passerelle IP de messagerie unifiée représente un périphérique matériel de passerelle IP ou un PBX IP. L'association de la passerelle IP de messagerie unifiée et d'un groupement de postes de messagerie unifiée établit un lien entre une passerelle VoIP ou un PBX IP et un plan de numérotation de messagerie unifiée.

Si vous avez créé ou activé une sécurité VoIP sur un plan de numérotation, la passerelle IP de messagerie unifiée que vous allez créer à l'aide d'une des procédures suivantes sera associée à un plan de numérotation de messagerie unifiée qui utilise la sécurité VoIP. Dans ce cas, vous devez utiliser un nom de domaine complet pour créer la passerelle IP de messagerie unifiée, et non une adresse IP. Vous devez également configurer la passerelle IP de messagerie unifiée pour écouter sur le port TCP 5061. Pour ce faire, exécutez la commande suivante : `Set-UMIPGateway -identity MyUMIPGateway -Port 5061`. Vous devez également vérifier que les passerelles VoIP ou les PBX IP ont également été configurés pour écouter sur le port 5061 pour le protocole TLS mutuel.

Effectuez la procédure suivante pour créer une passerelle de messagerie unifiée.

## Créer une passerelle IP de messagerie unifiée

1.  
    
    Dans le CAE, accédez à **Messagerie unifiée** \> **Passerelles IP de messagerie unifiée**, puis, cliquez sur **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter").

2.  Dans la page **Nouvelle passerelle IP de messagerie unifiée**, entrez les informations suivantes :
    
      - **Nom**   Cette zone de texte permet de spécifier un nom unique pour la passerelle IP de messagerie unifiée. Il s'agit du nom complet qui apparaît dans le CAE. Si vous devez modifier le nom complet de la passerelle IP de messagerie unifiée après sa création, vous devez d'abord supprimer la passerelle IP de messagerie unifiée existante, puis en créer une autre avec le nom approprié. Le nom de passerelle IP de messagerie unifiée est obligatoire mais utilisé à des fins d'affichage uniquement. Dans la mesure où votre organisation peut utiliser plusieurs passerelles IP de messagerie unifiée, nous vous recommandons d'utiliser des noms significatifs pour ces passerelles. La longueur maximale d'un nom de passerelle IP de messagerie unifiée est de 64 caractères pouvant contenir des espaces. Toutefois, il ne peut contenir aucun des caractères suivants : " / \\ \[ \] : ; | = , + \* ? \< \>.
    
      - **Adresse**   Vous pouvez configurer une passerelle IP de messagerie unifiée soit avec une adresse IP soit avec un nom de domaine complet. Utilisez cette boîte de dialogue pour spécifier l'adresse IP configurée sur la passerelle VoIP, au standard privé (PBX) SIP, PBX IP ou SBC ou un nom de domaine complet. Cette boîte de dialogue n'accepte que des noms de domaine complets valides et correctement mis en forme.
        
        Vous pouvez entrer des caractères alphabétiques et numériques dans cette zone. Les adresses IPv4, IPv6 et les adresses avec un nom de domaine complet sont prises en charge. Si vous souhaitez utiliser le protocole TLS mutuel entre une passerelle IP de messagerie unifiée et un plan de numérotation fonctionnant en mode Sécurisé SIP ou en mode sécurisé, vous devez configurer la passerelle IP de messagerie unifiée avec un nom de domaine complet. Vous devez également la configurer pour écouter le port 5061 et vérifier que les passerelles VoIP ou les PBX IP ont également été configurés pour écouter les demandes TLS mutuelles sur le port 5061. Pour configurer une passerelle IP de messagerie unifiée, exécutez la commande suivante : `Set-UMIPGateway -identity MyUMIPGateway -Port 5061`.
        
        Si vous utilisez un nom de domaine complet, vous devez également vous assurer que vous avez correctement configuré un enregistrement d’hôte DNS pour la passerelle VoIP afin de résoudre correctement le nom d’hôte en adresse IP. De même, si vous utilisez un nom de domaine complet à la place d'une adresse IP et si la configuration DNS de la passerelle IP de messagerie unifiée est modifiée, vous devez désactiver puis activer la passerelle IP de messagerie unifiée pour garantir une mise à jour correcte des informations de configuration de cette passerelle IP de messagerie unifiée
    
      - **Plan de numérotation de messagerie unifiée**   Cliquez sur le bouton **Parcourir** pour sélectionner le plan de numérotation de messagerie unifiée que vous voulez associer à la passerelle IP de messagerie unifiée. Lorsque vous sélectionnez un plan de numérotation de messagerie unifiée à associer à une passerelle IP de messagerie unifiée, un groupement de postes de messagerie unifiée est également créé par défaut et associé au plan de numérotation de messagerie unifiée que vous avez sélectionné. Si vous ne sélectionnez pas de plan de numérotation de messagerie unifiée, vous devez créer manuellement un groupement de postes de messagerie unifiée, puis l'associer à la passerelle IP de messagerie unifiée que vous avez créée.

3.  
    
    Cliquez sur **Enregistrer**.

## Étape 3 : Création et configuration des groupements de postes de messagerie unifiée (facultatif)

Le terme *groupement de postes* sert à décrire un groupe de ressources ou de numéros de poste PBX ou PBX IP qui sont partagés par les utilisateurs. Les groupements de postes servent à répartir efficacement les appels au sein de ou en dehors d'une division donnée.

Si vous avez créé une passerelle IP de messagerie unifiée et l'avez associée à un plan de numérotation de messagerie unifiée, un groupement de postes de messagerie unifiée par défaut a été créé. Vous pouvez associer un autre groupement de postes de messagerie unifiée à la même ou à une autre passerelle IP de messagerie unifiée, en fonction du nombre de passerelles IP de messagerie unifiée créées.

Lorsque vous créez un groupement de postes de messagerie unifiée, vous permettez à tous les serveurs de boîtes aux lettres qui sont spécifiés dans le plan de numérotation de messagerie unifiée de communiquer avec une passerelle VoIP. Pour plus d'informations, consultez la rubrique [Groupes de recherche de messagerie unifiée](um-hunt-groups-exchange-2013-help.md).

## Créer un groupement de postes de messagerie unifiée

1.  Dans le CAE, accédez à **Messagerie unifiée** \> **Plans de numérotation de messagerie unifiée**. Dans l'affichage Liste, sélectionnez le plan de numérotation de messagerie unifiée à modifier puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

2.  Dans la page **Plan de numérotation de messagerie unifiée**, sous **Groupements de postes de messagerie unifiée**, cliquez sur **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter").

3.  Dans la page **Nouveau groupement de postes de messagerie unifiée**, complétez les champs suivants :
    
      - **Passerelle IP de messagerie unifiée associée**   Ce champ en affichage seul indique le nom de la passerelle IP de messagerie unifiée associée au groupement de postes de messagerie unifiée.
    
      - **Nom**   Ce champ permet de saisir le nom complet du groupement de postes de messagerie unifiée. Un nom de groupement de postes de messagerie unifiée est requis et doit être unique, mais il est uniquement utilisé à des fins d'affichage dans le CAE et l'environnement de ligne de commande Exchange Management Shell. Si vous voulez modifier le nom d’affichage du groupement de postes après sa création, vous devez d’abord supprimer le groupement de postes existant, puis en créer un autre avec le nom approprié.
        
        Si votre organisation utilise plusieurs groupements de postes, nous vous recommandons d'utiliser des noms significatifs pour ces derniers. La longueur maximale d'un nom de groupement de postes de messagerie unifiée est de 64 caractères pouvant contenir des espaces. Toutefois, il ne peut contenir aucun des caractères suivants : " / \\ \[ \] : ; | = , + \* ? \< \>.
    
      - **Plan de numérotation**   Cliquez sur **Parcourir** pour sélectionner le plan de numérotation à associer au groupement de postes de messagerie unifiée. L'association d'un groupement de postes à un plan de numérotation est obligatoire. Un groupement de postes de messagerie unifiée peut être associé à une seule passerelle IP de messagerie unifiée et un seul plan de numérotation de messagerie unifiée.
    
      - **Identificateur de pilote**   Ce champ permet de spécifier une chaîne qui fournit une identification unique de l'identificateur de pilote (ID de pilote) configuré sur le PBX ou le PBX IP.
        
        Un numéro de poste ou un URI (Uniform Resource Identifier) du protocole SIP (Session Initiated Protocol) peut être utilisé dans ce champ. Les caractères alphanumériques sont acceptés dans ce champ. Pour les PBX hérités, une valeur numérique est utilisée comme identificateur de pilote. Toutefois, certains PBX IP peuvent utiliser les URI SIP.

4.  Cliquez sur **Enregistrer**.

Avant le déploiement

## Étape 4 : Création et configuration d'une stratégie de boîte aux lettres de messagerie unifiée

Des stratégies de boîte aux lettres de messagerie unifiée sont requises lorsque vous activez la messagerie unifiée pour des utilisateurs. La boîte aux lettres de chaque utilisateur à extension messagerie unifiée doit être liée à une seule stratégie de boîte aux lettres de messagerie unifiée. Une fois que vous avez créé une stratégie de boîte aux lettres de messagerie unifiée, vous devez relier une ou plusieurs boîtes aux lettres de messagerie unifiée à cette stratégie. Cela permet de contrôler les paramètres de sécurité du code confidentiel, tels que le nombre minimal de chiffres dans un code confidentiel ou le nombre maximal d'échecs d'ouverture de session pour les utilisateurs à extension messagerie unifiée qui sont associés à la stratégie de boîte aux lettres de messagerie unifiée.

Lorsque vous créez un plan de numérotation de messagerie unifiée, une stratégie de boîte aux lettres de messagerie unifiée est également créée. La stratégie de boîte aux lettres de messagerie unifiée est nommée Stratégie par défaut \<*DialPlanName*\>. Toutefois, si vous devez créer une stratégie de boîte aux lettres de messagerie unifiée, procédez comme suit.

## Créer une stratégie de boîte aux lettres de messagerie unifiée

1.  
    
    Dans le Centre d'administration Exchange, accédez à **Messagerie unifiée** \> **Plans de numérotation de messagerie unifiée**. Dans l'affichage Liste, sélectionnez le plan de numérotation de messagerie unifiée à modifier, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

2.  Dans la page **Plan de numérotation de messagerie unifiée**, sous **Stratégies de boîte aux lettres de messagerie unifiée**, cliquez sur **Ajouter** ![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter").

3.  Dans la page **Nouvelle stratégie de boîte aux lettres de messagerie unifiée**, dans le champ **Nom**, saisissez le nom de la nouvelle stratégie de boîte aux lettres de messagerie unifiée.
    
    Ce champ permet de spécifier un nom unique pour la stratégie de boîte aux lettres de messagerie unifiée. Il s'agit du nom complet qui apparaît dans le CAE. Si vous devez modifier le nom complet de la stratégie de boîte aux lettres de messagerie unifiée après sa création, vous devez d'abord supprimer la stratégie de boîte aux lettres de messagerie unifiée existante, puis créer une autre stratégie avec le nom approprié. Il n’est pas possible de supprimer une stratégie de boîte aux lettres de messagerie unifiée si l’un des utilisateurs à extension messagerie unifiée y est associé.
    
    Le nom de stratégie de boîte aux lettres de messagerie unifiée est obligatoire mais utilisé à des fins d'affichage uniquement. Dans la mesure où votre organisation peut utiliser plusieurs stratégies de boîte aux lettres de messagerie unifiée, nous vous recommandons d'utiliser des noms significatifs pour chaque stratégie. La longueur maximale d'un nom de stratégie de boîte aux lettres de messagerie unifiée est de 64 caractères pouvant contenir des espaces. Toutefois, il ne peut pas contenir les caractères suivants : " / \\ \[ \] : ; | = , + \* ? \< \>.

4.  Cliquez sur **Enregistrer** pour enregistrer la nouvelle stratégie de boîte aux lettres de messagerie unifiée. Lorsque vous enregistrez la stratégie de boîte aux lettres de messagerie unifiée, l'ensemble des paramètres par défaut, y compris les stratégies de code confidentiel, les fonctionnalités de messagerie vocale et les paramètres de messagerie vocale protégée sont activés. Si vous souhaitez personnaliser ou modifier les paramètres par défaut, utilisez la cmdlet **Set-UMMailbox** pour modifier les paramètres de la stratégie de boîte aux lettres de messagerie unifiée que vous venez de créer.

## Étape 5 : Création et configuration des standards automatiques de messagerie unifiée (facultatif)

La messagerie unifiée vous permet de créer un ou plusieurs standards automatiques de messagerie unifiée en fonction des besoins de votre organisation. Lorsque vous créez un standard automatique de messagerie unifiée, vous créez un système de menu vocal pour votre organisation. Les appelants internes ou externes à votre organisation peuvent alors se déplacer dans le système de menu pour localiser et placer ou transférer les appels vers les utilisateurs ou services de votre organisation.

Les appelants peuvent se déplacer dans le système de menu à l'aide de la multifréquence bi-tonalité (DTMF), appelée également entrées vocales ou à tonalité. Pour que la reconnaissance vocale automatique fonctionne de sorte que les utilisateurs puissent utiliser les entrées vocales, vous devez activer la reconnaissance vocale pour votre standard automatique de messagerie unifiée.

La création et l'utilisation des standards automatiques sont facultatives dans la messagerie unifiée. Toutefois, si vous voulez créer un standard automatique de messagerie unifiée, procédez comme suit.

## Créer un standard automatique de messagerie unifiée

1.  
    
    Dans le CAE, accédez à **Messagerie unifiée** \> **Plans de numérotation de messagerie unifiée**, sélectionnez le plan de numérotation pour lequel vous voulez ajouter un standard automatique, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

2.  Dans la page **Plan de numérotation de messagerie unifiée**, sous **Standards automatiques de messagerie unifiée**, cliquez sur **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter").

3.  Dans la page **Nouveau standard automatique de messagerie unifiée**, complétez les champs suivants :
    
      - **Nom**   Ce champ permet de créer le nom complet du standard automatique de messagerie unifiée. Un nom de standard automatique de messagerie unifiée est obligatoire et doit être unique. Toutefois, il est uniquement utilisé à des fins d'affichage dans le CAE et l'environnement de ligne de commande Exchange Management Shell.
        
        Si vous devez modifier le nom complet du standard automatique après sa création, vous devez d'abord supprimer le standard automatique de messagerie unifiée existant, puis créer un autre standard automatique avec le nom approprié. Si votre organisation utilise plusieurs standards automatiques de messagerie unifiée, nous vous recommandons d'utiliser des noms significatifs pour vos standards automatiques de messagerie unifiée. La longueur maximale d'un nom de standard automatique de messagerie unifiée est de 64 caractères pouvant contenir des espaces.
        
        Bien que vous puissiez nommer un nouveau standard automatique de messagerie unifiée pour inclure des espaces, si vous intégrez la messagerie unifiée à Office Communications Server 2007 R2 ou à Microsoft Lync Server, le nom du standard automatique ne peut pas contenir d’espaces. Par conséquent, si vous avez créé un standard automatique dont le nom complet comprend des espaces et que vous voulez intégrer ce standard à Office Communications Server 2007 R2 ou Lync Server, vous devez d’abord supprimer ce standard automatique, puis en créer un nouveau qui n’inclut pas d’espaces dans le nom complet.
    
      - **Créer ce standard automatique comme activé**   Cochez cette case pour permettre au standard automatique de répondre aux appels entrants une fois le standard automatique de messagerie unifiée créé. Par défaut, un nouveau standard automatique est créé comme désactivé.
        
        Si vous décidez de créer un standard automatique de messagerie unifiée comme désactivé, vous pouvez utiliser le CAE ou l'environnement de ligne de commande Exchange Management Shell après avoir créé le standard automatique.
    
      - **Définissez le standard automatique pour répondre aux commandes vocales**   Cochez cette case pour que le standard automatique de messagerie unifiée puisse utiliser la reconnaissance vocale. Si la reconnaissance vocale est activée pour le standard automatique, les appelants répondent aux invites personnalisées ou système utilisées par le standard automatique de messagerie unifiée en utilisant des entrées vocales ou à tonalité. Par défaut, le standard automatique n'est pas à reconnaissance vocale au moment de sa création.
        
        Pour que les appelants utilisent un standard automatique à reconnaissance vocale dans une langue autre que l'anglais (États-Unis), vous devez installer le module linguistique de messagerie unifiée approprié et configurer les propriétés du standard automatique pour utiliser cette langue. Le module linguistique de messagerie unifiée des États-Unis est installé par défaut lorsque vous installez un serveur de boîtes aux lettres.
    
      - **Numéros d'accès**   Ce champ permet d'entrer les numéros de poste ou de téléphone que les appelants utilisent pour atteindre le standard automatique. Tapez un numéro de poste ou un numéro de téléphone dans ce champ, puis cliquez sur **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter") pour ajouter le numéro à la liste. Le nombre de chiffres du numéro de poste ou du numéro de téléphone que vous composez ne doit pas correspondre au nombre de chiffres d'un numéro de poste configuré dans le plan de numérotation de messagerie unifiée associé. En effet, les appels directs sont permis aux standards automatiques de messagerie unifiée.
        
        Le nombre de numéros de poste ou d'identificateurs de pilote que vous saisissez est illimité. Toutefois, vous pouvez créer un nouveau standard automatique sans numéro de poste ou numéro de téléphone répertorié. Aucun numéro de poste ou numéro de téléphone n'est requis.
        
        Vous pouvez modifier ou supprimer un numéro de poste ou identificateur de pilote existant. Pour modifier un numéro de poste ou un numéro de téléphone existant, cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier"). Pour supprimer un numéro de poste existant ou un numéro de téléphone de la liste, cliquez sur **Supprimer**![Icône Suppression](images/Dd362328.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "Icône Suppression").

4.  Cliquez sur **Enregistrer**.

Avant le déploiement

## Tâches consécutives au déploiement pour la messagerie unifiée

Après avoir terminé une nouvelle installation des serveurs d'accès au client et de boîtes aux lettres et déployé correctement la messagerie unifiée, vous devez compléter les tâches consécutives au déploiement. Les tâches consécutives au déploiement vont vous permettre d'activer les utilisateurs pour la messagerie unifiée, de sécuriser le déploiement de la messagerie unifiée et de déployer les télécopies entrantes pour les utilisateurs à extension messagerie unifiée.

## Activer les utilisateurs pour la messagerie vocale.

Après avoir déployé vos passerelles VoIP ou PBX IP, installé les serveurs d'accès au client et de boîtes aux lettres et créé les composants requis pour la messagerie unifiée, vous devez activer les utilisateurs pour la messagerie unifiée. Pour plus d'informations, consultez la rubrique [Activation de la messagerie vocale pour un utilisateur](enable-a-user-for-voice-mail-exchange-2013-help.md).

## Protéger la messagerie vocale

La messagerie unifiée peut être configurée de manière utiliser AD RMS (Active Directory Rights Management Services) pour protéger les messages vocaux d'une organisation. Cette fonctionnalité est appelée Messagerie vocale protégée. Lorsqu'un message vocal est protégé, le destinataire ne peut non seulement pas le transférer, mais la messagerie unifiée garantit également que seuls le ou les destinataires peuvent accéder à son contenu. Les messages vocaux protégés sont accessibles via Microsoft Outlook 2010 ou version ultérieure, Outlook Web App ou Outlook Voice Access. Pour plus d'informations, consultez la rubrique [Protéger la messagerie vocale](protect-voice-mail-exchange-2013-help.md).

## Mutual TLS pour la messagerie unifiée

Pour utiliser le protocole TLS mutuel pour chiffrer le trafic SIP et RTP (Realtime Transport Protocol) échangé avec vos serveurs d'accès au client et de boîtes aux lettres, effectuez les tâches suivantes :

  - Exécutez l'Assistant Certificat Exchange. Pour plus d'informations, consultez la rubrique [Déploiement de certificats pour la messagerie unifiée](deploying-certificates-for-um-exchange-2013-help.md).

  - Importer le certificat sur les serveurs d'accès au client et de boîtes aux lettres.

  - Importez les certificats requis sur les passerelles VoIP, les PBX IP et les serveurs d'accès au client et de boîtes aux lettres de votre organisation.

  - Configurez la sécurité VoIP sur les plans de numérotation de messagerie unifiée. Pour plus d'informations, consultez la rubrique [Configuration du paramètre de sécurité VoIP](configure-the-voip-security-setting-exchange-2013-help.md).

  - Configurer le mode de démarrage sur les serveurs d'accès au client et de boîtes aux lettres. Pour plus de détails, consultez les rubriques [Configuration du mode de démarrage sur un serveur de boîtes aux lettres](configure-the-startup-mode-on-a-mailbox-server-exchange-2013-help.md) et [Configurer le mode de démarrage sur un serveur d'accès au Client](configure-the-startup-mode-on-a-client-access-server-exchange-2013-help.md).

  - Configurez les passerelles IP de messagerie unifiée pour écouter sur le port 5061. Pour plus d'informations, consultez la rubrique [Configuration du port d'écoute](configure-the-listening-port-exchange-2013-help.md).

## Stratégies de code confidentiel pour les utilisateurs à extension messagerie unifiée

Dans la messagerie unifiée, les stratégies de code confidentiel sont définies et configurées selon une stratégie de boîte aux lettres de messagerie unifiée. Lorsque vous activez un utilisateur pour la messagerie unifiée, vous associez cet utilisateur à une stratégie de boîte aux lettres de messagerie unifiée existante. Les stratégies de code confidentiel de messagerie unifiée qui sont configurées dans la stratégie de boîte aux lettres de messagerie unifiée doivent être conformes aux critères de sécurité de votre organisation. Pour plus d'informations sur la configuration des paramètres de code confidentiel pour les utilisateurs à extension messagerie unifiée, consultez la rubrique [Définition de la sécurité des codes confidentiels d'Outlook Voice Access](set-outlook-voice-access-pin-security-exchange-2013-help.md).

## Configurer les fonctionnalités de messagerie vocale cliente

Suite au déploiement de vos serveurs et des composants de messagerie unifiée requis, vous pouvez configurer différentes fonctionnalités facultatives liées à la messagerie vocale. Pour plus d'informations, consultez les rubriques suivantes :

  - [Configuration d’Outlook Voice Access](setting-up-outlook-voice-access-exchange-2013-help.md)

  - [Activation du transfert d'appels pour des utilisateurs de messagerie vocale](allow-voice-mail-users-to-forward-calls-exchange-2013-help.md)

  - [Activer la transcription des messages vocaux pour les utilisateurs](allow-users-to-see-a-voice-mail-transcript-exchange-2013-help.md)

  - [Activation de la réception de télécopies pour les utilisateurs de messagerie vocale](enable-voice-mail-users-to-receive-faxes-exchange-2013-help.md)

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159813.important(EXCHG.150).gif" title="Important" alt="Important" />Important :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Si vous intégrez votre environnement de messagerie unifiée à Microsoft Lync Server, plusieurs éléments supplémentaires sont à prendre en compte pour la planification. Pour plus d'informations, consultez la rubrique <a href="deploying-exchange-2013-um-and-lync-server-overview-exchange-2013-help.md">Présentation du déploiement de la messagerie unifiée Exchange 2013 et de Lync Server</a>.</td>
</tr>
</tbody>
</table>


Avant le déploiement

