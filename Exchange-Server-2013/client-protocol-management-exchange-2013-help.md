---
title: 'Gestion du protocole client: Exchange 2013 Help'
TOCTitle: Gestion du protocole client
ms:assetid: 89ba6d24-d1d3-46d5-a0ae-61f0d4c6df21
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ657727(v=EXCHG.150)
ms:contentKeyID: 50478636
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Gestion du protocole client

 

_**Sapplique à :**Exchange Server 2013_

_**Dernière rubrique modifiée :**2015-03-09_

La gestion des protocoles client de Microsoft Exchange ActiveSync, Microsoft Outlook Web App, POP3, IMAP4, du service de découverte automatique, des services Web Exchange et du service de disponibilité s’opère dans trois secteurs différents : le Centre d’administration Exchange (EAC), l’environnement de ligne de commande Exchange Management Shell et le gestionnaire Microsoft Internet Information Services (IIS). Les paramètres gérés dans chacun des emplacements varient selon le protocole client.

## Paramètres de gestion de Microsoft Outlook Web App

La plupart des paramètres qui affectent des fonctionnalités de Microsoft Outlook Web App sont accessibles aux utilisateurs et peuvent être définis dans le répertoire virtuel de Microsoft Outlook Web App ou configurés dans une stratégie de boîte aux lettres Microsoft Outlook Web App. Les stratégies de boîte aux lettres Microsoft Outlook Web App vous permettent de définir les fonctionnalités accessibles aux utilisateurs individuels. Les paramètres de stratégie de boîte aux lettres se substituent aux paramètres du répertoire virtuel. Pour plus d’informations sur la gestion de Microsoft Outlook Web App, consultez la rubrique [Outlook Web App](outlook-web-app-exchange-2013-help.md).

## Paramètres de gestion de Microsoft Exchange ActiveSync

Avec Exchange 2010, tous les protocoles d’accès au client étaient mis en oeuvre et gérés sur un même rôle serveur, le rôle serveur d’accès au client. La gestion des protocoles s’effectuait sur une instance unique d’IIS, il y avait un répertoire virtuel unique dans Active Directory pour chaque protocole de client et un jeu unique de cmdlets était utilisé pour configurer le répertoire virtuel.

Avec Exchange 2013, la gestion du protocole client pour Microsoft Exchange ActiveSync se réparti entre le serveur d’accès au client et le serveur de boîte aux lettres. Ce changement d’architecture vous permet d’exécuter différentes tâches de gestion de répertoires virtuels sur le serveur d’accès au client et sur le serveur de boîtes aux lettres. Si ces deux serveurs ne sont pas installés sur le même ordinateur physique, les paramètres que vous utilisez avec les cmdlets du répertoire virtuel doivent changer selon le rôle serveur utilisé pour l'exécution.

