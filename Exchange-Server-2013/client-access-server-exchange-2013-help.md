---
title: 'Serveur d’accès au client: Exchange 2013 Help'
TOCTitle: Serveur d’accès au client
ms:assetid: 87e206ab-7a7b-4b4f-be1a-5035713c74d2
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dd298114(v=EXCHG.150)
ms:contentKeyID: 50478622
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Serveur d’accès au client

 

_**Sapplique à :**Exchange Server 2013_

_**Dernière rubrique modifiée :**2014-07-02_

Dans Microsoft Exchange 2013, nous avons apportées des modifications architecturales majeures aux rôles de serveur Exchange. À la place des cinq rôles serveur déjà présents dans Exchange 2010 et Exchange 2007, nous avons réduit à trois le nombre de rôles serveur dans Exchange 2013 : le serveur d’accès au client et le serveur de boîtes aux lettres, et avec le Service Pack 1, le rôle serveur de transport Edge.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Exchange 2013 peut également utiliser le rôle serveur de transport Edge Exchange 2010.</td>
</tr>
</tbody>
</table>


Le serveur de boîtes aux lettres Exchange 2013 comprend tous les composants de serveur déjà présents dans Exchange 2010 : les protocoles d’accès au client, les services de transport, les bases de données de boîtes aux lettres et les services de messagerie unifiée (le serveur d’accès au client redirige le trafic SIP généré par les appels entrants vers le serveur de boîtes aux lettres). Pour plus d’informations sur le serveur de boîtes aux lettres d’Exchange 2013, consultez la rubrique [Serveur de boîtes aux lettres](mailbox-server-exchange-2013-help.md).

Le serveur d’accès au client fournit des services d’authentification, de proxy et de redirection limitée, ainsi que tous les protocoles d’accès au client habituels : HTTP, POP, IMAP et SMTP. Le serveur d’accès au client, dynamique et sans état, n’effectue aucun rendu des données. Rien n’est conservé en file d'attente ni stocké sur le serveur d’accès au Client. Pour plus d’informations sur la nouvelle architecture d’Exchange 2013, consultez la rubrique [Nouveautés d'Exchange 2013](what-s-new-in-exchange-2013-exchange-2013-help.md).

<table>
<thead>
<tr class="header">
<th><img src="images/Bb125224.warning(EXCHG.150).gif" title="Avertissement" alt="Avertissement" />Avertissement :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Les serveurs d’accès au client ne sont pas pris en charge dans les réseaux de périmètre et ils doivent être déployés dans votre environnement Active Directory interne. Tous les sites Active Directory qui contiennent un serveur de boîtes aux lettres doivent également contenir un serveur d’accès au client.</td>
</tr>
</tbody>
</table>


Ainsi, pour ces modifications d'architecture, certaines modifications ont été exécutées sur la connectivité client. Tout d’abord, le protocole RPC/TCP n’est plus pris en charge pour l’accès direct. Cela signifie que toute la connectivité Outlook doit utiliser le protocole RPC sur HTTPS (également appelé Outlook Anywhere) ou bien, avec Exchange 2013 SP1 et Outlook 2013 SP1, le protocole MAPI sur HTTP. En conséquence de ces changements, il n’est pas nécessaire d’avoir le service d’accès au client RPC sur le serveur d’accès au client. En outre, deux espaces de noms plus petits sont requis pour une solution à résilience de site que ce qui était demandé avec Exchange 2010, et il n’est plus nécessaire de fournir une affinité pour le service d’accès au client RPC. En outre, les clients Outlook ne se connectent plus à un nom de domaine complet (FQDN) du serveur comme ils le faisaient dans les versions précédentes d’Exchange. La découverte automatique permet à Outlook de trouver de nouveaux points de connexion constitués du GUID de boîte aux lettres de l’utilisateur + @ + la partie de domaine de l’adresse SMTP principale de l’utilisateur. Cette modification réduit considérablement le risque pour les utilisateurs de voir apparaître le message tant redouté suivant : « Votre administrateur a apporté des modifications à votre boîte aux lettres. » Seuls Outlook 2007 et les versions ultérieures sont pris en charge avec Exchange 2013.

## Fonctionnalité du serveur d’accès au client

Le serveur d’accès au client d’Exchange 2013 fonctionne comme une porte d’entrée, il admet toutes des demandes des clients et les achemine vers la base de données de boîtes aux lettres active appropriée. Le serveur d’accès au client fournit des fonctionnalités de sécurité réseau comme SSL (Secure Sockets Layer) et l’authentification du client, et gère des connexions aux clients par le biais de fonctionnalités de redirection et proxy. Le serveur d’accès au client authentifie les connexions des clients et, dans la plupart des cas, redirige via un proxy une demande sur le serveur de boîte aux lettres qui héberge la copie active actuelle de la base de données qui contient la boîte aux lettres de l’utilisateur. Dans certains cas, le serveur d’accès au client redirige la demande vers un serveur d’accès au client plus approprié, sur un emplacement différent ou en exécutant une version plus récente d’Exchange Server.

Les fonctionnalités du serveur d’accès au client sont les suivantes :

  - **Serveur sans état** Dans les versions précédentes d’Exchange, de nombreux protocoles d'accès aux clients nécessitaient une affinité de session. Par exemple, Outlook Web App nécessite que toutes les demandes effectuées par un client particulier soient gérées par un serveur d’accès au client spécifique d’un groupe à charge équilibrée des serveurs d’accès au client. Dans Exchange 2013, le serveur d’accès au client est sans état. En d’autres termes, puisque l’intégralité du traitement pour la boîte aux lettres s’effectue sur le serveur de boîtes aux lettres, le fait qu’un serveur d’accès au client ou un autre d’un groupe de serveurs d’accès au client reçoive chaque demande de client individuel est sans importance. Cette modification dans la fonctionnalité signifie qu’il n’est plus nécessaire d’avoir une affinité de session au niveau de l’équilibrage de charge. Ceci autorise les connexions entrantes vers le serveur d’accès au client grâce à des techniques simples utilisant une technologie d’équilibrage de charge comme la répétition alternée DNS. Elle permet également à des périphériques d’équilibrage de charge matérielle de prendre en charge bien plus de connexions simultanées.

  - **Regroupement de connexions** Les serveurs d’accès au client gèrent une authentification du client et envoie les données AuthN au serveur de boîtes aux lettres. Le compte utilisé par les serveurs d’accès au client pour la connexion aux serveurs de boîtes aux lettres est un compte privilégié qui est membre du groupe de serveurs Exchange. Ainsi, les serveurs d’accès au client peuvent établir efficacement des connexions en pool vers des serveurs de boîtes aux lettres. Un groupe de serveurs d’accès au client peut gérer des millions de connexions aux clients à partir d’Internet, en revanche bien moins de connexions sont utilisées pour rediriger via un proxy des demandes vers des serveurs de boîtes aux lettres dans cette version d’Exchange que dans les précédentes. L’efficacité des traitements et la latence de bout en bout en sont améliorées.

## Tâches de gestion sur le serveur d’accès au client

Dans Exchange 2013, plusieurs tâches clé peuvent s’exécuter sur le serveur d’accès au client. La gestion des certificats numériques s’effectue principalement sur le serveur d’accès au client ainsi qu’une partie de la gestion de protocole client pour Exchange ActiveSync, POP3 et IMAP4.

