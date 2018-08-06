---
title: 'Exchange 2013: ports réseau pr clients et flux de messag.: Exchange 2013 Help | Microsoft Docs'
TOCTitle: Ports réseau pour les clients et le flux de messagerie dans Exchange 2013
ms:assetid: fec09455-e99e-42eb-8b32-1ddc08d9a19e
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb331973(v=EXCHG.150)
ms:contentKeyID: 64118122
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Ports réseau pour les clients et le flux de messagerie dans Exchange 2013

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2016-12-09_

Cette rubrique fournit des informations sur les ports réseau utilisés par MicrosoftExchange Server 2013 pour la communication avec les clients de messagerie, les serveurs de messagerie Internet et autres services extérieurs à votre organisation Exchange locale. Avant d’aborder ce sujet en détail, saisissons d’abord les règles de base suivantes :

  - Nous ne prenons pas en charge la restriction ou l’altération du trafic réseau entre les serveurs Exchange internes, entre les serveurs Exchange internes et les serveurs Lync ou Skype Entreprise internes, ou entre les serveurs Exchange internes et les contrôleurs de domaine Active Directory internes dans toutes les topologies, quel qu’en soit le type. Si vous disposez de pare-feu ou de périphériques réseau pouvant potentiellement limiter ou altérer ce type de trafic réseau, vous devez configurer des règles autorisant la communication libre et illimitée entre ces serveurs (règles autorisant le trafic réseau entrant et sortant sur tous les ports, y compris les ports RPC aléatoires, et tous les protocoles ne modifiant jamais de bits sur le câble).

  - Les serveurs de transport Edge sont presque toujours situés dans un réseau de périmètre, il est donc prévu de restreindre le trafic réseau entre le serveur de transport Edge et Internet, et entre le serveur de transport Edge et votre organisation Exchange interne. Ces ports réseau sont décrits dans cette rubrique.

  - Il est prévu de restreindre le trafic réseau entre les clients et services externes et votre organisation Exchange interne. Il convient également de décider de limiter ou non le trafic réseau entre les clients internes et les serveurs Exchange internes. Ces ports réseau sont décrits dans cette rubrique.

**Contenu de cette rubrique**

Ports réseau requis pour les clients et services

Ports réseau requis pour le flux de messagerie (aucun serveur de transport Edge)

Ports réseau requis pour le flux de messagerie avec des serveurs de transport Edge

Ports réseau requis pour les déploiements hybrides

Ports réseau requis pour la messagerie unifiée

## Ports réseau requis pour les clients et services

Les ports réseau nécessaires pour que les clients de messagerie accèdent aux boîtes aux lettres et aux autres services de l’organisation Exchange sont décrits dans le schéma et le tableau ci-après.

**Remarques :** 

  - La destination de ces clients et services est un serveur d’accès au client. Il peut s’agir d’un serveur d’accès au client autonome, ou d’un serveur d’accès au client et d’un serveur de boîtes aux lettres installé sur le même ordinateur.

  - Bien que les clients et services décrits dans le schéma proviennent d’Internet, les concepts sont les mêmes pour les clients internes (par exemple, les clients d’une forêt de comptes qui accèdent aux serveurs Exchange dans une forêt de ressources). De la même manière, le tableau ne comporte pas de colonne source, car la source peut être n’importe quel emplacement extérieur à l’organisation Exchange (par exemple, Internet ou une forêt de comptes).

  - Les serveurs de transport Edge ne sont pas impliqués dans le trafic réseau associé à ces clients et services.

