---
title: 'Fonctionnalités abandonnées dans Exchange 2013: Exchange 2013 Help'
TOCTitle: Fonctionnalités abandonnées dans Exchange 2013
ms:assetid: 0ac0001c-b314-4108-b895-d9c0e271b489
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ619283(v=EXCHG.150)
ms:contentKeyID: 50477484
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Fonctionnalités abandonnées dans Exchange 2013

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2016-12-09_

Cette rubrique traite des composants, fonctions ou fonctionnalités supprimés, abandonnés ou remplacés dans Microsoft Exchange Server 2013.

> [!NOTE]  
> Les rubriques suivantes peuvent également vous intéresser :
> <ul>
> <li><p><a href="what-s-new-in-exchange-2013-exchange-2013-help.md">Nouveautés d'Exchange 2013</a>   Informations sur les nouvelles fonctions et fonctionnalités dans Exchange Server 2013.</p></li>
> <li><p><a href="https://go.microsoft.com/fwlink/p/?linkid=267479">Feuille de route concernant les technologies de développement pour Exchange 2013</a>    Consultez la section « Technologies de développement supprimées d'Exchange » pour obtenir des informations sur l'API et les fonctionnalités de développement qui ont été abandonnées dans Exchange 2013.</p></li></ul>

## Fonctionnalités Exchange 2010 abandonnées dans Exchange 2013

Cette section répertorie les fonctionnalités Exchange Server 2010 qui ne sont plus disponibles dans Exchange 2013.

## Architecture


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Fonctionnalité</th>
<th>Commentaires et atténuation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Rôle serveur de transport Hub</p></td>
<td><p>Le rôle serveur de transport Hub a été remplacé par des services de transport exécutés sur les rôles serveur de boîtes aux lettres et d’accès au client. Le rôle serveur de boîtes aux lettres comprend le service de transport Microsoft Exchange, le service de remise du transport de boîte aux lettres Microsoft Exchange et le dépôt de transport de boîtes aux lettres Microsoft Exchange. Le rôle de serveur d’accès au client comprend le service de transport frontal Microsoft Exchange. Pour plus d'informations, consultez la rubrique <a href="mail-flow-exchange-2013-help.md">Flux de messagerie</a>.</p></td>
</tr>
<tr class="even">
<td><p>Rôle serveur de messagerie unifiée</p></td>
<td><p>Le rôle serveur de messagerie unifiée a été remplacé par les services de messagerie unifiée exécutés sur les rôles serveur de boîtes aux lettres et d’accès au client. Le rôle serveur de boîtes aux lettres comprend le service de messagerie unifiée Microsoft Exchange et le rôle serveur d’accès au client comprend le service routeur des appels de messagerie unifiée Microsoft Exchange. Pour plus d'informations, consultez la rubrique <a href="voice-architecture-changes-exchange-2013-help.md">Modifications de l’architecture vocale</a>.</p></td>
</tr>
</tbody>
</table>


## Interfaces de gestion


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Fonctionnalité</th>
<th>Commentaires et atténuation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Console de gestion Exchange et Panneau de configuration Exchange</p></td>
<td><p>Le Centre d’administration Exchange (CAE) remplace la console de gestion Exchange et le Panneau de configuration Exchange. Le CAE utilise le même répertoire virtuel (/ecp) que le Panneau de configuration Exchange. Pour plus d'informations, consultez la rubrique <a href="exchange-admin-center-in-exchange-2013-exchange-2013-help.md">Centre d’administration Exchange dans Exchange 2013</a>.</p></td>
</tr>
</tbody>
</table>


## Accès client


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Fonctionnalité</th>
<th>Commentaires et atténuation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Outlook 2003 n’est pas pris en charge.</p></td>
<td><p>Pour connecter Microsoft Outlook à Exchange 2013, vous devez utiliser le service de découverte automatique. Toutefois, Microsoft Outlook 2003 ne prend pas en charge l’utilisation du service de découverte automatique.</p></td>
</tr>
<tr class="even">
<td><p>Accès RPC/TCP pour les clients Outlook</p></td>
<td><p>Dans Exchange 2013, les clients Microsoft Outlook peuvent se connecter à l’aide d’Outlook Anywhere (RPC/HTTP) ou MAPI sur HTTP dans Exchange 2013 Service Pack 1 et Outlook 2013 Service Pack 1 et versions ultérieures. Si vous avez des clients Outlook dans votre organisation, l’utilisation d’Outlook Anywhere et/ou de MAPI sur HTTP est requise. Pour plus d’informations, consultez les rubriques <a href="outlook-anywhere-exchange-2013-help.md">Outlook Anywhere</a> et <a href="mapi-over-http-exchange-2013-help.md">MAPI sur HTTP</a>.</p></td>
</tr>
</tbody>
</table>


