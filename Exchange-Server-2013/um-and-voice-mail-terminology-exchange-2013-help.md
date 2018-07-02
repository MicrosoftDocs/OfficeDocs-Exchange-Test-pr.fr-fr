---
title: 'Terminologie de la messagerie unifiée et de la messagerie vocale: Exchange 2013 Help'
TOCTitle: Terminologie de la messagerie unifiée et de la messagerie vocale
ms:assetid: 3a6d93f2-1802-4aed-8b83-35c7fd004d0c
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Ee633462(v=EXCHG.150)
ms:contentKeyID: 54652727
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Terminologie de la messagerie unifiée et de la messagerie vocale

 

_**Sapplique à :**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :**2013-04-22_

Cette rubrique contient des termes et définitions utilisés en relation avec la messagerie unifiée.

  - Codec audio  
    Codage numérique d'un signal vocal analogique. La plupart des codecs audio effectuent une compression des données, au détriment d'une perte de fidélité lors de la récupération de ces dernières. Les différences entre les codecs audio relèvent de la qualité de son perçue, de la bande passante requise pour les utiliser et de la configuration système requise pour l'encodage.

<!-- end list -->

  - Notes audio  
    Il est possible d'ajouter des notes écrites à des messages vocaux reçus dans Outlook ou Outlook Web App.

<!-- end list -->

  - Standard automatique  
    Système logiciel qui répond aux appels, lit des invites ou des instructions, et recueille les entrées par tonalités ou vocales de l'appelant. Les standards automatiques peuvent transférer des appels vers des numéros de téléphone, des utilisateurs désignés ou des entités (par exemple, un département au sein d'une entreprise) spécifiés par l'appelant, sans intervention d'un standardiste humain.

<!-- end list -->

  - Reconnaissance vocale (ASR)  
    Technologie permettant à un ordinateur de transcrire la parole humaine en un ensemble prédéfini de mots ou de phrases.

<!-- end list -->

  - Répondeur automatique  
    Système permettant à un appelant d'interagir avec un système de messagerie vocale en cas d'absence de réponse du numéro appelé à l'origine. Le système diffuse généralement un message d'accueil ou un une invite, et permet à l'appelant d'enregistrer un message vocal.

<!-- end list -->

  - Règles de répondeur automatique  
    Forme de répondeur automatique permettant à l'utilisateur de ce service de spécifier des règles de comportement vis-à-vis des appelants. L'utilisateur peut définir des conditions à évaluer, des messages d'accueil, des choix à proposer à l'appelant et des actions (par exemple, transfert d'appel ou dépôt d'un message) à effectuer à la suite du choix de l'appelant.

<!-- end list -->

  - Réseau à commutation de circuits  
    Réseau dans lequel existe une connexion dédiée. Une connexion dédiée est un circuit ou un canal installé entre deux nœuds afin de leur permettre de communiquer.

<!-- end list -->

  - Transfert d'appel conditionnel  
    Ensemble de conditions choisies par un utilisateur, applicables à la réception d'appels entrants. Ces derniers sont redirigés en fonction des conditions définies.

<!-- end list -->

  - Numérotation par nom  
    Fonctionnalité permettant à un appelant d'épeler le nom d'une personne à l'aide des touches d'un téléphone (ABC=2, DEF=3, etc.).

<!-- end list -->

  - Plan de numérotation  
    Pour la messagerie unifiée, il s'agit d'un ensemble de points de terminaison compatibles avec la téléphonie, qui partagent un plan de numérotation commun. Les détails du plan sont déterminés par le système téléphonique auquel la messagerie unifiée est connectée. Dans le cas le plus simple, il peut s'agir d'un autocommutateur privé (PBX) dont les différents postes disposent chacun d'un numéro unique et de longueur fixe.

<!-- end list -->

  - Groupe de règles de numérotation  
    Des groupes de règles de numérotation sont créés pour permettre la modification de numéros de téléphone avant leur envoi à un PBX compatible SIP ou à un PBX IP pour les appels sortants. Les groupes de règles de numérotation peuvent supprimer ou ajouter des chiffres aux numéros de téléphone qu'un serveur de messagerie unifiée utilise pour passer des appels.
    
    Chaque groupe de règles de numérotation contient des entrées de règle de numérotation qui déterminent les types d'appels nationaux/régionaux et internationaux que les utilisateurs faisant partie de ce groupe peuvent passer. Chaque groupe de règles de numérotation doit contenir au moins une entrée de règle de numérotation.

