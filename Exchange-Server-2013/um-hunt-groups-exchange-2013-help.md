---
title: 'Groupes de recherche de messagerie unifiée: Exchange 2013 Help'
TOCTitle: Groupes de recherche de messagerie unifiée
ms:assetid: 026129a1-b0b5-410a-bed6-2d49f85205b3
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Aa995918(v=EXCHG.150)
ms:contentKeyID: 50555337
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Groupes de recherche de messagerie unifiée

 

_**Sapplique à :** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2013-02-18_

Un groupement de postes de téléphonie offre un moyen de répartir des appels téléphoniques à partir d'un numéro unique vers plusieurs postes ou numéros de téléphone. Dans la messagerie unifiée, un groupement de postes de messagerie unifiée constitue une représentation logique d'un groupement de postes de téléphonie et relie une passerelle IP de messagerie unifiée à un plan de numérotation de messagerie unifiée.

Recherchez-vous les tâches de gestion liées aux groupements de postes de messagerie unifiée ? Voir [Procédures de groupe postes de messagerie unifiée](um-hunt-group-procedures-exchange-2013-help.md).

**Table des matières**

What is a hunt group

What is a pilot number

What is a UM hunt group

## Qu'est-ce qu'un groupement de postes ?

Le terme *groupement de postes* est utilisé pour décrire un groupe de numéros de poste PBX (Private Branch eXchange) ou PBX IP partagés par des utilisateurs. Les groupements de postes servent à répartir efficacement les appels au sein de ou en dehors d'une unité de gestion spécifique. La création et la définition d'un groupement de postes réduisent le risque qu'un appelant qui passe un appel entrant reçoive une tonalité d'occupation lors de la réception de l'appel.

Les groupements de postes permettent de localiser une ligne, un poste ou un canal ouvert lors de la réception d'un appel entrant. Les appels sont « basculés » vers la ligne suivante disponible si la ligne téléphonique principale est occupée ou ne répond pas. L'appelant reçoit une tonalité d'occupation ou est transféré vers la messagerie vocale uniquement si aucun poste du groupe n'est ouvert. Par exemple, un PBX ou un PBX IP peut être configuré avec 10 numéros de poste pour le service commercial. Les 10 numéros de poste du service commercial ne forment alors qu'un seul groupement de postes.

Les paramètres relatifs à un groupement de postes simple incluent un nom, un numéro de poste, la liste des membres du groupe accessibles et une méthode de sélection du groupement de postes. La méthode de sélection du groupement de postes détermine l'ordre de présentation des appels entrants auprès des membres du groupement de postes.

Il existe plusieurs algorithmes ou méthodes qui permettent à un PBX ou un PBX IP de localiser une ligne, un poste ou un canal ouvert. Ces méthodes sont les suivantes :

  - **Groupement de postes ou sonnerie sur tous les postes**    Quand un appel entrant est reçu sur le numéro de poste du groupement de postes, le PBX ou PBX IP fait sonner tous les numéros de poste du groupe.

  - **Recherche en débutant par le plus petit numéro ou recherche d'une ligne libre**   Il s'agit du paramètre par défaut sur la plupart des PBX et PBX IP. Cette méthode permet d'acheminer des appels vers la première ligne libre selon un ordre séquentiel, en commençant par la première ligne du groupe. Cette configuration est plus souvent trouvée sur les téléphones multilignes des petites entreprises.

  - **Recherche par décalage en fonction de la dernière ligne occupée ou recherche en cycle**   Cette méthode permet aux appels d'être acheminés vers la première ligne disponible, en commençant par la dernière ligne ayant géré un appel. Si un appel arrive sur la ligne 1, l'appel suivant va sur la ligne 2, le suivant sur la ligne 3, etc. lorsque des appels sont répartis selon la méthode dite du « décalage en fonction de la dernière ligne occupée (round-robin) ». Ce processus se poursuit même si une des lignes précédentes se libère. Quand la fin du groupement de postes est atteinte, les recherches recommencent à partir de la première ligne. Les lignes ne sont ignorées que si elles sont encore occupées par un appel précédent. La recherche en cycle ou par décalage en fonction de la dernière ligne occupée répartit la perturbation d'appels uniformément sur tous les appels, minimisant ainsi les risques de perturbation importante du service.

  - **Recherche de la ligne la plus inactive ou recherche par répartition uniforme**    Cette méthode permet d'acheminer l'appel vers la première ligne disponible du groupe qui a été inactive depuis le plus longtemps. Cette méthode utilise la durée pendant laquelle la personne qui prend l'appel a été occupée, au lieu de la disponibilité éventuelle de la ligne. Cette méthode est généralement utilisée dans les grands centres d'appels lorsque des personnes répondent à des appels entrants et que la charge est répartie uniformément sur le groupe de numéros de postes.