## Outlook Web App et Outlook


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Fonctionnalité</th>
<th>Commentaires et atténuation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Vérification de l'orthographe</p></td>
<td><p>Outlook Web App ne comporte plus de services de vérification orthographique intégrés. À la place, les fonctionnalités de vérification de l’orthographe de vos navigateurs web sont utilisées.</p></td>
</tr>
<tr class="even">
<td><p>Filtres personnalisables</p></td>
<td><p>Outlook Web App ne propose plus d'affichages filtrés personnalisables et ne prend plus en charge l'enregistrement des affichages filtrés dans les Favoris. Les filtres personnalisables ont été remplacés par des filtres fixes permettant d'afficher tous les messages, les messages non lus, les messages envoyés à l'utilisateur ou les messages marqués.</p></td>
</tr>
<tr class="odd">
<td><p>Indicateurs de message</p></td>
<td><p>La fonctionnalité de définition d’une date personnalisée sur un indicateur de message n’est pas disponible dans Outlook Web App. Vous pouvez utiliser Outlook pour définir des dates personnalisées.</p></td>
</tr>
<tr class="even">
<td><p>Liste des contacts de conversation</p>
<p></p></td>
<td><p>La liste de contacts de conversation qui s’affiche dans la liste des dossiers dans Outlook Web App pour Exchange 2010 n’est plus disponible.</p></td>
</tr>
<tr class="odd">
<td><p>Dossiers de recherche</p></td>
<td><p>La possibilité pour les utilisateurs de se servir des dossiers de recherche n’est pas disponible actuellement dans Outlook Web App.</p></td>
</tr>
</tbody>
</table>


## Flux de messagerie


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Fonctionnalité</th>
<th>Commentaires et atténuation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Connecteurs liés</p></td>
<td><p>Il n'est plus possible de lier un connecteur d'envoi à un connecteur de réception. Plus particulièrement, le paramètre <em>LinkedReceiveConnector</em> a été supprimé de <a href="https://technet.microsoft.com/fr-fr/library/aa998936(v=exchg.150)">New-SendConnector</a> et <a href="https://technet.microsoft.com/fr-fr/library/aa998294(v=exchg.150)">Set-SendConnector</a>.</p></td>
</tr>
</tbody>
</table>


## Protection contre le courrier indésirable et les logiciels malveillants


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Fonctionnalité</th>
<th>Commentaires et atténuation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Gestion de l'agent anti-spam dans la console de gestion Exchange</p></td>
<td><p>Dans Exchange 2010, quand vous activiez les agents anti-spam sur le serveur de transport Hub, vous pouviez les gérer dans la console de gestion Exchange. Dans Exchange 2013, lorsque vous activez les agents anti-spam sur un serveur de boîtes aux lettres, vous ne pouvez pas gérer ces agents à l’aide du CAE. Vous pouvez uniquement utiliser l’environnement de ligne de commande Exchange Management Shell. Pour plus d'informations sur la façon d'activer les agents anti-spam sur un serveur de boîtes aux lettres, consultez la rubrique <a href="enable-anti-spam-functionality-on-mailbox-servers-exchange-2013-help.md">Activer la fonctionnalité de blocage du courrier indésirable sur un serveur de boîtes aux lettres</a>.</p></td>
</tr>
<tr class="even">
<td><p>Agent de filtrage de connexions sur les serveurs de transport Hub</p></td>
<td><p>Dans Exchange 2010, quand vous activiez les agents anti-spam sur un serveur de transport Hub, l'agent de filtrage des pièces jointes était le seul agent anti-spam qui n'était pas disponible. Dans Exchange 2013, quand vous activez les agents anti-spam sur un serveur de boîtes aux lettres, les agents de filtrage des pièces jointes et de filtrage des connexions ne sont pas disponibles. L'agent de filtrage des connexions intègre les fonctionnalités Liste d'adresses IP autorisées et Liste d'adresses IP bloquées. Pour plus d'informations sur la façon d'activer les agents anti-spam sur un serveur de boîtes aux lettres, consultez la rubrique <a href="enable-anti-spam-functionality-on-mailbox-servers-exchange-2013-help.md">Activer la fonctionnalité de blocage du courrier indésirable sur un serveur de boîtes aux lettres</a>.</p>

