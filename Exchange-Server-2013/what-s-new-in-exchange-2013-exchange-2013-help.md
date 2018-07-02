---
title: "Nouveautés d'Exchange 2013: Exchange 2013 Help"
TOCTitle: Nouveautés d'Exchange 2013
ms:assetid: 97501135-2149-4590-8373-98e638ac8eb1
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ150540(v=EXCHG.150)
ms:contentKeyID: 50478749
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Nouveautés d'Exchange 2013

 

_**Sapplique à :**Exchange Server 2013_

_**Dernière rubrique modifiée :**2016-12-09_

Consultez toutes les dernières fonctionnalités dans Exchange 2013.

Microsoft Exchange Server 2013 offre un vaste éventail de nouvelles technologies, nouvelles fonctionnalités et nouveaux services à la gamme de produits Exchange Server. Son objectif est de soutenir les utilisateurs et les organisations dans leur évolution, à l'heure où la collaboration a remplacé la communication au cœur des habitudes de travail. Dans le même temps, Exchange Server 2013 permet de diminuer le coût total de possession, avec un déploiement de Exchange 2013 local ou une configuration de vos boîtes aux lettres dans le nuage. Les nouvelles fonctions et fonctionnalités de Exchange 2013 sont conçues pour :

  - **S'adapter à un personnel multigénérationnel**   Les employés valorisent l'intégration sociale et la facilité de trouver les utilisateurs. *Smart Search* étudie les comportements de communication et de collaboration des utilisateurs pour améliorer et classer par priorité les résultats de recherche dans Exchange. De plus, avec Exchange 2013, les utilisateurs peuvent fusionner les contacts à partir de sources multiples afin de proposer une vue unique pour une personne unique, en établissant des liens entre les informations de contact provenant de plusieurs emplacements.

  - **Proposer une expérience attrayante**   Microsoft Outlook 2013 et Microsoft Outlook Web App présentent une nouvelle apparence. Outlook Web App tire parti d'une interface utilisateur moderne qui prend également en charge la fonctionnalité tactile pour une expérience mobile améliorée avec Exchange.

  - **S'intégrer avec SharePoint et Lync**   Exchange 2013 offre une meilleure intégration avec Microsoft SharePoint 2013 et Microsoft Lync 2013 grâce aux boîtes aux lettres de site et à la découverte électronique locale. Ensemble, ces produits offrent une palette de fonctionnalités qui rendent possibles certains scénarios, tels que la découverte électronique d'entreprise et la collaboration à l'aide des boîtes aux lettres de site.

  - **Aider à répondre aux besoins croissants de conformité**    La conformité et la recherche électronique sont deux défis que doivent relever les organisations. Exchange 2013 vous aide à chercher et trouver les données non seulement dans Exchange, mais dans l’intégralité de votre organisation. Avec des fonctionnalités améliorées de recherche et d'indexation, vous pouvez faire des recherches dans Exchange 2013, Lync 2013, SharePoint 2013 et les serveurs de fichiers Windows. De plus, la protection contre la perte de données permet de sécuriser votre organisation afin que des utilisateurs ne puissent pas envoyer par inadvertance des informations sensibles à des personnes non autorisées. DLP vous aide à identifier, surveiller et protéger les données sensibles grâce à l'analyse approfondie du contenu.

  - **Fournir une solution résiliente**   Exchange 2013 tire parti de l'architecture Exchange Server 2010 mais a été repensé pour améliorer la simplicité, l'utilisation du matériel et la protection contre les pannes.

Pour plus d'informations sur les modifications apportées à Exchange Server 2013 depuis la version de publication (RTM), consultez la rubrique [Mises à jour pour Exchange 2013](updates-for-exchange-2013-exchange-2013-help.md).

Consultez les sections suivantes pour plus d’informations sur les nouveautés d’Exchange 2013 :

Centre d'administration Exchange

Architecture Exchange 2013

Installation

Stratégie et conformité de la messagerie

Protection anti-programme malveillant

Flux de messagerie

Destinataires

Partage et collaboration

Intégration à SharePoint et Lync

Clients et mobilité

Messagerie unifiée

Déplacements par lot de boîtes aux lettres

[Haute disponibilité et résilience de site](high-availability-and-site-resilience-exchange-2013-help.md)

Gestion de la charge de travail Exchange

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Pour obtenir des informations sur les fonctionnalités de versions précédentes d'Exchange qui ont été supprimées, abandonnées ou remplacées dans Exchange Server 2013, consultez la rubrique <a href="what-s-discontinued-in-exchange-2013-exchange-2013-help.md">Fonctionnalités abandonnées dans Exchange 2013</a>. La rubrique <a href="release-notes-for-exchange-2013-exchange-2013-help.md">Notes de publication relatives à Exchange 2013</a> peut également vous intéresser.</td>
</tr>
</tbody>
</table>


## Centre d'administration Exchange

