---
title: 'Vue d’ensemble des services d’Exchange 2013: Exchange 2013 Help'
TOCTitle: Vue d’ensemble des services d’Exchange 2013
ms:assetid: 2ed45d18-2ff3-4099-b841-050eb16a416b
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Ee423542(v=EXCHG.150)
ms:contentKeyID: 74479255
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Vue d’ensemble des services d’Exchange 2013

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2017-10-20_

Lors de l’installation de Exchange Server 2013, le programme d’installation exécute un ensemble de tâches qui installent de nouveaux services dans Microsoft Windows. Un service est un processus en arrière-plan qui peut être lancé lors du démarrage du serveur par le Gestionnaire de contrôle des services Windows. Les services sont conçus pour fonctionner de façon indépendante et sans intervention de l’administrateur de fichiers exécutables. Un service peut s’exécuter à un mode de console ou un mode de graphical user interface (interface utilisateur).

Toutes les versions antérieures d’Exchange comprenaient des composants mis en œuvre comme des services. Chaque rôle serveur Exchange comprend des services qui font partie de son rôle (ou dont il peut avoir besoin) pour exercer ses fonctions. Certains services ne deviennent actifs que pendant l’utilisation de fonctions spécifiques.

Les sections de cette rubrique décrivent les différents services installés par Exchange 2013 sur les serveurs de boîtes aux lettres, les serveurs d’accès Client et les serveurs de Transport Edge. Pour les services qui sont indiqués comme étant facultatifs, vous pouvez désactiver le service si vous déterminez que votre organisation n’a pas besoin de la fonctionnalité fournie par le service.

## services de Exchange sur les serveurs de boîte aux lettres Exchange 2013

Le tableau suivant décrit les services Exchange qui sont installés sur des serveurs de boîtes aux lettres.


<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>Nom du service</th>
<th>Nom court du service</th>
<th>Description et dépendances</th>
<th>Type de démarrage par défaut</th>
<th>Contexte de sécurité</th>
<th>Dépendances</th>
<th>Obligatoire ou facultatif</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Microsoft Exchange Topologie Active Directory</p></td>
<td><p>MSExchangeADTopology</p></td>
<td><p>Fournit des informations de topologie Active Directory aux services Exchange. Si ce service est arrêté, la plupart des services Exchange ne peuvent pas démarrer.</p></td>
<td><p>Automatique</p></td>
<td><p>Système local</p></td>
<td><p>Service de partage de port Net.TCP</p></td>
<td><p>Requis</p></td>
</tr>
<tr class="even">
<td><p>Mise à jour de la fonction antispam d’Microsoft Exchange</p></td>
<td><p>MSExchangeAntispamUpdate</p></td>
<td><p>Fournit des mises à jour de définition de courrier indésirable SmartScreen Exchange.</p>
> [!NOTE]
> Le 1er novembre 2016, Microsoft a cessé de produire des mises à jour des définitions de courrier indésirable pour les filtres SmartScreen dans Exchange et Outlook. Les définitions de courrier indésirable SmartScreen existantes restent en place, mais leur efficacité se dégradera probablement au cours du temps. Pour plus d’informations, voir l’article relatif à l’<a href="https://go.microsoft.com/fwlink/p/?linkid=835894">arrêt de la prise en charge de SmartScreen dans Outlook et Exchange</a>.