> [!NOTE]  
> Il n'est pas possible d'activer les agents anti-spam sur un serveur d'accès au client Exchange 2013. Par conséquent, le seul moyen d’obtenir un agent de filtrage des connexions consiste à installer un serveur de transport Edge dans le réseau de périmètre. Pour plus d’informations, voir <a href="edge-transport-servers-exchange-2013-help.md">Serveurs de transport Edge</a>.

</td>
</tr>
</tbody>
</table>


## Stratégie et conformité de messagerie


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Fonctionnalité</th>
<th>Commentaires et atténuation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Dossiers gérés</p></td>
<td><p>Dans Exchange 2010, vous utilisez des dossiers gérés pour assurer la gestion de la rétention de messagerie (MRM). Dans Exchange 2013, les dossiers gérés ne sont pas pris en charge. Vous devez utiliser des stratégies de rétention pour MRM.</p>

> [!NOTE]  
> Les cmdlets associés à des dossiers gérés sont toujours disponibles. Vous pouvez créer des dossiers gérés, des paramètres de contenu géré et des stratégies de boîte aux lettres de dossier géré, et appliquer une telle stratégie à un utilisateur. Toutefois, l’assistant MRM ignore le traitement des boîtes aux lettres qui ont une stratégie de boîte aux lettres de dossier géré.

</td>
</tr>
<tr class="even">
<td><p>Assistant Port du dossier géré</p></td>
<td><p>Dans Exchange 2010, vous utilisez l'Assistant Port du dossier géré pour créer des balises de rétention en fonction des paramètres de dossier géré et de contenu géré. Dans Exchange 2013, le Centre d’administration Exchange n’inclut pas cette fonctionnalité. Vous pouvez utiliser la cmdlet <strong>New-RetentionPolicyTag</strong> avec le paramètre <em>ManagedFolderToUpgrade</em> pour créer une balise de rétention basée sur un dossier géré.</p></td>
</tr>
</tbody>
</table>


## Messagerie unifiée et messagerie vocale


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Fonctionnalité</th>
<th>Commentaires et atténuation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Recherches d'annuaire à l'aide de la reconnaissance vocale automatique (ASR)</p></td>
<td><p>Dans Exchange 2010, grâce à la reconnaissance vocale (ASR), les utilisateurs d’Outlook Voice Access peuvent dicter le nom des utilisateurs à rechercher dans l’annuaire. La saisie vocale permet également de parcourir les menus, les messages et d’autres options dans Outlook Voice Access. Cependant, même si l’utilisateur d’Outlook Voice Access peut recourir à la saisie vocale, il a besoin du clavier du téléphone pour entrer son code confidentiel et explorer des options personnelles.</p>
<p>Dans Exchange 2013, les utilisateurs authentifiés et non authentifiés d’Outlook Voice Access ne peuvent pas effectuer des recherches dans l’annuaire à l’aide de la saisie vocale (ASR) quelle que soit la langue. Toutefois, les appelants qui passent par un standard automatique peuvent utiliser la saisie vocale dans plusieurs langues pour parcourir les menus du standard et rechercher des utilisateurs dans l’annuaire.</p></td>
</tr>
</tbody>
</table>


