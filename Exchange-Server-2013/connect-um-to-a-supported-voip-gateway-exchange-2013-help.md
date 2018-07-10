---
title: 'Connecter la messagerie unifiée à une passerelle VoIP pris en charge: Exchange 2013 Help'
TOCTitle: Connecter la messagerie unifiée à une passerelle VoIP pris en charge
ms:assetid: b8dfc8bd-2ee5-418d-b0a4-4fa2ec7e2a2e
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb124360(v=EXCHG.150)
ms:contentKeyID: 50555472
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Connecter la messagerie unifiée à une passerelle VoIP pris en charge

 

_**Sapplique à :** Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2013-04-19_

Lorsque vous installez une messagerie unifiée, vous devez configurer les passerelles VoIP (Voice over IP), les PBX IP, les PBX compatibles SIP ou les contrôleurs de frontière de session (SBC) sur votre réseau pour communiquer avec les serveurs d'accès au client qui exécutent le service routeur des appels de messagerie unifiée Microsoft Exchange et les serveurs de boîtes aux lettres qui exécutent le service de messagerie unifiée de votre organisation Exchange. Vous devez également configurer des serveurs d'accès au client et de boîtes aux lettres pour communiquer avec des passerelles VoIP, des PBX IP, des PBX compatibles SIP ou des contrôleurs de frontière de session (SBC).

> [!NOTE]
> Après avoir connecté vos serveurs d'accès au client et de boîtes aux lettres aux passerelles VoIP, PBX IP, PBX compatibles SIP ou contrôleurs de frontière de session (SBC) sur votre réseau de données, vous devez créer les composants de messagerie unifiée requis et activer la messagerie unifiée pour les utilisateurs pour qu'ils puissent utiliser le système de messagerie vocale.


## Étapes

Voici les étapes de base pour connecter des passerelles VoIP, PBX IP, PBX compatibles SIP ou contrôleurs de frontière de session (SBC) à des serveurs d'accès au client et de boîtes aux lettres :

Étape 1 : Installer les serveurs d'accès au client et de boîtes aux lettres dans votre organisation.

Étape 2 : Créer et configurer un plan de numérotation de messagerie unifiée de type numéro de poste, URI SIP ou E.164.

Étape 3 : Créez et configurez une passerelle IP de messagerie unifiée. Vous devez créer et configurer une passerelle IP de messagerie unifiée pour chaque passerelle VoIP, PBX IP, PBX compatible SIP ou contrôleur de frontière de session (SBC) qui doit accepter des appels entrants ou envoyer des appels sortants.

Étape 4 : Créer un groupement de postes de messagerie unifiée, si nécessaire. Si vous créez une passerelle IP de messagerie unifiée sans spécifier de plan de numérotation de messagerie unifiée, un groupement de postes de messagerie unifiée est alors créé automatiquement.

Consultez les sections suivantes pour obtenir plus d'informations sur chaque étape.

## Étape 1 : Installer vos serveurs d'accès au client et de boîtes aux lettres

Lorsque vous déployez des serveurs Exchange dans votre organisation, vous pouvez installer les serveurs d'accès au client et de boîtes aux lettres sur le même ordinateur ou installer le serveur d'accès au client sur un ordinateur distinct à partir du serveur de boîtes aux lettres. Pour installer le serveur d'accès au client, exécutez Setup.exe à partir du support d'installation. Utilisez la même commande que vous installiez le serveur d'accès au client sur un ordinateur distinct à partir du serveur de boîtes aux lettres ou sur le même ordinateur. Pour plus d'informations, consultez la rubrique [Installer Exchange 2013 à l’aide de l’Assistant Installation](install-exchange-2013-using-the-setup-wizard-exchange-2013-help.md). Pour ajouter des fonctionnalités à votre serveur Exchange actuel, utilisez **Programmes et fonctionnalités** ou Setup.exe.

## Étape 2 : Créer et configurer un plan de numérotation de messagerie unifiée

