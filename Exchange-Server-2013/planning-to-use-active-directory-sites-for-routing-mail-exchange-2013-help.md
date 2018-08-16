---
title: 'Planif. de l’utilisation de sites AD pr le routage de messages: Exchange 2013'
TOCTitle: Planification de l’utilisation de sites Active Directory pour le routage de messages
ms:assetid: 0f697cee-bcaa-4c69-b80c-7a2afd1817d2
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Aa996299(v=EXCHG.150)
ms:contentKeyID: 52062937
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Planification de l’utilisation de sites Active Directory pour le routage de messages

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2013-05-21_

Microsoft Exchange Server 2013 reconnaît les groupes de disponibilité de base de données (DAG) et les sites Active Directory comme limites de routage. Toutefois, Exchange 2013 utilise encore la topologie du site Active Directory pour déterminer la manière dont les messages sont transportés entre les serveurs Exchange dans différents DAG ou sites au sein de l'organisation. Pour plus d'informations, consultez la rubrique [Routage du courrier](mail-routing-exchange-2013-help.md).

Le service de transport sur un serveur de boîtes aux lettres assure le transport de messages à l'intérieur de l'organisation Exchange. Lorsque vous déployez une organisation Exchange 2013 pure, ou que vous introduisez Exchange 2013 dans une organisation Exchange Server 2010 pure, aucune configuration supplémentaire n'est requise pour établir le routage dans la forêt.

**Contenu de cette rubrique**

Utilisation par Exchange 2013 appartenance au site Active Directory

Détermination de l'appartenance au site Active Directory

Vue d'ensemble des liens de sites IP

Placement d'un serveur Exchange 2013 dans des sites Active Directory

## Utilisation par Exchange 2013 appartenance au site Active Directory

Exchange 2013 est une application sensible au site. Les applications sensibles au site peuvent déterminer leur propre appartenance au site Active Directory ainsi que l'appartenance au site d'autres serveurs en interrogeant Active Directory. Exchange 2013 utilise l'appartenance au site pour déterminer les contrôleurs de domaine et serveurs de catalogue global à utiliser pour traiter les requêtes d'Active Directory. En outre, quand un serveur exécutant Exchange doit déterminer l'adhésion au site Active Directory d'un autre serveur Exchange, il peut interroger Active Directory pour extraire le nom du site.

Dans Exchange 2013, le service de topologie Active Directory Microsoft Exchange est responsable de la mise à jour de l'attribut de site de l'objet serveur Exchange. Comme l'appartenance au site Active Directory est un attribut d'objet serveur, Exchange n'a pas à interroger le DNS pour résoudre une adresse de serveur en un sous-réseau associé à un site Active Directory. Le marquage de l'attribut de site Active Directory sur un objet serveur Exchange permet d'attribuer l'appartenance au site Active Directory à un serveur n'appartenant pas au domaine, tel qu'un serveur de transport Edge abonné.

