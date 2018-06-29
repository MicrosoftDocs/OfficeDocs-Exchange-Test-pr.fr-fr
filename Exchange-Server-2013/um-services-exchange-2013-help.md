---
title: 'Services de messagerie unifiée: Exchange 2013 Help'
TOCTitle: Services de messagerie unifiée
ms:assetid: f36835f2-1e5f-4e5a-88bc-0672af1e3498
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb125191(v=EXCHG.150)
ms:contentKeyID: 50555519
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Services de messagerie unifiée

 

_**Sapplique à :**Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :**2012-11-18_

Les serveurs d'accès au client qui exécutent le service routeur d'appels de messagerie unifiée Microsoft Exchange et les serveurs de boîtes aux lettres qui exécutent le service de messagerie unifiée Microsoft Exchange vous permettent de déployer une messagerie unifiée et des fonctionnalités de messagerie vocale pour les utilisateurs de votre organisation.

Souhaitez-vous rechercher les tâches de gestion relatives aux services de messagerie unifiée ? Voir [Procédures de services de messagerie unifiée](um-services-procedures-exchange-2013-help.md).

**Contenu de cette rubrique**

Client Access and Mailbox servers

Server configuration settings

Server operation

## Serveurs d'accès au client et de boîtes aux lettres

Dans Exchange 2013, les rôles serveur figurant dans Exchange 2007 et Exchange 2010 sont combinés en deux types de serveurs et tous les composants ou services issus de ces rôles serveur sont exécutés sur le même serveur physique ou sur deux serveurs séparés appelés serveur d'accès au client et serveur de boîtes aux lettres.

Dans ce nouveau modèle, le serveur d’accès au Client est chargé de découverte automatique, Secure Sockets Layer (SSL), l’authentification, la redirection et transmission par proxy. Serveur d’accès Client est le point d’entrée pour tous les appels entrants ou les demandes de protocole SIP (Session Initiation) pour la messagerie unifiée. La logique de routage et de rediriger les SIP est implémenté en tant que service qui est automatiquement inclus sur un serveur d’accès au Client. Ce service est appelé le service Microsoft Exchange Unified Messaging routeur d’appels. Il s’exécute sur chaque serveur d’accès au Client dans votre organisation.

Lorsqu’un serveur d’accès Client reçoit une requête SIP INVITE pour un appel entrant, le service Microsoft Exchange Unified Messaging routeur d’appels redirige l’appel entrant vers le serveur de boîtes aux lettres. Puis un canal multimédia (RTP ou SRTP) est créé entre la VoIP gateway, PBX IP ou session border controller (SBC) et le serveur de boîtes aux lettres qui héberge des boîtes aux lettres de l’utilisateur. Bien que le serveur d’accès au Client joue un redirecteur SIP, il traite uniquement les demandes SIP de passerelles VoIP, PBX IP ou SBCs. Il ne reçoit pas tout le trafic multimédia. Le trafic multimédia qui utilise le protocole RTP ou SRTP est transmis uniquement entre le serveur de boîtes aux lettres et les homologues SIP tels que des passerelles VoIP, PBX IP ou SBCs. Lorsque vous déployez Exchange 2013 et la messagerie unifiée, vous devez configurer vos passerelles VoIP, PBX IP ou SBCs pour pointer vers les serveurs d’accès au Client que vous avez installées de sorte que les appels entrants sont acheminés correctement pour la messagerie unifiée.

Dans Exchange 2013, le serveur de boîtes aux lettres gère les processus de mêmes que le rôle de serveur de messagerie unifiée est gérée dans Exchange 2007 et Exchange 2010. Le serveur de boîtes aux lettres s’exécute le service de messagerie unifiée de Microsoft Exchange et le processus de travail de la messagerie unifiée.

Lorsque vous êtes l’installation de vos serveurs d’accès au Client et boîte aux lettres et le déploiement de la messagerie unifiée, vous n’êtes pas obligé d’associer ou ajout de l’accès des clients ou serveurs de boîtes aux lettres vers la messagerie unifiée des plans de numérotation. Serveurs d’accès au client et boîte aux lettres de répondre à tous les appels entrants, puis utilisent les plans de numérotation de messagerie unifiée pour trouver des utilisateurs.

Toutefois, si vous êtes intégrer la messagerie unifiée Microsoft Office Communications Server 2007 R2 ou Microsoft Lync Server, le SIP et les canaux de médias RTP ou SRTP pour les appels entrants sont gérés par le serveur de boîtes aux lettres et les serveurs Lync. Dans un environnement intégré de Lync, vous ne disposez pas des passerelles VoIP, PBX IP ou SBCs. Lync, le serveur de boîtes aux lettres qui exécute le service de messagerie unifiée Microsoft Exchange ressemble à un serveur de messagerie unifiée Exchange 2010. Le serveur de boîtes aux lettres et le serveur d’accès au Client sont considérés comme des homologues approuvés, car les deux serveurs doivent être ajoutés à un plan de numérotation SIP. Lync achemine l’appel entrant en utilisant le composant de routage entrant, qui utilise le protocole SIP pour communiquer avec le serveur d’accès au Client et puis d’acheminer les appels vers un serveur de boîtes aux lettres.

Retour au début

## Paramètres de configuration du serveur