Après avoir installé les serveurs requis, vous devez commencer par créer un plan de numérotation de messagerie unifiée. Un plan de numérotation de messagerie unifiée contient les paramètres de configuration permettant de se connecter à votre réseau de téléphonie au moyen d'une liaison à une ou plusieurs passerelles IP de messagerie unifiée. Une passerelle IP de messagerie unifiée et un groupement de postes de messagerie unifiée sont directement liés à un plan de numérotation de messagerie unifiée et sont également requis. Pour plus d'informations, consultez la rubrique [Créer un plan de numérotation de messagerie unifiée](create-a-um-dial-plan-exchange-2013-help.md).

Un plan de numérotation de messagerie unifiée établit une liaison entre le numéro de poste téléphonique d'un utilisateur et sa boîte aux lettres à extension messagerie unifiée. Lorsque vous créez un plan de numérotation de messagerie unifiée, vous pouvez configurer le nombre de chiffres composant les numéros de postes, le type d'URI (Uniform Resource Identifier) et les paramètres de sécurité VoIP pour le plan de numérotation.

Il existe trois types de plan de numérotation : numéro de poste, URI SIP (Session Initiation Protocol) et E.164. Lorsque vous créez et configurez un plan de numérotation de messagerie unifiée, vous devez déterminer le type d'information qui est envoyé à partir de votre PBX IP, PBX compatible SIP ou PBX, et si les appels doivent être envoyés sur un serveur d'accès au client ou de boîtes aux lettres au format numéro de poste ou E.164. Si vous déployez Microsoft Office Communications Server 2007 R2 ou Microsoft Lync Server, vous devez créer et configurer un plan de numérotation URI SIP.

## Étape 3 : Créer et configurer une passerelle IP de messagerie unifiée

Après avoir créé un plan de numérotation de messagerie unifiée, vous devez créer une passerelle IP de messagerie unifiée pour représenter chaque passerelle VoIP, PBX IP ou contrôleur de frontière de session (SBC) de votre réseau. Lorsque vous créez une passerelle IP de messagerie unifiée, vous pouvez la configurer pour utiliser une adresse IP ou un nom de domaine complet. Si vous utilisez un nom de domaine complet, vous devez configurer correctement un enregistrement d'hôte DNS pour la passerelle IP afin de résoudre correctement le nom d'hôte en adresse IP.

L'installation de la passerelle VoIP, du PBX IP ou du contrôleur de frontière de session (SBC) doit être suivie de la création d'une passerelle IP de messagerie unifiée représentant le périphérique matériel physique. Après la création de la passerelle IP de messagerie unifiée, le serveur d'accès au client qui utilise la passerelle IP de messagerie unifiée doit envoyer une requête SIP OPTIONS à la passerelle VoIP, au PBX IP ou au contrôleur de frontière de session (SBC) pour s'assurer qu'ils répondent. Si la passerelle VoIP, le PBX IP, le PBX compatibles SIP ou le contrôleur de frontière de session (SBC) ne répond pas, le serveur d'accès au client consigne un événement avec l'ID 1088 dans le journal, en indiquant que la demande a échoué. Pour résoudre ce problème, vérifiez que la passerelle VoIP, le PBX IP ou le contrôleur de frontière de session (SBC) est accessible et en ligne et que la configuration de la messagerie unifiée est correcte.

Les serveurs d'accès au client et de boîtes aux lettres ne doivent communiquer qu'avec une passerelle VoIP, un PBX IP ou un contrôleur de frontière de session (SBC) répertorié(e) en tant qu'homologue SIP (Session Initiation Protocol) approuvé. Dans certains cas, si deux passerelles VoIP, PBX IP ou SBC sont configurés pour utiliser la même adresse IP, un événement avec l'ID 1175 sera journalisé. Cet événement peut se produire si vous avez configuré vos zones DNS avec des noms de domaine complets pour les passerelles VoIP de votre réseau. La messagerie unifiée protège contre les demandes non autorisées en récupérant l'URL interne du répertoire virtuel des services web de messagerie unifiée situé sur le serveur de boîtes aux lettres et utilise ensuite l'URL pour construire la liste des noms de domaines complets pour les homologues SIP approuvés. Lorsque deux noms de domaine complets correspondent à même adresse IP, cet événement est alors journalisé.