Les rôles de serveur Exchange 2013 utilisent les informations d'appartenance au site Active Directory comme suit :

  - **Dépôt de courrier**   Le service de dépôt de transport de boîtes aux lettres sur un serveur de boîtes aux lettres Exchange 2013 utilise les informations d'appartenance au site Active Directory pour déterminer les autres serveurs de boîtes aux lettres Exchange 2013 figurant dans le même site Active Directory. Si le serveur de boîtes aux lettres n'appartient pas à un DAG, ou si le DAG ne s'étend pas sur plusieurs sites Active Directory, le service de dépôt de transport de boîtes aux lettres sur le serveur de boîtes aux lettres source soumet les messages à router et à transporter au service de transport sur un serveur de boîtes aux lettres Exchange 2013 situé dans le même site Active Directory.

  - **Remise du courrier**   Le service de transport sur un serveur de boîtes aux lettres Exchange 2013 effectue une résolution de destinataire et interroge Active Directory pour mettre en correspondance une adresse de messagerie avec un compte de destinataire. Les informations du compte du destinataire incluent le nom de domaine complet (FQDN) de la base de données de boîtes aux lettres de l'utilisateur. Le service de transport interroge Active Directory pour déterminer le site Active Directory de la de la base de données de boîtes aux lettres de l'utilisateur. Si la base de données de boîtes aux lettres n'appartient pas à un DAG, il remet le message à ce serveur de boîtes aux lettres. Sinon, il relaie le message pour remise vers un autre serveur de boîtes aux lettres appartenant au même site que le serveur de boîtes aux lettres cible.

  - **Routage des messages**   Le service de transport sur des serveurs de boîtes aux lettres Exchange 2013 extrait des informations d'Active Directory pour déterminer comment le courrier doit être routé à l'intérieur de l'organisation. Exchange 2013 utilise le concept de *groupes de remise* pour déterminer où et quand router des messages. Selon la destination, le message peut être routé vers le service de transport ou le service de remise de transport de boîtes aux lettres sur un serveur de boîtes aux lettres Exchange 2013, ou vers un serveur de transport Hub exécutant une version antérieure d'Exchange. Pour plus d'informations, consultez la rubrique [Routage du courrier](mail-routing-exchange-2013-help.md).

  - **Dépôt de message de messagerie unifiée**   Le service de messagerie unifiée sur les serveurs de boîtes aux lettres Exchange 2013 utilise les informations d'appartenance au site Active Directory pour rechercher les autres serveurs de boîtes aux lettres figurant dans le même site Active Directory. Le service de messagerie unifiée dépose les messages à router au service de transport sur un serveur de boîtes aux lettres au sein du même site Active Directory. Le serveur du service de transport effectue une résolution de destinataire et interroge Active Directory pour établir une correspondance de numéro de téléphone, de numéro E.164 ou d'adresse SIP avec un compte de destinataire. Une fois la résolution du destinataire terminée, le service de transport remet le message à la boîte aux lettres cible de la même manière qu'un message électronique normal.

  - **Connexions client au serveur d'accès au client**   Quand le serveur d'accès au client reçoit une demande de connexion d'utilisateur, il interroge Active Directory pour identifier le serveur de boîtes aux lettres hébergeant la boîte aux lettres de l'utilisateur. Le serveur d'accès au client extrait ensuite l'appartenance au site Active Directory de ce serveur de boîtes aux lettres, puis transmet par proxy la connexion au serveur de boîtes aux lettres.

## Détermination de l'appartenance au site Active Directory

Les clients Active Directory supposent l'appartenance au site en mettant en correspondance l'adresse IP qui leur est attribuée avec un sous-réseau défini dans Sites et services Active Directory et associé à un site Active Directory. Le client utilise ensuite ces informations pour identifier les contrôleurs de domaine et les serveurs de catalogue global présents dans ce site, puis communique avec ces serveurs d'annuaire à des fins d'authentification et d'autorisation. Exchange 2013 tire parti de cette relation en préférant également extraire des informations sur les destinataires des serveurs d'annuaire figurant dans le même site que le serveur Exchange 2013.

Tous les ordinateurs faisant partie du même site Active Directory sont considérés comme bien connectés via une connexion réseau à grande vitesse et fiable. Par défaut, quand une forêt Active Directory est déployée pour la première fois, elle ne contient qu'un seul site nommé `Default-First-Site-Name`. Si l'administrateur ne configure aucun autre site manuellement, tous les ordinateurs serveurs et clients de la forêt sont considérés comme appartenant au `Default-First-Site-Name`.

Quand plusieurs sites sont définis, l'administrateur Active Directory doit définir les sous-réseaux présents dans l'organisation et les associer à des sites Active Directory.

Le service de topologie Active Directory Microsoft Exchange contrôle l'attribut d'appartenance au site sur l'objet serveur Exchange au démarrage du serveur. Si l'attribut du site doit être mis à jour, le service de topologie Active Directory Microsoft Exchange marque l'attribut à l'aide de la nouvelle valeur. Le service de topologie Active Directory Microsoft Exchange vérifie la valeur d'attribut du site toutes les 15 minutes, et met à jour la valeur si l'appartenance au site a changé. Le service de topologie Active Directory Microsoft Exchange utilise le service Net Logon pour obtenir les informations d'appartenance au site actuelles. Le service Net Logon met à jour l'appartenance au site toutes les cinq minutes. Cela signifie qu'une période de latence pouvant atteindre 20 minutes s'écoule entre le moment auquel l'appartenance au site change et celui auquel la nouvelle valeur est marquée sur l'attribut du site.