Exchange 2013 offre une console de gestion unifiée et unique qui facilite l'utilisation et optimise la gestion des déploiements locaux, en ligne ou hybrides. Le *Centre d'administration Exchange* (CAE) dans Exchange 2013 remplace la Console de gestion Exchange (EMC) et le Panneau de configuration Exchange (ECP) d'Exchange 2010 . (Cependant, « ECP » est encore le nom du répertoire virtuel utilisé par le Centre d'administration Exchange.) Les fonctionnalités du CAE comprennent :

  - **Affichage Liste**   L'affichage sous forme de liste du CAE a été conçu pour supprimer les limites de clés de l'ECP. L’ECP était limité pour afficher jusqu’à 500 objets et, si vous souhaitiez afficher des objets qui n’étaient pas répertoriés dans le volet d’informations, vous deviez utiliser les fonctions de recherche et de filtrage pour trouver ces objets spécifiques. Dans Exchange 2013, la limite d'affichage de cette vue dans le CAE est d'environ 20 000 objets. Quand le CAE renvoie des résultats, le client CAE effectue les opérations de recherche et de tri, ce qui améliore considérablement les performances par rapport à l'ECP d'Exchange 2010. De plus, la pagination a été ajoutée afin de pouvoir paginer les résultats. Vous pouvez également configurer la taille de page et exporter vers un fichier .csv.

  - **Ajout/Suppression de colonnes dans l'affichage de la liste des destinataires**   Vous pouvez choisir les colonnes à afficher, et à l'aide de cookies locaux, vous pouvez enregistrer vos affichages de listes personnalisés par machine que vous utilisez pour accéder au CAE.

  - **Sécurisation du répertoire virtuel de l'ECP**   Vous pouvez partitionner l'accès à Internet et aux intranets au sein du répertoire virtuel des services IIS de l'ECP afin d'activer ou de désactiver les fonctionnalités de gestion. Grâce à cette fonctionnalité, vous pouvez autoriser ou refuser l’accès à des utilisateurs qui essaient d’accéder au CAE par Internet depuis l’extérieur de l’environnement de votre organisation, tout en permettant à un utilisateur final d’accéder aux options Outlook Web App.

  - **Gestion des dossiers publics**   Dans Exchange 2010 et Exchange 2007, les dossiers publics étaient gérés via la console d'administration des dossiers publics. Les dossiers publics se trouvent désormais dans le CAE et vous n'avez besoin d'aucun outil supplémentaire pour les gérer.

  - **Notifications**   Dans Exchange 2013, le CAE dispose désormais d'un afficheur de notifications qui permet de connaître l'état des processus de longue durée et, si vous le souhaitez, de recevoir une notification via un message électronique une fois le processus terminé.

  - **Éditeur des utilisateurs RBAC (contrôle d'accès basé sur un rôle)**   Dans Exchange 2010, vous pouviez utiliser l'éditeur des utilisateurs RBAC à partir de la boîte à outils Exchange afin d'ajouter des utilisateurs aux groupes de rôles de gestion. Dans Exchange 2013, la fonctionnalité d'éditeur des utilisateurs RBAC se situe maintenant dans le CAE et vous n'avez pas besoin d'un outil séparé pour gérer le RBAC.

  - **Outils de messagerie unifiée**   Dans Exchange 2010, vous pouviez utiliser les outils de Statistiques d'appels et de Journaux d'appels utilisateurs pour obtenir des statistiques sur la messagerie unifiée et des informations spécifiques sur les appels d'un utilisateur à extension messagerie unifiée. Dans Exchange 2013, les outils de Statistiques d'appels et de Journaux d'appels utilisateurs se situent maintenant dans le CAE et vous n'avez pas besoin d'un outil séparé pour les gérer.

  - **Améliorations des groupes**   Le Centre d’administration Exchange (CAE) peut maintenant afficher jusqu’à 10 000 destinataires dans la fenêtre **GroupesSélectionner les membres**. Par défaut, jusqu’à 500 destinataires sont renvoyés lorsque vous ouvrez la fenêtre **Sélectionner les membres**, mais vous pouvez choisir de sélectionner jusqu’à 10 000 destinataires en cliquant sur **Obtenir tous les résultats** sous la liste des destinataires. Nous prenons maintenant en charge la navigation parmi plus de 500 destinataires avec la barre de défilement et nous avons également ajouté des fonctionnalités de recherche améliorées qui vous permettent de filtrer les destinataires affichés dans la liste des destinataires. Vous pouvez filtrer par :
    
      - Ville
    
      - Entreprise
    
      - Pays/Région
    
      - Service
    
      - Bureau
    
      - Fonction

Pour plus d'informations, consultez la rubrique [Centre d’administration Exchange dans Exchange 2013](exchange-admin-center-in-exchange-2013-exchange-2013-help.md).

## Architecture Exchange 2013

Les versions précédentes d'Exchange étaient optimisées et façonnées en respectant les exigences technologiques du moment. Par exemple, au cours du développement d'Exchange 2007, l'une des contraintes clés était la performance du processeur. Pour contourner le problème, Exchange 2007 était divisé en différents rôles de serveurs qui permettaient un équilibrage grâce à la séparation des serveurs. Toutefois, les rôles de serveurs dans Exchange 2007 et Exchange 2010 étaient étroitement associés. L'association étroite des rôles présentait certains désavantages comme la dépendance des versions, de l'emplacement géographique (tous les rôles sur un site spécifique) et de l'affinité des sessions (nécessitant une équilibrage de charge sur du matériel coûteux de couche 7), ainsi que la complexité de l'espace de noms.

À l'heure actuelle, la puissance des processeurs est beaucoup moins onéreuse et c'est n'est plus un facteur limitant. Ces barrières étant levées, l'objectif principal de la conception d'Exchange 2013 était d'améliorer la simplicité, l'utilisation du matériel et la protection contre les pannes. Avec Exchange 2013, nous avons réduit le nombre de rôles serveur à trois : les rôles serveur d’accès au client, de boîte aux lettres et de transport Edge.

Le serveur de boîtes aux lettres contient tous les composants de serveurs traditionnels trouvés dans Exchange 2010 : les protocoles d'accès au client, le service de transport, les bases de données de boîtes aux lettres et la messagerie unifiée. Le serveur de boîtes aux lettres gère toutes les activités des boîtes aux lettres actives sur ce serveur. Le serveur d'accès au client fournit l'authentification, la redirection limitée et les services proxy. Le serveur d'accès au client lui-même n'effectue pas de rendu de données. Le serveur d'accès au client est un serveur dynamique et sans état. Aucune information n'est jamais mise en file d'attente ni stockée sur le serveur d'accès au client. Le serveur d'accès au client offre tous les protocoles d'accès au client habituels : HTTP, POP, IMAP et SMTP.

Avec cette nouvelle architecture, le serveur d'accès au client et le serveur de boîtes aux lettres ne sont plus si étroitement liés. Tout le traitement et l'activité liés à une boîte aux lettres spécifique se passent sur le serveur de boîtes aux lettres qui héberge la copie de base de données active où réside la boîte aux lettres. Le rendu et la transformation des données sont réalisés en local sur la copie de base de données active, ce qui élimine les problèmes de compatibilité de version entre le serveur d'accès au client et le serveur de boîtes aux lettres.

Avec Exchange 2013 Service Pack 1, nous avons introduit le rôle serveur de transport Edge. Le rôle de transport Edge est généralement déployé sur votre réseau de périmètre, en dehors de votre forêt Active Directory interne, et il est conçu pour minimiser la surface d’attaque de votre déploiement Exchange. En gérant tous les flux de messagerie accessibles sur Internet, il ajoute également des couches supplémentaires de protection des messages et de sécurité contre les virus et les courriers indésirables, et il peut appliquer des règles de transport pour contrôler le flux des messages. Pour plus d’informations sur le rôle serveur de transport Edge, consultez la rubrique [Serveurs de transport Edge](edge-transport-servers-exchange-2013-help.md).

Les avantages de l'architecture Exchange 2013 sont les suivants :

  - **Souplesse de mise à niveau version**   Les exigences de mise à niveau ont été assouplies. Un serveur d'accès au client peut être mis à niveau de manière indépendante et dans n'importe quel ordre par rapport au serveur de boîte aux lettres.

  - **Indifférence des sessions**   Avec Exchange 2010, l'affinité entre les sessions pour le rôle serveur d'accès au client était nécessaire pour certains protocoles. Dans Exchange 2013, les composants du serveur d'accès au client et du serveur de boîtes aux lettres résident sur le même serveur de boîte aux lettres. Étant donné que le serveur d'accès au client sert simplement de proxy pour toutes les connexions d'un utilisateur vers un serveur de boîtes aux lettres spécifique, aucune affinité n'est nécessaire entre les sessions sur les serveurs d'accès au client. Cela permet aux connexions entrantes sur les serveurs d'accès au client d'être équilibrées à l'aide de techniques fournies par la technologie d'équilibrage de charge comme le plus petit nombre de connexions ou la répétition alternée.

  - **Simplicité de déploiement**   Avec une conception Exchange 2010 basée sur la résilience de site, vous nécessitiez jusqu'à huit espaces de noms différents : deux espaces de noms de protocole Internet, deux pour le secours Outlook Web App, un pour la découverte automatique, deux pour l'accès au client RPC et un pour SMTP. Un espace de noms hérité était également nécessaire lors des mises à niveau à partir d'Exchange 2003 ou Exchange 2007. Avec Exchange 2013, le nombre minimum d'espaces de noms passe à deux. En cas de coexistence avec Exchange 2007, vous devez quand même créer un nom d’hôte hérité, mais en cas de coexistence avec Exchange 2010 ou si vous installez une nouvelle organisation Exchange 2013, le nombre minimal d’espaces de nom dont vous avez besoin est de deux : un pour les protocoles clients et un pour la découverte automatique. Vous aurez peut-être aussi besoin d'un espace de noms SMTP.

En conséquence de ces changements d'architecture, certaines modifications ont été apportées à la connectivité client. Tout d'abord, le RPC n'est donc plus un protocole d'accès direct pris en charge. Cela signifie que la connectivité d'Outlook doit être assurée par RPC sur HTTP (autrement dit par le biais d'Outlook Anywhere). Au premier abord, cela peut ressembler à une limitation, mais les avantages supplémentaires sont certains. L'avantage le plus évident est qu'il est inutile d'avoir un service d'accès au client RPC sur le serveur d'accès au client. Il en découle une réduction de deux noms d'espace qui seraient normalement requis par une solution basée sur la résilience de site. En outre, il n'est plus nécessaire de fournir une affinité pour le service d'accès au client RPC.