Pour plus d’informations sur les changements d’architecture dans Exchange 2013, consultez la rubrique [Nouveautés d'Exchange 2013](what-s-new-in-exchange-2013-exchange-2013-help.md).

Deux types de paramètres peuvent s’appliquer au répertoire virtuel de Microsoft Exchange ActiveSync :

  - Paramètres applicables à la session de boîte aux lettres

  - Paramètres applicables au serveur et au répertoire virtuel

Les paramètres qui s'appliquent à la session de boîte aux lettres sont des paramètres de session utilisateur. Lorsqu’un utilisateur se connecte à un serveur d’accès au client, la connexion est redirigée via un proxy sur le serveur de boîtes aux lettres qui contient la boîte aux lettres de l’utilisateur. Un identificateur unique de répertoire virtuel est inclus avec la demande redirigée via un proxy. Le serveur de boîtes aux lettres extrait ensuite les paramètres du répertoire virtuel dans Active Directory et les applique à la session. Les paramètres du répertoire virtuel sont mis en cache sur le serveur de boîtes aux lettres pour améliorer les performances.

S’il s'agit d’une connexion redirigée via un proxy vers un site Active Directory différent, les paramètres de répertoire virtuel doivent être chargés à partir du serveur d’accès au client sur le même site sur celui du serveur de boîtes aux lettres et non à partir du serveur d’accès au client à l’origine de la connexion.

Les tableaux suivants indiquent les paramètres de répertoire virtuel qui peuvent être gérés sur tel ou tel serveur. Si vous tentez de gérer un paramètre particulier sur un serveur pour lequel cela n’est pas applicable, un message d’erreur vous avertit que la propriété que vous tentez de définir est en lecture seule pour le serveur sur lequel vous opérez.

**Paramètres de répertoire virtuel de Microsoft Exchange ActiveSync sur les serveurs d’accès au client**


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Paramètre</th>
<th>Serveur</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>le paramètre</p></td>
<td><p>Accès client</p></td>
</tr>
<tr class="even">
<td><p>BasicAuthEnabled</p></td>
<td><p>Accès client</p></td>
</tr>
<tr class="odd">
<td><p>ClientCertAuth</p></td>
<td><p>Accès client</p></td>
</tr>
<tr class="even">
<td><p>CompressionEnabled</p></td>
<td><p>Accès client</p></td>
</tr>
<tr class="odd">
<td><p>ExternalAuthenticationMethods</p></td>
<td><p>Accès client</p></td>
</tr>
<tr class="even">
<td><p>ExternalURL</p></td>
<td><p>Accès client</p></td>
</tr>
<tr class="odd">
<td><p>InternalAuthenticationMethods</p></td>
<td><p>Accès client</p></td>
</tr>
<tr class="even">
<td><p>InternalURL</p></td>
<td><p>Accès client</p></td>
</tr>
<tr class="odd">
<td><p>MobileClientCertificateAuthorityURL</p></td>
<td><p>Accès client</p></td>
</tr>
<tr class="even">
<td><p>MobileClientCertificateProvisioningEnabled</p></td>
<td><p>Accès client</p></td>
</tr>
<tr class="odd">
<td><p>MobileClientCertTemplateName</p></td>
<td><p>Accès client</p></td>
</tr>
<tr class="even">
<td><p>RemoteDocumentsActionForUnknownServers</p></td>
<td><p>Accès client</p></td>
</tr>
<tr class="odd">
<td><p>RemoteDocumentsAllowedServers</p></td>
<td><p>Accès client</p></td>
</tr>
<tr class="even">
<td><p>RemoteDocumentsBlockedServers</p></td>
<td><p>Accès client</p></td>
</tr>
<tr class="odd">
<td><p>RemoteDocumentsInternalDomainSuffixList</p></td>
<td><p>Accès client</p></td>
</tr>
<tr class="even">
<td><p>SendWatsonReport</p></td>
<td><p>Accès client</p></td>
</tr>
</tbody>
</table>


**Paramètres de répertoire virtuel de Microsoft Exchange ActiveSync sur les serveurs d’accès au client et de boîtes aux lettres**


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Paramètre</th>
<th>Serveur</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>ApplicationRoot</p></td>
<td><p>Accès client et boîte aux lettres</p></td>
</tr>
<tr class="even">
<td><p>AppPoolID</p></td>
<td><p>Accès client et boîte aux lettres</p></td>
</tr>
<tr class="odd">
<td><p>MetabasePath</p></td>
<td><p>Accès client et boîte aux lettres</p></td>
</tr>
<tr class="even">
<td><p>Name</p></td>
<td><p>Accès client et boîte aux lettres</p></td>
</tr>
<tr class="odd">
<td><p>Path</p></td>
<td><p>Accès client et boîte aux lettres</p></td>
</tr>
<tr class="even">
<td><p>ProxySubVdir</p></td>
<td><p>Accès client et boîte aux lettres</p></td>
</tr>
<tr class="odd">
<td><p>VirtualDirectoryName</p></td>
<td><p>Accès client et boîte aux lettres</p></td>
</tr>
<tr class="even">
<td><p>WebsiteName</p></td>
<td><p>Accès client et boîte aux lettres</p></td>
</tr>
</tbody>
</table>


## Gestion des paramètres POP3 et IMAP4

Dans Exchange 2013, l’implémentation des protocoles POP3 et IMAP4 a également été segmentée entre les rôles serveur d’accès au client et de boîtes aux lettres. En raison de la nouvelle implémentation, la connectivité POP3 et IMAP4 sont tous les deux gérés par un service sur le serveur d’accès au client et également par un service sur le serveur de boîtes aux lettres. Les noms des services qui s’exécutent sur le serveur d’accès au client sont les mêmes que ceux qui existaient dans Exchange 2010 : Le service Microsoft Exchange IMAP4 et le service Microsoft Exchange POP3. Les noms des deux nouveaux services qui s’exécutent sur le serveur de boîtes aux lettres sont le service IMAP4 principal de Microsoft Exchange et le service POP3 principal Microsoft Exchange.

Prenez en compte les éléments suivants puisque vous gérez la connectivité POP3 et IMAP4 dans votre organisation :

  - Si vous exécutez le rôle serveur d’accès au client et le rôle serveur de boîte aux lettres sur le même ordinateur, toutes les modifications que vous apportez aux paramètres POP3 ou IMAP4 s’appliquent automatiquement aux services POP3 et IMAP4.

  - Si vous exécutez le rôle serveur d’accès au client et le rôle serveur de boîtes aux lettres sur des ordinateurs distincts, vous devez gérer les paramètres sur l’ordinateur qui gère les paramètres que vous souhaitez modifier.

Les tableaux suivants indiquent les paramètres POP/IMAP associés à chacun des rôles serveur.

**Paramètres POP3 et IMAP4 sur le serveur d’accès au client**


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Paramètre</th>
<th>Serveur</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>AuthenticatedConnectionTimeout</p></td>
<td><p>Accès client</p></td>
</tr>
<tr class="even">
<td><p>Banner</p></td>
<td><p>Accès client</p></td>
</tr>
<tr class="odd">
<td><p>ExternalConnectionSettings</p></td>
<td><p>Accès client</p></td>
</tr>
<tr class="even">
<td><p>InternalConnectionSettings</p></td>
<td><p>Accès client</p></td>
</tr>
<tr class="odd">
<td><p>MaxCommandSize</p></td>
<td><p>Accès client</p></td>
</tr>
<tr class="even">
<td><p>MaxConnectionFromSingleIP</p></td>
<td><p>Accès client</p></td>
</tr>
<tr class="odd">
<td><p>MaxConnections</p></td>
<td><p>Accès client</p></td>
</tr>
<tr class="even">
<td><p>MaxConnectionsPerUser</p></td>
<td><p>Accès client</p></td>
</tr>
<tr class="odd">
<td><p>PreAuthenticatedConnectionTimeout</p></td>
<td><p>Accès client</p></td>
</tr>
<tr class="even">
<td><p>UnencryptedOrTLSBindings</p></td>
<td><p>Accès client</p></td>
</tr>
</tbody>
</table>


**Paramètres POP3 et IMAP4 sur le serveur de boîtes aux lettres**


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Paramètre</th>
<th>Serveur</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>CalendarItemRetrivalOption</p></td>
<td><p>Boîte aux lettres</p></td>
</tr>
<tr class="even">
<td><p>EnableExactRFC822Size</p></td>
<td><p>Boîte aux lettres</p></td>
</tr>
<tr class="odd">
<td><p>MessageRetrievalSortOrder</p></td>
<td><p>Boîte aux lettres</p></td>
</tr>
<tr class="even">
<td><p>OWAServerURL</p></td>
<td><p>Boîte aux lettres</p></td>
</tr>
<tr class="odd">
<td><p>ProxyTargetPort</p></td>
<td><p>Boîte aux lettres</p></td>
</tr>
<tr class="even">
<td><p>ShowHiddenFoldersEnabled</p></td>
<td><p>Boîte aux lettres</p></td>
</tr>
<tr class="odd">
<td><p>SuppressReadReceipt</p></td>
<td><p>Boîte aux lettres</p></td>
</tr>
</tbody>
</table>


**Paramètres POP3 et IMAP4 sur les serveurs d’accès au client et de boîtes aux lettres**


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Paramètre</th>
<th>Serveur</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>X509CertificateName</p></td>
<td><p>Accès client et boîte aux lettres</p></td>
</tr>
<tr class="even">
<td><p>EnforceCertificateErrors</p></td>
<td><p>Accès client et boîte aux lettres</p></td>
</tr>
<tr class="odd">
<td><p>LogFileLocation</p></td>
<td><p>Accès client et boîte aux lettres</p></td>
</tr>
<tr class="even">
<td><p>LogFileRolloverSettings</p></td>
<td><p>Accès client et boîte aux lettres</p></td>
</tr>
<tr class="odd">
<td><p>LoginType</p></td>
<td><p>Accès client et boîte aux lettres</p></td>
</tr>
<tr class="even">
<td><p>LogPerFileSizeQuota</p></td>
<td><p>Accès client et boîte aux lettres</p></td>
</tr>
<tr class="odd">
<td><p>ProotocolLogEnabled</p></td>
<td><p>Accès client et boîte aux lettres</p></td>
</tr>
<tr class="even">
<td><p>Server</p></td>
<td><p>Accès client et boîte aux lettres</p></td>
</tr>
<tr class="odd">
<td><p>X509CertificateName</p></td>
<td><p>Accès client et boîte aux lettres</p></td>
</tr>
</tbody>
</table>

