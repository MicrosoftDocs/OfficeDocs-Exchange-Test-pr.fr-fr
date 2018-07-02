---
title: 'Prise en charge d’IPv6 dans la messagerie unifiée: Exchange 2013 Help'
TOCTitle: Prise en charge d’IPv6 dans la messagerie unifiée
ms:assetid: 91242c85-ce4e-422a-954e-ab623d3d6939
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ150536(v=EXCHG.150)
ms:contentKeyID: 50478691
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Prise en charge d’IPv6 dans la messagerie unifiée

 

_**Sapplique à :**Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :**2015-04-07_

Le protocole IPv6 (Internet Protocol Version 6) est la version la plus récente du protocole Internet (IP). IPv6 est conçu pour corriger un grand nombre d’insuffisances d’IPv4, la précédente version du protocole Internet. Dans Microsoft Exchange Server 2010, IPv6 n’est pris en charge que si IPv4 est également utilisé. Un environnement exclusivement IPv6 n’est pas pris en charge. L’utilisation d’adresses IPv6 et de plages d’adresses IP n’est prise en charge que si IPv6 et IPv4 sont activés sur l’ordinateur qui exécute Exchange 2010 et si le réseau prend en charge les deux versions d’adresse IP. Cependant, étant donné que IPv4 et IPv6 sont totalement différents, un réseau IPv4 ne peut pas communiquer directement avec un réseau IPv6, et inversement. Pour pallier cette lacune, les administrateurs réseau doivent déployer des périphériques, par exemple des routeurs, qui sont capables de router des informations entre des réseaux IPv4 et IPv6. En cas de déploiement d’Exchange 2010 en utilisant IPv4 et IPv6, tous les rôles serveur à l'exception de la messagerie unifiée (UM) peuvent échanger des données avec des périphériques, des serveurs et des clients qui utilisent des adresses IPv6. Avec Exchange 2013, la messagerie unifiée n’est plus un rôle serveur distinct à l’instar des rôles serveur Transport, Accès au client et Boîte aux lettres dans Exchange 2007 et Exchange 2010. Les composants liés à la messagerie unifiée et aux services de reconnaissance vocale s’exécutent uniquement sur des serveurs d’accès au client et de boîtes aux lettres.

Dans Exchange 2013, puisque l’architecture de messagerie unifiée a changé et nécessite UCMA (Unified Communications Managed API) v4.0 pour prendre en charge IPv4 et IPv6 ainsi que d’autres fonctionnalités d’Exchange, les serveurs d’accès au client et de boîtes aux lettres qui disposent de composants et de services de messagerie unifiée prennent en charge complètement les réseaux IPv6.

## Prise en charge IPv6

A partir de Microsoft Exchange 2010 Service Pack 1 (SP1), le rôle serveur de messagerie unifiée s’appuie sur UCMA 2.0 pour sa signalisation SIP (Session Initiation Protocol) et son traitement de reconnaissance vocale sous-jacents. UCMA 2.0 est le principal composant des fonctionnalités de reconnaissance vocale dans la messagerie unifiée. Outre une synthèse vocale générée par la fonction de synthèse vocale (TTS), UCMA 2.0 contient une pile SIP, une pile média, des moteurs de reconnaissance vocale pour la reconnaissance vocale automatique.

Dans Exchange 2010, l’exécution d’une double pile (IPv4 et IPv6) était requise par tous les serveurs sauf pour la messagerie unifiée car celle-ci nécessitait UCMA 2.0 et prenait en charge IPv4 uniquement, et non IPv6. S’agissant de Exchange 2013, UCMA 4.0 est utilisé par la messagerie unifiée et est requis pour l’installation d’Exchange 2013 sur des serveurs d’accès au client et de boîtes aux lettres. UCMA 4.0 est nécessaire pour la prise en charge de nouvelles fonctionnalités et pour prendre en charge IPv6.