<!-- end list -->

  - Partenaire de télécopie  
    Les partenaires de télécopie d'une messagerie unifiée fournissent des applications ou des services capables d'accepter des appels transférés par la messagerie unifiée en cas de détection d'une tonalité de télécopie. Le produit ou service du partenaire reçoit alors les données de télécopie, puis crée un message et remet ce dernier à l'utilisateur à extension messagerie unifiée sous la forme d'un message électronique contenant une pièce jointe au format .tif. Ce type de message apparaît dans le dossier de recherche de télécopie d'Outlook et d'Outlook Web App.

<!-- end list -->

  - Groupement de postes  
    Ensemble de postes organisés en un groupe sur lequel un autocommutateur privé (PBX) classique, IP ou compatible SIP recherche un poste disponible. Un groupement de postes permet de diriger les appels vers des points de terminaison de même capacité ou vers une application telle qu'une messagerie vocale.

<!-- end list -->

  - Format de numéro national/régional  
    Le format de numéro national/régional spécifie la manière dont le numéro de téléphone d'un utilisateur doit être composé par la messagerie unifiée à partir d'un plan de numérotation vers un autre dont le code de pays est identique. Cette information est utilisée par un standard automatique et quand un utilisateur de Outlook Voice Access recherche l'utilisateur dans l'annuaire et tente de l'appeler.
    
    Cette entrée se compose d'un préfixe et d'un nombre variable de caractères (par exemple, 020xxxxxxx).

<!-- end list -->

  - Message d'information automatique  
    Message audio diffusé quand un appelant appelle pour la première fois un système de messagerie vocale. Ce message peut fournir des informations intéressantes.

<!-- end list -->

  - Code d'accès à l'international  
    Préfixe utilisé pour diriger un appel vers l'international. Le code d'accès à l'international est 011 aux États-Unis et 00 dans la plupart des autres pays.

<!-- end list -->

  - Format du numéro de téléphone international  
    Chaîne de chiffres utilisée pour définir la procédure d'appel à une personne située hors d'un pays donné.

<!-- end list -->

  - Autocommutateur privé avec protocole Internet (PBX IP)  
    Commutateur téléphonique prenant en charge la voix sur IP (VoIP) en mode natif. Un PBX IP utilise des protocoles VoIP pour communiquer avec des hôtes IP tels que des téléphones VoIP via un réseau à commutation par paquets. Certains PBX IP prennent également en charge les téléphones analogiques et numériques classiques.

<!-- end list -->

  - Méthode de sélection d'un nom correspondant  
    Mécanisme permettant à un appelant de différencier les utilisateurs dont les noms correspondent aux entrées par tonalité ou vocales.

<!-- end list -->

  - Indicateur de message en attente  
    Signal indiquant la présence d'un ou plusieurs messages vocaux non lus. Dans les systèmes de messagerie vocale, il s'agit fréquemment d'un voyant allumé sur le téléphone ou d'une tonalité cadencée.

<!-- end list -->

  - Service routeur de messagerie unifiée Microsoft Exchange  
    Service acheminant les appels entrants d'utilisateurs à extension messagerie unifiée vers le service de messagerie unifiée Microsoft Exchange.

<!-- end list -->

  - Service de messagerie unifiée Microsoft Exchange  
    Service implémentant les fonctionnalités de messagerie unifiée pour les utilisateurs à extension messagerie unifiée.

<!-- end list -->

  - Notification d'appel en absence  
    Message électronique envoyé à un utilisateur à extension messagerie unifiée, indiquant que quelque a appelé sans laisser de message vocal.

<!-- end list -->

  - Préfixe du numéro national  
    Préfixe utilisé pour diriger un appel comme un appel national. Aux États-Unis, ce préfixe est 1. En France, comme dans la plupart des autres pays du monde, ce préfixe est 0.

<!-- end list -->

  - Masque de numéro  
    Ensemble de numéros et de caractères génériques utilisés pour déterminer le numéro de téléphone que le serveur de boîtes aux lettres doit appeler. Un « X » représente un chiffre unique (0 à 9). Un astérisque (\*) représente une combinaison quelconque de tels chiffres.

<!-- end list -->

  - Extension numérique  
    Chaîne de chiffres ne contenant pas de signe « + » ou de code de pays/région. Dans les plans de numérotation, les extensions doivent avoir une longueur spécifiée.

<!-- end list -->

  - Automate d'appels  
    Processus par lequel la messagerie unifiée compose ou transfère des appels. La messagerie unifiée reçoit généralement des appels, mais en passe également parfois. Par exemple, l'automate d'appels intervient quand un standard automatique de messagerie unifiée transfère un appel au poste d'un utilisateur, ou quand un utilisateur à extension messagerie unifiée utilise la fonction Émettre au téléphone d'Outlook.