</td>
<td><p>Automatique</p></td>
<td><p>Système local</p></td>
<td><p>Microsoft Exchange Active Directory Topologie</p></td>
<td><p>Facultatif</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft Exchange Gestion de groupe de disponibilité de base de données (DAG)</p></td>
<td><p>MSExchangeDagMgmt</p></td>
<td><p>Fournit la gestion de la disposition de la base de données et du stockage pour les serveurs de boîtes aux lettres dans les groupes de disponibilité de base de données (DAG).</p></td>
<td><p>Automatique</p></td>
<td><p>Système local</p></td>
<td><p>Microsoft Exchange Active Directory Topologie</p>
<p>Service de partage de port Net.TCP</p></td>
<td><p>Requis</p></td>
</tr>
<tr class="even">
<td><p>Microsoft Exchange Diagnostic</p></td>
<td><p>MSExchangeDiagnostics</p></td>
<td><p>Fournit un agent qui surveille l’intégrité du serveur Exchange.</p></td>
<td><p>Automatique</p></td>
<td><p>Système local</p></td>
<td><p>Aucun</p></td>
<td><p>Requis</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft Exchange EdgeSync</p></td>
<td><p>MSExchangeEdgeSync</p></td>
<td><p>Réplique les données de destinataire et de configuration entre le serveur de boîtes aux lettres et UNRESOLVED_TOKEN_VAL(exADLDS_1st) (AD LDS) sur les serveurs de transport Edge abonnés sur un canal LDAP sécurisé.</p>
<p>Si vous n’avez pas de serveur de transport Edge abonnés, vous pouvez désactiver ce service.</p></td>
<td><p>Automatique</p></td>
<td><p>Système local</p></td>
<td><p>Microsoft Exchange Active Directory Topologie</p></td>
<td><p>Facultatif</p></td>
</tr>
<tr class="even">
<td><p>Microsoft Exchange Gestionnaire d’intégrité</p></td>
<td><p>MSExchangeHM</p></td>
<td><p>Partie de la disponibilité gérée qui surveille l’intégrité des composants clés sur le serveur Exchange.</p></td>
<td><p>Automatique</p></td>
<td><p>Système local</p></td>
<td><p>Windows Journal des événements</p>
<p>Windows Infrastructure de gestion</p></td>
<td><p>Requis</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft Exchange IMAP4 principal</p></td>
<td><p>MSExchangeIMAP4BE</p></td>
<td><p>Reçoit les connexions utilisant un serveur proxy client à partir de du service IMAP4 sur les serveurs d’accès Client. Par défaut, ce service n’est pas en cours d’exécution, afin que les clients IMAP4 ne peut pas se connecter au serveur Exchange jusqu'à ce que ce service est démarré.</p>
<p>Si vous n’avez aucun client IMAP4, vous pouvez désactiver ce service.</p></td>
<td><p>Manuel</p></td>
<td><p>Service réseau</p></td>
<td><p>Microsoft Exchange Active Directory Topologie</p></td>
<td><p>Facultatif</p></td>
</tr>
<tr class="even">
<td><p>Banque d’informations Microsoft Exchange</p></td>
<td><p>MSExchangeIS</p></td>
<td><p>Gère les bases de données de boîtes aux lettres sur le serveur. Si ce service est arrêté, les bases de données de boîtes aux lettres sur le serveur ne sont pas disponibles.</p></td>
<td><p>Automatique</p></td>
<td><p>Système local</p></td>
<td><p>Microsoft Exchange Active Directory Topologie</p>
<p>Appel de procédure distante (RPC)</p>
<p>Serveur</p>
<p>Windows Journal des événements</p>
<p>Station de travail</p></td>
<td><p>Requis</p></td>
</tr>
<tr class="odd">
<td><p>Assistants de boîte aux lettres Microsoft Exchange</p></td>
<td><p>MSExchangeMailboxAssistants</p></td>
<td><p>Effectue le traitement en arrière-plan de boîtes aux lettres dans les bases de données de boîtes aux lettres sur le serveur.</p></td>
<td><p>Automatique</p></td>
<td><p>Système local</p></td>
<td><p>Microsoft Exchange Active Directory Topologie</p></td>
<td><p>Requis</p></td>
</tr>
<tr class="even">
<td><p>Microsoft Exchange Réplication de boîte aux lettres</p></td>
<td><p>MSExchangeMailboxReplication</p></td>
<td><p>Traite les déplacements de boîtes aux lettres et les demandes de déplacement.</p></td>
<td><p>Automatique</p></td>
<td><p>Système local</p></td>
<td><p>Microsoft Exchange Active Directory Topologie</p>
<p>Service de partage de port Net.TCP</p></td>
<td><p>Requis</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft Exchange Remise du transport de boîte aux lettres</p></td>
<td><p>MSExchangeDelivery</p></td>
<td><p>Reçoit des messages SMTP du service de transport Microsoft Exchange (sur les serveurs de boîtes aux lettres locaux ou distants) et les remet à une base de données de boîtes aux lettres locale à l’aide de RPC.</p></td>
<td><p>Automatique</p></td>
<td><p>Service réseau</p></td>
<td><p>Microsoft Exchange Active Directory Topologie</p></td>
<td><p>Requis</p></td>
</tr>
<tr class="even">
<td><p>Microsoft Exchange Dépôt de transport de boîtes aux lettres</p></td>
<td><p>MSExchangeSubmission</p></td>
<td><p>Reçoit des messages RPC d’une base de données de boîtes aux lettres locale et les envoie via SMTP au service de transport Microsoft Exchange (sur les serveurs de boîtes aux lettres locaux ou distants).</p></td>
<td><p>Automatique</p></td>
<td><p>Système local</p></td>
<td><p>Microsoft Exchange Active Directory Topologie</p></td>
<td><p>Requis</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft Exchange POP3 principal</p></td>
<td><p>MSExchangePOP3BE</p></td>
<td><p>Reçoit les connexions de proxy client du service POP3 sur les serveurs d’accès Client. Par défaut, ce service n’est pas en cours d’exécution, afin que les clients POP3 ne peut pas se connecter au serveur Exchange jusqu'à ce que ce service est démarré.</p></td>
<td><p>Manuel</p></td>
<td><p>Service réseau</p></td>
<td><p>Microsoft Exchange Active Directory Topologie</p></td>
<td><p>Facultatif</p></td>
</tr>
<tr class="even">
<td><p>Service de réplication Microsoft Exchange</p></td>
<td><p>MSExchangeRepl</p></td>
<td><p>Fournit la fonctionnalité de réplication aux bases de données de boîtes aux lettres dans un groupe de disponibilité de base de données (DAG).</p></td>
<td><p>Automatique</p></td>
<td><p>Système local</p></td>
<td><p>Microsoft Exchange Active Directory Topologie</p></td>
<td><p>Requis</p></td>
</tr>
<tr class="odd">
<td><p>Accès au client RPC Microsoft Exchange</p></td>
<td><p>MSExchangeRPC</p></td>
<td><p>Gère les connexions du client RPC pour Exchange.</p></td>
<td><p>Automatique</p></td>
<td><p>Service réseau</p></td>
<td><p>Microsoft Exchange Active Directory Topologie</p></td>
<td><p>Requis</p></td>
</tr>
<tr class="even">
<td><p>Microsoft Exchange Recherche</p></td>
<td><p>MSExchangeFastSearch</p></td>
<td><p>Fournit l’indexation du contenu des boîtes aux lettres, ce qui améliore les performances de recherche de contenu.</p></td>
<td><p>Automatique</p></td>
<td><p>Système local</p></td>
<td><p>Microsoft Exchange Active Directory Topologie</p></td>
<td><p>Requis</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft Exchange Contrôleur d’hôte de recherche</p></td>
<td><p>HostControllerService</p></td>
<td><p>Fournit des services de déploiement et de gestion pour des applications sur le serveur Exchange local.</p></td>
<td><p>Automatique</p></td>
<td><p>Système local</p></td>
<td><p>Service HTTP</p></td>
<td><p>Obligatoire</p></td>
</tr>
<tr class="even">
<td><p>Microsoft Exchange Extension de serveur pour la Sauvegarde Windows Server</p></td>
<td><p>WSBExchange</p></td>
<td><p>Permet à la sauvegarde Windows Server de sauvegarder et restaurer les données du serveur Exchange.</p></td>
<td><p>Manuel</p></td>
<td><p>Système local</p></td>
<td><p>Aucun</p></td>
<td><p>Facultatif</p></td>
</tr>
<tr class="odd">
<td><p>Hôte de service Microsoft Exchange</p></td>
<td><p>MSExchangeServiceHost</p></td>
<td><p>Fournit un hôte de service pour les composants Exchange qui n’ont pas leurs propres services.</p></td>
<td><p>Automatique</p></td>
<td><p>Système local</p></td>
<td><p>Microsoft Exchange Active Directory Topologie</p></td>
<td><p>Requis</p></td>
</tr>
<tr class="even">
<td><p>Limitation de bande passante Microsoft Exchange</p></td>
<td><p>MSExchangeThrottling</p></td>
<td><p>Fournit la gestion de la charge de travail de l’utilisateur qui limite la vitesse des opérations des utilisateurs (anciennement connu sous le nom de limitation d’utilisateurs).</p></td>
<td><p>Automatique</p></td>
<td><p>Service réseau</p></td>
<td><p>Microsoft Exchange Active Directory Topologie</p></td>
<td><p>Requis</p></td>
</tr>
<tr class="odd">
<td><p>Transport Microsoft Exchange</p></td>
<td><p>MSExchangeTransport</p></td>
<td><p>Fournit le serveur SMTP et la pile de transport.</p></td>
<td><p>Automatique</p></td>
<td><p>Service réseau</p></td>
<td><p>Microsoft Exchange Active Directory Topologie</p>
<p>Microsoft Service de gestion du filtrage</p></td>
<td><p>Requis</p></td>
</tr>
<tr class="even">
<td><p>Recherche de journal de transport Microsoft Exchange</p></td>
<td><p>MSExchangeTransportLogSearch</p></td>
<td><p>Offre des fonctionnalités de recherche à distance dans les fichiers journaux de transport (suivi des messages, par exemple).</p></td>
<td><p>Automatique</p></td>
<td><p>Système local</p></td>
<td><p>Microsoft Exchange Active Directory Topologie</p></td>
<td><p>Facultatif</p></td>
</tr>
<tr class="odd">
<td><p>Messagerie unifiée Microsoft Exchange</p></td>
<td><p>MSExchangeUM</p></td>
<td><p>Offre des fonctionnalités de messagerie unifiée : permet de stocker les messages vocaux et les télécopies dans Exchange, et offre aux utilisateurs un accès téléphonique au courrier électronique, à la messagerie vocale, au calendrier, aux contacts ou un standard automatique. Si ce service est arrêté, la messagerie unifiée n’est pas disponible.</p>
<p>Si vous n’utilisez pas la messagerie unifiée, vous pouvez désactiver ce service.</p></td>
<td><p>Automatique</p></td>
<td><p>Système local</p></td>
<td><p>Isolation de clé CNG</p>
<p>Microsoft Exchange Active Directory Topologie</p></td>
<td><p>Facultatif</p></td>
</tr>
</tbody>
</table>