Ensuite, les clients Outlook ne se connectent plus à nom de domaine complet de serveur comme ils devaient le faire avec des versions précédentes d'Exchange. Outlook utilise la recherche automatique pour créer un point de connexion contenant un GUID de boîte aux lettres, le symbole @ et la partie domaine de l’adresse SMTP principale de l’utilisateur. Ce changement simple permet l'élimination quasi complète du message indésirable « Votre administrateur a apporté des modifications à votre boîte aux lettres. Veuillez redémarrer. » Seul Outlook 2007 et les versions ultérieures sont pris en charge avec Exchange 2013.

Le modèle haute disponibilité du composant de boîte aux lettres n'a pas subi de changement fondamental depuis Exchange 2010. L'unité de haute disponibilité est toujours le groupe de disponibilité de la base de données (DAG). Le DAG utilise toujours des clusters de basculement Windows Server. La réplication continue prend toujours en charge la réplication en mode fichier et en mode bloc. Toutefois, nous avons ajouté quelques améliorations. Les temps de basculement ont été réduits en conséquence d'améliorations apportées au code du journal des transactions, et de l'augmentation de la profondeur du point de contrôle sur les bases de données passives. Le service de banque de Microsoft Exchange a été réécrit en code managé (voir la section « Banque gérée » plus loin dans cette rubrique). Désormais, chaque base de données fonctionne sous son propre processus, ce qui permet d'isoler les problèmes de banque à une seule base de données.

## Banque gérée

Dans Exchange 2013, la *Banque gérée* est le nom donné aux processus de la Banque d'informations nouvellement réécrits : Microsoft.Exchange.Store.Service.exe et Microsoft.Exchange.Store.Worker.exe. La nouvelle Banque gérée est écrite en C\# et elle est étroitement intégrée au Service de réplication Microsoft Exchange (MSExchangeRepl.exe) afin d'améliorer la disponibilité grâce à une meilleure résilience. En outre, la Banque gérée a été conçue pour permettre une gestion plus granulaire de la consommation des ressources et une analyse plus rapide des causes premières à l'aide de diagnostics améliorés.

La Banque gérée fonctionne avec le Service de réplication Microsoft Exchange pour gérer les bases de données de boîtes aux lettres, lequel continue d’utiliser ESE (Extensible Storage Engine) comme moteur de base de données. Exchange 2013 comprend des modifications significatives au schéma de base de données des boîtes aux lettres et se traduit par des optimisations par rapport aux versions précédentes d’Exchange. Outre ces changements, le service de réplication Microsoft Exchange est responsable de la disponibilité des services en rapport avec les serveurs de boîtes aux lettres. Les modifications de l'architecture permettent d'accélérer le basculement des bases de données et d'améliorer la gestion des pannes physiques de disque.

La Banque gérée est également intégrée au moteur de recherche Search Foundation (le même moteur de recherche utilisé par SharePoint 2013) pour fournir des opérations d'indexation et de recherche plus performantes que Microsoft Search dans les versions précédentes d'Exchange.

Pour plus d'informations, consultez la rubrique [Haute disponibilité et résilience de site](high-availability-and-site-resilience-exchange-2013-help.md).

## Gestion des certificats