## Outils


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Fonctionnalité</th>
<th>Commentaires et atténuation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Exchange Best Practices Analyzer</p></td>
<td><p>Dans Exchange 2010, Exchange Best Practice Analyzer analysait votre déploiement Exchange pour déterminer si la configuration était conforme aux meilleures pratiques de Microsoft. Dans Exchange 2013, Exchange Best Practice Analyzer a été remplacé par <a href="https://go.microsoft.com/fwlink/p/?linkid=391077">Office 365 Best Practices Analyzer pour Exchange Server 2013</a>.</p></td>
</tr>
<tr class="even">
<td><p>Utilitaire de résolution des problèmes de flux de messagerie</p></td>
<td><p>Dans Exchange 2010, l'utilitaire de résolution des problèmes de flux de messagerie vous aidait à résoudre les problèmes courants liés au flux de messagerie. Dans Exchange 2013, cet utilitaire a été supprimé. Vous pouvez maintenant utiliser la fonctionnalité de suivi des messages du Centre d'administration Exchange dans Exchange 2013. Pour plus d'informations, consultez la rubrique <a href="track-messages-with-delivery-reports-exchange-2013-help.md">Suivre les messages avec des rapports de remise</a>.</p></td>
</tr>
<tr class="odd">
<td><p>Analyseur de performances</p></td>
<td><p>Dans Exchange 2010, l'Analyseur de performances figurait dans la boîte à outils Exchange pour vous permettre de collecter des informations sur les performances de votre système de messagerie. L'Analyseur de performances est généralement utilisé pour afficher des paramètres clés lors du dépannage de problèmes de performances. Dans Exchange 2013, l'Analyseur de performances a été supprimé de la boîte à outils. L'Analyseur de performances se trouve toujours sous <strong>Outils d'administration</strong> dans Windows Server 2008.</p></td>
</tr>
<tr class="even">
<td><p>Utilitaire de dépannage des performances</p></td>
<td><p>Dans Exchange 2013, l’utilitaire de dépannage des performances a été supprimé.</p></td>
</tr>
<tr class="odd">
<td><p>Visionneuse du journal de routage</p></td>
<td><p>Dans Exchange 2013, la visionneuse du journal de routage a été supprimée.</p></td>
</tr>
</tbody>
</table>


## Copies de bases de données de boîtes aux lettres


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Fonctionnalité</th>
<th>Commentaires et atténuation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><ul>
<li><p>Update-MailboxDatabaseCopy</p></li>
<li><p>Mise à jour de l’Assistant Copie de base de données de boîte aux lettres</p></li>
</ul></td>
<td><p>L’amorçage de catalogue d’index de contenu n’est plus possible par le biais du réseau de réplication et peut uniquement être réalisé via un réseau MAPI. Cela est avéré même lorsque vous utilisez le paramètre <code>-Network</code> dans la cmdlet Update-MailboxDatabaseCopy.</p></td>
</tr>
</tbody>
</table>


## Fonctionnalités Exchange 2007 abandonnées dans Exchange 2013

Cette section répertorie les fonctionnalités Exchange Server 2007 qui ne sont plus disponibles dans Exchange 2013.

## API et développement


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Fonctionnalité</th>
<th>Commentaires et atténuation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Exchange WebDAV</p></td>
<td><p>Utilisez les <a href="https://go.microsoft.com/fwlink/p/?linkid=167197">services web Exchange</a> ou l'<a href="https://go.microsoft.com/fwlink/p/?linkid=157179">API managée des services web Exchange</a>. Autrement, vous pouvez conserver un serveur Exchange 2007 pour les boîtes aux lettres qui sont gérées par des applications utilisant WebDAV. Pour plus d'informations, consultez la rubrique <a href="https://go.microsoft.com/fwlink/p/?linkid=169474">Migration à partir de WebDAV</a>.</p></td>
</tr>
</tbody>
</table>


## Architecture


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Fonctionnalité</th>
<th>Commentaires et atténuation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Groupes de stockage</p></td>
<td><p>Exchange 2013 n’utilise plus la construction de groupes de stockage, vous gérez maintenant simplement les bases de données de boîtes aux lettres. Pour plus d’informations, voir <a href="manage-mailbox-databases-in-exchange-2013-exchange-2013-help.md">Gestion des bases de données de boîtes aux lettres dans Exchange 2013</a>.</p></td>
</tr>
<tr class="even">
<td><p>API de sauvegarde en continu ESE (Extensible Storage Engine)</p></td>
<td><p>Exchange 2013 prend en charge uniquement les sauvegardes VSS (service de cliché instantané des volumes) compatibles Exchange. Exchange 2013 comprend un plug-in pour la Sauvegarde Windows Server, qui vous permet de sauvegarder et de restaurer les données. Pour plus d’informations, consultez la rubrique <a href="backup-restore-and-disaster-recovery-exchange-2013-help.md">Sauvegarde, restauration et récupération d’urgence</a>.</p></td>
</tr>
<tr class="odd">
<td><p>Notifications du Protocole UDP (User Datagram Protocol)</p></td>
<td><p>La prise en charge des notifications du protocole UDP est supprimée dans Exchange 2013. L'expérience utilisateur en est affectée quand les clients Outlook 2003 se connectent à leurs boîtes aux lettres sur un serveur Exchange 2013. Pour en savoir plus, consultez l'article 2009942 de la Base de connaissances de Microsoft <a href="http://go.microsoft.com/fwlink/?linkid=3052&kbid=2009942">La mise à jour des dossiers est longue lorsqu'un utilisateur Exchange Server 2010 utilise Outlook 2003 en mode en ligne</a>.</p></td>
</tr>
</tbody>
</table>