<!-- end list -->

  - Outlook Voice Access  
    Série d'invites vocales qui permettent à des appelants authentifiés d'accéder à leurs messageries électroniques et vocales, calendriers et informations de contact à l'aide d'un téléphone analogique, numérique ou mobile. Outlook Voice Access permet également aux appelants authentifiés de parcourir leurs informations personnelles dans leurs boîtes aux lettres, de passer des appels, de localiser des utilisateurs, et de naviguer dans les menus et invites du système en utilisant des entrées DTMF (à tonalités) ou vocales.

<!-- end list -->

  - Code d'accès à une ligne extérieure  
    Préfixe utilisé par un messagerie unifiée (ou une personne utilisant un poste externe sur le PBX ou PBX IP) pour accéder à une ligne extérieure. Ce préfixe est généralement 9.

<!-- end list -->

  - Commutation de paquets  
    Technique consistant à diviser un message de données en unités plus petites appelées paquets. Les paquets sont envoyés à leur destination par la meilleure route disponible, puis réassemblés côté réception.

<!-- end list -->

  - Identificateur pilote  
    Numéro de téléphone pointant vers un groupement de postes, servant de numéro d'accès pour les appels routés vers une messagerie unifiée. Parfois appelé numéro pilote.

<!-- end list -->

  - Code confidentiel  
    Code secret qu'un utilisateur compose sur son téléphone pour accéder à sa boîte aux lettres.

<!-- end list -->

  - Émettre au téléphone  
    Fonctionnalité de messagerie unifiée que les utilisateurs peuvent utiliser à partir d'un téléphone pour lire leurs messages vocaux, ou lire et enregistrer leurs messages d'accueil vocaux personnalisés.

<!-- end list -->

  - Autocommutateur privé (PBX)  
    Réseau téléphonique privé dans une organisation. Les numéros de téléphone ou de poste sont pris en charge, et les appels sont automatiquement routés vers ces derniers. Les utilisateurs peuvent s'appeler par leurs numéros de poste, même entre emplacements distribués.

<!-- end list -->

  - Invite  
    Message audio lu au téléphone pour expliquer les options valides aux utilisateurs.

<!-- end list -->

  - Messagerie vocale protégée  
    Fonctionnalité de messagerie unifiée utilisant la gestion des droits relatifs à l'information pour chiffrer le contenu des messages vocaux et spécifier les opérations autorisées sur ces derniers. La protection peut être activée par l'appelant (en marquant le message comme confidentiel) ou par une stratégie du système.

<!-- end list -->

  - Réseau téléphonique commuté (PSTN)  
    PSTN est le regroupement mondial des réseaux téléphoniques publics à commutation de circuits. Ce regroupement est similaire à Internet, en tant que regroupement mondial de réseaux publics à commutation par paquets basés sur le protocole IP.

<!-- end list -->

  - Réinitialiser  
    Quand un code confidentiel ou un mot de passe est réinitialisé, un nouveau code confidentiel ou mot de passe temporaire est choisi de manière aléatoire par le système. L'utilisateur devra changer le code confidentiel temporaire lors de sa prochaine connexion à Outlook Voice Access.

<!-- end list -->

  - Recherche de numéro inversée (RNL)  
    Méthode utilisée pour essayer de trouver le nom d'une personne, à partir d'un annuaire ou d'une banque d'informations, sur la base d'un numéro de téléphone.

<!-- end list -->

  - Codec RTAudio  
    Codec vocal avancé conçu pour des applications VoIP bidirectionnelles en temps réel telles que les jeux, l'audioconférence et les applications sans fil sur IP. RTAudio est le codec audio favori de Microsoft, et le codec par défaut pour les plateformes Microsoft Lync Server.

<!-- end list -->

  - PBX compatible SIP  
    Un PBX compatible SIP est un appareil téléphonique qui agit comme un commutateur réseau pour la commutation des appels au sein d'un réseau téléphonique ou d'un réseau à commutation de circuits. Un PBX compatible SIP diffère toutefois d'un PBX classique en ce qu'il peut se connecter à Internet et utiliser le protocole SIP pour passer des appels sur ce réseau.

<!-- end list -->

  - Notification SIP  
    Une notification SIP est un message SIP envoyé par un homologue SIP à un autre pour l'informer d'un changement.

<!-- end list -->

  - Homologue SIP  
    Appareil compatible SIP permettant d'établir des communications téléphoniques entre une passerelle VoIP, un PBX IP, un PBX compatible SIP, des serveurs Microsoft Lync, des téléphones VoIP et des services de messagerie unifiée.