Dans Exchange 2013, tous les composants de messagerie unifiée et les paramètres de configuration appliquent à un seul ordinateur exécutant le rôle de serveur de messagerie unifiée dans Exchange 2010 sont toujours disponibles. Toutefois, certains de ces composants et les paramètres de configuration se trouvent sur un serveur d’accès au Client et d’autres sont disponibles sur un serveur de boîtes aux lettres. Dans certains cas, le même paramètre est disponible dans les deux. La liste suivante indique les paramètres et les paramètres qui sont disponibles sur un serveur d’accès au Client et un serveur de boîtes aux lettres.

  - \[-DialPlans \<MultiValuedProperty\>\]

  - \[-MaxCallsAllowed \<Int32\>\]

  - \[-SipTcpListeningPort \<Int32\>\]

  - \[-SipTlsListeningPort \<Int32\>\]

  - \[-Status \<Enabled | Disabled | NoNewCalls\>\]

  - \[-UMStartupMode \<TCP | TLS | Dual\>\]

Pour le serveur de boîtes aux lettres, vous allez utiliser les applets de commande **Disable-UMService** , **Get-UMService**, des **Enable-UMService**et **Set-UMService**pour afficher ou configurer les propriétés de messagerie unifiée pour le service de messagerie unifiée Microsoft Exchange. Un ensemble différent d’applets de commande, **Set-UMCallRouterSettings** et **Get-UMCallRouterSettings**, sont utilisés pour afficher ou configurer les propriétés du service Microsoft Exchange Unified Messaging routeur d’appels sur un serveur d’accès au Client. Cela garantit que la existant **Get-UMServer**, **Set-UMServer**, **Enable-UMServer**et **Disable-UMServer** des applets de commande de Exchange 2007 et Exchange 2010 fonctionnera dans un déploiement de la coexistence avec des serveurs de boîtes aux lettres Exchange 2013. Cela garantit également que les applets de commande fonctionneront lorsque les serveurs de boîtes aux lettres et accès au Client sont installés sur les ordinateurs identiques ou différents.

Retour au début

## Fonctionnement du serveur

Lorsque les serveurs d'accès au client et de boîtes aux lettres sont installés, ils sont automatiquement activés pour pouvoir répondre aux appels vocaux entrants et sortants et acheminent les messages vocaux auprès des destinataires appropriés de votre organisation Exchange.

Vous pouvez autoriser le service de messagerie unifiée Microsoft Exchange sur un serveur de boîtes aux lettres ou le service Microsoft Exchange Unified Messaging routeur d’appels sur un serveur d’accès au Client pour répondre aux appels nouvelles ou en empêcher son. Par défaut, un serveur de boîtes aux lettres ou d’accès au Client est dans un état activé après son installation. Lorsque vous configurez le serveur de boîtes aux lettres ou d’accès au Client d’accepter des messages vocaux entrants, télécopie, standard automatique et les appels d’Outlook Voice Access, vous utilisez la cmdlet **Set-ServerComponentState** .

Configuration du Mode de Maintenance pour un serveur de boîtes aux lettres ou d’accès au Client Exchange 2013 permet de prendre le serveur hors service. Pour un serveur de boîtes aux lettres, out-of-service signifie que le serveur ne sont pas héberger les bases de données actives, toutes les files d’attente de transport sont vides, et le serveur n’accepte pas les appels entrants à partir des serveurs d’accès Client, passerelles VoIP, PBX IP, PBX compatible SIP ou SBCs. Pour un serveur d’accès au Client, out-of-service signifie que le serveur n’acceptera tous les appels entrants à partir de passerelles VoIP, PBX IP, PBX compatible SIP ou SBCs.

Exchange 2007 et Exchange 2010, il y avait un paramètre d’état qui peut être utilisé pour contrôler l’état de fonctionnement du serveur de messagerie unifiée. Dans Exchange 2013, aucun paramètre status n’est disponible à cet effet sur l’applet de commande **Set-UMService** pour un serveur de boîtes aux lettres ou de l’applet de commande **Set-UMCallRouterSettings** sur un serveur d’accès au Client.

Bien que les serveurs d'accès au client et de boîtes aux lettres soient définis sur « activé » au moment de leur installation, aucun des serveurs ne peut traiter ni acheminer correctement des appels entrants pour des utilisateurs à extension messagerie unifiée tant qu'un plan de numérotation de messagerie unifiée n'a pas été lié à au moins une passerelle IP de messagerie unifiée.

Après qu’un plan de numérotation est lié à une passerelle IP de messagerie unifiée, les serveurs d’accès au Client et boîte aux lettres localiser toutes les passerelles IP de messagerie unifiée associés avec les passerelles, PBX IP et SBC plan de numérotation de messagerie unifiée et VoIP. Pour détecter et identifier les éventuelles modifications de configuration sur plans de numérotation de MU ou des passerelles IP de MU, les serveurs d’accès au Client ou de boîtes aux lettres vérifient la configuration toutes les 10 minutes.

Si la passerelle IP de messagerie unifiée identifie des modifications apportées à la configuration, le serveur de boîte aux lettres ou d’accès au Client réagit en conséquence et commence à utiliser ou s’arrête à l’aide de la passerelle VoIP appropriée, IP PBX ou SBC. Une fois que les serveurs d’accès au Client et boîte aux lettres répondre entrant appels pour les utilisateurs qui sont liées à un plan de numérotation de messagerie unifiée et ils communiquent correctement avec des passerelles VoIP, PBX IP et SBC, vous pouvez exécuter un ensemble d’opérations de diagnostics pour vérifier qu’ils fonctionnent correctement et que la connectivité entre les passerelles les serveurs Exchange et VoIP, PBX IP ou SBCs fonctionne correctement.

Retour au début