## Vue d'ensemble des liens de sites IP

Les relations entre sites Active Directory sont définies par des liens de sites IP. Un lien de sites IP se compose d'au moins deux sites Active Directory. Tous les sites Active Directory faisant partie du lien communiquent au même coût. Les propriétés de lien de sites IP incluent une affectation de coût, un planning et un intervalle. Les propriétés de planification et d'intervalle sont utilisées uniquement pour déterminer la fréquence de réplication Active Directory. Exchange 2013 utilise l'affectation des coûts pour déterminer la route la moins coûteuse à suivre pour le trafic quand il existe plusieurs itinéraires vers la destination. Le coût de la route est déterminé en agrégeant le coût de tous les liens de sites dans un trajet de transmission. L'administrateur Active Directory attribue le coût à un lien en fonction de la vitesse relative du réseau et de la bande passante disponible par rapport à d'autres connexions disponibles.

Par défaut, le service de transport sur un serveur de boîtes aux lettres tente toujours d'établir une connexion directe avec le service de transport ou le service de remise de transport de boîtes aux lettres sur un serveur de boîtes aux lettes figurant dans un autre site Active Directory. Les messages transportés ne sont pas relayés via le service de transport sur chaque boîte aux lettres figurant dans un itinéraire de lien de sites. Toutefois, des serveurs de boîtes aux lettres figurant dans des sites Active Directory intermédiaires le long de l'itinéraire de routage peuvent relayer un message dans les scénarios suivants :

  - Le relais direct entre serveurs de boîtes aux lettres n'a pas lieu s'il existe un site hub le long de l'itinéraire de routage le moins coûteux. Vous pouvez configurer un site Active Directory comme site hub de façon à ce que les messages soient routés via le site hub avant d'être relayés vers le serveur cible. Les sites concentrateurs sont décrits plus bas dans cette rubrique.

  - Exchange 2013 utilise l'itinéraire de routage dérivé des informations de lien de sites IP en cas d'échec de communication avec le site Active Directory de destination. Si aucun serveur de boîtes aux lettres dans le site Active Directory de destination ne répond, la remise des messages remonte le long de l'itinéraire de routage le moins coûteux jusqu'à ce qu'une connexion soit établie avec un serveur de boîtes aux lettres dans un site Active Directory le long de l'itinéraire de routage. Les messages sont mis en file d'attente dans ce site Active Directory, et la file d'attente est en état de nouvelle tentative. Ce comportement est nommé *file d'attente au point de défaillance*.

  - Dans les organisations Exchange 2013 dépourvues de DAG, le service de transport sur un serveur de boîtes aux lettres peut également utiliser les informations de lien de sites IP pour optimiser le routage des messages envoyés à plusieurs destinataires. Le serveur de boîtes aux lettres retarde la bifurcation des messages jusqu'à atteindre un embranchement dans les itinéraires de routage vers les destinataires. Le message bifurqué est relayé vers la destination de chaque destinataire par un serveur de boîtes aux lettres dans le site Active Directory, qui représente l'embranchement dans les itinéraires de routage individuels. Cette fonctionnalité est appelée *distribution ramifiée retardée*.

## Désignation des sites hub

La cmdlet **Set-AdSite** permet de configurer un site Active Directory comme site hub. Quand il existe un site hub le long du chemin de routage le moins coûteux entre deux serveurs de transport, les messages sont routés via le site hub pour traitement avant d'être relayés vers le site de destination. Pour que ce comportement de routage ait lieu, le site hub doit figurer le long du chemin de routage le moins coûteux entre deux serveurs de transport. Cette configuration est appropriée uniquement si la topologie du réseau l'exige, par exemple, s'il y a des pare-feu entre des sites Active Directory, qui empêchent le relais direct des communications SMTP. Pour plus d'informations, consultez la rubrique [Configurer les paramètres de routage de messagerie Exchange dans Active Directory](configure-exchange-mail-routing-settings-in-active-directory-exchange-2013-help.md).

## Définition d'un coût spécifique d'Exchange sur un lien de sites IP

