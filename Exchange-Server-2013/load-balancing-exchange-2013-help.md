---
title: 'Équilibrage de charge: Exchange 2013 Help'
TOCTitle: Équilibrage de charge
ms:assetid: f572c193-6f3a-400e-9085-a9d3e5e18c59
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ898588(v=EXCHG.150)
ms:contentKeyID: 51407259
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Équilibrage de charge

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2016-12-09_

L'équilibrage de charge permet de répartir le trafic entre les serveurs. Il permet de distribuer les connexions clients entrantes sur une série de points de terminaison (par exemple, des serveurs d'accès au client) pour s'assurer qu'aucun d'eux ne reçoive une part disproportionnée de la charge. L'équilibrage de charge peut également offrir une redondance par basculement en cas de défaillance d'un ou plusieurs points de terminaison. En utilisant l'équilibrage de charge avec Exchange Server 2013, vous vous assurez que vos utilisateurs continuent à recevoir le service Exchange en cas de défaillance d'un ordinateur. L'équilibrage de charge permet également à votre déploiement de traiter plus de trafic qu'un seul serveur, tout en offrant un seul nom d'hôte pour vos clients.

L'équilibrage de charge a deux objectifs principaux. Il réduit l'impact d'échec d'un serveur d'accès au client unique à l'intérieur de vos sites Active Directory. Il garantit en outre une répartition égale de la charge entre vos serveurs d'accès au client.

Exchange 2013 inclut également les solutions suivantes pour le basculement et la redondance de basculement :

  - **Haute disponibilité**Exchange 2013 Cette solution utilise des groupes de disponibilité de base de données (DAG) pour assurer la synchronisation de plusieurs copies de vos boîtes aux lettres sur différents serveurs. Ainsi, en cas de défaillance d'une base de données sur un serveur, les utilisateurs peuvent se connecter à une copie synchronisée de cette base de données sur un autre serveur.

  - **Résilience de site** Vous pouvez déployer deux sites Active Directory dans des lieux géographiques distincts, maintenir la synchronisation des données de boîtes aux lettres entre eux, et faire en sorte que l'un des sites prenne toute la charge en cas de défaillance de l'autre.

  - **Déplacements de boîte aux lettres en ligne**  Dans un déplacement de boîte aux lettres en ligne, les utilisateurs peuvent accéder à leurs comptes de messagerie durant le déplacement. Les utilisateurs sont déconnectés de leur comptes uniquement pendant un court instant à la fin du processus, lors de la synchronisation finale. Vous pouvez effectuer des déplacements de boîtes aux lettres en ligne entre forêts ou dans une même forêt.

  - **Redondance des clichés instantanés**  La redondance des clichés instantanés protège la disponibilité et la capacité de récupération des messages en transit. Grâce à la redondance des clichés instantanés, la suppression d'un message dans les bases de données de transport est retardée jusqu'à ce que le serveur de transport vérifie que les sauts suivants de ce message ont abouti. En cas d'échec d'un des sauts avant le signalement du succès de la remise d'un message, ce dernier est soumis à nouveau pour livraison au saut qui n'a pas abouti.

## Changements d'architecture dans l'équilibrage de charge pour Exchange Server 2013

Dans Exchange Server 2010, les connexions clientes et le traitement étaient gérés par le rôle serveur d'accès au client. Cela exigeait que les connexions Outlook tant externes qu'internes, ainsi que les connexions d'appareils mobiles et les connexions clientes tierces, fassent l'objet d'un équilibrage de charge sur le groupe des serveurs d'accès au client d'un déploiement, afin d'obtenir une tolérance de panne et une utilisation efficace des serveurs. De nombreux protocoles d'accès au client Exchange 2010 nécessitaient une affinité, c'est-à-dire une relation entre le client et un serveur d'accès au client particulier. En particulier, Outlook Web App, le Panneau de configuration Exchange, les services web Exchange, Outlook Anywhere, les connexions MAPI TCP/IP Outlook, Exchange ActiveSync, le service de carnet d'adresses Exchange et Remote PowerShell nécessitaient ou bénéficiaient d'une affinité de serveur d'accès de client à client. Les options d'équilibrage de charge dans Exchange 2010 sont les suivantes :

  - Équilibrage de charge réseau Windows avec affinité d'IP source

  - Équilibrage de la charge matérielle