![Ports réseau requis pour les clients et services](images/Bb331973.f5ba3439-f001-43c8-848e-0e3fd0fce931(EXCHG.150).png "Ports réseau requis pour les clients et services")


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Objectif</th>
<th>Ports</th>
<th>Commentaires</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Des connexions web chiffrées sont utilisées par les services et clients suivants :</p>
<ul>
<li><p>Service de découverte automatique</p></li>
<li><p>Exchange ActiveSync</p></li>
<li><p>Services Web Exchange (EWS)</p></li>
<li><p>Distribution du Carnet d’adresses en mode hors connexion</p></li>
<li><p>Outlook Anywhere (RPC sur HTTP)</p></li>
<li><p>Outlook MAPI sur HTTP</p></li>
<li><p>Outlook Web App</p></li>
</ul></td>
<td><p>443/TCP (HTTPS)</p></td>
<td><p>Pour plus d’informations sur ces clients et services, consultez les rubriques suivantes :</p>
<ul>
<li><p><a href="autodiscover-service-for-exchange-2013.md">Service de découverte automatique</a></p></li>
<li><p><a href="exchange-activesync-exchange-2013-help.md">Exchange ActiveSync</a></p></li>
<li><p><a href="https://go.microsoft.com/fwlink/?linkid=529544">Référence EWS pour Exchange</a></p></li>
<li><p><a href="offline-address-books-exchange-2013-help.md">Carnets d’adresses en mode hors connexion</a></p></li>
<li><p><a href="outlook-anywhere-exchange-2013-help.md">Outlook Anywhere</a></p></li>
<li><p><a href="mapi-over-http-exchange-2013-help.md">MAPI sur HTTP</a></p></li>
<li><p><a href="what-s-new-for-outlook-web-app-in-exchange-2013-exchange-2013-help.md">Nouveautés Outlook Web App dans Exchange 2013</a></p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Des connexions web non chiffrées sont utilisées par les services et clients suivants :</p>
<ul>
<li><p>Publication de calendriers Internet</p></li>
<li><p>Outlook Web App (redirection vers 443/TCP)</p></li>
<li><p>Découverte automatique (secours lorsque 443/TCP n’est pas disponible)</p></li>
</ul></td>
<td><p>80/TCP (HTTPS)</p></td>
<td><p>Si possible, nous recommandons d’utiliser des connexions web chiffrées 443/TCP afin de protéger les données et les informations d’identification. Toutefois, vous pouvez constater que certains services doivent être configurés pour utiliser des connexions web non chiffrées 80/TCP sur le serveur d’accès au client.</p>
<p>Pour plus d’informations sur ces clients et services, consultez les rubriques suivantes :</p>
<ul>
<li><p><a href="enable-internet-calendar-publishing-exchange-2013-help.md">Activer la publication Internet des calendriers</a></p></li>
<li><p><a href="what-s-new-for-outlook-web-app-in-exchange-2013-exchange-2013-help.md">Nouveautés Outlook Web App dans Exchange 2013</a></p></li>
<li><p><a href="autodiscover-service-for-exchange-2013.md">Service de découverte automatique</a></p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Clients IMAP4</p></td>
<td><p>143/TCP (IMAP), 993/TCP (IMAP sécurisé)</p></td>
<td><p>IMAP4 est désactivé par défaut. Pour plus d’informations, voir <a href="pop3-and-imap4-in-exchange-server-2013-exchange-2013-help.md">POP3 et IMAP4 dans Exchange Server 2013</a>.</p>
<p>Le service IMAP4 sur le serveur d’accès au client envoie par proxy les connexions au service principal IMAP4 sur un serveur de boîtes aux lettres.</p></td>
</tr>
<tr class="even">
<td><p>Clients POP3</p></td>
<td><p>110/TCP (POP3), 995/TCP (POP3 sécurisé)</p></td>
<td><p>POP3 est désactivé par défaut. Pour plus d’informations, voir <a href="pop3-and-imap4-in-exchange-server-2013-exchange-2013-help.md">POP3 et IMAP4 dans Exchange Server 2013</a>.</p>
<p>Le service POP3 sur le serveur d’accès au client envoie par proxy les connexions au service principal POP3 sur un serveur de boîtes aux lettres.</p></td>
</tr>
<tr class="odd">
<td><p>Clients SMTP (authentifiés)</p></td>
<td><p>587/TCP (SMTP authentifié)</p></td>
<td><p>Le connecteur de réception par défaut, nommé « Client Frontend <em>&lt;Nom du serveur&gt;</em> » écoute les envois de client SMTP authentifiés sur le port 587 du serveur d’accès au client.</p>
<p><strong>Remarque :</strong></p>
<p>Si vous avez des clients de messagerie pouvant envoyer des courriers SMTP authentifiés uniquement sur le port 25, vous pouvez modifier la valeur de liaisons de carte réseau de ce connecteur de réception afin qu’il écoute également les envois de courriers SMTP authentifiés sur le port 25.</p></td>
</tr>
</tbody>
</table>


Retour au début

## Ports réseau requis pour le flux de messagerie

La remise des messages vers et depuis votre organisation Exchange dépend de votre topologie Exchange. Le facteur le plus important repose sur le fait que vous disposiez ou non d’un serveur de transport Edge abonné déployé sur votre réseau de périmètre.

## Ports réseau requis pour le flux de messagerie (aucun serveur de transport Edge)

