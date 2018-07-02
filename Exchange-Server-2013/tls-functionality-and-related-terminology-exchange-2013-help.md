---
title: 'Fonctionnalité TLS et terminologie associée: Exchange 2013 Help'
TOCTitle: Fonctionnalité TLS et terminologie associée
ms:assetid: 294ba2a9-892d-4a90-beec-9d298426b5f4
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb430753(v=EXCHG.150)
ms:contentKeyID: 52062947
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Fonctionnalité TLS et terminologie associée

 

_**Sapplique à :**Exchange Online, Exchange Server 2013_

_**Dernière rubrique modifiée :**2014-06-18_

Microsoft Exchange Server 2013 fournit des fonctionnalités administratives et d'autres améliorations qui améliorent la gestion globale du protocole TLS (Transport Layer Security). Au fur et à mesure de l'utilisation de cette fonctionnalité, vous devez en savoir plus sur certaines des nouvelles fonctions du protocole TLS. Certains termes et concepts s'appliquent à plusieurs fonctionnalités TLS. Dans cette rubrique, de courtes explications pour chaque fonctionnalité vous sont fournies et vous aideront à comprendre certaines différences, ainsi que la terminologie générale relative au protocole TLS et à la fonctionnalité de sécurité du domaine définie :

  - **Transport Layer Security**   TLS est un protocole standard utilisé pour sécuriser les communications web sur Internet ou des intranets. Il permet aux clients d'authentifier les serveurs ou, à titre facultatif, aux serveurs d'authentifier les clients. Il offre également un canal sécurisé en chiffrant les communications. TLS est la version la plus récente du protocole SSL (Secure Sockets Layer).

  - **Mutual TLS**   L'authentification Mutual TLS diffère du protocole TLS tel qu'il est généralement déployé. Généralement, quand le protocole TLS est déployé, il est utilisé uniquement à des fins de confidentialité sous la forme de chiffrement. Aucune authentification ne se produit entre l'expéditeur et le destinataire. Parfois, quand le protocole TLS est déployé, seul le serveur de réception est authentifié. Le déploiement de TLS est habituel dans l'implémentation HTTP de TLS. Cette implémentation, dans laquelle seul le serveur de réception est authentifié, est appelée SSL.
    
    Avec l'authentification Mutual TLS, chaque serveur vérifie l'identité de l'autre serveur en validant un certificat fourni par celui-ci. Dans ce scénario, quand des messages sont reçus de domaines externes sur des connexions vérifiées dans un environnement Exchange 2013, Microsoft Outlook affiche une icône **Domaine sécurisé**.

  - **Sécurité de domaine**   La sécurité de domaine est un ensemble de fonctionnalités, telles que la gestion des certificats et la fonctionnalité de connecteur, ainsi que le comportement client Outlook qui active Mutual TLS comme une technologie gérable et utile. La sécurité de domaine n'est pas prise en charge quand les messages sortants sont acheminés via un serveur d'accès au client Exchange 2013.

  - **TLS opportuniste**   Dans Exchange 2013, le programme d’installation crée un certificat auto-signé. Par défaut, TLS est activé. Cela permet à tout système émetteur de chiffrer la session SMTP entrante dans Exchange. Par défaut, Exchange 2013 teste également le protocole TLS pour toutes les connexions distantes.

  - **Confiance directe**   Par défaut, tout le trafic entre les serveurs de transport Edge et les serveurs de boîtes aux lettres est authentifié et chiffré. Le mécanisme sous-jacent pour l'authentification et le chiffrement est à nouveau mutual TLS. Au lieu d'utiliser une validation X.509, Exchange 2013 utilise une confiance directe pour authentifier les certificats. La confiance directe signifie que la présence du certificat dans Active Directory ou les services AD LDS (Active Directory Lightweight Directory Services) valide le certificat. Active Directory est considéré comme un mécanisme de stockage approuvé. Lorsque la confiance directe est utilisée, que le certificat soit auto-signé ou signé par une autorité de certification est sans importance. Quand vous abonnez un serveur de transport Edge à l'organisation Exchange, l'abonnement Edge publie le certificat du serveur de transport Edge dans Active Directory pour que les serveurs de boîtes aux lettres le valident. Le service Microsoft Exchange EdgeSync met à jour les services AD LDS avec l'ensemble des certificats de serveur de boîtes aux lettres pour validation par le serveur de transport Edge.

