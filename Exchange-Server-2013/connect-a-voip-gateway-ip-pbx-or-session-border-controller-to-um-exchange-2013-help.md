---
title: 'Connexion d’une passerelle VoIP, d’un IP PBX ou d’un contrôleur SBC à la MU'
TOCTitle: Connexion d’une passerelle VoIP, d’un IP PBX ou d’un contrôleur SBC à la messagerie unifiée
ms:assetid: a7cecf59-b93a-413b-bb88-29f2669ef2cf
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb124084(v=EXCHG.150)
ms:contentKeyID: 50555467
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Connexion d’une passerelle VoIP, d’un IP PBX ou d’un contrôleur SBC à la messagerie unifiée

 

_**Sapplique à :** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2016-12-09_

Vous devez configurer correctement les passerelles VoIP et les autocommutateurs privés (PBX) lorsque vous déployez la messagerie unifiée dans votre organisation. Si vous déployez la messagerie unifiée dans un environnement hybride, vous devrez également configurer correctement vos contrôleurs de frontière de session. Pour ce faire, vous devez configurer l’interface ou les interfaces des passerelles VoIP, les autocommutateurs privés IP et les contrôleurs de frontière de session que vous utilisez pour communiquer avec les serveurs d’accès au client qui exécutent le service de routage des appels de la messagerie unifiée de Microsoft Exchange et avec les serveurs de boîtes aux lettres qui exécutent le service de messagerie unifiée de Microsoft Exchange.

> [!IMPORTANT]
> Lorsque vous exécutez des tâches administratives sur une passerelle VoIP, un PBX IP ou un contrôleur de frontière de session à l’aide d’un navigateur web, les requêtes HTTP envoyées sur le réseau ne sont pas chiffrées. Pour augmenter le niveau de sécurité des passerelles VoIP, des PBX IP ou des contrôleurs de frontière de session sur votre réseau, utilisez le protocole IPsec (Internet Protocol security) ou SSL (Secure Sockets Layer) pour protéger les informations d’identification et données d’administration transmises sur le réseau. Il est également recommandé d’utiliser un mécanisme d’authentification efficace et des mots de passe administrateur complexes afin de protéger les informations d’identification d’administration du périphérique.


## Interfaces d’appareils de téléphonie IP

Il existe plusieurs types de ports ou d’interfaces que vous devez configurer pour activer les communications entre un PBX, une passerelle VoIP, un PBX IP ou un contrôleur de frontière de session (SBC) et les serveurs d’accès au client ou de boîtes à lettres de votre réseau. Lorsque vous configurez une passerelle VoIP, un PBX IP ou un contrôleur de frontière de session (SBC), vous devez tenir compte du fait que l’appareil peut être analogique, numérique ou les deux.

Si l’interface de la passerelle VoIP qui se connecte à un PBX est analogique, vous devez configurer correctement les paramètres adéquats pour permettre à la passerelle VoIP de communiquer avec vos serveurs d’accès au client et de boîtes aux lettres. Pour les PBX IP et contrôleurs de frontière de session (SBC), vous devez également configurer correctement les interfaces IP pour permettre à ces appareils de communiquer avec des serveurs d’accès au client et de boîtes aux lettres. Les types de connexions ou de ports de tous ces appareils sont différents et sont accessibles selon le modèle d’appareil et le fournisseur.

Pour permettre les communications avec des serveurs d’accès au client et de boîtes aux lettres sur votre réseau, procédez comme suit :

  - Pour les passerelles VoIP, vous devez configurer les interfaces de téléphonie pour communiquer avec vos PBX, et vous devez configurer l’interface IP pour l’appareil.

  - Pour les PBX IP, vous devez configurer les connexions basées sur les circuits et le réseau ou basées sur IP.

  - Pour les contrôleurs de frontière de session (SBC), vous devez configurer les deux interfaces IP, une pour votre réseau et l’autre qui se connecte via Internet ou une connexion de réseau étendu (WAN) dédiée.