L’usage d’UCMA 4.0 par la messagerie unifiée se justifie notamment par la prise en charge de nouvelles fonctionnalités de Microsoft Exchange 2013, y compris IPv6, les raisons en sont les suivantes :

  - Certaines agences gouvernementales exigent la prise en charge d’IPv6 pour les produits qu’elles utilisent.

  - La messagerie unifiée nécessite désormais la compatibilité avec des périphériques matériels comme des routeurs, des passerelles IP, des systèmes IP-PBX et des contrôleurs de frontière de session (ou contrôleur SBC) qui exécutent une double pile (IPv4 et IPv6) ou IPv6 uniquement.

  - Dans Exchange 2013, le service de messagerie unifiée de Microsoft Exchange s’exécute sur le serveur de boîtes aux lettres et le service Routeur d’appel de messagerie unifiée Microsoft Exchange s’exécute sur le serveur d’accès au client. Les rôles serveur de boîtes aux lettres et serveur d’accès au client dans Exchange 2013 nécessitent IPv4 et IPv6.

  - Les services en ligne autorisent les clients à se connecter à leur service en utilisation IPv4 ou IPv6.

  - L’espace d’adressage IPv4 public s’épuise. Pour Exchange Server 2013 Enterprise, il ne s’agit vraiment d’un problème pour la messagerie unifiée, puisque celle-ci communique toujours avec des homologues SIP internes qui peuvent être déployés avec un espace adresse IPv4 privé. Cependant, s’il s'agit d’une messagerie unifiée Exchange hébergée, l’équipement du client doit prendre en charge la messagerie unifiée hébergée en utilisant IPv4 et IPv6.

A l’exception de la messagerie unifiée et d’une petite partie du Transport, Exchange 2013 peut se connecter à des serveurs Exchange 2010 au sein d’une organisation lorsqu’un serveur d’accès au client ou un serveur de boîtes aux lettres s’exécute en mode double pile avec IPv4 et IPv6 activés. En d’autres termes, des clients peuvent installer Exchange 2013 sur des ordinateurs qui exécutent des adresses de pile IPv4 et IPv6 configurées. Ainsi, des clients IPv6 et d'autres serveurs Exchange, notamment Exchange Server 2010, peuvent se connecter directement à Exchange 2013.

La messagerie unifiée fonctionne sur des serveurs Windows exécuté en mode double pile. Ceci parce que des protocoles comme HTTP ignorent le type transport, et la messagerie unifiée utilise des protocoles VoIP (y compris SIP/RTP/STUN/TURN/ICE) qui ne sont pas dépendant les uns des autres. Ceci inclut une négociation de médias (RTP/SRTP), dans laquelle la messagerie unifiée publie et communique une liste d’adresses IP à des homologues SIP, comme des passerelles IP, des systèmes IP-PBX ou des contrôleurs SBC.

## Que signifie la prise en charge d’IPv6 pour la messagerie unifiée ?

Pour permettre à la messagerie unifiée de Microsoft Exchange 2013 de prendre en charge IPv6, les administrateurs de l’entreprise et de la messagerie unifiée en ligne doivent pouvoir bénéficier de la technologie IPv6 lorsqu’ils connectent une messagerie unifiée à des périphériques compatibles IPv6, notamment des périphériques comme des routeurs, des passerelles IP, des systèmes IP-PBX et des serveurs Office Communications Server 2007 R2 et Microsoft Lync. Toutefois, si IPv6 n’est pas nécessaire pour une interopérabilité et une compatibilité descendante avec des versions précédentes d’Exchange, les administrateurs n’ont pas besoin de faire des modifications supplémentaires et IPv4 peut être utilisé à la place.

Pour Exchange 2013 Enterprise, la messagerie unifiée doit communiquer directement avec des homologues SIP (passerelles IP, systèmes IP-PBX et contrôleurs SBC) susceptibles de ne pas prendre en charge IPv6 dans leurs logiciels et microprogrammes. En conséquence, la messagerie unifiée doit être en mesure de communiquer directement avec des homologues SIP compatibles avec IPv4 et, plus important, avec IPv6. Pour Exchange 2013 hébergé, la messagerie unifiée communique avec les équipements des clients via des contrôleurs SBC ou Lync Server 2010 ou Lync Server 15. Dans des environnements Exchange 2013 hébergés, des clients compatibles SIP IPv6 comme des contrôleurs SBC et des serveurs Lync peuvent potentiellement être déployés et donc gérer un processus de conversion IPv6 vers IPv4.