Vous pouvez configurer un ou plusieurs groupements de postes. Chaque groupement de postes doit comporter au minimum deux lignes. Si un numéro est déjà utilisé dans un groupement de postes, il ne sera pas accessible dans un autre.

Voici des exemples de groupements de postes de téléphonie simples et de leur fonctionnement.

**Exemple 1**

Le poste 300 (numéro pilote) est programmé pour faire sonner le poste 301, puis 302, puis 303, puis 304 quand un appel entre.

1.  Le poste 301 est occupé.

2.  Le poste 302 sonne, mais ne répond pas.

3.  Le poste 303 répond à l'appel.

4.  Le poste 304 est libre et en attente d'un appel entrant.

**Exemple 2**

Le poste 1000 (numéro pilote) est programmé pour faire sonner tous les postes 2000 à 2003 en même temps quand un appel entre :

1.  Le poste 2000 est libre.

2.  Le poste 2001 est libre.

3.  Le poste 2002 est libre.

4.  Le poste 2003 répond à l'appel entrant.

Retour au début

## Qu'est-ce qu'un numéro de pilote ?

Dans un réseau téléphonique, un PBX ou un PBX IP peut être configuré pour disposer d'un ou de plusieurs groupements de postes. Chaque groupement de postes créé sur un PBX ou un PBX IP doit être associé à un *numéro pilote*. L'utilisation d'un numéro pilote permet d'éliminer la tonalité d'occupation et d'acheminer les appels entrants vers les numéros de poste disponibles. Le PBX ou le PBX IP se sert du numéro pilote pour localiser le groupement de postes, et pour localiser ensuite le numéro de poste téléphonique sur lequel l'appel entrant a été reçu ainsi que les postes ayant été attribués au groupement de postes. Sans numéro pilote défini, le PBX ou PBX IP ne peut localiser l'emplacement de réception de l'appel entrant.

Un numéro pilote correspond à l'adresse, au poste ou à l'emplacement du groupement de postes au sein du PBX ou du PBX IP. Il s'agit généralement d'un numéro de poste « vide » ou d'un numéro de poste unique d'un groupement de postes de numéros de poste qui n'est associé à aucun téléphone ni à aucune personne. Par exemple, vous pourriez configurer un groupement de postes sur un PBX ou un PBX IP pour qu'il contienne les numéros de poste 4100, 4101, 4102, 4103, 4104 et 4105. Le numéro pilote du groupement de postes est configuré comme étant le poste 4100. Lors de la réception d'un appel sur le numéro de poste 4100, le PBX ou le PBX IP recherche le numéro de poste disponible suivant pour déterminer à qui transmettre l'appel. Dans cet exemple, le PBX ou le PBX IP doit utiliser son algorithme de recherche programmée pour consulter les numéros de poste 4101, 4102, 4103, 4104 et 4105.

L'utilisation d'un numéro pilote permet d'éliminer les tonalités d'occupation et d'acheminer les appels entrants vers des numéros de poste disponibles. Dans la messagerie unifiée, le numéro pilote du PBX ou du PBX IP est utilisé comme cible. Si aucun des numéros de poste du groupement de postes ne répond à un appel entrant, l'appel est acheminé vers le serveur de boîtes aux lettres qui exécute le service de messagerie unifiée de Microsoft Exchange.