<!-- end list -->

  - Sortie par étoile  
    Action qu'un appelant peut exécuter après s'être connecté à un standard automatique de messagerie unifiée pour accéder à Outlook Voice Access afin de relever ses messages électroniques et vocaux. À cette fin, il appuie sur la touche étoile (\*) durant la lecture des invites du standard automatique.

<!-- end list -->

  - Numéro d'accès d'abonné (numéro Outlook Voice Access)  
    Numéro configuré dans un PBX classique, IP ou compatible SIP, et sur un plan de numérotation de messagerie unifiée, qui permet aux utilisateurs d'accéder à leur boîte aux lettres à l'aide d'Outlook Voice Access. Dans certains cas, ce peut être le numéro d'accès d'abonné ou le numéro pilote (également appelé Identificateur pilote) sur le PBX classique, IP ou compatible SIP, et le groupement de postes de messagerie unifiée.

<!-- end list -->

  - Invite du système  
    Bref enregistrement audio pour la messagerie unifiée, que le serveur diffuse aux appelants. Des invites système souhaitent la bienvenue aux appelants, et les informent concernant les options à leur disposition dans le système de messagerie vocale.

<!-- end list -->

  - Interface utilisateur de téléphonie (TUI)  
    Interface permettant de naviguer dans les menus d'un système de messagerie vocale à l'aide d'entrées DTMF (à tonalités).

<!-- end list -->

  - Conversion de texte par synthèse vocale (TTS)  
    Technologies de traduction ou de conversion de texte écrit en texte vocal.

<!-- end list -->

  - Passerelle IP de messagerie unifiée  
    (Voir Passerelle IP). Une passerelle IP de messagerie unifiée est la représentation de messagerie unifiée Exchange de tout homologue SIP avec lequel il est possible de communiquer à l'aide de protocoles VoIP. Elle peut représenter un appareil capable de s'interfacer avec un PBX classique, IP ou compatible SIP, ou avec un serveur Microsoft Lync Server.

<!-- end list -->

  - Processus de travail de messagerie unifiée  
    Processus créé au démarrage du service de messagerie unifiée Microsoft Exchange. Lorsque le service de messagerie unifiée reçoit une demande de traitement d'un appel entrant, il la redirige immédiatement vers un processus de travail de messagerie unifiée qui assure ensuite toutes les interactions avec l'appelant.

<!-- end list -->

  - Gestionnaire du processus de travail de messagerie unifiée  
    Composant gérant la création et la surveillance de tous les processus de travail de messagerie unifiée créés.

<!-- end list -->

  - Messagerie unifiée  
    Application qui consolide la messagerie vocale et électronique d'un utilisateur dans une seule boîte aux lettres, de manière à ce que ce dernier puisse relever ses messages de tous types dans un emplacement unique. Le serveur de messagerie est utilisé comme plateforme pour tous les types de message, ce qui rend inutile la maintenance d'infrastructures séparées de messagerie vocale et de messagerie électronique.

<!-- end list -->

  - Messagerie vocale  
    Système qui enregistre et stocke les messages téléphoniques dans une boîte aux lettres utilisateur.

<!-- end list -->

  - Aperçu de messagerie vocale  
    Fonctionnalité permettant d'afficher le texte transcrit d'un enregistrement audio lors de la remise d'un message vocal.

<!-- end list -->

  - Message vocal  
    Message électronique contenant principalement de l'audio numérisé.

<!-- end list -->

  - Voix sur IP (VoIP)  
    Pratique consistant à utiliser un réseau de données IP pour transmettre des appels vocaux.

<!-- end list -->

  - Interface utilisateur vocale (VUI)  
    Interface permettant de naviguer dans les menus d'un système de messagerie vocale à l'aide d'entrées vocales.

<!-- end list -->

  - Passerelle VoIP
    
    1.  Périphérique matériel ou produit tiers qui connecte un PBX hérité à un réseau local. Une passerelle VolP traduit ou convertit des protocoles TDM ou basés sur la commutation de circuits téléphoniques en protocoles de commutation par paquets utilisables sur un réseau VolP.
    
    2.  Représentation par la messagerie unifiée Exchange d'un homologue SIP avec lequel il est possible de communiquer via des protocoles VoIP. Elle peut représenter un appareil capable de s'interfacer avec un PBX hérité ou IP, ou avec un serveur Microsoft Lync Server.

<!-- end list -->

  - Message d'accueil  
    Message diffusé quand un appelant externe se connecte à un standard automatique de messagerie unifiée ou quand un utilisateur d'Outlook Voice Access ou un autre appelant compose un numéro d'accès d'abonné configuré sur un plan de numérotation de messagerie unifiée. Le client peut modifier le message d'accueil par défaut pour l'adapter à une organisation ou à un emplacement spécifiques.