## Prise en charge de périphériques de messagerie unifiée pour IPv6

Puisque des serveurs de boîtes aux lettres et d’accès au client Microsoft Exchange 2013 qui exécutent des composants et des services de messagerie unifiée prennent en charge IPv6, des passerelles IP, des systèmes IP-PBX et des contrôleurs SBC, les fournisseurs doivent également être mesure de prendre en charge IPv6. Plusieurs problèmes affectant la prise en charge des périphériques pour IPv6 ont été identifiés :

  - Des passerelles IP, systèmes IP-PBX et contrôleurs SBC sont en mesure de prendre en charge IPv6, mais ils n’ont pas encore été testés avec IPv6 et la messagerie unifiée. Cette prise en charge pourra être ajouté à l’avenir, mais elle est dépendante du fournisseur de matériels.

  - Certaines passerelles IP n’ont actuellement aucune prise en charge IPv6.

  - Certains contrôleurs SBC disposent de fonctionnalités IPv4-IPv6, sauf que cela ne fonctionne pas pour la messagerie unifiée parce qu’ils ne prennent pas en charge les protocoles SRTP (Secure Real-time Transport Protocol)/SDES (Session Description Protocol Security).

  - Il existe des systèmes IP-PBX qui ne prennent en charge ni une double pile ni IPv6 pur, mais ces périphériques n’ont pas été testés pour un usage avec Exchange 2013.

Actuellement UCMA 4.0 est compatible IPv6, ce qui signifie qu’il peut accepter des connexions IPv6, mais que IPv4 peut également être accepté, en mode de fonctionnement double ou en établissant des connexions sortantes. Un fonctionnement en mode double autorise l’établissement de connexions IPv4 si une connexion à des versions précédentes de la messagerie unifiée d’Exchange s’avère nécessaire. S'agissant des installations Lync, ceci peut être effectué par Lync Server, qui obtient les informations de version à partir d’Active Directory pour la dernière version d’Exchange Server. Concernant les périphériques de téléphonie traditionnels, comme les passerelles IP, systèmes IP-PBX et contrôleurs SBC, pour la prise en charge des connexions IPv6 et IPv4, ceux-ci doivent être à l’écoute des deux types de connexion. Ceci s’explique par le fait que chaque homologue SIP doit être en mesure d’accepter les deux types de connexion pour des raisons de compatibilité descendante avec des versions précédentes de la messagerie unifiée de Microsoft Exchange. Ceci est également nécessaire pour prendre en charge l’automate d’appels pour les deux types de connexions.

## Configuration de la messagerie unifiée pour prendre en charge IPv6