La cmdlet **Set-AdSiteLink** dans l'environnement de ligne de commande permet de configurer un coût spécifique d'Exchange pour un lien de sites IP Active Directory. Le coût spécifique d'Exchange est un attribut séparé utilisé à la place du coût attribué à Active Directory pour déterminer l'itinéraire de routage Exchange. Cette configuration est utile quand les coûts de lien de sites IP Active Directory ne permettent pas d'obtenir une topologie de routage de messages Exchange optimale. Pour plus d'informations, consultez la rubrique [Configurer les paramètres de routage de messagerie Exchange dans Active Directory](configure-exchange-mail-routing-settings-in-active-directory-exchange-2013-help.md).

## Définition de restrictions de taille de message sur les liens de sites IP

Par défaut, Exchange 2013 n'impose pas de limite de taille aux messages relayés entre des serveurs de boîtes aux lettres figurant dans sites Active Directory différents. Si vous utilisez la cmdlet **Set-AdSiteLink** pour configurer une taille de message maximale sur un lien de sites IP Active Directory, le routage génère une notification d'échec de remise (NDR) pour tout message dont la taille est supérieure à la taille de message maximale configurée sur tout lien de sites Active Directory dans le chemin de routage le moins coûteux. Cette configuration est utile pour restreindre la taille des messages envoyés à des sites Active Directory distants qui doivent communiquer via des connexions à faible bande passante.

## Placement d'un serveur Exchange 2013 dans des sites Active Directory

Pour que le routage des messages entre serveurs Exchange 2013 se produise correctement, tous les serveurs Exchange déployés dans la forêt doivent appartenir à un site Active Directory. Assurez-vous que les adresses IP affectées se trouvent dans des sous-réseaux correctement associés à des sites Active Directory.

La première étape de planification du placement de serveurs Exchange 2013 dans la topologie du site Active Directory consiste à consigner la topologie actuelle. Votre documentation doit englober les aspects suivants :

  - sites ;

  - sous-réseaux et leur association au site ;

  - liens de sites IP et leurs sites membres ;

  - coûts des liens de sites IP ;

  - serveurs d'annuaire dans chaque site ;

  - connexions réseau physiques ;

  - emplacements des pare-feu.

Après avoir schématisé ces objets, planifiez le placement des serveurs Exchange. Tenez compte des informations suivantes lorsque vous placez les serveurs :

  - Pour pouvoir effectuer des recherches Active Directory, un serveur de boîtes aux lettres doit pouvoir communiquer directement avec un serveur de catalogue global.

  - Nous vous recommandons de déployer plusieurs serveurs de boîtes aux lettres dans chaque site Active Directory pour assurer l'équilibrage de charge et la tolérance de panne.

  - DAG et résilience de site

  - Le service de messagerie unifiée sur des serveurs de boîtes aux lettres dépose des messages vocaux au service de transport sur des serveurs de boîtes aux lettres en vue de leur remise à des boîtes aux lettres. Le serveur d'accès au client exécutant le service routeur d'appels de messagerie unifiée peut se trouver dans un site hub ou à proximité d'une passerelle IP ou VoIP, d'un PBX IP, d'un PBX compatible SIP ou de contrôleurs de frontière de session (SBC). Le service de transport sur un serveur de boîtes aux lettres ayant la même appartenance au site que le serveur d'accès au client reçoit les messages vocaux à transporter et router vers le service de transport sur d'autres serveurs de boîtes aux lettres au sein de l'organisation.

  - Les serveurs d'accès au client offrent un point de connectivité avec l'organisation Exchange pour les utilisateurs qui accèdent à Exchange à distance. Un serveur d'accès au client doit être déployé dans chaque site Active Directory contenant des serveurs de boîtes aux lettres.

Après avoir planifié le placement de votre serveur Exchange 2013, vous pouvez identifier des domaines où il est possible de modifier la topologie du site Active Directory afin d'améliorer le flux de communication. Vous pouvez ajuster les liens de sites IP et les coûts de liens de sites pour optimiser la remise du courrier. Une topologie Active Directory efficace ne nécessite aucune modification pour prendre en charge Exchange 2013.

