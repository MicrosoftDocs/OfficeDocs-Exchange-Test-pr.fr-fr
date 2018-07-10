---
title: 'Stratégie et conformité de messagerie: Exchange 2013 Help'
TOCTitle: Stratégie et conformité de messagerie
ms:assetid: 65f20a20-27a4-4f6e-9b27-f8705d65b8d9
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Aa998599(v=EXCHG.150)
ms:contentKeyID: 50478313
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Stratégie et conformité de messagerie

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2015-03-09_

La messagerie électronique est devenue un moyen de communication fiable et omniprésent pour les professionnels de l'information dans les organisations de toute taille. Magasins et boîtes aux lettres de messagerie sont devenus des référentiels de données précieuses. Il est important pour les organisations de reformuler des stratégies de messagerie qui dictent le bon usage de leurs systèmes de messagerie, fournissent aux utilisateurs des directives pour savoir comment agir face aux stratégies et, le cas échéant, fournissent des informations détaillées sur les types de communication pouvant être autorisés.

Les organisations peuvent également créer des stratégies afin de gérer le cycle de vie de la messagerie électronique, retenir des messages pendant le temps défini en fonction des exigences commerciales, juridiques et réglementaires, préserver les enregistrements des messages électroniques pour litige ou à des fins d'enquêtes et être préparé à rechercher et fournir les enregistrements de messages électroniques requis pour répondre aux demandes de la découverte électronique.

Toutes les informations sensibles, notamment la propriété intellectuelle, les secrets commerciaux, les plans d'affaires et les informations d'identification personnelle collectées ou traitées par votre organisation doivent également être protégées contre les fuites.

## Stratégie et conformité de la messagerie dans Exchange 2013