Vous devez redémarrer le service de messagerie unifiée MicrosoftExchange si une passerelle IP de messagerie unifiée est configurée pour utiliser un nom de domaine complet et si l'enregistrement DNS de la passerelle IP de messagerie unifiée est modifié après que le service a démarré. Si vous ne redémarrez pas le service, le serveur de boîtes aux lettres n'est pas en mesure de localiser la passerelle IP de messagerie unifiée. Cela est dû au fait qu'un serveur de boîtes aux lettres gère un cache pour toutes les passerelles IP de messagerie unifiée en mémoire et que la résolution DNS ne s'effectue qu'en cas de redémarrage du service ou de modification de la configuration d'une passerelle VoIP, d'un PBX IP et d'un contrôleur de frontière de session (SBC).

La messagerie unifiée Exchange prend en charge différents fournisseurs de passerelles VoIP et d'autres fournisseurs de PBX IP, de PBX compatibles SIP et de contrôleurs de frontière de session (SBC). Chacune des passerelles VoIP prises en charge est conçue pour se connecter à différents systèmes PBX tiers.

Pour plus d'informations sur les passerelles VoIP, consultez les rubriques suivantes :

  - [Créer une passerelle IP de messagerie unifiée](create-a-um-ip-gateway-exchange-2013-help.md)

  - [Notes de configuration pour les passerelles VoIP, les PBX IP et les PBX pris en charge](configuration-notes-for-supported-voip-gateways-ip-pbxs-and-pbxs-exchange-2013-help.md)

  - [Connexion d’une passerelle VoIP, d’un IP PBX ou d’un contrôleur SBC à la messagerie unifiée](connect-a-voip-gateway-ip-pbx-or-session-border-controller-to-um-exchange-2013-help.md)

Pour plus d'informations, consultez la rubrique [Connexion de votre système de messagerie vocale à votre réseau téléphonique](connect-your-voice-mail-system-to-your-telephone-network-exchange-2013-help.md).

## Étape 4 : Créer un groupement de postes de messagerie unifiée (si nécessaire)

Le terme groupement de postes est utilisé pour décrire un groupe de numéros de poste PBX (Private Branch eXchange) ou PBX IP étant partagés par des utilisateurs. Les groupements de postes servent à répartir efficacement les appels au sein de ou en dehors d'une unité de gestion spécifique. La création et la définition d'un groupement de postes réduisent le risque qu'un appelant qui passe un appel entrant reçoive une tonalité d'occupation lors de la réception de l'appel.

Les groupements de postes de messagerie unifiée reflètent en tout point les groupements de postes utilisés sur des PBX et des PBX IP. Lorsque vous configurez vos PBX et PBX IP, vous devez créer et configurer un ou plusieurs groupements de postes de messagerie unifiée. Les groupements de postes de messagerie unifiée agissent comme un lien entre la passerelle IP de messagerie unifiée et le plan de numérotation de messagerie unifiée.

Selon la manière dont vous créez votre passerelle IP de messagerie unifiée, vous devez peut-être créer un ou plusieurs groupements de postes de messagerie unifiée. Si vous ne liez pas de passerelle IP de messagerie unifiée à un plan de numérotation lors de la création d'une passerelle IP de messagerie unifiée, un groupement de postes de messagerie unifiée unique est alors créé par défaut. Si vous liez une passerelle IP de messagerie unifiée à un plan de numérotation de messagerie unifiée lorsque vous créez une passerelle IP de messagerie unifiée, tous les appels entrants sont envoyés par le biais de la passerelle IP de messagerie unifiée et ces appels sont acceptés par des serveurs d'accès au client et de boîtes aux lettres. Si vous ne liez pas de passerelle IP de messagerie unifiée à un plan de numérotation de messagerie unifiée lors de la création d'une passerelle IP de messagerie unifiée, vous devez créer un groupement de postes de messagerie unifiée avec l'identificateur de pilote approprié pour que les appels entrants puissent être transmis de la passerelle IP de messagerie unifiée à un plan de numérotation.

Si vous disposez de plusieurs numéros Outlook Voice Access et de standard automatique et avez lié une passerelle IP de messagerie unifiée à un plan de numérotation, vous devez supprimer le groupement de postes de messagerie unifiée créé par défaut, puis créer plusieurs groupements de postes de messagerie unifiée. Pour plus d'informations sur la création d'un groupement de postes de messagerie unifiée, consultez la rubrique [Créer un groupement de postes de messagerie unifiée](create-a-um-hunt-group-exchange-2013-help.md).