Retour au début

## Qu'est-ce qu'un groupement de postes de messagerie unifiée ?

Les groupements de postes de messagerie unifiée sont essentiels pour le fonctionnement du système de messagerie unifiée. Un groupement de postes de messagerie unifiée est une représentation logique d'un groupement de postes PBX ou PBX IP existant. Il permet de relier une passerelle IP de messagerie unifiée à un plan de numérotation de messagerie unifiée. Un même groupement de postes de messagerie unifiée peut également relier plusieurs passerelles IP de messagerie unifiée à un plan de numérotation de messagerie unifiée. Par défaut un groupement de postes de messagerie unifiée est créé lorsque vous créez une passerelle IP de messagerie unifiée et l'associez à un plan de numérotation de messagerie unifiée, et vous pouvez également créer d'autres groupements de postes. Vous devez créer au moins un groupement de postes de messagerie unifiée.

Les groupements de postes de messagerie unifiée servent à localiser le groupement de postes PBX ou PBX IP à partir duquel un appel entrant est reçu. Un numéro pilote défini pour un groupement de postes dans le PBX ou le PBX IP doit également être défini pour le groupement de postes de messagerie unifiée. Le numéro pilote sert à établir une correspondance entre les informations présentées pour des appels entrants en utilisant les informations de signalisation SIP (Session Initiation Protocol) sur le message vocal. Le numéro pilote permet aux serveurs Exchange d'interpréter l'appel ainsi que le plan de numérotation approprié afin de pouvoir acheminer l'appel correctement. L'absence d'un groupement de postes empêche les serveurs Exchange de connaître l'emplacement de l'appel entrant. Le fait de connaître l'emplacement des appels entrants permet aux serveurs Exchange d'accepter les informations d'en-tête des appels qui ont été transmises à partir de la passerelle VoIP, du PBX IP ou du PBX compatible SIP. Il est très important de configurer correctement vos groupements de postes de messagerie unifiée, car les appels entrants ne correspondant pas au numéro pilote défini dans le groupement de postes de messagerie unifiée restent sans réponse et le routage des appels entrants va échouer.

Quand vous créez un groupement de postes de messagerie unifiée sur des déploiements locaux ou hybrides, vous activez tous les serveurs d'accès au client et de boîtes aux lettres, qu'ils soient ajoutés ou non à un plan de numérotation de messagerie unifiée, pour communiquer avec une passerelle VoIP, un PBX IP ou un PBX compatible SIP. En effet, tous les serveurs d'accès au client et de boîtes aux lettres répondent aux appels entrants pour tous les plans de numérotation, et non pour un plan de numérotation de messagerie unifiée spécifique comme le faisait le serveur de messagerie unifiée dans les versions précédentes d'Exchange. Si vous supprimez le groupement de postes de messagerie unifiée, la passerelle IP de messagerie unifiée associée n'est pas en mesure de répondre aux appels entrants provenant d'une passerelle VoIP, d'un PBX IP ou d'un PBX compatible SIP ou d'émettre des appels sortants via la passerelle VoIP, le PBX IP ou le PBX compatible SIP en utilisant le numéro pilote spécifié.

Cependant, si vous intégrez un service de messagerie unifiée à Microsoft Office Communications Server 2007 R2 ou Microsoft Lync Server pour des déploiements locaux ou hybrides, vous devez ajouter tous les serveurs d'accès au client et de boîtes aux lettres à tous les plans de numérotation URI SIP qui ont été créés pour utiliser Communications Server 2007 R2 ou Lync Server. Ceci permet un fonctionnement correct du routage des appels et de l'automate d'appels.

Pour plus d'informations sur les passerelles IP de messagerie unifiée, consultez la rubrique [Passerelles IP de messagerie unifiée](um-ip-gateways-exchange-2013-help.md).