Le tableau suivant offre un aperçu des fonctionnalités de stratégie et de conformité de la messagerie dans Microsoft Exchange Server 2013 et contient des liens vers des rubriques capables de vous aider à en savoir plus et à gérer ces fonctionnalités.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Fonctionnalité</th>
<th>Description</th>
<th>Ressources</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Gestion des enregistrements de messagerie (MRM)</p></td>
<td><p>Afin d'être conformes aux réglementations applicables ou respecter les exigences juridiques et commerciales, les organisations incluent les stratégies de cycle de vie de la messagerie dans leur stratégie de messagerie. Les questions fréquemment posées auxquelles devraient répondre ces stratégies incluent les suivantes :</p>
<ul>
<li><p>Combien de temps les messages devraient-ils être conserver ?</p></li>
<li><p>Où les messages doivent-ils être conservés ?</p></li>
<li><p>Tous les messages doivent-ils être conservés pendant la même durée ?</p></li>
</ul>
<p>Exchange 2013 contient des fonctionnalités MRM qui vous permettent de mettre en œuvre les stratégies de cycle de vie de la messagerie électronique de votre organisation. MRM vous permet d'appliquer des paramètres de rétention uniformes à tous les messages, d'utiliser des stratégies de rétention personnalisées pour appliquer un paramètre de rétention de base pour la boîte aux lettres et de permettre, de manière facultative, aux utilisateurs de classer les messages afin qu'ils puissent être conservés pendant une durée spécifiée.</p></td>
<td><p><a href="messaging-records-management-exchange-2013-help.md">Gestion des enregistrements de messagerie</a></p></td>
</tr>
<tr class="even">
<td><p>Archivage local</p></td>
<td><p>L'<em>archivage sur place</em> vous permet de reprendre le contrôle sur les données de messagerie de votre organisation en supprimant le besoin de recourir aux fichiers (.pst) et autoriser les utilisateurs à stocker les messages dans une <em>boîte aux lettres d'archivage</em> accessible dans Outlook 2010 et version supérieure et Outlook Web App.</p></td>
<td><p><a href="in-place-archiving-in-exchange-2013-exchange-2013-help.md">Archivage inaltérable dans Exchange 2013</a></p></td>
</tr>
<tr class="odd">
<td><p>Blocage local</p></td>
<td><p>Lorsqu’une situation de litige est vraisemblablement à craindre, les organisations ont pour obligation de conserver les informations pertinentes qui sont stockées électroniquement (ESI), y compris la messagerie. Le blocage sur place vous permet de rechercher et de conserver les messages correspondant à des paramètres de requête. Les messages sont protégés contre la suppression, la modification et la falsification et peuvent être préservés indéfiniment ou pendant une période donnée.</p></td>
<td><p><a href="in-place-hold-and-litigation-hold-exchange-2013-help.md">Conservation inaltérable et conservation pour litige</a></p></td>
</tr>
<tr class="even">
<td><p>Découverte électronique locale</p></td>
<td><p>La découverte électronique sur place vous permet de rechercher des données de boîtes aux lettres dans votre organisation Exchange, de prévisualiser des résultats de recherche et de les copier dans une boîte aux lettres de découverte.</p></td>
<td><p><a href="in-place-ediscovery-exchange-2013-help.md">Découverte électronique locale</a></p></td>
</tr>
<tr class="odd">
<td><p>Journalisation</p></td>
<td><p>La journalisation peut aider votre organisation à répondre aux exigences réglementaires, légales et de conformité organisationnelle en enregistrant les communications électroniques échangées. Lors de la planification de la rétention et de la conformité de la messagerie, il est important de comprendre la journalisation, son intégration dans les stratégies de conformité de votre organisation et la sécurisation des messages journalisés à l’aide de Exchange 2013.</p></td>
<td><p><a href="journaling-exchange-2013-help.md">Journalisation</a></p></td>
</tr>
<tr class="even">
<td><p>Règles de transport</p></td>
<td><p>À l'aide des règles de transport, vous pouvez rechercher des conditions spécifiques pour des messages transitant par votre organisation puis prendre les mesures nécessaires en ce qui les concerne. Les règles de transport vous permettent d’appliquer des stratégies de messagerie aux messages électroniques, des messages sécurisés, de protéger les systèmes de messagerie et d’éviter les fuites d’informations.</p></td>
<td><p><a href="mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md">Règles de transport ou de flux de messagerie</a></p></td>
</tr>
<tr class="odd">
<td><p>Prévention des pertes de données (DLP)</p></td>
<td><p>Les fonctionnalités DLP vous aident à protéger vos données sensibles et informent les utilisateurs de vos stratégies et règlementations. DLP peut également vous permettre d'éviter aux utilisateur d'envoyer par erreur des informations sensibles à des personnes non autorisées. Lors de la configuration des stratégies DLP, vous pouvez identifier et protéger les données sensibles en analysant le contenu de votre système de messagerie, qui comprend de nombreux types de fichiers associés. Les modèles de stratégies DLP fournis dans Exchange 2013 sont fondés sur des normes règlementaires telles que les informations d'identification personnelle et les normes de sécurité des données industrielles des cartes de paiement (PCI-DSS). L'extensibilité de DLP permet d'inclure d'autres stratégies importantes pour votre organisation. De plus, la nouvelle fonctionnalité de conseils de stratégie vous permet d'informer les utilisateurs des violations de stratégies avant l'envoi des données sensibles.</p></td>
<td><p><a href="technical-overview-of-dlp-data-loss-prevention-in-exchange.md">Protection contre la perte de données</a></p></td>
</tr>
<tr class="even">
<td><p>Gestion des droits relatifs à l’information (IRM)</p></td>
<td><p>La gestion des droits relatifs à l'information (IRM) offre une protection persistante en ligne et hors ligne des messages électroniques et des pièces jointes au moye des services de gestion des droits Active Directory (AD RMS).</p></td>
<td><p><a href="information-rights-management-exchange-2013-help.md">Gestion des droits relatifs à l’information</a></p></td>
</tr>
<tr class="odd">
<td><p>S/MIME</p></td>
<td><p>Le protocole S/MIME permet aux utilisateurs disposant de boîtes aux lettres Office 365, d’Exchange 2013 et d’Exchange Online de protéger les informations sensibles en envoyant des messages électroniques signés et chiffrés au sein de leur organisation. Les administrateurs peuvent activer le protocole S/MIME pour les boîtes aux lettres Office 365 en synchronisant les certificats utilisateur entre Office 365 et leur serveur sur site, puis en configurant Outlook Online afin qu’il prenne en charge S/MIME.</p></td>
<td><p><a href="s-mime-for-message-signing-and-encryption-exchange-2013-help.md">S/MIME pour la signature et le chiffrement des messages</a></p></td>
</tr>
<tr class="even">
<td><p>Enregistrement d’audit dans les boîtes aux lettres</p></td>
<td><p>Les boîtes aux lettres étant susceptibles de renfermer des informations confidentielles, des informations ayant un impact significatif sur l’activité et des informations d’identification personnelle, il est important de connaître le nom des personnes qui se connectent aux boîtes aux lettres de votre organisation et les actions qui sont effectuées. Ceci est particulièrement important si les utilisateurs qui se connectent ne sont pas les propriétaires des boîtes aux lettres (nommés utilisateurs délégués). Grâce à l’enregistrement d’audit des boîtes aux lettres, vous pouvez enregistrer l’accès aux boîtes aux lettres par les propriétaires des boîtes aux lettres, les délégués (notamment les administrateurs disposant d’autorisations d'accès total aux boîtes aux lettres) et les administrateurs.</p></td>
<td><p><a href="mailbox-audit-logging-exchange-2013-help.md">Enregistrement d’audit dans les boîtes aux lettres</a></p>
<p><a href="exchange-auditing-reports-exchange-2013-help.md">Rapports d’audit Exchange</a></p></td>
</tr>
<tr class="odd">
<td><p>Connexion au service d’audit administrateur</p></td>
<td><p>Les journaux d’audit de l’administrateur vous permettent de conserver un journal des modifications apportées par les administrateurs à la configuration du serveur Exchange et de l’organisation et aux destinataires Exchange. Vous pouvez utiliser la journalisation d’audit de l’administrateur dans le cadre du processus de contrôle des modifications, ou pour effectuer un suivi des modifications et accéder à la configuration et aux destinataires à des fins de conformité.</p></td>
<td><p><a href="administrator-audit-logging-exchange-2013-help.md">Connexion au service d’audit administrateur</a></p></td>
</tr>
</tbody>
</table>