## services de Exchange sur les serveurs d’accès Client Exchange 2013

Le tableau suivant décrit les services Exchange sont installés sur les serveurs d’accès Client.


<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>Nom du service</th>
<th>Nom court du service</th>
<th>Description et dépendances</th>
<th>Type de démarrage par défaut</th>
<th>Contexte de sécurité</th>
<th>Dépendances</th>
<th>Obligatoire ou facultatif</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Microsoft Exchange Topologie Active Directory</p></td>
<td><p>MSExchangeADTopology</p></td>
<td><p>Fournit des informations de topologie Active Directory aux services Exchange. Si ce service est arrêté, la plupart des services Exchange ne peuvent pas démarrer.</p></td>
<td><p>Automatique</p></td>
<td><p>Système local</p></td>
<td><p>Service de partage de port Net.TCP</p></td>
<td><p>Requis</p></td>
</tr>
<tr class="even">
<td><p>Microsoft Exchange Diagnostic</p></td>
<td><p>MSExchangeDiagnostics</p></td>
<td><p>Fournit un agent qui surveille l’intégrité du serveur Exchange.</p></td>
<td><p>Automatique</p></td>
<td><p>Système local</p></td>
<td><p>Aucun</p></td>
<td><p>Requis</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft Exchange Transport frontal</p></td>
<td><p>MSExchangeFrontEndTransport</p></td>
<td><p>Connexions de proxy SMTP des hôtes externes pour le service de Transport sur les serveurs de boîte aux lettres Microsoft Exchange.</p></td>
<td><p>Automatique</p></td>
<td><p>Système local</p></td>
<td><p>Microsoft Exchange Active Directory Topologie</p></td>
<td><p>Requis</p></td>
</tr>
<tr class="even">
<td><p>Microsoft Exchange Gestionnaire d’intégrité</p></td>
<td><p>MSExchangeHM</p></td>
<td><p>Partie de la disponibilité gérée qui surveille l’intégrité des composants clés sur le serveur Exchange.</p></td>
<td><p>Automatique</p></td>
<td><p>Système local</p></td>
<td><p>Windows Journal des événements</p>
<p>Windows Infrastructure de gestion</p></td>
<td><p>Requis</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft Exchange IMAP4</p></td>
<td><p>MSExchangeIMAP4</p></td>
<td><p>Serveurs proxy IMAP4 de connexions client au service IMAP4 sur les serveurs de boîtes aux lettres. Par défaut, ce service n’est pas en cours d’exécution, afin que les clients IMAP4 ne peut pas se connecter au serveur Exchange jusqu'à ce que ce service est démarré.</p>
<p>Si vous n’avez aucun client IMAP4, vous pouvez désactiver ce service.</p></td>
<td><p>Manuel</p></td>
<td><p>Système local</p></td>
<td><p>Microsoft Exchange Active Directory Topologie</p></td>
<td><p>Facultatif</p></td>
</tr>
<tr class="even">
<td><p>Microsoft Exchange POP3</p></td>
<td><p>MSExchangePOP3</p></td>
<td><p>Proxy POP3 de connexions client au service IMAP4 sur les serveurs de boîtes aux lettres. Par défaut, ce service n’est pas en cours d’exécution, afin que les clients POP3 ne peut pas se connecter au serveur Exchange jusqu'à ce que ce service est démarré.</p></td>
<td><p>Manuel</p></td>
<td><p>Service réseau</p></td>
<td><p>Microsoft Exchange Active Directory Topologie</p></td>
<td><p>Facultatif</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft Exchange Contrôleur d’hôte de recherche</p></td>
<td><p>HostControllerService</p></td>
<td><p>Fournit des services de déploiement et de gestion pour des applications sur le serveur Exchange local.</p></td>
<td><p>Automatique</p></td>
<td><p>Système local</p></td>
<td><p>Service HTTP</p></td>
<td><p>Requis</p></td>
</tr>
<tr class="even">
<td><p>Hôte de service Microsoft Exchange</p></td>
<td><p>MSExchangeServiceHost</p></td>
<td><p>Fournit un hôte de service pour les composants Exchange qui n’ont pas leurs propres services.</p></td>
<td><p>Automatique</p></td>
<td><p>Système local</p></td>
<td><p>Microsoft Exchange Active Directory Topologie</p></td>
<td><p>Requis</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft Exchange Routeur d’appels de messagerie unifiée</p></td>
<td><p>MSExchangeUMCR</p></td>
<td><p>Redirige les connexions de client de messagerie unifiée vers le service de messagerie unifiée sur les serveurs de boîtes aux lettres.</p>
<p>Si vous n’utilisez pas la messagerie unifiée, vous pouvez désactiver ce service.</p></td>
<td><p>Automatique</p></td>
<td><p>Système local</p></td>
<td><p>Isolation de clé CNG</p>
<p>Microsoft Exchange Active Directory Topologie</p></td>
<td><p>Facultatif</p></td>
</tr>
</tbody>
</table>