Voici la liste des ressources trouvées sur Exchange TechCenter qui fournissent des informations vous permettant de configurer correctement vos passerelles VoIP, PBX IP et contrôleurs de frontière de session (SBC) :

  - **Documentation sur la passerelle IP, le PBX IP et le PBX pris en charge**   [Gestionnaire de téléphonie pour Exchange 2013](https://docs.microsoft.com/fr-fr/exchange/voice-mail-unified-messaging/telephone-system-integration-with-um/telephony-advisor-for-exchange-2013) inclut des fichiers de configuration et des informations d’installation que vous pouvez utiliser lors de la configuration des passerelles VoIP, des PBX IP et des contrôleurs de frontière de session.

  - **Notes de configuration et techniques**   [Notes de configuration pour les passerelles VoIP, les PBX IP et les PBX pris en charge](https://docs.microsoft.com/fr-fr/exchange/voice-mail-unified-messaging/telephone-system-integration-with-um/configuration-notes-for-voip-gateways) inclut des fichiers de configuration et des informations d’installation que vous pouvez utiliser lors de la configuration des passerelles VoIP, des PBX IP et des PBX.

  - **Notes de configuration pour la messagerie unifiée Exchange en ligne** [Notes de configuration pour les contrôleurs de frontière de session pris en charge](https://docs.microsoft.com/fr-fr/exchange/voice-mail-unified-messaging/telephone-system-integration-with-um/configuration-notes-for-session-border-controllers) inclut des fichiers de configuration et des informations d’installation que vous pouvez utiliser lors de la configuration des contrôleurs de frontière de session.   

Des spécialistes de la messagerie unifiée sont prêts à vous assister dans la configuration de vos appareils de téléphonie et de réseau basés sur IP. Un spécialiste de messagerie unifiée peut vous aider à vous assurer que la mise à niveau vers la messagerie unifiée à partir d’un système de messagerie vocale hérité ou tiers soit effectuée en douceur, et il vous aidera à planifier et à déployer un nouveau système de messagerie vocale grâce à la messagerie unifiée d’Exchange. Le déploiement d’un nouveau système de messagerie vocale ou la mise à niveau d’un système de messagerie vocale hérité nécessite une très bonne connaissance des passerelles VoIP, des IP PBX et de la messagerie unifiée. Pour plus d’informations sur la manière de contacter un spécialiste de la messagerie unifiée, consultez [Microsoft Exchange Server 2013 Unified Messaging (UM) Specialists](http://go.microsoft.com/fwlink/p/?linkid=262708) ou les partenaires de messagerie unifiée agréés dans [Microsoft Pinpoint](https://go.microsoft.com/fwlink/p/?linkid=261951).

Après avoir configuré une passerelle VoIP, un PBX IP ou une interface IP de contrôleur de frontière de session (SBC), vous devez créer une passerelle IP de messagerie unifiée pour représenter chacun des appareils que vous avez déployés. Pour plus d’informations sur la création d’une passerelle IP de messagerie unifiée, consultez la rubrique [Créer une passerelle IP de messagerie unifiée](https://docs.microsoft.com/fr-fr/exchange/voice-mail-unified-messaging/connect-voice-mail-system/create-um-ip-gateway).

Une fois que vous avez créé une passerelle IP de messagerie unifiée, les serveurs d’accès au client et de boîtes aux lettres liés à cette dernière envoient une demande SIP OPTIONS à la passerelle VoIP, au PBX IP ou au SBC pour s’assurer que le périphérique répond. Si la passerelle VoIP, le PBX IP ou le SBC ne répond pas à la demande, le serveur de boîtes aux lettres journalise un événement avec l’ID 1088 indiquant que la demande a échoué. Le cas échéant, vérifiez que la passerelle VoIP, le PBX IP ou le SBC est disponible et en ligne et que la messagerie unifiée est correctement configurée.

Les serveurs d’accès au client et de boîtes aux lettres ne doivent communiquer qu’avec une passerelle VoIP, un PBX IP ou un contrôleur de frontière de session (SBC) répertorié(e) en tant qu’homologue SIP (Session Initiation Protocol) approuvé. Un événement doté de l’ID 1175 est journalisé lorsque plusieurs hôtes DNS partagent la même adresse IP. Cet événement peut se produire si vous avez configuré vos zones DNS avec des noms de domaine complets pour les passerelles VoIP de votre réseau. La messagerie unifiée protège contre les demandes non autorisées en récupérant l’URL interne du répertoire virtuel des services web de messagerie unifiée situé sur le serveur de boîtes aux lettres et utilise ensuite l’URL pour construire la liste des noms de domaines complets pour les homologues SIP approuvés. Lorsque deux noms de domaine complets correspondent à même adresse IP, cet événement est alors journalisé.

> [!NOTE]
> Vous devez redémarrer le service de messagerie unifiée MicrosoftExchange si une passerelle VoIP, un PBX IP ou un SBC est configuré pour utiliser un nom de domaine complet et si l’enregistrement DNS de la passerelle VoIP, du PBX IP ou du SBC est modifié après que le service a démarré. Si vous ne redémarrez pas le service, le serveur de boîtes aux lettres n’est pas en mesure de localiser la passerelle VoIP, le PBX IP ou le SBC. Cela est dû au fait qu’un serveur de boîtes aux lettres gère un cache pour toutes les passerelles VoIP, tous les PBX IP ou tous les SBC en mémoire et que la résolution DNS ne s’effectue qu’en cas de redémarrage du service ou de modification de la configuration d’une passerelle VoIP, d’un PBX IP et d’un contrôleur de frontière de session (SBC).