En raison des besoins différents des protocoles clients dans Exchange 2010, nous recommandions d'utiliser une solution d'équilibrage de charge de couche 7. L'équilibrage de charge de couche 7, également appelé équilibrage de charge de niveau application, permettait à la solution d'équilibrage de charge d'utiliser des règles complexes pour déterminer la manière d'équilibrer chaque demande entrant dans le système, étant donné que la conversation entière entre client et serveur était disponible pour la logique d'équilibrage de charge. Ces règles complexes garantissaient que toutes les demandes d'un client donné arrivent au même point de terminaison de serveur d'accès au client. Dans Exchange 2010, si toutes les demandes d'un client donné n'arrivaient pas au même point de terminaison pour les protocoles nécessitant une affinité, cela avait un impact négatif sur l'expérience utilisateur. Pour plus d'informations sur les options d'équilibrage de charge d'Exchange 2010, consultez la rubrique [Présentation de l'équilibrage de la charge dans Exchange 2010](https://go.microsoft.com/fwlink/p/?linkid=196447).

Exchange Server 2013 inclut deux types principaux de serveurs : les serveurs d'accès au client et les serveurs de boîtes aux lettres. Dans Exchange 2013, les serveurs d'accès aux client font office de serveurs proxy basse densité, sans état, permettant aux clients de se connecter à des serveurs de boîtes aux lettres Exchange 2013. Les serveurs d'accès au client Exchange 2013 fournissent un espace de noms unifié et l'authentification. En outre, les serveurs d'accès au client Exchange 2013 :

  - prennent en charge le proxy et la logique de redirection pour les protocoles clients ;

  - prennent en charge l'utilisation de l'équilibrage de charge de couche 4.

Avec l'affinité de session et l'équilibrage de charge de couche 7, toutes les demandes entre le client et le serveur sont envoyées au même point de terminaison, comme requis par divers protocoles. Les demandes sont distribuées au niveau de la couche application. Avec l'équilibrage de charge de couche 4, les demandes sont distribuées au niveau de la couche de transport. La solution d'équilibrage de charge distribue les demandes du client, qui ne connaît qu'une seule adresse IP (parfois appelée adresse IP virtuelle ou VIP), à un ensemble de serveurs qui exécutent le travail. La connexion entre le client et le serveur doit être établie avant que le contenu de la demande soit déterminé, de façon à ce que l'équilibrage de charge sélectionne un serveur pour recevoir la demande avant d'en examiner le contenu. La sélection peut se faire de diverses manières, par exemple, selon le principe de « tourniquet » (round-robin) où chaque connexion entrante aboutit au serveur cible suivant dans une liste circulaire, ou selon le principe du nombre de connexions le moins élevé où l'équilibrage de charge envoie chaque connexion au serveur ayant le plus petit nombre de connexions à ce moment. À présent que cette affinité de session n’est plus requise, le système offre plus de flexibilité, de choix et de simplicité en rapport avec l’architecture d’équilibrage de charge que vous déployez. Un équilibrage de charge sans affinité de session vous permet d’augmenter la capacité et l’utilisation de l’équilibrage de charge, car le traitement n’est pas utilisé pour maintenir des options d’affinité plus impliquées telles que l’équilibrage de charge basé sur des cookies ou l’ID de session SSL (Secure Sockets Layer).

## Groupes de serveurs d'accès au client et Exchange 2013

In Exchange 2010, nous avons introduit le concept de tableau d'accès au client. Après configuration d'un tableau d'accès au client pour un site Active Directory, tous les serveurs d'accès au client d'un site devenaient automatiquement membres du tableau. Dans les versions actuelles d'Exchange 2013, aucune configuration de tableau d'accès au client n'est requise, car le déploiement d'un service avec équilibrage de charge et à haute disponibilité est beaucoup plus simple.

## Solutions d'équilibrage de charge

L'utilisation d'un équilibrage de charge matérielle est toujours prise en charge pour Exchange 2013. Pour plus d’informations sur les solutions d’équilibrage de charge matérielle qui ont passé les tests de solutions avec Exchange 2010 et qui fonctionneront probablement aussi bien avec Exchange 2013, voir [Déploiement d’équilibrage de charge Exchange Server 2010](https://go.microsoft.com/fwlink/p/?linkid=261834). Gardez à l’esprit que cette page affiche la configuration de couche 7 complexe des équilibreurs de charge matérielle avec Exchange 2010. Le trafic de l’équilibrage de charge Exchange 2013 peut être beaucoup plus simple, compte tenu des changements d’architecture décrits précédemment dans cette rubrique. Au lieu de configurer l’affinité de session de chaque protocole Exchange, l’équilibrage de charge peut diriger les connexions entrantes aux serveurs d’accès au client Exchange 2013 vers un serveur disponible sans traitement de l’affinité supplémentaire. L'équilibrage de charge matérielle joue encore un rôle important en relation avec la haute disponibilité du service Exchange, car il peut détecter quand un serveur d'accès au client devient indisponible, et le retirer du groupe de serveurs gérant les connexions entrantes.

## Équilibrage de la charge réseau Windows

L'équilibrage de la charge réseau Windows est une solution d'équilibrage de charge logicielle couramment utilisée pour les serveurs Exchange. Plusieurs limitations sont associées au déploiement de l'équilibrage de la charge réseau Windows avec Microsoft Exchange.

  - Cette solution ne peut pas être utilisée sur des serveurs Exchange où les groupes de disponibilité de base de données (DAG) pour les boîtes aux lettres sont également utilisés, car l'équilibrage de la charge réseau Windows est incompatible avec le cluster de basculement Windows. Si vous utilisez un DAG Exchange 2013 et ne souhaitez pas utiliser l'équilibrage de la charge réseau Windows, vous devez faire en sorte que le rôle serveur d'accès au client et le rôle serveur de boîte aux lettres s'exécutent sur des serveurs distincts.

  - L'équilibrage de la charge réseau Windows ne détecte pas les pannes de service. Il détecte uniquement les pannes de serveur par adresse IP. Cela signifie que, si un service web particulier, tel qu’Outlook Web App, est défaillant alors que le serveur fonctionne encore, l’équilibrage de la charge réseau Windows ne détecte pas la défaillance et continue à router les demandes vers ce serveur d’accès au client. Une intervention manuelle est requise pour retirer du groupe d'équilibrage de charge le serveur d'accès au client en panne.

  - L'utilisation de l'équilibrage de la charge réseau Windows peut entraîner un débordement des ports de connexions, ce qui risque de provoquer une saturation des réseaux.

  - Étant donné que l'équilibrage de la charge réseau Windows traite uniquement l'affinité client en utilisant l'adresse IP source, cette solution n'est pas efficace lorsque le groupe d'IP source est trop petit. Cela peut se produire lorsque le groupe d'IP source se trouve sur un sous-réseau distant ou lorsque votre organisation utilise une traduction d'adresses réseau.