Les ports réseau nécessaires pour les flux de messagerie dans une organisation Exchange disposant seulement de serveurs d’accès au client et de serveurs de boîtes aux lettres sont décrits dans le schéma et le tableau ci-après. Bien que le schéma représente des serveurs d’accès au client et de boîtes aux lettres distincts, les concepts sont les mêmes, que le serveur d’accès au client et le serveur de boîtes aux lettres soient installés sur le même ordinateur ou sur des ordinateurs différents.

![Ports réseau requis pour le flux de messagerie (aucun serveur de transport Edge)](images/Bb331973.af54dfd3-fe6b-4b6e-bb8e-b00df94a0be0(EXCHG.150).png "Ports réseau requis pour le flux de messagerie (aucun serveur de transport Edge)")


<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>Objectif</th>
<th>Ports</th>
<th>Source</th>
<th>Destination</th>
<th>Commentaires</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Courrier entrant</p></td>
<td><p>25/TCP (SMTP)</p></td>
<td><p>Internet (tout)</p></td>
<td><p>Serveur d’accès au client</p></td>
<td><p>Le connecteur de réception par défaut, nommé « Default Frontend &lt;<em>&lt;Client Access server name&gt;</em> » sur le serveur d’accès au client, écoute les messages SMTP entrants anonymes sur le port 25.</p>
<p>Le courrier est relayé du serveur d’accès au client à un serveur de boîte aux lettres via le connecteur d’envoi implicite et invisible interne à l’organisation qui achemine automatiquement les messages entre les serveurs Exchange de la même organisation.</p></td>
</tr>
<tr class="even">
<td><p>Courrier sortant</p></td>
<td><p>25/TCP (SMTP)</p></td>
<td><p>Serveur de boîtes aux lettres</p></td>
<td><p>Internet (tout)</p></td>
<td><p>Par défaut, Exchange ne crée pas de connecteurs d’envoi qui vous permettent d’envoyer des messages à Internet. Vous devez créer des connecteurs d’envoi manuellement. Pour plus d’informations, voir <a href="send-connectors-exchange-2013-help.md">Connecteurs d'envoi</a>.</p></td>
</tr>
<tr class="odd">
<td><p>Courrier sortant (si acheminé par le biais du serveur d’accès au client)</p></td>
<td><p>25/TCP (SMTP)</p></td>
<td><p>Serveur d’accès au client</p></td>
<td><p>Internet (tout)</p></td>
<td><p>Le courrier sortant est acheminé via un serveur d’accès au client uniquement lorsqu’un connecteur d’envoi est configuré avec <strong>Proxy via serveur d’accès au client</strong> dans le Centre d’administration Exchange ou <code>-FrontEndProxyEnabled $true</code> dans l’Environnement de ligne de commande Exchange Management Shell.</p>
<p>Dans ce cas, le connecteur de réception par défaut, nommé « Outbound Proxy Frontend <em>&lt;Nom du serveur d’accès au client&gt;</em> » sur le serveur d’accès au client, écoute le courrier sortant en provenant du serveur de boîtes aux lettres. Pour plus d’informations, voir <a href="create-a-send-connector-for-email-sent-to-the-internet-exchange-2013-help.md">Créer un connecteur d’envoi pour les messages électroniques envoyés vers Internet</a>.</p></td>
</tr>
<tr class="even">
<td><p>DNS pour la résolution du nom de tronçon de courrier suivant (non illustré)</p></td>
<td><p>53/UDP, 53/TCP (DNS)</p></td>
<td><p>Serveur Exchange Internet (serveur d’accès client ou serveur de boîte aux lettres)</p></td>
<td><p>Serveur DNS</p></td>
<td><p>Voir la section Résolution de noms.</p></td>
</tr>
</tbody>
</table>


Retour au début

## Ports réseau requis pour le flux de messagerie avec des serveurs de transport Edge

Un serveur de transport Edge abonné qui est installé sur votre réseau de périmètre élimine généralement le flux de messagerie SMTP par le biais du serveur d’accès au client. Notamment :

  - Le courrier sortant en provenance de l’organisation Exchange ne transite jamais par un serveur d’accès au client. Les messages proviennent toujours d’un serveur de boîtes aux lettres sur le site Active Directory abonné vers le serveur de transport Edge (quelle que soit la version d’Exchange sur le serveur de transport Edge).

  - Le courrier entrant ne transite jamais par un serveur d’accès au client autonome. Les messages proviennent toujours du serveur de transport Edge vers un serveur de boîtes aux lettres sur le site Active Directory abonné. Si le serveur de boîtes aux lettres et le serveur d’accès au client sont installés sur le même ordinateur, les messages provenant d’un serveur de transport Edge Exchange 2013 arrivent d’abord sur l’ordinateur du service de transport frontal (rôle du serveur d’accès au client) avant de transiter vers le service de transport (rôle du serveur de boîtes aux lettres). Les serveurs de transport Edge Exchange 2007 ou Exchange 2010 remettent toujours les messages directement au service de transport, même lorsque le serveur de boîtes aux lettres et le serveur d’accès au client sont installés sur le même ordinateur.