La gestion des certificats numériques est l'une des tâches de sécurité les plus importantes pour votre organisation Exchange. Il est primordial de s'assurer que les certificats sont configurés de manière appropriée dans le but de fournir une infrastructure de messagerie sécurisée pour l'entreprise. Dans Exchange 2010, la Console de gestion Exchange était la méthode principale de gestion des certificats. Dans Exchange 2013, la fonctionnalité de gestion des certificats est proposée dans le Centre d'administration Exchange, la nouvelle interface utilisateur de l'administrateur Exchange 2013.

En ce qui concerne les certificats, Exchange 2013 minimise leur nombre et les interactions nécessaires afin de réduire la charge de gestion et de temps de l'administrateur. Les certificats sont gérés à partir d'un emplacement central. Les avantages des changements dans la gestion des certificats sont les suivants :

  - La gestion des certificats peut être réalisée sur le serveur d'accès au client ou sur le serveur de boîtes aux lettres. Le serveur de boîtes aux lettres possède un certificat auto-signé installé par défaut. Le serveur d'accès au client approuve automatiquement le certificat auto-signé sur le serveur de boîtes aux lettres Exchange 2013 de sorte que les clients ne reçoivent pas d'avertissement à propos d'un certificat auto-signé non approuvé, à condition que le serveur d'accès au client Exchange 2013 dispose d'un certificat non auto-signé provenant soit d'une autorité de certification Windows, soit d'un tiers approuvé.

  - Dans des versions antérieures d'Exchange, il était difficile de vérifier si un certificat numérique était proche de la date d'expiration. Dans Exchange 2013, le centre de notifications affiche des avertissements lorsqu'un certificat stocké sur l'un des serveurs Exchange 2013 est sur le point d'expirer. Les administrateurs peuvent également choisir de recevoir ces notifications par courrier électronique.

Pour plus d'informations, consultez la rubrique [Certificats numériques et SSL](digital-certificates-and-ssl-exchange-2013-help.md).

## Installation

Le processus d'installation d'Exchange 2013 a été entièrement repensé afin de vérifier facilement que vous disposez des derniers correctifs de sécurité. Voici quelques-unes des améliorations apportées :

  - **Programme d'installation toujours à jour**   Lorsque vous exécutez l'Assistant Installation, il vous sera proposé de télécharger et d'utiliser les derniers correctifs de sécurité et modules linguistiques. Cette option ne fait pas que mettre à jour les fichiers qui seront utilisés pour exécuter Exchange, le programme d’installation lui-même peut être mis à jour. Cette conception nous permet de continuer à améliorer le programme d'installation après le lancement du produit et d'inclure et de mettre à jour les tests de préparation au fur et à mesure des changements ou mises à jour des exigences.
    
    Si vous utilisez le mode d’installation sans assistance, nous ne pouvons pas télécharger automatiquement les mises à jour. Cependant, vous pouvez quand même tirer parti de l'utilisation de la dernière version du programme d'installation en téléchargeant à l'avance les dernières mises à jour, puis en utilisant le paramètre `/UpdatesDir: <path>` pour permettre au programme d'installation de se mettre à jour avant le début du processus d'installation.

  - **Tests de préparation améliorés**   Les tests de préparation permettent de s'assurer que votre ordinateur et votre organisation sont prêts pour Exchange 2013. Après avoir fourni les informations nécessaires au processus d’installation, les tests de préparation sont lancés avant que l’installation ne commence. Le nouveau moteur de vérification de la préparation effectue tous les tests et vous indique les actions à entreprendre avant que l'installation ne continue, et il n'a jamais été aussi rapide. Comme avec les versions précédentes d'Exchange, vous pouvez indiquer au processus d'installation les fonctionnalités Windows à installer pour éviter de le faire manuellement.

  - **Un Assistant simplifié et moderne**   Nous avons supprimé toutes les étapes de l'Assistant Installation qui n'étaient pas absolument nécessaires à l'installation d'Exchange. Il en résulte un Assistant facile à suivre qui vous guide, étape par étape, tout au long du processus d'installation.

Pour plus d'informations, consultez la rubrique [Planification et déploiement](planning-and-deployment-for-exchange-2013-installation-instructions.md).

## Stratégie et conformité de la messagerie

Il y a deux nouvelles fonctionnalités liées à la stratégie et à la conformité de messagerie dans Exchange 2013 : la protection contre la perte de données et le connecteur Microsoft Rights Management.

Les fonctions de *protection contre la perte de données* (DLP) vous aident à protéger vos données sensibles et à informer les utilisateurs au sujet des stratégies internes de conformité. DLP peut aussi protéger votre organisation contre les utilisateurs qui enverraient par inadvertance des informations sensibles à des personnes non autorisées. DLP vous aide à identifier, surveiller et protéger les données sensibles grâce à l'analyse approfondie du contenu. Exchange 2013 offre des stratégies DLP intégrées, basées sur les normes réglementaires comme les normes de sécurité PII (informations d'identification personnelle) et PCI (secteur des cartes de paiement). Le produit peut aussi prendre en charge d'autres stratégies importantes dans votre secteur. En outre, les nouveaux Conseils de stratégie d'Outlook 2013 informent les utilisateurs en cas de violation d'une stratégie, avant que les données sensibles ne soient envoyées.

Le connecteur Microsoft Rights Management (connecteur RMS) est une application facultative qui vous permet d’améliorer la protection des données de votre serveur Exchange 2013 en se connectant à des services Microsoft Rights Management en nuage. Une fois que vous avez installé le connecteur RMS, il protège en continu les données pendant toute la durée de vie des informations et, comme ces services sont personnalisables, vous pouvez définir le niveau de protection dont vous avez besoin. Par exemple, vous pouvez limiter l’accès d’utilisateurs spécifiques à des courriers électroniques ou définir des droits d’affichage seul pour certains messages.

Pour en savoir plus sur ces fonctionnalités, consultez la rubrique suivante :

[Protection contre la perte de données](technical-overview-of-dlp-data-loss-prevention-in-exchange.md)