## services de Exchange sur les serveurs de Transport Edge Exchange 2013

Le tableau suivant décrit les services Exchange qui sont installés sur des serveurs de transport Edge.


<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>Nom du service</th>
<th>Nom court du service</th>
<th>Description</th>
<th>Type de démarrage par défaut</th>
<th>Contexte de sécurité</th>
<th>Dépendances</th>
<th>Obligatoire ou facultatif</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Microsoft Exchange ADAM</p></td>
<td><p>ADAM_MSExchange</p></td>
<td><p>Stocke les données de configuration et les données de destinataire sur le serveur de transport Edge. Ce service représente l’instance nommée de UNRESOLVED_TOKEN_VAL(exADLDS_1st) (AD LDS), qui est automatiquement créé par le programme d’installation Exchange.</p></td>
<td><p>Automatique</p></td>
<td><p>Service réseau</p></td>
<td><p>Système d’événements COM +</p></td>
<td><p>Requis</p></td>
</tr>
<tr class="even">
<td><p>Mise à jour de la fonction antispam d’Microsoft Exchange</p></td>
<td><p>MSExchangeAntispamUpdate</p></td>
<td><p>Fournit des mises à jour de définition de courrier indésirable SmartScreen Exchange.</p>
> [!NOTE]
> Le 1er novembre 2016, Microsoft a cessé de produire des mises à jour des définitions de courrier indésirable pour les filtres SmartScreen dans Exchange et Outlook. Les définitions de courrier indésirable SmartScreen existantes restent en place, mais leur efficacité se dégradera probablement au cours du temps. Pour plus d’informations, voir l’article relatif à l’<a href="https://go.microsoft.com/fwlink/p/?linkid=835894">arrêt de la prise en charge de SmartScreen dans Outlook et Exchange</a>.