## Disponibilité élevée


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Fonctionnalité</th>
<th>Commentaires et atténuation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Réplication continue en cluster (CCR)</p></td>
<td><p>Exchange 2013 utilise les groupes de disponibilité de base de données (DAG) et les copies de bases de données de boîtes aux lettres. Pour plus d'informations, consultez la rubrique <a href="high-availability-and-site-resilience-exchange-2013-help.md">Haute disponibilité et résilience de site</a>.</p></td>
</tr>
<tr class="even">
<td><p>Réplication continue locale (LCR)</p></td>
<td><p>Exchange 2013 utilise les DAG et les copies de bases de données de boîtes aux lettres. Pour plus d'informations, consultez la rubrique <a href="high-availability-and-site-resilience-exchange-2013-help.md">Haute disponibilité et résilience de site</a>.</p></td>
</tr>
<tr class="odd">
<td><p>Réplication continue de secours (Standby continuous replication - SCR)</p></td>
<td><p>Exchange 2013 utilise les DAG et les copies de bases de données de boîtes aux lettres. Pour plus d'informations, consultez la rubrique <a href="high-availability-and-site-resilience-exchange-2013-help.md">Haute disponibilité et résilience de site</a>.</p></td>
</tr>
<tr class="even">
<td><p>Cluster à copie unique (SCC)</p></td>
<td><p>Exchange 2013 utilise les DAG et les copies de bases de données de boîtes aux lettres. Pour plus d'informations, consultez la rubrique <a href="high-availability-and-site-resilience-exchange-2013-help.md">Haute disponibilité et résilience de site</a>.</p></td>
</tr>
<tr class="odd">
<td><p>Setup /recoverCMS</p></td>
<td><p>Exchange 2013 utilise Setup /m:RecoverServer. Pour plus d’informations, consultez la rubrique <a href="recover-an-exchange-server-exchange-2013-help.md">Récupérer un serveur Exchange</a>.</p></td>
</tr>
<tr class="even">
<td><p>Serveurs de boîtes aux lettres en cluster</p></td>
<td><p>Exchange 2013 utilise les DAG et les copies de bases de données de boîtes aux lettres. Pour plus d'informations, consultez la rubrique <a href="high-availability-and-site-resilience-exchange-2013-help.md">Haute disponibilité et résilience de site</a>.</p></td>
</tr>
</tbody>
</table>


## Accès client


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Fonctionnalité</th>
<th>Commentaires et atténuation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Authentification du client à l'aide de l'authentification intégrée Windows (NTLM) pour les utilisateurs POP3 et IMAP4</p></td>
<td><p>NTLM n'est pas pris en charge pour la connectivité client POP3 ou IMAP4 dans Exchange 2013. Les connexions de programmes clients POP3 ou IMAP4 utilisant NTLM échoueront. Si vous utilisez la version RTM pour Exchange 2013, l’alternative à NTLM recommandée consiste à utiliser l’authentification en texte brut avec SSL.</p>
<p>Si vous utilisez Exchange 2013, pour employer NTLM, vous devez conserver un serveur Exchange 2007 dans votre organisation Exchange 2013.</p></td>
</tr>
</tbody>
</table>