Pour plus d'informations, consultez la rubrique [Flux de messagerie](mail-flow-exchange-2013-help.md).

Les ports réseau nécessaires pour les flux de messagerie dans les organisations Exchange disposant de serveurs de transport Edge sont décrits dans le schéma et le tableau ci-après. Sauf mention contraire, les concepts sont les mêmes, que le serveur d’accès au client et le serveur de boîtes aux lettres soient installés sur le même ordinateur ou sur des ordinateurs différents.

![Ports réseau requis pour le flux de messagerie avec des serveurs de transport Edge](images/Bb331973.110c79b3-dbd9-4cb5-bba1-02048363ee1c(EXCHG.150).png "Ports réseau requis pour le flux de messagerie avec des serveurs de transport Edge")


<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>Objectif</th>
<th>Ports</th>
<th>Source</th>
<th>Destination</th>
<th>Commentaires</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Courrier entrant - Internet vers serveur de transport Edge</p></td>
<td><p>25/TCP (SMTP)</p></td>
<td><p>Internet (tout)</p></td>
<td><p>Serveur de transport Edge</p></td>
<td><p>Le connecteur de réception par défaut, nommé « Default internal Receive connector <em>&lt;Nom du serveur de transport Edge&gt;</em> » sur le serveur de transport Edge, écoute les messages SMTP anonymes sur le port 25.</p></td>
</tr>
<tr class="even">
<td><p>Courrier entrant - serveur de transport Edge vers organisation Exchange interne</p></td>
<td><p>25/TCP (SMTP)</p></td>
<td><p>Serveur de transport Edge</p></td>
<td><p>Serveurs de boîtes aux lettres dans le site Active Directory abonné</p></td>
<td><p>Le connecteur d’envoi par défaut nommé « EdgeSync - Entrant vers <em>&lt;Nom de site Active Directory&gt;</em> » relaie le courrier entrant sur le port 25 vers un serveur de boîtes aux lettres dans le site Active Directory abonné. Pour plus d’informations, consultez la section « Connecteurs d’envoi créés au cours du processus d’abonnement Edge » dans la rubrique <a href="edge-subscriptions-exchange-2013-help.md">Abonnements Edge</a>.</p>
<p>Le service qui reçoit réellement les messages dépend du fait que le serveur de boîtes aux lettres et le serveur d’accès au client soient installés sur le même ordinateur ou sur des ordinateurs différents.</p>
<ul>
<li><p><strong>Serveur de boîtes aux lettres autonomes</strong>   Le connecteur de réception par défaut, nommé « Default <em>&lt;Nom du serveur de boîtes aux lettres&gt;</em> », écoute le courrier entrant (y compris les messages provenant de serveurs de transport Edge) sur le port 25.</p></li>
<li><p><strong>Serveur de boîtes aux lettres et serveur d’accès au client installés sur le même ordinateur</strong>   Le connecteur de réception par défaut nommé « Default Frontend <em>&lt;Nom du serveur&gt;</em> » dans le service de transport frontal (le rôle de serveur d’accès au client) écoute le courrier entrant (y compris les messages provenant de serveurs de transport Edge Exchange 2013) sur le port 25.</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Courrier sortant - organisation Exchange interne vers serveur de transport Edge</p></td>
<td><p>25/TCP (SMTP)</p></td>
<td><p>Serveurs de boîtes aux lettres dans le site Active Directory abonné</p></td>
<td><p>Serveurs de transport Edge</p></td>
<td><p>Le courrier sortant contourne toujours le serveur d’accès au client.</p>
<p>Le courrier est relayé d’un serveur de boîtes aux lettres du site Active Directory abonné vers un serveur de transport Edge à l’aide du connecteur d’envoi implicite et invisible interne à l’organisation qui achemine automatiquement les messages entre les serveurs Exchange dans la même organisation.</p>
<p>Le connecteur de réception par défaut nommé « Connecteur de réception interne par défaut <em>&lt;Nom du serveur de transport Edge&gt;</em> » sur le serveur de transport Edge écoute le courrier SMTP sur le port 25 à partir d’un serveur de boîtes aux lettres dans le site Active Directory abonné.</p></td>
</tr>
<tr class="even">
<td><p>Courrier sortant - Serveur de transport Edge vers Internet</p></td>
<td><p>25/TCP (SMTP)</p></td>
<td><p>Serveur de transport Edge</p></td>
<td><p>Internet (tout)</p></td>
<td><p>Le connecteur d’envoi par défaut, nommé « EdgeSync - <em>&lt;Nom du site Active Directory&gt;</em> to Internet », relaie le courrier sortant sur le port 25 depuis le serveur de transport Edge vers Internet.</p></td>
</tr>
<tr class="odd">
<td><p>Synchronisation EdgeSync</p></td>
<td><p>50636/TCP (LDAP sécurisé)</p></td>
<td><p>Serveurs de boîtes aux lettres du site Active Directory abonné dans la synchronisation EdgeSync</p></td>
<td><p>Serveurs de transport Edge</p></td>
<td><p>Lorsque le serveur de transport Edge est abonné au site Active Directory, tous les serveurs de boîtes aux lettres qui existent dans le site à ce moment-là participent à la synchronisation EdgeSync. Toutefois, tous les serveurs de boîtes aux lettres ajoutés ultérieurement ne participent pas automatiquement à la synchronisation EdgeSync.</p></td>
</tr>
<tr class="even">
<td><p>DNS pour la résolution du nom de tronçon de courrier suivant (non illustré)</p></td>
<td><p>53/UDP, 53/TCP (DNS)</p></td>
<td><p>Serveur de transport Edge</p></td>
<td><p>Serveur DNS</p></td>
<td><p>Voir la section Résolution de noms.</p></td>
</tr>
<tr class="odd">
<td><p>Définition du serveur proxy pour la réputation de l’expéditeur (non illustré)</p></td>
<td><p>Défini par l’utilisateur</p></td>
<td><p>Serveurs de transport Edge</p></td>
<td><p>Internet</p></td>
<td><p>La réputation de l’expéditeur (agent d’analyse de protocole) analyse les chemins du courrier entrant afin de limiter le courrier indésirable. Si votre organisation utilise un serveur proxy pour contrôler l’accès à Internet, vous devez définir les détails concernant le serveur proxy pour que la réputation de l’expéditeur puisse fonctionner correctement (notamment, la détection des proxies ouverts et le blocage des expéditeurs). Vous utilisez les paramètres <em>ProxyServerName</em>, <em>ProxyServerPort</em> et <em>ProxyServerType</em> sur la cmdlet <strong>Set-SenderReputationConfig</strong> pour définir le serveur proxy de votre organisation afin que la réputation de l’expéditeur puisse se connecter à Internet. Pour plus d’informations, voir <a href="manage-sender-reputation-exchange-2013-help.md">Gérer la réputation de l’expéditeur</a>.</p></td>
</tr>
</tbody>
</table>