[Connecteur RMS](https://go.microsoft.com/fwlink/p/?linkid=330432)

## Archive, rétention et découverte électronique locales

Exchange 2013 comprend les améliorations suivantes apportées à l'archivage local, la rétention et la recherche électronique, afin d'aider votre organisation à répondre à ses exigences de conformité :

  - **Archive permanente**   L'archive permanente est un nouveau modèle de blocage unifié qui vous permet de répondre à vos exigences de conservation légale dans les scénarios suivants :
    
      - Conserver les résultats d'une requête (blocage basé sur une requête) qui vous permet une immuabilité portant sur toutes les boîtes aux lettres.
    
      - Mettre en place un blocage pendant un laps de temps afin de répondre aux exigences de rétention (par exemple, rétention de tous les éléments d'une boîte aux lettres pendant sept ans, scénario requérant l'utilisation des paramètres Récupération d'élément unique/Rétention des éléments supprimés dans Exchange 2010).
    
      - Placer une boîte aux lettres en conservation indéfinie (similaire à la mise en attente pour litige d'Exchange 2010).
    
      - Mettre plusieurs fois un utilisateur en attente pour répondre aux besoins de différents scénarios.

  - **Découverte électronique locale**   La découverte électronique locale permet aux utilisateurs autorisés de rechercher des données dans toutes les boîtes aux lettres et les archives sur place dans l'organisation Exchange 2013, et de copier les messages vers une boîte aux lettres de découverte pour révision. Dans Exchange 2013, la découverte électronique locale a été améliorée pour permettre aux gestionnaires de découverte de réaliser des recherches et mises en attentes plus efficaces. Ces améliorations incluent les points suivants :
    
      - La **Recherche fédérée** vous permet de rechercher et de préserver les données dans plusieurs référentiels de données. Avec Exchange 2013, vous pouvez réaliser des découvertes électroniques locales dans Exchange, SharePoint 2013 et Lync 2013. Vous pouvez utiliser le Centre de découverte électronique de SharePoint 2013 pour réaliser une découverte électronique locale et une archive permanente.
    
      - L'**archive permanente basée sur une requête** enregistre les résultats d'une requête, ce qui permet une immuabilité portant sur toutes les boîtes aux lettres.
    
      - **Exporter les résultats de la recherche** Les gestionnaires de découverte peuvent exporter le contenu d'une boîte aux lettres dans un fichier .pst à partir de la Console de découverte électronique SharePoint 2013. Les cmdlets de requête d'export de boîtes aux lettres ne sont plus nécessaires pour exporter une boîte aux lettres dans un fichier .pst.
    
      - **Statistiques de mots clés**   Les statistiques de recherche sont proposées par terme de recherche. Cela permet au gestionnaire de découverte de prendre rapidement des décisions avisées sur la façon d'affiner une requête de recherche afin d'obtenir de meilleurs résultats. Les résultats de recherche électronique sont classés par pertinence.
    
      - **Syntaxe KQL**   Les gestionnaires de découverte peuvent utiliser la syntaxe KQL (Keyword Query Language) dans les requêtes de recherche. KQL ressemble à la Syntaxe de recherche avancée (AQS), qui était utilisée pour les recherches de découverte dans Exchange 2010.
    
      - **Assistant Découverte électronique locale et archive permanente**   Les gestionnaires de découverte peuvent utiliser le nouvel Assistant Découverte électronique locale et archive permanente pour leurs opérations de découverte électronique et d'archive.
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>Si SharePoint 2013 n'est pas disponible, un sous-ensemble de la fonctionnalité de découverte électronique est disponible dans le Centre d'administration Exchange.</td>
        </tr>
        </tbody>
        </table>


  - **Recherche parmi les boîtes aux lettres principales et d'archivage dans Outlook Web App**   Les utilisateurs peuvent rechercher leurs boîtes aux lettres principales et d'archivage dans Outlook Web App. Il n'est plus nécessaire de réaliser deux recherches distinctes.

  - **Archivage de contenu Lync**   Exchange 2013 prend en charge l’archivage du contenu Lync 2013 dans la boîte aux lettres d’un utilisateur. Vous pouvez mettre le contenu Lync en attente à l'aide de l'archive permanente et utiliser la découverte électronique locale pour rechercher le contenu Lync archivé dans Exchange.

  - **Stratégies de rétention**   Les stratégies de rétention aident votre organisation à réduire les risques associés au courrier électronique et à d'autres types de communication, ainsi qu'à répondre aux exigences de rétention de la messagerie électronique. Les stratégies de rétention incluent les améliorations suivantes :
    
      - **Prise en charge des balises de rétention Calendrier et Tâches**   Vous pouvez également créer des balises de stratégie de rétention pour les dossiers Calendrier et Tâches par défaut pour les éléments expirés dans ces dossiers. Les éléments de ces dossiers sont également déplacés vers l’archive de l’utilisateur en fonction des paramètres de stratégie d’archive appliqués à cette boîte aux lettres.
    
      - **Amélioration de la capacité à conserver des éléments pour une période spécifique**   Vous pouvez utiliser la stratégie de rétention et un blocage sur place basé sur le temps pour renforcer la rétention des éléments pour une période donnée.

Pour plus d'informations, consultez la rubrique [Stratégie et conformité de messagerie](messaging-policy-and-compliance-exchange-2013-help.md).

## Règles de transport

Les règles de transport dans Exchange Server 2013 sont une continuation des fonctions disponibles dans Exchange Server 2010. Toutefois, plusieurs améliorations ont été apportées aux règles de transport dans Exchange 2013. Le changement le plus important est la prise en charge de la protection contre la perte de données (DLP). Nous avons également apporté de nouveaux prédicats et actions, une surveillance améliorée et certaines modifications d'architecture.

Pour plus d'informations, consultez [Nouveautés des règles de transport](what-s-new-for-transport-rules-exchange-2013-help.md).

## Gestion des droits relatifs à l'information

La Gestion des droits relatifs à l’information (IRM) est compatible avec Cryptographic Mode 2, mode cryptographique des Services AD RMS (Active Directory Rights Management Services) prenant en charge un chiffrement plus fort en vous permettant d’utiliser les clés 2048 bits pour RSA et les clés 256 bits pour SHA-1. Par ailleurs, Mode 2 vous permet d’utiliser l’algorithme de hachage SHA-2. Pour en savoir plus, consultez la rubrique relative aux [modes cryptographiques AD RMS](https://go.microsoft.com/fwlink/p/?linkid=263219).

## Audit

Exchange 2013 inclut les améliorations suivantes pour l’audit :

  - **Rapports d'audit**   Le Centre d'administration Exchange comprend une fonctionnalité d'audit permettant de générer des rapports ou d'exporter des entrées à partir du journal d'audit de boîte aux lettres et du journal d'audit de l'administrateur. Le journal d'audit de boîte aux lettres enregistre chaque accès à une boîte aux lettres par une personne autre que son propriétaire. Cela peut vous aider à déterminer qui a accédé à une boîte aux lettres et ce qui a été fait. Le journal d'audit de l'administrateur enregistre toute action, selon une cmdlet de l'environnement de ligne de commande Exchange Management Shell, exécutée par un administrateur. Cela peut vous aider à résoudre les problèmes de configuration ou à identifier la cause de problème de sécurité ou de conformité. Pour plus d'informations, consultez la rubrique [Rapports d’audit Exchange](exchange-auditing-reports-exchange-2013-help.md).

  - **Affichage du journal d’audit de l’administrateur**   Au lieu d’exporter le journal d’audit de l’administrateur, dont la réception par message électronique peut prendre jusqu’à 24 heures, vous pouvez afficher les entrées du journal d’audit de l’administrateur dans le CAE. Pour ce faire, accédez à **Gestion de la conformité**\>**Auditing** et cliquez sur **Consulter le journal d’audit de l’administrateur**. Jusqu’à 1 000 entrées s’affichent sur plusieurs pages. Pour affiner la recherche, vous pouvez spécifier une plage de dates. Pour plus d’informations, consultez [Consulter le journal d’audit de l’administrateur](view-the-administrator-audit-log-exchange-2013-help.md).

## Protection anti-programme malveillant

Les capacités anti-programme malveillant intégrées d'Exchange 2013 aident à protéger votre réseau contre les logiciels malveillants transférés par le biais de messages électroniques. Tous les messages envoyés ou reçus par votre serveur Exchange sont scannés à la recherche de programmes malveillants (virus et logiciels espions). Si un programme malveillant est détecté, le message est supprimé. Des notifications peuvent également être envoyées aux expéditeurs ou administrateurs lorsqu'un message infecté est supprimé et n'est pas remis. Vous pouvez choisir de remplacer les pièces jointes infectées par des messages par défaut ou personnalisés qui informent les destinataires de la détection de programmes malveillants.

Pour plus d'informations sur la protection anti-programme malveillant, consultez la rubrique [Détection anti-programmes malveillants](anti-malware-protection-exchange-2013-help.md).

## Flux de messagerie

La façon dont les messages circulent dans une organisation et leur traitement ont radicalement changé dans Exchange 2013. Voici un bref aperçu des changements :

  - **Pipeline de transport**   Le pipeline de transport dans Exchange 2013 est maintenant composé de différents services : le service de transport frontal sur les serveurs d'accès au client, le service de transport sur ​​des serveurs de boîtes aux lettres et le service de transport des boîtes aux lettres sur ​​les serveurs de boîtes aux lettres. Pour plus d'informations, consultez la rubrique [Flux de messagerie](mail-flow-exchange-2013-help.md).

  - **Routage**   Le routage des messages électroniques dans Exchange 2013 reconnaît les limites du DAG ainsi que les limites de site Active Directory. En outre, le routage de messagerie a été amélioré pour mettre les messages en file d'attente de manière plus directe pour les destinataires internes. Pour plus d'informations, consultez la rubrique [Routage du courrier](mail-routing-exchange-2013-help.md).

  - **Connecteurs**   La taille de message maximum par défaut pour un connecteur d'envoi ou de réception, comme indiqué par le paramètre *MaxMessageSize*, est passée de 10 à 25 Mo. Pour plus d'informations sur la configuration des paramètres d'un connecteur, consultez les rubriques [Set-SendConnector](https://technet.microsoft.com/fr-fr/library/aa998294\(v=exchg.150\)) et [Set-ReceiveConnector](https://technet.microsoft.com/fr-fr/library/bb125140\(v=exchg.150\)).
    
    Vous pouvez configurer un connecteur d'envoi dans le service de transport d'un serveur de boîtes aux lettres afin qu'il achemine le courrier sortant par le biais d'un serveur de transport frontal sur le site local Active Directory grâce au paramètre *FrontEndProxyEnabled* de la cmdlet **Set-SendConnector**, consolidant ainsi la façon dont le courrier est acheminé avec le service de transport.

  - **Transport Edge**   Vous pouvez également installer un serveur de transport Edge sur votre réseau de périmètre pour réduire la surface d’attaque et permettre la protection et la sécurité des messages. Pour plus d'informations, consultez la rubrique [Serveurs de transport Edge](edge-transport-servers-exchange-2013-help.md).

## Destinataires

Cette section décrit les améliorations apportées à la gestion des destinataires dans Exchange 2013 :

  - **Stratégie de noms de groupes**   Les administrateurs peuvent maintenant utiliser le Centre d'administration Exchange pour créer une *stratégie de noms de groupes* qui permet de normaliser et de gérer les noms des groupes de distribution créés par les utilisateurs dans votre organisation. Lors de la création d'un groupe de distribution, vous pouvez exiger l'ajout d'un préfixe et d'un suffixe spécifiques au nom, et interdire l'utilisation de mots spécifiques. Cela vous aide à réduire l'utilisation de mots inappropriés dans les noms de groupe.
    
    Pour plus d'informations, consultez la rubrique [Créer une stratégie de noms de groupe de distribution](create-a-distribution-group-naming-policy-exchange-2013-help.md).

  - **Suivi des messages**   Les administrateurs peuvent aussi utiliser le Centre d'administration Exchange pour suivre les informations de remise des messages électroniques envoyés ou reçus par un utilisateur dans votre organisation. Il suffit de sélectionner une boîte aux lettres, puis de rechercher les messages envoyés ou reçus par un utilisateur différent. Vous pouvez restreindre la recherche en entrant des mots spécifiques dans la ligne Objet. Le rapport de remise obtenu suit un message via le processus de remise et spécifie si le message à été remis correctement, si la remise est en attente ou s'il n'a pas été remis.
    
    Pour plus d'informations, consultez la rubrique [Suivre les messages avec des rapports de remise](track-messages-with-delivery-reports-exchange-2013-help.md).

## Partage et collaboration

Cette section décrit les améliorations apportées au partage et à la collaboration dans Exchange 2013.

  - **Dossiers publics**   Les dossiers publics tirent maintenant parti des technologies existantes en matière de haute disponibilité et de stockage dans la banque de boîtes aux lettres. L'architecture de dossiers publics utilise des boîtes aux lettres spécialement conçues pour stocker à la fois la hiérarchie et les contenus des dossiers publics. Cette nouvelle conception implique également qu'il n'y a plus de base de données de dossiers publics. La réplication des dossiers publics utilise désormais le modèle de réplication continue. La haute disponibilité de la hiérarchie et du contenu des boîtes aux lettres est assurée par le groupe de disponibilité de base de données (DAG). Avec cette conception, nous passons d'un modèle de réplication à plusieurs maîtres à un modèle de réplication à un seul maître.
    
    Les utilisateurs d’Outlook Web App dans votre organisation ont désormais la possibilité d’ajouter des dossiers publics à leurs favoris ou d’en supprimer. Auparavant, cette opération pouvait uniquement être effectuée dans Outlook.
    
    Pour plus d'informations, consultez la rubrique [Dossiers publics](public-folders-exchange-2013-help.md).

  - **Boîtes aux lettres de site**   Les messages électroniques et les documents sont généralement conservés dans deux référentiels de données uniques et séparés. La plupart des équipes collaborent en général en utilisant ces deux supports. Le défi est que les utilisateurs accèdent généralement aux messages électroniques et aux documents à l'aide de différents clients, ce qui réduit leur productivité et détériore leur expérience.
    
    La *boîte aux lettres de site* est un nouveau concept d'Exchange 2013 pour tenter de résoudre ces problèmes. Les boîtes aux lettres de site améliorent la collaboration et la productivité des utilisateurs en permettant l'accès à la fois aux documents sur un site SharePoint et dans des messages électroniques Outlook 2013, en utilisant la même interface client. Une boîte aux lettre de site se compose de l'appartenance à un site SharePoint (propriétaires et membres), un stockage partagé par le biais d'une boîte aux lettres Exchange pour des messages électroniques et un site SharePoint pour des documents, ainsi qu'une interface de gestion qui répond aux besoins de configuration et de cycle de vie.
    
    Pour plus d'informations, consultez la rubrique [Boîtes aux lettres de site](site-mailboxes-exchange-2013-help.md).

  - **Boîtes aux lettres partagées**   Dans des versions précédentes d'Exchange, la création d'une boîte aux lettres partagée était un processus en plusieurs étapes dans lequel vous deviez utiliser l'environnement de ligne de commande Exchange Management Shell pour définir les autorisations des délégués. Dans Exchange 2013, vous pouvez maintenant créer une boîte aux lettres partagée en une étape par le biais du Centre d'administration Exchange. Dans le Centre d’administration Exchange, accédez à **Destinataires**\>**Boîtes aux lettres partagées** pour créer une boîte aux lettres partagée. Une boîte aux lettres partagée est maintenant un type de destinataire. Vous pouvez ainsi facilement rechercher vos boîtes aux lettres partagées soit avec l'interface utilisateur, soit à l'aide de l'environnement de ligne de commande Exchange Management Shell.
    
    Pour plus d'informations, consultez la rubrique [Boîtes aux lettres partagées](shared-mailboxes-exchange-2013-help.md).

## Intégration à SharePoint et Lync

Exchange 2013 offre une meilleure intégration avec SharePoint 2013 et Lync 2013. Les avantages de cette intégration améliorée comprennent :

  - Exchange 2013 s'intègre à SharePoint 2013 pour permettre aux utilisateurs de collaborer de manière plus efficace en utilisant les boîtes aux lettres de site.

  - Lync Server 2013 peut archiver le contenu dans Exchange 2013 et utiliser Exchange 2013 en tant que magasin de contacts.

  - Les gestionnaires de découverte peuvent réaliser des découvertes électroniques locales et des archives permanentes dans les données SharePoint 2013, Exchange 2013 et Lync 2013.

  - L'authentification OAuth autorise les applications partenaires à s'authentifier en tant que service ou à assumer l'identité d'utilisateurs selon les besoins.

Pour plus d'informations, consultez la rubrique [Intégration à SharePoint et Lync](integration-with-sharepoint-and-lync-exchange-2013-help.md).

## Clients et mobilité

L'interface utilisateur Outlook Web App est nouvelle et optimisée pour les tablettes et smartphones, mais aussi pour les ordinateurs de bureau et portables. Les nouvelles fonctionnalités comprennent des applications pour Outlook qui permettent aux utilisateurs et aux administrateurs d'étendre les capacités d'Outlook Web App : liens de contacts, possibilité pour les utilisateurs d'ajouter des contacts à partir de leurs comptes LinkedIn et mises à jour de l'affichage et des fonctionnalités du calendrier.

Pour plus d'informations, consultez la rubrique [Nouveautés Outlook Web App dans Exchange 2013](what-s-new-for-outlook-web-app-in-exchange-2013-exchange-2013-help.md).

## Messagerie unifiée

La messagerie unifiée d'Exchange 2013 contient globalement les mêmes fonctionnalités de messagerie vocale qu'Exchange 2010. Cependant, certaines fonctions ont été améliorées et d'autres ont été ajoutées. Plus important encore, des changements d'architecture dans la messagerie unifiée d'Exchange 2013 ont engendré la division de composants, services et fonctionnalités inclus dans le rôle serveur de messagerie unifiée d'Exchange 2010. Ce rôle est maintenant réparti entre le rôle serveur de boîte aux lettres et le rôle serveur d'accès au client Exchange 2013.

Pour plus d'informations, consultez la rubrique [Nouveautés de la messagerie unifiée Exchange 2013](what-s-new-for-unified-messaging-in-exchange-2013-exchange-2013-help.md).

## Déplacements par lot de boîtes aux lettres

Exchange 2013 introduit le concept de déplacements par lot. La nouvelle architecture de déplacement est conçue sur les déplacements du service de réplication de boîte aux lettres avec amélioration de la capacité de gestion. La nouvelle architecture de déplacement par lot présente les améliorations suivantes :

  - Possibilité de déplacer un grand nombre de boîtes aux lettres par lots.

  - Notification par courrier électronique lors du déplacement avec rapports.

  - Nouvelle tentative automatique et priorisation automatique des déplacements.

  - Les boîtes aux lettres d'archivage principales et personnelles peuvent être déplacées ensemble ou séparément.

  - Un option permet de finaliser une demande manuelle de déplacement, afin de vérifier le déplacement avant de l'effectuer.

  - Synchronisation incrémentielle périodique pour migrer les modifications.

Pour plus d'informations, consultez la rubrique [Gestion des déplacements locaux](manage-on-premises-moves-exchange-2013-help.md).

## Haute disponibilité et résilience de site

Exchange 2013 utilise des groupe de disponibilité de base de données et des copies de bases de données de boîtes aux lettres, en plus d'autres fonctionnalités comme la récupération d'élément unique, les stratégies de rétention et les copies de bases de données retardées pour fournir la haute disponibilité, la résilience de site et la protection des données native d'Exchange. La plate-forme de haute disponibilité, la Banque d'informations Exchange et le Moteur de stockage extensible (ESE) ont tous été améliorés pour offrir une plus grande disponibilité, une gestion plus facile et des coûts réduits. Ces améliorations incluent les points suivants :

  - **Disponibilité gérée**   Avec la disponibilité gérée, la surveillance interne et les fonctionnalités orientées récupération sont étroitement intégrées afin d'aider à prévenir les pannes, à restaurer proactivement les services et à initialiser les basculements automatiques de serveurs ou à alerter les administrateurs afin qu'ils prennent des mesures. L'accent est mis sur le suivi et la gestion de l'expérience de l'utilisateur final plutôt que simplement sur la durée d'exécution du serveur et des composants pour aider à maintenir une disponibilité permanente du service.

  - **Banque gérée**   La Banque gérée est le nom donné aux processus de la Banque d'informations qui ont été réécrits sous Exchange 2013. La nouvelle Banque gérée est écrite en C\# et elle est étroitement intégrée avec le Service de réplication Microsoft Exchange (MSExchangeRepl.exe) afin de fournir une plus grande disponibilité grâce à une résilience accrue.

  - **Prise en charge de bases de données multiples par disque**   Exchange 2013 comprend des améliorations qui vous permettent de prendre en charge les bases de données multiples (mélange de copies actives et passives) sur le même disque, ce qui améliore l'efficacité des disques en tirant parti d'une plus grande capacité et d'un nombre d'opérations d'E/S par seconde accru.

  - **Réamorçage automatique**   Il vous permet de restaurer rapidement la redondance des bases de données après une panne de disque. Si un disque tombe en panne, la copie de la base de données stockée sur ce disque est copiée à partir de la copie de base de données active vers un disque de rechange sur le même serveur. Si plusieurs copies de bases de données ont été stockées sur le disque défectueux, elles peuvent toutes être automatiquement réamorcées sur un disque de rechange. Cela permet des réamorçages plus rapides, car les bases de données actives se trouvent probablement sur de multiples serveurs et les données sont copiées de manière parallèle.

  - **Récupération automatique après défaillance du stockage**   Cette fonctionnalité se situe dans la continuité des innovations lancées par Exchange 2010 afin de permettre une récupération système après des défaillances qui affectent la résilience ou la redondance. En plus des vérifications d’erreur d’Exchange 2010, Exchange 2013 présente des fonctionnalités supplémentaires de récupération pour les temps d’E/S élevés, la consommation excessive de mémoire par MSExchangeRepl.exe, et les cas extrêmes où le système est dans un tel état que les threads ne peuvent pas être planifiés.

  - **Améliorations apportées aux copies retardées**   Les copies retardées se gèrent de manière plus autonome grâce à l'exécution de la journalisation automatique. Les copies retardées lisent automatiquement les fichiers journaux dans différentes situations, telles que la restauration d'une seule page et les scénarios d'espace disque faible. Si le système détecte que la mise à jour corrective de page est nécessaire pour une copie retardée, les journaux seront automatiquement relus dans la copie retardée pour appliquer les mises à jour correctives. Les copies retardées invoqueront également cette fonction de relecture automatique lorsque le seuil d'espace disque insuffisant a été atteint et lorsque la copie retardée a été détectée comme étant la seule copie disponible pour une période spécifique. De plus, les copies retardées peuvent tirer parti de Safety Net, ce qui facilite la récupération ou l'activation. *Safety Net*, fonctionnalité améliorée dans Exchange 2013, est basée sur la benne de transport d'Exchange 2010.

  - **Améliorations apportées aux alertes de copie unique**   L'alerte de copie unique introduite dans Exchange 2010 n'est plus un script planifié de manière séparée. Elle est maintenant intégrée aux composants de disponibilité gérée au sein du système et il s’agit d’une fonction native dans Exchange.

  - **Auto-configuration du réseau des DAG**   Les groupes de disponibilité des bases de données (DAG) peuvent être automatiquement configurés par le système en fonction des paramètres de configuration. En plus des options de configuration manuelle, les DAG peuvent aussi faire la distinction entre les réseaux de réplication et MAPI, et sont capables de configurer des réseaux DAG automatiquement.

Pour plus d’informations sur ces deux fonctionnalités, consultez les rubriques [Haute disponibilité et résilience de site](high-availability-and-site-resilience-exchange-2013-help.md) et [Modifications apportées à la haute disponibilité et la résilience de site par rapport aux versions précédentes](changes-to-high-availability-and-site-resilience-over-previous-versions-exchange-2013-help.md).

## Gestion de la charge de travail Exchange

Une charge de travail Exchange est une fonctionnalité, un protocole ou un service de serveur Exchange explicitement défini a des fins de gestion des ressources système Exchange. Chaque charge de travail Exchange consomme des ressources système comme le processeur, des opérations de base de données de boîtes aux lettres ou des requêtes Active Directory afin d'exécuter des requêtes utilisateur ou un travail d'arrière-plan. Des exemples de charges de travail Exchange comprennent notamment Outlook Web App, Exchange ActiveSync, la migration des boîtes aux lettres et les assistants de boîtes aux lettres.

Il existe deux façons de gérer les charges de travail Exchange dans Exchange 2013 :

  - **Surveiller l'état des ressources système**   La gestion des charges de travail en fonction de l'état des ressources système est une nouvelle fonctionnalité d'Exchange 2013.

  - **Contrôle de la consommation des ressources par des utilisateurs individuels**   Le contrôle de la consommation des ressources par des utilisateurs individuels était possible sous Exchange 2010 (on parlait de limitation des utilisateurs), et cette fonctionnalité a été développée pour Exchange 2013.

Pour plus d'informations sur ces fonctionnalités, consultez la rubrique [Gestion de la charge de travail Exchange](exchange-workload-management-exchange-2013-help.md).