## Outlook Web App et Outlook


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Fonctionnalité</th>
<th>Commentaires et atténuation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Accès au document</p></td>
<td><p>Vous ne pouvez pas utiliser Outlook Web App pour accéder aux bibliothèques de documents Microsoft SharePoint et aux partages de fichiers Windows.</p></td>
</tr>
<tr class="even">
<td><p>Indicateurs de message</p></td>
<td><p>Il n’est pas possible de définir une date personnalisée sur un indicateur de message dans Outlook Web App 2013. Vous pouvez utiliser Outlook pour définir des dates personnalisées.</p></td>
</tr>
<tr class="odd">
<td><p>Vérification de l'orthographe</p></td>
<td><p>Outlook Web App utilise les fonctions de vérification de l’orthographe dans votre navigateur web.</p></td>
</tr>
<tr class="even">
<td><p>Dossiers de recherche</p></td>
<td><p>La possibilité pour les utilisateurs de se servir des dossiers de recherche n’est pas disponible actuellement dans Outlook Web App.</p></td>
</tr>
<tr class="odd">
<td><p>Nombre maximal de vues mises en cache</p></td>
<td><p>Exchange 2007 prenait en charge la modification du nombre maximal de vues mises en cache par le biais du paramètre de base de données (msExchMaxCachedViews) pour les clients Outlook. Exchange 2013 n’utilise plus ce paramètre.</p></td>
</tr>
</tbody>
</table>


## Fonctionnalités liées au destinataire


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Fonctionnalité</th>
<th>Commentaires et atténuation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Cmdlets <strong>Export-Mailbox</strong> et <strong>Import-Mailbox</strong></p></td>
<td><p>Dans Exchange 2013, utilisez les demandes d'importation ou d'exportation. Pour plus d'informations, consultez la rubrique <a href="mailbox-import-and-export-requests-exchange-2013-help.md">Demandes d’exportation et d’importation de boîtes aux lettres</a>.</p></td>
</tr>
<tr class="even">
<td><p>Cmdlet <strong>Move-Mailbox</strong></p></td>
<td><p>Dans Exchange 2013, utilisez les demandes de déplacement pour déplacer des boîtes aux lettres. Pour plus d'informations, consultez la rubrique <a href="mailbox-moves-in-exchange-2013-exchange-2013-help.md">Déplacements de boîtes aux lettres dans Exchange 2013</a>.</p></td>
</tr>
<tr class="odd">
<td><p>ISInteg</p></td>
<td><p>Dans Exchange 2013, utilisez <a href="https://technet.microsoft.com/fr-fr/library/ff625226(v=exchg.150)">New-MailboxRepairRequest</a>.</p></td>
</tr>
</tbody>
</table>


## Stratégie et conformité de messagerie


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Fonctionnalité</th>
<th>Commentaires et atténuation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Dossiers gérés</p></td>
<td><p>Dans Exchange 2007, vous utilisez des dossiers gérés pour assurer la gestion de la rétention de messagerie (MRM). Dans Exchange 2013, les dossiers gérés ne sont pas pris en charge. Vous devez utiliser des stratégies de rétention pour MRM.</p>

> [!NOTE]  
> Les cmdlets associés à des dossiers gérés sont toujours disponibles. Vous pouvez créer des dossiers gérés, des paramètres de contenu géré et des stratégies de boîte aux lettres de dossier géré, et appliquer une telle stratégie à un utilisateur. Toutefois, l’assistant MRM ignore le traitement des boîtes aux lettres qui ont une stratégie de boîte aux lettres de dossier géré.

</td>
</tr>
</tbody>
</table>


## Messagerie unifiée et messagerie vocale


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Fonctionnalité</th>
<th>Commentaires et atténuation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Recherches dans l’annuaire à l’aide de la reconnaissance vocale (ASR) pour Outlook Voice Access</p></td>
<td><p>Dans Exchange 2010, grâce à la reconnaissance vocale (ASR) disponible en anglais américain (en-US), les utilisateurs d’Outlook Voice Access peuvent dicter le nom des utilisateurs à rechercher dans l’annuaire. La saisie vocale permet également de parcourir les menus, les messages et d’autres options dans Outlook Voice Access. Cependant, même si l’utilisateur d’Outlook Voice Access peut recourir à la saisie vocale, il a besoin du clavier du téléphone pour entrer son code confidentiel et explorer des options personnelles.</p>
<p>Dans Exchange 2013, les utilisateurs authentifiés et non authentifiés d’Outlook Voice Access ne peuvent pas effectuer des recherches dans l’annuaire à l’aide de la saisie vocale (ASR) quelle que soit la langue. Toutefois, les appelants qui passent par un standard automatique peuvent utiliser la saisie vocale dans plusieurs langues pour parcourir les menus du standard et rechercher des utilisateurs dans l’annuaire.</p></td>
</tr>
</tbody>
</table>