</td>
<td><p>Automatique</p></td>
<td><p>Système local</p></td>
<td><p>Microsoft Exchange ADAM</p></td>
<td><p>Facultatif</p></td>
</tr>
<tr class="odd">
<td><p>Service d’identification Microsoft Exchange</p></td>
<td><p>MSExchangeEdgeCredential</p></td>
<td><p>Contrôle les changements d’informations d’identification dans UNRESOLVED_TOKEN_VAL(exADLDS_1st) (AD LDS) et installe les changements sur le serveur de transport Edge.</p></td>
<td><p>Automatique</p></td>
<td><p>Système local</p></td>
<td><p>Microsoft Exchange ADAM</p></td>
<td><p>Requis</p></td>
</tr>
<tr class="even">
<td><p>Microsoft Exchange Diagnostic</p></td>
<td><p>MSExchangeDiagnostics</p></td>
<td><p>Fournit un agent qui surveille l’intégrité du serveur Exchange.</p></td>
<td><p>Automatique</p></td>
<td><p>Système local</p></td>
<td><p>Aucun</p></td>
<td><p>Requis</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft Exchange Gestionnaire d’intégrité</p></td>
<td><p>MSExchangeHM</p></td>
<td><p>Partie de la disponibilité gérée qui surveille l’intégrité des composants clés sur le serveur Exchange.</p></td>
<td><p>Automatique</p></td>
<td><p>Système local</p></td>
<td><p>Journal des événements Windows</p>
<p>Windows Management Instrumentation</p></td>
<td><p>Requis</p></td>
</tr>
<tr class="even">
<td><p>Hôte de service Microsoft Exchange</p></td>
<td><p>MSExchangeServiceHost</p></td>
<td><p>Fournit un hôte de service pour les composants Exchange qui n’ont pas leurs propres services.</p></td>
<td><p>Automatique</p></td>
<td><p>Système local</p></td>
<td><p>Microsoft Exchange ADAM</p></td>
<td><p>Requis</p></td>
</tr>
<tr class="odd">
<td><p>Transport Microsoft Exchange</p></td>
<td><p>MSExchangeTransport</p></td>
<td><p>Fournit le serveur SMTP et la pile de transport.</p></td>
<td><p>Automatique</p></td>
<td><p>Service réseau</p></td>
<td><p>Microsoft Exchange ADAM</p></td>
<td><p>Requis</p></td>
</tr>
<tr class="even">
<td><p>Recherche de journal de transport Microsoft Exchange</p></td>
<td><p>MSExchangeTransportLogSearch</p></td>
<td><p>Offre des fonctionnalités de recherche à distance dans les fichiers journaux de transport (suivi des messages, par exemple).</p></td>
<td><p>Automatique</p></td>
<td><p>Système local</p></td>
<td><p>Microsoft Exchange ADAM</p></td>
<td><p>Facultatif</p></td>
</tr>
</tbody>
</table>

