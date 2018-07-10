---
title: 'Serveur de boîtes aux lettres: Exchange 2013 Help'
TOCTitle: Serveur de boîtes aux lettres
ms:assetid: 1aacc1c9-c81b-47d4-b222-ee73956cf968
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ150491(v=EXCHG.150)
ms:contentKeyID: 50477706
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Serveur de boîtes aux lettres

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2013-02-19_

Dans Microsoft Exchange Server 2010, le rôle serveur de boîte aux lettres hébergeait les bases de données de dossiers publics et de boîtes aux lettres et assurait le stockage des messages électroniques. Désormais, dans Exchange Server 2013, le rôle serveur de boîte aux lettres inclut également les protocoles d'accès au client, le service de transport, les bases de données de boîtes aux lettres et les composants de messagerie unifiée.

Dans Exchange 2013, le rôle serveur de boîte aux lettres est en interaction directe avec Active Directory, le serveur d'accès au client et les clients Microsoft Outlook dans les processus suivants :

  - Le serveur de boîtes aux lettres utilise LDAP pour accéder aux informations sur le destinataire, le serveur et la configuration de l'organisation à partir d'Active Directory.

  - Le serveur d'accès au client envoie des demandes de clients destinées au serveur de boîtes aux lettres, puis renvoie les données du serveur de boîtes aux lettres à destination des clients. Le serveur d'accès au client accède également aux fichiers du carnet d'adresses en ligne sur le serveur de boîtes aux lettres par l'intermédiaire du partage de fichiers NetBIOS. Le serveur d'accès au client envoie des messages, des données de disponibilité, des paramètres de profil du client et des données du carnet d'adresses en ligne entre le client et le serveur de boîtes aux lettres.

  - Les clients Outlook se trouvant à l'intérieur du pare-feu peuvent accéder au serveur d'accès au client pour envoyer et récupérer des messages. Les clients Outlook situés à l'extérieur du pare-feu peuvent accéder au serveur d'accès au client à l'aide d'Outlook Anywhere (qui utilise le composant Proxy RPC sur HTTP).

  - Les boîtes aux lettres des dossiers publics sont accessibles via RPC sur HTTP, que le client se trouve à l'intérieur ou à l'extérieur du pare-feu.

  - L'ordinateur administrateur extrait les informations de topologie Active Directory par l'intermédiaire du service de topologie Active Directory de Microsoft Exchange. Il extrait également les informations de stratégie d'adresse de messagerie et les informations de liste d'adresses.

  - Le serveur d'accès au client utilise LDAP ou l'interface NSPI (Name Service Provider Interface) pour contacter le serveur Active Directory et récupérer les informations Active Directory des utilisateurs.

**Architecture et interaction des serveurs d'accès au client et de boîtes aux lettres**

![Interaction avec le serveur d’accès au client et de boîtes aux lettres](images/JJ150491.d14577bf-14f9-40fa-bd49-a92932eb003a(EXCHG.150).gif "Interaction avec le serveur d’accès au client et de boîtes aux lettres")

Pour plus d'informations, consultez la section « Architecture d'Exchange 2013 » dans la rubrique [Nouveautés d'Exchange 2013](what-s-new-in-exchange-2013-exchange-2013-help.md).

## Nouvelles fonctionnalités des boîtes aux lettres

La liste suivante décrit brièvement certaines fonctionnalités nouvelles et améliorées du rôle de boîte aux lettres pour Exchange 2013 :

  - Évolution du groupe de disponibilité de base de données (DAG) Exchange 2010 :
    
      - Le code du journal des transactions a été refactorisé pour un basculement rapide avec un point de contrôle approfondi sur les copies de bases de données passives.
    
      - Pour assurer une résilience améliorée du site, les serveurs peuvent se trouver à des emplacements divers.

  - Exchange 2013 héberge désormais certains composants de l'accès au client, les composants de transport et les composants de la messagerie unifiée.

  - La banque d'informations Exchange a été ré-écrite en code managé pour améliorer les performances en termes de réduction et de fiabilité des E/S supplémentaires.

  - Chaque base de données Exchange 2013 est désormais exécutée par son propre processus.

  - La recherche intelligente a remplacé l'infrastructure de recherche dans plusieurs boîtes aux lettres d'Exchange 2010.

## Sécurisation des serveurs de boîtes aux lettres

Par défaut, les communications HTTP, Microsoft Exchange ActiveSync, POP3 et IMAP4 entre les serveurs de boîtes aux lettres et d'autres rôles serveur Exchange, contrôleurs de domaines et serveurs de catalogue global sont chiffrées. Par ailleurs, assurez-vous que vos serveurs de boîtes aux lettres ne sont pas accessibles via Internet.

## Pour plus d'informations

[Messagerie unifiée](unified-messaging-exchange-2013-help.md)

[Flux de messagerie](mail-flow-exchange-2013-help.md)

[Haute disponibilité et résilience de site](high-availability-and-site-resilience-exchange-2013-help.md)

[Stratégie et conformité de messagerie](messaging-policy-and-compliance-exchange-2013-help.md)

[Déplacements de boîtes aux lettres dans Exchange 2013](mailbox-moves-in-exchange-2013-exchange-2013-help.md)

[Gestion des bases de données de boîtes aux lettres dans Exchange 2013](manage-mailbox-databases-in-exchange-2013-exchange-2013-help.md)

[Stratégie et conformité de messagerie](messaging-policy-and-compliance-exchange-2013-help.md)

[Recipients](recipients-exchange-2013-help.md)

[Collaboration](collaboration-exchange-2013-help.md)