Retour au début

## Résolution de noms

La résolution DNS du prochain tronçon de courrier est une partie essentielle du flux de messagerie dans les organisations Exchange. Les serveurs Exchange chargés de recevoir les courriers entrants ou de remettre les courriers sortants doivent être en mesure de résoudre les noms d’hôtes internes et externes pour un routage de messagerie correct. Tous les serveurs Exchange internes doivent également pouvoir résoudre les noms d’hôtes internes pour un routage de messagerie correct. Il existe différentes façons de concevoir une infrastructure DNS, mais le principal objectif consiste à garantir que la résolution de nom pour le tronçon suivant fonctionne correctement sur l’ensemble de vos serveurs Exchange.

## Ports réseau requis pour les déploiements hybrides

Les ports réseau nécessaires pour une organisation qui utilise à la fois Exchange 2013 et MicrosoftOffice 365 sont traités à la section « Ports, points de terminaison et protocoles de déploiement hybride » de la rubrique [Configuration requise pour un déploiement hybride](https://technet.microsoft.com/fr-fr/library/hh534377\(v=exchg.150\)).

## Ports réseau requis pour la messagerie unifiée

Les ports réseau nécessaires pour la messagerie unifiée sont traités dans les rubriques suivantes :

  - [Protocoles, ports et services de messagerie unifiée](um-protocols-ports-and-services-exchange-2013-help.md)

  - [Exchange Server 2013 SP1 Architecture Poster](https://go.microsoft.com/fwlink/p/?linkid=518646)

Retour au début