Après avoir installé vos serveurs d’accès au client et de boîtes aux lettres, vous devez créer des plans de numérotation, des standards automatiques, des passerelles IP et des groupements de postes de messagerie unifiée. Pour permettre à la messagerie unifiée de prendre en charge IPv6, vous devez :

  - Créez une nouvelle passerelle IP de messagerie unifiée ou configurez une passerelle IP de messagerie unifiée existante avec une adresse IPv6 pour chacune des passerelles IP, PBX IP ou SBC de votre réseau. Lorsque vous créez et configurez les passerelles IP de messagerie unifiée requises, vous devez ajouter l'adresse IPv6 ou le nom de domaine complet pour la passerelle IP de messagerie unifiée. Si vous ajoutez le nom de domaine complet à la passerelle IP de messagerie unifiée, vous devez avoir créé les enregistrements DNS corrects pour résoudre le nom de domaine complet de la passerelle IP de messagerie unifiée en adresse IPv6. Si vous disposez d'une passerelle IP de messagerie unifiée existante, vous pouvez utiliser la cmdlet **Set-UMIPgateway** pour configurer l'adresse IPv6 ou le nom de domaine complet. Après avoir créé ou configuré les passerelles IP de messagerie unifiée, utilisez la cmdlet **Get-UMIPgateway** pour afficher les propriétés de la passerelle IP de messagerie unifiée et vérifier que les paramètres IPv6 sont corrects.

  - Configurez le paramètre *IPAddressFamily* sur chaque passerelle IP de MU. Pour permettre à la passerelle IP d’accepter des paquets IPv6, vous devez définir la passerelle IP de messagerie unifiée pour accepter les connexions IPv4 et IPv6 ou n’accepter que des connexions IPv6, en utilisant la cmdlet **Set-UMIPgateway** et en définissant le paramètre *IPAddressFamily* à une des valeurs suivantes :
    
      - *IPv4* – Il s’agit de la valeur par défaut. Elle est utilisée si aucune autre valeur n’est configurée.
    
      - *IPv6* - Ceci permet l’utilisation d’IPv6. Notez qu’IPv4 n’est pas utilisé.
    
      - *Any* – Ceci permet l’utilisation d’IPv6, mais si le périphérique ne prend pas en charge IPv6, IPv4 est alors utilisé à la place.

  - Après avoir configuré vos passerelles IP de messagerie unifiée, vous devez également configurer les passerelles IP, systèmes IP-PBX et contrôleurs SBC sur votre réseau pour prendre en charge IPv6. Pour plus d'informations, demandez au fournisseur du matériel une liste de périphériques qui prennent en charge IPv6 expliquant comment les configurer.

  - Vous aurez peut-être besoin de définir les serveurs d’accès au client et de boîtes aux lettres pour accepter le trafic IPv6 si l’un ou l’autre des serveurs n’est configuré que pour recevoir le trafic IPv4. Notez cependant que le paramètre par défaut concerne les serveurs d’accès au client qui exécutent le service Routeur d’appel de messagerie unifiée Microsoft Exchange et les serveurs de boîtes aux lettres qui exécutent le service de messagerie unifiée de Microsoft Exchange pour accepter le trafic IPv4 et IPv6. Pour plus d’informations sur la configuration des paramètres IPv6 sur les serveurs d’accès au client et de boîtes aux lettres, consultez les rubriques [Set-UMCallRouterSettings](https://technet.microsoft.com/fr-fr/library/jj215758\(v=exchg.150\)) et [Set-UMService](https://technet.microsoft.com/fr-fr/library/jj552412\(v=exchg.150\)).
    
    Il est peut-être nécessaire de configurer deux paramètres sur les serveurs d’accès au client et de boîtes aux lettres pour prendre en charge IPv6 : *IPAddressFamily* et *IPAddressFamilyConfigurable*. Pour permettre à des serveurs d’accès au client et de boîtes aux lettres d’accepter des paquets IPv6, vous devez définir ces serveurs pour accepter des connexions IPv4 et IPv6 ou uniquement des connexions IPv6. Pour configurer le paramètre *IPAddressFamily*, le paramètre *IPAddressFamilyConfigurable* doit être défini à `$true`.

## Logique d’adressage IP de messagerie unifiée

La logique sur laquelle se fonde la prise en charge d’IPv6 pour la messagerie unifiée dans Exchange 2013 est comme suit :

  - Les serveurs d’accès au client et de boîtes aux lettres sont à l’écoute sur les interfaces IPv4 et IPv6 lorsque la double pile est activée et que ces serveurs sont définis à *IPv6* ou *Any*. Sinon, seul IPv4 est utilisé.

  - Pour les appels sortants, la messagerie unifiée utilise un mode double si le paramètre *IPAddressFamily* pour les passerelles IP de messagerie unifiée, les serveurs d’accès au client et les serveurs de boîtes aux lettres est défini à *IPv6* ou *Any*. Sinon, seul IPv4 est utilisé.

En effectuant des appels sortant en mode double, si le paramètre *IPAddressFamily* est défini à *IPv6* ou *Any* :

  - UCMA doit obtenir la liste des adresses dans le nom de domaine complet (FQDN) pour un homologue SIP qu’il tente d'atteindre.

  - UCMA doit essayer toutes les adresses IPv6, le cas échéant.

  - Si UCMA détermine qu’une adresse n’est pas accessible, il doit inclure cette adresse dans une liste et ne doit pas la ressayer sur la base d’un intervalle configuré. Ainsi, la messagerie unifiée n’effectue pas de nouvelles tentatives inutilement sur des adresses réputées mauvaises.

  - Si aucune adresse IPv6 n’est accessible, UCMA doit basculer vers les adresses IPv4 de la liste des adresses pour des homologues SIP.

